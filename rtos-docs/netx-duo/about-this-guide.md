---
title: Azure RTOS NetX Duo Kullanıcı Kılavuzu hakkında
description: Bu kılavuz, Microsoft yüksek performanslı IPv4/IPv6 ikili ağ yığını olan Azure RTOS NetX Duo hakkında kapsamlı bilgiler içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b1eef5bfa28f13d7a6b627792f96039b252f2355
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826237"
---
# <a name="about-the-azure-rtos-netx-duo-user-guide"></a><span data-ttu-id="c4059-103">Azure RTOS NetX Duo Kullanıcı Kılavuzu hakkında</span><span class="sxs-lookup"><span data-stu-id="c4059-103">About The Azure RTOS NetX Duo User Guide</span></span>

<span data-ttu-id="c4059-104">Bu kılavuz, Microsoft yüksek performanslı IPv4/IPv6 ikili ağ yığını olan Azure RTOS NetX Duo hakkında kapsamlı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="c4059-104">This guide contains comprehensive information about Azure RTOS NetX Duo, the Microsoft high-performance IPv4/IPv6 dual network stack.</span></span> 

<span data-ttu-id="c4059-105">Temel ağ kavramlarıyla, Azure RTOS ThreadX ve C programlama diliyle tanıdık olan gömülü gerçek zamanlı yazılım geliştiricileri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c4059-105">It is intended for embedded real-time software developers familiar with basic networking concepts, Azure RTOS ThreadX, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="c4059-106">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="c4059-106">Organization</span></span>

<span data-ttu-id="c4059-107">[Bölüm 1](chapter1.md) -Azure RTOS NETX Duo 'i tanıtır</span><span class="sxs-lookup"><span data-stu-id="c4059-107">[Chapter 1](chapter1.md) - Introduces Azure RTOS NetX Duo</span></span>

<span data-ttu-id="c4059-108">[Bölüm 2](chapter2.md) -Azure RTOS NETX Duo 'U threadx uygulamanızla yüklemek ve kullanmak için temel adımlara izin verir</span><span class="sxs-lookup"><span data-stu-id="c4059-108">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS NetX Duo with your ThreadX application</span></span>

<span data-ttu-id="c4059-109">[Bölüm 3](chapter3.md) -Azure RTOS NETX Duo sistemine işlevsel bir genel bakış ve TCP/IP ağ standartları hakkında temel bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="c4059-109">[Chapter 3](chapter3.md) - Provides a functional overview of the Azure RTOS NetX Duo system and basic information about the TCP/IP networking standards</span></span>

<span data-ttu-id="c4059-110">[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS NETX Duo arabirimine ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c4059-110">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS NetX Duo</span></span>

<span data-ttu-id="c4059-111">[Bölüm 5](chapter5.md) -Azure RTOS NETX Duo için ağ sürücülerini açıklar</span><span class="sxs-lookup"><span data-stu-id="c4059-111">[Chapter 5](chapter5.md) - Describes network drivers for Azure RTOS NetX Duo</span></span>

<span data-ttu-id="c4059-112">[Ek A](appendix-a.md) -Azure RTOS NETX Duo Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="c4059-112">[Appendix A](appendix-a.md) - Azure RTOS NetX Duo Services</span></span>

<span data-ttu-id="c4059-113">[Ek B](appendix-b.md) -Azure RTOS NETX Duo sabitleri</span><span class="sxs-lookup"><span data-stu-id="c4059-113">[Appendix B](appendix-b.md) - Azure RTOS NetX Duo Constants</span></span>

<span data-ttu-id="c4059-114">[Ek C](appendix-c.md) -Azure RTOS NETX Duo veri türleri</span><span class="sxs-lookup"><span data-stu-id="c4059-114">[Appendix C](appendix-c.md) - Azure RTOS NetX Duo Data Types</span></span>

<span data-ttu-id="c4059-115">[Ek D](appendix-d.md) -BSD-Compatible yuvası API 'si</span><span class="sxs-lookup"><span data-stu-id="c4059-115">[Appendix D](appendix-d.md) - BSD-Compatible Socket API</span></span>

<span data-ttu-id="c4059-116">[Ek E](appendix-e.md) -ASCII grafik</span><span class="sxs-lookup"><span data-stu-id="c4059-116">[Appendix E](appendix-e.md) - ASCII Chart</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="c4059-117">Kılavuz kuralları</span><span class="sxs-lookup"><span data-stu-id="c4059-117">Guide Conventions</span></span>

<span data-ttu-id="c4059-118">İtalik yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="c4059-118">Italics - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="c4059-119">**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.</span><span class="sxs-lookup"><span data-stu-id="c4059-119">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4059-120">Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="c4059-120">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>
 
> [!WARNING]
> <span data-ttu-id="c4059-121">Uyarı sembolleri, önemli hatalara neden olabileceğinden, geliştiricilerin oluşmaması gereken durumlara dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="c4059-121">Warning symbols draw attention to situations that developers should avoid because they could cause fatal errors.</span></span>

## <a name="azure-rtos-netx-duo-data-types"></a><span data-ttu-id="c4059-122">Azure RTOS NetX Duo veri türleri</span><span class="sxs-lookup"><span data-stu-id="c4059-122">Azure RTOS NetX Duo Data Types</span></span>

<span data-ttu-id="c4059-123">Özel Azure RTOS NetX Duo denetim yapısı veri türlerine ek olarak, Azure RTOS NetX Duo hizmet çağrı arabirimlerinde kullanılan birkaç özel veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="c4059-123">In addition to the custom Azure RTOS NetX Duo control structure data types, there are several special data types that are used in Azure RTOS NetX Duo service call interfaces.</span></span> <span data-ttu-id="c4059-124">Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir.</span><span class="sxs-lookup"><span data-stu-id="c4059-124">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="c4059-125">Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır.</span><span class="sxs-lookup"><span data-stu-id="c4059-125">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="c4059-126">Tam uygulama ThreadX 'ten devralınır ve ThreadX dağıtımına dahil olan ***tx_port. h*** dosyasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c4059-126">The exact implementation is inherited from ThreadX and can be found in the ***tx_port.h*** file included in the ThreadX distribution.</span></span>

<span data-ttu-id="c4059-127">Aşağıda, Azure RTOS NetX Duo hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c4059-127">The following is a list of Azure RTOS NetX Duo service call data types and their associated meanings:</span></span>

<span data-ttu-id="c4059-128">**UINT**: temel işaretsiz tamsayı.</span><span class="sxs-lookup"><span data-stu-id="c4059-128">**UINT**: Basic unsigned integer.</span></span> <span data-ttu-id="c4059-129">Bu tür 32 bitlik işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir.</span><span class="sxs-lookup"><span data-stu-id="c4059-129">This type must support 32-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span>  
<span data-ttu-id="c4059-130">**Ulong**: imzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="c4059-130">**ULONG**: Unsigned long type.</span></span> <span data-ttu-id="c4059-131">Bu tür 32 bitlik işaretsiz verileri desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="c4059-131">This type must support 32-bit unsigned  data.</span></span>
<span data-ttu-id="c4059-132">**VOID**: derleyicinin VOID türüne neredeyse her zaman eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="c4059-132">**VOID**: Almost always equivalent to the compiler's void type.</span></span>  
<span data-ttu-id="c4059-133">**Char**: genellikle standart 8 bitlik bir karakter türüdür.</span><span class="sxs-lookup"><span data-stu-id="c4059-133">**CHAR**: Most often a standard 8-bit character type.</span></span>  

<span data-ttu-id="c4059-134">Ek veri türleri, Azure RTOS NetX Duo kaynağı içinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4059-134">Additional data types are used within the Azure RTOS NetX Duo source.</span></span> <span data-ttu-id="c4059-135">Bunlar, ***tx_port. h** _ veya _ *_nx_port. h_** dosyalarında konumlardır.</span><span class="sxs-lookup"><span data-stu-id="c4059-135">They are located in either the ***tx_port.h** _ or _ *_nx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="c4059-136">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="c4059-136">Customer Support Center</span></span>

<span data-ttu-id="c4059-137">Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin.</span><span class="sxs-lookup"><span data-stu-id="c4059-137">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="c4059-138">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:</span><span class="sxs-lookup"><span data-stu-id="c4059-138">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="c4059-139">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="c4059-139">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="c4059-140">Uygulamada ve/veya Azure RTOS NetX Duo üzerinde yapılan tüm değişikliklerin ayrıntılı bir açıklaması ve bundan önce sorun.</span><span class="sxs-lookup"><span data-stu-id="c4059-140">A detailed description of any changes to the application and/or Azure RTOS NetX Duo that preceded the problem.</span></span>
3. <span data-ttu-id="c4059-141">_Tx_version_id ve _nx_version_id dizelerinin içerikleri, dağılımının tx_port. h ve nx_port. h dosyalarında bulunur.</span><span class="sxs-lookup"><span data-stu-id="c4059-141">The contents of the _tx_version_id and _nx_version_id strings found in the tx_port.h and nx_port.h files of your distribution.</span></span> <span data-ttu-id="c4059-142">Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4059-142">These strings will provide us valuable information regarding your run- time environment.</span></span>
4. <span data-ttu-id="c4059-143">Aşağıdaki ULONG değişkenlerinin RAM 'ine ait içerikler:</span><span class="sxs-lookup"><span data-stu-id="c4059-143">The contents in RAM of the following ULONG variables:</span></span>

    <span data-ttu-id="c4059-144">**_tx_build_options**</span><span class="sxs-lookup"><span data-stu-id="c4059-144">**_tx_build_options**</span></span>

    <span data-ttu-id="c4059-145">**_nx_system_build_options1**</span><span class="sxs-lookup"><span data-stu-id="c4059-145">**_nx_system_build_options1**</span></span>

    <span data-ttu-id="c4059-146">**_nx_system_build_options2**</span><span class="sxs-lookup"><span data-stu-id="c4059-146">**_nx_system_build_options2**</span></span>

    <span data-ttu-id="c4059-147">**_nx_system_build_options3**</span><span class="sxs-lookup"><span data-stu-id="c4059-147">**_nx_system_build_options3**</span></span>

    <span data-ttu-id="c4059-148">**_nx_system_build_options4**</span><span class="sxs-lookup"><span data-stu-id="c4059-148">**_nx_system_build_options4**</span></span>

    <span data-ttu-id="c4059-149">**_nx_system_build_options5**</span><span class="sxs-lookup"><span data-stu-id="c4059-149">**_nx_system_build_options5**</span></span>

    <span data-ttu-id="c4059-150">Bu değişkenler, Azure RTOS ThreadX ve Azure RTOS NetX Duo kitaplıklarının nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.</span><span class="sxs-lookup"><span data-stu-id="c4059-150">These variables will give us information on how your Azure RTOS ThreadX and Azure RTOS NetX Duo libraries were built.</span></span>

5. <span data-ttu-id="c4059-151">Sorun algılandıktan hemen sonra yakalanan bir izleme arabelleği.</span><span class="sxs-lookup"><span data-stu-id="c4059-151">A trace buffer captured immediately after the problem was detected.</span></span> <span data-ttu-id="c4059-152">Bu, TX_ENABLE_EVENT_TRACE ile Azure RTOS ThreadX ve Azure RTOS NetX Duo kitaplıkları oluşturup izleme arabelleği bilgileriyle tx_trace_enable çağırarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c4059-152">This is accomplished by building the Azure RTOS ThreadX and Azure RTOS NetX Duo libraries with TX_ENABLE_EVENT_TRACE and calling tx_trace_enable with the trace buffer information.</span></span>
