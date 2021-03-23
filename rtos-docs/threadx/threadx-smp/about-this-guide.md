---
title: Bu Kılavuz Hakkında
description: Bu kılavuzda, Azure RTOS ThreadX SMP, Microsoft yüksek performanslı gömülü gerçek zamanlı çekirdek hakkında kapsamlı bilgiler sağlanmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2399666b5b4d7c34db50d539e200c90f06f7235f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825445"
---
# <a name="about-this-guide"></a><span data-ttu-id="d018a-103">Bu Kılavuz Hakkında</span><span class="sxs-lookup"><span data-stu-id="d018a-103">About This Guide</span></span>

<span data-ttu-id="d018a-104">Bu kılavuzda, Azure RTOS ThreadX SMP, Microsoft yüksek performanslı gömülü gerçek zamanlı çekirdek hakkında kapsamlı bilgiler sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d018a-104">This guide provides comprehensive information about Azure RTOS ThreadX SMP, the Microsoft high-performance embedded real-time kernel.</span></span>

<span data-ttu-id="d018a-105">Katıştırılmış gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d018a-105">It is intended for the embedded real-time software developer.</span></span> <span data-ttu-id="d018a-106">Geliştirici standart gerçek zamanlı işletim sistemi işlevleri ve C programlama diliyle tanıdık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="d018a-106">The developer should be familiar with standard real-time operating system functions and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="d018a-107">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="d018a-107">Organization</span></span>

| <span data-ttu-id="d018a-108">Ele</span><span class="sxs-lookup"><span data-stu-id="d018a-108">Chapter</span></span>       | <span data-ttu-id="d018a-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d018a-109">Overview</span></span>                    |
| ------------- | ---------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="d018a-110">**Bölüm 1**</span><span class="sxs-lookup"><span data-stu-id="d018a-110">**Chapter 1**</span></span> | <span data-ttu-id="d018a-111">ThreadX SMP ve gerçek zamanlı gömülü geliştirmeyle ilişkisi için temel bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="d018a-111">Provides a basic overview of ThreadX SMP and its relationship to real-time embedded development.</span></span>           |
| <span data-ttu-id="d018a-112">**Bölüm 2**</span><span class="sxs-lookup"><span data-stu-id="d018a-112">**Chapter 2**</span></span> | <span data-ttu-id="d018a-113">, Uygulamanıza yönelik olarak ThreadX SMP 'yi yüklemek ve kullanmak için temel adımları sağlar *.*</span><span class="sxs-lookup"><span data-stu-id="d018a-113">Gives the basic steps to install and use ThreadX SMP in your application right *out of the box*.</span></span>           |
| <span data-ttu-id="d018a-114">**Bölüm 3**</span><span class="sxs-lookup"><span data-stu-id="d018a-114">**Chapter 3**</span></span> | <span data-ttu-id="d018a-115">Yüksek performanslı gerçek zamanlı SMP çekirdeği olan ThreadX SMP 'nin işlevsel işleminde ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d018a-115">Describes in detail the functional operation of ThreadX SMP, the high-performance real-time SMP kernel.</span></span>    |
| <span data-ttu-id="d018a-116">**Bölüm 4**</span><span class="sxs-lookup"><span data-stu-id="d018a-116">**Chapter 4**</span></span> | <span data-ttu-id="d018a-117">Uygulamanın ThreadX SMP arabirimine ayrıntılarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d018a-117">Details the application’s interface to ThreadX SMP.</span></span>                                                        |
| <span data-ttu-id="d018a-118">**Bölüm 5**</span><span class="sxs-lookup"><span data-stu-id="d018a-118">**Chapter 5**</span></span> | <span data-ttu-id="d018a-119">ThreadX SMP uygulamaları için g/ç sürücüleri yazmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="d018a-119">Describes writing I/O drivers for ThreadX SMP applications.</span></span>                                                |
| <span data-ttu-id="d018a-120">**Bölüm 6**</span><span class="sxs-lookup"><span data-stu-id="d018a-120">**Chapter 6**</span></span> | <span data-ttu-id="d018a-121">Her ThreadX SMP işlemci desteği paketiyle birlikte sunulan tanıtım uygulamasını açıklar.</span><span class="sxs-lookup"><span data-stu-id="d018a-121">Describes the demonstration application that is supplied with every ThreadX SMP processor support package.</span></span> |
| <span data-ttu-id="d018a-122">**Ek A**</span><span class="sxs-lookup"><span data-stu-id="d018a-122">**Appendix A**</span></span> | <span data-ttu-id="d018a-123">ThreadX SMP API 'SI</span><span class="sxs-lookup"><span data-stu-id="d018a-123">ThreadX SMP API</span></span>        |
| <span data-ttu-id="d018a-124">**Ek B**</span><span class="sxs-lookup"><span data-stu-id="d018a-124">**Appendix B**</span></span> | <span data-ttu-id="d018a-125">ThreadX SMP sabitleri</span><span class="sxs-lookup"><span data-stu-id="d018a-125">ThreadX SMP constants</span></span>  |
| <span data-ttu-id="d018a-126">**Ek C**</span><span class="sxs-lookup"><span data-stu-id="d018a-126">**Appendix C**</span></span> | <span data-ttu-id="d018a-127">ThreadX SMP veri türleri</span><span class="sxs-lookup"><span data-stu-id="d018a-127">ThreadX SMP data types</span></span> |
| <span data-ttu-id="d018a-128">**Ek D**</span><span class="sxs-lookup"><span data-stu-id="d018a-128">**Appendix D**</span></span> | <span data-ttu-id="d018a-129">ASCII grafik</span><span class="sxs-lookup"><span data-stu-id="d018a-129">ASCII chart</span></span>            |

## <a name="guide-conventions"></a><span data-ttu-id="d018a-130">Kılavuz kuralları</span><span class="sxs-lookup"><span data-stu-id="d018a-130">Guide Conventions</span></span>

- <span data-ttu-id="d018a-131">*İtalik*  -  *yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.*</span><span class="sxs-lookup"><span data-stu-id="d018a-131">*Italics* - *typeface denotes book titles, emphasizes important words, and indicates variables.*</span></span>
- <span data-ttu-id="d018a-132">**Kalýn**  -  **yazı tipi dosya adlarını, anahtar sözcükleri gösterir ve önemli sözcükleri ve değişkenleri vurgular.**</span><span class="sxs-lookup"><span data-stu-id="d018a-132">**Boldface** - **typeface denotes file names, key words, and further emphasizes important words and variables.**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d018a-133">Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="d018a-133">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>

> [!WARNING]
> <span data-ttu-id="d018a-134">Uyarı sembolleri, geliştiricilerin önemli hatalara neden olabileceğinden kaçınmak için dikkatli olması gereken durumlara dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="d018a-134">Warning symbols draw attention to situations in which developers should take care to avoid because they could cause fatal errors.</span></span>

## <a name="threadx-smp-data-types"></a><span data-ttu-id="d018a-135">ThreadX SMP veri türleri</span><span class="sxs-lookup"><span data-stu-id="d018a-135">ThreadX SMP Data Types</span></span>

<span data-ttu-id="d018a-136">Özel ThreadX SMP denetim yapısı veri türlerine ek olarak, ThreadX SMP hizmeti çağrı arabirimlerinde kullanılan bir dizi özel veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="d018a-136">In addition to the custom ThreadX SMP control structure data types, there are a series of special data types that are used in ThreadX SMP service call interfaces.</span></span> <span data-ttu-id="d018a-137">Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir.</span><span class="sxs-lookup"><span data-stu-id="d018a-137">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="d018a-138">Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır.</span><span class="sxs-lookup"><span data-stu-id="d018a-138">This is done to insure portability between different C compilers.</span></span> <span data-ttu-id="d018a-139">Tam uygulama, dağıtım diskine dahil olan ***tx_port. h*** dosyasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="d018a-139">The exact implementation can be found in the ***tx_port.h*** file included on the distribution disk.</span></span>

<span data-ttu-id="d018a-140">Aşağıda, ThreadX SMP hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d018a-140">The following is a list of ThreadX SMP service call data types and their associated meanings:</span></span>

| <span data-ttu-id="d018a-141">Veri Türü</span><span class="sxs-lookup"><span data-stu-id="d018a-141">Data Type</span></span>          | <span data-ttu-id="d018a-142">Anlamı</span><span class="sxs-lookup"><span data-stu-id="d018a-142">Meaning</span></span>                                                          |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="d018a-143">**U**</span><span class="sxs-lookup"><span data-stu-id="d018a-143">**UINT**</span></span>  | <span data-ttu-id="d018a-144">Temel işaretsiz tamsayı.</span><span class="sxs-lookup"><span data-stu-id="d018a-144">Basic unsigned integer.</span></span> <span data-ttu-id="d018a-145">Bu tür 8 bit işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir.</span><span class="sxs-lookup"><span data-stu-id="d018a-145">This type must support 8-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span> |
| <span data-ttu-id="d018a-146">**'TUR**</span><span class="sxs-lookup"><span data-stu-id="d018a-146">**ULONG**</span></span> | <span data-ttu-id="d018a-147">İmzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="d018a-147">Unsigned long type.</span></span> <span data-ttu-id="d018a-148">Bu tür 32 bitlik işaretsiz verileri desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="d018a-148">This type must support 32-bit unsigned data.</span></span>                                                                     |
| <span data-ttu-id="d018a-149">**Kağıt**</span><span class="sxs-lookup"><span data-stu-id="d018a-149">**VOID**</span></span>  | <span data-ttu-id="d018a-150">Derleyicinin void türüne neredeyse her zaman eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="d018a-150">Almost always equivalent to the compiler’s void type.</span></span>                                                                                |
| <span data-ttu-id="d018a-151">**CHAR**</span><span class="sxs-lookup"><span data-stu-id="d018a-151">**CHAR**</span></span>  | <span data-ttu-id="d018a-152">Genellikle standart 8 bitlik bir karakter türü.</span><span class="sxs-lookup"><span data-stu-id="d018a-152">Most often a standard 8-bit character type.</span></span>                                                                                          |

<span data-ttu-id="d018a-153">Ek veri türleri, ThreadX SMP kaynağı içinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d018a-153">Additional data types are used within the ThreadX SMP source.</span></span> <span data-ttu-id="d018a-154">Bunlar ayrıca ***tx_port. h*** dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="d018a-154">They are also located in the ***tx_port.h*** file.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="d018a-155">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="d018a-155">Customer Support Center</span></span>

<span data-ttu-id="d018a-156">Destek e-postası: [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) Web sayfası: Azure.com/RTOS</span><span class="sxs-lookup"><span data-stu-id="d018a-156">Support email: [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) Web page: azure.com/rtos</span></span>

### <a name="latest-product-information"></a><span data-ttu-id="d018a-157">En son ürün bilgileri</span><span class="sxs-lookup"><span data-stu-id="d018a-157">Latest Product Information</span></span>

<span data-ttu-id="d018a-158">Azure.com/rtos Web sitesini ziyaret edin ve en son ThreadX SMP ürün sürümleri hakkında bilgiler de dahil olmak üzere en son çevrimiçi destek bilgilerini bulmak için "destek" menü seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d018a-158">Visit the azure.com/rtos web site and select the “Support” menu option to find the latest online support information, including information about the latest ThreadX SMP product releases.</span></span>

### <a name="what-we-need-from-you"></a><span data-ttu-id="d018a-159">Sizin için gerekenler</span><span class="sxs-lookup"><span data-stu-id="d018a-159">What We Need From You</span></span>

<span data-ttu-id="d018a-160">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:</span><span class="sxs-lookup"><span data-stu-id="d018a-160">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="d018a-161">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="d018a-161">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="d018a-162">Uygulamanın ve/veya ThreadX SMP değişikliklerinin bundan önce sorunun ayrıntılı bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="d018a-162">A detailed description of any changes to the application and/or ThreadX SMP that preceded the problem.</span></span>
3. <span data-ttu-id="d018a-163">***_Tx_version_id** _ dizesinin içeriği, dağılımının _ *_tx_port. h_** dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="d018a-163">The contents of the ***_tx_version_id** _ string found in the _ *_tx_port.h_** file of your distribution.</span></span> <span data-ttu-id="d018a-164">Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="d018a-164">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="d018a-165">***_Tx_build_options*** ulong değişkeninin RAM 'e ait içerik.</span><span class="sxs-lookup"><span data-stu-id="d018a-165">The contents in RAM of the ***_tx_build_options*** ULONG variable.</span></span> <span data-ttu-id="d018a-166">Bu değişken, ThreadX SMP Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.</span><span class="sxs-lookup"><span data-stu-id="d018a-166">This variable will give us information on how your ThreadX SMP library was built.</span></span>

### <a name="where-to-send-comments-about-this-guide"></a><span data-ttu-id="d018a-167">Bu kılavuzla Ilgili yorumların nereye gönderileceği</span><span class="sxs-lookup"><span data-stu-id="d018a-167">Where to Send Comments About This Guide</span></span>

<span data-ttu-id="d018a-168">[azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com)Konu satırına "ThreadX SMP Kullanıcı Kılavuzu" yazın ve müşteri destek merkezi 'ndeki tüm yorumları ve önerileri e-posta ile yapın.</span><span class="sxs-lookup"><span data-stu-id="d018a-168">Email any comments and suggestions to the Customer Support Center at [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) Enter “ThreadX SMP User Guide” in the subject line.</span></span>
