---
title: Azure RTOS ThreadX 'i anlama
description: Azure ThreadX, özellikle derin eklenmiş uygulamalar için tasarlanan gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS).
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 938619170ef51d354fa970134328c17407ae846a
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754871"
---
# <a name="overview-of-azure-rtos-threadx"></a><span data-ttu-id="3cd59-103">Azure RTOS ThreadX 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="3cd59-103">Overview of Azure RTOS ThreadX</span></span>

<span data-ttu-id="3cd59-104">Azure RTOS ThreadX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft 'un gelişmiş endüstriyel sınıf Real-Time Işletim sistemidir (RTOS).</span><span class="sxs-lookup"><span data-stu-id="3cd59-104">Azure RTOS ThreadX is Microsoft's advanced industrial grade Real-Time Operating System (RTOS) designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="3cd59-105">Azure RTOS ThreadX, Gelişmiş zamanlama, iletişim, eşitleme, süreölçer, bellek yönetimi ve kesme yönetim olanakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cd59-105">Azure RTOS ThreadX provides advanced scheduling, communication, synchronization, timer, memory management, and interrupt management facilities.</span></span> <span data-ttu-id="3cd59-106">Ayrıca, Azure RTOS ThreadX 'in picokernel™ mimarisi, önalım-Threshold™ zamanlama, olay zincirleme,™ yürütme profili oluşturma, performans ölçümleri ve sistem olay izleme dahil birçok gelişmiş özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="3cd59-106">In addition, Azure RTOS ThreadX has many advanced features, including its picokernel™ architecture, preemption-threshold™ scheduling, event-chaining,™ execution profiling, performance metrics, and system event tracing.</span></span> <span data-ttu-id="3cd59-107">En üstün kullanım kolaylığıyla birlikte, Azure RTOS ThreadX, katıştırılmış uygulamaların en zorlu kullanımı için ideal seçenektir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-107">Combined with its superior ease-of-use, Azure RTOS ThreadX is the ideal choice for the most demanding of embedded applications.</span></span> <span data-ttu-id="3cd59-108">2017 itibariyle, Azure RTOS ThreadX, tüketici cihazları, tıbbi elektronik ve endüstriyel denetim ekipmanı dahil olmak üzere çok çeşitli ürünlerde 6.200.000.000 ' den fazla dağıtıma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-108">As of 2017, Azure RTOS ThreadX has over 6.2 billion deployments, in a wide variety of products, including consumer devices, medical electronics, and industrial control equipment.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="3cd59-109">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="3cd59-109">API Protocols</span></span>

### <a name="azure-rtos-threadx-services"></a><span data-ttu-id="3cd59-110">Azure RTOS ThreadX Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="3cd59-110">Azure RTOS ThreadX Services</span></span>

* <span data-ttu-id="3cd59-111">Dinamik iş parçacığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-111">Dynamic thread creation</span></span>
* <span data-ttu-id="3cd59-112">İş parçacığı sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="3cd59-112">No limits on the number of threads</span></span>
* <span data-ttu-id="3cd59-113">Ana iş parçacığı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3cd59-113">Main thread APIs include:</span></span>
  * <span data-ttu-id="3cd59-114">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-114">tx_thread_create</span></span>
  * <span data-ttu-id="3cd59-115">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-115">tx_thread_delete</span></span>
  * <span data-ttu-id="3cd59-116">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="3cd59-116">tx_thread_preemption_change</span></span>
  * <span data-ttu-id="3cd59-117">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="3cd59-117">tx_thread_priority_change</span></span>
  * <span data-ttu-id="3cd59-118">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="3cd59-118">tx_thread_relinquish</span></span>
  * <span data-ttu-id="3cd59-119">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="3cd59-119">tx_thread_reset</span></span>
  * <span data-ttu-id="3cd59-120">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="3cd59-120">tx_thread_resume</span></span>
  * <span data-ttu-id="3cd59-121">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="3cd59-121">tx_thread_sleep</span></span>
  * <span data-ttu-id="3cd59-122">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="3cd59-122">tx_thread_suspend</span></span>
  * <span data-ttu-id="3cd59-123">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="3cd59-123">tx_thread_terminate</span></span>
  * <span data-ttu-id="3cd59-124">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="3cd59-124">tx_thread_wait_abort</span></span>
* <span data-ttu-id="3cd59-125">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-125">Additional information and performance APIs</span></span>

### <a name="message-queues"></a><span data-ttu-id="3cd59-126">İleti kuyrukları</span><span class="sxs-lookup"><span data-stu-id="3cd59-126">Message Queues</span></span>

* <span data-ttu-id="3cd59-127">Dinamik sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-127">Dynamic queue creation</span></span>
* <span data-ttu-id="3cd59-128">Sıra sayısında sınırlama yoktur</span><span class="sxs-lookup"><span data-stu-id="3cd59-128">No limits on the number of queues</span></span>
* <span data-ttu-id="3cd59-129">Değer (veya işaretçi aracılığıyla başvuruya göre) tarafından kopyalanmış iletiler</span><span class="sxs-lookup"><span data-stu-id="3cd59-129">Messages copied by value (or by reference via pointer)</span></span>
* <span data-ttu-id="3cd59-130">1 ile 16 32 bitlik sözcüklerden oluşan ileti boyutları</span><span class="sxs-lookup"><span data-stu-id="3cd59-130">Message sizes from 1 to 16 32-bit words</span></span>
* <span data-ttu-id="3cd59-131">Empty ve Full üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="3cd59-131">Optional thread suspension on empty and full</span></span>
* <span data-ttu-id="3cd59-132">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3cd59-132">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3cd59-133">Ana ileti kuyruğu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3cd59-133">Main message queue APIs include:</span></span>
  * <span data-ttu-id="3cd59-134">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-134">tx_queue_create</span></span>
  * <span data-ttu-id="3cd59-135">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-135">tx_queue_delete</span></span>
  * <span data-ttu-id="3cd59-136">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="3cd59-136">tx_queue_flush</span></span>
  * <span data-ttu-id="3cd59-137">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="3cd59-137">tx_queue_front_send</span></span>
  * <span data-ttu-id="3cd59-138">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="3cd59-138">tx_queue_receive</span></span>
  * <span data-ttu-id="3cd59-139">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="3cd59-139">tx_queue_send_notify</span></span>
* <span data-ttu-id="3cd59-140">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-140">Additional information and performance APIs</span></span>

### <a name="counting-semaphores"></a><span data-ttu-id="3cd59-141">Semafor sayma</span><span class="sxs-lookup"><span data-stu-id="3cd59-141">Counting Semaphores</span></span>

* <span data-ttu-id="3cd59-142">Dinamik semafor oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-142">Dynamic semaphore creation</span></span>
* <span data-ttu-id="3cd59-143">Semafor sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="3cd59-143">No limits on the number of semaphores</span></span>
* <span data-ttu-id="3cd59-144">32-bit sayma semaforları (0-4.294.967.295)</span><span class="sxs-lookup"><span data-stu-id="3cd59-144">32-bit counting semaphores (0 to 4,294,967,295)</span></span>
* <span data-ttu-id="3cd59-145">Tüketici-üretici veya kaynak korumasını destekler</span><span class="sxs-lookup"><span data-stu-id="3cd59-145">Supports consumer-producer or resource protection</span></span>
* <span data-ttu-id="3cd59-146">Semafor kullanılamadığında isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="3cd59-146">Optional thread suspension when semaphore unavailable</span></span>
* <span data-ttu-id="3cd59-147">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3cd59-147">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3cd59-148">Ana semafor API 'Leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3cd59-148">Main semaphore APIs include:</span></span>
  * <span data-ttu-id="3cd59-149">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-149">tx_semaphore_create</span></span>
  * <span data-ttu-id="3cd59-150">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-150">tx_semaphore_delete</span></span>
  * <span data-ttu-id="3cd59-151">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="3cd59-151">tx_semaphore_get</span></span>
  * <span data-ttu-id="3cd59-152">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="3cd59-152">tx_semaphore_put</span></span>
  * <span data-ttu-id="3cd59-153">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="3cd59-153">tx_semaphore_put_notify</span></span>
* <span data-ttu-id="3cd59-154">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-154">Additional information and performance APIs</span></span>

### <a name="mutexes"></a><span data-ttu-id="3cd59-155">Zaman Uyumu Sağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="3cd59-155">Mutexes</span></span>

* <span data-ttu-id="3cd59-156">Dinamik mutex oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-156">Dynamic mutex creation</span></span>
* <span data-ttu-id="3cd59-157">Birbirini kapsamayan sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="3cd59-157">No limits on the number of mutexes</span></span>
* <span data-ttu-id="3cd59-158">İç içe kaynak koruması destekleniyor</span><span class="sxs-lookup"><span data-stu-id="3cd59-158">Nested resource protection supported</span></span>
* <span data-ttu-id="3cd59-159">İsteğe bağlı öncelikli devralma destekleniyor</span><span class="sxs-lookup"><span data-stu-id="3cd59-159">Optional priority inheritance supported</span></span>
* <span data-ttu-id="3cd59-160">Mutex kullanılamadığında isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="3cd59-160">Optional thread suspension when mutex unavailable</span></span>
* <span data-ttu-id="3cd59-161">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3cd59-161">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3cd59-162">Ana mutex API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3cd59-162">Main mutex APIs include:</span></span>
  * <span data-ttu-id="3cd59-163">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-163">tx_mutex_create</span></span>
  * <span data-ttu-id="3cd59-164">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-164">tx_mutex_delete</span></span>
  * <span data-ttu-id="3cd59-165">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="3cd59-165">tx_mutex_get</span></span>
  * <span data-ttu-id="3cd59-166">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="3cd59-166">tx_mutex_put</span></span>
* <span data-ttu-id="3cd59-167">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-167">Additional information and performance APIs</span></span>

### <a name="event-flags"></a><span data-ttu-id="3cd59-168">Olay bayrakları</span><span class="sxs-lookup"><span data-stu-id="3cd59-168">Event Flags</span></span>

* <span data-ttu-id="3cd59-169">Dinamik olay bayrağı Grup oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-169">Dynamic event flag group creation</span></span>
* <span data-ttu-id="3cd59-170">Olay bayrak grupları sayısında sınırlama yok</span><span class="sxs-lookup"><span data-stu-id="3cd59-170">No limits on the number of event flag groups</span></span>
* <span data-ttu-id="3cd59-171">Bir iş parçacığının veya birden çok iş parçacığının eşitlenmesi</span><span class="sxs-lookup"><span data-stu-id="3cd59-171">Synchronization of one thread or multiple threads</span></span>
* <span data-ttu-id="3cd59-172">Atomik get ve Clear destekleniyor</span><span class="sxs-lookup"><span data-stu-id="3cd59-172">Atomic get and clear supported</span></span>
* <span data-ttu-id="3cd59-173">İsteğe bağlı çoklu iş parçacığı açma ve/veya olay kümesi askıya alma</span><span class="sxs-lookup"><span data-stu-id="3cd59-173">Optional multithread suspension on AND/OR set of events</span></span>
* <span data-ttu-id="3cd59-174">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3cd59-174">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3cd59-175">Ana olay bayrağı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3cd59-175">Main event flag APIs include:</span></span>
  * <span data-ttu-id="3cd59-176">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-176">tx_event_flags_create</span></span>
  * <span data-ttu-id="3cd59-177">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-177">tx_event_flags_delete</span></span>
  * <span data-ttu-id="3cd59-178">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="3cd59-178">tx_event_flags_get</span></span>
  * <span data-ttu-id="3cd59-179">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="3cd59-179">tx_event_flags_set</span></span>
  * <span data-ttu-id="3cd59-180">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="3cd59-180">tx_event_flags_set_notify</span></span>
* <span data-ttu-id="3cd59-181">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-181">Additional information and performance APIs</span></span>

### <a name="block-memory-pools"></a><span data-ttu-id="3cd59-182">Bellek havuzlarını engelle</span><span class="sxs-lookup"><span data-stu-id="3cd59-182">Block Memory Pools</span></span>

* <span data-ttu-id="3cd59-183">Dinamik blok havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-183">Dynamic block pool creation</span></span>
* <span data-ttu-id="3cd59-184">Blok havuzları sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="3cd59-184">No limits on the number of block pools</span></span>
* <span data-ttu-id="3cd59-185">Sabit boyutlu blokların boyutu veya havuzun boyutu için sınır yok</span><span class="sxs-lookup"><span data-stu-id="3cd59-185">No limits on size of fixed-size blocks or size of pool</span></span>
* <span data-ttu-id="3cd59-186">En hızlı olası bellek ayırma/anlaşma konumu</span><span class="sxs-lookup"><span data-stu-id="3cd59-186">Fastest possible memory allocation/deal-location</span></span>
* <span data-ttu-id="3cd59-187">Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="3cd59-187">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="3cd59-188">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3cd59-188">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3cd59-189">Ana blok havuzu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3cd59-189">Main block pool APIs include:</span></span>
  * <span data-ttu-id="3cd59-190">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-190">tx_block_pool_create</span></span>
  * <span data-ttu-id="3cd59-191">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-191">tx_block_pool_delete</span></span>
  * <span data-ttu-id="3cd59-192">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="3cd59-192">tx_block_allocate</span></span>
  * <span data-ttu-id="3cd59-193">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="3cd59-193">tx_block_release</span></span>
* <span data-ttu-id="3cd59-194">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-194">Additional information and performance APIs</span></span>

### <a name="byte-memory-pools"></a><span data-ttu-id="3cd59-195">Bayt bellek havuzları</span><span class="sxs-lookup"><span data-stu-id="3cd59-195">Byte Memory Pools</span></span>

* <span data-ttu-id="3cd59-196">Dinamik bayt havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-196">Dynamic byte pool creation</span></span>
* <span data-ttu-id="3cd59-197">Bayt havuzları sayısında sınır yoktur</span><span class="sxs-lookup"><span data-stu-id="3cd59-197">No limits on the number of byte pools</span></span>
* <span data-ttu-id="3cd59-198">Bayt havuzunun boyutu için sınır yok</span><span class="sxs-lookup"><span data-stu-id="3cd59-198">No limits on size of byte pool</span></span>
* <span data-ttu-id="3cd59-199">En esnek değişken uzunluklu bellek ayırma/ayırmayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="3cd59-199">Most flexible variable-length memory allocation/deallocation</span></span>
* <span data-ttu-id="3cd59-200">Ayırma boyutu yerleşim destekleniyor</span><span class="sxs-lookup"><span data-stu-id="3cd59-200">Allocation size locality supported</span></span>
* <span data-ttu-id="3cd59-201">Boş havuzda isteğe bağlı iş parçacığının askıya alınması</span><span class="sxs-lookup"><span data-stu-id="3cd59-201">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="3cd59-202">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3cd59-202">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3cd59-203">Ana byte havuzu API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3cd59-203">Main byte pool APIs include:</span></span>
  * <span data-ttu-id="3cd59-204">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-204">tx_byte_pool_create</span></span>
  * <span data-ttu-id="3cd59-205">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-205">tx_byte_pool_delete</span></span>
  * <span data-ttu-id="3cd59-206">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="3cd59-206">tx_byte_allocate</span></span>
  * <span data-ttu-id="3cd59-207">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="3cd59-207">tx_byte_release</span></span>
* <span data-ttu-id="3cd59-208">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-208">Additional information and performance APIs</span></span>

### <a name="application-timers"></a><span data-ttu-id="3cd59-209">Uygulama Süre süreleri</span><span class="sxs-lookup"><span data-stu-id="3cd59-209">Application Timers</span></span>

* <span data-ttu-id="3cd59-210">Dinamik zamanlayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-210">Dynamic timer creation</span></span>
* <span data-ttu-id="3cd59-211">Süre kaç kez süreyle ilgili sınır yoktur?</span><span class="sxs-lookup"><span data-stu-id="3cd59-211">No limits on the number of timers</span></span>
* <span data-ttu-id="3cd59-212">Düzenli aralıklarla veya tek seferlik süreerler desteklensin</span><span class="sxs-lookup"><span data-stu-id="3cd59-212">Periodic or one-shot timers supported</span></span>
* <span data-ttu-id="3cd59-213">Düzenli süre sonu değerleri farklı başlangıç süre sonu değerlerine sahip olabilir</span><span class="sxs-lookup"><span data-stu-id="3cd59-213">Periodic timers may have different initial expiration value</span></span>
* <span data-ttu-id="3cd59-214">Zamanlayıcı etkinleştirme veya devre dışı bırakmada arama yok</span><span class="sxs-lookup"><span data-stu-id="3cd59-214">No searching on timer activation or deactivation</span></span>
* <span data-ttu-id="3cd59-215">Bir donanım zamanlayıcı kesintisi ile yönlendiren tüm süreölçerler</span><span class="sxs-lookup"><span data-stu-id="3cd59-215">All timers driven from one hardware timer interrupt</span></span>
* <span data-ttu-id="3cd59-216">Ana zamanlayıcı API'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3cd59-216">Main timer APIs include:</span></span>
  * <span data-ttu-id="3cd59-217">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="3cd59-217">tx_timer_create</span></span>
  * <span data-ttu-id="3cd59-218">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="3cd59-218">tx_timer_delete</span></span>
  * <span data-ttu-id="3cd59-219">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="3cd59-219">tx_timer_activate</span></span>
  * <span data-ttu-id="3cd59-220">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="3cd59-220">tx_timer_change</span></span>
  * <span data-ttu-id="3cd59-221">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="3cd59-221">tx_timer_deactivate</span></span>
* <span data-ttu-id="3cd59-222">Ek bilgiler ve performans API'leri</span><span class="sxs-lookup"><span data-stu-id="3cd59-222">Additional information and performance APIs</span></span>

### <a name="azure-rtos-threadx-core-scheduler"></a><span data-ttu-id="3cd59-223">Azure RTOS ThreadX Core Scheduler</span><span class="sxs-lookup"><span data-stu-id="3cd59-223">Azure RTOS ThreadX Core Scheduler</span></span>

* <span data-ttu-id="3cd59-224">En az 2 KB FLASH,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="3cd59-224">Minimal 2KB FLASH,1KB RAM footprint</span></span>
* <span data-ttu-id="3cd59-225">Hızlı, mikrosaniye altı bağlam anahtarı</span><span class="sxs-lookup"><span data-stu-id="3cd59-225">Fast, sub-microsecond context-switch</span></span>
* <span data-ttu-id="3cd59-226">İş parçacığı sayısından bağımsız olarak tam olarak belirlenimci</span><span class="sxs-lookup"><span data-stu-id="3cd59-226">Fully deterministic regardless of number of threads</span></span>
* <span data-ttu-id="3cd59-227">Öncelik tabanlı, tamamen ön hazırlıklı zamanlama</span><span class="sxs-lookup"><span data-stu-id="3cd59-227">Priority-based, fully preemptive-scheduling</span></span>
* <span data-ttu-id="3cd59-228">İsteğe bağlı olarak 1024 düzeye kadar olan 32 varsayılan öncelik düzeyi</span><span class="sxs-lookup"><span data-stu-id="3cd59-228">32 default priority levels, optionally up to 1024 levels</span></span>
* <span data-ttu-id="3cd59-229">Öncelik düzeyinde işbirliğine açık zamanlama (FIFO)</span><span class="sxs-lookup"><span data-stu-id="3cd59-229">Cooperative scheduling within priority level (FIFO)</span></span>
* <span data-ttu-id="3cd59-230">Ön üretim eşiği teknolojisi</span><span class="sxs-lookup"><span data-stu-id="3cd59-230">Preemption-threshold technology</span></span>
* <span data-ttu-id="3cd59-231">İsteğe bağlı zamanlayıcı hizmetleri, şunları da içeren:</span><span class="sxs-lookup"><span data-stu-id="3cd59-231">Optional timer services, including:</span></span>
  * <span data-ttu-id="3cd59-232">İş parçacığı başına isteğe bağlı zaman dilimi</span><span class="sxs-lookup"><span data-stu-id="3cd59-232">Per-thread optional time-slice</span></span>
  * <span data-ttu-id="3cd59-233">Tüm engellemede isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3cd59-233">Optional timeout on all blocking</span></span>
  * <span data-ttu-id="3cd59-234">API'ler donanım süreölçer kesintisi için gerektirir</span><span class="sxs-lookup"><span data-stu-id="3cd59-234">APIs Requires on hardware timer interrupt</span></span>
* <span data-ttu-id="3cd59-235">Yürütme profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cd59-235">Execution profiling</span></span>
* <span data-ttu-id="3cd59-236">Sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="3cd59-236">System-level Trace</span></span>
* <span data-ttu-id="3cd59-237">Güvenlik birçok standart tarafından onaylandı</span><span class="sxs-lookup"><span data-stu-id="3cd59-237">Safety certified to many standards</span></span>

## <a name="threadx-footprint"></a><span data-ttu-id="3cd59-238">ThreadX ayak izi</span><span class="sxs-lookup"><span data-stu-id="3cd59-238">ThreadX footprint</span></span>

<span data-ttu-id="3cd59-239">Azure RTOS ThreadX için çok küçük bir 2 KB yönerge alanı ve en az ayak izi için 1 KB RAM gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-239">Azure RTOS ThreadX requires a remarkably small 2KB instruction area and 1KB of RAM for its minimal footprint.</span></span> <span data-ttu-id="3cd59-240">Bunun nedeni büyük ölçüde katmanlı olmayan picokernel mimarisi ™ otomatik ölçeklendirmedir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-240">This is largely due to its non-layered picokernel™ architecture and automatic scaling.</span></span> <span data-ttu-id="3cd59-241">Otomatik ölçeklendirme, bağlantı zamanında son görüntüye yalnızca uygulama tarafından kullanılan hizmetlerin (ve destekleyen altyapının) dahil olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-241">Automatic scaling means that only the services (and supporting infrastructure) used by the application are included in the final image at link time.</span></span>

<span data-ttu-id="3cd59-242">Burada Bazı tipik Azure RTOS ThreadX boyutu özellikleri vetir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-242">Here are some typical Azure RTOS ThreadX size characteristics.</span></span>

|<span data-ttu-id="3cd59-243">Azure RTOS ThreadX Hizmeti</span><span class="sxs-lookup"><span data-stu-id="3cd59-243">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="3cd59-244">Bayt Cinsinden Tipik Boyut</span><span class="sxs-lookup"><span data-stu-id="3cd59-244">Typical Size in Bytes</span></span>  |
|---------|---------|
|<span data-ttu-id="3cd59-245">Temel Hizmetler (Gerekli)</span><span class="sxs-lookup"><span data-stu-id="3cd59-245">Core Services (Require)</span></span> |<span data-ttu-id="3cd59-246">2.000</span><span class="sxs-lookup"><span data-stu-id="3cd59-246">2,000</span></span>  |
|<span data-ttu-id="3cd59-247">Kuyruk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="3cd59-247">Queue Services</span></span>  |<span data-ttu-id="3cd59-248">900</span><span class="sxs-lookup"><span data-stu-id="3cd59-248">900</span></span>  |
|<span data-ttu-id="3cd59-249">Olay Bayrağı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="3cd59-249">Event Flag Services</span></span>  |<span data-ttu-id="3cd59-250">900</span><span class="sxs-lookup"><span data-stu-id="3cd59-250">900</span></span>  |
|<span data-ttu-id="3cd59-251">Semaphore Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="3cd59-251">Semaphore Services</span></span>  |<span data-ttu-id="3cd59-252">450</span><span class="sxs-lookup"><span data-stu-id="3cd59-252">450</span></span>  |
|<span data-ttu-id="3cd59-253">Mutex Services</span><span class="sxs-lookup"><span data-stu-id="3cd59-253">Mutex Services</span></span>  |<span data-ttu-id="3cd59-254">1.200</span><span class="sxs-lookup"><span data-stu-id="3cd59-254">1,200</span></span>  |
|<span data-ttu-id="3cd59-255">Bellek Hizmetlerini Engelleme</span><span class="sxs-lookup"><span data-stu-id="3cd59-255">Block Memory Services</span></span>  |<span data-ttu-id="3cd59-256">550</span><span class="sxs-lookup"><span data-stu-id="3cd59-256">550</span></span>  |
|<span data-ttu-id="3cd59-257">Byte Memory Services</span><span class="sxs-lookup"><span data-stu-id="3cd59-257">Byte Memory Services</span></span>  |<span data-ttu-id="3cd59-258">900</span><span class="sxs-lookup"><span data-stu-id="3cd59-258">900</span></span>  |

## <a name="threadx-execution-speed"></a><span data-ttu-id="3cd59-259">ThreadX yürütme hızı</span><span class="sxs-lookup"><span data-stu-id="3cd59-259">ThreadX execution speed</span></span>

<span data-ttu-id="3cd59-260">Azure RTOS ThreadX, en popüler işlemcilerde mikrosaniyenin altında bir bağlam anahtarına sahip olur ve genel olarak diğer ticari RTOS'lara göre önemli ölçüde daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="3cd59-260">Azure RTOS ThreadX achieves a sub-microsecond context switch on most popular processors and is significantly faster overall than other commercial RTOSes.</span></span> <span data-ttu-id="3cd59-261">ThreadX, hızlı olmanın Azure RTOS yüksek oranda belirleyicidir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-261">In addition to being fast, Azure RTOS ThreadX is also highly deterministic.</span></span> <span data-ttu-id="3cd59-262">Hazır 200 iş parçacığı veya yalnızca bir tane olsa da aynı hızlı performansı elde ediyor.</span><span class="sxs-lookup"><span data-stu-id="3cd59-262">It achieves the same fast performance whether there are 200 threads ready, or just one.</span></span>

<span data-ttu-id="3cd59-263">Azure RTOS ThreadX'in tipik performans Azure RTOS vardır:</span><span class="sxs-lookup"><span data-stu-id="3cd59-263">Here are some typical performance characteristics of Azure RTOS ThreadX:</span></span>

* <span data-ttu-id="3cd59-264">Hızlı Önyükleme: Azure RTOS ThreadX'in önyüklemesi 120 döngüden kısadır.</span><span class="sxs-lookup"><span data-stu-id="3cd59-264">Fast Boot: Azure RTOS ThreadX boots in less than 120 cycles.</span></span>
* <span data-ttu-id="3cd59-265">İsteğe bağlı Temel hata denetimi kaldırıldı: Temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-265">Optional Removal of basic error checking: Basic Azure RTOS ThreadX error checking can be skipped at compile time.</span></span> <span data-ttu-id="3cd59-266">Bu, uygulama kodu doğrulandığında ve artık her parametrede hata denetimi gerektirmeyecek şekilde yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-266">This can be useful when the application code is verified and no longer requires error checking on each parameter.</span></span> <span data-ttu-id="3cd59-267">Bunun sistem genelinde değil bir derleme biriminde yapl olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3cd59-267">Note that this can be done on a compilation unit, rather than system-wide.</span></span>
* <span data-ttu-id="3cd59-268">Picokernel™ Tasarım: Hizmetler birbirine katmanlanmaz, bu nedenle gereksiz işlev çağrısı ek yükünü ortadan kaldırmış olur.</span><span class="sxs-lookup"><span data-stu-id="3cd59-268">Picokernel™ Design: Services are not layered on each other, thus eliminating unnecessary function call overhead.</span></span>
* <span data-ttu-id="3cd59-269">\*İyileştirilmiş Kesme İşlemesi: Ön hazırlık gerekli olmadığı sürece ISR girdisi/çıkışında yalnızca karalama yazmacı kaydedilir/geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-269">\*Optimized Interrupt Processing: Only scratch registers are saved/restored upon ISR entry/exit, unless preemption is necessary.</span></span>
* <span data-ttu-id="3cd59-270">İyileştirilmiş API İşleme:</span><span class="sxs-lookup"><span data-stu-id="3cd59-270">Optimized API Processing:</span></span>

    |<span data-ttu-id="3cd59-271">Azure RTOS ThreadX Hizmeti</span><span class="sxs-lookup"><span data-stu-id="3cd59-271">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="3cd59-272">MikroSaniyelerde Hizmet Süresi\*</span><span class="sxs-lookup"><span data-stu-id="3cd59-272">Service Time in Microseconds\*</span></span>  |
    |---------|---------|
    |<span data-ttu-id="3cd59-273">İş ParçacığıNı Askıya Alma</span><span class="sxs-lookup"><span data-stu-id="3cd59-273">Thread Suspend</span></span>  |<span data-ttu-id="3cd59-274">0.6</span><span class="sxs-lookup"><span data-stu-id="3cd59-274">0.6</span></span>  |
    |<span data-ttu-id="3cd59-275">İş Parçacığı Sürdürme</span><span class="sxs-lookup"><span data-stu-id="3cd59-275">Thread Resume</span></span>  |<span data-ttu-id="3cd59-276">0.6</span><span class="sxs-lookup"><span data-stu-id="3cd59-276">0.6</span></span>  |
    |<span data-ttu-id="3cd59-277">Kuyruk Gönderme</span><span class="sxs-lookup"><span data-stu-id="3cd59-277">Queue Send</span></span>  |<span data-ttu-id="3cd59-278">0.3</span><span class="sxs-lookup"><span data-stu-id="3cd59-278">0.3</span></span>  |
    |<span data-ttu-id="3cd59-279">Kuyruk Alma</span><span class="sxs-lookup"><span data-stu-id="3cd59-279">Queue Receive</span></span>  |<span data-ttu-id="3cd59-280">0.3</span><span class="sxs-lookup"><span data-stu-id="3cd59-280">0.3</span></span>  |
    |<span data-ttu-id="3cd59-281">Semaphore'ları al</span><span class="sxs-lookup"><span data-stu-id="3cd59-281">Get Semaphore</span></span>  |<span data-ttu-id="3cd59-282">0,2</span><span class="sxs-lookup"><span data-stu-id="3cd59-282">0.2</span></span>  |
    |<span data-ttu-id="3cd59-283">Semaphore koyma</span><span class="sxs-lookup"><span data-stu-id="3cd59-283">Put Semaphore</span></span>  |<span data-ttu-id="3cd59-284">0,2</span><span class="sxs-lookup"><span data-stu-id="3cd59-284">0.2</span></span>  |
    |<span data-ttu-id="3cd59-285">Bağlam Anahtarı</span><span class="sxs-lookup"><span data-stu-id="3cd59-285">Context Switch</span></span>  |<span data-ttu-id="3cd59-286">0,4</span><span class="sxs-lookup"><span data-stu-id="3cd59-286">0.4</span></span>  |
    |<span data-ttu-id="3cd59-287">Kesme Yanıtı</span><span class="sxs-lookup"><span data-stu-id="3cd59-287">Interrupt Response</span></span>  |<span data-ttu-id="3cd59-288">0.0 – 0.6</span><span class="sxs-lookup"><span data-stu-id="3cd59-288">0.0 – 0.6</span></span>  |

    <span data-ttu-id="3cd59-289">\**200 MHz hızında çalışan tipik işlemciye göre performans rakamları.*</span><span class="sxs-lookup"><span data-stu-id="3cd59-289">\**Performance figures based on typical processor running at 200MHz*.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="3cd59-290">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="3cd59-290">Advanced technology</span></span>

<span data-ttu-id="3cd59-291">Azure RTOS ThreadX, en önemli özelliği ön eşik zamanlaması olan gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-291">Azure RTOS ThreadX is advanced technology whose most notable feature is preemption-threshold scheduling.</span></span> <span data-ttu-id="3cd59-292">Bu özellik, ThreadX Azure RTOS benzersizdir ve kapsamlı akademik araştırmaların konusudur.</span><span class="sxs-lookup"><span data-stu-id="3cd59-292">This feature is unique to Azure RTOS ThreadX and has been the subject of extensive academic research.</span></span> <span data-ttu-id="3cd59-293">Örneğin, Yun Wang, Wangia Üniversitesi ve Manas Saksena, University of Pittsburgh tarafından Fixed-Priority Tasks with [Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf)ile Scheduling Fixed-Priority( Zamanlama).</span><span class="sxs-lookup"><span data-stu-id="3cd59-293">For example, see [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), by Yun Wang, Concordia University, and Manas Saksena, University of Pittsburgh.</span></span>

<span data-ttu-id="3cd59-294">Azure RTOS ThreadX'in özelliklerini göz önünde bulundurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cd59-294">Consider the capabilities of Azure RTOS ThreadX.</span></span>

* <span data-ttu-id="3cd59-295">Eksiksiz ve Kapsamlı Çok Görevli Tesisler</span><span class="sxs-lookup"><span data-stu-id="3cd59-295">Complete and Comprehensive Multitasking Facilities</span></span>
  * <span data-ttu-id="3cd59-296">İş parçacıkları, uygulama süreçleri, ileti kuyrukları, semaforları sayma, mutex'ler, olay bayrakları, blok ve byte bellek havuzları</span><span class="sxs-lookup"><span data-stu-id="3cd59-296">Threads, application timers, message queues, counting semaphores, mutexes, event flags, block and byte memory pools</span></span>
* <span data-ttu-id="3cd59-297">Priority-Based Ön Zamanlama</span><span class="sxs-lookup"><span data-stu-id="3cd59-297">Priority-Based Preemptive Scheduling</span></span>
* <span data-ttu-id="3cd59-298">Öncelik Esnekliği – En fazla 1024 Öncelik Düzeyi</span><span class="sxs-lookup"><span data-stu-id="3cd59-298">Priority Flexibility – Up to 1024 Priority Levels</span></span>
* <span data-ttu-id="3cd59-299">İşbirlikçi Zamanlama</span><span class="sxs-lookup"><span data-stu-id="3cd59-299">Cooperative Scheduling</span></span>
* <span data-ttu-id="3cd59-300">Preemption-Threshold™ – Azure RTOS ThreadX'e özeldir, bağlam geçişlerini azaltmaya ve zamanlanabilirliği garanti etmeye yardımcı olur (akademik araştırma başına)</span><span class="sxs-lookup"><span data-stu-id="3cd59-300">Preemption-Threshold™ – Unique to Azure RTOS ThreadX, helps reduce context switches and help guarantee schedulability (per academic research)</span></span>
* <span data-ttu-id="3cd59-301">Azure RTOS ThreadX MODULES aracılığıyla Bellek Koruması</span><span class="sxs-lookup"><span data-stu-id="3cd59-301">Memory Protection via Azure RTOS ThreadX MODULES</span></span>
* <span data-ttu-id="3cd59-302">Tam Belirleyici</span><span class="sxs-lookup"><span data-stu-id="3cd59-302">Fully Deterministic</span></span>
* <span data-ttu-id="3cd59-303">Olay İzleme – Son *n sistem/uygulama* olaylarını yakalama</span><span class="sxs-lookup"><span data-stu-id="3cd59-303">Event Trace – Capture last *n* system/application events</span></span>
* <span data-ttu-id="3cd59-304">Olay Zincirleme™ – ThreadX iletişimini veya eşitleme nesnesini her bir uygulama için Azure RTOS "notify" geri çağırma işlevini kaydetme</span><span class="sxs-lookup"><span data-stu-id="3cd59-304">Event Chaining™ – Register an application-specific “notify” callback function for each Azure RTOS ThreadX communication or synchronization object</span></span>
* <span data-ttu-id="3cd59-305">Azure RTOS İsteğe Bağlı Bellek Koruması ile ThreadX MODÜLLERI</span><span class="sxs-lookup"><span data-stu-id="3cd59-305">Azure RTOS ThreadX MODULES with Optional Memory Protection</span></span>
* <span data-ttu-id="3cd59-306">Run-Time Performans Ölçümleri</span><span class="sxs-lookup"><span data-stu-id="3cd59-306">Run-Time Performance Metrics</span></span>
  * <span data-ttu-id="3cd59-307">İş parçacığı yeniden dizilerinin sayısı</span><span class="sxs-lookup"><span data-stu-id="3cd59-307">Number of thread resumptions</span></span>
  * <span data-ttu-id="3cd59-308">İş parçacığı askıya alma sayısı</span><span class="sxs-lookup"><span data-stu-id="3cd59-308">Number of thread suspensions</span></span>
  * <span data-ttu-id="3cd59-309">İstenen iş parçacığı önempsi sayısı</span><span class="sxs-lookup"><span data-stu-id="3cd59-309">Number of solicited thread preemptions</span></span>
  * <span data-ttu-id="3cd59-310">Zaman uyumsuz iş parçacığı kesme önemptions sayısı</span><span class="sxs-lookup"><span data-stu-id="3cd59-310">Number of asynchronous thread interrupt preemptions</span></span>
  * <span data-ttu-id="3cd59-311">İş parçacığı öncelik ters çevirme sayısı</span><span class="sxs-lookup"><span data-stu-id="3cd59-311">Number of thread priority inversions</span></span>
  * <span data-ttu-id="3cd59-312">İş parçacığı ilinquishes sayısı</span><span class="sxs-lookup"><span data-stu-id="3cd59-312">Number of thread relinquishes</span></span>
* <span data-ttu-id="3cd59-313">Yürütme Profili Seti (EPK)</span><span class="sxs-lookup"><span data-stu-id="3cd59-313">Execution Profile Kit (EPK)</span></span>
* <span data-ttu-id="3cd59-314">Kesme Yığınını Ayırma</span><span class="sxs-lookup"><span data-stu-id="3cd59-314">Separate Interrupt Stack</span></span>
* <span data-ttu-id="3cd59-315">Run-Time Yığını Analizi</span><span class="sxs-lookup"><span data-stu-id="3cd59-315">Run-Time Stack Analysis</span></span>
* <span data-ttu-id="3cd59-316">Zamanlayıcı Kesme İşleme İyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="3cd59-316">Optimized Timer Interrupt Processing</span></span>

## <a name="multicore-support-amp--smp"></a><span data-ttu-id="3cd59-317">Çok çekirdekli destek (AMP & SMP)</span><span class="sxs-lookup"><span data-stu-id="3cd59-317">Multicore support (AMP & SMP)</span></span>

<span data-ttu-id="3cd59-318">Standart Azure RTOS ThreadX genellikle ayrı bir Azure RTOS ThreadX kopyasının ve uygulamanın (veya Linux'un) her çekirdekte yürütülür ve paylaşılan bellek veya OpenAMP gibi bir işlemciler arası iletişim mekanizması aracılığıyla birbirleriyle iletişim kurarak OpenAMP (Azure RTOS ThreadX OpenAMP'ı destekler) asimetrik Çok İşlemcili (AMP) bir şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3cd59-318">Standard Azure RTOS ThreadX is often used in an Asymmetric Multiprocessing (AMP) fashion, where a separate copy of Azure RTOS ThreadX and the application (or Linux) execute on each core and communicate with each other via shared memory or an inter-processor communication mechanism such as OpenAMP (Azure RTOS ThreadX supports OpenAMP).</span></span> <span data-ttu-id="3cd59-319">Bu, Azure RTOS ThreadX kullanan en tipik çok çekirdekli yapılandırmadır ve uygulama işlemcileri etkili bir şekilde yükleyene kadar en verimli yapılandırma olabilir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-319">This is the most typical multicore configuration using Azure RTOS ThreadX and can be the most efficient if the application is able to effectively load the processors.</span></span>

<span data-ttu-id="3cd59-320">İşlemcileri yüklemenin yüksek oranda dinamik olduğu ortamlar için Azure RTOS ThreadX Symetric Multiprocessing (SMP) aşağıdaki işlemci aileleri için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3cd59-320">For environments where loading the processors is highly dynamic, Azure RTOS ThreadX Symetric Multiprocessing (SMP) is available for the following processor families:</span></span>

* <span data-ttu-id="3cd59-321">ARM Cortex-Ax</span><span class="sxs-lookup"><span data-stu-id="3cd59-321">ARM Cortex-Ax</span></span>
* <span data-ttu-id="3cd59-322">ARM Cortex-Rx</span><span class="sxs-lookup"><span data-stu-id="3cd59-322">ARM Cortex-Rx</span></span>
* <span data-ttu-id="3cd59-323">ARM Cortex-A5x 64 bit</span><span class="sxs-lookup"><span data-stu-id="3cd59-323">ARM Cortex-A5x 64-bit</span></span>
* <span data-ttu-id="3cd59-324">MIPS 34K, 1004K ve interAptiv</span><span class="sxs-lookup"><span data-stu-id="3cd59-324">MIPS 34K, 1004K, and interAptiv</span></span>
* <span data-ttu-id="3cd59-325">PowerPC</span><span class="sxs-lookup"><span data-stu-id="3cd59-325">PowerPC</span></span>
* <span data-ttu-id="3cd59-326">Özet ARC HS</span><span class="sxs-lookup"><span data-stu-id="3cd59-326">Synopsys ARC HS</span></span>
* <span data-ttu-id="3cd59-327">x86</span><span class="sxs-lookup"><span data-stu-id="3cd59-327">x86</span></span>

<span data-ttu-id="3cd59-328">Azure RTOS ThreadX *SMP, n* işlemci arasında dinamik yük dengeleme gerçekleştirir ve tüm Azure RTOS ThreadX kaynaklarına (kuyruklar, semaforlar, olay bayrakları, bellek havuzları vb.) herhangi bir çekirdek üzerindeki herhangi bir iş parçacığı tarafından erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cd59-328">Azure RTOS ThreadX SMP performs dynamic load balancing across *n* processors and allows all Azure RTOS ThreadX resources (queues, semaphores, event flags, memory pools, etc.) to be accessed by any thread on any core.</span></span> <span data-ttu-id="3cd59-329">Azure RTOS ThreadX SMP, tüm çekirdeklerde Azure RTOS ThreadX API'sini tam olarak sağlar ve aşağıdaki yeni API'nin SMP işlemi için geçerli olduğunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="3cd59-329">Azure RTOS ThreadX SMP enables the complete Azure RTOS ThreadX API on all cores and introduces the following new API’s applicable to SMP operation:</span></span>

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a><span data-ttu-id="3cd59-330">Azure RTOS ThreadX Modülleri aracılığıyla bellek koruması</span><span class="sxs-lookup"><span data-stu-id="3cd59-330">Memory protection via Azure RTOS ThreadX Modules</span></span>

<span data-ttu-id="3cd59-331">Azure RTOS ThreadX MODULES adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının dinamik olarak hedefte dinamik olarak yüklenemiyor ve çalıştırılana (veya yerinde yürütülebilir) bir "Modül" içinde paketlenesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cd59-331">An add-on product called Azure RTOS ThreadX MODULES enables one or more application threads to be bundled into a “Module” that can be dynamically loaded and run (or executed in place) on the target.</span></span>

<span data-ttu-id="3cd59-332">Modüller, büyük uygulamaların yalnızca etkin iş parçacıklarının ihtiyaç sahip olduğu belleği kaplayacak şekilde alan yükseltme, hata düzeltme ve program bölümlelene olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cd59-332">Modules enable field upgrade, bug fixing, and program partitioning to allow large applications to occupy only the memory needed by active threads.</span></span>

<span data-ttu-id="3cd59-333">Ayrıca modüller, ThreadX'in kendi kendine Azure RTOS adres alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-333">Modules also have a completely separate address space from Azure RTOS ThreadX itself.</span></span> <span data-ttu-id="3cd59-334">Bu Azure RTOS ThreadX'in modüle bellek koruması (MPU veya MMU aracılığıyla) yer açmasını sağlar. Bu sayede modülün dışından yanlışlıkla erişilenler başka bir yazılım bileşenini bozmaz.</span><span class="sxs-lookup"><span data-stu-id="3cd59-334">This enables Azure RTOS ThreadX to place memory protection (via MPU or MMU) around the Module such that accidental access outside the module will not be able to corrupt any other software component.</span></span>

## <a name="misra-compliant"></a><span data-ttu-id="3cd59-335">MISRA uyumlu</span><span class="sxs-lookup"><span data-stu-id="3cd59-335">MISRA compliant</span></span>

<span data-ttu-id="3cd59-336">Azure RTOS ThreadX ve Azure RTOS ThreadX SMP kaynak kodu MISRA-C:2004 ve MISRA C:2012 ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="3cd59-336">Azure RTOS ThreadX and Azure RTOS ThreadX SMP source code is MISRA-C:2004 and MISRA C:2012 compliant.</span></span> <span data-ttu-id="3cd59-337">MISRA C, C programlama dilini kullanan kritik sistemler için bir dizi programlama kılavuzudur.</span><span class="sxs-lookup"><span data-stu-id="3cd59-337">MISRA C is a set of programming guidelines for critical systems using the C programming language.</span></span> <span data-ttu-id="3cd59-338">Özgün MISRA C yönergeleri öncelikli olarak otomotiv uygulamalarına yönelikti; ancak, MISRA C artık güvenlik açısından kritik herhangi bir uygulama için geçerli olduğu geniş ölçüde kabul ediliyor.</span><span class="sxs-lookup"><span data-stu-id="3cd59-338">The original MISRA C guidelines were primarily targeted toward automotive applications; however, MISRA C is now widely recognized as being applicable to any safety-critical application.</span></span> <span data-ttu-id="3cd59-339">Azure RTOS ThreadX, MISRA-C:2004 ve MISRA C:2012'nin tüm gerekli ve zorunlu kurallarıyla uyumludur.</span><span class="sxs-lookup"><span data-stu-id="3cd59-339">Azure RTOS ThreadX is compliant with all required and mandatory rules of MISRA-C:2004 and MISRA C:2012.</span></span>

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Misra sertifikası":::

## <a name="supports-most-popular-tools"></a><span data-ttu-id="3cd59-341">En popüler araçları destekler</span><span class="sxs-lookup"><span data-stu-id="3cd59-341">Supports most popular tools</span></span>

<span data-ttu-id="3cd59-342">Azure RTOS ThreadX, kullanılabilir en kapsamlı Azure RTOS ThreadX çekirdek farkındalığını da içeren IAR Embedded Workbench™ dahil olmak üzere en popüler tümleşik geliştirme araçlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="3cd59-342">Azure RTOS ThreadX supports most popular embedded development tools, including IAR’s Embedded Workbench™, which also has the most comprehensive Azure RTOS ThreadX kernel awareness available.</span></span> <span data-ttu-id="3cd59-343">Ek araç tümleştirmesi gnu (GCC), ARM DS-5/uVision®, Green River MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauteruter trace32®, TI Code-Composer Studio, CrossCore ve tüm analog cihazları içerir.</span><span class="sxs-lookup"><span data-stu-id="3cd59-343">Additional tool integration includes GNU (GCC), ARM DS-5/uVision®, Green Hills MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer Studio, CrossCore and all analog devices.</span></span>

## <a name="adaptation-layer-for-threadx"></a><span data-ttu-id="3cd59-344">ThreadX için uyarlama katmanı</span><span class="sxs-lookup"><span data-stu-id="3cd59-344">Adaptation layer for ThreadX</span></span>

<span data-ttu-id="3cd59-345">Azure RTOS ThreadX, özellikle sağlam bir şekilde eklenmiş uygulamalar için tasarlanan gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS).</span><span class="sxs-lookup"><span data-stu-id="3cd59-345">Azure RTOS ThreadX is an advanced real-time operating system (RTOS) designed specifically for deeply embedded applications.</span></span> <span data-ttu-id="3cd59-346">ThreadX, Auzre RTOS'a uygulama [](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) geçişini kolaylaştırmanıza yardımcı olmak için çeşitli eski RTOS API'leri (FreeRTOS, POSIX, OSEK vb.) için uyarlama katmanları sağlar</span><span class="sxs-lookup"><span data-stu-id="3cd59-346">To help ease application migration to Auzre RTOS, ThreadX provides [adaption layers](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) for various legacy RTOS APIs (FreeRTOS, POSIX, OSEK, etc.)</span></span>
