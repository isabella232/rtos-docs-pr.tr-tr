---
title: ThreadX Azure RTOS anlama
description: Azure ThreadX, özellikle derinden eklenmiş uygulamalar için tasarlanmış gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS).
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0fb861c2291046c2ac6edf1d03014996daa09a8e
ms.sourcegitcommit: c1b00341e0c5ab71372f3d9cc4ee3bdd3702b805
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111988371"
---
# <a name="overview-of-azure-rtos-threadx"></a><span data-ttu-id="9fa1f-103">Azure RTOS ThreadX'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="9fa1f-103">Overview of Azure RTOS ThreadX</span></span>

<span data-ttu-id="9fa1f-104">Azure RTOS ThreadX, Microsoft'un ayrıntılı, gerçek zamanlı Real-Time IoT uygulamaları için tasarlanmış gelişmiş endüstriyel sınıf işletim sistemidir (RTOS).</span><span class="sxs-lookup"><span data-stu-id="9fa1f-104">Azure RTOS ThreadX is Microsoft's advanced industrial grade Real-Time Operating System (RTOS) designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="9fa1f-105">Azure RTOS ThreadX gelişmiş zamanlama, iletişim, eşitleme, zamanlayıcı, bellek yönetimi ve kesme yönetimi özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-105">Azure RTOS ThreadX provides advanced scheduling, communication, synchronization, timer, memory management, and interrupt management facilities.</span></span> <span data-ttu-id="9fa1f-106">Ayrıca Azure RTOS ThreadX'in picokernel™ mimarisi™ preemption-threshold™ scheduling, event-chaining, ™ execution profiling, performance metrics ve system event tracing gibi birçok gelişmiş özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-106">In addition, Azure RTOS ThreadX has many advanced features, including its picokernel™ architecture, preemption-threshold™ scheduling, event-chaining,™ execution profiling, performance metrics, and system event tracing.</span></span> <span data-ttu-id="9fa1f-107">Azure RTOS ThreadX, üstün kullanım kolaylığıyla birlikte en zorlu tümleşik uygulamalar için ideal seçimdir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-107">Combined with its superior ease-of-use, Azure RTOS ThreadX is the ideal choice for the most demanding of embedded applications.</span></span> <span data-ttu-id="9fa1f-108">Azure RTOS ThreadX, 2017 yılında tüketici cihazları, tıbbi elektronik cihazlar ve endüstriyel kontrol ekipmanları gibi çok çeşitli ürünlerde 6,2 milyardan fazla dağıtıma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-108">As of 2017, Azure RTOS ThreadX has over 6.2 billion deployments, in a wide variety of products, including consumer devices, medical electronics, and industrial control equipment.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="9fa1f-109">API Protokolleri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-109">API Protocols</span></span>

### <a name="azure-rtos-threadx-services"></a><span data-ttu-id="9fa1f-110">Azure RTOS ThreadX Services</span><span class="sxs-lookup"><span data-stu-id="9fa1f-110">Azure RTOS ThreadX Services</span></span>

* <span data-ttu-id="9fa1f-111">Dinamik iş parçacığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-111">Dynamic thread creation</span></span>
* <span data-ttu-id="9fa1f-112">İş parçacığı sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-112">No limits on the number of threads</span></span>
* <span data-ttu-id="9fa1f-113">Ana iş parçacığı API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-113">Main thread APIs include:</span></span>
  * <span data-ttu-id="9fa1f-114">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-114">tx_thread_create</span></span>
  * <span data-ttu-id="9fa1f-115">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-115">tx_thread_delete</span></span>
  * <span data-ttu-id="9fa1f-116">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fa1f-116">tx_thread_preemption_change</span></span>
  * <span data-ttu-id="9fa1f-117">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fa1f-117">tx_thread_priority_change</span></span>
  * <span data-ttu-id="9fa1f-118">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fa1f-118">tx_thread_relinquish</span></span>
  * <span data-ttu-id="9fa1f-119">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fa1f-119">tx_thread_reset</span></span>
  * <span data-ttu-id="9fa1f-120">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fa1f-120">tx_thread_resume</span></span>
  * <span data-ttu-id="9fa1f-121">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fa1f-121">tx_thread_sleep</span></span>
  * <span data-ttu-id="9fa1f-122">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fa1f-122">tx_thread_suspend</span></span>
  * <span data-ttu-id="9fa1f-123">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fa1f-123">tx_thread_terminate</span></span>
  * <span data-ttu-id="9fa1f-124">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fa1f-124">tx_thread_wait_abort</span></span>
* <span data-ttu-id="9fa1f-125">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-125">Additional information and performance APIs</span></span>

### <a name="message-queues"></a><span data-ttu-id="9fa1f-126">İleti Kuyrukları</span><span class="sxs-lookup"><span data-stu-id="9fa1f-126">Message Queues</span></span>

* <span data-ttu-id="9fa1f-127">Dinamik kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-127">Dynamic queue creation</span></span>
* <span data-ttu-id="9fa1f-128">Kuyruk sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-128">No limits on the number of queues</span></span>
* <span data-ttu-id="9fa1f-129">Değere (veya işaretçi aracılığıyla başvuruya göre) kopyalanan iletiler</span><span class="sxs-lookup"><span data-stu-id="9fa1f-129">Messages copied by value (or by reference via pointer)</span></span>
* <span data-ttu-id="9fa1f-130">1 ile 16 32 bit sözcük arasında ileti boyutları</span><span class="sxs-lookup"><span data-stu-id="9fa1f-130">Message sizes from 1 to 16 32-bit words</span></span>
* <span data-ttu-id="9fa1f-131">Boş ve dolu isteğe bağlı iş parçacığı askıya alındı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-131">Optional thread suspension on empty and full</span></span>
* <span data-ttu-id="9fa1f-132">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-132">Optional timeout on all suspension</span></span>
* <span data-ttu-id="9fa1f-133">Ana ileti kuyruğu API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-133">Main message queue APIs include:</span></span>
  * <span data-ttu-id="9fa1f-134">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-134">tx_queue_create</span></span>
  * <span data-ttu-id="9fa1f-135">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-135">tx_queue_delete</span></span>
  * <span data-ttu-id="9fa1f-136">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fa1f-136">tx_queue_flush</span></span>
  * <span data-ttu-id="9fa1f-137">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fa1f-137">tx_queue_front_send</span></span>
  * <span data-ttu-id="9fa1f-138">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fa1f-138">tx_queue_receive</span></span>
  * <span data-ttu-id="9fa1f-139">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fa1f-139">tx_queue_send_notify</span></span>
* <span data-ttu-id="9fa1f-140">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-140">Additional information and performance APIs</span></span>

### <a name="counting-semaphores"></a><span data-ttu-id="9fa1f-141">Semaforları Sayma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-141">Counting Semaphores</span></span>

* <span data-ttu-id="9fa1f-142">Dinamik semafor oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-142">Dynamic semaphore creation</span></span>
* <span data-ttu-id="9fa1f-143">Semafor sayısına sınırlama yoktur</span><span class="sxs-lookup"><span data-stu-id="9fa1f-143">No limits on the number of semaphores</span></span>
* <span data-ttu-id="9fa1f-144">32 bit sayma semaforları (0-4.294.967.295)</span><span class="sxs-lookup"><span data-stu-id="9fa1f-144">32-bit counting semaphores (0 to 4,294,967,295)</span></span>
* <span data-ttu-id="9fa1f-145">Tüketici üreticisini veya kaynak korumasını destekler</span><span class="sxs-lookup"><span data-stu-id="9fa1f-145">Supports consumer-producer or resource protection</span></span>
* <span data-ttu-id="9fa1f-146">Semafor kullanılamıyorsa isteğe bağlı iş parçacığının askıya alınması</span><span class="sxs-lookup"><span data-stu-id="9fa1f-146">Optional thread suspension when semaphore unavailable</span></span>
* <span data-ttu-id="9fa1f-147">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-147">Optional timeout on all suspension</span></span>
* <span data-ttu-id="9fa1f-148">Ana semafor API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-148">Main semaphore APIs include:</span></span>
  * <span data-ttu-id="9fa1f-149">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-149">tx_semaphore_create</span></span>
  * <span data-ttu-id="9fa1f-150">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-150">tx_semaphore_delete</span></span>
  * <span data-ttu-id="9fa1f-151">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fa1f-151">tx_semaphore_get</span></span>
  * <span data-ttu-id="9fa1f-152">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fa1f-152">tx_semaphore_put</span></span>
  * <span data-ttu-id="9fa1f-153">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fa1f-153">tx_semaphore_put_notify</span></span>
* <span data-ttu-id="9fa1f-154">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-154">Additional information and performance APIs</span></span>

### <a name="mutexes"></a><span data-ttu-id="9fa1f-155">Zaman Uyumu Sağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fa1f-155">Mutexes</span></span>

* <span data-ttu-id="9fa1f-156">Dinamik mutex oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-156">Dynamic mutex creation</span></span>
* <span data-ttu-id="9fa1f-157">Mutex sayısı için sınır yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-157">No limits on the number of mutexes</span></span>
* <span data-ttu-id="9fa1f-158">İç içe kaynak koruması desteği</span><span class="sxs-lookup"><span data-stu-id="9fa1f-158">Nested resource protection supported</span></span>
* <span data-ttu-id="9fa1f-159">desteklenen isteğe bağlı öncelik devralma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-159">Optional priority inheritance supported</span></span>
* <span data-ttu-id="9fa1f-160">Mutex kullanılamıyorsa isteğe bağlı iş parçacığının askıya alınması</span><span class="sxs-lookup"><span data-stu-id="9fa1f-160">Optional thread suspension when mutex unavailable</span></span>
* <span data-ttu-id="9fa1f-161">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-161">Optional timeout on all suspension</span></span>
* <span data-ttu-id="9fa1f-162">Ana mutex API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-162">Main mutex APIs include:</span></span>
  * <span data-ttu-id="9fa1f-163">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-163">tx_mutex_create</span></span>
  * <span data-ttu-id="9fa1f-164">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-164">tx_mutex_delete</span></span>
  * <span data-ttu-id="9fa1f-165">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fa1f-165">tx_mutex_get</span></span>
  * <span data-ttu-id="9fa1f-166">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fa1f-166">tx_mutex_put</span></span>
* <span data-ttu-id="9fa1f-167">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-167">Additional information and performance APIs</span></span>

### <a name="event-flags"></a><span data-ttu-id="9fa1f-168">Olay Bayrakları</span><span class="sxs-lookup"><span data-stu-id="9fa1f-168">Event Flags</span></span>

* <span data-ttu-id="9fa1f-169">Dinamik olay bayrağı grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-169">Dynamic event flag group creation</span></span>
* <span data-ttu-id="9fa1f-170">Olay bayrağı gruplarının sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-170">No limits on the number of event flag groups</span></span>
* <span data-ttu-id="9fa1f-171">Bir iş parçacığını veya birden çok iş parçacığını eşitleme</span><span class="sxs-lookup"><span data-stu-id="9fa1f-171">Synchronization of one thread or multiple threads</span></span>
* <span data-ttu-id="9fa1f-172">Atomik get ve clear desteği</span><span class="sxs-lookup"><span data-stu-id="9fa1f-172">Atomic get and clear supported</span></span>
* <span data-ttu-id="9fa1f-173">AND/OR olay kümesi üzerinde isteğe bağlı çok iş parçacıklı askıya alma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-173">Optional multithread suspension on AND/OR set of events</span></span>
* <span data-ttu-id="9fa1f-174">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-174">Optional timeout on all suspension</span></span>
* <span data-ttu-id="9fa1f-175">Ana olay bayrağı API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-175">Main event flag APIs include:</span></span>
  * <span data-ttu-id="9fa1f-176">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-176">tx_event_flags_create</span></span>
  * <span data-ttu-id="9fa1f-177">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-177">tx_event_flags_delete</span></span>
  * <span data-ttu-id="9fa1f-178">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fa1f-178">tx_event_flags_get</span></span>
  * <span data-ttu-id="9fa1f-179">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fa1f-179">tx_event_flags_set</span></span>
  * <span data-ttu-id="9fa1f-180">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fa1f-180">tx_event_flags_set_notify</span></span>
* <span data-ttu-id="9fa1f-181">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-181">Additional information and performance APIs</span></span>

### <a name="block-memory-pools"></a><span data-ttu-id="9fa1f-182">Bellek Havuzlarını Engelleme</span><span class="sxs-lookup"><span data-stu-id="9fa1f-182">Block Memory Pools</span></span>

* <span data-ttu-id="9fa1f-183">Dinamik blok havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-183">Dynamic block pool creation</span></span>
* <span data-ttu-id="9fa1f-184">Blok havuzu sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-184">No limits on the number of block pools</span></span>
* <span data-ttu-id="9fa1f-185">Sabit boyutlu blokların veya havuzun boyutuyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-185">No limits on size of fixed-size blocks or size of pool</span></span>
* <span data-ttu-id="9fa1f-186">Mümkün olan en hızlı bellek ayırma/anlaşma konumu</span><span class="sxs-lookup"><span data-stu-id="9fa1f-186">Fastest possible memory allocation/deal-location</span></span>
* <span data-ttu-id="9fa1f-187">Boş havuzda isteğe bağlı iş parçacığının askıya alınması</span><span class="sxs-lookup"><span data-stu-id="9fa1f-187">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="9fa1f-188">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-188">Optional timeout on all suspension</span></span>
* <span data-ttu-id="9fa1f-189">Ana blok havuzu API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-189">Main block pool APIs include:</span></span>
  * <span data-ttu-id="9fa1f-190">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-190">tx_block_pool_create</span></span>
  * <span data-ttu-id="9fa1f-191">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-191">tx_block_pool_delete</span></span>
  * <span data-ttu-id="9fa1f-192">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fa1f-192">tx_block_allocate</span></span>
  * <span data-ttu-id="9fa1f-193">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fa1f-193">tx_block_release</span></span>
* <span data-ttu-id="9fa1f-194">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-194">Additional information and performance APIs</span></span>

### <a name="byte-memory-pools"></a><span data-ttu-id="9fa1f-195">Byte Memory Pools</span><span class="sxs-lookup"><span data-stu-id="9fa1f-195">Byte Memory Pools</span></span>

* <span data-ttu-id="9fa1f-196">Dinamik byte havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-196">Dynamic byte pool creation</span></span>
* <span data-ttu-id="9fa1f-197">Byte havuzlarının sayısına sınırlama yoktur</span><span class="sxs-lookup"><span data-stu-id="9fa1f-197">No limits on the number of byte pools</span></span>
* <span data-ttu-id="9fa1f-198">Byte havuzunun boyutuyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-198">No limits on size of byte pool</span></span>
* <span data-ttu-id="9fa1f-199">En esnek değişken uzunluklu bellek ayırma/ayırma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-199">Most flexible variable-length memory allocation/deallocation</span></span>
* <span data-ttu-id="9fa1f-200">Ayırma boyutu yerelliği destekle</span><span class="sxs-lookup"><span data-stu-id="9fa1f-200">Allocation size locality supported</span></span>
* <span data-ttu-id="9fa1f-201">Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-201">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="9fa1f-202">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-202">Optional timeout on all suspension</span></span>
* <span data-ttu-id="9fa1f-203">Ana bayt havuzu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-203">Main byte pool APIs include:</span></span>
  * <span data-ttu-id="9fa1f-204">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-204">tx_byte_pool_create</span></span>
  * <span data-ttu-id="9fa1f-205">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-205">tx_byte_pool_delete</span></span>
  * <span data-ttu-id="9fa1f-206">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fa1f-206">tx_byte_allocate</span></span>
  * <span data-ttu-id="9fa1f-207">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fa1f-207">tx_byte_release</span></span>
* <span data-ttu-id="9fa1f-208">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-208">Additional information and performance APIs</span></span>

### <a name="application-timers"></a><span data-ttu-id="9fa1f-209">Uygulama zamanlayıcıları</span><span class="sxs-lookup"><span data-stu-id="9fa1f-209">Application Timers</span></span>

* <span data-ttu-id="9fa1f-210">Dinamik süreölçer oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-210">Dynamic timer creation</span></span>
* <span data-ttu-id="9fa1f-211">Zamanlayıcılar sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="9fa1f-211">No limits on the number of timers</span></span>
* <span data-ttu-id="9fa1f-212">Düzenli veya tek atışı Zamanlayıcı destekleniyor</span><span class="sxs-lookup"><span data-stu-id="9fa1f-212">Periodic or one-shot timers supported</span></span>
* <span data-ttu-id="9fa1f-213">Düzenli zamanlayıcılar farklı başlangıç son kullanma değerine sahip olabilir</span><span class="sxs-lookup"><span data-stu-id="9fa1f-213">Periodic timers may have different initial expiration value</span></span>
* <span data-ttu-id="9fa1f-214">Süreölçer etkinleştirme veya devre dışı bırakma üzerinde arama yok</span><span class="sxs-lookup"><span data-stu-id="9fa1f-214">No searching on timer activation or deactivation</span></span>
* <span data-ttu-id="9fa1f-215">Bir donanım Zamanlayıcı kesmesinin yönettiği tüm zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fa1f-215">All timers driven from one hardware timer interrupt</span></span>
* <span data-ttu-id="9fa1f-216">Ana Zamanlayıcı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-216">Main timer APIs include:</span></span>
  * <span data-ttu-id="9fa1f-217">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fa1f-217">tx_timer_create</span></span>
  * <span data-ttu-id="9fa1f-218">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fa1f-218">tx_timer_delete</span></span>
  * <span data-ttu-id="9fa1f-219">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fa1f-219">tx_timer_activate</span></span>
  * <span data-ttu-id="9fa1f-220">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fa1f-220">tx_timer_change</span></span>
  * <span data-ttu-id="9fa1f-221">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fa1f-221">tx_timer_deactivate</span></span>
* <span data-ttu-id="9fa1f-222">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-222">Additional information and performance APIs</span></span>

### <a name="azure-rtos-threadx-core-scheduler"></a><span data-ttu-id="9fa1f-223">Azure RTOS ThreadX çekirdek Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-223">Azure RTOS ThreadX Core Scheduler</span></span>

* <span data-ttu-id="9fa1f-224">Minimum 2 KB FLASH, 1KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-224">Minimal 2KB FLASH,1KB RAM footprint</span></span>
* <span data-ttu-id="9fa1f-225">Fast, Sub-mikro ikinci bağlam-anahtar</span><span class="sxs-lookup"><span data-stu-id="9fa1f-225">Fast, sub-microsecond context-switch</span></span>
* <span data-ttu-id="9fa1f-226">İş parçacığı sayısından bağımsız olarak tam belirleyici</span><span class="sxs-lookup"><span data-stu-id="9fa1f-226">Fully deterministic regardless of number of threads</span></span>
* <span data-ttu-id="9fa1f-227">Öncelik temelli, tam preemptive-zamanlama</span><span class="sxs-lookup"><span data-stu-id="9fa1f-227">Priority-based, fully preemptive-scheduling</span></span>
* <span data-ttu-id="9fa1f-228">32 varsayılan öncelik düzeyleri, isteğe bağlı olarak 1024 düzeye kadar</span><span class="sxs-lookup"><span data-stu-id="9fa1f-228">32 default priority levels, optionally up to 1024 levels</span></span>
* <span data-ttu-id="9fa1f-229">Öncelik düzeyi (FıFO) içinde ortak zamanlama</span><span class="sxs-lookup"><span data-stu-id="9fa1f-229">Cooperative scheduling within priority level (FIFO)</span></span>
* <span data-ttu-id="9fa1f-230">Önalım-Threshold teknolojisi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-230">Preemption-threshold technology</span></span>
* <span data-ttu-id="9fa1f-231">Aşağıdakiler dahil isteğe bağlı Zamanlayıcı Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-231">Optional timer services, including:</span></span>
  * <span data-ttu-id="9fa1f-232">İş parçacığı başına isteğe bağlı saat dilimi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-232">Per-thread optional time-slice</span></span>
  * <span data-ttu-id="9fa1f-233">Tüm engellemede isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-233">Optional timeout on all blocking</span></span>
  * <span data-ttu-id="9fa1f-234">API 'Ler donanım süreölçer kesmesi gerektirir</span><span class="sxs-lookup"><span data-stu-id="9fa1f-234">APIs Requires on hardware timer interrupt</span></span>
* <span data-ttu-id="9fa1f-235">Yürütme profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-235">Execution profiling</span></span>
* <span data-ttu-id="9fa1f-236">Sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="9fa1f-236">System-level Trace</span></span>
* <span data-ttu-id="9fa1f-237">Birçok standartlara yönelik güvenlik sertifikalı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-237">Safety certified to many standards</span></span>

## <a name="most-deployed-rtos"></a><span data-ttu-id="9fa1f-238">En çok dağıtılan RTOS</span><span class="sxs-lookup"><span data-stu-id="9fa1f-238">Most deployed RTOS</span></span>

<span data-ttu-id="9fa1f-239">Azure RTOS ThreadX, önde gelen 'U M2M Market Intelligence firması, VDC Research 'e göre dünya genelinde 6.200.000.000 dağıtımlara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-239">Azure RTOS ThreadX has over 6.2 billion deployments worldwide, according to the leading M2M market intelligence firm, VDC Research.</span></span> <span data-ttu-id="9fa1f-240">Azure RTOS ThreadX 'in popülerliği, güvenilirliği, kalitesi, boyutu, performansı, gelişmiş özellikler, kullanım kolaylığı ve genel kullanım süresi avantajına yönelik bir testdir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-240">The popularity of Azure RTOS ThreadX is a testament to its reliability, quality, size, performance, advanced features, ease-of-use, and overall time-to-market advantages.</span></span>

> <span data-ttu-id="9fa1f-241">*"Şirketin temelleri ile bu yana kablosuz ve IoT pazarlarında THREADX 'in büyüme tratrumuzu izliyoruz ve THREADX 'in yaygın sektör benimsemesi tarafından giderek daha da artmaktadır."*</span><span class="sxs-lookup"><span data-stu-id="9fa1f-241">*“We have followed the growth trajectory of THREADX in the wireless and IoT markets since the company’s founding, and are increasingly impressed by the widespread industry adoption of THREADX.”*</span></span> <span data-ttu-id="9fa1f-242">– Chris Rommel, Executive Başkan Yardımcısı, VDC Research</span><span class="sxs-lookup"><span data-stu-id="9fa1f-242">– Chris Rommel, Executive Vice President, VDC Research</span></span>

## <a name="small-footprint"></a><span data-ttu-id="9fa1f-243">Küçük ayak izi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-243">Small footprint</span></span>

<span data-ttu-id="9fa1f-244">Azure RTOS ThreadX, en az bir kaplama için remarkalı küçük 2KB yönerge alanı ve 1KB RAM gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-244">Azure RTOS ThreadX requires a remarkably small 2KB instruction area and 1KB of RAM for its minimal footprint.</span></span> <span data-ttu-id="9fa1f-245">Bu, büyük bir olasılıkla katmanlı olmayan picokernel™ mimarisi ve otomatik ölçeklendirmesinden kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-245">This is largely due to its non-layered picokernel™ architecture and automatic scaling.</span></span> <span data-ttu-id="9fa1f-246">Otomatik ölçeklendirme, uygulama tarafından kullanılan hizmetlerin (ve destekleyici altyapının) bağlantı zamanında son görüntüye dahil olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-246">Automatic scaling means that only the services (and supporting infrastructure) used by the application are included in the final image at link time.</span></span>

<span data-ttu-id="9fa1f-247">Bazı tipik Azure RTOS ThreadX boyut özellikleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-247">Here are some typical Azure RTOS ThreadX size characteristics.</span></span>

|<span data-ttu-id="9fa1f-248">Azure RTOS ThreadX hizmeti</span><span class="sxs-lookup"><span data-stu-id="9fa1f-248">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="9fa1f-249">Bayt cinsinden normal boyut</span><span class="sxs-lookup"><span data-stu-id="9fa1f-249">Typical Size in Bytes</span></span>  |
|---------|---------|
|<span data-ttu-id="9fa1f-250">Çekirdek hizmetler (gerekli)</span><span class="sxs-lookup"><span data-stu-id="9fa1f-250">Core Services (Require)</span></span> |<span data-ttu-id="9fa1f-251">2.000</span><span class="sxs-lookup"><span data-stu-id="9fa1f-251">2,000</span></span>  |
|<span data-ttu-id="9fa1f-252">Kuyruk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-252">Queue Services</span></span>  |<span data-ttu-id="9fa1f-253">900</span><span class="sxs-lookup"><span data-stu-id="9fa1f-253">900</span></span>  |
|<span data-ttu-id="9fa1f-254">Olay bayrağı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-254">Event Flag Services</span></span>  |<span data-ttu-id="9fa1f-255">900</span><span class="sxs-lookup"><span data-stu-id="9fa1f-255">900</span></span>  |
|<span data-ttu-id="9fa1f-256">Semafor Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-256">Semaphore Services</span></span>  |<span data-ttu-id="9fa1f-257">450</span><span class="sxs-lookup"><span data-stu-id="9fa1f-257">450</span></span>  |
|<span data-ttu-id="9fa1f-258">Mutex Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-258">Mutex Services</span></span>  |<span data-ttu-id="9fa1f-259">1.200</span><span class="sxs-lookup"><span data-stu-id="9fa1f-259">1,200</span></span>  |
|<span data-ttu-id="9fa1f-260">Bellek hizmetlerini engelle</span><span class="sxs-lookup"><span data-stu-id="9fa1f-260">Block Memory Services</span></span>  |<span data-ttu-id="9fa1f-261">550</span><span class="sxs-lookup"><span data-stu-id="9fa1f-261">550</span></span>  |
|<span data-ttu-id="9fa1f-262">Bayt bellek Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-262">Byte Memory Services</span></span>  |<span data-ttu-id="9fa1f-263">900</span><span class="sxs-lookup"><span data-stu-id="9fa1f-263">900</span></span>  |

## <a name="fast-execution"></a><span data-ttu-id="9fa1f-264">Hızlı yürütme</span><span class="sxs-lookup"><span data-stu-id="9fa1f-264">Fast execution</span></span>

<span data-ttu-id="9fa1f-265">Azure RTOS ThreadX, en popüler işlemciler üzerinde bir alt mikro ikinci bağlam anahtarına erişir ve diğer ticari ortamlarından çok daha hızlı bir şekilde genel olarak daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-265">Azure RTOS ThreadX achieves a sub-microsecond context switch on most popular processors and is significantly faster overall than other commercial RTOSes.</span></span> <span data-ttu-id="9fa1f-266">Hızlı olmasının yanı sıra Azure RTOS ThreadX de oldukça belirleyici bir niteliğindedir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-266">In addition to being fast, Azure RTOS ThreadX is also highly deterministic.</span></span> <span data-ttu-id="9fa1f-267">Yalnızca bir tane veya tek bir 200 iş parçacığı olup olmadığı için aynı hızlı performansa erişir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-267">It achieves the same fast performance whether there are 200 threads ready, or just one.</span></span>

<span data-ttu-id="9fa1f-268">Azure RTOS ThreadX 'in bazı tipik performans özellikleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-268">Here are some typical performance characteristics of Azure RTOS ThreadX:</span></span>

* <span data-ttu-id="9fa1f-269">Hızlı önyükleme: 120 ' den az Döngülerde Azure RTOS ThreadX önyüklemeleri.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-269">Fast Boot: Azure RTOS ThreadX boots in less than 120 cycles.</span></span>
* <span data-ttu-id="9fa1f-270">Temel hata denetimi için isteğe bağlı kaldırma: temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-270">Optional Removal of basic error checking: Basic Azure RTOS ThreadX error checking can be skipped at compile time.</span></span> <span data-ttu-id="9fa1f-271">Bu, uygulama kodu doğrulandığında ve her parametreye artık hata denetimi gerektirmeyen yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-271">This can be useful when the application code is verified and no longer requires error checking on each parameter.</span></span> <span data-ttu-id="9fa1f-272">Bunun, sistem genelinde değil, bir derleme birimi üzerinde yapılabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-272">Note that this can be done on a compilation unit, rather than system-wide.</span></span>
* <span data-ttu-id="9fa1f-273">Picokernel™ tasarımı: hizmetler birbirlerine katmanlı değildir, bu nedenle gereksiz işlev çağrısı yükünü ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-273">Picokernel™ Design: Services are not layered on each other, thus eliminating unnecessary function call overhead.</span></span>
* <span data-ttu-id="9fa1f-274">\* İyileştirilmiş kesme Işleme: önalım gerekli değilse, yalnızca karalama kayıtları ıSR girdisi/çıkış üzerine kaydedilir/geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-274">\*Optimized Interrupt Processing: Only scratch registers are saved/restored upon ISR entry/exit, unless preemption is necessary.</span></span>
* <span data-ttu-id="9fa1f-275">İyileştirilmiş API Işleme:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-275">Optimized API Processing:</span></span>

    |<span data-ttu-id="9fa1f-276">Azure RTOS ThreadX hizmeti</span><span class="sxs-lookup"><span data-stu-id="9fa1f-276">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="9fa1f-277">Mikrosaniye cinsinden Hizmet Süresi \*</span><span class="sxs-lookup"><span data-stu-id="9fa1f-277">Service Time in Microseconds\*</span></span>  |
    |---------|---------|
    |<span data-ttu-id="9fa1f-278">İş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-278">Thread Suspend</span></span>  |<span data-ttu-id="9fa1f-279">0.6</span><span class="sxs-lookup"><span data-stu-id="9fa1f-279">0.6</span></span>  |
    |<span data-ttu-id="9fa1f-280">İş parçacığı özgeçmişi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-280">Thread Resume</span></span>  |<span data-ttu-id="9fa1f-281">0.6</span><span class="sxs-lookup"><span data-stu-id="9fa1f-281">0.6</span></span>  |
    |<span data-ttu-id="9fa1f-282">Kuyruğu gönder</span><span class="sxs-lookup"><span data-stu-id="9fa1f-282">Queue Send</span></span>  |<span data-ttu-id="9fa1f-283">0.3</span><span class="sxs-lookup"><span data-stu-id="9fa1f-283">0.3</span></span>  |
    |<span data-ttu-id="9fa1f-284">Kuyruk alma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-284">Queue Receive</span></span>  |<span data-ttu-id="9fa1f-285">0.3</span><span class="sxs-lookup"><span data-stu-id="9fa1f-285">0.3</span></span>  |
    |<span data-ttu-id="9fa1f-286">Semafor al</span><span class="sxs-lookup"><span data-stu-id="9fa1f-286">Get Semaphore</span></span>  |<span data-ttu-id="9fa1f-287">0,2</span><span class="sxs-lookup"><span data-stu-id="9fa1f-287">0.2</span></span>  |
    |<span data-ttu-id="9fa1f-288">Semaforu koy</span><span class="sxs-lookup"><span data-stu-id="9fa1f-288">Put Semaphore</span></span>  |<span data-ttu-id="9fa1f-289">0,2</span><span class="sxs-lookup"><span data-stu-id="9fa1f-289">0.2</span></span>  |
    |<span data-ttu-id="9fa1f-290">Bağlam anahtarı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-290">Context Switch</span></span>  |<span data-ttu-id="9fa1f-291">0,4</span><span class="sxs-lookup"><span data-stu-id="9fa1f-291">0.4</span></span>  |
    |<span data-ttu-id="9fa1f-292">Kesme yanıtı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-292">Interrupt Response</span></span>  |<span data-ttu-id="9fa1f-293">0,0 – 0,6</span><span class="sxs-lookup"><span data-stu-id="9fa1f-293">0.0 – 0.6</span></span>  |

    <span data-ttu-id="9fa1f-294">\**200 MHz hızında çalışan normal işlemciyi temel alan performans rakamları*.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-294">\**Performance figures based on typical processor running at 200MHz*.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="9fa1f-295">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="9fa1f-295">Advanced technology</span></span>

<span data-ttu-id="9fa1f-296">Azure RTOS ThreadX, en önemli özelliği önalım-Threshold zamanlaması olan gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-296">Azure RTOS ThreadX is advanced technology whose most notable feature is preemption-threshold scheduling.</span></span> <span data-ttu-id="9fa1f-297">Bu özellik Azure RTOS ThreadX için benzersizdir ve kapsamlı akademik araştırma konusu.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-297">This feature is unique to Azure RTOS ThreadX and has been the subject of extensive academic research.</span></span> <span data-ttu-id="9fa1f-298">Örneğin, bkz. [önalım Threshold ile Fixed-Priority görevleri zamanlama](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), Yıun Wang, Concorçya University ve Manas Saksena, tas haburi Üniversitesi.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-298">For example, see [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), by Yun Wang, Concordia University, and Manas Saksena, University of Pittsburgh.</span></span>

<span data-ttu-id="9fa1f-299">Azure RTOS ThreadX 'in yeteneklerini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-299">Consider the capabilities of Azure RTOS ThreadX.</span></span>

* <span data-ttu-id="9fa1f-300">Eksiksiz ve kapsamlı çoklu görev olanakları</span><span class="sxs-lookup"><span data-stu-id="9fa1f-300">Complete and Comprehensive Multitasking Facilities</span></span>
  * <span data-ttu-id="9fa1f-301">İş parçacıkları, uygulama süreçleri, ileti kuyrukları, semaforları sayma, mutex'ler, olay bayrakları, blok ve byte bellek havuzları</span><span class="sxs-lookup"><span data-stu-id="9fa1f-301">Threads, application timers, message queues, counting semaphores, mutexes, event flags, block and byte memory pools</span></span>
* <span data-ttu-id="9fa1f-302">Priority-Based Ön Zamanlama</span><span class="sxs-lookup"><span data-stu-id="9fa1f-302">Priority-Based Preemptive Scheduling</span></span>
* <span data-ttu-id="9fa1f-303">Öncelik Esnekliği – En fazla 1024 Öncelik Düzeyi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-303">Priority Flexibility – Up to 1024 Priority Levels</span></span>
* <span data-ttu-id="9fa1f-304">İşbirlikçi Zamanlama</span><span class="sxs-lookup"><span data-stu-id="9fa1f-304">Cooperative Scheduling</span></span>
* <span data-ttu-id="9fa1f-305">Preemption-Threshold™ – Azure RTOS ThreadX'e özeldir, bağlam geçişlerini azaltmaya ve zamanlanabilirliği garanti etmeye yardımcı olur (akademik araştırma başına)</span><span class="sxs-lookup"><span data-stu-id="9fa1f-305">Preemption-Threshold™ – Unique to Azure RTOS ThreadX, helps reduce context switches and help guarantee schedulability (per academic research)</span></span>
* <span data-ttu-id="9fa1f-306">Azure RTOS ThreadX MODULES aracılığıyla Bellek Koruması</span><span class="sxs-lookup"><span data-stu-id="9fa1f-306">Memory Protection via Azure RTOS ThreadX MODULES</span></span>
* <span data-ttu-id="9fa1f-307">Tam Belirleyici</span><span class="sxs-lookup"><span data-stu-id="9fa1f-307">Fully Deterministic</span></span>
* <span data-ttu-id="9fa1f-308">Olay İzleme – Son *n sistem/uygulama* olaylarını yakalama</span><span class="sxs-lookup"><span data-stu-id="9fa1f-308">Event Trace – Capture last *n* system/application events</span></span>
* <span data-ttu-id="9fa1f-309">Olay Zincirleme™ – ThreadX iletişimini veya eşitleme nesnesini her bir Azure RTOS uygulamaya özgü "notify" geri çağırma işlevini kaydetme</span><span class="sxs-lookup"><span data-stu-id="9fa1f-309">Event Chaining™ – Register an application-specific “notify” callback function for each Azure RTOS ThreadX communication or synchronization object</span></span>
* <span data-ttu-id="9fa1f-310">Azure RTOS İsteğe Bağlı Bellek Koruması ile ThreadX MODÜLLERI</span><span class="sxs-lookup"><span data-stu-id="9fa1f-310">Azure RTOS ThreadX MODULES with Optional Memory Protection</span></span>
* <span data-ttu-id="9fa1f-311">Run-Time Performans Ölçümleri</span><span class="sxs-lookup"><span data-stu-id="9fa1f-311">Run-Time Performance Metrics</span></span>
  * <span data-ttu-id="9fa1f-312">İş parçacığı yeniden dizilerinin sayısı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-312">Number of thread resumptions</span></span>
  * <span data-ttu-id="9fa1f-313">İş parçacığı askıya alma sayısı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-313">Number of thread suspensions</span></span>
  * <span data-ttu-id="9fa1f-314">İstenen iş parçacığı önhizmelerinin sayısı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-314">Number of solicited thread preemptions</span></span>
  * <span data-ttu-id="9fa1f-315">Zaman uyumsuz iş parçacığı kesme önemptions sayısı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-315">Number of asynchronous thread interrupt preemptions</span></span>
  * <span data-ttu-id="9fa1f-316">İş parçacığı öncelik ters çevirme sayısı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-316">Number of thread priority inversions</span></span>
  * <span data-ttu-id="9fa1f-317">İş parçacığı ilinquishes sayısı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-317">Number of thread relinquishes</span></span>
* <span data-ttu-id="9fa1f-318">Yürütme Profili Seti (EPK)</span><span class="sxs-lookup"><span data-stu-id="9fa1f-318">Execution Profile Kit (EPK)</span></span>
* <span data-ttu-id="9fa1f-319">Kesme Yığınını Ayırma</span><span class="sxs-lookup"><span data-stu-id="9fa1f-319">Separate Interrupt Stack</span></span>
* <span data-ttu-id="9fa1f-320">Run-Time Yığını Analizi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-320">Run-Time Stack Analysis</span></span>
* <span data-ttu-id="9fa1f-321">Zamanlayıcı Kesme İşleme İyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="9fa1f-321">Optimized Timer Interrupt Processing</span></span>

## <a name="multicore-support-amp--smp"></a><span data-ttu-id="9fa1f-322">Çok çekirdekli destek (AMP & SMP)</span><span class="sxs-lookup"><span data-stu-id="9fa1f-322">Multicore support (AMP & SMP)</span></span>

<span data-ttu-id="9fa1f-323">Standart Azure RTOS ThreadX genellikle ayrı bir Azure RTOS ThreadX kopyasının ve uygulamanın (veya Linux'ın) her çekirdekte yürütülür ve paylaşılan bellek veya OpenAMP gibi bir işlemciler arası iletişim mekanizması aracılığıyla birbirleriyle iletişim kurarak OpenAMP (Azure RTOS ThreadX OpenAMP'ı destekler) asimetrik Çok İşlemcili (AMP) bir şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-323">Standard Azure RTOS ThreadX is often used in an Asymmetric Multiprocessing (AMP) fashion, where a separate copy of Azure RTOS ThreadX and the application (or Linux) execute on each core and communicate with each other via shared memory or an inter-processor communication mechanism such as OpenAMP (Azure RTOS ThreadX supports OpenAMP).</span></span> <span data-ttu-id="9fa1f-324">Bu, Azure RTOS ThreadX kullanan en tipik çok çekirdekli yapılandırmadır ve uygulama işlemcileri etkili bir şekilde yükleyene kadar en verimli yapılandırma olabilir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-324">This is the most typical multicore configuration using Azure RTOS ThreadX and can be the most efficient if the application is able to effectively load the processors.</span></span>

<span data-ttu-id="9fa1f-325">İşlemcileri yüklemenin yüksek oranda dinamik olduğu ortamlar için Azure RTOS ThreadX Symetric Multiprocessing (SMP) aşağıdaki işlemci aileleri için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-325">For environments where loading the processors is highly dynamic, Azure RTOS ThreadX Symetric Multiprocessing (SMP) is available for the following processor families:</span></span>

* <span data-ttu-id="9fa1f-326">ARM Cortex-Ax</span><span class="sxs-lookup"><span data-stu-id="9fa1f-326">ARM Cortex-Ax</span></span>
* <span data-ttu-id="9fa1f-327">ARM Cortex-Rx</span><span class="sxs-lookup"><span data-stu-id="9fa1f-327">ARM Cortex-Rx</span></span>
* <span data-ttu-id="9fa1f-328">ARM Cortex-A5x 64 bit</span><span class="sxs-lookup"><span data-stu-id="9fa1f-328">ARM Cortex-A5x 64-bit</span></span>
* <span data-ttu-id="9fa1f-329">MIPS 34K, 1004K ve interAptiv</span><span class="sxs-lookup"><span data-stu-id="9fa1f-329">MIPS 34K, 1004K, and interAptiv</span></span>
* <span data-ttu-id="9fa1f-330">PowerPC</span><span class="sxs-lookup"><span data-stu-id="9fa1f-330">PowerPC</span></span>
* <span data-ttu-id="9fa1f-331">Özet ARC HS</span><span class="sxs-lookup"><span data-stu-id="9fa1f-331">Synopsys ARC HS</span></span>
* <span data-ttu-id="9fa1f-332">x86</span><span class="sxs-lookup"><span data-stu-id="9fa1f-332">x86</span></span>

<span data-ttu-id="9fa1f-333">Azure RTOS ThreadX *SMP, n* işlemci arasında dinamik yük dengeleme gerçekleştirir ve tüm Azure RTOS ThreadX kaynaklarına (kuyruklar, semaforlar, olay bayrakları, bellek havuzları vb.) herhangi bir çekirdek üzerindeki herhangi bir iş parçacığı tarafından erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-333">Azure RTOS ThreadX SMP performs dynamic load balancing across *n* processors and allows all Azure RTOS ThreadX resources (queues, semaphores, event flags, memory pools, etc.) to be accessed by any thread on any core.</span></span> <span data-ttu-id="9fa1f-334">Azure RTOS ThreadX SMP, tüm çekirdeklerde Azure RTOS ThreadX API'sini tam olarak sağlar ve aşağıdaki yeni API'nin SMP işlemi için geçerli olduğunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-334">Azure RTOS ThreadX SMP enables the complete Azure RTOS ThreadX API on all cores and introduces the following new API’s applicable to SMP operation:</span></span>

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a><span data-ttu-id="9fa1f-335">Azure RTOS ThreadX Modülleri aracılığıyla bellek koruması</span><span class="sxs-lookup"><span data-stu-id="9fa1f-335">Memory protection via Azure RTOS ThreadX Modules</span></span>

<span data-ttu-id="9fa1f-336">Azure RTOS ThreadX MODULES adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının dinamik olarak hedefte dinamik olarak yüklenemiyor ve çalıştırılana (veya yerinde yürütülebilir) bir "Modül" içinde paketlenesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-336">An add-on product called Azure RTOS ThreadX MODULES enables one or more application threads to be bundled into a “Module” that can be dynamically loaded and run (or executed in place) on the target.</span></span>

<span data-ttu-id="9fa1f-337">Modüller, büyük uygulamaların yalnızca etkin iş parçacıklarının ihtiyaç sahip olduğu belleği kaplayacak şekilde alan yükseltme, hata düzeltme ve program bölümlelene olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-337">Modules enable field upgrade, bug fixing, and program partitioning to allow large applications to occupy only the memory needed by active threads.</span></span>

<span data-ttu-id="9fa1f-338">Ayrıca modüller, ThreadX'in kendi kendine Azure RTOS adres alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-338">Modules also have a completely separate address space from Azure RTOS ThreadX itself.</span></span> <span data-ttu-id="9fa1f-339">Bu Azure RTOS ThreadX'in Modül'e bellek koruması (MPU veya MMU aracılığıyla) yüklemesini sağlar; böylece modülün dışından yanlışlıkla erişim başka bir yazılım bileşenini bozmaz.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-339">This enables Azure RTOS ThreadX to place memory protection (via MPU or MMU) around the Module such that accidental access outside the module will not be able to corrupt any other software component.</span></span>

## <a name="misra-compliant"></a><span data-ttu-id="9fa1f-340">MISRA uyumlu</span><span class="sxs-lookup"><span data-stu-id="9fa1f-340">MISRA compliant</span></span>

<span data-ttu-id="9fa1f-341">Azure RTOS ThreadX ve Azure RTOS ThreadX SMP souce kodu MISRA-C:2004 ve MISRA C:2012 ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-341">Azure RTOS ThreadX and Azure RTOS ThreadX SMP souce code is MISRA-C:2004 and MISRA C:2012 compliant.</span></span> <span data-ttu-id="9fa1f-342">MISRA C, C programlama dilini kullanan kritik sistemler için bir dizi programlama kılavuzudur.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-342">MISRA C is a set of programming guidelines for critical systems using the C programming language.</span></span> <span data-ttu-id="9fa1f-343">Özgün MISRA C yönergeleri öncelikli olarak otomotiv uygulamalarına yönelikti; ancak, MISRA C artık güvenlik açısından kritik herhangi bir uygulama için geçerli olduğu geniş ölçüde kabul ediliyor.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-343">The original MISRA C guidelines were primarily targeted toward automotive applications; however, MISRA C is now widely recognized as being applicable to any safety-critical application.</span></span> <span data-ttu-id="9fa1f-344">Azure RTOS ThreadX, MISRA-C:2004 ve MISRA C:2012'nin tüm gerekli ve zorunlu kurallarıyla uyumludur.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-344">Azure RTOS ThreadX is compliant with all required and mandatory rules of MISRA-C:2004 and MISRA C:2012.</span></span>

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Misra sertifikası":::

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="9fa1f-346">En popüler mimarileri destekler</span><span class="sxs-lookup"><span data-stu-id="9fa1f-346">Supports most popular architectures</span></span>

<span data-ttu-id="9fa1f-347">Azure RTOS ThreadX, en popüler 32/64 bit mikro işlemciler, hazır, tam olarak test edilmiş ve tam olarak desteklenen mikro işlemcilerde çalışır. Aşağıdakiler de dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="9fa1f-347">Azure RTOS ThreadX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

* <span data-ttu-id="9fa1f-348">Analog Cihazlar: SHARC, Blackfin, CM4xx</span><span class="sxs-lookup"><span data-stu-id="9fa1f-348">Analog Devices: SHARC, Blackfin, CM4xx</span></span>
* <span data-ttu-id="9fa1f-349">Andes Core: RISC-V</span><span class="sxs-lookup"><span data-stu-id="9fa1f-349">Andes Core: RISC-V</span></span>
* <span data-ttu-id="9fa1f-350">Ambiqmicro: Apollo MUS</span><span class="sxs-lookup"><span data-stu-id="9fa1f-350">Ambiqmicro: Apollo MCUs</span></span>
* <span data-ttu-id="9fa1f-351">ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="9fa1f-351">ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>
* <span data-ttu-id="9fa1f-352">Tempo: Xtensa, Diamond</span><span class="sxs-lookup"><span data-stu-id="9fa1f-352">Cadence: Xtensa, Diamond</span></span>
* <span data-ttu-id="9fa1f-353">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span><span class="sxs-lookup"><span data-stu-id="9fa1f-353">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>
* <span data-ttu-id="9fa1f-354">Cypress: RISC-V</span><span class="sxs-lookup"><span data-stu-id="9fa1f-354">Cypress: RISC-V</span></span>
* <span data-ttu-id="9fa1f-355">EnSilica: eSi-RISC</span><span class="sxs-lookup"><span data-stu-id="9fa1f-355">EnSilica: eSi-RISC</span></span>
* <span data-ttu-id="9fa1f-356">Infineon: XMC1000, XMC4000, TriCore</span><span class="sxs-lookup"><span data-stu-id="9fa1f-356">Infineon: XMC1000, XMC4000, TriCore</span></span>
* <span data-ttu-id="9fa1f-357">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span><span class="sxs-lookup"><span data-stu-id="9fa1f-357">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>
* <span data-ttu-id="9fa1f-358">Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="9fa1f-358">Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>
* <span data-ttu-id="9fa1f-359">Microsemi: RISC-V</span><span class="sxs-lookup"><span data-stu-id="9fa1f-359">Microsemi: RISC-V</span></span>
* <span data-ttu-id="9fa1f-360">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="9fa1f-360">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>
* <span data-ttu-id="9fa1f-361">Renesas: SH, HS, V850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="9fa1f-361">Renesas: SH, HS, V850, RX, RZ, Synergy</span></span>
* <span data-ttu-id="9fa1f-362">Silikon Laboratuvarları: EFM32</span><span class="sxs-lookup"><span data-stu-id="9fa1f-362">Silicon Labs: EFM32</span></span>
* <span data-ttu-id="9fa1f-363">Özetler: ARC 600, 700, ARC EM, ARC HS</span><span class="sxs-lookup"><span data-stu-id="9fa1f-363">Synopsys: ARC 600, 700, ARC EM, ARC HS</span></span>
* <span data-ttu-id="9fa1f-364">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="9fa1f-364">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>
* <span data-ttu-id="9fa1f-365">Tl: C5xxx, C6xxx,Xxxris, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="9fa1f-365">Tl: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>
* <span data-ttu-id="9fa1f-366">Dalga Bilişimi: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interApula, proAptiv, M Sınıfı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-366">Wave Computing: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>
* <span data-ttu-id="9fa1f-367">Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="9fa1f-367">Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

## <a name="supports-most-popular-tools"></a><span data-ttu-id="9fa1f-368">En popüler araçları destekler</span><span class="sxs-lookup"><span data-stu-id="9fa1f-368">Supports most popular tools</span></span>

<span data-ttu-id="9fa1f-369">Azure RTOS ThreadX, kullanılabilir en kapsamlı Azure RTOS ThreadX çekirdek farkındalığını da içeren IAR Embedded Workbench™ dahil olmak üzere en popüler tümleşik geliştirme araçlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-369">Azure RTOS ThreadX supports most popular embedded development tools, including IAR’s Embedded Workbench™, which also has the most comprehensive Azure RTOS ThreadX kernel awareness available.</span></span> <span data-ttu-id="9fa1f-370">Ek araç tümleştirmesi GNU (GCC), ARM DS-5/uVision®, Green Multi®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauteruter TRACE32®, TI Code-Composer Studio, CrossCore ve tüm analog cihazları içerir.</span><span class="sxs-lookup"><span data-stu-id="9fa1f-370">Additional tool integration includes GNU (GCC), ARM DS-5/uVision®, Green Hills MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer Studio, CrossCore and all analog devices.</span></span>

## <a name="adaptation-layer-for-threadx"></a><span data-ttu-id="9fa1f-371">ThreadX için uyarlama katmanı</span><span class="sxs-lookup"><span data-stu-id="9fa1f-371">Adaptation layer for ThreadX</span></span>

<span data-ttu-id="9fa1f-372">Azure RTOS ThreadX, özellikle sağlam bir şekilde eklenmiş uygulamalar için tasarlanan gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS).</span><span class="sxs-lookup"><span data-stu-id="9fa1f-372">Azure RTOS ThreadX is an advanced real-time operating system (RTOS) designed specifically for deeply embedded applications.</span></span> <span data-ttu-id="9fa1f-373">ThreadX, Auzre RTOS'a uygulama [](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) geçişini kolaylaştırmanıza yardımcı olmak için çeşitli eski RTOS API'leri (FreeRTOS, POSIX, OSEK vb.) için uyarlama katmanları sağlar</span><span class="sxs-lookup"><span data-stu-id="9fa1f-373">To help ease application migration to Auzre RTOS, ThreadX provides [adaption layers](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) for various legacy RTOS APIs (FreeRTOS, POSIX, OSEK, etc.)</span></span>
