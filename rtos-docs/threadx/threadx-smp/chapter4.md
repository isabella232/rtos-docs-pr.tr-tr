---
title: Bölüm 4-Azure RTOS ThreadX SMP hizmetlerinin açıklaması
description: Bu bölümde, tüm Azure RTOS ThreadX SMP Hizmetleri alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4432001b773b4ef4f99b1b34193e90863966aad4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828024"
---
# <a name="chapter-4---description-of-azure-rtos-threadx-smp-services"></a><span data-ttu-id="ff79b-103">Bölüm 4-Azure RTOS ThreadX SMP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="ff79b-103">Chapter 4 - Description of Azure RTOS ThreadX SMP Services</span></span>

<span data-ttu-id="ff79b-104">Bu bölümde, tüm Azure RTOS ThreadX SMP Hizmetleri alfabetik sırada bir açıklama bulunur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-104">This chapter contains a description of all Azure RTOS ThreadX SMP services in alphabetic order.</span></span> <span data-ttu-id="ff79b-105">Adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-105">Their names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="ff79b-106">Aşağıdaki açıklamaların "dönüş değerleri" bölümünde, **kalın yazı** DEĞERLERI, API hata denetimini devre dışı bırakmak için kullanılan tanımlama **TX_DISABLE_ERROR_CHECKING** etkilenmez; kalın olmayan içinde gösterilen değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-106">In the “Return Values” section in the following descriptions, values in **BOLD** are not affected by the **TX_DISABLE_ERROR_CHECKING** define used to disable API error checking; while values shown in nonbold are completely disabled.</span></span> <span data-ttu-id="ff79b-107">Buna ek olarak, "**önalım olası**" başlığı altında listelenen bir "**Evet**" seçeneği, hizmeti çağırmanın daha yüksek öncelikli bir iş parçacığını sürdürüleceği ve bu nedenle çağıran iş parçacığını öncelik verme gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-107">In addition, a “**Yes**” listed under the “**Preemption Possible**” heading indicates that calling the service may resume a higher-priority thread, thus preempting the calling thread.</span></span>

- <span data-ttu-id="ff79b-108">**tx_block_allocate**: *sabit boyutlu bellek bloğunu ayır*</span><span class="sxs-lookup"><span data-stu-id="ff79b-108">**tx_block_allocate**: *Allocate fixed-size block of memory*</span></span> 
- <span data-ttu-id="ff79b-109">**tx_block_pool_create**: *sabit boyutlu bellek blokları havuzu oluştur*</span><span class="sxs-lookup"><span data-stu-id="ff79b-109">**tx_block_pool_create**: *Create pool of fixed-size memory blocks*</span></span> 
- <span data-ttu-id="ff79b-110">**tx_block_pool_delete**: *bellek blok havuzunu Sil*</span><span class="sxs-lookup"><span data-stu-id="ff79b-110">**tx_block_pool_delete**: *Delete memory block pool*</span></span> 
- <span data-ttu-id="ff79b-111">**tx_block_pool_info_get**: *blok havuzu hakkında bilgi alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-111">**tx_block_pool_info_get**: *Retrieve information about block pool*</span></span> 
- <span data-ttu-id="ff79b-112">**tx_block_pool_performance_info_get**: *blok havuzu performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-112">**tx_block_pool_performance_info_get**: *Get block pool performance information*</span></span> 
- <span data-ttu-id="ff79b-113">**tx_block_pool_performance_system_info_get**: *blok havuzu sistem performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-113">**tx_block_pool_performance_system_info_get**: *Get block pool system performance information*</span></span> 
- <span data-ttu-id="ff79b-114">**tx_block_pool_prioritize**: *blok havuzunu askıya alma listesinin önceliğini belirleme*</span><span class="sxs-lookup"><span data-stu-id="ff79b-114">**tx_block_pool_prioritize**: *Prioritize block pool suspension list*</span></span> 
- <span data-ttu-id="ff79b-115">**tx_block_release**: *sabit boyutlu bellek bloğunu yayınlama*</span><span class="sxs-lookup"><span data-stu-id="ff79b-115">**tx_block_release**: *Release fixed-size block of memory*</span></span>
- <span data-ttu-id="ff79b-116">**tx_byte_allocate**: *bellek baytları ayırma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-116">**tx_byte_allocate**: *Allocate bytes of memory*</span></span> 
- <span data-ttu-id="ff79b-117">**tx_byte_pool_create**: *bayt bellek havuzu oluştur*</span><span class="sxs-lookup"><span data-stu-id="ff79b-117">**tx_byte_pool_create**: *Create memory pool of bytes*</span></span> 
- <span data-ttu-id="ff79b-118">**tx_byte_pool_delete**: *bellek bayt havuzunu Sil*</span><span class="sxs-lookup"><span data-stu-id="ff79b-118">**tx_byte_pool_delete**: *Delete memory byte pool*</span></span> 
- <span data-ttu-id="ff79b-119">**tx_byte_pool_info_get**: *bayt havuzu hakkında bilgi alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-119">**tx_byte_pool_info_get**: *Retrieve information about byte pool*</span></span> 
- <span data-ttu-id="ff79b-120">**tx_byte_pool_performance_info_get**: *bayt havuzu performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-120">**tx_byte_pool_performance_info_get**: *Get byte pool performance information*</span></span> 
- <span data-ttu-id="ff79b-121">**tx_byte_pool_performance_system_info_get**: *bayt havuzu sistem performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-121">**tx_byte_pool_performance_system_info_get**: *Get byte pool system performance information*</span></span> 
- <span data-ttu-id="ff79b-122">**tx_byte_pool_prioritize**: *bayt havuzu askıya alma listesinin önceliğini belirleme*</span><span class="sxs-lookup"><span data-stu-id="ff79b-122">**tx_byte_pool_prioritize**: *Prioritize byte pool suspension list*</span></span> 
- <span data-ttu-id="ff79b-123">**tx_byte_release**: *baytları bellek havuzuna geri bırakma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-123">**tx_byte_release**: *Release bytes back to memory pool*</span></span> 
- <span data-ttu-id="ff79b-124">**tx_event_flags_create**: *olay bayrakları grubu oluştur*</span><span class="sxs-lookup"><span data-stu-id="ff79b-124">**tx_event_flags_create**: *Create event flags group*</span></span> 
- <span data-ttu-id="ff79b-125">**tx_event_flags_delete**: *olay bayrakları grubunu sil*</span><span class="sxs-lookup"><span data-stu-id="ff79b-125">**tx_event_flags_delete**: *Delete event flags group*</span></span> 
- <span data-ttu-id="ff79b-126">**tx_event_flags_get**: *olay bayrakları grubundan olay bayraklarını al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-126">**tx_event_flags_get**: *Get event flags from event flags group*</span></span> 
- <span data-ttu-id="ff79b-127">**tx_event_flags_info_get**: *olay bayrakları grubu hakkında bilgi alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-127">**tx_event_flags_info_get**: *Retrieve information about event flags group*</span></span> 
- <span data-ttu-id="ff79b-128">**tx_event_flags_performance_info_get**: *olay bayrakları grup performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-128">**tx_event_flags_performance_info_get**: *Get event flags group performance information*</span></span> 
- <span data-ttu-id="ff79b-129">**tx_event_flags_performance_system_info_get**: *performans sistemi bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-129">**tx_event_flags_performance_system_info_get**: *Retrieve performance system information*</span></span> 
- <span data-ttu-id="ff79b-130">**tx_event_flags_set**: olay bayrakları *grubundaki olay bayraklarını ayarlama*</span><span class="sxs-lookup"><span data-stu-id="ff79b-130">**tx_event_flags_set**: *Set event flags in an event flags group*</span></span> 
- <span data-ttu-id="ff79b-131">**tx_event_flags_set_notify**: *olay bayrakları ayarlandığında uygulamayı bilgilendir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-131">**tx_event_flags_set_notify**: *Notify application when event flags are set*</span></span>
- <span data-ttu-id="ff79b-132">**tx_interrupt_control**: *kesmeleri etkinleştirme ve devre dışı bırakma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-132">**tx_interrupt_control**: *Enable and disable interrupts*</span></span> 
- <span data-ttu-id="ff79b-133">**tx_mutex_create**: *karşılıklı dışlama mutex oluşturma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-133">**tx_mutex_create**: *Create mutual exclusion mutex*</span></span> 
- <span data-ttu-id="ff79b-134">**tx_mutex_delete**: *karşılıklı dışlama mutex 'i Sil*</span><span class="sxs-lookup"><span data-stu-id="ff79b-134">**tx_mutex_delete**: *Delete mutual exclusion mutex*</span></span> 
- <span data-ttu-id="ff79b-135">**tx_mutex_get**: *mutex sahipliğini alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-135">**tx_mutex_get**: *Obtain ownership of mutex*</span></span> 
- <span data-ttu-id="ff79b-136">**tx_mutex_info_get**: *mutex hakkında bilgi alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-136">**tx_mutex_info_get**: *Retrieve information about mutex*</span></span> 
- <span data-ttu-id="ff79b-137">**tx_mutex_performance_info_get**: *mutex performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-137">**tx_mutex_performance_info_get**: *Get mutex performance information*</span></span> 
- <span data-ttu-id="ff79b-138">**tx_mutex_performance_system_info_get**: *mutex sistem performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-138">**tx_mutex_performance_system_info_get**: *Get mutex system performance information*</span></span> 
- <span data-ttu-id="ff79b-139">**tx_mutex_prioritize**: *mutex askıya alma listesini önceliklendir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-139">**tx_mutex_prioritize**: *Prioritize mutex suspension list*</span></span> 
- <span data-ttu-id="ff79b-140">**tx_mutex_put**: *mutex 'in sahipliğini yayınlama*</span><span class="sxs-lookup"><span data-stu-id="ff79b-140">**tx_mutex_put**: *Release ownership of mutex*</span></span> 
- <span data-ttu-id="ff79b-141">**tx_queue_create**: *ileti kuyruğu oluşturma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-141">**tx_queue_create**: *Create message queue*</span></span> 
- <span data-ttu-id="ff79b-142">**tx_queue_delete**: *ileti kuyruğunu sil*</span><span class="sxs-lookup"><span data-stu-id="ff79b-142">**tx_queue_delete**: *Delete message queue*</span></span> 
- <span data-ttu-id="ff79b-143">**tx_queue_flush**: *ileti kuyruğunda boş iletiler*</span><span class="sxs-lookup"><span data-stu-id="ff79b-143">**tx_queue_flush**: *Empty messages in message queue*</span></span> 
- <span data-ttu-id="ff79b-144">**tx_queue_front_send**: *sıranın önüne ileti gönderin*</span><span class="sxs-lookup"><span data-stu-id="ff79b-144">**tx_queue_front_send**: *Send message to the front of queue*</span></span> 
- <span data-ttu-id="ff79b-145">**tx_queue_info_get**: *kuyrukla ilgili bilgileri alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-145">**tx_queue_info_get**: *Retrieve information about queue*</span></span> 
- <span data-ttu-id="ff79b-146">**tx_queue_performance_info_get**: *sıra performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-146">**tx_queue_performance_info_get**: *Get queue performance information*</span></span> 
- <span data-ttu-id="ff79b-147">**tx_queue_performance_system_info_get**: *sıra sistem performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-147">**tx_queue_performance_system_info_get**: *Get queue system performance information*</span></span>
- <span data-ttu-id="ff79b-148">**tx_queue_prioritize**: *sıra askıya alma listesini önceliklendir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-148">**tx_queue_prioritize**: *Prioritize queue suspension list*</span></span> 
- <span data-ttu-id="ff79b-149">**tx_queue_receive**: *ileti kuyruğundan ileti al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-149">**tx_queue_receive**: *Get message from message queue*</span></span> 
- <span data-ttu-id="ff79b-150">**tx_queue_send**: ileti *kuyruğuna ileti gönder*</span><span class="sxs-lookup"><span data-stu-id="ff79b-150">**tx_queue_send**: *Send message to message queue*</span></span> 
- <span data-ttu-id="ff79b-151">**tx_queue_send_notify**: *ileti kuyruğa gönderildiğinde uygulamayı bilgilendir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-151">**tx_queue_send_notify**: *Notify application when message is sent to queue*</span></span> 
- <span data-ttu-id="ff79b-152">**tx_semaphore_ceiling_put**: *tavan ile sayım semafora bir örnek yerleştirme*</span><span class="sxs-lookup"><span data-stu-id="ff79b-152">**tx_semaphore_ceiling_put**: *Place an instance in counting semaphore with ceiling*</span></span> 
- <span data-ttu-id="ff79b-153">**tx_semaphore_create**: *sayım semaforu oluştur*</span><span class="sxs-lookup"><span data-stu-id="ff79b-153">**tx_semaphore_create**: *Create counting semaphore*</span></span> 
- <span data-ttu-id="ff79b-154">**tx_semaphore_delete**: *sayım semaforu Sil*</span><span class="sxs-lookup"><span data-stu-id="ff79b-154">**tx_semaphore_delete**: *Delete counting semaphore*</span></span> 
- <span data-ttu-id="ff79b-155">**tx_semaphore_get**: *sayım semafordan örnek al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-155">**tx_semaphore_get**: *Get instance from counting semaphore*</span></span> 
- <span data-ttu-id="ff79b-156">**tx_semaphore_info_get**: *semafor hakkında bilgi alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-156">**tx_semaphore_info_get**: *Retrieve information about semaphore*</span></span> 
- <span data-ttu-id="ff79b-157">**tx_semaphore_performance_info_get**: *semafor performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-157">**tx_semaphore_performance_info_get**: *Get semaphore performance information*</span></span> 
- <span data-ttu-id="ff79b-158">**tx_semaphore_performance_system_info_get**: *semafor sistem performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-158">**tx_semaphore_performance_system_info_get**: *Get semaphore system performance information*</span></span> 
- <span data-ttu-id="ff79b-159">**tx_semaphore_prioritize**: *semafor askıya alma listesini önceliklendir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-159">**tx_semaphore_prioritize**: *Prioritize semaphore suspension list*</span></span> 
- <span data-ttu-id="ff79b-160">**tx_semaphore_put**: *bir örneği sayım semafora yerleştirin*</span><span class="sxs-lookup"><span data-stu-id="ff79b-160">**tx_semaphore_put**: *Place an instance in counting semaphore*</span></span> 
- <span data-ttu-id="ff79b-161">**tx_semaphore_put_notify**: *semafor eklendiğinde uygulamayı bilgilendir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-161">**tx_semaphore_put_notify**: *Notify application when semaphore is put*</span></span> 
- <span data-ttu-id="ff79b-162">**tx_thread_create**: *uygulama iş parçacığı oluştur*</span><span class="sxs-lookup"><span data-stu-id="ff79b-162">**tx_thread_create**: *Create application thread*</span></span> 
- <span data-ttu-id="ff79b-163">**tx_thread_delete**: *uygulama iş parçacığını silme*</span><span class="sxs-lookup"><span data-stu-id="ff79b-163">**tx_thread_delete**: *Delete application thread*</span></span>
- <span data-ttu-id="ff79b-164">**tx_thread_entry_exit_notify**: *uygulamayı iş parçacığı girdisi ve çıkış sonrasında bilgilendir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-164">**tx_thread_entry_exit_notify**: *Notify application upon thread entry and exit*</span></span> 
- <span data-ttu-id="ff79b-165">**tx_thread_identify**: *Şu anda yürütülmekte olan iş parçacığına yönelik işaretçiyi alır*</span><span class="sxs-lookup"><span data-stu-id="ff79b-165">**tx_thread_identify**: *Retrieves pointer to currently executing thread*</span></span> 
- <span data-ttu-id="ff79b-166">**tx_thread_info_get**: *iş parçacığı hakkındaki bilgileri alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-166">**tx_thread_info_get**: *Retrieve information about thread*</span></span> 
- <span data-ttu-id="ff79b-167">**tx_thread_performance_info_get**: *iş parçacığı performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-167">**tx_thread_performance_info_get**: *Get thread performance information*</span></span> 
- <span data-ttu-id="ff79b-168">**tx_thread_performance_system_info_get**: *iş parçacığı sistemi performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-168">**tx_thread_performance_system_info_get**: *Get thread system performance information*</span></span> 
- <span data-ttu-id="ff79b-169">**tx_thread_preemption_change**: *önalım-uygulama iş parçacığının eşiğini Değiştir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-169">**tx_thread_preemption_change**: *Change preemption-threshold of application thread*</span></span> 
- <span data-ttu-id="ff79b-170">**tx_thread_priority_change**: *uygulama iş parçacığının önceliğini değiştirme*</span><span class="sxs-lookup"><span data-stu-id="ff79b-170">**tx_thread_priority_change**: *Change priority of application thread*</span></span> 
- <span data-ttu-id="ff79b-171">**tx_thread_relinquish**: *diğer uygulama iş parçacıklarıyla denetimi yeniden* oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff79b-171">**tx_thread_relinquish**: *Relinquish control to other application threads*</span></span> 
- <span data-ttu-id="ff79b-172">**tx_thread_reset**: *iş parçacığını Sıfırla*</span><span class="sxs-lookup"><span data-stu-id="ff79b-172">**tx_thread_reset**: *Reset thread*</span></span> 
- <span data-ttu-id="ff79b-173">**tx_thread_resume**: *askıya alınmış uygulama iş parçacığını sürdürür*</span><span class="sxs-lookup"><span data-stu-id="ff79b-173">**tx_thread_resume**: *Resume suspended application thread*</span></span> 
- <span data-ttu-id="ff79b-174">**tx_thread_sleep**: *belirtilen süre için geçerli iş parçacığını askıya al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-174">**tx_thread_sleep**: *Suspend current thread for specified time*</span></span> 
- <span data-ttu-id="ff79b-175">**tx_thread_smp_core_exclude**: *bir çekirdek kümesinde iş parçacığı yürütmeyi hariç tutma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-175">**tx_thread_smp_core_exclude**: *Exclude thread execution on a set of cores*</span></span> 
- <span data-ttu-id="ff79b-176">**tx_thread_smp_core_exclude_get**: *iş parçacığının geçerli çekirdek dışlamasını alır*</span><span class="sxs-lookup"><span data-stu-id="ff79b-176">**tx_thread_smp_core_exclude_get**: *Gets the thread's current core exclusion*</span></span> 
- <span data-ttu-id="ff79b-177">**tx_thread_smp_core_get**: *Şu anda yürütülen çağıran çekirdeğini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-177">**tx_thread_smp_core_get**: *Retrieve currently executing core of caller*</span></span> 
- <span data-ttu-id="ff79b-178">**tx_thread_stack_error_notify**: *iş parçacığı yığınını kaydet hata bildirimi geri araması*</span><span class="sxs-lookup"><span data-stu-id="ff79b-178">**tx_thread_stack_error_notify**: *Register thread stack error notification callback*</span></span> 
- <span data-ttu-id="ff79b-179">**tx_thread_suspend**: *uygulama iş parçacığını askıya al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-179">**tx_thread_suspend**: *Suspend application thread*</span></span>
- <span data-ttu-id="ff79b-180">**tx_thread_terminate**: *uygulama iş parçacığını sonlandırır*</span><span class="sxs-lookup"><span data-stu-id="ff79b-180">**tx_thread_terminate**: *Terminates application thread*</span></span> 
- <span data-ttu-id="ff79b-181">**tx_thread_time_slice_change**: *değişiklik zamanı-uygulama iş parçacığının dilimi*</span><span class="sxs-lookup"><span data-stu-id="ff79b-181">**tx_thread_time_slice_change**: *Changes time-slice of application thread*</span></span> 
- <span data-ttu-id="ff79b-182">**tx_thread_wait_abort**: *belirtilen iş parçacığının askıya alınma işlemini durdur*</span><span class="sxs-lookup"><span data-stu-id="ff79b-182">**tx_thread_wait_abort**: *Abort suspension of specified thread*</span></span> 
- <span data-ttu-id="ff79b-183">**tx_time_get**: *geçerli saati alır*</span><span class="sxs-lookup"><span data-stu-id="ff79b-183">**tx_time_get**: *Retrieves the current time*</span></span> 
- <span data-ttu-id="ff79b-184">**tx_time_set**: *geçerli saati ayarlar*</span><span class="sxs-lookup"><span data-stu-id="ff79b-184">**tx_time_set**: *Sets the current time*</span></span> 
- <span data-ttu-id="ff79b-185">**tx_timer_activate**: *uygulama zamanlayıcısını etkinleştir*</span><span class="sxs-lookup"><span data-stu-id="ff79b-185">**tx_timer_activate**: *Activate application timer*</span></span> 
- <span data-ttu-id="ff79b-186">**tx_timer_change**: *uygulama zamanlayıcısını değiştirme*</span><span class="sxs-lookup"><span data-stu-id="ff79b-186">**tx_timer_change**: *Change application timer*</span></span> 
- <span data-ttu-id="ff79b-187">**tx_timer_create**: *uygulama Zamanlayıcısı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-187">**tx_timer_create**: *Create application timer*</span></span> 
- <span data-ttu-id="ff79b-188">**tx_timer_deactivate**: *uygulama zamanlayıcısını devre dışı bırak*</span><span class="sxs-lookup"><span data-stu-id="ff79b-188">**tx_timer_deactivate**: *Deactivate application timer*</span></span> 
- <span data-ttu-id="ff79b-189">**tx_timer_delete**: *uygulama zamanlayıcısını Sil*</span><span class="sxs-lookup"><span data-stu-id="ff79b-189">**tx_timer_delete**: *Delete application timer*</span></span> 
- <span data-ttu-id="ff79b-190">**tx_timer_info_get**: *uygulama süreölçeri hakkında bilgi alma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-190">**tx_timer_info_get**: *Retrieve information about an application timer*</span></span> 
- <span data-ttu-id="ff79b-191">**tx_timer_performance_info_get**: *Zamanlayıcı performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-191">**tx_timer_performance_info_get**: *Get timer performance information*</span></span> 
- <span data-ttu-id="ff79b-192">**tx_timer_performance_system_info_get**: *Zamanlayıcı sistem performans bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="ff79b-192">**tx_timer_performance_system_info_get**: *Get timer system performance information*</span></span> 
- <span data-ttu-id="ff79b-193">**tx_timer_smp_core_exclude**: *bir çekirdek kümesinde süreölçer yürütmeyi hariç tutma*</span><span class="sxs-lookup"><span data-stu-id="ff79b-193">**tx_timer_smp_core_exclude**: *Exclude timer execution on a set of cores*</span></span> 
- <span data-ttu-id="ff79b-194">**tx_timer_smp_core_exclude_get**: *zamanlayıcının geçerli çekirdek dışlamasını alır*</span><span class="sxs-lookup"><span data-stu-id="ff79b-194">**tx_timer_smp_core_exclude_get**: *Gets the timer's current core exclusion*</span></span>

## <a name="tx_block_allocate"></a><span data-ttu-id="ff79b-195">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-195">tx_block_allocate</span></span>
<span data-ttu-id="ff79b-196">Sabit boyutlu bellek bloğunu ayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-196">Allocate fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-197">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-197">Prototype</span></span>

```C
UINT tx_block_allocate(TX_BLOCK_POOL *pool_ptr, VOID **block_ptr,
                          ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-198">Description</span></span>

<span data-ttu-id="ff79b-199">Bu hizmet, belirtilen bellek havuzundan sabit boyutlu bir bellek bloğu ayırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-199">This service allocates a fixed-size memory block from the specified memory pool.</span></span> <span data-ttu-id="ff79b-200">Bellek bloğunun gerçek boyutu bellek havuzu oluşturma sırasında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-200">The actual size of the memory block is determined during memory pool creation.</span></span>

> [!WARNING]
> <span data-ttu-id="ff79b-201">Uygulama kodunun ayrılan bellek bloğunun dışına yazmadığından emin olmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-201">It is important to ensure application code does not write outside the allocated memory block.</span></span> <span data-ttu-id="ff79b-202">Bu durumda, bir komşu (genellikle sonraki) bellek bloğunda bozulma oluşur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-202">If this happens, corruption occurs in an adjacent (usually subsequent) memory block.</span></span> <span data-ttu-id="ff79b-203">Sonuçlar tahmin edilemez ve genellikle önemli olur!</span><span class="sxs-lookup"><span data-stu-id="ff79b-203">The results are unpredictable and are often fatal!</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-204">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-204">Parameters</span></span>

- <span data-ttu-id="ff79b-205">**pool_ptr**: daha önce oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-205">**pool_ptr**: Pointer to a previously created memory block pool.</span></span>
- <span data-ttu-id="ff79b-206">**block_ptr**: hedef blok işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-206">**block_ptr**: Pointer to a destination block pointer.</span></span> <span data-ttu-id="ff79b-207">Başarılı bir ayırma sırasında, ayrılan bellek bloğunun adresi bu parametrenin gösterdiği yere yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-207">On successful allocation, the address of the allocated memory block is placed where this parameter points.</span></span>
- <span data-ttu-id="ff79b-208">**wait_option**: kullanılabilir bellek bloğu yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-208">**wait_option**: Defines how the service behaves if there are no memory blocks available.</span></span> <span data-ttu-id="ff79b-209">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-209">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-210">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-210">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="ff79b-211">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-211">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="ff79b-212">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-212">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>  
    
    <span data-ttu-id="ff79b-213">TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönede neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-213">Selecting TX_NO_WAIT results in an immediate return from this service regardless if it was successful or not.</span></span> <span data-ttu-id="ff79b-214">Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.</span><span class="sxs-lookup"><span data-stu-id="ff79b-214">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>

    <span data-ttu-id="ff79b-215">TX_WAIT_FOREVER seçilmesi, bir bellek bloğu kullanılabilir olana kadar çağıran iş parçacığının süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-215">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a memory block is available.</span></span>

    <span data-ttu-id="ff79b-216">Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, bellek bloğu beklenirken askıya alınması için en fazla Zamanlayıcı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-216">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-217">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-217">Return Values</span></span>

- <span data-ttu-id="ff79b-218">**TX_SUCCESS**: (0x00) başarılı bellek bloğu ayırması.</span><span class="sxs-lookup"><span data-stu-id="ff79b-218">**TX_SUCCESS**: (0x00) Successful memory block allocation.</span></span>
- <span data-ttu-id="ff79b-219">**TX_DELETED**: (0x01) bellek bloğu havuzu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-219">**TX_DELETED**: (0x01) Memory block pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-220">**TX_NO_MEMORY**: (0x10) hizmeti, belirtilen süre içinde beklenecek bir bellek bloğunu ayıramadı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-220">**TX_NO_MEMORY**: (0x10) Service was unable to allocate a block of memory within the specified time to wait.</span></span>
- <span data-ttu-id="ff79b-221">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-221">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer or ISR.</span></span>
- <span data-ttu-id="ff79b-222">TX_POOL_ERROR: (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-222">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="ff79b-223">TX_PTR_ERROR: (0x03) hedef işaretçisine geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-223">TX_PTR_ERROR: (0x03) Invalid pointer to destination pointer.</span></span>
- <span data-ttu-id="ff79b-224">TX_WAIT_ERROR: (0x04) iş parçacığından oluşan çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-224">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-225">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-225">Allowed From</span></span>

<span data-ttu-id="ff79b-226">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-226">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-227">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-227">Preemption Possible</span></span>

<span data-ttu-id="ff79b-228">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-228">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-229">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-229">Example</span></span>

```c
TX_BLOCK_POOL   my_pool;
unsigned char*memory_ptr;
UINT         status;

/* Allocate a memory block from my_pool. Assume that the
   pool has already been created with a call to
   tx_block_pool_create. */
status = tx_block_allocate(&my_pool, (VOID **) &memory_ptr,
                               TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
   address of the allocated block of memory. */
```

### <a name="see-also"></a><span data-ttu-id="ff79b-230">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-230">See Also</span></span>

- <span data-ttu-id="ff79b-231">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-231">tx_block_pool_create</span></span>
- <span data-ttu-id="ff79b-232">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-232">tx_block_pool_delete</span></span>
- <span data-ttu-id="ff79b-233">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-233">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-234">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-234">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-235">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-235">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-236">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-236">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-237">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-237">tx_block_release</span></span>

## <a name="tx_block_pool_create"></a><span data-ttu-id="ff79b-238">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-238">tx_block_pool_create</span></span>
<span data-ttu-id="ff79b-239">Sabit boyutlu bellek blokları Havuzu Oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-239">Create pool of fixed-size memory blocks</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-240">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-240">Prototype</span></span>

```C
UINT tx_block_pool_create(TX_BLOCK_POOL *pool_ptr,
                          CHAR *name_ptr, ULONG block_size,
                          VOID *pool_start, ULONG pool_size);
```
### <a name="description"></a><span data-ttu-id="ff79b-241">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-241">Description</span></span>

<span data-ttu-id="ff79b-242">Bu hizmet sabit boyutlu bellek blokları havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-242">This service creates a pool of fixed-size memory blocks.</span></span> <span data-ttu-id="ff79b-243">Belirtilen bellek alanı, formülü kullanılarak olabildiğince çok sabit boyutlu bellek bloklarına ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-243">The memory area specified is divided into as many fixed-size memory blocks as possible using the formula:</span></span>    
<span data-ttu-id="ff79b-244">**Toplam blok** = (**toplam bayt**)/(**blok boyutu** + sizeof (void \*))</span><span class="sxs-lookup"><span data-stu-id="ff79b-244">**total blocks** = (**total bytes**) / (**block size** + sizeof(void \*))</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-245">Her bellek bloğunda, kullanıcıya görünmeyen bir ek yük işaretçisi bulunur ve önceki formülde "sizeof (void \*)" ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-245">Each memory block contains one pointer of overhead that is invisible to the user and is represented by the “sizeof(void \*)” in the preceding formula.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-246">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-246">Parameters</span></span>

- <span data-ttu-id="ff79b-247">**pool_ptr**: bellek blok havuzu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-247">**pool_ptr**: Pointer to a memory block pool control block.</span></span>
- <span data-ttu-id="ff79b-248">**name_ptr**: bellek bloğu havuzunun adına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-248">**name_ptr**: Pointer to the name of the memory block pool.</span></span>
- <span data-ttu-id="ff79b-249">**block_size**: her bir bellek bloğundaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-249">**block_size**: Number of bytes in each memory block.</span></span>
- <span data-ttu-id="ff79b-250">**pool_start**: bellek bloğu havuzunun başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-250">**pool_start**: Starting address of the memory block pool.</span></span> <span data-ttu-id="ff79b-251">Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-251">The starting address must be aligned to the size of the ULONG data type..</span></span>
- <span data-ttu-id="ff79b-252">**pool_size**: bellek blok havuzu için kullanılabilen toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-252">**pool_size**: Total number of bytes available for the memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-253">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-253">Return Values</span></span>

- <span data-ttu-id="ff79b-254">**TX_SUCCESS**: (0x00) başarılı bellek bloğu havuzu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-254">**TX_SUCCESS**: (0x00) Successful memory block pool creation.</span></span>
- <span data-ttu-id="ff79b-255">TX_POOL_ERROR: (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-255">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span> <span data-ttu-id="ff79b-256">İşaretçi NULL ya da havuz zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-256">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="ff79b-257">TX_PTR_ERROR: (0x03) havuzun başlangıç adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-257">TX_PTR_ERROR: (0x03) Invalid starting address of the pool.</span></span>
- <span data-ttu-id="ff79b-258">TX_SIZE_ERROR: (0x05) havuzun boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-258">TX_SIZE_ERROR: (0x05) Size of pool is invalid.</span></span>
- <span data-ttu-id="ff79b-259">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-259">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-260">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-260">Allowed From</span></span>

<span data-ttu-id="ff79b-261">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-261">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-262">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-262">Preemption Possible</span></span>

<span data-ttu-id="ff79b-263">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-263">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-264">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-264">Example</span></span>

```C
TX_BLOCK_POOL  my_pool;
UINT           status;

/* Create a memory pool whose total size is 1000 bytes
   starting at address 0x100000. Each block in this
   pool is defined to be 50 bytes long. */
status = tx_block_pool_create(&my_pool, "my_pool_name",
               50, (VOID *) 0x100000, 1000);

/* If status equals TX_SUCCESS, my_pool contains 18
   memory blocks of 50 bytes each. The reason
   there are not 20 blocks in the pool is
   because of the one overhead pointer associated with each
   block. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-265">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-265">See Also</span></span>

- <span data-ttu-id="ff79b-266">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-266">tx_block_allocate</span></span>
- <span data-ttu-id="ff79b-267">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-267">tx_block_pool_delete</span></span>
- <span data-ttu-id="ff79b-268">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-268">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-269">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-269">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-270">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-270">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-271">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-271">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-272">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-272">tx_block_release</span></span>

## <a name="tx_block_pool_delete"></a><span data-ttu-id="ff79b-273">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-273">tx_block_pool_delete</span></span>

<span data-ttu-id="ff79b-274">Bellek blok havuzunu Sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-274">Delete memory block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-275">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-275">Prototype</span></span>

```C
UINT tx_block_pool_delete(TX_BLOCK_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-276">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-276">Description</span></span>

<span data-ttu-id="ff79b-277">Bu hizmet, belirtilen blok bellek havuzunu siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-277">This service deletes the specified block-memory pool.</span></span> <span data-ttu-id="ff79b-278">Bu havuzdan bir bellek bloğunun beklediği tüm iş parçacıkları sürdürülür ve TX_DELETED bir dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-278">All threads suspended waiting for a memory block from this pool are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-279">Bu hizmet tamamlandıktan sonra kullanılabilir olan havuz ile ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-279">It is the application’s responsibility to manage the memory area associated with the pool, which is available after this service completes.</span></span> <span data-ttu-id="ff79b-280">Ayrıca, uygulamanın silinen bir havuzun veya eski bellek bloklarının kullanımını engellemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-280">In addition, the application must prevent use of a deleted pool or its former memory blocks.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-281">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-281">Parameters</span></span>

- <span data-ttu-id="ff79b-282">**pool_ptr**: daha önce oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-282">**pool_ptr**: Pointer to a previously created memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-283">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-283">Return Values</span></span>

- <span data-ttu-id="ff79b-284">**TX_SUCCESS**: (0x00) başarılı bellek blok havuzu silme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-284">**TX_SUCCESS**: (0x00) Successful memory block pool deletion.</span></span>
- <span data-ttu-id="ff79b-285">TX_POOL_ERROR: (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-285">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="ff79b-286">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-286">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-287">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-287">Allowed From</span></span>

<span data-ttu-id="ff79b-288">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-288">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-289">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-289">Preemption Possible</span></span>

<span data-ttu-id="ff79b-290">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-290">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-291">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-291">Example</span></span>

```C
TX_BLOCK_POOLmy_pool;
UINT           status;

    /* Delete entire memory block pool. Assume that the pool
      has already been created with a call to
      tx_block_pool_create. */
    status =  tx_block_pool_delete(&my_pool);

    /* If status equals TX_SUCCESS, the memory block pool is
       deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-292">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-292">See Also</span></span>

- <span data-ttu-id="ff79b-293">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-293">tx_block_allocate</span></span>
- <span data-ttu-id="ff79b-294">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-294">tx_block_pool_create</span></span>
- <span data-ttu-id="ff79b-295">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-295">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-296">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-296">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-297">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-297">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-298">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-298">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-299">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-299">tx_block_release</span></span>

## <a name="tx_block_pool_info_get"></a><span data-ttu-id="ff79b-300">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-300">tx_block_pool_info_get</span></span>

<span data-ttu-id="ff79b-301">Blok havuzu hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="ff79b-301">Retrieve information about block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-302">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-302">Prototype</span></span>

```C
UINT tx_block_pool_info_get(TX_BLOCK_POOL *pool_ptr, CHAR **name,
                          ULONG *available, ULONG *total_blocks,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_BLOCK_POOL **next_pool);
```
### <a name="description"></a><span data-ttu-id="ff79b-303">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-303">Description</span></span>

<span data-ttu-id="ff79b-304">Bu hizmet, belirtilen blok bellek havuzu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-304">This service retrieves information about the specified block memory pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-305">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-305">Parameters</span></span>

- <span data-ttu-id="ff79b-306">**pool_ptr**: daha önce oluşturulmuş bellek bloğu havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-306">**pool_ptr**: Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="ff79b-307">**ad**: blok havuzunun adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-307">**name**: Pointer to destination for the pointer to the block pool’s name.</span></span>
- <span data-ttu-id="ff79b-308">**kullanılabilir**: blok havuzundaki kullanılabilir blok sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-308">**available**: Pointer to destination for the number of available blocks in the block pool.</span></span>
- <span data-ttu-id="ff79b-309">**total_blocks**: blok havuzundaki toplam blok sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-309">**total_blocks**: Pointer to destination for the total number of blocks in the block pool.</span></span>
- <span data-ttu-id="ff79b-310">**first_suspended**: Bu blok havuzunun askıya alınma listesindeki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-310">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this block pool.</span></span>
- <span data-ttu-id="ff79b-311">**suspended_count**: Bu blok havuzunda Şu anda askıya alınmış olan iş parçacıklarının sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-311">**suspended_count**: Pointer to destination for the number of threads currently suspended on this block pool.</span></span>
- <span data-ttu-id="ff79b-312">**next_pool**: sonraki oluşturulan blok havuzun işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-312">**next_pool**: Pointer to destination for the pointer of the next created block pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-313">Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-313">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-314">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-314">Return Values</span></span>

- <span data-ttu-id="ff79b-315">**TX_SUCCESS**: (0x00) başarılı blok havuzu bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-315">**TX_SUCCESS**: (0x00) Successful block pool information retrieve.</span></span>
- <span data-ttu-id="ff79b-316">TX_POOL_ERROR: (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-316">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-317">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-317">Allowed From</span></span>

<span data-ttu-id="ff79b-318">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-318">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-319">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-319">Example</span></span>

```C
TX_BLOCK_POOL    my_pool;
CHAR             *name;
ULONG            available;
ULONG            total_blocks;
TX_THREAD        *first_suspended;
ULONG            suspended_count;
TX_BLOCK_POOL    *next_pool;
UINT             status;

/* Retrieve information about the previously created
   block pool "my_pool." */
status = tx_block_pool_info_get(&my_pool, &name,
                &available,&total_blocks,
                &first_suspended, &suspended_count,
                &next_pool);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-320">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-320">See Also</span></span>

- <span data-ttu-id="ff79b-321">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-321">tx_block_allocate</span></span>
- <span data-ttu-id="ff79b-322">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-322">tx_block_pool_create</span></span>
- <span data-ttu-id="ff79b-323">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-323">tx_block_pool_delete</span></span>
- <span data-ttu-id="ff79b-324">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-324">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-325">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-325">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-326">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-326">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-327">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-327">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-328">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-328">tx_block_release</span></span>

## <a name="tx_block_pool_performance_info_get"></a><span data-ttu-id="ff79b-329">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-329">tx_block_pool_performance_info_get</span></span>

<span data-ttu-id="ff79b-330">Blok havuzu performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-330">Get block pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-331">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-331">Prototype</span></span>

```c
UINT tx_block_pool_performance_info_get(TX_BLOCK_POOL *pool_ptr,
       ULONG *allocates, ULONG *releases,
       ULONG *suspensions, ULONG *timeouts));
```

### <a name="description"></a><span data-ttu-id="ff79b-332">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-332">Description</span></span>

<span data-ttu-id="ff79b-333">Bu hizmet, belirtilen bellek bloğu havuzuyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-333">This service retrieves performance information about the specified memory block pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-334">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-334">The ThreadX SMP library and application must be built with **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-335">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-335">Parameters</span></span>

- <span data-ttu-id="ff79b-336">**pool_ptr**: daha önce oluşturulmuş bellek bloğu havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-336">**pool_ptr**: Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="ff79b-337">ayır: Bu havuzda gerçekleştirilen **ayrılan** istek sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-337">**allocates**: Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="ff79b-338">**yayınlar**: Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-338">**releases**: Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="ff79b-339">**getirilmesi**: Bu havuzdaki iş parçacığı ayırma getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-339">**suspensions**: Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="ff79b-340">**zaman aşımları**: Bu havuzda askıya alınma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-340">**timeouts**: Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-341">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-341">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-342">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-342">Return Values</span></span>

- <span data-ttu-id="ff79b-343">**TX_SUCCESS**: (0x00) başarılı blok havuzu performans Get.</span><span class="sxs-lookup"><span data-stu-id="ff79b-343">**TX_SUCCESS**: (0x00) Successful block pool performance get.</span></span>
- <span data-ttu-id="ff79b-344">**TX_PTR_ERROR**: (0x03) geçersiz blok havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-344">**TX_PTR_ERROR**: (0x03) Invalid block pool pointer.</span></span>
- <span data-ttu-id="ff79b-345">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-345">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-346">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-346">Allowed From</span></span>

<span data-ttu-id="ff79b-347">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-347">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-348">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-348">Example</span></span>

```C
TX_BLOCK_POOL     my_pool;
ULONG             allocates;
ULONG             releases;
ULONG             suspensions;
ULONG             timeouts;

/* Retrieve performance information on the previously created block
   pool. */
status = tx_block_pool_performance_info_get(&my_pool, &allocates,
                                            &releases,
                &suspensions,
                &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-349">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-349">See Also</span></span>

- <span data-ttu-id="ff79b-350">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-350">tx_block_allocate</span></span>
- <span data-ttu-id="ff79b-351">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-351">tx_block_pool_create</span></span>
- <span data-ttu-id="ff79b-352">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-352">tx_block_pool_delete</span></span>
- <span data-ttu-id="ff79b-353">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-353">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-354">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-354">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-355">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-355">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-356">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-356">tx_block_release</span></span>

## <a name="tx_block_pool_performance_system_info_get"></a><span data-ttu-id="ff79b-357">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-357">tx_block_pool_performance_system_info_get</span></span>

<span data-ttu-id="ff79b-358">Blok havuzu sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-358">Get block pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-359">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-359">Prototype</span></span>

```C
UINT tx_block_pool_performance_system_info_get(ULONG *allocates,
       ULONG *releases, ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-360">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-360">Description</span></span>

<span data-ttu-id="ff79b-361">Bu hizmet, uygulamadaki tüm bellek blok havuzlarıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-361">This service retrieves performance information about all memory block pools in the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-362">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-362">The ThreadX SMP library and application must be built with **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-363">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-363">Parameters</span></span>

- <span data-ttu-id="ff79b-364">**ayırır**: tüm blok havuzlarında gerçekleştirilen toplam ayırma isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-364">**allocates**: Pointer to destination for the total number of allocate requests performed on all block pools.</span></span>
- <span data-ttu-id="ff79b-365">**yayınlar**: tüm blok havuzlarında gerçekleştirilen yayın isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-365">**releases**: Pointer to destination for the total number of release requests performed on all block pools.</span></span>
- <span data-ttu-id="ff79b-366">**getirilmesi**: tüm blok havuzlarındaki iş parçacığı ayırma getirilmesi toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-366">**suspensions**: Pointer to destination for the total number of thread allocation suspensions on all block pools.</span></span>
- <span data-ttu-id="ff79b-367">**zaman aşımları**: tüm blok havuzlarında askıya alınma zaman aşımlarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-367">**timeouts**: Pointer to destination for the total number of allocate suspension timeouts on all block pools.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-368">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-368">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-369">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-369">Return Values</span></span>

- <span data-ttu-id="ff79b-370">**TX_SUCCESS**: (0x00) başarılı blok havuzu sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-370">**TX_SUCCESS**: (0x00) Successful block pool system performance get.</span></span>
- <span data-ttu-id="ff79b-371">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-371">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-372">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-372">Allowed From</span></span>

<span data-ttu-id="ff79b-373">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-373">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-374">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-374">Example</span></span>

```C
ULONG         allocates;
ULONG         releases;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all the block pools in
   the system. */
status = tx_block_pool_performance_system_info_get(&allocates,
                     &releases,&suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-375">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-375">See Also</span></span>

- <span data-ttu-id="ff79b-376">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-376">tx_block_allocate</span></span>
- <span data-ttu-id="ff79b-377">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-377">tx_block_pool_create</span></span>
- <span data-ttu-id="ff79b-378">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-378">tx_block_pool_delete</span></span>
- <span data-ttu-id="ff79b-379">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-379">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-380">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-380">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-381">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-381">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-382">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-382">tx_block_release</span></span>

## <a name="tx_block_pool_prioritize"></a><span data-ttu-id="ff79b-383">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-383">tx_block_pool_prioritize</span></span>

<span data-ttu-id="ff79b-384">Blok havuzunu askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="ff79b-384">Prioritize block pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-385">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-385">Prototype</span></span>

```C
UINT tx_block_pool_prioritize(TX_BLOCK_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-386">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-386">Description</span></span>

<span data-ttu-id="ff79b-387">Bu hizmet, askıya alma listesinin önünde bu havuzdaki bellek bloğu için en yüksek öncelikli iş parçacığını askıya aldı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-387">This service places the highest priority thread suspended for a block of memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="ff79b-388">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-388">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-389">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-389">Parameters</span></span> 

- <span data-ttu-id="ff79b-390">**pool_ptr**: bellek blok havuzu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-390">**pool_ptr**: Pointer to a memory block pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-391">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-391">Return Values</span></span>

- <span data-ttu-id="ff79b-392">**TX_SUCCESS**: (0x00) başarılı blok havuzu önceliği.</span><span class="sxs-lookup"><span data-stu-id="ff79b-392">**TX_SUCCESS**: (0x00) Successful block pool prioritize.</span></span>
- <span data-ttu-id="ff79b-393">TX_POOL_ERROR: (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-393">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-394">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-394">Allowed From</span></span>

<span data-ttu-id="ff79b-395">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-395">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-396">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-396">Preemption Possible</span></span>

<span data-ttu-id="ff79b-397">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-397">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-398">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-398">Example</span></span>

```C
TX_BLOCK_POOL my_pool;
UINT          status;

/* Ensure that the highest priority thread will receive
   the next free block in this pool. */
status = tx_block_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_block_release call will wake up this thread. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-399">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-399">See Also</span></span>

- <span data-ttu-id="ff79b-400">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-400">tx_block_allocate</span></span>
- <span data-ttu-id="ff79b-401">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-401">tx_block_pool_create</span></span>
- <span data-ttu-id="ff79b-402">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-402">tx_block_pool_delete</span></span>
- <span data-ttu-id="ff79b-403">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-403">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-404">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-404">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-405">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-405">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-406">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-406">tx_block_release</span></span>

## <a name="tx_block_release"></a><span data-ttu-id="ff79b-407">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-407">tx_block_release</span></span>

<span data-ttu-id="ff79b-408">Sabit boyutlu bellek bloğunu serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="ff79b-408">Release fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-409">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-409">Prototype</span></span>

```C
UINT tx_block_release(VOID *block_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-410">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-410">Description</span></span>

<span data-ttu-id="ff79b-411">Bu hizmet önceden ayrılmış bir bloğu, ilişkili bellek havuzuna geri yayınlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-411">This service releases a previously allocated block back to its associated memory pool.</span></span> <span data-ttu-id="ff79b-412">Bu havuzdan bellek blokları bekleyen bir veya daha fazla iş parçacığı varsa, askıya alınan ilk iş parçacığına bu bellek bloğu verilir ve devam edilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-412">If there are one or more threads suspended waiting for memory blocks from this pool, the first thread suspended is given this memory block and resumed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-413">Uygulamanın, havuza geri sunulduktan sonra bir bellek bloğu alanını kullanmasını engellemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-413">The application must prevent using a memory block area after it has been released back to the pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-414">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-414">Parameters</span></span>

- <span data-ttu-id="ff79b-415">**block_ptr**: önceden ayrılmış bellek bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-415">**block_ptr**: Pointer to the previously allocated memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-416">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-416">Return Values</span></span>

- <span data-ttu-id="ff79b-417">**TX_SUCCESS**: (0x00) başarılı bellek bloğu sürümü.</span><span class="sxs-lookup"><span data-stu-id="ff79b-417">**TX_SUCCESS**: (0x00) Successful memory block release.</span></span>
- <span data-ttu-id="ff79b-418">TX_PTR_ERROR: (0x03) bellek bloğunun işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-418">TX_PTR_ERROR: (0x03) Invalid pointer to memory block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-419">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-419">Allowed From</span></span>

<span data-ttu-id="ff79b-420">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-420">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-421">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-421">Preemption Possible</span></span>

<span data-ttu-id="ff79b-422">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-422">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-423">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-423">Example</span></span>

```C
TX_BLOCK_POOLmy_pool;
unsigned char*memory_ptr;
UINT         status;

/* Release a memory block back to my_pool. Assume that the
   pool has been created and the memory block has been
   allocated. */
status = tx_block_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the block of memory pointed
   to by memory_ptr has been returned to the pool. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-424">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-424">See Also</span></span>

- <span data-ttu-id="ff79b-425">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-425">tx_block_allocate</span></span>
- <span data-ttu-id="ff79b-426">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-426">tx_block_pool_create</span></span>
- <span data-ttu-id="ff79b-427">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-427">tx_block_pool_delete</span></span>
- <span data-ttu-id="ff79b-428">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-428">tx_block_pool_info_get</span></span>
- <span data-ttu-id="ff79b-429">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-429">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-430">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-430">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-431">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-431">tx_block_pool_prioritize</span></span>

## <a name="tx_byte_allocate"></a><span data-ttu-id="ff79b-432">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-432">tx_byte_allocate</span></span>

<span data-ttu-id="ff79b-433">Bellek baytları ayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-433">Allocate bytes of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-434">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-434">Prototype</span></span>

```C
UINT tx_byte_allocate(TX_BYTE_POOL *pool_ptr,
                          VOID **memory_ptr, ULONG memory_size,
                          ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-435">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-435">Description</span></span>

<span data-ttu-id="ff79b-436">Bu hizmet, belirtilen bellek bayt havuzundan belirtilen sayıda bayt ayırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-436">This service allocates the specified number of bytes from the specified memory byte pool.</span></span>

> [!WARNING]
> <span data-ttu-id="ff79b-437">Uygulama kodunun ayrılan bellek bloğunun dışına yazmadığından emin olmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-437">It is important to ensure application code does not write outside the allocated memory block.</span></span> <span data-ttu-id="ff79b-438">Bu durumda, bir komşu (genellikle sonraki) bellek bloğunda bozulma oluşur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-438">If this happens, corruption occurs in an adjacent (usually subsequent) memory block.</span></span> <span data-ttu-id="ff79b-439">Sonuçlar tahmin edilemez ve genellikle önemli olur!</span><span class="sxs-lookup"><span data-stu-id="ff79b-439">The results are unpredictable and are often fatal!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-440">Bu hizmetin performansı, blok boyutunun ve havuzdaki parçalanma miktarının bir işlevidir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-440">The performance of this service is a function of the block size and the amount of fragmentation in the pool.</span></span> <span data-ttu-id="ff79b-441">Bu nedenle, bu hizmet yürütmenin zaman kritik iş parçacıkları sırasında kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-441">Hence, this service should not be used during time-critical threads of execution.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-442">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-442">Parameters</span></span>

- <span data-ttu-id="ff79b-443">**pool_ptr**: daha önce oluşturulmuş bir bellek havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-443">**pool_ptr**: Pointer to a previously created memory pool.</span></span>
- <span data-ttu-id="ff79b-444">**memory_ptr**: hedef bellek işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-444">**memory_ptr**: Pointer to a destination memory pointer.</span></span> <span data-ttu-id="ff79b-445">Başarılı bir ayırma sırasında, ayrılan bellek alanının adresi bu parametrenin işaret ettiği yere yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-445">On successful allocation, the address of the allocated memory area is placed where this parameter points to.</span></span>
- <span data-ttu-id="ff79b-446">**memory_size**: istenen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-446">**memory_size**: Number of bytes requested.</span></span>
- <span data-ttu-id="ff79b-447">**wait_option**: yeterli kullanılabilir bellek yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-447">**wait_option**: Defines how the service behaves if there is not enough memory available.</span></span> <span data-ttu-id="ff79b-448">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-448">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-449">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-449">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="ff79b-450">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-450">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="ff79b-451">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-451">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="ff79b-452">TX_NO_WAIT seçilmesi, başarılı olup olmamasından bağımsız olarak bu hizmetten anında geri dönerek sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-452">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="ff79b-453">*Bu, hizmet başlatma işleminden çağrıldığında geçerli tek seçenektir.*</span><span class="sxs-lookup"><span data-stu-id="ff79b-453">*This is the only valid option if the service is called from initialization.*</span></span>

    <span data-ttu-id="ff79b-454">TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının yeterli bellek kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-454">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until enough memory is available.</span></span>

    <span data-ttu-id="ff79b-455">Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, bellek beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-455">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the memory.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-456">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-456">Return Values</span></span>

- <span data-ttu-id="ff79b-457">**TX_SUCCESS**: (0x00) başarılı bellek ayırma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-457">**TX_SUCCESS**: (0x00) Successful memory allocation.</span></span>
- <span data-ttu-id="ff79b-458">**TX_DELETED**: (0x01) bellek havuzu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-458">**TX_DELETED**: (0x01) Memory pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-459">**TX_NO_MEMORY**: (0x10) hizmeti, belleği, belirtilen süre içinde beklemek için ayıramadı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-459">**TX_NO_MEMORY**: (0x10) Service was unable to allocate the memory within the specified time to wait.</span></span>
- <span data-ttu-id="ff79b-460">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-460">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-461">TX_POOL_ERROR: (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-461">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="ff79b-462">TX_PTR_ERROR: (0x03) hedef işaretçisine geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-462">TX_PTR_ERROR: (0x03) Invalid pointer to destination pointer.</span></span>
- <span data-ttu-id="ff79b-463">TX_SIZE_ERROR: (0X05) Istenen Boyut sıfır veya havuzdan büyük.</span><span class="sxs-lookup"><span data-stu-id="ff79b-463">TX_SIZE_ERROR: (0X05) Requested size is zero or larger than the pool.</span></span>
- <span data-ttu-id="ff79b-464">TX_WAIT_ERROR: (0x04) iş parçacığından oluşan çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-464">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="ff79b-465">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-465">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-466">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-466">Allowed From</span></span>

<span data-ttu-id="ff79b-467">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-467">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-468">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-468">Preemption Possible</span></span>

<span data-ttu-id="ff79b-469">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-469">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-470">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-470">Example</span></span>

```C
TX_BYTE_POOL my_pool;
unsigned char*memory_ptr;
UINT         status;

/* Allocate a 112 byte memory area from my_pool. Assume
   that the pool has already been created with a call to
   tx_byte_pool_create. */
status =  tx_byte_allocate(&my_pool, (VOID **) &memory_ptr,
                       112, TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
   address of the allocated memory area. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-471">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-471">See Also</span></span>

- <span data-ttu-id="ff79b-472">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-472">tx_byte_pool_create</span></span>
- <span data-ttu-id="ff79b-473">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-473">tx_byte_pool_delete</span></span>
- <span data-ttu-id="ff79b-474">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-474">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="ff79b-475">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-475">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-476">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-476">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-477">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-477">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-478">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-478">tx_byte_release</span></span>

## <a name="tx_byte_pool_create"></a><span data-ttu-id="ff79b-479">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-479">tx_byte_pool_create</span></span>

<span data-ttu-id="ff79b-480">Bayt bellek havuzu oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-480">Create memory pool of bytes</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-481">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-481">Prototype</span></span>

```C
UINT tx_byte_pool_create(TX_BYTE_POOL *pool_ptr,
                          CHAR *name_ptr, VOID *pool_start,
                          ULONG pool_size);
```
### <a name="description"></a><span data-ttu-id="ff79b-482">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-482">Description</span></span>

<span data-ttu-id="ff79b-483">Bu hizmet, belirtilen alanda bir bellek bayt havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-483">This service creates a memory byte pool in the area specified.</span></span> <span data-ttu-id="ff79b-484">İlk olarak havuz, temel olarak bir çok büyük ücretsiz bloğundan oluşur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-484">Initially the pool consists of basically one very large free block.</span></span> <span data-ttu-id="ff79b-485">Ancak, ayırmalar yapıldığından havuz daha küçük bloklar halinde bozulur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-485">However, the pool is broken into smaller blocks as allocations are made.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-486">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-486">Parameters</span></span>

- <span data-ttu-id="ff79b-487">**pool_ptr**: bellek havuzu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-487">**pool_ptr**: Pointer to a memory pool control block.</span></span>
- <span data-ttu-id="ff79b-488">**name_ptr**: bellek havuzunun adına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-488">**name_ptr**: Pointer to the name of the memory pool.</span></span>
- <span data-ttu-id="ff79b-489">**pool_start**: bellek havuzunun başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-489">**pool_start**: Starting address of the memory pool.</span></span> <span data-ttu-id="ff79b-490">Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-490">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="ff79b-491">**pool_size**: bellek havuzu için kullanılabilen toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-491">**pool_size**: Total number of bytes available for the memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-492">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-492">Return Values</span></span>

- <span data-ttu-id="ff79b-493">**TX_SUCCESS**: (0x00) başarılı bellek havuzu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-493">**TX_SUCCESS**: (0x00) Successful memory pool creation.</span></span>
- <span data-ttu-id="ff79b-494">TX_POOL_ERROR: (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-494">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span> <span data-ttu-id="ff79b-495">İşaretçi NULL ya da havuz zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-495">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="ff79b-496">TX_PTR_ERROR: (0x03) havuzun başlangıç adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-496">TX_PTR_ERROR: (0x03) Invalid starting address of the pool.</span></span>
- <span data-ttu-id="ff79b-497">TX_SIZE_ERROR: (0x05) havuzun boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-497">TX_SIZE_ERROR: (0x05) Size of pool is invalid.</span></span>
- <span data-ttu-id="ff79b-498">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-498">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-499">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-499">Allowed From</span></span>

<span data-ttu-id="ff79b-500">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-500">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-501">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-501">Preemption Possible</span></span>

<span data-ttu-id="ff79b-502">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-502">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-503">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-503">Example</span></span>

```C
TX_BYTE_POOL my_pool;
UINT         status;

/* Create a memory pool whose total size is 2000 bytes
   starting at address 0x500000. */
status =  tx_byte_pool_create(&my_pool, "my_pool_name",
             (VOID *) 0x500000, 2000);

/* If status equals TX_SUCCESS, my_pool is available for
   allocating memory. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-504">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-504">See Also</span></span>

- <span data-ttu-id="ff79b-505">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-505">tx_byte_allocate</span></span>
- <span data-ttu-id="ff79b-506">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-506">tx_byte_pool_delete</span></span>
- <span data-ttu-id="ff79b-507">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-507">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="ff79b-508">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-508">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-509">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-509">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-510">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-510">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-511">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-511">tx_byte_release</span></span>

## <a name="tx_byte_pool_delete"></a><span data-ttu-id="ff79b-512">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-512">tx_byte_pool_delete</span></span>

<span data-ttu-id="ff79b-513">Bellek bayt havuzunu Sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-513">Delete memory byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-514">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-514">Prototype</span></span>

```C
UINT tx_byte_pool_delete(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-515">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-515">Description</span></span>

<span data-ttu-id="ff79b-516">Bu hizmet, belirtilen bellek bayt havuzunu siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-516">This service deletes the specified memory byte pool.</span></span> <span data-ttu-id="ff79b-517">Bu havuzdan bellek beklemeyi askıya alınmış tüm iş parçacıkları sürdürülür ve TX_DELETED bir dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-517">All threads suspended waiting for memory from this pool are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-518">Bu hizmet tamamlandıktan sonra kullanılabilir olan havuz ile ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-518">It is the application’s responsibility to manage the memory area associated with the pool, which is available after this service completes.</span></span> <span data-ttu-id="ff79b-519">Ayrıca, uygulamanın silinen bir havuzun veya daha önce ayrılmış belleğin kullanımını önlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-519">In addition, the application must prevent use of a deleted pool or memory previously allocated from it.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-520">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-520">Parameters</span></span> 

- <span data-ttu-id="ff79b-521">**pool_ptr**: daha önce oluşturulmuş bir bellek havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-521">**pool_ptr**: Pointer to a previously created memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-522">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-522">Return Values</span></span>

- <span data-ttu-id="ff79b-523">**TX_SUCCESS**: (0x00) başarılı bellek havuzu silme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-523">**TX_SUCCESS**: (0x00) Successful memory pool deletion.</span></span>
- <span data-ttu-id="ff79b-524">TX_POOL_ERROR: (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-524">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="ff79b-525">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-525">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-526">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-526">Allowed From</span></span>

<span data-ttu-id="ff79b-527">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-527">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-528">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-528">Preemption Possible</span></span>

<span data-ttu-id="ff79b-529">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-529">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-530">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-530">Example</span></span>

```C
TX_BYTE_POOL my_pool;
UINT         status;

/* Delete entire memory pool. Assume that the pool has already
   been created with a call to tx_byte_pool_create. */
status =   tx_byte_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, memory pool is deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-531">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-531">See Also</span></span>

- <span data-ttu-id="ff79b-532">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-532">tx_byte_allocate</span></span>
- <span data-ttu-id="ff79b-533">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-533">tx_byte_pool_create</span></span>
- <span data-ttu-id="ff79b-534">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-534">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="ff79b-535">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-535">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-536">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-536">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-537">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-537">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-538">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-538">tx_byte_release</span></span>

## <a name="tx_byte_pool_info_get"></a><span data-ttu-id="ff79b-539">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-539">tx_byte_pool_info_get</span></span>

<span data-ttu-id="ff79b-540">Bayt havuzu hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="ff79b-540">Retrieve information about byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-541">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-541">Prototype</span></span>

```C
UINT tx_byte_pool_info_get(TX_BYTE_POOL *pool_ptr, CHAR **name,
                          ULONG *available, ULONG *fragments,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_BYTE_POOL **next_pool);
```
### <a name="description"></a><span data-ttu-id="ff79b-542">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-542">Description</span></span>

<span data-ttu-id="ff79b-543">Bu hizmet, belirtilen bellek bayt havuzu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-543">This service retrieves information about the specified memory byte pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-544">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-544">Parameters</span></span>

- <span data-ttu-id="ff79b-545">**pool_ptr**: daha önce oluşturulmuş bellek havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-545">**pool_ptr**: Pointer to previously created memory pool.</span></span>
- <span data-ttu-id="ff79b-546">**ad**: bayt havuzunun adı işaretçisinin hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-546">**name**: Pointer to destination for the pointer to the byte pool’s name.</span></span>
- <span data-ttu-id="ff79b-547">**kullanılabilir**: havuzdaki kullanılabilir bayt sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-547">**available**: Pointer to destination for the number of available bytes in the pool.</span></span>
- <span data-ttu-id="ff79b-548">**parçalar**: bayt havuzundaki toplam bellek parçası sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-548">**fragments**: Pointer to destination for the total number of memory fragments in the byte pool.</span></span>
- <span data-ttu-id="ff79b-549">**first_suspended**: Bu bayt havuzunun askıya alınma listesindeki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-549">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this byte pool.</span></span>
- <span data-ttu-id="ff79b-550">**suspended_count**: Bu bayt havuzunda Şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-550">**suspended_count**: Pointer to destination for the number of threads currently suspended on this byte pool.</span></span>
- <span data-ttu-id="ff79b-551">**next_pool**: sonraki oluşturulan bayt havuzunun işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-551">**next_pool**: Pointer to destination for the pointer of the next created byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-552">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-552">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-553">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-553">Return Values</span></span>

- <span data-ttu-id="ff79b-554">**TX_SUCCESS**: (0x00) başarılı havuz bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-554">**TX_SUCCESS**: (0x00) Successful pool information retrieve.</span></span>
- <span data-ttu-id="ff79b-555">TX_POOL_ERROR: (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-555">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-556">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-556">Allowed From</span></span>

<span data-ttu-id="ff79b-557">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-557">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-558">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-558">Preemption Possible</span></span>

<span data-ttu-id="ff79b-559">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-559">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-560">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-560">Example</span></span>

```C
TX_BYTE_POOL my_pool;
CHAR         *name;
ULONG        available;
ULONG        fragments;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_BYTE_POOL *next_pool;
UINT         status;

/* Retrieve information about the previously created
   block pool "my_pool." */
status =  tx_byte_pool_info_get(&my_pool, &name,
             &available, &fragments,
             &first_suspended, &suspended_count,
             &next_pool);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-561">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-561">See Also</span></span>

- <span data-ttu-id="ff79b-562">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-562">tx_byte_allocate</span></span>
- <span data-ttu-id="ff79b-563">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-563">tx_byte_pool_create</span></span>
- <span data-ttu-id="ff79b-564">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-564">tx_byte_pool_delete</span></span>
- <span data-ttu-id="ff79b-565">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-565">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-566">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-566">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-567">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-567">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-568">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-568">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_info_get"></a><span data-ttu-id="ff79b-569">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-569">tx_byte_pool_performance_info_get</span></span>

<span data-ttu-id="ff79b-570">Bayt havuzu performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-570">Get byte pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-571">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-571">Prototype</span></span>

```C
UINT tx_byte_pool_performance_info_get(TX_BYTE_POOL *pool_ptr,
        ULONG *allocates, ULONG *releases,
        ULONG *fragments_searched, ULONG *merges, ULONG *splits,
        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-572">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-572">Description</span></span>

<span data-ttu-id="ff79b-573">Bu hizmet, belirtilen bellek bayt havuzuyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-573">This service retrieves performance information about the specified memory byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-574">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-574">The ThreadX SMP library and application must be built with **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-575">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-575">Parameters</span></span>

- <span data-ttu-id="ff79b-576">**pool_ptr**: daha önce oluşturulan bellek bayt havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-576">**pool_ptr**: Pointer to previously created memory byte pool.</span></span>
- <span data-ttu-id="ff79b-577">ayır: Bu havuzda gerçekleştirilen **ayrılan** istek sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-577">**allocates**: Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="ff79b-578">**yayınlar**: Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-578">**releases**: Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="ff79b-579">**fragments_searched**: Bu havuzdaki ayırma istekleri sırasında aranan iç bellek parçacıklarının sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-579">**fragments_searched**: Pointer to destination for the number of internal memory fragments searched during allocation requests on this pool.</span></span>
- <span data-ttu-id="ff79b-580">**birleştirmeler**: Bu havuzdaki ayırma istekleri sırasında birleştirilmiş iç bellek blokları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-580">**merges**: Pointer to destination for the number of internal memory blocks merged during allocation requests on this pool.</span></span>
- <span data-ttu-id="ff79b-581">**bölmeler**: Bu havuzdaki ayırma istekleri sırasında oluşturulan iç bellek blokları sayısı (parçalar) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-581">**splits**: Pointer to destination for the number of internal memory blocks split (fragments) created during allocation requests on this pool.</span></span>
- <span data-ttu-id="ff79b-582">**getirilmesi**: Bu havuzdaki iş parçacığı ayırma getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-582">**suspensions**: Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="ff79b-583">**zaman aşımları**: Bu havuzda askıya alınma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-583">**timeouts**: Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-584">Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-584">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-585">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-585">Return Values</span></span>

- <span data-ttu-id="ff79b-586">TX_SUCCESS: (0x00) başarılı bayt havuzu performans Get.</span><span class="sxs-lookup"><span data-stu-id="ff79b-586">TX_SUCCESS: (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="ff79b-587">**TX_PTR_ERROR**: (0x03) geçersiz bayt havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-587">**TX_PTR_ERROR**: (0x03) Invalid byte pool pointer.</span></span>
- <span data-ttu-id="ff79b-588">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-588">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-589">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-589">Allowed From</span></span>

<span data-ttu-id="ff79b-590">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-590">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-591">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-591">Example</span></span>

```C
TX_BYTE_POOL     my_pool;
ULONG            fragments_searched;
ULONG            merges;
ULONG            splits;
ULONG            allocates;
ULONG            releases;
ULONG            suspensions;
ULONG            timeouts;

/* Retrieve performance information on the previously created byte
   pool.  */
status =  tx_byte_pool_performance_info_get(&my_pool,
                &fragments_searched,
                &merges, &splits,
                &allocates, &releases,
                      &suspensions,&timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-592">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-592">See Also</span></span>

- <span data-ttu-id="ff79b-593">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-593">tx_byte_allocate</span></span>
- <span data-ttu-id="ff79b-594">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-594">tx_byte_pool_create</span></span>
- <span data-ttu-id="ff79b-595">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-595">tx_byte_pool_delete</span></span>
- <span data-ttu-id="ff79b-596">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-596">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="ff79b-597">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-597">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-598">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-598">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-599">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-599">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_system_info_get"></a><span data-ttu-id="ff79b-600">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-600">tx_byte_pool_performance_system_info_get</span></span>

<span data-ttu-id="ff79b-601">Bayt havuzu sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-601">Get byte pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-602">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-602">Prototype</span></span>

```C
UINT  tx_byte_pool_performance_system_info_get(ULONG *allocates,
        ULONG *releases, ULONG *fragments_searched, ULONG *merges,
        ULONG *splits, ULONG *suspensions, ULONG *timeouts);;
```
### <a name="description"></a><span data-ttu-id="ff79b-603">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-603">Description</span></span>

<span data-ttu-id="ff79b-604">Bu hizmet sistemdeki tüm bellek bayt havuzlarıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-604">This service retrieves performance information about all memory byte pools in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-605">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-605">The ThreadX SMP library and application must be built with **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-606">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-606">Parameters</span></span>

- <span data-ttu-id="ff79b-607">ayır: Bu havuzda gerçekleştirilen **ayrılan** istek sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-607">**allocates**: Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="ff79b-608">**yayınlar**: Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-608">**releases**: Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="ff79b-609">**fragments_searched**: tüm bayt havuzlarındaki ayırma istekleri sırasında aranan iç bellek parçacıklarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-609">**fragments_searched**: Pointer to destination for the total number of internal memory fragments searched during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="ff79b-610">**birleştirmeler**: tüm bayt havuzlarındaki ayırma istekleri sırasında birleştirilmiş iç bellek bloklarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-610">**merges**: Pointer to destination for the total number of internal memory blocks merged during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="ff79b-611">**bölmeler**: tüm bayt havuzlarındaki ayırma istekleri sırasında oluşturulan toplam iç bellek bloğu sayısı (parça) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-611">**splits**: Pointer to destination for the total number of internal memory blocks split (fragments) created during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="ff79b-612">**getirilmesi**: tüm bayt havuzlarındaki iş parçacığı ayırma getirilmesi toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-612">**suspensions**: Pointer to destination for the total number of thread allocation suspensions on all byte pools.</span></span>
- <span data-ttu-id="ff79b-613">**zaman aşımları**: tüm bayt havuzlarında askıya alınma zaman aşımlarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-613">**timeouts**: Pointer to destination for the total number of allocate suspension timeouts on all byte pools.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-614">Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-614">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-615">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-615">Return Values</span></span>

- <span data-ttu-id="ff79b-616">**TX_SUCCESS**: (0x00) başarılı bayt havuzu performans Get.</span><span class="sxs-lookup"><span data-stu-id="ff79b-616">**TX_SUCCESS**: (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="ff79b-617">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-617">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-618">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-618">Allowed From</span></span>

<span data-ttu-id="ff79b-619">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-619">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-620">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-620">Example</span></span>

```C
ULONG         fragments_searched;
ULONG         merges;
ULONG         splits;
ULONG         allocates;
ULONG         releases;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all byte pools in the
   system. */
status =
tx_byte_pool_performance_system_info_get(&fragments_searched,
                &merges, &splits, &allocates, &releases,
                &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-621">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-621">See Also</span></span>

- <span data-ttu-id="ff79b-622">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-622">tx_byte_allocate</span></span>
- <span data-ttu-id="ff79b-623">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-623">tx_byte_pool_create</span></span>
- <span data-ttu-id="ff79b-624">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-624">tx_byte_pool_delete</span></span>
- <span data-ttu-id="ff79b-625">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-625">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="ff79b-626">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-626">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-627">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-627">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="ff79b-628">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-628">tx_byte_release</span></span>

## <a name="tx_byte_pool_prioritize"></a><span data-ttu-id="ff79b-629">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-629">tx_byte_pool_prioritize</span></span>

<span data-ttu-id="ff79b-630">Bayt havuzunun askıya alınma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="ff79b-630">Prioritize byte pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-631">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-631">Prototype</span></span>

```c
UINT tx_byte_pool_prioritize(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-632">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-632">Description</span></span>

<span data-ttu-id="ff79b-633">Bu hizmet, bu havuzdaki bellek için askıya alınan en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-633">This service places the highest priority thread suspended for memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="ff79b-634">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-634">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-635">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-635">Parameters</span></span> 

- <span data-ttu-id="ff79b-636">**pool_ptr**: bellek havuzu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-636">**pool_ptr**: Pointer to a memory pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-637">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-637">Return Values</span></span>

- <span data-ttu-id="ff79b-638">**TX_SUCCESS**: (0x00) başarılı bellek havuzu önceliği belirleme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-638">**TX_SUCCESS**: (0x00) Successful memory pool prioritize.</span></span>
- <span data-ttu-id="ff79b-639">TX_POOL_ERROR: (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-639">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-640">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-640">Allowed From</span></span>

<span data-ttu-id="ff79b-641">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-641">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-642">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-642">Preemption Possible</span></span>

<span data-ttu-id="ff79b-643">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-643">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-644">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-644">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next free memory from this pool. */
status = tx_byte_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_byte_release call will wake up this thread,
   if there is enough memory to satisfy its request. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-645">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-645">See Also</span></span>

- <span data-ttu-id="ff79b-646">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-646">tx_byte_allocate</span></span>
- <span data-ttu-id="ff79b-647">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-647">tx_byte_pool_create</span></span>
- <span data-ttu-id="ff79b-648">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-648">tx_byte_pool_delete</span></span>
- <span data-ttu-id="ff79b-649">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-649">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="ff79b-650">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-650">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-651">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-651">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-652">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-652">tx_byte_release</span></span>

## <a name="tx_byte_release"></a><span data-ttu-id="ff79b-653">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="ff79b-653">tx_byte_release</span></span>

<span data-ttu-id="ff79b-654">Baytları bellek havuzuna geri bırakma</span><span class="sxs-lookup"><span data-stu-id="ff79b-654">Release bytes back to memory pool</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-655">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-655">Prototype</span></span>

```C
UINT tx_byte_release(VOID *memory_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-656">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-656">Description</span></span>

<span data-ttu-id="ff79b-657">Bu hizmet önceden ayrılmış bir bellek alanını ilişkili havuzuna geri yayınlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-657">This service releases a previously allocated memory area back to its associated pool.</span></span> <span data-ttu-id="ff79b-658">Bu havuzdan bellek beklemeyi askıya alınmış bir veya daha fazla iş parçacığı varsa, askıya alınan her iş parçacığına bellek verilir ve bellek tükenene veya daha fazla askıya alınmış iş parçacığı kalmayana kadar devam sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-658">If there are one or more threads suspended waiting for memory from this pool, each suspended thread is given memory and resumed until the memory is exhausted or until there are no more suspended threads.</span></span> <span data-ttu-id="ff79b-659">Askıya alınan iş parçacıkları için bellek ayırma işlemi, her zaman askıya alınan ilk iş parçacığı ile başlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-659">This process of allocating memory to suspended threads always begins with the first thread suspended.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-660">Uygulamanın, serbest bırakıldıktan sonra bellek alanını kullanmasını önleyecek olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-660">The application must prevent using the memory area after it is released.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-661">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-661">Parameters</span></span>

- <span data-ttu-id="ff79b-662">**memory_ptr**: önceden ayrılmış bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-662">**memory_ptr**: Pointer to the previously allocated memory area.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-663">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-663">Return Values</span></span>

- <span data-ttu-id="ff79b-664">**TX_SUCCESS**: (0x00) başarılı bellek sürümü.</span><span class="sxs-lookup"><span data-stu-id="ff79b-664">**TX_SUCCESS**: (0x00) Successful memory release.</span></span>
- <span data-ttu-id="ff79b-665">TX_PTR_ERROR: (0x03) geçersiz bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-665">TX_PTR_ERROR: (0x03) Invalid memory area pointer.</span></span>
- <span data-ttu-id="ff79b-666">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-666">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-667">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-667">Allowed From</span></span>

<span data-ttu-id="ff79b-668">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-668">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-669">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-669">Preemption Possible</span></span>

<span data-ttu-id="ff79b-670">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-670">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-671">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-671">Example</span></span>

```C
unsigned char    *memory_ptr;
UINT             status;

/* Release a memory back to my_pool. Assume that the memory
   area was previously allocated from my_pool. */
status =  tx_byte_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the memory pointed to by
   memory_ptr has been returned to the pool. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-672">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-672">See Also</span></span>

- <span data-ttu-id="ff79b-673">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="ff79b-673">tx_byte_allocate</span></span>
- <span data-ttu-id="ff79b-674">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-674">tx_byte_pool_create</span></span>
- <span data-ttu-id="ff79b-675">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-675">tx_byte_pool_delete</span></span>
- <span data-ttu-id="ff79b-676">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-676">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="ff79b-677">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-677">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="ff79b-678">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-678">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-679">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-679">tx_byte_pool_prioritize</span></span>

## <a name="tx_event_flags_create"></a><span data-ttu-id="ff79b-680">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-680">tx_event_flags_create</span></span>

<span data-ttu-id="ff79b-681">Olay bayrakları grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-681">Create event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-682">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-682">Prototype</span></span>

```c
UINT tx_event_flags_create(TX_EVENT_FLAGS_GROUP *group_ptr,
                          CHAR *name_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-683">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-683">Description</span></span>

<span data-ttu-id="ff79b-684">Bu hizmet bir 32 olay bayrağı grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-684">This service creates a group of 32 event flags.</span></span> <span data-ttu-id="ff79b-685">Gruptaki tüm 32 olay bayrakları sıfır olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-685">All 32 event flags in the group are initialized to zero.</span></span> <span data-ttu-id="ff79b-686">Her olay bayrağı tek bir bit ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-686">Each event flag is represented by a single bit.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-687">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-687">Parameters</span></span>

- <span data-ttu-id="ff79b-688">**group_ptr**: bir olay bayrakları Grup denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-688">**group_ptr**: Pointer to an event flags group control block.</span></span> 
- <span data-ttu-id="ff79b-689">**name_ptr**: olay bayrakları grubunun adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-689">**name_ptr**: Pointer to the name of the event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-690">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-690">Return Values</span></span>

- <span data-ttu-id="ff79b-691">**TX_SUCCESS**: (0x00) başarılı olay grubu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-691">**TX_SUCCESS**: (0x00) Successful event group creation.</span></span>
- <span data-ttu-id="ff79b-692">TX_GROUP_ERROR: (0x06) geçersiz olay grubu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-692">TX_GROUP_ERROR: (0x06) Invalid event group pointer.</span></span> <span data-ttu-id="ff79b-693">İşaretçi NULL ya da olay grubu zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-693">Either the pointer is NULL or the event group is already created.</span></span>
- <span data-ttu-id="ff79b-694">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-694">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-695">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-695">Allowed From</span></span>

<span data-ttu-id="ff79b-696">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-696">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-697">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-697">Preemption Possible</span></span>

<span data-ttu-id="ff79b-698">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-698">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-699">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-699">Example</span></span>

```C
TX_EVENT_FLAGS_GROUP my_event_group;
UINT         status;

/* Create an event flags group. */
status = tx_event_flags_create(&my_event_group,
            "my_event_group_name");

/* If status equals TX_SUCCESS, my_event_group is ready
   for get and set services. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-700">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-700">See Also</span></span>

- <span data-ttu-id="ff79b-701">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-701">tx_event_flags_delete</span></span>
- <span data-ttu-id="ff79b-702">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-702">tx_event_flags_get</span></span>
- <span data-ttu-id="ff79b-703">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-703">tx_event_flags_info_get</span></span>
- <span data-ttu-id="ff79b-704">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-704">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="ff79b-705">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-705">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-706">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-706">tx_event_flags_set</span></span>
- <span data-ttu-id="ff79b-707">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-707">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_delete"></a><span data-ttu-id="ff79b-708">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-708">tx_event_flags_delete</span></span>

<span data-ttu-id="ff79b-709">Olay bayrakları grubunu sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-709">Delete event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-710">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-710">Prototype</span></span>

```c
UINT tx_event_flags_delete(TX_EVENT_FLAGS_GROUP *group_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-711">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-711">Description</span></span>

<span data-ttu-id="ff79b-712">Bu hizmet, belirtilen olay bayrakları grubunu siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-712">This service deletes the specified event flags group.</span></span> <span data-ttu-id="ff79b-713">Bu gruptan gelen olayların beklediği tüm iş parçacıkları sürdürülür ve TX_DELETED bir dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-713">All threads suspended waiting for events from this group are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-714">Uygulama, olay bayrakları grubu silinmeden önce bu olay bayrakları grubu için bir küme bildirme geri çağrısının tamamlandığını (veya devre dışı) içerdiğinden emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-714">The application must ensure that a set notify callback for this event flags group is completed (or disabled) before deleting the event flags group.</span></span> <span data-ttu-id="ff79b-715">Ayrıca, uygulamanın, silinen bir olay bayrakları grubunun gelecekteki tüm kullanımını önlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-715">In addition, the application must prevent all future use of a deleted event flags group.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-716">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-716">Parameters</span></span> 

- <span data-ttu-id="ff79b-717">**group_ptr**: daha önce oluşturulmuş bir olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-717">**group_ptr**: Pointer to a previously created event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-718">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-718">Return Values</span></span>

- <span data-ttu-id="ff79b-719">**TX_SUCCESS**: (0x00) başarılı olay bayrakları grubu silme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-719">**TX_SUCCESS**: (0x00) Successful event flags group deletion.</span></span>
- <span data-ttu-id="ff79b-720">TX_GROUP_ERROR: (0x06) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-720">TX_GROUP_ERROR: (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="ff79b-721">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-721">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-722">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-722">Allowed From</span></span>

<span data-ttu-id="ff79b-723">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-723">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-724">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-724">Preemption Possible</span></span>

<span data-ttu-id="ff79b-725">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-725">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-726">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-726">Example</span></span>

```C
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT                 status;

/* Delete event flags group. Assume that the group has
   already been created with a call to
   tx_event_flags_create. */
status = tx_event_flags_delete(&my_event_flags_group);

/* If status equals TX_SUCCESS, the event flags group is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-727">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-727">See Also</span></span>

- <span data-ttu-id="ff79b-728">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-728">tx_event_flags_create</span></span>
- <span data-ttu-id="ff79b-729">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-729">tx_event_flags_get</span></span>
- <span data-ttu-id="ff79b-730">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-730">tx_event_flags_info_get</span></span>
- <span data-ttu-id="ff79b-731">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-731">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="ff79b-732">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-732">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-733">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-733">tx_event_flags_set</span></span>
- <span data-ttu-id="ff79b-734">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-734">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_get"></a><span data-ttu-id="ff79b-735">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-735">tx_event_flags_get</span></span>

<span data-ttu-id="ff79b-736">Olay bayrakları grubundan olay bayraklarını al</span><span class="sxs-lookup"><span data-stu-id="ff79b-736">Get event flags from event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-737">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-737">Prototype</span></span>

```C
UINT tx_event_flags_get(TX_EVENT_FLAGS_GROUP *group_ptr,
                          ULONG requested_flags, UINT get_option,
                          ULONG *actual_flags_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-738">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-738">Description</span></span>

<span data-ttu-id="ff79b-739">Bu hizmet, belirtilen olay bayrakları grubundan olay bayraklarını alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-739">This service retrieves event flags from the specified event flags group.</span></span> <span data-ttu-id="ff79b-740">Her olay bayrakları grubu 32 olay bayrağını içerir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-740">Each event flags group contains 32 event flags.</span></span> <span data-ttu-id="ff79b-741">Her bayrak tek bir bit ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-741">Each flag is represented by a single bit.</span></span> <span data-ttu-id="ff79b-742">Bu hizmet, giriş parametreleri tarafından seçilen çeşitli olay bayrağı kombinasyonlarını alabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-742">This service can retrieve a variety of event flag combinations, as selected by the input parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-743">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-743">Parameters</span></span>

- <span data-ttu-id="ff79b-744">**group_ptr**: daha önce oluşturulmuş bir olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-744">**group_ptr**: Pointer to a previously created event flags group.</span></span>
- <span data-ttu-id="ff79b-745">**requested_flags**: istenen olay bayraklarını temsil eden 32 bitlik işaretsiz değişken.</span><span class="sxs-lookup"><span data-stu-id="ff79b-745">**requested_flags**: 32-bit unsigned variable that represents the requested event flags.</span></span>
- <span data-ttu-id="ff79b-746">**get_option**: istenen olay bayraklarının tümünün veya herhangi birinin gerekli olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-746">**get_option**: Specifies whether all or any of the requested event flags are required.</span></span> <span data-ttu-id="ff79b-747">Aşağıdakiler geçerli seçimlerdir:</span><span class="sxs-lookup"><span data-stu-id="ff79b-747">The following are valid selections:</span></span>
    - <span data-ttu-id="ff79b-748">**TX_AND**: (0x02)</span><span class="sxs-lookup"><span data-stu-id="ff79b-748">**TX_AND**: (0x02)</span></span>
    - <span data-ttu-id="ff79b-749">**TX_AND_CLEAR**: (0x03)</span><span class="sxs-lookup"><span data-stu-id="ff79b-749">**TX_AND_CLEAR**: (0x03)</span></span>
    - <span data-ttu-id="ff79b-750">**TX_OR**: (0x00)</span><span class="sxs-lookup"><span data-stu-id="ff79b-750">**TX_OR**: (0x00)</span></span>
    - <span data-ttu-id="ff79b-751">**TX_OR_CLEAR**: (0x01)</span><span class="sxs-lookup"><span data-stu-id="ff79b-751">**TX_OR_CLEAR**: (0x01)</span></span>

    <span data-ttu-id="ff79b-752">TX_AND veya TX_AND_CLEAR seçilmesi, tüm olay bayraklarının grupta mevcut olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-752">Selecting TX_AND or TX_AND_CLEAR specifies that all event flags must be present in the group.</span></span> <span data-ttu-id="ff79b-753">TX_OR veya TX_OR_CLEAR seçilmesi herhangi bir olay bayrağının tatmin edici olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-753">Selecting TX_OR or TX_OR_CLEAR specifies that any event flag is satisfactory.</span></span> <span data-ttu-id="ff79b-754">TX_AND_CLEAR veya TX_OR_CLEAR belirtilirse, isteği karşılayan olay bayrakları temizlenir (sıfır olarak ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="ff79b-754">Event flags that satisfy the request are cleared (set to zero) if TX_AND_CLEAR or TX_OR_CLEAR are specified.</span></span>

- <span data-ttu-id="ff79b-755">**actual_flags_ptr**: alınan olay bayraklarının yerleştirildiği hedefin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-755">**actual_flags_ptr**: Pointer to destination of where the retrieved event flags are placed.</span></span> <span data-ttu-id="ff79b-756">Alınan gerçek bayrakların istenmedi bayrakları içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ff79b-756">Note that the actual flags obtained may contain flags that were not requested.</span></span>
- <span data-ttu-id="ff79b-757">**wait_option**: seçili olay bayrakları ayarlanmamışsa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-757">**wait_option**: Defines how the service behaves if the selected event flags are not set.</span></span> <span data-ttu-id="ff79b-758">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-758">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-759">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-759">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="ff79b-760">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-760">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="ff79b-761">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-761">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="ff79b-762">TX_NO_WAIT seçilmesi, başarılı olup olmamasından bağımsız olarak bu hizmetten anında geri dönerek sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-762">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="ff79b-763">Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.</span><span class="sxs-lookup"><span data-stu-id="ff79b-763">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>

    <span data-ttu-id="ff79b-764">TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının olay bayrakları kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-764">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the event flags are available.</span></span>

    <span data-ttu-id="ff79b-765">Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, olay bayrakları beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-765">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the event flags.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-766">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-766">Return Values</span></span>

- <span data-ttu-id="ff79b-767">**TX_SUCCESS**: (0x00) başarılı olay bayrakları al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-767">**TX_SUCCESS**: (0x00) Successful event flags get.</span></span>
- <span data-ttu-id="ff79b-768">**TX_DELETED**: (0x01) olay bayrakları grubu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-768">**TX_DELETED**: (0x01) Event flags group was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-769">**TX_NO_EVENTS**: (0x07) hizmet, belirtilen olayları beklemek için belirtilen süre içinde alamadı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-769">**TX_NO_EVENTS**: (0x07) Service was unable to get the specified events within the specified time to wait.</span></span>
- <span data-ttu-id="ff79b-770">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-770">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-771">TX_GROUP_ERROR: (0x06) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-771">TX_GROUP_ERROR: (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="ff79b-772">TX_PTR_ERROR: (0x03) gerçek olay bayrakları için geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-772">TX_PTR_ERROR: (0x03) Invalid pointer for actual event flags.</span></span>
- <span data-ttu-id="ff79b-773">TX_WAIT_ERROR: (0x04) iş parçacığından oluşan çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-773">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="ff79b-774">TX_OPTION_ERROR: (0x08) geçersiz Get-OPTION belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-774">TX_OPTION_ERROR: (0x08) Invalid get-option was specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-775">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-775">Allowed From</span></span>

<span data-ttu-id="ff79b-776">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-776">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-777">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-777">Preemption Possible</span></span>

<span data-ttu-id="ff79b-778">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-778">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-779">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-779">Example</span></span>

```C
TX_EVENT_FLAGS_GROUP my_event_flags_group;
ULONG         actual_events;
UINT          status;

/* Request that event flags 0, 4, and 8 are all set. Also,
   if they are set they should be cleared. If the event
   flags are not set, this service suspends for a maximum of
   20 timer-ticks. */
status = tx_event_flags_get(&my_event_flags_group, 0x111,
                      TX_AND_CLEAR, &actual_events, 20);

/* If status equals TX_SUCCESS, actual_events contains the
   actual events obtained. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-780">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-780">See Also</span></span>

- <span data-ttu-id="ff79b-781">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-781">tx_event_flags_create</span></span>
- <span data-ttu-id="ff79b-782">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-782">tx_event_flags_delete</span></span>
- <span data-ttu-id="ff79b-783">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-783">tx_event_flags_info_get</span></span>
- <span data-ttu-id="ff79b-784">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-784">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="ff79b-785">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-785">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-786">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-786">tx_event_flags_set</span></span>
- <span data-ttu-id="ff79b-787">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-787">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_info_get"></a><span data-ttu-id="ff79b-788">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-788">tx_event_flags_info_get</span></span>

<span data-ttu-id="ff79b-789">Olay bayrakları grubu hakkında bilgi al</span><span class="sxs-lookup"><span data-stu-id="ff79b-789">Retrieve information about event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-790">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-790">Prototype</span></span>

```C
UINT tx_event_flags_info_get(TX_EVENT_FLAGS_GROUP *group_ptr,
                         CHAR **name, ULONG *current_flags,
                         TX_THREAD **first_suspended,
                         ULONG *suspended_count,
                         TX_EVENT_FLAGS_GROUP **next_group);
```
### <a name="description"></a><span data-ttu-id="ff79b-791">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-791">Description</span></span>

<span data-ttu-id="ff79b-792">Bu hizmet, belirtilen olay bayrakları grubu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-792">This service retrieves information about the specified event flags group.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-793">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-793">Parameters</span></span>

- <span data-ttu-id="ff79b-794">**group_ptr**: bir olay bayrakları Grup denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-794">**group_ptr**: Pointer to an event flags group control block.</span></span>
- <span data-ttu-id="ff79b-795">**Name**: olay bayrakları grubunun adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-795">**name**: Pointer to destination for the pointer to the event flags group’s name.</span></span>
- <span data-ttu-id="ff79b-796">**current_flags**: olay bayrakları grubundaki geçerli küme bayrakları için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-796">**current_flags**: Pointer to destination for the current set flags in the event flags group.</span></span>
- <span data-ttu-id="ff79b-797">**first_suspended**: Bu olay bayrakları grubunun askıya alınma listesindeki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-797">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this event flags group.</span></span>
- <span data-ttu-id="ff79b-798">**suspended_count**: Bu olay bayrakları grubunda askıya alınmış olan iş parçacıklarının sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-798">**suspended_count**: Pointer to destination for the number of threads currently suspended on this event flags group.</span></span>
- <span data-ttu-id="ff79b-799">**next_group**: sonraki oluşturulan olay bayrakları grubunun işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-799">**next_group**: Pointer to destination for the pointer of the next created event flags group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-800">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-800">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-801">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-801">Return Values</span></span>

- <span data-ttu-id="ff79b-802">**TX_SUCCESS**: (0x00) başarılı olay grubu bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-802">**TX_SUCCESS**: (0x00) Successful event group information retrieval.</span></span>
- <span data-ttu-id="ff79b-803">TX_GROUP_ERROR: (0x06) geçersiz olay grubu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-803">TX_GROUP_ERROR: (0x06) Invalid event group pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-804">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-804">Allowed From</span></span>

<span data-ttu-id="ff79b-805">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-805">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-806">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-806">Preemption Possible</span></span>

<span data-ttu-id="ff79b-807">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-807">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-808">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-808">Example</span></span>

```c
TX_EVENT_FLAGS_GROUPmy_event_group;
CHAR          *name;
ULONG         current_flags;
TX_THREAD     *first_suspended;
ULONG         suspended_count;
TX_EVENT_FLAGS_GROUP*next_group;
UINT          status;

/* Retrieve information about the previously created
   event flags group "my_event_group." */
status =  tx_event_flags_info_get(&my_event_group, &name,
             &current_flags,
             &first_suspended, &suspended_count,
             &next_group);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-809">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-809">See Also</span></span>

- <span data-ttu-id="ff79b-810">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-810">tx_event_flags_create</span></span>
- <span data-ttu-id="ff79b-811">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-811">tx_event_flags_delete</span></span>
- <span data-ttu-id="ff79b-812">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-812">tx_event_flags_get</span></span>
- <span data-ttu-id="ff79b-813">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-813">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="ff79b-814">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-814">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-815">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-815">tx_event_flags_set</span></span>
- <span data-ttu-id="ff79b-816">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-816">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_performance-info_get"></a><span data-ttu-id="ff79b-817">tx_event_flags_performance info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-817">tx_event_flags_performance info_get</span></span>

<span data-ttu-id="ff79b-818">Olay bayrakları grubu performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-818">Get event flags group performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-819">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-819">Prototype</span></span>

```C
UINT tx_event_flags_performance_info_get(TX_EVENT_FLAGS_GROUP
                        *group_ptr, ULONG *sets, ULONG *gets,
                        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-820">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-820">Description</span></span>

<span data-ttu-id="ff79b-821">Bu hizmet, belirtilen olay bayrakları grubuyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-821">This service retrieves performance information about the specified event flags group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-822">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek için bu hizmetin tanımlanmış **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-822">ThreadX SMP library and application must be built with **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-823">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-823">Parameters</span></span>

- <span data-ttu-id="ff79b-824">**group_ptr**: daha önce oluşturulan olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-824">**group_ptr**: Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="ff79b-825">**Ayarlar**: Bu grupta gerçekleştirilen olay bayrak kümesi isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-825">**sets**: Pointer to destination for the number of event flags set requests performed on this group.</span></span>
- <span data-ttu-id="ff79b-826">**alır**: Bu grupta gerçekleştirilen olay bayrakları Al istekleri sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-826">**gets**: Pointer to destination for the number of event flags get requests performed on this group.</span></span>
- <span data-ttu-id="ff79b-827">**getirilmesi**: Bu grupta getirilmesi al iş parçacığı olay bayrakları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-827">**suspensions**: Pointer to destination for the number of thread event flags get suspensions on this group.</span></span>
- <span data-ttu-id="ff79b-828">**zaman aşımları**: olay bayraklarının sayısı için hedefin işaretçisi bu gruptaki askıya alma zaman aşımlarını al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-828">**timeouts**: Pointer to destination for the number of event flags get suspension timeouts on this group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-829">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-829">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-830">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-830">Return Values</span></span>

- <span data-ttu-id="ff79b-831">**TX_SUCCESS**: (0x00) başarılı olay bayrakları grup performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-831">**TX_SUCCESS**: (0x00) Successful event flags group performance get.</span></span>
- <span data-ttu-id="ff79b-832">**TX_PTR_ERROR**: (0x03) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-832">**TX_PTR_ERROR**: (0x03) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="ff79b-833">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-833">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-834">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-834">Allowed From</span></span>

<span data-ttu-id="ff79b-835">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-835">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-836">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-836">Example</span></span>

```C
TX_EVENT_FLAGS_GROUPmy_event_flag_group;
ULONG           sets;
ULONG           gets;
ULONG           suspensions;
ULONG           timeouts;

/* Retrieve performance information on the previously created event
   flag group. */
status =  tx_event_flags_performance_info_get(&my_event_flag_group,
   &sets, &gets, &suspensions,
   &timeouts);

/* If status is TX_SUCCESS the performance information was successfully
   retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-837">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-837">See Also</span></span>

- <span data-ttu-id="ff79b-838">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-838">tx_event_flags_create</span></span>
- <span data-ttu-id="ff79b-839">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-839">tx_event_flags_delete</span></span>
- <span data-ttu-id="ff79b-840">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-840">tx_event_flags_get</span></span>
- <span data-ttu-id="ff79b-841">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-841">tx_event_flags_info_get</span></span>
- <span data-ttu-id="ff79b-842">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-842">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-843">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-843">tx_event_flags_set</span></span>
- <span data-ttu-id="ff79b-844">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-844">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_performance_system_info_get"></a><span data-ttu-id="ff79b-845">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-845">tx_event_flags_performance_system_info_get</span></span>

<span data-ttu-id="ff79b-846">Performans sistemi bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-846">Retrieve performance system information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-847">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-847">Prototype</span></span>

```c
UINT  tx_event_flags_performance_system_info_get(ULONG *sets,
        ULONG *gets,ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-848">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-848">Description</span></span>

<span data-ttu-id="ff79b-849">Bu hizmet sistemdeki tüm olay bayrakları gruplarıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-849">This service retrieves performance information about all event flags groups in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-850">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek için bu hizmetin tanımlanmış **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-850">ThreadX SMP library and application must be built with **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-851">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-851">Parameters</span></span>

- <span data-ttu-id="ff79b-852">**Ayarlar**: tüm gruplarda gerçekleştirilen olay bayrakları kümesi isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-852">**sets**: Pointer to destination for the total number of event flags set requests performed on all groups.</span></span>
- <span data-ttu-id="ff79b-853">**alır**: tüm gruplarda gerçekleştirilen olay bayrakları al isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-853">**gets**: Pointer to destination for the total number of event flags get requests performed on all groups.</span></span>
- <span data-ttu-id="ff79b-854">**getirilmesi**: tüm gruplar üzerinde getirilmesi al iş parçacığı olay bayraklarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-854">**suspensions**: Pointer to destination for the total number of thread event flags get suspensions on all groups.</span></span>
- <span data-ttu-id="ff79b-855">**zaman aşımları**: olay bayraklarının toplam sayısı için hedefin işaretçisi tüm gruplardaki askıya alınma zaman aşımlarını alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-855">**timeouts**: Pointer to destination for the total number of event flags get suspension timeouts on all groups.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-856">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-856">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-857">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-857">Return Values</span></span>

- <span data-ttu-id="ff79b-858">**TX_SUCCESS**: (0x00) başarılı olay bayrakları sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-858">**TX_SUCCESS**: (0x00) Successful event flags system performance get.</span></span>
- <span data-ttu-id="ff79b-859">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-859">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-860">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-860">Allowed From</span></span>

<span data-ttu-id="ff79b-861">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-861">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-862">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-862">Example</span></span>

```c
ULONG         sets;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all previously created event
   flag groups. */
status = tx_event_flags_performance_system_info_get(&sets, &gets,
                &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-863">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-863">See Also</span></span>

- <span data-ttu-id="ff79b-864">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-864">tx_event_flags_create</span></span>
- <span data-ttu-id="ff79b-865">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-865">tx_event_flags_delete</span></span>
- <span data-ttu-id="ff79b-866">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-866">tx_event_flags_get</span></span>
- <span data-ttu-id="ff79b-867">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-867">tx_event_flags_info_get</span></span>
- <span data-ttu-id="ff79b-868">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-868">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="ff79b-869">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-869">tx_event_flags_set</span></span>
- <span data-ttu-id="ff79b-870">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-870">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set"></a><span data-ttu-id="ff79b-871">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-871">tx_event_flags_set</span></span>

<span data-ttu-id="ff79b-872">Olay bayrakları grubundaki olay bayraklarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="ff79b-872">Set event flags in an event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-873">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-873">Prototype</span></span>

```C
UINT tx_event_flags_set(TX_EVENT_FLAGS_GROUP *group_ptr,
                          ULONG  flags_to_set,UINT set_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-874">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-874">Description</span></span>

<span data-ttu-id="ff79b-875">Bu hizmet, belirtilen set-Option öğesine bağlı olarak bir olay bayrakları grubundaki olay bayraklarını ayarlar veya temizler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-875">This service sets or clears event flags in an event flags group, depending upon the specified set-option.</span></span> <span data-ttu-id="ff79b-876">Olay bayrakları isteği artık karşılanan tüm askıya alınmış iş parçacıkları devam ettirildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-876">All suspended threads whose event flags request is now satisfied are resumed.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-877">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-877">Parameters</span></span>

- <span data-ttu-id="ff79b-878">**group_ptr**: önceden oluşturulan olay bayrakları Grup denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-878">**group_ptr**: Pointer to the previously created event flags group control block.</span></span>
- <span data-ttu-id="ff79b-879">**flags_to_set**: seçili küme seçeneğine göre ayarlanacak veya temizlenecek olay bayraklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-879">**flags_to_set**: Specifies the event flags to set or clear based upon the set option selected.</span></span>
- <span data-ttu-id="ff79b-880">**set_option**: belirtilen olay bayraklarının, grubun geçerli olay bayraklarına mi yoksa ORed mi olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-880">**set_option**: Specifies whether the event flags specified are ANDed or ORed into the current event flags of the group.</span></span> <span data-ttu-id="ff79b-881">Aşağıdakiler geçerli seçimlerdir:</span><span class="sxs-lookup"><span data-stu-id="ff79b-881">The following are valid selections:</span></span>
    - <span data-ttu-id="ff79b-882">**TX_AND**: (0x02)</span><span class="sxs-lookup"><span data-stu-id="ff79b-882">**TX_AND**: (0x02)</span></span>
    - <span data-ttu-id="ff79b-883">**TX_OR**: (0x00) TX_AND seçilmesi, belirtilen olay bayraklarının gruptaki geçerli olay bayraklarına olduğunu **ve** bulunduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-883">**TX_OR**: (0x00) Selecting TX_AND specifies that the specified event flags are **AND** ed into the current event flags in the group.</span></span> <span data-ttu-id="ff79b-884">Bu seçenek, genellikle bir gruptaki olay bayraklarını temizlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-884">This option is often used to clear event flags in a group.</span></span> <span data-ttu-id="ff79b-885">Aksi takdirde, TX_OR belirtilirse, belirtilen olay bayrakları gruptaki geçerli olayla **birlikte olur.**</span><span class="sxs-lookup"><span data-stu-id="ff79b-885">Otherwise, if TX_OR is specified, the specified event flags are **OR** ed with the current event in the group.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-886">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-886">Return Values</span></span>

- <span data-ttu-id="ff79b-887">**TX_SUCCESS**: (0x00) başarılı olay bayrakları kümesi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-887">**TX_SUCCESS**: (0x00) Successful event flags set.</span></span>
- <span data-ttu-id="ff79b-888">TX_GROUP_ERROR: (0x06) olay bayrakları grubuna yönelik geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-888">TX_GROUP_ERROR: (0x06) Invalid pointer to event flags group.</span></span>
- <span data-ttu-id="ff79b-889">TX_OPTION_ERROR: (0x08) geçersiz set-OPTION belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-889">TX_OPTION_ERROR: (0x08) Invalid set-option specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-890">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-890">Allowed From</span></span>

<span data-ttu-id="ff79b-891">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-891">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-892">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-892">Preemption Possible</span></span>

<span data-ttu-id="ff79b-893">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-893">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-894">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-894">Example</span></span>

```C
TX_EVENT_FLAGS_GROUPmy_event_flags_group;
UINT         status;

/* Set event flags 0, 4, and 8. */
status =  tx_event_flags_set(&my_event_flags_group,
                           0x111, TX_OR);

/* If status equals TX_SUCCESS, the event flags have been
   set and any suspended thread whose request was satisfied
   has been resumed. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-895">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-895">See Also</span></span>

- <span data-ttu-id="ff79b-896">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-896">tx_event_flags_create</span></span>
- <span data-ttu-id="ff79b-897">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-897">tx_event_flags_delete</span></span>
- <span data-ttu-id="ff79b-898">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-898">tx_event_flags_get</span></span>
- <span data-ttu-id="ff79b-899">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-899">tx_event_flags_info_get</span></span>
- <span data-ttu-id="ff79b-900">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-900">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="ff79b-901">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-901">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-902">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-902">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set_notify"></a><span data-ttu-id="ff79b-903">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-903">tx_event_flags_set_notify</span></span>

<span data-ttu-id="ff79b-904">Olay bayrakları ayarlandığında uygulamaya bildir</span><span class="sxs-lookup"><span data-stu-id="ff79b-904">Notify application when event flags are set</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-905">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-905">Prototype</span></span>

```C
UINT tx_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr,
       VOID (*events_set_notify)(TX_EVENT_FLAGS_GROUP *));
```
### <a name="description"></a><span data-ttu-id="ff79b-906">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-906">Description</span></span>

<span data-ttu-id="ff79b-907">Bu hizmet, belirtilen olay bayrakları grubunda bir veya daha fazla olay bayrağı ayarlandığında çağrılan bir bildirim geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-907">This service registers a notification callback function that is called whenever one or more event flags are set in the specified event flags group.</span></span> <span data-ttu-id="ff79b-908">Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-908">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ff79b-909">Uygulamanın olay bayrakları kümesi bildirim geri çağrısının, askıya alma seçeneğiyle herhangi bir ThreadX SMP API çağrısı yapmasına izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ff79b-909">The application’s event flags set notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-910">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-910">Parameters</span></span> 
- <span data-ttu-id="ff79b-911">**group_ptr**: daha önce oluşturulan olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-911">**group_ptr**: Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="ff79b-912">**events_set_notify**: uygulamanın olay bayrakları kümesi bildirim işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-912">**events_set_notify**: Pointer to application’s event flags set notification function.</span></span> <span data-ttu-id="ff79b-913">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-913">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-914">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-914">Return Values</span></span>

- <span data-ttu-id="ff79b-915">**TX_SUCCESS**: (0x00) olay bayrakları ayarlama bildiriminin başarılı kaydı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-915">**TX_SUCCESS**: (0x00) Successful registration of event flags set notification.</span></span>
- <span data-ttu-id="ff79b-916">TX_GROUP_ERROR: (0x06) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-916">TX_GROUP_ERROR: (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="ff79b-917">TX_FEATURE_NOT_ENABLED: (0xFF) sistem, bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-917">TX_FEATURE_NOT_ENABLED: (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-918">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-918">Allowed From</span></span>

<span data-ttu-id="ff79b-919">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-919">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-920">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-920">Example</span></span>

```C
TX_EVENT_FLAGS_GROUPmy_group;

/* Register the "my_event_flags_set_notify" function for monitoring
   event flags set in the event flags group "my_group." */
status =  tx_event_flags_set_notify(&my_group,
                my_event_flags_set_notify);

/* If status is TX_SUCCESS the event flags set notification function
   was successfully registered. */

void my_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr)
   /* One or more event flags was set in this group! */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-921">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-921">See Also</span></span>

- <span data-ttu-id="ff79b-922">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-922">tx_event_flags_create</span></span>
- <span data-ttu-id="ff79b-923">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-923">tx_event_flags_delete</span></span>
- <span data-ttu-id="ff79b-924">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-924">tx_event_flags_get</span></span>
- <span data-ttu-id="ff79b-925">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-925">tx_event_flags_info_get</span></span>
- <span data-ttu-id="ff79b-926">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-926">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="ff79b-927">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-927">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-928">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-928">tx_event_flags_set</span></span>

## <a name="tx_interrupt_control"></a><span data-ttu-id="ff79b-929">tx_interrupt_control</span><span class="sxs-lookup"><span data-stu-id="ff79b-929">tx_interrupt_control</span></span>

<span data-ttu-id="ff79b-930">Kesmeleri etkinleştirme ve devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="ff79b-930">Enable and disable interrupts</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-931">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-931">Prototype</span></span>

```C
UINT tx_interrupt_control(UINT new_posture);
```
### <a name="description"></a><span data-ttu-id="ff79b-932">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-932">Description</span></span>

<span data-ttu-id="ff79b-933">Bu hizmet, **new_posture** giriş parametresi tarafından belirtilen kesintileri etkinleştirilir veya devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-933">This service enables or disables interrupts as specified by the input parameter **new_posture**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-934">Bu hizmet bir uygulama iş parçacığından çağrılırsa, kesme sonrası bu iş parçacığı bağlamının bir parçası olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-934">If this service is called from an application thread, the interrupt posture remains part of that thread’s context.</span></span> <span data-ttu-id="ff79b-935">Örneğin, iş parçacığı kesintileri devre dışı bırakmak ve sonra askıya almak için bu yordamı çağırırsa, kesintiler yeniden devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-935">For example, if the thread calls this routine to disable interrupts and then suspends, when it is resumed, interrupts are disabled again.</span></span>

> [!WARNING]
> <span data-ttu-id="ff79b-936">Bu hizmet, başlatma sırasında kesmeleri etkinleştirmek için kullanılmamalıdır!</span><span class="sxs-lookup"><span data-stu-id="ff79b-936">This service should not be used to enable interrupts during initialization!</span></span> <span data-ttu-id="ff79b-937">Bunun yapılması öngörülemeyen sonuçlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-937">Doing so could cause unpredictable results.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-938">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-938">Parameters</span></span>

- <span data-ttu-id="ff79b-939">**new_posture**: Bu parametre, kesmelerin devre dışı veya etkin olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-939">**new_posture**: This parameter specifies whether interrupts are disabled or enabled.</span></span> <span data-ttu-id="ff79b-940">Yasal değerler **TX_INT_DISABLE ve TX_INT_ENABLE içerir.**</span><span class="sxs-lookup"><span data-stu-id="ff79b-940">Legal values include **TX_INT_DISABLE and TX_INT_ENABLE.**</span></span> <span data-ttu-id="ff79b-941">Bu parametrelerin gerçek değerleri bağlantı noktasına özeldir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-941">The actual values for these parameters are port specific.</span></span> <span data-ttu-id="ff79b-942">Bunlara ek olarak, bazı işleme mimarileri ek kesme devre dışı bırakmayı destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-942">In addition, some processing architectures might support additional interrupt disable postures.</span></span> <span data-ttu-id="ff79b-943">Daha fazla ayrıntı için lütfen dağıtım diskinde sağlanan **_readme_threadx.txt_** bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="ff79b-943">Please see the **_readme_threadx.txt_** information supplied on the distribution disk for more details.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-944">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-944">Return Values</span></span>

- <span data-ttu-id="ff79b-945">önceki duruşunu: Bu hizmet, çağrıyı yapana önceki kesme sonrası geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-945">previous posture: This service returns the previous interrupt posture to the caller.</span></span> <span data-ttu-id="ff79b-946">Bu, hizmet kullanıcılarının kesintiler devre dışı bırakıldıktan sonra önceki duruşunu geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-946">This allows users of the service to restore the previous posture after interrupts are disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-947">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-947">Allowed From</span></span>

<span data-ttu-id="ff79b-948">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-948">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-949">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-949">Preemption Possible</span></span>

<span data-ttu-id="ff79b-950">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-950">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-951">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-951">Example</span></span>

```C
UINT my_old_posture;

/* Lockout interrupts */
my_old_posture =  tx_interrupt_control(TX_INT_DISABLE);

/* Perform critical operations that need interrupts
   locked-out.... */

/* Restore previous interrupt lockout posture. */
tx_interrupt_control(my_old_posture);
```
### <a name="see-also"></a><span data-ttu-id="ff79b-952">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-952">See Also</span></span>

<span data-ttu-id="ff79b-953">Yok</span><span class="sxs-lookup"><span data-stu-id="ff79b-953">None</span></span>

## <a name="tx_mutex_create"></a><span data-ttu-id="ff79b-954">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-954">tx_mutex_create</span></span>

<span data-ttu-id="ff79b-955">Karşılıklı dışlama mutex oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-955">Create mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-956">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-956">Prototype</span></span>

```C
UINT tx_mutex_create(TX_MUTEX *mutex_ptr,
                          CHAR *name_ptr, UINT priority_inherit);
```
### <a name="description"></a><span data-ttu-id="ff79b-957">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-957">Description</span></span>
    
<span data-ttu-id="ff79b-958">Bu hizmet, kaynak koruması için iş parçacıkları arası karşılıklı dışlama için bir mutex oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-958">This service creates a mutex for inter-thread mutual exclusion for resource protection.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-959">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-959">Parameters</span></span>

- <span data-ttu-id="ff79b-960">**mutex_ptr**: Mutex denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-960">**mutex_ptr**: Pointer to a mutex control block.</span></span>
- <span data-ttu-id="ff79b-961">**name_ptr**: mutex adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-961">**name_ptr**: Pointer to the name of the mutex.</span></span>
- <span data-ttu-id="ff79b-962">**priority_inherit**: bu mutex 'in öncelik devralmayı destekleyip desteklemediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-962">**priority_inherit**: Specifies whether or not this mutex supports priority inheritance.</span></span> <span data-ttu-id="ff79b-963">Bu değer TX_INHERIT, öncelikli devralma desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-963">If this value is TX_INHERIT, then priority inheritance is supported.</span></span> <span data-ttu-id="ff79b-964">Ancak TX_NO_INHERIT belirtilirse, bu mutex tarafından öncelik devralımı desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="ff79b-964">However, if TX_NO_INHERIT is specified, priority inheritance is not supported by this mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-965">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-965">Return Values</span></span>

- <span data-ttu-id="ff79b-966">**TX_SUCCESS**: (0x00) başarılı mutex oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-966">**TX_SUCCESS**: (0x00) Successful mutex creation.</span></span>
- <span data-ttu-id="ff79b-967">TX_MUTEX_ERROR: (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-967">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span> <span data-ttu-id="ff79b-968">İşaretçi NULL ya da mutex zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-968">Either the pointer is NULL or the mutex is already created.</span></span>
- <span data-ttu-id="ff79b-969">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-969">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>
- <span data-ttu-id="ff79b-970">TX_INHERIT_ERROR: (0x1F) geçersiz öncelik devralma parametresi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-970">TX_INHERIT_ERROR: (0x1F) Invalid priority inherit parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-971">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-971">Allowed From</span></span>

<span data-ttu-id="ff79b-972">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-972">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-973">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-973">Preemption Possible</span></span>

<span data-ttu-id="ff79b-974">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-974">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-975">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-975">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Create a mutex to provide protection over a
   common resource. */
status =  tx_mutex_create(&my_mutex,"my_mutex_name",
                           TX_NO_INHERIT);

/* If status equals TX_SUCCESS, my_mutex is ready for
   use. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-976">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-976">See Also</span></span>

- <span data-ttu-id="ff79b-977">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-977">tx_mutex_delete</span></span>
- <span data-ttu-id="ff79b-978">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-978">tx_mutex_get</span></span>
- <span data-ttu-id="ff79b-979">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-979">tx_mutex_info_get</span></span>
- <span data-ttu-id="ff79b-980">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-980">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="ff79b-981">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-981">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-982">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-982">tx_mutex_prioritize</span></span>
- <span data-ttu-id="ff79b-983">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-983">tx_mutex_put</span></span>

## <a name="tx_mutex_delete"></a><span data-ttu-id="ff79b-984">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-984">tx_mutex_delete</span></span>

<span data-ttu-id="ff79b-985">Karşılıklı dışlama mutex 'i Sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-985">Delete mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-986">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-986">Prototype</span></span>

```C
UINT tx_mutex_delete(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-987">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-987">Description</span></span>

<span data-ttu-id="ff79b-988">Bu hizmet, belirtilen mutex 'i siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-988">This service deletes the specified mutex.</span></span> <span data-ttu-id="ff79b-989">Mutex bekleniyor olan tüm iş parçacıkları sürdürülür ve TX_DELETED dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-989">All threads suspended waiting for the mutex are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-990">Silinen bir mutex 'in kullanımını önleyen uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-990">It is the application’s responsibility to prevent use of a deleted mutex.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-991">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-991">Parameters</span></span>

- <span data-ttu-id="ff79b-992">**mutex_ptr**: daha önce oluşturulmuş bir mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-992">**mutex_ptr**: Pointer to a previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-993">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-993">Return Values</span></span>

- <span data-ttu-id="ff79b-994">**TX_SUCCESS**: (0x00) başarılı mutex silme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-994">**TX_SUCCESS**: (0x00) Successful mutex deletion.</span></span>
- <span data-ttu-id="ff79b-995">TX_MUTEX_ERROR: (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-995">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="ff79b-996">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-996">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-997">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-997">Allowed From</span></span>

<span data-ttu-id="ff79b-998">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-998">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-999">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-999">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1000">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1000">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1001">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1001">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Delete a mutex. Assume that the mutex
   has already been created. */
status =  tx_mutex_delete(&my_mutex);

/* If status equals TX_SUCCESS, the mutex is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1002">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1002">See Also</span></span>

- <span data-ttu-id="ff79b-1003">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1003">tx_mutex_create</span></span>
- <span data-ttu-id="ff79b-1004">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1004">tx_mutex_get</span></span>
- <span data-ttu-id="ff79b-1005">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1005">tx_mutex_info_get</span></span>
- <span data-ttu-id="ff79b-1006">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1006">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1007">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1007">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1008">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1008">tx_mutex_prioritize</span></span>
- <span data-ttu-id="ff79b-1009">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1009">tx_mutex_put</span></span>

## <a name="tx_mutex_get"></a><span data-ttu-id="ff79b-1010">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1010">tx_mutex_get</span></span>

<span data-ttu-id="ff79b-1011">Mutex sahipliğini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1011">Obtain ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1012">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1012">Prototype</span></span>

```C
UINT tx_mutex_get(TX_MUTEX *mutex_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-1013">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1013">Description</span></span>

<span data-ttu-id="ff79b-1014">Bu hizmet, belirtilen mutex 'in özel sahipliğini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1014">This service attempts to obtain exclusive ownership of the specified mutex.</span></span> <span data-ttu-id="ff79b-1015">Çağıran iş parçacığı zaten mutex 'e sahipse, bir iç sayaç artırılır ve başarılı bir durum döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1015">If the calling thread already owns the mutex, an internal counter is incremented and a successful status is returned.</span></span>

<span data-ttu-id="ff79b-1016">Mutex, başka bir iş parçacığına aitse ve bu iş parçacığı daha yüksek önceliktir ve öncelikli devralma, karşılıklı dışlama oluşturma sırasında belirtilmişse, daha düşük öncelikli iş parçacığının önceliği geçici olarak çağıran iş parçacığından çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1016">If the mutex is owned by another thread and this thread is higher priority and priority inheritance was specified at mutex create, the lower priority thread’s priority will be temporarily raised to that of the calling thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1017">Prioritykalýtým ile bir mutex sahibi olan düşük öncelikli iş parçacığının önceliği, zaman uyumu sahipliği sırasında asla bir dış iş parçacığı tarafından değiştirilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1017">The priority of the lower priority thread owning a mutex with priorityinheritance should never be modified by an external thread during mutex ownership.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1018">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1018">Parameters</span></span>

- <span data-ttu-id="ff79b-1019">**mutex_ptr**: daha önce oluşturulmuş bir mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1019">**mutex_ptr**: Pointer to a previously created mutex.</span></span>
- <span data-ttu-id="ff79b-1020">**wait_option**: mutex 'in zaten başka bir iş parçacığına ait olması durumunda hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1020">**wait_option**: Defines how the service behaves if the mutex is already owned by another thread.</span></span> <span data-ttu-id="ff79b-1021">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-1021">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-1022">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1022">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="ff79b-1023">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1023">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="ff79b-1024">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1024">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="ff79b-1025">TX_NO_WAIT seçilmesi, başarılı olup olmamasından bağımsız olarak bu hizmetten anında geri dönerek sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1025">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="ff79b-1026">*Bu, hizmet başlatma işleminden çağrıldığında geçerli tek seçenektir.*</span><span class="sxs-lookup"><span data-stu-id="ff79b-1026">*This is the only valid option if the service is called from Initialization.*</span></span>

    <span data-ttu-id="ff79b-1027">TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının mutex kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1027">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the mutex is available.</span></span>

    <span data-ttu-id="ff79b-1028">Sayısal değer (1-0xFFFFFFFE) seçildiğinde, mutex için beklerken askıya alınması için en fazla Zamanlayıcı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1028">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1029">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1029">Return Values</span></span>

- <span data-ttu-id="ff79b-1030">**TX_SUCCESS**: (0x00) başarılı mutex al işlemi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1030">**TX_SUCCESS**: (0x00) Successful mutex get operation.</span></span>
- <span data-ttu-id="ff79b-1031">**TX_DELETED**: (0x01) mutex, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1031">**TX_DELETED**: (0x01) Mutex was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-1032">**TX_NOT_AVAILABLE**: (0x1d) hizmeti, mutex 'in sahipliğini, belirtilen süre içinde beklemek için alamadı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1032">**TX_NOT_AVAILABLE**: (0x1D) Service was unable to get ownership of the mutex within the specified time to wait.</span></span>
- <span data-ttu-id="ff79b-1033">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1033">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-1034">TX_MUTEX_ERROR: (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1034">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="ff79b-1035">TX_WAIT_ERROR: (0x04) iş parçacığından oluşan çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1035">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="ff79b-1036">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1036">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1037">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1037">Allowed From</span></span>

<span data-ttu-id="ff79b-1038">Başlatma ve iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-1038">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1039">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1039">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1040">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1040">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1041">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1041">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Obtain exclusive ownership of the mutex "my_mutex".
   If the mutex "my_mutex" is not available, suspend until it
   becomes available. */
status =  tx_mutex_get(&my_mutex, TX_WAIT_FOREVER);
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1042">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1042">See Also</span></span>

- <span data-ttu-id="ff79b-1043">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1043">tx_mutex_create</span></span>
- <span data-ttu-id="ff79b-1044">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1044">tx_mutex_delete</span></span>
- <span data-ttu-id="ff79b-1045">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1045">tx_mutex_info_get</span></span>
- <span data-ttu-id="ff79b-1046">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1046">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1047">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1047">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1048">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1048">tx_mutex_prioritize</span></span>
- <span data-ttu-id="ff79b-1049">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1049">tx_mutex_put</span></span>

## <a name="tx_mutex_info_get"></a><span data-ttu-id="ff79b-1050">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1050">tx_mutex_info_get</span></span>

<span data-ttu-id="ff79b-1051">Mutex hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="ff79b-1051">Retrieve information about mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1052">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1052">Prototype</span></span>

```C
UINT tx_mutex_info_get(TX_MUTEX *mutex_ptr, CHAR **name,
                          ULONG *count, TX_THREAD **owner,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count, TX_MUTEX **next_mutex);
```
### <a name="description"></a><span data-ttu-id="ff79b-1053">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1053">Description</span></span>

<span data-ttu-id="ff79b-1054">Bu hizmet, belirtilen mutex 'ten bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1054">This service retrieves information from the specified mutex.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1055">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1055">Parameters</span></span>

- <span data-ttu-id="ff79b-1056">**mutex_ptr**: Mutex denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1056">**mutex_ptr**: Pointer to mutex control block.</span></span>
- <span data-ttu-id="ff79b-1057">**ad**: zaman uyumu adının işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1057">**name**: Pointer to destination for the pointer to the mutex’s name.</span></span>
- <span data-ttu-id="ff79b-1058">**Count**: mutex 'in sahiplik sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1058">**count**: Pointer to destination for the ownership count of the mutex.</span></span>
- <span data-ttu-id="ff79b-1059">**sahip**: sahibi olan iş parçacığının işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1059">**owner**: Pointer to destination for the owning thread’s pointer.</span></span>
- <span data-ttu-id="ff79b-1060">**first_suspended**: bu mutex 'in askıya alınma listesindeki ilk iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1060">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this mutex.</span></span>
- <span data-ttu-id="ff79b-1061">**suspended_count**: bu mutex üzerinde şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1061">**suspended_count**: Pointer to destination for the number of threads currently suspended on this mutex.</span></span>
- <span data-ttu-id="ff79b-1062">**next_mutex**: sonraki oluşturulan mutex işaretçisinin işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1062">**next_mutex**: Pointer to destination for the pointer of the next created mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1063">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1063">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1064">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1064">Return Values</span></span>

- <span data-ttu-id="ff79b-1065">**TX_SUCCESS**: (0x00) başarılı mutex bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1065">**TX_SUCCESS**: (0x00) Successful mutex information retrieval.</span></span>
- <span data-ttu-id="ff79b-1066">TX_MUTEX_ERROR: (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1066">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1067">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1067">Allowed From</span></span>

<span data-ttu-id="ff79b-1068">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1068">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1069">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1069">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1070">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1070">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1071">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1071">Example</span></span>

```C
TX_MUTEX     my_mutex;
CHAR         *name;
ULONG        count;
TX_THREAD    *owner;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_MUTEX     *next_mutex;
UINT         status;

/* Retrieve information about the previously created
   mutex "my_mutex." */
status =  tx_mutex_info_get(&my_mutex, &name,
                          &count, &owner,
                          &first_suspended, &suspended_count,
                          &next_mutex);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1072">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1072">See Also</span></span>

- <span data-ttu-id="ff79b-1073">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1073">tx_mutex_create</span></span>
- <span data-ttu-id="ff79b-1074">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1074">tx_mutex_delete</span></span>
- <span data-ttu-id="ff79b-1075">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1075">tx_mutex_get</span></span>
- <span data-ttu-id="ff79b-1076">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1076">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1077">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1077">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1078">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1078">tx_mutex_prioritize</span></span>
- <span data-ttu-id="ff79b-1079">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1079">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_info_get"></a><span data-ttu-id="ff79b-1080">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1080">tx_mutex_performance_info_get</span></span>

<span data-ttu-id="ff79b-1081">Mutex performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1081">Get mutex performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1082">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1082">Prototype</span></span>

```C
UINT tx_mutex_performance_info_get(TX_MUTEX *mutex_ptr, ULONG *puts,
       ULONG *gets, ULONG *suspensions, ULONG *timeouts,
       ULONG *inversions, ULONG *inheritances);
```
### <a name="description"></a><span data-ttu-id="ff79b-1083">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1083">Description</span></span>

<span data-ttu-id="ff79b-1084">Bu hizmet, belirtilen mutex hakkında performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1084">This service retrieves performance information about the specified mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1085">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_MUTEX_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1085">The ThreadX SMP library and application must be built with **TX_MUTEX_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1086">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1086">Parameters</span></span>

- <span data-ttu-id="ff79b-1087">**mutex_ptr**: daha önce oluşturulmuş mutex için işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1087">**mutex_ptr**: Pointer to previously created mutex.</span></span>
- <span data-ttu-id="ff79b-1088">**koyar**: bu mutex üzerinde gerçekleştirilen put isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1088">**puts**: Pointer to destination for the number of put requests performed on this mutex.</span></span>
- <span data-ttu-id="ff79b-1089">**Al: Bu** mutex üzerinde gerçekleştirilen GET isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1089">**gets**: Pointer to destination for the number of get requests performed on this mutex.</span></span>
- <span data-ttu-id="ff79b-1090">**getirilmesi**: bu mutex üzerinde getirilmesi al iş parçacığı mutex 'i için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1090">**suspensions**: Pointer to destination for the number of thread mutex get suspensions on this mutex.</span></span>
- <span data-ttu-id="ff79b-1091">**zaman aşımları**: bu mutex 'teki mutex alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1091">**timeouts**: Pointer to destination for the number of mutex get suspension timeouts on this mutex.</span></span>
- <span data-ttu-id="ff79b-1092">**Inversions**: bu mutex 'teki iş parçacığı önceliği ınsürümlerin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1092">**inversions**: Pointer to destination for the number of thread priority inversions on this mutex.</span></span>
- <span data-ttu-id="ff79b-1093">**Inheritances**: bu mutex 'teki iş parçacığı önceliği devralma işlemleri sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1093">**inheritances**: Pointer to destination for the number of thread priority inheritance operations on this mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1094">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1094">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1095">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1095">Return Values</span></span>

- <span data-ttu-id="ff79b-1096">**TX_SUCCESS**: (0x00) başarılı mutex performansı Get.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1096">**TX_SUCCESS**: (0x00) Successful mutex performance get.</span></span> 
- <span data-ttu-id="ff79b-1097">**TX_PTR_ERROR**: (0x03) geçersiz mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1097">**TX_PTR_ERROR**: (0x03) Invalid mutex pointer.</span></span>
- <span data-ttu-id="ff79b-1098">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1098">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1099">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1099">Allowed From</span></span>

<span data-ttu-id="ff79b-1100">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1100">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1101">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1101">Example</span></span>

```C
TX_MUTEX     my_mutex;
ULONG        puts;
ULONG        gets;
ULONG        suspensions;
ULONG        timeouts;
ULONG        inversions;
ULONG        inheritances;

/* Retrieve performance information on the previously created
   mutex. */
status =  tx_mutex_performance_info_get(&my_mutex_ptr, &puts, &gets,
                &suspensions, &timeouts, &inversions,
                &inheritances);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1102">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1102">See Also</span></span>

- <span data-ttu-id="ff79b-1103">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1103">tx_mutex_create</span></span>
- <span data-ttu-id="ff79b-1104">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1104">tx_mutex_delete</span></span>
- <span data-ttu-id="ff79b-1105">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1105">tx_mutex_get</span></span>
- <span data-ttu-id="ff79b-1106">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1106">tx_mutex_info_get</span></span>
- <span data-ttu-id="ff79b-1107">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1107">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1108">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1108">tx_mutex_prioritize</span></span>
- <span data-ttu-id="ff79b-1109">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1109">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_system_info_get"></a><span data-ttu-id="ff79b-1110">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1110">tx_mutex_performance_system_info_get</span></span>

<span data-ttu-id="ff79b-1111">Mutex sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1111">Get mutex system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1112">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1112">Prototype</span></span>

```C
UINT  tx_mutex_performance_system_info_get(ULONG *puts, ULONG *gets,
        ULONG *suspensions, ULONG *timeouts,
        ULONG *inversions, ULONG *inheritances);
```
### <a name="description"></a><span data-ttu-id="ff79b-1113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1113">Description</span></span>

<span data-ttu-id="ff79b-1114">Bu hizmet, sistemdeki tüm zaman uyumu sağlayıcılar hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1114">This service retrieves performance information about all the mutexes in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1115">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_MUTEX_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1115">The ThreadX SMP library and application must be built with **TX_MUTEX_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1116">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1116">Parameters</span></span>

- <span data-ttu-id="ff79b-1117">**koyar**: tüm zaman uyumu sağlayıcılar üzerinde gerçekleştirilen put isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1117">**puts**: Pointer to destination for the total number of put requests performed on all mutexes.</span></span>
- <span data-ttu-id="ff79b-1118">**Al: tüm** zaman uyumu sağlayıcılar üzerinde gerçekleştirilen GET isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1118">**gets**: Pointer to destination for the total number of get requests performed on all mutexes.</span></span>
- <span data-ttu-id="ff79b-1119">**getirilmesi**: tüm zaman uyumu sağlayıcılar üzerinde getirilmesi al toplam iş parçacığı mutex 'i için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1119">**suspensions**: Pointer to destination for the total number of thread mutex get suspensions on all mutexes.</span></span>
- <span data-ttu-id="ff79b-1120">**zaman aşımları**: tüm mutex 'ler üzerinde askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1120">**timeouts**: Pointer to destination for the total number of mutex get suspension timeouts on all mutexes.</span></span>
- <span data-ttu-id="ff79b-1121">**Inversions**: tüm zaman uyumu sağlayıcılar üzerinde iş parçacığı önceliği Inversions 'ın toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1121">**inversions**: Pointer to destination for the total number of thread priority inversions on all mutexes.</span></span>
- <span data-ttu-id="ff79b-1122">**Inheritances**: tüm zaman uyumu sağlayıcılar üzerinde iş parçacığı önceliği devralma işlemlerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1122">**inheritances**: Pointer to destination for the total number of thread priority inheritance operations on all mutexes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1123">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1123">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1124">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1124">Return Values</span></span>

- <span data-ttu-id="ff79b-1125">**TX_SUCCESS**: (0x00) başarılı mutex sistem performansı Get.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1125">**TX_SUCCESS**: (0x00) Successful mutex system performance get.</span></span>
- <span data-ttu-id="ff79b-1126">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1126">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1127">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1127">Allowed From</span></span>

<span data-ttu-id="ff79b-1128">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1128">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1129">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1129">Example</span></span>

```C
ULONG         puts;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;
ULONG         inversions;
ULONG         inheritances;

/* Retrieve performance information on all previously created
   mutexes. */
status = tx_mutex_performance_system_info_get(&puts, &gets,
                &suspensions, &timeouts,
                &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1130">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1130">See Also</span></span>

- <span data-ttu-id="ff79b-1131">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1131">tx_mutex_create</span></span>
- <span data-ttu-id="ff79b-1132">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1132">tx_mutex_delete</span></span>
- <span data-ttu-id="ff79b-1133">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1133">tx_mutex_get</span></span>
- <span data-ttu-id="ff79b-1134">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1134">tx_mutex_info_get</span></span>
- <span data-ttu-id="ff79b-1135">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1135">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1136">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1136">tx_mutex_prioritize</span></span>
- <span data-ttu-id="ff79b-1137">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1137">tx_mutex_put</span></span>

## <a name="tx_mutex_prioritize"></a><span data-ttu-id="ff79b-1138">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1138">tx_mutex_prioritize</span></span>

<span data-ttu-id="ff79b-1139">Mutex askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="ff79b-1139">Prioritize mutex suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1140">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1140">Prototype</span></span>

```C
UINT tx_mutex_prioritize(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1141">Description</span></span>

<span data-ttu-id="ff79b-1142">Bu hizmet, askıya alma listesinin önünde mutex 'in sahipliği için askıya alınan en yüksek öncelik iş parçacığını koyar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1142">This service places the highest priority thread suspended for ownership of the mutex at the front of the suspension list.</span></span> <span data-ttu-id="ff79b-1143">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1143">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1144">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1144">Parameters</span></span> 

- <span data-ttu-id="ff79b-1145">**mutex_ptr**: daha önce oluşturulmuş olan mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1145">**mutex_ptr**: Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1146">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1146">Return Values</span></span>

- <span data-ttu-id="ff79b-1147">**TX_SUCCESS**: (0x00) başarılı mutex önceliği.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1147">**TX_SUCCESS**: (0x00) Successful mutex prioritize.</span></span>
- <span data-ttu-id="ff79b-1148">TX_MUTEX_ERROR: (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1148">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1149">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1149">Allowed From</span></span>

<span data-ttu-id="ff79b-1150">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1150">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1151">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1151">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1152">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1152">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1153">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1153">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Ensure that the highest priority thread will receive
   ownership of the mutex when it becomes available. */
status = tx_mutex_prioritize(&my_mutex);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_mutex_put call that releases ownership of the
   mutex will give ownership to this thread and wake it
   up. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1154">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1154">See Also</span></span>

- <span data-ttu-id="ff79b-1155">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1155">tx_mutex_create</span></span>
- <span data-ttu-id="ff79b-1156">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1156">tx_mutex_delete</span></span>
- <span data-ttu-id="ff79b-1157">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1157">tx_mutex_get</span></span>
- <span data-ttu-id="ff79b-1158">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1158">tx_mutex_info_get</span></span>
- <span data-ttu-id="ff79b-1159">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1159">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1160">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1160">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1161">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1161">tx_mutex_put</span></span>

## <a name="tx_mutex_put"></a><span data-ttu-id="ff79b-1162">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1162">tx_mutex_put</span></span>

<span data-ttu-id="ff79b-1163">Mutex 'in sahipliğini serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="ff79b-1163">Release ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1164">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1164">Prototype</span></span>

```C
UINT tx_mutex_put(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1165">Description</span></span>

<span data-ttu-id="ff79b-1166">Bu hizmet, belirtilen mutex 'in sahiplik sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1166">This service decrements the ownership count of the specified mutex.</span></span> <span data-ttu-id="ff79b-1167">Sahiplik sayısı sıfırsa, mutex kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1167">If the ownership count is zero, the mutex is made available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1168">Karşılıklı dışlama oluşturma sırasında öncelik devralma seçilmişse, serbest bırakma iş parçacığının önceliği, başlangıçta mutex 'in sahipliğini aldığında sahip olduğu önceliğe geri yüklenecektir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1168">If priority inheritance was selected during mutex creation, the priority of the releasing thread will be restored to the priority it had when it originally obtained ownership of the mutex.</span></span> <span data-ttu-id="ff79b-1169">Mutex 'in sahipliği sırasında, serbest bırakma iş parçacığında yapılan diğer tüm öncelik değişiklikleri geri alınabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1169">Any other priority changes made to the releasing thread during ownership of the mutex may be undone.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1170">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1170">Parameters</span></span>

- <span data-ttu-id="ff79b-1171">**mutex_ptr**: daha önce oluşturulmuş olan mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1171">**mutex_ptr**: Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1172">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1172">Return Values</span></span>

- <span data-ttu-id="ff79b-1173">**TX_SUCCESS**: (0x00) başarılı mutex sürümü.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1173">**TX_SUCCESS**: (0x00) Successful mutex release.</span></span>
- <span data-ttu-id="ff79b-1174">**TX_NOT_OWNED**: (0x1E) mutex, arayana ait değil.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1174">**TX_NOT_OWNED**: (0x1E) Mutex is not owned by caller.</span></span>
- <span data-ttu-id="ff79b-1175">TX_MUTEX_ERROR: (0x1C) MUTEX için geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1175">TX_MUTEX_ERROR: (0x1C) Invalid pointer to mutex.</span></span>
- <span data-ttu-id="ff79b-1176">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1176">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1177">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1177">Allowed From</span></span>

<span data-ttu-id="ff79b-1178">Başlatma ve iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-1178">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1179">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1179">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1180">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1180">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1181">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1181">Example</span></span>

```C
TX_MUTEX         my_mutex;
UINT             status;
/* Release ownership of "my_mutex." */
status =  tx_mutex_put(&my_mutex);

/* If status equals TX_SUCCESS, the mutex ownership
   count has been decremented and if zero, released. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1182">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1182">See Also</span></span>

- <span data-ttu-id="ff79b-1183">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1183">tx_mutex_create</span></span>
- <span data-ttu-id="ff79b-1184">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1184">tx_mutex_delete</span></span>
- <span data-ttu-id="ff79b-1185">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1185">tx_mutex_get</span></span>
- <span data-ttu-id="ff79b-1186">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1186">tx_mutex_info_get</span></span>
- <span data-ttu-id="ff79b-1187">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1187">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1188">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1188">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1189">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1189">tx_mutex_prioritize</span></span>

## <a name="tx_queue_create"></a><span data-ttu-id="ff79b-1190">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1190">tx_queue_create</span></span>

<span data-ttu-id="ff79b-1191">İleti kuyruğu oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-1191">Create message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1192">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1192">Prototype</span></span>

```c
UINT tx_queue_create(TX_QUEUE *queue_ptr, CHAR *name_ptr,
                          UINT message_size,
                          VOID *queue_start, ULONG queue_size);
```
### <a name="description"></a><span data-ttu-id="ff79b-1193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1193">Description</span></span>

<span data-ttu-id="ff79b-1194">Bu hizmet, genellikle karşılıklı iş parçacığı iletişimi için kullanılan bir ileti kuyruğu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1194">This service creates a message queue that is typically used for interthread communication.</span></span> <span data-ttu-id="ff79b-1195">Toplam ileti sayısı, belirtilen ileti boyutundan ve sıradaki toplam bayt sayısından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1195">The total number of messages is calculated from the specified message size and the total number of bytes in the queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1196">Kuyruğun bellek alanında belirtilen toplam bayt sayısı, belirtilen ileti boyutuyla eşit olarak bölünemiyor ise, bellek alanındaki kalan baytlar kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1196">If the total number of bytes specified in the queue’s memory area is not evenly divisible by the specified message size, the remaining bytes in the memory area are not used.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1197">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1197">Parameters</span></span>

- <span data-ttu-id="ff79b-1198">**queue_ptr**: ileti kuyruğu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1198">**queue_ptr**: Pointer to a message queue control block.</span></span>
- <span data-ttu-id="ff79b-1199">**name_ptr**: ileti sırasının adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1199">**name_ptr**: Pointer to the name of the message queue.</span></span>
- <span data-ttu-id="ff79b-1200">**message_size**: kuyruktaki her iletinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1200">**message_size**: Specifies the size of each message in the queue.</span></span> <span data-ttu-id="ff79b-1201">İleti boyutları 1 32 bitlik sözcükten 16 32 bit sözcüklere kadar değişir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1201">Message sizes range from 1 32-bit word to 16 32-bit words.</span></span> <span data-ttu-id="ff79b-1202">Geçerli ileti boyutu seçenekleri, 1 ile 16 arasında (dahil) sayısal değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1202">Valid message size options are numerical values from 1 through 16, inclusive.</span></span>
- <span data-ttu-id="ff79b-1203">**queue_start**: ileti sırasının başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1203">**queue_start**: Starting address of the message queue.</span></span> <span data-ttu-id="ff79b-1204">Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1204">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="ff79b-1205">**queue_size**: ileti kuyruğu için kullanılabilen toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1205">**queue_size**: Total number of bytes available for the message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1206">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1206">Return Values</span></span>

- <span data-ttu-id="ff79b-1207">**TX_SUCCESS**: (0x00) başarılı ileti kuyruğu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1207">**TX_SUCCESS**: (0x00) Successful message queue creation.</span></span>
- <span data-ttu-id="ff79b-1208">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1208">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span> <span data-ttu-id="ff79b-1209">İşaretçi NULL ya da sıra zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1209">Either the pointer is NULL or the queue is already created.</span></span>
- <span data-ttu-id="ff79b-1210">TX_PTR_ERROR: (0x03) ileti sırasının başlangıç adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1210">TX_PTR_ERROR: (0x03) Invalid starting address of the message queue.</span></span>
- <span data-ttu-id="ff79b-1211">TX_SIZE_ERROR: (0x05) ileti sırasının boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1211">TX_SIZE_ERROR: (0x05) Size of message queue is invalid.</span></span>
- <span data-ttu-id="ff79b-1212">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1212">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1213">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1213">Allowed From</span></span>

<span data-ttu-id="ff79b-1214">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-1214">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1215">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1215">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1216">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1216">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1217">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1217">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;

/* Create a message queue whose total size is 2000 bytes
   starting at address 0x300000. Each message in this
   queue is defined to be 4 32-bit words long. */
status = tx_queue_create(&my_queue, "my_queue_name",
            4, (VOID *) 0x300000, 2000);

/* If status equals TX_SUCCESS, my_queue contains room
   for storing 125 messages (2000 bytes/ 16 bytes per
   message). */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1218">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1218">See Also</span></span>

- <span data-ttu-id="ff79b-1219">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1219">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1220">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1220">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1221">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1221">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1222">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1222">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1223">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1223">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1224">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1224">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1225">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1225">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1226">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1226">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1227">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1227">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1228">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1228">tx_queue_send_notify</span></span>

## <a name="tx_queue_delete"></a><span data-ttu-id="ff79b-1229">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1229">tx_queue_delete</span></span>

<span data-ttu-id="ff79b-1230">İleti kuyruğunu sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-1230">Delete message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1231">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1231">Prototype</span></span>

```C
UINT tx_queue_delete(TX_QUEUE *queue_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1232">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1232">Description</span></span>

<span data-ttu-id="ff79b-1233">Bu hizmet, belirtilen ileti sırasını siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1233">This service deletes the specified message queue.</span></span> <span data-ttu-id="ff79b-1234">Bu kuyruktan bir ileti beklemeden askıya alınmış tüm iş parçacıkları sürdürülür ve TX_DELETED dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1234">All threads suspended waiting for a message from this queue are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1235">Uygulama, kuyruk silinmeden önce bu sıra için gönderilen bildirim geri çağrısının tamamlandı (veya devre dışı) olduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1235">The application must ensure that any send notify callback for this queue is completed (or disabled) before deleting the queue.</span></span> <span data-ttu-id="ff79b-1236">Ayrıca, uygulamanın, silinen bir kuyruğun gelecekteki kullanımını önlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1236">In addition, the application must prevent any future use of a deleted queue.</span></span>

<span data-ttu-id="ff79b-1237">*Ayrıca, bu hizmet tamamlandıktan sonra kullanılabilir olan Kuyrukla ilişkili bellek alanını yönetmek için uygulamanın sorumluluğundadır.*</span><span class="sxs-lookup"><span data-stu-id="ff79b-1237">*It is also the application's responsibility to manage the memory area associated with the queue, which is available after this service completes.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1238">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1238">Parameters</span></span> 

- <span data-ttu-id="ff79b-1239">**queue_ptr**: daha önce oluşturulmuş bir ileti kuyruğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1239">**queue_ptr**: Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1240">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1240">Return Values</span></span>

- <span data-ttu-id="ff79b-1241">**TX_SUCCESS**: (0x00) başarılı ileti kuyruğu silme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1241">**TX_SUCCESS**: (0x00) Successful message queue deletion.</span></span>
- <span data-ttu-id="ff79b-1242">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1242">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="ff79b-1243">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1243">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1244">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1244">Allowed From</span></span>

<span data-ttu-id="ff79b-1245">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-1245">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1246">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1246">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1247">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1247">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1248">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1248">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;

/* Delete entire message queue. Assume that the queue
   has already been created with a call to
   tx_queue_create. */
status = tx_queue_delete(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1249">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1249">See Also</span></span>

- <span data-ttu-id="ff79b-1250">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1250">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1251">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1251">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1252">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1252">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1253">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1253">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1254">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1254">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1255">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1255">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1256">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1256">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1257">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1257">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1258">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1258">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1259">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1259">tx_queue_send_notify</span></span>

## <a name="tx_queue_flush"></a><span data-ttu-id="ff79b-1260">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1260">tx_queue_flush</span></span>

<span data-ttu-id="ff79b-1261">İleti sırasındaki boş iletiler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1261">Empty messages in message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1262">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1262">Prototype</span></span>

```C
UINT tx_queue_flush(TX_QUEUE *queue_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1263">Description</span></span>

<span data-ttu-id="ff79b-1264">Bu hizmet, belirtilen ileti kuyruğunda depolanan tüm iletileri siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1264">This service deletes all messages stored in the specified message queue.</span></span> <span data-ttu-id="ff79b-1265">Sıra doluysa, askıya alınmış tüm iş parçacıklarının iletileri atılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1265">If the queue is full, messages of all suspended threads are discarded.</span></span> <span data-ttu-id="ff79b-1266">Askıya alınan her iş parçacığı daha sonra ileti gönderme işleminin başarılı olduğunu belirten bir dönüş durumuyla sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1266">Each suspended thread is then resumed with a return status that indicates the message send was successful.</span></span> <span data-ttu-id="ff79b-1267">Sıra boşsa, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1267">If the queue is empty, this service does nothing.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1268">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1268">Parameters</span></span> 

- <span data-ttu-id="ff79b-1269">**queue_ptr**: daha önce oluşturulmuş bir ileti kuyruğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1269">**queue_ptr**: Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1270">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1270">Return Values</span></span>

- <span data-ttu-id="ff79b-1271">**TX_SUCCESS**: (0x00) başarılı ileti kuyruğu Temizleme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1271">**TX_SUCCESS**: (0x00) Successful message queue flush.</span></span>
- <span data-ttu-id="ff79b-1272">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1272">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1273">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1273">Allowed From</span></span>

<span data-ttu-id="ff79b-1274">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1274">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1275">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1275">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1276">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1276">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1277">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1277">Example</span></span>

```c
TX_QUEUE     my_queue;
UINT         status;

/* Flush out all pending messages in the specified message
   queue. Assume that the queue has already been created
   with a call to tx_queue_create. */
status =  tx_queue_flush(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
    empty. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1278">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1278">See Also</span></span>

- <span data-ttu-id="ff79b-1279">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1279">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1280">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1280">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1281">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1281">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1282">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1282">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1283">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1283">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1284">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1284">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1285">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1285">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1286">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1286">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1287">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1287">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1288">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1288">tx_queue_send_notify</span></span>

## <a name="tx_queue_front_send"></a><span data-ttu-id="ff79b-1289">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1289">tx_queue_front_send</span></span>

<span data-ttu-id="ff79b-1290">Kuyruğun önüne ileti gönder</span><span class="sxs-lookup"><span data-stu-id="ff79b-1290">Send message to the front of queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1291">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1291">Prototype</span></span>

```C
UINT tx_queue_front_send(TX_QUEUE *queue_ptr,
                           VOID *source_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-1292">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1292">Description</span></span>

<span data-ttu-id="ff79b-1293">Bu hizmet, belirtilen ileti sırasının ön konumuna bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1293">This service sends a message to the front location of the specified message queue.</span></span> <span data-ttu-id="ff79b-1294">İleti, kaynak işaretçi tarafından belirtilen bellek alanından kuyruğun önüne **kopyalanır** .</span><span class="sxs-lookup"><span data-stu-id="ff79b-1294">The message is **copied** to the front of the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1295">Parameters</span></span>

- <span data-ttu-id="ff79b-1296">**queue_ptr**: ileti kuyruğu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1296">**queue_ptr**: Pointer to a message queue control block.</span></span>
- <span data-ttu-id="ff79b-1297">**source_ptr**: ileti işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1297">**source_ptr**: Pointer to the message.</span></span>
- <span data-ttu-id="ff79b-1298">**wait_option**: ileti sırası doluysa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1298">**wait_option**: Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="ff79b-1299">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-1299">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-1300">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1300">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="ff79b-1301">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1301">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="ff79b-1302">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1302">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="ff79b-1303">TX_NO_WAIT seçilmesi, başarılı olup olmamasından bağımsız olarak bu hizmetten anında geri dönerek sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1303">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="ff79b-1304">*Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.*</span><span class="sxs-lookup"><span data-stu-id="ff79b-1304">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.*</span></span>

    <span data-ttu-id="ff79b-1305">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının sırada yer açılıncaya kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1305">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>

    <span data-ttu-id="ff79b-1306">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, sıradaki Oda beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1306">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1307">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1307">Return Values</span></span>

- <span data-ttu-id="ff79b-1308">**TX_SUCCESS**: (0x00) Ileti gönderme başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1308">**TX_SUCCESS**: (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="ff79b-1309">**TX_DELETED**: (0x01) ileti kuyruğu iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1309">**TX_DELETED**: (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-1310">**TX_QUEUE_FULL**: (0x0B) hizmet, belirtilen süre için sıra dolu olduğundan ileti gönderemedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1310">**TX_QUEUE_FULL**: (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="ff79b-1311">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1311">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-1312">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1312">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="ff79b-1313">TX_PTR_ERROR: (0x03) ileti için geçersiz kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1313">TX_PTR_ERROR: (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="ff79b-1314">TX_WAIT_ERROR: (0x04) iş parçacığından oluşan çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1314">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1315">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1315">Allowed From</span></span>

<span data-ttu-id="ff79b-1316">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1316">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1317">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1317">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1318">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1318">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1319">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1319">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;
ULONG        my_message[4];

/* Send a message to the front of "my_queue." Return
   immediately, regardless of success. This wait
   option is used for calls from initialization, timers,
   and ISRs. */
status = tx_queue_front_send(&my_queue, my_message,
            TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is at the front
   of the specified queue. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1320">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1320">See Also</span></span>

- <span data-ttu-id="ff79b-1321">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1321">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1322">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1322">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1323">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1323">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1324">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1324">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1325">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1325">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1326">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1326">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1327">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1327">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1328">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1328">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1329">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1329">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1330">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1330">tx_queue_send_notify</span></span>

## <a name="tx_queue_info_get"></a><span data-ttu-id="ff79b-1331">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1331">tx_queue_info_get</span></span>

<span data-ttu-id="ff79b-1332">Kuyruk hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="ff79b-1332">Retrieve information about queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1333">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1333">Prototype</span></span>

```C
UINT tx_queue_info_get(TX_QUEUE *queue_ptr, CHAR **name,
        ULONG *enqueued, ULONG *available_storage
        TX_THREAD **first_suspended, ULONG *suspended_count,
        TX_QUEUE **next_queue);
```
### <a name="description"></a><span data-ttu-id="ff79b-1334">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1334">Description</span></span>

<span data-ttu-id="ff79b-1335">Bu hizmet, belirtilen ileti kuyruğu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1335">This service retrieves information about the specified message queue.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1336">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1336">Parameters</span></span>

- <span data-ttu-id="ff79b-1337">**queue_ptr**: daha önce oluşturulmuş bir ileti kuyruğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1337">**queue_ptr**: Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="ff79b-1338">**ad**: kuyruğun adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1338">**name**: Pointer to destination for the pointer to the queue’s name.</span></span>
- <span data-ttu-id="ff79b-1339">**sıraya alındı**: Şu anda kuyruktaki ileti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1339">**enqueued**: Pointer to destination for the number of messages currently in the queue.</span></span>
- <span data-ttu-id="ff79b-1340">**available_storage**: sıranın Şu anda alana sahip olduğu ileti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1340">**available_storage**: Pointer to destination for the number of messages the queue currently has space for.</span></span>
- <span data-ttu-id="ff79b-1341">**first_suspended**: bu sıranın askıya alınma listesindeki iş parçacığına yönelik işaretçinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1341">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this queue.</span></span>
- <span data-ttu-id="ff79b-1342">**suspended_count**: bu kuyrukta askıya alınmış olan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1342">**suspended_count**: Pointer to destination for the number of threads currently suspended on this queue.</span></span>
- <span data-ttu-id="ff79b-1343">**next_queue**: sonraki oluşturulan sıranın işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1343">**next_queue**: Pointer to destination for the pointer of the next created queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1344">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1344">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1345">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1345">Return Values</span></span>

- <span data-ttu-id="ff79b-1346">**TX_SUCCESS**: (0x00) başarılı kuyruk bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1346">**TX_SUCCESS**: (0x00) Successful queue information get.</span></span>
- <span data-ttu-id="ff79b-1347">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1347">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1348">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1348">Allowed From</span></span>

<span data-ttu-id="ff79b-1349">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1349">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1350">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1350">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1351">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1351">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1352">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1352">Example</span></span>

```C
TX_QUEUE     my_queue;
CHAR         *name;
ULONG        enqueued;
ULONG        available_storage;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_QUEUE     *next_queue;
UINT         status;

/* Retrieve information about the previously created
   message queue "my_queue." */
status = tx_queue_info_get(&my_queue, &name,
            &enqueued, &available_storage,
            &first_suspended, &suspended_count,
            &next_queue);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1353">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1353">See Also</span></span>

- <span data-ttu-id="ff79b-1354">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1354">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1355">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1355">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1356">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1356">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1357">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1357">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1358">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1358">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1359">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1359">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1360">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1360">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1361">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1361">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1362">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1362">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1363">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1363">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_info_get"></a><span data-ttu-id="ff79b-1364">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1364">tx_queue_performance_info_get</span></span>

<span data-ttu-id="ff79b-1365">Sıra performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1365">Get queue performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1366">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1366">Prototype</span></span>

```C
UINT  tx_queue_performance_info_get(TX_QUEUE *queue_ptr,
        ULONG *messages_sent, ULONG *messages_received,
        ULONG *empty_suspensions, ULONG *full_suspensions,
        ULONG *full_errors, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-1367">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1367">Description</span></span>

<span data-ttu-id="ff79b-1368">Bu hizmet, belirtilen sıra hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1368">This service retrieves performance information about the specified queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1369">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_QUEUE_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1369">The ThreadX SMP library and application must be built with **TX_QUEUE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1370">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1370">Parameters</span></span>

- <span data-ttu-id="ff79b-1371">**queue_ptr**: daha önce oluşturulan sıraya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1371">**queue_ptr**: Pointer to previously created queue.</span></span>
- <span data-ttu-id="ff79b-1372">**messages_sent**: bu kuyrukta gerçekleştirilen gönderme isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1372">**messages_sent**: Pointer to destination for the number of send requests performed on this queue.</span></span>
- <span data-ttu-id="ff79b-1373">**messages_received**: bu kuyrukta gerçekleştirilen alma isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1373">**messages_received**: Pointer to destination for the number of receive requests performed on this queue.</span></span>
- <span data-ttu-id="ff79b-1374">**empty_suspensions**: Bu kuyruktaki sıra boş getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1374">**empty_suspensions**: Pointer to destination for the number of queue empty suspensions on this queue.</span></span>
- <span data-ttu-id="ff79b-1375">**full_suspensions**: Bu kuyruktaki Queue Full getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1375">**full_suspensions**: Pointer to destination for the number of queue full suspensions on this queue.</span></span>
- <span data-ttu-id="ff79b-1376">**full_errors**: Bu kuyruktaki sıranın tam hatalarının sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1376">**full_errors**: Pointer to destination for the number of queue full errors on this queue.</span></span>
- <span data-ttu-id="ff79b-1377">**zaman aşımları**: Bu kuyruktaki iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1377">**timeouts**: Pointer to destination for the number of thread suspension timeouts on this queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1378">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1378">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1379">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1379">Return Values</span></span>

- <span data-ttu-id="ff79b-1380">**TX_SUCCESS**: (0x00) başarılı kuyruk performansı alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1380">**TX_SUCCESS**: (0x00) Successful queue performance get.</span></span>
- <span data-ttu-id="ff79b-1381">**TX_PTR_ERROR**: (0x03) geçersiz kuyruk işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1381">**TX_PTR_ERROR**: (0x03) Invalid queue pointer.</span></span>
- <span data-ttu-id="ff79b-1382">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1382">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1383">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1383">Allowed From</span></span>

<span data-ttu-id="ff79b-1384">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1384">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1385">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1385">Example</span></span>

```C
TX_QUEUE     my_queue;
ULONG        messages_sent;
ULONG        messages_received;
ULONG        empty_suspensions;
ULONG        full_suspensions;
ULONG        full_errors;
ULONG        timeouts;

/* Retrieve performance information on the previously created
   queue. */
status = tx_queue_performance_info_get(&my_queue, &messages_sent,
            &messages_received, &empty_suspensions,
            &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1386">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1386">See Also</span></span>

- <span data-ttu-id="ff79b-1387">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1387">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1388">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1388">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1389">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1389">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1390">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1390">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1391">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1391">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1392">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1392">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1393">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1393">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1394">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1394">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1395">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1395">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1396">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1396">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_system_info_get"></a><span data-ttu-id="ff79b-1397">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1397">tx_queue_performance_system_info_get</span></span>

<span data-ttu-id="ff79b-1398">Sıra sistemi performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1398">Get queue system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1399">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1399">Prototype</span></span>

```C
UINT  tx_queue_performance_system_info_get(ULONG *messages_sent,
        ULONG *messages_received, ULONG *empty_suspensions,
        ULONG *full_suspensions, ULONG *full_errors,
        ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-1400">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1400">Description</span></span>

<span data-ttu-id="ff79b-1401">Bu hizmet sistemdeki tüm kuyruklarla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1401">This service retrieves performance information about all the queues in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1402">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_QUEUE_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1402">The ThreadX SMP library and application must be built with **TX_QUEUE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1403">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1403">Parameters</span></span>

- <span data-ttu-id="ff79b-1404">**messages_sent**: tüm kuyruklarda gerçekleştirilen gönderme isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1404">**messages_sent**: Pointer to destination for the total number of send requests performed on all queues.</span></span>
- <span data-ttu-id="ff79b-1405">**messages_received**: tüm kuyruklarda gerçekleştirilen Alım isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1405">**messages_received**: Pointer to destination for the total number of receive requests performed on all queues.</span></span>
- <span data-ttu-id="ff79b-1406">**empty_suspensions**: tüm kuyruklarda boş kuyruk boş getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1406">**empty_suspensions**: Pointer to destination for the total number of queue empty suspensions on all queues.</span></span>
- <span data-ttu-id="ff79b-1407">**full_suspensions**: tüm kuyruklarda toplam Queue Full getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1407">**full_suspensions**: Pointer to destination for the total number of queue full suspensions on all queues.</span></span>
- <span data-ttu-id="ff79b-1408">**full_errors**: tüm sıralarda toplam sıra tam hatalarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1408">**full_errors**: Pointer to destination for the total number of queue full errors on all queues.</span></span>
- <span data-ttu-id="ff79b-1409">**zaman aşımları**: tüm sıralarda toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1409">**timeouts**: Pointer to destination for the total number of thread suspension timeouts on all queues.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1410">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1410">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1411">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1411">Return Values</span></span>

- <span data-ttu-id="ff79b-1412">**TX_SUCCESS**: (0x00) başarılı kuyruk sistem performansı alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1412">**TX_SUCCESS**: (0x00) Successful queue system performance get.</span></span>
- <span data-ttu-id="ff79b-1413">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1413">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1414">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1414">Allowed From</span></span>

<span data-ttu-id="ff79b-1415">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1415">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1416">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1416">Example</span></span>

```c
ULONG         messages_sent;
ULONG         messages_received;
ULONG         empty_suspensions;
ULONG         full_suspensions;
ULONG         full_errors;
ULONG         timeouts;

/* Retrieve performance information on all previously created
   queues. */
status = tx_queue_performance_system_info_get(&messages_sent,
            &messages_received, &empty_suspensions,
            &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1417">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1417">See Also</span></span>

- <span data-ttu-id="ff79b-1418">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1418">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1419">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1419">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1420">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1420">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1421">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1421">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1422">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1422">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1423">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1423">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1424">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1424">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1425">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1425">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1426">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1426">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1427">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1427">tx_queue_send_notify</span></span>

## <a name="tx_queue_prioritize"></a><span data-ttu-id="ff79b-1428">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1428">tx_queue_prioritize</span></span>

<span data-ttu-id="ff79b-1429">Sıra askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="ff79b-1429">Prioritize queue suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1430">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1430">Prototype</span></span>

```C
UINT tx_queue_prioritize(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="ff79b-1431">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1431">Description</span></span>

<span data-ttu-id="ff79b-1432">Bu hizmet, askıya alma listesinin önünde bu kuyruğa bir ileti (veya bir ileti yerleştirmek için) için askıya alınan en yüksek öncelik iş parçacığını yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1432">This service places the highest priority thread suspended for a message (or to place a message) on this queue at the front of the suspension list.</span></span> <span data-ttu-id="ff79b-1433">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1433">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1434">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1434">Parameters</span></span> 

- <span data-ttu-id="ff79b-1435">**queue_ptr**: daha önce oluşturulmuş bir ileti kuyruğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1435">**queue_ptr**: Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1436">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1436">Return Values</span></span>

- <span data-ttu-id="ff79b-1437">**TX_SUCCESS**: (0x00) başarılı sıra önceliği belirleme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1437">**TX_SUCCESS**: (0x00) Successful queue prioritize.</span></span>
- <span data-ttu-id="ff79b-1438">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1438">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1439">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1439">Allowed From</span></span>

<span data-ttu-id="ff79b-1440">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1440">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1441">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1441">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1442">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1442">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1443">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1443">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next message placed on this queue. */
status = tx_queue_prioritize(&my_queue);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_queue_send or tx_queue_front_send call made
   to this queue will wake up this thread. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1444">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1444">See Also</span></span>

- <span data-ttu-id="ff79b-1445">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1445">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1446">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1446">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1447">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1447">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1448">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1448">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1449">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1449">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1450">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1450">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1451">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1451">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1452">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1452">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1453">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1453">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1454">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1454">tx_queue_send_notify</span></span>

## <a name="tx_queue_receive"></a><span data-ttu-id="ff79b-1455">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1455">tx_queue_receive</span></span>

<span data-ttu-id="ff79b-1456">İleti kuyruğundan ileti al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1456">Get message from message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1457">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1457">Prototype</span></span>

```C
UINT tx_queue_receive(TX_QUEUE *queue_ptr,
                          VOID *destination_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-1458">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1458">Description</span></span>

<span data-ttu-id="ff79b-1459">Bu hizmet, belirtilen ileti sırasından bir ileti alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1459">This service retrieves a message from the specified message queue.</span></span> <span data-ttu-id="ff79b-1460">Alınan ileti, kuyruktan hedef işaretçi tarafından belirtilen bellek alanına **kopyalanır** .</span><span class="sxs-lookup"><span data-stu-id="ff79b-1460">The retrieved message is **copied** from the queue into the memory area specified by the destination pointer.</span></span> <span data-ttu-id="ff79b-1461">Bu ileti daha sonra kuyruktan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1461">That message is then removed from the queue.</span></span>

> [!WARNING]
> <span data-ttu-id="ff79b-1462">Belirtilen hedef bellek alanı iletiyi tutabilecek kadar büyük olmalıdır; Yani, **destination_ptr** tarafından işaret edilen ileti hedefi en az bu sıranın ileti boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1462">The specified destination memory area must be large enough to hold the message; i.e., the message destination pointed to by **destination_ptr** must be at least as large as the message size for this queue.</span></span> <span data-ttu-id="ff79b-1463">Aksi takdirde, hedef yeterince büyük değilse, aşağıdaki bellek alanında bellek bozulması oluşur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1463">Otherwise, if the destination is not large enough, memory corruption occurs in the following memory area.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1464">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1464">Parameters</span></span>

- <span data-ttu-id="ff79b-1465">**queue_ptr**: daha önce oluşturulmuş bir ileti kuyruğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1465">**queue_ptr**: Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="ff79b-1466">**destination_ptr**: iletinin kopyalanacağı konum.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1466">**destination_ptr**: Location of where to copy the message.</span></span>
- <span data-ttu-id="ff79b-1467">**wait_option**: ileti sırası boş ise hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1467">**wait_option**: Defines how the service behaves if the message queue is empty.</span></span> <span data-ttu-id="ff79b-1468">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-1468">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-1469">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1469">**TX_NO_WAIT**: (0x00000000)</span></span> 
    - <span data-ttu-id="ff79b-1470">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1470">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span> 
    - <span data-ttu-id="ff79b-1471">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1471">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="ff79b-1472">TX_NO_WAIT seçilmesi, başarılı olup olmamasından bağımsız olarak bu hizmetten anında geri dönerek sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1472">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="ff79b-1473">Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1473">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>

    <span data-ttu-id="ff79b-1474">TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının bir ileti kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1474">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a message is available.</span></span>

    <span data-ttu-id="ff79b-1475">Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, ileti beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1475">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a message.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1476">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1476">Return Values</span></span>

- <span data-ttu-id="ff79b-1477">**TX_SUCCESS**: (0x00) iletiyi başarıyla alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1477">**TX_SUCCESS**: (0x00) Successful retrieval of message.</span></span>
- <span data-ttu-id="ff79b-1478">**TX_DELETED**: (0x01) ileti kuyruğu iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1478">**TX_DELETED**: (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-1479">**TX_QUEUE_EMPTY**: (0X0a) hizmeti, belirtilen sürenin süresi boyunca sıra boş olduğundan bir iletiyi alamadı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1479">**TX_QUEUE_EMPTY**: (0x0A) Service was unable to retrieve a message because the queue was empty for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="ff79b-1480">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1480">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-1481">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1481">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="ff79b-1482">TX_PTR_ERROR: (0x03) ileti için geçersiz hedef işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1482">TX_PTR_ERROR: (0x03) Invalid destination pointer for message.</span></span>
- <span data-ttu-id="ff79b-1483">TX_WAIT_ERROR: (0x04) iş parçacığından oluşan çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1483">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1484">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1484">Allowed From</span></span>

<span data-ttu-id="ff79b-1485">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1485">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1486">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1486">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1487">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1487">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1488">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1488">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;
ULONG my_message[4];

/* Retrieve a message from "my_queue." If the queue is
   empty, suspend until a message is present. Note that
   this suspension is only possible from application
   threads. */
status =  tx_queue_receive(&my_queue, my_message,
                          TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the message is in
   "my_message." */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1489">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1489">See Also</span></span>

- <span data-ttu-id="ff79b-1490">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1490">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1491">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1491">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1492">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1492">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1493">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1493">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1494">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1494">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1495">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1495">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1496">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1496">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1497">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1497">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1498">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1498">tx_queue_send</span></span>
- <span data-ttu-id="ff79b-1499">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1499">tx_queue_send_notify</span></span>

## <a name="tx_queue_send"></a><span data-ttu-id="ff79b-1500">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1500">tx_queue_send</span></span>

<span data-ttu-id="ff79b-1501">İletiyi ileti kuyruğuna gönder</span><span class="sxs-lookup"><span data-stu-id="ff79b-1501">Send message to message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1502">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1502">Prototype</span></span>

```C
UINT tx_queue_send(TX_QUEUE *queue_ptr,
                          VOID *source_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="ff79b-1503">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1503">Description</span></span>

<span data-ttu-id="ff79b-1504">Bu hizmet, belirtilen ileti kuyruğuna bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1504">This service sends a message to the specified message queue.</span></span> <span data-ttu-id="ff79b-1505">Gönderilen ileti, kaynak işaretçi tarafından belirtilen bellek alanından kuyruğa **kopyalanır** .</span><span class="sxs-lookup"><span data-stu-id="ff79b-1505">The sent message is **copied** to the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1506">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1506">Parameters</span></span>

- <span data-ttu-id="ff79b-1507">**queue_ptr**: daha önce oluşturulmuş bir ileti kuyruğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1507">**queue_ptr**: Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="ff79b-1508">**source_ptr**: ileti işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1508">**source_ptr**: Pointer to the message.</span></span>
- <span data-ttu-id="ff79b-1509">**wait_option**: ileti sırası doluysa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1509">**wait_option**: Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="ff79b-1510">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-1510">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-1511">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1511">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="ff79b-1512">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1512">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="ff79b-1513">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1513">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="ff79b-1514">TX_NO_WAIT seçilmesi, başarılı olup olmamasından bağımsız olarak bu hizmetten anında geri dönerek sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1514">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="ff79b-1515">*Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.*</span><span class="sxs-lookup"><span data-stu-id="ff79b-1515">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.*</span></span>

    <span data-ttu-id="ff79b-1516">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının sırada yer açılıncaya kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1516">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>

    <span data-ttu-id="ff79b-1517">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, sıradaki Oda beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1517">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1518">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1518">Return Values</span></span>

- <span data-ttu-id="ff79b-1519">**TX_SUCCESS**: (0x00) Ileti gönderme başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1519">**TX_SUCCESS**: (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="ff79b-1520">**TX_DELETED**: (0x01) ileti kuyruğu iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1520">**TX_DELETED**: (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-1521">**TX_QUEUE_FULL**: (0x0B) hizmet, belirtilen süre için sıra dolu olduğundan ileti gönderemedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1521">**TX_QUEUE_FULL**: (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="ff79b-1522">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1522">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-1523">TX_QUEUE_ERROR: (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1523">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="ff79b-1524">TX_PTR_ERROR: (0x03) ileti için geçersiz kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1524">TX_PTR_ERROR: (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="ff79b-1525">TX_WAIT_ERROR: (0x04) iş parçacığından oluşan çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1525">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1526">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1526">Allowed From</span></span>

<span data-ttu-id="ff79b-1527">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1527">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1528">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1528">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1529">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1529">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1530">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1530">Example</span></span>

```C
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to "my_queue." Return immediately,
   regardless of success. This wait option is used for
   calls from initialization, timers, and ISRs. */
status =  tx_queue_send(&my_queue, my_message, TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is in the
   queue. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1531">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1531">See Also</span></span>

- <span data-ttu-id="ff79b-1532">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1532">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1533">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1533">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1534">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1534">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1535">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1535">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1536">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1536">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1537">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1537">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1538">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1538">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1539">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1539">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1540">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1540">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1541">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1541">tx_queue_send_notify</span></span>

## <a name="tx_queue_send_notify"></a><span data-ttu-id="ff79b-1542">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1542">tx_queue_send_notify</span></span> 

<span data-ttu-id="ff79b-1543">İleti kuyruğa gönderildiğinde uygulamayı bilgilendir</span><span class="sxs-lookup"><span data-stu-id="ff79b-1543">Notify application when message is sent to queue</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1544">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1544">Prototype</span></span>

```C
UINT  tx_queue_send_notify(TX_QUEUE *queue_ptr,
        VOID (*queue_send_notify)(TX_QUEUE *));
```
### <a name="description"></a><span data-ttu-id="ff79b-1545">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1545">Description</span></span>

<span data-ttu-id="ff79b-1546">Bu hizmet, belirtilen sıraya bir ileti gönderildiğinde çağrılan bir bildirim geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1546">This service registers a notification callback function that is called whenever a message is sent to the specified queue.</span></span> <span data-ttu-id="ff79b-1547">Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1547">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ff79b-1548">Uygulamanın kuyruk gönderme bildirimi geri çağırması, askıya alma seçeneği ile herhangi bir ThreadX SMP API çağrısı yapılmasına izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1548">The application’s queue send notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1549">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1549">Parameters</span></span> 

- <span data-ttu-id="ff79b-1550">**queue_ptr**: daha önce oluşturulan sıraya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1550">**queue_ptr**: Pointer to previously created queue.</span></span>
- <span data-ttu-id="ff79b-1551">**queue_send_notify**: uygulamanın kuyruk gönderme bildirimi işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1551">**queue_send_notify**: Pointer to application’s queue send notification function.</span></span> <span data-ttu-id="ff79b-1552">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1552">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1553">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1553">Return Values</span></span>

- <span data-ttu-id="ff79b-1554">**TX_SUCCESS**: (0x00) kuyruk gönderme bildiriminin başarılı kaydı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1554">**TX_SUCCESS**: (0x00) Successful registration of queue send notification.</span></span>
- <span data-ttu-id="ff79b-1555">TX_QUEUE_ERROR: (0x09) geçersiz kuyruk işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1555">TX_QUEUE_ERROR: (0x09) Invalid queue pointer.</span></span>
- <span data-ttu-id="ff79b-1556">TX_FEATURE_NOT_ENABLED: (0xFF) sistem, bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1556">TX_FEATURE_NOT_ENABLED: (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1557">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1557">Allowed From</span></span>

<span data-ttu-id="ff79b-1558">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1558">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1559">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1559">Example</span></span>

```C
TX_QUEUE         my_queue;

/* Register the "my_queue_send_notify" function for monitoring
   messages sent to the queue "my_queue." */
status = tx_queue_send_notify(&my_queue, my_queue_send_notify);

/* If status is TX_SUCCESS the queue send notification function was
   successfully registered. */
void my_queue_send_notify(TX_QUEUE *queue_ptr)
{
/* A message was just sent to this queue! */
}
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1560">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1560">See Also</span></span>

- <span data-ttu-id="ff79b-1561">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1561">tx_queue_create</span></span>
- <span data-ttu-id="ff79b-1562">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1562">tx_queue_delete</span></span>
- <span data-ttu-id="ff79b-1563">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="ff79b-1563">tx_queue_flush</span></span>
- <span data-ttu-id="ff79b-1564">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1564">tx_queue_front_send</span></span>
- <span data-ttu-id="ff79b-1565">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1565">tx_queue_info_get</span></span>
- <span data-ttu-id="ff79b-1566">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1566">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1567">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1567">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1568">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1568">tx_queue_prioritize</span></span>
- <span data-ttu-id="ff79b-1569">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="ff79b-1569">tx_queue_receive</span></span>
- <span data-ttu-id="ff79b-1570">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="ff79b-1570">tx_queue_send</span></span>

## <a name="tx_semaphore_ceiling_put"></a><span data-ttu-id="ff79b-1571">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1571">tx_semaphore_ceiling_put</span></span> 

<span data-ttu-id="ff79b-1572">Tavan ile sayım semafora bir örnek yerleştirme</span><span class="sxs-lookup"><span data-stu-id="ff79b-1572">Place an instance in counting semaphore with ceiling</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1573">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1573">Prototype</span></span>

```C
UINT  tx_semaphore_ceiling_put(TX_SEMAPHORE *semaphore_ptr,
        ULONG ceiling);
```
### <a name="description"></a><span data-ttu-id="ff79b-1574">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1574">Description</span></span>

<span data-ttu-id="ff79b-1575">Bu hizmet, gerçekte belirtilen sayım semafora bir örnek koyar ve bu da gerçekteki sayım semaforu bir tane artırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1575">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span> <span data-ttu-id="ff79b-1576">Sayım semaforun geçerli değeri belirtilen tavan değerinden büyük veya bu değere eşitse, örnek yerleştirmeyecektir ve bir TX_CEILING_EXCEEDED hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1576">If the counting semaphore’s current value is greater than or equal to the specified ceiling, the instance will not be put and a TX_CEILING_EXCEEDED error will be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1577">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1577">Parameters</span></span> 

- <span data-ttu-id="ff79b-1578">**semaphore_ptr**: daha önce oluşturulan semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1578">**semaphore_ptr**: Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="ff79b-1579">**tavan**: semafor için izin verilen üst sınır (geçerli değer aralığı 1 ile 0xFFFFFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="ff79b-1579">**ceiling**: Maximum limit allowed for the semaphore (valid values range from 1 through 0xFFFFFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1580">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1580">Return Values</span></span>

- <span data-ttu-id="ff79b-1581">**TX_SUCCESS**: (0x00) başarılı semafor tavan koyun.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1581">**TX_SUCCESS**: (0x00) Successful semaphore ceiling put.</span></span>
- <span data-ttu-id="ff79b-1582">**TX_CEILING_EXCEEDED**: (0x21) PUT isteği tavan aşıyor.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1582">**TX_CEILING_EXCEEDED**: (0x21) Put request exceeds ceiling.</span></span>
- <span data-ttu-id="ff79b-1583">TX_INVALID_CEILING: (0x22) tavan için geçersiz sıfır değeri sağlandı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1583">TX_INVALID_CEILING: (0x22) An invalid value of zero was supplied for ceiling.</span></span>
- <span data-ttu-id="ff79b-1584">TX_SEMAPHORE_ERROR: (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1584">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1585">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1585">Allowed From</span></span>

<span data-ttu-id="ff79b-1586">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1586">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1587">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1587">Example</span></span>

```c
TX_SEMAPHORE     my_semaphore;

/* Increment the counting semaphore "my_semaphore" but make sure
   that it never exceeds 7 as specified in the call. */
status = tx_semaphore_ceiling_put(&my_semaphore, 7);

/* If status is TX_SUCCESS the semaphore count has been
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1588">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1588">See Also</span></span>

- <span data-ttu-id="ff79b-1589">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1589">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1590">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1590">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1591">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1591">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1592">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1592">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1593">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1593">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1594">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1594">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1595">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1595">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1596">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1596">tx_semaphore_put</span></span>
- <span data-ttu-id="ff79b-1597">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1597">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_create"></a><span data-ttu-id="ff79b-1598">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1598">tx_semaphore_create</span></span>

<span data-ttu-id="ff79b-1599">Sayım semaforu oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-1599">Create counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1600">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1600">Prototype</span></span>

```C
UINT tx_semaphore_create(TX_SEMAPHORE *semaphore_ptr,
                           CHAR *name_ptr, ULONG initial_count);
```
### <a name="description"></a><span data-ttu-id="ff79b-1601">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1601">Description</span></span>

<span data-ttu-id="ff79b-1602">Bu hizmet, iş parçacıkları arası eşitleme için bir sayım semaforu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1602">This service creates a counting semaphore for inter-thread synchronization.</span></span> <span data-ttu-id="ff79b-1603">İlk semafor sayısı bir giriş parametresi olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1603">The initial semaphore count is specified as an input parameter.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1604">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1604">Parameters</span></span> 

- <span data-ttu-id="ff79b-1605">**semaphore_ptr**: semafor denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1605">**semaphore_ptr**: Pointer to a semaphore control block.</span></span> 
- <span data-ttu-id="ff79b-1606">**name_ptr**: semafor adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1606">**name_ptr**: Pointer to the name of the semaphore.</span></span>
- <span data-ttu-id="ff79b-1607">**initial_count**: Bu semafor için başlangıç sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1607">**initial_count**: Specifies the initial count for this semaphore.</span></span> <span data-ttu-id="ff79b-1608">Yasal değerler 0x00000000 ile 0xFFFFFFFF arasında değişir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1608">Legal values range from 0x00000000 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1609">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1609">Return Values</span></span>

- <span data-ttu-id="ff79b-1610">**TX_SUCCESS**: (0x00) başarılı semafor oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1610">**TX_SUCCESS**: (0x00) Successful semaphore creation.</span></span>
- <span data-ttu-id="ff79b-1611">TX_SEMAPHORE_ERROR: (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1611">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span> <span data-ttu-id="ff79b-1612">İşaretçi NULL ya da semafor zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1612">Either the pointer is NULL or the semaphore is already created.</span></span>
- <span data-ttu-id="ff79b-1613">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1613">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1614">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1614">Allowed From</span></span>

<span data-ttu-id="ff79b-1615">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-1615">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1616">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1616">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1617">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1617">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1618">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1618">Example</span></span>

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Create a counting semaphore whose initial value is 1.
   This is typically the technique used to make a binary
   semaphore. Binary semaphores are used to provide
   protection over a common resource. */
status = tx_semaphore_create(&my_semaphore,
            "my_semaphore_name", 1);

/* If status equals TX_SUCCESS, my_semaphore is ready for
   use. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1619">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1619">See Also</span></span>

- <span data-ttu-id="ff79b-1620">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1620">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1621">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1621">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1622">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1622">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1623">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1623">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1624">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1624">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1625">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1625">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1626">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1626">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1627">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1627">tx_semaphore_put</span></span>
- <span data-ttu-id="ff79b-1628">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1628">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_delete"></a><span data-ttu-id="ff79b-1629">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1629">tx_semaphore_delete</span></span>

<span data-ttu-id="ff79b-1630">Sayım semaforu Sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-1630">Delete counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1631">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1631">Prototype</span></span>

```C
UINT tx_semaphore_delete(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1632">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1632">Description</span></span>

<span data-ttu-id="ff79b-1633">Bu hizmet, belirtilen sayım semaforu siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1633">This service deletes the specified counting semaphore.</span></span> <span data-ttu-id="ff79b-1634">Bir semafor örneği için bekleyen askıya alınan tüm iş parçacıkları sürdürülür ve TX_DELETED dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1634">All threads suspended waiting for a semaphore instance are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1635">Uygulama, semafor silinmeden önce Bu semafor için bir put bildirimi geri çağrısının tamamlandığından (veya devre dışı bırakıldığından) emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1635">The application must ensure that a put notify callback for this semaphore is completed (or disabled) before deleting the semaphore.</span></span> <span data-ttu-id="ff79b-1636">Ayrıca, uygulamanın, silinen semaforun gelecekteki tüm kullanımını önlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1636">In addition, the application must prevent all future use of a deleted semaphore.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1637">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1637">Parameters</span></span> 

- <span data-ttu-id="ff79b-1638">**semaphore_ptr**: daha önce oluşturulmuş bir semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1638">**semaphore_ptr**: Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1639">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1639">Return Values</span></span>

- <span data-ttu-id="ff79b-1640">**TX_SUCCESS**: (0x00) semafor silme işlemi başarıyla sayılıyor.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1640">**TX_SUCCESS**: (0x00) Successful counting semaphore deletion.</span></span>
- <span data-ttu-id="ff79b-1641">TX_SEMAPHORE_ERROR: (0x0C) geçersiz sayma semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1641">TX_SEMAPHORE_ERROR: (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="ff79b-1642">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1642">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1643">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1643">Allowed From</span></span>

<span data-ttu-id="ff79b-1644">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-1644">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1645">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1645">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1646">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1646">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1647">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1647">Example</span></span>

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Delete counting semaphore. Assume that the counting
   semaphore has already been created. */
status = tx_semaphore_delete(&my_semaphore);

/* If status equals TX_SUCCESS, the counting semaphore is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1648">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1648">See Also</span></span>

- <span data-ttu-id="ff79b-1649">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1649">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1650">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1650">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1651">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1651">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1652">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1652">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1653">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1653">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1654">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1654">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1655">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1655">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1656">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1656">tx_semaphore_put</span></span>
- <span data-ttu-id="ff79b-1657">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1657">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_get"></a><span data-ttu-id="ff79b-1658">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1658">tx_semaphore_get</span></span>

<span data-ttu-id="ff79b-1659">Sayım semafordan örnek al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1659">Get instance from counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1660">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1660">Prototype</span></span>

```C
UINT tx_semaphore_get(TX_SEMAPHORE *semaphore_ptr,
                          ULONG wait_option)
```
### <a name="description"></a><span data-ttu-id="ff79b-1661">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1661">Description</span></span>

<span data-ttu-id="ff79b-1662">Bu hizmet, belirtilen sayım semafordan bir örnek (tek bir sayı) alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1662">This service retrieves an instance (a single count) from the specified counting semaphore.</span></span> <span data-ttu-id="ff79b-1663">Sonuç olarak, belirtilen Semaforun sayısı bir ile azaltılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1663">As a result, the specified semaphore’s count is decreased by one.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1664">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1664">Parameters</span></span>

- <span data-ttu-id="ff79b-1665">**semaphore_ptr**: daha önce oluşturulmuş bir sayım semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1665">**semaphore_ptr**: Pointer to a previously created counting semaphore.</span></span>
- <span data-ttu-id="ff79b-1666">**wait_option**: semaforun kullanılabilir bir örneği yoksa hizmetin nasıl davranacağını tanımlar; Yani, semafor sayısı sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1666">**wait_option**: Defines how the service behaves if there are no instances of the semaphore available; i.e., the semaphore count is zero.</span></span> <span data-ttu-id="ff79b-1667">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ff79b-1667">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="ff79b-1668">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1668">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="ff79b-1669">**TX_WAIT_FOREVER**: (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1669">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="ff79b-1670">zaman aşımı değeri: (0x00000001 üzerinden 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="ff79b-1670">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="ff79b-1671">TX_NO_WAIT seçilmesi, başarılı olup olmamasından bağımsız olarak bu hizmetten anında geri dönerek sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1671">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="ff79b-1672">*Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.*</span><span class="sxs-lookup"><span data-stu-id="ff79b-1672">*This is the only valid option if the service is called from a non-thread; e.g., initialization, timer, or ISR.*</span></span>

    <span data-ttu-id="ff79b-1673">TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının bir semafor örneği kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1673">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a semaphore instance is available.</span></span> 

    <span data-ttu-id="ff79b-1674">Bir sayısal değer (1-0xFFFFFFFE) seçilmesi, bir semafor örneği beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1674">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a semaphore instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1675">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1675">Return Values</span></span>

- <span data-ttu-id="ff79b-1676">**TX_SUCCESS**: (0x00) bir semafor örneğinin başarılı bir şekilde alımı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1676">**TX_SUCCESS**: (0x00) Successful retrieval of a semaphore instance.</span></span>
- <span data-ttu-id="ff79b-1677">**TX_DELETED**: (0x01) iş parçacığı askıya alınırken sayım semaforu silindi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1677">**TX_DELETED**: (0x01) Counting semaphore was deleted while thread was suspended.</span></span>
- <span data-ttu-id="ff79b-1678">**TX_NO_INSTANCE**: (0x0D) hizmeti, sayım semaforun bir örneğini alamadı (semafor sayısı, belirtilen süre içinde beklenecek şekilde sıfır).</span><span class="sxs-lookup"><span data-stu-id="ff79b-1678">**TX_NO_INSTANCE**: (0x0D) Service was unable to retrieve an instance of the counting semaphore (semaphore count is zero within the specified time to wait).</span></span>
- <span data-ttu-id="ff79b-1679">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1679">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-1680">TX_SEMAPHORE_ERROR: (0x0C) geçersiz sayma semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1680">TX_SEMAPHORE_ERROR: (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="ff79b-1681">TX_WAIT_ERROR: (0x04) iş parçacığı olmayan bir çağrıda TX_NO_WAIT dışında bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1681">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1682">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1682">Allowed From</span></span>

<span data-ttu-id="ff79b-1683">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1683">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1684">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1684">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1685">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1685">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1686">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1686">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Get a semaphore instance from the semaphore
   "my_semaphore." If the semaphore count is zero,
   suspend until an instance becomes available.
   Note that this suspension is only possible from
   application threads. */
status =  tx_semaphore_get(&my_semaphore, TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the thread has obtained
   an instance of the semaphore. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1687">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1687">See Also</span></span>

- <span data-ttu-id="ff79b-1688">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1688">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1689">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1689">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1690">tx_semahore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1690">tx_semahore_delete</span></span>
- <span data-ttu-id="ff79b-1691">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1691">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1692">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1692">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1693">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1693">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1694">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1694">tx_semaphore_put</span></span>
- <span data-ttu-id="ff79b-1695">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1695">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_info_get"></a><span data-ttu-id="ff79b-1696">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1696">tx_semaphore_info_get</span></span>

<span data-ttu-id="ff79b-1697">Semafor hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="ff79b-1697">Retrieve information about semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1698">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1698">Prototype</span></span>

```C
UINT tx_semaphore_info_get(TX_SEMAPHORE *semaphore_ptr,
                          CHAR **name, ULONG *current_value,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_SEMAPHORE **next_semaphore)
```
### <a name="description"></a><span data-ttu-id="ff79b-1699">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1699">Description</span></span>

<span data-ttu-id="ff79b-1700">Bu hizmet belirtilen semafor hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1700">This service retrieves information about the specified semaphore.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1701">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1701">Parameters</span></span>

- <span data-ttu-id="ff79b-1702">**semaphore_ptr**: semafor denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1702">**semaphore_ptr**: Pointer to semaphore control block.</span></span>
- <span data-ttu-id="ff79b-1703">**ad**: semafor adının işaretçisinin hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1703">**name**: Pointer to destination for the pointer to the semaphore’s name.</span></span>
- <span data-ttu-id="ff79b-1704">**Current_value**: geçerli semafor sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1704">**current_value**: Pointer to destination for the current semaphore’s count.</span></span>
- <span data-ttu-id="ff79b-1705">**first_suspended**: Bu semaforın askıya alınma listesindeki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1705">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this semaphore.</span></span>
- <span data-ttu-id="ff79b-1706">**suspended_count**: Bu semaforda Şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1706">**suspended_count**: Pointer to destination for the number of threads currently suspended on this semaphore.</span></span>
- <span data-ttu-id="ff79b-1707">**next_semaphore**: sonraki oluşturulan semaforın işaretçisinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1707">**next_semaphore**: Pointer to destination for the pointer of the next created semaphore.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1708">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1708">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1709">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1709">Return Values</span></span>

- <span data-ttu-id="ff79b-1710">**TX_SUCCESS**: (0x00) başarılı semafor bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1710">**TX_SUCCESS**: (0x00) Successful semaphore information retrieval.</span></span>
- <span data-ttu-id="ff79b-1711">TX_SEMAPHORE_ERROR: (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1711">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1712">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1712">Allowed From</span></span>

<span data-ttu-id="ff79b-1713">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1713">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1714">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1714">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1715">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1715">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1716">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1716">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
CHAR         *name;
ULONG        current_value;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_SEMAPHORE *next_semaphore;
UINT         status;

/* Retrieve information about the previously created
   semaphore "my_semaphore." */
status =  tx_semaphore_info_get(&my_semaphore, &name,
                      &current_value,
                      &first_suspended, &suspended_count,
                      &next_semaphore);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1717">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1717">See Also</span></span>

- <span data-ttu-id="ff79b-1718">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1718">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1719">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1719">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1720">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1720">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1721">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1721">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1722">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1722">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1723">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1723">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1724">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1724">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1725">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1725">tx_semaphore_put</span></span>
- <span data-ttu-id="ff79b-1726">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1726">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_info_get"></a><span data-ttu-id="ff79b-1727">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1727">tx_semaphore_performance_info_get</span></span> 

<span data-ttu-id="ff79b-1728">Semafor performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1728">Get semaphore performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1729">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1729">Prototype</span></span>

```C
UINT  tx_semaphore_performance_info_get(TX_SEMAPHORE *semaphore_ptr,
        ULONG *puts, ULONG *gets,
        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-1730">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1730">Description</span></span>

<span data-ttu-id="ff79b-1731">Bu hizmet, belirtilen semafor hakkında performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1731">This service retrieves performance information about the specified semaphore.</span></span>

> [!NOTE]
> <span data-ttu-id="ff79b-1732">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1732">The ThreadX SMP library and application must be built with **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1733">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1733">Parameters</span></span>

- <span data-ttu-id="ff79b-1734">**semaphore_ptr**: daha önce oluşturulan semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1734">**semaphore_ptr**: Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="ff79b-1735">**koyar**: Bu semafor üzerinde gerçekleştirilen put isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1735">**puts**: Pointer to destination for the number of put requests performed on this semaphore.</span></span>
- <span data-ttu-id="ff79b-1736">**Al: Bu** semafor üzerinde gerçekleştirilen GET isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1736">**gets**: Pointer to destination for the number of get requests performed on this semaphore.</span></span>
- <span data-ttu-id="ff79b-1737">**getirilmesi**: Bu semaforda iş parçacığı getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1737">**suspensions**: Pointer to destination for the number of thread suspensions on this semaphore.</span></span>
- <span data-ttu-id="ff79b-1738">**zaman aşımları**: Bu semaforda iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1738">**timeouts**: Pointer to destination for the number of thread suspension timeouts on this semaphore.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1739">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1739">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1740">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1740">Return Values</span></span>

- <span data-ttu-id="ff79b-1741">**TX_SUCCESS**: (0x00) başarılı semafor performansı Get.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1741">**TX_SUCCESS**: (0x00) Successful semaphore performance get.</span></span>
- <span data-ttu-id="ff79b-1742">**TX_PTR_ERROR**: (0x03) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1742">**TX_PTR_ERROR**: (0x03) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="ff79b-1743">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1743">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1744">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1744">Allowed From</span></span>

<span data-ttu-id="ff79b-1745">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1745">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1746">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1746">Example</span></span>

```C
TX_SEMAPHORE     my_semaphore;
ULONG            puts;
ULONG            gets;
ULONG            suspensions;
ULONG            timeouts;

/* Retrieve performance information on the previously created
   semaphore. */
status =  tx_semaphore_performance_info_get(&my_semaphore, &puts,
               &gets, &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1747">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1747">See Also</span></span>

- <span data-ttu-id="ff79b-1748">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1748">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1749">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1749">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1750">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1750">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1751">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1751">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1752">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1752">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1753">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1753">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1754">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1754">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1755">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1755">tx_semaphore_put</span></span>
- <span data-ttu-id="ff79b-1756">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1756">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_system_info_get"></a><span data-ttu-id="ff79b-1757">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1757">tx_semaphore_performance_system_info_get</span></span> 

<span data-ttu-id="ff79b-1758">Semafor sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-1758">Get semaphore system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1759">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1759">Prototype</span></span>

```C
UINT tx_semaphore_performance_system_info_get(ULONG *puts,
       ULONG *gets, ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="ff79b-1760">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1760">Description</span></span>

<span data-ttu-id="ff79b-1761">Bu hizmet sistemdeki tüm Semaforlar hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1761">This service retrieves performance information about all the semaphores in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1762">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1762">The ThreadX SMP library and application must be built with **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1763">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1763">Parameters</span></span>

- <span data-ttu-id="ff79b-1764">**koyar**: tüm Semaforlarda gerçekleştirilen put isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1764">**puts**: Pointer to destination for the total number of put requests performed on all semaphores.</span></span>
- <span data-ttu-id="ff79b-1765">**Al: tüm** Semaforlarda gerçekleştirilen GET isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1765">**gets**: Pointer to destination for the total number of get requests performed on all semaphores.</span></span>
- <span data-ttu-id="ff79b-1766">**getirilmesi**: tüm Semaforlarda toplam iş parçacığı getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1766">**suspensions**: Pointer to destination for the total number of thread suspensions on all semaphores.</span></span>
- <span data-ttu-id="ff79b-1767">**zaman aşımları**: tüm Semaforlarda toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1767">**timeouts**: Pointer to destination for the total number of thread suspension timeouts on all semaphores.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1768">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1768">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1769">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1769">Return Values</span></span>

- <span data-ttu-id="ff79b-1770">TX_SUCCESS: (0x00) başarılı semafor sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1770">TX_SUCCESS: (0x00) Successful semaphore system performance get.</span></span>
- <span data-ttu-id="ff79b-1771">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1771">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1772">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1772">Allowed From</span></span>

<span data-ttu-id="ff79b-1773">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1773">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1774">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1774">Example</span></span>

```C
ULONG         puts;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all previously created
   semaphores. */
status = tx_semaphore_performance_system_info_get(&puts, &gets,
               &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1775">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1775">See Also</span></span>

- <span data-ttu-id="ff79b-1776">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1776">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1777">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1777">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1778">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1778">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1779">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1779">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1780">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1780">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1781">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1781">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1782">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1782">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1783">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1783">tx_semaphore_put</span></span>
- <span data-ttu-id="ff79b-1784">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1784">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_prioritize"></a><span data-ttu-id="ff79b-1785">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1785">tx_semaphore_prioritize</span></span>

<span data-ttu-id="ff79b-1786">Semafor askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="ff79b-1786">Prioritize semaphore suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1787">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1787">Prototype</span></span>

```C
UINT tx_semaphore_prioritize(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1788">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1788">Description</span></span>

<span data-ttu-id="ff79b-1789">Bu hizmet, askıya alma listesinin önündeki semafor örneği için askıya alınan en yüksek öncelik iş parçacığını koyar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1789">This service places the highest priority thread suspended for an instance of the semaphore at the front of the suspension list.</span></span> <span data-ttu-id="ff79b-1790">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1790">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1791">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1791">Parameters</span></span> 

- <span data-ttu-id="ff79b-1792">**semaphore_ptr**: daha önce oluşturulmuş bir semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1792">**semaphore_ptr**: Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1793">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1793">Return Values</span></span>

- <span data-ttu-id="ff79b-1794">**TX_SUCCESS**: (0x00) başarılı semafor önceliği belirleme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1794">**TX_SUCCESS**: (0x00) Successful semaphore prioritize.</span></span>
- <span data-ttu-id="ff79b-1795">TX_SEMAPHORE_ERROR: (0x0C) geçersiz sayma semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1795">TX_SEMAPHORE_ERROR: (0x0C) Invalid counting semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1796">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1796">Allowed From</span></span>

<span data-ttu-id="ff79b-1797">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1797">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1798">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1798">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1799">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1799">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1800">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1800">Example</span></span>

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next instance of this semaphore. */
status =  tx_semaphore_prioritize(&my_semaphore);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_semaphore_put call made to this semaphore will
   wake up this thread. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1801">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1801">See Also</span></span>

- <span data-ttu-id="ff79b-1802">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1802">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1803">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1803">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1804">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1804">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1805">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1805">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1806">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1806">tx_semaphore_put</span></span>

## <a name="tx_semaphore_put"></a><span data-ttu-id="ff79b-1807">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1807">tx_semaphore_put</span></span>

<span data-ttu-id="ff79b-1808">Sayım semafora bir örnek yerleştirme</span><span class="sxs-lookup"><span data-stu-id="ff79b-1808">Place an instance in counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1809">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1809">Prototype</span></span>

```C
UINT tx_semaphore_put(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1810">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1810">Description</span></span>

<span data-ttu-id="ff79b-1811">Bu hizmet, gerçekte belirtilen sayım semafora bir örnek koyar ve bu da gerçekteki sayım semaforu bir tane artırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1811">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1812">Semaforun hepsi (OxFFFFFFFF) olduğunda bu hizmet çağrılırsa, yeni PUT işlemi semaforun sıfıra sıfırlanmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1812">If this service is called when the semaphore is all ones (OxFFFFFFFF), the new put operation will cause the semaphore to be reset to zero.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1813">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1813">Parameters</span></span>

- <span data-ttu-id="ff79b-1814">**semaphore_ptr**: önceden oluşturulan sayım semaforu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1814">**semaphore_ptr**: Pointer to the previously created counting semaphore control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1815">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1815">Return Values</span></span>

- <span data-ttu-id="ff79b-1816">**TX_SUCCESS**: (0x00) başarılı semafor put.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1816">**TX_SUCCESS**: (0x00) Successful semaphore put.</span></span>
- <span data-ttu-id="ff79b-1817">TX_SEMAPHORE_ERROR: (0x0C) semaforu saymak için geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1817">TX_SEMAPHORE_ERROR: (0x0C) Invalid pointer to counting semaphore.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1818">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1818">Allowed From</span></span>

<span data-ttu-id="ff79b-1819">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1819">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1820">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1820">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1821">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1821">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1822">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1822">Example</span></span>

```C
TX_SEMAPHORE     my_semaphore;
UINT             status;

/* Increment the counting semaphore "my_semaphore." */
status =  tx_semaphore_put(&my_semaphore);

/* If status equals TX_SUCCESS, the semaphore count has
   been incremented. Of course, if a thread was waiting,
   it was given the semaphore instance and resumed. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1823">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1823">See Also</span></span>

- <span data-ttu-id="ff79b-1824">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1824">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1825">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1825">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1826">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1826">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1827">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1827">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1828">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1828">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1829">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1829">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1830">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1830">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1831">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1831">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1832">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1832">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_put_notify"></a><span data-ttu-id="ff79b-1833">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1833">tx_semaphore_put_notify</span></span>

<span data-ttu-id="ff79b-1834">Semafor yerleştirayarlandığında uygulamaya bildir</span><span class="sxs-lookup"><span data-stu-id="ff79b-1834">Notify application when semaphore is put</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1835">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1835">Prototype</span></span>

```C
UINT  tx_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr,
        VOID (*semaphore_put_notify)(TX_SEMAPHORE *));
```
### <a name="description"></a><span data-ttu-id="ff79b-1836">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1836">Description</span></span>

<span data-ttu-id="ff79b-1837">Bu hizmet, belirtilen semafor her gerçekleştiğinde çağrılan bir bildirim geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1837">This service registers a notification callback function that is called whenever the specified semaphore is put.</span></span> <span data-ttu-id="ff79b-1838">Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1838">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ff79b-1839">Uygulamanın semafor bildirimi geri çağrısının, askıya alma seçeneği ile herhangi bir ThreadX SMP API çağrısı yapmasına izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1839">The application’s semaphore notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1840">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1840">Parameters</span></span> 

- <span data-ttu-id="ff79b-1841">**semaphore_ptr**: daha önce oluşturulan semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1841">**semaphore_ptr**: Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="ff79b-1842">**semaphore_put_notify**: uygulamanın semafor put bildirimi işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1842">**semaphore_put_notify**: Pointer to application’s semaphore put notification function.</span></span> <span data-ttu-id="ff79b-1843">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1843">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1844">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1844">Return Values</span></span>

- <span data-ttu-id="ff79b-1845">**TX_SUCCESS**: (0x00) semafor put bildiriminin başarılı kaydı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1845">**TX_SUCCESS**: (0x00) Successful registration of semaphore put notification.</span></span>
- <span data-ttu-id="ff79b-1846">TX_SEMAPHORE_ERROR: (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1846">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="ff79b-1847">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1847">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1848">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1848">Allowed From</span></span>

<span data-ttu-id="ff79b-1849">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1849">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1850">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1850">Example</span></span>

```C
TX_SEMAPHORE     my_semaphore;

/* Register the "my_semaphore_put_notify" function for monitoring
   the put operations on the semaphore "my_semaphore." */
status =  tx_semaphore_put_notify(&my_semaphore,
                my_semaphore_put_notify);

/* If status is TX_SUCCESS the semaphore put notification function
   was successfully registered. */

void my_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr)
{
   /* The semaphore was just put! */
}
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1851">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1851">See Also</span></span>

- <span data-ttu-id="ff79b-1852">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1852">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="ff79b-1853">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1853">tx_semaphore_create</span></span>
- <span data-ttu-id="ff79b-1854">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1854">tx_semaphore_delete</span></span>
- <span data-ttu-id="ff79b-1855">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1855">tx_semaphore_get</span></span>
- <span data-ttu-id="ff79b-1856">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1856">tx_semaphore_info_get</span></span>
- <span data-ttu-id="ff79b-1857">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1857">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1858">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1858">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1859">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="ff79b-1859">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="ff79b-1860">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="ff79b-1860">tx_semaphore_put</span></span>

## <a name="tx_thread_create"></a><span data-ttu-id="ff79b-1861">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1861">tx_thread_create</span></span>

<span data-ttu-id="ff79b-1862">Uygulama iş parçacığı oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-1862">Create application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1863">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1863">Prototype</span></span>

```C
UINT tx_thread_create(TX_THREAD *thread_ptr,
                          CHAR *name_ptr, VOID (*entry_function)(ULONG),
                          ULONG entry_input, VOID *stack_start,
                          ULONG stack_size, UINT priority,
                          UINT preempt_threshold, ULONG time_slice,
                          UINT auto_start);
```
### <a name="description"></a><span data-ttu-id="ff79b-1864">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1864">Description</span></span>

<span data-ttu-id="ff79b-1865">Bu hizmet, belirtilen görev girişi işlevinde yürütmeyi Başlatan bir uygulama iş parçacığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1865">This service creates an application thread that starts execution at the specified task entry function.</span></span> <span data-ttu-id="ff79b-1866">Yığın, öncelik, önalım-Threshold ve zaman dilimi, giriş parametreleri tarafından belirtilen özniteliklerin arasındadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1866">The stack, priority, preemption-threshold, and time-slice are among the attributes specified by the input parameters.</span></span> <span data-ttu-id="ff79b-1867">Ayrıca, iş parçacığının ilk yürütme durumu da belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1867">In addition, the initial execution state of the thread is also specified.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1868">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1868">Parameters</span></span>

- <span data-ttu-id="ff79b-1869">**thread_ptr**: iş parçacığı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1869">**thread_ptr**: Pointer to a thread control block.</span></span>
- <span data-ttu-id="ff79b-1870">**name_ptr**: iş parçacığının adına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1870">**name_ptr**: Pointer to the name of the thread.</span></span>
- <span data-ttu-id="ff79b-1871">**entry_function**: iş parçacığı yürütmesi Için ilk C işlevini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1871">**entry_function**: Specifies the initial C function for thread execution.</span></span> <span data-ttu-id="ff79b-1872">Bir iş parçacığı bu giriş işlevinden döndüğünde, tamamlanmış bir duruma konur ve süresiz olarak askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1872">When a thread returns from this entry function, it is placed in a completed state and suspended indefinitely.</span></span>
- <span data-ttu-id="ff79b-1873">**entry_input**: ilk yürütüldüğünde iş parçacığının giriş işlevine geçirilen 32 bitlik bir değer.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1873">**entry_input**: A 32-bit value that is passed to the thread’s entry function when it first executes.</span></span> <span data-ttu-id="ff79b-1874">Bu giriş için kullanım, uygulama tarafından özel olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1874">The use for this input is determined exclusively by the application.</span></span>
- <span data-ttu-id="ff79b-1875">**stack_start**: yığının bellek alanının başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1875">**stack_start**: Starting address of the stack’s memory area.</span></span> 
- <span data-ttu-id="ff79b-1876">**stack_size**: yığın bellek alanındaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1876">**stack_size**: Number bytes in the stack memory area.</span></span> <span data-ttu-id="ff79b-1877">İş parçacığının yığın alanı, en kötü durum işlevi çağrı iç içe ve yerel değişken kullanımını işleyecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1877">The thread’s stack area must be large enough to handle its worst-case function call nesting and local variable usage.</span></span>
- <span data-ttu-id="ff79b-1878">**Öncelik**: iş parçacığının sayısal önceliği.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1878">**priority**: Numerical priority of thread.</span></span> <span data-ttu-id="ff79b-1879">Geçerli değerler 0 ile (TX_MAX_PRIORITES-1) arasındadır; burada 0 değeri, en yüksek önceliği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1879">Legal values range from 0 through (TX_MAX_PRIORITES-1), where a value of 0 represents the highest priority.</span></span>
- <span data-ttu-id="ff79b-1880">**preempt_threshold**: devre dışı önalım en yüksek öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="ff79b-1880">**preempt_threshold**: Highest priority level (0 through (TX_MAX_PRIORITIES-1)) of disabled preemption.</span></span> <span data-ttu-id="ff79b-1881">Bu iş parçacığını yalnızca bu düzeyden daha yüksek öncelikler için izin verilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1881">Only priorities higher than this level are allowed to preempt this thread.</span></span> <span data-ttu-id="ff79b-1882">Bu değer, belirtilen önceliğe eşit veya ondan küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1882">This value must be less than or equal to the specified priority.</span></span> <span data-ttu-id="ff79b-1883">İş parçacığı önceliğine eşit bir değer önalım eşiğini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1883">A value equal to the thread priority disables preemption-threshold.</span></span>
- <span data-ttu-id="ff79b-1884">**time_slice**: Zamanlayıcı sayısı-bu iş parçacığının, aynı önceliğe sahip diğer hazırlık iş parçacıklarından çalıştırılması için çalışmasına izin verilen süre işaretleri.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1884">**time_slice**: Number of timer-ticks this thread is allowed to run before other ready threads of the same priority are given a chance to run.</span></span> <span data-ttu-id="ff79b-1885">Önalım-Threshold kullanmanın zaman dilimini devre dışı bıraktığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1885">Note that using preemption-threshold disables time-slicing.</span></span> <span data-ttu-id="ff79b-1886">Yasal zaman dilimi değerleri 1 ile 0xFFFFFFFF (dahil) arasındadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1886">Legal time-slice values range from 1 to 0xFFFFFFFF (inclusive).</span></span> <span data-ttu-id="ff79b-1887">**TX_NO_TIME_SLICE** değeri (0 değeri), bu iş parçacığının zaman dilimzamanını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1887">A value of **TX_NO_TIME_SLICE** (a value of 0) disables time-slicing of this thread.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ff79b-1888">Zaman dilimletmek, daha hafif bir sistem yükü miktarına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1888">Using time-slicing results in a slight amount of system overhead.</span></span> <span data-ttu-id="ff79b-1889">Zaman dilimi yalnızca birden çok iş parçacığının aynı önceliğe sahip olduğu durumlarda faydalıdır, benzersiz önceliğe sahip iş parçacıkları zaman dilimi atanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1889">Since time-slicing is only useful in cases where multiple threads share the same priority, threads having a unique priority should not be assigned a time-slice.</span></span>

- <span data-ttu-id="ff79b-1890">**auto_start**: iş parçacığının hemen başlatılıp başlatılmayacağını veya askıya alınma durumuna yerleştirilip yerleştirilmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1890">**auto_start**: Specifies whether the thread starts immediately or is placed in a suspended state.</span></span> <span data-ttu-id="ff79b-1891">Yasal seçenekler **TX_AUTO_START** (0x01) ve **TX_DONT_START** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ff79b-1891">Legal options are **TX_AUTO_START** (0x01) and **TX_DONT_START** (0x00).</span></span> <span data-ttu-id="ff79b-1892">TX_DONT_START belirtilirse, uygulamanın iş parçacığının çalışması için daha sonra tx_thread_resume çağırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1892">If TX_DONT_START is specified, the application must later call tx_thread_resume in order for the thread to run.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1893">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1893">Return Values</span></span>

- <span data-ttu-id="ff79b-1894">**TX_SUCCESS**: (0x00) başarılı iş parçacığı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1894">**TX_SUCCESS**: (0x00) Successful thread creation.</span></span>
- <span data-ttu-id="ff79b-1895">TX_THREAD_ERROR: (0x0E) geçersiz iş parçacığı denetim işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1895">TX_THREAD_ERROR: (0x0E) Invalid thread control pointer.</span></span> <span data-ttu-id="ff79b-1896">İşaretçi NULL ya da iş parçacığı zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1896">Either the pointer is NULL or the thread is already created.</span></span>
- <span data-ttu-id="ff79b-1897">TX_PTR_ERROR: (0x03) giriş noktasının başlangıç adresi geçersiz veya yığın alanı geçersiz, genellikle NULL.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1897">TX_PTR_ERROR: (0x03) Invalid starting address of the entry point or the stack area is invalid, usually NULL.</span></span>
- <span data-ttu-id="ff79b-1898">TX_SIZE_ERROR: (0x05) yığın alanının boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1898">TX_SIZE_ERROR: (0x05) Size of stack area is invalid.</span></span> <span data-ttu-id="ff79b-1899">İş parçacıklarının yürütülmesi için en az **TX_MINIMUM_STACK** bayt olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1899">Threads must have at least **TX_MINIMUM_STACK** bytes to execute.</span></span>
- <span data-ttu-id="ff79b-1900">TX_PRIORITY_ERROR: (0x0F) geçersiz iş parçacığı önceliği (0-(TX_MAX_PRIORITIES-1) aralığı dışında bir değer.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1900">TX_PRIORITY_ERROR: (0x0F) Invalid thread priority, which is a value outside the range of (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="ff79b-1901">TX_THRESH_ERROR: (0x18) geçersiz preemptionthreshold belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1901">TX_THRESH_ERROR: (0x18) Invalid preemptionthreshold specified.</span></span> <span data-ttu-id="ff79b-1902">Bu değer, iş parçacığının ilk önceliğine eşit veya ondan küçük geçerli bir öncelik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1902">This value must be a valid priority less than or equal to the initial priority of the thread.</span></span>
- <span data-ttu-id="ff79b-1903">TX_START_ERROR: (0x10) geçersiz otomatik başlatma seçimi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1903">TX_START_ERROR: (0x10) Invalid auto-start selection.</span></span>
- <span data-ttu-id="ff79b-1904">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1904">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1905">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1905">Allowed From</span></span>

<span data-ttu-id="ff79b-1906">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-1906">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1907">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1907">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1908">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-1908">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1909">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1909">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Create a thread of priority 15 whose entry point is
   "my_thread_entry". This thread’s stack area is 1000
   bytes in size, starting at address 0x400000. The
   preemption-threshold is setup to allow preemption of threads
   with priorities ranging from 0 through 14. Time-slicing is
   disabled. This thread is automatically put into a ready
   condition. */
status =  tx_thread_create(&my_thread, "my_thread_name",
                my_thread_entry, 0x1234,
                (VOID *) 0x400000, 1000,
                15, 15, TX_NO_TIME_SLICE,
                TX_AUTO_START);

/* If status equals TX_SUCCESS, my_thread is ready
   for execution! */
...

/* Thread’s entry function. When "my_thread" actually
   begins execution, control is transferred to this
   function. */
VOID my_thread_entry (ULONG initial_input)
{

    /* When we get here, the value of initial_input is
    0x1234. See how this was specified during
    creation. */

    /* The real work of the thread, including calls to
    other function should be called from here! */

    /* When this function returns, the corresponding
    thread is placed into a "completed" state. */
}
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1910">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1910">See Also</span></span>

- <span data-ttu-id="ff79b-1911">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1911">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-1912">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1912">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-1913">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1913">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-1914">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1914">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-1915">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1915">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1916">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1916">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1917">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1917">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-1918">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1918">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-1919">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-1919">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-1920">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-1920">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-1921">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-1921">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-1922">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-1922">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-1923">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1923">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-1924">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-1924">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-1925">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-1925">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-1926">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1926">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-1927">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-1927">tx_thread_wait_abort</span></span>

## <a name="tx_thread_delete"></a><span data-ttu-id="ff79b-1928">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1928">tx_thread_delete</span></span>

<span data-ttu-id="ff79b-1929">Uygulama iş parçacığını Sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-1929">Delete application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1930">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1930">Prototype</span></span>

```C
UINT tx_thread_delete(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-1931">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1931">Description</span></span>

<span data-ttu-id="ff79b-1932">Bu hizmet, belirtilen uygulama iş parçacığını siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1932">This service deletes the specified application thread.</span></span> <span data-ttu-id="ff79b-1933">Belirtilen iş parçacığının sonlandırılmış veya tamamlanmış durumda olması gerektiğinden, bu hizmet kendisini silmeye çalışan bir iş parçacığından çağrılamaz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1933">Since the specified thread must be in a terminated or completed state, this service cannot be called from a thread attempting to delete itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-1934">Bu hizmet tamamlandıktan sonra kullanılabilir olan iş parçacığının yığınında ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1934">It is the application’s responsibility to manage the memory area associated with the thread’s stack, which is available after this service completes.</span></span> <span data-ttu-id="ff79b-1935">Ayrıca, uygulamanın silinen bir iş parçacığının kullanımını önlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1935">In addition, the application must prevent use of a deleted thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1936">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1936">Parameters</span></span>

- <span data-ttu-id="ff79b-1937">**thread_ptr**: daha önce oluşturulmuş bir uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1937">**thread_ptr**: Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1938">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1938">Return Values</span></span>

- <span data-ttu-id="ff79b-1939">**TX_SUCCESS**: (0x00) başarılı iş parçacığı silme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1939">**TX_SUCCESS**: (0x00) Successful thread deletion.</span></span>
- <span data-ttu-id="ff79b-1940">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1940">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-1941">**TX_DELETE_ERROR**: (0x11) belirtilen iş parçacığı sonlandırılmış veya tamamlanmış durumda değil.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1941">**TX_DELETE_ERROR**: (0x11) Specified thread is not in a terminated or completed state.</span></span>
- <span data-ttu-id="ff79b-1942">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1942">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1943">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1943">Allowed From</span></span>

<span data-ttu-id="ff79b-1944">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-1944">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-1945">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-1945">Preemption Possible</span></span>

<span data-ttu-id="ff79b-1946">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-1946">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1947">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1947">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Delete an application thread whose control block is
   "my_thread". Assume that the thread has already been
   created with a call to tx_thread_create. */
status =  tx_thread_delete(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-1948">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1948">See Also</span></span>

- <span data-ttu-id="ff79b-1949">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1949">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-1950">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1950">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-1951">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1951">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-1952">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1952">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-1953">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1953">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1954">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1954">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1955">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1955">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-1956">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1956">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-1957">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-1957">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-1958">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-1958">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-1959">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-1959">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-1960">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-1960">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-1961">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1961">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-1962">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-1962">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-1963">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-1963">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-1964">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1964">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-1965">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-1965">tx_thread_wait_abort</span></span>

## <a name="tx_thread_entry_exit_notify"></a><span data-ttu-id="ff79b-1966">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1966">tx_thread_entry_exit_notify</span></span>

<span data-ttu-id="ff79b-1967">İş parçacığı girdisi ve çıkış sonrasında uygulamayı bilgilendir</span><span class="sxs-lookup"><span data-stu-id="ff79b-1967">Notify application upon thread entry and exit</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-1968">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-1968">Prototype</span></span>

```C
UINT  tx_thread_entry_exit_notify(TX_THREAD *thread_ptr,
        VOID (*entry_exit_notify)(TX_THREAD *, UINT));
```
### <a name="description"></a><span data-ttu-id="ff79b-1969">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-1969">Description</span></span>

<span data-ttu-id="ff79b-1970">Bu hizmet, belirtilen iş parçacığı girildiğinde veya çıktığında çağrılan bir bildirim geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1970">This service registers a notification callback function that is called whenever the specified thread is entered or exits.</span></span> <span data-ttu-id="ff79b-1971">Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1971">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ff79b-1972">Uygulamanın iş parçacığı giriş/çıkış bildirimi geri çağrısının, askıya alma seçeneğiyle herhangi bir ThreadX SMP API çağrısı yapmasına izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1972">The application’s thread entry/exit notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-1973">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-1973">Parameters</span></span>

- <span data-ttu-id="ff79b-1974">**thread_ptr**: daha önce oluşturulmuş iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1974">**thread_ptr**: Pointer to previously created thread.</span></span>
- <span data-ttu-id="ff79b-1975">**entry_exit_notify**: uygulamanın iş parçacığı giriş/çıkış bildirimi işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1975">**entry_exit_notify**: Pointer to application’s thread entry/exit notification function.</span></span> <span data-ttu-id="ff79b-1976">Giriş/çıkış bildirimi işlevinin ikinci parametresi, bir giriş veya çıkış varsa belirler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1976">The second parameter to the entry/exit notification function designates if an entry or exit is present.</span></span> <span data-ttu-id="ff79b-1977">TX_THREAD_ENTRY (0x00) değeri, iş parçacığının girildiğini belirtir, ancak değer TX_THREAD_EXIT (0x01), iş parçacığının çıkış olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1977">The value TX_THREAD_ENTRY (0x00) indicates the thread was entered, while the value TX_THREAD_EXIT (0x01) indicates the thread was exited.</span></span> <span data-ttu-id="ff79b-1978">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1978">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-1979">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-1979">Return Values</span></span>

- <span data-ttu-id="ff79b-1980">**TX_SUCCESS**: (0x00) iş parçacığı giriş/çıkış bildirimi işlevinin başarılı kaydı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1980">**TX_SUCCESS**: (0x00) Successful registration of the thread entry/exit notification function.</span></span>
- <span data-ttu-id="ff79b-1981">TX_THREAD_ERROR: (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1981">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="ff79b-1982">**TX_FEATURE_NOT_ENABLED (0xFF)** Sistem, bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1982">**TX_FEATURE_NOT_ENABLED(0xFF)** The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-1983">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-1983">Allowed From</span></span>

<span data-ttu-id="ff79b-1984">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-1984">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-1985">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-1985">Example</span></span>

```C
TX_THREAD         my_thread;

/* Register the "my_entry_exit_notify" function for monitoring
   the entry/exit of the thread "my_thread." */
status =  tx_thread_entry_exit_notify(&my_thread,
                my_entry_exit_notify);

/* If status is TX_SUCCESS the entry/exit notification function was
   successfully registered. */
void my_entry_exit_notify(TX_THREAD *thread_ptr, UINT condition)
{

    /* Determine if the thread was entered or exited. */
    if (condition == TX_THREAD_ENTRY)
                 /* Thread entry! */
    else if (condition == TX_THREAD_EXIT)
         /* Thread exit! */
}
```

### <a name="see-also"></a><span data-ttu-id="ff79b-1986">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-1986">See Also</span></span>

- <span data-ttu-id="ff79b-1987">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-1987">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-1988">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-1988">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-1989">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1989">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-1990">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-1990">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-1991">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1991">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-1992">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1992">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-1993">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-1993">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-1994">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1994">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-1995">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-1995">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-1996">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-1996">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-1997">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-1997">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-1998">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-1998">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-1999">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-1999">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2000">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2000">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2001">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2001">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2002">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2002">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2003">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2003">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2004">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2004">tx_thread_wait_abort</span></span>

## <a name="tx_thread_identify"></a><span data-ttu-id="ff79b-2005">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2005">tx_thread_identify</span></span>

<span data-ttu-id="ff79b-2006">Şu anda yürütülmekte olan iş parçacığına olan işaretçiyi alır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2006">Retrieves pointer to currently executing thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2007">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2007">Prototype</span></span>

```C
TX_THREAD* tx_thread_identify(VOID);
```
### <a name="description"></a><span data-ttu-id="ff79b-2008">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2008">Description</span></span>

<span data-ttu-id="ff79b-2009">Bu hizmet şu anda yürütülmekte olan iş parçacığına bir işaretçi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2009">This service returns a pointer to the currently executing thread.</span></span> <span data-ttu-id="ff79b-2010">İş parçacığı yürütülerek, bu hizmet null bir işaretçi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2010">If no thread is executing, this service returns a null pointer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2011">Bu hizmet bir ıSR 'den çağrılırsa, dönüş değeri yürütülen kesme işleyicisinden önce çalışan iş parçacığını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2011">If this service is called from an ISR, the return value represents the thread running prior to the executing interrupt handler.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2012">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2012">Parameters</span></span>

<span data-ttu-id="ff79b-2013">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2013">None</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2014">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2014">Return Values</span></span>

- <span data-ttu-id="ff79b-2015">iş parçacığı işaretçisi: Şu anda yürütülmekte olan iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2015">thread pointer: Pointer to the currently executing thread.</span></span> <span data-ttu-id="ff79b-2016">İş parçacığı yürütülerek, dönüş değeri TX_NULL.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2016">If no thread is executing, the return value is TX_NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2017">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2017">Allowed From</span></span>

<span data-ttu-id="ff79b-2018">İş parçacıkları ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2018">Threads and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2019">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2019">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2020">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2020">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2021">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2021">Example</span></span>

```C
TX_THREAD     *my_thread_ptr;

/* Find out who we are! */
my_thread_ptr =  tx_thread_identify();

/* If my_thread_ptr is non-null, we are currently executing
   from that thread or an ISR that interrupted that thread.
   Otherwise, this service was called
   from an ISR when no thread was running when the
   interrupt occurred.  */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2022">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2022">See Also</span></span>

- <span data-ttu-id="ff79b-2023">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2023">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2024">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2024">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2025">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2025">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2026">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2026">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2027">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2027">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2028">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2028">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2029">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2029">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2030">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2030">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2031">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2031">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2032">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2032">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2033">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2033">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2034">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2034">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2035">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2035">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2036">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2036">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2037">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2037">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2038">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2038">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2039">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2039">tx_thread_wait_abort</span></span>

## <a name="tx_thread_info_get"></a><span data-ttu-id="ff79b-2040">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2040">tx_thread_info_get</span></span>

<span data-ttu-id="ff79b-2041">İş parçacığı hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="ff79b-2041">Retrieve information about thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2042">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2042">Prototype</span></span>

```C
UINT tx_thread_info_get(TX_THREAD *thread_ptr, CHAR **name,
                          UINT *state, ULONG *run_count,
                          UINT *priority,
                          UINT *preemption_threshold,
                          ULONG *time_slice,
                          TX_THREAD **next_thread,
                          TX_THREAD **suspended_thread);
```
### <a name="description"></a><span data-ttu-id="ff79b-2043">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2043">Description</span></span>

<span data-ttu-id="ff79b-2044">Bu hizmet, belirtilen iş parçacığı hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2044">This service retrieves information about the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2045">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2045">Parameters</span></span> 

- <span data-ttu-id="ff79b-2046">**thread_ptr**: iş parçacığı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2046">**thread_ptr**: Pointer to thread control block.</span></span>
- <span data-ttu-id="ff79b-2047">**ad**: iş parçacığının adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2047">**name**: Pointer to destination for the pointer to the thread’s name.</span></span>
- <span data-ttu-id="ff79b-2048">**durum**: iş parçacığının geçerli yürütme durumu için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2048">**state**:  Pointer to destination for the thread’s current execution state.</span></span> <span data-ttu-id="ff79b-2049">Olası değerler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ff79b-2049">Possible values are as follows:</span></span>
    - <span data-ttu-id="ff79b-2050">**TX_READY**: (0x00)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2050">**TX_READY**: (0x00)</span></span>
    - <span data-ttu-id="ff79b-2051">**TX_COMPLETED**: (0x01)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2051">**TX_COMPLETED**: (0x01)</span></span>
    - <span data-ttu-id="ff79b-2052">**TX_TERMINATED**: (0x02)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2052">**TX_TERMINATED**: (0x02)</span></span>
    - <span data-ttu-id="ff79b-2053">**TX_SUSPENDED**: (0x03)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2053">**TX_SUSPENDED**: (0x03)</span></span>
    - <span data-ttu-id="ff79b-2054">**TX_SLEEP**: (0x04)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2054">**TX_SLEEP**: (0x04)</span></span>
    - <span data-ttu-id="ff79b-2055">**TX_QUEUE_SUSP**: (0x05)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2055">**TX_QUEUE_SUSP**: (0x05)</span></span>
    - <span data-ttu-id="ff79b-2056">**TX_SEMAPHORE_SUSP**: (0x06)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2056">**TX_SEMAPHORE_SUSP**: (0x06)</span></span>
    - <span data-ttu-id="ff79b-2057">**TX_EVENT_FLAG**: (0x07)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2057">**TX_EVENT_FLAG**: (0x07)</span></span>
    - <span data-ttu-id="ff79b-2058">**TX_BLOCK_MEMORY**: (0x08)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2058">**TX_BLOCK_MEMORY**: (0x08)</span></span>
    - <span data-ttu-id="ff79b-2059">**TX_BYTE_MEMORY**: (0x09)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2059">**TX_BYTE_MEMORY**: (0x09)</span></span>
    - <span data-ttu-id="ff79b-2060">**TX_MUTEX_SUSP**: (0x0D)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2060">**TX_MUTEX_SUSP**: (0x0D)</span></span>

- <span data-ttu-id="ff79b-2061">**run_count**: iş parçacığının çalışma sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2061">**run_count**: Pointer to destination for the thread’s run count.</span></span> 
- <span data-ttu-id="ff79b-2062">**Öncelik**: iş parçacığının önceliği için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2062">**priority**: Pointer to destination for the thread’s priority.</span></span>
- <span data-ttu-id="ff79b-2063">**preemption_threshold**: iş parçacığının önalım-Threshold için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2063">**preemption_threshold**: Pointer to destination for the thread’s preemption-threshold.</span></span>
- <span data-ttu-id="ff79b-2064">**time_slice**: iş parçacığının zaman dilimi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2064">**time_slice**: Pointer to destination for the thread’s time-slice.</span></span> 
- <span data-ttu-id="ff79b-2065">**next_thread**: sonraki oluşturulan iş parçacığı işaretçisinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2065">**next_thread**: Pointer to destination for next created thread pointer.</span></span>
- <span data-ttu-id="ff79b-2066">**suspended_thread**: askıya alma listesindeki bir sonraki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2066">**suspended_thread**: Pointer to destination for pointer to next thread in suspension list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2067">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2067">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2068">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2068">Return Values</span></span>

- <span data-ttu-id="ff79b-2069">**TX_SUCCESS**: (0x00) başarılı iş parçacığı bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2069">**TX_SUCCESS**: (0x00) Successful thread information retrieval.</span></span>
- <span data-ttu-id="ff79b-2070">TX_THREAD_ERROR: (0x0E) geçersiz iş parçacığı denetim işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2070">TX_THREAD_ERROR: (0x0E) Invalid thread control pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2071">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2071">Allowed From</span></span>

<span data-ttu-id="ff79b-2072">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2072">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2073">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2073">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2074">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2074">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2075">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2075">Example</span></span>

```C
TX_THREAD my_thread;
CHAR *name;
UINT state;
ULONG run_count;
UINT priority;
UINT preemption_threshold;
UINT time_slice;
TX_THREAD *next_thread;
TX_THREAD *suspended_thread;
UINT status;

/* Retrieve information about the previously created
   thread "my_thread." */
status =  tx_thread_info_get(&my_thread, &name,
                  &state, &run_count,
            &priority, &preemption_threshold,
                  &time_slice, &next_thread,&suspended_thread);
/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2076">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2076">See Also</span></span>

- <span data-ttu-id="ff79b-2077">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2077">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2078">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2078">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2079">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2079">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2080">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2080">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2081">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2081">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2082">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2082">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2083">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2083">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2084">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2084">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2085">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2085">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2086">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2086">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2087">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2087">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2088">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2088">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2089">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2089">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2090">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2090">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2091">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2091">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2092">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2092">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2093">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2093">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_info_get"></a><span data-ttu-id="ff79b-2094">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2094">tx_thread_performance_info_get</span></span> 

<span data-ttu-id="ff79b-2095">İş parçacığı performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-2095">Get thread performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2096">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2096">Prototype</span></span>

```C
UINT  tx_thread_performance_info_get(TX_THREAD *thread_ptr,
        ULONG *resumptions, ULONG *suspensions,
        ULONG *solicited_preemptions, ULONG *interrupt_preemptions,
        ULONG *priority_inversions, ULONG *time_slices,
        ULONG *relinquishes, ULONG *timeouts, ULONG *wait_aborts,
        TX_THREAD **last_preempted_by);
```
### <a name="description"></a><span data-ttu-id="ff79b-2097">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2097">Description</span></span>

<span data-ttu-id="ff79b-2098">Bu hizmet, belirtilen iş parçacığıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2098">This service retrieves performance information about the specified thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2099">Bu hizmetin performans bilgilerini döndürmesi için ThreadX SMP kitaplığı ve uygulamasının tanımlanmış **TX_THREAD_ENABLE_PERFORMANCE_INFO** ile oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2099">The ThreadX SMP library and application must be built with **TX_THREAD_ENABLE_PERFORMANCE_INFO** defined in order for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2100">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2100">Parameters</span></span> 

- <span data-ttu-id="ff79b-2101">**thread_ptr**: daha önce oluşturulmuş iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2101">**thread_ptr**: Pointer to previously created thread.</span></span>
- <span data-ttu-id="ff79b-2102">**bağlantının sürdürülmesi**: Bu iş parçacığının bağlantının sürdürülmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2102">**resumptions**: Pointer to destination for the number of resumptions of this thread.</span></span>
- <span data-ttu-id="ff79b-2103">**getirilmesi**: Bu iş parçacığının getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2103">**suspensions**: Pointer to destination for the number of suspensions of this thread.</span></span>
- <span data-ttu-id="ff79b-2104">**solicited_preemptions**: Bu iş parçacığı tarafından yapılan bir THREADX API hizmeti çağrısının sonucu olarak, preemptions sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2104">**solicited_preemptions**: Pointer to destination for the number of preemptions as a result of a ThreadX API service call made by this thread.</span></span>
- <span data-ttu-id="ff79b-2105">**interrupt_preemptions**: kesme işlemenin sonucu olarak bu iş parçacığının preemptions sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2105">**interrupt_preemptions**: Pointer to destination for the number of preemptions of this thread as a result of interrupt processing.</span></span>
- <span data-ttu-id="ff79b-2106">**priority_inversions**: Bu iş parçacığının öncelik Inin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2106">**priority_inversions**: Pointer to destination for the number of priority inversions of this thread.</span></span>
- <span data-ttu-id="ff79b-2107">**time_slices**: Bu iş parçacığının zaman içindeki zaman sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2107">**time_slices**: Pointer to destination for the number of timeslices of this thread.</span></span>
- <span data-ttu-id="ff79b-2108">**relinquishes**: Bu iş parçacığı tarafından gerçekleştirilen iş parçacığı relinleri sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2108">**relinquishes**: Pointer to destination for the number of thread relinquishes performed by this thread.</span></span>
- <span data-ttu-id="ff79b-2109">**zaman aşımları**: Bu iş parçacığında askıya alınma zaman aşımları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2109">**timeouts**: Pointer to destination for the number of suspension timeouts on this thread.</span></span>
- <span data-ttu-id="ff79b-2110">**wait_aborts**: Bu iş parçacığında gerçekleştirilen bekleme iptal sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2110">**wait_aborts**: Pointer to destination for the number of wait aborts performed on this thread.</span></span>
- <span data-ttu-id="ff79b-2111">**last_preempted_by**: Bu iş parçacığını en son alan iş parçacığı işaretçisinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2111">**last_preempted_by**: Pointer to destination for the thread pointer that last preempted this thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2112">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2112">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2113">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2113">Return Values</span></span>

- <span data-ttu-id="ff79b-2114">**TX_SUCCESS**: (0x00) başarılı iş parçacığı performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2114">**TX_SUCCESS**: (0x00) Successful thread performance get.</span></span>
- <span data-ttu-id="ff79b-2115">**TX_PTR_ERROR**: (0x03) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2115">**TX_PTR_ERROR**: (0x03) Invalid thread pointer.</span></span>
- <span data-ttu-id="ff79b-2116">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2116">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2117">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2117">Allowed From</span></span>

<span data-ttu-id="ff79b-2118">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2118">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2119">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2119">Example</span></span>

```c
TX_THREAD     my_thread;
ULONG         resumptions;
ULONG         suspensions;
ULONG         solicited_preemptions;
ULONG         interrupt_preemptions;
ULONG         priority_inversions;
ULONG         time_slices;
ULONG         relinquishes;
ULONG         timeouts;
ULONG         wait_aborts;
TX_THREAD     *last_preempted_by;

/* Retrieve performance information on the previously created
   thread. */
status = tx_thread_performance_info_get(&my_thread, &resumptions,
               &suspensions,
               &solicited_preemptions, &interrupt_preemptions,
               &priority_inversions, &time_slices,
               &relinquishes, &timeouts,
               &wait_aborts, &last_preempted_by);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2120">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2120">See Also</span></span>

- <span data-ttu-id="ff79b-2121">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2121">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2122">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2122">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2123">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2123">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2124">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2124">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2125">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2125">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2126">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2126">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2127">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2127">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2128">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2128">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2129">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2129">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2130">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2130">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2131">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2131">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2132">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2132">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2133">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2133">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2134">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2134">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2135">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2135">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2136">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2136">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2137">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2137">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_system_info_get"></a><span data-ttu-id="ff79b-2138">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2138">tx_thread_performance_system_info_get</span></span> 

<span data-ttu-id="ff79b-2139">İş parçacığı sistemi performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-2139">Get thread system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2140">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2140">Prototype</span></span>

```C
UINT tx_thread_performance_system_info_get(ULONG *resumptions,
       ULONG *suspensions, ULONG *solicited_preemptions,
       ULONG *interrupt_preemptions, ULONG *priority_inversions,
       ULONG *time_slices, ULONG *relinquishes, ULONG *timeouts,
       ULONG *wait_aborts, ULONG *non_idle_returns,
       ULONG *idle_returns);
```
### <a name="description"></a><span data-ttu-id="ff79b-2141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2141">Description</span></span>

<span data-ttu-id="ff79b-2142">Bu hizmet, sistemdeki tüm iş parçacıkları hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2142">This service retrieves performance information about all the threads in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2143">Bu hizmetin performans bilgilerini döndürmesi için ThreadX SMP kitaplığı ve uygulamasının tanımlanmış **TX_THREAD_ENABLE_PERFORMANCE_INFO** ile oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2143">The ThreadX SMP library and application must be built with **TX_THREAD_ENABLE_PERFORMANCE_INFO** defined in order for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2144">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2144">Parameters</span></span>

- <span data-ttu-id="ff79b-2145">**bağlantının sürdürülmesi**: toplam iş parçacığı sayısı için hedef işaretçisi bağlantının sürdürülmesi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2145">**resumptions**: Pointer to destination for the total number of thread resumptions.</span></span>
- <span data-ttu-id="ff79b-2146">**getirilmesi**: toplam iş parçacığı sayısı için hedef işaretçisi getirilmesi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2146">**suspensions**: Pointer to destination for the total number of thread suspensions.</span></span>
- <span data-ttu-id="ff79b-2147">**solicited_preemptions**: THREADX API hizmetini çağıran bir iş parçacığının sonucu olarak, toplam iş parçacığı sayısı için hedef işaretçi preemptions.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2147">**solicited_preemptions**: Pointer to destination for the total number of thread preemptions as a result of a thread calling a ThreadX API service.</span></span>
- <span data-ttu-id="ff79b-2148">**interrupt_preemptions**: kesme işlemenin sonucu olarak toplam iş parçacığı sayısı için hedef işaretçi preemptions.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2148">**interrupt_preemptions**: Pointer to destination for the total number of thread preemptions as a result of interrupt processing.</span></span>
- <span data-ttu-id="ff79b-2149">**priority_inversions**: toplam iş parçacığı önceliği ınsürümlerin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2149">**priority_inversions**: Pointer to destination for the total number of thread priority inversions.</span></span>
- <span data-ttu-id="ff79b-2150">**time_slices**: iş parçacığı zaman dilimlerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2150">**time_slices**: Pointer to destination for the total number of thread time-slices.</span></span>
- <span data-ttu-id="ff79b-2151">**relinquishes**: toplam iş parçacığı yeniden sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2151">**relinquishes**: Pointer to destination for the total number of thread relinquishes.</span></span>
- <span data-ttu-id="ff79b-2152">**zaman aşımları**: toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2152">**timeouts**: Pointer to destination for the total number of thread suspension timeouts.</span></span>
- <span data-ttu-id="ff79b-2153">**wait_aborts**: toplam iş parçacığı bekleme sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2153">**wait_aborts**: Pointer to destination for the total number of thread wait aborts.</span></span> 
- <span data-ttu-id="ff79b-2154">**non_idle_returns**: başka bir iş parçacığı yürütülmeye hazırlandığınızda, bir iş parçacığının sisteme kaç kez geri döndüğünü gösteren hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2154">**non_idle_returns**: Pointer to destination for the number of times a thread returns to the system when another thread is ready to execute.</span></span> 
- <span data-ttu-id="ff79b-2155">**idle_returns**: başka bir iş parçacığı yürütülmeye hazırlanmışsa (boştaki sistem), bir iş parçacığının sisteme kaç kez geri döndüğünü gösteren hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2155">**idle_returns**: Pointer to destination for the number of times a thread returns to the system when no other thread is ready to execute (idle system).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2156">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2156">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2157">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2157">Return Values</span></span>

- <span data-ttu-id="ff79b-2158">**TX_SUCCESS**: (0x00) başarılı iş parçacığı sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2158">**TX_SUCCESS**: (0x00) Successful thread system performance get.</span></span>
- <span data-ttu-id="ff79b-2159">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2159">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2160">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2160">Allowed From</span></span>

<span data-ttu-id="ff79b-2161">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2161">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2162">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2162">Example</span></span>

```C
ULONG         resumptions;
ULONG         suspensions;
ULONG         solicited_preemptions;
ULONG         interrupt_preemptions;
ULONG         priority_inversions;
ULONG         time_slices;
ULONG         relinquishes;
ULONG         timeouts;
ULONG         wait_aborts;
ULONG         non_idle_returns;
ULONG         idle_returns;

/* Retrieve performance information on all previously created
   thread. */
status = tx_thread_performance_system_info_get(&resumptions,
                &suspensions,
                &solicited_preemptions, &interrupt_preemptions,
                &priority_inversions, &time_slices, &relinquishes,
                &timeouts, &wait_aborts, &non_idle_returns,
                &idle_returns);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2163">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2163">See Also</span></span>

- <span data-ttu-id="ff79b-2164">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2164">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2165">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2165">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2166">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2166">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2167">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2167">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2168">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2168">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2169">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2169">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2170">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2170">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2171">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2171">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2172">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2172">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2173">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2173">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2174">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2174">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2175">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2175">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2176">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2176">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2177">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2177">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2178">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2178">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2179">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2179">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2180">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2180">tx_thread_wait_abort</span></span>

## <a name="tx_thread_preemption_change"></a><span data-ttu-id="ff79b-2181">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2181">tx_thread_preemption_change</span></span>

<span data-ttu-id="ff79b-2182">Önalım-uygulama iş parçacığının eşiğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="ff79b-2182">Change preemption-threshold of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2183">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2183">Prototype</span></span>

```C
UINT tx_thread_preemption_change(TX_THREAD *thread_ptr,
                          UINT new_threshold, UINT *old_threshold);
```
### <a name="description"></a><span data-ttu-id="ff79b-2184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2184">Description</span></span>

<span data-ttu-id="ff79b-2185">Bu hizmet, belirtilen iş parçacığının önalım eşiğini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2185">This service changes the preemption-threshold of the specified thread.</span></span> <span data-ttu-id="ff79b-2186">Önalım-Threshold, önalım-Threshold değerine eşit veya daha küçük olan iş parçacıkları tarafından belirtilen iş parçacığının önalım ' i engelliyor.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2186">The preemption-threshold prevents preemption of the specified thread by threads equal to or less than the preemption-threshold value.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2187">Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2187">Using preemption-threshold disables time-slicing for the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2188">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2188">Parameters</span></span>

- <span data-ttu-id="ff79b-2189">**thread_ptr**: daha önce oluşturulmuş bir uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2189">**thread_ptr**: Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="ff79b-2190">**new_threshold**: New önalım-Threshold öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="ff79b-2190">**new_threshold**: New preemption-threshold priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="ff79b-2191">**old_threshold**: önceki önalım-Threshold döndürecek konuma yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2191">**old_threshold**: Pointer to a location to return the previous preemption-threshold.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2192">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2192">Return Values</span></span>

- <span data-ttu-id="ff79b-2193">**TX_SUCCESS**: (0x00) başarılı önalım-eşik değişikliği.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2193">**TX_SUCCESS**: (0x00) Successful preemption-threshold change.</span></span>
- <span data-ttu-id="ff79b-2194">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2194">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-2195">**TX_THRESH_ERROR**: (0X18) belirtilen yeni önalım-Threshold geçerli iş parçacığı önceliğine göre geçerli bir iş parçacığı önceliği ((0 ila (TX_MAX_PRIORITIES-1) veya daha büyük (düşük öncelik) değil.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2195">**TX_THRESH_ERROR**: (0x18) Specified new preemption-threshold is not a valid thread priority (a value other than (0 through (TX_MAX_PRIORITIES-1)) or is greater than (lower priority) than the current thread priority.</span></span>
- <span data-ttu-id="ff79b-2196">TX_PTR_ERROR: (0x03) önceki preemptionthreshold depolama konumuna yönelik geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2196">TX_PTR_ERROR: (0x03) Invalid pointer to previous preemptionthreshold storage location.</span></span>
- <span data-ttu-id="ff79b-2197">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2197">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2198">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2198">Allowed From</span></span>

<span data-ttu-id="ff79b-2199">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2199">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2200">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2200">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2201">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2201">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2202">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2202">Example</span></span>

```c
TX_THREAD     my_thread;
UINT          my_old_threshold;
UINT          status;

/* Disable all preemption of the specified thread. The
   current preemption-threshold is returned in
   "my_old_threshold". Assume that "my_thread" has
   already been created. */
status = tx_thread_preemption_change(&my_thread,
                             0, &my_old_threshold);

/* If status equals TX_SUCCESS, the application thread is
   non-preemptable by another thread. Note that ISRs are
   not prevented by preemption disabling. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2203">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2203">See Also</span></span>

- <span data-ttu-id="ff79b-2204">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2204">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2205">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2205">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2206">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2206">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2207">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2207">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2208">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2208">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2209">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2209">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2210">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2210">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2211">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2211">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2212">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2212">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2213">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2213">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2214">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2214">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2215">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2215">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2216">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2216">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2217">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2217">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2218">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2218">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2219">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2219">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2220">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2220">tx_thread_wait_abort</span></span>

## <a name="tx_thread_priority_change"></a><span data-ttu-id="ff79b-2221">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2221">tx_thread_priority_change</span></span>

<span data-ttu-id="ff79b-2222">Uygulama iş parçacığının önceliğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="ff79b-2222">Change priority of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2223">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2223">Prototype</span></span>

```C
UINT tx_thread_priority_change(TX_THREAD *thread_ptr,
                          UINT new_priority, UINT *old_priority);
```
### <a name="description"></a><span data-ttu-id="ff79b-2224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2224">Description</span></span>

<span data-ttu-id="ff79b-2225">Bu hizmet, belirtilen iş parçacığının önceliğini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2225">This service changes the priority of the specified thread.</span></span> <span data-ttu-id="ff79b-2226">Geçerli öncelikler 0 ile (TX_MAX_PRIORITES-1) arasındadır; burada 0 en yüksek öncelik düzeyini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2226">Valid priorities range from 0 through (TX_MAX_PRIORITES-1), where 0 represents the highest priority level.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2227">Belirtilen iş parçacığının önalım-Threshold değeri otomatik olarak yeni önceliğe ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2227">The preemption-threshold of the specified thread is automatically set to the new priority.</span></span> <span data-ttu-id="ff79b-2228">Yeni bir eşik isteniyorsa, **tx_thread_preemption_change** hizmeti bu çağrıdan sonra kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2228">If a new threshold is desired, the **tx_thread_preemption_change** service must be used after this call.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2229">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2229">Parameters</span></span>

- <span data-ttu-id="ff79b-2230">**thread_ptr**: daha önce oluşturulmuş bir uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2230">**thread_ptr**: Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="ff79b-2231">**new_priority**: yeni iş parçacığı öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="ff79b-2231">**new_priority**: New thread priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="ff79b-2232">**old_priority**: iş parçacığının önceki önceliğini döndürmek için bir konuma yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2232">**old_priority**: Pointer to a location to return the thread’s previous priority.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2233">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2233">Return Values</span></span>

- <span data-ttu-id="ff79b-2234">**TX_SUCCESS**: (0x00) başarılı öncelik değişikliği.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2234">**TX_SUCCESS**: (0x00) Successful priority change.</span></span>
- <span data-ttu-id="ff79b-2235">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2235">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-2236">TX_PRIORITY_ERROR: (0x0F) belirtilen yeni öncelik geçerli değil ((0-(TX_MAX_PRIORITIES-1) dışında bir değer).</span><span class="sxs-lookup"><span data-stu-id="ff79b-2236">TX_PRIORITY_ERROR: (0x0F) Specified new priority is not valid (a value other than (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="ff79b-2237">TX_PTR_ERROR: (0x03) önceki öncelikli depolama konumuna yönelik geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2237">TX_PTR_ERROR: (0x03) Invalid pointer to previous priority storage location.</span></span>
- <span data-ttu-id="ff79b-2238">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2238">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2239">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2239">Allowed From</span></span>

<span data-ttu-id="ff79b-2240">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2240">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2241">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2241">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2242">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2242">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2243">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2243">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          my_old_priority;
UINT          status;

/* Change the thread represented by "my_thread" to priority
   0. */
status = tx_thread_priority_change(&my_thread,
                            0, &my_old_priority);

/* If status equals TX_SUCCESS, the application thread is
   now at the highest priority level in the system. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2244">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2244">See Also</span></span>

- <span data-ttu-id="ff79b-2245">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2245">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2246">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2246">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2247">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2247">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2248">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2248">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2249">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2249">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2250">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2250">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2251">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2251">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2252">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2252">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2253">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2253">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2254">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2254">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2255">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2255">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2256">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2256">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2257">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2257">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2258">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2258">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2259">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2259">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2260">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2260">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2261">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2261">tx_thread_wait_abort</span></span>

## <a name="tx_thread_relinquish"></a><span data-ttu-id="ff79b-2262">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2262">tx_thread_relinquish</span></span>

<span data-ttu-id="ff79b-2263">Diğer uygulama iş parçacıklarıyla denetimi yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff79b-2263">Relinquish control to other application threads</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2264">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2264">Prototype</span></span>

```C
VOID tx_thread_relinquish(VOID);
```
### <a name="description"></a><span data-ttu-id="ff79b-2265">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2265">Description</span></span>

<span data-ttu-id="ff79b-2266">Bu hizmet, aynı veya daha yüksek önceliğe sahip başka bir hazırlık iş parçacığına işlemci denetimini yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2266">This service relinquishes processor control to other ready-to-run threads at the same or higher priority.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2267">Aynı önceliğe sahip iş parçacıklarıyla, bu hizmetin aynı önceliğe sahip iş parçacıklarından de daha fazla denetim, geçerli iş parçacığının önalım-Threshold ayarı nedeniyle yürütmenin en yüksek öncelikli iş parçacığına karşı çalışmasını engelledi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2267">In addition to relinquishing control to threads of the same priority, this service also relinquishes control to the highest-priority thread prevented from execution because of the current thread's preemption-threshold setting.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2268">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2268">Parameters</span></span>

<span data-ttu-id="ff79b-2269">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2269">None</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2270">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2270">Return Values</span></span>

<span data-ttu-id="ff79b-2271">Yok</span><span class="sxs-lookup"><span data-stu-id="ff79b-2271">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2272">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2272">Allowed From</span></span>

<span data-ttu-id="ff79b-2273">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-2273">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2274">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2274">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2275">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2275">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2276">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2276">Example</span></span>

```C
ULONG run_counter_1 =  0;
ULONG run_counter_2 =  0;

/* Example of two threads relinquishing control to
   each other in an infinite loop. Assume that
   both of these threads are ready and have the same
   priority. The run counters will always stay within one
   of each other. */

VOID  my_first_thread(ULONG thread_input)
{
    /* Endless loop of relinquish. */
    while(1)
    {

        /* Increment the run counter. */
        run_counter_1++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}

VOID my_second_thread(ULONG thread_input)
{
    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_2++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2277">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2277">See Also</span></span>

- <span data-ttu-id="ff79b-2278">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2278">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2279">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2279">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2280">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2280">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2281">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2281">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2282">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2282">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2283">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2283">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2284">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2284">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2285">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2285">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2286">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2286">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2287">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2287">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2288">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2288">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2289">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2289">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2290">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2290">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2291">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2291">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2292">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2292">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2293">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2293">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2294">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2294">tx_thread_wait_abort</span></span>

## <a name="tx_thread_reset"></a><span data-ttu-id="ff79b-2295">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2295">tx_thread_reset</span></span>

<span data-ttu-id="ff79b-2296">İş parçacığını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="ff79b-2296">Reset thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2297">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2297">Prototype</span></span>

```C
UINT tx_thread_reset(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2298">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2298">Description</span></span>

<span data-ttu-id="ff79b-2299">Bu hizmet, belirtilen iş parçacığını iş parçacığı oluşturma sırasında tanımlanan giriş noktasında yürütülecek şekilde sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2299">This service resets the specified thread to execute at the entry point defined at thread creation.</span></span> <span data-ttu-id="ff79b-2300">İş parçacığı sıfırlanmak için bir **TX_COMPLETED** veya **TX_TERMINATED** durumunda olmalıdır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2300">The thread must be in either a **TX_COMPLETED** or **TX_TERMINATED** state for it to be reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2301">Yeniden yürütülmesi için iş parçacığının sürdürülmeye devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2301">The thread must be resumed for it to execute again.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2302">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2302">Parameters</span></span> 

- <span data-ttu-id="ff79b-2303">**thread_ptr**: daha önce oluşturulmuş bir iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2303">**thread_ptr**: Pointer to a previously created thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2304">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2304">Return Values</span></span>

- <span data-ttu-id="ff79b-2305">**TX_SUCCESS**: (0x00) başarılı iş parçacığı sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2305">**TX_SUCCESS**: (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="ff79b-2306">**TX_NOT_DONE**: (0x20) belirtilen iş parçacığı TX_COMPLETED veya TX_TERMINATED durumunda değil.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2306">**TX_NOT_DONE**: (0x20) Specified thread is not in a TX_COMPLETED or TX_TERMINATED state.</span></span>
- <span data-ttu-id="ff79b-2307">TX_THREAD_ERROR: (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2307">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="ff79b-2308">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2308">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2309">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2309">Allowed From</span></span>

<span data-ttu-id="ff79b-2310">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-2310">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2311">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2311">Example</span></span>

```C
TX_THREAD     my_thread;

/* Reset the previously created thread "my_thread." */
status = tx_thread_reset(&my_thread);

/* If status is TX_SUCCESS the thread is reset. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2312">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2312">See Also</span></span>

- <span data-ttu-id="ff79b-2313">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2313">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2314">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2314">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2315">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2315">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2316">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2316">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2317">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2317">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2318">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2318">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2319">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2319">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2320">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2320">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2321">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2321">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2322">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2322">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2323">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2323">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2324">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2324">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2325">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2325">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2326">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2326">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2327">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2327">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2328">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2328">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2329">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2329">tx_thread_wait_abort</span></span>

## <a name="tx_thread_resume"></a><span data-ttu-id="ff79b-2330">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2330">tx_thread_resume</span></span>

<span data-ttu-id="ff79b-2331">Askıya alınmış uygulama iş parçacığını sürdürür</span><span class="sxs-lookup"><span data-stu-id="ff79b-2331">Resume suspended application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2332">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2332">Prototype</span></span>

```C
UINT tx_thread_resume(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2333">Description</span></span>

<span data-ttu-id="ff79b-2334">Bu hizmet, daha önce bir ***tx_thread_suspend*** çağrısıyla askıya alınmış bir iş parçacığını yürütmeye devam eder veya hazırlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2334">This service resumes or prepares for execution a thread that was previously suspended by a ***tx_thread_suspend*** call.</span></span> <span data-ttu-id="ff79b-2335">Ayrıca, bu hizmet otomatik başlatma olmadan oluşturulan iş parçacıklarını sürdürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2335">In addition, this service resumes threads that were created without an automatic start.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2336">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2336">Parameters</span></span>

- <span data-ttu-id="ff79b-2337">**thread_ptr**: askıya alınmış bir uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2337">**thread_ptr**: Pointer to a suspended application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2338">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2338">Return Values</span></span>

- <span data-ttu-id="ff79b-2339">**TX_SUCCESS**: (0x00) başarılı iş parçacığı özgeçmişi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2339">**TX_SUCCESS**: (0x00) Successful thread resume.</span></span>
- <span data-ttu-id="ff79b-2340">**TX_SUSPEND_LIFTED**: (0x19) daha önce Gecikmeli askıya alma yükseltilmemiş idi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2340">**TX_SUSPEND_LIFTED**: (0x19) Previously set delayed suspension was lifted.</span></span>
- <span data-ttu-id="ff79b-2341">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2341">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-2342">**TX_RESUME_ERROR**: (0x12) belirtilen iş parçacığı askıya alınmaz veya daha önce **_tx_thread_suspend_** dışında bir hizmet tarafından askıya alındı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2342">**TX_RESUME_ERROR**: (0x12) Specified thread is not suspended or was previously suspended by a service other than **_tx_thread_suspend_**.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2343">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2343">Allowed From</span></span>

<span data-ttu-id="ff79b-2344">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2344">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2345">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2345">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2346">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2346">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2347">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2347">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Resume the thread represented by "my_thread". */
status =  tx_thread_resume(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   now ready to execute. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2348">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2348">See Also</span></span>

- <span data-ttu-id="ff79b-2349">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2349">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2350">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2350">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2351">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2351">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2352">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2352">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2353">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2353">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2354">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2354">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2355">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2355">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2356">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2356">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2357">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2357">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2358">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2358">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2359">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2359">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2360">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2360">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2361">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2361">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2362">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2362">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2363">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2363">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2364">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2364">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2365">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2365">tx_thread_wait_abort</span></span>

## <a name="tx_thread_sleep"></a><span data-ttu-id="ff79b-2366">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2366">tx_thread_sleep</span></span>

<span data-ttu-id="ff79b-2367">Belirtilen süre boyunca geçerli iş parçacığını askıya al</span><span class="sxs-lookup"><span data-stu-id="ff79b-2367">Suspend current thread for specified time</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2368">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2368">Prototype</span></span>

```C
UINT tx_thread_sleep(ULONG timer_ticks);
```
### <a name="description"></a><span data-ttu-id="ff79b-2369">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2369">Description</span></span>

<span data-ttu-id="ff79b-2370">Bu hizmet, çağıran iş parçacığının belirtilen sayıda süreölçer onay işareti için askıda olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2370">This service causes the calling thread to suspend for the specified number of timer ticks.</span></span> <span data-ttu-id="ff79b-2371">Süreölçer Tick ile ilişkili fiziksel sürenin miktarı uygulamaya özgüdür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2371">The amount of physical time associated with a timer tick is application specific.</span></span> <span data-ttu-id="ff79b-2372">Bu hizmet, yalnızca bir uygulama iş parçacığından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2372">This service can be called only from an application thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2373">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2373">Parameters</span></span>

- <span data-ttu-id="ff79b-2374">**timer_ticks**: çağıran uygulama iş parçacığını askıya almak için süreölçer onay işaretleri sayısı, 0 ile 0xFFFFFFFF arasında değişir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2374">**timer_ticks**: The number of timer ticks to suspend the calling application thread, ranging from 0 through 0xFFFFFFFF.</span></span> <span data-ttu-id="ff79b-2375">0 belirtilirse, hizmet hemen döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2375">If 0 is specified, the service returns immediately.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2376">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2376">Return Values</span></span>

- <span data-ttu-id="ff79b-2377">**TX_SUCCESS**: (0x00) başarılı iş parçacığı uykusu.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2377">**TX_SUCCESS**: (0x00) Successful thread sleep.</span></span>
- <span data-ttu-id="ff79b-2378">**TX_WAIT_ABORTED**: (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2378">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="ff79b-2379">**TX_CALLER_ERROR**: (0x13) hizmet iş parçacığından çağrıldı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2379">**TX_CALLER_ERROR**: (0x13) Service called from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2380">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2380">Allowed From</span></span>

<span data-ttu-id="ff79b-2381">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-2381">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2382">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2382">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2383">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2383">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2384">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2384">Example</span></span>

```C
UINT status;

/* Make the calling thread sleep for 100
   timer-ticks. */
status = tx_thread_sleep(100);

/* If status equals TX_SUCCESS, the currently running
   application thread slept for the specified number of
   timer-ticks. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2385">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2385">See Also</span></span>

- <span data-ttu-id="ff79b-2386">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2386">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2387">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2387">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2388">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2388">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2389">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2389">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2390">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2390">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2391">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2391">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2392">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2392">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2393">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2393">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2394">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2394">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2395">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2395">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2396">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2396">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2397">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2397">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2398">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2398">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2399">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2399">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2400">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2400">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2401">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2401">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2402">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2402">tx_thread_wait_abort</span></span>

## <a name="tx_thread_smp_core_exclude"></a><span data-ttu-id="ff79b-2403">tx_thread_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="ff79b-2403">tx_thread_smp_core_exclude</span></span>

<span data-ttu-id="ff79b-2404">Bir çekirdek kümesinde iş parçacığı yürütmeyi hariç tutma</span><span class="sxs-lookup"><span data-stu-id="ff79b-2404">Exclude thread execution on a set of cores</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2405">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2405">Prototype</span></span>

```C
UINT  tx_thread_smp_core_exclude(TX_THREAD *thread_ptr,
                          ULONG exclusion_map);
```
### <a name="description"></a><span data-ttu-id="ff79b-2406">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2406">Description</span></span>

<span data-ttu-id="ff79b-2407">Bu işlev, belirtilen iş parçacığını "*exclusion_map*" adlı bit eşlemesinde belirtilen çekirdekler üzerinde yürütmeyi dışlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2407">This function excludes the specified thread from executing on the core(s) specified in the bit map called "*exclusion_map*."</span></span> <span data-ttu-id="ff79b-2408">"*Exclusion_map*" içindeki her bir bit, bir çekirdeği temsil eder (bit 0, Core 0, vb.).</span><span class="sxs-lookup"><span data-stu-id="ff79b-2408">Each bit in "*exclusion_map*" represents a core (bit 0 represents core 0, etc.).</span></span> <span data-ttu-id="ff79b-2409">Bit ayarlandıysa, ilgili çekirdeğin belirtilen iş parçacığını yürütmesi dışında tutulur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2409">If the bit is set, the corresponding core is excluded from executing the specified thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2410">İşlemci dışlamanın kullanımı, en iyi eşleşmeyi bulmak için iş parçacığında temel eşleme mantığına ek işlemeye neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2410">Use of processor exclusion may cause additional processing in the thread to core mapping logic in order to find the optimal match.</span></span> <span data-ttu-id="ff79b-2411">Bu işlem, Ready iş parçacıklarının sayısıyla sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2411">This processing is bounded by the number of ready threads.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2412">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2412">Parameters</span></span> 

- <span data-ttu-id="ff79b-2413">**thread_ptr**: çekirdek dışlamasını değiştirmek için iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2413">**thread_ptr**: Pointer to thread to change the core exclusion.</span></span>
- <span data-ttu-id="ff79b-2414">**exclusion_map**: bir oturbitin, çekirdeğin dışlandığını gösterdiği bit eşlem.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2414">**exclusion_map**: Bit map where a sit bit indicates that that core is excluded.</span></span> <span data-ttu-id="ff79b-2415">0 değeri sağlamak, iş parçacığının herhangi bir çekirdek üzerinde (varsayılan) yürütülmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2415">Supplying a 0 value enables the thread to execute on any core (default).</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2416">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2416">Return Values</span></span>

- <span data-ttu-id="ff79b-2417">TX_SUCCESS: (0x00) başarılı çekirdek dışlama.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2417">TX_SUCCESS: (0x00) Successful core exclusion.</span></span>
- <span data-ttu-id="ff79b-2418">TX_THREAD_ERROR: (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2418">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2419">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2419">Allowed From</span></span>

<span data-ttu-id="ff79b-2420">Başlatma, ISRs, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2420">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2421">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2421">Example</span></span>

```C
/* Exclude core 0 for "Thread 0". */
tx_thread_smp_core_exclude(&thread_0, 0x01);
```

### <a name="see-also"></a><span data-ttu-id="ff79b-2422">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2422">See Also</span></span>

- <span data-ttu-id="ff79b-2423">tx_thread_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2423">tx_thread_smp_core_exclude_get</span></span>
- <span data-ttu-id="ff79b-2424">tx_thread_smp_core_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2424">tx_thread_smp_core_get</span></span>

## <a name="tx_thread_smp_core_exclude_get"></a><span data-ttu-id="ff79b-2425">tx_thread_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2425">tx_thread_smp_core_exclude_get</span></span>

<span data-ttu-id="ff79b-2426">İş parçacığının geçerli çekirdek dışlamasını alır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2426">Gets the thread's current core exclusion</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2427">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2427">Prototype</span></span>

```C
UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr,
                         ULONG *exclusion_map_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2428">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2428">Description</span></span>

<span data-ttu-id="ff79b-2429">Bu işlev, geçerli çekirdek dışlama listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2429">This function returns the current core exclusion list.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2430">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2430">Parameters</span></span>

- <span data-ttu-id="ff79b-2431">**thread_ptr**: çekirdek dışlamanın alınacağı iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2431">**thread_ptr**: Pointer to thread from which to retrieve the core exclusion.</span></span>
- <span data-ttu-id="ff79b-2432">**exclusion_map_ptr**: geçerli çekirdek dışlama bit eşlemesi için hedef.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2432">**exclusion_map_ptr**: Destination for current core exclusion bit map.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2433">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2433">Return Values</span></span>

- <span data-ttu-id="ff79b-2434">TX_SUCCESS: (0x00) iş parçacığının Çekirdek dışlamanın başarıyla alımı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2434">TX_SUCCESS: (0x00) Successful retrieval of thread's core exclusion.</span></span>
- <span data-ttu-id="ff79b-2435">TX_THREAD_ERROR: (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2435">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="ff79b-2436">TX_PTR_ERROR: (0x03) geçersiz dışlama hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2436">TX_PTR_ERROR: (0x03) Invalid exclusion destination pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2437">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2437">Allowed From</span></span>

<span data-ttu-id="ff79b-2438">Başlatma, ISRs, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2438">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2439">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2439">Example</span></span>

```C
ULONGexcluded_cores;
/* Retrieve the core exclusion for "Thread 0". */
tx_thread_smp_core_exclude_get(&thread_0, &excluded_cores);
```

### <a name="see-also"></a><span data-ttu-id="ff79b-2440">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2440">See Also</span></span>

- <span data-ttu-id="ff79b-2441">tx_thread_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="ff79b-2441">tx_thread_smp_core_exclude</span></span>
- <span data-ttu-id="ff79b-2442">tx_thread_smp_core_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2442">tx_thread_smp_core_get</span></span>

## <a name="tx_thread_smp_core_get"></a><span data-ttu-id="ff79b-2443">tx_thread_smp_core_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2443">tx_thread_smp_core_get</span></span>

<span data-ttu-id="ff79b-2444">Çağıranın Şu anda yürütülmekte olan çekirdeğini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-2444">Retrieve currently executing core of caller</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2445">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2445">Prototype</span></span>

```C
UINT  tx_thread_smp_core_get(void);
```
### <a name="description"></a><span data-ttu-id="ff79b-2446">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2446">Description</span></span>

<span data-ttu-id="ff79b-2447">Bu işlev, bu hizmeti yürüten çekirdeğin çekirdek KIMLIĞINI döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2447">This function returns the core ID of the core executing this service.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2448">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2448">Parameters</span></span>

<span data-ttu-id="ff79b-2449">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2449">None</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2450">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2450">Return Values</span></span>

- <span data-ttu-id="ff79b-2451">core_id: Şu anda yürütülmekte olan çekirdeğin KIMLIĞI, (0 ila TX_THREAD_SMP_MAX_CORES-1)</span><span class="sxs-lookup"><span data-stu-id="ff79b-2451">core_id: ID of currently executing core, (0 through TX_THREAD_SMP_MAX_CORES-1)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2452">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2452">Allowed From</span></span>

<span data-ttu-id="ff79b-2453">Başlatma, ISRs, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2453">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2454">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2454">Example</span></span>

```C
UINTcore;
/* Pickup the currently executing core. */
core = tx_thread_smp_core_get();

/* At this point, “core” contains the executing core ID. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2455">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2455">See Also</span></span>

- <span data-ttu-id="ff79b-2456">tx_thread_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="ff79b-2456">tx_thread_smp_core_exclude</span></span>
- <span data-ttu-id="ff79b-2457">tx_thread_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2457">tx_thread_smp_core_exclude_get</span></span>

## <a name="tx_thread_stack_error_notify"></a><span data-ttu-id="ff79b-2458">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2458">tx_thread_stack_error_notify</span></span>

<span data-ttu-id="ff79b-2459">İş parçacığı yığınını kaydet hata bildirimi geri araması</span><span class="sxs-lookup"><span data-stu-id="ff79b-2459">Register thread stack error notification callback</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2460">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2460">Prototype</span></span>

```C
UINT tx_thread_stack_error_notify(VOID (*error_handler)(TX_THREAD *));
```
### <a name="description"></a><span data-ttu-id="ff79b-2461">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2461">Description</span></span>

<span data-ttu-id="ff79b-2462">Bu hizmet, iş parçacığı yığın hatalarını işlemek için bir bildirim geri çağırma işlevi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2462">This service registers a notification callback function for handling thread stack errors.</span></span> <span data-ttu-id="ff79b-2463">ThreadX SMP yürütme sırasında bir iş parçacığı yığını hatası algıladığında, hatayı işlemek için bu bildirim işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2463">When ThreadX SMP detects a thread stack error during execution, it will call this notification function to process the error.</span></span> <span data-ttu-id="ff79b-2464">Hatanın işlenmesi uygulama tarafından tamamen tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2464">Processing of the error is completely defined by the application.</span></span> <span data-ttu-id="ff79b-2465">Sistemin tamamını sıfırlamak için ihlal iş parçacığını askıya almadan herhangi bir şey yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2465">Anything from suspending the violating thread to resetting the entire system may be done.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2466">Bu hizmetin performans bilgilerini döndürmesi için ThreadX SMP kitaplığı, **TX_ENABLE_STACK_CHECKING** tanımlanmış olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2466">The ThreadX SMP library must be built with **TX_ENABLE_STACK_CHECKING** defined in order for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2467">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2467">Parameters</span></span>

- <span data-ttu-id="ff79b-2468">**error_handler**: uygulamanın yığın hata işleme işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2468">**error_handler**: Pointer to application’s stack error handling function.</span></span> <span data-ttu-id="ff79b-2469">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2469">If this value is TX_NULL, the notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2470">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2470">Return Values</span></span>

- <span data-ttu-id="ff79b-2471">**TX_SUCCESS**: (0x00) başarılı iş parçacığı sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2471">**TX_SUCCESS**: (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="ff79b-2472">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2472">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2473">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2473">Allowed From</span></span>

<span data-ttu-id="ff79b-2474">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2474">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2475">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2475">Example</span></span>

```C
void my_stack_error_handler(TX_THREAD *thread_ptr);

/* Register the "my_stack_error_handler" function with ThreadX SMP
   so that thread stack errors can be handled by the application. */
status =  tx_thread_stack_error_notify(my_stack_error_handler);

/* If status is TX_SUCCESS the stack error handler is registered.*/
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2476">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2476">See Also</span></span>

- <span data-ttu-id="ff79b-2477">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2477">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2478">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2478">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2479">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2479">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2480">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2480">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2481">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2481">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2482">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2482">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2483">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2483">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2484">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2484">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2485">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2485">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2486">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2486">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2487">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2487">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2488">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2488">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2489">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2489">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2490">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2490">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2491">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2491">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2492">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2492">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2493">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2493">tx_thread_wait_abort</span></span>

## <a name="tx_thread_suspend"></a><span data-ttu-id="ff79b-2494">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2494">tx_thread_suspend</span></span>

<span data-ttu-id="ff79b-2495">Uygulama iş parçacığını askıya al</span><span class="sxs-lookup"><span data-stu-id="ff79b-2495">Suspend application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2496">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2496">Prototype</span></span>

```C
UINT tx_thread_suspend(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2497">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2497">Description</span></span>

<span data-ttu-id="ff79b-2498">Bu hizmet belirtilen uygulama iş parçacığını askıya alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2498">This service suspends the specified application thread.</span></span> <span data-ttu-id="ff79b-2499">Bir iş parçacığı, kendisini askıya almak için bu hizmeti çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2499">A thread may call this service to suspend itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2500">Belirtilen iş parçacığı başka bir nedenle zaten askıya alınmışsa, önceki askıya alma yükseltilmemiş olana kadar bu askıya alma işlemi dahili olarak tutulur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2500">If the specified thread is already suspended for another reason, this suspension is held internally until the prior suspension is lifted.</span></span> <span data-ttu-id="ff79b-2501">Bu gerçekleştiğinde, belirtilen iş parçacığının koşulsuz olarak askıya alınması gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2501">When that happens, this unconditional suspension of the specified thread is performed.</span></span> <span data-ttu-id="ff79b-2502">Daha fazla koşulsuz askıya alma isteği etkisizdir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2502">Further unconditional suspension requests have no effect.</span></span>

<span data-ttu-id="ff79b-2503">Askıya alındıktan sonra, yeniden yürütmek için iş parçacığının ***tx_thread_resume*** tarafından sürdürülmeye devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2503">After being suspended, the thread must be resumed by ***tx_thread_resume*** to execute again.</span></span>

## <a name="parameters"></a><span data-ttu-id="ff79b-2504">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2504">Parameters</span></span>

- <span data-ttu-id="ff79b-2505">**thread_ptr**: uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2505">**thread_ptr**: Pointer to an application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2506">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2506">Return Values</span></span>

- <span data-ttu-id="ff79b-2507">**TX_SUCCESS**: (0x00) başarılı iş parçacığı askıya alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2507">**TX_SUCCESS**: (0x00) Successful thread suspend.</span></span>
- <span data-ttu-id="ff79b-2508">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2508">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-2509">**TX_SUSPEND_ERROR**: (0x14) belirtilen iş parçacığı sonlandırılmış veya tamamlanmış durumda.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2509">**TX_SUSPEND_ERROR**: (0x14) Specified thread is in a terminated or completed state.</span></span>
- <span data-ttu-id="ff79b-2510">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2510">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2511">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2511">Allowed From</span></span>

<span data-ttu-id="ff79b-2512">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2512">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2513">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2513">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2514">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2514">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2515">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2515">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Suspend the thread represented by "my_thread". */
status = tx_thread_suspend(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   unconditionally suspended. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2516">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2516">See Also</span></span>

- <span data-ttu-id="ff79b-2517">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2517">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2518">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2518">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2519">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2519">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2520">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2520">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2521">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2521">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2522">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2522">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2523">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2523">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2524">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2524">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2525">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2525">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2526">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2526">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2527">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2527">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2528">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2528">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2529">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2529">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2530">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2530">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2531">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2531">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2532">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2532">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2533">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2533">tx_thread_wait_abort</span></span>

## <a name="tx_thread_terminate"></a><span data-ttu-id="ff79b-2534">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2534">tx_thread_terminate</span></span>

<span data-ttu-id="ff79b-2535">Uygulama iş parçacığını sonlandırır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2535">Terminates application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2536">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2536">Prototype</span></span>

```C
UINT tx_thread_terminate(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2537">Description</span></span>

<span data-ttu-id="ff79b-2538">Bu hizmet, iş parçacığının askıya alınmadığına bakılmaksızın belirtilen uygulama iş parçacığını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2538">This service terminates the specified application thread regardless of whether the thread is suspended or not.</span></span> <span data-ttu-id="ff79b-2539">Bir iş parçacığı, kendisini sonlandırmak için bu hizmeti çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2539">A thread may call this service to terminate itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2540">Sonlandırıldıktan sonra, yeniden yürütülmesi için iş parçacığının sıfırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2540">After being terminated, the thread must be reset for it to execute again.</span></span>

> [!WARNING]
> <span data-ttu-id="ff79b-2541">İş parçacığının sonlandırma için uygun bir durumda olduğundan emin olmak uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2541">It is the application's responsibility to ensure the thread is in a state suitable for termination.</span></span> <span data-ttu-id="ff79b-2542">Örneğin, bir iş parçacığı kritik uygulama işlemleri sırasında veya bu tür işlemleri bilinmeyen bir durumda bırakabileceği diğer ara yazılım bileşenleri içinde sonlandırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2542">For example, a thread should not be terminated during critical application processing or inside of other middleware components where it could leave such processing in an unknown state.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2543">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2543">Parameters</span></span>

- <span data-ttu-id="ff79b-2544">**thread_ptr**: uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2544">**thread_ptr**: Pointer to application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2545">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2545">Return Values</span></span>

- <span data-ttu-id="ff79b-2546">**TX_SUCCESS**: (0x00) başarılı iş parçacığı sona erdiriliyor.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2546">**TX_SUCCESS**: (0x00) Successful thread terminate.</span></span>
- <span data-ttu-id="ff79b-2547">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2547">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-2548">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2548">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2549">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2549">Allowed From</span></span>

<span data-ttu-id="ff79b-2550">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2550">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2551">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2551">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2552">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2552">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2553">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2553">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Terminate the thread represented by "my_thread". */
status =  tx_thread_terminate(&my_thread);

/* If status equals TX_SUCCESS, the thread is terminated
   and cannot execute again until it is reset. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2554">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2554">See Also</span></span>

- <span data-ttu-id="ff79b-2555">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2555">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2556">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2556">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2557">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2557">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2558">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2558">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2559">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2559">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2560">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2560">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2561">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2561">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2562">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2562">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2563">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2563">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2564">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2564">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2565">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2565">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2566">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2566">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2567">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2567">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2568">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2568">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2569">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2569">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2570">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2570">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="ff79b-2571">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2571">tx_thread_wait_abort</span></span>

## <a name="tx_thread_time_slice_change"></a><span data-ttu-id="ff79b-2572">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2572">tx_thread_time_slice_change</span></span>

<span data-ttu-id="ff79b-2573">Değişiklik saati-uygulama iş parçacığının dilimi</span><span class="sxs-lookup"><span data-stu-id="ff79b-2573">Changes time-slice of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2574">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2574">Prototype</span></span>

```C
UINT tx_thread_time_slice_change(TX_THREAD *thread_ptr,
                          ULONG new_time_slice, ULONG *old_time_slice);
```
### <a name="description"></a><span data-ttu-id="ff79b-2575">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2575">Description</span></span>

<span data-ttu-id="ff79b-2576">Bu hizmet, belirtilen uygulama iş parçacığının zaman dilimini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2576">This service changes the time-slice of the specified application thread.</span></span> <span data-ttu-id="ff79b-2577">Bir iş parçacığı için zaman dilimi seçme, aynı veya daha yüksek önceliklerin diğer iş parçacıklarının yürütme şansı olması için belirtilen sayıda süreölçer işareti yürütümeyeceğini yöntem.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2577">Selecting a time-slice for a thread insures that it won’t execute more than the specified number of timer ticks before other threads of the same or higher priorities have a chance to execute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2578">Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2578">Using preemption-threshold disables time-slicing for the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2579">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2579">Parameters</span></span>

- <span data-ttu-id="ff79b-2580">**thread_ptr**: uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2580">**thread_ptr**: Pointer to application thread.</span></span>
- <span data-ttu-id="ff79b-2581">**new_time_slice**: yeni zaman dilimi değeri.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2581">**new_time_slice**: New time slice value.</span></span> <span data-ttu-id="ff79b-2582">Yasal değerler 1 ile 0xFFFFFFFF arasında TX_NO_TIME_SLICE ve sayısal değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2582">Legal values include TX_NO_TIME_SLICE and numeric values from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="ff79b-2583">**old_time_slice**: belirtilen iş parçacığının önceki timeslice değerini depolamak için konum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2583">**old_time_slice**: Pointer to location for storing the previous timeslice value of the specified thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2584">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2584">Return Values</span></span>

- <span data-ttu-id="ff79b-2585">**TX_SUCCESS**: (0x00) başarılı zaman dilimi şansı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2585">**TX_SUCCESS**: (0x00) Successful time-slice chance.</span></span>
- <span data-ttu-id="ff79b-2586">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2586">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-2587">TX_PTR_ERROR: (0x03) önceki zaman dilimi depolama konumu işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2587">TX_PTR_ERROR: (0x03) Invalid pointer to previous time-slice storage location.</span></span>
- <span data-ttu-id="ff79b-2588">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2588">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2589">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2589">Allowed From</span></span>

<span data-ttu-id="ff79b-2590">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2590">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2591">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2591">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2592">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2592">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2593">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2593">Example</span></span>

```C
TX_THREAD     my_thread;
ULONG         my_old_time_slice;
UINT          status;

/* Change the time-slice of the thread associated with
   "my_thread" to 20. This will mean that "my_thread"
   can only run for 20 timer-ticks consecutively before
   other threads of equal or higher priority get a chance
   to run. */
status = tx_thread_time_slice_change(&my_thread, 20,
                             &my_old_time_slice);

/* If status equals TX_SUCCESS, the thread’s time-slice
   has been changed to 20 and the previous time-slice is
   in "my_old_time_slice." */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2594">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2594">See Also</span></span>

- <span data-ttu-id="ff79b-2595">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2595">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2596">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2596">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2597">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2597">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2598">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2598">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2599">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2599">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2600">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2600">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2601">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2601">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2602">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2602">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2603">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2603">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2604">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2604">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2605">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2605">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2606">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2606">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2607">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2607">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2608">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2608">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2609">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2609">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2610">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2610">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2611">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2611">tx_thread_wait_abort</span></span>

## <a name="tx_thread_wait_abort"></a><span data-ttu-id="ff79b-2612">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="ff79b-2612">tx_thread_wait_abort</span></span>

<span data-ttu-id="ff79b-2613">Belirtilen iş parçacığını askıya alma işlemini durdur</span><span class="sxs-lookup"><span data-stu-id="ff79b-2613">Abort suspension of specified thread</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2614">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2614">Prototype</span></span>

```C
UINT tx_thread_wait_abort(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="ff79b-2615">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2615">Description</span></span>

<span data-ttu-id="ff79b-2616">Bu hizmet, belirtilen iş parçacığının uyku veya diğer nesne askıya alınma işlemini iptal eder.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2616">This service aborts sleep or any other object suspension of the specified thread.</span></span> <span data-ttu-id="ff79b-2617">Bekleme iptal edildiğinde, iş parçacığının beklediği hizmetten bir TX_WAIT_ABORTED değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2617">If the wait is aborted, a TX_WAIT_ABORTED value is returned from the service that the thread was waiting on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2618">Bu hizmet, tx_thread_suspend hizmeti tarafından yapılan açık askıya alma sürümü oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2618">This service does not release explicit suspension that is made by the tx_thread_suspend service.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2619">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2619">Parameters</span></span>

- <span data-ttu-id="ff79b-2620">**thread_ptr**: daha önce oluşturulmuş bir uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2620">**thread_ptr**: Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2621">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2621">Return Values</span></span>

- <span data-ttu-id="ff79b-2622">**TX_SUCCESS**: (0x00) başarılı iş parçacığı bekleme iptali.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2622">**TX_SUCCESS**: (0x00) Successful thread wait abort.</span></span>
- <span data-ttu-id="ff79b-2623">TX_THREAD_ERROR: (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2623">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="ff79b-2624">**TX_WAIT_ABORT_ERROR**: (0x1B) belirtilen iş parçacığı bekleme durumunda değil.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2624">**TX_WAIT_ABORT_ERROR**: (0x1B) Specified thread is not in a waiting state.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2625">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2625">Allowed From</span></span>

<span data-ttu-id="ff79b-2626">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2626">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2627">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2627">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2628">Yes</span><span class="sxs-lookup"><span data-stu-id="ff79b-2628">Yes</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2629">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2629">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Abort the suspension condition of "my_thread." */
status =  tx_thread_wait_abort(&my_thread);

/* If status equals TX_SUCCESS, the thread is now ready
   again, with a return value showing its suspension
   was aborted (TX_WAIT_ABORTED). */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2630">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2630">See Also</span></span>

- <span data-ttu-id="ff79b-2631">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2631">tx_thread_create</span></span>
- <span data-ttu-id="ff79b-2632">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2632">tx_thread_delete</span></span>
- <span data-ttu-id="ff79b-2633">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2633">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="ff79b-2634">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2634">tx_thread_identify</span></span>
- <span data-ttu-id="ff79b-2635">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2635">tx_thread_info_get</span></span>
- <span data-ttu-id="ff79b-2636">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2636">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2637">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2637">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="ff79b-2638">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2638">tx_thread_preemption_change</span></span>
- <span data-ttu-id="ff79b-2639">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2639">tx_thread_priority_change</span></span>
- <span data-ttu-id="ff79b-2640">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="ff79b-2640">tx_thread_relinquish</span></span>
- <span data-ttu-id="ff79b-2641">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="ff79b-2641">tx_thread_reset</span></span>
- <span data-ttu-id="ff79b-2642">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="ff79b-2642">tx_thread_resume</span></span>
- <span data-ttu-id="ff79b-2643">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="ff79b-2643">tx_thread_sleep</span></span>
- <span data-ttu-id="ff79b-2644">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="ff79b-2644">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="ff79b-2645">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="ff79b-2645">tx_thread_suspend</span></span>
- <span data-ttu-id="ff79b-2646">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2646">tx_thread_terminate</span></span>
- <span data-ttu-id="ff79b-2647">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2647">tx_thread_time_slice_change</span></span>

## <a name="tx_time_get"></a><span data-ttu-id="ff79b-2648">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2648">tx_time_get</span></span>

<span data-ttu-id="ff79b-2649">Geçerli saati alır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2649">Retrieves the current time</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2650">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2650">Prototype</span></span>

```C
ULONG tx_time_get(VOID);
```
### <a name="description"></a><span data-ttu-id="ff79b-2651">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2651">Description</span></span>

<span data-ttu-id="ff79b-2652">Bu hizmet, iç sistem saatinin içeriğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2652">This service returns the contents of the internal system clock.</span></span> <span data-ttu-id="ff79b-2653">Her timertick, iç sistem saatini bir artırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2653">Each timertick increases the internal system clock by one.</span></span> <span data-ttu-id="ff79b-2654">Sistem saati, başlatma sırasında sıfır olarak ayarlanır ve hizmet ***tx_time_set*** belirli bir değere değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2654">The system clock is set to zero during initialization and can be changed to a specific value by the service ***tx_time_set***.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2655">Her Zamanlayıcı-onay her temsil eden gerçek zaman uygulamaya özgüdür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2655">The actual time each timer-tick represents is application specific.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2656">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2656">Parameters</span></span>

<span data-ttu-id="ff79b-2657">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2657">None</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2658">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2658">Return Values</span></span>

- <span data-ttu-id="ff79b-2659">sistem saat işaretleri: iç, ücretsiz çalışan, sistem saatinin değeri.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2659">system clock ticks: Value of the internal, free running, system clock.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2660">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2660">Allowed From</span></span>

<span data-ttu-id="ff79b-2661">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2661">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2662">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2662">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2663">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2663">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2664">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2664">Example</span></span>

```C
ULONG current_time;

/* Pickup the current system time, in timer-ticks. */
current_time =  tx_time_get();

/* Current time now contains a copy of the internal system
   clock. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2665">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2665">See Also</span></span>

- <span data-ttu-id="ff79b-2666">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-2666">tx_time_set</span></span>

## <a name="tx_time_set"></a><span data-ttu-id="ff79b-2667">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="ff79b-2667">tx_time_set</span></span>

<span data-ttu-id="ff79b-2668">Geçerli saati ayarlar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2668">Sets the current time</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2669">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2669">Prototype</span></span>

```C
VOID tx_time_set(ULONG new_time);
```
### <a name="description"></a><span data-ttu-id="ff79b-2670">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2670">Description</span></span>

<span data-ttu-id="ff79b-2671">Bu hizmet, iç sistem saatini belirtilen değere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2671">This service sets the internal system clock to the specified value.</span></span> <span data-ttu-id="ff79b-2672">Her Zamanlayıcı-onay, iç sistem saatini bir artırır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2672">Each timer-tick increases the internal system clock by one.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2673">Her Zamanlayıcı-onay her temsil eden gerçek zaman uygulamaya özgüdür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2673">The actual time each timer-tick represents is application specific.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2674">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2674">Parameters</span></span>

- <span data-ttu-id="ff79b-2675">**new_time**: yeni saat, sistem saatine yerleştirilecek, yasal değerler 0 ile 0xFFFFFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2675">**new_time**: New time to put in the system clock, legal values range from 0 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2676">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2676">Return Values</span></span>

<span data-ttu-id="ff79b-2677">Yok</span><span class="sxs-lookup"><span data-stu-id="ff79b-2677">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2678">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2678">Allowed From</span></span>

<span data-ttu-id="ff79b-2679">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2679">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2680">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2680">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2681">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2681">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2682">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2682">Example</span></span>

```c
/* Set the internal system time to 0x1234. */
tx_time_set(0x1234);

/* Current time now contains 0x1234 until the next timer
   interrupt. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2683">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2683">See Also</span></span>

- <span data-ttu-id="ff79b-2684">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2684">tx_time_get</span></span>

## <a name="tx_timer_activate"></a><span data-ttu-id="ff79b-2685">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2685">tx_timer_activate</span></span>

<span data-ttu-id="ff79b-2686">Uygulama zamanlayıcısını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ff79b-2686">Activate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2687">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2687">Prototype</span></span>

```C
UINT tx_timer_activate(TX_TIMER *timer_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2688">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2688">Description</span></span>

<span data-ttu-id="ff79b-2689">Bu hizmet, belirtilen uygulama zamanlayıcısını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2689">This service activates the specified application timer.</span></span> <span data-ttu-id="ff79b-2690">Aynı anda süresi dolan zamanlayıcılar için geçen süre sonu yordamları, etkinleştirildikleri sırada yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2690">The expiration routines of timers that expire at the same time are executed in the order they were activated.</span></span>

> [!NOTE]
> <span data-ttu-id="ff79b-2691">Zaman aşımına uğradı bir tek bir zamanlayıcının yeniden etkinleştirilmeden önce **tx_timer_change** aracılığıyla sıfırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2691">That an expired one-shot timer must be reset via **tx_timer_change** before it can be activated again.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2692">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2692">Parameters</span></span>

- <span data-ttu-id="ff79b-2693">**timer_ptr**: daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2693">**timer_ptr**: Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2694">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2694">Return Values</span></span>

- <span data-ttu-id="ff79b-2695">**TX_SUCCESS**: (0x00) başarılı uygulama süreölçeri etkinleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2695">**TX_SUCCESS**: (0x00) Successful application timer activation.</span></span>
- <span data-ttu-id="ff79b-2696">**TX_TIMER_ERROR**: (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2696">**TX_TIMER_ERROR**: (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="ff79b-2697">**TX_ACTIVATE_ERROR**: (0x17) Zamanlayıcı zaten etkin veya zaten süresi geçmiş tek bir görüntü süreölçeri.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2697">**TX_ACTIVATE_ERROR**: (0x17) Timer was already active or is a one-shot timer that has already expired.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2698">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2698">Allowed From</span></span>

<span data-ttu-id="ff79b-2699">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2699">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2700">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2700">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2701">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2701">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2702">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2702">Example</span></span>

```C
TX_TIMER     my_timer;
UINT         status;

/* Activate an application timer. Assume that the
   application timer has already been created. */
status = tx_timer_activate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   now active. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2703">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2703">See Also</span></span>

- <span data-ttu-id="ff79b-2704">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2704">tx_timer_change</span></span>
- <span data-ttu-id="ff79b-2705">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2705">tx_timer_create</span></span>
- <span data-ttu-id="ff79b-2706">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2706">tx_timer_deactivate</span></span>
- <span data-ttu-id="ff79b-2707">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2707">tx_timer_delete</span></span>
- <span data-ttu-id="ff79b-2708">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2708">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2709">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2709">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2710">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2710">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_change"></a><span data-ttu-id="ff79b-2711">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2711">tx_timer_change</span></span>

<span data-ttu-id="ff79b-2712">Uygulama zamanlayıcısını değiştirme</span><span class="sxs-lookup"><span data-stu-id="ff79b-2712">Change application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2713">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2713">Prototype</span></span>

```C
UINT tx_timer_change(TX_TIMER *timer_ptr,
                          ULONG initial_ticks, ULONG reschedule_ticks);
```
### <a name="description"></a><span data-ttu-id="ff79b-2714">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2714">Description</span></span>

<span data-ttu-id="ff79b-2715">Bu hizmet, belirtilen uygulama süreölçerinin süre sonu özelliklerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2715">This service changes the expiration characteristics of the specified application timer.</span></span> <span data-ttu-id="ff79b-2716">Bu hizmet çağrılmadan önce zamanlayıcı devre dışı bırakılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2716">The timer must be deactivated prior to calling this service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2717">Zamanlayıcıyı yeniden başlatmak için bu hizmetten sonra **tx_timer_activate** hizmetine bir çağrı yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2717">A call to the **tx_timer_activate** service is required after this service in order to start the timer again.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2718">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2718">Parameters</span></span>

- <span data-ttu-id="ff79b-2719">**timer_ptr**: bir Zamanlayıcı denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2719">**timer_ptr**: Pointer to a timer control block.</span></span>
- <span data-ttu-id="ff79b-2720">**initial_ticks**: Zamanlayıcı süre sonu için başlangıç onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2720">**initial_ticks**: Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="ff79b-2721">Yasal değerler 1 ile 0xFFFFFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2721">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="ff79b-2722">**reschedule_ticks**: ilk sonra tüm süreölçer süre sonları için işaret sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2722">**reschedule_ticks**: Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="ff79b-2723">Bu parametre için bir sıfır, zamanlayıcının tek bir görüntü süreölçeri olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2723">A zero for this parameter makes the timer a one-shot timer.</span></span> <span data-ttu-id="ff79b-2724">Aksi takdirde, düzenli zamanlayıcılar için 1 ile 0xFFFFFFFF arasında geçerli değerler değişir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2724">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ff79b-2725">Zaman aşımına uğradı bir tek bir zamanlayıcının yeniden etkinleştirilmeden önce **tx_timer_change** aracılığıyla sıfırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2725">That an expired one-shot timer must be reset via **tx_timer_change** before it can be activated again.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2726">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2726">Return Values</span></span>

- <span data-ttu-id="ff79b-2727">**TX_SUCCESS**: (0x00) başarılı uygulama süreölçeri değişikliği.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2727">**TX_SUCCESS**: (0x00) Successful application timer change.</span></span>
- <span data-ttu-id="ff79b-2728">TX_TIMER_ERROR: (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2728">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="ff79b-2729">TX_TICK_ERROR: (0x16) ilk Ticks için geçersiz değer (sıfır) sağlandı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2729">TX_TICK_ERROR: (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="ff79b-2730">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2730">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2731">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2731">Allowed From</span></span>

<span data-ttu-id="ff79b-2732">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2732">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2733">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2733">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2734">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2734">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2735">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2735">Example</span></span>

```C
TX_TIMER         my_timer;
UINT             status;

/* Change a previously created and now deactivated timer
   to expire every 50 timer ticks, including the initial
   expiration. */
status =  tx_timer_change(&my_timer,50, 50);

/* If status equals TX_SUCCESS, the specified timer is
   changed to expire every 50 ticks. */

/* Activate the specified timer to get it started again. */
status = tx_timer_activate(&my_timer);
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2736">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2736">See Also</span></span>

- <span data-ttu-id="ff79b-2737">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2737">tx_timer_activate</span></span>
- <span data-ttu-id="ff79b-2738">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2738">tx_timer_create</span></span>
- <span data-ttu-id="ff79b-2739">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2739">tx_timer_deactivate</span></span>
- <span data-ttu-id="ff79b-2740">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2740">tx_timer_delete</span></span>
- <span data-ttu-id="ff79b-2741">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2741">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2742">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2742">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2743">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2743">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_create"></a><span data-ttu-id="ff79b-2744">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2744">tx_timer_create</span></span>

<span data-ttu-id="ff79b-2745">Uygulama süreölçeri oluştur</span><span class="sxs-lookup"><span data-stu-id="ff79b-2745">Create application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2746">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2746">Prototype</span></span>

```C
UINT tx_timer_create(TX_TIMER *timer_ptr, CHAR *name_ptr,
                          VOID (*expiration_function)(ULONG),
                          ULONG expiration_input, ULONG initial_ticks,
                          ULONG reschedule_ticks, UINT auto_activate)
```
### <a name="description"></a><span data-ttu-id="ff79b-2747">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2747">Description</span></span>

<span data-ttu-id="ff79b-2748">Bu hizmet, belirtilen süre sonu işleviyle ve periyodik olarak bir uygulama süreölçeri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2748">This service creates an application timer with the specified expiration function and periodic.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2749">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2749">Parameters</span></span>

- <span data-ttu-id="ff79b-2750">**timer_ptr**: bir Zamanlayıcı denetim bloğunun işaretçisi</span><span class="sxs-lookup"><span data-stu-id="ff79b-2750">**timer_ptr**: Pointer to a timer control block</span></span>
- <span data-ttu-id="ff79b-2751">**name_ptr**: zamanlayıcının adına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2751">**name_ptr**: Pointer to the name of the timer.</span></span>
- <span data-ttu-id="ff79b-2752">**expiration_function**: Zamanlayıcının süresi dolduğunda çağrılacak uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2752">**expiration_function**: Application function to call when the timer expires.</span></span>
- <span data-ttu-id="ff79b-2753">**expiration_input**: Zamanlayıcının süresi dolduğunda sona erme işlevine geçirilecek giriş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2753">**expiration_input**: Input to pass to expiration function when timer expires.</span></span>
- <span data-ttu-id="ff79b-2754">**initial_ticks**: Zamanlayıcı süre sonu için başlangıç onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2754">**initial_ticks**: Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="ff79b-2755">Yasal değerler 1 ile 0xFFFFFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2755">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="ff79b-2756">**reschedule_ticks**: ilk sonra tüm süreölçer süre sonları için işaret sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2756">**reschedule_ticks**: Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="ff79b-2757">Bu parametre için bir sıfır, zamanlayıcının tek bir görüntü süreölçeri olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2757">A zero for this parameter makes the timer a one-shot timer.</span></span> <span data-ttu-id="ff79b-2758">Aksi takdirde, düzenli zamanlayıcılar için 1 ile 0xFFFFFFFF arasında geçerli değerler değişir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2758">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ff79b-2759">Tek bir anlık zamanlayıcı süresi dolduktan sonra, yeniden etkinleştirilmeden önce tx_timer_change aracılığıyla sıfırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2759">After a one-shot timer expires, it must be reset via tx_timer_change before it can be activated again.</span></span>

- <span data-ttu-id="ff79b-2760">**Auto_Activate**: zamanlayıcının oluşturma sırasında otomatik olarak etkinleştirildiğini belirler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2760">**auto_activate**: Determines if the timer is automatically activated during creation.</span></span> <span data-ttu-id="ff79b-2761">Bu değer **TX_AUTO_ACTIVATE** (0x01), süreölçer etkin hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2761">If this value is **TX_AUTO_ACTIVATE** (0x01) the timer is made active.</span></span> <span data-ttu-id="ff79b-2762">Aksi takdirde, **TX_NO_ACTIVATE** (0x00) değeri seçilirse, süreölçer etkin olmayan bir durumda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2762">Otherwise, if the value **TX_NO_ACTIVATE** (0x00) is selected, the timer is created in a non-active state.</span></span> <span data-ttu-id="ff79b-2763">Bu durumda, süreölçer 'in gerçekten başlatılmış olması için sonraki bir **_tx_timer_activate_** hizmet çağrısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2763">In this case, a subsequent **_tx_timer_activate_** service call is necessary to get the timer actually started.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2764">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2764">Return Values</span></span>

- <span data-ttu-id="ff79b-2765">**TX_SUCCESS**: (0x00) uygulama Zamanlayıcı oluşturma işlemi başarılı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2765">**TX_SUCCESS**: (0x00) Successful application timer creation.</span></span>
- <span data-ttu-id="ff79b-2766">TX_TIMER_ERROR: (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2766">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span> <span data-ttu-id="ff79b-2767">İşaretçi NULL ya da süreölçer zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2767">Either the pointer is NULL or the timer is already created.</span></span>
- <span data-ttu-id="ff79b-2768">TX_TICK_ERROR: (0x16) ilk Ticks için geçersiz değer (sıfır) sağlandı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2768">TX_TICK_ERROR: (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="ff79b-2769">TX_ACTIVATE_ERROR: (0x17) geçersiz etkinleştirme seçildi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2769">TX_ACTIVATE_ERROR: (0x17) Invalid activation selected.</span></span>
- <span data-ttu-id="ff79b-2770">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2770">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2771">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2771">Allowed From</span></span>

<span data-ttu-id="ff79b-2772">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-2772">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2773">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2773">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2774">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2774">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2775">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2775">Example</span></span>

```C
TX_TIMER     my_timer;
UINT         status;

/* Create an application timer that executes
   "my_timer_function" after 100 ticks initially and then
   after every 25 ticks. This timer is specified to start
   immediately! */
status =  tx_timer_create(&my_timer,"my_timer_name",
                my_timer_function, 0x1234, 100, 25,
                TX_AUTO_ACTIVATE);

/* If status equals TX_SUCCESS, my_timer_function will
   be called 100 timer ticks later and then called every
   25 timer ticks. Note that the value 0x1234 is passed to
   my_timer_function every time it is called. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2776">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2776">See Also</span></span>

- <span data-ttu-id="ff79b-2777">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2777">tx_timer_activate</span></span>
- <span data-ttu-id="ff79b-2778">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2778">tx_timer_change</span></span>
- <span data-ttu-id="ff79b-2779">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2779">tx_timer_deactivate</span></span>
- <span data-ttu-id="ff79b-2780">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2780">tx_timer_delete</span></span>
- <span data-ttu-id="ff79b-2781">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2781">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2782">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2782">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2783">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2783">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_deactivate"></a><span data-ttu-id="ff79b-2784">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2784">tx_timer_deactivate</span></span>

<span data-ttu-id="ff79b-2785">Uygulama zamanlayıcısını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="ff79b-2785">Deactivate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2786">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2786">Prototype</span></span>

```C
UINT tx_timer_deactivate(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="ff79b-2787">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2787">Description</span></span>

<span data-ttu-id="ff79b-2788">Bu hizmet, belirtilen uygulama zamanlayıcısını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2788">This service deactivates the specified application timer.</span></span> <span data-ttu-id="ff79b-2789">Süreölçer zaten devre dışı bırakılmışsa, bu hizmetin bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2789">If the timer is already deactivated, this service has no effect.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2790">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2790">Parameters</span></span> 

- <span data-ttu-id="ff79b-2791">**timer_ptr**: daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2791">**timer_ptr**: Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2792">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2792">Return Values</span></span>

- <span data-ttu-id="ff79b-2793">**TX_SUCCESS**: (0x00) başarılı uygulama süreölçeri devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2793">**TX_SUCCESS**: (0x00) Successful application timer deactivation.</span></span>
- <span data-ttu-id="ff79b-2794">TX_TIMER_ERROR: (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2794">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2795">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2795">Allowed From</span></span>

<span data-ttu-id="ff79b-2796">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2796">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2797">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2797">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2798">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2798">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2799">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2799">Example</span></span>

```C
TX_TIMER     my_timer;
UINT         status;

/* Deactivate an application timer. Assume that the
   application timer has already been created. */
status =  tx_timer_deactivate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   now deactivated. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2800">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2800">See Also</span></span>

- <span data-ttu-id="ff79b-2801">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2801">tx_timer_activate</span></span>
- <span data-ttu-id="ff79b-2802">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2802">tx_timer_change</span></span>
- <span data-ttu-id="ff79b-2803">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2803">tx_timer_create</span></span>
- <span data-ttu-id="ff79b-2804">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2804">tx_timer_delete</span></span>
- <span data-ttu-id="ff79b-2805">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2805">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2806">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2806">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2807">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2807">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_delete"></a><span data-ttu-id="ff79b-2808">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2808">tx_timer_delete</span></span>

<span data-ttu-id="ff79b-2809">Uygulama zamanlayıcısını Sil</span><span class="sxs-lookup"><span data-stu-id="ff79b-2809">Delete application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2810">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2810">Prototype</span></span>

```C
UINT tx_timer_delete(TX_TIMER *timer_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2811">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2811">Description</span></span>

<span data-ttu-id="ff79b-2812">Bu hizmet, belirtilen uygulama zamanlayıcısını siler.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2812">This service deletes the specified application timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2813">Silinen bir zamanlayıcının kullanımını önleyen uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2813">It is the application’s responsibility to prevent use of a deleted timer.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2814">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2814">Parameters</span></span> 

- <span data-ttu-id="ff79b-2815">**timer_ptr**: daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2815">**timer_ptr**: Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2816">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2816">Return Values</span></span>

- <span data-ttu-id="ff79b-2817">**TX_SUCCESS**: (0x00) başarılı uygulama süreölçeri silme.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2817">**TX_SUCCESS**: (0x00) Successful application timer deletion.</span></span>
- <span data-ttu-id="ff79b-2818">TX_TIMER_ERROR: (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2818">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="ff79b-2819">TX_CALLER_ERROR: (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2819">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2820">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2820">Allowed From</span></span>

<span data-ttu-id="ff79b-2821">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ff79b-2821">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2822">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2822">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2823">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2823">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2824">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2824">Example</span></span>

```c
TX_TIMER     my_timer;
UINT         status;

/* Delete application timer. Assume that the application
   timer has already been created. */
status =  tx_timer_delete(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2825">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2825">See Also</span></span>

- <span data-ttu-id="ff79b-2826">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2826">tx_timer_activate</span></span>
- <span data-ttu-id="ff79b-2827">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2827">tx_timer_change</span></span>
- <span data-ttu-id="ff79b-2828">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2828">tx_timer_create</span></span>
- <span data-ttu-id="ff79b-2829">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2829">tx_timer_deactivate</span></span>
- <span data-ttu-id="ff79b-2830">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2830">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2831">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2831">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2832">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2832">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_info_get"></a><span data-ttu-id="ff79b-2833">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2833">tx_timer_info_get</span></span>

<span data-ttu-id="ff79b-2834">Uygulama süreölçeri hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="ff79b-2834">Retrieve information about an application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2835">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2835">Prototype</span></span>

```C
UINT tx_timer_info_get(TX_TIMER *timer_ptr, CHAR **name,
                          UINT *active, ULONG *remaining_ticks,
                          ULONG *reschedule_ticks,
                          TX_TIMER **next_timer)
```
### <a name="description"></a><span data-ttu-id="ff79b-2836">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2836">Description</span></span>

<span data-ttu-id="ff79b-2837">Bu hizmet, belirtilen uygulama süreölçeri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2837">This service retrieves information about the specified application timer.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2838">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2838">Parameters</span></span>

- <span data-ttu-id="ff79b-2839">**timer_ptr**: daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2839">**timer_ptr**: Pointer to a previously created application timer.</span></span>
- <span data-ttu-id="ff79b-2840">**Name**: zamanlayıcının adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2840">**name**: Pointer to destination for the pointer to the timer’s name.</span></span>
- <span data-ttu-id="ff79b-2841">**etkin**: süreölçer etkin göstergesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2841">**active**: Pointer to destination for the timer active indication.</span></span> <span data-ttu-id="ff79b-2842">Süreölçer devre dışı bırakılırsa veya bu hizmet zamanlayıcının kendisinden çağrılırsa bir TX_FALSE değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2842">If the timer is inactive or this service is called from the timer itself, a TX_FALSE value is returned.</span></span> <span data-ttu-id="ff79b-2843">Aksi takdirde, süreölçer etkin ise bir TX_TRUE değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2843">Otherwise, if the timer is active, a TX_TRUE value is returned.</span></span>
- <span data-ttu-id="ff79b-2844">**remaining_ticks**: Zamanlayıcının süresi dolmadan önce kalan Zamanlayıcı onay işareti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2844">**remaining_ticks**: Pointer to destination for the number of timer ticks left before the timer expires.</span></span>
- <span data-ttu-id="ff79b-2845">**reschedule_ticks**: Bu süreölçeri otomatik olarak yeniden çizelgelemek için kullanılacak süreölçer onay işareti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2845">**reschedule_ticks**: Pointer to destination for the number of timer ticks that will be used to automatically reschedule this timer.</span></span> <span data-ttu-id="ff79b-2846">Değer sıfırsa, süreölçer tek bir çekmeydir ve yeniden planlanmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2846">If the value is zero, then the timer is a one-shot and won’t be rescheduled.</span></span>
- <span data-ttu-id="ff79b-2847">**next_timer**: sonraki oluşturulan uygulama süreölçerinin işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2847">**next_timer**: Pointer to destination for the pointer of the next created application timer.</span></span>

> [!NOTE]
> <span data-ttu-id="ff79b-2848">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2848">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2849">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2849">Return Values</span></span>

- <span data-ttu-id="ff79b-2850">**TX_SUCCESS**: (0x00) başarılı Zamanlayıcı bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2850">**TX_SUCCESS**: (0x00) Successful timer information retrieval.</span></span>
- <span data-ttu-id="ff79b-2851">TX_TIMER_ERROR: (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2851">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2852">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2852">Allowed From</span></span>

<span data-ttu-id="ff79b-2853">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2853">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="ff79b-2854">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="ff79b-2854">Preemption Possible</span></span>

<span data-ttu-id="ff79b-2855">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2855">No</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2856">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2856">Example</span></span>

```C
TX_TIMER     my_timer;
CHAR         *name;
UINT         active;
ULONG        remaining_ticks;
ULONG        reschedule_ticks;
TX_TIMER     *next_timer;
UINT         status;

/* Retrieve information about the previously created
   application timer "my_timer." */
status =  tx_timer_info_get(&my_timer, &name,
                          &active,&remaining_ticks,
                &reschedule_ticks,
                         &next_timer);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2857">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2857">See Also</span></span>

- <span data-ttu-id="ff79b-2858">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2858">tx_timer_activate</span></span>
- <span data-ttu-id="ff79b-2859">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2859">tx_timer_change</span></span>
- <span data-ttu-id="ff79b-2860">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2860">tx_timer_create</span></span>
- <span data-ttu-id="ff79b-2861">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2861">tx_timer_deactivate</span></span>
- <span data-ttu-id="ff79b-2862">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2862">tx_timer_delete</span></span>
- <span data-ttu-id="ff79b-2863">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2863">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2864">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2864">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="ff79b-2865">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2865">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_info_get"></a><span data-ttu-id="ff79b-2866">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2866">tx_timer_performance_info_get</span></span> 

<span data-ttu-id="ff79b-2867">Zamanlayıcı performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-2867">Get timer performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2868">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2868">Prototype</span></span>

```C
UINT  tx_timer_performance_info_get(TX_TIMER *timer_ptr,
        ULONG *activates, ULONG *reactivates,
        ULONG *deactivates, ULONG *expirations,
        ULONG *expiration_adjusts);
```
### <a name="description"></a><span data-ttu-id="ff79b-2869">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2869">Description</span></span>

<span data-ttu-id="ff79b-2870">Bu hizmet, belirtilen uygulama süreölçeri hakkında performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2870">This service retrieves performance information about the specified application timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2871">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_TIMER_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2871">The ThreadX SMP library and application must be built with **TX_TIMER_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2872">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2872">Parameters</span></span> 

- <span data-ttu-id="ff79b-2873">**timer_ptr**: daha önce oluşturulan Zamanlayıcı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2873">**timer_ptr**: Pointer to previously created timer.</span></span>
- <span data-ttu-id="ff79b-2874">**etkinleştirir**: Bu zamanlayıcıda gerçekleştirilen etkinleştirme isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2874">**activates**: Pointer to destination for the number of activation requests performed on this timer.</span></span>
- <span data-ttu-id="ff79b-2875">yeniden **etkinleştirilen**: Bu dönemsel zamanlayıcıda gerçekleştirilen otomatik yeniden etkinleştirme sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2875">**reactivates**: Pointer to destination for the number of automatic reactivations performed on this periodic timer.</span></span>
- <span data-ttu-id="ff79b-2876">**devre dışı bırakır**: Bu zamanlayıcıda gerçekleştirilen devre dışı bırakma isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2876">**deactivates**: Pointer to destination for the number of deactivation requests performed on this timer.</span></span>
- <span data-ttu-id="ff79b-2877">**süre sonu**: Bu zamanlayıcının süre sonu sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2877">**expirations**: Pointer to destination for the number of expirations of this timer.</span></span>
- <span data-ttu-id="ff79b-2878">**expiration_adjusts**: Bu zamanlayıcıda gerçekleştirilen iç süre sonu ayarlamaları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2878">**expiration_adjusts**: Pointer to destination for the number of internal expiration adjustments performed on this timer.</span></span> <span data-ttu-id="ff79b-2879">Bu ayarlamalar, varsayılan Zamanlayıcı listesi boyutundan daha büyük olan zamanlayıcılar için süreölçer kesme işlemi sırasında yapılır (varsayılan süre sonu 32 ' den büyük olan zamanlayıcılar).</span><span class="sxs-lookup"><span data-stu-id="ff79b-2879">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2880">Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2880">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2881">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2881">Return Values</span></span>

- <span data-ttu-id="ff79b-2882">**TX_SUCCESS**: (0x00) başarılı Zamanlayıcı performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2882">**TX_SUCCESS**: (0x00) Successful timer performance get.</span></span>
- <span data-ttu-id="ff79b-2883">**TX_PTR_ERROR**: (0x03) geçersiz süreölçer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2883">**TX_PTR_ERROR**: (0x03) Invalid timer pointer.</span></span>
- <span data-ttu-id="ff79b-2884">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2884">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2885">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2885">Allowed From</span></span>

<span data-ttu-id="ff79b-2886">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2886">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2887">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2887">Example</span></span>

```C
TX_TIMER     my_timer;
ULONG        activates;
ULONG        reactivates;
ULONG        deactivates;
ULONG        expirations;
ULONG        expiration_adjusts;

/* Retrieve performance information on the previously created
   timer.  */
status =  tx_timer_performance_info_get(&my_timer, &activates,
                &reactivates,&deactivates, &expirations,
                &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2888">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2888">See Also</span></span>

- <span data-ttu-id="ff79b-2889">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2889">tx_timer_activate</span></span>
- <span data-ttu-id="ff79b-2890">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2890">tx_timer_change</span></span>
- <span data-ttu-id="ff79b-2891">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2891">tx_timer_create</span></span>
- <span data-ttu-id="ff79b-2892">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2892">tx_timer_deactivate</span></span>
- <span data-ttu-id="ff79b-2893">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2893">tx_timer_delete</span></span>
- <span data-ttu-id="ff79b-2894">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2894">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2895">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2895">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_system_info_get"></a><span data-ttu-id="ff79b-2896">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2896">tx_timer_performance_system_info_get</span></span> 

<span data-ttu-id="ff79b-2897">Zamanlayıcı sistemi performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="ff79b-2897">Get timer system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2898">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2898">Prototype</span></span>

```C
UINT  tx_timer_performance_system_info_get(ULONG *activates,
        ULONG *reactivates, ULONG *deactivates,
        ULONG *expirations, ULONG *expiration_adjusts);
```
### <a name="description"></a><span data-ttu-id="ff79b-2899">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2899">Description</span></span>

<span data-ttu-id="ff79b-2900">Bu hizmet, sistemdeki tüm uygulama zamanlayıcıları hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2900">This service retrieves performance information about all the application timers in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2901">ThreadX SMP kitaplığı ve uygulaması, performans bilgilerini döndürmek üzere bu hizmetin tanımladığı **TX_TIMER_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2901">The ThreadX SMP library and application must be built with **TX_TIMER_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2902">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2902">Parameters</span></span>

- <span data-ttu-id="ff79b-2903">**etkinleştirir**: tüm zamanlayıcılar üzerinde gerçekleştirilen etkinleştirme isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2903">**activates**: Pointer to destination for the total number of activation requests performed on all timers.</span></span>
- <span data-ttu-id="ff79b-2904">yeniden **etkinleştirilen**: tüm düzenli zamanlayıcıların toplam otomatik yeniden etkinleştirme sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2904">**reactivates**: Pointer to destination for the total number of automatic reactivation performed on all periodic timers.</span></span>
- <span data-ttu-id="ff79b-2905">**devre dışı bırakır**: tüm zamanlayıcılar üzerinde gerçekleştirilen devre dışı bırakma isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2905">**deactivates**: Pointer to destination for the total number of deactivation requests performed on all timers.</span></span>
- <span data-ttu-id="ff79b-2906">**süre sonu**: tüm zamanlayıcılar üzerindeki toplam süre sonu sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2906">**expirations**: Pointer to destination for the total number of expirations on all timers.</span></span>
- <span data-ttu-id="ff79b-2907">**expiration_adjusts**: tüm zamanlayıcılar üzerinde gerçekleştirilen iç süre sonu ayarlamaları toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2907">**expiration_adjusts**: Pointer to destination for the total number of internal expiration adjustments performed on all timers.</span></span> <span data-ttu-id="ff79b-2908">Bu ayarlamalar, varsayılan Zamanlayıcı listesi boyutundan daha büyük olan zamanlayıcılar için süreölçer kesme işlemi sırasında yapılır (varsayılan süre sonu 32 ' den büyük olan zamanlayıcılar).</span><span class="sxs-lookup"><span data-stu-id="ff79b-2908">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2909">Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2909">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2910">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2910">Return Values</span></span>

- <span data-ttu-id="ff79b-2911">**TX_SUCCESS**: (0x00) başarılı Zamanlayıcı sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2911">**TX_SUCCESS**: (0x00) Successful timer system performance get.</span></span>
- <span data-ttu-id="ff79b-2912">**TX_FEATURE_NOT_ENABLED**: (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2912">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2913">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2913">Allowed From</span></span>

<span data-ttu-id="ff79b-2914">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ff79b-2914">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2915">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2915">Example</span></span>

```C
ULONG     activates;
ULONG     reactivates;
ULONG     deactivates;
ULONG     expirations;
ULONG     expiration_adjusts;

/* Retrieve performance information on all previously created
   timers.  */
status =  tx_timer_performance_system_info_get(&activates,
                &reactivates, &deactivates, &expirations,
                &expiration_adjusts);
/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2916">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2916">See Also</span></span>

- <span data-ttu-id="ff79b-2917">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2917">tx_timer_activate</span></span>
- <span data-ttu-id="ff79b-2918">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="ff79b-2918">tx_timer_change</span></span>
- <span data-ttu-id="ff79b-2919">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="ff79b-2919">tx_timer_create</span></span>
- <span data-ttu-id="ff79b-2920">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="ff79b-2920">tx_timer_deactivate</span></span>
- <span data-ttu-id="ff79b-2921">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="ff79b-2921">tx_timer_delete</span></span>
- <span data-ttu-id="ff79b-2922">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2922">tx_timer_info_get</span></span>
- <span data-ttu-id="ff79b-2923">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2923">tx_timer_performance_info_get</span></span>

## <a name="tx_timer_smp_core_exclude"></a><span data-ttu-id="ff79b-2924">tx_timer_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="ff79b-2924">tx_timer_smp_core_exclude</span></span>

<span data-ttu-id="ff79b-2925">Bir çekirdek kümesinde süreölçer yürütmeyi hariç tutma</span><span class="sxs-lookup"><span data-stu-id="ff79b-2925">Exclude timer execution on a set of cores</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2926">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2926">Prototype</span></span>

```C
UINT  tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);
```
### <a name="description"></a><span data-ttu-id="ff79b-2927">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2927">Description</span></span>

<span data-ttu-id="ff79b-2928">Bu işlev, belirtilen süreölçeri "*exclusion_map*" adlı bit eşlemesinde belirtilen çekirdekler üzerinde yürütmeyi dışlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2928">This function excludes the specified timer from executing on the core(s) specified in the bit map called "*exclusion_map*."</span></span> <span data-ttu-id="ff79b-2929">"*Exclusion_map*" içindeki her bir bit, bir çekirdeği temsil eder (bit 0, Core 0, vb.).</span><span class="sxs-lookup"><span data-stu-id="ff79b-2929">Each bit in "*exclusion_map*" represents a core (bit 0 represents core 0, etc.).</span></span> <span data-ttu-id="ff79b-2930">Bit ayarlandıysa, ilgili çekirdek belirtilen zamanlayıcının yürütülmesi dışında tutulur.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2930">If the bit is set, the corresponding core is excluded from executing the specified timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff79b-2931">İşlemci dışlamanın kullanımı, en iyi eşleşmeyi bulmak için iş parçacığında temel eşleme mantığına ek işlemeye neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2931">Use of processor exclusion may cause additional processing in the thread to core mapping logic in order to find the optimal match.</span></span> <span data-ttu-id="ff79b-2932">Bu işlem, Ready iş parçacıklarının sayısıyla sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2932">This processing is bounded by the number of ready threads.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2933">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2933">Parameters</span></span>

- <span data-ttu-id="ff79b-2934">**timer_ptr**: çekirdek dışlamasını değiştirmek için süreölçer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2934">**timer_ptr**: Pointer to timer to change the core exclusion.</span></span>
- <span data-ttu-id="ff79b-2935">**exclusion_map**: bir oturbitin, çekirdeğin dışlandığını gösterdiği bit eşlem.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2935">**exclusion_map**: Bit map where a sit bit indicates that that core is excluded.</span></span> <span data-ttu-id="ff79b-2936">0 değeri sağlamak, zamanlayıcının herhangi bir çekirdek üzerinde (varsayılan) yürütülmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2936">Supplying a 0 value enables the timer to execute on any core (default).</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2937">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2937">Return Values</span></span>

- <span data-ttu-id="ff79b-2938">**TX_SUCCESS** (0x00) başarılı çekirdek dışlama.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2938">**TX_SUCCESS** (0x00) Successful core exclusion.</span></span>
- <span data-ttu-id="ff79b-2939">**TX_TIMER_ERROR** (0x0E) geçersiz süreölçer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2939">**TX_TIMER_ERROR** (0x0E) Invalid timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2940">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2940">Allowed From</span></span>

<span data-ttu-id="ff79b-2941">Başlatma, ISRs, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2941">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2942">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2942">Example</span></span>

```C
/* Exclude core 0 for "Timer 0". */
tx_timer_smp_core_exclude(&timer_0, 0x01);
```

### <a name="see-also"></a><span data-ttu-id="ff79b-2943">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2943">See Also</span></span>

- <span data-ttu-id="ff79b-2944">tx_timer_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2944">tx_timer_smp_core_exclude_get</span></span>

## <a name="tx_timer_smp_core_exclude_get"></a><span data-ttu-id="ff79b-2945">tx_timer_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="ff79b-2945">tx_timer_smp_core_exclude_get</span></span>

<span data-ttu-id="ff79b-2946">Zamanlayıcının geçerli çekirdek dışlamasını alır</span><span class="sxs-lookup"><span data-stu-id="ff79b-2946">Gets the timer's current core exclusion</span></span>

### <a name="prototype"></a><span data-ttu-id="ff79b-2947">Prototype</span><span class="sxs-lookup"><span data-stu-id="ff79b-2947">Prototype</span></span>

```C
UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr,
                         ULONG *exclusion_map_ptr);
```
### <a name="description"></a><span data-ttu-id="ff79b-2948">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff79b-2948">Description</span></span>

<span data-ttu-id="ff79b-2949">Bu işlev, geçerli çekirdek dışlama listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2949">This function returns the current core exclusion list.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff79b-2950">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ff79b-2950">Parameters</span></span>

- <span data-ttu-id="ff79b-2951">**timer_ptr**: çekirdek dışlamanın alınacağı zamanlayıcıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2951">**timer_ptr**: Pointer to timer from which to retrieve the core exclusion.</span></span>
- <span data-ttu-id="ff79b-2952">**exclusion_map_ptr**: geçerli çekirdek dışlama bit eşlemesi için hedef.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2952">**exclusion_map_ptr**: Destination for current core exclusion bit map.</span></span>

### <a name="return-values"></a><span data-ttu-id="ff79b-2953">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ff79b-2953">Return Values</span></span>

- <span data-ttu-id="ff79b-2954">TX_SUCCESS: (0x00) zamanlayıcının çekirdek dışlamasını başarıyla alma.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2954">TX_SUCCESS: (0x00) Successful retrieval of timer's core exclusion.</span></span>
- <span data-ttu-id="ff79b-2955">TX_TIMER_ERROR: (0x0E) geçersiz süreölçer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2955">TX_TIMER_ERROR: (0x0E) Invalid timer pointer.</span></span>
- <span data-ttu-id="ff79b-2956">TX_PTR_ERROR: (0x03) geçersiz dışlama hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2956">TX_PTR_ERROR: (0x03) Invalid exclusion destination pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ff79b-2957">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ff79b-2957">Allowed From</span></span>

<span data-ttu-id="ff79b-2958">Başlatma, ISRs, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff79b-2958">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="ff79b-2959">Örnek</span><span class="sxs-lookup"><span data-stu-id="ff79b-2959">Example</span></span>

```C
ULONGexcluded_cores;

/* Retrieve the core exclusion for "Timer 0". */
tx_timer_smp_core_exclude_get(&timer_0,&excluded_cores);
```
### <a name="see-also"></a><span data-ttu-id="ff79b-2960">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ff79b-2960">See Also</span></span>

- <span data-ttu-id="ff79b-2961">tx_timer_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="ff79b-2961">tx_timer_smp_core_exclude</span></span>