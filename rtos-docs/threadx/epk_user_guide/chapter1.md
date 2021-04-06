---
title: Bölüm 1-yürütme profili kiti 'ne giriş
description: Bu bölümde, Azure RTOS ThreadX Execution profile Kit 'e (EPK) giriş yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d30676437535229ad5bdbca10dcc9ca009d6e74
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377652"
---
# <a name="chapter-1--introduction-to-the-execution-profile-kit"></a><span data-ttu-id="35235-103">Bölüm 1 yürütme profili setini giriş</span><span class="sxs-lookup"><span data-stu-id="35235-103">Chapter 1  Introduction to the Execution Profile Kit</span></span>

<span data-ttu-id="35235-104">ThreadX Execution profile Kit (EPK), uygulamaların iş parçacıkları, kesme hizmeti yordamları (ISRS) ve boşta sistem koşulları için yürütme zamanını dinamik olarak izlemelerine yönelik bir altyapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="35235-104">The ThreadX Execution Profile Kit (EPK) provides an infrastructure for applications to dynamically track execution time for threads, Interrupt Service Routines (ISRs), and idle system conditions.</span></span> <span data-ttu-id="35235-105">Bu, özellikle iyileştirme ve en yüksek performans için uygulamayı ayarlama açısından kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="35235-105">This is especially useful for optimization and tuning the application for maximum performance.</span></span> <span data-ttu-id="35235-106">Ancak, aynı zamanda önemli bir hata ayıklama yardımıdır.</span><span class="sxs-lookup"><span data-stu-id="35235-106">However, it is also a valuable debug aid.</span></span>

<span data-ttu-id="35235-107">EPK, \" \" iş parçacığı girişi, iş parçacığı ÇıKıŞı, ISR GIRIŞI ve ISR çıkış üzerinde çağrılan derleme kodundaki threadx zamanlama mantığıyla yerleşik kancaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="35235-107">The EPK relies on \"hooks\" built into the ThreadX scheduling logic in assembly code that are called on thread entry, thread exit, ISR entry, and ISR exit.</span></span> <span data-ttu-id="35235-108">EPK yordamları, bu tür olaylar arasındaki süreyi hesaplar ve değişim süresini genel değişkenlerde ve **TX_THREAD** denetim bloğunun üyelerini de depolar.</span><span class="sxs-lookup"><span data-stu-id="35235-108">The EPK routines calculate the time in between such events and store the delta time in global variables as well as members of the **TX_THREAD** control block.</span></span>

> [!NOTE]
> <span data-ttu-id="35235-109">*Geliştirici, çalışan bir ThreadX uygulamasına donanım görünürlüğü sağlamak için g/ç PIN 'lerini değiştirmek için bu kanca işlevlerini kendi mantığıyla değiştirebilir ve hatta* değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="35235-109">*The developer is free to modify or even replace these hook functions with their own logic to toggle I/O pins in order to provide hardware visibility to a running ThreadX application*.</span></span>

## 

## <a name="epk-requirements"></a><span data-ttu-id="35235-110">EPK gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="35235-110">EPK Requirements</span></span>

<span data-ttu-id="35235-111">EPK, çalışması için ThreadX 6,0 (veya üzeri) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="35235-111">The EPK requires ThreadX 6.0 (or above) in order to operate.</span></span> <span data-ttu-id="35235-112">EPK Ayrıca \" \" , donanım saat kaynağını arttırmadan makul bir çözüm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="35235-112">The EPK also requires a \"reasonable\" resolution, incrementing hardware time source.</span></span> <span data-ttu-id="35235-113">En makul çözüm, genellikle mikro ikinci ölçekte bir şey olur.</span><span class="sxs-lookup"><span data-stu-id="35235-113">The most reasonable resolution would typically be something on a microsecond scale.</span></span> <span data-ttu-id="35235-114">Çözüm çok harika olursa EPK sayaçları çok hızlı bir şekilde en fazla olur.</span><span class="sxs-lookup"><span data-stu-id="35235-114">If the resolution is too great, the EPK counters will max out too quickly.</span></span> <span data-ttu-id="35235-115">Buna karşılık, çözüm çok küçükse doğru zamanlama mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="35235-115">Conversely, if the resolution is too small, accurate timing is not possible.</span></span> <span data-ttu-id="35235-116">Uygulama zaman kaynağı, \***tx_execution_profile. h** _ ' de _ \* TX_EXECUTION_TIME_SOURCE \* \* makrosu tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="35235-116">The application time source is defined in ***tx_execution_profile.h** _ by the macro _*TX_EXECUTION_TIME_SOURCE\*\*.</span></span>

<span data-ttu-id="35235-117">C derleyicisi, \" \" imzasız 64 bitlik toplam sayaç için imzasız uzun uzun bir tür içermelidir.</span><span class="sxs-lookup"><span data-stu-id="35235-117">The C compiler must support the type \"unsigned long long\" for unsigned 64-bit total counters.</span></span> <span data-ttu-id="35235-118">Ayrıca, EPK genel değişkenlerin derleyicinin çalışma zamanı başlangıç kodu tarafından başlatıldığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="35235-118">Furthermore, the EPK assumes the global variables are initialized by the compiler run-time startup code.</span></span> <span data-ttu-id="35235-119">Böyle bir durum yoksa, ***tx_execution_profile. c*** ' de tanımlanan genel değişkenlerin uygulama tarafından 0 olarak başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="35235-119">If this is not the case, the global variables defined in ***tx_execution_profile.c*** must be initialized to 0 by the application.</span></span>

## <a name="epk-installation"></a><span data-ttu-id="35235-120">EPK yüklemesi</span><span class="sxs-lookup"><span data-stu-id="35235-120">EPK Installation</span></span>

<span data-ttu-id="35235-121">ThreadX EPK 'yi yüklemek için aşağıdaki adımları izleyin ve tüm ThreadX kitaplığını ve uygulamasını yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="35235-121">To install the ThreadX EPK, follow the steps below and rebuild the entire ThreadX library and application.</span></span>

1. <span data-ttu-id="35235-122">ThreadX kitaplığı derleme projenize EPK kaynak dosyalarını (***tx_execution_profile. h** _ ve _*_tx_execution_profile. c_\*_) dahil edin.</span><span class="sxs-lookup"><span data-stu-id="35235-122">Include the EPK source files (***tx_execution_profile.h** _ and _*_tx_execution_profile.c_\*_) in your ThreadX library build project.</span></span> <span data-ttu-id="35235-123">Bu dosyalar, _ *_yardımcı programı/Execution_Profile_*\* klasörü altındaki [Azure RTOS threadx deposu](<https://github.com/azure-rtos/threadx>) içinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="35235-123">These files can be in the [Azure RTOS ThreadX repo](<https://github.com/azure-rtos/threadx>) under the _ *_utility/Execution_Profile_*\* folder).</span></span>

1. <span data-ttu-id="35235-124">***Tx_port. h** _ ' de _ *TX_THREAD_EXTENSION_3** makrosunu aşağıdaki gibi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="35235-124">In ***tx_port.h** _, define the _ *TX_THREAD_EXTENSION_3** macro as follows.</span></span>
```
    #define TX_THREAD_EXTENSION_3 unsigned long long tx_thread_execution_time_total; \
    unsigned long tx_thread_execution_time_last_start;
```

3. <span data-ttu-id="35235-125">Donanım zaman kaynağınıza eşlemek için **_tx_execution_profile. h_** içinde **TX_EXECUTION_TIME_SOURCE** makrosunu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="35235-125">Define the **TX_EXECUTION_TIME_SOURCE** macro in **_tx_execution_profile.h_** to map to your hardware time source.</span></span>

1. <span data-ttu-id="35235-126">Zamanlama kancalarının ThreadX derleme kodundan çağrılması için derleme ortamının **TX_ENABLE_EXECUTION_CHANGE_NOTIFY** tanımladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="35235-126">Ensure that the build environment defines **TX_ENABLE_EXECUTION_CHANGE_NOTIFY** so that the scheduling hooks are called from the ThreadX assembly code.</span></span>

1. <span data-ttu-id="35235-127">64 bit zaman kaynağını kullanmak istiyorsanız, bunun nasıl yapılacağını gösteren yönergeler için lütfen ***tx_execution_profile. h*** dosyasını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="35235-127">If you wish to use 64-bit time source, please review the ***tx_execution_profile.h*** file for instructions on how to accomplish this.</span></span>

1. <span data-ttu-id="35235-128">Tüm bu seçeneklerin düzgün derlenmesi için tüm kitaplık ve uygulamayı yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="35235-128">Rebuild the entire library and application so that all of these options are properly compiled-in.</span></span>

<span data-ttu-id="35235-129">Artık, uygulamanızla EPK kullanmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="35235-129">You are now ready to use EPK with your application.</span></span>

##  <a name="epk-example"></a><span data-ttu-id="35235-130">EPK örneği</span><span class="sxs-lookup"><span data-stu-id="35235-130">EPK Example</span></span> 

<span data-ttu-id="35235-131">Aşağıda, mikro saniye başına 7,2 kez artan 32 bitlik bir Zamanlayıcı kaynağıyla yapılandırılmış standart bir ThreadX tanıtımı üzerinde kullanılan EPK örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="35235-131">The following is an example of EPK being used on a standard ThreadX demonstration, configured with a 32-bit timer source that increments 7.2 times per microsecond.</span></span> 

<span data-ttu-id="35235-132">**TX_EXECUTION_TIME_SOURCE** makro, 0xE0001004 ' te bellek eşlemeli Zamanlayıcı kaydını aşağıda gösterildiği gibi almak için tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="35235-132">The **TX_EXECUTION_TIME_SOURCE** macro is defined to pick up the memory-mapped timer register at 0xE0001004, as follows.</span></span>
```
(EXECUTION_TIME_SOURCE_TYPE) \*((ULONG \*) 0xE0001004)
```

<span data-ttu-id="35235-133">Tanıtım çalıştırmasının beş saniye boyunca çalışmasına izin vermek aşağıdaki sonuçları verir.</span><span class="sxs-lookup"><span data-stu-id="35235-133">Letting the demonstration run for five seconds yields the following results.</span></span>

![Tanıtım çalışmasına izin veren sonuçlar.](media/demo_results.png)

<span data-ttu-id="35235-135">Standart ThreadX tanıtımda boşta kalma süresi olmadığından (iş parçacıkları 1 ve 2 sürekli olarak çalıştırılır), EPK boşta kalma süresi için sıfır değerini doğru şekilde bildirir.</span><span class="sxs-lookup"><span data-stu-id="35235-135">Since the standard ThreadX demonstration has no idle time (threads 1 and 2 run continuously), the EPK correctly reports zero for idle time.</span></span> <span data-ttu-id="35235-136">Her yürütme kategorisinin mikrosaniye değerini türetmek için ıSR toplam süre ve iş parçacığı değerleri 7,2 ile ayrılabilir.</span><span class="sxs-lookup"><span data-stu-id="35235-136">The ISR total time and thread values may be divided by 7.2 in order to derive the microseconds for each execution category.</span></span> <span data-ttu-id="35235-137">EPK Ayrıca bu bilgilere erişmek için API 'Ler sağlar (lütfen bkz. [Bölüm 2](chapter2.md)).</span><span class="sxs-lookup"><span data-stu-id="35235-137">The EPK also provides APIs to access this information (please see please see [Chapter 2](chapter2.md)).</span></span>