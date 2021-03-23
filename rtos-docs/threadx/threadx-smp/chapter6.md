---
title: Bölüm 6-Azure RTOS ThreadX SMP için tanıtım sistemi
description: Bu bölüm, tüm Azure RTOS ThreadX SMP işlemci desteği paketleriyle birlikte sunulan tanıtım sisteminin bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b94dad3c5ec94befd57200049138b184461a9b55
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827994"
---
# <a name="chapter-6---demonstration-system-for-azure-rtos-threadx-smp"></a><span data-ttu-id="dfb08-103">Bölüm 6-Azure RTOS ThreadX SMP için tanıtım sistemi</span><span class="sxs-lookup"><span data-stu-id="dfb08-103">Chapter 6 - Demonstration System for Azure RTOS ThreadX SMP</span></span>

<span data-ttu-id="dfb08-104">Bu bölüm, tüm Azure RTOS ThreadX SMP işlemci desteği paketleriyle birlikte sunulan tanıtım sisteminin bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-104">This chapter contains a description of the demonstration system that is delivered with all Azure RTOS ThreadX SMP processor support packages.</span></span> 

## <a name="overview"></a><span data-ttu-id="dfb08-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="dfb08-105">Overview</span></span>

<span data-ttu-id="dfb08-106">Her ThreadX SMP ürün dağıtımı, desteklenen tüm mikro işlemcilerde çalışan bir tanıtım sistemi içerir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-106">Each ThreadX SMP product distribution contains a demonstration system that runs on all supported microprocessors.</span></span>

<span data-ttu-id="dfb08-107">Bu örnek sistem ***demo_threadx. c*** dağıtım dosyasında tanımlanmıştır ve THREADX SMP 'in gömülü bir çoklu iş parçacıklı ortamda nasıl kullanıldığını göstermek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-107">This example system is defined in the distribution file ***demo_threadx.c*** and is designed to illustrate how ThreadX SMP is used in an embedded multithread environment.</span></span> <span data-ttu-id="dfb08-108">Tanıtım, başlatma, sekiz iş parçacığı, bir bayt havuzu, bir blok havuzu, bir kuyruk, bir semafor, bir mutex ve bir olay bayrakları grubundan oluşur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-108">The demonstration consists of initialization, eight threads, one byte pool, one block pool, one queue, one semaphore, one mutex, and one event flags group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfb08-109">İş parçacığının yığın boyutu dışında, tanıtım uygulaması tüm ThreadX SMP desteklenen işlemcilerde aynıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-109">Except for the thread’s stack size, the demonstration application is identical on all ThreadX SMP supported processors.</span></span>

<span data-ttu-id="dfb08-110">Bu bölümün geri kalanı boyunca başvurulan satır numaraları dahil olmak üzere ***demo_threadx. c***' nin tüm listesi, sayfa 324 ve sonrasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-110">The complete listing of ***demo_threadx.c***, including the line numbers referenced throughout the remainder of this chapter, is displayed on page 324 and following.</span></span>

## <a name="application-define"></a><span data-ttu-id="dfb08-111">Uygulama tanımlama</span><span class="sxs-lookup"><span data-stu-id="dfb08-111">Application Define</span></span>

<span data-ttu-id="dfb08-112">***Tx_application_define*** işlevi, temel THREADX SMP başlatma işlemi tamamlandıktan sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="dfb08-112">The ***tx_application_define*** function executes after the basic ThreadX SMP initialization is complete.</span></span> <span data-ttu-id="dfb08-113">İş parçacıkları, kuyruklar, Semaforlar, zaman uyumu sağlayıcılar, olay bayrakları ve bellek havuzları dahil olmak üzere tüm ilk sistem kaynaklarını ayarlamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-113">It is responsible for setting up all of the initial system resources, including threads, queues, semaphores, mutexes, event flags, and memory pools.</span></span>

<span data-ttu-id="dfb08-114">Tanıtım sisteminin \***tx_application_define** _ (_line numaraları 60-164 \*), tanıtım nesnelerini aşağıdaki sırayla oluşturur:</span><span class="sxs-lookup"><span data-stu-id="dfb08-114">The demonstration system’s ***tx_application_define** _ (_line numbers 60-164*) creates the demonstration objects in the following order:</span></span>

```C
byte_pool_0
thread_0
thread_1
thread_2
thread_3
thread_4
thread_5
thread_6
thread_7
queue_0
semaphore_0
event_flags_0
mutex_0
block_pool_0
```
<span data-ttu-id="dfb08-115">Tanıtım sistemi başka hiçbir ek ThreadX SMP nesnesi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="dfb08-115">The demonstration system does not create any other additional ThreadX SMP objects.</span></span> <span data-ttu-id="dfb08-116">Ancak gerçek bir uygulama, iş parçacıklarının yürütülmesi sırasında çalışma zamanı sırasında sistem nesneleri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-116">However, an actual application may create system objects during runtime inside of executing threads.</span></span>

### <a name="initial-execution"></a><span data-ttu-id="dfb08-117">İlk yürütme</span><span class="sxs-lookup"><span data-stu-id="dfb08-117">Initial Execution</span></span> 
<span data-ttu-id="dfb08-118">Tüm iş parçacıkları **TX_AUTO_START** seçeneğiyle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-118">All threads are created with the **TX_AUTO_START** option.</span></span> <span data-ttu-id="dfb08-119">Bu, başlangıçta yürütülmeye hazırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="dfb08-119">This makes them initially ready for execution.</span></span> <span data-ttu-id="dfb08-120">**_Tx_application_define_** tamamlandıktan sonra Denetim, iş parçacığı zamanlayıcısına aktarılır ve her bir iş parçacığına buradan gönderilir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-120">After **_tx_application_define_** completes, control is transferred to the thread scheduler and from there to each individual thread.</span></span>

<span data-ttu-id="dfb08-121">İş parçacıklarının yürütülme sırası önceliklerine göre ve oluşturuldukları sırada belirlenir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-121">The order in which the threads execute is determined by their priority and the order that they were created.</span></span> <span data-ttu-id="dfb08-122">Tanıtım sisteminde, en yüksek önceliğesahip olduğundan (_1 \* önceliğiyle oluşturulmuş olduğundan) ilk olarak bir thread_0 _ yürütülür. \***Thread_0** askıya alındıktan sonra_ , _*_thread_5_*_ yürütülür ve ardından _*_thread_3_*_, _*_thread_4_*_, _*_thread_6_*_, _*_thread_7_*_, _*_thread_1_*_ ve finally _ \*_thread_2_.</span><span class="sxs-lookup"><span data-stu-id="dfb08-122">In the demonstration system, ***thread_0** _ executes first because it has the highest priority (_it was created with a priority of 1*). After \***thread_0**_ suspends, _*_thread_5_*_ is executed, followed by the execution of _*_thread_3_*_, _*_thread_4_*_, _*_thread_6_*_, _*_thread_7_*_, _*_thread_1_*_, and finally _\*_thread_2_\*\*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfb08-123">**Thread_3** ve **thread_4** aynı önceliğe sahip olsa da (her ikisi de 8 önceliğiyle oluşturulmuştur), ilk olarak **thread_3** yürütülür.</span><span class="sxs-lookup"><span data-stu-id="dfb08-123">Even though **thread_3** and **thread_4** have the same priority (both created with a priority of 8), **thread_3** executes first.</span></span> <span data-ttu-id="dfb08-124">Bunun nedeni **thread_3** oluşturulması ve **thread_4** önce hazırlanmaya gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-124">This is because **thread_3** was created and became ready before **thread_4**.</span></span> <span data-ttu-id="dfb08-125">Eşit önceliğe sahip iş parçacıkları bir FıFO olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="dfb08-125">Threads of equal priority execute in a FIFO fashion.</span></span>

## <a name="thread-0"></a><span data-ttu-id="dfb08-126">İş parçacığı 0</span><span class="sxs-lookup"><span data-stu-id="dfb08-126">Thread 0</span></span>

<span data-ttu-id="dfb08-127">\***Thread_0_entry** _ işlevi, iş parçacığının giriş noktasını işaretler _(satırlar 167-190 \*). \***Thread_0**_ , tanıtım sisteminde yürütülecek ilk iş parçacığıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-127">The function ***thread_0_entry** _ marks the entry point of the thread _(lines 167-190*). \***Thread_0**_ is the first thread in the demonstration system to execute.</span></span> <span data-ttu-id="dfb08-128">İşlem basittir: sayacını artırır, 10 Zamanlayıcı onay işaretleri için bir olay bayrağı koyar, bir olay bayrağını bir uyandır _ *_thread_5_* \*, sonra da diziyi yineler.</span><span class="sxs-lookup"><span data-stu-id="dfb08-128">Its processing is simple: it increments its counter, sleeps for 10 timer ticks, sets an event flag to wake up _\*_thread_5_\*\*, then repeats the sequence.</span></span>

<span data-ttu-id="dfb08-129">***Thread_0*** , sistemdeki en yüksek öncelikli iş parçacığıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-129">***Thread_0*** is the highest priority thread in the system.</span></span> <span data-ttu-id="dfb08-130">İstenen uyku süresi sona erdiğinde, gösteride çalışan diğer iş parçacıklarını da çalışır hale gelir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-130">When its requested sleep expires, it will preempt any other executing thread in the demonstration.</span></span>

## <a name="thread-1"></a><span data-ttu-id="dfb08-131">İş parçacığı 1</span><span class="sxs-lookup"><span data-stu-id="dfb08-131">Thread 1</span></span>

<span data-ttu-id="dfb08-132">\***Thread_1_entry** _ işlevi iş parçacığının giriş noktasını işaretler _(satırlar 193-216 \*). \***Thread_1**_ , tanıtım sisteminde yürütülecek ikinci-son iş parçacığıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-132">The function ***thread_1_entry** _ marks the entry point of the thread _(lines 193-216*). \***Thread_1**_ is the second-to-last thread in the demonstration system to execute.</span></span> <span data-ttu-id="dfb08-133">İşlemesi, sayacını arttırmadan, _*_thread_2_*_ bir ileti göndermekten (_\* \***queue_0**_) ve diziyi tekrarlarından oluşur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-133">Its processing consists of incrementing its counter, sending a message to _*_thread_2_*_ (_through\* \***queue_0**_), and repeating the sequence.</span></span> <span data-ttu-id="dfb08-134">_*_Thread_1_*_ _*_queue_0_*_ dolduğunda her ne kadar zaman beklediğine dikkat edin (_line 207 \*).</span><span class="sxs-lookup"><span data-stu-id="dfb08-134">Notice that _*_thread_1_*_ suspends whenever _*_queue_0_*_ becomes full (_line 207\*).</span></span>

## <a name="thread-2"></a><span data-ttu-id="dfb08-135">İş parçacığı 2</span><span class="sxs-lookup"><span data-stu-id="dfb08-135">Thread 2</span></span>

<span data-ttu-id="dfb08-136">\***Thread_2_entry** _ işlevi, iş parçacığının giriş noktasını işaretler _(satırlar 219-243 \*). \***Thread_2**_ , tanıtım sisteminde yürütülecek son iş parçacığıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-136">The function ***thread_2_entry** _ marks the entry point of the thread _(lines 219-243*). \***Thread_2**_ is the last thread in the demonstration system to execute.</span></span> <span data-ttu-id="dfb08-137">İşlemesi, sayacını arttırmadan, _*_thread_1_*_ ( _*_queue_0_*_) bir ileti almaya ve sırayı tekrarlamadan oluşur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-137">Its processing consists of incrementing its counter, getting a message from _*_thread_1_*_ (through _*_queue_0_*_), and repeating the sequence.</span></span> <span data-ttu-id="dfb08-138">_*_Queue_0_*_ boş olduğunda _*_thread_2_*_ askıya aldığından (_line 233 \*) dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="dfb08-138">Notice that _*_thread_2_*_ suspends whenever _*_queue_0_*_ becomes empty (_line 233\*).</span></span>

<span data-ttu-id="dfb08-139">***Thread_1** _ ve _*_thread_2_\*_ tanıtım sisteminde (_priority 16) en düşük önceliği paylaşsa da *, bunlar aynı zamanda yalnızca yürütmeye yönelik olan tek iş parçacıklarından oluşur. Bunlar aynı zamanda, zaman dilimle oluşturulan tek iş parçacıklarında (* satırlar 87 ve 93 \*).</span><span class="sxs-lookup"><span data-stu-id="dfb08-139">Although ***thread_1** _ and _*_thread_2_*_ share the lowest priority in the demonstration system (_priority 16 *), they are also the only threads that are ready for execution most of the time. They are also the only threads created with time-slicing (* lines 87 and 93*).</span></span> <span data-ttu-id="dfb08-140">Diğer iş parçacığı yürütülmeden önce, her iş parçacığının en fazla 4 süreölçer işareti yürütmesine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-140">Each thread is allowed to execute for a maximum of 4 timer ticks before the other thread is executed.</span></span>

## <a name="threads-3-and-4"></a><span data-ttu-id="dfb08-141">İş parçacıkları 3 ve 4</span><span class="sxs-lookup"><span data-stu-id="dfb08-141">Threads 3 and 4</span></span>

<span data-ttu-id="dfb08-142">***Thread_3_and_4_entry** _ işlevi _*_thread_3_*_ ve _*_thread_4_\*_ giriş noktasını işaretler _(satır 246-280 \*). Her iki iş parçacığı da 8 önceliğine sahiptir ve bu, tanıtım sistemindeki üçüncü ve dördüncü iş parçacıklarının yürütülmesine neden olur. Her iş parçacığının işleme işlemi aynıdır: sayacını artırma, \***semaphore_0** alma_, 2 Zamanlayıcı işareti için uyuyan, _*_semaphore_0_*_ serbest bırakma ve diziyi yineleme.</span><span class="sxs-lookup"><span data-stu-id="dfb08-142">The function ***thread_3_and_4_entry** _ marks the entry point of both _*_thread_3_*_ and _*_thread_4_*_ _(lines 246-280*). Both threads have a priority of 8, which makes them the third and fourth threads in the demonstration system to execute. The processing for each thread is the same: incrementing its counter, getting \***semaphore_0**_, sleeping for 2 timer ticks, releasing _*_semaphore_0_*_, and repeating the sequence.</span></span> <span data-ttu-id="dfb08-143">Her bir iş parçacığının _*_semaphore_0_*_ kullanılamadığında her zaman askıya aldığından (_line 264 \*) dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="dfb08-143">Notice that each thread suspends whenever _*_semaphore_0_*_ is unavailable (_line 264\*).</span></span>

<span data-ttu-id="dfb08-144">Ayrıca, her iki iş parçacığı de ana işlemleri için aynı işlevi kullanır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-144">Also both threads use the same function for their main processing.</span></span> <span data-ttu-id="dfb08-145">Bu, her ikisi de kendi benzersiz yığınına sahip olduğundan ve C doğal olarak yeniden alındığından, sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-145">This presents no problems because they both have their own unique stack, and C is naturally reentrant.</span></span> <span data-ttu-id="dfb08-146">Her bir iş parçacığı, ne zaman iş parçacığı giriş parametresi (*satır 258*), ne zaman oluşturulduklarında (satır *102 ve 109*) inceleyerek olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="dfb08-146">Each thread determines which one it is by examination of the thread input parameter (*line 258*), which is setup when they are created (*lines 102 and 109*).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfb08-147">İş parçacığı yürütme sırasında geçerli iş parçacığı noktasını almak ve bunu denetim bloğunun adresiyle karşılaştırmak, iş parçacığı kimliğini belirleyebilmek için de makul bir işlem olur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-147">It is also reasonable to obtain the current thread point during thread execution and compare it with the control block’s address to determine thread identity.</span></span>

## <a name="thread-5"></a><span data-ttu-id="dfb08-148">İş parçacığı 5</span><span class="sxs-lookup"><span data-stu-id="dfb08-148">Thread 5</span></span>

<span data-ttu-id="dfb08-149">\***Thread_5_entry** _ işlevi, iş parçacığının giriş noktasını işaretler _(satırlar 283-305 \*). \***Thread_5**_ , tanıtım sisteminde yürütülecek ikinci iş parçacığıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-149">The function ***thread_5_entry** _ marks the entry point of the thread _(lines 283-305*). \***Thread_5**_ is the second thread in the demonstration system to execute.</span></span> <span data-ttu-id="dfb08-150">İşlemesi, sayacını arttırmadan, _*_thread_0_*_ ( _*_event_flags_0_*_ aracılığıyla) bir olay bayrağını almaya ve sırayı tekrarlamadan oluşur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-150">Its processing consists of incrementing its counter, getting an event flag from _*_thread_0_*_ (through _*_event_flags_0_*_), and repeating the sequence.</span></span> <span data-ttu-id="dfb08-151">_*_Thread_5_*_ , _*_event_flags_0_*_ içindeki olay bayrağını her ne zaman askıya alacağını (_line 298 \*) unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dfb08-151">Notice that _*_thread_5_*_ suspends whenever the event flag in _*_event_flags_0_*_ is not available (_line 298\*).</span></span>

## <a name="threads-6-and-7"></a><span data-ttu-id="dfb08-152">İş parçacıkları 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="dfb08-152">Threads 6 and 7</span></span>

<span data-ttu-id="dfb08-153">***Thread_6_and_7_entry** _ işlevi _*_thread_6_*_ ve _*_thread_7_\*_ giriş noktasını işaretler _(satır 307-358 \*). Her iki iş parçacığı da 8 önceliğine sahiptir ve bu da, tanıtım sistemindeki beşinci ve altıncı iş parçacıklarını yürütür. Her iş parçacığı için işleme aynıdır: sayacını artırma, iki kez \***mutex_0**_ , 2 Zamanlayıcı işareti için uyuyan, _*_mutex_0_*_ iki kez serbest bırakma ve diziyi yineleme.</span><span class="sxs-lookup"><span data-stu-id="dfb08-153">The function ***thread_6_and_7_entry** _ marks the entry point of both _*_thread_6_*_ and _*_thread_7_*_ _(lines 307-358*). Both threads have a priority of 8, which makes them the fifth and sixth threads in the demonstration system to execute. The processing for each thread is the same: incrementing its counter, getting \***mutex_0**_ twice, sleeping for 2 timer ticks, releasing _*_mutex_0_*_ twice, and repeating the sequence.</span></span> <span data-ttu-id="dfb08-154">Her bir iş parçacığının _*_mutex_0_*_ kullanılamadığında her zaman askıya aldığından (_line 325 \*) dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="dfb08-154">Notice that each thread suspends whenever _*_mutex_0_*_ is unavailable (_line 325\*).</span></span>

<span data-ttu-id="dfb08-155">Ayrıca, her iki iş parçacığı de ana işlemleri için aynı işlevi kullanır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-155">Also both threads use the same function for their main processing.</span></span> <span data-ttu-id="dfb08-156">Bu, her ikisi de kendi benzersiz yığınına sahip olduğundan ve C doğal olarak yeniden alındığından, sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="dfb08-156">This presents no problems because they both have their own unique stack, and C is naturally reentrant.</span></span> <span data-ttu-id="dfb08-157">Her bir iş parçacığı, ne zaman iş parçacığı giriş parametresi (*satır 319*), ne zaman oluşturulduklarında (satır *126 ve 133*) inceleyerek olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="dfb08-157">Each thread determines which one it is by examination of the thread input parameter (*line 319*), which is setup when they are created (*lines 126 and 133*).</span></span>

## <a name="observing-the-demonstration"></a><span data-ttu-id="dfb08-158">Tanıtımı gözlemleme</span><span class="sxs-lookup"><span data-stu-id="dfb08-158">Observing the Demonstration</span></span>

<span data-ttu-id="dfb08-159">Tanıtım iş parçacıklarının her biri kendi benzersiz sayacını arttırır.</span><span class="sxs-lookup"><span data-stu-id="dfb08-159">Each of the demonstration threads increments its own unique counter.</span></span> <span data-ttu-id="dfb08-160">Demo işlemini denetlemek için aşağıdaki sayaçlar incelenmeyebilir:</span><span class="sxs-lookup"><span data-stu-id="dfb08-160">The following counters may be examined to check on the demo’s operation:</span></span>

```C
thread_0_counter
thread_1_counter
thread_2_counter
thread_3_counter
thread_4_counter
thread_5_counter
thread_6_counter
thread_7_counter
```

<span data-ttu-id="dfb08-161">Bu sayaçların her biri, tanıtım yürütüldüğünde, ***thread_1_counter** _ ve _ *_thread_2_counter_** en hızlı hızda artan şekilde artmaya devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-161">Each of these counters should continue to increase as the demonstration executes, with ***thread_1_counter** _ and _ *_thread_2_counter_** increasing at the fastest rate.</span></span>

## <a name="distribution-file-demo_threadxc"></a><span data-ttu-id="dfb08-162">Dağıtım dosyası: demo_threadx. c</span><span class="sxs-lookup"><span data-stu-id="dfb08-162">Distribution file: demo_threadx.c</span></span>

<span data-ttu-id="dfb08-163">Bu bölümde, bu bölüm boyunca başvurulan satır numaraları dahil olmak üzere ***demo_threadx. c***' nin tüm listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dfb08-163">This section displays the complete listing of ***demo_threadx.c***, including the line numbers referenced throughout this chapter.</span></span>

```C
000 /* This is a small demo of the high-performance ThreadX SMP kernel. It includes examples of eight
001 threads of different priorities, using a message queue, semaphore, mutex, event flags group,
002 byte pool, and block pool. */
003
004 #include "tx_api.h"
005
006 #define DEMO_STACK_SIZE         1024
007 #define DEMO_BYTE_POOL_SIZE     9120
008 #define DEMO_BLOCK_POOL_SIZE    100
009 #define DEMO_QUEUE_SIZE         100
010
011 /* Define the ThreadX SMP object control blocks...  */
012
013 TX_THREAD               thread_0;
014 TX_THREAD               thread_1;
015 TX_THREAD               thread_2;
016 TX_THREAD               thread_3;
017 TX_THREAD               thread_4;
018 TX_THREAD               thread_5;
019 TX_THREAD               thread_6;
020 TX_THREAD               thread_7;
021 TX_QUEUE                queue_0;
022 TX_SEMAPHORE            semaphore_0;
023 TX_MUTEX                mutex_0;
024 TX_EVENT_FLAGS_GROUP    event_flags_0;
025 TX_BYTE_POOL            byte_pool_0;
026 TX_BLOCK_POOL           block_pool_0;
027
028 /* Define the counters used in the demo application...  */
029
030 ULONG                    thread_0_counter;
031 ULONG                    thread_1_counter;
032 ULONG                    thread_1_messages_sent;
033 ULONG                    thread_2_counter;
034 ULONG                    thread_2_messages_received;
035 ULONG                    thread_3_counter;
036 ULONG                    thread_4_counter;
037 ULONG                    thread_5_counter;
038 ULONG                    thread_6_counter;
039 ULONG                    thread_7_counter;
040
041 /* Define thread prototypes.  */
042
043 void    thread_0_entry(ULONG thread_input);
044 void    thread_1_entry(ULONG thread_input);
045 void    thread_2_entry(ULONG thread_input);
046 void    thread_3_and_4_entry(ULONG thread_input);
047 void    thread_5_entry(ULONG thread_input);
048 void    thread_6_and_7_entry(ULONG thread_input);
049
050
051 /* Define main entry point.  */
052
053 int main()
054 {
055
056     /* Enter the ThreadX SMP kernel. */
057     tx_kernel_enter();
058 }
059
060 /* Define what the initial system looks like. */
061 void    tx_application_define(void *first_unused_memory)
062 {
063
064 CHAR    *pointer;
065
066    /* Create a byte memory pool from which to allocate the thread stacks. */
067    tx_byte_pool_create(&byte_pool_0, "byte pool 0", first_unused_memory,
068                               DEMO_BYTE_POOL_SIZE);
069
070    /* Put system definition stuff in here, e.g., thread creates and other assorted
071       create information. */
072
073    /* Allocate the stack for thread 0. */
074    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
075
076    /* Create the main thread. */
077    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
078                               pointer, DEMO_STACK_SIZE,
079                               1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
080
081    /* Allocate the stack for thread 1. */
082    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
083
084    /* Create threads 1 and 2. These threads pass information through a ThreadX SMP
085       message queue. It is also interesting to note that these threads have a time
086       slice. */
087    tx_thread_create(&thread_1, "thread 1", thread_1_entry, 1,
088                              pointer, DEMO_STACK_SIZE,
089                              16, 16, 4, TX_AUTO_START);
090
091    /* Allocate the stack for thread 2. */
092    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
093    tx_thread_create(&thread_2, "thread 2", thread_2_entry, 2,
094                              pointer, DEMO_STACK_SIZE,
095                              16, 16, 4, TX_AUTO_START);
096
097    /* Allocate the stack for thread 3. */
098    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
099
100    /* Create threads 3 and 4. These threads compete for a ThreadX SMP counting semaphore.
101       An interesting thing here is that both threads share the same instruction area. */
102    tx_thread_create(&thread_3, "thread 3", thread_3_and_4_entry, 3,
103                              pointer, DEMO_STACK_SIZE,
104                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
105
106    /* Allocate the stack for thread 4. */
107    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
108
109    tx_thread_create(&thread_4, "thread 4", thread_3_and_4_entry, 4,
110                              pointer, DEMO_STACK_SIZE,
111                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
112
113    /* Allocate the stack for thread 5. */
114    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
115
116    /* Create thread 5. This thread simply pends on an event flag, which will be set
117       by thread_0. */
118    tx_thread_create(&thread_5, "thread 5", thread_5_entry, 5,
119                              pointer, DEMO_STACK_SIZE,
120                              4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
121
122    /* Allocate the stack for thread 6. */
123    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
124
125    /* Create threads 6 and 7. These threads compete for a ThreadX SMP mutex. */
126    tx_thread_create(&thread_6, "thread 6", thread_6_and_7_entry, 6,
127                              pointer, DEMO_STACK_SIZE,
128                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
129
130    /* Allocate the stack for thread 7. */
131    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
132
133    tx_thread_create(&thread_7, "thread 7", thread_6_and_7_entry, 7,
134                              pointer, DEMO_STACK_SIZE,
135                              8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);
136
137    /* Allocate the message queue. */
138    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_QUEUE_SIZE*sizeof(ULONG), TX_NO_WAIT);
139
140    /* Create the message queue shared by threads 1 and 2. */
141    tx_queue_create(&queue_0, "queue 0", TX_1_ULONG, pointer, DEMO_QUEUE_SIZE*sizeof(ULONG));
142
143    /* Create the semaphore used by threads 3 and 4. */
144    tx_semaphore_create(&semaphore_0, "semaphore 0", 1);
145
146    /* Create the event flags group used by threads 1 and 5. */
147    tx_event_flags_create(&event_flags_0, "event flags 0");
148
149    /* Create the mutex used by thread 6 and 7 without priority inheritance. */
150    tx_mutex_create(&mutex_0, "mutex 0", TX_NO_INHERIT);
151
152    /* Allocate the memory for a small block pool. */
153    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_BLOCK_POOL_SIZE, TX_NO_WAIT);
154
155    /* Create a block memory pool to allocate a message buffer from. */
156    tx_block_pool_create(&block_pool_0, "block pool 0", sizeof(ULONG), pointer,
157                 DEMO_BLOCK_POOL_SIZE);
158
159    /* Allocate a block and release the block memory. */
160    tx_block_allocate(&block_pool_0, &pointer, TX_NO_WAIT);
161
162    /* Release the block back to the pool. */
163    tx_block_release(pointer);
164 }
165
166    /* Define the test threads. */
167    void thread_0_entry(ULONG thread_input)
168 {
169
170 UINT status;
171
172
173    /* This thread simply sits in while-forever-sleep loop. */
174     while(1)
175    {
176
177    /* Increment the thread counter. */
178    thread_0_counter++;
179
180    /* Sleep for 10 ticks. */
181    tx_thread_sleep(10);
182
183    /* Set event flag 0 to wakeup thread 5. */
184    status = tx_event_flags_set(&event_flags_0, 0x1, TX_OR);
185
186    /* Check status. */
187    if (status != TX_SUCCESS)
188       break;
189    }
190 }
191
192
193 void    thread_1_entry(ULONG thread_input)
194 {
195
196 UINT    status;
197
198
199    /* This thread simply sends messages to a queue shared by thread 2. */
200    while(1)
201    {
202
203         /* Increment the thread counter. */
204         thread_1_counter++;
205
206         /* Send message to queue 0. */
207         status = tx_queue_send(&queue_0, &thread_1_messages_sent, TX_WAIT_FOREVER);
208
209         /* Check completion status. */
210         if (status != TX_SUCCESS)
211            break;
212
213         /* Increment the message sent. */
214         thread_1_messages_sent++;
215    }
216 }
217
218
219 void     thread_2_entry(ULONG thread_input)
220 {
221
222 ULONG     received_message;
223 UINT      status;
224
225     /* This thread retrieves messages placed on the queue by thread 1. */
226     while(1)
227     {
228
229         /* Increment the thread counter. */
230         thread_2_counter++;
231
232         /* Retrieve a message from the queue. */
233         status = tx_queue_receive(&queue_0, &received_message, TX_WAIT_FOREVER);
234
235         /* Check completion status and make sure the message is what we
236            expected. */
237         if ((status != TX_SUCCESS) || (received_message != thread_2_messages_received))
238            break;
239
240         /* Otherwise, all is okay. Increment the received message count. */
241         thread_2_messages_received++;
242      }
243 }
244
245
246 void     thread_3_and_4_entry(ULONG thread_input)
247 {
248
249 UINT     status;
250
251
252     /* This function is executed from thread 3 and thread 4. As the loop
253        below shows, these function compete for ownership of semaphore_0. */
254     while(1)
255     {
256
257         /* Increment the thread counter. */
258         if (thread_input == 3)
259            thread_3_counter++;
260         else
261            thread_4_counter++;
262
263         /* Get the semaphore with suspension. */
264         status = tx_semaphore_get(&semaphore_0, TX_WAIT_FOREVER);
265
266         /* Check status. */
267         if (status != TX_SUCCESS)
268            break;
269
270         /* Sleep for 2 ticks to hold the semaphore. */
271         tx_thread_sleep(2);
272
273         /* Release the semaphore. */
274         status = tx_semaphore_put(&semaphore_0);
275
276         /* Check status. */
277         if (status != TX_SUCCESS)
278             break;
279     }
280 }
281
282
283 void     thread_5_entry(ULONG thread_input)
284 {
285
286 UINT     status;
287 ULONG    actual_flags;
288
289
290     /* This thread simply waits for an event in a forever loop. */
291     while(1)
292     {
293
294         /* Increment the thread counter. */
295         thread_5_counter++;
296
297         /* Wait for event flag 0. */
298         status = tx_event_flags_get(&event_flags_0, 0x1, TX_OR_CLEAR,
299                                &actual_flags, TX_WAIT_FOREVER);
300
301         /* Check status. */
302         if ((status != TX_SUCCESS) || (actual_flags != 0x1))
303            break;
304     }
305 }
306
307 void     thread_6_and_7_entry(ULONG thread_input)
308 {
309
310 UINT     status;
311
312
313     /* This function is executed from thread 6 and thread 7. As the loop
314         below shows, these function compete for ownership of mutex_0. */
315     while(1)
316     {
317
318         /* Increment the thread counter. */
319         if (thread_input == 6)
320            thread_6_counter++;
321         else
322            thread_7_counter++;
323
324         /* Get the mutex with suspension. */
325         status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);
326
327         /* Check status. */
328         if (status != TX_SUCCESS)
329            break;
330
331         /* Get the mutex again with suspension. This shows
332            that an owning thread may retrieve the mutex it
333            owns multiple times. */
334         status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);
335
336         /* Check status. */
337         if (status != TX_SUCCESS)
338             break;
339
340         /* Sleep for 2 ticks to hold the mutex. */
341         tx_thread_sleep(2);
342
343         /* Release the mutex. */
344         status = tx_mutex_put(&mutex_0);
345
346         /* Check status. */
347         if (status != TX_SUCCESS)
348            break;
349
350         /* Release the mutex again. This will actually
351            release ownership since it was obtained twice. */
352         status = tx_mutex_put(&mutex_0);
353
354         /* Check status. */
355         if (status != TX_SUCCESS)
356            break;
357     }
358 }
```