---
title: Bölüm 2-Azure RTOS ThreadX yükleme ve kullanımı
description: Bu bölümde, yüksek performanslı Azure RTOS ThreadX çekirdeğinin yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e1bf85d363b07c81f226d494107eae9ba18114a7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825456"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-threadx"></a><span data-ttu-id="273b9-103">Bölüm 2-Azure RTOS ThreadX yükleme ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="273b9-103">Chapter 2 - Installation and Use of Azure RTOS ThreadX</span></span>

<span data-ttu-id="273b9-104">Bu bölümde, yüksek performanslı Azure RTOS ThreadX çekirdeğinin yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="273b9-104">This chapter contains a description of various issues related to installation, setup, and usage of the high-performance Azure RTOS ThreadX kernel.</span></span>

## <a name="host-considerations"></a><span data-ttu-id="273b9-105">Ana bilgisayar konuları</span><span class="sxs-lookup"><span data-stu-id="273b9-105">Host Considerations</span></span>

<span data-ttu-id="273b9-106">Katıştırılmış yazılım genellikle Windows veya Linux (UNIX) ana bilgisayar bilgisayarlarında geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="273b9-106">Embedded software is usually developed on Windows or Linux (Unix) host computers.</span></span> <span data-ttu-id="273b9-107">Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-107">After the application is compiled, linked, and located on the host, it is downloaded to the target hardware for execution.</span></span>

<span data-ttu-id="273b9-108">Genellikle hedef indirme, geliştirme aracı hata ayıklayıcısı içinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="273b9-108">Usually the target download is done from within the development tool debugger.</span></span> <span data-ttu-id="273b9-109">İndirme tamamlandıktan sonra, hata ayıklayıcı hedef yürütme denetimi (go, dur, kesme noktası, vb.) sağlamaktan ve bellek ve işlemci kayıtlarına erişime karşı sorumludur.</span><span class="sxs-lookup"><span data-stu-id="273b9-109">After the download has completed, the debugger is responsible for providing target execution control (go, halt, breakpoint, etc.) as well as access to memory and processor registers.</span></span>

<span data-ttu-id="273b9-110">Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="273b9-110">Most development tool debuggers communicate with the target hardware via on-chip debug (OCD) connections such as JTAG (IEEE 1149.1) and Background Debug Mode (BDM).</span></span> <span data-ttu-id="273b9-111">Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="273b9-111">Debuggers also communicate with target hardware through In-Circuit Emulation (ICE) connections.</span></span> <span data-ttu-id="273b9-112">OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-112">Both OCD and ICE connections provide robust solutions with minimal intrusion on the target resident software.</span></span>

<span data-ttu-id="273b9-113">Konakta kullanılan kaynaklar için, ThreadX kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 1 MB alan gerektirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-113">As for resources used on the host, the source code for ThreadX is delivered in ASCII format and requires approximately 1 MByte of space on the host computer's hard disk.</span></span>

## <a name="target-considerations"></a><span data-ttu-id="273b9-114">Hedef konuları</span><span class="sxs-lookup"><span data-stu-id="273b9-114">Target Considerations</span></span>

<span data-ttu-id="273b9-115">ThreadX, hedefte 2 Kbayt ile 20 Kbayt arasında salt okuma belleği (ROM) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-115">ThreadX requires between 2 KBytes and 20 KBytes of Read Only Memory (ROM) on the target.</span></span> <span data-ttu-id="273b9-116">Ayrıca, ThreadX Sistem yığını ve diğer genel veri yapıları için hedefin rastgele erişim belleği (RAM) için bir 1 ile 2 kilobayt daha gerektirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-116">It also requires another 1 to 2 KBytes of the target's Random Access Memory (RAM) for the ThreadX system stack and other global data structures.</span></span>

<span data-ttu-id="273b9-117">Hizmet çağrısı zaman aşımları, zaman dilimme ve uygulama zamanlayıcıları gibi Zamanlayıcı ile ilgili işlevlerde, temeldeki hedef donanımın düzenli bir kesme kaynağı sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="273b9-117">For timer-related functions like service call time-outs, time-slicing, and application timers to function, the underlying target hardware must provide a periodic interrupt source.</span></span> <span data-ttu-id="273b9-118">İşlemcinin bu özelliği varsa, ThreadX tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="273b9-118">If the processor has this capability, it is utilized by ThreadX.</span></span> <span data-ttu-id="273b9-119">Aksi takdirde, hedef işlemcinin düzenli bir kesme üretme özelliği yoksa, kullanıcının donanımının bunu sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="273b9-119">Otherwise, if the target processor does not have the ability to generate a periodic interrupt, the user's hardware must provide it.</span></span> <span data-ttu-id="273b9-120">Süreölçer kesmesi kurulumu ve yapılandırması, genellikle ThreadX dağıtımındaki ***tx_initialize_low_level*** derleme dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="273b9-120">Setup and configuration of the timer interrupt is typically located in the ***tx_initialize_low_level*** assembly file in the ThreadX distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="273b9-121">*Dönemsel süreölçer kesme kaynağı kullanılabilir olmasa bile ThreadX hala işlevsel olur. Ancak, zamanlayıcıyla ilgili hizmetlerden hiçbiri işlevsel değildir.*</span><span class="sxs-lookup"><span data-stu-id="273b9-121">*ThreadX is still functional even if no periodic timer interrupt source is available. However, none of the timer-related services are functional.*</span></span>

## <a name="product-distribution"></a><span data-ttu-id="273b9-122">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="273b9-122">Product Distribution</span></span>

<span data-ttu-id="273b9-123">Azure RTOS ThreadX, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/threadx/> .</span><span class="sxs-lookup"><span data-stu-id="273b9-123">Azure RTOS ThreadX can be obtained from our public source code repository at <https://github.com/azure-rtos/threadx/>.</span></span>

<span data-ttu-id="273b9-124">Aşağıda, depodaki birçok önemli dosyanın bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="273b9-124">The following is a list of several important files in the repository.</span></span>

| <span data-ttu-id="273b9-125">Kısaltın</span><span class="sxs-lookup"><span data-stu-id="273b9-125">Filename</span></span> | <span data-ttu-id="273b9-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="273b9-126">Description</span></span> |
|------------------- | ----------- |
| <span data-ttu-id="273b9-127">**tx_api. h**</span><span class="sxs-lookup"><span data-stu-id="273b9-127">**tx_api.h**</span></span>                      | <span data-ttu-id="273b9-128">Tüm sistem eşlerini, veri yapılarını ve hizmet prototiplerini içeren C üstbilgi dosyası.</span><span class="sxs-lookup"><span data-stu-id="273b9-128">C header file containing all system equates, data structures, and service prototypes.</span></span>                                                             |
| <span data-ttu-id="273b9-129">**tx_port. h**</span><span class="sxs-lookup"><span data-stu-id="273b9-129">**tx_port.h**</span></span>                     | <span data-ttu-id="273b9-130">Tüm geliştirme araçlarını ve targetspecific veri tanımlarını ve yapılarını içeren C üstbilgi dosyası.</span><span class="sxs-lookup"><span data-stu-id="273b9-130">C header file containing all development-tool and targetspecific data definitions and structures.</span></span>                                                 |
| <span data-ttu-id="273b9-131">**demo_threadx. c**</span><span class="sxs-lookup"><span data-stu-id="273b9-131">**demo_threadx.c**</span></span>                | <span data-ttu-id="273b9-132">Küçük bir demo uygulaması içeren C dosyası.</span><span class="sxs-lookup"><span data-stu-id="273b9-132">C file containing a small demo application.</span></span>                                                                                                       |
| <span data-ttu-id="273b9-133">**TX. a (veya TX. lib)**</span><span class="sxs-lookup"><span data-stu-id="273b9-133">**tx.a (or tx.lib)**</span></span>              | <span data-ttu-id="273b9-134">*Standart* paketiyle dağıtılan Threadx C kitaplığının ikili sürümü.</span><span class="sxs-lookup"><span data-stu-id="273b9-134">Binary version of the ThreadX C library that is distributed with the *standard* package.</span></span>                                                          |
|                                   |                                                                                                                                                   |

>[!NOTE]
><span data-ttu-id="273b9-135">*Tüm dosya adları küçük bir durumdur. Bu adlandırma kuralı, komutların Linux (UNIX) geliştirme platformlarına dönüştürülmesini kolaylaştırır.*</span><span class="sxs-lookup"><span data-stu-id="273b9-135">*All file names are in lower-case. This naming convention makes it easier to convert the commands to Linux (Unix) development platforms.*</span></span>

## <a name="threadx-installation"></a><span data-ttu-id="273b9-136">ThreadX yüklemesi</span><span class="sxs-lookup"><span data-stu-id="273b9-136">ThreadX Installation</span></span>

<span data-ttu-id="273b9-137">ThreadX, GitHub deposu yerel makinenize kopyalanarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="273b9-137">ThreadX is installed by cloning the GitHub repository to your local machine.</span></span> <span data-ttu-id="273b9-138">Bilgisayarınızda ThreadX deposunun bir kopyasını oluşturmak için tipik sözdizimi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="273b9-138">The following is typical syntax for creating a clone of the ThreadX repository on your PC.</span></span>

```c
    git clone https://github.com/azure-rtos/threadx
```

<span data-ttu-id="273b9-139">Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="273b9-139">Alternatively you can download a copy of the repository using the download button on the GitHub main page.</span></span>

<span data-ttu-id="273b9-140">Ayrıca, çevrimiçi deponun ön sayfasında ThreadX kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="273b9-140">You will also find instructions for building the ThreadX library on the front page of the online repository.</span></span>

> [!NOTE]
> <span data-ttu-id="273b9-141">\* Uygulama yazılımının ThreadX kitaplık dosyasına (genellikle **TX. a** veya **TX. lib**) ve C içerme dosyalarına **_tx_api. h_* _ ve _*_tx_port. h_\*_ erişimi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="273b9-141">*Application software needs access to the ThreadX library file (usually **tx.a** or **tx.lib**) and the C include files **_tx_api.h_* _ and _*_tx_port.h_*_.</span></span> <span data-ttu-id="273b9-142">Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaların uygulama geliştirme area._ kopyalanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-142">This is accomplished either by setting the appropriate path for the development tools or by copying these files into the application development area._</span></span>

## <a name="using-threadx"></a><span data-ttu-id="273b9-143">ThreadX kullanma</span><span class="sxs-lookup"><span data-stu-id="273b9-143">Using ThreadX</span></span>

<span data-ttu-id="273b9-144">ThreadX kullanmak için, uygulama kodu derleme sırasında ***tx_api. h** _ Içermeli ve threadx çalışma zamanı kitaplığı _*_TX. a_\*_ (veya _ *_TX. lib_* \*) ile bağlantı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="273b9-144">To use ThreadX, the application code must include ***tx_api.h** _ during compilation and link with the ThreadX run-time library _*_tx.a_*_ (or _*_tx.lib_\*\*).</span></span>

<span data-ttu-id="273b9-145">Bir ThreadX uygulaması derlemek için gereken dört adım vardır.</span><span class="sxs-lookup"><span data-stu-id="273b9-145">There are four steps required to build a ThreadX application.</span></span>

1. <span data-ttu-id="273b9-146">***Tx_api. h*** dosyasını threadx Hizmetleri veya veri yapıları kullanan tüm uygulama dosyalarına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="273b9-146">Include the ***tx_api.h*** file in all application files that use ThreadX services or data structures.</span></span>

1. <span data-ttu-id="273b9-147">Standart C \***Main** _ işlevini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="273b9-147">Create the standard C \***main** _ function.</span></span> <span data-ttu-id="273b9-148">Bu işlev, ThreadX 'i başlatmak için sonunda _ *_tx_kernel_enter_*\* çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="273b9-148">This function must eventually call _ *_tx_kernel_enter_*\* to start ThreadX.</span></span> <span data-ttu-id="273b9-149">Çekirdek girilmeden önce, ThreadX içermeyen uygulamaya özgü başlatma eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-149">Application-specific initialization that does not involve ThreadX may be added prior to entering the kernel.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="273b9-150">\* ThreadX giriş işlevi \***tx_kernel_enter** _ döndürmüyor.</span><span class="sxs-lookup"><span data-stu-id="273b9-150">\*The ThreadX entry function \***tx_kernel_enter** _ does not return.</span></span> <span data-ttu-id="273b9-151">Bu nedenle, it._ sonra herhangi bir işlem veya işlev çağrısı yerleştirmediğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="273b9-151">So be sure not to place any processing or function calls after it._</span></span>

1. <span data-ttu-id="273b9-152">***Tx_application_define*** işlevini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="273b9-152">Create the ***tx_application_define*** function.</span></span> <span data-ttu-id="273b9-153">Bu, ilk sistem kaynaklarının oluşturulduğu yerdir.</span><span class="sxs-lookup"><span data-stu-id="273b9-153">This is where the initial system resources are created.</span></span> <span data-ttu-id="273b9-154">Sistem kaynaklarına örnek olarak iş parçacıkları, kuyruklar, bellek havuzları, olay bayrakları grupları, zaman uyumu sağlayıcılar ve semaforlar verilebilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-154">Examples of system resources include threads, queues, memory pools, event flags groups, mutexes, and semaphores.</span></span>

1. <span data-ttu-id="273b9-155">Uygulama kaynağını derleyin ve ThreadX çalışma zamanı kitaplığı ***TX. lib*** ile bağlayın.</span><span class="sxs-lookup"><span data-stu-id="273b9-155">Compile application source and link with the ThreadX run-time library ***tx.lib***.</span></span> <span data-ttu-id="273b9-156">Elde edilen görüntü hedefe indirilebilir ve yürütülür!</span><span class="sxs-lookup"><span data-stu-id="273b9-156">The resulting image can be downloaded to the target and executed!</span></span>

## <a name="small-example-system"></a><span data-ttu-id="273b9-157">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="273b9-157">Small Example System</span></span>

<span data-ttu-id="273b9-158">Şekil 1 ' deki küçük örnek sistem, önceliği 3 olan tek bir iş parçacığının oluşturulmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="273b9-158">The small example system in Figure 1 shows the creation of a single thread with a priority of 3.</span></span> <span data-ttu-id="273b9-159">İş parçacığı yürütülür, bir sayacı artırır, sonra bir saat çentik için uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="273b9-159">The thread executes, increments a counter, then sleeps for one clock tick.</span></span>
<span data-ttu-id="273b9-160">Bu işlem süresiz olarak devam eder.</span><span class="sxs-lookup"><span data-stu-id="273b9-160">This process continues forever.</span></span>

```c
#include "tx_api.h"
unsigned long my_thread_counter = 0;
TX_THREAD my_thread;
main( )
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter( );
}
void tx_application_define(void *first_unused_memory)
{
    /* Create my_thread! */
    tx_thread_create(&my_thread, "My Thread",
    my_thread_entry, 0x1234, first_unused_memory, 1024,
    3, 3, TX_NO_TIME_SLICE, TX_AUTO_START);
}
void my_thread_entry(ULONG thread_input)
{
    /* Enter into a forever loop. */
    while(1)
    {
        /* Increment thread counter. */
        my_thread_counter++;
        /* Sleep for 1 tick. */
        tx_thread_sleep(1);
    }
}
```

<span data-ttu-id="273b9-161">**ŞEKIL 1. Uygulama geliştirme şablonu**</span><span class="sxs-lookup"><span data-stu-id="273b9-161">**FIGURE 1. Template for Application Development**</span></span>

<span data-ttu-id="273b9-162">Bu basit bir örnek olsa da, gerçek uygulama geliştirmesi için iyi bir şablon sağlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-162">Although this is a simple example, it provides a good template for real application development.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="273b9-163">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="273b9-163">Troubleshooting</span></span>

<span data-ttu-id="273b9-164">Her ThreadX bağlantı noktası, bir demo uygulaması ile birlikte dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="273b9-164">Each ThreadX port is delivered with a demonstration application.</span></span> <span data-ttu-id="273b9-165">Her zaman, gerçek hedef donanım veya sanal ortam üzerinde tanıtım sisteminin çalışmasını sağlamak iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="273b9-165">It is always a good idea to first get the demonstration system running—either on actual target hardware or simulated environment.</span></span>

<span data-ttu-id="273b9-166">Tanıtım sistemi düzgün yürütülemez, bazı sorun giderme ipuçları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="273b9-166">If the demonstration system does not execute properly, the following are some troubleshooting tips.</span></span>

1. <span data-ttu-id="273b9-167">Tanıtım 'in ne kadarının çalıştığını belirleme.</span><span class="sxs-lookup"><span data-stu-id="273b9-167">Determine how much of the demonstration is running.</span></span>
1. <span data-ttu-id="273b9-168">Yığın boyutlarını artırın (gerçek uygulama kodunda tanıtım için olduğundan daha önemlidir).</span><span class="sxs-lookup"><span data-stu-id="273b9-168">Increase stack sizes (this is more important in actual application code than it is for the demonstration).</span></span>
1. <span data-ttu-id="273b9-169">ThreadX kitaplığını tanımlanan TX_ENABLE_STACK_CHECKING yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="273b9-169">Rebuild the ThreadX library with TX_ENABLE_STACK_CHECKING defined.</span></span> <span data-ttu-id="273b9-170">Bu, yerleşik ThreadX yığın denetimini sunar.</span><span class="sxs-lookup"><span data-stu-id="273b9-170">This enables the built-in ThreadX stack checking.</span></span>
1. <span data-ttu-id="273b9-171">Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın.</span><span class="sxs-lookup"><span data-stu-id="273b9-171">Temporarily bypass any recent changes to see if the problem disappears or changes.</span></span> <span data-ttu-id="273b9-172">Bu tür bilgiler mühendislerin desteklenmesi için yararlı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="273b9-172">Such information should prove useful to support engineers.</span></span>

<span data-ttu-id="273b9-173">Sorun giderme adımlarından toplanan bilgileri göndermek için "[Müşteri Destek Merkezi](about-this-guide.md#customer-support-center)" bölümünde özetlenen yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="273b9-173">Follow the procedures outlined in "[Customer Support Center](about-this-guide.md#customer-support-center)" to send the information gathered from the troubleshooting steps.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="273b9-174">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="273b9-174">Configuration Options</span></span>

<span data-ttu-id="273b9-175">Threadx kitaplığı ve uygulama için ThreadX kullanarak birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="273b9-175">There are several configuration options when building the ThreadX library and the application using ThreadX.</span></span> <span data-ttu-id="273b9-176">Aşağıdaki seçenekler uygulama kaynağında, komut satırında veya ***tx_user. h*** içerme dosyası içinde tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-176">The options below can be defined in the application source, on the command line, or within the ***tx_user.h*** include file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="273b9-177">\* ***Tx_user. h** _ ' de tanımlanan seçenekler, yalnızca uygulama ve threadx kitaplığı _ *TX_INCLUDE_USER_DEFINE_FILE** tanımlı ile derlenme uygulandığında uygulanır.\*</span><span class="sxs-lookup"><span data-stu-id="273b9-177">*Options defined in ***tx_user.h** _ are applied only if the application and ThreadX library are built with _ *TX_INCLUDE_USER_DEFINE_FILE** defined.*</span></span>

### <a name="smallest-configuration"></a><span data-ttu-id="273b9-178">En küçük yapılandırma</span><span class="sxs-lookup"><span data-stu-id="273b9-178">Smallest Configuration</span></span>

<span data-ttu-id="273b9-179">En küçük kod boyutu için, aşağıdaki ThreadX yapılandırma seçenekleri göz önünde bulundurulmalıdır (diğer tüm seçeneklerin yokluğu olarak).</span><span class="sxs-lookup"><span data-stu-id="273b9-179">For the smallest code size, the following ThreadX configuration options should be considered (in absence of all other options).</span></span>

```c
TX_DISABLE_ERROR_CHECKING
TX_DISABLE_PREEMPTION_THRESHOLD
TX_DISABLE_NOTIFY_CALLBACKS
TX_DISABLE_REDUNDANT_CLEARING
TX_DISABLE_STACK_FILLING
TX_NOT_INTERRUPTABLE
TX_TIMER_PROCESS_IN_ISR
```

### <a name="fastest-configuration"></a><span data-ttu-id="273b9-180">En hızlı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="273b9-180">Fastest Configuration</span></span>

<span data-ttu-id="273b9-181">En hızlı yürütme için, daha önce en küçük yapılandırma için kullanılan yapılandırma seçenekleri, ancak bu seçeneklerle aynı zamanda göz önünde bulundurululur.</span><span class="sxs-lookup"><span data-stu-id="273b9-181">For the fastest execution, the same configuration options used for the Smallest Configuration previously, but with these options also considered.</span></span>

```c
TX_REACTIVATE_INLINE
TX_INLINE_THREAD_RESUME_SUSPEND
```

<span data-ttu-id="273b9-182">[Ayrıntılı yapılandırma seçenekleri](#detailed-configuration-options) açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="273b9-182">[Detailed configuration options](#detailed-configuration-options) are described.</span></span>

### <a name="global-time-source"></a><span data-ttu-id="273b9-183">Küresel saat kaynağı</span><span class="sxs-lookup"><span data-stu-id="273b9-183">Global Time Source</span></span>

<span data-ttu-id="273b9-184">Diğer Microsoft Azure RTOS ürünleri (FileX, NetX, GUıDX, USBX, vb.) için ThreadX, bir saniye temsil eden ThreadX Zamanlayıcı işareti sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-184">For other Microsoft Azure RTOS products (FileX, NetX, GUIX, USBX, etc.), ThreadX defines the number of ThreadX timer ticks that represents one second.</span></span> <span data-ttu-id="273b9-185">Diğerleri zaman gereksinimlerini bu sabiti temel alarak türeteler.</span><span class="sxs-lookup"><span data-stu-id="273b9-185">Others derive their time requirements based on this constant.</span></span> <span data-ttu-id="273b9-186">Varsayılan olarak, değer 100 ' dir ve bir 10 MS dönemsel kesmesi varsayılıyor.</span><span class="sxs-lookup"><span data-stu-id="273b9-186">By default, the value is 100, assuming a 10ms periodic interrupt.</span></span> <span data-ttu-id="273b9-187">Kullanıcı, ***tx_port. h*** veya IDE veya komut satırı içindeki istenen değeri TX_TIMER_TICKS_PER_SECOND tanımlayarak bu değeri geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-187">The user may override this value by defining TX_TIMER_TICKS_PER_SECOND with the desired value in ***tx_port.h*** or within the IDE or command line.</span></span>

### <a name="detailed-configuration-options"></a><span data-ttu-id="273b9-188">Ayrıntılı yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="273b9-188">Detailed Configuration Options</span></span>

<span data-ttu-id="273b9-189">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-189">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-190">Bu seçenek tanımlandığı zaman, bayt havuzlarındaki performans bilgilerinin toplanmasında izin vermez.</span><span class="sxs-lookup"><span data-stu-id="273b9-190">When defined, this option enables the gathering of performance information on byte pools.</span></span> <span data-ttu-id="273b9-191">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-191">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-192">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-192">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-193">Bu seçenek tanımlandığı zaman, bayt havuzlarındaki performans bilgilerinin toplanmasında izin vermez.</span><span class="sxs-lookup"><span data-stu-id="273b9-193">When defined, this option enables the gathering of performance information on byte pools.</span></span> <span data-ttu-id="273b9-194">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-194">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-195">**TX_DISABLE_ERROR_CHECKING**</span><span class="sxs-lookup"><span data-stu-id="273b9-195">**TX_DISABLE_ERROR_CHECKING**</span></span>

<span data-ttu-id="273b9-196">Temel hizmet çağrısı hata denetimini atlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-196">Bypasses basic service call error checking.</span></span> <span data-ttu-id="273b9-197">Uygulama kaynağında tanımlandığında, tüm temel parametre hata denetimi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="273b9-197">When defined in the application source, all basic parameter error checking is disabled.</span></span> <span data-ttu-id="273b9-198">Bu, performansı %30 ' a kadar iyileştirebilir ve resim boyutunu da azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-198">This may improve performance by as much as 30% and may also reduce the image size.</span></span>

> [!NOTE]
> <span data-ttu-id="273b9-199">*Yalnızca uygulamanın tüm giriş parametrelerini, dış girişten türetilmiş giriş parametreleri de dahil olmak üzere tüm koşullarda her zaman geçerli olacağını düşünüyorsanız, hata denetimini devre dışı bırakabilirsiniz. Hata denetimi devre dışı olduğunda API için geçersiz giriş sağlanırsa, ortaya çıkan davranış tanımsızdır ve bellek bozulması veya sistem kilitlenmesiyle sonuçlanabilir.*</span><span class="sxs-lookup"><span data-stu-id="273b9-199">*It is only safe to disable error checking if the application can absolutely guarantee all input parameters are always valid under all circumstances, including input parameters derived from external input. If invalid input is supplied to the API with error checking disabled, the resulting behavior is undefined and could result in memory corruption or system crash.*</span></span>

> [!NOTE]
> <span data-ttu-id="273b9-200">*Bir hata denetimini devre dışı bırakarak etkilenmeyen ThreadX API dönüş değerleri, Bölüm 4 ' teki her API açıklamasının "dönüş değerleri" bölümünde kalın olarak listelenir. Hata denetimi TX_DISABLE_ERROR_CHECKING seçeneği kullanılarak devre dışı bırakılmışsa, kalın olmayan dönüş değerleri hükümsüz olur.*</span><span class="sxs-lookup"><span data-stu-id="273b9-200">*ThreadX API return values not affected by disabling error checking are listed in bold in the “Return Values” section of each API description in Chapter 4. The nonbold return values are void if error checking is disabled by using the TX_DISABLE_ERROR_CHECKING option.*</span></span>

<span data-ttu-id="273b9-201">**TX_DISABLE_NOTIFY_CALLBACKS**</span><span class="sxs-lookup"><span data-stu-id="273b9-201">**TX_DISABLE_NOTIFY_CALLBACKS**</span></span>

<span data-ttu-id="273b9-202">Tanımlandığında, çeşitli ThreadX nesneleri için bildirim geri aramalarını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="273b9-202">When defined, disables the notify callbacks for various ThreadX objects.</span></span> <span data-ttu-id="273b9-203">Bu seçeneğin kullanılması, kod boyutunu biraz azaltır ve performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-203">Using this option slightly reduces code size and improves performance.</span></span> <span data-ttu-id="273b9-204">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-204">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-205">**TX_DISABLE_PREEMPTION_THRESHOLD**</span><span class="sxs-lookup"><span data-stu-id="273b9-205">**TX_DISABLE_PREEMPTION_THRESHOLD**</span></span>

<span data-ttu-id="273b9-206">Tanımlandığında, önalım-Threshold özelliğini devre dışı bırakır ve kod boyutunu biraz azaltır ve performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-206">When defined, disables the preemption-threshold feature and slightly reduces code size and improves performance.</span></span> <span data-ttu-id="273b9-207">Kuşkusuz, önalım-Threshold özellikleri artık kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="273b9-207">Of course, the preemption-threshold capabilities are no longer available.</span></span> <span data-ttu-id="273b9-208">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-208">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-209">**TX_DISABLE_REDUNDANT_CLEARING**</span><span class="sxs-lookup"><span data-stu-id="273b9-209">**TX_DISABLE_REDUNDANT_CLEARING**</span></span>

<span data-ttu-id="273b9-210">Tanımlandığında, ThreadX Global C veri yapılarını sıfıra başlatma mantığını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="273b9-210">When defined, removes the logic for initializing ThreadX global C data structures to zero.</span></span> <span data-ttu-id="273b9-211">Bu, yalnızca derleyicinin başlatma kodu tüm başlatılmamış C genel verilerini sıfıra ayarlarsa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="273b9-211">This should only be used if the compiler's initialization code sets all un-initialized C global data to zero.</span></span> <span data-ttu-id="273b9-212">Bu seçeneğin kullanılması, kod boyutunu biraz azaltır ve başlatma sırasında performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-212">Using this option slightly reduces code size and improves performance during initialization.</span></span> <span data-ttu-id="273b9-213">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-213">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-214">**TX_DISABLE_STACK_FILLING**</span><span class="sxs-lookup"><span data-stu-id="273b9-214">**TX_DISABLE_STACK_FILLING**</span></span>

<span data-ttu-id="273b9-215">Tanımlandığında, her iş parçacığının yığınının her baytında 0xEF değerini yerleştirmeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="273b9-215">When defined, disables placing the 0xEF value in each byte of each thread's stack when created.</span></span> <span data-ttu-id="273b9-216">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-216">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-217">**TX_ENABLE_EVENT_TRACE**</span><span class="sxs-lookup"><span data-stu-id="273b9-217">**TX_ENABLE_EVENT_TRACE**</span></span>

<span data-ttu-id="273b9-218">Tanımlandığında ThreadX, bir TraceX izleme arabelleği oluşturmak için olay toplama kodu sunar.</span><span class="sxs-lookup"><span data-stu-id="273b9-218">When defined, ThreadX enables the event gathering code for creating a TraceX trace buffer.</span></span>

<span data-ttu-id="273b9-219">**TX_ENABLE_STACK_CHECKING**</span><span class="sxs-lookup"><span data-stu-id="273b9-219">**TX_ENABLE_STACK_CHECKING**</span></span>

<span data-ttu-id="273b9-220">Tanımlandığında,, yığın alanından önce ve sonra ne kadar yığın kullanıldığını ve bu veri deseninin "sınırlarını" incelemesini içeren ThreadX çalışma zamanı yığın denetimini mümkün olur.</span><span class="sxs-lookup"><span data-stu-id="273b9-220">When defined, enables ThreadX run-time stack checking, which includes analysis of how much stack has been used and examination of data pattern "fences" before and after the stack area.</span></span> <span data-ttu-id="273b9-221">Yığın hatası algılanırsa, kayıtlı uygulama yığını hata işleyicisi çağırılır.</span><span class="sxs-lookup"><span data-stu-id="273b9-221">If a stack error is detected, the registered application stack error handler is called.</span></span> <span data-ttu-id="273b9-222">Bu seçenek, biraz daha fazla ek yüke ve kod boyutuna neden olur.</span><span class="sxs-lookup"><span data-stu-id="273b9-222">This option does result in slightly increased overhead and code size.</span></span> <span data-ttu-id="273b9-223">Daha fazla bilgi için ***tx_thread_stack_error_notify*** API işlevini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="273b9-223">Review the ***tx_thread_stack_error_notify*** API function for more information.</span></span> <span data-ttu-id="273b9-224">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-224">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-225">**TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-225">**TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-226">Tanımlandığında, olay bayrakları gruplarında performans bilgilerinin toplanması etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-226">When defined, enables the gathering of performance information on event flags groups.</span></span> <span data-ttu-id="273b9-227">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-227">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-228">**TX_INLINE_THREAD_RESUME_SUSPEND**</span><span class="sxs-lookup"><span data-stu-id="273b9-228">**TX_INLINE_THREAD_RESUME_SUSPEND**</span></span>

<span data-ttu-id="273b9-229">Tanımlandığında, ThreadX, satır içi kod aracılığıyla ***tx_thread_resume** _ ve _ *_tx_thread_suspend_** API çağrılarını geliştirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-229">When defined, ThreadX improves the ***tx_thread_resume** _ and _ *_tx_thread_suspend_** API calls via in-line code.</span></span> <span data-ttu-id="273b9-230">Bu, kod boyutunu artırır ancak bu iki API çağrısının performansını geliştirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-230">This increases code size but enhances performance of these two API calls.</span></span>

<span data-ttu-id="273b9-231">**TX_MAX_PRIORITIES**</span><span class="sxs-lookup"><span data-stu-id="273b9-231">**TX_MAX_PRIORITIES**</span></span>

<span data-ttu-id="273b9-232">ThreadX için öncelik düzeylerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-232">Defines the priority levels for ThreadX.</span></span> <span data-ttu-id="273b9-233">Yasal değerler 32 ile 1024 (dahil) arasındadır ve 32 ile eşit olarak *bölünebilmelidir.*</span><span class="sxs-lookup"><span data-stu-id="273b9-233">Legal values range from 32 through 1024 (inclusive) and *must* be evenly divisible by 32.</span></span> <span data-ttu-id="273b9-234">Desteklenen öncelik düzeyi sayısının artırılması, her 32 öncelikteki RAM kullanımını 128 bayt kadar artırır.</span><span class="sxs-lookup"><span data-stu-id="273b9-234">Increasing the number of priority levels supported increases the RAM usage by 128 bytes for every group of 32 priorities.</span></span> <span data-ttu-id="273b9-235">Ancak, performans üzerinde yalnızca göz ardı edilebilir bir efekt vardır.</span><span class="sxs-lookup"><span data-stu-id="273b9-235">However, there is only a negligible effect on performance.</span></span> <span data-ttu-id="273b9-236">Varsayılan olarak, bu değer 32 öncelik düzeylerine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="273b9-236">By default, this value is set to 32 priority levels.</span></span>

<span data-ttu-id="273b9-237">**TX_MINIMUM_STACK**</span><span class="sxs-lookup"><span data-stu-id="273b9-237">**TX_MINIMUM_STACK**</span></span>

<span data-ttu-id="273b9-238">Minimum yığın boyutunu (bayt cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-238">Defines the minimum stack size (in bytes).</span></span> <span data-ttu-id="273b9-239">İş parçacıklarının oluşturulduğu zaman denetlenirken hata denetimi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="273b9-239">It is used for error checking when threads are created.</span></span> <span data-ttu-id="273b9-240">Varsayılan değer, bağlantı noktasına özeldir ve ***tx_port. h*** içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="273b9-240">The default value is port-specific and is found in ***tx_port.h***.</span></span>

<span data-ttu-id="273b9-241">**TX_MISRA_ENABLE**</span><span class="sxs-lookup"><span data-stu-id="273b9-241">**TX_MISRA_ENABLE**</span></span>

<span data-ttu-id="273b9-242">Tanımlandığında, ThreadX, MISRA C uyumlu kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="273b9-242">When defined, ThreadX utilizes MISRA C compliant conventions.</span></span> <span data-ttu-id="273b9-243">Ayrıntılar için  ***ThreadX_MISRA_Compliance.pdf*** bakın.</span><span class="sxs-lookup"><span data-stu-id="273b9-243">Refer to  ***ThreadX_MISRA_Compliance.pdf*** for details.</span></span>

<span data-ttu-id="273b9-244">**TX_MUTEX_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-244">**TX_MUTEX_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-245">Tanımlandığında, zaman uyumu sağlayıcılar üzerinde performans bilgilerinin toplanması sağlanır.</span><span class="sxs-lookup"><span data-stu-id="273b9-245">When defined, enables the gathering of performance information on mutexes.</span></span> <span data-ttu-id="273b9-246">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-246">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-247">**TX_NO_TIMER**</span><span class="sxs-lookup"><span data-stu-id="273b9-247">**TX_NO_TIMER**</span></span>

<span data-ttu-id="273b9-248">Tanımlandığında, ThreadX Zamanlayıcı mantığı tamamen devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="273b9-248">When defined, the ThreadX timer logic is completely disabled.</span></span> <span data-ttu-id="273b9-249">Bu, ThreadX Zamanlayıcı özelliklerinin (iş parçacığı Sleep, API zaman aşımları, zaman Dilimleme ve uygulama zamanlayıcıları) kullanıldığı durumlarda faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="273b9-249">This is useful in cases where the ThreadX timer features (thread sleep, API timeouts, time-slicing, and application timers) are not utilized.</span></span> <span data-ttu-id="273b9-250">**TX_NO_TIMER** belirtilirse, **TX_TIMER_PROCESS_IN_ISR** seçeneğinin de tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="273b9-250">If **TX_NO_TIMER** is specified, the option **TX_TIMER_PROCESS_IN_ISR** must also be defined.</span></span>

<span data-ttu-id="273b9-251">**TX_NOT_INTERRUPTABLE**</span><span class="sxs-lookup"><span data-stu-id="273b9-251">**TX_NOT_INTERRUPTABLE**</span></span>

<span data-ttu-id="273b9-252">Tanımlandığında, ThreadX kesme kilitleme süresini en aza indirmeye çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="273b9-252">When defined, ThreadX does not attempt to minimize interrupt lockout time.</span></span> <span data-ttu-id="273b9-253">Bu, daha hızlı yürütmeye neden olur, ancak kesme kilitleme süresini biraz artırır.</span><span class="sxs-lookup"><span data-stu-id="273b9-253">This results in faster execution but does slightly increase interrupt lockout time.</span></span>

<span data-ttu-id="273b9-254">**TX_QUEUE_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-254">**TX_QUEUE_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-255">Tanımlandığında, kuyruklarda performans bilgilerinin toplanması etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-255">When defined, enables the gathering of performance information on queues.</span></span> <span data-ttu-id="273b9-256">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-256">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-257">**TX_REACTIVATE_INLINE**</span><span class="sxs-lookup"><span data-stu-id="273b9-257">**TX_REACTIVATE_INLINE**</span></span>

<span data-ttu-id="273b9-258">Tanımlandığında, bir işlev çağrısı kullanmak yerine ThreadX süreölçerinin satır içi yeniden etkinleştirmeyi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="273b9-258">When defined, performs reactivation of ThreadX timers inline instead of using a function call.</span></span> <span data-ttu-id="273b9-259">Bu, performansı artırır ancak kod boyutunu biraz artırır.</span><span class="sxs-lookup"><span data-stu-id="273b9-259">This improves performance but slightly increases code size.</span></span> <span data-ttu-id="273b9-260">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-260">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-261">**TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-261">**TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-262">Tanımlandığında, Semaforlarda performans bilgilerinin toplanması etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-262">When defined, enables the gathering of performance information on semaphores.</span></span> <span data-ttu-id="273b9-263">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-263">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-264">**TX_THREAD_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-264">**TX_THREAD_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-265">Tanımlandığında, iş parçacıklarında performans bilgilerinin toplanması etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-265">When defined, enables the gathering of performance information on threads.</span></span> <span data-ttu-id="273b9-266">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-266">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-267">**TX_TIMER_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="273b9-267">**TX_TIMER_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="273b9-268">Tanımlandığında, zamanlayıcılar üzerinde performans bilgilerini toplamaya izin vermez.</span><span class="sxs-lookup"><span data-stu-id="273b9-268">When defined, enables the gathering of performance information on timers.</span></span> <span data-ttu-id="273b9-269">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-269">By default, this option is not defined.</span></span>

<span data-ttu-id="273b9-270">**TX_TIMER_PROCESS_IN_ISR**</span><span class="sxs-lookup"><span data-stu-id="273b9-270">**TX_TIMER_PROCESS_IN_ISR**</span></span>

<span data-ttu-id="273b9-271">Tanımlandığında, ThreadX için iç sistem süreölçeri iş parçacığını ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="273b9-271">When defined, eliminates the internal system timer thread for ThreadX.</span></span> <span data-ttu-id="273b9-272">Süreölçer yığınına ve denetim bloğuna artık gerek duyulmadığından, bu durum Zamanlayıcı olaylarına ve daha küçük RAM gereksinimlerine göre performansı artırmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="273b9-272">This results in improved performance on timer events and smaller RAM requirements because the timer stack and control block are no longer needed.</span></span> <span data-ttu-id="273b9-273">Ancak, bu seçeneğin kullanılması, tüm Zamanlayıcı süre sonu işlemesini Zamanlayıcı ıSR düzeyine kaydırır.</span><span class="sxs-lookup"><span data-stu-id="273b9-273">However, using this option moves all the timer expiration processing to the timer ISR level.</span></span> <span data-ttu-id="273b9-274">Varsayılan olarak, bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="273b9-274">By default, this option is not defined.</span></span>

> [!NOTE]
> <span data-ttu-id="273b9-275">*Zamanlayıcılardan izin verilen hizmetlere ISRs 'den izin verilmeyebilir, bu nedenle bu seçenek kullanılırken izin verilmiyor olabilir.*</span><span class="sxs-lookup"><span data-stu-id="273b9-275">*Services allowed from timers may not be allowed from ISRs and thus might not be allowed when using this option.*</span></span>

<span data-ttu-id="273b9-276">**TX_TIMER_THREAD_PRIORITY**</span><span class="sxs-lookup"><span data-stu-id="273b9-276">**TX_TIMER_THREAD_PRIORITY**</span></span>

<span data-ttu-id="273b9-277">İç ThreadX sistem Zamanlayıcı iş parçacığının önceliğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-277">Defines the priority of the internal ThreadX system timer thread.</span></span> <span data-ttu-id="273b9-278">Varsayılan değer öncelik 0 ' dır; ThreadX için en yüksek öncelik.</span><span class="sxs-lookup"><span data-stu-id="273b9-278">The default value is priority 0—the highest priority in ThreadX.</span></span> <span data-ttu-id="273b9-279">Varsayılan değer ***tx_port. h*** içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="273b9-279">The default value is defined in ***tx_port.h***.</span></span>

<span data-ttu-id="273b9-280">**TX_TIMER_THREAD_STACK_SIZE**</span><span class="sxs-lookup"><span data-stu-id="273b9-280">**TX_TIMER_THREAD_STACK_SIZE**</span></span>

<span data-ttu-id="273b9-281">İç ThreadX sistem Zamanlayıcı iş parçacığının yığın boyutunu (bayt cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="273b9-281">Defines the stack size (in bytes) of the internal ThreadX system timer thread.</span></span> <span data-ttu-id="273b9-282">Bu iş parçacığı tüm iş parçacığı uyku isteklerinin yanı sıra tüm hizmet çağrı zaman aşımlarını işler.</span><span class="sxs-lookup"><span data-stu-id="273b9-282">This thread processes all thread sleep requests as well as all service call timeouts.</span></span> <span data-ttu-id="273b9-283">Ayrıca, tüm uygulama süreölçeri geri çağırma yordamları bu içerikten çağrılır.</span><span class="sxs-lookup"><span data-stu-id="273b9-283">In addition, all application timer callback routines are invoked from this context.</span></span> <span data-ttu-id="273b9-284">Varsayılan değer, bağlantı noktasına özeldir ve ***tx_port. h*** içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="273b9-284">The default value is port-specific and is found in ***tx_port.h***.</span></span>

## <a name="threadx-version-id"></a><span data-ttu-id="273b9-285">ThreadX sürüm KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="273b9-285">ThreadX Version ID</span></span>

<span data-ttu-id="273b9-286">Programcı, Işparçacığıx sürümünü, \***tx_port. h** _ dosyasının inceağından elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-286">The programmer can obtain the ThreadX version from examination of the \***tx_port.h** _ file.</span></span> <span data-ttu-id="273b9-287">Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir.</span><span class="sxs-lookup"><span data-stu-id="273b9-287">In addition, this file also contains a version history of the corresponding port.</span></span> <span data-ttu-id="273b9-288">Uygulama yazılımı,/_ \* _tx_version_id \* \* genel dizesini inceleyerek ThreadX sürümünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="273b9-288">Application software can obtain the ThreadX version by examining the global string _\*_tx_version_id\*\*.</span></span>
