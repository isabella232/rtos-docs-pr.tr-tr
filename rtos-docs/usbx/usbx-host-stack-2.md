---
title: Bölüm 2-Azure RTOS USBX konak yığını yüklemesi
description: USBX konak yığınını yüklemeyi öğrenin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 4c33f95b8ac268c557fd947a1303ec3af315a37e
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377093"
---
# <a name="chapter-2---azure-rtos-usbx-host-stack-installation"></a><span data-ttu-id="238a9-103">Bölüm 2-Azure RTOS USBX konak yığını yüklemesi</span><span class="sxs-lookup"><span data-stu-id="238a9-103">Chapter 2 - Azure RTOS USBX Host Stack Installation</span></span>

## <a name="host-considerations"></a><span data-ttu-id="238a9-104">Ana bilgisayar konuları</span><span class="sxs-lookup"><span data-stu-id="238a9-104">Host Considerations</span></span>

### <a name="computer-type"></a><span data-ttu-id="238a9-105">Bilgisayar türü</span><span class="sxs-lookup"><span data-stu-id="238a9-105">Computer Type</span></span>

<span data-ttu-id="238a9-106">Katıştırılmış Geliştirme genellikle Windows bılgısayar veya UNIX ana bilgisayarları üzerinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-106">Embedded development is usually performed on Windows PC or Unix host computers.</span></span> <span data-ttu-id="238a9-107">Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-107">After the application is compiled, linked, and located on the host, it is downloaded to the target hardware for execution.</span></span>

### <a name="download-interfaces"></a><span data-ttu-id="238a9-108">Arabirimleri indir</span><span class="sxs-lookup"><span data-stu-id="238a9-108">Download Interfaces</span></span>

<span data-ttu-id="238a9-109">Genellikle, paralel arabirimler, USB ve Ethernet daha popüler olsa da, hedef indirme bir RS-232 seri arabirimi üzerinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-109">Usually, the target download is done over an RS-232 serial interface, although parallel interfaces, USB, and Ethernet are becoming more popular.</span></span> <span data-ttu-id="238a9-110">Kullanılabilir seçenekler için geliştirme aracı belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="238a9-110">See the development tool documentation for available options.</span></span>

### <a name="debugging-tools"></a><span data-ttu-id="238a9-111">Hata ayıklama araçları</span><span class="sxs-lookup"><span data-stu-id="238a9-111">Debugging Tools</span></span>

<span data-ttu-id="238a9-112">Hata ayıklama, genellikle program görüntüsü indirdiği bağlantıyla aynı bağlantı üzerinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-112">Debugging is done typically over the same link as the program image download.</span></span> <span data-ttu-id="238a9-113">Arka plan hata ayıklama Izleyicisi (BDM) ve In-Circuit öykünücü (ıCE) araçları aracılığıyla hedefte çalışan küçük izleme programlarından farklı hata ayıklayıcılar vardır.</span><span class="sxs-lookup"><span data-stu-id="238a9-113">A variety of debuggers exist, ranging from small monitor programs running on the target through Background Debug Monitor (BDM) and In-Circuit Emulator (ICE) tools.</span></span> <span data-ttu-id="238a9-114">ICE Aracı, gerçek hedef donanımının en sağlam hata ayıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="238a9-114">The ICE tool provides the most robust debugging of actual target hardware.</span></span>

### <a name="required-hard-disk-space"></a><span data-ttu-id="238a9-115">Gerekli sabit disk alanı</span><span class="sxs-lookup"><span data-stu-id="238a9-115">Required Hard Disk Space</span></span>

<span data-ttu-id="238a9-116">USBX için kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 500 Kbayt alan gerektirir.</span><span class="sxs-lookup"><span data-stu-id="238a9-116">The source code for USBX is delivered in ASCII format and requires approximately 500 KBytes of space on the host computer's hard disk.</span></span>

## <a name="target-considerations"></a><span data-ttu-id="238a9-117">Hedef konuları</span><span class="sxs-lookup"><span data-stu-id="238a9-117">Target Considerations</span></span>

<span data-ttu-id="238a9-118">USBX, ana bilgisayar modundaki hedefte yalnızca 24 Kbayt ve 64 Kbayt arasında salt okuma belleği (ROM) arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="238a9-118">USBX requires between 24 KBytes and 64 KBytes of Read Only Memory (ROM) on the target in host mode.</span></span> <span data-ttu-id="238a9-119">Gerekli bellek miktarı, kullanılan denetleyicinin türüne ve USBX ile bağlantılı USB sınıflarına bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="238a9-119">The amount of memory required is dependent on the type of controller used and the USB classes linked to USBX.</span></span> <span data-ttu-id="238a9-120">USBX genel veri yapıları ve bellek havuzu için hedefin rastgele erişim belleği (RAM) için bir 32 Kbayt gerekir.</span><span class="sxs-lookup"><span data-stu-id="238a9-120">Another 32 KBytes of the target's Random Access Memory (RAM) are required for USBX global data structures and memory pool.</span></span> <span data-ttu-id="238a9-121">Bu bellek havuzu, USB üzerindeki beklenen cihaz sayısına ve USB denetleyicisinin türüne göre de ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-121">This memory pool can also be adjusted depending on the expected number of devices on the USB and the type of USB controller.</span></span> <span data-ttu-id="238a9-122">USBX cihaz tarafı, cihaz denetleyicisinin türüne göre kabaca 10-12 K ROM gerektirir.</span><span class="sxs-lookup"><span data-stu-id="238a9-122">The USBX device side requires roughly 10-12 K of ROM depending on the type of device controller.</span></span> <span data-ttu-id="238a9-123">RAM bellek kullanımı, cihaz tarafından Öykünülen sınıfın türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="238a9-123">The RAM memory usage depends on the type of class emulated by the device.</span></span>

<span data-ttu-id="238a9-124">USBX Ayrıca, Işparçacığıx semaforları, zaman uyumu sağlayıcılar ve birden çok iş parçacığı koruması için iş parçacıklarını ve USB veri yolu topolojisini izlemek için g/ç askıya alma ve düzenli işlemeyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="238a9-124">USBX also relies on ThreadX semaphores, mutexes, and threads for multiple thread protection, and I/O suspension and periodic processing for monitoring the USB bus topology.</span></span>

### <a name="product-distribution"></a><span data-ttu-id="238a9-125">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="238a9-125">Product Distribution</span></span>

<span data-ttu-id="238a9-126">Azure RTOS USBX, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/usbx/> .</span><span class="sxs-lookup"><span data-stu-id="238a9-126">Azure RTOS USBX can be obtained from our public source code repository at <https://github.com/azure-rtos/usbx/>.</span></span>

<span data-ttu-id="238a9-127">Depodaki birçok önemli dosyanın listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="238a9-127">The following is a list of several important files in the repository:</span></span>

- <span data-ttu-id="238a9-128">***ux_api. h***: Bu C üstbilgi dosyası tüm sistem eş, veri yapılarını ve hizmet prototiplerini içerir.</span><span class="sxs-lookup"><span data-stu-id="238a9-128">***ux_api.h***: This C header file contains all system equates, data structures, and service prototypes.</span></span>
- <span data-ttu-id="238a9-129">***ux_port. h***: Bu C üstbilgi dosyası, tüm geliştirme aracına özgü veri tanımlarını ve yapılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="238a9-129">***ux_port.h***: This C header file contains all development-tool-specific data definitions and structures.</span></span>
- <span data-ttu-id="238a9-130">***UX. lib***: Bu, USBX C kitaplığının ikili sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="238a9-130">***ux.lib***: This is the binary version of the USBX C library.</span></span> <span data-ttu-id="238a9-131">Standart paketiyle dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-131">It is distributed with the standard package.</span></span>
- <span data-ttu-id="238a9-132">***demo_usbx. c***: basıt bır USBX tanıtımı içeren c dosyası</span><span class="sxs-lookup"><span data-stu-id="238a9-132">***demo_usbx.c***: The C file containing a simple USBX demo</span></span>

<span data-ttu-id="238a9-133">Tüm dosya adları küçük harfli.</span><span class="sxs-lookup"><span data-stu-id="238a9-133">All filenames are in lower-case.</span></span> <span data-ttu-id="238a9-134">Bu adlandırma kuralı, komutları UNIX geliştirme platformlarına dönüştürmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="238a9-134">This naming convention makes it easier to convert the commands to Unix development platforms.</span></span>

## <a name="usbx-installation"></a><span data-ttu-id="238a9-135">USBX yüklemesi</span><span class="sxs-lookup"><span data-stu-id="238a9-135">USBX Installation</span></span>

<span data-ttu-id="238a9-136">USBX, GitHub deposu yerel makinenize kopyalanarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="238a9-136">USBX is installed by cloning the GitHub repository to your local machine.</span></span> <span data-ttu-id="238a9-137">Aşağıda, bilgisayarınızda USBX deposunun bir kopyasını oluşturmak için tipik sözdizimi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="238a9-137">The following is typical syntax for creating a clone of the USBX repository on your PC:</span></span>

```powershell
    git clone https://github.com/azure-rtos/usbx
```

<span data-ttu-id="238a9-138">Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="238a9-138">Alternatively you can download a copy of the repository using the download button on the GitHub main page.</span></span>

<span data-ttu-id="238a9-139">Ayrıca, çevrimiçi deponun ön sayfasında USBX kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="238a9-139">You will also find instructions for building the USBX library on the front page of the online repository.</span></span>

<span data-ttu-id="238a9-140">Aşağıdaki genel yönergeler, neredeyse tüm yüklemeler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="238a9-140">The following general instructions apply to virtually any installation:</span></span>

1. <span data-ttu-id="238a9-141">Konak sabit sürücüsüne daha önce ThreadX 'i yüklediğiniz dizini kullanın.</span><span class="sxs-lookup"><span data-stu-id="238a9-141">Use the same directory in which you previously installed ThreadX on the host hard drive.</span></span> <span data-ttu-id="238a9-142">Tüm USBX adları benzersizdir ve önceki USBX yüklemesine engel olmaz.</span><span class="sxs-lookup"><span data-stu-id="238a9-142">All USBX names are unique and will not interfere with the previous USBX installation.</span></span>
2. <span data-ttu-id="238a9-143">_ *_Tx_application_define_* başlangıcına veya yanına \***ux_system_initialize** _ çağrısı ekleyin. \* Bu, USBX kaynaklarının başlatıldığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="238a9-143">Add a call to ***ux_system_initialize** _ at or near the beginning of _ *_tx_application_define_.** This is where the USBX resources are initialized.</span></span>
3. <span data-ttu-id="238a9-144">\*\*\*Ux_host_stack_initialize \*\*\* için bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="238a9-144">Add a call to \***ux_host_stack_initialize\*.**</span></span>
4. <span data-ttu-id="238a9-145">Gerekli USBX 'i başlatmak için bir veya daha fazla çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="238a9-145">Add one or more calls to initialize the required USBX.</span></span>
5. <span data-ttu-id="238a9-146">Sistemde bulunan konak denetleyicilerini başlatmak için bir veya daha fazla çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="238a9-146">Add one or more calls to initialize the host controllers available in the system.</span></span>
6. <span data-ttu-id="238a9-147">Alt düzey donanım başlatma ve kesme vektör yönlendirmesi eklemek için tx_low_level_initialize. c dosyasını değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-147">It may be required to modify the tx_low_level_initialize.c file to add low-level hardware initialization and interrupt vector routing.</span></span> <span data-ttu-id="238a9-148">Bu donanım platformuna özeldir ve burada ele alınmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="238a9-148">This is specific to the hardware platform and will not be discussed here.</span></span>
7. <span data-ttu-id="238a9-149">Uygulama kaynak kodunu derleme ve USBX ve ThreadX çalışma zamanı kitaplıkları (FileX ve/veya NETX), UX. a (veya UX. lib) ve TX. a (ya da TX. lib) ile bağlantı için gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-149">Compile application source code and link with the USBX and ThreadX run time libraries (FileX and/or Netx may also be required if the USB storage class and/or USB network classes are to be compiled in), ux.a (or ux.lib) and tx.a (or tx.lib).</span></span> <span data-ttu-id="238a9-150">Sonuç hedefe indirilebilir ve yürütülür.</span><span class="sxs-lookup"><span data-stu-id="238a9-150">The resulting can be downloaded to the target and executed.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="238a9-151">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="238a9-151">Configuration Options</span></span>

<span data-ttu-id="238a9-152">USBX kitaplığını oluşturmak için birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="238a9-152">There are several configuration options for building the USBX library.</span></span> <span data-ttu-id="238a9-153">Tüm Seçenekler ***ux_user. h*** içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="238a9-153">All options are located in the ***ux_user.h***.</span></span>

<span data-ttu-id="238a9-154">Aşağıdaki listede her yapılandırma seçeneğinin ayrıntıları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="238a9-154">The list below details each configuration option.</span></span>


- <span data-ttu-id="238a9-155">**UX_PERIODIC_RATE**: Bu değer, belirli bir donanım platformu için saniye başına kaç saat sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-155">**UX_PERIODIC_RATE**: This value represents how many ticks per seconds for a specific hardware platform.</span></span> <span data-ttu-id="238a9-156">Varsayılan değer, her milisaniyeye göre bir değer belirten 1000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="238a9-156">The default is 1000 indicating one tick per millisecond.</span></span>
- <span data-ttu-id="238a9-157">**UX_MAX_CLASS_DRIVER**: Bu değer, USBX tarafından yüklenebilen en fazla sınıf sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="238a9-157">**UX_MAX_CLASS_DRIVER**: This value is the maximum number of classes that can be loaded by USBX.</span></span> <span data-ttu-id="238a9-158">Bu değer, bir sınıfın örnek sayısını değil, sınıf kapsayıcısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-158">This value represents the class container and not the number of instances of a class.</span></span> <span data-ttu-id="238a9-159">Örneğin, belirli bir USBX uygulamasının hub sınıfı, yazıcı sınıfı ve depolama sınıfı olması gerekiyorsa, bu sınıflara ait cihazların sayısından bağımsız olarak UX_MAX_CLASS_DRIVER değeri 3 olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-159">For instance, if a particular implementation of USBX needs the hub class, the printer class, and the storage class, then the UX_MAX_CLASS_DRIVER value can be set to 3 regardless of the number of devices that belong to these classes.</span></span>
- <span data-ttu-id="238a9-160">**UX_MAX_HCD**: Bu değer, sistemde kullanılabilir olan farklı konak denetleyicilerinin sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-160">**UX_MAX_HCD**: This value represents the number of different host controllers that are available in the system.</span></span> <span data-ttu-id="238a9-161">USB 1,1 desteği için bu değer genellikle 1 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="238a9-161">For USB 1.1 support, this value will mostly be 1.</span></span> <span data-ttu-id="238a9-162">USB 2,0 desteği için bu değer 1 ' den fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-162">For USB 2.0 support this value can be more than 1.</span></span> <span data-ttu-id="238a9-163">Bu değer aynı anda çalışan eşzamanlı konak denetleyicilerinin sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-163">This value represents the number of concurrent host controllers running at the same time.</span></span> <span data-ttu-id="238a9-164">Örneğin, iki adet OHCı çalışan ya da bir EHCı ve bir adet bir EHCı denetleyicisi çalışan iki örnek varsa, UX_MAX_HCD 2 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="238a9-164">If for instance, there are two instances of OHCI running or one EHCI and one OHCI controllers running, the UX_MAX_HCD should be set to 2.</span></span> 
- <span data-ttu-id="238a9-165">**UX_MAX_DEVICES**: Bu değer, USB 'ye iliştirilebilecek maksimum cihaz sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-165">**UX_MAX_DEVICES**: This value represents the maximum number of devices that can be attached to the USB.</span></span> <span data-ttu-id="238a9-166">Normalde, tek bir USB üzerinde teorik en büyük sayı 127 cihazlardır.</span><span class="sxs-lookup"><span data-stu-id="238a9-166">Normally, the theoretical maximum number on a single USB is 127 devices.</span></span> <span data-ttu-id="238a9-167">Bu değer, belleği korumak için küçültülemez.</span><span class="sxs-lookup"><span data-stu-id="238a9-167">This value can be scaled down to conserve memory.</span></span> <span data-ttu-id="238a9-168">Bu değerin sistemdeki USB veri yolu sayısından bağımsız olarak toplam cihaz sayısını temsil ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="238a9-168">It should be noted that this value represents the total number of devices regardless of the number of USB buses in the system.</span></span>
- <span data-ttu-id="238a9-169">**UX_MAX_ED**: Bu değer, denetleyici havuzundaki en fazla EDS sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-169">**UX_MAX_ED**: This value represents the maximum number of EDs in the controller pool.</span></span> <span data-ttu-id="238a9-170">Bu sayı yalnızca bir denetleyiciye atanır.</span><span class="sxs-lookup"><span data-stu-id="238a9-170">This number is assigned to one controller only.</span></span> <span data-ttu-id="238a9-171">Birden çok denetleyici örneği varsa, bu değer her bir denetleyici tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-171">If multiple instances of controllers are present, this value is used by each individual controller.</span></span>
- <span data-ttu-id="238a9-172">**UX_MAX_TD ve UX_MAX_ISO_TD**: Bu değer, denetleyici havuzundaki en fazla normal ve zaman aralıklı tds sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-172">**UX_MAX_TD and UX_MAX_ISO_TD**: This value represents the maximum number of regular and isochronous TDs in the controller pool.</span></span> <span data-ttu-id="238a9-173">Bu sayı yalnızca bir denetleyiciye atanır.</span><span class="sxs-lookup"><span data-stu-id="238a9-173">This number is assigned to one controller only.</span></span> <span data-ttu-id="238a9-174">Birden çok denetleyici örneği varsa, bu değer her bir denetleyici tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-174">If multiple instances of controllers are present, this value is used by each individual controller.</span></span>
- <span data-ttu-id="238a9-175">**UX_THREAD_STACK_SIZE**: Bu değer, USBX iş parçacıklarının bayt cinsinden yığınının boyutudur.</span><span class="sxs-lookup"><span data-stu-id="238a9-175">**UX_THREAD_STACK_SIZE**: This value is the size of the stack in bytes for the USBX threads.</span></span> <span data-ttu-id="238a9-176">Kullanılan işlemciye ve ana bilgisayar denetleyicisine bağlı olarak genellikle 1024 bayt veya 2048 bayt olabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-176">It can be typically 1024 bytes or 2048 bytes depending on the processor used and the host controller.</span></span>
- <span data-ttu-id="238a9-177">**UX_HOST_ENUM_THREAD_STACK_SIZE**: Bu değer, USB ana bilgisayar numaralandırma iş parçacığının yığın boyutudur.</span><span class="sxs-lookup"><span data-stu-id="238a9-177">**UX_HOST_ENUM_THREAD_STACK_SIZE**: This value is the stack size of the USB host enumeration thread.</span></span> <span data-ttu-id="238a9-178">Bu sembol ayarlanmıyorum, USBX konak numaralandırma iş parçacığı yığın boyutu **UX_THREAD_STACK_SIZE** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="238a9-178">If this symbol I not set, the USBX host enumeration thread stack size is set to **UX_THREAD_STACK_SIZE**.</span></span> 
- <span data-ttu-id="238a9-179">**UX_HOST_HCD_THREAD_STACK_SIZE**: Bu değer, USB Host HCD iş parçacığının yığın boyutudur.</span><span class="sxs-lookup"><span data-stu-id="238a9-179">**UX_HOST_HCD_THREAD_STACK_SIZE**: This value is the stack size of the USB host HCD thread.</span></span> <span data-ttu-id="238a9-180">Bu sembol ayarlanmıyorum, USBX Host HCD iş parçacığı yığın boyutu **UX_THREAD_STACK_SIZE** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="238a9-180">If this symbol I not set, the USBX host HCD thread stack size is set to **UX_THREAD_STACK_SIZE**.</span></span>
- <span data-ttu-id="238a9-181">**UX_THREAD_PRIORITY_ENUM**: Bu, veri yolu topolojisini izleyen USBX sabit listesi Iş parçacıklarının threadx öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="238a9-181">**UX_THREAD_PRIORITY_ENUM**: This is the ThreadX priority value for the USBX enumeration threads that monitors the bus topology.</span></span>
- <span data-ttu-id="238a9-182">**UX_THREAD_PRIORITY_CLASS**: Bu, standart USBX iş parçacıkları Için threadx öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="238a9-182">**UX_THREAD_PRIORITY_CLASS**: This is the ThreadX priority value for the standard USBX threads.</span></span>
- <span data-ttu-id="238a9-183">**UX_THREAD_PRIORITY_KEYBOARD**: Bu, USBX HID Klavye sınıfı Için threadx öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="238a9-183">**UX_THREAD_PRIORITY_KEYBOARD**: This is the ThreadX priority value for the USBX HID keyboard class.</span></span>
- <span data-ttu-id="238a9-184">**UX_THREAD_PRIORITY_HCD**: Bu, konak denetleyicisi iş parçacığı Için threadx öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="238a9-184">**UX_THREAD_PRIORITY_HCD**: This is the ThreadX priority value for the host controller thread.</span></span>
- <span data-ttu-id="238a9-185">**UX_NO_TIME_SLICE**: Bu değer aslında iş parçacıkları için kullanılacak zaman dilimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="238a9-185">**UX_NO_TIME_SLICE**: This value actually defines the time slice that will be used for threads.</span></span> <span data-ttu-id="238a9-186">Örneğin, 0 olarak tanımlanmışsa, ThreadX hedef bağlantı noktası zaman dilimlerini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="238a9-186">For example, if defined to 0, the ThreadX target port does not use time slices.</span></span>
- <span data-ttu-id="238a9-187">**UX_MAX_HOST_LUN**: Bu değer, konak depolama sınıfı sürücüsünde temsil edilen en fazla SCSI mantıksal birim sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-187">**UX_MAX_HOST_LUN**: This value represents the maximum number of SCSI logical units represented in the host storage class driver.</span></span>
- <span data-ttu-id="238a9-188">**UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT**: tanımlanmışsa, bu değer CB veya CBI protokolünü (disket gibi) kullanan depolama cihazlarını işleyecek kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="238a9-188">**UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT**: If defined, this value includes code to handle storage devices that use the CB or CBI protocol (such as floppy disks).</span></span> <span data-ttu-id="238a9-189">Varsayılan olarak kapalıdır çünkü bu protokoller artık neredeyse tüm modern depolama cihazlarının kullandığı toplu taşıma (BOT Protokolü) tarafından yerine geçti.</span><span class="sxs-lookup"><span data-stu-id="238a9-189">It is off by default because these protocols are obsolete, being superseded by the Bulk Only Transport (BOT protocol, which virtually all modern storage devices use.</span></span>
- <span data-ttu-id="238a9-190">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE**: tanımlanmışsa, bu değer ux_host_class_hid_keyboard_key_get yalnızca, tuş basışları ve önemli yayınlar için anahtar değişikliklerini rapor etmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="238a9-190">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE**: If defined, this value causes ux_host_class_hid_keyboard_key_get to only report key changes that is, key presses and key releases.</span></span> <span data-ttu-id="238a9-191">Varsayılan olarak, yalnızca bir anahtar aşağı olduğunda bildirir.</span><span class="sxs-lookup"><span data-stu-id="238a9-191">By default, it only reports when a key is down.</span></span>
- <span data-ttu-id="238a9-192">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY**: yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** tanımlanmışsa kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-192">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY**: Only used if **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** is defined.</span></span> <span data-ttu-id="238a9-193">Tanımlandıysa, ux_host_class_hid_keyboard_key_get yalnızca tuşu basılı/aşağı değişiklikleri rapor etmesine neden olur; anahtar serbest bırakıldı/yukarı değişiklikler bildirilmedi.</span><span class="sxs-lookup"><span data-stu-id="238a9-193">If defined, causes ux_host_class_hid_keyboard_key_get to only report key pressed/down changes; key released/up changes are not reported.</span></span>
- <span data-ttu-id="238a9-194">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS**: yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** tanımlanmışsa kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-194">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS**: Only used if **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** is defined.</span></span> <span data-ttu-id="238a9-195">Tanımlandıysa, ux_host_class_hid_keyboard_key_get kilit anahtarını (CapsLock/NumLock/ScrollLock) değişikliklerini rapor etmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="238a9-195">If defined, causes ux_host_class_hid_keyboard_key_get to report lock key (CapsLock/NumLock/ScrollLock) changes.</span></span>
- <span data-ttu-id="238a9-196">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS**: yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** tanımlanmışsa kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238a9-196">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS**: Only used if **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** is defined.</span></span> <span data-ttu-id="238a9-197">Tanımlanmışsa, ux_host_class_hid_keyboard_key_get değiştirici anahtarı (Ctrl/Alt/Shift/GUI) değişikliklerini rapor etmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="238a9-197">If defined, causes ux_host_class_hid_keyboard_key_get to report modifier key (Ctrl/Alt/Shift/GUI) changes.</span></span>
- <span data-ttu-id="238a9-198">**UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**: tanımlanmışsa, bu değer CDC-ECD ana bilgisayar sınıfındaki paketlerin sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238a9-198">**UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**: If defined, this value represents the number of packets in the CDC-ECM host class.</span></span> <span data-ttu-id="238a9-199">Varsayılan değer 16 ' dır.</span><span class="sxs-lookup"><span data-stu-id="238a9-199">The default is 16.</span></span>

## <a name="source-code-tree"></a><span data-ttu-id="238a9-200">Kaynak kod ağacı</span><span class="sxs-lookup"><span data-stu-id="238a9-200">Source Code Tree</span></span>

<span data-ttu-id="238a9-201">USBX dosyaları birkaç dizinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="238a9-201">The USBX files are provided in several directories.</span></span>

![Kaynak kod ağacı](media/usbx-host-stack/source-code-tree.png)

<span data-ttu-id="238a9-203">Dosyaları adlarıyla tanınabilir hale getirmek için aşağıdaki kural benimsenmiştir:</span><span class="sxs-lookup"><span data-stu-id="238a9-203">In order to make the files recognizable by their names, the following convention has been adopted:</span></span>

| <span data-ttu-id="238a9-204">Dosya sonek adı</span><span class="sxs-lookup"><span data-stu-id="238a9-204">File Suffix Name</span></span> | <span data-ttu-id="238a9-205">Dosya açıklaması</span><span class="sxs-lookup"><span data-stu-id="238a9-205">File description</span></span>                          |
| ---------------- | ----------------------------------------- |
| <span data-ttu-id="238a9-206">ux_host_stack</span><span class="sxs-lookup"><span data-stu-id="238a9-206">ux_host_stack</span></span>    | <span data-ttu-id="238a9-207">USBX konak yığını çekirdek dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-207">usbx host stack core files</span></span>                |
| <span data-ttu-id="238a9-208">ux_host_class</span><span class="sxs-lookup"><span data-stu-id="238a9-208">ux_host_class</span></span>    | <span data-ttu-id="238a9-209">USBX konak yığını sınıfları dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-209">usbx host stack classes files</span></span>             |
| <span data-ttu-id="238a9-210">ux_hcd</span><span class="sxs-lookup"><span data-stu-id="238a9-210">ux_hcd</span></span>           | <span data-ttu-id="238a9-211">USBX konak yığını denetleyici sürücü dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-211">usbx host stack controller driver files</span></span>   |
| <span data-ttu-id="238a9-212">ux_device_stack</span><span class="sxs-lookup"><span data-stu-id="238a9-212">ux_device_stack</span></span>  | <span data-ttu-id="238a9-213">USBX cihaz yığını çekirdek dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-213">usbx device stack core files</span></span>              |
| <span data-ttu-id="238a9-214">ux_device_class</span><span class="sxs-lookup"><span data-stu-id="238a9-214">ux_device_class</span></span>  | <span data-ttu-id="238a9-215">USBX cihaz yığını sınıfları dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-215">usbx device stack classes files</span></span>           |
| <span data-ttu-id="238a9-216">ux_dcd</span><span class="sxs-lookup"><span data-stu-id="238a9-216">ux_dcd</span></span>           | <span data-ttu-id="238a9-217">USBX cihaz yığını denetleyici sürücü dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-217">usbx device stack controller driver files</span></span> |
| <span data-ttu-id="238a9-218">ux_otg</span><span class="sxs-lookup"><span data-stu-id="238a9-218">ux_otg</span></span>           | <span data-ttu-id="238a9-219">USBX OTG denetleyicisi sürücüyle ilgili dosyalar</span><span class="sxs-lookup"><span data-stu-id="238a9-219">usbx otg controller driver related files</span></span>  |
| <span data-ttu-id="238a9-220">ux_pictbridge</span><span class="sxs-lookup"><span data-stu-id="238a9-220">ux_pictbridge</span></span>    | <span data-ttu-id="238a9-221">USBX PictBridge dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-221">usbx pictbridge files</span></span>                     |
| <span data-ttu-id="238a9-222">ux_utility</span><span class="sxs-lookup"><span data-stu-id="238a9-222">ux_utility</span></span>       | <span data-ttu-id="238a9-223">USBX yardımcı program işlevleri</span><span class="sxs-lookup"><span data-stu-id="238a9-223">usbx utility functions</span></span>                    |
| <span data-ttu-id="238a9-224">demo_usbx</span><span class="sxs-lookup"><span data-stu-id="238a9-224">demo_usbx</span></span>        | <span data-ttu-id="238a9-225">USBX için tanıtım dosyaları</span><span class="sxs-lookup"><span data-stu-id="238a9-225">demonstration files for USBX</span></span>              |

## <a name="initialization-of-usbx-resources"></a><span data-ttu-id="238a9-226">USBX kaynaklarının başlatılması</span><span class="sxs-lookup"><span data-stu-id="238a9-226">Initialization of USBX resources</span></span>

<span data-ttu-id="238a9-227">USBX 'in kendi bellek yöneticisi vardır.</span><span class="sxs-lookup"><span data-stu-id="238a9-227">USBX has its own memory manager.</span></span> <span data-ttu-id="238a9-228">USBX 'in ana bilgisayar veya cihaz tarafı başlatılmadan önce belleğin USBX 'e ayrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="238a9-228">The memory needs to be allocated to USBX before the host or device side of USBX is initialized.</span></span> <span data-ttu-id="238a9-229">USBX bellek Yöneticisi belleğin önbelleğe alınabilme sistemlerine uyum sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-229">USBX memory manager can accommodate systems where memory can be cached.</span></span>

<span data-ttu-id="238a9-230">Aşağıdaki işlev USBX bellek kaynaklarını 128K normal bellekle başlatır ve önbellek güvenli belleği için ayrı havuz içermez:</span><span class="sxs-lookup"><span data-stu-id="238a9-230">The following function initializes USBX memory resources with 128K of regular memory and no separate pool for cache safe memory:</span></span>

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

<span data-ttu-id="238a9-231">Ux_system_initialize prototipi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="238a9-231">The prototype for the ux_system_initialize is as follows.</span></span>

```c
UINT ux_system_initialize( 
    VOID *regular_memory_pool_start,
    ULONG regular_memory_size,
    VOID *cache_safe_memory_pool_start,
    ULONG cache_safe_memory_size);
```

### <a name="input-parameters"></a><span data-ttu-id="238a9-232">Giriş parametreleri:</span><span class="sxs-lookup"><span data-stu-id="238a9-232">Input parameters:</span></span>

- <span data-ttu-id="238a9-233">**regular_memory_pool_start** Normal bellek havuzunun başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="238a9-233">**regular_memory_pool_start** Beginning of the regular memory pool.</span></span>
- <span data-ttu-id="238a9-234">**regular_memory_size** Normal bellek havuzunun boyutu.</span><span class="sxs-lookup"><span data-stu-id="238a9-234">**regular_memory_size** Size of the regular memory pool.</span></span>
- <span data-ttu-id="238a9-235">**cache_safe_memory_pool_start** Önbellek güvenli bellek havuzunun başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="238a9-235">**cache_safe_memory_pool_start** Beginning of the cache safe memory pool.</span></span>
- <span data-ttu-id="238a9-236">**cache_safe_memory_size** Önbellek güvenli bellek havuzunun boyutu.</span><span class="sxs-lookup"><span data-stu-id="238a9-236">**cache_safe_memory_size** Size of the cache safe memory pool.</span></span>    |

<span data-ttu-id="238a9-237">Tüm sistemler önbellek güvenli belleği tanımını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="238a9-237">Not all systems require the definition of cache safe memory.</span></span> <span data-ttu-id="238a9-238">Böyle bir sistemde, bellek işaretçisi için başlatma sırasında geçirilen değerler UX_NULL olarak ayarlanacak ve havuzun boyutu 0 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="238a9-238">In such a system, the values passed during the initialization for the memory pointer will be set to UX_NULL and the size of the pool to 0.</span></span> <span data-ttu-id="238a9-239">USBX daha sonra önbellek güvenli havuzunun yerine normal bellek havuzunu kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="238a9-239">USBX will then use the regular memory pool in lieu of the cache safe pool.</span></span>

<span data-ttu-id="238a9-240">Normal belleğin önbellek güvenli olmadığı ve bir denetleyicinin DMA belleği (örneğin, OHCı, diğer bir deyişle, diğer bir deyişle, diğer bir deyişle, EHCı denetleyicileri) gerçekleştirmesi gereken bir sistemde, önbellek güvenli bölgesinde bir bellek havuzu tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="238a9-240">In a system where the regular memory is not cache safe and a controller requires to perform DMA memory (like OHCI, EHCI controllers amongst others) it is necessary to define a memory pool in a cache safe zone.</span></span>

## <a name="uninitialization-of-usbx-resources"></a><span data-ttu-id="238a9-241">USBX kaynaklarının başlatılması geri alınıyor</span><span class="sxs-lookup"><span data-stu-id="238a9-241">Uninitialization of USBX resources</span></span>

<span data-ttu-id="238a9-242">USBX, kaynakları serbest bırakarak sonlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-242">USBX can be terminated by releasing its resources.</span></span> <span data-ttu-id="238a9-243">USBX 'i sonlandırmadan önce tüm sınıfların ve denetleyici kaynaklarının düzgün şekilde sonlandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="238a9-243">Prior to terminating usbx, all classes and controller resources need to be terminated properly.</span></span> <span data-ttu-id="238a9-244">Aşağıdaki işlev, USBX bellek kaynaklarını başlatır:</span><span class="sxs-lookup"><span data-stu-id="238a9-244">The following function uninitializes USBX memory resources :</span></span>

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

<span data-ttu-id="238a9-245">Ux_system_initialize prototipi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="238a9-245">The prototype for the ux_system_initialize is as follows.</span></span>

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-host-controllers"></a><span data-ttu-id="238a9-246">USB ana bilgisayar denetleyicilerinin tanımı</span><span class="sxs-lookup"><span data-stu-id="238a9-246">Definition of USB Host Controllers</span></span>

<span data-ttu-id="238a9-247">USBX 'in konak modunda çalışması için en az bir USB ana bilgisayar denetleyicisi tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="238a9-247">It is required to define at least one USB host controller for USBX to operate in host mode.</span></span> <span data-ttu-id="238a9-248">Uygulama başlatma dosyası bu tanımı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="238a9-248">The application initialization file should contain this definition.</span></span> <span data-ttu-id="238a9-249">Aşağıdaki satır bir genel ana bilgisayar denetleyicisinin tanımını gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="238a9-249">The following line performs the definition of a generic host controller.</span></span>

```c
ux_host_stack_hcd_register("ux_hcd_controller",
        ux_hcd_controller_initialize, 0xd0000, 0x0a);
```

<span data-ttu-id="238a9-250">Ux_host_stack_hcd_register aşağıdaki prototiple sahiptir.</span><span class="sxs-lookup"><span data-stu-id="238a9-250">The ux_host_stack_hcd_register has the following prototype.</span></span>

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_initialize_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

<span data-ttu-id="238a9-251">Ux_host_stack_hcd_register işlevi aşağıdaki parametrelere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="238a9-251">The ux_host_stack_hcd_register function has the following parameters.</span></span>

- <span data-ttu-id="238a9-252">**hcd_name**: denetleyici adının dizesi</span><span class="sxs-lookup"><span data-stu-id="238a9-252">**hcd_name**: string of the controller name</span></span>
- <span data-ttu-id="238a9-253">**hcd_initialize_function**: denetleyicinin başlatma işlevi</span><span class="sxs-lookup"><span data-stu-id="238a9-253">**hcd_initialize_function**: initialization function of the controller</span></span>
- <span data-ttu-id="238a9-254">**hcd_param1**: genellikle denetleyici tarafından kullanılan GÇ değeri veya bellek</span><span class="sxs-lookup"><span data-stu-id="238a9-254">**hcd_param1**: usually the IO value or Memory used by the controller</span></span>
- <span data-ttu-id="238a9-255">**hcd_param2**: genellikle denetleyici tarafından kullanılan IRQ</span><span class="sxs-lookup"><span data-stu-id="238a9-255">**hcd_param2**: usually the IRQ used by the controller</span></span>

<span data-ttu-id="238a9-256">Önceki örneğimizde:</span><span class="sxs-lookup"><span data-stu-id="238a9-256">In our previous example:</span></span>

- <span data-ttu-id="238a9-257">"ux_hcd_controller" denetleyicinin adıdır</span><span class="sxs-lookup"><span data-stu-id="238a9-257">"ux_hcd_controller" is the name of the controller</span></span>
- <span data-ttu-id="238a9-258">"ux_hcd_controller_initialize", ana bilgisayar denetleyicisi için başlatma yordamdır</span><span class="sxs-lookup"><span data-stu-id="238a9-258">"ux_hcd_controller_initialize" is the initialization routine for the host controller</span></span>
- <span data-ttu-id="238a9-259">0xD0000, ana bilgisayar denetleyicisi yazmaçlarının bellekte görünebileceği adrestir</span><span class="sxs-lookup"><span data-stu-id="238a9-259">0xd0000 is the address at which the host controller registers are visible in memory</span></span>
- <span data-ttu-id="238a9-260">ve 0x0A, ana bilgisayar denetleyicisi tarafından kullanılan IRQ 'dir.</span><span class="sxs-lookup"><span data-stu-id="238a9-260">and 0x0a is the IRQ used by the host controller.</span></span>

<span data-ttu-id="238a9-261">Aşağıda, ana bilgisayar denetleyicisi ve birkaç sınıf ile USBX 'in ana bilgisayar modunda başlatılmasına örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="238a9-261">Following is an example of the initialization of USBX in host mode with one host controller and several classes.</span></span>

```c
UINT status;

/* Initialize USBX. */
ux_system_initialize(memory_ptr, (128*1024),0,0);

/* The code below is required for installing the USBX host stack. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, host stack has been initialized. */

/* Register all the host classes for this USBX implementation. */
status = ux_host_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_storage", ux_host_class_storage_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_printer", ux_host_class_printer_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_audio", ux_host_class_audio_entry);

/* If status equals UX_SUCCESS, host class has been registered. */

/* Register all the USB host controllers available in this system. */ 
status = ux_host_stack_hcd_register("ux_hcd_controller", ux_hcd_controller_initialize, 0x300000, 0x0a);

/* If status equals UX_SUCCESS, USB host controllers have been registered. */
```

## <a name="definition-of-host-classes"></a><span data-ttu-id="238a9-262">Konak sınıflarının tanımı</span><span class="sxs-lookup"><span data-stu-id="238a9-262">Definition of Host Classes</span></span>

<span data-ttu-id="238a9-263">USBX ile bir veya daha fazla konak sınıfı tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="238a9-263">It is required to define one or more host classes with USBX.</span></span> <span data-ttu-id="238a9-264">USB yığını USB cihazını yapılandırdıktan sonra USB bir cihaz için bir USB sınıfı gerekir.</span><span class="sxs-lookup"><span data-stu-id="238a9-264">A USB class is required to drive a USB device after the USB stack has configured the USB device.</span></span> <span data-ttu-id="238a9-265">Cihaza özel bir USB sınıfı.</span><span class="sxs-lookup"><span data-stu-id="238a9-265">A USB class is specific to the device.</span></span> <span data-ttu-id="238a9-266">USB cihaz tanımlayıcılarında bulunan arabirimlerin sayısına bağlı olarak bir USB cihazını yönlendirmek için bir veya daha fazla sınıf gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-266">One or more classes may be required to drive a USB device depending on the number of interfaces contained in the USB device descriptors.</span></span>

<span data-ttu-id="238a9-267">Bu, HUB sınıfının kaydına bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="238a9-267">This is an example of the registration of the HUB class.</span></span>

```c
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);
```

<span data-ttu-id="238a9-268">Ux_host_class_register işlevi aşağıdaki prototiple sahiptir.</span><span class="sxs-lookup"><span data-stu-id="238a9-268">The function ux_host_class_register has the following prototype.</span></span>

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name, 
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

- <span data-ttu-id="238a9-269">**class_name** , sınıfın adıdır</span><span class="sxs-lookup"><span data-stu-id="238a9-269">**class_name** is the name of the class</span></span>
- <span data-ttu-id="238a9-270">**class_entry_address** , sınıfın giriş noktasıdır</span><span class="sxs-lookup"><span data-stu-id="238a9-270">**class_entry_address** is the entry point of the class</span></span>

<span data-ttu-id="238a9-271">HUB sınıfı başlatma örneğinde:</span><span class="sxs-lookup"><span data-stu-id="238a9-271">In the example of the HUB class initialization:</span></span>

- <span data-ttu-id="238a9-272">"ux_host_class_hub", hub sınıfının adıdır</span><span class="sxs-lookup"><span data-stu-id="238a9-272">"ux_host_class_hub" is the name of the hub class</span></span>
- <span data-ttu-id="238a9-273">ux_host_class_hub_entry, HUB sınıfının giriş noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="238a9-273">ux_host_class_hub_entry is the entry point of the HUB class.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="238a9-274">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="238a9-274">Troubleshooting</span></span>

<span data-ttu-id="238a9-275">USBX, bir tanıtım dosyası ve simülasyon ortamıyla birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="238a9-275">USBX is delivered with a demonstration file and a simulation environment.</span></span> <span data-ttu-id="238a9-276">Her zaman, hedef donanımda veya belirli bir demo platformunda ilk olarak çalışan tanıtım platformunu almak iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="238a9-276">It is always a good idea to get the demonstration platform running first—either on the target hardware or a specific demonstration platform.</span></span>

<span data-ttu-id="238a9-277">Tanıtım sistemi çalışmazsa, sorunu daraltmak için aşağıdaki işlemleri deneyin.</span><span class="sxs-lookup"><span data-stu-id="238a9-277">If the demonstration system does not work, try the following things to narrow the problem.</span></span>

## <a name="usbx-version-id"></a><span data-ttu-id="238a9-278">USBX sürüm KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="238a9-278">USBX Version ID</span></span>

<span data-ttu-id="238a9-279">USBX ' in geçerli sürümü, hem Kullanıcı hem de uygulama yazılımının çalışma zamanı sırasında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-279">The current version of USBX is available both to the user and the application software during run-time.</span></span> <span data-ttu-id="238a9-280">Programcı, USBX sürümünü, \***ux_port. h** _ dosyasının inceağından elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-280">The programmer can obtain the USBX version from examination of the \***ux_port.h** _ file.</span></span> <span data-ttu-id="238a9-281">Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir.</span><span class="sxs-lookup"><span data-stu-id="238a9-281">In addition, this file also contains a version history of the corresponding port.</span></span> <span data-ttu-id="238a9-282">Uygulama yazılımı, _ *_ux_port. h_* \* içinde tanımlanan _ *_ _ux_version_id_* _ genel dizesini inceleyerek USBX sürümünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="238a9-282">Application software can obtain the USBX version by examining the global string _ *_ _ux_version_id_* _, which is defined in _\*_ux_port.h_\*\*.</span></span>
