---
title: Bölüm 6-Azure RTOS ThreadX izleme olayları
description: Bu bölümde, Azure RTOS ThreadX olayları açıklanmaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 8f0ff03d112597371059d925f64b7511454e123c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827556"
---
# <a name="chapter-6---azure-rtos-threadx-trace-events"></a><span data-ttu-id="d0679-103">Bölüm 6-Azure RTOS ThreadX izleme olayları</span><span class="sxs-lookup"><span data-stu-id="d0679-103">Chapter 6 - Azure RTOS ThreadX trace events</span></span>

<span data-ttu-id="d0679-104">Bu bölümde, Azure RTOS ThreadX olayları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0679-104">This chapter describes the Azure RTOS ThreadX events.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="d0679-105">Olay ve simgelerin listesi</span><span class="sxs-lookup"><span data-stu-id="d0679-105">List of Events and Icons</span></span>

<span data-ttu-id="d0679-106">Aşağıda, TraceX tarafından görünen ThreadX olaylarının listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0679-106">The following is a list of ThreadX events displayed by TraceX:</span></span>

| <span data-ttu-id="d0679-107">**Simge**</span><span class="sxs-lookup"><span data-stu-id="d0679-107">**Icon**</span></span>                         | <span data-ttu-id="d0679-108">**Anlamı**</span><span class="sxs-lookup"><span data-stu-id="d0679-108">**Meaning**</span></span> |
| -------------------------------- | ------------------------------------- |
| ![İç iş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image1.png)    | <span data-ttu-id="d0679-110">İç iş parçacığı özgeçmişi</span><span class="sxs-lookup"><span data-stu-id="d0679-110">Internal thread resume</span></span>  |
| ![İç iş parçacığı askıya alma simgesi](./media/user-guide/tx-events/image2.png)    | <span data-ttu-id="d0679-112">İç iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="d0679-112">Internal thread suspend</span></span> |
| ![Kesme hizmeti yordamı giriş simgesi](./media/user-guide/tx-events/image3.png)    | <span data-ttu-id="d0679-114">Kesme hizmeti yordamı (ıSR) ENTER</span><span class="sxs-lookup"><span data-stu-id="d0679-114">Interrupt Service Routine (ISR) Enter</span></span> |
| ![Kesme hizmeti yordamı çıkış simgesi](./media/user-guide/tx-events/image4.png)    | <span data-ttu-id="d0679-116">Kesme hizmeti yordamı (ıSR) çıkış</span><span class="sxs-lookup"><span data-stu-id="d0679-116">Interrupt Service Routine (ISR) Exit</span></span>  |
| ![İç zaman dilimi simgesi](./media/user-guide/tx-events/image5.png)    | <span data-ttu-id="d0679-118">İç zaman dilimi</span><span class="sxs-lookup"><span data-stu-id="d0679-118">Internal time-slice</span></span> |
| ![Çalışma simgesi](./media/user-guide/tx-events/image6.png)    | <span data-ttu-id="d0679-120">Çalışma</span><span class="sxs-lookup"><span data-stu-id="d0679-120">Running</span></span> |
| ![Blok havuz ayırma simgesi](./media/user-guide/tx-events/image7.png)    | <span data-ttu-id="d0679-122">**Havuz ayırmayı engelle** (*tx_block_allocate*)</span><span class="sxs-lookup"><span data-stu-id="d0679-122">**Block pool allocate** (*tx_block_allocate*)</span></span>  |
| ![Blok Havuzu Oluştur simgesi](./media/user-guide/tx-events/image8.png)    | <span data-ttu-id="d0679-124">**Havuz oluşturmayı engelle** (*tx_block_pool_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-124">**Block pool create** (*tx_block_pool_create*)</span></span> |
| ![Blok havuzunu silme simgesi](./media/user-guide/tx-events/image9.png)    | <span data-ttu-id="d0679-126">**Blok havuzunu silme** (*tx_block_pool_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-126">**Block pool delete** (*tx_block_pool_delete*)</span></span> |
| ![Havuz bilgilerini engelle al simgesi](./media/user-guide/tx-events/image10.png)    | <span data-ttu-id="d0679-128">**Havuz bilgilerini engelle al** (*tx_block_pool_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-128">**Block pool information get** (*tx_block_pool_info_get*)</span></span> |
| ![Blok havuzu performans bilgileri Get con](./media/user-guide/tx-events/image11.png)    | <span data-ttu-id="d0679-130">**Blok havuzu performans bilgileri Get** (*tx_block_pool_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-130">**Block pool performance information get** (*tx_block_pool_performance_info_get*)</span></span> |
| ![Blok havuzu sistem performans bilgileri al simgesi](./media/user-guide/tx-events/image12.png)    | <span data-ttu-id="d0679-132">**Blok havuzu sistem performans bilgileri Get** (*tx_block_pool_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-132">**Block pool system performance information get** (*tx_block_pool_performance_system_info_get*)</span></span> |
| ![Blok havuzu öncelik simgeleri simgesi](./media/user-guide/tx-events/image13.png)    | <span data-ttu-id="d0679-134">**Blok havuzu önceliklerini belirleme** (*tx_block_pool_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="d0679-134">**Block pool prioritize** (*tx_block_pool_prioritize*)</span></span> |
| ![Havuz simgesine yayını engelle](./media/user-guide/tx-events/image14.png)    | <span data-ttu-id="d0679-136">**Havuza yayını engelle** (*tx_block_release*)</span><span class="sxs-lookup"><span data-stu-id="d0679-136">**Block release to pool** (*tx_block_release*)</span></span> |
| ![Bayt havuzu bellek ayırma simgesi](./media/user-guide/tx-events/image15.png)    | <span data-ttu-id="d0679-138">**Bayt havuzu bellek ayırır** (*tx_byte_allocate*)</span><span class="sxs-lookup"><span data-stu-id="d0679-138">**Byte pool allocate memory** (*tx_byte_allocate*)</span></span> |
| ![Bayt havuzu oluşturma simgesi](./media/user-guide/tx-events/image16.png)    | <span data-ttu-id="d0679-140">**Bayt havuzu oluşturma** (*tx_byte_pool_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-140">**Byte pool create** (*tx_byte_pool_create*)</span></span> |
| ![Bayt havuzu silme simgesi](./media/user-guide/tx-events/image17.png)    | <span data-ttu-id="d0679-142">**Bayt havuzu silme** (*tx_byte_pool_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-142">**Byte pool delete** (*tx_byte_pool_delete*)</span></span> |
| ![Bayt havuzu bilgileri al simgesi](./media/user-guide/tx-events/image18.png)    | <span data-ttu-id="d0679-144">**Bayt havuzu bilgileri Get** (*tx_byte_pool_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-144">**Byte pool information get** (*tx_byte_pool_info_get*)</span></span> |
| ![Bayt havuzu performans bilgileri al simgesi](./media/user-guide/tx-events/image19.png)    | <span data-ttu-id="d0679-146">**Bayt havuzu performans bilgilerine al** (*tx_byte_pool_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-146">**Byte pool performance information get** (*tx_byte_pool_performance_info_get*)</span></span> |
| ![Bayt havuzu sistem performans bilgileri al simgesi](./media/user-guide/tx-events/image20.png)    | <span data-ttu-id="d0679-148">**Bayt havuzu sistem performansı bilgileri al** (*tx_byte_pool_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-148">**Byte pool system performance information get** (*tx_byte_pool_performance_system_info_get*)</span></span> |
| ![\* Bayt havuzu öncelik simgeleri simgesi](./media/user-guide/tx-events/image21.png)    | <span data-ttu-id="d0679-150">**Bayt havuzu önceliklerini belirleme** (*tx_byte_pool_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="d0679-150">**Byte pool prioritize** (*tx_byte_pool_prioritize*)</span></span> |
| ![Havuza bayt bellek yayını simgesi](./media/user-guide/tx-events/image22.png)    | <span data-ttu-id="d0679-152">**Havuza bayt bellek yayını** (*tx_byte_release*)</span><span class="sxs-lookup"><span data-stu-id="d0679-152">**Byte memory release to pool** (*tx_byte_release*)</span></span> |
| ![Olay bayrakları Oluştur simgesi](./media/user-guide/tx-events/image23.png)    | <span data-ttu-id="d0679-154">**Olay bayrakları oluştur** (*tx_event_flags_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-154">**Event flags create** (*tx_event_flags_create*)</span></span> |
| ![Olay bayrakları silme simgesi](./media/user-guide/tx-events/image24.png)    | <span data-ttu-id="d0679-156">**Olay bayrakları silme** (*tx_event_flags_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-156">**Event flags delete** (*tx_event_flags_delete*)</span></span> |
| ![Olay bayrakları al simgesi](./media/user-guide/tx-events/image25.png)    | <span data-ttu-id="d0679-158">**Olay bayrakları al** (*tx_event_flags_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-158">**Event flags get** (*tx_event_flags_get*)</span></span> |
| ![Olay bayrakları bilgileri al simgesi](./media/user-guide/tx-events/image26.png)    | <span data-ttu-id="d0679-160">**Olay bayrakları bilgileri Get** (*tx_event_flags_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-160">**Event flags information get** (*tx_event_flags_info_get*)</span></span> |
| ![Olay bayrakları performans bilgileri al simgesi](./media/user-guide/tx-events/image27.png)    | <span data-ttu-id="d0679-162">**Olay bayrakları performans bilgileri Get** (*tx_event_flags_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-162">**Event flags performance information get** (*tx_event_flags_performance_info_get*)</span></span> |
| ![Olay bayrakları sistem performans bilgileri al simgesi](./media/user-guide/tx-events/image28.png)    | <span data-ttu-id="d0679-164">**Olay bayrakları sistem performans bilgileri al** (*tx_event_flags_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-164">**Event flags system performance information get** (*tx_event_flags_performance_system_info_get*)</span></span> |
| ![Olay bayrakları kümesi simgesi](./media/user-guide/tx-events/image29.png)    | <span data-ttu-id="d0679-166">**Olay bayrak kümesi** (*tx_event_flags_set*)</span><span class="sxs-lookup"><span data-stu-id="d0679-166">**Event flags set** (*tx_event_flags_set*)</span></span> |
| ![Olay bayrakları ayarlama bildirim simgesi](./media/user-guide/tx-events/image30.png)    | <span data-ttu-id="d0679-168">**Olay bayrak kümesi bildir** (*tx_event_flags_set_notify*)</span><span class="sxs-lookup"><span data-stu-id="d0679-168">**Event flags set notify** (*tx_event_flags_set_notify*)</span></span> |
| ![Kesmeyi etkinleştir/devre dışı bırak simgesi](./media/user-guide/tx-events/image31.png)    | <span data-ttu-id="d0679-170">**Kesme etkinleştir/devre dışı bırak** (*tx_interrupt_control*)</span><span class="sxs-lookup"><span data-stu-id="d0679-170">**Interrupt enable/disable** (*tx_interrupt_control*)</span></span> |
| ![Mutex Oluştur simgesi](./media/user-guide/tx-events/image32.png)    | <span data-ttu-id="d0679-172">**Mutex oluşturma** (*tx_mutex_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-172">**Mutex create** (*tx_mutex_create*)</span></span> |
| ![Mutex silme simgesi](./media/user-guide/tx-events/image33.png)    | <span data-ttu-id="d0679-174">**Mutex silme** (*tx_mutex_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-174">**Mutex delete** (*tx_mutex_delete*)</span></span> |
| ![Mutex al simgesi](./media/user-guide/tx-events/image34.png)    | <span data-ttu-id="d0679-176">**Mutex Get** (*tx_mutex_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-176">**Mutex get** (*tx_mutex_get*)</span></span> |
| ![Mutex bilgileri al simgesi](./media/user-guide/tx-events/image35.png)    | <span data-ttu-id="d0679-178">**Mutex bilgileri al** (*tx_mutex_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-178">**Mutex information get** (*tx_mutex_info_get*)</span></span> |
| ![Mutex performans bilgileri al simgesi](./media/user-guide/tx-events/image36.png)    | <span data-ttu-id="d0679-180">**Mutex performans bilgileri Get** (*tx_mutex_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-180">**Mutex performance information get** (*tx_mutex_performance_info_get*)</span></span> |
| ![Mutex sistem performansı bilgileri al simgesi](./media/user-guide/tx-events/image37.png)    | <span data-ttu-id="d0679-182">**Mutex sistem performansı bilgileri Get** (*tx_mutex_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-182">**Mutex system performance information get** (*tx_mutex_performance_system_info_get*)</span></span> |
| ![Mutex öncelik simgesi](./media/user-guide/tx-events/image38.png)    | <span data-ttu-id="d0679-184">**Mutex önceliği** (*tx_mutex_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="d0679-184">**Mutex prioritize** (*tx_mutex_prioritize*)</span></span> |
| ![Mutex put simgesi](./media/user-guide/tx-events/image39.png)    | <span data-ttu-id="d0679-186">**Mutex put** (*tx_mutex_put*)</span><span class="sxs-lookup"><span data-stu-id="d0679-186">**Mutex put** (*tx_mutex_put*)</span></span> |
| ![Kuyruk Oluştur simgesi](./media/user-guide/tx-events/image40.png)    | <span data-ttu-id="d0679-188">**Sıra oluşturma** (*tx_queue_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-188">**Queue create** (*tx_queue_create*)</span></span> |
| ![Kuyruk silme simgesi](./media/user-guide/tx-events/image41.png)    | <span data-ttu-id="d0679-190">**Kuyruk silme** (*tx_queue_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-190">**Queue delete** (*tx_queue_delete*)</span></span> |
| ![Kuyruğu Temizleme simgesi](./media/user-guide/tx-events/image42.png)    | <span data-ttu-id="d0679-192">**Kuyruğu Temizleme** (*tx_queue_flush*)</span><span class="sxs-lookup"><span data-stu-id="d0679-192">**Queue flush** (*tx_queue_flush*)</span></span> |
| ![Kuyruk ön Gönder simgesi](./media/user-guide/tx-events/image43.png)    | <span data-ttu-id="d0679-194">**Kuyruk ön gönderme** (*tx_queue_front_send*)</span><span class="sxs-lookup"><span data-stu-id="d0679-194">**Queue front send** (*tx_queue_front_send*)</span></span> |
| ![Kuyruk bilgileri alma simgesi](./media/user-guide/tx-events/image44.png)    | <span data-ttu-id="d0679-196">**Kuyruk bilgileri alma** (*tx_queue_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-196">**Queue information get** (*tx_queue_info_get*)</span></span> |
| ![Sıra performans bilgileri alma simgesi](./media/user-guide/tx-events/image45.png)    | <span data-ttu-id="d0679-198">**Performans bilgilerini sıraya al** (*tx_queue_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-198">**Queue performance information get** (*tx_queue_performance_info_get*)</span></span> |
| ![Sistem performans bilgilerini sıraya alma simgesi](./media/user-guide/tx-events/image46.png)    | <span data-ttu-id="d0679-200">**Sistem performans bilgilerini sıraya al** (*tx_queue_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-200">**Queue system performance information get** (*tx_queue_performance_system_info_get*)</span></span> |
| ![Sıra önceliği belirleme simgesi](./media/user-guide/tx-events/image47.png)    | <span data-ttu-id="d0679-202">**Sıra önceliklerini belirleme** (*tx_queue_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="d0679-202">**Queue prioritize** (*tx_queue_prioritize*)</span></span> |
| ![Kuyruk alma iletisi simgesi](./media/user-guide/tx-events/image48.png)    | <span data-ttu-id="d0679-204">**Kuyruk alma iletisi** (*tx_queue_receive*)</span><span class="sxs-lookup"><span data-stu-id="d0679-204">**Queue receive message** (*tx_queue_receive*)</span></span> |
| ![Kuyruk iletisi gönder simgesi](./media/user-guide/tx-events/image49.png)    | <span data-ttu-id="d0679-206">**Kuyruk gönderme iletisi** (*tx_queue_send*)</span><span class="sxs-lookup"><span data-stu-id="d0679-206">**Queue send message** (*tx_queue_send*)</span></span> |
| ![Kuyruk gönder bildirim simgesi](./media/user-guide/tx-events/image50.png)    | <span data-ttu-id="d0679-208">**Kuyruk gönderme bildirimi** (*tx_queue_send_notify*)</span><span class="sxs-lookup"><span data-stu-id="d0679-208">**Queue send notify** (*tx_queue_send_notify*)</span></span> |
| ![Semafor tavan koyma simgesi](./media/user-guide/tx-events/image51.png)    | <span data-ttu-id="d0679-210">**Semafor tavan yerleştirme** (*tx_semaphore_ceiling_put*)</span><span class="sxs-lookup"><span data-stu-id="d0679-210">**Semaphore ceiling put** (*tx_semaphore_ceiling_put*)</span></span> |
| ![Semafor Oluştur simgesi](./media/user-guide/tx-events/image52.png)    | <span data-ttu-id="d0679-212">**Semafor oluşturma** (*tx_semaphore_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-212">**Semaphore create** (*tx_semaphore_create*)</span></span> |
| ![Semafor silme simgesi](./media/user-guide/tx-events/image53.png)    | <span data-ttu-id="d0679-214">**Semafor silme** (*tx_semaphore_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-214">**Semaphore delete** (*tx_semaphore_delete*)</span></span> |
| ![Semafor al simgesi](./media/user-guide/tx-events/image54.png)    | <span data-ttu-id="d0679-216">**Semafor al** (*tx_semaphore_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-216">**Semaphore get** (*tx_semaphore_get*)</span></span> |
| ![Semafor bilgileri al simgesi](./media/user-guide/tx-events/image55.png)    | <span data-ttu-id="d0679-218">**Semafor bilgileri al** (*tx_semaphore_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-218">**Semaphore information get** (*tx_semaphore_info_get*)</span></span> |
| ![Semafor performans bilgileri al simgesi](./media/user-guide/tx-events/image56.png)    | <span data-ttu-id="d0679-220">**Semafor performans bilgileri Get** (*tx_semaphroe_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-220">**Semaphore performance information get** (*tx_semaphroe_performance_info_get*)</span></span> |
| ![Semafor sistem performansı bilgileri al simgesi](./media/user-guide/tx-events/image57.png)    | <span data-ttu-id="d0679-222">**Semafor sistem performansı bilgileri Get** (*tx_semaphore_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-222">**Semaphore system performance information get** (*tx_semaphore_performance_system_info_get*)</span></span> |
| ![Semafor önceliği belirleme simgesi](./media/user-guide/tx-events/image58.png)    | <span data-ttu-id="d0679-224">**Semafor önceliklerini belirleme** (*tx_semaphore_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="d0679-224">**Semaphore prioritize** (*tx_semaphore_prioritize*)</span></span> |
| ![Semafor put simgesi](./media/user-guide/tx-events/image59.png)    | <span data-ttu-id="d0679-226">**Semafor put** (*tx_semaphore_put*)</span><span class="sxs-lookup"><span data-stu-id="d0679-226">**Semaphore put** (*tx_semaphore_put*)</span></span> |
| ![Semafor put bildirim simgesi](./media/user-guide/tx-events/image60.png)    | <span data-ttu-id="d0679-228">**Semafor put bildirimi** (*tx_semaphore_put_notify*)</span><span class="sxs-lookup"><span data-stu-id="d0679-228">**Semaphore put notify** (*tx_semaphore_put_notify*)</span></span> |
| ![İş parçacığı Oluştur simgesi](./media/user-guide/tx-events/image61.png)    | <span data-ttu-id="d0679-230">**Iş parçacığı oluşturma** (*tx_thread_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-230">**Thread create** (*tx_thread_create*)</span></span> |
| ![İş parçacığı silme simgesi](./media/user-guide/tx-events/image62.png)    | <span data-ttu-id="d0679-232">**Iş parçacığı silme** (*tx_thread_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-232">**Thread delete** (*tx_thread_delete*)</span></span> |
| ![İş parçacığı çıkış/giriş bildirim simgesi](./media/user-guide/tx-events/image63.png)    | <span data-ttu-id="d0679-234">**Iş parçacığı çıkış/giriş bildirimi** (*tx_thread_entry_exit_notify*)</span><span class="sxs-lookup"><span data-stu-id="d0679-234">**Thread exit/entry notify** (*tx_thread_entry_exit_notify*)</span></span> |
| ![İş parçacığı tanımla simgesi](./media/user-guide/tx-events/image64.png)    | <span data-ttu-id="d0679-236">**Iş parçacığı tanımla** (*tx_thread_identify*)</span><span class="sxs-lookup"><span data-stu-id="d0679-236">**Thread identify** (*tx_thread_identify*)</span></span> |
| ![İş parçacığı bilgileri al simgesi](./media/user-guide/tx-events/image65.png)    | <span data-ttu-id="d0679-238">**Iş parçacığı bilgileri al** (*tx_thread_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-238">**Thread information get** (*tx_thread_info_get*)</span></span> |
| ![İş parçacığı performans bilgileri al simgesi](./media/user-guide/tx-events/image66.png)    | <span data-ttu-id="d0679-240">**Iş parçacığı performans bilgileri al** (*tx_thread_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-240">**Thread performance information get** (*tx_thread_performance_info_get*)</span></span> |
| ![İş parçacığı performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image67.png)    | <span data-ttu-id="d0679-242">**Iş parçacığı performansı sistem bilgileri al** (*tx_thread_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-242">**Thread performance system information get** (*tx_thread_performance_system_info_get*)</span></span> |
| ![İş parçacığı önalım Değiştir simgesi](./media/user-guide/tx-events/image68.png)    | <span data-ttu-id="d0679-244">**Iş parçacığı önalım değişikliği** (*tx_thread_preemption_change*)</span><span class="sxs-lookup"><span data-stu-id="d0679-244">**Thread preemption change** (*tx_thread_preemption_change*)</span></span> |
| ![İş parçacığı önceliği değişikliği simgesi](./media/user-guide/tx-events/image69.png)    | <span data-ttu-id="d0679-246">**Iş parçacığı önceliği değişikliği** (*tx_thread_priority_change*)</span><span class="sxs-lookup"><span data-stu-id="d0679-246">**Thread priority change** (*tx_thread_priority_change*)</span></span> |
| ![İş parçacığı relinsi simgesi](./media/user-guide/tx-events/image70.png)    | <span data-ttu-id="d0679-248">**Iş parçacığı relinsi** (*tx_thread_relinquish*)</span><span class="sxs-lookup"><span data-stu-id="d0679-248">**Thread relinquish** (*tx_thread_relinquish*)</span></span> |
| ![İş parçacığı sıfırlama simgesi](./media/user-guide/tx-events/image71.png)    | <span data-ttu-id="d0679-250">**Iş parçacığı sıfırlama** (*tx_thread_reset*)</span><span class="sxs-lookup"><span data-stu-id="d0679-250">**Thread reset** (*tx_thread_reset*)</span></span> |
| ![\* İş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image72.png)    | <span data-ttu-id="d0679-252">**Iş parçacığı özgeçmişi** (\**tx_thread_resume*)</span><span class="sxs-lookup"><span data-stu-id="d0679-252">**Thread resume** (\**tx_thread_resume*)</span></span> |
| ![İş parçacığı uyku simgesi](./media/user-guide/tx-events/image73.png)    | <span data-ttu-id="d0679-254">**Iş parçacığı Sleep** (*tx_thread_sleep*) \*</span><span class="sxs-lookup"><span data-stu-id="d0679-254">**Thread Sleep** (*tx_thread_sleep*)\*</span></span> |
| ![İş parçacığı yığını hata bildirme simgesi](./media/user-guide/tx-events/image74.png)    | <span data-ttu-id="d0679-256">**Iş parçacığı yığını hata bildirimi** (*tx_thread_stack_error_notify*)</span><span class="sxs-lookup"><span data-stu-id="d0679-256">**Thread stack error notify** (*tx_thread_stack_error_notify*)</span></span> |
| ![İş parçacığı bekletme simgesi](./media/user-guide/tx-events/image75.png)    | <span data-ttu-id="d0679-258">**Iş parçacığı askıya alma** (*tx_thread_suspend*)</span><span class="sxs-lookup"><span data-stu-id="d0679-258">**Thread suspend** (*tx_thread_suspend*)</span></span> |
| ![İş parçacığı Sonlandır simgesi](./media/user-guide/tx-events/image76.png)    | <span data-ttu-id="d0679-260">**Iş parçacığı Sonlandır** (*tx_thread_terminate*)</span><span class="sxs-lookup"><span data-stu-id="d0679-260">**Thread terminate** (*tx_thread_terminate*)</span></span> |
| ![İş parçacığı zaman dilimi değişikliği simgesi](./media/user-guide/tx-events/image77.png)    | <span data-ttu-id="d0679-262">**Iş parçacığı zaman dilimi değişikliği** (*tx_thread_time_slice_change*)</span><span class="sxs-lookup"><span data-stu-id="d0679-262">**Thread time-slice change** (*tx_thread_time_slice_change*)</span></span> |
| ![İş parçacığı beklemeyi durdur simgesi](./media/user-guide/tx-events/image78.png)    | <span data-ttu-id="d0679-264">**Iş parçacığı beklemeyi durdur** (*tx_thread_wait_abort*)</span><span class="sxs-lookup"><span data-stu-id="d0679-264">**Thread wait abort** (*tx_thread_wait_abort*)</span></span> |
| ![Zaman al simgesi](./media/user-guide/tx-events/image79.png)    | <span data-ttu-id="d0679-266">**Zaman al** (*tx_time_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-266">**Time get** (*tx_time_get*)</span></span> |
| ![Zaman kümesi simgesi](./media/user-guide/tx-events/image80.png)    | <span data-ttu-id="d0679-268">**Zaman kümesi** (*tx_time_set*)</span><span class="sxs-lookup"><span data-stu-id="d0679-268">**Time set** (*tx_time_set*)</span></span> |
| ![\* Süreölçer etkinleştirme simgesi](./media/user-guide/tx-events/image81.png)    | <span data-ttu-id="d0679-270">**Süreölçer etkinleştirme** (*tx_timer_activate*)</span><span class="sxs-lookup"><span data-stu-id="d0679-270">**Timer activate** (*tx_timer_activate*)</span></span> |
| ![Süreölçer değişikliği simgesi](./media/user-guide/tx-events/image82.png)    | <span data-ttu-id="d0679-272">**Süreölçer değişikliği** (*tx_timer_change*)</span><span class="sxs-lookup"><span data-stu-id="d0679-272">**Timer change** (*tx_timer_change*)</span></span> |
| ![Süreölçer oluşturma simgesi](./media/user-guide/tx-events/image83.png)    | <span data-ttu-id="d0679-274">**Süreölçer oluşturma** (*tx_timer_create*)</span><span class="sxs-lookup"><span data-stu-id="d0679-274">**Timer create** (*tx_timer_create*)</span></span> |
| ![Zamanlayıcı devre dışı bırakma simgesi](./media/user-guide/tx-events/image84.png)    | <span data-ttu-id="d0679-276">**Süreölçer devre dışı bırakma** (*tx_timer_deactivate*)</span><span class="sxs-lookup"><span data-stu-id="d0679-276">**Timer deactivate** (*tx_timer_deactivate*)</span></span> |
| ![Süreölçer silme simgesi](./media/user-guide/tx-events/image85.png)    | <span data-ttu-id="d0679-278">**Süreölçer silme** (*tx_timer_delete*)</span><span class="sxs-lookup"><span data-stu-id="d0679-278">**Timer delete** (*tx_timer_delete*)</span></span> |
| ![Süreölçer bilgileri al simgesi](./media/user-guide/tx-events/image86.png)    | <span data-ttu-id="d0679-280">**Süreölçer bilgileri Get** (*tx_timer_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-280">**Timer information get** (*tx_timer_info_get*)</span></span> |
| ![Süreölçer performans bilgileri al simgesi](./media/user-guide/tx-events/image87.png)    | <span data-ttu-id="d0679-282">**Süreölçer performans bilgileri Get** (*tx_timer_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-282">**Timer performance information get** (*tx_timer_performance_info_get*)</span></span> |
| ![\* Süreölçer performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image88.png)    | <span data-ttu-id="d0679-284">**Zamanlayıcı performansı sistem bilgileri Get** (*tx_timer_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="d0679-284">**Timer performance system information get** (*tx_timer_performance_system_info_get*)</span></span> |
| ![User-Defined Eventicon](./media/user-guide/tx-events/image0.png)    | <span data-ttu-id="d0679-286">**Kullanıcı tanımlı olay** (bkz. Bölüm 10)</span><span class="sxs-lookup"><span data-stu-id="d0679-286">**User-Defined Event** (See Chapter 10)</span></span>    |

## <a name="event-descriptions"></a><span data-ttu-id="d0679-287">Olay Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="d0679-287">Event Descriptions</span></span>

### <a name="internal-thread-resume"></a><span data-ttu-id="d0679-288">İç iş parçacığı özgeçmişi</span><span class="sxs-lookup"><span data-stu-id="d0679-288">Internal thread resume</span></span>

#### <a name="internal-thread-resume"></a><span data-ttu-id="d0679-289">İç iş parçacığı özgeçmişi</span><span class="sxs-lookup"><span data-stu-id="d0679-289">Internal thread resume</span></span>

<span data-ttu-id="d0679-290">**Simge** ![ İç iş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-290">**Icon** ![Internal thread resume icon](./media/user-guide/tx-events/image1.png)</span></span>

<span data-ttu-id="d0679-291">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-291">**Description**</span></span>

<span data-ttu-id="d0679-292">Bu olay, bir iş parçacığını yürütmeye devam eden ThreadX içindeki iç işlemeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-292">This event represents the internal processing in ThreadX that resumes a thread for execution.</span></span> <span data-ttu-id="d0679-293">Belirtilen iş parçacığı en yüksek önceliktir ve önalım-Threshold, yürütmeyi engellemez, sistem bu yeni Ready iş parçacığını yürütmeye başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0679-293">If the specified thread is the highest priority and preemption-threshold does not block its execution, the system will start executing this newly ready thread.</span></span>

<span data-ttu-id="d0679-294">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-294">**Information Fields**</span></span>

- <span data-ttu-id="d0679-295">Bilgi alanı 1: devam eden iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-295">Info Field 1: Pointer to the thread being resumed.</span></span>
- <span data-ttu-id="d0679-296">Bilgi alanı 2: iş parçacığının devam eden önceki durumu aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="d0679-296">Info Field 2: Previous state of the thread being resumed, as follows:</span></span>

  |  <span data-ttu-id="d0679-297">İş parçacığı durumu</span><span class="sxs-lookup"><span data-stu-id="d0679-297">Thread state</span></span>                     | <span data-ttu-id="d0679-298">Değer</span><span class="sxs-lookup"><span data-stu-id="d0679-298">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="d0679-299">TX_READY</span><span class="sxs-lookup"><span data-stu-id="d0679-299">TX_READY</span></span>                         | <span data-ttu-id="d0679-300">0</span><span class="sxs-lookup"><span data-stu-id="d0679-300">0</span></span>       |
  |  <span data-ttu-id="d0679-301">TX_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="d0679-301">TX_COMPLETED</span></span>                     | <span data-ttu-id="d0679-302">1</span><span class="sxs-lookup"><span data-stu-id="d0679-302">1</span></span>       |
  |  <span data-ttu-id="d0679-303">TX_TERMINATED</span><span class="sxs-lookup"><span data-stu-id="d0679-303">TX_TERMINATED</span></span>                    | <span data-ttu-id="d0679-304">2</span><span class="sxs-lookup"><span data-stu-id="d0679-304">2</span></span>       |
  |  <span data-ttu-id="d0679-305">TX_SUSPENDED</span><span class="sxs-lookup"><span data-stu-id="d0679-305">TX_SUSPENDED</span></span>                     | <span data-ttu-id="d0679-306">3</span><span class="sxs-lookup"><span data-stu-id="d0679-306">3</span></span>       |
  |  <span data-ttu-id="d0679-307">TX_SLEEP</span><span class="sxs-lookup"><span data-stu-id="d0679-307">TX_SLEEP</span></span>                         | <span data-ttu-id="d0679-308">4</span><span class="sxs-lookup"><span data-stu-id="d0679-308">4</span></span>       |
  |  <span data-ttu-id="d0679-309">TX_QUEUE_SUSP</span><span class="sxs-lookup"><span data-stu-id="d0679-309">TX_QUEUE_SUSP</span></span>                    | <span data-ttu-id="d0679-310">5</span><span class="sxs-lookup"><span data-stu-id="d0679-310">5</span></span>       |
  |  <span data-ttu-id="d0679-311">TX_SEMAPHORE_SUSP</span><span class="sxs-lookup"><span data-stu-id="d0679-311">TX_SEMAPHORE_SUSP</span></span>                | <span data-ttu-id="d0679-312">6</span><span class="sxs-lookup"><span data-stu-id="d0679-312">6</span></span>       |
  |  <span data-ttu-id="d0679-313">TX_EVENT_FLAG</span><span class="sxs-lookup"><span data-stu-id="d0679-313">TX_EVENT_FLAG</span></span>                    | <span data-ttu-id="d0679-314">7</span><span class="sxs-lookup"><span data-stu-id="d0679-314">7</span></span>       |
  |  <span data-ttu-id="d0679-315">TX_BLOCK_MEMORY</span><span class="sxs-lookup"><span data-stu-id="d0679-315">TX_BLOCK_MEMORY</span></span>                  | <span data-ttu-id="d0679-316">8</span><span class="sxs-lookup"><span data-stu-id="d0679-316">8</span></span>       |
  |  <span data-ttu-id="d0679-317">TX_BYTE_MEMORY</span><span class="sxs-lookup"><span data-stu-id="d0679-317">TX_BYTE_MEMORY</span></span>                   | <span data-ttu-id="d0679-318">9</span><span class="sxs-lookup"><span data-stu-id="d0679-318">9</span></span>       |
  |  <span data-ttu-id="d0679-319">TX_TCP_IP</span><span class="sxs-lookup"><span data-stu-id="d0679-319">TX_TCP_IP</span></span>                        | <span data-ttu-id="d0679-320">12</span><span class="sxs-lookup"><span data-stu-id="d0679-320">12</span></span>      |
  |  <span data-ttu-id="d0679-321">TX_MUTEX_SUSP</span><span class="sxs-lookup"><span data-stu-id="d0679-321">TX_MUTEX_SUSP</span></span>                    | <span data-ttu-id="d0679-322">13</span><span class="sxs-lookup"><span data-stu-id="d0679-322">13</span></span>      |

- <span data-ttu-id="d0679-323">Bilgi alanı 3: çağrı sırasında yığın işaretçisi değeri.</span><span class="sxs-lookup"><span data-stu-id="d0679-323">Info Field 3: Stack pointer value during the call.</span></span> 
- <span data-ttu-id="d0679-324">Bilgi alanı 4: yürütülecek sonraki en yüksek öncelikli iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-324">Info Field 4: Pointer to next highest priority thread to execute.</span></span>

### <a name="internal-thread-suspend"></a><span data-ttu-id="d0679-325">İç iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="d0679-325">Internal thread suspend</span></span>

#### <a name="internal-thread-suspend"></a><span data-ttu-id="d0679-326">İç iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="d0679-326">Internal thread suspend</span></span>

<span data-ttu-id="d0679-327">**Simge** ![ İç iş parçacığı askıya alma simgesi](./media/user-guide/tx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-327">**Icon** ![Internal thread suspend icon](./media/user-guide/tx-events/image2.png)</span></span>

<span data-ttu-id="d0679-328">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-328">**Description**</span></span>

<span data-ttu-id="d0679-329">Bu olay, bir iş parçacığının yürütmesini askıya alan ThreadX içindeki iç işlemeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-329">This event represents the internal processing in ThreadX that suspends a thread's execution.</span></span> <span data-ttu-id="d0679-330">Yürütmeye hazırlanma bir sonraki en yüksek öncelikli iş parçacığı dördüncü bilgi alanına yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d0679-330">The next highest priority thread ready for execution is placed in the fourth information field.</span></span> <span data-ttu-id="d0679-331">Bu değer NULL ise, yürütme için hazırlanmaya yönelik başka bir iş parçacığı yoktur ve Sistem boşta kalır.</span><span class="sxs-lookup"><span data-stu-id="d0679-331">If this value is NULL, there is no other thread ready for execution and the system is idle.</span></span>

<span data-ttu-id="d0679-332">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-332">**Information Fields**</span></span>

- <span data-ttu-id="d0679-333">Bilgi alanı 1: askıya alınan iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-333">Info Field 1: Pointer to the thread being suspended.</span></span>
- <span data-ttu-id="d0679-334">Bilgi alanı 2: şu şekilde askıya alınan iş parçacığının yeni durumu:</span><span class="sxs-lookup"><span data-stu-id="d0679-334">Info Field 2: New state of the thread being suspended, as follows:</span></span>

  |  <span data-ttu-id="d0679-335">İş parçacığı durumu</span><span class="sxs-lookup"><span data-stu-id="d0679-335">Thread state</span></span>                     | <span data-ttu-id="d0679-336">Değer</span><span class="sxs-lookup"><span data-stu-id="d0679-336">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="d0679-337">TX_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="d0679-337">TX_COMPLETED</span></span>                     | <span data-ttu-id="d0679-338">1</span><span class="sxs-lookup"><span data-stu-id="d0679-338">1</span></span>       |
  |  <span data-ttu-id="d0679-339">TX_TERMINATED</span><span class="sxs-lookup"><span data-stu-id="d0679-339">TX_TERMINATED</span></span>                    | <span data-ttu-id="d0679-340">2</span><span class="sxs-lookup"><span data-stu-id="d0679-340">2</span></span>       |
  |  <span data-ttu-id="d0679-341">TX_SUSPENDED</span><span class="sxs-lookup"><span data-stu-id="d0679-341">TX_SUSPENDED</span></span>                     | <span data-ttu-id="d0679-342">3</span><span class="sxs-lookup"><span data-stu-id="d0679-342">3</span></span>       |
  |  <span data-ttu-id="d0679-343">TX_SLEEP</span><span class="sxs-lookup"><span data-stu-id="d0679-343">TX_SLEEP</span></span>                         | <span data-ttu-id="d0679-344">4</span><span class="sxs-lookup"><span data-stu-id="d0679-344">4</span></span>       |
  |  <span data-ttu-id="d0679-345">TX_QUEUE_SUSP</span><span class="sxs-lookup"><span data-stu-id="d0679-345">TX_QUEUE_SUSP</span></span>                    | <span data-ttu-id="d0679-346">5</span><span class="sxs-lookup"><span data-stu-id="d0679-346">5</span></span>       |
  |  <span data-ttu-id="d0679-347">TX_SEMAPHORE_SUSP</span><span class="sxs-lookup"><span data-stu-id="d0679-347">TX_SEMAPHORE_SUSP</span></span>                | <span data-ttu-id="d0679-348">6</span><span class="sxs-lookup"><span data-stu-id="d0679-348">6</span></span>       |
  |  <span data-ttu-id="d0679-349">TX_EVENT_FLAG</span><span class="sxs-lookup"><span data-stu-id="d0679-349">TX_EVENT_FLAG</span></span>                    | <span data-ttu-id="d0679-350">7</span><span class="sxs-lookup"><span data-stu-id="d0679-350">7</span></span>       |
  |  <span data-ttu-id="d0679-351">TX_BLOCK_MEMORY</span><span class="sxs-lookup"><span data-stu-id="d0679-351">TX_BLOCK_MEMORY</span></span>                  | <span data-ttu-id="d0679-352">8</span><span class="sxs-lookup"><span data-stu-id="d0679-352">8</span></span>       |
  |  <span data-ttu-id="d0679-353">TX_BYTE_MEMORY</span><span class="sxs-lookup"><span data-stu-id="d0679-353">TX_BYTE_MEMORY</span></span>                   | <span data-ttu-id="d0679-354">9</span><span class="sxs-lookup"><span data-stu-id="d0679-354">9</span></span>       |
  |  <span data-ttu-id="d0679-355">TX_TCP_IP</span><span class="sxs-lookup"><span data-stu-id="d0679-355">TX_TCP_IP</span></span>                        | <span data-ttu-id="d0679-356">12</span><span class="sxs-lookup"><span data-stu-id="d0679-356">12</span></span>      |
  |  <span data-ttu-id="d0679-357">TX_MUTEX_SUSP</span><span class="sxs-lookup"><span data-stu-id="d0679-357">TX_MUTEX_SUSP</span></span>                    | <span data-ttu-id="d0679-358">13</span><span class="sxs-lookup"><span data-stu-id="d0679-358">13</span></span>      |

- <span data-ttu-id="d0679-359">Bilgi alanı 3: çağrı sırasında yığın işaretçisi değeri.</span><span class="sxs-lookup"><span data-stu-id="d0679-359">Info Field 3: Stack pointer value during the call.</span></span> <span data-ttu-id="d0679-360">Bilgi alanı 4: yürütülecek sonraki en yüksek öncelikli iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-360">Info Field 4: Pointer to next highest priority thread to execute.</span></span> <span data-ttu-id="d0679-361">NULL ise sistem boştadır.</span><span class="sxs-lookup"><span data-stu-id="d0679-361">If NULL, the system is idle.</span></span>

### <a name="interrupt-service-routine-isr-enter"></a><span data-ttu-id="d0679-362">Kesme hizmeti yordamı (ıSR) ENTER</span><span class="sxs-lookup"><span data-stu-id="d0679-362">Interrupt Service Routine (ISR) enter</span></span> 

#### <a name="enter-isr"></a><span data-ttu-id="d0679-363">ISR girin</span><span class="sxs-lookup"><span data-stu-id="d0679-363">Enter ISR</span></span> 

<span data-ttu-id="d0679-364">**Simge** ![ I S R simgesini girin](./media/user-guide/tx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-364">**Icon** ![Enter I S R icon](./media/user-guide/tx-events/image3.png)</span></span>

<span data-ttu-id="d0679-365">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-365">**Description**</span></span>

<span data-ttu-id="d0679-366">Bu olay, uygulamaya bir kesme hizmeti yordamı (ıSR) girmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-366">This event represents entering an Interrupt Service Routine (ISR) in the application.</span></span> <span data-ttu-id="d0679-367">Kesme hizmeti rutin yürütmesi, ıSR çıkış olayı gerçekleşene kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-367">The interrupt service routine execution continues until the ISR exit event takes place.</span></span>

<span data-ttu-id="d0679-368">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-368">**Information Fields**</span></span>

- <span data-ttu-id="d0679-369">Bilgi alanı 1: çağrı sırasında yığın işaretçisi değeri.</span><span class="sxs-lookup"><span data-stu-id="d0679-369">Info Field 1: Stack pointer value during the call.</span></span>
- <span data-ttu-id="d0679-370">Bilgi alanı 2: uygulama tanımlı ıSR numarası (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="d0679-370">Info Field 2: Application-defined ISR number (optional).</span></span>
- <span data-ttu-id="d0679-371">Bilgi alanı 3: Iç Içe kesme sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-371">Info Field 3: Nested interrupt count.</span></span>
- <span data-ttu-id="d0679-372">Bilgi alanı 4: Iç önalım devre dışı bayrağı.</span><span class="sxs-lookup"><span data-stu-id="d0679-372">Info Field 4: Internal preemption disable flag.</span></span>

### <a name="interrupt-service-routine-isr-exit"></a><span data-ttu-id="d0679-373">Kesme hizmeti yordamı (ıSR) çıkış</span><span class="sxs-lookup"><span data-stu-id="d0679-373">Interrupt Service Routine (ISR) exit</span></span> 

#### <a name="exit-isr"></a><span data-ttu-id="d0679-374">Çıkış ıSR</span><span class="sxs-lookup"><span data-stu-id="d0679-374">Exit ISR</span></span>

<span data-ttu-id="d0679-375">**Simge** ![ Çıkış ı R m simgesi](./media/user-guide/tx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-375">**Icon** ![Exit I S R icon](./media/user-guide/tx-events/image4.png)</span></span>

<span data-ttu-id="d0679-376">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-376">**Description**</span></span>

<span data-ttu-id="d0679-377">Bu olay, uygulamadaki bir kesme hizmeti yordamının (ıSR) çıkış işlemini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-377">This event represents exiting an Interrupt Service Routine (ISR) in the application.</span></span>

<span data-ttu-id="d0679-378">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-378">**Information Fields**</span></span>

- <span data-ttu-id="d0679-379">Bilgi alanı 1: çağrı sırasında yığın işaretçisi değeri.</span><span class="sxs-lookup"><span data-stu-id="d0679-379">Info Field 1: Stack pointer value during the call.</span></span>
- <span data-ttu-id="d0679-380">Bilgi alanı 2: uygulama tanımlı ıSR numarası (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="d0679-380">Info Field 2: Application-defined ISR number (optional).</span></span>
- <span data-ttu-id="d0679-381">Bilgi alanı 3: Iç Içe kesme sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-381">Info Field 3: Nested interrupt count.</span></span>
- <span data-ttu-id="d0679-382">Bilgi alanı 4: Iç önalım devre dışı bayrağı.</span><span class="sxs-lookup"><span data-stu-id="d0679-382">Info Field 4: Internal preemption disable flag.</span></span>

### <a name="internal-time-slice"></a><span data-ttu-id="d0679-383">İç zaman dilimi</span><span class="sxs-lookup"><span data-stu-id="d0679-383">Internal time-slice</span></span>

#### <a name="internal-time-slice"></a><span data-ttu-id="d0679-384">İç zaman dilimi</span><span class="sxs-lookup"><span data-stu-id="d0679-384">Internal time-slice</span></span>

<span data-ttu-id="d0679-385">**Simge** ![ İç zaman dilimi simgesi](./media/user-guide/tx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-385">**Icon** ![Internal time-slice icon](./media/user-guide/tx-events/image5.png)</span></span>

<span data-ttu-id="d0679-386">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-386">**Description**</span></span>

<span data-ttu-id="d0679-387">Bu olay, Işparçacığıx ' te zaman dilimi işlemini gerçekleştiren iç işlemeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-387">This event represents the internal processing in ThreadX that performs the time-slice operation.</span></span> <span data-ttu-id="d0679-388">Aynı önceliğe sahip bir sonraki iş parçacığı ilk bilgi alanına yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d0679-388">The next thread of the same priority is placed in the first information field.</span></span> <span data-ttu-id="d0679-389">Bu değer, geçerli iş parçacığıyla aynı ise, hiçbir zaman dilimi gerçekleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="d0679-389">If this value is the same as the current thread, no time-slice was performed.</span></span>

- <span data-ttu-id="d0679-390">Bilgi alanı 1: yürütülecek sonraki iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-390">Info Field 1: Pointer to the next thread to execute.</span></span>
- <span data-ttu-id="d0679-391">Bilgi alanı 2: Iç Içe kesme sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-391">Info Field 2: Nested interrupt count.</span></span>
- <span data-ttu-id="d0679-392">Bilgi alanı 3: Iç önalım devre dışı bayrağı.</span><span class="sxs-lookup"><span data-stu-id="d0679-392">Info Field 3: Internal preemption disable flag.</span></span>
- <span data-ttu-id="d0679-393">Bilgi alanı 4: çağrı sırasında yığın işaretçisi değeri.</span><span class="sxs-lookup"><span data-stu-id="d0679-393">Info Field 4: Stack pointer value during the call.</span></span>

### <a name="running"></a><span data-ttu-id="d0679-394">Çalışma</span><span class="sxs-lookup"><span data-stu-id="d0679-394">Running</span></span>

#### <a name="running-in-context"></a><span data-ttu-id="d0679-395">Bağlamda çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d0679-395">Running in context</span></span>

<span data-ttu-id="d0679-396">**Simge** ![ Çalışma simgesi](./media/user-guide/tx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-396">**Icon** ![Running icon](./media/user-guide/tx-events/image6.png)</span></span>

<span data-ttu-id="d0679-397">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-397">**Description**</span></span>

<span data-ttu-id="d0679-398">Bu olay bir iş parçacığı bağlamı veya boşta sistem içinde çalışmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-398">This event represents running within a thread context or idle system.</span></span> <span data-ttu-id="d0679-399">Bir kesmenin sonucu olarak bağlamdaki sonraki değişiklikleri göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0679-399">It is used to illustrate subsequent changes in context as a result of an interrupt.</span></span>

<span data-ttu-id="d0679-400">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-400">**Information Fields**</span></span>
- <span data-ttu-id="d0679-401">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-401">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-402">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-402">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-403">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-403">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-404">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-404">Info Field 4: Not used.</span></span>

### <a name="block-allocate"></a><span data-ttu-id="d0679-405">Blok ayır</span><span class="sxs-lookup"><span data-stu-id="d0679-405">Block Allocate</span></span> 

#### <a name="tx_block_allocate"></a><span data-ttu-id="d0679-406">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="d0679-406">tx_block_allocate</span></span>

<span data-ttu-id="d0679-407">**Simge** ![ Blok ayırma simgesi](./media/user-guide/tx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-407">**Icon** ![Block allocate icon](./media/user-guide/tx-events/image7.png)</span></span>

<span data-ttu-id="d0679-408">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-408">**Description**</span></span>

<span data-ttu-id="d0679-409">Bu olay tx_block_allocate aracılığıyla bir bellek bloğu ayırmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-409">This event represents allocating a memory block via tx_block_allocate.</span></span> <span data-ttu-id="d0679-410">Başarılı olursa, ayrılan bloğun adresi ikinci bilgi alanında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d0679-410">If successful, the address of the block allocated is returned in the second information field.</span></span>

<span data-ttu-id="d0679-411">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-411">**Information Fields**</span></span>
- <span data-ttu-id="d0679-412">Bilgi alanı 1: karşılık gelen blok havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-412">Info Field 1: Pointer to the corresponding block pool.</span></span>
- <span data-ttu-id="d0679-413">Bilgi alanı 2: döndürülen bellek bloğunun Işaretçisi (başarılıysa).</span><span class="sxs-lookup"><span data-stu-id="d0679-413">Info Field 2: Pointer to the memory block returned (if successful).</span></span>
- <span data-ttu-id="d0679-414">Bilgi alanı 3: tx_block_allocate çağrısına sağlanan bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d0679-414">Info Field 3: The wait option supplied to the tx_block_allocate call.</span></span>
- <span data-ttu-id="d0679-415">Bilgi alanı 4: Bu ayırdıktan sonra havuzda kalan kullanılabilir bloklar.</span><span class="sxs-lookup"><span data-stu-id="d0679-415">Info Field 4: Remaining available blocks in the pool after this allocation.</span></span>

### <a name="block-pool-create"></a><span data-ttu-id="d0679-416">Havuz oluşturmayı engelle</span><span class="sxs-lookup"><span data-stu-id="d0679-416">Block Pool Create</span></span>

#### <a name="tx_block_pool_create"></a><span data-ttu-id="d0679-417">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="d0679-417">tx_block_pool_create</span></span>

<span data-ttu-id="d0679-418">**Simge** ![ Blok Havuzu Oluştur simgesi](./media/user-guide/tx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-418">**Icon** ![Block pool create icon](./media/user-guide/tx-events/image8.png)</span></span>

<span data-ttu-id="d0679-419">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-419">**Description**</span></span>

<span data-ttu-id="d0679-420">Bu olay, tx_block_pool_create aracılığıyla bir bellek blok havuzu oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-420">This event represents creating a memory block pool via tx_block_pool_create.</span></span>

<span data-ttu-id="d0679-421">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-421">**Information Fields**</span></span>

- <span data-ttu-id="d0679-422">Bilgi alanı 1: karşılık gelen blok havuzu denetim bloğuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-422">Info Field 1: Pointer to the corresponding block pool control block.</span></span>
- <span data-ttu-id="d0679-423">Bilgi alanı 2: havuzun başlangıç belleği alanının Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-423">Info Field 2: Pointer to the starting memory area of the pool.</span></span>
- <span data-ttu-id="d0679-424">Bilgi alanı 3: havuzdaki blokların sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-424">Info Field 3: The number of blocks in the pool.</span></span> <span data-ttu-id="d0679-425">Bilgi alanı 4: havuzdaki her bloğun bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="d0679-425">Info Field 4: The size of each block in the pool in bytes.</span></span>

### <a name="block-pool-delete"></a><span data-ttu-id="d0679-426">Blok havuzunu silme</span><span class="sxs-lookup"><span data-stu-id="d0679-426">Block Pool Delete</span></span>

#### <a name="tx_block_pool_delete"></a><span data-ttu-id="d0679-427">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-427">tx_block_pool_delete</span></span>

<span data-ttu-id="d0679-428">**Simge** ![ Blok havuzunu silme simgesi](./media/user-guide/tx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-428">**Icon** ![Block pool delete icon](./media/user-guide/tx-events/image9.png)</span></span>

<span data-ttu-id="d0679-429">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-429">**Description**</span></span>

<span data-ttu-id="d0679-430">Bu olay, tx_block_pool_delete aracılığıyla bir bellek blok havuzunu silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-430">This event represents deleting a memory block pool via tx_block_pool_delete.</span></span>

<span data-ttu-id="d0679-431">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-431">**Information Fields**</span></span>

- <span data-ttu-id="d0679-432">Bilgi alanı 1: blok havuzu denetim bloğuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-432">Info Field 1: Pointer to the block pool control block.</span></span>
- <span data-ttu-id="d0679-433">Bilgi alanı 2: çağrı sırasında yığın işaretçisi değeri.</span><span class="sxs-lookup"><span data-stu-id="d0679-433">Info Field 2: Stack pointer value during the call.</span></span>
- <span data-ttu-id="d0679-434">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-434">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-435">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-435">Info Field 4: Not used.</span></span>

### <a name="block-pool-information-get"></a><span data-ttu-id="d0679-436">Havuz bilgilerini engelle al</span><span class="sxs-lookup"><span data-stu-id="d0679-436">Block Pool Information Get</span></span> 

#### <a name="tx_block_pool_info_get"></a><span data-ttu-id="d0679-437">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-437">tx_block_pool_info_get</span></span>

<span data-ttu-id="d0679-438">**Simge** ![ Havuz bilgilerini engelle al simgesi](./media/user-guide/tx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-438">**Icon** ![Block pool information get icon](./media/user-guide/tx-events/image10.png)</span></span>

<span data-ttu-id="d0679-439">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-439">**Description**</span></span>

<span data-ttu-id="d0679-440">Bu olay, tx_block_pool_info_get aracılığıyla bir bellek blok havuzu hakkında bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-440">This event represents getting information about a memory block pool via tx_block_pool_info_get.</span></span>

<span data-ttu-id="d0679-441">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-441">**Information Fields**</span></span>

- <span data-ttu-id="d0679-442">Bilgi alanı 1: blok havuzu denetim bloğuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-442">Info Field 1: Pointer to the block pool control block.</span></span>
- <span data-ttu-id="d0679-443">Bilgi alanı 2: çağrı sırasında yığın işaretçisi değeri.</span><span class="sxs-lookup"><span data-stu-id="d0679-443">Info Field 2: Stack pointer value during the call.</span></span>
- <span data-ttu-id="d0679-444">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-444">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-445">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-445">Info Field 4: Not used.</span></span>

### <a name="block-pool-performance-information-get"></a><span data-ttu-id="d0679-446">Blok havuzu performans bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="d0679-446">Block Pool Performance Information Get</span></span>

#### <a name="tx_block_pool_performance_info_get"></a><span data-ttu-id="d0679-447">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-447">tx_block_pool_performance_info_get</span></span>

<span data-ttu-id="d0679-448">**Simge** ![ Blok havuzu performans bilgileri al simgesi](./media/user-guide/tx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-448">**Icon** ![Block pool performance information get icon](./media/user-guide/tx-events/image11.png)</span></span>

<span data-ttu-id="d0679-449">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-449">**Description**</span></span>

<span data-ttu-id="d0679-450">Bu olay, tx_block_pool_performance_info_get aracılığıyla bir bellek blok havuzu hakkında performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-450">This event represents getting performance information about a memory block pool via tx_block_pool_performance_info_get.</span></span>

<span data-ttu-id="d0679-451">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-451">**Information Fields**</span></span>

- <span data-ttu-id="d0679-452">Bilgi alanı 1: blok havuzu denetim bloğuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-452">Info Field 1: Pointer to the block pool control block.</span></span>
- <span data-ttu-id="d0679-453">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-453">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-454">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-454">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-455">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-455">Info Field 4: Not used.</span></span>

### <a name="block-pool-performance-system-information-get"></a><span data-ttu-id="d0679-456">Blok havuz performansı sistem bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="d0679-456">Block Pool Performance System Information Get</span></span>

#### <a name="tx_block_pool_performance_system_info_get"></a><span data-ttu-id="d0679-457">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-457">tx_block_pool_performance_system_info_get</span></span>

<span data-ttu-id="d0679-458">**Simge** ![ Blok havuz performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-458">**Icon** ![Block pool performance system information get icon](./media/user-guide/tx-events/image12.png)</span></span>

<span data-ttu-id="d0679-459">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-459">**Description**</span></span>

<span data-ttu-id="d0679-460">Bu olay, tüm bellek bloğu havuzları hakkında tx_block_pool_performance_system_info_get aracılığıyla performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-460">This event represents getting performance information about all memory block pools via tx_block_pool_performance_system_info_get.</span></span>

<span data-ttu-id="d0679-461">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-461">**Information Fields**</span></span>
- <span data-ttu-id="d0679-462">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-462">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-463">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-463">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-464">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-464">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-465">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-465">Info Field 4: Not used.</span></span>

### <a name="block-pool-prioritize"></a><span data-ttu-id="d0679-466">Blok havuzu önceliği belirleme</span><span class="sxs-lookup"><span data-stu-id="d0679-466">Block Pool Prioritize</span></span>

#### <a name="tx_block_pool_prioritize"></a><span data-ttu-id="d0679-467">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="d0679-467">tx_block_pool_prioritize</span></span>

<span data-ttu-id="d0679-468">**Simge** ![ Blok havuzu öncelik simgeleri simgesi](./media/user-guide/tx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-468">**Icon** ![Block pool prioritize icon](./media/user-guide/tx-events/image13.png)</span></span>

<span data-ttu-id="d0679-469">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-469">**Description**</span></span>

<span data-ttu-id="d0679-470">Bu olay, HighestPriority askıya alınan iş parçacığını blok havuzunun askıya alma listesinin önüne yerleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-470">This event represents placing the highestpriority suspended thread at the front of the block pool suspension list.</span></span> <span data-ttu-id="d0679-471">Tx_block_release çağrılmadan önce Bu yapıldığında, en yüksek önceliğe sahip iş parçacığı yayınlanan bloğu alır.</span><span class="sxs-lookup"><span data-stu-id="d0679-471">If this is done prior to calling tx_block_release, the highest priority suspended thread will receive the released block.</span></span>

<span data-ttu-id="d0679-472">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-472">**Information Fields**</span></span>
- <span data-ttu-id="d0679-473">Bilgi alanı 1: bellek blok havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-473">Info Field 1: Memory block pool pointer.</span></span>
- <span data-ttu-id="d0679-474">Bilgi alanı 2: Bu blok havuzunda askıya alınan iş parçacıklarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-474">Info Field 2: Number of threads suspended on this block pool.</span></span>
- <span data-ttu-id="d0679-475">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-475">Info Field 3: Stack pointer at the time of the call.</span></span>
- <span data-ttu-id="d0679-476">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-476">Info Field 4: Not used.</span></span>

### <a name="block-release"></a><span data-ttu-id="d0679-477">Yayını engelle</span><span class="sxs-lookup"><span data-stu-id="d0679-477">Block Release</span></span> 

#### <a name="tx_block_release"></a><span data-ttu-id="d0679-478">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="d0679-478">tx_block_release</span></span>

<span data-ttu-id="d0679-479">**Simge** ![ Blok yayını simgesi](./media/user-guide/tx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-479">**Icon** ![Block release icon](./media/user-guide/tx-events/image14.png)</span></span>

<span data-ttu-id="d0679-480">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-480">**Description**</span></span>

<span data-ttu-id="d0679-481">Bu olay, daha önce ayrılmış bir bloğu blok havuzuna geri bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-481">This event represents releasing a previously allocated block back to the block pool.</span></span>

<span data-ttu-id="d0679-482">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-482">**Information Fields**</span></span>

- <span data-ttu-id="d0679-483">Bilgi alanı 1: bellek blok havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-483">Info Field 1: Memory block pool pointer.</span></span>
- <span data-ttu-id="d0679-484">Bilgi alanı 2: serbest bırakmak için blok Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-484">Info Field 2: Pointer to block to release.</span></span>
- <span data-ttu-id="d0679-485">Bilgi alanı 3: Bu blok havuzunda askıya alınan iş parçacığı sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-485">Info Field 3: Number of threads suspended on this block pool.</span></span>
- <span data-ttu-id="d0679-486">Bilgi alanı 4: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-486">Info Field 4: Stack pointer at the time of the call.</span></span>

### <a name="byte-allocate"></a><span data-ttu-id="d0679-487">Bayt ayırma</span><span class="sxs-lookup"><span data-stu-id="d0679-487">Byte Allocate</span></span> 

#### <a name="tx_byte_allocate"></a><span data-ttu-id="d0679-488">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="d0679-488">tx_byte_allocate</span></span>

<span data-ttu-id="d0679-489">**Simge** ![ Bayt ayırma simgesi](./media/user-guide/tx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-489">**Icon** ![Byte allocate icon](./media/user-guide/tx-events/image15.png)</span></span>

<span data-ttu-id="d0679-490">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-490">**Description**</span></span>

<span data-ttu-id="d0679-491">Bu olay tx_byte_allocate aracılığıyla bellek ayırmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-491">This event represents allocating memory via tx_byte_allocate.</span></span> <span data-ttu-id="d0679-492">Başarılı olursa, ayrılan bellek adresi ikinci bilgi alanında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d0679-492">If successful, the address of the memory allocated is returned in the second information field.</span></span>

<span data-ttu-id="d0679-493">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-493">**Information Fields**</span></span>
- <span data-ttu-id="d0679-494">Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-494">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="d0679-495">Bilgi alanı 2: döndürülen bellek Işaretçisi (başarılıysa).</span><span class="sxs-lookup"><span data-stu-id="d0679-495">Info Field 2: Pointer to the memory returned (if successful).</span></span>
- <span data-ttu-id="d0679-496">Bilgi alanı 3: istenen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-496">Info Field 3: Number of bytes requested.</span></span> <span data-ttu-id="d0679-497">Bilgi alanı 4: tx_byte_allocate çağrısına sağlanan bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d0679-497">Info Field 4: The wait option supplied to the tx_byte_allocate call.</span></span>

### <a name="byte-pool-create"></a><span data-ttu-id="d0679-498">Bayt havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0679-498">Byte Pool Create</span></span>

#### <a name="tx_byte_pool_create"></a><span data-ttu-id="d0679-499">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="d0679-499">tx_byte_pool_create</span></span>

<span data-ttu-id="d0679-500">**Simge** ![ Bayt havuzu oluşturma simgesi](./media/user-guide/tx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-500">**Icon** ![Byte pool create icon](./media/user-guide/tx-events/image16.png)</span></span>

<span data-ttu-id="d0679-501">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-501">**Description**</span></span>

<span data-ttu-id="d0679-502">Bu olay tx_byte_pool_create aracılığıyla bir bayt havuzu oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-502">This event represents creating a byte pool via tx_byte_pool_create.</span></span>

<span data-ttu-id="d0679-503">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-503">**Information Fields**</span></span>

- <span data-ttu-id="d0679-504">Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-504">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="d0679-505">Bilgi alanı 2: bellek alanının başlangıcına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-505">Info Field 2: Pointer to the start of the memory area.</span></span> <span data-ttu-id="d0679-506">Bilgi alanı 3: bayt havuzundaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-506">Info Field 3: Number of bytes in the byte pool.</span></span>
- <span data-ttu-id="d0679-507">Bilgi alanı 4: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-507">Info Field 4: The stack pointer at the time of the call.</span></span>

### <a name="byte-pool-delete"></a><span data-ttu-id="d0679-508">Bayt havuzu silme</span><span class="sxs-lookup"><span data-stu-id="d0679-508">Byte Pool Delete</span></span> 

#### <a name="tx_byte_pool_delete"></a><span data-ttu-id="d0679-509">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-509">tx_byte_pool_delete</span></span>

<span data-ttu-id="d0679-510">**Simge** ![ Bayt havuzu silme simgesi](./media/user-guide/tx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-510">**Icon** ![Byte pool delete icon](./media/user-guide/tx-events/image17.png)</span></span>

<span data-ttu-id="d0679-511">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-511">**Description**</span></span>

<span data-ttu-id="d0679-512">Bu olay, tx_byte_pool_delete aracılığıyla bir bayt havuzunun silinmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-512">This event represents deleting a byte pool via tx_byte_pool_delete.</span></span>

<span data-ttu-id="d0679-513">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-513">**Information Fields**</span></span>

- <span data-ttu-id="d0679-514">Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-514">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="d0679-515">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-515">Info Field 2: The stack pointer at the time of the call.</span></span>
- <span data-ttu-id="d0679-516">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-516">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-517">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-517">Info Field 4: Not used.</span></span>

### <a name="byte-pool-information-get"></a><span data-ttu-id="d0679-518">Bayt havuzu bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="d0679-518">Byte Pool Information Get</span></span>

#### <a name="tx_byte_pool_info_get"></a><span data-ttu-id="d0679-519">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-519">tx_byte_pool_info_get</span></span>

<span data-ttu-id="d0679-520">**Simge** ![ Bayt havuzu bilgileri al simgesi](./media/user-guide/tx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-520">**Icon** ![Byte pool information get icon](./media/user-guide/tx-events/image18.png)</span></span>

<span data-ttu-id="d0679-521">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-521">**Description**</span></span>

<span data-ttu-id="d0679-522">Bu olay, tx_byte_pool_info_get aracılığıyla bayt havuzu bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-522">This event represents getting byte pool information via tx_byte_pool_info_get.</span></span>

<span data-ttu-id="d0679-523">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-523">**Information Fields**</span></span>

- <span data-ttu-id="d0679-524">Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-524">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="d0679-525">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-525">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-526">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-526">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-527">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-527">Info Field 4: Not used.</span></span>

### <a name="byte-pool-performance-info-get"></a><span data-ttu-id="d0679-528">Bayt havuzu performans bilgisi al</span><span class="sxs-lookup"><span data-stu-id="d0679-528">Byte Pool Performance Info Get</span></span> 

#### <a name="tx_byte_pool_info_get"></a><span data-ttu-id="d0679-529">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-529">tx_byte_pool_info_get</span></span>

<span data-ttu-id="d0679-530">**Simge** ![ Bayt havuzu performans bilgisi al simgesi](./media/user-guide/tx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-530">**Icon** ![Byte pool performance info get icon](./media/user-guide/tx-events/image19.png)</span></span>

<span data-ttu-id="d0679-531">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-531">**Description**</span></span>

<span data-ttu-id="d0679-532">Bu olay, tx_byte_pool_performance_info_get aracılığıyla bayt havuzu performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-532">This event represents getting byte pool performance information via tx_byte_pool_performance_info_get.</span></span>

<span data-ttu-id="d0679-533">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-533">**Information Fields**</span></span>

- <span data-ttu-id="d0679-534">Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-534">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="d0679-535">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-535">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-536">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-536">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-537">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-537">Info Field 4: Not used.</span></span>

### <a name="byte-pool-performance-system-info-get"></a><span data-ttu-id="d0679-538">Bayt havuzu performans sistemi bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="d0679-538">Byte Pool Performance System Info Get</span></span> 

#### <a name="tx_byte_pool_performance_system_info_get"></a><span data-ttu-id="d0679-539">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-539">tx_byte_pool_performance_system_info_get</span></span>

<span data-ttu-id="d0679-540">**Simge** ![ Bayt havuzu performans sistemi bilgileri al simgesi](./media/user-guide/tx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-540">**Icon** ![Byte pool performance system info get icon](./media/user-guide/tx-events/image20.png)</span></span>

<span data-ttu-id="d0679-541">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-541">**Description**</span></span>

<span data-ttu-id="d0679-542">Bu olay, tx_byte_pool_performance_system_info_get aracılığıyla bayt havuzu performans sistemi bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-542">This event represents getting byte pool performance system information via tx_byte_pool_performance_system_info_get.</span></span>

<span data-ttu-id="d0679-543">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-543">**Information Fields**</span></span>

- <span data-ttu-id="d0679-544">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-544">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-545">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-545">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-546">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-546">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-547">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-547">Info Field 4: Not used.</span></span>

### <a name="byte-pool-prioritize"></a><span data-ttu-id="d0679-548">Bayt havuzu önceliği belirleme</span><span class="sxs-lookup"><span data-stu-id="d0679-548">Byte Pool Prioritize</span></span>

#### <a name="tx_byte_pool_prioritize"></a><span data-ttu-id="d0679-549">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="d0679-549">tx_byte_pool_prioritize</span></span>

<span data-ttu-id="d0679-550">**Simge** ![ Bayt havuzu öncelik simgesi](./media/user-guide/tx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-550">**Icon** ![Byte pool prioritize icon](./media/user-guide/tx-events/image21.png)</span></span>

<span data-ttu-id="d0679-551">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-551">**Description**</span></span>

<span data-ttu-id="d0679-552">Bu olay, tx_byte_pool_prioritize aracılığıyla bayt havuzunun askıya alma listesinin önceliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-552">This event represents prioritizing the byte pool's suspension list via tx_byte_pool_prioritize.</span></span>

<span data-ttu-id="d0679-553">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-553">**Information Fields**</span></span>

- <span data-ttu-id="d0679-554">Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-554">Info Field 1: Pointer to corresponding byte pool.</span></span>
- <span data-ttu-id="d0679-555">Bilgi alanı 2: bayt havuzunda Şu anda askıya alınan iş parçacıklarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-555">Info Field 2: Number of threads currently suspended on byte pool.</span></span>
- <span data-ttu-id="d0679-556">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-556">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-557">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-557">Info Field 4: Not used.</span></span>

### <a name="byte-release"></a><span data-ttu-id="d0679-558">Bayt yayını</span><span class="sxs-lookup"><span data-stu-id="d0679-558">Byte Release</span></span>

#### <a name="tx_byte_release"></a><span data-ttu-id="d0679-559">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="d0679-559">tx_byte_release</span></span>

<span data-ttu-id="d0679-560">**Simge** ![ Bayt yayın simgesi](./media/user-guide/tx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-560">**Icon** ![Byte release icon](./media/user-guide/tx-events/image22.png)</span></span>

<span data-ttu-id="d0679-561">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-561">**Description**</span></span>

<span data-ttu-id="d0679-562">Bu olay, bir bayt havuzundan ayrılan bellek bloğunu tx_byte_release aracılığıyla serbest bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-562">This event represents releasing a block of memory allocated from a byte pool via tx_byte_release.</span></span>

<span data-ttu-id="d0679-563">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-563">**Information Fields**</span></span>

- <span data-ttu-id="d0679-564">Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-564">Info Field 1: Pointer to corresponding byte pool.</span></span>
- <span data-ttu-id="d0679-565">Bilgi alanı 2: önceden ayrılmış bayt havuzu belleği Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-565">Info Field 2: Pointer to previously allocated byte pool memory.</span></span>
- <span data-ttu-id="d0679-566">Bilgi alanı 3: Bu bayt havuzunda askıya alınan iş parçacığı sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-566">Info Field 3: Number of threads suspended on this byte pool.</span></span>
- <span data-ttu-id="d0679-567">Bilgi alanı 4: kullanılabilir bellek bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-567">Info Field 4: Number of available bytes of memory.</span></span>

### <a name="event-flags-create"></a><span data-ttu-id="d0679-568">Olay bayrakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0679-568">Event Flags Create</span></span> 

#### <a name="tx_event_flags_create"></a><span data-ttu-id="d0679-569">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="d0679-569">tx_event_flags_create</span></span>

<span data-ttu-id="d0679-570">**Simge** ![ Olay bayrakları Oluştur simgesi](./media/user-guide/tx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-570">**Icon** ![Event flags create icon](./media/user-guide/tx-events/image23.png)</span></span>

<span data-ttu-id="d0679-571">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-571">**Description**</span></span>

<span data-ttu-id="d0679-572">Bu olay tx_event_flags_create aracılığıyla yeni bir olay bayrakları grubu oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-572">This event represents creating a new event flags group via tx_event_flags_create.</span></span>

<span data-ttu-id="d0679-573">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-573">**Information Fields**</span></span> 
- <span data-ttu-id="d0679-574">Bilgi alanı 1: olay bayrakları Grup denetim bloğuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-574">Info Field 1: Pointer to event flags group control block.</span></span>
- <span data-ttu-id="d0679-575">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-575">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-576">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-576">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-577">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-577">Info Field 4: Not used.</span></span>

### <a name="event-flags-delete"></a><span data-ttu-id="d0679-578">Olay bayraklarını silme</span><span class="sxs-lookup"><span data-stu-id="d0679-578">Event Flags Delete</span></span> 

#### <a name="tx_event_flags_delete"></a><span data-ttu-id="d0679-579">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-579">tx_event_flags_delete</span></span>

<span data-ttu-id="d0679-580">**Simge** ![ Olay bayrakları silme simgesi](./media/user-guide/tx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-580">**Icon** ![Event flags delete icon](./media/user-guide/tx-events/image24.png)</span></span>

<span data-ttu-id="d0679-581">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-581">**Description**</span></span>

<span data-ttu-id="d0679-582">Bu olay, tx_event_flags_delete aracılığıyla bir olay bayrakları grubunu silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-582">This event represents deleting an event flags group via tx_event_flags_delete.</span></span>

<span data-ttu-id="d0679-583">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-583">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-584">Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-584">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="d0679-585">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-585">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-586">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-586">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-587">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-587">Info Field 4: Not used.</span></span>

### <a name="event-flags-get"></a><span data-ttu-id="d0679-588">Olay bayrakları al</span><span class="sxs-lookup"><span data-stu-id="d0679-588">Event Flags Get</span></span> 

#### <a name="tx_event_flags_get"></a><span data-ttu-id="d0679-589">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="d0679-589">tx_event_flags_get</span></span>

<span data-ttu-id="d0679-590">**Simge** ![ Olay bayrakları gt simgesi](./media/user-guide/tx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-590">**Icon** ![Event flags gt icon](./media/user-guide/tx-events/image25.png)</span></span>

<span data-ttu-id="d0679-591">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-591">**Description**</span></span>

<span data-ttu-id="d0679-592">Bu olay, tx_event_flags_get aracılığıyla var olan bir olay bayrakları grubundan olay bayraklarını almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-592">This event represents retrieving event flags from an existing event flags group via tx_event_flags_get.</span></span>

<span data-ttu-id="d0679-593">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-593">**Information Fields**</span></span>

- <span data-ttu-id="d0679-594">Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-594">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="d0679-595">Bilgi alanı 2: istenen olay bayrakları.</span><span class="sxs-lookup"><span data-stu-id="d0679-595">Info Field 2: Event flags requested.</span></span>
- <span data-ttu-id="d0679-596">Bilgi alanı 3: grupta ayarlanmış olan olay bayrakları.</span><span class="sxs-lookup"><span data-stu-id="d0679-596">Info Field 3: Event flags currently set in the group.</span></span>
- <span data-ttu-id="d0679-597">Bilgi alanı 4: Get olay bayraklarda istenen seçenek.</span><span class="sxs-lookup"><span data-stu-id="d0679-597">Info Field 4: Option requested on the event flags get.</span></span>

### <a name="event-flags-information-get"></a><span data-ttu-id="d0679-598">Olay bayrakları bilgileri al</span><span class="sxs-lookup"><span data-stu-id="d0679-598">Event Flags Information Get</span></span>

#### <a name="tx_event_flags_info_get"></a><span data-ttu-id="d0679-599">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-599">tx_event_flags_info_get</span></span>

<span data-ttu-id="d0679-600">**Simge** ![ Olay bayrakları bilgileri al simgesi](./media/user-guide/tx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-600">**Icon** ![Event flags information get icon](./media/user-guide/tx-events/image26.png)</span></span>

<span data-ttu-id="d0679-601">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-601">**Description**</span></span>

<span data-ttu-id="d0679-602">Bu olay, tx_event_flags_info_get aracılığıyla mevcut bir olay bayrakları grubuyla ilgili bilgileri almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-602">This event represents retrieving information regarding an existing event flags group via tx_event_flags_info_get.</span></span>

<span data-ttu-id="d0679-603">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-603">**Information Fields**</span></span>

- <span data-ttu-id="d0679-604">Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-604">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="d0679-605">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-605">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-606">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-606">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-607">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-607">Info Field 4: Not used.</span></span>

### <a name="event-flags-performance-information-get"></a><span data-ttu-id="d0679-608">Olay bayrakları performans bilgileri al</span><span class="sxs-lookup"><span data-stu-id="d0679-608">Event Flags Performance Information Get</span></span> 

#### <a name="tx_event_flags_performance_info_get"></a><span data-ttu-id="d0679-609">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-609">tx_event_flags_performance_info_get</span></span>

<span data-ttu-id="d0679-610">**Simge** ![ Olay bayrakları performans bilgileri al simgesi](./media/user-guide/tx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-610">**Icon** ![Event flags performance information get icon](./media/user-guide/tx-events/image27.png)</span></span>

<span data-ttu-id="d0679-611">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-611">**Description**</span></span>

<span data-ttu-id="d0679-612">Bu olay, tx_event_flags_performance_info_get aracılığıyla mevcut bir olay bayrakları grubuyla ilgili performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-612">This event represents retrieving performance information regarding an existing event flags group via tx_event_flags_performance_info_get.</span></span>

<span data-ttu-id="d0679-613">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-613">**Information Fields**</span></span> 
- <span data-ttu-id="d0679-614">Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-614">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="d0679-615">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="d0679-615">Info Field 2: Not used</span></span>
- <span data-ttu-id="d0679-616">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="d0679-616">Info Field 3: Not used</span></span>
- <span data-ttu-id="d0679-617">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="d0679-617">Info Field 4: Not Used</span></span>

### <a name="event-flags-performance-system-info-get"></a><span data-ttu-id="d0679-618">Olay bayrakları performans sistem bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="d0679-618">Event Flags Performance System Info Get</span></span>

#### <a name="tx_event_flags_performance_system_info_get"></a><span data-ttu-id="d0679-619">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-619">tx_event_flags_performance_system_info_get</span></span>

<span data-ttu-id="d0679-620">**Simge** ![ Olay bayrakları performans sistem bilgileri al simgesi](./media/user-guide/tx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-620">**Icon** ![Event flags performance system info get icon](./media/user-guide/tx-events/image28.png)</span></span>

<span data-ttu-id="d0679-621">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-621">**Description**</span></span>

<span data-ttu-id="d0679-622">Bu olay, tx_event_flags_performance_system_info_get aracılığıyla mevcut bir olay bayrakları grubuyla ilgili performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-622">This event represents retrieving performance information regarding an existing event flags group via tx_event_flags_performance_system_info_get.</span></span>

<span data-ttu-id="d0679-623">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-623">**Information Fields**</span></span>
- <span data-ttu-id="d0679-624">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-624">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-625">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-625">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-626">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-626">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-627">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-627">Info Field 4: Not used.</span></span>

### <a name="event-flags-set"></a><span data-ttu-id="d0679-628">Olay bayrak kümesi</span><span class="sxs-lookup"><span data-stu-id="d0679-628">Event Flags Set</span></span> 

#### <a name="tx_event_flags_set"></a><span data-ttu-id="d0679-629">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="d0679-629">tx_event_flags_set</span></span>

<span data-ttu-id="d0679-630">**Simge** ![ Olay bayrakları kümesi simgesi](./media/user-guide/tx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-630">**Icon** ![Event flags set icon](./media/user-guide/tx-events/image29.png)</span></span>

<span data-ttu-id="d0679-631">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-631">**Description**</span></span>

<span data-ttu-id="d0679-632">Bu olay, tx_event_flags_set aracılığıyla var olan bir olay bayrakları grubundaki olay bayraklarını ayarlamayı (veya temizlemeyi) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-632">This event represents setting (or clearing) event flags in an existing event flags group via tx_event_flags_set.</span></span>

<span data-ttu-id="d0679-633">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-633">**Information Fields**</span></span>

- <span data-ttu-id="d0679-634">Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-634">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="d0679-635">Bilgi alanı 2: ayarlanacak (veya temizlenecek) olay bayrakları.</span><span class="sxs-lookup"><span data-stu-id="d0679-635">Info Field 2: Event flags to set (or clear).</span></span>
- <span data-ttu-id="d0679-636">Bilgi alanı 3: ve veya ya da olay bayrağı seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d0679-636">Info Field 3: AND or OR event flag option.</span></span>
- <span data-ttu-id="d0679-637">Bilgi alanı 4: olay bayrak grubunda askıya alınan iş parçacıklarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-637">Info Field 4: Number of threads suspended on event flag group.</span></span>

### <a name="event-flags-set-notify"></a><span data-ttu-id="d0679-638">Olay bayrakları kümesi bildir</span><span class="sxs-lookup"><span data-stu-id="d0679-638">Event Flags Set Notify</span></span>

#### <a name="tx_event_flags_set_notify"></a><span data-ttu-id="d0679-639">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="d0679-639">tx_event_flags_set_notify</span></span>

<span data-ttu-id="d0679-640">**Simge** ![ Olay bayrakları ayarlama bildirim simgesi](./media/user-guide/tx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-640">**Icon** ![Event flags set notify icon](./media/user-guide/tx-events/image30.png)</span></span>

<span data-ttu-id="d0679-641">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-641">**Description**</span></span>

<span data-ttu-id="d0679-642">Bu olay, tx_event_flags_set_notify aracılığıyla var olan bir olay bayrakları grubundaki herhangi bir olay bayrağı ayarlama işlemi için bir bildirim geri çağrısının kaydedilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-642">This event represents registering a notification callback for any event flag set operation on an existing event flags group via tx_event_flags_set_notify.</span></span>

<span data-ttu-id="d0679-643">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-643">**Information Fields**</span></span>

- <span data-ttu-id="d0679-644">Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-644">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="d0679-645">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-645">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-646">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-646">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-647">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-647">Info Field 4: Not used.</span></span>

### <a name="interrupt-control"></a><span data-ttu-id="d0679-648">Kesme denetimi</span><span class="sxs-lookup"><span data-stu-id="d0679-648">Interrupt Control</span></span> 

#### <a name="tx_interrupt_control"></a><span data-ttu-id="d0679-649">tx_interrupt_control</span><span class="sxs-lookup"><span data-stu-id="d0679-649">tx_interrupt_control</span></span>

<span data-ttu-id="d0679-650">**Simge** ![ Kesme denetimi simgesi](./media/user-guide/tx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-650">**Icon** ![Interrupt control icon](./media/user-guide/tx-events/image31.png)</span></span>

<span data-ttu-id="d0679-651">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-651">**Description**</span></span>

<span data-ttu-id="d0679-652">Bu olay, tx_interrupt_control aracılığıyla işlemcinin kesme kilitleme duruşunu değiştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-652">This event represents changing the interrupt lockout posture of the processor via tx_interrupt_control.</span></span>

<span data-ttu-id="d0679-653">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-653">**Information Fields**</span></span>

- <span data-ttu-id="d0679-654">Bilgi alanı 1: yeni kesme sonrası.</span><span class="sxs-lookup"><span data-stu-id="d0679-654">Info Field 1: New interrupt posture.</span></span>
- <span data-ttu-id="d0679-655">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-655">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-656">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-656">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-657">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-657">Info Field 4: Not used.</span></span>

### <a name="mutex-create"></a><span data-ttu-id="d0679-658">Mutex oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0679-658">Mutex Create</span></span> 

#### <a name="tx_mutex_create"></a><span data-ttu-id="d0679-659">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="d0679-659">tx_mutex_create</span></span>

<span data-ttu-id="d0679-660">**Simge** ![ Mutex Oluştur simgesi](./media/user-guide/tx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-660">**Icon** ![Mutex create icon](./media/user-guide/tx-events/image32.png)</span></span>

<span data-ttu-id="d0679-661">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-661">**Description**</span></span>

<span data-ttu-id="d0679-662">Bu olay tx_mutex_create aracılığıyla bir mutex oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-662">This event represents creating a mutex via tx_mutex_create.</span></span>

<span data-ttu-id="d0679-663">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-663">**Information Fields**</span></span>

- <span data-ttu-id="d0679-664">Bilgi alanı 1: Mutex denetim bloğu Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-664">Info Field 1: Pointer to mutex control block.</span></span>
- <span data-ttu-id="d0679-665">Bilgi alanı 2: öncelik devralma seçeneği</span><span class="sxs-lookup"><span data-stu-id="d0679-665">Info Field 2: Priority inheritance option</span></span>
- <span data-ttu-id="d0679-666">(TX_INHERIT veya TX_NO_INHERIT).</span><span class="sxs-lookup"><span data-stu-id="d0679-666">(TX_INHERIT or TX_NO_INHERIT).</span></span>
- <span data-ttu-id="d0679-667">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-667">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-668">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-668">Info Field 4: Not used.</span></span>

### <a name="mutex-delete"></a><span data-ttu-id="d0679-669">Mutex silme</span><span class="sxs-lookup"><span data-stu-id="d0679-669">Mutex Delete</span></span> 

#### <a name="tx_mutex_delete"></a><span data-ttu-id="d0679-670">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-670">tx_mutex_delete</span></span>

<span data-ttu-id="d0679-671">**Simge** ![ Mutex silme simgesi](./media/user-guide/tx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-671">**Icon** ![Mutex delete icon](./media/user-guide/tx-events/image33.png)</span></span>

<span data-ttu-id="d0679-672">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-672">**Description**</span></span>

<span data-ttu-id="d0679-673">Bu olay bir mutex 'i tx_mutex_delete aracılığıyla silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-673">This event represents deleting a mutex via tx_mutex_delete.</span></span>

<span data-ttu-id="d0679-674">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-674">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-675">Bilgi alanı 1: mutex Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-675">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="d0679-676">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-676">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-677">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-677">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-678">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-678">Info Field 4: Not used.</span></span>

### <a name="mutex-get"></a><span data-ttu-id="d0679-679">Mutex al</span><span class="sxs-lookup"><span data-stu-id="d0679-679">Mutex Get</span></span> 

#### <a name="tx_mutex_get"></a><span data-ttu-id="d0679-680">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="d0679-680">tx_mutex_get</span></span>

<span data-ttu-id="d0679-681">**Simge** ![ Mutex al simgesi](./media/user-guide/tx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-681">**Icon** ![Mutex get icon](./media/user-guide/tx-events/image34.png)</span></span>

<span data-ttu-id="d0679-682">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-682">**Description**</span></span>

<span data-ttu-id="d0679-683">Bu olay tx_mutex_get aracılığıyla bir mutex elde etmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-683">This event represents obtaining a mutex via tx_mutex_get.</span></span>

<span data-ttu-id="d0679-684">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-684">**Information Fields**</span></span>

- <span data-ttu-id="d0679-685">Bilgi alanı 1: mutex Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-685">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="d0679-686">Bilgi alanı 2: tx_mutex_get çağrısına sağlanan bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d0679-686">Info Field 2: The wait option supplied to the tx_mutex_get call.</span></span>
- <span data-ttu-id="d0679-687">Bilgi alanı 3: mutex 'e sahip iş parçacığına yönelik Işaretçi (NULL, mutex 'in sahip olmadığı anlamına gelir).</span><span class="sxs-lookup"><span data-stu-id="d0679-687">Info Field 3: Pointer to thread that owns the mutex (NULL implies the mutex is not owned).</span></span>
- <span data-ttu-id="d0679-688">Bilgi alanı 4: sahip olan iş parçacığının tx_mutex_get kaç kez çağırdığı.</span><span class="sxs-lookup"><span data-stu-id="d0679-688">Info Field 4: Number of times the owning thread has called tx_mutex_get.</span></span>

### <a name="mutex-information-get"></a><span data-ttu-id="d0679-689">Mutex bilgileri al</span><span class="sxs-lookup"><span data-stu-id="d0679-689">Mutex Information Get</span></span>

#### <a name="tx_mutex_info_get"></a><span data-ttu-id="d0679-690">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-690">tx_mutex_info_get</span></span>

<span data-ttu-id="d0679-691">**Simge** ![ Mutex bilgileri al simgesi](./media/user-guide/tx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-691">**Icon** ![Mutex information get icon](./media/user-guide/tx-events/image35.png)</span></span>

<span data-ttu-id="d0679-692">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-692">**Description**</span></span>

<span data-ttu-id="d0679-693">Bu olay, tx_mutex_info_get aracılığıyla mutex bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-693">This event represents retrieving mutex information via tx_mutex_info_get.</span></span>

<span data-ttu-id="d0679-694">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-694">**Information Fields**</span></span>

- <span data-ttu-id="d0679-695">Bilgi alanı 1: mutex Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-695">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="d0679-696">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-696">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-697">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-697">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-698">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-698">Info Field 4: Not used.</span></span>

### <a name="mutex-performance-information-get"></a><span data-ttu-id="d0679-699">Mutex performans bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="d0679-699">Mutex Performance Information Get</span></span> 

#### <a name="tx_mutex_performance_info_get"></a><span data-ttu-id="d0679-700">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-700">tx_mutex_performance_info_get</span></span>

<span data-ttu-id="d0679-701">**Simge** ![ Mutex performans bilgileri al simgesi](./media/user-guide/tx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-701">**Icon** ![Mutex performance information get icon](./media/user-guide/tx-events/image36.png)</span></span>

<span data-ttu-id="d0679-702">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-702">**Description**</span></span>

<span data-ttu-id="d0679-703">Bu olay, tx_mutex_performance_info_get aracılığıyla mutex performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-703">This event represents retrieving mutex performance information via tx_mutex_performance_info_get.</span></span>

<span data-ttu-id="d0679-704">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-704">**Information Fields**</span></span>

- <span data-ttu-id="d0679-705">Bilgi alanı 1: mutex Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-705">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="d0679-706">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-706">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-707">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-707">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-708">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-708">Info Field 4: Not used.</span></span>

### <a name="mutex-performance-system-info-get"></a><span data-ttu-id="d0679-709">Mutex performans sistem bilgisi al</span><span class="sxs-lookup"><span data-stu-id="d0679-709">Mutex Performance System Info Get</span></span>

#### <a name="tx_mutex_performance_system_info_get"></a><span data-ttu-id="d0679-710">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-710">tx_mutex_performance_system_info_get</span></span>

<span data-ttu-id="d0679-711">**Simge** ![ Mutex performans sistem bilgileri al simgesi](./media/user-guide/tx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-711">**Icon** ![Mutex performance system info get icon](./media/user-guide/tx-events/image37.png)</span></span>

<span data-ttu-id="d0679-712">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-712">**Description**</span></span>

<span data-ttu-id="d0679-713">Bu olay, tx_mutex_performance_system_info_get aracılığıyla mutex sistem performansı bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-713">This event represents retrieving mutex system performance information via tx_mutex_performance_system_info_get.</span></span>

<span data-ttu-id="d0679-714">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-714">**Information Fields**</span></span>

- <span data-ttu-id="d0679-715">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-715">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-716">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-716">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-717">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-717">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-718">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-718">Info Field 4: Not used.</span></span>

### <a name="mutex-prioritize"></a><span data-ttu-id="d0679-719">Mutex öncelik</span><span class="sxs-lookup"><span data-stu-id="d0679-719">Mutex Prioritize</span></span> 

#### <a name="tx_mutex_prioritize"></a><span data-ttu-id="d0679-720">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="d0679-720">tx_mutex_prioritize</span></span>

<span data-ttu-id="d0679-721">**Simge** ![ Mutex öncelik simgesi](./media/user-guide/tx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-721">**Icon** ![Mutex prioritize icon](./media/user-guide/tx-events/image38.png)</span></span>

<span data-ttu-id="d0679-722">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-722">**Description**</span></span>

<span data-ttu-id="d0679-723">Bu olay, mutex 'in askıya alma listesinin tx_mutex_prioritize aracılığıyla önceliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-723">This event represents prioritizing the mutex's suspension list via tx_mutex_prioritize.</span></span>

<span data-ttu-id="d0679-724">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-724">**Information Fields**</span></span>

- <span data-ttu-id="d0679-725">Bilgi alanı 1: karşılık gelen mutex Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-725">Info Field 1: Pointer to corresponding mutex.</span></span>
- <span data-ttu-id="d0679-726">Bilgi alanı 2: mutex üzerinde şu anda askıya alınan iş parçacıklarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-726">Info Field 2: Number of threads currently suspended on the mutex.</span></span>
- <span data-ttu-id="d0679-727">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-727">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-728">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-728">Info Field 4: Not used.</span></span>

### <a name="mutex-put"></a><span data-ttu-id="d0679-729">Mutex put</span><span class="sxs-lookup"><span data-stu-id="d0679-729">Mutex Put</span></span> 

#### <a name="tx_mutex_put"></a><span data-ttu-id="d0679-730">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="d0679-730">tx_mutex_put</span></span>

<span data-ttu-id="d0679-731">**Simge** ![ Mutex put simgesi](./media/user-guide/tx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-731">**Icon** ![Mutex put icon](./media/user-guide/tx-events/image39.png)</span></span>

<span data-ttu-id="d0679-732">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-732">**Description**</span></span>

<span data-ttu-id="d0679-733">Bu olay, tx_mutex_put aracılığıyla daha önce sahip olunan bir mutex 'i kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="d0679-733">This event represents releasing a previously owned mutex via tx_mutex_put.</span></span>

<span data-ttu-id="d0679-734">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-734">**Information Fields**</span></span>

- <span data-ttu-id="d0679-735">Bilgi alanı 1: karşılık gelen mutex Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-735">Info Field 1: Pointer to corresponding mutex.</span></span>
- <span data-ttu-id="d0679-736">Bilgi alanı 2: mutex 'e sahip iş parçacığı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-736">Info Field 2: Pointer of thread owning the mutex.</span></span>
- <span data-ttu-id="d0679-737">Bilgi alanı 3: bekleyen mutex GET isteklerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-737">Info Field 3: Number of outstanding mutex get requests.</span></span>
- <span data-ttu-id="d0679-738">Bilgi alanı 4: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-738">Info Field 4: Stack pointer at time of call.</span></span>

### <a name="queue-create"></a><span data-ttu-id="d0679-739">Sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0679-739">Queue Create</span></span> 

#### <a name="tx_queue_create"></a><span data-ttu-id="d0679-740">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="d0679-740">tx_queue_create</span></span>

<span data-ttu-id="d0679-741">**Simge** ![ Kuyruk Oluştur simgesi](./media/user-guide/tx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-741">**Icon** ![Queue create icon](./media/user-guide/tx-events/image40.png)</span></span>

<span data-ttu-id="d0679-742">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-742">**Description**</span></span>

<span data-ttu-id="d0679-743">Bu olay tx_queue_create aracılığıyla bir ileti kuyruğu oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-743">This event represents creating a message queue via tx_queue_create.</span></span>

<span data-ttu-id="d0679-744">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-744">**Information Fields**</span></span>

- <span data-ttu-id="d0679-745">Bilgi alanı 1: kuyruk denetim bloğu Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-745">Info Field 1: Pointer to queue control block.</span></span>
- <span data-ttu-id="d0679-746">Bilgi alanı 2: ileti boyutu-32 bitlik kelimeler.</span><span class="sxs-lookup"><span data-stu-id="d0679-746">Info Field 2: Size of message – in terms of 32-bit words.</span></span>
- <span data-ttu-id="d0679-747">Bilgi alanı 3: kuyruk belleği alanının başlangıcı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-747">Info Field 3: Pointer to start of queue memory area.</span></span>
- <span data-ttu-id="d0679-748">Bilgi alanı 4: kuyruk belleği alanındaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-748">Info Field 4: Number of bytes in the queue memory area.</span></span>

### <a name="queue-delete"></a><span data-ttu-id="d0679-749">Kuyruğu silme</span><span class="sxs-lookup"><span data-stu-id="d0679-749">Queue Delete</span></span> 

#### <a name="tx_queue_delete"></a><span data-ttu-id="d0679-750">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-750">tx_queue_delete</span></span>

<span data-ttu-id="d0679-751">**Simge** ![ Kuyruk silme simgesi](./media/user-guide/tx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-751">**Icon** ![Queue delete icon](./media/user-guide/tx-events/image41.png)</span></span>

<span data-ttu-id="d0679-752">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-752">**Description**</span></span>

<span data-ttu-id="d0679-753">Bu olay tx_queue_delete aracılığıyla bir kuyruğu silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-753">This event represents deleting a queue via tx_queue_delete.</span></span>

<span data-ttu-id="d0679-754">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-754">**Information Fields**</span></span>

- <span data-ttu-id="d0679-755">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-755">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-756">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-756">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-757">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-757">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-758">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-758">Info Field 4: Not used.</span></span>

### <a name="queue-flush"></a><span data-ttu-id="d0679-759">Kuyruğu Temizleme</span><span class="sxs-lookup"><span data-stu-id="d0679-759">Queue Flush</span></span> 

#### <a name="tx_queue_flush"></a><span data-ttu-id="d0679-760">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="d0679-760">tx_queue_flush</span></span>

<span data-ttu-id="d0679-761">**Simge** ![ Kuyruğu Temizleme simgesi](./media/user-guide/tx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-761">**Icon** ![Queue flush icon](./media/user-guide/tx-events/image42.png)</span></span>

<span data-ttu-id="d0679-762">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-762">**Description**</span></span>

<span data-ttu-id="d0679-763">Bu olay, tx_queue_flush aracılığıyla bir kuyruğun Temizleme (tüm kuyruk içeriğini temizleme) işlemini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-763">This event represents flushing (clearing all queue contents) of a queue via tx_queue_flush.</span></span>

<span data-ttu-id="d0679-764">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-764">**Information Fields**</span></span>

- <span data-ttu-id="d0679-765">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-765">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-766">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-766">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-767">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-767">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-768">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-768">Info Field 4: Not used.</span></span>

### <a name="queue-front-send"></a><span data-ttu-id="d0679-769">Kuyruk ön gönderimi</span><span class="sxs-lookup"><span data-stu-id="d0679-769">Queue Front Send</span></span> 

#### <a name="tx_queue_front_send"></a><span data-ttu-id="d0679-770">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="d0679-770">tx_queue_front_send</span></span>

<span data-ttu-id="d0679-771">**Simge** ![ Kuyruk ön Gönder simgesi](./media/user-guide/tx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-771">**Icon** ![Queue front send icon](./media/user-guide/tx-events/image43.png)</span></span>

<span data-ttu-id="d0679-772">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-772">**Description**</span></span>

<span data-ttu-id="d0679-773">Bu olay tx_queue_front_send aracılığıyla bir kuyruğun önüne ileti gönderilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-773">This event represents sending a message to the front of a queue via tx_queue_front_send.</span></span>

<span data-ttu-id="d0679-774">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-774">**Information Fields**</span></span>

- <span data-ttu-id="d0679-775">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-775">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-776">Bilgi alanı 2: ileti başlangıcı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-776">Info Field 2: Pointer to start of message.</span></span>
- <span data-ttu-id="d0679-777">Bilgi alanı 3: bekleme seçeneği sağlandı</span><span class="sxs-lookup"><span data-stu-id="d0679-777">Info Field 3: Wait option supplied to the</span></span>
- <span data-ttu-id="d0679-778">tx_queue_front_send çağrısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-778">tx_queue_front_send call.</span></span>
- <span data-ttu-id="d0679-779">Bilgi alanı 4: zaten sıralanmış ileti sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-779">Info Field 4: Number of messages already enqueued.</span></span>

### <a name="queue-information-get"></a><span data-ttu-id="d0679-780">Kuyruk bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="d0679-780">Queue Information Get</span></span> 

#### <a name="tx_queue_info_get"></a><span data-ttu-id="d0679-781">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-781">tx_queue_info_get</span></span>

<span data-ttu-id="d0679-782">**Simge** ![ Kuyruk bilgileri alma simgesi](./media/user-guide/tx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-782">**Icon** ![Queue information get icon](./media/user-guide/tx-events/image44.png)</span></span>

<span data-ttu-id="d0679-783">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-783">**Description**</span></span>

<span data-ttu-id="d0679-784">Bu olay tx_queue_info_get aracılığıyla bir sıra hakkında bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-784">This event represents getting information about a queue via tx_queue_info_get.</span></span>

<span data-ttu-id="d0679-785">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-785">**Information Fields**</span></span> 
- <span data-ttu-id="d0679-786">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-786">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-787">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-787">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-788">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-788">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-789">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-789">Info Field 4: Not used.</span></span>

### <a name="queue-performance-info-get"></a><span data-ttu-id="d0679-790">Sıra performans bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="d0679-790">Queue Performance Info Get</span></span> 

#### <a name="tx_queue_performance_info_get"></a><span data-ttu-id="d0679-791">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-791">tx_queue_performance_info_get</span></span>

<span data-ttu-id="d0679-792">**Simge** ![ Sıra performans bilgileri alma simgesi](./media/user-guide/tx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-792">**Icon** ![Queue performance info get icon](./media/user-guide/tx-events/image45.png)</span></span>

<span data-ttu-id="d0679-793">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-793">**Description**</span></span>

<span data-ttu-id="d0679-794">Bu olay tx_queue_performance_info_get aracılığıyla bir kuyrukla ilgili performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-794">This event represents getting performance information about a queue via tx_queue_performance_info_get.</span></span>

<span data-ttu-id="d0679-795">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-795">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-796">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-796">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-797">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-797">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-798">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-798">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-799">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-799">Info Field 4: Not used.</span></span>

### <a name="queue-performance-system-info-get"></a><span data-ttu-id="d0679-800">Performans sistemi bilgilerini sıraya al</span><span class="sxs-lookup"><span data-stu-id="d0679-800">Queue Performance System Info Get</span></span> 

#### <a name="tx_queue_performance_system_info_get"></a><span data-ttu-id="d0679-801">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-801">tx_queue_performance_system_info_get</span></span>

<span data-ttu-id="d0679-802">**Simge** ![ Sıra performansı sistem bilgileri alma simgesi](./media/user-guide/tx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-802">**Icon** ![Queue performance system info get icon](./media/user-guide/tx-events/image46.png)</span></span>

<span data-ttu-id="d0679-803">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-803">**Description**</span></span>

<span data-ttu-id="d0679-804">Bu olay, sistemdeki tüm kuyrukların sistem performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-804">This event represents getting system performance information about all the queues in the system.</span></span>

<span data-ttu-id="d0679-805">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-805">**Information Fields**</span></span>

- <span data-ttu-id="d0679-806">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-806">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-807">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-807">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-808">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-808">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-809">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-809">Info Field 4: Not used.</span></span>

### <a name="queue-prioritize"></a><span data-ttu-id="d0679-810">Kuyruk önceliği belirleme</span><span class="sxs-lookup"><span data-stu-id="d0679-810">Queue Prioritize</span></span> 

#### <a name="tx_queue_prioritize"></a><span data-ttu-id="d0679-811">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="d0679-811">tx_queue_prioritize</span></span>

<span data-ttu-id="d0679-812">**Simge** ![ Sıra önceliği belirleme simgesi](./media/user-guide/tx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-812">**Icon** ![Queue prioritize icon](./media/user-guide/tx-events/image47.png)</span></span>

<span data-ttu-id="d0679-813">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-813">**Description**</span></span>

<span data-ttu-id="d0679-814">Bu olay, sıranın askıya alınma listesinin tx_queue_prioritize aracılığıyla önceliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-814">This event represents prioritizing the queue's suspension list via tx_queue_prioritize.</span></span>

<span data-ttu-id="d0679-815">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-815">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-816">Bilgi alanı 1: karşılık gelen sıraya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-816">Info Field 1: Pointer to corresponding queue.</span></span>
- <span data-ttu-id="d0679-817">Bilgi alanı 2: sırada askıya alınmış olan iş parçacıklarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-817">Info Field 2: Number of threads currently suspended on the queue.</span></span>
- <span data-ttu-id="d0679-818">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-818">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-819">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-819">Info Field 4: Not used.</span></span>

#### <a name="queue-receive"></a><span data-ttu-id="d0679-820">Kuyruk alma</span><span class="sxs-lookup"><span data-stu-id="d0679-820">Queue Receive</span></span> 

##### <a name="tx_queue_receive"></a><span data-ttu-id="d0679-821">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="d0679-821">tx_queue_receive</span></span>

<span data-ttu-id="d0679-822">**Simge** ![ Kuyruk alma simgesi](./media/user-guide/tx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-822">**Icon** ![Queue receive icon](./media/user-guide/tx-events/image48.png)</span></span>

<span data-ttu-id="d0679-823">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-823">**Description**</span></span>

<span data-ttu-id="d0679-824">Bu olay, tx_queue_receive aracılığıyla bir kuyruktan ileti almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-824">This event represents receiving a message from a queue via tx_queue_receive.</span></span>

<span data-ttu-id="d0679-825">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-825">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-826">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-826">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-827">Bilgi alanı 2: ileti hedefi Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-827">Info Field 2: Pointer to destination for message.</span></span> <span data-ttu-id="d0679-828">Bilgi alanı 3: çağrıya izin verilen bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d0679-828">Info Field 3: Wait option supplied to the call.</span></span>
- <span data-ttu-id="d0679-829">Bilgi alanı 4: Şu anda sıradaki ileti sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-829">Info Field 4: Number of messages currently queued.</span></span>

### <a name="queue-send"></a><span data-ttu-id="d0679-830">Kuyruğu gönder</span><span class="sxs-lookup"><span data-stu-id="d0679-830">Queue Send</span></span> 

#### <a name="tx_queue_send"></a><span data-ttu-id="d0679-831">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="d0679-831">tx_queue_send</span></span>

<span data-ttu-id="d0679-832">**Simge** ![ Kuyruk Gönder simgesi](./media/user-guide/tx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-832">**Icon** ![Queue send icon](./media/user-guide/tx-events/image49.png)</span></span>

<span data-ttu-id="d0679-833">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-833">**Description**</span></span>

<span data-ttu-id="d0679-834">Bu olay tx_queue_send aracılığıyla bir kuyruğa ileti göndermeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-834">This event represents sending a message to a queue via tx_queue_send.</span></span>

<span data-ttu-id="d0679-835">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-835">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-836">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-836">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-837">Bilgi alanı 2: ileti Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-837">Info Field 2: Pointer to message.</span></span>
- <span data-ttu-id="d0679-838">Bilgi alanı 3: çağrıya izin verilen bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d0679-838">Info Field 3: Wait option supplied to the call.</span></span>
- <span data-ttu-id="d0679-839">Bilgi alanı 4: Şu anda sıradaki ileti sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-839">Info Field 4: Number of messages currently queued.</span></span>

### <a name="queue-send-notify"></a><span data-ttu-id="d0679-840">Kuyruk gönderme bildirimi</span><span class="sxs-lookup"><span data-stu-id="d0679-840">Queue Send Notify</span></span> 

#### <a name="tx_queue_send_notify"></a><span data-ttu-id="d0679-841">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="d0679-841">tx_queue_send_notify</span></span>

<span data-ttu-id="d0679-842">**Simge** ![ Kuyruk gönder bildirim simgesi](./media/user-guide/tx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-842">**Icon** ![Queue send notify icon](./media/user-guide/tx-events/image50.png)</span></span>

<span data-ttu-id="d0679-843">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-843">**Description**</span></span>

<p><span data-ttu-id="d0679-844">Bu olay, bir sıraya her ileti gönderildiğinde çağrılan tx_queue_send_notify aracılığıyla geri çağırma kaydını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-844">This event represents registering a callback via tx_queue_send_notify which is called whenever a message is sent to a queue.</span></span>

<span data-ttu-id="d0679-845">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-845">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-846">Bilgi alanı 1: kuyruk Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-846">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="d0679-847">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-847">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-848">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-848">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-849">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-849">Info Field 4: Not used.</span></span>

### <a name="semaphore-ceiling-put"></a><span data-ttu-id="d0679-850">Semafor tavan koyma</span><span class="sxs-lookup"><span data-stu-id="d0679-850">Semaphore Ceiling Put</span></span> 

#### <a name="tx_semaphore_ceiling_put"></a><span data-ttu-id="d0679-851">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="d0679-851">tx_semaphore_ceiling_put</span></span>

<span data-ttu-id="d0679-852">**Simge** ![ Semafor tavan koyma simgesi](./media/user-guide/tx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-852">**Icon** ![Semaphore ceiling put icon](./media/user-guide/tx-events/image51.png)</span></span>

<span data-ttu-id="d0679-853">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-853">**Description**</span></span>

<span data-ttu-id="d0679-854">Bu olay tx_semaphore_ceiling_put aracılığıyla bir semafora yerleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-854">This event represents putting to a semaphore via tx_semaphore_ceiling_put.</span></span> <span data-ttu-id="d0679-855">Bu, semaforun en büyük değerinin incelendiğinden ve put işleminin en büyük değer veya tavan boyutunu aşmasına izin verilmediğinden tx_semaphore_put farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d0679-855">This differs from tx_semaphore_put in that the maximum value of the semaphore is examined such that the put operation is not allowed to exceed the maximum value or ceiling.</span></span>

<span data-ttu-id="d0679-856">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-856">**Information Fields**</span></span>

- <span data-ttu-id="d0679-857">Bilgi alanı 1: semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-857">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="d0679-858">Bilgi alanı 2: geçerli semafor sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-858">Info Field 2: Current semaphore count.</span></span>
- <span data-ttu-id="d0679-859">Bilgi alanı 3: semaforda askıya alınan iş parçacığı sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-859">Info Field 3: Number of threads suspended on the semaphore.</span></span>
- <span data-ttu-id="d0679-860">Bilgi alanı 4: çağrıya tavan sınırı sağlandı.</span><span class="sxs-lookup"><span data-stu-id="d0679-860">Info Field 4: Ceiling limit supplied to the call.</span></span>

#### <a name="semaphore-create"></a><span data-ttu-id="d0679-861">Semafor oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0679-861">Semaphore Create</span></span> 

##### <a name="tx_semaphore_create"></a><span data-ttu-id="d0679-862">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="d0679-862">tx_semaphore_create</span></span>

<span data-ttu-id="d0679-863">**Simge** ![ Semafor Oluştur simgesi](./media/user-guide/tx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-863">**Icon** ![Semaphore create icon](./media/user-guide/tx-events/image52.png)</span></span>

<span data-ttu-id="d0679-864">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-864">**Description**</span></span>

<span data-ttu-id="d0679-865">Bu olay tx_semaphore_create aracılığıyla semafor oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-865">This event represents creating a semaphore via tx_semaphore_create.</span></span>

<span data-ttu-id="d0679-866">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-866">**Information Fields**</span></span>

- <span data-ttu-id="d0679-867">Bilgi alanı 1: semafor denetim bloğu Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-867">Info Field 1: Pointer to semaphore control block.</span></span>
- <span data-ttu-id="d0679-868">Bilgi alanı 2: Ilk semafor sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-868">Info Field 2: Initial semaphore count.</span></span>
- <span data-ttu-id="d0679-869">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-869">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-870">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-870">Info Field 4: Not used.</span></span>

### <a name="semaphore-delete"></a><span data-ttu-id="d0679-871">Semafor silme</span><span class="sxs-lookup"><span data-stu-id="d0679-871">Semaphore Delete</span></span> 

#### <a name="tx_semaphore_delete"></a><span data-ttu-id="d0679-872">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-872">tx_semaphore_delete</span></span>

<span data-ttu-id="d0679-873">**Simge** ![ Semafor silme simgesi](./media/user-guide/tx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-873">**Icon** ![Semaphore delete icon](./media/user-guide/tx-events/image53.png)</span></span>

<span data-ttu-id="d0679-874">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-874">**Description**</span></span>

<span data-ttu-id="d0679-875">Bu olay tx_semaphore_delete aracılığıyla bir semaforu silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-875">This event represents deleting a semaphore via tx_semaphore_delete.</span></span>

<span data-ttu-id="d0679-876">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-876">**Information Fields**</span></span>

- <span data-ttu-id="d0679-877">Bilgi alanı 1: semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-877">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="d0679-878">NFO alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-878">nfo Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-879">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-879">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-880">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-880">Info Field 4: Not used.</span></span>

### <a name="semaphore-get"></a><span data-ttu-id="d0679-881">Semafor al</span><span class="sxs-lookup"><span data-stu-id="d0679-881">Semaphore Get</span></span> 

#### <a name="tx_semaphore_get"></a><span data-ttu-id="d0679-882">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="d0679-882">tx_semaphore_get</span></span>

<span data-ttu-id="d0679-883">**Simge** ![ Semafor al simgesi](./media/user-guide/tx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-883">**Icon** ![Semaphore get icon](./media/user-guide/tx-events/image54.png)</span></span>

<span data-ttu-id="d0679-884">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-884">**Description**</span></span>

<span data-ttu-id="d0679-885">Bu olay tx_semaphore_get aracılığıyla bir semafor edinmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-885">This event represents obtaining a semaphore via tx_semaphore_get.</span></span>

<span data-ttu-id="d0679-886">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-886">**Information Fields**</span></span>

- <span data-ttu-id="d0679-887">Bilgi alanı 1: semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-887">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="d0679-888">Bilgi alanı 2: çağrıya izin verilen bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d0679-888">Info Field 2: Wait option supplied to the call.</span></span>
- <span data-ttu-id="d0679-889">Bilgi alanı 3: geçerli semafor sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-889">Info Field 3: Current semaphore count.</span></span>
- <span data-ttu-id="d0679-890">Bilgi alanı 4: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-890">Info Field 4: Stack pointer at time of call.</span></span>

### <a name="semaphore-information-get"></a><span data-ttu-id="d0679-891">Semafor bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="d0679-891">Semaphore Information Get</span></span> 

#### <a name="tx_semaphore_info_get"></a><span data-ttu-id="d0679-892">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-892">tx_semaphore_info_get</span></span>

<span data-ttu-id="d0679-893">**Simge** ![ Semafor bilgileri al simgesi](./media/user-guide/tx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-893">**Icon** ![Semaphore information get icon](./media/user-guide/tx-events/image55.png)</span></span>

<span data-ttu-id="d0679-894">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-894">**Description**</span></span>

<span data-ttu-id="d0679-895">Bu olay, tx_semaphore_info_get aracılığıyla bir semafor hakkında bilgi edinmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-895">This event represents obtaining information about a semaphore via tx_semaphore_info_get.</span></span>

<span data-ttu-id="d0679-896">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-896">**Information Fields**</span></span>

- <span data-ttu-id="d0679-897">Bilgi alanı 1: semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-897">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="d0679-898">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-898">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-899">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-899">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-900">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-900">Info Field 4: Not used.</span></span>

### <a name="semaphore-performance-info-get"></a><span data-ttu-id="d0679-901">Semafor performans bilgisi al</span><span class="sxs-lookup"><span data-stu-id="d0679-901">Semaphore Performance Info Get</span></span> 

#### <a name="tx_semaphore_performance_info_get"></a><span data-ttu-id="d0679-902">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-902">tx_semaphore_performance_info_get</span></span>

<span data-ttu-id="d0679-903">**Simge** ![ Semafor performans bilgisi al simgesi](./media/user-guide/tx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-903">**Icon** ![Semaphore performance info get icon](./media/user-guide/tx-events/image56.png)</span></span>

<span data-ttu-id="d0679-904">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-904">**Description**</span></span>

<span data-ttu-id="d0679-905">Bu olay, tx_semaphore_performance_info_get aracılığıyla bir semafor hakkındaki performans bilgilerini elde eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-905">This event represents obtaining performance information about a semaphore via tx_semaphore_performance_info_get.</span></span>

<span data-ttu-id="d0679-906">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-906">**Information Fields**</span></span>

- <span data-ttu-id="d0679-907">Bilgi alanı 1: semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-907">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="d0679-908">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-908">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-909">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-909">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-910">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-910">Info Field 4: Not used.</span></span>

### <a name="semaphore-performance-system-info"></a><span data-ttu-id="d0679-911">Semafor performansı sistem bilgileri</span><span class="sxs-lookup"><span data-stu-id="d0679-911">Semaphore Performance System Info</span></span> 

#### <a name="tx_semaphore_performance_system_info_get"></a><span data-ttu-id="d0679-912">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-912">tx_semaphore_performance_system_info_get</span></span>

<span data-ttu-id="d0679-913">**Simge** ![ Semafor performansı sistem bilgisi simgesi](./media/user-guide/tx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-913">**Icon** ![Semaphore performance system info icon](./media/user-guide/tx-events/image57.png)</span></span>

<span data-ttu-id="d0679-914">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-914">**Description**</span></span>

<span data-ttu-id="d0679-915">Bu olay, tx_semaphore_performance_system_info_get aracılığıyla sistemdeki tüm Semaforlar hakkında performans bilgilerini elde eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-915">This event represents obtaining performance information about all semaphores in the system via tx_semaphore_performance_system_info_get.</span></span>

<span data-ttu-id="d0679-916">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-916">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-917">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-917">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-918">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-918">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-919">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-919">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-920">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-920">Info Field 4: Not used.</span></span>

### <a name="semaphore-prioritize"></a><span data-ttu-id="d0679-921">Semafor önceliği belirleme</span><span class="sxs-lookup"><span data-stu-id="d0679-921">Semaphore Prioritize</span></span> 

#### <a name="tx_semaphore_prioritize"></a><span data-ttu-id="d0679-922">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="d0679-922">tx_semaphore_prioritize</span></span>

<span data-ttu-id="d0679-923">**Simge** ![ Semafor önceliği belirleme simgesi](./media/user-guide/tx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-923">**Icon** ![Semaphore prioritize icon](./media/user-guide/tx-events/image58.png)</span></span>

<span data-ttu-id="d0679-924">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-924">**Description**</span></span>

<span data-ttu-id="d0679-925">Bu olay, tx_semaphore_prioritize aracılığıyla semafor askıya alma listesinin önceliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-925">This event represents prioritizing the semaphore's suspension list via tx_semaphore_prioritize.</span></span>

<span data-ttu-id="d0679-926">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-926">**Information Fields**</span></span>

- <span data-ttu-id="d0679-927">Bilgi alanı 1: karşılık gelen semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-927">Info Field 1: Pointer to corresponding semaphore.</span></span>
- <span data-ttu-id="d0679-928">Bilgi alanı 2: semafor üzerinde şu anda askıya alınan iş parçacığı sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-928">Info Field 2: Number of threads currently suspended on the semaphore.</span></span>
- <span data-ttu-id="d0679-929">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-929">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-930">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-930">Info Field 4: Not used.</span></span>

### <a name="semaphore-put"></a><span data-ttu-id="d0679-931">Semafor put</span><span class="sxs-lookup"><span data-stu-id="d0679-931">Semaphore Put</span></span> 

#### <a name="tx_semaphore_put"></a><span data-ttu-id="d0679-932">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="d0679-932">tx_semaphore_put</span></span>

<span data-ttu-id="d0679-933">**Simge** ![ Semafor put simgesi](./media/user-guide/tx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-933">**Icon** ![Semaphore put icon](./media/user-guide/tx-events/image59.png)</span></span>

<span data-ttu-id="d0679-934">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-934">**Description**</span></span>

<span data-ttu-id="d0679-935">Bu olay tx_semaphore_put aracılığıyla bir semafor örneği serbest bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-935">This event represents releasing a semaphore instance via tx_semaphore_put.</span></span>

<span data-ttu-id="d0679-936">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-936">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-937">Bilgi alanı 1: karşılık gelen semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-937">Info Field 1: Pointer to corresponding semaphore.</span></span> <span data-ttu-id="d0679-938">Bilgi alanı 2: geçerli semafor sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-938">Info Field 2: Current semaphore count.</span></span>
- <span data-ttu-id="d0679-939">Bilgi alanı 3: semaforda askıya alınan iş parçacığı sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-939">Info Field 3: Number of threads suspended on the semaphore.</span></span>
- <span data-ttu-id="d0679-940">Bilgi alanı 4: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-940">Info Field 4: Stack pointer at time of call.</span></span>

### <a name="semaphore-put-notify"></a><span data-ttu-id="d0679-941">Semafor put bildirimi</span><span class="sxs-lookup"><span data-stu-id="d0679-941">Semaphore Put Notify</span></span> 

#### <a name="tx_semaphore_put_notify"></a><span data-ttu-id="d0679-942">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="d0679-942">tx_semaphore_put_notify</span></span>

<span data-ttu-id="d0679-943">**Simge** ![ Semafor put bildirim simgesi](./media/user-guide/tx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-943">**Icon** ![Semaphore put notify icon](./media/user-guide/tx-events/image60.png)</span></span>

<span data-ttu-id="d0679-944">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-944">**Description**</span></span>

<span data-ttu-id="d0679-945">Bu olay, bir semafor örneği her gerçekleştiğinde çağrılan tx_semaphore_put_notify aracılığıyla geri çağırma kaydını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-945">This event represents registering a callback via tx_semaphore_put_notify that is called whenever a semaphore instance is put.</span></span>

<span data-ttu-id="d0679-946">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-946">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-947">Bilgi alanı 1: semafor Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-947">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="d0679-948">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-948">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-949">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-949">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-950">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-950">Info Field 4: Not used.</span></span>

### <a name="thread-create"></a><span data-ttu-id="d0679-951">İş parçacığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0679-951">Thread Create</span></span> 

#### <a name="tx_thread_create"></a><span data-ttu-id="d0679-952">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="d0679-952">tx_thread_create</span></span>

<span data-ttu-id="d0679-953">**Simge** ![ İş parçacığı Oluştur simgesi](./media/user-guide/tx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-953">**Icon** ![Thread create icon](./media/user-guide/tx-events/image61.png)</span></span>

<span data-ttu-id="d0679-954">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-954">**Description**</span></span>

<span data-ttu-id="d0679-955">Bu olay tx_thread_create aracılığıyla bir iş parçacığı oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-955">This event represents creating a thread via tx_thread_create.</span></span>

<span data-ttu-id="d0679-956">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-956">**Information Fields**</span></span>

- <span data-ttu-id="d0679-957">Bilgi alanı 1: iş parçacığı denetim bloğu Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-957">Info Field 1: Pointer to thread control block.</span></span>
- <span data-ttu-id="d0679-958">Bilgi alanı 2: iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="d0679-958">Info Field 2: Priority of thread.</span></span>
- <span data-ttu-id="d0679-959">Bilgi alanı 3: iş parçacığı için yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-959">Info Field 3: Stack pointer for thread.</span></span>
- <span data-ttu-id="d0679-960">NFO alanı 4: yığın boyutu bayt cinsinden.</span><span class="sxs-lookup"><span data-stu-id="d0679-960">nfo Field 4: Size of stack in bytes.</span></span>

### <a name="thread-delete"></a><span data-ttu-id="d0679-961">İş parçacığı silme</span><span class="sxs-lookup"><span data-stu-id="d0679-961">Thread Delete</span></span> 

#### <a name="tx_thread_delete"></a><span data-ttu-id="d0679-962">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-962">tx_thread_delete</span></span>

<span data-ttu-id="d0679-963">**Simge** ![ İş parçacığı silme simgesi](./media/user-guide/tx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-963">**Icon** ![Thread delete icon](./media/user-guide/tx-events/image62.png)</span></span>

<span data-ttu-id="d0679-964">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-964">**Description**</span></span>

<span data-ttu-id="d0679-965">Bu olay tx_thread_delete aracılığıyla bir iş parçacığını silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-965">This event represents deleting a thread via tx_thread_delete.</span></span>

<span data-ttu-id="d0679-966">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-966">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-967">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-967">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-968">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-968">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-969">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-969">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-970">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-970">Info Field 4: Not used.</span></span>

### <a name="thread-entryexit-notify"></a><span data-ttu-id="d0679-971">İş parçacığı giriş/çıkış bildirimi</span><span class="sxs-lookup"><span data-stu-id="d0679-971">Thread Entry/Exit Notify</span></span> 

#### <a name="tx_thread_entry_exit_notify"></a><span data-ttu-id="d0679-972">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="d0679-972">tx_thread_entry_exit_notify</span></span>

<span data-ttu-id="d0679-973">**Simge** ![ İş parçacığı girişi/çıkış bildirimi simgesi](./media/user-guide/tx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-973">**Icon** ![Thread entry/exit notify icon](./media/user-guide/tx-events/image63.png)</span></span>

<span data-ttu-id="d0679-974">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-974">**Description**</span></span>

<span data-ttu-id="d0679-975">Bu olay, bir iş parçacığı girildiğinde veya çıktığında çağrılan tx_thread_entry_exit_notify aracılığıyla geri çağırma kaydını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-975">This event represents registering a callback via tx_thread_entry_exit_notify that is called whenever a thread is entered or exits.</span></span>

<span data-ttu-id="d0679-976">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-976">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-977">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-977">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-978">Bilgi alanı 2: kayıt sırasında Iş parçacığı durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-978">Info Field 2: Thread state at time of the registration.</span></span>
- <span data-ttu-id="d0679-979">Bilgi alanı 3: çağrı sırasında yığın Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-979">Info Field 3: Pointer to stack at time of call.</span></span>
- <span data-ttu-id="d0679-980">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-980">Info Field 4: Not used.</span></span>

#### <a name="thread-identify"></a><span data-ttu-id="d0679-981">İş parçacığı tanımla</span><span class="sxs-lookup"><span data-stu-id="d0679-981">Thread Identify</span></span> 

##### <a name="tx_thread_identify"></a><span data-ttu-id="d0679-982">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="d0679-982">tx_thread_identify</span></span>

<span data-ttu-id="d0679-983">**Simge** ![ İş parçacığı tanımla simgesi](./media/user-guide/tx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-983">**Icon** ![Thread identify icon](./media/user-guide/tx-events/image64.png)</span></span>

<span data-ttu-id="d0679-984">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-984">**Description**</span></span>

<span data-ttu-id="d0679-985">Bu olay, geçerli iş parçacığı işaretçisinin tx_thread_identify aracılığıyla alınmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-985">This event represents getting the current thread pointer via tx_thread_identify.</span></span>

<span data-ttu-id="d0679-986">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-986">**Information Fields**</span></span>

- <span data-ttu-id="d0679-987">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-987">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-988">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-988">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-989">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-989">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-990">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-990">Info Field 4: Not used.</span></span>

### <a name="thread-information-get"></a><span data-ttu-id="d0679-991">İş parçacığı bilgileri al</span><span class="sxs-lookup"><span data-stu-id="d0679-991">Thread Information Get</span></span> 

#### <a name="tx_thread_info_get"></a><span data-ttu-id="d0679-992">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-992">tx_thread_info_get</span></span>

<span data-ttu-id="d0679-993">**Simge** ![ İş parçacığı bilgileri al simgesi](./media/user-guide/tx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-993">**Icon** ![Thread information get icon](./media/user-guide/tx-events/image65.png)</span></span>

<span data-ttu-id="d0679-994">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-994">**Description**</span></span>

<span data-ttu-id="d0679-995">Bu olay, tx_thread_info_get aracılığıyla belirtilen iş parçacığı hakkında bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-995">This event represents getting information about the specified thread via tx_thread_info_get.</span></span>

<span data-ttu-id="d0679-996">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-996">**Information Fields**</span></span>

- <span data-ttu-id="d0679-997">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-997">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-998">Bilgi alanı 2: çağrı sırasında iş parçacığının durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-998">Info Field 2: State of thread at time of call.</span></span>
- <span data-ttu-id="d0679-999">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-999">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1000">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1000">Info Field 4: Not used.</span></span>

#### <a name="thread-performance-information-get"></a><span data-ttu-id="d0679-1001">İş parçacığı performans bilgileri al</span><span class="sxs-lookup"><span data-stu-id="d0679-1001">Thread Performance Information Get</span></span> 

##### <a name="tx_thread_performance_info_get"></a><span data-ttu-id="d0679-1002">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-1002">tx_thread_performance_info_get</span></span>

<span data-ttu-id="d0679-1003">**Simge** ![ İş parçacığı performans bilgileri al simgesi](./media/user-guide/tx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1003">**Icon** ![Thread performance information get icon](./media/user-guide/tx-events/image66.png)</span></span>

<span data-ttu-id="d0679-1004">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1004">**Description**</span></span>

<span data-ttu-id="d0679-1005">Bu olay, tx_thread_performance_info_get aracılığıyla belirtilen iş parçacığıyla ilgili performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1005">This event represents getting performance information about the specified thread via tx_thread_performance_info_get.</span></span>

<span data-ttu-id="d0679-1006">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1006">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1007">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1007">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-1008">Bilgi alanı 2: çağrı sırasında iş parçacığının durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1008">Info Field 2: State of thread at time of call.</span></span>
- <span data-ttu-id="d0679-1009">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1009">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1010">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1010">Info Field 4: Not used.</span></span>

### <a name="thread-performance-system-info-get"></a><span data-ttu-id="d0679-1011">İş parçacığı performans sistem bilgileri al</span><span class="sxs-lookup"><span data-stu-id="d0679-1011">Thread Performance System Info Get</span></span> 

#### <a name="tx_thread_performance_system_info_get"></a><span data-ttu-id="d0679-1012">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-1012">tx_thread_performance_system_info_get</span></span>

<span data-ttu-id="d0679-1013">**Simge** ![ İş parçacığı performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1013">**Icon** ![Thread performance system info get icon](./media/user-guide/tx-events/image67.png)</span></span>

<span data-ttu-id="d0679-1014">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1014">**Description**</span></span>

<span data-ttu-id="d0679-1015">Bu olay, tüm iş parçacıkları hakkındaki tx_thread_performance_system_info_get aracılığıyla performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1015">This event represents getting performance information about all threads via tx_thread_performance_system_info_get.</span></span>

<span data-ttu-id="d0679-1016">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1016">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-1017">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1017">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-1018">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1018">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-1019">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1019">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1020">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1020">Info Field 4: Not used.</span></span>

### <a name="thread-preemption-change"></a><span data-ttu-id="d0679-1021">İş parçacığı önalım değişikliği</span><span class="sxs-lookup"><span data-stu-id="d0679-1021">Thread Preemption Change</span></span> 

#### <a name="tx_thread_preemption_change"></a><span data-ttu-id="d0679-1022">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="d0679-1022">tx_thread_preemption_change</span></span>

<span data-ttu-id="d0679-1023">**Simge** ![ İş parçacığı önalım Değiştir simgesi](./media/user-guide/tx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1023">**Icon** ![Thread preemption change icon](./media/user-guide/tx-events/image68.png)</span></span>

<span data-ttu-id="d0679-1024">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1024">**Description**</span></span>

<span data-ttu-id="d0679-1025">Bu olay, bir iş parçacığının önalım-Threshold tx_thread_preemption_change aracılığıyla değiştirilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1025">This event represents changing a thread's preemption-threshold via tx_thread_preemption_change.</span></span>

<span data-ttu-id="d0679-1026">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1026">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-1027">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1027">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-1028">Bilgi alanı 2: New önalım-Threshold.</span><span class="sxs-lookup"><span data-stu-id="d0679-1028">Info Field 2: New preemption-threshold.</span></span>
- <span data-ttu-id="d0679-1029">Bilgi alanı 3: önceki önalım-Threshold.</span><span class="sxs-lookup"><span data-stu-id="d0679-1029">Info Field 3: Previous preemption-threshold.</span></span>
- <span data-ttu-id="d0679-1030">Bilgi alanı 4: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1030">Info Field 4: Thread's state at time of call.</span></span>

### <a name="thread-priority-change"></a><span data-ttu-id="d0679-1031">İş parçacığı önceliği değişikliği</span><span class="sxs-lookup"><span data-stu-id="d0679-1031">Thread Priority Change</span></span> 

#### <a name="tx_thread_priority_change"></a><span data-ttu-id="d0679-1032">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="d0679-1032">tx_thread_priority_change</span></span>

<span data-ttu-id="d0679-1033">**Simge** ![ İş parçacığı önceliği değişikliği simgesi](./media/user-guide/tx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1033">**Icon** ![Thread priority change icon](./media/user-guide/tx-events/image69.png)</span></span>

<span data-ttu-id="d0679-1034">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1034">**Description**</span></span>

<span data-ttu-id="d0679-1035">Bu olay bir iş parçacığının önceliğini tx_thread_priority_change aracılığıyla değiştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1035">This event represents changing a thread's priority via tx_thread_priority_change.</span></span>

- <span data-ttu-id="d0679-1036">Bilgi alanları</span><span class="sxs-lookup"><span data-stu-id="d0679-1036">Information Fields</span></span> 
- <span data-ttu-id="d0679-1037">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1037">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-1038">Bilgi alanı 2: yeni öncelik.</span><span class="sxs-lookup"><span data-stu-id="d0679-1038">Info Field 2: New priority.</span></span>
- <span data-ttu-id="d0679-1039">Bilgi alanı 3: önceki öncelik.</span><span class="sxs-lookup"><span data-stu-id="d0679-1039">Info Field 3: Previous priority.</span></span>
- <span data-ttu-id="d0679-1040">Bilgi alanı 4: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1040">Info Field 4: Thread's state at time of call.</span></span>

### <a name="thread-relinquish"></a><span data-ttu-id="d0679-1041">İş parçacığı Relinsi</span><span class="sxs-lookup"><span data-stu-id="d0679-1041">Thread Relinquish</span></span> 

#### <a name="tx_thread_relinquish"></a><span data-ttu-id="d0679-1042">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="d0679-1042">tx_thread_relinquish</span></span>

<span data-ttu-id="d0679-1043">**Simge** ![ İş parçacığı relinsi simgesi](./media/user-guide/tx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1043">**Icon** ![Thread relinquish icon](./media/user-guide/tx-events/image70.png)</span></span>

<span data-ttu-id="d0679-1044">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1044">**Description**</span></span>

<span data-ttu-id="d0679-1045">Bu olay, tx_thread_relinquish aracılığıyla bir iş parçacığından işlemciyi yeniden eğme eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1045">This event represents relinquishing the processor from a thread via tx_thread_relinquish.</span></span>

<span data-ttu-id="d0679-1046">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1046">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1047">Bilgi alanı 1: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1047">Info Field 1: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1048">Bilgi alanı 2: yürütülecek sonraki iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1048">Info Field 2: Pointer to the next thread to execute.</span></span>
- <span data-ttu-id="d0679-1049">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1049">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1050">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1050">Info Field 4: Not used.</span></span>

### <a name="thread-reset"></a><span data-ttu-id="d0679-1051">İş parçacığı sıfırlama</span><span class="sxs-lookup"><span data-stu-id="d0679-1051">Thread Reset</span></span> 

#### <a name="tx_thread_reset"></a><span data-ttu-id="d0679-1052">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="d0679-1052">tx_thread_reset</span></span>

<span data-ttu-id="d0679-1053">**Simge** ![ İş parçacığı sıfırlama simgesi](./media/user-guide/tx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1053">**Icon** ![Thread reset icon](./media/user-guide/tx-events/image71.png)</span></span>

<span data-ttu-id="d0679-1054">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1054">**Description**</span></span>

<span data-ttu-id="d0679-1055">Bu olay, tamamlanmış veya sonlandırılmış bir iş parçacığının tx_thread_reset aracılığıyla sıfırlanmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1055">This event represents resetting a completed or terminated thread via tx_thread_reset.</span></span>

<span data-ttu-id="d0679-1056">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1056">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1057">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1057">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-1058">Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1058">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="d0679-1059">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1059">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1060">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1060">Info Field 4: Not used.</span></span>

#### <a name="thread-resume"></a><span data-ttu-id="d0679-1061">İş parçacığı özgeçmişi</span><span class="sxs-lookup"><span data-stu-id="d0679-1061">Thread Resume</span></span> 

##### <a name="tx_thread_resume"></a><span data-ttu-id="d0679-1062">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="d0679-1062">tx_thread_resume</span></span>

<span data-ttu-id="d0679-1063">**Simge** ![ İş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1063">**Icon** ![Thread resume icon](./media/user-guide/tx-events/image72.png)</span></span>

<span data-ttu-id="d0679-1064">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1064">**Description**</span></span>

<span data-ttu-id="d0679-1065">Bu olay, askıya alınmış bir iş parçacığının tx_thread_resume aracılığıyla sürdürülmeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0679-1065">This event represents resuming a suspended thread via tx_thread_resume.</span></span>

<span data-ttu-id="d0679-1066">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1066">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1067">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1067">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-1068">Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1068">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="d0679-1069">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1069">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1070">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1070">Info Field 4: Not used.</span></span>

### <a name="thread-sleep"></a><span data-ttu-id="d0679-1071">İş parçacığı uyuması</span><span class="sxs-lookup"><span data-stu-id="d0679-1071">Thread Sleep</span></span> 

#### <a name="tx_thread_sleep"></a><span data-ttu-id="d0679-1072">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="d0679-1072">tx_thread_sleep</span></span>

<span data-ttu-id="d0679-1073">**Simge** ![ İş parçacığı uyku simgesi](./media/user-guide/tx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1073">**Icon** ![Thread sleep icon](./media/user-guide/tx-events/image73.png)</span></span>

<span data-ttu-id="d0679-1074">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1074">**Description**</span></span>

<span data-ttu-id="d0679-1075">Bu olay, tx_thread_sleep aracılığıyla belirtilen sayıda süreölçer işareti için geçerli iş parçacığını askıya alma temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1075">This event represents suspending the current thread for a specified number of timer ticks via tx_thread_sleep.</span></span>

<span data-ttu-id="d0679-1076">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1076">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1077">Bilgi alanı 1: askıya alınacak onay işareti sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-1077">Info Field 1: Number of ticks to suspend for.</span></span>
- <span data-ttu-id="d0679-1078">Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1078">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="d0679-1079">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1079">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1080">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1080">Info Field 4: Not used.</span></span>

### <a name="thread-stack-error-notify"></a><span data-ttu-id="d0679-1081">İş parçacığı yığını hata bildirimi</span><span class="sxs-lookup"><span data-stu-id="d0679-1081">Thread Stack Error Notify</span></span> 

#### <a name="tx_thread_stack_error_notify_event"></a><span data-ttu-id="d0679-1082">tx_thread_stack_error_notify_event</span><span class="sxs-lookup"><span data-stu-id="d0679-1082">tx_thread_stack_error_notify_event</span></span>

<span data-ttu-id="d0679-1083">**Simge** ![ İş parçacığı yığını hata bildirme simgesi](./media/user-guide/tx-events/image74.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1083">**Icon** ![Thread stack error notify icon](./media/user-guide/tx-events/image74.png)</span></span>

<span data-ttu-id="d0679-1084">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1084">**Description**</span></span>

<span data-ttu-id="d0679-1085">Bu olay, tx_thread_stack_error_notify_event aracılığıyla bir iş parçacığı yığını hata bildirimi yordamının kaydedilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1085">This event represents registering a thread stack error notification routine via tx_thread_stack_error_notify_event.</span></span>

<span data-ttu-id="d0679-1086">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1086">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-1087">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1087">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-1088">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1088">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-1089">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1089">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1090">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1090">Info Field 4: Not used.</span></span>

### <a name="thread-suspend"></a><span data-ttu-id="d0679-1091">İş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="d0679-1091">Thread Suspend</span></span> 

#### <a name="tx_thread_suspend"></a><span data-ttu-id="d0679-1092">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="d0679-1092">tx_thread_suspend</span></span>

<span data-ttu-id="d0679-1093">**Simge** ![ İş parçacığı bekletme simgesi](./media/user-guide/tx-events/image75.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1093">**Icon** ![Thread suspend icon](./media/user-guide/tx-events/image75.png)</span></span>

<span data-ttu-id="d0679-1094">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1094">**Description**</span></span>

<span data-ttu-id="d0679-1095">Bu olay tx_thread_suspend aracılığıyla bir iş parçacığını askıya alma temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1095">This event represents suspending a thread via tx_thread_suspend.</span></span>

<span data-ttu-id="d0679-1096">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1096">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-1097">Bilgi alanı 1: askıya alınacak iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1097">Info Field 1: Pointer to thread to suspend.</span></span>
- <span data-ttu-id="d0679-1098">Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1098">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="d0679-1099">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1099">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1100">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1100">Info Field 4: Not used.</span></span>

### <a name="thread-terminate"></a><span data-ttu-id="d0679-1101">İş parçacığı Sonlandır</span><span class="sxs-lookup"><span data-stu-id="d0679-1101">Thread Terminate</span></span> 

#### <a name="tx_thread_terminate"></a><span data-ttu-id="d0679-1102">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="d0679-1102">tx_thread_terminate</span></span>

<span data-ttu-id="d0679-1103">**Simge** ![ İş parçacığı Sonlandır simgesi](./media/user-guide/tx-events/image76.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1103">**Icon** ![Thread terminate icon](./media/user-guide/tx-events/image76.png)</span></span>

<span data-ttu-id="d0679-1104">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1104">**Description**</span></span>

<span data-ttu-id="d0679-1105">Bu olay bir iş parçacığının tx_thread_terminate aracılığıyla sonlandırılmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1105">This event represents terminating a thread via tx_thread_terminate.</span></span>

<span data-ttu-id="d0679-1106">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1106">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-1107">Bilgi alanı 1: sonlandırılacak iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1107">Info Field 1: Pointer to thread to terminate.</span></span>
- <span data-ttu-id="d0679-1108">Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1108">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="d0679-1109">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1109">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1110">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1110">Info Field 4: Not used.</span></span>

### <a name="thread-time-slice-change"></a><span data-ttu-id="d0679-1111">İş parçacığı Time-Slice değişikliği</span><span class="sxs-lookup"><span data-stu-id="d0679-1111">Thread Time-Slice Change</span></span> 

#### <a name="tx_thread_time_slice_change"></a><span data-ttu-id="d0679-1112">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="d0679-1112">tx_thread_time_slice_change</span></span>

<span data-ttu-id="d0679-1113">**Simge** ![ İş parçacığı zaman dilimi değişikliği simgesi](./media/user-guide/tx-events/image77.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1113">**Icon** ![Thread time-slice change icon](./media/user-guide/tx-events/image77.png)</span></span>

<span data-ttu-id="d0679-1114">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1114">**Description**</span></span>

<span data-ttu-id="d0679-1115">Bu olay, bir iş parçacığının zaman dilimini tx_thread_time_slice_change aracılığıyla değiştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1115">This event represents changing a thread's time-slice via tx_thread_time_slice_change.</span></span>

<span data-ttu-id="d0679-1116">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1116">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1117">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1117">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-1118">Bilgi alanı 2: yeni saat dilimi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1118">Info Field 2: New time-slice.</span></span>
- <span data-ttu-id="d0679-1119">Bilgi alanı 3: önceki zaman dilimi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1119">Info Field 3: Previous time-slice.</span></span>
- <span data-ttu-id="d0679-1120">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1120">Info Field 4: Not used.</span></span>

### <a name="thread-wait-abort"></a><span data-ttu-id="d0679-1121">İş parçacığı beklemeyi durdur</span><span class="sxs-lookup"><span data-stu-id="d0679-1121">Thread Wait Abort</span></span> 

#### <a name="tx_thread_wait_abort"></a><span data-ttu-id="d0679-1122">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="d0679-1122">tx_thread_wait_abort</span></span>

<span data-ttu-id="d0679-1123">**Simge** ![ İş parçacığı beklemeyi durdur simgesi](./media/user-guide/tx-events/image78.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1123">**Icon** ![Thread wait abort icon](./media/user-guide/tx-events/image78.png)</span></span>

<span data-ttu-id="d0679-1124">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1124">**Description**</span></span>

<span data-ttu-id="d0679-1125">Bu olay, bir iş parçacığının askıya alınma tx_thread_wait_abort aracılığıyla iptal eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1125">This event represents aborting a thread's suspension via tx_thread_wait_abort.</span></span>

<span data-ttu-id="d0679-1126">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1126">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1127">Bilgi alanı 1: iş parçacığına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1127">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="d0679-1128">Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.</span><span class="sxs-lookup"><span data-stu-id="d0679-1128">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="d0679-1129">Bilgi alanı 3: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1129">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1130">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1130">Info Field 4: Not used.</span></span>

### <a name="time-get"></a><span data-ttu-id="d0679-1131">Zaman al</span><span class="sxs-lookup"><span data-stu-id="d0679-1131">Time Get</span></span> 

#### <a name="tx_time_get"></a><span data-ttu-id="d0679-1132">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="d0679-1132">tx_time_get</span></span>

<span data-ttu-id="d0679-1133">**Simge** ![ Zaman al simgesi](./media/user-guide/tx-events/image79.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1133">**Icon** ![Time get icon](./media/user-guide/tx-events/image79.png)</span></span>

<span data-ttu-id="d0679-1134">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1134">**Description**</span></span>

<span data-ttu-id="d0679-1135">Bu olay, tx_time_get aracılığıyla geçerli süreölçer işaret sayısını almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1135">This event represents getting the current number of timer ticks via tx_time_get.</span></span>

<span data-ttu-id="d0679-1136">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1136">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1137">Bilgi alanı 1: geçerli süreölçer onay işaretleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-1137">Info Field 1: Current number of timer ticks.</span></span>
- <span data-ttu-id="d0679-1138">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1138">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1139">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1139">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1140">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1140">Info Field 4: Not used.</span></span>

### <a name="time-set"></a><span data-ttu-id="d0679-1141">Zaman kümesi</span><span class="sxs-lookup"><span data-stu-id="d0679-1141">Time Set</span></span> 

#### <a name="tx_time_set"></a><span data-ttu-id="d0679-1142">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="d0679-1142">tx_time_set</span></span>

<span data-ttu-id="d0679-1143">**Simge** ![ Zaman kümesi simgesi](./media/user-guide/tx-events/image80.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1143">**Icon** ![Time set icon](./media/user-guide/tx-events/image80.png)</span></span>

<span data-ttu-id="d0679-1144">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1144">**Description**</span></span>

<span data-ttu-id="d0679-1145">Bu olay, tx_time_set aracılığıyla geçerli süreölçer işareti sayısını ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1145">This event represents setting the current number of timer ticks via tx_time_set.</span></span>

<span data-ttu-id="d0679-1146">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1146">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1147">Bilgi alanı 1: yeni süreölçer onay işaretleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0679-1147">Info Field 1: New number of timer ticks.</span></span>
- <span data-ttu-id="d0679-1148">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1148">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-1149">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1149">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1150">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1150">Info Field 4: Not used.</span></span>

### <a name="timer-activate"></a><span data-ttu-id="d0679-1151">Süreölçer etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d0679-1151">Timer Activate</span></span> 

#### <a name="tx_timer_activate"></a><span data-ttu-id="d0679-1152">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="d0679-1152">tx_timer_activate</span></span>

<span data-ttu-id="d0679-1153">**Simge** ![ Süreölçer etkinleştirme simgesi](./media/user-guide/tx-events/image81.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1153">**Icon** ![Timer activate icon](./media/user-guide/tx-events/image81.png)</span></span>

<span data-ttu-id="d0679-1154">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1154">**Description**</span></span>

<span data-ttu-id="d0679-1155">Bu olay, tx_timer_activate aracılığıyla belirtilen süreölçeri etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1155">This event represents activating the specified timer via tx_timer_activate.</span></span>

<span data-ttu-id="d0679-1156">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1156">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1157">Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1157">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="d0679-1158">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1158">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-1159">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1159">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1160">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1160">Info Field 4: Not used.</span></span>

### <a name="timer-change"></a><span data-ttu-id="d0679-1161">Süreölçer değişikliği</span><span class="sxs-lookup"><span data-stu-id="d0679-1161">Timer Change</span></span> 

#### <a name="tx_timer_change"></a><span data-ttu-id="d0679-1162">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="d0679-1162">tx_timer_change</span></span>

<span data-ttu-id="d0679-1163">**Simge** ![ Süreölçer değişikliği simgesi](./media/user-guide/tx-events/image82.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1163">**Icon** ![Timer change icon](./media/user-guide/tx-events/image82.png)</span></span>

<span data-ttu-id="d0679-1164">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1164">**Description**</span></span>

<span data-ttu-id="d0679-1165">Bu olay, tx_timer_change aracılığıyla belirtilen zamanlayıcının değiştirilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1165">This event represents changing the specified timer via tx_timer_change.</span></span>

<span data-ttu-id="d0679-1166">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1166">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1167">Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1167">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="d0679-1168">Bilgi alanı 2: Ilk süre sonu işaretleri.</span><span class="sxs-lookup"><span data-stu-id="d0679-1168">Info Field 2: Initial expiration ticks.</span></span>
- <span data-ttu-id="d0679-1169">Bilgi alanı 3: süre sonu işaretlerini yeniden zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="d0679-1169">Info Field 3: Reschedule expiration ticks.</span></span>
- <span data-ttu-id="d0679-1170">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1170">Info Field 4: Not used.</span></span>

### <a name="timer-create"></a><span data-ttu-id="d0679-1171">Süreölçer oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0679-1171">Timer Create</span></span> 

#### <a name="tx_timer_create"></a><span data-ttu-id="d0679-1172">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="d0679-1172">tx_timer_create</span></span>

<span data-ttu-id="d0679-1173">**Simge** ![ Süreölçer oluşturma simgesi](./media/user-guide/tx-events/image83.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1173">**Icon** ![Timer create icon](./media/user-guide/tx-events/image83.png)</span></span>

<span data-ttu-id="d0679-1174">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1174">**Description**</span></span>

<span data-ttu-id="d0679-1175">Bu olay tx_timer_create aracılığıyla bir Zamanlayıcı oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1175">This event represents creating a timer via tx_timer_create.</span></span>

<span data-ttu-id="d0679-1176">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1176">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1177">Bilgi alanı 1: Zamanlayıcı denetim bloğu Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1177">Info Field 1: Pointer to timer control block.</span></span>
- <span data-ttu-id="d0679-1178">Bilgi alanı 2: Ilk süre sonu işaretleri.</span><span class="sxs-lookup"><span data-stu-id="d0679-1178">Info Field 2: Initial expiration ticks.</span></span>
- <span data-ttu-id="d0679-1179">Bilgi alanı 3: süre sonu işaretlerini yeniden zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="d0679-1179">Info Field 3: Reschedule expiration ticks.</span></span>
- <span data-ttu-id="d0679-1180">Bilgi alanı 4: otomatik etkinleştir değeri — TX_AUTO_ACTIVATE (1) ya da TX_NO_ACTIVATE (0).</span><span class="sxs-lookup"><span data-stu-id="d0679-1180">Info Field 4: Automatic enable value—either TX_AUTO_ACTIVATE (1) or TX_NO_ACTIVATE (0).</span></span>

### <a name="timer-deactivate"></a><span data-ttu-id="d0679-1181">Zamanlayıcı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="d0679-1181">Timer Deactivate</span></span> 

#### <a name="tx_timer_deactivate"></a><span data-ttu-id="d0679-1182">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="d0679-1182">tx_timer_deactivate</span></span>

<span data-ttu-id="d0679-1183">**Simge** ![ Zamanlayıcı devre dışı bırakma simgesi](./media/user-guide/tx-events/image84.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1183">**Icon** ![Timer deactivate icon](./media/user-guide/tx-events/image84.png)</span></span>

<span data-ttu-id="d0679-1184">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1184">**Description**</span></span>

<span data-ttu-id="d0679-1185">Bu olay, tx_timer_deactivate aracılığıyla bir süreölçeri devre dışı bırakma temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1185">This event represents deactivating a timer via tx_timer_deactivate.</span></span>

<span data-ttu-id="d0679-1186">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1186">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1187">Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1187">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="d0679-1188">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1188">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1189">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1189">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1190">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1190">Info Field 4: Not used.</span></span>

### <a name="timer-delete"></a><span data-ttu-id="d0679-1191">Süreölçer silme</span><span class="sxs-lookup"><span data-stu-id="d0679-1191">Timer Delete</span></span> 

#### <a name="tx_timer_delete"></a><span data-ttu-id="d0679-1192">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="d0679-1192">tx_timer_delete</span></span>

<span data-ttu-id="d0679-1193">**Simge** ![ Süreölçer silme simgesi](./media/user-guide/tx-events/image85.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1193">**Icon** ![Timer delete icon](./media/user-guide/tx-events/image85.png)</span></span>

<span data-ttu-id="d0679-1194">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1194">**Description**</span></span>

<span data-ttu-id="d0679-1195">Bu olay, tx_timer_delete aracılığıyla bir süreölçeri silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1195">This event represents deleting a timer via tx_timer_delete.</span></span>

<span data-ttu-id="d0679-1196">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1196">**Information Fields**</span></span> 

- <span data-ttu-id="d0679-1197">Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1197">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="d0679-1198">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1198">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-1199">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1199">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1200">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1200">Info Field 4: Not used.</span></span>

### <a name="timer-information-get"></a><span data-ttu-id="d0679-1201">Süreölçer bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="d0679-1201">Timer Information Get</span></span> 

#### <a name="tx_timer_info_get"></a><span data-ttu-id="d0679-1202">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-1202">tx_timer_info_get</span></span>

<span data-ttu-id="d0679-1203">**Simge** ![ Süreölçer bilgi al simgesi](./media/user-guide/tx-events/image86.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1203">**Icon** ![Timer get information icon](./media/user-guide/tx-events/image86.png)</span></span>

<span data-ttu-id="d0679-1204">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1204">**Description**</span></span>

<span data-ttu-id="d0679-1205">Bu olay tx_timer_info_get aracılığıyla süreölçer bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1205">This event represents getting timer information via tx_timer_info_get.</span></span>

<span data-ttu-id="d0679-1206">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1206">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1207">Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1207">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="d0679-1208">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1208">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-1209">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1209">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1210">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1210">Info Field 4: Not used.</span></span>

### <a name="timer-performance-information-get"></a><span data-ttu-id="d0679-1211">Süreölçer performans bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="d0679-1211">Timer Performance Information Get</span></span> 

#### <a name="tx_timer_performance_info_get"></a><span data-ttu-id="d0679-1212">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-1212">tx_timer_performance_info_get</span></span>

<span data-ttu-id="d0679-1213">**Simge** ![ Süreölçer performans bilgileri al simgesi](./media/user-guide/tx-events/image87.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1213">**Icon** ![Timer performance information get icon](./media/user-guide/tx-events/image87.png)</span></span>

<span data-ttu-id="d0679-1214">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1214">**Description**</span></span> 

<span data-ttu-id="d0679-1215">Bu olay, tx_timer_performance_info_get aracılığıyla Zamanlayıcı performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1215">This event represents getting timer performance information via tx_timer_performance_info_get.</span></span>

<span data-ttu-id="d0679-1216">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1216">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1217">Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1217">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="d0679-1218">Bilgi alanı 2: çağrı sırasında yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0679-1218">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="d0679-1219">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1219">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1220">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1220">Info Field 4: Not used.</span></span>

### <a name="timer-system-performance-info-get"></a><span data-ttu-id="d0679-1221">Zamanlayıcı sistem performansı bilgileri al</span><span class="sxs-lookup"><span data-stu-id="d0679-1221">Timer System Performance Info Get</span></span> 

#### <a name="tx_timer_performance_system_info_get"></a><span data-ttu-id="d0679-1222">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="d0679-1222">tx_timer_performance_system_info_get</span></span>

<span data-ttu-id="d0679-1223">**Simge** ![ Süreölçer sistem performansı bilgileri al simgesi](./media/user-guide/tx-events/image88.png)</span><span class="sxs-lookup"><span data-stu-id="d0679-1223">**Icon** ![Timer system performance info get icon](./media/user-guide/tx-events/image88.png)</span></span>


<span data-ttu-id="d0679-1224">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d0679-1224">**Description**</span></span> 

<span data-ttu-id="d0679-1225">Bu olay, tx_timer_performance_system_info_get aracılığıyla tüm süreölçer performans bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d0679-1225">This event represents getting all timer performance information via tx_timer_performance_system_info_get.</span></span>

<span data-ttu-id="d0679-1226">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="d0679-1226">**Information Fields**</span></span>

- <span data-ttu-id="d0679-1227">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1227">Info Field 1: Not used.</span></span>
- <span data-ttu-id="d0679-1228">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1228">Info Field 2: Not used.</span></span>
- <span data-ttu-id="d0679-1229">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1229">Info Field 3: Not used.</span></span>
- <span data-ttu-id="d0679-1230">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="d0679-1230">Info Field 4: Not used.</span></span>