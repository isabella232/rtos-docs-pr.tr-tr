---
title: Bölüm 1-Azure RTOS USBX cihaz yığınına giriş
description: USBX, derin eklenmiş uygulamalar için tam özellikli bir USB yığınıdır. Bu bölümde, avantajları ve uygulaması açıklanarak USBX tanıtılmıştır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 8b1e08130d4531fd82629378761cd5b1752f0a07
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550295"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-device-stack"></a><span data-ttu-id="36fe2-104">Bölüm 1-Azure RTOS USBX cihaz yığınına giriş</span><span class="sxs-lookup"><span data-stu-id="36fe2-104">Chapter 1 - Introduction to Azure RTOS USBX Device Stack</span></span>

<span data-ttu-id="36fe2-105">USBX, derin eklenmiş uygulamalar için tam özellikli bir USB yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="36fe2-105">USBX is a full-featured USB stack for deeply embedded applications.</span></span> <span data-ttu-id="36fe2-106">Bu bölümde, uygulamaları ve avantajları açıklanarak USBX tanıtılmaktadır</span><span class="sxs-lookup"><span data-stu-id="36fe2-106">This chapter introduces USBX, describing its applications and benefits</span></span> 

## <a name="usbx-features"></a><span data-ttu-id="36fe2-107">USBX özellikleri</span><span class="sxs-lookup"><span data-stu-id="36fe2-107">USBX features</span></span>

<span data-ttu-id="36fe2-108">USBX var olan üç USB belirtimini destekler: 1,1, 2,0 ve OTG.</span><span class="sxs-lookup"><span data-stu-id="36fe2-108">USBX supports the three existing USB specifications: 1.1, 2.0 and OTG.</span></span> <span data-ttu-id="36fe2-109">Ölçeklenebilir olacak şekilde tasarlanmıştır ve tek bir bağlı cihazla basit USB Topolojilerine ve birden çok cihaz ve basamaklı hub 'lara sahip karmaşık topolojilerle uyum sağlar.</span><span class="sxs-lookup"><span data-stu-id="36fe2-109">It is designed to be scalable and will accommodate simple USB topologies with only one connected device as well as complex topologies with multiple devices and cascading hubs.</span></span> <span data-ttu-id="36fe2-110">USBX, USB protokollerinin tüm veri aktarımı türlerini destekler: denetim, toplu, kesme ve zaman aralıklı.</span><span class="sxs-lookup"><span data-stu-id="36fe2-110">USBX supports all the data transfer types of the USB protocols: control, bulk, interrupt, and isochronous.</span></span>

<span data-ttu-id="36fe2-111">USBX hem ana bilgisayar tarafını hem de cihaz tarafını destekler.</span><span class="sxs-lookup"><span data-stu-id="36fe2-111">USBX supports both the host side and the device side.</span></span> <span data-ttu-id="36fe2-112">Her bir kenar üç katmandan oluşur.</span><span class="sxs-lookup"><span data-stu-id="36fe2-112">Each side is composed of three layers.</span></span>

- <span data-ttu-id="36fe2-113">Denetleyici katmanı</span><span class="sxs-lookup"><span data-stu-id="36fe2-113">Controller layer</span></span>
- <span data-ttu-id="36fe2-114">Yığın katmanı</span><span class="sxs-lookup"><span data-stu-id="36fe2-114">Stack layer</span></span>
- <span data-ttu-id="36fe2-115">Sınıf katmanı</span><span class="sxs-lookup"><span data-stu-id="36fe2-115">Class layer</span></span>

<span data-ttu-id="36fe2-116">USB katmanları arasındaki ilişki aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="36fe2-116">The relationship between the USB layers is as follows:</span></span>

![USB katmanları](media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a><span data-ttu-id="36fe2-118">Ürün vurguları</span><span class="sxs-lookup"><span data-stu-id="36fe2-118">Product Highlights</span></span>

- <span data-ttu-id="36fe2-119">Tüm ThreadX işlemci desteğini</span><span class="sxs-lookup"><span data-stu-id="36fe2-119">Complete ThreadX processor support</span></span>
- <span data-ttu-id="36fe2-120">Hiçbir çatı yok</span><span class="sxs-lookup"><span data-stu-id="36fe2-120">No royalties</span></span>
- <span data-ttu-id="36fe2-121">Tamamen ANSI C kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="36fe2-121">Complete ANSI C source code</span></span>
- <span data-ttu-id="36fe2-122">Gerçek zamanlı performans</span><span class="sxs-lookup"><span data-stu-id="36fe2-122">Real-time performance</span></span>
- <span data-ttu-id="36fe2-123">Yanıt veren teknik destek</span><span class="sxs-lookup"><span data-stu-id="36fe2-123">Responsive technical support</span></span>
- <span data-ttu-id="36fe2-124">Birden çok sınıf desteği</span><span class="sxs-lookup"><span data-stu-id="36fe2-124">Multiple class support</span></span>
- <span data-ttu-id="36fe2-125">Birden çok sınıf örneği</span><span class="sxs-lookup"><span data-stu-id="36fe2-125">Multiple class instances</span></span>
- <span data-ttu-id="36fe2-126">ThreadX, FileX ve NetX ile sınıfların tümleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="36fe2-126">Integration of classes with ThreadX, FileX, and NetX</span></span>
- <span data-ttu-id="36fe2-127">Birden çok yapılandırmaya sahip USB cihazları için destek</span><span class="sxs-lookup"><span data-stu-id="36fe2-127">Support for USB devices with multiple configurations</span></span>
- <span data-ttu-id="36fe2-128">USB Bileşik cihazları için destek</span><span class="sxs-lookup"><span data-stu-id="36fe2-128">Support for USB composite devices</span></span>
- <span data-ttu-id="36fe2-129">USB güç yönetimi desteği</span><span class="sxs-lookup"><span data-stu-id="36fe2-129">Support for USB power management</span></span>
- <span data-ttu-id="36fe2-130">USB OTG desteği</span><span class="sxs-lookup"><span data-stu-id="36fe2-130">Support for USB OTG</span></span>
- <span data-ttu-id="36fe2-131">Trackingex için izleme olaylarını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="36fe2-131">Export trace events for TraceX</span></span>

## <a name="powerful-services-of-usbx"></a><span data-ttu-id="36fe2-132">USBX güçlü Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="36fe2-132">Powerful Services of USBX</span></span>

### <a name="complete-usb-device-framework-support"></a><span data-ttu-id="36fe2-133">Tüm USB cihaz çerçevesi desteğini</span><span class="sxs-lookup"><span data-stu-id="36fe2-133">Complete USB Device Framework Support</span></span>

<span data-ttu-id="36fe2-134">USBX, birden çok yapılandırma, birden çok arabirim ve birden çok farklı ayar dahil olmak üzere en zorlu USB cihazlarını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="36fe2-134">USBX can support the most demanding USB devices, including multiple configurations, multiple interfaces, and multiple alternate settings.</span></span>

### <a name="easy-to-use-apis"></a><span data-ttu-id="36fe2-135">Kullanımı kolay API 'Ler</span><span class="sxs-lookup"><span data-stu-id="36fe2-135">Easy-To-Use APIs</span></span>

<span data-ttu-id="36fe2-136">USBX, anlaşılması ve kullanılması kolay bir şekilde, en iyi şekilde gömülü USB yığınını sağlar.</span><span class="sxs-lookup"><span data-stu-id="36fe2-136">USBX provides the best deeply embedded USB stack in a manner that is easy to understand and use.</span></span> <span data-ttu-id="36fe2-137">USBX API 'SI, Hizmetleri sezgisel ve tutarlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="36fe2-137">The USBX API makes the services intuitive and consistent.</span></span> <span data-ttu-id="36fe2-138">Belirtilen USBX sınıfı API 'Lerini kullanarak, Kullanıcı uygulamasının USB protokollerinin karmaşıklığını anlaması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="36fe2-138">By using the provided USBX class APIs, the user application does not need to understand the complexity of the USB protocols.</span></span>
