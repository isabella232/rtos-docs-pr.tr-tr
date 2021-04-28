---
title: Azure RTOS Gux ve Azure RTOS Gux Studio 'Yu anlama
description: Azure RTOS Gux, katıştırılmış sistem geliştiricilerin ihtiyaçlarını karşılamak için oluşturulmuş bir profesyonel kalite paketidir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 8f4a1578fcabdabfb213ced9c6593f6cffc964aa
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171412"
---
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a><span data-ttu-id="2dc76-103">Azure RTOS Gux ve Azure RTOS Gux Studio 'ya genel bakış</span><span class="sxs-lookup"><span data-stu-id="2dc76-103">Overview of Azure RTOS GUIX and Azure RTOS GUIX Studio</span></span>

<span data-ttu-id="2dc76-104">Azure Gux Embedded GUI, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf GUI çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="2dc76-104">Azure GUIX embedded GUI is Microsoft’s advanced, industrial grade GUI solution designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="2dc76-105">Microsoft ayrıca, Azure RTOS Gux Studio adlı tam özellikli bir WYSıWYG masaüstü tasarım aracı sağlar. bu sayede, geliştiricilerin masaüstündeki GUI 'sini tasarlamalarını ve hedefe aktarılabilecek Azure RTOS Gux Embedded GUI kodunu oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2dc76-105">Microsoft also provides a full-featured WYSIWYG desktop design tool named Azure RTOS GUIX Studio, which allows developers to design their GUI on the desktop and generate Azure RTOS GUIX embedded GUI code that can then be exported to the target.</span></span> <span data-ttu-id="2dc76-106">Azure RTOS Gux Azure RTOS ThreadX RTOS ile tamamen tümleşiktir ve Azure RTOS ThreadX tarafından desteklenen işlemcilerin birçoğu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-106">Azure RTOS GUIX is fully integrated with Azure RTOS ThreadX RTOS and is available for many of the same processors supported by Azure RTOS ThreadX.</span></span> <span data-ttu-id="2dc76-107">Bunun hepsi son derece küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla, Azure RTOS Gux 'i bir kullanıcı arabirimi gerektiren en zorlu eklenmiş IoT uygulamalarına yönelik ideal seçim haline getirir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-107">All of this combined with an extremely small footprint, fast execution, and superior ease-of-use, make Azure RTOS GUIX the ideal choice for the most demanding embedded IoT applications requiring a user interface.</span></span> 

## <a name="azure-rtos-guix-api"></a><span data-ttu-id="2dc76-108">Azure RTOS Gux API 'SI</span><span class="sxs-lookup"><span data-stu-id="2dc76-108">Azure RTOS GUIX API</span></span>

### <a name="powerful-apis"></a><span data-ttu-id="2dc76-109">Güçlü API 'Ler</span><span class="sxs-lookup"><span data-stu-id="2dc76-109">Powerful APIs</span></span>

* <span data-ttu-id="2dc76-110">Gerektiğinde doğrudan tuval çizimi için tam destek</span><span class="sxs-lookup"><span data-stu-id="2dc76-110">Full support for direct canvas drawing when needed</span></span>
* <span data-ttu-id="2dc76-111">Azure RTOS Gux Studio tarafından üretilen kodla kolay bir şekilde etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="2dc76-111">Simple to interact with Azure RTOS GUIX Studio generated code</span></span>
* <span data-ttu-id="2dc76-112">Çizgi, dikdörtgen, çokgen vb. için API 'Ler</span><span class="sxs-lookup"><span data-stu-id="2dc76-112">APIs for line, rectangle, polygon, etc.</span></span>
* <span data-ttu-id="2dc76-113">Daire, yay, pasta, kii, elips, vb. için API 'Ler.</span><span class="sxs-lookup"><span data-stu-id="2dc76-113">APIs for circle, arc, pie, chord, ellipse, etc.</span></span>
* <span data-ttu-id="2dc76-114">Metin çizme ve konumlandırma için API 'Ler</span><span class="sxs-lookup"><span data-stu-id="2dc76-114">APIs for text drawing and positioning</span></span>
* <span data-ttu-id="2dc76-115">Kenar yumuşatma, doku dolguları ve düz dolgular</span><span class="sxs-lookup"><span data-stu-id="2dc76-115">Anti-aliasing, texture fills, and solid fills</span></span>
* <span data-ttu-id="2dc76-116">Ekranları ve pencere öğelerini oluşturmak ve yeniden oluşturmak için API 'Ler</span><span class="sxs-lookup"><span data-stu-id="2dc76-116">APIs for creating and modifing screens and widgets</span></span>

### <a name="azure-rtos-guix-studio-generated-files"></a><span data-ttu-id="2dc76-117">Azure RTOS Gux Studio tarafından oluşturulan dosyalar</span><span class="sxs-lookup"><span data-stu-id="2dc76-117">Azure RTOS GUIX Studio Generated Files</span></span>

* <span data-ttu-id="2dc76-118">Otomatik olarak oluşturulan ANSI C kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="2dc76-118">Automatically generated ANSI C source files</span></span>
* <span data-ttu-id="2dc76-119">Düzen ayrıntılarından uygulama yazılımını yalıtılmış olarak</span><span class="sxs-lookup"><span data-stu-id="2dc76-119">Insulates application software from layout details</span></span>
* <span data-ttu-id="2dc76-120">Kullanıcı arabirimi tasarımı için gereken yazı tiplerini ve görüntüleri içerir</span><span class="sxs-lookup"><span data-stu-id="2dc76-120">Includes fonts and images required by UI design</span></span>
* <span data-ttu-id="2dc76-121">Uygulama koduyla derlenen oluşturulan dosyalar</span><span class="sxs-lookup"><span data-stu-id="2dc76-121">Generated files compiled with application code</span></span>
* <span data-ttu-id="2dc76-122">Ekran düzeni, uygulama mantığını etkilemeden güncelleştirilebilen</span><span class="sxs-lookup"><span data-stu-id="2dc76-122">Screen layout can be updated without affecting application logic</span></span>
* <span data-ttu-id="2dc76-123">Kaynak kimlikleri dil ve tema bağımsızlık oluşturma</span><span class="sxs-lookup"><span data-stu-id="2dc76-123">Resource IDs create language and theme independence</span></span>
* <span data-ttu-id="2dc76-124">Kullanıcı tarafından sağlanan özel çizim ve olay işleme işlevleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-124">User-supplied custom drawing and event processing functions</span></span>

### <a name="widget-library"></a><span data-ttu-id="2dc76-125">Pencere öğesi kitaplığı</span><span class="sxs-lookup"><span data-stu-id="2dc76-125">Widget library</span></span>

* <span data-ttu-id="2dc76-126">Önceden tanımlanmış ancak özelleştirilebilir ortak arabirim öğeleri kümesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-126">Pre-defined but customizable set of common interface elements</span></span>
* <span data-ttu-id="2dc76-127">Son derece küçük, kompakt ve verimli</span><span class="sxs-lookup"><span data-stu-id="2dc76-127">Extremely small, compact, and efficient</span></span>
* <span data-ttu-id="2dc76-128">Kitaplık, düğme, ölçer, liste, pencere, kaydırma, kaydırıcı, ilerleme çubuğu, istem ve çok daha fazlasını içerir</span><span class="sxs-lookup"><span data-stu-id="2dc76-128">Library includes button, gauge, list, window, scroll, slider, progress bar, prompt and many more</span></span>
* <span data-ttu-id="2dc76-129">Tamamen özelleştirilebilir çizim ve görünüm</span><span class="sxs-lookup"><span data-stu-id="2dc76-129">Fully customizable drawing and appearance</span></span>
* <span data-ttu-id="2dc76-130">Tamamen özelleştirilebilir işlem ve olay işleme</span><span class="sxs-lookup"><span data-stu-id="2dc76-130">Fully customizable operation and event handling</span></span>
* <span data-ttu-id="2dc76-131">Yalnızca kullanılan pencere öğeleri uygulama yazılımıyla bağlantılı</span><span class="sxs-lookup"><span data-stu-id="2dc76-131">Only the widgets used are linked with application software</span></span>

### <a name="math-and-utilities"></a><span data-ttu-id="2dc76-132">Matematik ve yardımcı programlar</span><span class="sxs-lookup"><span data-stu-id="2dc76-132">Math and utilities</span></span>

* <span data-ttu-id="2dc76-133">Sin, cos, Arcsin, arccos, tanjant, kare kök işlevleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-133">Functions for sin, cos, arcsin, arccos, tangent, square root</span></span>
* <span data-ttu-id="2dc76-134">Ekran bölgelerini düzenleme işlevleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-134">Functions for manipulating screen regions</span></span>
* <span data-ttu-id="2dc76-135">Sistem Yapılandırması ve başlangıç</span><span class="sxs-lookup"><span data-stu-id="2dc76-135">System configuration and startup</span></span>
* <span data-ttu-id="2dc76-136">Bellek havuzu tanımı (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="2dc76-136">Memory pool definition (optional)</span></span>
* <span data-ttu-id="2dc76-137">Zamanlayıcı yönetimi</span><span class="sxs-lookup"><span data-stu-id="2dc76-137">Timer Management</span></span>
* <span data-ttu-id="2dc76-138">Animasyon yönetimi</span><span class="sxs-lookup"><span data-stu-id="2dc76-138">Animation Management</span></span>
* <span data-ttu-id="2dc76-139">Kirli liste Bakımı</span><span class="sxs-lookup"><span data-stu-id="2dc76-139">Dirty list maintenance</span></span>

### <a name="image-processing"></a><span data-ttu-id="2dc76-140">Görüntü işleme</span><span class="sxs-lookup"><span data-stu-id="2dc76-140">Image processing</span></span>

* <span data-ttu-id="2dc76-141">JPEG ve PNG görüntülerinin çalışma zamanı kodunu çözme işlevleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-141">Functions for runtime decode of jpeg and png images</span></span>
* <span data-ttu-id="2dc76-142">Titreme ve renk alanı dönüştürmeyi Uygula</span><span class="sxs-lookup"><span data-stu-id="2dc76-142">Apply dithering and color space conversion</span></span>
* <span data-ttu-id="2dc76-143">Görüntü döndürme</span><span class="sxs-lookup"><span data-stu-id="2dc76-143">Image rotation</span></span>
* <span data-ttu-id="2dc76-144">Görüntü ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2dc76-144">Image scaling</span></span>
* <span data-ttu-id="2dc76-145">Görüntü karıştırma</span><span class="sxs-lookup"><span data-stu-id="2dc76-145">Image blending</span></span>

### <a name="event-processing"></a><span data-ttu-id="2dc76-146">Olay işleme</span><span class="sxs-lookup"><span data-stu-id="2dc76-146">Event processing</span></span>

* <span data-ttu-id="2dc76-147">Boştayken Azure RTOS Gux iş parçacığını otomatik olarak askıya alır</span><span class="sxs-lookup"><span data-stu-id="2dc76-147">Automatically suspends Azure RTOS GUIX thread when idle</span></span>
* <span data-ttu-id="2dc76-148">UI tasarımında popüler olay odaklı programlama modeli</span><span class="sxs-lookup"><span data-stu-id="2dc76-148">Event-driven programming model popular in UI design</span></span>
* <span data-ttu-id="2dc76-149">Azure RTOS Gux çizim iş parçacığından giriş sürücülerini yalıtılmış olarak</span><span class="sxs-lookup"><span data-stu-id="2dc76-149">Insulates input drivers from Azure RTOS GUIX drawing thread</span></span>
* <span data-ttu-id="2dc76-150">Olayları gönderme ve alma işlevleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-150">Functions for sending and receiving events</span></span>
* <span data-ttu-id="2dc76-151">Tüm Azure RTOS Gux pencere öğesi türleri için önceden tanımlanmış olay türleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-151">Pre-defined event types for all Azure RTOS GUIX widget types</span></span>
* <span data-ttu-id="2dc76-152">Kullanıcı tanımlı özel olaylar destekleniyor</span><span class="sxs-lookup"><span data-stu-id="2dc76-152">User-defined custom events supported</span></span>

### <a name="canvas-processing"></a><span data-ttu-id="2dc76-153">Tuval işleme</span><span class="sxs-lookup"><span data-stu-id="2dc76-153">Canvas processing</span></span>

* <span data-ttu-id="2dc76-154">Kırpma ve Z düzeninde bakım</span><span class="sxs-lookup"><span data-stu-id="2dc76-154">Clipping and Z-Order maintenance</span></span>
* <span data-ttu-id="2dc76-155">Donanım ayrıntılarından pencere öğesi kitaplığını yalıtılmış olarak</span><span class="sxs-lookup"><span data-stu-id="2dc76-155">Insulates widget library from hardware details</span></span>
* <span data-ttu-id="2dc76-156">Uygulamanın donanım ayrıntılarından yalıtılmış olması</span><span class="sxs-lookup"><span data-stu-id="2dc76-156">Insulates application from hardware details</span></span>
* <span data-ttu-id="2dc76-157">Kirli alanların otomatik arka plan yenilemesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-157">Automatic background refresh of dirty areas</span></span>
* <span data-ttu-id="2dc76-158">Katmanlama ve karıştırma desteği ile birden çok canvaya</span><span class="sxs-lookup"><span data-stu-id="2dc76-158">Multiple canvases with layering and blending supported</span></span>
* <span data-ttu-id="2dc76-159">Uygulama yazılımı tarafından doğrudan çağrılabilir</span><span class="sxs-lookup"><span data-stu-id="2dc76-159">Can be invoked directly by the application software</span></span>

### <a name="input-device-drivers"></a><span data-ttu-id="2dc76-160">Giriş cihazı sürücüleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-160">Input device driver(s)</span></span>

* <span data-ttu-id="2dc76-161">Donanıma özel destek, Azure RTOS Gux ve donanım ayrıntılarından yalıtılmış uygulama</span><span class="sxs-lookup"><span data-stu-id="2dc76-161">Hardware-specific support, Azure RTOS GUIX and application insulated from hardware details</span></span>
* <span data-ttu-id="2dc76-162">Dirensel dokunma, uç Touch ve tuş takımı destekleniyor</span><span class="sxs-lookup"><span data-stu-id="2dc76-162">Resistive Touch, Cap Touch, and keypad supported</span></span>
* <span data-ttu-id="2dc76-163">Azure RTOS Gux olay kuyruğuna geçirilen giriş olayları</span><span class="sxs-lookup"><span data-stu-id="2dc76-163">Input events passed to Azure RTOS GUIX event queue</span></span>

### <a name="display-drivers"></a><span data-ttu-id="2dc76-164">Görüntü sürücüleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-164">Display drivers</span></span>

* <span data-ttu-id="2dc76-165">Donanıma özgü destek</span><span class="sxs-lookup"><span data-stu-id="2dc76-165">Hardware-specific support</span></span>
* <span data-ttu-id="2dc76-166">Tüm renk derinliği ve biçimleri için sunulan genel sürücüler</span><span class="sxs-lookup"><span data-stu-id="2dc76-166">Generic drivers provided for all color depth and formats</span></span>
* <span data-ttu-id="2dc76-167">Kullanılabilir grafik hızlandırıcılarını kullanacak şekilde özelleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="2dc76-167">Customized to utilize available graphics accelerators</span></span>

### <a name="target-hardware"></a><span data-ttu-id="2dc76-168">Hedef donanım</span><span class="sxs-lookup"><span data-stu-id="2dc76-168">Target hardware</span></span>

* <span data-ttu-id="2dc76-169">Grafik çıkışı yapabilen neredeyse tüm donanımlar, GUıDX ile uyumludur</span><span class="sxs-lookup"><span data-stu-id="2dc76-169">Nearly any hardware capable of graphical output Is compatible with GUIX</span></span>
* <span data-ttu-id="2dc76-170">Birden çok fiziksel görüntüleme destekleniyor</span><span class="sxs-lookup"><span data-stu-id="2dc76-170">Multiple physical displays supported</span></span>
* <span data-ttu-id="2dc76-171">En az RAM ve Flash gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="2dc76-171">Minimal RAM and Flash requirements</span></span>

## <a name="create-elegant-user-interfaces"></a><span data-ttu-id="2dc76-172">Zarif Kullanıcı arabirimleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="2dc76-172">Create Elegant User Interfaces</span></span>

<span data-ttu-id="2dc76-173">Azure RTOS Gux ve Azure RTOS Gux Studio, benzersiz şekilde zarif Kullanıcı arabirimleri oluşturmak için gereken tüm özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="2dc76-173">Azure RTOS GUIX and Azure RTOS GUIX Studio provide all the features necessary to create uniquely elegant user interfaces.</span></span> <span data-ttu-id="2dc76-174">Standart Azure RTOS Gux paketi, tıbbi cihaz başvurusu, akıllı bir izleme başvurusu, bir giriş otomasyon başvurusu, endüstriyel denetim başvurusu, bir otomatik Molem başvurusu ve çeşitli sprite ve animasyon örnekleri dahil olmak üzere çeşitli örnek kullanıcı arabirimlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-174">The standard Azure RTOS GUIX package includes various sample user interfaces, including a medical device reference, a smart watch reference, a home automation reference, an industrial control reference, an automotive reference, and various sprite and animation examples.</span></span> <span data-ttu-id="2dc76-175">Lütfen aşağıda gösterilen başvuru örneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2dc76-175">Please click on the reference examples shown below.</span></span>

### <a name="home-automation"></a><span data-ttu-id="2dc76-176">Ana Otomasyon</span><span class="sxs-lookup"><span data-stu-id="2dc76-176">Home Automation</span></span>

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a><span data-ttu-id="2dc76-177">Birinin</span><span class="sxs-lookup"><span data-stu-id="2dc76-177">Medical</span></span>

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a><span data-ttu-id="2dc76-178">Tüketici</span><span class="sxs-lookup"><span data-stu-id="2dc76-178">Consumer</span></span>

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a><span data-ttu-id="2dc76-179">Beyaz mallar</span><span class="sxs-lookup"><span data-stu-id="2dc76-179">White Goods</span></span>

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a><span data-ttu-id="2dc76-180">Otomotiv</span><span class="sxs-lookup"><span data-stu-id="2dc76-180">Automotive</span></span>

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a><span data-ttu-id="2dc76-181">Sanayi</span><span class="sxs-lookup"><span data-stu-id="2dc76-181">Industrial</span></span>

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

<span data-ttu-id="2dc76-182">Her Azure RTOS Gux başvurusunda, başvuru tasarımının tüm grafik öğelerini tanımlayan karşılık gelen bir Azure RTOS Gux Studio projesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="2dc76-182">Each Azure RTOS GUIX reference has a corresponding Azure RTOS GUIX Studio project that defines all the graphical elements of the reference design.</span></span> <span data-ttu-id="2dc76-183">Başvuru tasarımını değiştirmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-183">Changing a reference design is easy.</span></span> <span data-ttu-id="2dc76-184">Yalnızca ilgili Azure RTOS Gux projesini açın, istenen değişiklikleri yapın, projeyi kaydedin ve *Proje*' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="2dc76-184">Simply open the corresponding Azure RTOS GUIX project, make the desired changes, save the project, and then select *Project*.</span></span>

<span data-ttu-id="2dc76-185">Azure RTOS Gux için C kodu oluşturmak üzere tüm çıkış dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2dc76-185">Generate All Output Files to generate the C code for Azure RTOS GUIX.</span></span> <span data-ttu-id="2dc76-186">Ardından hedef uygulamayı yeniden oluşturup değiştirilen başvuru tasarımını gözlemleyecek şekilde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2dc76-186">Then simply rebuild the target application and run to observe the modified reference design.</span></span>

### <a name="memory-footprint"></a><span data-ttu-id="2dc76-187">Bellek ayak izi</span><span class="sxs-lookup"><span data-stu-id="2dc76-187">Memory footprint</span></span>

<span data-ttu-id="2dc76-188">Azure RTOS Gux, bir tuval için gereken belleği dahil etmez ve temel destek için 13.2 KB 'lık FLASH ve 4KB RAM 'in daha az küçük bir ayak izine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-188">Azure RTOS GUIX has a remarkably small minimal footprint of 13.2KB of FLASH and 4KB RAM for basic support, not including the memory required for a canvas.</span></span>

<span data-ttu-id="2dc76-189">Dahili GRAM ve kendi kendini yenileme teknolojisine sahip bir ekran için tuval belleği gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-189">For a display with internal GRAM and self-refresh technology, no canvas memory is required.</span></span> <span data-ttu-id="2dc76-190">Ancak, çizim performansını artırmak veya görüntüleme için yerel olarak kullanılan bir görüntüleme yapılandırması için, uygulama tarafından bir tuval bellek alanı tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-190">However, to improve drawing performance, or for a display configuration that does not utilize GRAM local to the display, a canvas memory area is defined by the application.</span></span>

<span data-ttu-id="2dc76-191">Tuval bellek gereksinimleri, Tuval boyutunun ve renk derinliğinin bir işlevidir ve formül tarafından tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="2dc76-191">Canvas memory requirements are a function of the canvas size as well as the color depth, and are defined by the formula:</span></span>

<span data-ttu-id="2dc76-192"><i>Tuval RAM (bayt) = (x \* y \* (BPP/8))</i></span><span class="sxs-lookup"><span data-stu-id="2dc76-192"><i>Canvas RAM (bytes) = (x \* y \* (bpp/8))</i></span></span>

<span data-ttu-id="2dc76-193">Burada "x" ve "y", tuvalin boyutlarıdır (görüntü).</span><span class="sxs-lookup"><span data-stu-id="2dc76-193">Where “x” and “y” are the dimensions of the canvas (display).</span></span>

<span data-ttu-id="2dc76-194">Çoğu uygulama, temel Azure RTOS Gux kitaplığı depolama gereksinimlerine dahil olmayan grafik kaynakları da kullanır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-194">Most applications also utilize graphical resources, which are not included in the core Azure RTOS GUIX library storage requirements.</span></span> <span data-ttu-id="2dc76-195">Bu kaynaklar, yazı tiplerini, grafik simgelerini (pixelmaps) ve statik dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-195">These resources include fonts, graphical icons (pixelmaps), and static strings.</span></span> <span data-ttu-id="2dc76-196">Bu veriler, const bellek bölümünde (örn. FLASH) depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-196">This data can be stored in the const memory section (i.e. FLASH).</span></span>

<span data-ttu-id="2dc76-197">Bu bellek alanının boyutu, kullanılan benzersiz yazı tiplerinin sayısını ve boyutunu, kullanılan grafik simgelerinin sayısını ve boyutunu, çıkış rengi biçimini ve her bir kaynağın sıkıştırılmış verileri kullanıp kullanmadığını, her iki yazı tipinin ve pixelmap verilerinin RLE sıkıştırmasını desteklediğinden bu yana bir dizi etkene bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-197">The size of this memory area is dependent on a number of factors, including the number and size of unique fonts used, the number and size of the graphical icons used, the output color format, and whether or not each resource is using compressed data, since Azure RTOS GUIX supports RLE compression of both font and pixelmap data.</span></span> <span data-ttu-id="2dc76-198">Her kaynak için depolama gereksinimleri, Azure RTOS Gux Studio uygulamasında görüntülenir ve kullanıcının uygulama kaynakları tarafından tüketilen Flash bellek miktarını izlemesine ve izlemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="2dc76-198">The storage requirements for each resource are displayed within the Azure RTOS GUIX Studio application, allowing the user to track and monitor the amount of flash memory that will be consumed by the application resources.</span></span>

<span data-ttu-id="2dc76-199">Azure RTOS ThreadX gibi Azure RTOS Gux boyutu, uygulama tarafından gerçekten kullanılan hizmetlere göre otomatik olarak ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-199">Like Azure RTOS ThreadX, the size of Azure RTOS GUIX automatically scales based on the services actually used by the application.</span></span> <span data-ttu-id="2dc76-200">Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-200">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

#### <a name="simple-easy-to-use"></a><span data-ttu-id="2dc76-201">Basit, kullanımı kolay</span><span class="sxs-lookup"><span data-stu-id="2dc76-201">Simple, easy-to-use</span></span>

<span data-ttu-id="2dc76-202">Azure RTOS Gux kullanımı çok basittir ve Azure RTOS Gux Studio, geliştiricilerin masaüstünü görsel olarak tasarlamasına ve gerçek hedefte çalışan C kodu oluşturmasına izin vererek daha da kolay hale gelir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-202">Azure RTOS GUIX is very simple to use and Azure RTOS GUIX Studio makes it even easier by allowing developers to visually design on the desktop and generate C code that runs on the actual target.</span></span> <span data-ttu-id="2dc76-203">Uygulamalar daha sonra kendi özel olay işleme ve çizim işlevlerini ekleyerek GUI 'sini tamamlamalarını sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-203">Applications can then add their own custom event handling and drawing functions to complete their GUI.</span></span>

<span data-ttu-id="2dc76-204">Azure RTOS Gux API 'SI kullanımı basittir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-204">Using the Azure RTOS GUIX API is straightforward.</span></span> <span data-ttu-id="2dc76-205">Azure RTOS Gux API 'SI sezgisel ve yüksek işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-205">The Azure RTOS GUIX API is both intuitive and highly functional.</span></span> <span data-ttu-id="2dc76-206">API adları, gerçek sözcüklerden oluşur ve "alfabe adı" ve/veya diğer dosya sistemi ürünlerinde ortak olan çok sayıda kısaltılmış isimlerdir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-206">The API names are made of real words and not the “alphabet soup” and/or the highly abbreviated names that are so common in other file system products.</span></span> <span data-ttu-id="2dc76-207">Tüm Azure RTOS Gux API 'Lerinin önde bir *gx_* vardır ve bir ad fiil adlandırma kuralını takip edin.</span><span class="sxs-lookup"><span data-stu-id="2dc76-207">All Azure RTOS GUIX APIs have a leading *gx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="2dc76-208">Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-208">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="2dc76-209">Örneğin, bir pencere öğesi denetim bloğunu başlatacak tüm API 'Ler &lt; widget_type &gt; _Create olarak adlandırılır ve her pencere öğesi türü için oluşturma işlevi parametreleri her zaman aynı sırada tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-209">For example, all APIs that initialize a widget control block are named &lt; widget_type&gt;_create, and the create function parameters for each widget type are always defined in the same order.</span></span>

### <a name="comprehensive-set-of-built-in-widgets"></a><span data-ttu-id="2dc76-210">Kapsamlı yerleşik pencere öğeleri kümesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-210">Comprehensive set of built-in widgets</span></span>

* <span data-ttu-id="2dc76-211">Azure RTOS Gux, aşağıdakiler dahil olmak üzere zengin bir yerleşik pencere öğesi kümesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="2dc76-211">Azure RTOS GUIX provides a rich set of built-in widgets, including:</span></span>
* <span data-ttu-id="2dc76-212">Accordion menüsü</span><span class="sxs-lookup"><span data-stu-id="2dc76-212">Accordion Menu</span></span>
* <span data-ttu-id="2dc76-213">Düğme</span><span class="sxs-lookup"><span data-stu-id="2dc76-213">Button</span></span>
* <span data-ttu-id="2dc76-214">Onay kutusu</span><span class="sxs-lookup"><span data-stu-id="2dc76-214">Checkbox</span></span>
* <span data-ttu-id="2dc76-215">Dairesel ölçer</span><span class="sxs-lookup"><span data-stu-id="2dc76-215">Circular Gauge</span></span>
* <span data-ttu-id="2dc76-216">Açılan liste</span><span class="sxs-lookup"><span data-stu-id="2dc76-216">Drop Down List</span></span>
* <span data-ttu-id="2dc76-217">Yatay liste</span><span class="sxs-lookup"><span data-stu-id="2dc76-217">Horizontal List</span></span>
* <span data-ttu-id="2dc76-218">Yatay kaydırma çubuğu penceresi</span><span class="sxs-lookup"><span data-stu-id="2dc76-218">Horizontal Scrollbar Window</span></span>
* <span data-ttu-id="2dc76-219">Simge</span><span class="sxs-lookup"><span data-stu-id="2dc76-219">Icon</span></span>
* <span data-ttu-id="2dc76-220">Simge düğmesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-220">Icon Button</span></span>
* <span data-ttu-id="2dc76-221">Çizgi grafik</span><span class="sxs-lookup"><span data-stu-id="2dc76-221">Line Chart</span></span>
* <span data-ttu-id="2dc76-222">Menü</span><span class="sxs-lookup"><span data-stu-id="2dc76-222">Menu</span></span>
* <span data-ttu-id="2dc76-223">Çok satırlı metin düğmesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-223">Multi Line Text Button</span></span>
* <span data-ttu-id="2dc76-224">Çok satırlı metin girişi</span><span class="sxs-lookup"><span data-stu-id="2dc76-224">Multi Line Text Input</span></span>
* <span data-ttu-id="2dc76-225">Çok satırlı metin görünümü</span><span class="sxs-lookup"><span data-stu-id="2dc76-225">Multi Line Text View</span></span>
* <span data-ttu-id="2dc76-226">Sayısal pixelmap Istemi</span><span class="sxs-lookup"><span data-stu-id="2dc76-226">Numeric Pixelmap Prompt</span></span>
* <span data-ttu-id="2dc76-227">Sayısal Istem</span><span class="sxs-lookup"><span data-stu-id="2dc76-227">Numeric Prompt</span></span>
* <span data-ttu-id="2dc76-228">Sayısal kaydırma tekerleği</span><span class="sxs-lookup"><span data-stu-id="2dc76-228">Numeric Scroll Wheel</span></span>
* <span data-ttu-id="2dc76-229">Pixelmap düğmesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-229">Pixelmap Button</span></span>
* <span data-ttu-id="2dc76-230">Pixelmap Istemi</span><span class="sxs-lookup"><span data-stu-id="2dc76-230">Pixelmap Prompt</span></span>
* <span data-ttu-id="2dc76-231">Pixelmap kaydırıcısı</span><span class="sxs-lookup"><span data-stu-id="2dc76-231">Pixelmap Slider</span></span>
* <span data-ttu-id="2dc76-232">Pixelmap Sprite</span><span class="sxs-lookup"><span data-stu-id="2dc76-232">Pixelmap Sprite</span></span>
* <span data-ttu-id="2dc76-233">İlerleme Çubuğu</span><span class="sxs-lookup"><span data-stu-id="2dc76-233">Progress Bar</span></span>
* <span data-ttu-id="2dc76-234">İstem</span><span class="sxs-lookup"><span data-stu-id="2dc76-234">Prompt</span></span>
* <span data-ttu-id="2dc76-235">Radyal Ilerleme çubuğu</span><span class="sxs-lookup"><span data-stu-id="2dc76-235">Radial Progress Bar</span></span>
* <span data-ttu-id="2dc76-236">Radyo Düğmesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-236">Radio Button</span></span>
* <span data-ttu-id="2dc76-237">Tekerleği kaydır</span><span class="sxs-lookup"><span data-stu-id="2dc76-237">Scroll Wheel</span></span>
* <span data-ttu-id="2dc76-238">Tek satırlık metin girişi</span><span class="sxs-lookup"><span data-stu-id="2dc76-238">Single Line Text Input</span></span>
* <span data-ttu-id="2dc76-239">Kaydırıcı</span><span class="sxs-lookup"><span data-stu-id="2dc76-239">Slider</span></span>
* <span data-ttu-id="2dc76-240">Dize kaydırma tekerleği</span><span class="sxs-lookup"><span data-stu-id="2dc76-240">String Scroll Wheel</span></span>
* <span data-ttu-id="2dc76-241">Metin düğmesi</span><span class="sxs-lookup"><span data-stu-id="2dc76-241">Text Button</span></span>
* <span data-ttu-id="2dc76-242">Ağacı Görünümü</span><span class="sxs-lookup"><span data-stu-id="2dc76-242">Tree View</span></span>
* <span data-ttu-id="2dc76-243">Dikey Liste</span><span class="sxs-lookup"><span data-stu-id="2dc76-243">Vertical List</span></span>
* <span data-ttu-id="2dc76-244">Dikey kaydırma çubuğu</span><span class="sxs-lookup"><span data-stu-id="2dc76-244">Vertical Scrollbar</span></span>

<span data-ttu-id="2dc76-245">Uygulamanın kendi müşteri pencere öğelerini de oluşturması kolay bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-245">It’s easy for the application to create its own customer widgets as well.</span></span>

### <a name="complete-low-level-drawing-api"></a><span data-ttu-id="2dc76-246">Düşük düzey çizim API 'sini doldurun</span><span class="sxs-lookup"><span data-stu-id="2dc76-246">Complete low-level drawing API</span></span>

<span data-ttu-id="2dc76-247">Azure RTOS Gux sağlam bir tuval çizimi API 'SI sağlar ve uygulamanın karmaşık grafik şekillerini işlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-247">Azure RTOS GUIX provides a robust canvas drawing API, allowing the application to render complex graphical shapes.</span></span>

<span data-ttu-id="2dc76-248">Tüm işlevler, yüksek renk derinliği hedefleri üzerinde kenar yumuşatmasını destekler ve Solid ve pixelmap örüntüsünün dolgusu dahil olmak üzere tüm şekiller ana hatlarıyla doldurulabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-248">All functions support anti-aliasing on high color depth targets, and all shapes can be filled our outlined, including solid and pixelmap pattern fills.</span></span> <span data-ttu-id="2dc76-249">Tüm çizim temelleri 16 BPP ve daha yüksek renk derinliğinde çalışırken fırça Alpha 'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="2dc76-249">All drawing primitives support brush alpha when running at 16 bpp and higher color depth.</span></span> <span data-ttu-id="2dc76-250">Çizim işlevleri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="2dc76-250">Drawing functions include:</span></span>

* <span data-ttu-id="2dc76-251">Yay çiz</span><span class="sxs-lookup"><span data-stu-id="2dc76-251">Arc Draw</span></span>
* <span data-ttu-id="2dc76-252">Daire çiz</span><span class="sxs-lookup"><span data-stu-id="2dc76-252">Circle Draw</span></span>
* <span data-ttu-id="2dc76-253">Çizgi çizme</span><span class="sxs-lookup"><span data-stu-id="2dc76-253">Line Draw</span></span>
* <span data-ttu-id="2dc76-254">Pasta çiz</span><span class="sxs-lookup"><span data-stu-id="2dc76-254">Pie Draw</span></span>
* <span data-ttu-id="2dc76-255">Pixelmap Blend</span><span class="sxs-lookup"><span data-stu-id="2dc76-255">Pixelmap Blend</span></span>
* <span data-ttu-id="2dc76-256">Pixelmap kutucuğu</span><span class="sxs-lookup"><span data-stu-id="2dc76-256">Pixelmap Tile</span></span>
* <span data-ttu-id="2dc76-257">Çokgen Çiz</span><span class="sxs-lookup"><span data-stu-id="2dc76-257">Polygon Draw</span></span>
* <span data-ttu-id="2dc76-258">Metin çizme</span><span class="sxs-lookup"><span data-stu-id="2dc76-258">Text Draw</span></span>
* <span data-ttu-id="2dc76-259">Chun çiz</span><span class="sxs-lookup"><span data-stu-id="2dc76-259">Chord Draw</span></span>
* <span data-ttu-id="2dc76-260">Elips çizme</span><span class="sxs-lookup"><span data-stu-id="2dc76-260">Ellipse Draw</span></span>
* <span data-ttu-id="2dc76-261">Piksel çizimi</span><span class="sxs-lookup"><span data-stu-id="2dc76-261">Pixel Draw</span></span>
* <span data-ttu-id="2dc76-262">Pixelmap çiz</span><span class="sxs-lookup"><span data-stu-id="2dc76-262">Pixelmap Draw</span></span>
* <span data-ttu-id="2dc76-263">Pixelmap döndürme</span><span class="sxs-lookup"><span data-stu-id="2dc76-263">Pixelmap Rotate</span></span>
* <span data-ttu-id="2dc76-264">Dikdörtgen çiz</span><span class="sxs-lookup"><span data-stu-id="2dc76-264">Rectangle Draw</span></span>
* <span data-ttu-id="2dc76-265">Metin Blend</span><span class="sxs-lookup"><span data-stu-id="2dc76-265">Text Blend</span></span>

### <a name="default-free-fonts-and-easy-to-add-more"></a><span data-ttu-id="2dc76-266">Varsayılan ücretsiz yazı tipleri ve ekleme daha kolay</span><span class="sxs-lookup"><span data-stu-id="2dc76-266">Default free fonts and easy to add more</span></span>

<span data-ttu-id="2dc76-267">Azure RTOS Gux, ücretsiz bir TrueType yazı tipi kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="2dc76-267">Azure RTOS GUIX provides a free set of TrueType fonts.</span></span> <span data-ttu-id="2dc76-268">Geliştiriciler, istediğiniz gibi ek TrueType yazı tipleri ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-268">Developers can add additional TrueType fonts as desired.</span></span>

<span data-ttu-id="2dc76-269">Azure RTOS Gux yazı tipi biçimi, 8bpp Anti-düzgünleştirme, 4bpp düzgünleştirme ve 1bpp tek renkli yazı tiplerini destekler.</span><span class="sxs-lookup"><span data-stu-id="2dc76-269">The Azure RTOS GUIX font format supports 8bpp anti-aliasing, 4bpp anti-aliasing, and 1bpp monochrome fonts.</span></span> <span data-ttu-id="2dc76-270">En fazla kaynak sınırlamalı uygulamalar için, Azure RTOS Gux önceden TrueType yazı tiplerini Gux Studio Desktop aracımızı kullanarak sıkıştırılmış bir bit eşlem biçimine göre işler.</span><span class="sxs-lookup"><span data-stu-id="2dc76-270">For the most resource-constrained applications, Azure RTOS GUIX pre-renders the TrueType fonts to a compressed bitmap format using our GUIX Studio desktop tool.</span></span>

### <a name="custom-jpg-and-png-decoder-implementation"></a><span data-ttu-id="2dc76-271">Özel JPG ve PNG kod çözücü uygulama</span><span class="sxs-lookup"><span data-stu-id="2dc76-271">Custom JPG and PNG decoder implementation</span></span>

<span data-ttu-id="2dc76-272">Özel JPG ve PNG kod çözücü uygulama JPG ve PNG dosya kod çözücü uygulama.</span><span class="sxs-lookup"><span data-stu-id="2dc76-272">Custom JPG and PNG decoder implementation JPG and PNG file decoder implementation.</span></span> <span data-ttu-id="2dc76-273">Bu uygulama, Azure RTOS GUıDX uyumlu pixelmap biçim görüntülerinin renk alanı dönüştürmeyi, titreme ve çalışma zamanı oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2dc76-273">This implementation supports color space conversion, dithering, and runtime creation of Azure RTOS GUIX-compatible pixelmap format images.</span></span>

### <a name="extensive-display-and-touchscreen-support"></a><span data-ttu-id="2dc76-274">Kapsamlı ekran ve dokunmatik ekran desteği</span><span class="sxs-lookup"><span data-stu-id="2dc76-274">Extensive display and touchscreen support</span></span>

<span data-ttu-id="2dc76-275">Azure RTOS Gux, 1bpp tek renkli, 8 BPP palet, 8 BPP 3:3:2 biçimi de dahil olmak üzere neredeyse tüm renk biçimleri için genel görüntüleme sürücüleri sağlar</span><span class="sxs-lookup"><span data-stu-id="2dc76-275">Azure RTOS GUIX provides generic display drivers for nearly all color formats, including 1bpp monochrome, 8 bpp palette, 8 bpp 3:3:2 format,</span></span>

<span data-ttu-id="2dc76-276">16 BPP 565 RGB biçimi, 16 BPP 4:4:4:4 biçimi, 32 BPP x:r: g:b biçimi ve 32 BPP a:r: g:b biçimi.</span><span class="sxs-lookup"><span data-stu-id="2dc76-276">16 bpp 565 rgb format, 16 bpp 4:4:4:4 format, 32 bpp x:r:g:b format, and 32 bpp a:r:g:b format.</span></span> <span data-ttu-id="2dc76-277">Ayrıca, Azure RTOS Gux, en popüler LCD denetleyiciler ve donanım hızlandırıcılarının (ST Kmesanat, Renesas Synergy, vb.) çoğuyla tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-277">In addition, Azure RTOS GUIX is integrated with many of the most popular LCD controllers and hardware accelerators (ST ChromeArt, Renesas Synergy, etc.).</span></span>

<span data-ttu-id="2dc76-278">Azure RTOS Gux, dokunmatik ekranı (hareket desteği dahil), kalemi ve sanal klavye girişi cihazlarını tam olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="2dc76-278">Azure RTOS GUIX fully supports touchscreen (including gesture support), pen, and virtual keyboard input devices.</span></span>

### <a name="azure-rtos-guix-studio-desktop-wysiwyg-tool"></a><span data-ttu-id="2dc76-279">Azure RTOS Gux Studio masaüstü WYSıWYG aracı</span><span class="sxs-lookup"><span data-stu-id="2dc76-279">Azure RTOS GUIX Studio desktop WYSIWYG tool</span></span>

<span data-ttu-id="2dc76-280">Azure RTOS Gux Studio, kullanıcının GUI ekranlarını oluşturmak için kullanılan grafik öğelerini sürükleyip bırakması için tam bir WYSıWYG ekranı tasarım ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2dc76-280">Azure RTOS GUIX Studio provides a complete WYSIWYG screen design environment which allows the user to drag-and-drop graphical elements used to build the GUI screens.</span></span> <span data-ttu-id="2dc76-281">Azure RTOS Gux Studio otomatik olarak Azure RTOS Gux kitaplığı ile uyumlu C kodu oluşturur ve hedefte derlenmeye ve çalıştırılmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-281">Azure RTOS GUIX Studio automatically generates C code compatible with the Azure RTOS GUIX library, ready to be compiled and run on the target.</span></span> <span data-ttu-id="2dc76-282">Geliştiriciler, tümleşik Azure RTOS Gux Studio yazı tipi oluşturma aracı 'nı kullanarak bir uygulama içinde kullanılmak üzere önceden oluşturulmuş yazı tiplerini oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-282">Developers can produce pre-rendered fonts for use within an application using the integrated Azure RTOS GUIX Studio font generation tool.</span></span> <span data-ttu-id="2dc76-283">Yazı tipleri, tek renkli veya kenar yumuşatma uygulanmış biçimlerde oluşturulabilir ve hedefte yer kazanmak için iyileştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-283">Fonts can be generated in monochrome or anti-aliased formats, and are optimized to save space on the target.</span></span> <span data-ttu-id="2dc76-284">Yazı tiplerinde, çok dilli uygulamalar için Unicode karakterler de dahil olmak üzere herhangi bir karakter kümesi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-284">Fonts can include any set of characters, including Unicode characters for multi-lingual applications.</span></span>

<img alt="Diagram of SGS-TUV Saar certification logo" class="alignnone size-full wp-image-1500" height="341" sizes="(max-width: 535px) 100vw, 535px" src="./media/overview/studio_screen_shot.png"/>

<span data-ttu-id="2dc76-285">Azure RTOS Gux Studio, hedef sistemde kullanılmak üzere sıkıştırılan Azure RTOS Gux pixelmaps 'e dönüştürme ile PNG veya JPG dosyalarından grafiklerin içeri aktarılacağını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-285">Azure RTOS GUIX Studio facilitates the import of graphics from PNG or JPG files with conversion to compressed Azure RTOS GUIX Pixelmaps for use on the target system.</span></span> <span data-ttu-id="2dc76-286">Azure RTOS Gux pencere öğesi türlerinin birçoğu, özel bir görünüm ve kullanım için Kullanıcı grafiklerini içerecek şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-286">Many of the Azure RTOS GUIX widget types are designed to incorporate user graphics for a custom look and feel.</span></span> <span data-ttu-id="2dc76-287">Ayrıca, Azure RTOS Gux Studio, Azure RTOS Gux pencere öğeleri tarafından kullanılan varsayılan renklerin ve çizim stillerinin özelleştirilmesine olanak tanıyarak, geliştiricilerin Azure RTOS Gux 'in görünüşünü çok kolay bir şekilde ayarlamasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-287">In addition, Azure RTOS GUIX Studio allows customization of the default colors and drawing styles used by the Azure RTOS GUIX widgets, allowing developers to tune the appearance of Azure RTOS GUIX very easily.</span></span> <span data-ttu-id="2dc76-288">Uygulama dizelerinin oluşturulması ve bakımı, Azure RTOS Gux Studio 'nun başka bir yerleşik tesisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="2dc76-288">Generation and maintenance of application strings is another built-in facility of Azure RTOS GUIX Studio.</span></span> <span data-ttu-id="2dc76-289">Bu, geliştiricilerin geliştirme için bir dil kullanarak bir uygulama tasarlamasını ve ürün yayımlandıktan sonra hızlı ve kolay bir şekilde ek dil desteği eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2dc76-289">This enables developers to design an application using one language for developing, and quickly and easily add support for additional languages after the product is released.</span></span> <span data-ttu-id="2dc76-290">Azure RTOS Gux Studio ortamındaki bir BILGISAYAR masaüstünde, GUI kavramlarının ve ekran akışlarının test edilmesine ve ekran geçişlerinin ve animasyonların gözlemlerine yönelik bir hızlı ve kolay bir şekilde oluşturulmasına ve bu uygulamanın tamamına yönelik kapsamlı bir Azure RTOS Gux uygulaması çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-290">A complete Azure RTOS GUIX application can be executed on a PC desktop within the Azure RTOS GUIX Studio environment, allowing a quick and easy generation and demonstration of GUI concepts, testing of screen flows, and observation of screen transitions and animations.</span></span> <span data-ttu-id="2dc76-291">İşlem tamamlandığında tasarım, hedef Ready C veri yapıları olarak verilebildiğinden, Azure RTOS Gux ve Azure RTOS ThreadX kitaplıklarıyla derlenmeye ve bunlarla bağlantı kurulabilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-291">When completed, a design can be exported as target-ready C data structures, ready to be compiled and linked with the Azure RTOS GUIX and Azure RTOS ThreadX libraries.</span></span>

<span data-ttu-id="2dc76-292">Azure RTOS Gux ve Azure RTOS Gux Studio birden çok kaynak teması destekler ve bir uygulamanın çalışma zamanında kolayca yeniden başlatılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-292">Azure RTOS GUIX and Azure RTOS GUIX Studio support multiple resource themes, allowing an application to be easily reskinned at run-time.</span></span> <span data-ttu-id="2dc76-293">Yazı tipleri, renkler ve pixelmaps, tek bir basit API ile çalışma zamanında değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2dc76-293">Fonts, colors, and pixelmaps can be changed at run-time with one simple API.</span></span>

<span data-ttu-id="2dc76-294">GUX Studio hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="2dc76-294">Learn more about GUIX Studio</span></span>

### <a name="complete-win32-simulation"></a><span data-ttu-id="2dc76-295">Win32 simülasyonu</span><span class="sxs-lookup"><span data-stu-id="2dc76-295">Complete Win32 simulation</span></span>

<span data-ttu-id="2dc76-296">Azure RTOS Gux, hedef panoda çalışan tam olarak aynı çizim kitaplığını kullanarak bir Windows bilgisayarında çalışır.</span><span class="sxs-lookup"><span data-stu-id="2dc76-296">Azure RTOS GUIX runs on a Windows PC, using exactly the same drawing library that runs on the target board.</span></span> <span data-ttu-id="2dc76-297">Azure RTOS Gux ile, bılgısayarda GUI uygulaması oluşturup çalıştırabilir ve hata ayıklama, hızlı prototipleme, tanıtım ve WYSıWYG hedefi işlemi için Hedefinizdeki aynı uygulama kodunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2dc76-297">With Azure RTOS GUIX, you can build and run a GUI application on the PC, and use the same application code on your target for debugging, rapid prototyping, demonstration, and WYSIWYG target operation.</span></span>

### <a name="advanced-technology"></a><span data-ttu-id="2dc76-298">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="2dc76-298">Advanced technology</span></span>

* <span data-ttu-id="2dc76-299">Azure RTOS Gux 'in gelişmiş teknolojisi şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="2dc76-299">Azure RTOS GUIX's advanced technology incorporates:</span></span>
* <span data-ttu-id="2dc76-300">Alfa karıştırma</span><span class="sxs-lookup"><span data-stu-id="2dc76-300">Alpha blending</span></span>
* <span data-ttu-id="2dc76-301">Kenar yumuşatma</span><span class="sxs-lookup"><span data-stu-id="2dc76-301">Anti-Aliasing</span></span>
* <span data-ttu-id="2dc76-302">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2dc76-302">Automatic scaling</span></span>
* <span data-ttu-id="2dc76-303">Bit eşlem sıkıştırması</span><span class="sxs-lookup"><span data-stu-id="2dc76-303">Bitmap compression</span></span>
* <span data-ttu-id="2dc76-304">Tuval karışımı</span><span class="sxs-lookup"><span data-stu-id="2dc76-304">Canvas blending</span></span>
* <span data-ttu-id="2dc76-305">Özel pencere öğesi desteği</span><span class="sxs-lookup"><span data-stu-id="2dc76-305">Custom widget support</span></span>
* <span data-ttu-id="2dc76-306">Ertelenmiş çizim desteği</span><span class="sxs-lookup"><span data-stu-id="2dc76-306">Deferred drawing support</span></span>
* <span data-ttu-id="2dc76-307">Titreme desteği</span><span class="sxs-lookup"><span data-stu-id="2dc76-307">Dithering support</span></span>
* <span data-ttu-id="2dc76-308">Endian bağımsız programlama</span><span class="sxs-lookup"><span data-stu-id="2dc76-308">Endian neutral programming</span></span>
* <span data-ttu-id="2dc76-309">Donanım hızlandırıcısı desteği</span><span class="sxs-lookup"><span data-stu-id="2dc76-309">Hardware accelerator support</span></span>
* <span data-ttu-id="2dc76-310">Çok dilli destek ve UTF-8 kodlaması</span><span class="sxs-lookup"><span data-stu-id="2dc76-310">Multilingual support and UTF-8 encoding</span></span>
* <span data-ttu-id="2dc76-311">Birden çok görüntü ve tuval desteği</span><span class="sxs-lookup"><span data-stu-id="2dc76-311">Multiple display and canvas support</span></span>
* <span data-ttu-id="2dc76-312">En iyi duruma getirilmiş kırpma, çizim ve olay işleme</span><span class="sxs-lookup"><span data-stu-id="2dc76-312">Optimized clipping, drawing, and event handling</span></span>
* <span data-ttu-id="2dc76-313">Çalışma zamanı JPEG ve PNG kod çözücü</span><span class="sxs-lookup"><span data-stu-id="2dc76-313">Runtime JPEG and PNG decoder</span></span>
* <span data-ttu-id="2dc76-314">Kaplama ve Temalar</span><span class="sxs-lookup"><span data-stu-id="2dc76-314">Skinning and Themes</span></span>
* <span data-ttu-id="2dc76-315">Tek renkli 32 bitlik gerçek renk ile alfa grafik biçimlerini destekler</span><span class="sxs-lookup"><span data-stu-id="2dc76-315">Supports monochrome through 32-bit true-color with alpha graphics formats</span></span>
* <span data-ttu-id="2dc76-316">Geçişler, sprites ve animasyon desteği</span><span class="sxs-lookup"><span data-stu-id="2dc76-316">Transitions, Sprites, and Animation support</span></span>
* <span data-ttu-id="2dc76-317">Win32 simülasyonu</span><span class="sxs-lookup"><span data-stu-id="2dc76-317">Win32 simulation</span></span>
* <span data-ttu-id="2dc76-318">Viewports ve Z düzeninde bakım dahil olmak üzere pencere yönetimi</span><span class="sxs-lookup"><span data-stu-id="2dc76-318">Window management including Viewports and Z-order maintenance</span></span>
