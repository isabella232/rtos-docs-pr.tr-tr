---
title: Bölüm 3-USBX DPUMP sınıfı konuları
description: USBX, konak ve cihaz tarafı için bir DPUMP sınıfı içerir. Bu sınıf kendi kendine standart bir sınıf değildir, bunun yerine iki toplu kanal kullanarak basit bir cihaz oluşturmayı ve bu iki kanal üzerinde veri göndermeyi ve geriye doğru göndermeyi gösteren bir örnek.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c7870f1984fe3104d30e3b9efd82010218acbe27
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828613"
---
# <a name="chapter-3---usbx-dpump-class-considerations"></a><span data-ttu-id="2895a-104">Bölüm 3-USBX DPUMP sınıfı konuları</span><span class="sxs-lookup"><span data-stu-id="2895a-104">Chapter 3 - USBX DPUMP Class Considerations</span></span>

<span data-ttu-id="2895a-105">USBX, konak ve cihaz tarafı için bir **DPUMP** sınıfı içerir.</span><span class="sxs-lookup"><span data-stu-id="2895a-105">USBX contains a **DPUMP** class for the host and device side.</span></span> <span data-ttu-id="2895a-106">Bu sınıf kendi kendine standart bir sınıf değildir, bunun yerine iki toplu kanal kullanarak basit bir cihaz oluşturmayı ve bu iki kanal üzerinde veri göndermeyi ve geriye doğru göndermeyi gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="2895a-106">This class is not a standard class in itself, but rather an example that illustrates how to create a simple device by using two bulk pipes and sending data back and forth on these two pipes.</span></span> <span data-ttu-id="2895a-107">**DPUMP** sınıfı, özel bir sınıf veya eski RS232 cihazları başlatmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2895a-107">The **DPUMP** class could be used to start a custom class or for legacy RS232 devices.</span></span>

<span data-ttu-id="2895a-108">USB DPUMP akış grafiği:</span><span class="sxs-lookup"><span data-stu-id="2895a-108">USB DPUMP flow chart:</span></span>

![USB DPUMP akış grafiği](./media/usbx-device-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-device-class"></a><span data-ttu-id="2895a-110">USBX DPUMP cihaz sınıfı</span><span class="sxs-lookup"><span data-stu-id="2895a-110">USBX DPUMP Device Class</span></span>

<span data-ttu-id="2895a-111">Device **DPUMP** sınıfı, USB konakla bağlantı kurulduğunda başlatılan bir iş parçacığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="2895a-111">The device **DPUMP** class uses a thread, which is started upon connection to the USB host.</span></span> <span data-ttu-id="2895a-112">İş parçacığı, toplu çıkış uç noktasında gelen bir paketi bekler.</span><span class="sxs-lookup"><span data-stu-id="2895a-112">The thread waits for a packet coming on the Bulk Out endpoint.</span></span> <span data-ttu-id="2895a-113">Paket alındığında, içeriği toplu uç nokta arabelleğine kopyalar ve bu uç noktada, konağın bu uç noktadan okuma isteği vermesini bekleyen bir işlem gönderir.</span><span class="sxs-lookup"><span data-stu-id="2895a-113">When a packet is received, it copies the content to the Bulk In endpoint buffer and posts a transaction on this endpoint, waiting for the host to issue a request to read from this endpoint.</span></span> <span data-ttu-id="2895a-114">Bu, toplu ve toplu uç noktalar arasında bir geri döngü mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="2895a-114">This provides a loopback mechanism between the Bulk Out and Bulk In endpoints.</span></span>
