---
title: USBX DPUMP sınıfı değerlendirmeleri
description: USBX, konak ve cihaz tarafı için bir DPUMP sınıfı içerir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9960b391418fa2f9203e761115bcba71cc3619e8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828073"
---
# <a name="chapter-3-usbx-dpump-class-considerations"></a>Bölüm 3: USBX DPUMP sınıfı konuları

USBX, konak ve cihaz tarafı için bir DPUMP sınıfı içerir. Bu sınıf kendi kendine standart bir sınıf değildir, bunun yerine iki toplu kanal kullanarak basit bir cihaz oluşturmayı ve bu iki kanal üzerinde veri göndermeyi ve geriye doğru göndermeyi gösteren bir örnek. DPUMP sınıfı, özel bir sınıf veya eski RS232 cihazları başlatmak için kullanılabilir.

USB DPUMP akış grafiği:

![USB DPUMP akış grafiği](./media/usbx-host-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-host-class"></a>USBX DPUMP Host sınıfı

DPUMP sınıfının konak tarafında, biri veri göndermek için bir tane olmak üzere iki işlev vardır:

- `ux_host_class_dpump_write`
- `ux_host_class_dpump_read`

Her iki işlev de DPUMP uygulamasını daha kolay hale getirmek için engelleniyor. Aynı anda hem kanalların hem de aynı anda çalıştırılması gerekiyorsa, uygulamanın bir iletme iş parçacığı ve alma iş parçacığı oluşturması gerekir.

Yazma işlevinin prototipi aşağıdaki gibidir.

```C
UINT ux_host_class_dpump_write(UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,  
    ULONG *actual_length)
```

Konum:

- dpump, sınıfının örneğidir
- data_pointer gönderilecek arabelleğin işaretçisi
- requested_length, gönderileceği uzunluktadır
- actual_length, aktarımın tamamlanmasından sonra, başarıyla veya kısmen gönderilen uzunluktadır.

Alma işlevinin prototipi benzerdir.

```C
UINT ux_host_class_dpump_read(
    UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

Bir uygulamanın cihaz tarafına bir paket yazdığı ve alımda aynı paketi aldığı konak DPUMP sınıfına bir örnek aşağıda verilmiştir:

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

## <a name="usbx-dpump-device-class"></a>USBX DPUMP cihaz sınıfı

Device DPUMP sınıfı, USB konakla bağlantı kurulduğunda başlatılan bir iş parçacığı kullanır. İş parçacığı, toplu çıkış uç noktasında gelen bir paketi bekler. Paket alındığında, içeriği toplu uç nokta arabelleğine kopyalar ve bu uç noktada, konağın bu uç noktadan okuma isteği vermesini bekleyen bir işlem gönderir. Bu, toplu ve toplu uç noktalar arasında bir geri döngü mekanizması sağlar.
