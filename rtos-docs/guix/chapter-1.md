---
title: Bölüm 1-Gux 'e giriş
description: GUX, katıştırılmış Azure RTOS ThreadX tabanlı uygulamalar için özel olarak tasarlanan (GUI) yüksek performanslı gerçek zamanlı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b90da988a03d59b1bca3f5584164d641bef96454
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827203"
---
# <a name="chapter-1---introduction-to-azure-rtos-guix"></a><span data-ttu-id="2bf07-103">Bölüm 1-Azure RTOS Gux 'e giriş</span><span class="sxs-lookup"><span data-stu-id="2bf07-103">Chapter 1 - Introduction to Azure RTOS GUIX</span></span>

<span data-ttu-id="2bf07-104">Azure RTOS Gux (GUıDX), katıştırılmış ThreadX tabanlı uygulamalar için özel olarak tasarlanmış bir grafik arabirimi çerçevesinin yüksek performanslı gerçek zamanlı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-104">Azure RTOS GUIX (GUIX) is a high-performance real-time implementation of a graphical interface framework designed exclusively for embedded ThreadX-based applications.</span></span> <span data-ttu-id="2bf07-105">Bu bölümde, GUıDX 'e giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-105">This chapter contains an introduction to GUIX and a description of its applications and benefits.</span></span>

## <a name="guix-feature-overview"></a><span data-ttu-id="2bf07-106">GUX özelliğine genel bakış</span><span class="sxs-lookup"><span data-stu-id="2bf07-106">GUIX Feature Overview</span></span>

<span data-ttu-id="2bf07-107">Diğer birçok GUI uygulamasının aksine, GUıDX, küçük mikro denetleyicideki uygulamalardan güçlü RıSC ve DSP işlemcileri kullanan uygulamalara kolayca ölçeklendirerek çok yönlü olacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-107">Unlike many other GUI implementations, GUIX is designed to be versatile—easily scaling from small micro-controller-based applications to those that use powerful RISC and DSP processors.</span></span> <span data-ttu-id="2bf07-108">Bu, başlangıçta iş istasyonu ortamları için tasarlanan, ancak ekli tasarımlara sıkıştırılan genel etki alanı veya diğer ticari uygulamalar için keskin karşıtlığa sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-108">This is in sharp contrast to public domain or other commercial implementations originally intended for workstation environments but then squeezed into embedded designs.</span></span> <span data-ttu-id="2bf07-109">GUX özelliklerine genel bakış aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2bf07-109">An overview of GUIX features follows:</span></span>

- <span data-ttu-id="2bf07-110">Ana bilgisayar tabanlı tasarım aracı Gux Studio ile kullanımı kolay</span><span class="sxs-lookup"><span data-stu-id="2bf07-110">Easy to use with host-based design tool GUIX Studio</span></span>

- <span data-ttu-id="2bf07-111">Tam barındırılan prototipleme için Win32 Gux çalışma zamanı ortamı</span><span class="sxs-lookup"><span data-stu-id="2bf07-111">Win32 GUIX run-time environment for complete hosted prototyping</span></span>

- <span data-ttu-id="2bf07-112">, ThreadX tarafından desteklenen işlemcilerin çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="2bf07-112">Supports most processors supported by ThreadX</span></span>

- <span data-ttu-id="2bf07-113">Yalnızca ANSI C 'de yazılmış</span><span class="sxs-lookup"><span data-stu-id="2bf07-113">Written exclusively in ANSI C</span></span>

- <span data-ttu-id="2bf07-114">Endian nötr</span><span class="sxs-lookup"><span data-stu-id="2bf07-114">Endian neutral</span></span>

- <span data-ttu-id="2bf07-115">En küçük, Faücretli katıştırılmış GUI</span><span class="sxs-lookup"><span data-stu-id="2bf07-115">Smallest, Fasted Embedded GUI</span></span>

- <span data-ttu-id="2bf07-116">Çalışma zamanı yapılandırılabilir, nesne sayısı, ekran boyutu vb.</span><span class="sxs-lookup"><span data-stu-id="2bf07-116">Run-time configurable, number of objects, screen size, etc.</span></span>

- <span data-ttu-id="2bf07-117">Kolay yazma ekran sürücüsü arabirimi</span><span class="sxs-lookup"><span data-stu-id="2bf07-117">Easy to write display driver interface</span></span>

- <span data-ttu-id="2bf07-118">Renk (32-BPP renk derinliğine kadar), tek renkli ve gri tonlamalı destek</span><span class="sxs-lookup"><span data-stu-id="2bf07-118">Color (up to 32-bpp color depth), monochrome, and grayscale support</span></span>

- <span data-ttu-id="2bf07-119">UTF8 dize kodlaması ve dize kaynakları aracılığıyla çok dilli destek</span><span class="sxs-lookup"><span data-stu-id="2bf07-119">Multilingual support via UTF8 string encoding and string resources</span></span>

- <span data-ttu-id="2bf07-120">Varsayılan ücretsiz yazı tipleri ve yeni yazı tipi ekleme kolay</span><span class="sxs-lookup"><span data-stu-id="2bf07-120">Default free fonts and easy to add new fonts</span></span>

- <span data-ttu-id="2bf07-121">Çeşitli boyutlarda birden çok çizim desteklenir</span><span class="sxs-lookup"><span data-stu-id="2bf07-121">Multiple drawing Canvases supported, of various sizes</span></span>

- <span data-ttu-id="2bf07-122">Farklı boyutlarda birden çok ekran ve renk derinlikleri desteklenir</span><span class="sxs-lookup"><span data-stu-id="2bf07-122">Multiple displays of different sizes and color depths supported</span></span>

- <span data-ttu-id="2bf07-123">Ekran geçiş desteği (belirme, soluklaştırma, çekme vb.)</span><span class="sxs-lookup"><span data-stu-id="2bf07-123">Screen Transition support (fade in, fade out, swipe, etc.)</span></span>

- <span data-ttu-id="2bf07-124">Dokunmatik ekran, hareket ve sanal klavye desteği</span><span class="sxs-lookup"><span data-stu-id="2bf07-124">Touch Screen, Gesture, and Virtual Keyboard Support</span></span>

- <span data-ttu-id="2bf07-125">Bit eşlem sıkıştırması</span><span class="sxs-lookup"><span data-stu-id="2bf07-125">Bitmap compression</span></span>

- <span data-ttu-id="2bf07-126">Alfa karıştırma desteği</span><span class="sxs-lookup"><span data-stu-id="2bf07-126">Alpha Blending Support</span></span>

- <span data-ttu-id="2bf07-127">Titreme desteği</span><span class="sxs-lookup"><span data-stu-id="2bf07-127">Dither Support</span></span>

- <span data-ttu-id="2bf07-128">Kenar yumuşatma desteği</span><span class="sxs-lookup"><span data-stu-id="2bf07-128">Anti-Aliasing Support</span></span>

- <span data-ttu-id="2bf07-129">Kaplama ve Temalar</span><span class="sxs-lookup"><span data-stu-id="2bf07-129">Skinning and Themes</span></span>

- <span data-ttu-id="2bf07-130">Tuval karışımı</span><span class="sxs-lookup"><span data-stu-id="2bf07-130">Canvas Blending</span></span>

- <span data-ttu-id="2bf07-131">Tüm pencere yönetimi</span><span class="sxs-lookup"><span data-stu-id="2bf07-131">Complete Window Management</span></span>

  - <span data-ttu-id="2bf07-132">Üst/alt öğe Ilişkisi</span><span class="sxs-lookup"><span data-stu-id="2bf07-132">Parent/Child Relationship</span></span>

  - <span data-ttu-id="2bf07-133">Dinamik oluşturma, silme, yeniden boyutlandırma, taşıma</span><span class="sxs-lookup"><span data-stu-id="2bf07-133">Dynamic creation, deletion, resizing, moving</span></span>
  - <span data-ttu-id="2bf07-134">Ayrı olay işleme ve çizim</span><span class="sxs-lookup"><span data-stu-id="2bf07-134">Separate event handling and drawing</span></span> 
  - <span data-ttu-id="2bf07-135">Z-düzeni</span><span class="sxs-lookup"><span data-stu-id="2bf07-135">Z-order</span></span>
  - <span data-ttu-id="2bf07-136">Kırpma ve görünümler</span><span class="sxs-lookup"><span data-stu-id="2bf07-136">Clipping and views</span></span>

- <span data-ttu-id="2bf07-137">Kapsamlı pencere öğeleri kümesi</span><span class="sxs-lookup"><span data-stu-id="2bf07-137">Extensive Set of Widgets</span></span>

  - <span data-ttu-id="2bf07-138">Çeşitli düğme türleri, sürgüler ve çevirmeler</span><span class="sxs-lookup"><span data-stu-id="2bf07-138">Various button types, sliders, and dials</span></span>

  - <span data-ttu-id="2bf07-139">Açılan liste</span><span class="sxs-lookup"><span data-stu-id="2bf07-139">Drop Down List</span></span>
  
  - <span data-ttu-id="2bf07-140">İstem</span><span class="sxs-lookup"><span data-stu-id="2bf07-140">Prompt</span></span>

  - <span data-ttu-id="2bf07-141">Çok satırlı metin görünümü</span><span class="sxs-lookup"><span data-stu-id="2bf07-141">Multi-Line text view</span></span>
  
  - <span data-ttu-id="2bf07-142">Tek ve çok satırlı metin girişi</span><span class="sxs-lookup"><span data-stu-id="2bf07-142">Single and Multi-Line text input</span></span>
  
  - <span data-ttu-id="2bf07-143">Sayısal ve metin kaydırma tekerlekleri</span><span class="sxs-lookup"><span data-stu-id="2bf07-143">Numeric and Textual Scroll Wheels</span></span>
  
  - <span data-ttu-id="2bf07-144">Pencereler ve kaydırma çubukları</span><span class="sxs-lookup"><span data-stu-id="2bf07-144">Windows and Scroll Bars</span></span>
  
  - <span data-ttu-id="2bf07-145">Radyal Ilerleme çubuğu</span><span class="sxs-lookup"><span data-stu-id="2bf07-145">Radial Progress Bar</span></span>
  
  - <span data-ttu-id="2bf07-146">Öğesini</span><span class="sxs-lookup"><span data-stu-id="2bf07-146">Sprite</span></span>

### <a name="ansi-c-source-code"></a><span data-ttu-id="2bf07-147">ANSI C kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="2bf07-147">ANSI C Source Code</span></span>

<span data-ttu-id="2bf07-148">GUX, ANSI C 'de tamamen yazılır ve doğrudan bir ANSI C derleyicisi ve ThreadX desteği olan tüm işlemci mimarisine taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-148">GUIX is written completely in ANSI C and is portable immediately to virtually any processor architecture that has an ANSI C compiler and ThreadX support.</span></span> <span data-ttu-id="2bf07-149">ANSI C 'de yazılmış olsa da, GUıDX, nesne odaklı bir model ve devralma kullanır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-149">Although written in ANSI C, GUIX uses an object oriented model and inheritance.</span></span>

### <a name="not-a-black-box"></a><span data-ttu-id="2bf07-150">Siyah kutu değil</span><span class="sxs-lookup"><span data-stu-id="2bf07-150">Not A Black Box</span></span>

<span data-ttu-id="2bf07-151">GUX dağıtımların çoğu, tüm C kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-151">Most distributions of GUIX include the complete C source code.</span></span> <span data-ttu-id="2bf07-152">Bu, birçok ticari GUI uygulamalarıyla oluşan "kara kutu" sorunlarını ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-152">This eliminates the “black-box” problems that occur with many commercial GUI implementations.</span></span> <span data-ttu-id="2bf07-153">GUX kullanarak uygulamalar, GUI 'nin neler yaptığını tam olarak görebilir, hiçbir gizleyebilmekte!</span><span class="sxs-lookup"><span data-stu-id="2bf07-153">By using GUIX, applications developers can see exactly what the GUI is doing—there are no mysteries!</span></span>

<span data-ttu-id="2bf07-154">Kaynak kodun olması, uygulamaya özgü değişikliklere de izin verir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-154">Having the source code also allows for application specific modifications.</span></span> <span data-ttu-id="2bf07-155">Önerilmese de, gerekli olduğunda GUI 'yi değiştirme imkanına kesinlikle yarar vardır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-155">Although not recommended, it is certainly beneficial to have the ability to modify the GUI if it is required.</span></span> <span data-ttu-id="2bf07-156">Bu özellikler özellikle, şirket içi veya genel etki alanı ürünleriyle çalışmaya alışkın olan geliştiricilere Comforting.</span><span class="sxs-lookup"><span data-stu-id="2bf07-156">These features are especially comforting to developers accustomed to working with in-house or public domain products.</span></span> <span data-ttu-id="2bf07-157">Bunlar, kaynak kodu ve değişiklik yapabilme yeteneğinin olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="2bf07-157">They expect to have source code and the ability to modify it.</span></span> <span data-ttu-id="2bf07-158">GUX, bu tür geliştiriciler için en üstün GUI yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-158">GUIX is the ultimate GUI software for such developers.</span></span>

## <a name="embedded-gui-applications"></a><span data-ttu-id="2bf07-159">Katıştırılmış GUI uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2bf07-159">Embedded GUI Applications</span></span>

<span data-ttu-id="2bf07-160">Katıştırılmış GUI uygulamaları, bir kullanıcı arabirimi gereksinimi olan ve cep telefonları, iletişim donatımı, oto motor, lazer yazıcılar, tıbbi cihazlar vb. gibi ürünlerin içinde gizlenen mikro işlemcilerde yürütülen uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-160">Embedded GUI applications are applications that have a user interface requirement and execute on microprocessors hidden inside products such as cellular phones, communication equipment, automotive engines, laser printers, medical devices, and so forth.</span></span> <span data-ttu-id="2bf07-161">Bu uygulamalarda neredeyse her zaman bazı bellek ve performans kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-161">Such applications almost always have some memory and performance constraints.</span></span> <span data-ttu-id="2bf07-162">Katıştırılmış GUI 'ye yönelik başka bir ayrım, yazılım ve donanımının özel bir amaca sahip olması olabilir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-162">Another distinction of embedded GUI is that their software and hardware have a dedicated purpose.</span></span>

### <a name="real-time-gui-software"></a><span data-ttu-id="2bf07-163">Gerçek zamanlı GUI yazılımı</span><span class="sxs-lookup"><span data-stu-id="2bf07-163">Real-time GUI Software</span></span>

<span data-ttu-id="2bf07-164">Temelde, işlemesini tam bir süre içinde gerçekleştirmesi gereken GUI yazılımına *gerçek ZAMANLı GUI* yazılımı denır ve GUI uygulamalarına zaman kısıtlamaları eklendiğinde bunlar gerçek zamanlı uygulamalar olarak sınıflandırılır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-164">Basically, GUI software that must perform its processing within an exact period of time is called *real-time GUI* software, and when time constraints are imposed on GUI applications, they are classified as realtime applications.</span></span> <span data-ttu-id="2bf07-165">Gömülü GUI uygulamaları, dış dünyada kendi kendine ait etkileşimlerinden dolayı neredeyse her zaman gerçek zamanlı olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-165">Embedded GUI applications are almost always real-time because of their inherent interaction with the external world.</span></span>

## <a name="guix-benefits"></a><span data-ttu-id="2bf07-166">GUX avantajları</span><span class="sxs-lookup"><span data-stu-id="2bf07-166">GUIX Benefits</span></span>

<span data-ttu-id="2bf07-167">Ekli uygulamalar için Gux kullanmanın başlıca avantajları yüksek performanslı, özellik açısından zengin ve çok küçük bellek gereksinimleridir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-167">The primary benefits of using GUIX for embedded applications are high-performance, feature rich, and very small memory requirements.</span></span> <span data-ttu-id="2bf07-168">GUX, yüksek performanslı, çok görevli Azure RTOS ThreadX gerçek zamanlı işletim sistemiyle tamamen tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-168">GUIX is also completely integrated with the high-performance, multitasking Azure RTOS ThreadX real-time operating system.</span></span>

### <a name="improved-responsiveness"></a><span data-ttu-id="2bf07-169">İyileştirilmiş yanıt hızı</span><span class="sxs-lookup"><span data-stu-id="2bf07-169">Improved Responsiveness</span></span>

<span data-ttu-id="2bf07-170">Yüksek performanslı Gux ürünü, uygulamaların daha önce hiç olmadığı kadar hızlı yanıt vermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bf07-170">The high-performance GUIX product enables applications to respond faster than ever before.</span></span> <span data-ttu-id="2bf07-171">Bu, özellikle önemli miktarda görsel bilgi veya bu tür bilgileri görüntülemek için katı zamanlama gereksinimlerine sahip olan katıştırılmış uygulamalar için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-171">This is especially important for embedded applications that either have a significant volume of visual information or strict timing requirements on displaying such information.</span></span>

### <a name="software-maintenance"></a><span data-ttu-id="2bf07-172">Yazılım Bakımı</span><span class="sxs-lookup"><span data-stu-id="2bf07-172">Software Maintenance</span></span>

<span data-ttu-id="2bf07-173">GUIX kullanmak, geliştiricilerin katıştırılmış uygulamalarının GUI yönlerini kolayca bölümlememesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bf07-173">Using GUIX allows developers to easily partition the GUI aspects of their embedded application.</span></span> <span data-ttu-id="2bf07-174">Bu bölümlendirme, tüm geliştirme sürecini kolaylaştırır ve gelecekteki yazılım bakımını önemli ölçüde geliştirir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-174">This partitioning makes the entire development process easy and significantly enhances future software maintenance.</span></span>

### <a name="increased-throughput"></a><span data-ttu-id="2bf07-175">Artan verimlilik</span><span class="sxs-lookup"><span data-stu-id="2bf07-175">Increased Throughput</span></span>

<span data-ttu-id="2bf07-176">GUX, doğrudan katıştırılmış uygulamaya aktarılan en yüksek performanslı GUI 'yi sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bf07-176">GUIX provides the highest-performance GUI available, which directly transfers to the embedded application.</span></span> <span data-ttu-id="2bf07-177">GUX uygulamaları, Kullanıcı arabirimi bilgilerini Gux olmayan uygulamalardan daha hızlı işleyebilir!</span><span class="sxs-lookup"><span data-stu-id="2bf07-177">GUIX applications are able to process user interface information faster than non-GUIX applications!</span></span>

### <a name="processor-isolation"></a><span data-ttu-id="2bf07-178">İşlemci yalıtımı</span><span class="sxs-lookup"><span data-stu-id="2bf07-178">Processor Isolation</span></span>

<span data-ttu-id="2bf07-179">GUIX, uygulama ile temel alınan işlemci ve görüntüleme donanımı arasında sağlam, işlemciye sahip bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bf07-179">GUIX provides a robust, processor-independent interface between the application and the underlying processor and display hardware.</span></span> <span data-ttu-id="2bf07-180">Bu, geliştiricilerin, ekran donanımı sorunlarıyla ilgili ek süre harcamak yerine, Kullanıcı arabiriminin üst düzey yönlerini yoğunlaşmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bf07-180">This allows developers to concentrate on the high-level aspects of the user interface rather than spending extra time dealing with display hardware issues.</span></span>

### <a name="ease-of-use"></a><span data-ttu-id="2bf07-181">Kullanım kolaylığı</span><span class="sxs-lookup"><span data-stu-id="2bf07-181">Ease of Use</span></span>

<span data-ttu-id="2bf07-182">GUX, uygulama geliştiricisi göz önünde bulundurularak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-182">GUIX is designed with the application developer in mind.</span></span> <span data-ttu-id="2bf07-183">GUX mimarisi ve hizmet çağrısı arabiriminin anlaşılması kolaydır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-183">The GUIX architecture and service call interface are easy to understand.</span></span> <span data-ttu-id="2bf07-184">Sonuç olarak, GUıDX geliştiricileri gelişmiş özelliklerini hızlı bir şekilde kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-184">As a result, GUIX developers can quickly use its advanced features.</span></span>

### <a name="improve-time-to-market"></a><span data-ttu-id="2bf07-185">Pazara ulaşma süresini iyileştirme</span><span class="sxs-lookup"><span data-stu-id="2bf07-185">Improve Time to Market</span></span>

<span data-ttu-id="2bf07-186">GUX 'in güçlü özellikleri yazılım geliştirme sürecini hızlandırır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-186">The powerful features of GUIX accelerate the software development process.</span></span> <span data-ttu-id="2bf07-187">GUX, çoğu işlemciyi soyutlar ve donanım sorunlarını görüntüler, böylece bu konular uygulama kullanıcı arabirimi uygulamasının çoğunluğunda kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="2bf07-187">GUIX abstracts most processor and display hardware issues, thereby removing these concerns from a majority of application user interface implementation.</span></span> <span data-ttu-id="2bf07-188">Bu özellik, kullanımı kolaylaştırma ve gelişmiş özellik kümesiyle birlikte, pazara daha hızlı bir süre içinde sonuçlanır!</span><span class="sxs-lookup"><span data-stu-id="2bf07-188">This feature, coupled with the ease-of-use and advanced feature set, results in a faster time to market!</span></span>

### <a name="protecting-the-software-investment"></a><span data-ttu-id="2bf07-189">Yazılım yatırımınızı koruma</span><span class="sxs-lookup"><span data-stu-id="2bf07-189">Protecting the Software Investment</span></span>

<span data-ttu-id="2bf07-190">GUX, ANSI C 'de özel olarak yazılır ve Azure RTOS ThreadX gerçek zamanlı işletim sistemiyle tamamen tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-190">GUIX is written exclusively in ANSI C and is fully integrated with the Azure RTOS ThreadX real-time operating system.</span></span> <span data-ttu-id="2bf07-191">Bu, Gux uygulamalarının tüm ThreadX desteklenen işlemcilere anında taşınabilir olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-191">This means GUIX applications are instantly portable to all ThreadX supported processors.</span></span> <span data-ttu-id="2bf07-192">Daha iyi bir şekilde, her hafta için ThreadX ile tamamen yeni bir işlemci mimarisi desteklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2bf07-192">Better yet, a completely new processor architecture can be supported with ThreadX in a matter of weeks.</span></span> <span data-ttu-id="2bf07-193">Sonuç olarak, GUıDX kullanılması uygulamanın geçiş yolunu sağlar ve orijinal geliştirme yatırımını korur.</span><span class="sxs-lookup"><span data-stu-id="2bf07-193">As a result, using GUIX ensures the application’s migration path and protects the original development investment.</span></span>
