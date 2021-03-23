---
title: Bölüm 5-Azure RTOS ThreadX SMP için cihaz sürücüleri
description: Bu bölümde, Azure RTOS ThreadX SMP için cihaz sürücülerinin bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: acfb54a25cc8bc27b7d0aaeff48956529d90c9e1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828018"
---
# <a name="chapter-5---device-drivers-for-azure-rtos-threadx-smp"></a><span data-ttu-id="54358-103">Bölüm 5-Azure RTOS ThreadX SMP için cihaz sürücüleri</span><span class="sxs-lookup"><span data-stu-id="54358-103">Chapter 5 - Device Drivers for Azure RTOS ThreadX SMP</span></span>

<span data-ttu-id="54358-104">Bu bölümde, Azure RTOS ThreadX SMP için cihaz sürücülerinin bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="54358-104">This chapter contains a description of device drivers for Azure RTOS ThreadX SMP.</span></span> <span data-ttu-id="54358-105">Bu bölümde sunulan bilgiler, geliştiricilerin uygulamaya özgü sürücüleri yazmasına yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="54358-105">The information presented in this chapter is designed to help developers write application specific drivers.</span></span> 

## <a name="device-driver-introduction"></a><span data-ttu-id="54358-106">Cihaz sürücüsü giriş</span><span class="sxs-lookup"><span data-stu-id="54358-106">Device Driver Introduction</span></span>

<span data-ttu-id="54358-107">Dış ortamla iletişim, çoğu katıştırılmış uygulamanın önemli bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="54358-107">Communication with the external environment is an important component of most embedded applications.</span></span> <span data-ttu-id="54358-108">Bu iletişim, katıştırılmış uygulama yazılımının erişebileceği donanım cihazları aracılığıyla gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="54358-108">This communication is accomplished through hardware devices that are accessible to the embedded application software.</span></span> <span data-ttu-id="54358-109">Bu cihazları yönetmeden sorumlu yazılım bileşenleri genellikle *cihaz sürücüleri* olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="54358-109">The software components responsible for managing such devices are commonly called *Device Drivers*.</span></span>

<span data-ttu-id="54358-110">Katıştırılmış ve gerçek zamanlı sistemlerdeki cihaz sürücüleri, doğal olarak uygulamaya bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="54358-110">Device drivers in embedded, real-time systems are inherently application dependent.</span></span> <span data-ttu-id="54358-111">Bu iki asıl nedenden dolayı geçerlidir: hedef donanımın büyük ölçüde çeşitliliğe ve gerçek zamanlı uygulamalara uygulanan eşit oranda performans gereksinimleridir.</span><span class="sxs-lookup"><span data-stu-id="54358-111">This is true for two principal reasons: the vast diversity of target hardware and the equally vast performance requirements imposed on real-time applications.</span></span> <span data-ttu-id="54358-112">Bu nedenle, her uygulamanın gereksinimlerini karşılayacak ortak bir sürücü kümesi sağlanması neredeyse imkansızdır.</span><span class="sxs-lookup"><span data-stu-id="54358-112">Because of this, it is virtually impossible to provide a common set of drivers that will meet the requirements of every application.</span></span> <span data-ttu-id="54358-113">Bu nedenlerden dolayı, bu bölümdeki bilgiler, kullanıcıların *raf dışı* THREADX SMP cihaz sürücülerini özelleştirmesini ve kendi belirli sürücülerini yazmasını sağlamak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="54358-113">For these reasons, the information in this chapter is designed to help users customize *off-the-shelf* ThreadX SMP device drivers and write their own specific drivers.</span></span>

## <a name="driver-functions"></a><span data-ttu-id="54358-114">Sürücü Işlevleri</span><span class="sxs-lookup"><span data-stu-id="54358-114">Driver Functions</span></span>

<span data-ttu-id="54358-115">ThreadX SMP cihaz sürücüleri, aşağıdaki gibi sekiz temel işlevsel alandan oluşur:</span><span class="sxs-lookup"><span data-stu-id="54358-115">ThreadX SMP device drivers are composed of eight basic functional areas, as follows:</span></span>

- <span data-ttu-id="54358-116">**Sürücü başlatma**</span><span class="sxs-lookup"><span data-stu-id="54358-116">**Driver Initialization**</span></span>
- <span data-ttu-id="54358-117">**Sürücü denetimi**</span><span class="sxs-lookup"><span data-stu-id="54358-117">**Driver Control**</span></span>
- <span data-ttu-id="54358-118">**Sürücü erişimi**</span><span class="sxs-lookup"><span data-stu-id="54358-118">**Driver Access**</span></span>
- <span data-ttu-id="54358-119">**Sürücü girişi**</span><span class="sxs-lookup"><span data-stu-id="54358-119">**Driver Input**</span></span>
- <span data-ttu-id="54358-120">**Sürücü çıkışı**</span><span class="sxs-lookup"><span data-stu-id="54358-120">**Driver Output**</span></span>
- <span data-ttu-id="54358-121">**Sürücü kesintileri**</span><span class="sxs-lookup"><span data-stu-id="54358-121">**Driver Interrupts**</span></span>
- <span data-ttu-id="54358-122">**Sürücü durumu**</span><span class="sxs-lookup"><span data-stu-id="54358-122">**Driver Status**</span></span>
- <span data-ttu-id="54358-123">**Sürücü sonlandırma**</span><span class="sxs-lookup"><span data-stu-id="54358-123">**Driver Termination**</span></span>

<span data-ttu-id="54358-124">Başlatma dışında, her sürücü işlevsel alanı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="54358-124">With the exception of initialization, each driver functional area is optional.</span></span> <span data-ttu-id="54358-125">Ayrıca, her bir alandaki tam işleme cihaz sürücüsüne özeldir.</span><span class="sxs-lookup"><span data-stu-id="54358-125">Furthermore, the exact processing in each area is specific to the device driver.</span></span>

### <a name="driver-initialization"></a><span data-ttu-id="54358-126">Sürücü başlatma</span><span class="sxs-lookup"><span data-stu-id="54358-126">Driver Initialization</span></span> 
<span data-ttu-id="54358-127">Bu işlevsel alan, gerçek donanım cihazının ve sürücünün iç veri yapılarının başlatılmasından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="54358-127">This functional area is responsible for initialization of the actual hardware device and the internal data structures of the driver.</span></span> <span data-ttu-id="54358-128">Başlatma tamamlanana kadar diğer sürücü hizmetlerini çağırmaya izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="54358-128">Calling other driver services is not allowed until initialization is complete.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54358-129">Sürücünün başlatma işlevi bileşeni genellikle **tx_application_define** işlevden veya bir başlatma iş parçacığından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="54358-129">The driver’s initialization function component is typically called from the **tx_application_define** function or from an initialization thread.</span></span>

### <a name="driver-control"></a><span data-ttu-id="54358-130">Sürücü denetimi</span><span class="sxs-lookup"><span data-stu-id="54358-130">Driver Control</span></span> 
<span data-ttu-id="54358-131">Sürücü başlatıldıktan ve işleme hazırladıktan sonra, bu işlevsel alan çalışma zamanı denetiminden sorumludur.</span><span class="sxs-lookup"><span data-stu-id="54358-131">After the driver is initialized and ready for operation, this functional area is responsible for run-time control.</span></span> <span data-ttu-id="54358-132">Genellikle, çalışma zamanı denetimi, temel alınan donanım cihazında değişiklik yapmaktan oluşur.</span><span class="sxs-lookup"><span data-stu-id="54358-132">Typically, run-time control consists of making changes to the underlying hardware device.</span></span> <span data-ttu-id="54358-133">Örnek olarak, bir seri cihazın baud hızını değiştirme veya bir diskte yeni bir kesim arama sayılabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-133">Examples include changing the baud rate of a serial device or seeking a new sector on a disk.</span></span>

### <a name="driver-access"></a><span data-ttu-id="54358-134">Sürücü erişimi</span><span class="sxs-lookup"><span data-stu-id="54358-134">Driver Access</span></span> 
<span data-ttu-id="54358-135">Bazı cihaz sürücüleri yalnızca tek bir uygulama iş parçacığından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="54358-135">Some device drivers are called only from a single application thread.</span></span> <span data-ttu-id="54358-136">Böyle durumlarda, bu işlevsel alan gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="54358-136">In such cases, this functional area is not needed.</span></span> <span data-ttu-id="54358-137">Ancak, birden çok iş parçacığının eşzamanlı sürücü erişimine ihtiyacı olan uygulamalarda, cihaz sürücüsüne atama/sürüm tesislerini ekleyerek etkileşiminin denetlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="54358-137">However, in applications where multiple threads need simultaneous driver access, their interaction must be controlled by adding assign/ release facilities in the device driver.</span></span> <span data-ttu-id="54358-138">Alternatif olarak, uygulama sürücü erişimini denetlemek ve sürücü içinde ek yüke ve karmaşıkmaya engel olmak için bir semafor kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-138">Alternatively, the application may use a semaphore to control driver access and avoid extra overhead and complication inside the driver.</span></span> 

### <a name="driver-input"></a><span data-ttu-id="54358-139">Sürücü girişi</span><span class="sxs-lookup"><span data-stu-id="54358-139">Driver Input</span></span> 
<span data-ttu-id="54358-140">Bu işlevsel alan tüm cihaz girişinden sorumludur.</span><span class="sxs-lookup"><span data-stu-id="54358-140">This functional area is responsible for all device input.</span></span> <span data-ttu-id="54358-141">Sürücü girişiyle ilişkili asıl sorunlar genellikle girişin nasıl arabelleğe alınacağını ve iş parçacıklarının böyle bir girişi nasıl bekleyeceğini kapsar.</span><span class="sxs-lookup"><span data-stu-id="54358-141">The principal issues associated with driver input usually involve how the input is buffered and how threads wait for such input.</span></span> 

### <a name="driver-output"></a><span data-ttu-id="54358-142">Sürücü çıkışı</span><span class="sxs-lookup"><span data-stu-id="54358-142">Driver Output</span></span> 
<span data-ttu-id="54358-143">Bu işlevsel alan tüm cihaz çıktıından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="54358-143">This functional area is responsible for all device output.</span></span> <span data-ttu-id="54358-144">Sürücü çıkışıyla ilişkili asıl sorunlar genellikle çıktının nasıl arabelleğe alınacağını ve iş parçacıklarının çıktıyı gerçekleştirmeyi nasıl bekleyeceğini kapsar.</span><span class="sxs-lookup"><span data-stu-id="54358-144">The principal issues associated with driver output usually involve how the output is buffered and how threads wait to perform output.</span></span> 

### <a name="driver-interrupts"></a><span data-ttu-id="54358-145">Sürücü kesintileri</span><span class="sxs-lookup"><span data-stu-id="54358-145">Driver Interrupts</span></span> 
<span data-ttu-id="54358-146">Birçok gerçek zamanlı sistem, cihaz girişi, çıkış, denetim ve hata olaylarının sürücüsünü bilgilendirmek için donanım kesmelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="54358-146">Most real-time systems rely on hardware interrupts to notify the driver of device input, output, control, and error events.</span></span> <span data-ttu-id="54358-147">Kesmeler, bu tür dış olaylara garantili bir yanıt süresi sağlar.</span><span class="sxs-lookup"><span data-stu-id="54358-147">Interrupts provide a guaranteed response time to such external events.</span></span> <span data-ttu-id="54358-148">Kesmeler yerine, sürücü yazılımı bu tür olaylar için düzenli olarak dış donanımı denetleyebilir.</span><span class="sxs-lookup"><span data-stu-id="54358-148">Instead of interrupts, the driver software may periodically check the external hardware for such events.</span></span> <span data-ttu-id="54358-149">Bu teknik *yoklama* olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="54358-149">This technique is called *polling*.</span></span> <span data-ttu-id="54358-150">Kesmelerden daha az gerçek zamanlı, ancak yoklama bazı daha az gerçek zamanlı uygulamalar açısından anlamlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-150">It is less real-time than interrupts, but polling may make sense for some less real-time applications.</span></span> 

### <a name="driver-status"></a><span data-ttu-id="54358-151">Sürücü durumu</span><span class="sxs-lookup"><span data-stu-id="54358-151">Driver Status</span></span> 
<span data-ttu-id="54358-152">Bu işlev alanı, sürücü işlemiyle ilişkili çalışma zamanı durumu ve istatistiklerini sağlamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="54358-152">This function area is responsible for providing runtime status and statistics associated with the driver operation.</span></span> <span data-ttu-id="54358-153">Bu işlev alanı tarafından yönetilen bilgiler genellikle aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="54358-153">Information managed by this function area typically includes the following:</span></span> 
- <span data-ttu-id="54358-154">Geçerli cihaz durumu</span><span class="sxs-lookup"><span data-stu-id="54358-154">Current device status</span></span>
- <span data-ttu-id="54358-155">Giriş baytları</span><span class="sxs-lookup"><span data-stu-id="54358-155">Input bytes</span></span>
- <span data-ttu-id="54358-156">Çıkış baytları</span><span class="sxs-lookup"><span data-stu-id="54358-156">Output bytes</span></span>
- <span data-ttu-id="54358-157">Cihaz hata sayıları</span><span class="sxs-lookup"><span data-stu-id="54358-157">Device error counts</span></span>

### <a name="driver-termination"></a><span data-ttu-id="54358-158">Sürücü sonlandırma</span><span class="sxs-lookup"><span data-stu-id="54358-158">Driver Termination</span></span> 
<span data-ttu-id="54358-159">Bu işlevsel alan isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="54358-159">This functional area is optional.</span></span> <span data-ttu-id="54358-160">Yalnızca sürücü ve/veya fiziksel donanım cihazının kapatılması gerekiyorsa gereklidir.</span><span class="sxs-lookup"><span data-stu-id="54358-160">It is only required if the driver and/or the physical hardware device need to be shut down.</span></span> <span data-ttu-id="54358-161">Sonlandırıldıktan sonra, yeniden başlatılana kadar sürücünün yeniden çağrılmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54358-161">After being terminated, the driver must not be called again until it is re-initialized.</span></span> 

## <a name="simple-driver-example"></a><span data-ttu-id="54358-162">Basit sürücü örneği</span><span class="sxs-lookup"><span data-stu-id="54358-162">Simple Driver Example</span></span>

<span data-ttu-id="54358-163">Bir aygıt sürücüsünü tanımlamanın en iyi yolu bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="54358-163">An example is the best way to describe a device driver.</span></span> <span data-ttu-id="54358-164">Bu örnekte, sürücü bir yapılandırma kaydı, bir giriş kaydı ve bir çıkış kaydı ile basit bir seri donanım cihazı olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="54358-164">In this example, the driver assumes a simple serial hardware device with a configuration register, an input register, and an output register.</span></span> <span data-ttu-id="54358-165">Bu basit sürücü örneği, başlatma, giriş, çıkış ve kesme işlevsel bölgelerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="54358-165">This simple driver example illustrates the initialization, input, output, and interrupt functional areas.</span></span>

### <a name="simple-driver-initialization"></a><span data-ttu-id="54358-166">Basit sürücü başlatma</span><span class="sxs-lookup"><span data-stu-id="54358-166">Simple Driver Initialization</span></span> 
<span data-ttu-id="54358-167">Basit sürücünün ***tx_sdriver_initialize*** işlevi, sürücünün giriş ve çıkış işlemini yönetmek için kullanılan iki sayım semaforu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54358-167">The ***tx_sdriver_initialize*** function of the simple driver creates two counting semaphores that are used to manage the driver’s input and output operation.</span></span> <span data-ttu-id="54358-168">Giriş semaforu, seri donanım aygıtı tarafından bir karakter alındığında giriş ıSR tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="54358-168">The input semaphore is set by the input ISR when a character is received by the serial hardware device.</span></span> <span data-ttu-id="54358-169">Bu nedenle, giriş semaforu ilk sıfır sayısı ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="54358-169">Because of this, the input semaphore is created with an initial count of zero.</span></span>

<span data-ttu-id="54358-170">Buna karşılık, çıkış semaforu seri donanım iletme kaydının kullanılabilirliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="54358-170">Conversely, the output semaphore indicates the availability of the serial hardware transmit register.</span></span> <span data-ttu-id="54358-171">İlk olarak, iletme kaydının kullanılabilir olduğunu göstermek için bir değeriyle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="54358-171">It is created with a value of one to indicate the transmit register is initially available.</span></span>

<span data-ttu-id="54358-172">Başlatma işlevi, giriş ve çıkış bildirimleri için düşük düzeyli kesme vektör işleyicilerini yüklemeden de sorumludur.</span><span class="sxs-lookup"><span data-stu-id="54358-172">The initialization function is also responsible for installing the low-level interrupt vector handlers for input and output notifications.</span></span> <span data-ttu-id="54358-173">Diğer ThreadX SMP kesme hizmeti yordamları gibi, düşük düzey işleyicinin basit sürücü ıSR 'yi çağırmadan önce \***_tx_thread_context_save** _ ' i çağırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54358-173">Like other ThreadX SMP interrupt service routines, the low-level handler must call \***_tx_thread_context_save** _ before calling the simple driver ISR.</span></span> <span data-ttu-id="54358-174">Sürücü ıSR çağrıldıktan sonra, alt düzey işleyicinin _ \* _ _tx_thread_context_restore_\* \* çağrısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="54358-174">After the driver ISR returns, the low-level handler must call _\*_ _tx_thread_context_restore_\*\*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54358-175">Başlatmanın diğer sürücü işlevlerinden herhangi birinin önüne çağrılması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="54358-175">It is important that initialization is called before any of the other driver functions.</span></span> <span data-ttu-id="54358-176">Genellikle, **tx_application_define**'tan sürücü başlatma çağrılır.</span><span class="sxs-lookup"><span data-stu-id="54358-176">Typically, driver initialization is called from **tx_application_define**.</span></span>

<span data-ttu-id="54358-177">Basit sürücünün başlatma kaynak kodu için sayfa 306 ' de Şekil 9 ' a bakın.</span><span class="sxs-lookup"><span data-stu-id="54358-177">See Figure 9 on page 306 for the initialization source code of the simple driver.</span></span>

```C
VOID     tx_sdriver_initialize(VOID)
{

    /* Initialize the two counting semaphores used to control
       the simple driver I/O. */
    tx_semaphore_create(&tx_sdriver_input_semaphore,
                       "simple driver input semaphore", 0);
    tx_semaphore_create(&tx_sdriver_output_semaphore,
                       "simple driver output semaphore", 1);

    /* Setup interrupt vectors for input and output ISRs.
       The initial vector handling should call the ISRs
       defined in this file. */

    /* Configure serial device hardware for RX/TX interrupt
       generation, baud rate, stop bits, etc. */
}
```
<span data-ttu-id="54358-178">**ŞEKIL 9. Basit sürücü başlatma**</span><span class="sxs-lookup"><span data-stu-id="54358-178">**FIGURE 9. Simple Driver Initialization**</span></span>

### <a name="simple-driver-input"></a><span data-ttu-id="54358-179">Basit sürücü girişi</span><span class="sxs-lookup"><span data-stu-id="54358-179">Simple Driver Input</span></span> 
<span data-ttu-id="54358-180">Giriş semaforu etrafında basit sürücü merkezlerinin girişi.</span><span class="sxs-lookup"><span data-stu-id="54358-180">Input for the simple driver centers around the input semaphore.</span></span> <span data-ttu-id="54358-181">Bir seri cihaz giriş kesmesi alındığında, giriş semaforu ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="54358-181">When a serial device input interrupt is received, the input semaphore is set.</span></span> <span data-ttu-id="54358-182">Bir veya daha fazla iş parçacığı sürücüden bir karakter bekliyorsa, en uzun bekleme olan iş parçacığı sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="54358-182">If one or more threads are waiting for a character from the driver, the thread waiting the longest is resumed.</span></span> <span data-ttu-id="54358-183">Bekleyen bir iş parçacığı yoksa semafor, bir iş parçacığı sürücü giriş işlevini çağırana kadar ayarlanmış olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="54358-183">If no threads are waiting, the semaphore simply remains set until a thread calls the drive input function.</span></span>

<span data-ttu-id="54358-184">Basit sürücü girişi işleme için çeşitli sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="54358-184">There are several limitations to the simple driver input handling.</span></span> <span data-ttu-id="54358-185">Giriş karakterlerinin düşürülme olasılığı en önemlidir.</span><span class="sxs-lookup"><span data-stu-id="54358-185">The most significant is the potential for dropping input characters.</span></span> <span data-ttu-id="54358-186">Bu, önceki karakter işlenmeden önce gelen giriş karakterlerini arabelleğe alma özelliği olmadığı için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="54358-186">This is possible because there is no ability to buffer input characters that arrive before the previous character is processed.</span></span> <span data-ttu-id="54358-187">Bu, giriş karakter arabelleği eklenerek kolayca işlenir.</span><span class="sxs-lookup"><span data-stu-id="54358-187">This is easily handled by adding an input character buffer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54358-188">Yalnızca iş parçacıklarının **tx_sdriver_input** işlevini çağırması izin verilir.</span><span class="sxs-lookup"><span data-stu-id="54358-188">Only threads are allowed to call the **tx_sdriver_input** function.</span></span>

<span data-ttu-id="54358-189">Şekil 10 ' da basit sürücü girişiyle ilişkili kaynak kodu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="54358-189">Figure 10 shows the source code associated with simple driver input.</span></span>

```C
UCHAR     tx_sdriver_input(VOID)
{

    /* Determine if there is a character waiting. If not,
        suspend. */
    tx_semaphore_get(&tx_sdriver_input_semaphore,
                                             TX_WAIT_FOREVER;
    /* Return character from serial RX hardware register. */
    return(*serial_hardware_input_ptr);
}

VOID     tx_sdriver_input_ISR(VOID)
{
    /* See if an input character notification is pending. */
    if (!tx_sdriver_input_semaphore.tx_semaphore_count)
    {
        /* If not, notify thread of an input character. */
        tx_semaphore_put(&tx_sdriver_input_semaphore);
    }
}
```
<span data-ttu-id="54358-190">**ŞEKIL 10. Basit sürücü girişi**</span><span class="sxs-lookup"><span data-stu-id="54358-190">**FIGURE 10. Simple Driver Input**</span></span>

### <a name="simple-driver-output"></a><span data-ttu-id="54358-191">Basit sürücü çıktısı</span><span class="sxs-lookup"><span data-stu-id="54358-191">Simple Driver Output</span></span> 
<span data-ttu-id="54358-192">Çıktı işleme, seri cihazın aktarım kaydı ücretsizdir sinyali almak için çıkış semaforu kullanır.</span><span class="sxs-lookup"><span data-stu-id="54358-192">Output processing utilizes the output semaphore to signal when the serial device’s transmit register is free.</span></span> <span data-ttu-id="54358-193">Çıkış karakteri cihaza gerçekten yazılmadan önce, çıkış semaforu alınır.</span><span class="sxs-lookup"><span data-stu-id="54358-193">Before an output character is actually written to the device, the output semaphore is obtained.</span></span> <span data-ttu-id="54358-194">Mevcut değilse, önceki iletim henüz tamamlanmaz.</span><span class="sxs-lookup"><span data-stu-id="54358-194">If it is not available, the previous transmit is not yet complete.</span></span>

<span data-ttu-id="54358-195">Çıkış ıSR, iletim tamamlanma kesmesini işlemekten sorumludur.</span><span class="sxs-lookup"><span data-stu-id="54358-195">The output ISR is responsible for handling the transmit complete interrupt.</span></span> <span data-ttu-id="54358-196">Çıkış semaforu ayarlamak için çıkış ıSR miktarları işleme, böylece başka bir karakterin çıkışına izin veriliyor.</span><span class="sxs-lookup"><span data-stu-id="54358-196">Processing of the output ISR amounts to setting the output semaphore, thereby allowing output of another character.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54358-197">Yalnızca iş parçacıklarının **tx_sdriver_output** işlevini çağırması izin verilir.</span><span class="sxs-lookup"><span data-stu-id="54358-197">Only threads are allowed to call the **tx_sdriver_output** function.</span></span>

<span data-ttu-id="54358-198">Şekil 11 ' de, basit sürücü çıkışıyla ilişkili kaynak kodu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="54358-198">Figure 11 shows the source code associated with simple driver output.</span></span>

```C
VOID     tx_sdriver_output(UCHAR alpha)
{

    /* Determine if the hardware is ready to transmit a
       character. If not, suspend until the previous output
        completes. */
    tx_semaphore_get(&tx_sdriver_output_semaphore,
                                            TX_WAIT_FOREVER);
    /* Send the character through the hardware. */
    *serial_hardware_output_ptr = alpha;
}

VOID     tx_sdriver_output_ISR(VOID)
{
    /* Notify thread last character transmit is
        complete. */
    tx_semaphore_put(&tx_sdriver_output_semaphore);
}
```
<span data-ttu-id="54358-199">**ŞEKIL 11. Basit sürücü çıktısı**</span><span class="sxs-lookup"><span data-stu-id="54358-199">**FIGURE 11. Simple Driver Output**</span></span>

### <a name="simple-driver-shortcomings"></a><span data-ttu-id="54358-200">Basit sürücü eksikler</span><span class="sxs-lookup"><span data-stu-id="54358-200">Simple Driver Shortcomings</span></span> 
<span data-ttu-id="54358-201">Bu basit cihaz sürücüsü örneği, bir ThreadX SMP cihaz sürücüsünün temel fikrini gösterir.</span><span class="sxs-lookup"><span data-stu-id="54358-201">This simple device driver example illustrates the basic idea of a ThreadX SMP device driver.</span></span> <span data-ttu-id="54358-202">Ancak, basit cihaz sürücüsü veri arabelleğe alma veya herhangi bir ek yük sorununu gidermez, ancak gerçek dünyada ThreadX SMP sürücülerini tam olarak göstermez.</span><span class="sxs-lookup"><span data-stu-id="54358-202">However, because the simple device driver does not address data buffering or any overhead issues, it does not fully represent real-world ThreadX SMP drivers.</span></span> <span data-ttu-id="54358-203">Aşağıdaki bölümde, cihaz sürücüleriyle ilişkili daha gelişmiş sorunlardan bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="54358-203">The following section describes some of the more advanced issues associated with device drivers.</span></span>

## <a name="advanced-driver-issues"></a><span data-ttu-id="54358-204">Gelişmiş sürücü sorunları</span><span class="sxs-lookup"><span data-stu-id="54358-204">Advanced Driver Issues</span></span>

<span data-ttu-id="54358-205">Daha önce belirtildiği gibi, cihaz sürücüleri, uygulamaları için benzersiz olan gereksinimlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="54358-205">As mentioned previously, device drivers have requirements as unique as their applications.</span></span> <span data-ttu-id="54358-206">Bazı uygulamalar, yüksek frekanslı cihaz kesintileri nedeniyle, başka bir uygulama en iyi duruma getirilmiş sürücü ISRs gerektirirken, çok büyük miktarda veri arabelleğe alma gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="54358-206">Some applications may require an enormous amount of data buffering while another application may require optimized driver ISRs because of high-frequency device interrupts.</span></span>

### <a name="io-buffering"></a><span data-ttu-id="54358-207">G/ç arabelleğe alma</span><span class="sxs-lookup"><span data-stu-id="54358-207">I/O Buffering</span></span> 
<span data-ttu-id="54358-208">Gerçek zamanlı gömülü uygulamalarda veri arabelleğe alma, önemli bir planlama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="54358-208">Data buffering in real-time embedded applications requires considerable planning.</span></span> <span data-ttu-id="54358-209">Tasarımın bazıları temel alınan donanım aygıtı tarafından dikte edilir.</span><span class="sxs-lookup"><span data-stu-id="54358-209">Some of the design is dictated by the underlying hardware device.</span></span> <span data-ttu-id="54358-210">Cihaz temel bayt g/ç sağlıyorsa, büyük olasılıkla basit bir dairesel arabellek olabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-210">If the device provides basic byte I/O, a simple circular buffer is probably in order.</span></span> <span data-ttu-id="54358-211">Ancak, cihaz blok, DMA veya paket g/ç sağlıyorsa, büyük olasılıkla bir arabellek yönetimi düzeni garanti edilir.</span><span class="sxs-lookup"><span data-stu-id="54358-211">However, if the device provides block, DMA, or packet I/O, a buffer management scheme is probably warranted.</span></span> 

### <a name="circular-byte-buffers"></a><span data-ttu-id="54358-212">Dairesel bayt arabellekleri</span><span class="sxs-lookup"><span data-stu-id="54358-212">Circular Byte Buffers</span></span> 
<span data-ttu-id="54358-213">Döngüsel bayt arabellekleri genellikle UART gibi basit bir seri donanım cihazını yöneten sürücülerde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54358-213">Circular byte buffers are typically used in drivers that manage a simple serial hardware device like a UART.</span></span> <span data-ttu-id="54358-214">Genellikle giriş ve çıkış için bir tane olmak üzere iki dairesel arabellek çoğu zaman bu durumlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54358-214">Two circular buffers are most often used in such situations—one for input and one for output.</span></span>

<span data-ttu-id="54358-215">Her döngüsel bayt arabelleği bir bayt bellek alanından (genellikle bir Uchar dizisi), bir okuma işaretçisine ve bir yazma işaretçisine oluşur.</span><span class="sxs-lookup"><span data-stu-id="54358-215">Each circular byte buffer is comprised of a byte memory area (typically an array of UCHARs), a read pointer, and a write pointer.</span></span> <span data-ttu-id="54358-216">Okuma işaretçisi ve yazma işaretçileri arabellekteki aynı bellek konumuna başvuru yaparken bir arabellek boş kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="54358-216">A buffer is considered empty when the read pointer and the write pointers reference the same memory location in the buffer.</span></span> <span data-ttu-id="54358-217">Sürücü başlatma, hem okuma hem de yazma arabelleği işaretçilerini arabelleğin başlangıç adresine ayarlar.</span><span class="sxs-lookup"><span data-stu-id="54358-217">Driver initialization sets both the read and write buffer pointers to the beginning address of the buffer.</span></span>

### <a name="circular-buffer-input"></a><span data-ttu-id="54358-218">Döngüsel arabellek girişi</span><span class="sxs-lookup"><span data-stu-id="54358-218">Circular Buffer Input</span></span> 
<span data-ttu-id="54358-219">Giriş arabelleği, uygulamanın kendisine hazırlanmadan önce gelen karakterleri tutmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54358-219">The input buffer is used to hold characters that arrive before the application is ready for them.</span></span> <span data-ttu-id="54358-220">Bir giriş karakteri alındığında (genellikle bir kesme hizmeti yordamında), yeni karakter donanım aygıtından alınır ve yazma işaretçisi tarafından işaret edilen konumdaki giriş arabelleğine konur.</span><span class="sxs-lookup"><span data-stu-id="54358-220">When an input character is received (usually in an interrupt service routine), the new character is retrieved from the hardware device and placed into the input buffer at the location pointed to by the write pointer.</span></span> <span data-ttu-id="54358-221">Yazma işaretçisi daha sonra arabellekte bir sonraki konuma ilerlemiş olur.</span><span class="sxs-lookup"><span data-stu-id="54358-221">The write pointer is then advanced to the next position in the buffer.</span></span> <span data-ttu-id="54358-222">Sonraki konum arabelleğin sonunu aşıyorsa, yazma işaretçisi arabelleğin başlangıcına ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="54358-222">If the next position is past the end of the buffer, the write pointer is set to the beginning of the buffer.</span></span> <span data-ttu-id="54358-223">Yeni yazma işaretçisi okuma işaretçiyle aynıysa yazma işaretçisinin ilerleme durumu iptal edildiğinde sıranın tam koşulu işlenir.</span><span class="sxs-lookup"><span data-stu-id="54358-223">The queue full condition is handled by canceling the write pointer advancement if the new write pointer is the same as the read pointer.</span></span>

<span data-ttu-id="54358-224">Sürücüye yönelik uygulama giriş bayt istekleri, giriş arabelleğinin okuma ve yazma işaretçilerini ilk olarak inceler.</span><span class="sxs-lookup"><span data-stu-id="54358-224">Application input byte requests to the driver first examine the read and write pointers of the input buffer.</span></span> <span data-ttu-id="54358-225">Okuma ve yazma işaretçileri aynıysa, arabellek boştur.</span><span class="sxs-lookup"><span data-stu-id="54358-225">If the read and write pointers are identical, the buffer is empty.</span></span> <span data-ttu-id="54358-226">Aksi takdirde, okuma işaretçisi aynı değilse, okuma işaretçisi tarafından işaret edilen bayt giriş arabelleğinden kopyalanır ve okuma işaretçisi bir sonraki arabellek konumuna göre ilerlemiş olur.</span><span class="sxs-lookup"><span data-stu-id="54358-226">Otherwise, if the read pointer is not the same, the byte pointed to by the read pointer is copied from the input buffer and the read pointer is advanced to the next buffer location.</span></span> <span data-ttu-id="54358-227">Yeni okuma işaretçisi arabelleğin sonunu aşıyorsa, başlangıca sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="54358-227">If the new read pointer is past the end of the buffer, it is reset to the beginning.</span></span> <span data-ttu-id="54358-228">Şekil 12 ' de dairesel giriş arabelleğinin mantığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="54358-228">Figure 12 shows the logic for the circular input buffer.</span></span>

```C
UCHAR     tx_input_buffer[MAX_SIZE];
UCHAR     tx_input_write_ptr;
UCHAR     tx_input_read_ptr;

/* Initialization.  */
tx_input_write_ptr =  &tx_input_buffer[0];
tx_input_read_ptr =    &tx_input_buffer[0];

/* Input byte ISR... UCHAR alpha has character from device. */
save_ptr =  tx_input_write_ptr;
*tx_input_write_ptr++ =  alpha;
if (tx_input_write_ptr > &tx_input_buffer[MAX_SIZE-1])
    tx_input_write_ptr =  &tx_input_buffer[0];  /* Wrap */
if (tx_input_write_ptr == tx_input_read_ptr)
    tx_input_write_ptr =  save_ptr;  /* Buffer full */

/* Retrieve input byte from buffer... */
if (tx_input_read_ptr != tx_input_write_ptr)
{
    alpha =  *tx_input_read_ptr++;
    if (tx_input_read_ptr > &tx_input_buffer[MAX_SIZE-1])
        tx_input_read_ptr =  &tx_input_buffer[0];
}
```
<span data-ttu-id="54358-229">**ŞEKIL 12. Döngüsel giriş arabelleği mantığı**</span><span class="sxs-lookup"><span data-stu-id="54358-229">**FIGURE 12. Logic for Circular Input Buffer**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54358-230">Güvenilir bir işlem için hem giriş hem de çıkış dairesel arabelleklerinin okuma ve yazma işaretçilerini yaparken kesintileri kilitleme gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="54358-230">For reliable operation, it may be necessary to lockout interrupts when manipulating the read and write pointers of both the input and output circular buffers.</span></span>

### <a name="circular-output-buffer"></a><span data-ttu-id="54358-231">Döngüsel çıkış arabelleği</span><span class="sxs-lookup"><span data-stu-id="54358-231">Circular Output Buffer</span></span> 
<span data-ttu-id="54358-232">Çıktı arabelleği, donanım aygıtı önceki baytı göndermeden önce çıkış için ulaşan karakterleri tutmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54358-232">The output buffer is used to hold characters that have arrived for output before the hardware device finished sending the previous byte.</span></span> <span data-ttu-id="54358-233">Çıkış arabelleği işleme, giriş arabelleği işlemeye benzerdir, ancak iletim çıkış isteği çıkış okuma işaretçisini, uygulama çıktı isteği çıkış yazma işaretçisinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="54358-233">Output buffer processing is similar to input buffer processing, except the transmit complete interrupt processing manipulates the output read pointer, while the application output request utilizes the output write pointer.</span></span> <span data-ttu-id="54358-234">Aksi takdirde, çıkış arabelleği işleme aynıdır.</span><span class="sxs-lookup"><span data-stu-id="54358-234">Otherwise, the output buffer processing is the same.</span></span> <span data-ttu-id="54358-235">Şekil 13, döngüsel çıkış arabelleğinin mantığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="54358-235">Figure 13shows the logic for the circular output buffer.</span></span>

```C
UCHAR     tx_output_buffer[MAX_SIZE];
UCHAR     tx_output_write_ptr;
UCHAR     tx_output_read_ptr;

/* Initialization.  */
tx_output_write_ptr =  &tx_output_buffer[0];
tx_output_read_ptr =   &tx_output_buffer[0];

/* Transmit complete ISR... Device ready to send. */
if (tx_output_read_ptr != tx_output_write_ptr)
{
    *device_reg =  *tx_output_read_ptr++;
    if (tx_output_read_reg > &tx_output_buffer[MAX_SIZE-1])
    tx_output_read_ptr =  &tx_output_buffer[0];
}

/* Output byte driver service. If device busy, buffer! */
save_ptr =  tx_output_write_ptr;
*tx_output_write_ptr++ =  alpha;
if (tx_output_write_ptr > &tx_output_buffer[MAX_SIZE-1])
    tx_output_write_ptr =  &tx_output_buffer[0];  /* Wrap */
if (tx_output_write_ptr == tx_output_read_ptr)
    tx_output_write_ptr =  save_ptr;  /* Buffer full!  */
```
<span data-ttu-id="54358-236">**ŞEKIL 13. Döngüsel çıkış arabelleği mantığı**</span><span class="sxs-lookup"><span data-stu-id="54358-236">**FIGURE 13. Logic for Circular Output Buffer**</span></span>

### <a name="buffer-io-management"></a><span data-ttu-id="54358-237">Arabellek g/ç yönetimi</span><span class="sxs-lookup"><span data-stu-id="54358-237">Buffer I/O Management</span></span> 
<span data-ttu-id="54358-238">Gömülü mikro işlemcilerin performansını artırmak için, birçok çevresel cihaz cihazı yazılım tarafından sağlanan arabelleklerle veri iletir ve alır.</span><span class="sxs-lookup"><span data-stu-id="54358-238">To improve the performance of embedded microprocessors, many peripheral device devices transmit and receive data with buffers supplied by software.</span></span> <span data-ttu-id="54358-239">Bazı uygulamalarda, tek tek veri paketlerini iletmek veya almak için birden çok arabellek kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-239">In some implementations, multiple buffers may be used to transmit or receive individual packets of data.</span></span> 

<span data-ttu-id="54358-240">G/ç arabelleklerinin boyutu ve konumu, uygulama ve/veya sürücü yazılımı tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="54358-240">The size and location of I/O buffers is determined by the application and/or driver software.</span></span> <span data-ttu-id="54358-241">Genellikle, arabellekler boyut olarak sabitlenir ve bir ThreadX SMP blok bellek havuzu içinde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="54358-241">Typically, buffers are fixed in size and managed within a ThreadX SMP block memory pool.</span></span> <span data-ttu-id="54358-242">Şekil 14s tipik bir g/ç arabelleğini ve bunların ayırmasını yöneten bir ThreadX SMP blok bellek havuzunu açıklar.</span><span class="sxs-lookup"><span data-stu-id="54358-242">Figure 14describes a typical I/O buffer and a ThreadX SMP block memory pool that manages their allocation.</span></span>

```C
typedef struct TX_IO_BUFFER_STRUCT
{

      struct TX_IO_BUFFER_STRUCT *tx_next_packet;
    struct TX_IO_BUFFER_STRUCT *tx_next_buffer;
      UCHAR  tx_buffer_area[TX_MAX_BUFFER_SIZE];
} TX_IO_BUFFER;

TX_BLOCK_POOL tx_io_block_pool;

/* Create a pool of I/O buffers. Assume that the pointer
   "free_memory_ptr"points to an available memory area that
   is 64 KBytes in size. */

tx_block_pool_create(&tx_io_block_pool,
                  "Sample IO Driver Buffer Pool",
                  free_memory_ptr, 0x10000,
                  sizeof(TX_IO_BUFFER));
```
<span data-ttu-id="54358-243">**ŞEKIL 14. G/ç arabelleği**</span><span class="sxs-lookup"><span data-stu-id="54358-243">**FIGURE 14. I/O Buffer**</span></span>

### <a name="tx_io_buffer"></a><span data-ttu-id="54358-244">TX_IO_BUFFER</span><span class="sxs-lookup"><span data-stu-id="54358-244">TX_IO_BUFFER</span></span> 
<span data-ttu-id="54358-245">TypeDef TX_IO_BUFFER iki işaretçisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="54358-245">The typedef TX_IO_BUFFER consists of two pointers.</span></span> <span data-ttu-id="54358-246">\***Tx_next_packet** _ işaretçisi, giriş veya çıkış listesinde birden çok paketi bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54358-246">The \***tx_next_packet** _ pointer is used to link multiple packets on either the input or output list.</span></span> <span data-ttu-id="54358-247">_ *_Tx_next_buffer_*\* işaretçisi, cihazdan tek bir veri paketini oluşturan arabellekleri birbirine bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54358-247">The _ *_tx_next_buffer_*\* pointer is used to link together buffers that make up an individual packet of data from the device.</span></span> <span data-ttu-id="54358-248">Arabellek havuzdan ayrıldığında, bu işaretçilerin her ikisi de NULL olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="54358-248">Both of these pointers are set to NULL when the buffer is allocated from the pool.</span></span> <span data-ttu-id="54358-249">Ayrıca, bazı cihazlar arabellek alanının ne kadarının veri içerdiğini göstermek için başka bir alan gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="54358-249">In addition, some devices may require another field to indicate how much of the buffer area actually contains data.</span></span>

### <a name="buffered-io-advantage"></a><span data-ttu-id="54358-250">Arabelleğe alınan g/ç avantajı</span><span class="sxs-lookup"><span data-stu-id="54358-250">Buffered I/O Advantage</span></span> 
<span data-ttu-id="54358-251">Arabellek g/ç düzeninin avantajları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="54358-251">What are the advantages of a buffer I/O scheme?</span></span> <span data-ttu-id="54358-252">En büyük avantaj, verilerin cihaz kayıtları ve uygulamanın belleği arasında kopyalanamaması.</span><span class="sxs-lookup"><span data-stu-id="54358-252">The biggest advantage is that data is not copied between the device registers and the application’s memory.</span></span> <span data-ttu-id="54358-253">Bunun yerine, sürücü cihaza bir dizi arabellek işaretçisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="54358-253">Instead, the driver provides the device with a series of buffer pointers.</span></span> <span data-ttu-id="54358-254">Fiziksel aygıt g/ç, sağlanan arabellek belleğini doğrudan kullanır.</span><span class="sxs-lookup"><span data-stu-id="54358-254">Physical device I/O utilizes the supplied buffer memory directly.</span></span>

<span data-ttu-id="54358-255">Bilgilerin giriş veya çıkış paketlerini kopyalamak için işlemcinin kullanılması son derece maliyetlidir ve yüksek performanslı iş g/ç durumunda kaçınılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="54358-255">Using the processor to copy input or output packets of information is extremely costly and should be avoided in any high throughput I/O situation.</span></span>

<span data-ttu-id="54358-256">Ara belleğe alınan g/ç yaklaşımının bir diğer avantajı da giriş ve çıkış listelerinin tam koşulları olmaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-256">Another advantage to the buffered I/O approach is that the input and output lists do not have full conditions.</span></span> <span data-ttu-id="54358-257">Tüm kullanılabilir arabellekler her iki listede de herhangi bir anda olabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-257">All of the available buffers can be on either list at any one time.</span></span> <span data-ttu-id="54358-258">Bu, daha önce bölümün başında sunulan basit bayt dairesel arabelleklerle karşıttır.</span><span class="sxs-lookup"><span data-stu-id="54358-258">This contrasts with the simple byte circular buffers presented earlier in the chapter.</span></span> <span data-ttu-id="54358-259">Her birinin derlemede belirlenen sabit bir boyutu vardır.</span><span class="sxs-lookup"><span data-stu-id="54358-259">Each had a fixed size determined at compilation.</span></span>

### <a name="buffered-driver-responsibilities"></a><span data-ttu-id="54358-260">Arabellekli sürücü sorumlulukları</span><span class="sxs-lookup"><span data-stu-id="54358-260">Buffered Driver Responsibilities</span></span> 
<span data-ttu-id="54358-261">Arabelleğe alınmış cihaz sürücüleri yalnızca, g/ç arabelleklerinin bağlı listelerini yönetme ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="54358-261">Buffered device drivers are only concerned with managing linked lists of I/O buffers.</span></span> <span data-ttu-id="54358-262">Uygulama yazılımı hazırlanmadan önce alınan paketlere yönelik bir giriş arabelleği listesi tutulur.</span><span class="sxs-lookup"><span data-stu-id="54358-262">An input buffer list is maintained for packets that are received before the application software is ready.</span></span> <span data-ttu-id="54358-263">Buna karşılık, bir çıkış arabelleği listesi, donanım cihazından daha hızlı gönderilmekte olan paketlerin bakımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="54358-263">Conversely, an output buffer list is maintained for packets being sent faster than the hardware device can handle them.</span></span> <span data-ttu-id="54358-264">Sayfa 314 ' de şekil 15 ' te, veri paketlerinin basit giriş ve çıkış bağlantılı listeleri ve her bir paketi oluşturan arabellekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="54358-264">Figure 15 on page 314 shows simple input and output linked lists of data packets and the buffer(s) that make up each packet.</span></span>

![Arabellekli sürücü sorumlulukları](media/image11.png)

<span data-ttu-id="54358-266">**ŞEKIL 15. Input-Output listeleri**</span><span class="sxs-lookup"><span data-stu-id="54358-266">**FIGURE 15. Input-Output Lists**</span></span>

<span data-ttu-id="54358-267">Aynı g/ç arabelleklerine sahip arabellekli sürücülerle uygulamalar arabirimi.</span><span class="sxs-lookup"><span data-stu-id="54358-267">Applications interface with buffered drivers with the same I/O buffers.</span></span> <span data-ttu-id="54358-268">İletim sırasında, uygulama yazılımı, iletmek için bir veya daha fazla arabelleme sahip olan sürücüyü sağlar.</span><span class="sxs-lookup"><span data-stu-id="54358-268">On transmit, application software provides the driver with one or more buffers to transmit.</span></span> <span data-ttu-id="54358-269">Uygulama yazılımı giriş istediğinde, sürücü g/ç arabelleklerinde giriş verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="54358-269">When the application software requests input, the driver returns the input data in I/O buffers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54358-270">Bazı uygulamalarda, uygulamanın sürücüden gelen bir giriş arabelleği için boş bir arabellek alışverişi gerektirdiğini gerektiren bir sürücü giriş arabirimi oluşturmak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-270">In some applications, it may be useful to build a driver input interface that requires the application to exchange a free buffer for an input buffer from the driver.</span></span> <span data-ttu-id="54358-271">Bu, sürücünün içindeki bazı arabellek ayırma işlemlerini giderebilirler.</span><span class="sxs-lookup"><span data-stu-id="54358-271">This might alleviate some buffer allocation processing inside of the driver.</span></span>

### <a name="interrupt-management"></a><span data-ttu-id="54358-272">Kesme yönetimi</span><span class="sxs-lookup"><span data-stu-id="54358-272">Interrupt Management</span></span> 
<span data-ttu-id="54358-273">Bazı uygulamalarda, cihaz kesme sıklığı C 'de ıSR yazmayı veya her kesme üzerinde ThreadX SMP ile etkileşime geçmesini engelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="54358-273">In some applications, the device interrupt frequency may prohibit writing the ISR in C or to interact with ThreadX SMP on each interrupt.</span></span> <span data-ttu-id="54358-274">Örneğin, kesintiye uğramayan bağlamı kaydetmek ve geri yüklemek için 25 ABD sürüyorsa, kesme sıklığının 50 ABD olduğu durumlarda tam bağlam kaydetme işlemini gerçekleştirmek önerilmez.</span><span class="sxs-lookup"><span data-stu-id="54358-274">For example, if it takes 25us to save and restore the interrupted context, it would not be advisable to perform a full context save if the interrupt frequency was 50us.</span></span> <span data-ttu-id="54358-275">Bu gibi durumlarda, birçok cihaz kesmesi işlemek için küçük bir derleme dili ıSR kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54358-275">In such cases, a small assembly language ISR is used to handle most of the device interrupts.</span></span> <span data-ttu-id="54358-276">Bu lowtavan ıSR yalnızca gerektiğinde ThreadX SMP ile etkileşime girebilmelidir.</span><span class="sxs-lookup"><span data-stu-id="54358-276">This lowoverhead ISR would only interact with ThreadX SMP when necessary.</span></span>

<span data-ttu-id="54358-277">Bölüm 3 ' ün sonundaki kesme yönetimi tartışmasında benzer bir tartışma bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-277">A similar discussion can be found in the interrupt management discussion at the end of Chapter 3.</span></span>

> [!NOTE]
> <span data-ttu-id="54358-278">Sürücü kodunun kritik bölümlerini sürücü ıSR kodundan korumak için kesme kilidi kullanılacaksa, iş parçacığı düzeyi sürücü kodunun her zaman ıSR 'nin üzerinde işlendiği aynı çekirdek üzerinde yürütülmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="54358-278">If interrupt lockout is to be used to protect critical sections of driver code from driver ISR code, the thread level driver code must always execute on the same core that the ISR is processed on.</span></span> <span data-ttu-id="54358-279">Aksi halde, TX_DISABLE ve TX_RESTORE gibi iç ThreadX SMP temel elemanlarına, yerleşik tabanlı korumanın de yerleşik olarak kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54358-279">Otherwise, internal ThreadX SMP primitives like TX_DISABLE and TX_RESTORE should be used that also have inter-core protection built-in.</span></span>

### <a name="thread-suspension"></a><span data-ttu-id="54358-280">İş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="54358-280">Thread Suspension</span></span> 
<span data-ttu-id="54358-281">Bu bölümde daha önce sunulan basit sürücü örneğinde, bir karakter kullanılamıyorsa giriş hizmeti 'nin çağıranı askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="54358-281">In the simple driver example presented earlier in this chapter, the caller of the input service suspends if a character is not available.</span></span> <span data-ttu-id="54358-282">Bazı uygulamalarda bu, kabul edilebilir olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="54358-282">In some applications, this might not be acceptable.</span></span>

<span data-ttu-id="54358-283">Örneğin, bir sürücüden gelen girişin işlenmesinden sorumlu iş parçacığının başka bir işi de varsa, yalnızca sürücü girişinin askıya alınması büyük olasılıkla işe gitmemelidir.</span><span class="sxs-lookup"><span data-stu-id="54358-283">For example, if the thread responsible for processing input from a driver also has other duties, suspending on just the driver input is probably not going to work.</span></span> <span data-ttu-id="54358-284">Bunun yerine, sürücünün iş parçacığına diğer işleme isteklerinin yapılma biçimine benzer şekilde istek işleme için özelleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="54358-284">Instead, the driver needs to be customized to request processing similar to the way other processing requests are made to the thread.</span></span>

<span data-ttu-id="54358-285">Çoğu durumda, giriş arabelleği bağlı bir listeye yerleştirilir ve iş parçacığının giriş kuyruğuna bir giriş olayı iletisi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="54358-285">In most cases, the input buffer is placed on a linked list and an input event message is sent to the thread’s input queue.</span></span>