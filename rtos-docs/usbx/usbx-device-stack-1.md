---
title: Bölüm 1-Azure RTOS USBX cihaz yığınına giriş
description: Bu bölümde, uygulamaları ve avantajları açıklanarak USBX cihaz yığını tanıtılmaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 383651bb0af42842329ad15b212e597f63a916aa
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377076"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-device-stack"></a><span data-ttu-id="15dad-103">Bölüm 1-Azure RTOS USBX cihaz yığınına giriş</span><span class="sxs-lookup"><span data-stu-id="15dad-103">Chapter 1 - Introduction to Azure RTOS USBX Device Stack</span></span>

<span data-ttu-id="15dad-104">USBX, derin eklenmiş uygulamalar için tam özellikli bir USB yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="15dad-104">USBX is a full-featured USB stack for deeply embedded applications.</span></span> <span data-ttu-id="15dad-105">Bu bölümde, uygulamaları ve avantajları açıklanarak USBX tanıtılmaktadır</span><span class="sxs-lookup"><span data-stu-id="15dad-105">This chapter introduces USBX, describing its applications and benefits</span></span> 

## <a name="usbx-features"></a><span data-ttu-id="15dad-106">USBX özellikleri</span><span class="sxs-lookup"><span data-stu-id="15dad-106">USBX features</span></span>

<span data-ttu-id="15dad-107">USBX var olan üç USB belirtimini destekler: 1,1, 2,0 ve OTG.</span><span class="sxs-lookup"><span data-stu-id="15dad-107">USBX supports the three existing USB specifications: 1.1, 2.0 and OTG.</span></span> <span data-ttu-id="15dad-108">Ölçeklenebilir olacak şekilde tasarlanmıştır ve tek bir bağlı cihazla basit USB Topolojilerine ve birden çok cihaz ve basamaklı hub 'lara sahip karmaşık topolojilerle uyum sağlar.</span><span class="sxs-lookup"><span data-stu-id="15dad-108">It is designed to be scalable and will accommodate simple USB topologies with only one connected device as well as complex topologies with multiple devices and cascading hubs.</span></span> <span data-ttu-id="15dad-109">USBX, USB protokollerinin tüm veri aktarımı türlerini destekler: denetim, toplu, kesme ve zaman aralıklı.</span><span class="sxs-lookup"><span data-stu-id="15dad-109">USBX supports all the data transfer types of the USB protocols: control, bulk, interrupt, and isochronous.</span></span>

<span data-ttu-id="15dad-110">USBX hem ana bilgisayar tarafını hem de cihaz tarafını destekler.</span><span class="sxs-lookup"><span data-stu-id="15dad-110">USBX supports both the host side and the device side.</span></span> <span data-ttu-id="15dad-111">Her bir kenar üç katmandan oluşur.</span><span class="sxs-lookup"><span data-stu-id="15dad-111">Each side is composed of three layers.</span></span>

- <span data-ttu-id="15dad-112">Denetleyici katmanı</span><span class="sxs-lookup"><span data-stu-id="15dad-112">Controller layer</span></span>
- <span data-ttu-id="15dad-113">Yığın katmanı</span><span class="sxs-lookup"><span data-stu-id="15dad-113">Stack layer</span></span>
- <span data-ttu-id="15dad-114">Sınıf katmanı</span><span class="sxs-lookup"><span data-stu-id="15dad-114">Class layer</span></span>

<span data-ttu-id="15dad-115">USB katmanları arasındaki ilişki aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="15dad-115">The relationship between the USB layers is as follows:</span></span>

![USB katmanları](media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a><span data-ttu-id="15dad-117">Ürün vurguları</span><span class="sxs-lookup"><span data-stu-id="15dad-117">Product Highlights</span></span>

- <span data-ttu-id="15dad-118">Tüm ThreadX işlemci desteğini</span><span class="sxs-lookup"><span data-stu-id="15dad-118">Complete ThreadX processor support</span></span>
- <span data-ttu-id="15dad-119">Hiçbir çatı yok</span><span class="sxs-lookup"><span data-stu-id="15dad-119">No royalties</span></span>
- <span data-ttu-id="15dad-120">Tamamen ANSI C kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="15dad-120">Complete ANSI C source code</span></span>
- <span data-ttu-id="15dad-121">Gerçek zamanlı performans</span><span class="sxs-lookup"><span data-stu-id="15dad-121">Real-time performance</span></span>
- <span data-ttu-id="15dad-122">Yanıt veren teknik destek</span><span class="sxs-lookup"><span data-stu-id="15dad-122">Responsive technical support</span></span>
- <span data-ttu-id="15dad-123">Birden çok sınıf desteği</span><span class="sxs-lookup"><span data-stu-id="15dad-123">Multiple class support</span></span>
- <span data-ttu-id="15dad-124">Birden çok sınıf örneği</span><span class="sxs-lookup"><span data-stu-id="15dad-124">Multiple class instances</span></span>
- <span data-ttu-id="15dad-125">ThreadX, FileX ve NetX ile sınıfların tümleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="15dad-125">Integration of classes with ThreadX, FileX, and NetX</span></span>
- <span data-ttu-id="15dad-126">Birden çok yapılandırmaya sahip USB cihazları için destek</span><span class="sxs-lookup"><span data-stu-id="15dad-126">Support for USB devices with multiple configurations</span></span>
- <span data-ttu-id="15dad-127">USB Bileşik cihazları için destek</span><span class="sxs-lookup"><span data-stu-id="15dad-127">Support for USB composite devices</span></span>
- <span data-ttu-id="15dad-128">USB güç yönetimi desteği</span><span class="sxs-lookup"><span data-stu-id="15dad-128">Support for USB power management</span></span>
- <span data-ttu-id="15dad-129">USB OTG desteği</span><span class="sxs-lookup"><span data-stu-id="15dad-129">Support for USB OTG</span></span>
- <span data-ttu-id="15dad-130">Trackingex için izleme olaylarını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="15dad-130">Export trace events for TraceX</span></span>

## <a name="powerful-services-of-usbx"></a><span data-ttu-id="15dad-131">USBX güçlü Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="15dad-131">Powerful Services of USBX</span></span>

### <a name="complete-usb-device-framework-support"></a><span data-ttu-id="15dad-132">Tüm USB cihaz çerçevesi desteğini</span><span class="sxs-lookup"><span data-stu-id="15dad-132">Complete USB Device Framework Support</span></span>

<span data-ttu-id="15dad-133">USBX, birden çok yapılandırma, birden çok arabirim ve birden çok farklı ayar dahil olmak üzere en zorlu USB cihazlarını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="15dad-133">USBX can support the most demanding USB devices, including multiple configurations, multiple interfaces, and multiple alternate settings.</span></span>

### <a name="easy-to-use-apis"></a><span data-ttu-id="15dad-134">Kullanımı kolay API 'Ler</span><span class="sxs-lookup"><span data-stu-id="15dad-134">Easy-To-Use APIs</span></span>

<span data-ttu-id="15dad-135">USBX, anlaşılması ve kullanılması kolay bir şekilde, en iyi şekilde gömülü USB yığınını sağlar.</span><span class="sxs-lookup"><span data-stu-id="15dad-135">USBX provides the best deeply embedded USB stack in a manner that is easy to understand and use.</span></span> <span data-ttu-id="15dad-136">USBX API 'SI, Hizmetleri sezgisel ve tutarlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="15dad-136">The USBX API makes the services intuitive and consistent.</span></span> <span data-ttu-id="15dad-137">Belirtilen USBX sınıfı API 'Lerini kullanarak, Kullanıcı uygulamasının USB protokollerinin karmaşıklığını anlaması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="15dad-137">By using the provided USBX class APIs, the user application does not need to understand the complexity of the USB protocols.</span></span>
