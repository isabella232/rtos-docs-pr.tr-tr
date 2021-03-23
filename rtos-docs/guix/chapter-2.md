---
title: Bölüm 2-Gux yükleme ve kullanımı
description: Bu bölümde, HighPerformance Kullanıcı arabirimi ürününün Gux ' i yükleme, kurulum ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6527227062fc667b3f527a798d6621914c374c5c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826392"
---
# <a name="chapter-2---installation-and-use-of-guix"></a><span data-ttu-id="b1612-103">Bölüm 2-Gux yükleme ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="b1612-103">Chapter 2 - Installation and Use of GUIX</span></span>

<span data-ttu-id="b1612-104">Bu bölümde, HighPerformance Kullanıcı arabirimi ürününün Gux ' i yükleme, kurulum ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1612-104">This chapter contains a description of various issues related to installation, setup, and use of the highperformance user interface product GUIX.</span></span>  

## <a name="host-considerations"></a><span data-ttu-id="b1612-105">Ana bilgisayar konuları</span><span class="sxs-lookup"><span data-stu-id="b1612-105">Host Considerations</span></span>

<span data-ttu-id="b1612-106">Katıştırılmış Geliştirme genellikle Windows veya Linux (UNIX) ana bilgisayar bilgisayarlarında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b1612-106">Embedded development is usually performed on Windows or Linux (Unix) host computers.</span></span> <span data-ttu-id="b1612-107">Uygulama derlendikten, bağlanır ve çalıştırılabilir dosya konakta üretildikten sonra, yürütme için hedef donanıma indirilir.</span><span class="sxs-lookup"><span data-stu-id="b1612-107">After the application is compiled, linked, and the executable is generated on the host, it is downloaded to the target hardware for execution.</span></span>

<span data-ttu-id="b1612-108">Genellikle hedef indirme işlemi geliştirme aracının hata ayıklayıcı içinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="b1612-108">Usually the target download is done from within the development tool's debugger.</span></span> <span data-ttu-id="b1612-109">İndirmeden sonra, hata ayıklayıcı, hedef yürütme denetimi (go, dur, kesme noktası vb.) ve bellek ve işlemci kayıtlarına erişimi sağlamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="b1612-109">After download, the debugger is responsible for providing target execution control (go, halt, breakpoint, etc.) as well as access to memory and processor registers.</span></span>

<span data-ttu-id="b1612-110">Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b1612-110">Most development tool debuggers communicate with the target hardware via on-chip debug (OCD) connections such as JTAG (IEEE 1149.1) and Background Debug Mode (BDM).</span></span> <span data-ttu-id="b1612-111">Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b1612-111">Debuggers also communicate with target hardware through In-Circuit Emulation (ICE) connections.</span></span> <span data-ttu-id="b1612-112">OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1612-112">Both OCD and ICE connections provide robust solutions with minimal intrusion on the target resident software.</span></span>

<span data-ttu-id="b1612-113">Konakta kullanılan kaynaklar için, GUXI kaynak kodu ASCII biçiminde dağıtılır ve konak bilgisayarın sabit diskinde yaklaşık 30 MB alan gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b1612-113">As for resources used on the host, the source code for GUXI is delivered in ASCII format and requires approximately 30 Mbytes of space on the host computer’s hard disk.</span></span>

## <a name="target-considerations"></a><span data-ttu-id="b1612-114">Hedef konuları</span><span class="sxs-lookup"><span data-stu-id="b1612-114">Target Considerations</span></span>

<span data-ttu-id="b1612-115">GUX, hedefte 5 Kbayt ve 80 Kbayt Read-Only bellek (ROM) arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b1612-115">GUIX requires between 5 KBytes and 80 Kbytes of Read-Only Memory (ROM) on the target.</span></span> <span data-ttu-id="b1612-116">GUX iş parçacığı yığını ve diğer genel veri yapıları için hedefin rastgele erişim belleği (RAM) için bir adet 5-10Kbayt gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b1612-116">Another 5 to 10KBytes of the target’s Random Access Memory (RAM) are required for the GUIX thread stack and other global data structures.</span></span>

<span data-ttu-id="b1612-117">Ayrıca, GUıDX, bir ThreadX süreölçeri ve bir ThreadX mutex nesnesi kullanılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b1612-117">In addition, GUIX requires the use of a ThreadX timer and a ThreadX mutex object.</span></span> <span data-ttu-id="b1612-118">Bu tesisler, Gux içinde düzenli işleme ihtiyaçları ve iş parçacığı koruması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1612-118">These facilities are used for periodic processing needs and thread protection inside GUIX.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="b1612-119">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="b1612-119">Product Distribution</span></span>

<span data-ttu-id="b1612-120">Azure RTOS Gux, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/guix/> .</span><span class="sxs-lookup"><span data-stu-id="b1612-120">Azure RTOS GUIX can be obtained from our public source code repository at <https://github.com/azure-rtos/guix/>.</span></span>

<span data-ttu-id="b1612-121">Aşağıda, çoğu ürün dağıtımlarıyla ortak olan önemli dosyaların bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b1612-121">The following is a list of the important files common to most product distributions:</span></span>

| <span data-ttu-id="b1612-122">Kısaltın&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="b1612-122">Filename&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span>| <span data-ttu-id="b1612-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b1612-123">Description</span></span>   |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <span data-ttu-id="b1612-124">gx_api. h</span><span class="sxs-lookup"><span data-stu-id="b1612-124">gx_api.h</span></span>        | <span data-ttu-id="b1612-125">Bu C üstbilgi dosyası tüm sistem eş, veri yapılarını ve hizmet prototiplerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b1612-125">This C header file contains all system equates, data structures, and service prototypes.</span></span> |
| <span data-ttu-id="b1612-126">gx_port. h</span><span class="sxs-lookup"><span data-stu-id="b1612-126">gx_port.h</span></span>       | <span data-ttu-id="b1612-127">Bu C üstbilgi dosyası, hedefe özgü ve geliştirme aracına özgü veri tanımlarını ve yapılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="b1612-127">This C header file contains all target-specific and development tool-specific data definitions and structures.</span></span>                                                                                                                                         |
| <span data-ttu-id="b1612-128">GX. a (veya GX. lib)</span><span class="sxs-lookup"><span data-stu-id="b1612-128">gx.a (or gx.lib)</span></span> | <span data-ttu-id="b1612-129">Bu, GUıDX C kitaplığının ikili sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="b1612-129">This is the binary version of the GUIX C library.</span></span> <span data-ttu-id="b1612-130">Bu, normal olarak, sunulan Gux kitaplık kaynak dosyalarını derleyip arşivleyerek oluşturulur, ancak bu kitaplık, donanım hedefi ve lisans türüne bağlı olarak önceden oluşturulmuş biçimde sağlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1612-130">This is normally built by compiling and archiving the provided GUIX library source files, however this library may be provided in pre-built form depending on your hardware target and license type.</span></span> |
|

> [!IMPORTANT]
> <span data-ttu-id="b1612-131">*Tüm dosyalar küçük harfli olduğundan, komutların Linux (UNIX) geliştirme platformlarına dönüştürülmesini kolaylaştırır.*</span><span class="sxs-lookup"><span data-stu-id="b1612-131">*All files are in lower-case, making it easy to convert the commands to Linux (Unix) development platforms.*</span></span>

## <a name="guix-installation"></a><span data-ttu-id="b1612-132">GUX yüklemesi</span><span class="sxs-lookup"><span data-stu-id="b1612-132">GUIX Installation</span></span>

<span data-ttu-id="b1612-133">GUIX, GitHub deposu yerel makinenize kopyalanarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b1612-133">GUIX is installed by cloning the GitHub repository to your local machine.</span></span> <span data-ttu-id="b1612-134">Aşağıda, bilgisayarınızda Gux deposunun bir kopyasını oluşturmak için tipik sözdizimi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b1612-134">The following is typical syntax for creating a clone of the GUIX repository on your PC:</span></span>

```c
    git clone https://github.com/azure-rtos/guix
```

<span data-ttu-id="b1612-135">Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1612-135">Alternatively you can download a copy of the repository using the download button on the GitHub main page.</span></span>

<span data-ttu-id="b1612-136">Ayrıca, çevrimiçi deponun ön sayfasında Gux kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b1612-136">You will also find instructions for building the GUIX library on the front page of the online repository.</span></span>

>[!NOTE]  
> <span data-ttu-id="b1612-137">*Uygulama yazılımının, genellikle **GX. a** (veya **GX. lib**) olarak adlandırılan Gux kitaplık dosyasına erişmesi gerekir ve C içerme dosyaları **gx_api. h** ve **gx_port. h**. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaları uygulama geliştirme alanına kopyalayarak gerçekleştirilir.*</span><span class="sxs-lookup"><span data-stu-id="b1612-137">*Application software needs access to the GUIX library file, usually called **gx.a** (or **gx.lib**), and the C include files **gx_api.h** and **gx_port.h**. This is accomplished either by setting the appropriate path for the development tools or by copying these files into the application development area.*</span></span>

## <a name="using-guix"></a><span data-ttu-id="b1612-138">GUX kullanma</span><span class="sxs-lookup"><span data-stu-id="b1612-138">Using GUIX</span></span>

<span data-ttu-id="b1612-139">GUX kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="b1612-139">Using GUIX is easy.</span></span> <span data-ttu-id="b1612-140">Temel olarak, uygulama kodu derleme sırasında ***gx_api. h** _ ve Gux Kitaplığı _*_GX. a_\*_ (veya _ *_GX. lib_*) \* ile bağlantı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b1612-140">Basically, the application code must include ***gx_api.h** _ during compilation and link with the GUIX library _*_gx.a_*_ (or _ *_gx.lib_*)*.</span></span>

<span data-ttu-id="b1612-141">Bir Gux uygulaması oluşturmak için gereken dört kolay adım vardır:</span><span class="sxs-lookup"><span data-stu-id="b1612-141">There are four easy steps required to build a GUIX application:</span></span>

| <span data-ttu-id="b1612-142">Adımlar</span><span class="sxs-lookup"><span data-stu-id="b1612-142">Steps</span></span>   | <span data-ttu-id="b1612-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b1612-143">Description</span></span>    |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <span data-ttu-id="b1612-144">&nbsp;1. Adım:</span><span class="sxs-lookup"><span data-stu-id="b1612-144">Step&nbsp;1:</span></span> | <span data-ttu-id="b1612-145">***Gx_api. h*** dosyasını Gux hizmetlerini veya veri yapılarını kullanan tüm uygulama dosyalarına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b1612-145">Include the ***gx_api.h*** file in all application files that use GUIX services or data structures.</span></span>                                                               |
| <span data-ttu-id="b1612-146">&nbsp;2. Adım:</span><span class="sxs-lookup"><span data-stu-id="b1612-146">Step&nbsp;2:</span></span> | <span data-ttu-id="b1612-147">_ *_Tx_application_define_*\* işlevinden veya bir uygulama iş parçacığından \***gx_system_initialize** _ çağırarak Gux sistemini başlatın.</span><span class="sxs-lookup"><span data-stu-id="b1612-147">Initialize the GUIX system by calling ***gx_system_initialize** _ from the _ *_tx_application_define_** function or an application thread.</span></span>                       |
| <span data-ttu-id="b1612-148">Adım &nbsp; 3:</span><span class="sxs-lookup"><span data-stu-id="b1612-148">Step&nbsp;3:</span></span> | <span data-ttu-id="b1612-149">Bir görüntü örneği oluşturun, ekran için bir tuval oluşturun ve kök pencereyi ve gereken diğer pencereleri veya pencere öğelerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1612-149">Create a display instance, create a canvas for the display, and create the root window and any other windows or widgets necessary.</span></span>                                 |
| <span data-ttu-id="b1612-150">&nbsp;4. Adım:</span><span class="sxs-lookup"><span data-stu-id="b1612-150">Step&nbsp;4:</span></span> | <span data-ttu-id="b1612-151">GUX çalışma zamanı kitaplığı \***GX. a** _ (veya _ *_GX. lib_* \*) ile uygulama kaynağını derleyin ve bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b1612-151">Compile application source and link with the GUIX runtime library ***gx.a** _ (or _*_gx.lib_\*\*).</span></span> <span data-ttu-id="b1612-152">Elde edilen görüntü hedefe indirilebilir ve yürütülür!</span><span class="sxs-lookup"><span data-stu-id="b1612-152">The resulting image can be downloaded to the target and executed!</span></span> |

## <a name="troubleshooting"></a><span data-ttu-id="b1612-153">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b1612-153">Troubleshooting</span></span>

<span data-ttu-id="b1612-154">Her bir Gux bağlantı noktası, belirli bir görüntüleme donanımında yürütülen bir tanıtım uygulamasıyla birlikte dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b1612-154">Each GUIX port is delivered with a demonstration application that executes on specific display hardware.</span></span> <span data-ttu-id="b1612-155">Aynı temel tanıtım, Gux 'in tüm sürümleriyle birlikte dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b1612-155">The same basic demonstration is delivered with all versions of GUIX.</span></span> <span data-ttu-id="b1612-156">Öncelikle tanıtım sisteminin çalıştırılması her zaman iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="b1612-156">It is always a good idea to get the demonstration system running first.</span></span>

<span data-ttu-id="b1612-157">Tanıtım sistemi düzgün çalışmıyorsa, sorunu daraltmak için aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1612-157">If the demonstration system does not run properly, perform the following operations to narrow the problem:</span></span>

1. <span data-ttu-id="b1612-158">Tanıtım 'in ne kadarının çalıştığını belirleme.</span><span class="sxs-lookup"><span data-stu-id="b1612-158">Determine how much of the demonstration is running.</span></span>

2. <span data-ttu-id="b1612-159">Bir derleme zamanı sabiti **GX_THREAD_STACK_SIZE** ve Gux kitaplığını yeniden DERLEYEREK Gux iş parçacığının yığın boyutunu artırın</span><span class="sxs-lookup"><span data-stu-id="b1612-159">Increase the stack size of the GUIX thread by changing the  compile-time constant **GX_THREAD_STACK_SIZE** and recompiling  the GUIX library</span></span>

3. <span data-ttu-id="b1612-160">GUX kitaplığını yapılandırma seçeneği bölümünde listelenen uygun hata ayıklama seçenekleriyle yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="b1612-160">Recompile the GUIX library with the appropriate debug options listed  in the configuration option section.</span></span>

4. <span data-ttu-id="b1612-161">Tüm API çağrılarından dönüş durumunu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b1612-161">Examine the return status from all API calls.</span></span>

5. <span data-ttu-id="b1612-162">***_Gx_system_error_process*** işlevde bir kesme noktası ayarlayarak iç sistem hatası olup olmadığını belirleme.</span><span class="sxs-lookup"><span data-stu-id="b1612-162">Determine if there is an internal system error by setting a breakpoint at the function ***_gx_system_error_process***.</span></span> <span data-ttu-id="b1612-163">Hata kodu ve çağıranın, yanlış gitmeye yönelik ipuçları vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1612-163">There error code and caller should give clues as to what might be going wrong.</span></span>

6. <span data-ttu-id="b1612-164">Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın.</span><span class="sxs-lookup"><span data-stu-id="b1612-164">Temporarily bypass any recent changes to see if the problem disappears or changes.</span></span> <span data-ttu-id="b1612-165">Bu tür bilgiler, Microsoft Destek mühendislerinin yararlı olduğunu kanıtlamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1612-165">Such information should prove useful to Microsoft support engineers.</span></span>

<span data-ttu-id="b1612-166">Sorun giderme adımlarından toplanan bilgileri göndermek için "sizin bizim için gerekenler" başlıklı bölümde açıklanan yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b1612-166">Follow the procedures outlined in the section titled “What We Need From You” to send the information gathered from the troubleshooting steps.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="b1612-167">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="b1612-167">Configuration Options</span></span>

<span data-ttu-id="b1612-168">GUX kitaplığı ve Gux kullanarak uygulama oluşturulurken birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="b1612-168">There are several configuration options when building the GUIX library and the application using GUIX.</span></span> <span data-ttu-id="b1612-169">Bu seçenekler, uygulama gereksinimlerinize en iyi şekilde uyum sağlamak için kitaplık boyutunu ve özellik kümesini ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1612-169">These options are used to tune the library size and feature set to best fit your application requirements.</span></span> <span data-ttu-id="b1612-170">Örneğin, uygulamanızın Gux API hizmetlerinden yalnızca bir iş parçacığı varsa, kritik kod bölümlerinin birden çok iş parçacığı tarafından önceden çıkarılması ile ilişkili ek yükü ortadan kaldırmak için **GX_DISABLE_MULTITHREAD_SUPPORT** yapılandırma bayrağı tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b1612-170">For example, if your application will have only one thread utilizing the GUIX API services, the configuration flag **GX_DISABLE_MULTITHREAD_SUPPORT** should be defined to eliminate the overhead associated with protecting critical code sections from pre-emption by multiple threads.</span></span> <span data-ttu-id="b1612-171">Çeşitli yapılandırma bayrakları uygulama kaynağında, komut satırında veya **_gx_user. h_** içerme dosyası içinde tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b1612-171">The various configuration flags can be defined in the application source, on the command line, or within the **_gx_user.h_** include file.</span></span>

<span data-ttu-id="b1612-172">GUX kitaplık yapılandırma bayrakları her değiştirildiğinde, yapılandırma değişikliklerinin etkili olabilmesi için hem Gux kitaplığını hem de uygulama modüllerinizi yeniden oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1612-172">Whenever the GUIX library configuration flags are modified, it is required to rebuild both the GUIX library and your application modules for the configuration changes to take effect.</span></span>

<span data-ttu-id="b1612-173">Yapılandırma bayraklarının tüm listesi Ek H: GUIX Build-Time yapılandırma bayraklarıyla belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b1612-173">The complete list of configuration flags is documented in Appendix H: GUIX Build-Time Configuration Flags.</span></span>

## <a name="guix-version-id"></a><span data-ttu-id="b1612-174">GUX sürüm KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="b1612-174">GUIX Version ID</span></span>

<span data-ttu-id="b1612-175">Geçerli Gux sürümü çalışma zamanı sırasında hem Kullanıcı hem de uygulama yazılımı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b1612-175">The current version of GUIX is available to both the user and the application software during runtime.</span></span> <span data-ttu-id="b1612-176">Programcı, "**gx_port. h** _ dosyasının INCEAĞıNDAN Gux sürümünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="b1612-176">The programmer can obtain the GUIX version from examination of the \***gx_port.h** _ file.</span></span> <span data-ttu-id="b1612-177">Ayrıca, bu dosya Ayrıca karşılık gelen bağlantı noktası uygulama yazılımının bir sürüm geçmişini içerir _ *_gx_port. h_* \* içindeki genel dizeyi _ *_ _gx_version_id_* _ ' i inceleyerek, guıdx sürümünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="b1612-177">In addition, this file also contains a version history of the corresponding port Application software can obtain the GUIX version by examining the global string _ *_ _gx_version_id_* _ in _\*_gx_port.h_\*\*.</span></span>

<span data-ttu-id="b1612-178">Uygulama yazılımı ayrıca, \***gx_api. h** içinde tanımlanan sabitlerden gelen sürüm bilgilerini de alabilir. \* Bu sabitler, geçerli ürün sürümünü ada ve ürünün birincil ve ikincil sürümüne göre belirler.</span><span class="sxs-lookup"><span data-stu-id="b1612-178">Application software can also obtain release information from the constants shown below defined in \***gx_api.h**.\* These constants identify the current product release by name and the product major and minor version.</span></span>

```C
#define __PRODUCT_GUIX__

#define __GUIX_MAJOR_VERSION__

#define __GUIX_MINOR_VERSION__
```
