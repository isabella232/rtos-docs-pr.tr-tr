---
title: USBX DPUMP Sınıf Konuları
description: USBX, konak ve cihaz tarafı için bir DPUMP sınıfı içerir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 72aa9c1e2200049bf81d64543b690edd001c4ecf9c2cdeb4c3bea5f1b03aa5b8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802591"
---
# <a name="chapter-3-usbx-dpump-class-considerations"></a>Bölüm 3: USBX DPUMP Sınıf Konuları

USBX, konak ve cihaz tarafı için bir DPUMP sınıfı içerir. Bu sınıf kendi içinde standart bir sınıf değildir, bunun yerine iki toplu kanallar kullanarak ve bu iki kanallar üzerinde ileri ve geri veri göndererek basit bir cihaz oluşturmayı gösteren bir örnektir. DPUMP sınıfı, özel bir sınıf başlatmak veya eski RS232 cihazları için kullanılabilir.

USB DPUMP akış grafiği:

![USB DPUMP akış grafiği](./media/usbx-host-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-host-class"></a>USBX DPUMP Konak Sınıfı

DPUMP Sınıfının ana bilgisayar tarafında biri veri göndermek, biri de veri almak için olmak için olmak için iki işlev vardır:

- `ux_host_class_dpump_write`
- `ux_host_class_dpump_read`

Her iki işlev de DPUMP uygulamasını daha kolay hale getirir. Her iki borunun da (IN ve OUT) aynı anda çalışıyor olması gerekiyorsa, uygulamanın bir iletme iş parçacığı ve bir alma iş parçacığı oluşturması gerekir.

Yazma işlevinin prototipi aşağıdaki gibidir.

```C
UINT ux_host_class_dpump_write(UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,  
    ULONG *actual_length)
```

Konum:

- dpump sınıfının örneğidir
- data_pointer, gönderilecek arabelleğin işaretçisi
- requested_length uzunluğu
- actual_length, aktarım tamamlandıktan sonra başarıyla veya kısmen gönderilen uzunluk olur.

Alıcı işlevin prototipi de benzerdir.

```C
UINT ux_host_class_dpump_read(
    UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

Bir uygulamanın cihaz tarafına paket yazdığı ve aynı paketi sinyalden aldığı konak DPUMP sınıfı örneği:

```C
/* We start with a 'A' in buffer. */
current_char = 'A';

while(1)
{
    /* Initialize the write buffer. */
    ux_utility_memory_set(out_buffer, current_char,
        UX_HOST_CLASS_DPUMP_PACKET_SIZE);

    /* Increment the character in buffer. */
    current_char++;

    /* Check for upper alphabet limit. */
    if (current_char > 'Z')
        current_char = 'A';

    /* Write to the Data Pump Bulk out endpoint. */
    status = ux_host_class_dpump_write (dpump, out_buffer,
        UX_HOST_CLASS_DPUMP_PACKET_SIZE,
        &actual_length);

    /* Verify that the status and the amount of data is correct. */
    if ((status == UX_SUCCESS) && actual_length == UX_HOST_CLASS_DPUMP_PACKET_SIZE)
    {
        /* Read to the Data Pump Bulk out endpoint. */
        status = ux_host_class_dpump_read (dpump, in_buffer,
            UX_HOST_CLASS_DPUMP_PACKET_SIZE, &actual_length);
    }
}
```

## <a name="usbx-dpump-device-class"></a>USBX DPUMP Cihaz Sınıfı

Cihaz DPUMP sınıfı, USB ana bilgisayarıyla bağlantıdan sonra başlatan bir iş parçacığı kullanır. İş parçacığı, Toplu Dışarı Uç Noktasına gelen bir paketi bekler. Bir paket alınca, içeriği Toplu Uç Nokta arabelleğine kopyalar ve bu uç noktada bir işlem gönderir ve ana bilgisayar tarafından bu uç noktadan okunacak bir istekte bulunduracak şekilde bekler. Bu, Toplu Dışarı ve Toplu Alma uç noktaları arasında bir geri döngü mekanizması sağlar.
