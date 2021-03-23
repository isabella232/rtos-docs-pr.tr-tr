---
title: Azure RTOS GUIX Kullanıcı Kılavuzu
description: Bu kılavuzda, Microsoft 'un yüksek performanslı GUI ürünü olan Azure RTOS Gux hakkında kapsamlı bilgiler yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: b7af0fba59b599c9c8db3ab80a3271eacfd11992
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827292"
---
# <a name="about-guix-user-guide"></a><span data-ttu-id="92d22-103">GUX Kullanıcı Kılavuzu hakkında</span><span class="sxs-lookup"><span data-stu-id="92d22-103">About GUIX User Guide</span></span>

<span data-ttu-id="92d22-104">Bu kılavuzda, Microsoft 'un yüksek performanslı GUI ürünü olan Azure RTOS Gux hakkında kapsamlı bilgiler yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="92d22-104">This guide contains comprehensive information about Azure RTOS GUIX, the high-performance GUI product from Microsoft.</span></span> <span data-ttu-id="92d22-105">Temel GUI kavramlarını, Azure RTOS ThreadX ve C programlama dilini bilen, yerleşik gerçek zamanlı yazılım geliştiricileri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="92d22-105">It is intended for embedded real-time software developers familiar with basic GUI concepts, Azure RTOS ThreadX, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="92d22-106">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="92d22-106">Organization</span></span>

[<span data-ttu-id="92d22-107">Bölüm 1-Azure RTOS Gux 'e giriş</span><span class="sxs-lookup"><span data-stu-id="92d22-107">Chapter 1 - Introduction to Azure RTOS GUIX</span></span>](chapter-1.md)

[<span data-ttu-id="92d22-108">Bölüm 2-Azure RTOS Gux 'i yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="92d22-108">Chapter 2 - Installation and use of Azure RTOS GUIX</span></span>](chapter-2.md)

[<span data-ttu-id="92d22-109">Bölüm 3-Azure RTOS Gux 'e Işlevsel genel bakış</span><span class="sxs-lookup"><span data-stu-id="92d22-109">Chapter 3 - Functional Overview of Azure RTOS GUIX</span></span>](chapter-3.md)

[<span data-ttu-id="92d22-110">Bölüm 4-Azure RTOS GUıDX hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="92d22-110">Chapter 4 - Description of Azure RTOS GUIX Services</span></span>](chapter-4.md)

[<span data-ttu-id="92d22-111">Bölüm 5-Azure RTOS Gux görüntüleme sürücüleri</span><span class="sxs-lookup"><span data-stu-id="92d22-111">Chapter 5 - Azure RTOS GUIX Display Drivers</span></span>](chapter-5.md)  

[<span data-ttu-id="92d22-112">Azure RTOS Gux örneği</span><span class="sxs-lookup"><span data-stu-id="92d22-112">Azure RTOS GUIX Example</span></span>](guix-example.md)

[<span data-ttu-id="92d22-113">Ek A-Azure RTOS Gux renk tanımları</span><span class="sxs-lookup"><span data-stu-id="92d22-113">Appendix A - Azure RTOS GUIX Color Definitions</span></span>](appendix-a.md)

[<span data-ttu-id="92d22-114">Ek B-Azure RTOS Gux renk biçimleri</span><span class="sxs-lookup"><span data-stu-id="92d22-114">Appendix B - Azure RTOS GUIX Color Formats</span></span>](appendix-b.md)

[<span data-ttu-id="92d22-115">Ek C-Azure RTOS Gux pencere öğesi stilleri</span><span class="sxs-lookup"><span data-stu-id="92d22-115">Appendix C - Azure RTOS GUIX Widget Styles</span></span>](appendix-c.md)

[<span data-ttu-id="92d22-116">Ek D-Azure RTOS Gux fırçası, tuval ve gradyan öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="92d22-116">Appendix D - Azure RTOS GUIX Brush, Canvas and Gradient Attributes</span></span>](appendix-d.md)

[<span data-ttu-id="92d22-117">Ek E-Azure RTOS Gux olay açıklaması</span><span class="sxs-lookup"><span data-stu-id="92d22-117">Appendix E - Azure RTOS GUIX Event Description</span></span>](appendix-e.md)

[<span data-ttu-id="92d22-118">Ek F-Azure RTOS Gux RTOS bağlama hizmetleri</span><span class="sxs-lookup"><span data-stu-id="92d22-118">Appendix F - Azure RTOS GUIX RTOS Binding Services</span></span>](appendix-f.md)

[<span data-ttu-id="92d22-119">Ek G-Azure RTOS Gux yazı tipi yapısı</span><span class="sxs-lookup"><span data-stu-id="92d22-119">Appendix G - Azure RTOS GUIX Font Structure</span></span>](appendix-g.md)

[<span data-ttu-id="92d22-120">Ek H-Azure RTOS Gux Build-Time yapılandırma bayrakları</span><span class="sxs-lookup"><span data-stu-id="92d22-120">Appendix H - Azure RTOS GUIX Build-Time Configuration flags</span></span>](appendix-h.md)

[<span data-ttu-id="92d22-121">Ek ı-Azure RTOS Gux bilgi yapıları</span><span class="sxs-lookup"><span data-stu-id="92d22-121">Appendix I - Azure RTOS GUIX Information Structures</span></span>](appendix-i.md)

## <a name="guide-conventions"></a><span data-ttu-id="92d22-122">Kılavuz kuralları</span><span class="sxs-lookup"><span data-stu-id="92d22-122">Guide Conventions</span></span>

<span data-ttu-id="92d22-123">*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="92d22-123">*Italics* - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="92d22-124">**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.</span><span class="sxs-lookup"><span data-stu-id="92d22-124">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92d22-125">Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.</span><span class="sxs-lookup"><span data-stu-id="92d22-125">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>

## <a name="azure-rtos-guix-data-types"></a><span data-ttu-id="92d22-126">Azure RTOS Gux veri türleri</span><span class="sxs-lookup"><span data-stu-id="92d22-126">Azure RTOS GUIX Data Types</span></span>

<span data-ttu-id="92d22-127">Özel Azure RTOS Gux denetim yapısı veri türlerine ek olarak, Azure RTOS Gux hizmet çağrı arabirimlerinde kullanılan birkaç özel veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="92d22-127">In addition to the custom Azure RTOS GUIX control structure data types, there are several special data types that are used in Azure RTOS GUIX service call interfaces.</span></span> <span data-ttu-id="92d22-128">Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir.</span><span class="sxs-lookup"><span data-stu-id="92d22-128">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="92d22-129">Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır.</span><span class="sxs-lookup"><span data-stu-id="92d22-129">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="92d22-130">Tam uygulama ThreadX 'ten devralınır ve ThreadX dağıtımına dahil olan ***tx_port. h*** dosyasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="92d22-130">The exact implementation is inherited from ThreadX and can be found in the ***tx_port.h*** file included in the ThreadX distribution.</span></span>

<span data-ttu-id="92d22-131">Aşağıda, Azure RTOS Gux hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="92d22-131">The following is a list of Azure RTOS GUIX service call data types and their associated meanings:</span></span>

| <!-- --> | <!-- --> |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="92d22-132">**U**</span><span class="sxs-lookup"><span data-stu-id="92d22-132">**UINT**</span></span>             | <span data-ttu-id="92d22-133">Temel işaretsiz tamsayı.</span><span class="sxs-lookup"><span data-stu-id="92d22-133">Basic unsigned integer.</span></span> <span data-ttu-id="92d22-134">Bu tür, en uygun imzasız veri türüyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="92d22-134">This type is mapped to the most convenient unsigned data type.</span></span>                                |
| <span data-ttu-id="92d22-135">**INT**</span><span class="sxs-lookup"><span data-stu-id="92d22-135">**INT**</span></span>              | <span data-ttu-id="92d22-136">Temel işaretli tamsayı.</span><span class="sxs-lookup"><span data-stu-id="92d22-136">Basic signed integer.</span></span> <span data-ttu-id="92d22-137">Bu tür, en uygun imzalı veri türüyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="92d22-137">This type is mapped to the most convenient signed data type.</span></span>                                    |
| <span data-ttu-id="92d22-138">**'TUR**</span><span class="sxs-lookup"><span data-stu-id="92d22-138">**ULONG**</span></span>            | <span data-ttu-id="92d22-139">İmzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="92d22-139">Unsigned long type.</span></span> <span data-ttu-id="92d22-140">Bu tür 32 bitlik işaretsiz verileri desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="92d22-140">This type must support 32-bit unsigned data.</span></span>                                                      |
| <span data-ttu-id="92d22-141">**Kağıt**</span><span class="sxs-lookup"><span data-stu-id="92d22-141">**VOID**</span></span>             | <span data-ttu-id="92d22-142">Derleyicinin void türüne neredeyse her zaman eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="92d22-142">Almost always equivalent to the compiler’s void type.</span></span>                                                                 |
| <span data-ttu-id="92d22-143">**GX_CHAR**</span><span class="sxs-lookup"><span data-stu-id="92d22-143">**GX_CHAR**</span></span>         | <span data-ttu-id="92d22-144">En yaygın olarak, derleyici tarafından tanımlanan char türü olarak yazın.</span><span class="sxs-lookup"><span data-stu-id="92d22-144">Most often typedefed as the compiler defined char type.</span></span>                                                               |
| <span data-ttu-id="92d22-145">**GX_BYTE**</span><span class="sxs-lookup"><span data-stu-id="92d22-145">**GX_BYTE**</span></span>          | <span data-ttu-id="92d22-146">8 bit imzalı tür.</span><span class="sxs-lookup"><span data-stu-id="92d22-146">8-bit signed type.</span></span>                                                                                                    |
| <span data-ttu-id="92d22-147">**GX_UBYTE**</span><span class="sxs-lookup"><span data-stu-id="92d22-147">**GX_UBYTE**</span></span>         | <span data-ttu-id="92d22-148">8 bit işaretsiz tür.</span><span class="sxs-lookup"><span data-stu-id="92d22-148">8-bit unsigned type.</span></span>                                                                                                  |
| <span data-ttu-id="92d22-149">**GX_VALUE**</span><span class="sxs-lookup"><span data-stu-id="92d22-149">**GX_VALUE**</span></span>        | <span data-ttu-id="92d22-150">16 veya 32 bit imzalı tür.</span><span class="sxs-lookup"><span data-stu-id="92d22-150">16 or 32 bit signed type.</span></span> <span data-ttu-id="92d22-151">Hedef sistemde en iyi performans için gereken şekilde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="92d22-151">Defined as needed for best performance on the target system.</span></span>                                |
| <span data-ttu-id="92d22-152">**GX_FIXED_VAL**</span><span class="sxs-lookup"><span data-stu-id="92d22-152">**GX_FIXED_VAL**</span></span>   | <span data-ttu-id="92d22-153">Sabit noktalı sayısal veri türü.</span><span class="sxs-lookup"><span data-stu-id="92d22-153">Fixed point numeric data type.</span></span>                                                                                        |
| <span data-ttu-id="92d22-154">**GX_RESOURCE_ID**</span><span class="sxs-lookup"><span data-stu-id="92d22-154">**GX_RESOURCE_ID**</span></span> | <span data-ttu-id="92d22-155">İmzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="92d22-155">Unsigned long type.</span></span>                                                                                                   |
| <span data-ttu-id="92d22-156">**GX_COLOR**</span><span class="sxs-lookup"><span data-stu-id="92d22-156">**GX_COLOR**</span></span>        | <span data-ttu-id="92d22-157">İmzasız Long türü.</span><span class="sxs-lookup"><span data-stu-id="92d22-157">Unsigned long type.</span></span>                                                                                                   |
| <span data-ttu-id="92d22-158">**GX_STRING**</span><span class="sxs-lookup"><span data-stu-id="92d22-158">**GX_STRING**</span></span>       | <span data-ttu-id="92d22-159">GX_CHAR \* gx_string_ptr ve UINT gx_string_length içeren yapı.</span><span class="sxs-lookup"><span data-stu-id="92d22-159">Structure containing GX_CHAR \*gx_string_ptr and UINT gx_string_length.</span></span>                                          |
| <span data-ttu-id="92d22-160">**GX_POINT**</span><span class="sxs-lookup"><span data-stu-id="92d22-160">**GX_POINT**</span></span>        | <span data-ttu-id="92d22-161">Gx_point_x ve gx_point_y içeren yapı.</span><span class="sxs-lookup"><span data-stu-id="92d22-161">Structure containing gx_point_x and gx_point_y.</span></span>                                                                   |
| <span data-ttu-id="92d22-162">**GX_RECTANGLE**</span><span class="sxs-lookup"><span data-stu-id="92d22-162">**GX_RECTANGLE**</span></span>    | <span data-ttu-id="92d22-163">Gx_rectangle_left, gx_rectangle_top, gx_rectangle_right ve gx_rectangle_bottom alanları içeren yapı.</span><span class="sxs-lookup"><span data-stu-id="92d22-163">Structure containing gx_rectangle_left, gx_rectangle_top, gx_rectangle_right, and gx_rectangle_bottom fields.</span></span> |
| <span data-ttu-id="92d22-164">**GX_GLYPH**</span><span class="sxs-lookup"><span data-stu-id="92d22-164">**GX_GLYPH**</span></span>        | <span data-ttu-id="92d22-165">Glif ölçümleri içeren yapı.</span><span class="sxs-lookup"><span data-stu-id="92d22-165">Structure containing glyph metrics.</span></span>                                                                                   |
| <span data-ttu-id="92d22-166">**GX_FONT**</span><span class="sxs-lookup"><span data-stu-id="92d22-166">**GX_FONT**</span></span>         | <span data-ttu-id="92d22-167">Yazı tipi ölçümlerini içeren yapı.</span><span class="sxs-lookup"><span data-stu-id="92d22-167">Structure containing font metrics.</span></span>                                                                                    |
| <span data-ttu-id="92d22-168">**GX_BRUSH**</span><span class="sxs-lookup"><span data-stu-id="92d22-168">**GX_BRUSH**</span></span>        | <span data-ttu-id="92d22-169">Fırça ölçümlerini içeren yapı.</span><span class="sxs-lookup"><span data-stu-id="92d22-169">Structure containing brush metrics.</span></span>                                                                               |
<span data-ttu-id="92d22-170">**GX_PIXELMAP**</span><span class="sxs-lookup"><span data-stu-id="92d22-170">**GX_PIXELMAP**</span></span>       | <span data-ttu-id="92d22-171">Pixelmap ölçümlerini içeren yapı.</span><span class="sxs-lookup"><span data-stu-id="92d22-171">Structure containing pixelmap metrics.</span></span>

<span data-ttu-id="92d22-172">Ek veri türleri, Azure RTOS Gux kaynağı içinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="92d22-172">Additional data types are used within the Azure RTOS GUIX source.</span></span> <span data-ttu-id="92d22-173">Bunlar, ***tx_port. h** _ veya _ *_gx_port. h_** dosyalarında konumlardır.</span><span class="sxs-lookup"><span data-stu-id="92d22-173">They are located in either the ***tx_port.h** _ or _ *_gx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="92d22-174">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="92d22-174">Customer Support Center</span></span>

<span data-ttu-id="92d22-175">Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin.</span><span class="sxs-lookup"><span data-stu-id="92d22-175">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="92d22-176">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:</span><span class="sxs-lookup"><span data-stu-id="92d22-176">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="92d22-177">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="92d22-177">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>

2. <span data-ttu-id="92d22-178">Uygulamada ve/veya Azure RTOS Gux ' te yapılan tüm değişikliklerin ayrıntılı bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="92d22-178">A detailed description of any changes to the application and/or Azure RTOS GUIX that preceded the problem.</span></span>

3. <span data-ttu-id="92d22-179">_Tx_version_id ve gx_version_id dizelerinin içeriği, _**tx_port. h**_ ve _ \*_gx_port. h_\*\*, dağıtım dosyalarınızın dosyalarında bulunur.</span><span class="sxs-lookup"><span data-stu-id="92d22-179">The contents of the _tx_version_id and _gx_version_id strings found in the \***tx_port.h**_ and _ *_gx_port.h_*\* files of your distribution.</span></span> <span data-ttu-id="92d22-180">Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="92d22-180">These strings will provide us valuable Information regarding your run-time environment.</span></span>

4. <span data-ttu-id="92d22-181">Aşağıdaki ULONG değişkenlerinin RAM 'ine ait içerikler:</span><span class="sxs-lookup"><span data-stu-id="92d22-181">The contents in RAM of the following ULONG variables:</span></span>

    <span data-ttu-id="92d22-182">**_tx_build_options** **_gx_system_build_options**</span><span class="sxs-lookup"><span data-stu-id="92d22-182">**_tx_build_options** **_gx_system_build_options**</span></span>

    <span data-ttu-id="92d22-183">Bu değişkenler, Azure RTOS ThreadX ve Azure RTOS Gux kitaplıklarının nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.</span><span class="sxs-lookup"><span data-stu-id="92d22-183">These variables will give us information on how your Azure RTOS ThreadX and Azure RTOS GUIX libraries were built.</span></span>

5. <span data-ttu-id="92d22-184">Aşağıdaki ULONG değişkenlerinin RAM 'ine ait içerikler:</span><span class="sxs-lookup"><span data-stu-id="92d22-184">The contents in RAM of the following ULONG variables:</span></span>

    <span data-ttu-id="92d22-185">**_gx_system_last_error** **_gx_system_error_count**</span><span class="sxs-lookup"><span data-stu-id="92d22-185">**_gx_system_last_error** **_gx_system_error_count**</span></span>

    <span data-ttu-id="92d22-186">Bu değişkenler, Azure RTOS Gux 'teki iç sistem hatalarını izler.</span><span class="sxs-lookup"><span data-stu-id="92d22-186">These variables keep track of internal system errors in Azure RTOS GUIX.</span></span> <span data-ttu-id="92d22-187">_Gx_system_error_count sıfırdan büyükse, lütfen _gx_system_error_process işlevinde döndürülen işlev için bir kesme noktası ayarlayın ve bu noktada _gx_system_last_error değerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="92d22-187">If the _gx_system_error_count is greater than one, please set a breakpoint on the function return in the _gx_system_error_process function and provide the value of _gx_system_last_error at this point.</span></span> <span data-ttu-id="92d22-188">Bu, birinci iç Azure RTOS Gux sistem hatasını verir.</span><span class="sxs-lookup"><span data-stu-id="92d22-188">This will yield the first internal Azure RTOS GUIX system error.</span></span>

6. <span data-ttu-id="92d22-189">Sorun algılandıktan hemen sonra yakalanan bir izleme arabelleği.</span><span class="sxs-lookup"><span data-stu-id="92d22-189">A trace buffer captured immediately after the problem was detected.</span></span> <span data-ttu-id="92d22-190">Bu, TX_ENABLE_EVENT_TRACE ile Azure RTOS ThreadX ve Azure RTOS Gux kitaplıkları oluşturup izleme arabelleği bilgileriyle tx_trace_enable çağırarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="92d22-190">This is accomplished by building the Azure RTOS ThreadX and Azure RTOS GUIX libraries with TX_ENABLE_EVENT_TRACE and calling tx_trace_enable with the trace buffer information.</span></span>

7. <span data-ttu-id="92d22-191">Kullandığınız Azure RTOS Gux Studio projesi, varsa veya en düşük bir proje rapor ettiğiniz eksiklikleri göstermek için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="92d22-191">The Azure RTOS GUIX Studio project you are using, if applicable, or at a minimum a small project sufficient to demonstrate the deficiency you are reporting.</span></span>
