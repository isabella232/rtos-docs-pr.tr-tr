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
# <a name="chapter-3-usbx-dpump-class-considerations"></a><span data-ttu-id="55a5a-103">Bölüm 3: USBX DPUMP sınıfı konuları</span><span class="sxs-lookup"><span data-stu-id="55a5a-103">Chapter 3: USBX DPUMP Class Considerations</span></span>

<span data-ttu-id="55a5a-104">USBX, konak ve cihaz tarafı için bir DPUMP sınıfı içerir.</span><span class="sxs-lookup"><span data-stu-id="55a5a-104">USBX contains a DPUMP class for the host and device side.</span></span> <span data-ttu-id="55a5a-105">Bu sınıf kendi kendine standart bir sınıf değildir, bunun yerine iki toplu kanal kullanarak basit bir cihaz oluşturmayı ve bu iki kanal üzerinde veri göndermeyi ve geriye doğru göndermeyi gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="55a5a-105">This class is not a standard class in itself, but rather an example that illustrates how to create a simple device by using two bulk pipes and sending data back and forth on these two pipes.</span></span> <span data-ttu-id="55a5a-106">DPUMP sınıfı, özel bir sınıf veya eski RS232 cihazları başlatmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="55a5a-106">The DPUMP class could be used to start a custom class or for legacy RS232 devices.</span></span>

<span data-ttu-id="55a5a-107">USB DPUMP akış grafiği:</span><span class="sxs-lookup"><span data-stu-id="55a5a-107">USB DPUMP flow chart:</span></span>

![USB DPUMP akış grafiği](./media/usbx-host-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-host-class"></a><span data-ttu-id="55a5a-109">USBX DPUMP Host sınıfı</span><span class="sxs-lookup"><span data-stu-id="55a5a-109">USBX DPUMP Host Class</span></span>

<span data-ttu-id="55a5a-110">DPUMP sınıfının konak tarafında, biri veri göndermek için bir tane olmak üzere iki işlev vardır:</span><span class="sxs-lookup"><span data-stu-id="55a5a-110">The host side of the DPUMP Class has two functions, one for sending data and one for receiving data:</span></span>

- `ux_host_class_dpump_write`
- `ux_host_class_dpump_read`

<span data-ttu-id="55a5a-111">Her iki işlev de DPUMP uygulamasını daha kolay hale getirmek için engelleniyor.</span><span class="sxs-lookup"><span data-stu-id="55a5a-111">Both functions are blocking to make the DPUMP application easier.</span></span> <span data-ttu-id="55a5a-112">Aynı anda hem kanalların hem de aynı anda çalıştırılması gerekiyorsa, uygulamanın bir iletme iş parçacığı ve alma iş parçacığı oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="55a5a-112">If it is necessary to have both pipes (IN and OUT) running at the same time, the application will be required to create a transmit thread and a receive thread.</span></span>

<span data-ttu-id="55a5a-113">Yazma işlevinin prototipi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="55a5a-113">The prototype for the writing function is as follows.</span></span>

```C
UINT ux_host_class_dpump_write(UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,  
    ULONG *actual_length)
```

<span data-ttu-id="55a5a-114">Konum:</span><span class="sxs-lookup"><span data-stu-id="55a5a-114">Where:</span></span>

- <span data-ttu-id="55a5a-115">dpump, sınıfının örneğidir</span><span class="sxs-lookup"><span data-stu-id="55a5a-115">dpump is the instance of the class</span></span>
- <span data-ttu-id="55a5a-116">data_pointer gönderilecek arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="55a5a-116">data_pointer is the pointer to the buffer to be sent</span></span>
- <span data-ttu-id="55a5a-117">requested_length, gönderileceği uzunluktadır</span><span class="sxs-lookup"><span data-stu-id="55a5a-117">requested_length is the length to send</span></span>
- <span data-ttu-id="55a5a-118">actual_length, aktarımın tamamlanmasından sonra, başarıyla veya kısmen gönderilen uzunluktadır.</span><span class="sxs-lookup"><span data-stu-id="55a5a-118">actual_length is the length sent after completion of the transfer, either successfully or partially.</span></span>

<span data-ttu-id="55a5a-119">Alma işlevinin prototipi benzerdir.</span><span class="sxs-lookup"><span data-stu-id="55a5a-119">The prototype for the receiving function is similar.</span></span>

```C
UINT ux_host_class_dpump_read(
    UX_HOST_CLASS_DPUMP *dpump,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

<span data-ttu-id="55a5a-120">Bir uygulamanın cihaz tarafına bir paket yazdığı ve alımda aynı paketi aldığı konak DPUMP sınıfına bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="55a5a-120">Here is an example of the host DPUMP class where an application writes a packet to the device side and receives the same packet on the reception:</span></span>

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

## <a name="usbx-dpump-device-class"></a><span data-ttu-id="55a5a-121">USBX DPUMP cihaz sınıfı</span><span class="sxs-lookup"><span data-stu-id="55a5a-121">USBX DPUMP Device Class</span></span>

<span data-ttu-id="55a5a-122">Device DPUMP sınıfı, USB konakla bağlantı kurulduğunda başlatılan bir iş parçacığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="55a5a-122">The device DPUMP class uses a thread, which is started upon connection to the USB host.</span></span> <span data-ttu-id="55a5a-123">İş parçacığı, toplu çıkış uç noktasında gelen bir paketi bekler.</span><span class="sxs-lookup"><span data-stu-id="55a5a-123">The thread waits for a packet coming on the Bulk Out endpoint.</span></span> <span data-ttu-id="55a5a-124">Paket alındığında, içeriği toplu uç nokta arabelleğine kopyalar ve bu uç noktada, konağın bu uç noktadan okuma isteği vermesini bekleyen bir işlem gönderir.</span><span class="sxs-lookup"><span data-stu-id="55a5a-124">When a packet is received, it copies the content to the Bulk In endpoint buffer and posts a transaction on this endpoint, waiting for the host to issue a request to read from this endpoint.</span></span> <span data-ttu-id="55a5a-125">Bu, toplu ve toplu uç noktalar arasında bir geri döngü mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="55a5a-125">This provides a loopback mechanism between the Bulk Out and Bulk In endpoints.</span></span>
