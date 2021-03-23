---
title: Azure RTOS FileX Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un yüksek performanslı gerçek zamanlı dosya sistemi olan Azure RTOS FileX hakkında kapsamlı bilgiler içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0ebcebdd2b227ed8d9ccf8b3078b716f90f35bef
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825559"
---
# <a name="about-this-filex-user-guide"></a><span data-ttu-id="df2c6-103">Bu FileX Kullanıcı Kılavuzu hakkında</span><span class="sxs-lookup"><span data-stu-id="df2c6-103">About This FileX User Guide</span></span>

<span data-ttu-id="df2c6-104">Bu kılavuz, Microsoft 'un yüksek performanslı ve gerçek zamanlı katıştırılmış dosya sistemi olan Azure RTOS FileX hakkında kapsamlı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-104">This guide contains comprehensive information about Azure RTOS FileX, the high-performance, real-time embedded file system from Microsoft.</span></span> <span data-ttu-id="df2c6-105">Bu kılavuzdan en iyi şekilde kazanmak için standart gerçek zamanlı işletim sistemi işlevleri, FAT dosya sistemi hizmetleri ve C programlama dili hakkında bilgi sahibi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-105">To gain the most from this guide, you should be familiar with standard real-time operating system functions, FAT file system services, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="df2c6-106">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="df2c6-106">Organization</span></span>

<span data-ttu-id="df2c6-107">[Bölüm 1](chapter1.md) -Azure RTOS FileX 'i tanıtır</span><span class="sxs-lookup"><span data-stu-id="df2c6-107">[Chapter 1](chapter1.md) - Introduces Azure RTOS FileX</span></span>

<span data-ttu-id="df2c6-108">[Bölüm 2](chapter2.md) -Azure RTOS threadx uygulamanızla Azure RTOS FileX 'i yüklemek ve kullanmak için temel adımları sağlar</span><span class="sxs-lookup"><span data-stu-id="df2c6-108">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS FileX with your Azure RTOS ThreadX application</span></span>

<span data-ttu-id="df2c6-109">[Bölüm 3](chapter3.md) -Azure RTOS FileX SISTEMINE ve FAT dosya sistemi biçimleriyle ilgili temel bilgilere yönelik işlevsel bir genel bakış sağlar</span><span class="sxs-lookup"><span data-stu-id="df2c6-109">[Chapter 3](chapter3.md) - Provides a functional overview of the Azure RTOS FileX system and basic information about FAT file system formats</span></span>

<span data-ttu-id="df2c6-110">[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS FileX 'e ait arabiriminin ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="df2c6-110">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS FileX</span></span>

<span data-ttu-id="df2c6-111">[Bölüm 5](chapter5.md) -sağlanan Azure RTOS FILEX RAM sürücüsünü ve kendi özel Azure RTOS FileX sürücülerinizi yazmayı açıklar</span><span class="sxs-lookup"><span data-stu-id="df2c6-111">[Chapter 5](chapter5.md) - Describes the supplied Azure RTOS FileX RAM driver and how to write your own custom Azure RTOS FileX drivers</span></span>

<span data-ttu-id="df2c6-112">[Bölüm 6](chapter6.md) -Azure RTOS FileX hata dayanıklı modülünü açıklar</span><span class="sxs-lookup"><span data-stu-id="df2c6-112">[Chapter 6](chapter6.md) - Describes the Azure RTOS FileX Fault Tolerant Module</span></span>

<span data-ttu-id="df2c6-113">[Ek A](appendix-a.md) -Azure RTOS FileX Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="df2c6-113">[Appendix A](appendix-a.md) - Azure RTOS FileX Services</span></span>

<span data-ttu-id="df2c6-114">[Ek B](appendix-b.md) -Azure RTOS FileX sabitleri</span><span class="sxs-lookup"><span data-stu-id="df2c6-114">[Appendix B](appendix-b.md) - Azure RTOS FileX Constants</span></span>

<span data-ttu-id="df2c6-115">[Ek C](appendix-c.md) -Azure RTOS FileX veri türleri</span><span class="sxs-lookup"><span data-stu-id="df2c6-115">[Appendix C](appendix-c.md) - Azure RTOS FileX Data Types</span></span>

<span data-ttu-id="df2c6-116">[Ek D](appendix-d.md) -ASCII grafik</span><span class="sxs-lookup"><span data-stu-id="df2c6-116">[Appendix D](appendix-d.md) - ASCII Chart</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="df2c6-117">Kılavuz kuralları</span><span class="sxs-lookup"><span data-stu-id="df2c6-117">Guide Conventions</span></span>

<span data-ttu-id="df2c6-118">*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-118">*Italics* - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="df2c6-119">**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.</span><span class="sxs-lookup"><span data-stu-id="df2c6-119">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!NOTE]
> <span data-ttu-id="df2c6-120">Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="df2c6-120">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df2c6-121">Uyarı sembolleri, önemli hatalara neden olabileceğinden, geliştiricilerin oluşmaması gereken durumlara dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="df2c6-121">Warning symbols draw attention to situations that developers should avoid because they could cause fatal errors.</span></span>

## <a name="filex-data-types"></a><span data-ttu-id="df2c6-122">FileX veri türleri</span><span class="sxs-lookup"><span data-stu-id="df2c6-122">FileX Data Types</span></span>

<span data-ttu-id="df2c6-123">Özel Azure RTOS FileX denetim yapısı veri türlerine ek olarak, Azure RTOS FileX hizmet çağrı arabirimlerinde kullanılan bir dizi özel veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="df2c6-123">In addition to the custom Azure RTOS FileX control structure data types, there is a series of special data types that are used in Azure RTOS FileX service call interfaces.</span></span> <span data-ttu-id="df2c6-124">Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-124">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="df2c6-125">Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır.</span><span class="sxs-lookup"><span data-stu-id="df2c6-125">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="df2c6-126">Tam uygulama Azure RTOS ThreadX 'ten devralınmıştır ve Azure RTOS ThreadX dağıtımına eklenen tx_port. h dosyasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-126">The exact implementation is inherited from Azure RTOS ThreadX and can be found in the tx_port.h file included in the Azure RTOS ThreadX distribution.</span></span>

<span data-ttu-id="df2c6-127">Aşağıda, Azure RTOS FileX hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-127">The following is a list of Azure RTOS FileX service call data types and their associated meanings.</span></span>
| <span data-ttu-id="df2c6-128">Tür</span><span class="sxs-lookup"><span data-stu-id="df2c6-128">Type</span></span>  | <span data-ttu-id="df2c6-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="df2c6-129">Description</span></span>  |
|---|---|
| <span data-ttu-id="df2c6-130">**U**</span><span class="sxs-lookup"><span data-stu-id="df2c6-130">**UINT**</span></span> | <span data-ttu-id="df2c6-131">Temel işaretsiz tamsayı.</span><span class="sxs-lookup"><span data-stu-id="df2c6-131">Basic unsigned integer.</span></span> <span data-ttu-id="df2c6-132">Bu tür 8 bit işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-132">This type must support 8-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span> |
| <span data-ttu-id="df2c6-133">**'TUR**</span><span class="sxs-lookup"><span data-stu-id="df2c6-133">**ULONG**</span></span> | <span data-ttu-id="df2c6-134">İmzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="df2c6-134">Unsigned long type.</span></span> <span data-ttu-id="df2c6-135">Bu tür 32 bitlik işaretsiz verileri desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-135">This type must support 32-bit unsigned data.</span></span> |
| <span data-ttu-id="df2c6-136">**Kağıt**</span><span class="sxs-lookup"><span data-stu-id="df2c6-136">**VOID**</span></span> | <span data-ttu-id="df2c6-137">Derleyicinin void türüne neredeyse her zaman eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="df2c6-137">Almost always equivalent to the compiler’s void type.</span></span> |
| <span data-ttu-id="df2c6-138">**CHAR**</span><span class="sxs-lookup"><span data-stu-id="df2c6-138">**CHAR**</span></span> | <span data-ttu-id="df2c6-139">Genellikle standart 8 bitlik bir karakter türü.</span><span class="sxs-lookup"><span data-stu-id="df2c6-139">Most often a standard 8-bit character type.</span></span> |
| <span data-ttu-id="df2c6-140">**ULONG64**</span><span class="sxs-lookup"><span data-stu-id="df2c6-140">**ULONG64**</span></span> | <span data-ttu-id="df2c6-141">64-bit işaretsiz tamsayı veri türü.</span><span class="sxs-lookup"><span data-stu-id="df2c6-141">64-bit unsigned integer data type.</span></span> |

<span data-ttu-id="df2c6-142">Ek veri türleri, FileX kaynağı içinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="df2c6-142">Additional data types are used within the FileX source.</span></span> <span data-ttu-id="df2c6-143">Bunlar, ***tx_port. h** _ veya _ *_fx_port. h_** dosyalarında konumlardır.</span><span class="sxs-lookup"><span data-stu-id="df2c6-143">They are located in either the ***tx_port.h** _ or _ *_fx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="df2c6-144">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="df2c6-144">Customer Support Center</span></span>

<span data-ttu-id="df2c6-145">Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin.</span><span class="sxs-lookup"><span data-stu-id="df2c6-145">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="df2c6-146">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin.</span><span class="sxs-lookup"><span data-stu-id="df2c6-146">Please supply us with the following information in an email message so we can more efficiently resolve your support request.</span></span>

1. <span data-ttu-id="df2c6-147">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="df2c6-147">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="df2c6-148">Uygulamada ve/veya FileX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.</span><span class="sxs-lookup"><span data-stu-id="df2c6-148">A detailed description of any changes to the application and/or FileX that preceded the problem.</span></span>
3. <span data-ttu-id="df2c6-149">_Tx_version_id ve fx_version_id dizelerinin içeriği, _**tx_port. h**_ ve _ \*_fx_port. h_\*\*, dağıtım dosyalarınızın dosyalarında bulunur.</span><span class="sxs-lookup"><span data-stu-id="df2c6-149">The contents of the _tx_version_id and _fx_version_id strings found in the \***tx_port.h**_ and _ *_fx_port.h_*\* files of your distribution.</span></span> <span data-ttu-id="df2c6-150">Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="df2c6-150">These strings will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="df2c6-151">Aşağıdaki **ulong** değişkenlerinin RAM 'e ait içerik.</span><span class="sxs-lookup"><span data-stu-id="df2c6-151">The contents in RAM of the following **ULONG** variables.</span></span> <span data-ttu-id="df2c6-152">Bu değişkenler, ThreadX ve FileX kitaplıklarınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir:</span><span class="sxs-lookup"><span data-stu-id="df2c6-152">These variables will give us information on how your ThreadX and FileX libraries were built:</span></span>

    <span data-ttu-id="df2c6-153">**_tx_build_options**</span><span class="sxs-lookup"><span data-stu-id="df2c6-153">**_tx_build_options**</span></span>

    <span data-ttu-id="df2c6-154">**_fx_system_build_options1**</span><span class="sxs-lookup"><span data-stu-id="df2c6-154">**_fx_system_build_options1**</span></span>

    <span data-ttu-id="df2c6-155">**_fx_system_build_options2**</span><span class="sxs-lookup"><span data-stu-id="df2c6-155">**_fx_system_build_options2**</span></span>

    <span data-ttu-id="df2c6-156">**_fx_system_build_options3**</span><span class="sxs-lookup"><span data-stu-id="df2c6-156">**_fx_system_build_options3**</span></span>
