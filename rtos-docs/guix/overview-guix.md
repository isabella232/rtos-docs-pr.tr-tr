---
title: Azure RTOS Gux ve Azure RTOS Gux Studio 'Yu anlama
description: Azure RTOS Gux, katıştırılmış sistem geliştiricilerin ihtiyaçlarını karşılamak için oluşturulmuş bir profesyonel kalite paketidir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0d0ff37784673f851ab918e20b255d19ddf98b0f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827094"
---
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a><span data-ttu-id="12a04-103">Azure RTOS Gux ve Azure RTOS Gux Studio 'ya genel bakış</span><span class="sxs-lookup"><span data-stu-id="12a04-103">Overview of Azure RTOS GUIX and Azure RTOS GUIX Studio</span></span>

<span data-ttu-id="12a04-104">Azure Gux Embedded GUI, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf GUI çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="12a04-104">Azure GUIX embedded GUI is Microsoft’s advanced, industrial grade GUI solution designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="12a04-105">Microsoft ayrıca, Azure RTOS Gux Studio adlı tam özellikli bir WYSıWYG masaüstü tasarım aracı sağlar. bu sayede, geliştiricilerin masaüstündeki GUI 'sini tasarlamalarını ve hedefe aktarılabilecek Azure RTOS Gux Embedded GUI kodunu oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-105">Microsoft also provides a full-featured WYSIWYG desktop design tool named Azure RTOS GUIX Studio, which allows developers to design their GUI on the desktop and generate Azure RTOS GUIX embedded GUI code that can then be exported to the target.</span></span> <span data-ttu-id="12a04-106">Azure RTOS Gux Azure RTOS ThreadX RTOS ile tamamen tümleşiktir ve Azure RTOS ThreadX tarafından desteklenen işlemcilerin birçoğu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-106">Azure RTOS GUIX is fully integrated with Azure RTOS ThreadX RTOS and is available for many of the same processors supported by Azure RTOS ThreadX.</span></span> <span data-ttu-id="12a04-107">Bunun hepsi son derece küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla, Azure RTOS Gux 'i bir kullanıcı arabirimi gerektiren en zorlu eklenmiş IoT uygulamalarına yönelik ideal seçim haline getirir.</span><span class="sxs-lookup"><span data-stu-id="12a04-107">All of this combined with an extremely small footprint, fast execution, and superior ease-of-use, make Azure RTOS GUIX the ideal choice for the most demanding embedded IoT applications requiring a user interface.</span></span> 

## <a name="azure-rtos-guix-api"></a><span data-ttu-id="12a04-108">Azure RTOS Gux API 'SI</span><span class="sxs-lookup"><span data-stu-id="12a04-108">Azure RTOS GUIX API</span></span>

### <a name="intuitive-and-consistent-api"></a><span data-ttu-id="12a04-109">Sezgisel ve tutarlı API</span><span class="sxs-lookup"><span data-stu-id="12a04-109">Intuitive and consistent API</span></span>

* <span data-ttu-id="12a04-110">İsim-fiil adlandırma kuralı</span><span class="sxs-lookup"><span data-stu-id="12a04-110">Noun-verb naming convention</span></span>

* <span data-ttu-id="12a04-111">Tüm API 'Lerde Azure RTOS Gux olarak kolayca tanımlanabilmesi için önde gelen *gx_* vardır</span><span class="sxs-lookup"><span data-stu-id="12a04-111">All APIs have leading *gx_* to easily identify as Azure RTOS GUIX</span></span>

* <span data-ttu-id="12a04-112">Olay odaklı programlama modeli (API)</span><span class="sxs-lookup"><span data-stu-id="12a04-112">Event-driven programming model (API)</span></span>

* <span data-ttu-id="12a04-113">Gerektiğinde doğrudan tuval çizimi için tam destek</span><span class="sxs-lookup"><span data-stu-id="12a04-113">Full support for direct canvas drawing when needed</span></span>

* <span data-ttu-id="12a04-114">Azure RTOS Gux Studio tarafından üretilen kodla kolay bir şekilde etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="12a04-114">Simple to interact with Azure RTOS GUIX Studio generated code</span></span>

* <span data-ttu-id="12a04-115">Çizgi, dikdörtgen, çokgen vb. için API 'Ler</span><span class="sxs-lookup"><span data-stu-id="12a04-115">APIs for line, rectangle, polygon, etc.</span></span>

* <span data-ttu-id="12a04-116">Daire, yay, pasta, kii, elips, vb. için API 'Ler.</span><span class="sxs-lookup"><span data-stu-id="12a04-116">APIs for circle, arc, pie, chord, ellipse, etc.</span></span>

* <span data-ttu-id="12a04-117">Metin çizme ve konumlandırma için API 'Ler</span><span class="sxs-lookup"><span data-stu-id="12a04-117">APIs for text drawing and positioning</span></span>

* <span data-ttu-id="12a04-118">Kenar yumuşatma, doku dolguları ve düz dolgular</span><span class="sxs-lookup"><span data-stu-id="12a04-118">Anti-aliasing, texture fills, and solid fills</span></span>

* <span data-ttu-id="12a04-119">Ekranları ve pencere öğelerini oluşturmak ve yeniden oluşturmak için API 'Ler</span><span class="sxs-lookup"><span data-stu-id="12a04-119">APIs for creating and modifing screens and widgets</span></span>

### <a name="azure-rtos-guix-studio-generated-files"></a><span data-ttu-id="12a04-120">Azure RTOS Gux Studio tarafından oluşturulan dosyalar</span><span class="sxs-lookup"><span data-stu-id="12a04-120">Azure RTOS GUIX Studio Generated Files</span></span>

* <span data-ttu-id="12a04-121">Otomatik olarak oluşturulan ANSI C kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="12a04-121">Automatically generated ANSI C source files</span></span>

* <span data-ttu-id="12a04-122">Düzen ayrıntılarından uygulama yazılımını yalıtılmış olarak</span><span class="sxs-lookup"><span data-stu-id="12a04-122">Insulates application software from layout details</span></span>

* <span data-ttu-id="12a04-123">Kullanıcı arabirimi tasarımı için gereken yazı tiplerini ve görüntüleri içerir</span><span class="sxs-lookup"><span data-stu-id="12a04-123">Includes fonts and images required by UI design</span></span>

* <span data-ttu-id="12a04-124">Uygulama koduyla derlenen oluşturulan dosyalar</span><span class="sxs-lookup"><span data-stu-id="12a04-124">Generated files compiled with application code</span></span>

* <span data-ttu-id="12a04-125">Ekran düzeni, uygulama mantığını etkilemeden güncelleştirilebilen</span><span class="sxs-lookup"><span data-stu-id="12a04-125">Screen layout can be updated without affecting application logic</span></span>

* <span data-ttu-id="12a04-126">Kaynak kimlikleri dil ve tema bağımsızlık oluşturma</span><span class="sxs-lookup"><span data-stu-id="12a04-126">Resource IDs create language and theme independence</span></span>

* <span data-ttu-id="12a04-127">Kullanıcı tarafından sağlanan özel çizim ve olay işleme işlevleri</span><span class="sxs-lookup"><span data-stu-id="12a04-127">User-supplied custom drawing and event processing functions</span></span>

### <a name="widget-library"></a><span data-ttu-id="12a04-128">Pencere öğesi kitaplığı</span><span class="sxs-lookup"><span data-stu-id="12a04-128">Widget library</span></span>

* <span data-ttu-id="12a04-129">Önceden tanımlanmış ancak özelleştirilebilir ortak arabirim öğeleri kümesi</span><span class="sxs-lookup"><span data-stu-id="12a04-129">Pre-defined but customizable set of common interface elements</span></span>

* <span data-ttu-id="12a04-130">Son derece küçük, kompakt ve verimli</span><span class="sxs-lookup"><span data-stu-id="12a04-130">Extremely small, compact, and efficient</span></span>

* <span data-ttu-id="12a04-131">Kitaplık, düğme, ölçer, liste, pencere, kaydırma, kaydırıcı, ilerleme çubuğu, istem ve çok daha fazlasını içerir</span><span class="sxs-lookup"><span data-stu-id="12a04-131">Library includes button, gauge, list, window, scroll, slider, progress bar, prompt and many more</span></span>

* <span data-ttu-id="12a04-132">Tamamen özelleştirilebilir çizim ve görünüm</span><span class="sxs-lookup"><span data-stu-id="12a04-132">Fully customizable drawing and appearance</span></span>

* <span data-ttu-id="12a04-133">Tamamen özelleştirilebilir işlem ve olay işleme</span><span class="sxs-lookup"><span data-stu-id="12a04-133">Fully customizable operation and event handling</span></span>

* <span data-ttu-id="12a04-134">Yalnızca kullanılan pencere öğeleri uygulama yazılımıyla bağlantılı</span><span class="sxs-lookup"><span data-stu-id="12a04-134">Only the widgets used are linked with application software</span></span>

### <a name="math-and-utilities"></a><span data-ttu-id="12a04-135">Matematik ve yardımcı programlar</span><span class="sxs-lookup"><span data-stu-id="12a04-135">Math and utilities</span></span>

* <span data-ttu-id="12a04-136">Sin, cos, Arcsin, arccos, tanjant, kare kök işlevleri</span><span class="sxs-lookup"><span data-stu-id="12a04-136">Functions for sin, cos, arcsin, arccos, tangent, square root</span></span>

* <span data-ttu-id="12a04-137">Ekran bölgelerini düzenleme işlevleri</span><span class="sxs-lookup"><span data-stu-id="12a04-137">Functions for manipulating screen regions</span></span>

* <span data-ttu-id="12a04-138">Sistem Yapılandırması ve başlangıç</span><span class="sxs-lookup"><span data-stu-id="12a04-138">System configuration and startup</span></span>

* <span data-ttu-id="12a04-139">Bellek havuzu tanımı (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="12a04-139">Memory pool definition (optional)</span></span>

* <span data-ttu-id="12a04-140">Zamanlayıcı yönetimi</span><span class="sxs-lookup"><span data-stu-id="12a04-140">Timer Management</span></span>

* <span data-ttu-id="12a04-141">Animasyon yönetimi</span><span class="sxs-lookup"><span data-stu-id="12a04-141">Animation Management</span></span>

* <span data-ttu-id="12a04-142">Kirli liste Bakımı</span><span class="sxs-lookup"><span data-stu-id="12a04-142">Dirty list maintenance</span></span>

### <a name="image-processing"></a><span data-ttu-id="12a04-143">Görüntü işleme</span><span class="sxs-lookup"><span data-stu-id="12a04-143">Image processing</span></span>

* <span data-ttu-id="12a04-144">JPEG ve PNG görüntülerinin çalışma zamanı kodunu çözme işlevleri</span><span class="sxs-lookup"><span data-stu-id="12a04-144">Functions for runtime decode of jpeg and png images</span></span>

* <span data-ttu-id="12a04-145">Titreme ve renk alanı dönüştürmeyi Uygula</span><span class="sxs-lookup"><span data-stu-id="12a04-145">Apply dithering and color space conversion</span></span>

* <span data-ttu-id="12a04-146">Görüntü döndürme</span><span class="sxs-lookup"><span data-stu-id="12a04-146">Image rotation</span></span>

* <span data-ttu-id="12a04-147">Görüntü ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="12a04-147">Image scaling</span></span>

* <span data-ttu-id="12a04-148">Görüntü karıştırma</span><span class="sxs-lookup"><span data-stu-id="12a04-148">Image blending</span></span>

### <a name="event-processing"></a><span data-ttu-id="12a04-149">Olay işleme</span><span class="sxs-lookup"><span data-stu-id="12a04-149">Event processing</span></span>

* <span data-ttu-id="12a04-150">Boştayken Azure RTOS Gux iş parçacığını otomatik olarak askıya alır</span><span class="sxs-lookup"><span data-stu-id="12a04-150">Automatically suspends Azure RTOS GUIX thread when idle</span></span>

* <span data-ttu-id="12a04-151">UI tasarımında popüler olay odaklı programlama modeli</span><span class="sxs-lookup"><span data-stu-id="12a04-151">Event-driven programming model popular in UI design</span></span>

* <span data-ttu-id="12a04-152">Azure RTOS Gux çizim iş parçacığından giriş sürücülerini yalıtılmış olarak</span><span class="sxs-lookup"><span data-stu-id="12a04-152">Insulates input drivers from Azure RTOS GUIX drawing thread</span></span>

* <span data-ttu-id="12a04-153">Olayları gönderme ve alma işlevleri</span><span class="sxs-lookup"><span data-stu-id="12a04-153">Functions for sending and receiving events</span></span>

* <span data-ttu-id="12a04-154">Tüm Azure RTOS Gux pencere öğesi türleri için önceden tanımlanmış olay türleri</span><span class="sxs-lookup"><span data-stu-id="12a04-154">Pre-defined event types for all Azure RTOS GUIX widget types</span></span>

* <span data-ttu-id="12a04-155">Kullanıcı tanımlı özel olaylar destekleniyor</span><span class="sxs-lookup"><span data-stu-id="12a04-155">User-defined custom events supported</span></span>

### <a name="canvas-processing"></a><span data-ttu-id="12a04-156">Tuval işleme</span><span class="sxs-lookup"><span data-stu-id="12a04-156">Canvas processing</span></span>

* <span data-ttu-id="12a04-157">Kırpma ve Z düzeninde bakım</span><span class="sxs-lookup"><span data-stu-id="12a04-157">Clipping and Z-Order maintenance</span></span>

* <span data-ttu-id="12a04-158">Donanım ayrıntılarından pencere öğesi kitaplığını yalıtılmış olarak</span><span class="sxs-lookup"><span data-stu-id="12a04-158">Insulates widget library from hardware details</span></span>

* <span data-ttu-id="12a04-159">Uygulamanın donanım ayrıntılarından yalıtılmış olması</span><span class="sxs-lookup"><span data-stu-id="12a04-159">Insulates application from hardware details</span></span>

* <span data-ttu-id="12a04-160">Kirli alanların otomatik arka plan yenilemesi</span><span class="sxs-lookup"><span data-stu-id="12a04-160">Automatic background refresh of dirty areas</span></span>

* <span data-ttu-id="12a04-161">Katmanlama ve karıştırma desteği ile birden çok canvaya</span><span class="sxs-lookup"><span data-stu-id="12a04-161">Multiple canvases with layering and blending supported</span></span>

* <span data-ttu-id="12a04-162">Uygulama yazılımı tarafından doğrudan çağrılabilir</span><span class="sxs-lookup"><span data-stu-id="12a04-162">Can be invoked directly by the application software</span></span>

### <a name="input-device-drivers"></a><span data-ttu-id="12a04-163">Giriş cihazı sürücüleri</span><span class="sxs-lookup"><span data-stu-id="12a04-163">Input device driver(s)</span></span>

* <span data-ttu-id="12a04-164">Donanıma özel destek, Azure RTOS Gux ve donanım ayrıntılarından yalıtılmış uygulama</span><span class="sxs-lookup"><span data-stu-id="12a04-164">Hardware-specific support, Azure RTOS GUIX and application insulated from hardware details</span></span>

* <span data-ttu-id="12a04-165">Dirensel dokunma, uç Touch ve tuş takımı destekleniyor</span><span class="sxs-lookup"><span data-stu-id="12a04-165">Resistive Touch, Cap Touch, and keypad supported</span></span>

* <span data-ttu-id="12a04-166">Azure RTOS Gux olay kuyruğuna geçirilen giriş olayları</span><span class="sxs-lookup"><span data-stu-id="12a04-166">Input events passed to Azure RTOS GUIX event queue</span></span>

### <a name="display-drivers"></a><span data-ttu-id="12a04-167">Görüntü sürücüleri</span><span class="sxs-lookup"><span data-stu-id="12a04-167">Display drivers</span></span>

* <span data-ttu-id="12a04-168">Donanıma özgü destek</span><span class="sxs-lookup"><span data-stu-id="12a04-168">Hardware-specific support</span></span>

* <span data-ttu-id="12a04-169">Tüm renk derinliği ve biçimleri için sunulan genel sürücüler</span><span class="sxs-lookup"><span data-stu-id="12a04-169">Generic drivers provided for all color depth and formats</span></span>

* <span data-ttu-id="12a04-170">Kullanılabilir grafik hızlandırıcılarını kullanacak şekilde özelleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="12a04-170">Customized to utilize available graphics accelerators</span></span>

### <a name="target-hardware"></a><span data-ttu-id="12a04-171">Hedef donanım</span><span class="sxs-lookup"><span data-stu-id="12a04-171">Target hardware</span></span>

* <span data-ttu-id="12a04-172">Grafik çıkışı yapabilen neredeyse tüm donanımlar, GUıDX ile uyumludur</span><span class="sxs-lookup"><span data-stu-id="12a04-172">Nearly any hardware capable of graphical output Is compatible with GUIX</span></span>

* <span data-ttu-id="12a04-173">Birden çok fiziksel görüntüleme destekleniyor</span><span class="sxs-lookup"><span data-stu-id="12a04-173">Multiple physical displays supported</span></span>

* <span data-ttu-id="12a04-174">En az RAM ve Flash gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="12a04-174">Minimal RAM and Flash requirements</span></span>

## <a name="create-elegant-user-interfaces"></a><span data-ttu-id="12a04-175">Zarif Kullanıcı arabirimleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="12a04-175">Create Elegant User Interfaces</span></span>

<span data-ttu-id="12a04-176">Azure RTOS Gux ve Azure RTOS Gux Studio, benzersiz şekilde zarif Kullanıcı arabirimleri oluşturmak için gereken tüm özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-176">Azure RTOS GUIX and Azure RTOS GUIX Studio provide all the features necessary to create uniquely elegant user interfaces.</span></span> <span data-ttu-id="12a04-177">Standart Azure RTOS Gux paketi, tıbbi cihaz başvurusu, akıllı bir izleme başvurusu, bir giriş otomasyon başvurusu, endüstriyel denetim başvurusu, bir otomatik Molem başvurusu ve çeşitli sprite ve animasyon örnekleri dahil olmak üzere çeşitli örnek kullanıcı arabirimlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="12a04-177">The standard Azure RTOS GUIX package includes various sample user interfaces, including a medical device reference, a smart watch reference, a home automation reference, an industrial control reference, an automotive reference, and various sprite and animation examples.</span></span> <span data-ttu-id="12a04-178">Lütfen aşağıda gösterilen başvuru örneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12a04-178">Please click on the reference examples shown below.</span></span>

### <a name="home-automation"></a><span data-ttu-id="12a04-179">Ana Otomasyon</span><span class="sxs-lookup"><span data-stu-id="12a04-179">Home Automation</span></span>

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a><span data-ttu-id="12a04-180">Birinin</span><span class="sxs-lookup"><span data-stu-id="12a04-180">Medical</span></span>

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a><span data-ttu-id="12a04-181">Tüketici</span><span class="sxs-lookup"><span data-stu-id="12a04-181">Consumer</span></span>

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a><span data-ttu-id="12a04-182">Beyaz mallar</span><span class="sxs-lookup"><span data-stu-id="12a04-182">White Goods</span></span>

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a><span data-ttu-id="12a04-183">Otomotiv</span><span class="sxs-lookup"><span data-stu-id="12a04-183">Automotive</span></span>

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a><span data-ttu-id="12a04-184">Sanayi</span><span class="sxs-lookup"><span data-stu-id="12a04-184">Industrial</span></span>

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

<span data-ttu-id="12a04-185">Her Azure RTOS Gux başvurusunda, başvuru tasarımının tüm grafik öğelerini tanımlayan karşılık gelen bir Azure RTOS Gux Studio projesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="12a04-185">Each Azure RTOS GUIX reference has a corresponding Azure RTOS GUIX Studio project that defines all the graphical elements of the reference design.</span></span> <span data-ttu-id="12a04-186">Başvuru tasarımını değiştirmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="12a04-186">Changing a reference design is easy.</span></span> <span data-ttu-id="12a04-187">Yalnızca ilgili Azure RTOS Gux projesini açın, istenen değişiklikleri yapın, projeyi kaydedin ve *Proje*' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="12a04-187">Simply open the corresponding Azure RTOS GUIX project, make the desired changes, save the project, and then select *Project*.</span></span>

<span data-ttu-id="12a04-188">Azure RTOS Gux için C kodu oluşturmak üzere tüm çıkış dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="12a04-188">Generate All Output Files to generate the C code for Azure RTOS GUIX.</span></span> <span data-ttu-id="12a04-189">Ardından hedef uygulamayı yeniden oluşturup değiştirilen başvuru tasarımını gözlemleyecek şekilde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="12a04-189">Then simply rebuild the target application and run to observe the modified reference design.</span></span>

### <a name="small-footprint"></a><span data-ttu-id="12a04-190">Küçük ayak izi</span><span class="sxs-lookup"><span data-stu-id="12a04-190">Small-footprint</span></span>

<span data-ttu-id="12a04-191">Azure RTOS Gux, bir tuval için gereken belleği dahil etmez ve temel destek için 13.2 KB 'lık FLASH ve 4KB RAM 'in daha az küçük bir ayak izine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="12a04-191">Azure RTOS GUIX has a remarkably small minimal footprint of 13.2KB of FLASH and 4KB RAM for basic support, not including the memory required for a canvas.</span></span>

<span data-ttu-id="12a04-192">Dahili GRAM ve kendi kendini yenileme teknolojisine sahip bir ekran için tuval belleği gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="12a04-192">For a display with internal GRAM and self-refresh technology, no canvas memory is required.</span></span> <span data-ttu-id="12a04-193">Ancak, çizim performansını artırmak veya görüntüleme için yerel olarak kullanılan bir görüntüleme yapılandırması için, uygulama tarafından bir tuval bellek alanı tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="12a04-193">However, to improve drawing performance, or for a display configuration that does not utilize GRAM local to the display, a canvas memory area is defined by the application.</span></span>

<span data-ttu-id="12a04-194">Tuval bellek gereksinimleri, Tuval boyutunun ve renk derinliğinin bir işlevidir ve formül tarafından tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="12a04-194">Canvas memory requirements are a function of the canvas size as well as the color depth, and are defined by the formula:</span></span>

<span data-ttu-id="12a04-195"><i>Tuval RAM (bayt) = (x \* y \* (BPP/8))</i></span><span class="sxs-lookup"><span data-stu-id="12a04-195"><i>Canvas RAM (bytes) = (x \* y \* (bpp/8))</i></span></span>

<span data-ttu-id="12a04-196">Burada "x" ve "y", tuvalin boyutlarıdır (görüntü).</span><span class="sxs-lookup"><span data-stu-id="12a04-196">Where “x” and “y” are the dimensions of the canvas (display).</span></span>

<span data-ttu-id="12a04-197">Çoğu uygulama, temel Azure RTOS Gux kitaplığı depolama gereksinimlerine dahil olmayan grafik kaynakları da kullanır.</span><span class="sxs-lookup"><span data-stu-id="12a04-197">Most applications also utilize graphical resources, which are not included in the core Azure RTOS GUIX library storage requirements.</span></span> <span data-ttu-id="12a04-198">Bu kaynaklar, yazı tiplerini, grafik simgelerini (pixelmaps) ve statik dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="12a04-198">These resources include fonts, graphical icons (pixelmaps), and static strings.</span></span> <span data-ttu-id="12a04-199">Bu veriler, const bellek bölümünde (örn. FLASH) depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-199">This data can be stored in the const memory section (i.e. FLASH).</span></span>

<span data-ttu-id="12a04-200">Bu bellek alanının boyutu, kullanılan benzersiz yazı tiplerinin sayısını ve boyutunu, kullanılan grafik simgelerinin sayısını ve boyutunu, çıkış rengi biçimini ve her bir kaynağın sıkıştırılmış verileri kullanıp kullanmadığını, her iki yazı tipinin ve pixelmap verilerinin RLE sıkıştırmasını desteklediğinden bu yana bir dizi etkene bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="12a04-200">The size of this memory area is dependent on a number of factors, including the number and size of unique fonts used, the number and size of the graphical icons used, the output color format, and whether or not each resource is using compressed data, since Azure RTOS GUIX supports RLE compression of both font and pixelmap data.</span></span> <span data-ttu-id="12a04-201">Her kaynak için depolama gereksinimleri, Azure RTOS Gux Studio uygulamasında görüntülenir ve kullanıcının uygulama kaynakları tarafından tüketilen Flash bellek miktarını izlemesine ve izlemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-201">The storage requirements for each resource are displayed within the Azure RTOS GUIX Studio application, allowing the user to track and monitor the amount of flash memory that will be consumed by the application resources.</span></span>

<span data-ttu-id="12a04-202">Azure RTOS ThreadX gibi Azure RTOS Gux boyutu, uygulama tarafından gerçekten kullanılan hizmetlere göre otomatik olarak ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-202">Like Azure RTOS ThreadX, the size of Azure RTOS GUIX automatically scales based on the services actually used by the application.</span></span> <span data-ttu-id="12a04-203">Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="12a04-203">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

### <a name="fast-execution"></a><span data-ttu-id="12a04-204">Hızlı yürütme</span><span class="sxs-lookup"><span data-stu-id="12a04-204">Fast execution</span></span>

<span data-ttu-id="12a04-205">Azure RTOS Gux, özel olarak C dilinde yazılır ve hız için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="12a04-205">Azure RTOS GUIX is written exclusively in C and is designed for speed.</span></span> <span data-ttu-id="12a04-206">Azure RTOS Gux, en az iç işlev çağrısı katmanlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="12a04-206">Azure RTOS GUIX has minimal internal function call layering.</span></span>

<span data-ttu-id="12a04-207">Ayrıca, Azure RTOS Gux, iyileştirilmiş kırpma, çizim ve olay işleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-207">In addition, Azure RTOS GUIX provides optimized clipping, drawing, and event handling.</span></span> <span data-ttu-id="12a04-208">Tüm bu ve genel performansa dayalı bir tasarım felsesı, Azure RTOS Gux 'in olası en hızlı performansı elde etmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="12a04-208">All of this and a general performance-oriented design philosophy help Azure RTOS GUIX achieve the fastest possible performance.</span></span>

### <a name="pre-certified--by-tuv-to-many-safety-standards"></a><span data-ttu-id="12a04-209">TUV tarafından birçok güvenlik standartlarına önceden sertifikalı</span><span class="sxs-lookup"><span data-stu-id="12a04-209">Pre-certified  by TUV to many safety standards</span></span>

<span data-ttu-id="12a04-210">Azure RTOS Gux, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW güvenlik sınıfı C, ISO 26262 ASIL D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir.</span><span class="sxs-lookup"><span data-stu-id="12a04-210">Azure RTOS GUIX has been certified by SGS-TUV  Saar for use in safety-critical systems, according to IEC-61508 SIL 4, IEC-62304  SW Safety Class C, ISO 26262 ASIL D and EN 50128.</span></span> <span data-ttu-id="12a04-211">Sertifika, Azure RTOS Gux 'in, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımların geliştirilmesinde kullanılabileceğini onaylar.</span><span class="sxs-lookup"><span data-stu-id="12a04-211">The certification confirms that Azure RTOS GUIX can be used in the development of safety-related software for the highest safety integrity levels of IEC-61508, IEC-62304, ISO 26262 and EN 50128 for the “Functional Safety of electrical, electronic, and programmable electronic safety-related systems.”</span></span> <span data-ttu-id="12a04-212">Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="12a04-212">SGS-TUV Saar, formed through a joint venture of Germany’s SGS-Group and TUV Saarland, has become the leading accredited, independent company for testing, auditing, verifying and certifying embedded software for safety-related systems worldwide.</span></span> <span data-ttu-id="12a04-213">Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenlik düzeyini güvence altına almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="12a04-213">The industrial safety standard IEC 61508, and all standards that are derived from it, including IEC-62304, ISO 26262 and EN 50128, are used to assure the functional safety of electrical, electronic, and programmable electronic safety-related medical devices, process control systems, industrial machinery, automobiles and railway control systems.</span></span>

<img alt="SGS-TUV Saar" class="img-responsive" src="https://rtos.com/wp-content/uploads/2017/10/partener-logo-sgs-tuv-saar-2.png"/>

#### <a name="simple-easy-to-use"></a><span data-ttu-id="12a04-214">Basit, kullanımı kolay</span><span class="sxs-lookup"><span data-stu-id="12a04-214">Simple, easy-to-use</span></span>

<span data-ttu-id="12a04-215">Azure RTOS Gux kullanımı çok basittir ve Azure RTOS Gux Studio, geliştiricilerin masaüstünü görsel olarak tasarlamasına ve gerçek hedefte çalışan C kodu oluşturmasına izin vererek daha da kolay hale gelir.</span><span class="sxs-lookup"><span data-stu-id="12a04-215">Azure RTOS GUIX is very simple to use and Azure RTOS GUIX Studio makes it even easier by allowing developers to visually design on the desktop and generate C code that runs on the actual target.</span></span> <span data-ttu-id="12a04-216">Uygulamalar daha sonra kendi özel olay işleme ve çizim işlevlerini ekleyerek GUI 'sini tamamlamalarını sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-216">Applications can then add their own custom event handling and drawing functions to complete their GUI.</span></span>

<span data-ttu-id="12a04-217">Azure RTOS Gux API 'SI kullanımı basittir.</span><span class="sxs-lookup"><span data-stu-id="12a04-217">Using the Azure RTOS GUIX API is straightforward.</span></span> <span data-ttu-id="12a04-218">Azure RTOS Gux API 'SI sezgisel ve yüksek işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="12a04-218">The Azure RTOS GUIX API is both intuitive and highly functional.</span></span> <span data-ttu-id="12a04-219">API adları, gerçek sözcüklerden oluşur ve "alfabe adı" ve/veya diğer dosya sistemi ürünlerinde ortak olan çok sayıda kısaltılmış isimlerdir.</span><span class="sxs-lookup"><span data-stu-id="12a04-219">The API names are made of real words and not the “alphabet soup” and/or the highly abbreviated names that are so common in other file system products.</span></span> <span data-ttu-id="12a04-220">Tüm Azure RTOS Gux API 'Lerinin önde bir *gx_* vardır ve bir ad fiil adlandırma kuralını takip edin.</span><span class="sxs-lookup"><span data-stu-id="12a04-220">All Azure RTOS GUIX APIs have a leading *gx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="12a04-221">Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="12a04-221">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="12a04-222">Örneğin, bir pencere öğesi denetim bloğunu başlatacak tüm API 'Ler &lt; widget_type &gt; _Create olarak adlandırılır ve her pencere öğesi türü için oluşturma işlevi parametreleri her zaman aynı sırada tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="12a04-222">For example, all APIs that initialize a widget control block are named &lt; widget_type&gt;_create, and the create function parameters for each widget type are always defined in the same order.</span></span>

### <a name="comprehensive-set-of-built-in-widgets"></a><span data-ttu-id="12a04-223">Kapsamlı yerleşik pencere öğeleri kümesi</span><span class="sxs-lookup"><span data-stu-id="12a04-223">Comprehensive set of built-in widgets</span></span>

* <span data-ttu-id="12a04-224">Azure RTOS Gux, aşağıdakiler dahil olmak üzere zengin bir yerleşik pencere öğesi kümesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="12a04-224">Azure RTOS GUIX provides a rich set of built-in widgets, including:</span></span>

* <span data-ttu-id="12a04-225">Accordion menüsü</span><span class="sxs-lookup"><span data-stu-id="12a04-225">Accordion Menu</span></span>

* <span data-ttu-id="12a04-226">Düğme</span><span class="sxs-lookup"><span data-stu-id="12a04-226">Button</span></span>

* <span data-ttu-id="12a04-227">Onay kutusu</span><span class="sxs-lookup"><span data-stu-id="12a04-227">Checkbox</span></span>

* <span data-ttu-id="12a04-228">Dairesel ölçer</span><span class="sxs-lookup"><span data-stu-id="12a04-228">Circular Gauge</span></span>

* <span data-ttu-id="12a04-229">Açılan liste</span><span class="sxs-lookup"><span data-stu-id="12a04-229">Drop Down List</span></span>

* <span data-ttu-id="12a04-230">Yatay liste</span><span class="sxs-lookup"><span data-stu-id="12a04-230">Horizontal List</span></span>

* <span data-ttu-id="12a04-231">Yatay kaydırma çubuğu penceresi</span><span class="sxs-lookup"><span data-stu-id="12a04-231">Horizontal Scrollbar Window</span></span>

* <span data-ttu-id="12a04-232">Simge</span><span class="sxs-lookup"><span data-stu-id="12a04-232">Icon</span></span>

* <span data-ttu-id="12a04-233">Simge düğmesi</span><span class="sxs-lookup"><span data-stu-id="12a04-233">Icon Button</span></span>

* <span data-ttu-id="12a04-234">Çizgi grafik</span><span class="sxs-lookup"><span data-stu-id="12a04-234">Line Chart</span></span>

* <span data-ttu-id="12a04-235">Menü</span><span class="sxs-lookup"><span data-stu-id="12a04-235">Menu</span></span>

* <span data-ttu-id="12a04-236">Çok satırlı metin düğmesi</span><span class="sxs-lookup"><span data-stu-id="12a04-236">Multi Line Text Button</span></span>

* <span data-ttu-id="12a04-237">Çok satırlı metin girişi</span><span class="sxs-lookup"><span data-stu-id="12a04-237">Multi Line Text Input</span></span>

* <span data-ttu-id="12a04-238">Çok satırlı metin görünümü</span><span class="sxs-lookup"><span data-stu-id="12a04-238">Multi Line Text View</span></span>

* <span data-ttu-id="12a04-239">Sayısal pixelmap Istemi</span><span class="sxs-lookup"><span data-stu-id="12a04-239">Numeric Pixelmap Prompt</span></span>

* <span data-ttu-id="12a04-240">Sayısal Istem</span><span class="sxs-lookup"><span data-stu-id="12a04-240">Numeric Prompt</span></span>

* <span data-ttu-id="12a04-241">Sayısal kaydırma tekerleği</span><span class="sxs-lookup"><span data-stu-id="12a04-241">Numeric Scroll Wheel</span></span>

* <span data-ttu-id="12a04-242">Pixelmap düğmesi</span><span class="sxs-lookup"><span data-stu-id="12a04-242">Pixelmap Button</span></span>

* <span data-ttu-id="12a04-243">Pixelmap Istemi</span><span class="sxs-lookup"><span data-stu-id="12a04-243">Pixelmap Prompt</span></span>

* <span data-ttu-id="12a04-244">Pixelmap kaydırıcısı</span><span class="sxs-lookup"><span data-stu-id="12a04-244">Pixelmap Slider</span></span>

* <span data-ttu-id="12a04-245">Pixelmap Sprite</span><span class="sxs-lookup"><span data-stu-id="12a04-245">Pixelmap Sprite</span></span>

* <span data-ttu-id="12a04-246">İlerleme Çubuğu</span><span class="sxs-lookup"><span data-stu-id="12a04-246">Progress Bar</span></span>

* <span data-ttu-id="12a04-247">İstem</span><span class="sxs-lookup"><span data-stu-id="12a04-247">Prompt</span></span>

* <span data-ttu-id="12a04-248">Radyal Ilerleme çubuğu</span><span class="sxs-lookup"><span data-stu-id="12a04-248">Radial Progress Bar</span></span>

* <span data-ttu-id="12a04-249">Radyo Düğmesi</span><span class="sxs-lookup"><span data-stu-id="12a04-249">Radio Button</span></span>

* <span data-ttu-id="12a04-250">Tekerleği kaydır</span><span class="sxs-lookup"><span data-stu-id="12a04-250">Scroll Wheel</span></span>

* <span data-ttu-id="12a04-251">Tek satırlık metin girişi</span><span class="sxs-lookup"><span data-stu-id="12a04-251">Single Line Text Input</span></span>

* <span data-ttu-id="12a04-252">Kaydırıcı</span><span class="sxs-lookup"><span data-stu-id="12a04-252">Slider</span></span>

* <span data-ttu-id="12a04-253">Dize kaydırma tekerleği</span><span class="sxs-lookup"><span data-stu-id="12a04-253">String Scroll Wheel</span></span>

* <span data-ttu-id="12a04-254">Metin düğmesi</span><span class="sxs-lookup"><span data-stu-id="12a04-254">Text Button</span></span>

* <span data-ttu-id="12a04-255">Ağacı Görünümü</span><span class="sxs-lookup"><span data-stu-id="12a04-255">Tree View</span></span>

* <span data-ttu-id="12a04-256">Dikey Liste</span><span class="sxs-lookup"><span data-stu-id="12a04-256">Vertical List</span></span>

* <span data-ttu-id="12a04-257">Dikey kaydırma çubuğu</span><span class="sxs-lookup"><span data-stu-id="12a04-257">Vertical Scrollbar</span></span>

<span data-ttu-id="12a04-258">Uygulamanın kendi müşteri pencere öğelerini de oluşturması kolay bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="12a04-258">It’s easy for the application to create its own customer widgets as well.</span></span>

### <a name="complete-low-level-drawing-api"></a><span data-ttu-id="12a04-259">Düşük düzey çizim API 'sini doldurun</span><span class="sxs-lookup"><span data-stu-id="12a04-259">Complete low-level drawing API</span></span>

<span data-ttu-id="12a04-260">Azure RTOS Gux sağlam bir tuval çizimi API 'SI sağlar ve uygulamanın karmaşık grafik şekillerini işlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="12a04-260">Azure RTOS GUIX provides a robust canvas drawing API, allowing the application to render complex graphical shapes.</span></span>

<span data-ttu-id="12a04-261">Tüm işlevler, yüksek renk derinliği hedefleri üzerinde kenar yumuşatmasını destekler ve Solid ve pixelmap örüntüsünün dolgusu dahil olmak üzere tüm şekiller ana hatlarıyla doldurulabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-261">All functions support anti-aliasing on high color depth targets, and all shapes can be filled our outlined, including solid and pixelmap pattern fills.</span></span> <span data-ttu-id="12a04-262">Tüm çizim temelleri 16 BPP ve daha yüksek renk derinliğinde çalışırken fırça Alpha 'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="12a04-262">All drawing primitives support brush alpha when running at 16 bpp and higher color depth.</span></span> <span data-ttu-id="12a04-263">Çizim işlevleri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="12a04-263">Drawing functions include:</span></span>

* <span data-ttu-id="12a04-264">Yay çiz</span><span class="sxs-lookup"><span data-stu-id="12a04-264">Arc Draw</span></span>

* <span data-ttu-id="12a04-265">Daire çiz</span><span class="sxs-lookup"><span data-stu-id="12a04-265">Circle Draw</span></span>

* <span data-ttu-id="12a04-266">Çizgi çizme</span><span class="sxs-lookup"><span data-stu-id="12a04-266">Line Draw</span></span>

* <span data-ttu-id="12a04-267">Pasta çiz</span><span class="sxs-lookup"><span data-stu-id="12a04-267">Pie Draw</span></span>

* <span data-ttu-id="12a04-268">Pixelmap Blend</span><span class="sxs-lookup"><span data-stu-id="12a04-268">Pixelmap Blend</span></span>

* <span data-ttu-id="12a04-269">Pixelmap kutucuğu</span><span class="sxs-lookup"><span data-stu-id="12a04-269">Pixelmap Tile</span></span>

* <span data-ttu-id="12a04-270">Çokgen Çiz</span><span class="sxs-lookup"><span data-stu-id="12a04-270">Polygon Draw</span></span>

* <span data-ttu-id="12a04-271">Metin çizme</span><span class="sxs-lookup"><span data-stu-id="12a04-271">Text Draw</span></span>

* <span data-ttu-id="12a04-272">Chun çiz</span><span class="sxs-lookup"><span data-stu-id="12a04-272">Chord Draw</span></span>

* <span data-ttu-id="12a04-273">Elips çizme</span><span class="sxs-lookup"><span data-stu-id="12a04-273">Ellipse Draw</span></span>

* <span data-ttu-id="12a04-274">Piksel çizimi</span><span class="sxs-lookup"><span data-stu-id="12a04-274">Pixel Draw</span></span>

* <span data-ttu-id="12a04-275">Pixelmap çiz</span><span class="sxs-lookup"><span data-stu-id="12a04-275">Pixelmap Draw</span></span>

* <span data-ttu-id="12a04-276">Pixelmap döndürme</span><span class="sxs-lookup"><span data-stu-id="12a04-276">Pixelmap Rotate</span></span>

* <span data-ttu-id="12a04-277">Dikdörtgen çiz</span><span class="sxs-lookup"><span data-stu-id="12a04-277">Rectangle Draw</span></span>

* <span data-ttu-id="12a04-278">Metin Blend</span><span class="sxs-lookup"><span data-stu-id="12a04-278">Text Blend</span></span>

### <a name="default-free-fonts-and-easy-to-add-more"></a><span data-ttu-id="12a04-279">Varsayılan ücretsiz yazı tipleri ve ekleme daha kolay</span><span class="sxs-lookup"><span data-stu-id="12a04-279">Default free fonts and easy to add more</span></span>

<span data-ttu-id="12a04-280">Azure RTOS Gux, ücretsiz bir TrueType yazı tipi kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-280">Azure RTOS GUIX provides a free set of TrueType fonts.</span></span> <span data-ttu-id="12a04-281">Geliştiriciler, istediğiniz gibi ek TrueType yazı tipleri ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-281">Developers can add additional TrueType fonts as desired.</span></span>

<span data-ttu-id="12a04-282">Azure RTOS Gux yazı tipi biçimi, 8bpp Anti-düzgünleştirme, 4bpp düzgünleştirme ve 1bpp tek renkli yazı tiplerini destekler.</span><span class="sxs-lookup"><span data-stu-id="12a04-282">The Azure RTOS GUIX font format supports 8bpp anti-aliasing, 4bpp anti-aliasing, and 1bpp monochrome fonts.</span></span> <span data-ttu-id="12a04-283">En fazla kaynak sınırlamalı uygulamalar için, Azure RTOS Gux önceden TrueType yazı tiplerini Gux Studio Desktop aracımızı kullanarak sıkıştırılmış bir bit eşlem biçimine göre işler.</span><span class="sxs-lookup"><span data-stu-id="12a04-283">For the most resource-constrained applications, Azure RTOS GUIX pre-renders the TrueType fonts to a compressed bitmap format using our GUIX Studio desktop tool.</span></span>

### <a name="custom-jpg-and-png-decoder-implementation"></a><span data-ttu-id="12a04-284">Özel JPG ve PNG kod çözücü uygulama</span><span class="sxs-lookup"><span data-stu-id="12a04-284">Custom JPG and PNG decoder implementation</span></span>

<span data-ttu-id="12a04-285">Özel JPG ve PNG kod çözücü uygulama JPG ve PNG dosya kod çözücü uygulama.</span><span class="sxs-lookup"><span data-stu-id="12a04-285">Custom JPG and PNG decoder implementation JPG and PNG file decoder implementation.</span></span> <span data-ttu-id="12a04-286">Bu uygulama, Azure RTOS GUıDX uyumlu pixelmap biçim görüntülerinin renk alanı dönüştürmeyi, titreme ve çalışma zamanı oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="12a04-286">This implementation supports color space conversion, dithering, and runtime creation of Azure RTOS GUIX-compatible pixelmap format images.</span></span>

### <a name="extensive-display-and-touchscreen-support"></a><span data-ttu-id="12a04-287">Kapsamlı ekran ve dokunmatik ekran desteği</span><span class="sxs-lookup"><span data-stu-id="12a04-287">Extensive display and touchscreen support</span></span>

<span data-ttu-id="12a04-288">Azure RTOS Gux, 1bpp tek renkli, 8 BPP palet, 8 BPP 3:3:2 biçimi de dahil olmak üzere neredeyse tüm renk biçimleri için genel görüntüleme sürücüleri sağlar</span><span class="sxs-lookup"><span data-stu-id="12a04-288">Azure RTOS GUIX provides generic display drivers for nearly all color formats, including 1bpp monochrome, 8 bpp palette, 8 bpp 3:3:2 format,</span></span>

<span data-ttu-id="12a04-289">16 BPP 565 RGB biçimi, 16 BPP 4:4:4:4 biçimi, 32 BPP x:r: g:b biçimi ve 32 BPP a:r: g:b biçimi.</span><span class="sxs-lookup"><span data-stu-id="12a04-289">16 bpp 565 rgb format, 16 bpp 4:4:4:4 format, 32 bpp x:r:g:b format, and 32 bpp a:r:g:b format.</span></span> <span data-ttu-id="12a04-290">Ayrıca, Azure RTOS Gux, en popüler LCD denetleyiciler ve donanım hızlandırıcılarının (ST Kmesanat, Renesas Synergy, vb.) çoğuyla tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="12a04-290">In addition, Azure RTOS GUIX is integrated with many of the most popular LCD controllers and hardware accelerators (ST ChromeArt, Renesas Synergy, etc.).</span></span>

<span data-ttu-id="12a04-291">Azure RTOS Gux, dokunmatik ekranı (hareket desteği dahil), kalemi ve sanal klavye girişi cihazlarını tam olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="12a04-291">Azure RTOS GUIX fully supports touchscreen (including gesture support), pen, and virtual keyboard input devices.</span></span>

### <a name="azure-rtos-guix-studio-desktop-wysiwyg-tool"></a><span data-ttu-id="12a04-292">Azure RTOS Gux Studio masaüstü WYSıWYG aracı</span><span class="sxs-lookup"><span data-stu-id="12a04-292">Azure RTOS GUIX Studio desktop WYSIWYG tool</span></span>

<span data-ttu-id="12a04-293">Azure RTOS Gux Studio, kullanıcının GUI ekranlarını oluşturmak için kullanılan grafik öğelerini sürükleyip bırakması için tam bir WYSıWYG ekranı tasarım ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-293">Azure RTOS GUIX Studio provides a complete WYSIWYG screen design environment which allows the user to drag-and-drop graphical elements used to build the GUI screens.</span></span> <span data-ttu-id="12a04-294">Azure RTOS Gux Studio otomatik olarak Azure RTOS Gux kitaplığı ile uyumlu C kodu oluşturur ve hedefte derlenmeye ve çalıştırılmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="12a04-294">Azure RTOS GUIX Studio automatically generates C code compatible with the Azure RTOS GUIX library, ready to be compiled and run on the target.</span></span> <span data-ttu-id="12a04-295">Geliştiriciler, tümleşik Azure RTOS Gux Studio yazı tipi oluşturma aracı 'nı kullanarak bir uygulama içinde kullanılmak üzere önceden oluşturulmuş yazı tiplerini oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-295">Developers can produce pre-rendered fonts for use within an application using the integrated Azure RTOS GUIX Studio font generation tool.</span></span> <span data-ttu-id="12a04-296">Yazı tipleri, tek renkli veya kenar yumuşatma uygulanmış biçimlerde oluşturulabilir ve hedefte yer kazanmak için iyileştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="12a04-296">Fonts can be generated in monochrome or anti-aliased formats, and are optimized to save space on the target.</span></span> <span data-ttu-id="12a04-297">Yazı tiplerinde, çok dilli uygulamalar için Unicode karakterler de dahil olmak üzere herhangi bir karakter kümesi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-297">Fonts can include any set of characters, including Unicode characters for multi-lingual applications.</span></span>

<img alt="Diagram of SGS-TUV Saar certification logo" class="alignnone size-full wp-image-1500" height="341" sizes="(max-width: 535px) 100vw, 535px" src="./media/overview/studio_screen_shot.png"/>

<span data-ttu-id="12a04-298">Azure RTOS Gux Studio, hedef sistemde kullanılmak üzere sıkıştırılan Azure RTOS Gux pixelmaps 'e dönüştürme ile PNG veya JPG dosyalarından grafiklerin içeri aktarılacağını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="12a04-298">Azure RTOS GUIX Studio facilitates the import of graphics from PNG or JPG files with conversion to compressed Azure RTOS GUIX Pixelmaps for use on the target system.</span></span> <span data-ttu-id="12a04-299">Azure RTOS Gux pencere öğesi türlerinin birçoğu, özel bir görünüm ve kullanım için Kullanıcı grafiklerini içerecek şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="12a04-299">Many of the Azure RTOS GUIX widget types are designed to incorporate user graphics for a custom look and feel.</span></span> <span data-ttu-id="12a04-300">Ayrıca, Azure RTOS Gux Studio, Azure RTOS Gux pencere öğeleri tarafından kullanılan varsayılan renklerin ve çizim stillerinin özelleştirilmesine olanak tanıyarak, geliştiricilerin Azure RTOS Gux 'in görünüşünü çok kolay bir şekilde ayarlamasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="12a04-300">In addition, Azure RTOS GUIX Studio allows customization of the default colors and drawing styles used by the Azure RTOS GUIX widgets, allowing developers to tune the appearance of Azure RTOS GUIX very easily.</span></span> <span data-ttu-id="12a04-301">Uygulama dizelerinin oluşturulması ve bakımı, Azure RTOS Gux Studio 'nun başka bir yerleşik tesisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="12a04-301">Generation and maintenance of application strings is another built-in facility of Azure RTOS GUIX Studio.</span></span> <span data-ttu-id="12a04-302">Bu, geliştiricilerin geliştirme için bir dil kullanarak bir uygulama tasarlamasını ve ürün yayımlandıktan sonra hızlı ve kolay bir şekilde ek dil desteği eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-302">This enables developers to design an application using one language for developing, and quickly and easily add support for additional languages after the product is released.</span></span> <span data-ttu-id="12a04-303">Azure RTOS Gux Studio ortamındaki bir BILGISAYAR masaüstünde, GUI kavramlarının ve ekran akışlarının test edilmesine ve ekran geçişlerinin ve animasyonların gözlemlerine yönelik bir hızlı ve kolay bir şekilde oluşturulmasına ve bu uygulamanın tamamına yönelik kapsamlı bir Azure RTOS Gux uygulaması çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-303">A complete Azure RTOS GUIX application can be executed on a PC desktop within the Azure RTOS GUIX Studio environment, allowing a quick and easy generation and demonstration of GUI concepts, testing of screen flows, and observation of screen transitions and animations.</span></span> <span data-ttu-id="12a04-304">İşlem tamamlandığında tasarım, hedef Ready C veri yapıları olarak verilebildiğinden, Azure RTOS Gux ve Azure RTOS ThreadX kitaplıklarıyla derlenmeye ve bunlarla bağlantı kurulabilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-304">When completed, a design can be exported as target-ready C data structures, ready to be compiled and linked with the Azure RTOS GUIX and Azure RTOS ThreadX libraries.</span></span>

<span data-ttu-id="12a04-305">Azure RTOS Gux ve Azure RTOS Gux Studio birden çok kaynak teması destekler ve bir uygulamanın çalışma zamanında kolayca yeniden başlatılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="12a04-305">Azure RTOS GUIX and Azure RTOS GUIX Studio support multiple resource themes, allowing an application to be easily reskinned at run-time.</span></span> <span data-ttu-id="12a04-306">Yazı tipleri, renkler ve pixelmaps, tek bir basit API ile çalışma zamanında değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="12a04-306">Fonts, colors, and pixelmaps can be changed at run-time with one simple API.</span></span>

<span data-ttu-id="12a04-307">GUX Studio hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="12a04-307">Learn more about GUIX Studio</span></span>

### <a name="complete-win32-simulation"></a><span data-ttu-id="12a04-308">Win32 simülasyonu</span><span class="sxs-lookup"><span data-stu-id="12a04-308">Complete Win32 simulation</span></span>

<span data-ttu-id="12a04-309">Azure RTOS Gux, hedef panoda çalışan tam olarak aynı çizim kitaplığını kullanarak bir Windows bilgisayarında çalışır.</span><span class="sxs-lookup"><span data-stu-id="12a04-309">Azure RTOS GUIX runs on a Windows PC, using exactly the same drawing library that runs on the target board.</span></span> <span data-ttu-id="12a04-310">Azure RTOS Gux ile, bılgısayarda GUI uygulaması oluşturup çalıştırabilir ve hata ayıklama, hızlı prototipleme, tanıtım ve WYSıWYG hedefi işlemi için Hedefinizdeki aynı uygulama kodunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12a04-310">With Azure RTOS GUIX, you can build and run a GUI application on the PC, and use the same application code on your target for debugging, rapid prototyping, demonstration, and WYSIWYG target operation.</span></span>

### <a name="advanced-technology"></a><span data-ttu-id="12a04-311">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="12a04-311">Advanced technology</span></span>

* <span data-ttu-id="12a04-312">Azure RTOS Gux 'in gelişmiş teknolojisi şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="12a04-312">Azure RTOS GUIX's advanced technology incorporates:</span></span>

* <span data-ttu-id="12a04-313">Alfa karıştırma</span><span class="sxs-lookup"><span data-stu-id="12a04-313">Alpha blending</span></span>

* <span data-ttu-id="12a04-314">Kenar yumuşatma</span><span class="sxs-lookup"><span data-stu-id="12a04-314">Anti-Aliasing</span></span>

* <span data-ttu-id="12a04-315">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="12a04-315">Automatic scaling</span></span>

* <span data-ttu-id="12a04-316">Bit eşlem sıkıştırması</span><span class="sxs-lookup"><span data-stu-id="12a04-316">Bitmap compression</span></span>

* <span data-ttu-id="12a04-317">Tuval karışımı</span><span class="sxs-lookup"><span data-stu-id="12a04-317">Canvas blending</span></span>

* <span data-ttu-id="12a04-318">Özel pencere öğesi desteği</span><span class="sxs-lookup"><span data-stu-id="12a04-318">Custom widget support</span></span>

* <span data-ttu-id="12a04-319">Ertelenmiş çizim desteği</span><span class="sxs-lookup"><span data-stu-id="12a04-319">Deferred drawing support</span></span>

* <span data-ttu-id="12a04-320">Titreme desteği</span><span class="sxs-lookup"><span data-stu-id="12a04-320">Dithering support</span></span>

* <span data-ttu-id="12a04-321">Endian bağımsız programlama</span><span class="sxs-lookup"><span data-stu-id="12a04-321">Endian neutral programming</span></span>

* <span data-ttu-id="12a04-322">Donanım hızlandırıcısı desteği</span><span class="sxs-lookup"><span data-stu-id="12a04-322">Hardware accelerator support</span></span>

* <span data-ttu-id="12a04-323">Çok dilli destek ve UTF-8 kodlaması</span><span class="sxs-lookup"><span data-stu-id="12a04-323">Multilingual support and UTF-8 encoding</span></span>

* <span data-ttu-id="12a04-324">Birden çok görüntü ve tuval desteği</span><span class="sxs-lookup"><span data-stu-id="12a04-324">Multiple display and canvas support</span></span>

* <span data-ttu-id="12a04-325">En iyi duruma getirilmiş kırpma, çizim ve olay işleme</span><span class="sxs-lookup"><span data-stu-id="12a04-325">Optimized clipping, drawing, and event handling</span></span>

* <span data-ttu-id="12a04-326">Çalışma zamanı JPEG ve PNG kod çözücü</span><span class="sxs-lookup"><span data-stu-id="12a04-326">Runtime JPEG and PNG decoder</span></span>

* <span data-ttu-id="12a04-327">Kaplama ve Temalar</span><span class="sxs-lookup"><span data-stu-id="12a04-327">Skinning and Themes</span></span>

* <span data-ttu-id="12a04-328">Tek renkli 32 bitlik gerçek renk ile alfa grafik biçimlerini destekler</span><span class="sxs-lookup"><span data-stu-id="12a04-328">Supports monochrome through 32-bit true-color with alpha graphics formats</span></span>

* <span data-ttu-id="12a04-329">Geçişler, sprites ve animasyon desteği</span><span class="sxs-lookup"><span data-stu-id="12a04-329">Transitions, Sprites, and Animation support</span></span>

* <span data-ttu-id="12a04-330">Win32 simülasyonu</span><span class="sxs-lookup"><span data-stu-id="12a04-330">Win32 simulation</span></span>

* <span data-ttu-id="12a04-331">Viewports ve Z düzeninde bakım dahil olmak üzere pencere yönetimi</span><span class="sxs-lookup"><span data-stu-id="12a04-331">Window management including Viewports and Z-order maintenance</span></span>

### <a name="fastest-time-to-market"></a><span data-ttu-id="12a04-332">En hızlı pazar süresi</span><span class="sxs-lookup"><span data-stu-id="12a04-332">Fastest time-to-market</span></span>

<span data-ttu-id="12a04-333">Azure RTOS Gux 'i yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="12a04-333">Azure RTOS GUIX is easy to install, learn, use, debug, verify, certify and maintain.</span></span> <span data-ttu-id="12a04-334">Azure RTOS Gux Studio, yerleşik GUI tasarımının ve uygulamasının daha kolay yapılmasına de yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="12a04-334">Azure RTOS GUIX Studio also helps making embedded GUI design and implementation easier.</span></span> <span data-ttu-id="12a04-335">Sonuç olarak, Azure RTOS Gux, katıştırılmış IoT cihazları için en popüler GUI çözümlerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="12a04-335">As a result, Azure RTOS GUIX is one of the most popular GUI solutions for embedded IoT devices.</span></span> <span data-ttu-id="12a04-336">Tutarlı Pazar süresi avantajımız, şu şekilde oluşturulmuştur:</span><span class="sxs-lookup"><span data-stu-id="12a04-336">Our consistent time-to-market advantage is built on:</span></span>

* <span data-ttu-id="12a04-337">Kalite belgeleri: lütfen [Azure RTOS Gux Kullanıcı Kılavuzumuzu](about-guix.md) gözden geçirin ve kendiniz görün!</span><span class="sxs-lookup"><span data-stu-id="12a04-337">Quality Documentation – please review our [Azure RTOS GUIX User Guide](about-guix.md) and see for yourself!</span></span>

* <span data-ttu-id="12a04-338">Tüm kaynak kodu kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="12a04-338">Complete Source Code Availability</span></span>

* <span data-ttu-id="12a04-339">Kullanımı kolay API</span><span class="sxs-lookup"><span data-stu-id="12a04-339">Easy-to-use API</span></span>

* <span data-ttu-id="12a04-340">Kapsamlı ve gelişmiş özellik kümesi</span><span class="sxs-lookup"><span data-stu-id="12a04-340">Comprehensive and Advanced Feature Set</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="12a04-341">Tek bir basit lisans</span><span class="sxs-lookup"><span data-stu-id="12a04-341">One Simple License</span></span>

<span data-ttu-id="12a04-342">Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="12a04-342">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="12a04-343">Tam, en yüksek kaliteli kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="12a04-343">Full, highest-quality source code</span></span>

<span data-ttu-id="12a04-344">Yıl boyunca, Azure RTOS NetX kaynak kodu, çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı.</span><span class="sxs-lookup"><span data-stu-id="12a04-344">Throughout the years, Azure RTOS NetX source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="12a04-345">Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.</span><span class="sxs-lookup"><span data-stu-id="12a04-345">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="12a04-346">Popüler mimarilerin çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="12a04-346">Supports most popular architectures</span></span>

<span data-ttu-id="12a04-347">Azure RTOS Gux, en popüler 32/64 bit mikro işlemciler, kullanıma hazır, tam olarak sınanmış ve aşağıdakiler dahil olmak üzere tam olarak desteklenmiş şekilde çalışır:</span><span class="sxs-lookup"><span data-stu-id="12a04-347">Azure RTOS GUIX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

<span data-ttu-id="12a04-348">Gelişmiş mimariler:</span><span class="sxs-lookup"><span data-stu-id="12a04-348">Advanced Architectures:</span></span>

<span data-ttu-id="12a04-349">**Analog cihazlar**: parça, BlackICE, CM4xx</span><span class="sxs-lookup"><span data-stu-id="12a04-349">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="12a04-350">**Andes Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="12a04-350">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="12a04-351">**Ambiqmicro**: Apollo MCUs</span><span class="sxs-lookup"><span data-stu-id="12a04-351">**Ambiqmicro**: Apollo MCUs</span></span>

<span data-ttu-id="12a04-352">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı</span><span class="sxs-lookup"><span data-stu-id="12a04-352">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="12a04-353">**Temposunda**: xtensa, elmas</span><span class="sxs-lookup"><span data-stu-id="12a04-353">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="12a04-354">**Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi</span><span class="sxs-lookup"><span data-stu-id="12a04-354">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="12a04-355">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="12a04-355">**Cypress**: RISC-V</span></span>

<span data-ttu-id="12a04-356">**Ensilica**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="12a04-356">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="12a04-357">**Infineon**: XMC1000, XMC4000, kanore</span><span class="sxs-lookup"><span data-stu-id="12a04-357">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="12a04-358">**Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, varış a 10</span><span class="sxs-lookup"><span data-stu-id="12a04-358">**Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="12a04-359">**Mikro yonga**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="12a04-359">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="12a04-360">**Mikro yarı**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="12a04-360">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="12a04-361">**NXP**: LPC, ARM7, ARM9, PowerPC, 68K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="12a04-361">**NXP**: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="12a04-362">**Renesas**: SH, HS, v850, RX, Rz, Synergy</span><span class="sxs-lookup"><span data-stu-id="12a04-362">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="12a04-363">**Silicon Labs**: EFM32</span><span class="sxs-lookup"><span data-stu-id="12a04-363">**Silicon Labs**: EFM32</span></span>

<span data-ttu-id="12a04-364">**Synopsys**: Arc 600, 700, Arc Em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="12a04-364">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="12a04-365">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="12a04-365">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="12a04-366">**TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="12a04-366">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="12a04-367">**Dalga bilgi işlem**: MIPS32 4k, 24K, 34K, 1004K, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M sınıfı</span><span class="sxs-lookup"><span data-stu-id="12a04-367">**Wave Computing**: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="12a04-368">**Xilinx**: mikro Blaze, PowerPC 405, zynq, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="12a04-368">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>
