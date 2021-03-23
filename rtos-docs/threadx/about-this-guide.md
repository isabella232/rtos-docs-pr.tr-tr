---
title: Azure RTOS ThreadX Kılavuzu hakkında
description: Bu kılavuz, Microsoft yüksek performanslı gerçek zamanlı çekirdek olan Azure RTOS ThreadX hakkında kapsamlı bilgiler sağlar.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ad9f782942bcdbb2dc49a9c841d865d97bcb1d4e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826591"
---
# <a name="about-the-azure-rtos-threadx-guide"></a><span data-ttu-id="359b4-103">Azure RTOS ThreadX Kılavuzu hakkında</span><span class="sxs-lookup"><span data-stu-id="359b4-103">About the Azure RTOS ThreadX Guide</span></span>

<span data-ttu-id="359b4-104">Bu kılavuz, Microsoft yüksek performanslı gerçek zamanlı çekirdek olan Azure RTOS ThreadX hakkında kapsamlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="359b4-104">This guide provides comprehensive information about Azure RTOS ThreadX, the Microsoft high-performance real-time kernel.</span></span> 

<span data-ttu-id="359b4-105">Katıştırılmış gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="359b4-105">It is intended for the embedded real-time software developer.</span></span> <span data-ttu-id="359b4-106">Geliştirici standart gerçek zamanlı işletim sistemi işlevleri ve C programlama diliyle tanıdık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="359b4-106">The developer should be familiar with standard real-time operating system functions and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="359b4-107">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="359b4-107">Organization</span></span>

<span data-ttu-id="359b4-108">[Bölüm 1](chapter1.md) -Azure RTOS threadx için temel bir genel bakış ve gerçek zamanlı gömülü geliştirmeyle ilişkisi sağlar</span><span class="sxs-lookup"><span data-stu-id="359b4-108">[Chapter 1](chapter1.md) - Provides a basic overview of Azure RTOS ThreadX and its relationship to real-time embedded development</span></span>

<span data-ttu-id="359b4-109">[Bölüm 2](chapter2.md) -uygulamanızda Azure RTOS threadx 'i yüklemek ve kullanmak için temel adımlara izin verir </span><span class="sxs-lookup"><span data-stu-id="359b4-109">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS ThreadX in your application right *out of the box*</span></span>

<span data-ttu-id="359b4-110">[Bölüm 3](chapter3.md) -Azure RTOS threadx 'in işlevsel işlemi ayrıntılı olarak, yüksek performanslı gerçek zamanlı çekirdek</span><span class="sxs-lookup"><span data-stu-id="359b4-110">[Chapter 3](chapter3.md) - Describes in detail the functional operation of Azure RTOS ThreadX, the high performance real-time kernel</span></span>

<span data-ttu-id="359b4-111">[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS threadx 'e ait arabiriminin ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="359b4-111">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS ThreadX</span></span>

<span data-ttu-id="359b4-112">[Bölüm 5](chapter5.md) -Azure RTOS threadx uygulamaları için g/ç sürücülerinin yazılmasını açıklar</span><span class="sxs-lookup"><span data-stu-id="359b4-112">[Chapter 5](chapter5.md) - Describes writing I/O drivers for Azure RTOS ThreadX applications</span></span>

<span data-ttu-id="359b4-113">[Bölüm 6](chapter6.md) -her Azure RTOS threadx işlemci desteği paketiyle birlikte sunulan tanıtım uygulamasını açıklar</span><span class="sxs-lookup"><span data-stu-id="359b4-113">[Chapter 6](chapter6.md) - Describes the demonstration application that is supplied with every Azure RTOS ThreadX processor support package</span></span>

<span data-ttu-id="359b4-114">[Ek A](appendix-a.md) -Azure RTOS THREADX API 'si</span><span class="sxs-lookup"><span data-stu-id="359b4-114">[Appendix A](appendix-a.md) - Azure RTOS ThreadX API</span></span>

<span data-ttu-id="359b4-115">[Ek B](appendix-b.md) -Azure RTOS threadx sabitleri</span><span class="sxs-lookup"><span data-stu-id="359b4-115">[Appendix B](appendix-b.md) - Azure RTOS ThreadX constants</span></span>

<span data-ttu-id="359b4-116">[Ek C](appendix-c.md) -Azure RTOS threadx veri türleri</span><span class="sxs-lookup"><span data-stu-id="359b4-116">[Appendix C](appendix-c.md) - Azure RTOS ThreadX data types</span></span>

<span data-ttu-id="359b4-117">[Ek D](appendix-d.md) -ASCII grafik</span><span class="sxs-lookup"><span data-stu-id="359b4-117">[Appendix D](appendix-d.md) - ASCII chart</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="359b4-118">Kılavuz kuralları</span><span class="sxs-lookup"><span data-stu-id="359b4-118">Guide Conventions</span></span>

<span data-ttu-id="359b4-119">*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve parametreleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="359b4-119">*Italics* - typeface denotes book titles, emphasizes important words, and indicates parameters.</span></span>

<span data-ttu-id="359b4-120">**Kalın** yazı tipi, anahtar sözcükler, sabitler, tür adları, Kullanıcı arabirimi öğeleri, değişken adları ve önemli sözcükleri daha fazla vurgular.</span><span class="sxs-lookup"><span data-stu-id="359b4-120">**Boldface** - typeface denotes key words, constants, type names, user interface elements, variable names, and further emphasizes important words.</span></span>

<span data-ttu-id="359b4-121">***İtalik ve kalın*** yazı tipi dosya adlarını ve işlev adlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="359b4-121">***Italics and Boldface*** - typeface denotes file names and function names.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="359b4-122">Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="359b4-122">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>

> [!WARNING]
> <span data-ttu-id="359b4-123">Uyarı sembolleri, geliştiricilerin önemli hatalara neden olabileceğinden kaçınmak için dikkatli olması gereken durumlara dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="359b4-123">Warning symbols draw attention to situations in which developers should take care to avoid because they could cause fatal errors.</span></span>

## <a name="azure-rtos-threadx-data-types"></a><span data-ttu-id="359b4-124">Azure RTOS ThreadX veri türleri</span><span class="sxs-lookup"><span data-stu-id="359b4-124">Azure RTOS ThreadX Data Types</span></span>

<span data-ttu-id="359b4-125">Özel Azure RTOS ThreadX denetim yapısı veri türlerine ek olarak, Azure RTOS ThreadX hizmet çağrı arabirimlerinde kullanılan bir dizi özel veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="359b4-125">In addition to the custom Azure RTOS ThreadX control structure data types, there are a series of special data types that are used in Azure RTOS ThreadX service call interfaces.</span></span> <span data-ttu-id="359b4-126">Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir.</span><span class="sxs-lookup"><span data-stu-id="359b4-126">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="359b4-127">Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır.</span><span class="sxs-lookup"><span data-stu-id="359b4-127">This is done to insure portability between different C compilers.</span></span> <span data-ttu-id="359b4-128">Tam uygulama, kaynağa dahil olan ***tx_port. h*** dosyasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="359b4-128">The exact implementation can be found in the ***tx_port.h*** file included with the source.</span></span>

<span data-ttu-id="359b4-129">Aşağıda, Azure RTOS ThreadX hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="359b4-129">The following is a list of Azure RTOS ThreadX service call data types and their associated meanings:</span></span>

| <span data-ttu-id="359b4-130">Veri türü</span><span class="sxs-lookup"><span data-stu-id="359b4-130">Data type</span></span>  | <span data-ttu-id="359b4-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="359b4-131">Description</span></span> |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| <span data-ttu-id="359b4-132">**U**</span><span class="sxs-lookup"><span data-stu-id="359b4-132">**UINT**</span></span> | <span data-ttu-id="359b4-133">Temel işaretsiz tamsayı.</span><span class="sxs-lookup"><span data-stu-id="359b4-133">Basic unsigned integer.</span></span> <span data-ttu-id="359b4-134">Bu tür 8 bit işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir.</span><span class="sxs-lookup"><span data-stu-id="359b4-134">This type must support 8-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span> |
| <span data-ttu-id="359b4-135">**'TUR**</span><span class="sxs-lookup"><span data-stu-id="359b4-135">**ULONG**</span></span> | <span data-ttu-id="359b4-136">İmzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="359b4-136">Unsigned long type.</span></span> <span data-ttu-id="359b4-137">Bu tür 32 bitlik işaretsiz verileri desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="359b4-137">This type must support 32-bit unsigned data.</span></span> |
| <span data-ttu-id="359b4-138">**Kağıt**</span><span class="sxs-lookup"><span data-stu-id="359b4-138">**VOID**</span></span> | <span data-ttu-id="359b4-139">Derleyicinin void türüne neredeyse her zaman eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="359b4-139">Almost always equivalent to the compiler's void type.</span></span> |
| <span data-ttu-id="359b4-140">**CHAR**</span><span class="sxs-lookup"><span data-stu-id="359b4-140">**CHAR**</span></span> | <span data-ttu-id="359b4-141">Genellikle standart 8 bitlik bir karakter türü.</span><span class="sxs-lookup"><span data-stu-id="359b4-141">Most often a standard 8-bit character type.</span></span> |
|  |  |

<span data-ttu-id="359b4-142">Ek veri türleri, Azure RTOS ThreadX kaynağı içinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="359b4-142">Additional data types are used within the Azure RTOS ThreadX source.</span></span> <span data-ttu-id="359b4-143">Bunlar ayrıca ***tx_port. h*** dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="359b4-143">They are also located in the ***tx_port.h*** file.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="359b4-144">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="359b4-144">Customer Support Center</span></span>

<span data-ttu-id="359b4-145">Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin.</span><span class="sxs-lookup"><span data-stu-id="359b4-145">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="359b4-146">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:</span><span class="sxs-lookup"><span data-stu-id="359b4-146">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="359b4-147">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="359b4-147">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="359b4-148">Uygulamada ve/veya Azure RTOS ThreadX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.</span><span class="sxs-lookup"><span data-stu-id="359b4-148">A detailed description of any changes to the application and/or Azure RTOS ThreadX that preceded the problem.</span></span>
3. <span data-ttu-id="359b4-149">*_Tx_version_id* dizesinin içeriği, dağılımının *tx_port. h* dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="359b4-149">The contents of the *_tx_version_id* string found in the *tx_port.h* file of your distribution.</span></span> <span data-ttu-id="359b4-150">Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="359b4-150">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="359b4-151">**_Tx_build_options** **ulong** değişkeninin RAM 'e ait içerik.</span><span class="sxs-lookup"><span data-stu-id="359b4-151">The contents in RAM of the **_tx_build_options** **ULONG** variable.</span></span> <span data-ttu-id="359b4-152">Bu değişken, Azure RTOS ThreadX Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.</span><span class="sxs-lookup"><span data-stu-id="359b4-152">This variable will give us information on how your Azure RTOS ThreadX library was built.</span></span>
