---
title: Azure RTOS NetX Kullanıcı Kılavuzu hakkında
description: Bu kılavuz, Microsoft yüksek performanslı ağ yığını olan Azure RTOS NetX hakkında kapsamlı bilgiler içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8e1c23892c4360ddc8783b04ae8f23e371899f1d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826920"
---
# <a name="about-the-azure-rtos-netx-user-guide"></a><span data-ttu-id="05640-103">Azure RTOS NetX Kullanıcı Kılavuzu hakkında</span><span class="sxs-lookup"><span data-stu-id="05640-103">About The Azure RTOS NetX User Guide</span></span>

<span data-ttu-id="05640-104">Bu kılavuz, Microsoft yüksek performanslı ağ yığını olan Azure RTOS NetX hakkında kapsamlı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="05640-104">This guide contains comprehensive information about Azure RTOS NetX, the Microsoft high-performance network stack.</span></span>

<span data-ttu-id="05640-105">Temel ağ kavramlarıyla, Azure RTOS ThreadX ve C programlama diliyle tanıdık olan gömülü gerçek zamanlı yazılım geliştiricileri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="05640-105">It is intended for embedded real-time software developers familiar with basic networking concepts, Azure RTOS ThreadX, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="05640-106">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="05640-106">Organization</span></span>

<span data-ttu-id="05640-107">[Bölüm 1](chapter1.md) -Azure RTOS NETX 'i tanıtır</span><span class="sxs-lookup"><span data-stu-id="05640-107">[Chapter 1](chapter1.md) - Introduces Azure RTOS NetX</span></span>

<span data-ttu-id="05640-108">[Bölüm 2](chapter2.md) -Threadx uygulamanızla Azure RTOS NETX 'i yüklemek ve kullanmak için temel adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="05640-108">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS NetX with your ThreadX application.</span></span>

<span data-ttu-id="05640-109">[Bölüm 3](chapter3.md) -Azure RTOS NETX sistemine yönelik işlevsel bir genel bakış ve TCP/IP ağ standartları hakkında temel bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="05640-109">[Chapter 3](chapter3.md) - Provides a functional overview of the Azure RTOS NetX system and basic information about the TCP/IP networking standards.</span></span>

<span data-ttu-id="05640-110">[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS NETX 'e ait arabiriminin ayrıntılarını.</span><span class="sxs-lookup"><span data-stu-id="05640-110">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS NetX.</span></span>

<span data-ttu-id="05640-111">[Bölüm 5](chapter5.md) -Azure RTOS NETX için ağ sürücülerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="05640-111">[Chapter 5](chapter5.md) - Describes network drivers for Azure RTOS NetX.</span></span>

<span data-ttu-id="05640-112">[Ek A](appendix-a.md) -Azure RTOS NETX Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="05640-112">[Appendix A](appendix-a.md) - Azure RTOS NetX Services</span></span>

<span data-ttu-id="05640-113">[Ek B](appendix-b.md) -Azure RTOS NETX sabitleri</span><span class="sxs-lookup"><span data-stu-id="05640-113">[Appendix B](appendix-b.md) - Azure RTOS NetX Constants</span></span>

<span data-ttu-id="05640-114">[Ek C](appendix-c.md) -Azure RTOS NETX veri türleri</span><span class="sxs-lookup"><span data-stu-id="05640-114">[Appendix C](appendix-c.md) - Azure RTOS NetX Data Types</span></span>

<span data-ttu-id="05640-115">[Ek D](appendix-d.md) -BSD-Compatible yuvası API 'si</span><span class="sxs-lookup"><span data-stu-id="05640-115">[Appendix D](appendix-d.md) - BSD-Compatible Socket API</span></span>

<span data-ttu-id="05640-116">[Ek E](appendix-e.md) -ASCII grafik</span><span class="sxs-lookup"><span data-stu-id="05640-116">[Appendix E](appendix-e.md) - ASCII Chart</span></span>

## <a name="azure-rtos-netx-data-types"></a><span data-ttu-id="05640-117">Azure RTOS NetX veri türleri</span><span class="sxs-lookup"><span data-stu-id="05640-117">Azure RTOS NetX Data Types</span></span>

<span data-ttu-id="05640-118">Özel Azure RTOS NetX denetim yapısı veri türlerine ek olarak, Azure RTOS NetX hizmet çağrı arabirimlerinde kullanılan birkaç özel veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="05640-118">In addition to the custom Azure RTOS NetX control structure data types, there are several special data types that are used in Azure RTOS NetX service call interfaces.</span></span> <span data-ttu-id="05640-119">Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir.</span><span class="sxs-lookup"><span data-stu-id="05640-119">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="05640-120">Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır.</span><span class="sxs-lookup"><span data-stu-id="05640-120">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="05640-121">Tam uygulama ThreadX 'ten devralınır ve ThreadX dağıtımına dahil olan ***tx_port. h*** dosyasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="05640-121">The exact implementation is inherited from ThreadX and can be found in the ***tx_port.h*** file included in the ThreadX distribution.</span></span>

<span data-ttu-id="05640-122">Aşağıda, Azure RTOS NetX hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="05640-122">The following is a list of Azure RTOS NetX service call data types and their associated meanings:</span></span>

| <!-- -->    | <!-- -->    |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="05640-123">**U**</span><span class="sxs-lookup"><span data-stu-id="05640-123">**UINT**</span></span>  | <span data-ttu-id="05640-124">Temel işaretsiz tamsayı.</span><span class="sxs-lookup"><span data-stu-id="05640-124">Basic unsigned integer.</span></span> <span data-ttu-id="05640-125">Bu tür 32 bitlik işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir.</span><span class="sxs-lookup"><span data-stu-id="05640-125">This type must support 32-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span> |
| <span data-ttu-id="05640-126">**'TUR**</span><span class="sxs-lookup"><span data-stu-id="05640-126">**ULONG**</span></span> | <span data-ttu-id="05640-127">İmzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="05640-127">Unsigned long type.</span></span> <span data-ttu-id="05640-128">Bu tür 32 bitlik işaretsiz verileri desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="05640-128">This type must support 32-bit unsigned data.</span></span>                                                                      |
| <span data-ttu-id="05640-129">**Kağıt**</span><span class="sxs-lookup"><span data-stu-id="05640-129">**VOID**</span></span>  | <span data-ttu-id="05640-130">Derleyicinin void türüne neredeyse her zaman eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="05640-130">Almost always equivalent to the compiler's void type.</span></span>                                                                                 |
| <span data-ttu-id="05640-131">**CHAR**</span><span class="sxs-lookup"><span data-stu-id="05640-131">**CHAR**</span></span>  | <span data-ttu-id="05640-132">Genellikle standart 8 bitlik bir karakter türü.</span><span class="sxs-lookup"><span data-stu-id="05640-132">Most often a standard 8-bit character type.</span></span>                                                                                           |

<span data-ttu-id="05640-133">Ek veri türleri, Azure RTOS NetX kaynağı içinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="05640-133">Additional data types are used within the Azure RTOS NetX source.</span></span> <span data-ttu-id="05640-134">Bunlar, ***tx_port. h** _ veya _ *_nx_port. h_** dosyalarında konumlardır.</span><span class="sxs-lookup"><span data-stu-id="05640-134">They are located in either the ***tx_port.h** _ or _ *_nx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="05640-135">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="05640-135">Customer Support Center</span></span>

<span data-ttu-id="05640-136">Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin.</span><span class="sxs-lookup"><span data-stu-id="05640-136">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="05640-137">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:</span><span class="sxs-lookup"><span data-stu-id="05640-137">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="05640-138">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="05640-138">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>

2. <span data-ttu-id="05640-139">Uygulamada ve/veya Azure RTOS NetX üzerinde yapılan tüm değişikliklerin ayrıntılı bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="05640-139">A detailed description of any changes to the application and/or Azure RTOS NetX that preceded the problem.</span></span>

3. <span data-ttu-id="05640-140">**_Tx_version_id** ve **_nx_version_id** dizelerinin içerikleri, dağılımının **_tx_port. h_*_ ve _*_nx_port. h_** dosyalarında bulunur.</span><span class="sxs-lookup"><span data-stu-id="05640-140">The contents of the **_tx_version_id** and **_nx_version_id** strings found in the **_tx_port.h_*_ and _*_nx_port.h_** files of your distribution.</span></span> <span data-ttu-id="05640-141">Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="05640-141">These strings will provide us valuable information regarding your run-time environment.</span></span>

4. <span data-ttu-id="05640-142">Aşağıdaki **ulong** değişkenlerinin RAM 'ine ait içerikler:</span><span class="sxs-lookup"><span data-stu-id="05640-142">The contents in RAM of the following **ULONG** variables:</span></span>

    <span data-ttu-id="05640-143">**_tx_build_options**</span><span class="sxs-lookup"><span data-stu-id="05640-143">**_tx_build_options**</span></span>

    <span data-ttu-id="05640-144">**_nx_system_build_options1**</span><span class="sxs-lookup"><span data-stu-id="05640-144">**_nx_system_build_options1**</span></span>

    <span data-ttu-id="05640-145">**_nx_system_build_options2**</span><span class="sxs-lookup"><span data-stu-id="05640-145">**_nx_system_build_options2**</span></span>

    <span data-ttu-id="05640-146">**_nx_system_build_options3**</span><span class="sxs-lookup"><span data-stu-id="05640-146">**_nx_system_build_options3**</span></span>

    <span data-ttu-id="05640-147">**_nx_system_build_options4**</span><span class="sxs-lookup"><span data-stu-id="05640-147">**_nx_system_build_options4**</span></span>

    <span data-ttu-id="05640-148">**_nx_system_build_options5**</span><span class="sxs-lookup"><span data-stu-id="05640-148">**_nx_system_build_options5**</span></span>

    <span data-ttu-id="05640-149">Bu değişkenler, Azure RTOS ThreadX ve Azure RTOS NetX kitaplıklarının nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.</span><span class="sxs-lookup"><span data-stu-id="05640-149">These variables will give us information on how your Azure RTOS ThreadX and Azure RTOS NetX libraries were built.</span></span>

5. <span data-ttu-id="05640-150">Sorun algılandıktan hemen sonra yakalanan bir izleme arabelleği.</span><span class="sxs-lookup"><span data-stu-id="05640-150">A trace buffer captured immediately after the problem was detected.</span></span> <span data-ttu-id="05640-151">Bu, **TX_ENABLE_EVENT_TRACE** Ile Azure RTOS threadx ve Azure RTOS NETX kitaplıkları oluşturup izleme arabelleği bilgileriyle **tx_trace_enable** çağırarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="05640-151">This is accomplished by building the Azure RTOS ThreadX and Azure RTOS NetX libraries with **TX_ENABLE_EVENT_TRACE** and calling **tx_trace_enable** with the trace buffer information.</span></span> <span data-ttu-id="05640-152">Ayrıntılar için Azure RTOS TraceX Kullanıcı kılavuzuna bakın.</span><span class="sxs-lookup"><span data-stu-id="05640-152">Refer to the Azure RTOS TraceX User Guide for details.</span></span>
