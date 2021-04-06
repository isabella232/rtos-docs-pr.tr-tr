---
title: Bölüm 2-Azure RTOS USBX cihaz yığını yüklemesi
description: USBX cihaz yığınını yüklemeyi öğrenin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 62f036af27c5da29baf9cba58b5b26631167c3a1
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377161"
---
# <a name="chapter-2---azure-rtos-usbx-device-stack-installation"></a><span data-ttu-id="a151f-103">Bölüm 2-Azure RTOS USBX cihaz yığını yüklemesi</span><span class="sxs-lookup"><span data-stu-id="a151f-103">Chapter 2 - Azure RTOS USBX Device Stack Installation</span></span>

## <a name="host-considerations"></a><span data-ttu-id="a151f-104">Ana bilgisayar konuları</span><span class="sxs-lookup"><span data-stu-id="a151f-104">Host Considerations</span></span>

### <a name="computer-type"></a><span data-ttu-id="a151f-105">Bilgisayar türü</span><span class="sxs-lookup"><span data-stu-id="a151f-105">Computer Type</span></span>

<span data-ttu-id="a151f-106">Katıştırılmış Geliştirme genellikle Windows bılgısayar veya UNIX ana bilgisayarları üzerinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-106">Embedded development is usually performed on Windows PC or Unix host computers.</span></span> <span data-ttu-id="a151f-107">Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-107">After the application is compiled, linked, and located on the host, it is downloaded to the target hardware for execution.</span></span>

### <a name="download-interfaces"></a><span data-ttu-id="a151f-108">Arabirimleri indir</span><span class="sxs-lookup"><span data-stu-id="a151f-108">Download Interfaces</span></span>

<span data-ttu-id="a151f-109">Genellikle, paralel arabirimler, USB ve Ethernet daha popüler olsa da, hedef indirme bir RS-232 seri arabirimi üzerinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="a151f-109">Usually the target download is done over an RS-232 serial interface, although parallel interfaces, USB, and Ethernet are becoming more popular.</span></span> <span data-ttu-id="a151f-110">Kullanılabilir seçenekler için geliştirme aracı belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="a151f-110">See the development tool documentation for available options.</span></span>

### <a name="debugging-tools"></a><span data-ttu-id="a151f-111">Hata ayıklama araçları</span><span class="sxs-lookup"><span data-stu-id="a151f-111">Debugging Tools</span></span>

<span data-ttu-id="a151f-112">Hata ayıklama, genellikle program görüntüsü indirdiği bağlantıyla aynı bağlantı üzerinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="a151f-112">Debugging is done typically over the same link as the program image download.</span></span> <span data-ttu-id="a151f-113">Arka plan hata ayıklama Izleyicisi (BDM) ve In-Circuit öykünücü (ıCE) araçları aracılığıyla hedefte çalışan küçük izleme programlarından farklı hata ayıklayıcılar vardır.</span><span class="sxs-lookup"><span data-stu-id="a151f-113">A variety of debuggers exist, ranging from small monitor programs running on the target through Background Debug Monitor (BDM) and In-Circuit Emulator (ICE) tools.</span></span> <span data-ttu-id="a151f-114">ICE Aracı, gerçek hedef donanımının en sağlam hata ayıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a151f-114">The ICE tool provides the most robust debugging of actual target hardware.</span></span>

### <a name="required-hard-disk-space"></a><span data-ttu-id="a151f-115">Gerekli sabit disk alanı</span><span class="sxs-lookup"><span data-stu-id="a151f-115">Required Hard Disk Space</span></span>

<span data-ttu-id="a151f-116">USBX için kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 500 Kbayt alan gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a151f-116">The source code for USBX is delivered in ASCII format and requires approximately 500 KBytes of space on the host computer's hard disk.</span></span>

### <a name="target-considerations"></a><span data-ttu-id="a151f-117">Hedef konuları</span><span class="sxs-lookup"><span data-stu-id="a151f-117">Target Considerations</span></span>

<span data-ttu-id="a151f-118">USBX, ana bilgisayar modundaki hedefte yalnızca 24 Kbayt ve 64 Kbayt arasında salt okuma belleği (ROM) arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a151f-118">USBX requires between 24 KBytes and 64 KBytes of Read Only Memory (ROM) on the target in host mode.</span></span> <span data-ttu-id="a151f-119">Gerekli bellek miktarı, kullanılan denetleyicinin türüne ve USBX ile bağlantılı USB sınıflarına bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="a151f-119">The amount of memory required is dependent on the type of controller used and the USB classes linked to USBX.</span></span> <span data-ttu-id="a151f-120">USBX genel veri yapıları ve bellek havuzu için hedefin rastgele erişim belleği (RAM) için bir 32 Kbayt gerekir.</span><span class="sxs-lookup"><span data-stu-id="a151f-120">Another 32 KBytes of the target's Random Access Memory (RAM) are required for USBX global data structures and memory pool.</span></span> <span data-ttu-id="a151f-121">Bu bellek havuzu, USB üzerindeki beklenen cihaz sayısına ve USB denetleyicisinin türüne göre de ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-121">This memory pool can also be adjusted depending on the expected number of devices on the USB and the type of USB controller.</span></span> <span data-ttu-id="a151f-122">USBX cihaz tarafı, cihaz denetleyicisinin türüne göre kabaca 10-12 K ROM gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a151f-122">The USBX device side requires roughly 10-12 K of ROM depending on the type of device controller.</span></span> <span data-ttu-id="a151f-123">RAM bellek kullanımı, cihaz tarafından Öykünülen sınıfın türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a151f-123">The RAM memory usage depends on the type of class emulated by the device.</span></span>

<span data-ttu-id="a151f-124">USBX Ayrıca, Işparçacığıx semaforları, zaman uyumu sağlayıcılar ve birden çok iş parçacığı koruması için iş parçacıklarını ve USB veri yolu topolojisini izlemek için g/ç askıya alma ve düzenli işlemeyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="a151f-124">USBX also relies on ThreadX semaphores, mutexes, and threads for multiple thread protection, and I/O suspension and periodic processing for monitoring the USB bus topology.</span></span>

### <a name="product-distribution"></a><span data-ttu-id="a151f-125">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="a151f-125">Product Distribution</span></span>

<span data-ttu-id="a151f-126">Azure RTOS USBX, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/usbx/> .</span><span class="sxs-lookup"><span data-stu-id="a151f-126">Azure RTOS USBX can be obtained from our public source code repository at <https://github.com/azure-rtos/usbx/>.</span></span>

<span data-ttu-id="a151f-127">Aşağıda, depodaki birçok önemli dosyanın bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a151f-127">The following is a list of several important files in the repository.</span></span>

* <span data-ttu-id="a151f-128">***ux_api. h***: Bu C üstbilgi dosyası tüm sistem eş, veri yapılarını ve hizmet prototiplerini içerir.</span><span class="sxs-lookup"><span data-stu-id="a151f-128">***ux_api.h***: This C header file contains all system equates, data structures, and service prototypes.</span></span>
* <span data-ttu-id="a151f-129">***ux_port. h***: Bu C üstbilgi dosyası, tüm geliştirme aracına özgü veri tanımlarını ve yapılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a151f-129">***ux_port.h***: This C header file contains all development-tool-specific data definitions and structures.</span></span>
* <span data-ttu-id="a151f-130">***UX. lib***: Bu, USBX C kitaplığının ikili sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="a151f-130">***ux.lib***:  This is the binary version of the USBX C library.</span></span> <span data-ttu-id="a151f-131">Standart paketiyle dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="a151f-131">It is distributed with the standard package.</span></span>
* <span data-ttu-id="a151f-132">***demo_usbx. c***: basıt bır USBX tanıtımı içeren c dosyası</span><span class="sxs-lookup"><span data-stu-id="a151f-132">***demo_usbx.c***: The C file containing a simple USBX demo</span></span>

<span data-ttu-id="a151f-133">Tüm dosya adları küçük harfli.</span><span class="sxs-lookup"><span data-stu-id="a151f-133">All filenames are in lower-case.</span></span> <span data-ttu-id="a151f-134">Bu adlandırma kuralı, komutları UNIX geliştirme platformlarına dönüştürmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="a151f-134">This naming convention makes it easier to convert the commands to Unix development platforms.</span></span>

## <a name="usbx-installation"></a><span data-ttu-id="a151f-135">USBX yüklemesi</span><span class="sxs-lookup"><span data-stu-id="a151f-135">USBX Installation</span></span>

<span data-ttu-id="a151f-136">USBX, GitHub deposu yerel makinenize kopyalanarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a151f-136">USBX is installed by cloning the GitHub repository to your local machine.</span></span> <span data-ttu-id="a151f-137">Aşağıda, bilgisayarınızda USBX deposunun bir kopyasını oluşturmak için tipik sözdizimi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a151f-137">The following is typical syntax for creating a clone of the USBX repository on your PC:</span></span>

```c
    git clone https://github.com/azure-rtos/usbx
```

<span data-ttu-id="a151f-138">Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a151f-138">Alternatively you can download a copy of the repository using the download button on the GitHub main page.</span></span>

<span data-ttu-id="a151f-139">Ayrıca, çevrimiçi deponun ön sayfasında USBX kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a151f-139">You will also find instructions for building the USBX library on the front page of the online repository.</span></span>

<span data-ttu-id="a151f-140">Aşağıdaki genel yönergeler, neredeyse tüm yüklemeler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="a151f-140">The following general instructions apply to virtually any installation:</span></span>

1. <span data-ttu-id="a151f-141">Konak sabit sürücüsüne daha önce ThreadX 'i yüklediğiniz dizini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a151f-141">Use the same directory in which you previously installed ThreadX on the host hard drive.</span></span> <span data-ttu-id="a151f-142">Tüm USBX adları benzersizdir ve önceki USBX yüklemesine engel olmaz.</span><span class="sxs-lookup"><span data-stu-id="a151f-142">All USBX names are unique and will not interfere with the previous USBX installation.</span></span>
1. <span data-ttu-id="a151f-143">_ *_Tx_application_define_* \* başlangıcına veya yanına \***ux_system_initialize** _ çağrısı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a151f-143">Add a call to ***ux_system_initialize** _ at or near the beginning of _*_tx_application_define_\*\*.</span></span> <span data-ttu-id="a151f-144">Bu, USBX kaynaklarının başlatıldığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="a151f-144">This is where the USBX resources are initialized.</span></span>
1. <span data-ttu-id="a151f-145">\*\*\*Ux_device_stack_initialize \*\*\* için bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a151f-145">Add a call to \***ux_device_stack_initialize\*.**</span></span>
1. <span data-ttu-id="a151f-146">Gerekli USBX sınıflarını (konak ve/veya cihazlar sınıfları) başlatmak için bir veya daha fazla çağrı ekleyin</span><span class="sxs-lookup"><span data-stu-id="a151f-146">Add one or more calls to initialize the required USBX classes (either host and/or devices classes)</span></span>
1. <span data-ttu-id="a151f-147">Sistemde kullanılabilir olan cihaz denetleyicisini başlatmak için bir veya daha fazla çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a151f-147">Add one or more calls to initialize the device controller available in the system.</span></span>
1. <span data-ttu-id="a151f-148">Alt düzey donanım başlatma ve kesme vektör yönlendirmesi eklemek için tx_low_level_initialize. c dosyasını değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-148">It may be required to modify the tx_low_level_initialize.c file to add low-level hardware initialization and interrupt vector routing.</span></span> <span data-ttu-id="a151f-149">Bu, donanım platformuna özeldir ve burada ele alınmayacak. |</span><span class="sxs-lookup"><span data-stu-id="a151f-149">This is specific to the hardware platform and will not be discussed here.|</span></span>
1. <span data-ttu-id="a151f-150">Uygulama kaynak kodunu derleme ve USBX ve ThreadX çalışma zamanı kitaplıkları (FileX ve/veya NETX), UX. a (veya UX. lib) ve TX. a (ya da TX. lib) ile bağlantı için gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-150">Compile application source code and link with the USBX and ThreadX run time libraries (FileX and/or Netx may also be required if the USB storage class and/or USB network classes are to be compiled in), ux.a (or ux.lib) and tx.a (or tx.lib).</span></span> <span data-ttu-id="a151f-151">Sonuç hedefe indirilebilir ve yürütülür!</span><span class="sxs-lookup"><span data-stu-id="a151f-151">The resulting can be downloaded to the target and executed!</span></span>

## <a name="configuration-options"></a><span data-ttu-id="a151f-152">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="a151f-152">Configuration Options</span></span>

<span data-ttu-id="a151f-153">USBX kitaplığını oluşturmak için birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="a151f-153">There are several configuration options for building the USBX library.</span></span> <span data-ttu-id="a151f-154">Tüm Seçenekler ***ux_user. h*** içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="a151f-154">All options are located in the ***ux_user.h***.</span></span>

<span data-ttu-id="a151f-155">Aşağıdaki listede her yapılandırma seçeneğinin ayrıntıları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a151f-155">The list below details each configuration option.</span></span>

| <span data-ttu-id="a151f-156">Yapılandırma &nbsp; seçeneği</span><span class="sxs-lookup"><span data-stu-id="a151f-156">Configuration&nbsp;Option</span></span> | <span data-ttu-id="a151f-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a151f-157">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a151f-158">**UX_PERIODIC_RATE**</span><span class="sxs-lookup"><span data-stu-id="a151f-158">**UX_PERIODIC_RATE**</span></span> | <span data-ttu-id="a151f-159">Bu değer, belirli bir donanım platformu için saniye başına kaç saat sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a151f-159">This value represents how many ticks per seconds for a specific hardware platform.</span></span> <span data-ttu-id="a151f-160">Varsayılan değer, milisaniye başına 1 değer belirten 1000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="a151f-160">The default is 1000 indicating 1 tick per millisecond.</span></span> |
| <span data-ttu-id="a151f-161">**UX_THREAD_STACK_SIZE**</span><span class="sxs-lookup"><span data-stu-id="a151f-161">**UX_THREAD_STACK_SIZE**</span></span> | <span data-ttu-id="a151f-162">Bu değer, USBX iş parçacıklarının bayt cinsinden yığınının boyutudur.</span><span class="sxs-lookup"><span data-stu-id="a151f-162">This value is the size of the stack in bytes for the USBX threads.</span></span> <span data-ttu-id="a151f-163">Kullanılan işlemciye ve ana bilgisayar denetleyicisine bağlı olarak genellikle 1024 bayt veya 2048 bayt olabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-163">It can be typically 1024 bytes or 2048 bytes depending on the processor used and the host controller.</span></span> |
| <span data-ttu-id="a151f-164">**UX_THREAD_PRIORITY_ENUM**</span><span class="sxs-lookup"><span data-stu-id="a151f-164">**UX_THREAD_PRIORITY_ENUM**</span></span> | <span data-ttu-id="a151f-165">Bu, veri yolu topolojisini izleyen USBX sabit listesi iş parçacıklarının ThreadX öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="a151f-165">This is the ThreadX priority value for the USBX enumeration threads that monitors the bus topology.</span></span> |
| <span data-ttu-id="a151f-166">**UX_THREAD_PRIORITY_CLASS**</span><span class="sxs-lookup"><span data-stu-id="a151f-166">**UX_THREAD_PRIORITY_CLASS**</span></span> | <span data-ttu-id="a151f-167">Bu, standart USBX iş parçacıkları için ThreadX öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="a151f-167">This is the ThreadX priority value for the standard USBX threads.</span></span> |
| <span data-ttu-id="a151f-168">**UX_THREAD_PRIORITY_KEYBOARD**</span><span class="sxs-lookup"><span data-stu-id="a151f-168">**UX_THREAD_PRIORITY_KEYBOARD**</span></span> | <span data-ttu-id="a151f-169">Bu, USBX HID Klavye sınıfı için ThreadX öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="a151f-169">This is the ThreadX priority value for the USBX HID keyboard class.</span></span> |
| <span data-ttu-id="a151f-170">**UX_THREAD_PRIORITY_DCD**</span><span class="sxs-lookup"><span data-stu-id="a151f-170">**UX_THREAD_PRIORITY_DCD**</span></span> | <span data-ttu-id="a151f-171">Bu, cihaz denetleyicisi iş parçacığı için ThreadX öncelik değeridir.</span><span class="sxs-lookup"><span data-stu-id="a151f-171">This is the ThreadX priority value for the device controller thread.</span></span> |
| <span data-ttu-id="a151f-172">**UX_NO_TIME_SLICE**</span><span class="sxs-lookup"><span data-stu-id="a151f-172">**UX_NO_TIME_SLICE**</span></span> | <span data-ttu-id="a151f-173">Bu değer aslında iş parçacıkları için kullanılacak zaman dilimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a151f-173">This value actually defines the time slice that will be used for threads.</span></span> <span data-ttu-id="a151f-174">Örneğin, 0 olarak tanımlanmışsa, ThreadX hedef bağlantı noktası zaman dilimlerini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="a151f-174">For example, if defined to 0, the ThreadX target port does not use time slices.</span></span> |
| <span data-ttu-id="a151f-175">**UX_MAX_SLAVE_CLASS_DRIVER**</span><span class="sxs-lookup"><span data-stu-id="a151f-175">**UX_MAX_SLAVE_CLASS_DRIVER**</span></span> | <span data-ttu-id="a151f-176">Bu, ux_device_stack_class_register aracılığıyla kaydedilenebilir en fazla USBX sınıfı sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="a151f-176">This is the maximum number of USBX classes that can be registered via ux_device_stack_class_register.</span></span> |
| <span data-ttu-id="a151f-177">**UX_MAX_SLAVE_LUN**</span><span class="sxs-lookup"><span data-stu-id="a151f-177">**UX_MAX_SLAVE_LUN**</span></span> | <span data-ttu-id="a151f-178">Bu değer, cihaz depolama sınıfı sürücüsünde temsil edilen SCSI Mantıksal birimlerinin geçerli sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a151f-178">This value represents the current number of SCSI logical units represented in the device storage class driver.</span></span> |
| <span data-ttu-id="a151f-179">**UX_SLAVE_CLASS_STORAGE_INCLUDE_MMC**</span><span class="sxs-lookup"><span data-stu-id="a151f-179">**UX_SLAVE_CLASS_STORAGE_INCLUDE_MMC**</span></span> | <span data-ttu-id="a151f-180">Tanımlı ise, depolama sınıfı, DVD-ROM olan çok ortamlı komutları (MMC) işleymeyecektir.</span><span class="sxs-lookup"><span data-stu-id="a151f-180">If defined, the storage class will handle Multi-Media Commands (MMC) that is, DVD-ROM.</span></span> |
| <span data-ttu-id="a151f-181">**UX_DEVICE_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**</span><span class="sxs-lookup"><span data-stu-id="a151f-181">**UX_DEVICE_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**</span></span> | <span data-ttu-id="a151f-182">Bu değer, CDC-ECD sınıfı ' paket havuzundaki NetX paketlerinin sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a151f-182">This value represents the number of NetX packets in the CDC-ECM class' packet pool.</span></span> <span data-ttu-id="a151f-183">Varsayılan değer 16 ' dır.</span><span class="sxs-lookup"><span data-stu-id="a151f-183">The default is 16.</span></span> |
| <span data-ttu-id="a151f-184">**UX_SLAVE_REQUEST_CONTROL_MAX_LENGTH**</span><span class="sxs-lookup"><span data-stu-id="a151f-184">**UX_SLAVE_REQUEST_CONTROL_MAX_LENGTH**</span></span> | <span data-ttu-id="a151f-185">Bu değer, cihaz yığınındaki bir denetim uç noktasında alınan en fazla bayt sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a151f-185">This value represents the maximum number of bytes received on a control endpoint in the device stack.</span></span> <span data-ttu-id="a151f-186">Varsayılan değer 256 bayttır, ancak bellek kısıtlama ortamlarında azaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-186">The default is 256 bytes but can be reduced in memory constraint environments.</span></span> |
| <span data-ttu-id="a151f-187">**UX_DEVICE_CLASS_HID_EVENT_BUFFER_LENGTH**</span><span class="sxs-lookup"><span data-stu-id="a151f-187">**UX_DEVICE_CLASS_HID_EVENT_BUFFER_LENGTH**</span></span> | <span data-ttu-id="a151f-188">Bu değer, bir HID raporunun bayt cinsinden uzunluk üst sınırını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a151f-188">This value represents the maximum length in bytes of a HID report.</span></span> |
| <span data-ttu-id="a151f-189">**UX_DEVICE_CLASS_HID_MAX_EVENTS_QUEUE**</span><span class="sxs-lookup"><span data-stu-id="a151f-189">**UX_DEVICE_CLASS_HID_MAX_EVENTS_QUEUE**</span></span> | <span data-ttu-id="a151f-190">Bu değer, bir kerede sıraya alınabilen en fazla HID raporu sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a151f-190">This value represents the maximum number of HID reports that can be queued at once.</span></span> |
| <span data-ttu-id="a151f-191">**UX_SLAVE_REQUEST_DATA_MAX_LENGTH**</span><span class="sxs-lookup"><span data-stu-id="a151f-191">**UX_SLAVE_REQUEST_DATA_MAX_LENGTH**</span></span> | <span data-ttu-id="a151f-192">Bu değer, cihaz yığınındaki bir toplu bitiş noktasında alınan en fazla bayt sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a151f-192">This value represents the maximum number of bytes received on a bulk endpoint in the device stack.</span></span> <span data-ttu-id="a151f-193">Varsayılan değer 4096 bayttır, ancak bellek kısıtlama ortamlarında azaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-193">The default is 4096 bytes but can be reduced in memory constraint environments.</span></span> |

## <a name="source-code-tree"></a><span data-ttu-id="a151f-194">Kaynak kod ağacı</span><span class="sxs-lookup"><span data-stu-id="a151f-194">Source Code Tree</span></span>

<span data-ttu-id="a151f-195">USBX dosyaları birkaç dizinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a151f-195">The USBX files are provided in several directories.</span></span>

![Kaynak kod ağacı](media/usbx-device-stack/source-code-tree.png)

<span data-ttu-id="a151f-197">Dosyaları adlarıyla tanınabilir hale getirmek için aşağıdaki kural benimsenmiştir:</span><span class="sxs-lookup"><span data-stu-id="a151f-197">In order to make the files recognizable by their names, the following convention has been adopted:</span></span>

| <span data-ttu-id="a151f-198">Dosya sonek adı</span><span class="sxs-lookup"><span data-stu-id="a151f-198">File Suffix Name</span></span>  | <span data-ttu-id="a151f-199">Dosya açıklaması</span><span class="sxs-lookup"><span data-stu-id="a151f-199">File description</span></span>                          |
| ----------------- | ----------------------------------------- |
| <span data-ttu-id="a151f-200">ux_host_stack</span><span class="sxs-lookup"><span data-stu-id="a151f-200">ux_host_stack</span></span>   | <span data-ttu-id="a151f-201">USBX konak yığını çekirdek dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-201">usbx host stack core files</span></span>                |
| <span data-ttu-id="a151f-202">ux_host_class</span><span class="sxs-lookup"><span data-stu-id="a151f-202">ux_host_class</span></span>   | <span data-ttu-id="a151f-203">USBX konak yığını sınıfları dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-203">usbx host stack classes files</span></span>             |
| <span data-ttu-id="a151f-204">ux_hcd</span><span class="sxs-lookup"><span data-stu-id="a151f-204">ux_hcd</span></span>           | <span data-ttu-id="a151f-205">USBX konak yığını denetleyici sürücü dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-205">usbx host stack controller driver files</span></span>   |
| <span data-ttu-id="a151f-206">ux_device_stack</span><span class="sxs-lookup"><span data-stu-id="a151f-206">ux_device_stack</span></span> | <span data-ttu-id="a151f-207">USBX cihaz yığını çekirdek dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-207">usbx device stack core files</span></span>              |
| <span data-ttu-id="a151f-208">ux_device_class</span><span class="sxs-lookup"><span data-stu-id="a151f-208">ux_device_class</span></span> | <span data-ttu-id="a151f-209">USBX cihaz yığını sınıfları dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-209">usbx device stack classes files</span></span>           |
| <span data-ttu-id="a151f-210">ux_dcd</span><span class="sxs-lookup"><span data-stu-id="a151f-210">ux_dcd</span></span>           | <span data-ttu-id="a151f-211">USBX cihaz yığını denetleyici sürücü dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-211">usbx device stack controller driver files</span></span> |
| <span data-ttu-id="a151f-212">ux_otg</span><span class="sxs-lookup"><span data-stu-id="a151f-212">ux_otg</span></span>           | <span data-ttu-id="a151f-213">USBX OTG denetleyicisi sürücüyle ilgili dosyalar</span><span class="sxs-lookup"><span data-stu-id="a151f-213">usbx otg controller driver related files</span></span>  |
| <span data-ttu-id="a151f-214">ux_pictbridge</span><span class="sxs-lookup"><span data-stu-id="a151f-214">ux_pictbridge</span></span>    | <span data-ttu-id="a151f-215">USBX PictBridge dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-215">usbx pictbridge files</span></span>                     |
| <span data-ttu-id="a151f-216">ux_utility</span><span class="sxs-lookup"><span data-stu-id="a151f-216">ux_utility</span></span>       | <span data-ttu-id="a151f-217">USBX yardımcı program işlevleri</span><span class="sxs-lookup"><span data-stu-id="a151f-217">usbx utility functions</span></span>                    |
| <span data-ttu-id="a151f-218">demo_usbx</span><span class="sxs-lookup"><span data-stu-id="a151f-218">demo_usbx</span></span>        | <span data-ttu-id="a151f-219">USBX için tanıtım dosyaları</span><span class="sxs-lookup"><span data-stu-id="a151f-219">demonstration files for USBX</span></span>              |

## <a name="initialization-of-usbx-resources"></a><span data-ttu-id="a151f-220">USBX kaynaklarının başlatılması</span><span class="sxs-lookup"><span data-stu-id="a151f-220">Initialization of USBX resources</span></span>

<span data-ttu-id="a151f-221">USBX 'in kendi bellek yöneticisi vardır.</span><span class="sxs-lookup"><span data-stu-id="a151f-221">USBX has its own memory manager.</span></span> <span data-ttu-id="a151f-222">USBX 'in ana bilgisayar veya cihaz tarafı başlatılmadan önce belleğin USBX 'e ayrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a151f-222">The memory needs to be allocated to USBX before the host or device side of USBX is initialized.</span></span> <span data-ttu-id="a151f-223">USBX bellek Yöneticisi belleğin önbelleğe alınabilme sistemlerine uyum sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-223">USBX memory manager can accommodate systems where memory can be cached.</span></span>

<span data-ttu-id="a151f-224">Aşağıdaki işlev, 128 K normal bellek ile USBX bellek kaynaklarını başlatır ve önbellek güvenli belleği için ayrı bir havuz yoktur:</span><span class="sxs-lookup"><span data-stu-id="a151f-224">The following function initializes USBX memory resources with 128 K of regular memory and no separate pool for cache safe memory:</span></span>

```c
/* Initialize USBX Memory */
ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

<span data-ttu-id="a151f-225">Ux_system_initialize prototipi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a151f-225">The prototype for the ux_system_initialize is as follows:</span></span>

```c
UINT ux_system_initialize(VOID *regular_memory_pool_start,
        ULONG regular_memory_size,
        VOID *cache_safe_memory_pool_start,
        ULONG cache_safe_memory_size);
```

<span data-ttu-id="a151f-226">Giriş parametreleri:</span><span class="sxs-lookup"><span data-stu-id="a151f-226">Input parameters:</span></span>

| <span data-ttu-id="a151f-227">Parametre</span><span class="sxs-lookup"><span data-stu-id="a151f-227">Parameter</span></span>                          | <span data-ttu-id="a151f-228">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a151f-228">Description</span></span>                             |
| ---------------------------------- | --------------------------------------- |
| <span data-ttu-id="a151f-229">VOID \* regular_memory_pool_start</span><span class="sxs-lookup"><span data-stu-id="a151f-229">VOID \*regular_memory_pool_start</span></span>    | <span data-ttu-id="a151f-230">Normal bellek havuzunun başlangıcı</span><span class="sxs-lookup"><span data-stu-id="a151f-230">Beginning of the regular memory pool</span></span>    |
| <span data-ttu-id="a151f-231">ULONG regular_memory_size</span><span class="sxs-lookup"><span data-stu-id="a151f-231">ULONG regular_memory_size</span></span>          | <span data-ttu-id="a151f-232">Normal bellek havuzunun boyutu</span><span class="sxs-lookup"><span data-stu-id="a151f-232">Size of the regular memory pool</span></span>         |
| <span data-ttu-id="a151f-233">VOID \* cache_safe_memory_pool_start</span><span class="sxs-lookup"><span data-stu-id="a151f-233">VOID \*cache_safe_memory_pool_start</span></span> | <span data-ttu-id="a151f-234">Önbellek güvenli bellek havuzunun başlangıcı</span><span class="sxs-lookup"><span data-stu-id="a151f-234">Beginning of the cache safe memory pool</span></span> |
| <span data-ttu-id="a151f-235">ULONG cache_safe_memory_size</span><span class="sxs-lookup"><span data-stu-id="a151f-235">ULONG cache_safe_memory_size</span></span>       | <span data-ttu-id="a151f-236">Önbellek güvenli bellek havuzunun boyutu</span><span class="sxs-lookup"><span data-stu-id="a151f-236">Size of the cache safe memory pool</span></span>      |

<span data-ttu-id="a151f-237">Tüm sistemler önbellek güvenli belleği tanımını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="a151f-237">Not all systems require the definition of cache safe memory.</span></span> <span data-ttu-id="a151f-238">Böyle bir sistemde, bellek işaretçisi için başlatma sırasında geçirilen değerler UX_NULL olarak ayarlanacak ve havuzun boyutu 0 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a151f-238">In such a system, the values passed during the initialization for the memory pointer will be set to UX_NULL and the size of the pool to 0.</span></span> <span data-ttu-id="a151f-239">USBX daha sonra önbellek güvenli havuzunun yerine normal bellek havuzunu kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a151f-239">USBX will then use the regular memory pool in lieu of the cache safe pool.</span></span>

<span data-ttu-id="a151f-240">Normal belleğin önbellek güvenli olmadığı ve bir denetleyicinin DMA belleği gerçekleştirmesi gereken bir sistemde, önbellek güvenli bölgesinde bir bellek havuzu tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a151f-240">In a system where the regular memory is not cache safe and a controller requires to perform DMA memory it is necessary to define a memory pool in a cache safe zone.</span></span>

## <a name="uninitialization-of-usbx-resources"></a><span data-ttu-id="a151f-241">USBX kaynaklarının başlatılması geri alınıyor</span><span class="sxs-lookup"><span data-stu-id="a151f-241">Uninitialization of USBX resources</span></span>

<span data-ttu-id="a151f-242">USBX, kaynakları serbest bırakarak sonlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-242">USBX can be terminated by releasing its resources.</span></span> <span data-ttu-id="a151f-243">USBX 'i sonlandırmadan önce tüm sınıfların ve denetleyici kaynaklarının düzgün şekilde sonlandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a151f-243">Prior to terminating usbx, all classes and controller resources need to be terminated properly.</span></span> <span data-ttu-id="a151f-244">Aşağıdaki işlev, USBX bellek kaynaklarını başlatır:</span><span class="sxs-lookup"><span data-stu-id="a151f-244">The following function uninitializes USBX memory resources:</span></span>

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

<span data-ttu-id="a151f-245">Ux_system_initialize prototipi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a151f-245">The prototype for the ux_system_initialize is as follows:</span></span>

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-device-controller"></a><span data-ttu-id="a151f-246">USB cihaz denetleyicisinin tanımı</span><span class="sxs-lookup"><span data-stu-id="a151f-246">Definition of USB Device Controller</span></span>

<span data-ttu-id="a151f-247">Cihaz modunda çalışmak için herhangi bir zamanda yalnızca bir USB cihaz denetleyicisi tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-247">Only one USB device controller can be defined at any time to operate in device mode.</span></span> <span data-ttu-id="a151f-248">Uygulama başlatma dosyası bu tanımı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="a151f-248">The application initialization file should contain this definition.</span></span> <span data-ttu-id="a151f-249">Aşağıdaki satır genel bir USB denetleyicisinin tanımını gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="a151f-249">The following line performs the definition of a generic usb controller:</span></span>

```c
ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);
```

<span data-ttu-id="a151f-250">USB cihazının başlatılması aşağıdaki prototiple sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a151f-250">The USB device initialization has the following prototype:</span></span>

```c
UINT ux_dcd_controller_initialize(ULONG dcd_io,
    ULONG dcd_irq, ULONG dcd_vbus_address);
```

<span data-ttu-id="a151f-251">Şu parametrelerle birlikte:</span><span class="sxs-lookup"><span data-stu-id="a151f-251">with the following parameters:</span></span>

| <span data-ttu-id="a151f-252">Pararmetre</span><span class="sxs-lookup"><span data-stu-id="a151f-252">Pararmeter</span></span>               | <span data-ttu-id="a151f-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a151f-253">Description</span></span>                      |
| ------------------------ | -------------------------------- |
| <span data-ttu-id="a151f-254">ULONG dcd_io</span><span class="sxs-lookup"><span data-stu-id="a151f-254">ULONG dcd_io</span></span>            | <span data-ttu-id="a151f-255">Denetleyici GÇ adresi</span><span class="sxs-lookup"><span data-stu-id="a151f-255">Address of the controller IO</span></span>     |
| <span data-ttu-id="a151f-256">ULONG dcd_irq</span><span class="sxs-lookup"><span data-stu-id="a151f-256">ULONG dcd_irq</span></span>           | <span data-ttu-id="a151f-257">Denetleyici tarafından kullanılan kesme</span><span class="sxs-lookup"><span data-stu-id="a151f-257">Interrupt used by the controller</span></span> |
| <span data-ttu-id="a151f-258">ULONG dcd_vbus_address</span><span class="sxs-lookup"><span data-stu-id="a151f-258">ULONG dcd_vbus_address</span></span> | <span data-ttu-id="a151f-259">VBUS GıO adresi</span><span class="sxs-lookup"><span data-stu-id="a151f-259">Address of the VBUS GPIO</span></span>         |

<span data-ttu-id="a151f-260">Aşağıdaki örnek, Storage cihaz sınıfı ve genel bir denetleyici ile USBX 'in cihaz modunda başlatılması örneğidir:</span><span class="sxs-lookup"><span data-stu-id="a151f-260">The following example is the initialization of USBX in device mode with the storage device class and a generic controller:</span></span>

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024), 0, 0);

/* The code below is required for installing the device portion of USBX */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, installation was successful. */

/* Store the number of LUN in this device storage instance: single LUN. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 1;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x1e6bfe;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read = tx_demo_thread_flash_media_read;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write = tx_demo_thread_flash_media_write;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status = tx_demo_thread_flash_media_status;

/* Initialize the device storage class. The class is connected with interface 0 */
status = ux_device_stack_class_register(ux_system_slave_class_storage_name ux_device_class_storage_entry,
    ux_device_class_storage_thread,0, (VOID *)&storage_parameter);

/* Register the device controllers available in this system */
status = ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);

/* If status equals UX_SUCCESS, registration was successful. */
```

## <a name="troubleshooting"></a><span data-ttu-id="a151f-261">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="a151f-261">Troubleshooting</span></span>

<span data-ttu-id="a151f-262">USBX, bir tanıtım dosyası ve simülasyon ortamıyla birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="a151f-262">USBX is delivered with a demonstration file and a simulation environment.</span></span> <span data-ttu-id="a151f-263">Her zaman, hedef donanımda veya belirli bir demo platformunda ilk olarak çalışan tanıtım platformunu almak iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="a151f-263">It is always a good idea to get the demonstration platform running first—either on the target hardware or a specific demonstration platform.</span></span>

## <a name="usbx-version-id"></a><span data-ttu-id="a151f-264">USBX sürüm KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="a151f-264">USBX Version ID</span></span>

<span data-ttu-id="a151f-265">USBX ' in geçerli sürümü, hem Kullanıcı hem de uygulama yazılımının çalışma zamanı sırasında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-265">The current version of USBX is available both to the user and the application software during run-time.</span></span> <span data-ttu-id="a151f-266">Programcı, USBX sürümünü, \***ux_port. h** _ dosyasının inceağından elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-266">The programmer can obtain the USBX version from examination of the \***ux_port.h** _ file.</span></span> <span data-ttu-id="a151f-267">Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir.</span><span class="sxs-lookup"><span data-stu-id="a151f-267">In addition, this file also contains a version history of the corresponding port.</span></span> <span data-ttu-id="a151f-268">Uygulama yazılımı, _ *_ux_port. h_* \* içinde tanımlanan _ *_ _ux_version_id_* _ genel dizesini inceleyerek USBX sürümünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="a151f-268">Application software can obtain the USBX version by examining the global string _ *_ _ux_version_id_* _, which is defined in _\*_ux_port.h_\*\*.</span></span>
