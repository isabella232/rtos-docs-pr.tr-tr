---
title: Azure RTOS ThreadX 'i anlama
description: Azure ThreadX, özellikle derin eklenmiş uygulamalar için tasarlanan gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS).
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: e786e5bf1f434ec9543823dee8784b677a2b371f
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171395"
---
# <a name="overview-of-azure-rtos-threadx"></a><span data-ttu-id="98fda-103">Azure RTOS ThreadX 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="98fda-103">Overview of Azure RTOS ThreadX</span></span>

<span data-ttu-id="98fda-104">Azure RTOS ThreadX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft 'un gelişmiş endüstriyel sınıf Real-Time Işletim sistemidir (RTOS).</span><span class="sxs-lookup"><span data-stu-id="98fda-104">Azure RTOS ThreadX is Microsoft's advanced industrial grade Real-Time Operating System (RTOS) designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="98fda-105">Azure RTOS ThreadX, Gelişmiş zamanlama, iletişim, eşitleme, süreölçer, bellek yönetimi ve kesme yönetim olanakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="98fda-105">Azure RTOS ThreadX provides advanced scheduling, communication, synchronization, timer, memory management, and interrupt management facilities.</span></span> <span data-ttu-id="98fda-106">Ayrıca, Azure RTOS ThreadX 'in picokernel™ mimarisi, önalım-Threshold™ zamanlama, olay zincirleme,™ yürütme profili oluşturma, performans ölçümleri ve sistem olay izleme dahil birçok gelişmiş özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="98fda-106">In addition, Azure RTOS ThreadX has many advanced features, including its picokernel™ architecture, preemption-threshold™ scheduling, event-chaining,™ execution profiling, performance metrics, and system event tracing.</span></span> <span data-ttu-id="98fda-107">En üstün kullanım kolaylığıyla birlikte, Azure RTOS ThreadX, katıştırılmış uygulamaların en zorlu kullanımı için ideal seçenektir.</span><span class="sxs-lookup"><span data-stu-id="98fda-107">Combined with its superior ease-of-use, Azure RTOS ThreadX is the ideal choice for the most demanding of embedded applications.</span></span> <span data-ttu-id="98fda-108">2017 itibariyle, Azure RTOS ThreadX, tüketici cihazları, tıbbi elektronik ve endüstriyel denetim ekipmanı dahil olmak üzere çok çeşitli ürünlerde 6.200.000.000 ' den fazla dağıtıma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="98fda-108">As of 2017, Azure RTOS ThreadX has over 6.2 billion deployments, in a wide variety of products, including consumer devices, medical electronics, and industrial control equipment.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="98fda-109">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="98fda-109">API Protocols</span></span>

### <a name="azure-rtos-threadx-services"></a><span data-ttu-id="98fda-110">Azure RTOS ThreadX Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="98fda-110">Azure RTOS ThreadX Services</span></span>

* <span data-ttu-id="98fda-111">Dinamik iş parçacığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-111">Dynamic thread creation</span></span>
* <span data-ttu-id="98fda-112">İş parçacığı sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="98fda-112">No limits on the number of threads</span></span>
* <span data-ttu-id="98fda-113">Ana iş parçacığı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="98fda-113">Main thread APIs include:</span></span>
  * <span data-ttu-id="98fda-114">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="98fda-114">tx_thread_create</span></span>
  * <span data-ttu-id="98fda-115">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-115">tx_thread_delete</span></span>
  * <span data-ttu-id="98fda-116">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="98fda-116">tx_thread_preemption_change</span></span>
  * <span data-ttu-id="98fda-117">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="98fda-117">tx_thread_priority_change</span></span>
  * <span data-ttu-id="98fda-118">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="98fda-118">tx_thread_relinquish</span></span>
  * <span data-ttu-id="98fda-119">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="98fda-119">tx_thread_reset</span></span>
  * <span data-ttu-id="98fda-120">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="98fda-120">tx_thread_resume</span></span>
  * <span data-ttu-id="98fda-121">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="98fda-121">tx_thread_sleep</span></span>
  * <span data-ttu-id="98fda-122">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="98fda-122">tx_thread_suspend</span></span>
  * <span data-ttu-id="98fda-123">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="98fda-123">tx_thread_terminate</span></span>
  * <span data-ttu-id="98fda-124">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="98fda-124">tx_thread_wait_abort</span></span>
* <span data-ttu-id="98fda-125">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-125">Additional information and performance APIs</span></span>

### <a name="message-queues"></a><span data-ttu-id="98fda-126">İleti kuyrukları</span><span class="sxs-lookup"><span data-stu-id="98fda-126">Message Queues</span></span>

* <span data-ttu-id="98fda-127">Dinamik sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-127">Dynamic queue creation</span></span>
* <span data-ttu-id="98fda-128">Sıra sayısında sınırlama yoktur</span><span class="sxs-lookup"><span data-stu-id="98fda-128">No limits on the number of queues</span></span>
* <span data-ttu-id="98fda-129">Değer (veya işaretçi aracılığıyla başvuruya göre) tarafından kopyalanmış iletiler</span><span class="sxs-lookup"><span data-stu-id="98fda-129">Messages copied by value (or by reference via pointer)</span></span>
* <span data-ttu-id="98fda-130">1 ile 16 32 bitlik sözcüklerden oluşan ileti boyutları</span><span class="sxs-lookup"><span data-stu-id="98fda-130">Message sizes from 1 to 16 32-bit words</span></span>
* <span data-ttu-id="98fda-131">Empty ve Full üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="98fda-131">Optional thread suspension on empty and full</span></span>
* <span data-ttu-id="98fda-132">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="98fda-132">Optional timeout on all suspension</span></span>
* <span data-ttu-id="98fda-133">Ana ileti kuyruğu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="98fda-133">Main message queue APIs include:</span></span>
  * <span data-ttu-id="98fda-134">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="98fda-134">tx_queue_create</span></span>
  * <span data-ttu-id="98fda-135">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-135">tx_queue_delete</span></span>
  * <span data-ttu-id="98fda-136">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="98fda-136">tx_queue_flush</span></span>
  * <span data-ttu-id="98fda-137">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="98fda-137">tx_queue_front_send</span></span>
  * <span data-ttu-id="98fda-138">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="98fda-138">tx_queue_receive</span></span>
  * <span data-ttu-id="98fda-139">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="98fda-139">tx_queue_send_notify</span></span>
* <span data-ttu-id="98fda-140">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-140">Additional information and performance APIs</span></span>

### <a name="counting-semaphores"></a><span data-ttu-id="98fda-141">Semafor sayma</span><span class="sxs-lookup"><span data-stu-id="98fda-141">Counting Semaphores</span></span>

* <span data-ttu-id="98fda-142">Dinamik semafor oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-142">Dynamic semaphore creation</span></span>
* <span data-ttu-id="98fda-143">Semafor sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="98fda-143">No limits on the number of semaphores</span></span>
* <span data-ttu-id="98fda-144">32-bit sayma semaforları (0-4.294.967.295)</span><span class="sxs-lookup"><span data-stu-id="98fda-144">32-bit counting semaphores (0 to 4,294,967,295)</span></span>
* <span data-ttu-id="98fda-145">Tüketici-üretici veya kaynak korumasını destekler</span><span class="sxs-lookup"><span data-stu-id="98fda-145">Supports consumer-producer or resource protection</span></span>
* <span data-ttu-id="98fda-146">Semafor kullanılamadığında isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="98fda-146">Optional thread suspension when semaphore unavailable</span></span>
* <span data-ttu-id="98fda-147">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="98fda-147">Optional timeout on all suspension</span></span>
* <span data-ttu-id="98fda-148">Ana semafor API 'Leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="98fda-148">Main semaphore APIs include:</span></span>
  * <span data-ttu-id="98fda-149">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="98fda-149">tx_semaphore_create</span></span>
  * <span data-ttu-id="98fda-150">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-150">tx_semaphore_delete</span></span>
  * <span data-ttu-id="98fda-151">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="98fda-151">tx_semaphore_get</span></span>
  * <span data-ttu-id="98fda-152">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="98fda-152">tx_semaphore_put</span></span>
  * <span data-ttu-id="98fda-153">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="98fda-153">tx_semaphore_put_notify</span></span>
* <span data-ttu-id="98fda-154">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-154">Additional information and performance APIs</span></span>

### <a name="mutexes"></a><span data-ttu-id="98fda-155">Zaman Uyumu Sağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="98fda-155">Mutexes</span></span>

* <span data-ttu-id="98fda-156">Dinamik mutex oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-156">Dynamic mutex creation</span></span>
* <span data-ttu-id="98fda-157">Birbirini kapsamayan sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="98fda-157">No limits on the number of mutexes</span></span>
* <span data-ttu-id="98fda-158">İç içe kaynak koruması destekleniyor</span><span class="sxs-lookup"><span data-stu-id="98fda-158">Nested resource protection supported</span></span>
* <span data-ttu-id="98fda-159">İsteğe bağlı öncelikli devralma destekleniyor</span><span class="sxs-lookup"><span data-stu-id="98fda-159">Optional priority inheritance supported</span></span>
* <span data-ttu-id="98fda-160">Mutex kullanılamadığında isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="98fda-160">Optional thread suspension when mutex unavailable</span></span>
* <span data-ttu-id="98fda-161">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="98fda-161">Optional timeout on all suspension</span></span>
* <span data-ttu-id="98fda-162">Ana mutex API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="98fda-162">Main mutex APIs include:</span></span>
  * <span data-ttu-id="98fda-163">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="98fda-163">tx_mutex_create</span></span>
  * <span data-ttu-id="98fda-164">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-164">tx_mutex_delete</span></span>
  * <span data-ttu-id="98fda-165">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="98fda-165">tx_mutex_get</span></span>
  * <span data-ttu-id="98fda-166">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="98fda-166">tx_mutex_put</span></span>
* <span data-ttu-id="98fda-167">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-167">Additional information and performance APIs</span></span>

### <a name="event-flags"></a><span data-ttu-id="98fda-168">Olay bayrakları</span><span class="sxs-lookup"><span data-stu-id="98fda-168">Event Flags</span></span>

* <span data-ttu-id="98fda-169">Dinamik olay bayrağı Grup oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-169">Dynamic event flag group creation</span></span>
* <span data-ttu-id="98fda-170">Olay bayrak grupları sayısında sınırlama yok</span><span class="sxs-lookup"><span data-stu-id="98fda-170">No limits on the number of event flag groups</span></span>
* <span data-ttu-id="98fda-171">Bir iş parçacığının veya birden çok iş parçacığının eşitlenmesi</span><span class="sxs-lookup"><span data-stu-id="98fda-171">Synchronization of one thread or multiple threads</span></span>
* <span data-ttu-id="98fda-172">Atomik get ve Clear destekleniyor</span><span class="sxs-lookup"><span data-stu-id="98fda-172">Atomic get and clear supported</span></span>
* <span data-ttu-id="98fda-173">İsteğe bağlı çoklu iş parçacığı açma ve/veya olay kümesi askıya alma</span><span class="sxs-lookup"><span data-stu-id="98fda-173">Optional multithread suspension on AND/OR set of events</span></span>
* <span data-ttu-id="98fda-174">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="98fda-174">Optional timeout on all suspension</span></span>
* <span data-ttu-id="98fda-175">Ana olay bayrağı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="98fda-175">Main event flag APIs include:</span></span>
  * <span data-ttu-id="98fda-176">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="98fda-176">tx_event_flags_create</span></span>
  * <span data-ttu-id="98fda-177">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-177">tx_event_flags_delete</span></span>
  * <span data-ttu-id="98fda-178">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="98fda-178">tx_event_flags_get</span></span>
  * <span data-ttu-id="98fda-179">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="98fda-179">tx_event_flags_set</span></span>
  * <span data-ttu-id="98fda-180">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="98fda-180">tx_event_flags_set_notify</span></span>
* <span data-ttu-id="98fda-181">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-181">Additional information and performance APIs</span></span>

### <a name="block-memory-pools"></a><span data-ttu-id="98fda-182">Bellek havuzlarını engelle</span><span class="sxs-lookup"><span data-stu-id="98fda-182">Block Memory Pools</span></span>

* <span data-ttu-id="98fda-183">Dinamik blok havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-183">Dynamic block pool creation</span></span>
* <span data-ttu-id="98fda-184">Blok havuzları sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="98fda-184">No limits on the number of block pools</span></span>
* <span data-ttu-id="98fda-185">Sabit boyutlu blokların boyutu veya havuzun boyutu için sınır yok</span><span class="sxs-lookup"><span data-stu-id="98fda-185">No limits on size of fixed-size blocks or size of pool</span></span>
* <span data-ttu-id="98fda-186">En hızlı olası bellek ayırma/anlaşma konumu</span><span class="sxs-lookup"><span data-stu-id="98fda-186">Fastest possible memory allocation/deal-location</span></span>
* <span data-ttu-id="98fda-187">Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="98fda-187">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="98fda-188">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="98fda-188">Optional timeout on all suspension</span></span>
* <span data-ttu-id="98fda-189">Ana blok havuzu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="98fda-189">Main block pool APIs include:</span></span>
  * <span data-ttu-id="98fda-190">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="98fda-190">tx_block_pool_create</span></span>
  * <span data-ttu-id="98fda-191">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-191">tx_block_pool_delete</span></span>
  * <span data-ttu-id="98fda-192">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="98fda-192">tx_block_allocate</span></span>
  * <span data-ttu-id="98fda-193">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="98fda-193">tx_block_release</span></span>
* <span data-ttu-id="98fda-194">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-194">Additional information and performance APIs</span></span>

### <a name="byte-memory-pools"></a><span data-ttu-id="98fda-195">Bayt bellek havuzları</span><span class="sxs-lookup"><span data-stu-id="98fda-195">Byte Memory Pools</span></span>

* <span data-ttu-id="98fda-196">Dinamik bayt havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-196">Dynamic byte pool creation</span></span>
* <span data-ttu-id="98fda-197">Bayt havuzları sayısında sınır yoktur</span><span class="sxs-lookup"><span data-stu-id="98fda-197">No limits on the number of byte pools</span></span>
* <span data-ttu-id="98fda-198">Bayt havuzunun boyutu için sınır yok</span><span class="sxs-lookup"><span data-stu-id="98fda-198">No limits on size of byte pool</span></span>
* <span data-ttu-id="98fda-199">En esnek değişken uzunluklu bellek ayırma/ayırmayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="98fda-199">Most flexible variable-length memory allocation/deallocation</span></span>
* <span data-ttu-id="98fda-200">Ayırma boyutu yerleşim destekleniyor</span><span class="sxs-lookup"><span data-stu-id="98fda-200">Allocation size locality supported</span></span>
* <span data-ttu-id="98fda-201">Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="98fda-201">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="98fda-202">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="98fda-202">Optional timeout on all suspension</span></span>
* <span data-ttu-id="98fda-203">Ana bayt havuzu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="98fda-203">Main byte pool APIs include:</span></span>
  * <span data-ttu-id="98fda-204">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="98fda-204">tx_byte_pool_create</span></span>
  * <span data-ttu-id="98fda-205">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-205">tx_byte_pool_delete</span></span>
  * <span data-ttu-id="98fda-206">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="98fda-206">tx_byte_allocate</span></span>
  * <span data-ttu-id="98fda-207">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="98fda-207">tx_byte_release</span></span>
* <span data-ttu-id="98fda-208">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-208">Additional information and performance APIs</span></span>

### <a name="application-timers"></a><span data-ttu-id="98fda-209">Uygulama zamanlayıcıları</span><span class="sxs-lookup"><span data-stu-id="98fda-209">Application Timers</span></span>

* <span data-ttu-id="98fda-210">Dinamik süreölçer oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-210">Dynamic timer creation</span></span>
* <span data-ttu-id="98fda-211">Zamanlayıcılar sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="98fda-211">No limits on the number of timers</span></span>
* <span data-ttu-id="98fda-212">Düzenli veya tek atışı Zamanlayıcı destekleniyor</span><span class="sxs-lookup"><span data-stu-id="98fda-212">Periodic or one-shot timers supported</span></span>
* <span data-ttu-id="98fda-213">Düzenli zamanlayıcılar farklı başlangıç son kullanma değerine sahip olabilir</span><span class="sxs-lookup"><span data-stu-id="98fda-213">Periodic timers may have different initial expiration value</span></span>
* <span data-ttu-id="98fda-214">Süreölçer etkinleştirme veya devre dışı bırakma üzerinde arama yok</span><span class="sxs-lookup"><span data-stu-id="98fda-214">No searching on timer activation or deactivation</span></span>
* <span data-ttu-id="98fda-215">Bir donanım Zamanlayıcı kesmesinin yönettiği tüm zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="98fda-215">All timers driven from one hardware timer interrupt</span></span>
* <span data-ttu-id="98fda-216">Ana Zamanlayıcı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="98fda-216">Main timer APIs include:</span></span>
  * <span data-ttu-id="98fda-217">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="98fda-217">tx_timer_create</span></span>
  * <span data-ttu-id="98fda-218">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="98fda-218">tx_timer_delete</span></span>
  * <span data-ttu-id="98fda-219">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="98fda-219">tx_timer_activate</span></span>
  * <span data-ttu-id="98fda-220">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="98fda-220">tx_timer_change</span></span>
  * <span data-ttu-id="98fda-221">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="98fda-221">tx_timer_deactivate</span></span>
* <span data-ttu-id="98fda-222">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="98fda-222">Additional information and performance APIs</span></span>

### <a name="azure-rtos-threadx-core-scheduler"></a><span data-ttu-id="98fda-223">Azure RTOS ThreadX çekirdek Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="98fda-223">Azure RTOS ThreadX Core Scheduler</span></span>

* <span data-ttu-id="98fda-224">Minimum 2 KB FLASH, 1KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="98fda-224">Minimal 2KB FLASH,1KB RAM footprint</span></span>
* <span data-ttu-id="98fda-225">Fast, Sub-mikro ikinci bağlam-anahtar</span><span class="sxs-lookup"><span data-stu-id="98fda-225">Fast, sub-microsecond context-switch</span></span>
* <span data-ttu-id="98fda-226">İş parçacığı sayısından bağımsız olarak tam belirleyici</span><span class="sxs-lookup"><span data-stu-id="98fda-226">Fully deterministic regardless of number of threads</span></span>
* <span data-ttu-id="98fda-227">Öncelik temelli, tam preemptive-zamanlama</span><span class="sxs-lookup"><span data-stu-id="98fda-227">Priority-based, fully preemptive-scheduling</span></span>
* <span data-ttu-id="98fda-228">32 varsayılan öncelik düzeyleri, isteğe bağlı olarak 1024 düzeye kadar</span><span class="sxs-lookup"><span data-stu-id="98fda-228">32 default priority levels, optionally up to 1024 levels</span></span>
* <span data-ttu-id="98fda-229">Öncelik düzeyi (FıFO) içinde ortak zamanlama</span><span class="sxs-lookup"><span data-stu-id="98fda-229">Cooperative scheduling within priority level (FIFO)</span></span>
* <span data-ttu-id="98fda-230">Önalım-Threshold teknolojisi</span><span class="sxs-lookup"><span data-stu-id="98fda-230">Preemption-threshold technology</span></span>
* <span data-ttu-id="98fda-231">Aşağıdakiler dahil isteğe bağlı Zamanlayıcı Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="98fda-231">Optional timer services, including:</span></span>
  * <span data-ttu-id="98fda-232">İş parçacığı başına isteğe bağlı saat dilimi</span><span class="sxs-lookup"><span data-stu-id="98fda-232">Per-thread optional time-slice</span></span>
  * <span data-ttu-id="98fda-233">Tüm engellemede isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="98fda-233">Optional timeout on all blocking</span></span>
  * <span data-ttu-id="98fda-234">API 'Ler donanım süreölçer kesmesi gerektirir</span><span class="sxs-lookup"><span data-stu-id="98fda-234">APIs Requires on hardware timer interrupt</span></span>
* <span data-ttu-id="98fda-235">Yürütme profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="98fda-235">Execution profiling</span></span>
* <span data-ttu-id="98fda-236">Sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="98fda-236">System-level Trace</span></span>
* <span data-ttu-id="98fda-237">Birçok standartlara yönelik güvenlik sertifikalı</span><span class="sxs-lookup"><span data-stu-id="98fda-237">Safety certified to many standards</span></span>

## <a name="most-deployed-rtos"></a><span data-ttu-id="98fda-238">En çok dağıtılan RTOS</span><span class="sxs-lookup"><span data-stu-id="98fda-238">Most deployed RTOS</span></span>

<span data-ttu-id="98fda-239">Azure RTOS ThreadX, önde gelen 'U M2M Market Intelligence firması, VDC Research 'e göre dünya genelinde 6.200.000.000 dağıtımlara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="98fda-239">Azure RTOS ThreadX has over 6.2 billion deployments worldwide, according to the leading M2M market intelligence firm, VDC Research.</span></span> <span data-ttu-id="98fda-240">Azure RTOS ThreadX 'in popülerliği, güvenilirliği, kalitesi, boyutu, performansı, gelişmiş özellikler, kullanım kolaylığı ve genel kullanım süresi avantajına yönelik bir testdir.</span><span class="sxs-lookup"><span data-stu-id="98fda-240">The popularity of Azure RTOS ThreadX is a testament to its reliability, quality, size, performance, advanced features, ease-of-use, and overall time-to-market advantages.</span></span>

> <span data-ttu-id="98fda-241">*"Şirketin temelleri ile bu yana kablosuz ve IoT pazarlarında THREADX 'in büyüme tratrumuzu izliyoruz ve THREADX 'in yaygın sektör benimsemesi tarafından giderek daha da artmaktadır."*</span><span class="sxs-lookup"><span data-stu-id="98fda-241">*“We have followed the growth trajectory of THREADX in the wireless and IoT markets since the company’s founding, and are increasingly impressed by the widespread industry adoption of THREADX.”*</span></span> <span data-ttu-id="98fda-242">– Chris Rommel, Executive Başkan Yardımcısı, VDC Research</span><span class="sxs-lookup"><span data-stu-id="98fda-242">– Chris Rommel, Executive Vice President, VDC Research</span></span>

## <a name="small-footprint"></a><span data-ttu-id="98fda-243">Küçük ayak izi</span><span class="sxs-lookup"><span data-stu-id="98fda-243">Small footprint</span></span>

<span data-ttu-id="98fda-244">Azure RTOS ThreadX, en az bir kaplama için remarkalı küçük 2KB yönerge alanı ve 1KB RAM gerektirir.</span><span class="sxs-lookup"><span data-stu-id="98fda-244">Azure RTOS ThreadX requires a remarkably small 2KB instruction area and 1KB of RAM for its minimal footprint.</span></span> <span data-ttu-id="98fda-245">Bu, büyük bir olasılıkla katmanlı olmayan picokernel™ mimarisi ve otomatik ölçeklendirmesinden kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="98fda-245">This is largely due to its non-layered picokernel™ architecture and automatic scaling.</span></span> <span data-ttu-id="98fda-246">Otomatik ölçeklendirme, uygulama tarafından kullanılan hizmetlerin (ve destekleyici altyapının) bağlantı zamanında son görüntüye dahil olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="98fda-246">Automatic scaling means that only the services (and supporting infrastructure) used by the application are included in the final image at link time.</span></span>

<span data-ttu-id="98fda-247">Bazı tipik Azure RTOS ThreadX boyut özellikleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="98fda-247">Here are some typical Azure RTOS ThreadX size characteristics.</span></span>

|<span data-ttu-id="98fda-248">Azure RTOS ThreadX hizmeti</span><span class="sxs-lookup"><span data-stu-id="98fda-248">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="98fda-249">Bayt cinsinden normal boyut</span><span class="sxs-lookup"><span data-stu-id="98fda-249">Typical Size in Bytes</span></span>  |
|---------|---------|
|<span data-ttu-id="98fda-250">Çekirdek hizmetler (gerekli)</span><span class="sxs-lookup"><span data-stu-id="98fda-250">Core Services (Require)</span></span> |<span data-ttu-id="98fda-251">2.000</span><span class="sxs-lookup"><span data-stu-id="98fda-251">2,000</span></span>  |
|<span data-ttu-id="98fda-252">Kuyruk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="98fda-252">Queue Services</span></span>  |<span data-ttu-id="98fda-253">900</span><span class="sxs-lookup"><span data-stu-id="98fda-253">900</span></span>  |
|<span data-ttu-id="98fda-254">Olay bayrağı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="98fda-254">Event Flag Services</span></span>  |<span data-ttu-id="98fda-255">900</span><span class="sxs-lookup"><span data-stu-id="98fda-255">900</span></span>  |
|<span data-ttu-id="98fda-256">Semafor Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="98fda-256">Semaphore Services</span></span>  |<span data-ttu-id="98fda-257">450</span><span class="sxs-lookup"><span data-stu-id="98fda-257">450</span></span>  |
|<span data-ttu-id="98fda-258">Mutex Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="98fda-258">Mutex Services</span></span>  |<span data-ttu-id="98fda-259">1.200</span><span class="sxs-lookup"><span data-stu-id="98fda-259">1,200</span></span>  |
|<span data-ttu-id="98fda-260">Bellek hizmetlerini engelle</span><span class="sxs-lookup"><span data-stu-id="98fda-260">Block Memory Services</span></span>  |<span data-ttu-id="98fda-261">550</span><span class="sxs-lookup"><span data-stu-id="98fda-261">550</span></span>  |
|<span data-ttu-id="98fda-262">Bayt bellek Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="98fda-262">Byte Memory Services</span></span>  |<span data-ttu-id="98fda-263">900</span><span class="sxs-lookup"><span data-stu-id="98fda-263">900</span></span>  |

## <a name="fast-execution"></a><span data-ttu-id="98fda-264">Hızlı yürütme</span><span class="sxs-lookup"><span data-stu-id="98fda-264">Fast execution</span></span>

<span data-ttu-id="98fda-265">Azure RTOS ThreadX, en popüler işlemciler üzerinde bir alt mikro ikinci bağlam anahtarına erişir ve diğer ticari ortamlarından çok daha hızlı bir şekilde genel olarak daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="98fda-265">Azure RTOS ThreadX achieves a sub-microsecond context switch on most popular processors and is significantly faster overall than other commercial RTOSes.</span></span> <span data-ttu-id="98fda-266">Hızlı olmasının yanı sıra Azure RTOS ThreadX de oldukça belirleyici bir niteliğindedir.</span><span class="sxs-lookup"><span data-stu-id="98fda-266">In addition to being fast, Azure RTOS ThreadX is also highly deterministic.</span></span> <span data-ttu-id="98fda-267">Yalnızca bir tane veya tek bir 200 iş parçacığı olup olmadığı için aynı hızlı performansa erişir.</span><span class="sxs-lookup"><span data-stu-id="98fda-267">It achieves the same fast performance whether there are 200 threads ready, or just one.</span></span>

<span data-ttu-id="98fda-268">Azure RTOS ThreadX 'in bazı tipik performans özellikleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="98fda-268">Here are some typical performance characteristics of Azure RTOS ThreadX:</span></span>

* <span data-ttu-id="98fda-269">Hızlı önyükleme: 120 ' den az Döngülerde Azure RTOS ThreadX önyüklemeleri.</span><span class="sxs-lookup"><span data-stu-id="98fda-269">Fast Boot: Azure RTOS ThreadX boots in less than 120 cycles.</span></span>
* <span data-ttu-id="98fda-270">Temel hata denetimi için isteğe bağlı kaldırma: temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="98fda-270">Optional Removal of basic error checking: Basic Azure RTOS ThreadX error checking can be skipped at compile time.</span></span> <span data-ttu-id="98fda-271">Bu, uygulama kodu doğrulandığında ve her parametreye artık hata denetimi gerektirmeyen yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="98fda-271">This can be useful when the application code is verified and no longer requires error checking on each parameter.</span></span> <span data-ttu-id="98fda-272">Bunun, sistem genelinde değil, bir derleme birimi üzerinde yapılabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="98fda-272">Note that this can be done on a compilation unit, rather than system-wide.</span></span>
* <span data-ttu-id="98fda-273">Picokernel™ tasarımı: hizmetler birbirlerine katmanlı değildir, bu nedenle gereksiz işlev çağrısı yükünü ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="98fda-273">Picokernel™ Design: Services are not layered on each other, thus eliminating unnecessary function call overhead.</span></span>
* <span data-ttu-id="98fda-274">\* İyileştirilmiş kesme Işleme: önalım gerekli değilse, yalnızca karalama kayıtları ıSR girdisi/çıkış üzerine kaydedilir/geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="98fda-274">\*Optimized Interrupt Processing: Only scratch registers are saved/restored upon ISR entry/exit, unless preemption is necessary.</span></span>
* <span data-ttu-id="98fda-275">İyileştirilmiş API Işleme:</span><span class="sxs-lookup"><span data-stu-id="98fda-275">Optimized API Processing:</span></span>

    |<span data-ttu-id="98fda-276">Azure RTOS ThreadX hizmeti</span><span class="sxs-lookup"><span data-stu-id="98fda-276">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="98fda-277">Mikrosaniye cinsinden Hizmet Süresi \*</span><span class="sxs-lookup"><span data-stu-id="98fda-277">Service Time in Microseconds\*</span></span>  |
    |---------|---------|
    |<span data-ttu-id="98fda-278">İş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="98fda-278">Thread Suspend</span></span>  |<span data-ttu-id="98fda-279">0.6</span><span class="sxs-lookup"><span data-stu-id="98fda-279">0.6</span></span>  |
    |<span data-ttu-id="98fda-280">İş parçacığı özgeçmişi</span><span class="sxs-lookup"><span data-stu-id="98fda-280">Thread Resume</span></span>  |<span data-ttu-id="98fda-281">0.6</span><span class="sxs-lookup"><span data-stu-id="98fda-281">0.6</span></span>  |
    |<span data-ttu-id="98fda-282">Kuyruğu gönder</span><span class="sxs-lookup"><span data-stu-id="98fda-282">Queue Send</span></span>  |<span data-ttu-id="98fda-283">0.3</span><span class="sxs-lookup"><span data-stu-id="98fda-283">0.3</span></span>  |
    |<span data-ttu-id="98fda-284">Kuyruk alma</span><span class="sxs-lookup"><span data-stu-id="98fda-284">Queue Receive</span></span>  |<span data-ttu-id="98fda-285">0.3</span><span class="sxs-lookup"><span data-stu-id="98fda-285">0.3</span></span>  |
    |<span data-ttu-id="98fda-286">Semafor al</span><span class="sxs-lookup"><span data-stu-id="98fda-286">Get Semaphore</span></span>  |<span data-ttu-id="98fda-287">0,2</span><span class="sxs-lookup"><span data-stu-id="98fda-287">0.2</span></span>  |
    |<span data-ttu-id="98fda-288">Semaforu koy</span><span class="sxs-lookup"><span data-stu-id="98fda-288">Put Semaphore</span></span>  |<span data-ttu-id="98fda-289">0,2</span><span class="sxs-lookup"><span data-stu-id="98fda-289">0.2</span></span>  |
    |<span data-ttu-id="98fda-290">Bağlam anahtarı</span><span class="sxs-lookup"><span data-stu-id="98fda-290">Context Switch</span></span>  |<span data-ttu-id="98fda-291">0,4</span><span class="sxs-lookup"><span data-stu-id="98fda-291">0.4</span></span>  |
    |<span data-ttu-id="98fda-292">Kesme yanıtı</span><span class="sxs-lookup"><span data-stu-id="98fda-292">Interrupt Response</span></span>  |<span data-ttu-id="98fda-293">0,0 – 0,6</span><span class="sxs-lookup"><span data-stu-id="98fda-293">0.0 – 0.6</span></span>  |

    <span data-ttu-id="98fda-294">\**200 MHz hızında çalışan normal işlemciyi temel alan performans rakamları*.</span><span class="sxs-lookup"><span data-stu-id="98fda-294">\**Performance figures based on typical processor running at 200MHz*.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="98fda-295">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="98fda-295">Advanced technology</span></span>

<span data-ttu-id="98fda-296">Azure RTOS ThreadX, en önemli özelliği önalım-Threshold zamanlaması olan gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="98fda-296">Azure RTOS ThreadX is advanced technology whose most notable feature is preemption-threshold scheduling.</span></span> <span data-ttu-id="98fda-297">Bu özellik Azure RTOS ThreadX için benzersizdir ve kapsamlı akademik araştırma konusu.</span><span class="sxs-lookup"><span data-stu-id="98fda-297">This feature is unique to Azure RTOS ThreadX and has been the subject of extensive academic research.</span></span> <span data-ttu-id="98fda-298">Örneğin, bkz. [önalım Threshold ile Fixed-Priority görevleri zamanlama](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), Yıun Wang, Concorçya University ve Manas Saksena, tas haburi Üniversitesi.</span><span class="sxs-lookup"><span data-stu-id="98fda-298">For example, see [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), by Yun Wang, Concordia University, and Manas Saksena, University of Pittsburgh.</span></span>

<span data-ttu-id="98fda-299">Azure RTOS ThreadX 'in yeteneklerini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="98fda-299">Consider the capabilities of Azure RTOS ThreadX.</span></span>

* <span data-ttu-id="98fda-300">Eksiksiz ve kapsamlı çoklu görev olanakları</span><span class="sxs-lookup"><span data-stu-id="98fda-300">Complete and Comprehensive Multitasking Facilities</span></span>
  * <span data-ttu-id="98fda-301">İş parçacıkları, uygulama zamanlayıcılar, ileti kuyrukları, sayma semaforları, zaman uyumu sağlayıcılar, olay bayrakları, blok ve bayt bellek havuzları</span><span class="sxs-lookup"><span data-stu-id="98fda-301">Threads, application timers, message queues, counting semaphores, mutexes, event flags, block and byte memory pools</span></span>
* <span data-ttu-id="98fda-302">Priority-Based preemptive zamanlaması</span><span class="sxs-lookup"><span data-stu-id="98fda-302">Priority-Based Preemptive Scheduling</span></span>
* <span data-ttu-id="98fda-303">Öncelik esnekliği – 1024 öncelik düzeyine kadar</span><span class="sxs-lookup"><span data-stu-id="98fda-303">Priority Flexibility – Up to 1024 Priority Levels</span></span>
* <span data-ttu-id="98fda-304">Cooperative zamanlaması</span><span class="sxs-lookup"><span data-stu-id="98fda-304">Cooperative Scheduling</span></span>
* <span data-ttu-id="98fda-305">Önalım-Threshold™ – Azure RTOS ThreadX için benzersizdir, bağlam anahtarlarının azaltılmasına yardımcı olur ve schedulability (akademik araştırma başına) garantisi sağlar</span><span class="sxs-lookup"><span data-stu-id="98fda-305">Preemption-Threshold™ – Unique to Azure RTOS ThreadX, helps reduce context switches and help guarantee schedulability (per academic research)</span></span>
* <span data-ttu-id="98fda-306">Azure RTOS ThreadX MODÜLLERI aracılığıyla bellek koruması</span><span class="sxs-lookup"><span data-stu-id="98fda-306">Memory Protection via Azure RTOS ThreadX MODULES</span></span>
* <span data-ttu-id="98fda-307">Tam belirleyici</span><span class="sxs-lookup"><span data-stu-id="98fda-307">Fully Deterministic</span></span>
* <span data-ttu-id="98fda-308">Olay Izleme – son *n* sistem/uygulama olaylarını yakala</span><span class="sxs-lookup"><span data-stu-id="98fda-308">Event Trace – Capture last *n* system/application events</span></span>
* <span data-ttu-id="98fda-309">Olay zincirleme™ – her bir Azure RTOS ThreadX iletişimi veya eşitleme nesnesi için uygulamaya özgü "bildirim" geri çağırma işlevini kaydetme</span><span class="sxs-lookup"><span data-stu-id="98fda-309">Event Chaining™ – Register an application-specific “notify” callback function for each Azure RTOS ThreadX communication or synchronization object</span></span>
* <span data-ttu-id="98fda-310">Isteğe bağlı bellek koruması ile Azure RTOS ThreadX MODÜLLERI</span><span class="sxs-lookup"><span data-stu-id="98fda-310">Azure RTOS ThreadX MODULES with Optional Memory Protection</span></span>
* <span data-ttu-id="98fda-311">Run-Time performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="98fda-311">Run-Time Performance Metrics</span></span>
  * <span data-ttu-id="98fda-312">İş parçacığı bağlantının sürdürülmesi sayısı</span><span class="sxs-lookup"><span data-stu-id="98fda-312">Number of thread resumptions</span></span>
  * <span data-ttu-id="98fda-313">İş parçacığı getirilmesi sayısı</span><span class="sxs-lookup"><span data-stu-id="98fda-313">Number of thread suspensions</span></span>
  * <span data-ttu-id="98fda-314">İstek iş parçacığı preemptions sayısı</span><span class="sxs-lookup"><span data-stu-id="98fda-314">Number of solicited thread preemptions</span></span>
  * <span data-ttu-id="98fda-315">Zaman uyumsuz iş parçacığı kesme preemptions sayısı</span><span class="sxs-lookup"><span data-stu-id="98fda-315">Number of asynchronous thread interrupt preemptions</span></span>
  * <span data-ttu-id="98fda-316">İş parçacığı önceliği ınsürümlerin sayısı</span><span class="sxs-lookup"><span data-stu-id="98fda-316">Number of thread priority inversions</span></span>
  * <span data-ttu-id="98fda-317">İş parçacığı relinkler sayısı</span><span class="sxs-lookup"><span data-stu-id="98fda-317">Number of thread relinquishes</span></span>
* <span data-ttu-id="98fda-318">Yürütme profili seti (EPK)</span><span class="sxs-lookup"><span data-stu-id="98fda-318">Execution Profile Kit (EPK)</span></span>
* <span data-ttu-id="98fda-319">Kesme yığınını ayır</span><span class="sxs-lookup"><span data-stu-id="98fda-319">Separate Interrupt Stack</span></span>
* <span data-ttu-id="98fda-320">Run-Time Stack Analizi</span><span class="sxs-lookup"><span data-stu-id="98fda-320">Run-Time Stack Analysis</span></span>
* <span data-ttu-id="98fda-321">İyileştirilmiş Zamanlayıcı kesme Işlemi</span><span class="sxs-lookup"><span data-stu-id="98fda-321">Optimized Timer Interrupt Processing</span></span>

## <a name="multicore-support-amp--smp"></a><span data-ttu-id="98fda-322">Birden çok Ore desteği (AMP & SMP)</span><span class="sxs-lookup"><span data-stu-id="98fda-322">Multicore support (AMP & SMP)</span></span>

<span data-ttu-id="98fda-323">Standart Azure RTOS ThreadX genellikle asimetrik çoklu Işlem (AMP) ile birlikte kullanılır, burada Azure RTOS ThreadX ve uygulamanın (veya Linux) her çekirdek üzerinde yürütülür ve paylaşılan bellek aracılığıyla birbirleriyle iletişim kurar veya OpenAMP (Azure RTOS ThreadX, OpenAMP gibi işlemciler arası bir iletişim mekanizması) vardır.</span><span class="sxs-lookup"><span data-stu-id="98fda-323">Standard Azure RTOS ThreadX is often used in an Asymmetric Multiprocessing (AMP) fashion, where a separate copy of Azure RTOS ThreadX and the application (or Linux) execute on each core and communicate with each other via shared memory or an inter-processor communication mechanism such as OpenAMP (Azure RTOS ThreadX supports OpenAMP).</span></span> <span data-ttu-id="98fda-324">Bu, Azure RTOS ThreadX kullanan en yaygın çok sayıda yapılandırmadır ve uygulama, işlemcileri etkin bir şekilde yükleyebiliyor olması halinde en etkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="98fda-324">This is the most typical multicore configuration using Azure RTOS ThreadX and can be the most efficient if the application is able to effectively load the processors.</span></span>

<span data-ttu-id="98fda-325">İşlemcilerin yüklenmesi çok dinamik olduğundan, aşağıdaki işlemci aileleri için Azure RTOS ThreadX Symetric çok Işlem (SMP) kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="98fda-325">For environments where loading the processors is highly dynamic, Azure RTOS ThreadX Symetric Multiprocessing (SMP) is available for the following processor families:</span></span>

* <span data-ttu-id="98fda-326">ARM Cortex-Ax</span><span class="sxs-lookup"><span data-stu-id="98fda-326">ARM Cortex-Ax</span></span>
* <span data-ttu-id="98fda-327">ARM Cortex-Rx</span><span class="sxs-lookup"><span data-stu-id="98fda-327">ARM Cortex-Rx</span></span>
* <span data-ttu-id="98fda-328">ARM Cortex-A5x 64 bit</span><span class="sxs-lookup"><span data-stu-id="98fda-328">ARM Cortex-A5x 64-bit</span></span>
* <span data-ttu-id="98fda-329">MIPS 34K, 1004K ve ınteraptiv</span><span class="sxs-lookup"><span data-stu-id="98fda-329">MIPS 34K, 1004K, and interAptiv</span></span>
* <span data-ttu-id="98fda-330">PowerPC</span><span class="sxs-lookup"><span data-stu-id="98fda-330">PowerPC</span></span>
* <span data-ttu-id="98fda-331">Synopsys ARC HS</span><span class="sxs-lookup"><span data-stu-id="98fda-331">Synopsys ARC HS</span></span>
* <span data-ttu-id="98fda-332">x86</span><span class="sxs-lookup"><span data-stu-id="98fda-332">x86</span></span>

<span data-ttu-id="98fda-333">Azure RTOS ThreadX SMP, *n* işlemciler genelinde dinamik yük dengeleme gerçekleştirir ve tüm Azure RTOS threadx kaynaklarına (kuyruklar, Semaforlar, olay bayrakları, bellek havuzları vb.) tüm çekirdeklerde herhangi bir iş parçacığı tarafından erişilmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="98fda-333">Azure RTOS ThreadX SMP performs dynamic load balancing across *n* processors and allows all Azure RTOS ThreadX resources (queues, semaphores, event flags, memory pools, etc.) to be accessed by any thread on any core.</span></span> <span data-ttu-id="98fda-334">Azure RTOS ThreadX SMP tüm çekirdekler için tam Azure RTOS ThreadX API 'sini sağlar ve SMP işlemi için geçerli olan aşağıdaki yeni API 'yi tanıtır:</span><span class="sxs-lookup"><span data-stu-id="98fda-334">Azure RTOS ThreadX SMP enables the complete Azure RTOS ThreadX API on all cores and introduces the following new API’s applicable to SMP operation:</span></span>

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a><span data-ttu-id="98fda-335">Azure RTOS ThreadX modülleri aracılığıyla bellek koruması</span><span class="sxs-lookup"><span data-stu-id="98fda-335">Memory protection via Azure RTOS ThreadX Modules</span></span>

<span data-ttu-id="98fda-336">Azure RTOS ThreadX MODÜLLERI adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının, hedefte dinamik olarak yüklenebilen ve çalıştırılabilen (veya yerinde yürütülen) bir "Module" içine paketlenmiş olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="98fda-336">An add-on product called Azure RTOS ThreadX MODULES enables one or more application threads to be bundled into a “Module” that can be dynamically loaded and run (or executed in place) on the target.</span></span>

<span data-ttu-id="98fda-337">Modüller, büyük uygulamaların yalnızca etkin iş parçacıkları tarafından gereken belleği kaplamasına izin vermek için alan yükseltmeyi, hata düzeltmeyi ve program bölümlemesini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="98fda-337">Modules enable field upgrade, bug fixing, and program partitioning to allow large applications to occupy only the memory needed by active threads.</span></span>

<span data-ttu-id="98fda-338">Modüller Ayrıca Azure RTOS ThreadX öğesinden tamamen ayrı bir adres alanına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="98fda-338">Modules also have a completely separate address space from Azure RTOS ThreadX itself.</span></span> <span data-ttu-id="98fda-339">Bu, Azure RTOS ThreadX 'in, modülün dışında yanlışlıkla erişiminin diğer yazılım bileşenlerini bozmayacak şekilde bellek korumasını (MPU veya MMU aracılığıyla) yerleştirmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="98fda-339">This enables Azure RTOS ThreadX to place memory protection (via MPU or MMU) around the Module such that accidental access outside the module will not be able to corrupt any other software component.</span></span>


## <a name="misra-compliant"></a><span data-ttu-id="98fda-340">Hatalı ra uyumlu</span><span class="sxs-lookup"><span data-stu-id="98fda-340">MISRA compliant</span></span>

<span data-ttu-id="98fda-341">Azure RTOS ThreadX ve Azure RTOS ThreadX SMP souce Code yanlış ra-C:2004 ve MISRA C:2012 uyumludur.</span><span class="sxs-lookup"><span data-stu-id="98fda-341">Azure RTOS ThreadX and Azure RTOS ThreadX SMP souce code is MISRA-C:2004 and MISRA C:2012 compliant.</span></span> <span data-ttu-id="98fda-342">MISRA C, C programlama dilini kullanan kritik sistemler için bir programlama yönergeleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="98fda-342">MISRA C is a set of programming guidelines for critical systems using the C programming language.</span></span> <span data-ttu-id="98fda-343">Özgün MISRA C yönergeleri öncelikli olarak, ilk olarak bir oto ve uygulamaları hedeflenmiştir; Ancak, MISRA C artık güvenlik açısından kritik uygulamalar için geçerli olduğu şekilde çok daha tanınır.</span><span class="sxs-lookup"><span data-stu-id="98fda-343">The original MISRA C guidelines were primarily targeted toward automotive applications; however, MISRA C is now widely recognized as being applicable to any safety-critical application.</span></span> <span data-ttu-id="98fda-344">Azure RTOS ThreadX, tüm gerekli ve zorunlu, MISRA-C:2004 ve MISRA c:2012'nin tüm kuralları ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="98fda-344">Azure RTOS ThreadX is compliant with all required and mandatory rules of MISRA-C:2004 and MISRA C:2012.</span></span>

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Hatalı ra sertifikası":::

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="98fda-346">Popüler mimarilerin çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="98fda-346">Supports most popular architectures</span></span>

<span data-ttu-id="98fda-347">Azure RTOS ThreadX, en popüler 32/64 bit mikro işlemciler üzerinde çalışır, kullanıma hazır, tamamen sınanmış ve aşağıdakiler dahil olmak üzere tam olarak desteklenmektedir:</span><span class="sxs-lookup"><span data-stu-id="98fda-347">Azure RTOS ThreadX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

* <span data-ttu-id="98fda-348">Analog cihazlar: parça, BlackICE, CM4xx</span><span class="sxs-lookup"><span data-stu-id="98fda-348">Analog Devices: SHARC, Blackfin, CM4xx</span></span>
* <span data-ttu-id="98fda-349">Andes Core: RıSC-V</span><span class="sxs-lookup"><span data-stu-id="98fda-349">Andes Core: RISC-V</span></span>
* <span data-ttu-id="98fda-350">Ambiqmicro: Apollo MCUs</span><span class="sxs-lookup"><span data-stu-id="98fda-350">Ambiqmicro: Apollo MCUs</span></span>
* <span data-ttu-id="98fda-351">ARM: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı</span><span class="sxs-lookup"><span data-stu-id="98fda-351">ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>
* <span data-ttu-id="98fda-352">Temposunda: Xtensa, elmas</span><span class="sxs-lookup"><span data-stu-id="98fda-352">Cadence: Xtensa, Diamond</span></span>
* <span data-ttu-id="98fda-353">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WERWIFI</span><span class="sxs-lookup"><span data-stu-id="98fda-353">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>
* <span data-ttu-id="98fda-354">Cypress: RıSC-V</span><span class="sxs-lookup"><span data-stu-id="98fda-354">Cypress: RISC-V</span></span>
* <span data-ttu-id="98fda-355">EnSilica: eSi-RıSC</span><span class="sxs-lookup"><span data-stu-id="98fda-355">EnSilica: eSi-RISC</span></span>
* <span data-ttu-id="98fda-356">Infineon: XMC1000, XMC4000, Kanore</span><span class="sxs-lookup"><span data-stu-id="98fda-356">Infineon: XMC1000, XMC4000, TriCore</span></span>
* <span data-ttu-id="98fda-357">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, varış a 10</span><span class="sxs-lookup"><span data-stu-id="98fda-357">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>
* <span data-ttu-id="98fda-358">Mikro yonga: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="98fda-358">Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>
* <span data-ttu-id="98fda-359">Mikro yarı: RıSC-V</span><span class="sxs-lookup"><span data-stu-id="98fda-359">Microsemi: RISC-V</span></span>
* <span data-ttu-id="98fda-360">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="98fda-360">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>
* <span data-ttu-id="98fda-361">Renesas: SH, HS, v850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="98fda-361">Renesas: SH, HS, V850, RX, RZ, Synergy</span></span>
* <span data-ttu-id="98fda-362">Silicon Labs: EFM32</span><span class="sxs-lookup"><span data-stu-id="98fda-362">Silicon Labs: EFM32</span></span>
* <span data-ttu-id="98fda-363">Synopsys: ARC 600, 700, ARC EM, ARC HS</span><span class="sxs-lookup"><span data-stu-id="98fda-363">Synopsys: ARC 600, 700, ARC EM, ARC HS</span></span>
* <span data-ttu-id="98fda-364">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="98fda-364">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>
* <span data-ttu-id="98fda-365">TL: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="98fda-365">Tl: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>
* <span data-ttu-id="98fda-366">Dalga Bilgi Işlem: MıPS32 4K, 24K, 34K, 1004K, ver 5K, mikro Aptiv, ınteraptiv, proAptiv, M sınıfı</span><span class="sxs-lookup"><span data-stu-id="98fda-366">Wave Computing: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>
* <span data-ttu-id="98fda-367">Xilinx: mikro Blaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="98fda-367">Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

## <a name="supports-most-popular-tools"></a><span data-ttu-id="98fda-368">Popüler araçların çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="98fda-368">Supports most popular tools</span></span>

<span data-ttu-id="98fda-369">Azure RTOS ThreadX, en kapsamlı Azure RTOS ThreadX çekirdek tanıma 'yı de içeren ıAR 'ın Embedded çalışma ekranı™ dahil olmak üzere en popüler katıştırılmış geliştirme araçlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="98fda-369">Azure RTOS ThreadX supports most popular embedded development tools, including IAR’s Embedded Workbench™, which also has the most comprehensive Azure RTOS ThreadX kernel awareness available.</span></span> <span data-ttu-id="98fda-370">Ek araç tümleştirmesi, GNU (GCC), ARM DS-5/uVision®, yeşil Tepls MULTI®, Rüzgar River çalışma ekranı™, hayal Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Defterbach TRACE32®, TI Code-Composer Studio, çapraz puan ve tüm örneksel cihazları içerir.</span><span class="sxs-lookup"><span data-stu-id="98fda-370">Additional tool integration includes GNU (GCC), ARM DS-5/uVision®, Green Hills MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer Studio, CrossCore and all analog devices.</span></span>
