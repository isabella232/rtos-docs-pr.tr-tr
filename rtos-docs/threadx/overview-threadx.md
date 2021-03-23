---
title: Azure RTOS ThreadX 'i anlama
description: Azure ThreadX, özellikle derin eklenmiş uygulamalar için tasarlanan gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS).
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: acee58d9c48cb7a66993aaa5dc4a565dfe96234d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827346"
---
# <a name="overview-of-azure-rtos-threadx"></a><span data-ttu-id="75e91-103">Azure RTOS ThreadX 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="75e91-103">Overview of Azure RTOS ThreadX</span></span>

<span data-ttu-id="75e91-104">Azure RTOS ThreadX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft 'un gelişmiş endüstriyel sınıf Real-Time Işletim sistemidir (RTOS).</span><span class="sxs-lookup"><span data-stu-id="75e91-104">Azure RTOS ThreadX is Microsoft's advanced industrial grade Real-Time Operating System (RTOS) designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="75e91-105">Azure RTOS ThreadX, Gelişmiş zamanlama, iletişim, eşitleme, süreölçer, bellek yönetimi ve kesme yönetim olanakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="75e91-105">Azure RTOS ThreadX provides advanced scheduling, communication, synchronization, timer, memory management, and interrupt management facilities.</span></span> <span data-ttu-id="75e91-106">Ayrıca, Azure RTOS ThreadX 'in picokernel™ mimarisi, önalım-Threshold™ zamanlama, olay zincirleme,™ yürütme profili oluşturma, performans ölçümleri ve sistem olay izleme dahil birçok gelişmiş özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="75e91-106">In addition, Azure RTOS ThreadX has many advanced features, including its picokernel™ architecture, preemption-threshold™ scheduling, event-chaining,™ execution profiling, performance metrics, and system event tracing.</span></span> <span data-ttu-id="75e91-107">En üstün kullanım kolaylığıyla birlikte, Azure RTOS ThreadX, katıştırılmış uygulamaların en zorlu kullanımı için ideal seçenektir.</span><span class="sxs-lookup"><span data-stu-id="75e91-107">Combined with its superior ease-of-use, Azure RTOS ThreadX is the ideal choice for the most demanding of embedded applications.</span></span> <span data-ttu-id="75e91-108">2017 itibariyle, Azure RTOS ThreadX, tüketici cihazları, tıbbi elektronik ve endüstriyel denetim ekipmanı dahil olmak üzere çok çeşitli ürünlerde 6.200.000.000 ' den fazla dağıtıma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="75e91-108">As of 2017, Azure RTOS ThreadX has over 6.2 billion deployments, in a wide variety of products, including consumer devices, medical electronics, and industrial control equipment.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="75e91-109">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="75e91-109">API Protocols</span></span>

### <a name="azure-rtos-threadx-api"></a><span data-ttu-id="75e91-110">Azure RTOS ThreadX API 'SI</span><span class="sxs-lookup"><span data-stu-id="75e91-110">Azure RTOS ThreadX API</span></span>

* <span data-ttu-id="75e91-111">Sezgisel ve tutarlı API</span><span class="sxs-lookup"><span data-stu-id="75e91-111">Intuitive and consistent API</span></span>
* <span data-ttu-id="75e91-112">İsim-fiil adlandırma kuralı</span><span class="sxs-lookup"><span data-stu-id="75e91-112">Noun-verb naming convention</span></span>
* <span data-ttu-id="75e91-113">Tüm API 'Lerde Azure RTOS ThreadX olarak kolayca tanımlanabilmesi için önde gelen *tx_* vardır</span><span class="sxs-lookup"><span data-stu-id="75e91-113">All APIs have leading *tx_* to easily identify as Azure RTOS ThreadX</span></span>
* <span data-ttu-id="75e91-114">API 'Lerin engellenmesi isteğe bağlı iş parçacığı zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="75e91-114">Blocking APIs have optional thread timeout</span></span>
* <span data-ttu-id="75e91-115">Birçok API uygulama ISRs 'den doğrudan kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="75e91-115">Many APIs are directly available from application ISRs</span></span>

### <a name="azure-rtos-threadx-services"></a><span data-ttu-id="75e91-116">Azure RTOS ThreadX Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="75e91-116">Azure RTOS ThreadX Services</span></span>

* <span data-ttu-id="75e91-117">Dinamik iş parçacığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-117">Dynamic thread creation</span></span>
* <span data-ttu-id="75e91-118">İş parçacığı sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="75e91-118">No limits on the number of threads</span></span>
* <span data-ttu-id="75e91-119">Ana iş parçacığı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="75e91-119">Main thread APIs include:</span></span>
  * <span data-ttu-id="75e91-120">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="75e91-120">tx_thread_create</span></span>
  * <span data-ttu-id="75e91-121">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-121">tx_thread_delete</span></span>
  * <span data-ttu-id="75e91-122">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="75e91-122">tx_thread_preemption_change</span></span>
  * <span data-ttu-id="75e91-123">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="75e91-123">tx_thread_priority_change</span></span>
  * <span data-ttu-id="75e91-124">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="75e91-124">tx_thread_relinquish</span></span>
  * <span data-ttu-id="75e91-125">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="75e91-125">tx_thread_reset</span></span>
  * <span data-ttu-id="75e91-126">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="75e91-126">tx_thread_resume</span></span>
  * <span data-ttu-id="75e91-127">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="75e91-127">tx_thread_sleep</span></span>
  * <span data-ttu-id="75e91-128">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="75e91-128">tx_thread_suspend</span></span>
  * <span data-ttu-id="75e91-129">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="75e91-129">tx_thread_terminate</span></span>
  * <span data-ttu-id="75e91-130">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="75e91-130">tx_thread_wait_abort</span></span>
* <span data-ttu-id="75e91-131">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-131">Additional information and performance APIs</span></span>

### <a name="message-queues"></a><span data-ttu-id="75e91-132">İleti kuyrukları</span><span class="sxs-lookup"><span data-stu-id="75e91-132">Message Queues</span></span>

* <span data-ttu-id="75e91-133">Dinamik sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-133">Dynamic queue creation</span></span>
* <span data-ttu-id="75e91-134">Sıra sayısında sınırlama yoktur</span><span class="sxs-lookup"><span data-stu-id="75e91-134">No limits on the number of queues</span></span>
* <span data-ttu-id="75e91-135">Değer (veya işaretçi aracılığıyla başvuruya göre) tarafından kopyalanmış iletiler</span><span class="sxs-lookup"><span data-stu-id="75e91-135">Messages copied by value (or by reference via pointer)</span></span>
* <span data-ttu-id="75e91-136">1 ile 16 32 bitlik sözcüklerden oluşan ileti boyutları</span><span class="sxs-lookup"><span data-stu-id="75e91-136">Message sizes from 1 to 16 32-bit words</span></span>
* <span data-ttu-id="75e91-137">Empty ve Full üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="75e91-137">Optional thread suspension on empty and full</span></span>
* <span data-ttu-id="75e91-138">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="75e91-138">Optional timeout on all suspension</span></span>
* <span data-ttu-id="75e91-139">Ana ileti kuyruğu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="75e91-139">Main message queue APIs include:</span></span>
  * <span data-ttu-id="75e91-140">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="75e91-140">tx_queue_create</span></span>
  * <span data-ttu-id="75e91-141">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-141">tx_queue_delete</span></span>
  * <span data-ttu-id="75e91-142">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="75e91-142">tx_queue_flush</span></span>
  * <span data-ttu-id="75e91-143">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="75e91-143">tx_queue_front_send</span></span>
  * <span data-ttu-id="75e91-144">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="75e91-144">tx_queue_receive</span></span>
  * <span data-ttu-id="75e91-145">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="75e91-145">tx_queue_send_notify</span></span>
* <span data-ttu-id="75e91-146">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-146">Additional information and performance APIs</span></span>

### <a name="counting-semaphores"></a><span data-ttu-id="75e91-147">Semafor sayma</span><span class="sxs-lookup"><span data-stu-id="75e91-147">Counting Semaphores</span></span>

* <span data-ttu-id="75e91-148">Dinamik semafor oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-148">Dynamic semaphore creation</span></span>
* <span data-ttu-id="75e91-149">Semafor sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="75e91-149">No limits on the number of semaphores</span></span>
* <span data-ttu-id="75e91-150">32-bit sayma semaforları (0-4.294.967.295)</span><span class="sxs-lookup"><span data-stu-id="75e91-150">32-bit counting semaphores (0 to 4,294,967,295)</span></span>
* <span data-ttu-id="75e91-151">Tüketici-üretici veya kaynak korumasını destekler</span><span class="sxs-lookup"><span data-stu-id="75e91-151">Supports consumer-producer or resource protection</span></span>
* <span data-ttu-id="75e91-152">Semafor kullanılamadığında isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="75e91-152">Optional thread suspension when semaphore unavailable</span></span>
* <span data-ttu-id="75e91-153">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="75e91-153">Optional timeout on all suspension</span></span>
* <span data-ttu-id="75e91-154">Ana semafor API 'Leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="75e91-154">Main semaphore APIs include:</span></span>
  * <span data-ttu-id="75e91-155">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="75e91-155">tx_semaphore_create</span></span>
  * <span data-ttu-id="75e91-156">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-156">tx_semaphore_delete</span></span>
  * <span data-ttu-id="75e91-157">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="75e91-157">tx_semaphore_get</span></span>
  * <span data-ttu-id="75e91-158">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="75e91-158">tx_semaphore_put</span></span>
  * <span data-ttu-id="75e91-159">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="75e91-159">tx_semaphore_put_notify</span></span>
* <span data-ttu-id="75e91-160">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-160">Additional information and performance APIs</span></span>

### <a name="mutexes"></a><span data-ttu-id="75e91-161">Zaman Uyumu Sağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="75e91-161">Mutexes</span></span>

* <span data-ttu-id="75e91-162">Dinamik mutex oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-162">Dynamic mutex creation</span></span>
* <span data-ttu-id="75e91-163">Birbirini kapsamayan sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="75e91-163">No limits on the number of mutexes</span></span>
* <span data-ttu-id="75e91-164">İç içe kaynak koruması destekleniyor</span><span class="sxs-lookup"><span data-stu-id="75e91-164">Nested resource protection supported</span></span>
* <span data-ttu-id="75e91-165">İsteğe bağlı öncelikli devralma destekleniyor</span><span class="sxs-lookup"><span data-stu-id="75e91-165">Optional priority inheritance supported</span></span>
* <span data-ttu-id="75e91-166">Mutex kullanılamadığında isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="75e91-166">Optional thread suspension when mutex unavailable</span></span>
* <span data-ttu-id="75e91-167">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="75e91-167">Optional timeout on all suspension</span></span>
* <span data-ttu-id="75e91-168">Ana mutex API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="75e91-168">Main mutex APIs include:</span></span>
  * <span data-ttu-id="75e91-169">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="75e91-169">tx_mutex_create</span></span>
  * <span data-ttu-id="75e91-170">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-170">tx_mutex_delete</span></span>
  * <span data-ttu-id="75e91-171">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="75e91-171">tx_mutex_get</span></span>
  * <span data-ttu-id="75e91-172">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="75e91-172">tx_mutex_put</span></span>
* <span data-ttu-id="75e91-173">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-173">Additional information and performance APIs</span></span>

### <a name="event-flags"></a><span data-ttu-id="75e91-174">Olay bayrakları</span><span class="sxs-lookup"><span data-stu-id="75e91-174">Event Flags</span></span>

* <span data-ttu-id="75e91-175">Dinamik olay bayrağı Grup oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-175">Dynamic event flag group creation</span></span>
* <span data-ttu-id="75e91-176">Olay bayrak grupları sayısında sınırlama yok</span><span class="sxs-lookup"><span data-stu-id="75e91-176">No limits on the number of event flag groups</span></span>
* <span data-ttu-id="75e91-177">Bir iş parçacığının veya birden çok iş parçacığının eşitlenmesi</span><span class="sxs-lookup"><span data-stu-id="75e91-177">Synchronization of one thread or multiple threads</span></span>
* <span data-ttu-id="75e91-178">Atomik get ve Clear destekleniyor</span><span class="sxs-lookup"><span data-stu-id="75e91-178">Atomic get and clear supported</span></span>
* <span data-ttu-id="75e91-179">İsteğe bağlı çoklu iş parçacığı açma ve/veya olay kümesi askıya alma</span><span class="sxs-lookup"><span data-stu-id="75e91-179">Optional multithread suspension on AND/OR set of events</span></span>
* <span data-ttu-id="75e91-180">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="75e91-180">Optional timeout on all suspension</span></span>
* <span data-ttu-id="75e91-181">Ana olay bayrağı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="75e91-181">Main event flag APIs include:</span></span>
  * <span data-ttu-id="75e91-182">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="75e91-182">tx_event_flags_create</span></span>
  * <span data-ttu-id="75e91-183">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-183">tx_event_flags_delete</span></span>
  * <span data-ttu-id="75e91-184">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="75e91-184">tx_event_flags_get</span></span>
  * <span data-ttu-id="75e91-185">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="75e91-185">tx_event_flags_set</span></span>
  * <span data-ttu-id="75e91-186">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="75e91-186">tx_event_flags_set_notify</span></span>
* <span data-ttu-id="75e91-187">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-187">Additional information and performance APIs</span></span>

### <a name="block-memory-pools"></a><span data-ttu-id="75e91-188">Bellek havuzlarını engelle</span><span class="sxs-lookup"><span data-stu-id="75e91-188">Block Memory Pools</span></span>

* <span data-ttu-id="75e91-189">Dinamik blok havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-189">Dynamic block pool creation</span></span>
* <span data-ttu-id="75e91-190">Blok havuzları sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="75e91-190">No limits on the number of block pools</span></span>
* <span data-ttu-id="75e91-191">Sabit boyutlu blokların boyutu veya havuzun boyutu için sınır yok</span><span class="sxs-lookup"><span data-stu-id="75e91-191">No limits on size of fixed-size blocks or size of pool</span></span>
* <span data-ttu-id="75e91-192">En hızlı olası bellek ayırma/anlaşma konumu</span><span class="sxs-lookup"><span data-stu-id="75e91-192">Fastest possible memory allocation/deal-location</span></span>
* <span data-ttu-id="75e91-193">Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="75e91-193">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="75e91-194">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="75e91-194">Optional timeout on all suspension</span></span>
* <span data-ttu-id="75e91-195">Ana blok havuzu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="75e91-195">Main block pool APIs include:</span></span>
  * <span data-ttu-id="75e91-196">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="75e91-196">tx_block_pool_create</span></span>
  * <span data-ttu-id="75e91-197">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-197">tx_block_pool_delete</span></span>
  * <span data-ttu-id="75e91-198">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="75e91-198">tx_block_allocate</span></span>
  * <span data-ttu-id="75e91-199">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="75e91-199">tx_block_release</span></span>
* <span data-ttu-id="75e91-200">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-200">Additional information and performance APIs</span></span>

### <a name="byte-memory-pools"></a><span data-ttu-id="75e91-201">Bayt bellek havuzları</span><span class="sxs-lookup"><span data-stu-id="75e91-201">Byte Memory Pools</span></span>

* <span data-ttu-id="75e91-202">Dinamik bayt havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-202">Dynamic byte pool creation</span></span>
* <span data-ttu-id="75e91-203">Bayt havuzları sayısında sınır yoktur</span><span class="sxs-lookup"><span data-stu-id="75e91-203">No limits on the number of byte pools</span></span>
* <span data-ttu-id="75e91-204">Bayt havuzunun boyutu için sınır yok</span><span class="sxs-lookup"><span data-stu-id="75e91-204">No limits on size of byte pool</span></span>
* <span data-ttu-id="75e91-205">En esnek değişken uzunluklu bellek ayırma/ayırmayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="75e91-205">Most flexible variable-length memory allocation/deallocation</span></span>
* <span data-ttu-id="75e91-206">Ayırma boyutu yerleşim destekleniyor</span><span class="sxs-lookup"><span data-stu-id="75e91-206">Allocation size locality supported</span></span>
* <span data-ttu-id="75e91-207">Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="75e91-207">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="75e91-208">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="75e91-208">Optional timeout on all suspension</span></span>
* <span data-ttu-id="75e91-209">Ana bayt havuzu API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="75e91-209">Main byte pool APIs include:</span></span>
  * <span data-ttu-id="75e91-210">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="75e91-210">tx_byte_pool_create</span></span>
  * <span data-ttu-id="75e91-211">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-211">tx_byte_pool_delete</span></span>
  * <span data-ttu-id="75e91-212">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="75e91-212">tx_byte_allocate</span></span>
  * <span data-ttu-id="75e91-213">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="75e91-213">tx_byte_release</span></span>
* <span data-ttu-id="75e91-214">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-214">Additional information and performance APIs</span></span>

### <a name="application-timers"></a><span data-ttu-id="75e91-215">Uygulama zamanlayıcıları</span><span class="sxs-lookup"><span data-stu-id="75e91-215">Application Timers</span></span>

* <span data-ttu-id="75e91-216">Dinamik süreölçer oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-216">Dynamic timer creation</span></span>
* <span data-ttu-id="75e91-217">Zamanlayıcılar sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="75e91-217">No limits on the number of timers</span></span>
* <span data-ttu-id="75e91-218">Düzenli veya tek atışı Zamanlayıcı destekleniyor</span><span class="sxs-lookup"><span data-stu-id="75e91-218">Periodic or one-shot timers supported</span></span>
* <span data-ttu-id="75e91-219">Düzenli zamanlayıcılar farklı başlangıç son kullanma değerine sahip olabilir</span><span class="sxs-lookup"><span data-stu-id="75e91-219">Periodic timers may have different initial expiration value</span></span>
* <span data-ttu-id="75e91-220">Süreölçer etkinleştirme veya devre dışı bırakma üzerinde arama yok</span><span class="sxs-lookup"><span data-stu-id="75e91-220">No searching on timer activation or deactivation</span></span>
* <span data-ttu-id="75e91-221">Bir donanım Zamanlayıcı kesmesinin yönettiği tüm zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="75e91-221">All timers driven from one hardware timer interrupt</span></span>
* <span data-ttu-id="75e91-222">Ana Zamanlayıcı API 'Leri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="75e91-222">Main timer APIs include:</span></span>
  * <span data-ttu-id="75e91-223">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="75e91-223">tx_timer_create</span></span>
  * <span data-ttu-id="75e91-224">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="75e91-224">tx_timer_delete</span></span>
  * <span data-ttu-id="75e91-225">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="75e91-225">tx_timer_activate</span></span>
  * <span data-ttu-id="75e91-226">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="75e91-226">tx_timer_change</span></span>
  * <span data-ttu-id="75e91-227">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="75e91-227">tx_timer_deactivate</span></span>
* <span data-ttu-id="75e91-228">Ek bilgi ve performans API 'Leri</span><span class="sxs-lookup"><span data-stu-id="75e91-228">Additional information and performance APIs</span></span>

### <a name="azure-rtos-threadx-core-scheduler"></a><span data-ttu-id="75e91-229">Azure RTOS ThreadX çekirdek Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="75e91-229">Azure RTOS ThreadX Core Scheduler</span></span>

* <span data-ttu-id="75e91-230">Minimum 2 KB FLASH, 1KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="75e91-230">Minimal 2KB FLASH,1KB RAM footprint</span></span>
* <span data-ttu-id="75e91-231">Fast, Sub-mikro ikinci bağlam-anahtar</span><span class="sxs-lookup"><span data-stu-id="75e91-231">Fast, sub-microsecond context-switch</span></span>
* <span data-ttu-id="75e91-232">İş parçacığı sayısından bağımsız olarak tam belirleyici</span><span class="sxs-lookup"><span data-stu-id="75e91-232">Fully deterministic regardless of number of threads</span></span>
* <span data-ttu-id="75e91-233">Öncelik temelli, tam preemptive-zamanlama</span><span class="sxs-lookup"><span data-stu-id="75e91-233">Priority-based, fully preemptive-scheduling</span></span>
* <span data-ttu-id="75e91-234">32 varsayılan öncelik düzeyleri, isteğe bağlı olarak 1024 düzeye kadar</span><span class="sxs-lookup"><span data-stu-id="75e91-234">32 default priority levels, optionally up to 1024 levels</span></span>
* <span data-ttu-id="75e91-235">Öncelik düzeyi (FıFO) içinde ortak zamanlama</span><span class="sxs-lookup"><span data-stu-id="75e91-235">Cooperative scheduling within priority level (FIFO)</span></span>
* <span data-ttu-id="75e91-236">Önalım-Threshold teknolojisi</span><span class="sxs-lookup"><span data-stu-id="75e91-236">Preemption-threshold technology</span></span>
* <span data-ttu-id="75e91-237">Aşağıdakiler dahil isteğe bağlı Zamanlayıcı Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="75e91-237">Optional timer services, including:</span></span>
  * <span data-ttu-id="75e91-238">İş parçacığı başına isteğe bağlı saat dilimi</span><span class="sxs-lookup"><span data-stu-id="75e91-238">Per-thread optional time-slice</span></span>
  * <span data-ttu-id="75e91-239">Tüm engellemede isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="75e91-239">Optional timeout on all blocking</span></span>
  * <span data-ttu-id="75e91-240">API 'Ler donanım süreölçer kesmesi gerektirir</span><span class="sxs-lookup"><span data-stu-id="75e91-240">APIs Requires on hardware timer interrupt</span></span>
* <span data-ttu-id="75e91-241">Yürütme profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="75e91-241">Execution profiling</span></span>
* <span data-ttu-id="75e91-242">Sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="75e91-242">System-level Trace</span></span>
* <span data-ttu-id="75e91-243">Birçok standartlara yönelik güvenlik sertifikalı</span><span class="sxs-lookup"><span data-stu-id="75e91-243">Safety certified to many standards</span></span>

## <a name="most-deployed-rtos"></a><span data-ttu-id="75e91-244">En çok dağıtılan RTOS</span><span class="sxs-lookup"><span data-stu-id="75e91-244">Most deployed RTOS</span></span>

<span data-ttu-id="75e91-245">Azure RTOS ThreadX, önde gelen 'U M2M Market Intelligence firması, VDC Research 'e göre dünya genelinde 6.200.000.000 dağıtımlara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="75e91-245">Azure RTOS ThreadX has over 6.2 billion deployments worldwide, according to the leading M2M market intelligence firm, VDC Research.</span></span> <span data-ttu-id="75e91-246">Azure RTOS ThreadX 'in popülerliği, güvenilirliği, kalitesi, boyutu, performansı, gelişmiş özellikler, kullanım kolaylığı ve genel kullanım süresi avantajına yönelik bir testdir.</span><span class="sxs-lookup"><span data-stu-id="75e91-246">The popularity of Azure RTOS ThreadX is a testament to its reliability, quality, size, performance, advanced features, ease-of-use, and overall time-to-market advantages.</span></span>

> <span data-ttu-id="75e91-247">*"Şirketin temelleri ile bu yana kablosuz ve IoT pazarlarında THREADX 'in büyüme tratrumuzu izliyoruz ve THREADX 'in yaygın sektör benimsemesi tarafından giderek daha da artmaktadır."*</span><span class="sxs-lookup"><span data-stu-id="75e91-247">*“We have followed the growth trajectory of THREADX in the wireless and IoT markets since the company’s founding, and are increasingly impressed by the widespread industry adoption of THREADX.”*</span></span> <span data-ttu-id="75e91-248">– Chris Rommel, Executive Başkan Yardımcısı, VDC Research</span><span class="sxs-lookup"><span data-stu-id="75e91-248">– Chris Rommel, Executive Vice President, VDC Research</span></span>

## <a name="small-footprint"></a><span data-ttu-id="75e91-249">Küçük ayak izi</span><span class="sxs-lookup"><span data-stu-id="75e91-249">Small footprint</span></span>

<span data-ttu-id="75e91-250">Azure RTOS ThreadX, en az bir kaplama için remarkalı küçük 2KB yönerge alanı ve 1KB RAM gerektirir.</span><span class="sxs-lookup"><span data-stu-id="75e91-250">Azure RTOS ThreadX requires a remarkably small 2KB instruction area and 1KB of RAM for its minimal footprint.</span></span> <span data-ttu-id="75e91-251">Bu, büyük bir olasılıkla katmanlı olmayan picokernel™ mimarisi ve otomatik ölçeklendirmesinden kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="75e91-251">This is largely due to its non-layered picokernel™ architecture and automatic scaling.</span></span> <span data-ttu-id="75e91-252">Otomatik ölçeklendirme, uygulama tarafından kullanılan hizmetlerin (ve destekleyici altyapının) bağlantı zamanında son görüntüye dahil olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="75e91-252">Automatic scaling means that only the services (and supporting infrastructure) used by the application are included in the final image at link time.</span></span>

<span data-ttu-id="75e91-253">Bazı tipik Azure RTOS ThreadX boyut özellikleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="75e91-253">Here are some typical Azure RTOS ThreadX size characteristics:</span></span>

|<span data-ttu-id="75e91-254">Azure RTOS ThreadX hizmeti</span><span class="sxs-lookup"><span data-stu-id="75e91-254">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="75e91-255">Bayt cinsinden normal boyut</span><span class="sxs-lookup"><span data-stu-id="75e91-255">Typical Size in Bytes</span></span>  |
|---------|---------|
|<span data-ttu-id="75e91-256">Çekirdek hizmetler (gerekli)</span><span class="sxs-lookup"><span data-stu-id="75e91-256">Core Services (Require)</span></span> |<span data-ttu-id="75e91-257">2.000</span><span class="sxs-lookup"><span data-stu-id="75e91-257">2,000</span></span>  |
|<span data-ttu-id="75e91-258">Kuyruk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="75e91-258">Queue Services</span></span>  |<span data-ttu-id="75e91-259">900</span><span class="sxs-lookup"><span data-stu-id="75e91-259">900</span></span>  |
|<span data-ttu-id="75e91-260">Olay bayrağı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="75e91-260">Event Flag Services</span></span>  |<span data-ttu-id="75e91-261">900</span><span class="sxs-lookup"><span data-stu-id="75e91-261">900</span></span>  |
|<span data-ttu-id="75e91-262">Semafor Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="75e91-262">Semaphore Services</span></span>  |<span data-ttu-id="75e91-263">450</span><span class="sxs-lookup"><span data-stu-id="75e91-263">450</span></span>  |
|<span data-ttu-id="75e91-264">Mutex Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="75e91-264">Mutex Services</span></span>  |<span data-ttu-id="75e91-265">1.200</span><span class="sxs-lookup"><span data-stu-id="75e91-265">1,200</span></span>  |
|<span data-ttu-id="75e91-266">Bellek hizmetlerini engelle</span><span class="sxs-lookup"><span data-stu-id="75e91-266">Block Memory Services</span></span>  |<span data-ttu-id="75e91-267">550</span><span class="sxs-lookup"><span data-stu-id="75e91-267">550</span></span>  |
|<span data-ttu-id="75e91-268">Bayt bellek Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="75e91-268">Byte Memory Services</span></span>  |<span data-ttu-id="75e91-269">900</span><span class="sxs-lookup"><span data-stu-id="75e91-269">900</span></span>  |

## <a name="fast-execution"></a><span data-ttu-id="75e91-270">Hızlı yürütme</span><span class="sxs-lookup"><span data-stu-id="75e91-270">Fast execution</span></span>

<span data-ttu-id="75e91-271">Azure RTOS ThreadX, en popüler işlemciler üzerinde bir alt mikro ikinci bağlam anahtarına erişir ve diğer ticari ortamlarından çok daha hızlı bir şekilde genel olarak daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="75e91-271">Azure RTOS ThreadX achieves a sub-microsecond context switch on most popular processors and is significantly faster overall than other commercial RTOSes.</span></span> <span data-ttu-id="75e91-272">Hızlı olmasının yanı sıra Azure RTOS ThreadX de oldukça belirleyici bir niteliğindedir.</span><span class="sxs-lookup"><span data-stu-id="75e91-272">In addition to being fast, Azure RTOS ThreadX is also highly deterministic.</span></span> <span data-ttu-id="75e91-273">Yalnızca bir tane veya tek bir 200 iş parçacığı olup olmadığı için aynı hızlı performansa erişir.</span><span class="sxs-lookup"><span data-stu-id="75e91-273">It achieves the same fast performance whether there are 200 threads ready, or just one.</span></span>

<span data-ttu-id="75e91-274">Azure RTOS ThreadX 'in bazı tipik performans özellikleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="75e91-274">Here are some typical performance characteristics of Azure RTOS ThreadX:</span></span>

* <span data-ttu-id="75e91-275">Hızlı önyükleme: 120 ' den az Döngülerde Azure RTOS ThreadX önyüklemeleri.</span><span class="sxs-lookup"><span data-stu-id="75e91-275">Fast Boot: Azure RTOS ThreadX boots in less than 120 cycles.</span></span>
* <span data-ttu-id="75e91-276">Temel hata denetimi için isteğe bağlı kaldırma: temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="75e91-276">Optional Removal of basic error checking: Basic Azure RTOS ThreadX error checking can be skipped at compile time.</span></span> <span data-ttu-id="75e91-277">Bu, uygulama kodu doğrulandığında ve her parametreye artık hata denetimi gerektirmeyen yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="75e91-277">This can be useful when the application code is verified and no longer requires error checking on each parameter.</span></span> <span data-ttu-id="75e91-278">Bunun, sistem genelinde değil, bir derleme birimi üzerinde yapılabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75e91-278">Note that this can be done on a compilation unit, rather than system-wide.</span></span>
* <span data-ttu-id="75e91-279">Picokernel™ tasarımı: hizmetler birbirlerine katmanlı değildir, bu nedenle gereksiz işlev çağrısı yükünü ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="75e91-279">Picokernel™ Design: Services are not layered on each other, thus eliminating unnecessary function call overhead.</span></span>
* <span data-ttu-id="75e91-280">\* İyileştirilmiş kesme Işleme: önalım gerekli değilse, yalnızca karalama kayıtları ıSR girdisi/çıkış üzerine kaydedilir/geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="75e91-280">\*Optimized Interrupt Processing: Only scratch registers are saved/restored upon ISR entry/exit, unless preemption is necessary.</span></span>
* <span data-ttu-id="75e91-281">İyileştirilmiş API Işleme:</span><span class="sxs-lookup"><span data-stu-id="75e91-281">Optimized API Processing:</span></span>

    |<span data-ttu-id="75e91-282">Azure RTOS ThreadX hizmeti</span><span class="sxs-lookup"><span data-stu-id="75e91-282">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="75e91-283">Mikrosaniye cinsinden Hizmet Süresi \*</span><span class="sxs-lookup"><span data-stu-id="75e91-283">Service Time in Microseconds\*</span></span>  |
    |---------|---------|
    |<span data-ttu-id="75e91-284">İş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="75e91-284">Thread Suspend</span></span>  |<span data-ttu-id="75e91-285">0.6</span><span class="sxs-lookup"><span data-stu-id="75e91-285">0.6</span></span>  |
    |<span data-ttu-id="75e91-286">İş parçacığı özgeçmişi</span><span class="sxs-lookup"><span data-stu-id="75e91-286">Thread Resume</span></span>  |<span data-ttu-id="75e91-287">0.6</span><span class="sxs-lookup"><span data-stu-id="75e91-287">0.6</span></span>  |
    |<span data-ttu-id="75e91-288">Kuyruğu gönder</span><span class="sxs-lookup"><span data-stu-id="75e91-288">Queue Send</span></span>  |<span data-ttu-id="75e91-289">0.3</span><span class="sxs-lookup"><span data-stu-id="75e91-289">0.3</span></span>  |
    |<span data-ttu-id="75e91-290">Kuyruk alma</span><span class="sxs-lookup"><span data-stu-id="75e91-290">Queue Receive</span></span>  |<span data-ttu-id="75e91-291">0.3</span><span class="sxs-lookup"><span data-stu-id="75e91-291">0.3</span></span>  |
    |<span data-ttu-id="75e91-292">Semafor al</span><span class="sxs-lookup"><span data-stu-id="75e91-292">Get Semaphore</span></span>  |<span data-ttu-id="75e91-293">0,2</span><span class="sxs-lookup"><span data-stu-id="75e91-293">0.2</span></span>  |
    |<span data-ttu-id="75e91-294">Semaforu koy</span><span class="sxs-lookup"><span data-stu-id="75e91-294">Put Semaphore</span></span>  |<span data-ttu-id="75e91-295">0,2</span><span class="sxs-lookup"><span data-stu-id="75e91-295">0.2</span></span>  |
    |<span data-ttu-id="75e91-296">Bağlam anahtarı</span><span class="sxs-lookup"><span data-stu-id="75e91-296">Context Switch</span></span>  |<span data-ttu-id="75e91-297">0,4</span><span class="sxs-lookup"><span data-stu-id="75e91-297">0.4</span></span>  |
    |<span data-ttu-id="75e91-298">Kesme yanıtı</span><span class="sxs-lookup"><span data-stu-id="75e91-298">Interrupt Response</span></span>  |<span data-ttu-id="75e91-299">0,0 – 0,6</span><span class="sxs-lookup"><span data-stu-id="75e91-299">0.0 – 0.6</span></span>  |

    <span data-ttu-id="75e91-300">\**200 MHz hızında çalışan normal işlemciyi temel alan performans rakamları*.</span><span class="sxs-lookup"><span data-stu-id="75e91-300">\**Performance figures based on typical processor running at 200MHz*.</span></span>

## <a name="pre-certified-by-tuv-and-ul-to-many-safety-standards"></a><span data-ttu-id="75e91-301">TUV ve UL ile birçok güvenlik standartlarına ön sertifikalı</span><span class="sxs-lookup"><span data-stu-id="75e91-301">Pre-certified by TUV and UL to many safety standards</span></span>

<span data-ttu-id="75e91-302">Azure RTOS ThreadX ve Azure RTOS ThreadX SMP, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW Safety Class C, ISO 26262 asıl D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir.</span><span class="sxs-lookup"><span data-stu-id="75e91-302">Azure RTOS ThreadX and Azure RTOS ThreadX SMP have been certified by SGS-TUV Saar for use in safety-critical systems, according to IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D and EN 50128.</span></span> <span data-ttu-id="75e91-303">Sertifika, Azure RTOS ThreadX ve Azure RTOS ThreadX SMP 'in, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımlar geliştirmesinde kullanılabileceğini onaylar.</span><span class="sxs-lookup"><span data-stu-id="75e91-303">The certification confirms that Azure RTOS ThreadX and Azure RTOS ThreadX SMP can be used in the development of safety-related software for the highest safety integrity levels of IEC-61508, IEC-62304, ISO 26262 and EN 50128 for the “Functional Safety of electrical, electronic, and programmable electronic safety-related systems.”</span></span> <span data-ttu-id="75e91-304">Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="75e91-304">SGS-TUV Saar, formed through a joint venture of Germany’s SGS-Group and TUV Saarland, has become the leading accredited, independent company for testing, auditing, verifying and certifying embedded software for safety-related systems worldwide.</span></span> <span data-ttu-id="75e91-305">Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil olmak üzere, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenliğini sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="75e91-305">The industrial safety standard IEC 61508, and all standards that are derived from it, including IEC-62304, ISO 26262 and EN 50128, are used to ensure the functional safety of electrical, electronic, and programmable electronic safety-related medical devices, process control systems, industrial machinery, automobiles and railway control systems.</span></span>

:::image type="content" source="media/overview-threadx/partener-logo-sgs-tuv-saar-2.png" alt-text="SGS TUV SAAR sertifikası":::

<span data-ttu-id="75e91-307">Azure RTOS ThreadX ve Azure RTOS ThreadX SMP, UL tarafından, ınım60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R 1998 ve programlanabilir.</span><span class="sxs-lookup"><span data-stu-id="75e91-307">Azure RTOS ThreadX and Azure RTOS ThreadX SMP have been recognized by UL for compliance with UL 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R, and UL 1998 safety standards for software in programmable components.</span></span> <span data-ttu-id="75e91-308">UL, en fazla uzman sürmek güvenlik çözümleri sunan küresel, bağımsız bir güvenlik bilimi şirketidir. Bu, elektrik, yenilenebilir enerji ve Nanotechnology için genel olarak elektrik 'yi benimseme özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="75e91-308">UL is a global, independent, safety-science company with more than a century of expertise innovating safety solutions, ranging from the public adoption of electricity to breakthroughs in sustainability, renewable energy, and nanotechnology.</span></span>

:::image type="content" source="media/overview-threadx/cru-logo-certification.png" alt-text="UL sertifikası":::

<span data-ttu-id="75e91-310">TUV ve UL sertifikalarıyla ilişkili yapıtlar (sertifika, güvenlik el kitabı, test raporu vb.) satış için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="75e91-310">Artifacts (Certificate, Safety Manual, Test Report, etc.) associated with the TUV and UL certifications are available for sale.</span></span>

## <a name="eal4-common-criteria-security-certification"></a><span data-ttu-id="75e91-311">EAL4 + ortak ölçütler güvenlik sertifikası</span><span class="sxs-lookup"><span data-stu-id="75e91-311">EAL4+ Common Criteria security certification</span></span>

<span data-ttu-id="75e91-312">Azure RTOS, EAL4 + ortak ölçütler güvenlik sertifikası elde etti.</span><span class="sxs-lookup"><span data-stu-id="75e91-312">Azure RTOS has achieved EAL4+ Common Criteria security certification.</span></span> <span data-ttu-id="75e91-313">Evalution (TOE) hedefi Azure RTOS ThreadX, Azure RTOS NetX-Duo, Azure RTOS NetX güvenli TLS ve Azure RTOS NetX MQTT 'yi kapsamaktadır.</span><span class="sxs-lookup"><span data-stu-id="75e91-313">The Target of Evalution (TOE) covers Azure RTOS ThreadX, Azure RTOS NetX-Duo, Azure RTOS NetX Secure TLS, and Azure RTOS NetX MQTT.</span></span> <span data-ttu-id="75e91-314">Bu, derin eklenmiş sensörler, cihazlar, uç yönlendiriciler ve ağ geçitleri için gereken en yaygın IoT protokollerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="75e91-314">This represents the most typical IoT protocols required by deeply embedded sensors, devices, edge routers, and gateways.</span></span>

:::image type="content" border="false" source="media/overview-threadx/eal-logo-certification.png" alt-text="EAL sertifikası":::

<span data-ttu-id="75e91-316">Azure RTOS güvenlik sertifikası için kullanılan BT güvenlik değerlendirmesi özelliği, en parlama BV ve sertifika yetkilisi de en iyi şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="75e91-316">The IT Security Evaluation Facility used for the Azure RTOS security certification is Brightsight BV and the Certification Authority is SERTIT.</span></span>

## <a name="simple-easy-to-use"></a><span data-ttu-id="75e91-317">Basit, kullanımı kolay</span><span class="sxs-lookup"><span data-stu-id="75e91-317">Simple, easy to use</span></span>

<span data-ttu-id="75e91-318">Azure RTOS ThreadX kullanımı çok basittir.</span><span class="sxs-lookup"><span data-stu-id="75e91-318">Azure RTOS ThreadX is very simple to use.</span></span> <span data-ttu-id="75e91-319">Azure RTOS ThreadX API 'SI sezgisel ve yüksek işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="75e91-319">The Azure RTOS ThreadX API is both intuitive and highly functional.</span></span> <span data-ttu-id="75e91-320">API adları, diğer RTOS ürünlerinde ortak olan çok sayıda kısaltılmış adlardan oluşan alfabeden değil, gerçek sözcüklerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="75e91-320">The API names are made of real words and not the alphabet soup of highly abbreviated names that are so common in other RTOS products.</span></span> <span data-ttu-id="75e91-321">Tüm Azure RTOS ThreadX API 'Lerinin lideri vardır `tx_` ve bir ad fiil adlandırma kuralını izler.</span><span class="sxs-lookup"><span data-stu-id="75e91-321">All Azure RTOS ThreadX APIs have a leading `tx_` and follow a noun-verb naming convention.</span></span> <span data-ttu-id="75e91-322">Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="75e91-322">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="75e91-323">Örneğin, askıya aldığı tüm API 'lerde API 'Ler için aynı şekilde işlev gören isteğe bağlı bir zaman aşımı vardır.</span><span class="sxs-lookup"><span data-stu-id="75e91-323">For example, all APIs that suspend have an optional timeout that functions in an identical manner for APIs.</span></span>

<span data-ttu-id="75e91-324">Azure RTOS ThreadX uygulaması oluşturmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="75e91-324">Building an Azure RTOS ThreadX application is easy.</span></span> <span data-ttu-id="75e91-325">Uygulamanın *tx_api. h*, `tx_kernel_enter` Main 'ten çağrı, `tx_application_define` işlevi tanımlama ve bir iş parçacığı oluşturma, iş parçacığı giriş noktası işlevini tanımlama ve Azure RTOS threadx kitaplığı (genellikle *TX. a*) ile bağlantı içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="75e91-325">The application needs to include *tx_api.h*, call `tx_kernel_enter` from main, define the `tx_application_define` function and create one thread, define the thread entry point function, and link against the Azure RTOS ThreadX library (typically *tx.a*).</span></span>

<span data-ttu-id="75e91-326">Azure RTOS ThreadX, sunulan en yüksek Caliber belgelerini de botrın.</span><span class="sxs-lookup"><span data-stu-id="75e91-326">Azure RTOS ThreadX also boasts the highest caliber of documentation available.</span></span> 

## <a name="advanced-technology"></a><span data-ttu-id="75e91-327">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="75e91-327">Advanced technology</span></span>

<span data-ttu-id="75e91-328">Azure RTOS ThreadX, en önemli özelliği önalım-Threshold zamanlaması olan gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="75e91-328">Azure RTOS ThreadX is advanced technology whose most notable feature is preemption-threshold scheduling.</span></span> <span data-ttu-id="75e91-329">Bu özellik Azure RTOS ThreadX için benzersizdir ve kapsamlı akademik araştırma konusu.</span><span class="sxs-lookup"><span data-stu-id="75e91-329">This feature is unique to Azure RTOS ThreadX and has been the subject of extensive academic research.</span></span> <span data-ttu-id="75e91-330">Örneğin, bkz. [önalım Threshold ile Fixed-Priority görevleri zamanlama](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), Yıun Wang, Concorçya University ve Manas Saksena, tas haburi Üniversitesi.</span><span class="sxs-lookup"><span data-stu-id="75e91-330">For example, see [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), by Yun Wang, Concordia University, and Manas Saksena, University of Pittsburgh.</span></span>

<span data-ttu-id="75e91-331">Azure RTOS ThreadX 'in yeteneklerini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="75e91-331">Consider the capabilities of Azure RTOS ThreadX:</span></span>

* <span data-ttu-id="75e91-332">Eksiksiz ve kapsamlı çoklu görev olanakları</span><span class="sxs-lookup"><span data-stu-id="75e91-332">Complete and Comprehensive Multitasking Facilities</span></span>
  * <span data-ttu-id="75e91-333">İş parçacıkları, uygulama zamanlayıcılar, ileti kuyrukları, sayma semaforları, zaman uyumu sağlayıcılar, olay bayrakları, blok ve bayt bellek havuzları</span><span class="sxs-lookup"><span data-stu-id="75e91-333">Threads, application timers, message queues, counting semaphores, mutexes, event flags, block and byte memory pools</span></span>
* <span data-ttu-id="75e91-334">Priority-Based preemptive zamanlaması</span><span class="sxs-lookup"><span data-stu-id="75e91-334">Priority-Based Preemptive Scheduling</span></span>
* <span data-ttu-id="75e91-335">Öncelik esnekliği – 1024 öncelik düzeyine kadar</span><span class="sxs-lookup"><span data-stu-id="75e91-335">Priority Flexibility – Up to 1024 Priority Levels</span></span>
* <span data-ttu-id="75e91-336">Cooperative zamanlaması</span><span class="sxs-lookup"><span data-stu-id="75e91-336">Cooperative Scheduling</span></span>
* <span data-ttu-id="75e91-337">Önalım-Threshold™ – Azure RTOS ThreadX için benzersizdir, bağlam anahtarlarının azaltılmasına yardımcı olur ve schedulability (akademik araştırma başına) garantisi sağlar</span><span class="sxs-lookup"><span data-stu-id="75e91-337">Preemption-Threshold™ – Unique to Azure RTOS ThreadX, helps reduce context switches and help guarantee schedulability (per academic research)</span></span>
* <span data-ttu-id="75e91-338">Azure RTOS ThreadX MODÜLLERI aracılığıyla bellek koruması</span><span class="sxs-lookup"><span data-stu-id="75e91-338">Memory Protection via Azure RTOS ThreadX MODULES</span></span>
* <span data-ttu-id="75e91-339">Tam belirleyici</span><span class="sxs-lookup"><span data-stu-id="75e91-339">Fully Deterministic</span></span>
* <span data-ttu-id="75e91-340">Olay Izleme – son *n* sistem/uygulama olaylarını yakala</span><span class="sxs-lookup"><span data-stu-id="75e91-340">Event Trace – Capture last *n* system/application events</span></span>
* <span data-ttu-id="75e91-341">Olay zincirleme™ – her bir Azure RTOS ThreadX iletişimi veya eşitleme nesnesi için uygulamaya özgü "bildirim" geri çağırma işlevini kaydetme</span><span class="sxs-lookup"><span data-stu-id="75e91-341">Event Chaining™ – Register an application-specific “notify” callback function for each Azure RTOS ThreadX communication or synchronization object</span></span>
* <span data-ttu-id="75e91-342">Isteğe bağlı bellek koruması ile Azure RTOS ThreadX MODÜLLERI</span><span class="sxs-lookup"><span data-stu-id="75e91-342">Azure RTOS ThreadX MODULES with Optional Memory Protection</span></span>
* <span data-ttu-id="75e91-343">Run-Time performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="75e91-343">Run-Time Performance Metrics</span></span>
  * <span data-ttu-id="75e91-344">İş parçacığı bağlantının sürdürülmesi sayısı</span><span class="sxs-lookup"><span data-stu-id="75e91-344">Number of thread resumptions</span></span>
  * <span data-ttu-id="75e91-345">İş parçacığı getirilmesi sayısı</span><span class="sxs-lookup"><span data-stu-id="75e91-345">Number of thread suspensions</span></span>
  * <span data-ttu-id="75e91-346">İstek iş parçacığı preemptions sayısı</span><span class="sxs-lookup"><span data-stu-id="75e91-346">Number of solicited thread preemptions</span></span>
  * <span data-ttu-id="75e91-347">Zaman uyumsuz iş parçacığı kesme preemptions sayısı</span><span class="sxs-lookup"><span data-stu-id="75e91-347">Number of asynchronous thread interrupt preemptions</span></span>
  * <span data-ttu-id="75e91-348">İş parçacığı önceliği ınsürümlerin sayısı</span><span class="sxs-lookup"><span data-stu-id="75e91-348">Number of thread priority inversions</span></span>
  * <span data-ttu-id="75e91-349">İş parçacığı relinkler sayısı</span><span class="sxs-lookup"><span data-stu-id="75e91-349">Number of thread relinquishes</span></span>
* <span data-ttu-id="75e91-350">Yürütme profili seti (EPK)</span><span class="sxs-lookup"><span data-stu-id="75e91-350">Execution Profile Kit (EPK)</span></span>
* <span data-ttu-id="75e91-351">Kesme yığınını ayır</span><span class="sxs-lookup"><span data-stu-id="75e91-351">Separate Interrupt Stack</span></span>
* <span data-ttu-id="75e91-352">Run-Time Stack Analizi</span><span class="sxs-lookup"><span data-stu-id="75e91-352">Run-Time Stack Analysis</span></span>
* <span data-ttu-id="75e91-353">İyileştirilmiş Zamanlayıcı kesme Işlemi</span><span class="sxs-lookup"><span data-stu-id="75e91-353">Optimized Timer Interrupt Processing</span></span>

## <a name="multicore-support-amp--smp"></a><span data-ttu-id="75e91-354">Birden çok Ore desteği (AMP & SMP)</span><span class="sxs-lookup"><span data-stu-id="75e91-354">Multicore support (AMP & SMP)</span></span>

<span data-ttu-id="75e91-355">Standart Azure RTOS ThreadX genellikle asimetrik çoklu Işlem (AMP) ile birlikte kullanılır, burada Azure RTOS ThreadX ve uygulamanın (veya Linux) her çekirdek üzerinde yürütülür ve paylaşılan bellek aracılığıyla birbirleriyle iletişim kurar veya OpenAMP (Azure RTOS ThreadX, OpenAMP gibi işlemciler arası bir iletişim mekanizması) vardır.</span><span class="sxs-lookup"><span data-stu-id="75e91-355">Standard Azure RTOS ThreadX is often used in an Asymmetric Multiprocessing (AMP) fashion, where a separate copy of Azure RTOS ThreadX and the application (or Linux) execute on each core and communicate with each other via shared memory or an inter-processor communication mechanism such as OpenAMP (Azure RTOS ThreadX supports OpenAMP).</span></span> <span data-ttu-id="75e91-356">Bu, Azure RTOS ThreadX kullanan en yaygın çok sayıda yapılandırmadır ve uygulama, işlemcileri etkin bir şekilde yükleyebiliyor olması halinde en etkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="75e91-356">This is the most typical multicore configuration using Azure RTOS ThreadX and can be the most efficient if the application is able to effectively load the processors.</span></span>

<span data-ttu-id="75e91-357">İşlemcilerin yüklenmesi çok dinamik olduğundan, aşağıdaki işlemci aileleri için Azure RTOS ThreadX Symetric çok Işlem (SMP) kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="75e91-357">For environments where loading the processors is highly dynamic, Azure RTOS ThreadX Symetric Multiprocessing (SMP) is available for the following processor families:</span></span>

* <span data-ttu-id="75e91-358">ARM Cortex-Ax</span><span class="sxs-lookup"><span data-stu-id="75e91-358">ARM Cortex-Ax</span></span>
* <span data-ttu-id="75e91-359">ARM Cortex-Rx</span><span class="sxs-lookup"><span data-stu-id="75e91-359">ARM Cortex-Rx</span></span>
* <span data-ttu-id="75e91-360">ARM Cortex-A5x 64 bit</span><span class="sxs-lookup"><span data-stu-id="75e91-360">ARM Cortex-A5x 64-bit</span></span>
* <span data-ttu-id="75e91-361">MIPS 34K, 1004K ve ınteraptiv</span><span class="sxs-lookup"><span data-stu-id="75e91-361">MIPS 34K, 1004K, and interAptiv</span></span>
* <span data-ttu-id="75e91-362">PowerPC</span><span class="sxs-lookup"><span data-stu-id="75e91-362">PowerPC</span></span>
* <span data-ttu-id="75e91-363">Synopsys ARC HS</span><span class="sxs-lookup"><span data-stu-id="75e91-363">Synopsys ARC HS</span></span>
* <span data-ttu-id="75e91-364">x86</span><span class="sxs-lookup"><span data-stu-id="75e91-364">x86</span></span>

<span data-ttu-id="75e91-365">Azure RTOS ThreadX SMP, *n* işlemciler genelinde dinamik yük dengeleme gerçekleştirir ve tüm Azure RTOS threadx kaynaklarına (kuyruklar, Semaforlar, olay bayrakları, bellek havuzları vb.) tüm çekirdeklerde herhangi bir iş parçacığı tarafından erişilmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="75e91-365">Azure RTOS ThreadX SMP performs dynamic load balancing across *n* processors and allows all Azure RTOS ThreadX resources (queues, semaphores, event flags, memory pools, etc.) to be accessed by any thread on any core.</span></span> <span data-ttu-id="75e91-366">Azure RTOS ThreadX SMP tüm çekirdekler için tam Azure RTOS ThreadX API 'sini sağlar ve SMP işlemi için geçerli olan aşağıdaki yeni API 'yi tanıtır:</span><span class="sxs-lookup"><span data-stu-id="75e91-366">Azure RTOS ThreadX SMP enables the complete Azure RTOS ThreadX API on all cores and introduces the following new API’s applicable to SMP operation:</span></span>

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a><span data-ttu-id="75e91-367">Azure RTOS ThreadX modülleri aracılığıyla bellek koruması</span><span class="sxs-lookup"><span data-stu-id="75e91-367">Memory protection via Azure RTOS ThreadX Modules</span></span>

<span data-ttu-id="75e91-368">Azure RTOS ThreadX MODÜLLERI adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının, hedefte dinamik olarak yüklenebilen ve çalıştırılabilen (veya yerinde yürütülen) bir "Module" içine paketlenmiş olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="75e91-368">An add-on product called Azure RTOS ThreadX MODULES enables one or more application threads to be bundled into a “Module” that can be dynamically loaded and run (or executed in place) on the target.</span></span>

<span data-ttu-id="75e91-369">Modüller, büyük uygulamaların yalnızca etkin iş parçacıkları tarafından gereken belleği kaplamasına izin vermek için alan yükseltmeyi, hata düzeltmeyi ve program bölümlemesini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="75e91-369">Modules enable field upgrade, bug fixing, and program partitioning to allow large applications to occupy only the memory needed by active threads.</span></span>

<span data-ttu-id="75e91-370">Modüller Ayrıca Azure RTOS ThreadX öğesinden tamamen ayrı bir adres alanına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="75e91-370">Modules also have a completely separate address space from Azure RTOS ThreadX itself.</span></span> <span data-ttu-id="75e91-371">Bu, Azure RTOS ThreadX 'in, modülün dışında yanlışlıkla erişiminin diğer yazılım bileşenlerini bozmayacak şekilde bellek korumasını (MPU veya MMU aracılığıyla) yerleştirmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="75e91-371">This enables Azure RTOS ThreadX to place memory protection (via MPU or MMU) around the Module such that accidental access outside the module will not be able to corrupt any other software component.</span></span>

## <a name="fastest-time-to-market"></a><span data-ttu-id="75e91-372">En hızlı pazar süresi</span><span class="sxs-lookup"><span data-stu-id="75e91-372">Fastest time-to-market</span></span>

<span data-ttu-id="75e91-373">Azure RTOS ThreadX 'i yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="75e91-373">Azure RTOS ThreadX is easy to install, learn, use, debug, verify, certify and maintain.</span></span> <span data-ttu-id="75e91-374">Sonuç olarak, Azure RTOS ThreadX, gömülü Pazar öngörülebilir (EMF) anketlere göre son yedi yılda en önde gelen pazar saati RTOS ' dır.</span><span class="sxs-lookup"><span data-stu-id="75e91-374">As a result, Azure RTOS ThreadX has been the leading time-to-market RTOS for the last seven consecutive years, per the Embedded Market Forecasters (EMF) surveys.</span></span> <span data-ttu-id="75e91-375">Anketler sürekli olarak Azure RTOS ThreadX 'i kullanan tasarımların %70 ' ını, diğer tüm Rtolar aracılığıyla elde edeceğiniz şekilde gösterir.</span><span class="sxs-lookup"><span data-stu-id="75e91-375">The surveys consistently show that 70% of designs using Azure RTOS ThreadX get to market on time – surpassing all other RTOSes.</span></span>

<span data-ttu-id="75e91-376">Aşağıda, tutarlı bir pazarlama süresi avantajımız için nedenler verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="75e91-376">The following are reasons for our consistent time-to-market advantage:</span></span>

* <span data-ttu-id="75e91-377">Kalite belgeleri</span><span class="sxs-lookup"><span data-stu-id="75e91-377">Quality Documentation</span></span>
* <span data-ttu-id="75e91-378">Tüm kaynak kodu kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="75e91-378">Complete Source Code Availability</span></span>
* <span data-ttu-id="75e91-379">Kullanımı kolay API</span><span class="sxs-lookup"><span data-stu-id="75e91-379">Easy-to-Use API</span></span>
* <span data-ttu-id="75e91-380">Kapsamlı ve gelişmiş özellik kümesi</span><span class="sxs-lookup"><span data-stu-id="75e91-380">Comprehensive and Advanced Feature Set</span></span>
* <span data-ttu-id="75e91-381">Geniş üçüncü taraf araçları tümleştirmesi – özellikle ıAR 'ın Embedded çalışma ekranı™</span><span class="sxs-lookup"><span data-stu-id="75e91-381">Broad 3rd Party Tools Integration – Especially IAR’s Embedded Workbench™</span></span>

## <a name="royalty-free"></a><span data-ttu-id="75e91-382">Ücretsiz lisanslı</span><span class="sxs-lookup"><span data-stu-id="75e91-382">Royalty free</span></span>

<span data-ttu-id="75e91-383">Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="75e91-383">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="75e91-384">Tam, en yüksek kaliteli kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="75e91-384">Full, highest-quality source code</span></span>

<span data-ttu-id="75e91-385">Azure RTOS ThreadX, çok başından başlayarak tam C kaynak kodla dağıtılan bir endüstriyel sınıf RTOS olacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="75e91-385">From the very beginning, Azure RTOS ThreadX was designed to be an Industrial Grade RTOS, distributed with full C source code.</span></span> <span data-ttu-id="75e91-386">Azure RTOS ThreadX kaynak kodu, çubuğun kalitesini ve kolayca anlaşılmasına ayarlı.</span><span class="sxs-lookup"><span data-stu-id="75e91-386">Azure RTOS ThreadX source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="75e91-387">Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.</span><span class="sxs-lookup"><span data-stu-id="75e91-387">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

<span data-ttu-id="75e91-388">Azure RTOS ThreadX, her C kodu satırının anlamlı bir yorumu olan gereksinimi dahil olmak üzere katı kodlama kurallarına uyar.</span><span class="sxs-lookup"><span data-stu-id="75e91-388">Azure RTOS ThreadX conforms to strict coding conventions, including the requirement that every line of C code has a meaningful comment.</span></span> <span data-ttu-id="75e91-389">Ayrıca, Azure RTOS ThreadX kaynağı en yüksek standartlara sertifikalıdır.</span><span class="sxs-lookup"><span data-stu-id="75e91-389">In addition, the Azure RTOS ThreadX source has been certified to the highest standards.</span></span>

## <a name="misra-compliant"></a><span data-ttu-id="75e91-390">Hatalı ra uyumlu</span><span class="sxs-lookup"><span data-stu-id="75e91-390">MISRA compliant</span></span>

<span data-ttu-id="75e91-391">Azure RTOS ThreadX ve Azure RTOS ThreadX SMP souce Code yanlış ra-C:2004 ve MISRA C:2012 uyumludur.</span><span class="sxs-lookup"><span data-stu-id="75e91-391">Azure RTOS ThreadX and Azure RTOS ThreadX SMP souce code is MISRA-C:2004 and MISRA C:2012 compliant.</span></span> <span data-ttu-id="75e91-392">MISRA C, C programlama dilini kullanan kritik sistemler için bir programlama yönergeleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="75e91-392">MISRA C is a set of programming guidelines for critical systems using the C programming language.</span></span> <span data-ttu-id="75e91-393">Özgün MISRA C yönergeleri öncelikli olarak, ilk olarak bir oto ve uygulamaları hedeflenmiştir; Ancak, MISRA C artık güvenlik açısından kritik uygulamalar için geçerli olduğu şekilde çok daha tanınır.</span><span class="sxs-lookup"><span data-stu-id="75e91-393">The original MISRA C guidelines were primarily targeted toward automotive applications; however, MISRA C is now widely recognized as being applicable to any safety-critical application.</span></span> <span data-ttu-id="75e91-394">Azure RTOS ThreadX, tüm gerekli ve zorunlu, MISRA-C:2004 ve MISRA c:2012'nin tüm kuralları ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="75e91-394">Azure RTOS ThreadX is compliant with all required and mandatory rules of MISRA-C:2004 and MISRA C:2012.</span></span>

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Hatalı ra sertifikası":::

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="75e91-396">Popüler mimarilerin çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="75e91-396">Supports most popular architectures</span></span>

<span data-ttu-id="75e91-397">Azure RTOS ThreadX, en popüler 32/64 bit mikro işlemciler üzerinde çalışır, kullanıma hazır, tamamen sınanmış ve aşağıdakiler dahil olmak üzere tam olarak desteklenmektedir:</span><span class="sxs-lookup"><span data-stu-id="75e91-397">Azure RTOS ThreadX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

* <span data-ttu-id="75e91-398">Analog cihazlar: parça, BlackICE, CM4xx</span><span class="sxs-lookup"><span data-stu-id="75e91-398">Analog Devices: SHARC, Blackfin, CM4xx</span></span>
* <span data-ttu-id="75e91-399">Andes Core: RıSC-V</span><span class="sxs-lookup"><span data-stu-id="75e91-399">Andes Core: RISC-V</span></span>
* <span data-ttu-id="75e91-400">Ambiqmicro: Apollo MCUs</span><span class="sxs-lookup"><span data-stu-id="75e91-400">Ambiqmicro: Apollo MCUs</span></span>
* <span data-ttu-id="75e91-401">ARM: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı</span><span class="sxs-lookup"><span data-stu-id="75e91-401">ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>
* <span data-ttu-id="75e91-402">Temposunda: Xtensa, elmas</span><span class="sxs-lookup"><span data-stu-id="75e91-402">Cadence: Xtensa, Diamond</span></span>
* <span data-ttu-id="75e91-403">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WERWIFI</span><span class="sxs-lookup"><span data-stu-id="75e91-403">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>
* <span data-ttu-id="75e91-404">Cypress: RıSC-V</span><span class="sxs-lookup"><span data-stu-id="75e91-404">Cypress: RISC-V</span></span>
* <span data-ttu-id="75e91-405">EnSilica: eSi-RıSC</span><span class="sxs-lookup"><span data-stu-id="75e91-405">EnSilica: eSi-RISC</span></span>
* <span data-ttu-id="75e91-406">Infineon: XMC1000, XMC4000, Kanore</span><span class="sxs-lookup"><span data-stu-id="75e91-406">Infineon: XMC1000, XMC4000, TriCore</span></span>
* <span data-ttu-id="75e91-407">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, varış a 10</span><span class="sxs-lookup"><span data-stu-id="75e91-407">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>
* <span data-ttu-id="75e91-408">Mikro yonga: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="75e91-408">Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>
* <span data-ttu-id="75e91-409">Mikro yarı: RıSC-V</span><span class="sxs-lookup"><span data-stu-id="75e91-409">Microsemi: RISC-V</span></span>
* <span data-ttu-id="75e91-410">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="75e91-410">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>
* <span data-ttu-id="75e91-411">Renesas: SH, HS, v850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="75e91-411">Renesas: SH, HS, V850, RX, RZ, Synergy</span></span>
* <span data-ttu-id="75e91-412">Silicon Labs: EFM32</span><span class="sxs-lookup"><span data-stu-id="75e91-412">Silicon Labs: EFM32</span></span>
* <span data-ttu-id="75e91-413">Synopsys: ARC 600, 700, ARC EM, ARC HS</span><span class="sxs-lookup"><span data-stu-id="75e91-413">Synopsys: ARC 600, 700, ARC EM, ARC HS</span></span>
* <span data-ttu-id="75e91-414">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="75e91-414">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>
* <span data-ttu-id="75e91-415">TL: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="75e91-415">Tl: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>
* <span data-ttu-id="75e91-416">Dalga Bilgi Işlem: MıPS32 4K, 24K, 34K, 1004K, ver 5K, mikro Aptiv, ınteraptiv, proAptiv, M sınıfı</span><span class="sxs-lookup"><span data-stu-id="75e91-416">Wave Computing: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>
* <span data-ttu-id="75e91-417">Xilinx: mikro Blaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="75e91-417">Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

## <a name="supports-most-popular-tools"></a><span data-ttu-id="75e91-418">Popüler araçların çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="75e91-418">Supports most popular tools</span></span>

<span data-ttu-id="75e91-419">Azure RTOS ThreadX, en kapsamlı Azure RTOS ThreadX çekirdek tanıma 'yı de içeren ıAR 'ın Embedded çalışma ekranı™ dahil olmak üzere en popüler katıştırılmış geliştirme araçlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="75e91-419">Azure RTOS ThreadX supports most popular embedded development tools, including IAR’s Embedded Workbench™, which also has the most comprehensive Azure RTOS ThreadX kernel awareness available.</span></span> <span data-ttu-id="75e91-420">Ek araç tümleştirmesi, GNU (GCC), ARM DS-5/uVision®, yeşil Tepls MULTI®, Rüzgar River çalışma ekranı™, hayal Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Defterbach TRACE32®, TI Code-Composer Studio, çapraz puan ve tüm örneksel cihazları içerir.</span><span class="sxs-lookup"><span data-stu-id="75e91-420">Additional tool integration includes GNU (GCC), ARM DS-5/uVision®, Green Hills MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer Studio, CrossCore and all analog devices.</span></span>
