---
title: Bölüm 1-Azure RTOS USBX konak yığınına giriş
description: USBX, derin eklenmiş uygulamalar için tam özellikli bir USB yığınıdır. Bu bölümde, uygulamaları ve avantajları açıklanarak USBX tanıtılmıştır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9ee49903e764e20316438be16b47d2d9208b1363
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828546"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-host-stack"></a><span data-ttu-id="adc09-104">Bölüm 1-Azure RTOS USBX konak yığınına giriş</span><span class="sxs-lookup"><span data-stu-id="adc09-104">Chapter 1 - Introduction to Azure RTOS USBX Host Stack</span></span>

<span data-ttu-id="adc09-105">USBX, derin eklenmiş uygulamalar için tam özellikli bir USB yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="adc09-105">USBX is a full-featured USB stack for deeply embedded applications.</span></span> <span data-ttu-id="adc09-106">Bu bölümde, uygulamaları ve avantajları açıklanarak USBX tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="adc09-106">This chapter introduces USBX, describing its applications and benefits.</span></span>

## <a name="usbx-features"></a><span data-ttu-id="adc09-107">USBX özellikleri</span><span class="sxs-lookup"><span data-stu-id="adc09-107">USBX features</span></span>

<span data-ttu-id="adc09-108">USBX mevcut üç USB belirtimini destekler: 1,1, 2,0 ve OTG.</span><span class="sxs-lookup"><span data-stu-id="adc09-108">USBX support the three existing USB specifications: 1.1, 2.0 and OTG.</span></span> <span data-ttu-id="adc09-109">Ölçeklenebilir olacak şekilde tasarlanmıştır ve tek bir bağlı cihazla basit USB Topolojilerine ve birden çok cihaz ve basamaklı hub 'lara sahip karmaşık topolojilerle uyum sağlar.</span><span class="sxs-lookup"><span data-stu-id="adc09-109">It is designed to be scalable and will accommodate simple USB topologies with only one connected device as well as complex topologies with multiple devices and cascading hubs.</span></span> <span data-ttu-id="adc09-110">USBX, USB protokollerinin tüm veri aktarımı türlerini destekler: denetim, toplu, kesme ve zaman aralıklı.</span><span class="sxs-lookup"><span data-stu-id="adc09-110">USBX supports all the data transfer types of the USB protocols: control, bulk, interrupt, and isochronous.</span></span>

<span data-ttu-id="adc09-111">USBX hem ana bilgisayar tarafını hem de cihaz tarafını destekler.</span><span class="sxs-lookup"><span data-stu-id="adc09-111">USBX supports both the host side and the device side.</span></span> <span data-ttu-id="adc09-112">Her bir kenar üç katmandan oluşur.</span><span class="sxs-lookup"><span data-stu-id="adc09-112">Each side is comprised of three layers.</span></span>

- <span data-ttu-id="adc09-113">Denetleyici katmanı</span><span class="sxs-lookup"><span data-stu-id="adc09-113">Controller layer</span></span>
- <span data-ttu-id="adc09-114">Yığın katmanı</span><span class="sxs-lookup"><span data-stu-id="adc09-114">Stack layer</span></span>
- <span data-ttu-id="adc09-115">Sınıf katmanı</span><span class="sxs-lookup"><span data-stu-id="adc09-115">Class layer</span></span>

<span data-ttu-id="adc09-116">USB katmanları arasındaki ilişki aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="adc09-116">The relationship between the USB layers is as follows.</span></span>

![USB katmanları](./media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a><span data-ttu-id="adc09-118">Ürün vurguları</span><span class="sxs-lookup"><span data-stu-id="adc09-118">Product Highlights</span></span>

- <span data-ttu-id="adc09-119">Tüm ThreadX işlemci desteğini</span><span class="sxs-lookup"><span data-stu-id="adc09-119">Complete ThreadX processor support</span></span>
- <span data-ttu-id="adc09-120">Hiçbir çatı yok</span><span class="sxs-lookup"><span data-stu-id="adc09-120">No royalties</span></span>
- <span data-ttu-id="adc09-121">Tamamen ANSI C kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="adc09-121">Complete ANSI C source code</span></span>
- <span data-ttu-id="adc09-122">Gerçek zamanlı performans</span><span class="sxs-lookup"><span data-stu-id="adc09-122">Real-time performance</span></span>
- <span data-ttu-id="adc09-123">Yanıt veren teknik destek</span><span class="sxs-lookup"><span data-stu-id="adc09-123">Responsive technical support</span></span>
- <span data-ttu-id="adc09-124">Birden çok konak denetleyicisi desteği</span><span class="sxs-lookup"><span data-stu-id="adc09-124">Multiple host controller support</span></span>
- <span data-ttu-id="adc09-125">Birden çok sınıf desteği</span><span class="sxs-lookup"><span data-stu-id="adc09-125">Multiple class support</span></span>
- <span data-ttu-id="adc09-126">Birden çok sınıf örneği</span><span class="sxs-lookup"><span data-stu-id="adc09-126">Multiple class instances</span></span>
- <span data-ttu-id="adc09-127">ThreadX, FileX ve NetX ile sınıfların tümleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="adc09-127">Integration of classes with ThreadX, FileX and NetX</span></span>
- <span data-ttu-id="adc09-128">Birden çok yapılandırmaya sahip USB cihazları için destek</span><span class="sxs-lookup"><span data-stu-id="adc09-128">Support for USB devices with multiple configuration</span></span>
- <span data-ttu-id="adc09-129">USB Bileşik cihazları için destek</span><span class="sxs-lookup"><span data-stu-id="adc09-129">Support for USB composite devices</span></span>
- <span data-ttu-id="adc09-130">Geçişli hub 'lar için destek</span><span class="sxs-lookup"><span data-stu-id="adc09-130">Support for cascading hubs</span></span>
- <span data-ttu-id="adc09-131">USB güç yönetimi desteği</span><span class="sxs-lookup"><span data-stu-id="adc09-131">Support for USB power management</span></span>
- <span data-ttu-id="adc09-132">USB OTG desteği</span><span class="sxs-lookup"><span data-stu-id="adc09-132">Support for USB OTG</span></span>
- <span data-ttu-id="adc09-133">Trackingex için izleme olaylarını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="adc09-133">Export trace events for TraceX</span></span>

## <a name="powerful-services-of-usbx"></a><span data-ttu-id="adc09-134">USBX güçlü Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="adc09-134">Powerful Services of USBX</span></span>

### <a name="multiple-host-controller-support"></a><span data-ttu-id="adc09-135">Birden çok konak denetleyicisi desteği</span><span class="sxs-lookup"><span data-stu-id="adc09-135">Multiple Host Controller Support</span></span>

<span data-ttu-id="adc09-136">USBX, eşzamanlı olarak çalışan birden çok USB konak denetleyicisini destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="adc09-136">USBX can support multiple USB host controllers running concurrently.</span></span> <span data-ttu-id="adc09-137">Bu özellik, Günümüzde pazardaki en fazla USB 2,0 ana bilgisayar denetleyicisiyle ilişkili geriye dönük uyumluluk şemasını kullanarak, USBX 'in USB 2,0 standardını desteklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="adc09-137">This feature allows USBX to support the USB 2.0 standard using the backward compatibility scheme associated with most USB 2.0 host controllers on the market today.</span></span>

### <a name="usb-software-scheduler"></a><span data-ttu-id="adc09-138">USB yazılım Zamanlayıcısı</span><span class="sxs-lookup"><span data-stu-id="adc09-138">USB Software Scheduler</span></span>

<span data-ttu-id="adc09-139">USBX, donanım listesi işleme içermeyen USB denetleyicilerini desteklemek için gereken bir USB yazılım zamanlayıcısını içerir.</span><span class="sxs-lookup"><span data-stu-id="adc09-139">USBX contains a USB software scheduler necessary to support USB controllers that do not have hardware list processing.</span></span> <span data-ttu-id="adc09-140">USBX yazılım Zamanlayıcısı, USB aktarımlarını doğru hizmet ve öncelik sıklığıyla düzenler ve USB denetleyicisinin her aktarımı yürütmesini ister.</span><span class="sxs-lookup"><span data-stu-id="adc09-140">The USBX software scheduler will organize USB transfers with the correct frequency of service and priority, and will instruct the USB controller to execute each transfer.</span></span>

### <a name="complete-usb-device-framework-support"></a><span data-ttu-id="adc09-141">Tüm USB cihaz çerçevesi desteğini</span><span class="sxs-lookup"><span data-stu-id="adc09-141">Complete USB Device Framework Support</span></span>

<span data-ttu-id="adc09-142">USBX, birden çok yapılandırma, birden çok arabirim ve birden çok farklı ayar dahil olmak üzere en zorlu USB cihazlarını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="adc09-142">USBX can support the most demanding USB devices, including multiple configurations, multiple interfaces, and multiple alternate settings.</span></span>

### <a name="easy-to-use-apis"></a><span data-ttu-id="adc09-143">Kullanımı kolay API 'Ler</span><span class="sxs-lookup"><span data-stu-id="adc09-143">Easy-To-Use APIs</span></span>

<span data-ttu-id="adc09-144">USBX, anlaşılması ve kullanılması kolay bir şekilde en iyi şekilde gömülü USB yığınını sağlar.</span><span class="sxs-lookup"><span data-stu-id="adc09-144">USBX provides the very best deeply embedded USB stack in a manner that is easy to understand and use.</span></span> <span data-ttu-id="adc09-145">USBX API 'SI, Hizmetleri sezgisel ve tutarlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="adc09-145">The USBX API makes the services intuitive and consistent.</span></span> <span data-ttu-id="adc09-146">Belirtilen USBX sınıfı API 'Lerini kullanarak, Kullanıcı uygulamasının USB protokollerinin karmaşıklığını anlaması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="adc09-146">By using the provided USBX class APIs, the user application does not need to understand the complexity of the USB protocols.</span></span>
