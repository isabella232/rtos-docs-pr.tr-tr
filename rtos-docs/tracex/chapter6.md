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
# <a name="chapter-6---azure-rtos-threadx-trace-events"></a>Bölüm 6-Azure RTOS ThreadX izleme olayları

Bu bölümde, Azure RTOS ThreadX olayları açıklanmaktadır. 

## <a name="list-of-events-and-icons"></a>Olay ve simgelerin listesi

Aşağıda, TraceX tarafından görünen ThreadX olaylarının listesi verilmiştir:

| **Simge**                         | **Anlamı** |
| -------------------------------- | ------------------------------------- |
| ![İç iş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image1.png)    | İç iş parçacığı özgeçmişi  |
| ![İç iş parçacığı askıya alma simgesi](./media/user-guide/tx-events/image2.png)    | İç iş parçacığı askıya alma |
| ![Kesme hizmeti yordamı giriş simgesi](./media/user-guide/tx-events/image3.png)    | Kesme hizmeti yordamı (ıSR) ENTER |
| ![Kesme hizmeti yordamı çıkış simgesi](./media/user-guide/tx-events/image4.png)    | Kesme hizmeti yordamı (ıSR) çıkış  |
| ![İç zaman dilimi simgesi](./media/user-guide/tx-events/image5.png)    | İç zaman dilimi |
| ![Çalışma simgesi](./media/user-guide/tx-events/image6.png)    | Çalışma |
| ![Blok havuz ayırma simgesi](./media/user-guide/tx-events/image7.png)    | **Havuz ayırmayı engelle** (*tx_block_allocate*)  |
| ![Blok Havuzu Oluştur simgesi](./media/user-guide/tx-events/image8.png)    | **Havuz oluşturmayı engelle** (*tx_block_pool_create*) |
| ![Blok havuzunu silme simgesi](./media/user-guide/tx-events/image9.png)    | **Blok havuzunu silme** (*tx_block_pool_delete*) |
| ![Havuz bilgilerini engelle al simgesi](./media/user-guide/tx-events/image10.png)    | **Havuz bilgilerini engelle al** (*tx_block_pool_info_get*) |
| ![Blok havuzu performans bilgileri Get con](./media/user-guide/tx-events/image11.png)    | **Blok havuzu performans bilgileri Get** (*tx_block_pool_performance_info_get*) |
| ![Blok havuzu sistem performans bilgileri al simgesi](./media/user-guide/tx-events/image12.png)    | **Blok havuzu sistem performans bilgileri Get** (*tx_block_pool_performance_system_info_get*) |
| ![Blok havuzu öncelik simgeleri simgesi](./media/user-guide/tx-events/image13.png)    | **Blok havuzu önceliklerini belirleme** (*tx_block_pool_prioritize*) |
| ![Havuz simgesine yayını engelle](./media/user-guide/tx-events/image14.png)    | **Havuza yayını engelle** (*tx_block_release*) |
| ![Bayt havuzu bellek ayırma simgesi](./media/user-guide/tx-events/image15.png)    | **Bayt havuzu bellek ayırır** (*tx_byte_allocate*) |
| ![Bayt havuzu oluşturma simgesi](./media/user-guide/tx-events/image16.png)    | **Bayt havuzu oluşturma** (*tx_byte_pool_create*) |
| ![Bayt havuzu silme simgesi](./media/user-guide/tx-events/image17.png)    | **Bayt havuzu silme** (*tx_byte_pool_delete*) |
| ![Bayt havuzu bilgileri al simgesi](./media/user-guide/tx-events/image18.png)    | **Bayt havuzu bilgileri Get** (*tx_byte_pool_info_get*) |
| ![Bayt havuzu performans bilgileri al simgesi](./media/user-guide/tx-events/image19.png)    | **Bayt havuzu performans bilgilerine al** (*tx_byte_pool_performance_info_get*) |
| ![Bayt havuzu sistem performans bilgileri al simgesi](./media/user-guide/tx-events/image20.png)    | **Bayt havuzu sistem performansı bilgileri al** (*tx_byte_pool_performance_system_info_get*) |
| ![* Bayt havuzu öncelik simgeleri simgesi](./media/user-guide/tx-events/image21.png)    | **Bayt havuzu önceliklerini belirleme** (*tx_byte_pool_prioritize*) |
| ![Havuza bayt bellek yayını simgesi](./media/user-guide/tx-events/image22.png)    | **Havuza bayt bellek yayını** (*tx_byte_release*) |
| ![Olay bayrakları Oluştur simgesi](./media/user-guide/tx-events/image23.png)    | **Olay bayrakları oluştur** (*tx_event_flags_create*) |
| ![Olay bayrakları silme simgesi](./media/user-guide/tx-events/image24.png)    | **Olay bayrakları silme** (*tx_event_flags_delete*) |
| ![Olay bayrakları al simgesi](./media/user-guide/tx-events/image25.png)    | **Olay bayrakları al** (*tx_event_flags_get*) |
| ![Olay bayrakları bilgileri al simgesi](./media/user-guide/tx-events/image26.png)    | **Olay bayrakları bilgileri Get** (*tx_event_flags_info_get*) |
| ![Olay bayrakları performans bilgileri al simgesi](./media/user-guide/tx-events/image27.png)    | **Olay bayrakları performans bilgileri Get** (*tx_event_flags_performance_info_get*) |
| ![Olay bayrakları sistem performans bilgileri al simgesi](./media/user-guide/tx-events/image28.png)    | **Olay bayrakları sistem performans bilgileri al** (*tx_event_flags_performance_system_info_get*) |
| ![Olay bayrakları kümesi simgesi](./media/user-guide/tx-events/image29.png)    | **Olay bayrak kümesi** (*tx_event_flags_set*) |
| ![Olay bayrakları ayarlama bildirim simgesi](./media/user-guide/tx-events/image30.png)    | **Olay bayrak kümesi bildir** (*tx_event_flags_set_notify*) |
| ![Kesmeyi etkinleştir/devre dışı bırak simgesi](./media/user-guide/tx-events/image31.png)    | **Kesme etkinleştir/devre dışı bırak** (*tx_interrupt_control*) |
| ![Mutex Oluştur simgesi](./media/user-guide/tx-events/image32.png)    | **Mutex oluşturma** (*tx_mutex_create*) |
| ![Mutex silme simgesi](./media/user-guide/tx-events/image33.png)    | **Mutex silme** (*tx_mutex_delete*) |
| ![Mutex al simgesi](./media/user-guide/tx-events/image34.png)    | **Mutex Get** (*tx_mutex_get*) |
| ![Mutex bilgileri al simgesi](./media/user-guide/tx-events/image35.png)    | **Mutex bilgileri al** (*tx_mutex_info_get*) |
| ![Mutex performans bilgileri al simgesi](./media/user-guide/tx-events/image36.png)    | **Mutex performans bilgileri Get** (*tx_mutex_performance_info_get*) |
| ![Mutex sistem performansı bilgileri al simgesi](./media/user-guide/tx-events/image37.png)    | **Mutex sistem performansı bilgileri Get** (*tx_mutex_performance_system_info_get*) |
| ![Mutex öncelik simgesi](./media/user-guide/tx-events/image38.png)    | **Mutex önceliği** (*tx_mutex_prioritize*) |
| ![Mutex put simgesi](./media/user-guide/tx-events/image39.png)    | **Mutex put** (*tx_mutex_put*) |
| ![Kuyruk Oluştur simgesi](./media/user-guide/tx-events/image40.png)    | **Sıra oluşturma** (*tx_queue_create*) |
| ![Kuyruk silme simgesi](./media/user-guide/tx-events/image41.png)    | **Kuyruk silme** (*tx_queue_delete*) |
| ![Kuyruğu Temizleme simgesi](./media/user-guide/tx-events/image42.png)    | **Kuyruğu Temizleme** (*tx_queue_flush*) |
| ![Kuyruk ön Gönder simgesi](./media/user-guide/tx-events/image43.png)    | **Kuyruk ön gönderme** (*tx_queue_front_send*) |
| ![Kuyruk bilgileri alma simgesi](./media/user-guide/tx-events/image44.png)    | **Kuyruk bilgileri alma** (*tx_queue_info_get*) |
| ![Sıra performans bilgileri alma simgesi](./media/user-guide/tx-events/image45.png)    | **Performans bilgilerini sıraya al** (*tx_queue_performance_info_get*) |
| ![Sistem performans bilgilerini sıraya alma simgesi](./media/user-guide/tx-events/image46.png)    | **Sistem performans bilgilerini sıraya al** (*tx_queue_performance_system_info_get*) |
| ![Sıra önceliği belirleme simgesi](./media/user-guide/tx-events/image47.png)    | **Sıra önceliklerini belirleme** (*tx_queue_prioritize*) |
| ![Kuyruk alma iletisi simgesi](./media/user-guide/tx-events/image48.png)    | **Kuyruk alma iletisi** (*tx_queue_receive*) |
| ![Kuyruk iletisi gönder simgesi](./media/user-guide/tx-events/image49.png)    | **Kuyruk gönderme iletisi** (*tx_queue_send*) |
| ![Kuyruk gönder bildirim simgesi](./media/user-guide/tx-events/image50.png)    | **Kuyruk gönderme bildirimi** (*tx_queue_send_notify*) |
| ![Semafor tavan koyma simgesi](./media/user-guide/tx-events/image51.png)    | **Semafor tavan yerleştirme** (*tx_semaphore_ceiling_put*) |
| ![Semafor Oluştur simgesi](./media/user-guide/tx-events/image52.png)    | **Semafor oluşturma** (*tx_semaphore_create*) |
| ![Semafor silme simgesi](./media/user-guide/tx-events/image53.png)    | **Semafor silme** (*tx_semaphore_delete*) |
| ![Semafor al simgesi](./media/user-guide/tx-events/image54.png)    | **Semafor al** (*tx_semaphore_get*) |
| ![Semafor bilgileri al simgesi](./media/user-guide/tx-events/image55.png)    | **Semafor bilgileri al** (*tx_semaphore_info_get*) |
| ![Semafor performans bilgileri al simgesi](./media/user-guide/tx-events/image56.png)    | **Semafor performans bilgileri Get** (*tx_semaphroe_performance_info_get*) |
| ![Semafor sistem performansı bilgileri al simgesi](./media/user-guide/tx-events/image57.png)    | **Semafor sistem performansı bilgileri Get** (*tx_semaphore_performance_system_info_get*) |
| ![Semafor önceliği belirleme simgesi](./media/user-guide/tx-events/image58.png)    | **Semafor önceliklerini belirleme** (*tx_semaphore_prioritize*) |
| ![Semafor put simgesi](./media/user-guide/tx-events/image59.png)    | **Semafor put** (*tx_semaphore_put*) |
| ![Semafor put bildirim simgesi](./media/user-guide/tx-events/image60.png)    | **Semafor put bildirimi** (*tx_semaphore_put_notify*) |
| ![İş parçacığı Oluştur simgesi](./media/user-guide/tx-events/image61.png)    | **Iş parçacığı oluşturma** (*tx_thread_create*) |
| ![İş parçacığı silme simgesi](./media/user-guide/tx-events/image62.png)    | **Iş parçacığı silme** (*tx_thread_delete*) |
| ![İş parçacığı çıkış/giriş bildirim simgesi](./media/user-guide/tx-events/image63.png)    | **Iş parçacığı çıkış/giriş bildirimi** (*tx_thread_entry_exit_notify*) |
| ![İş parçacığı tanımla simgesi](./media/user-guide/tx-events/image64.png)    | **Iş parçacığı tanımla** (*tx_thread_identify*) |
| ![İş parçacığı bilgileri al simgesi](./media/user-guide/tx-events/image65.png)    | **Iş parçacığı bilgileri al** (*tx_thread_info_get*) |
| ![İş parçacığı performans bilgileri al simgesi](./media/user-guide/tx-events/image66.png)    | **Iş parçacığı performans bilgileri al** (*tx_thread_performance_info_get*) |
| ![İş parçacığı performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image67.png)    | **Iş parçacığı performansı sistem bilgileri al** (*tx_thread_performance_system_info_get*) |
| ![İş parçacığı önalım Değiştir simgesi](./media/user-guide/tx-events/image68.png)    | **Iş parçacığı önalım değişikliği** (*tx_thread_preemption_change*) |
| ![İş parçacığı önceliği değişikliği simgesi](./media/user-guide/tx-events/image69.png)    | **Iş parçacığı önceliği değişikliği** (*tx_thread_priority_change*) |
| ![İş parçacığı relinsi simgesi](./media/user-guide/tx-events/image70.png)    | **Iş parçacığı relinsi** (*tx_thread_relinquish*) |
| ![İş parçacığı sıfırlama simgesi](./media/user-guide/tx-events/image71.png)    | **Iş parçacığı sıfırlama** (*tx_thread_reset*) |
| ![* İş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image72.png)    | **Iş parçacığı özgeçmişi** (**tx_thread_resume*) |
| ![İş parçacığı uyku simgesi](./media/user-guide/tx-events/image73.png)    | **Iş parçacığı Sleep** (*tx_thread_sleep*) * |
| ![İş parçacığı yığını hata bildirme simgesi](./media/user-guide/tx-events/image74.png)    | **Iş parçacığı yığını hata bildirimi** (*tx_thread_stack_error_notify*) |
| ![İş parçacığı bekletme simgesi](./media/user-guide/tx-events/image75.png)    | **Iş parçacığı askıya alma** (*tx_thread_suspend*) |
| ![İş parçacığı Sonlandır simgesi](./media/user-guide/tx-events/image76.png)    | **Iş parçacığı Sonlandır** (*tx_thread_terminate*) |
| ![İş parçacığı zaman dilimi değişikliği simgesi](./media/user-guide/tx-events/image77.png)    | **Iş parçacığı zaman dilimi değişikliği** (*tx_thread_time_slice_change*) |
| ![İş parçacığı beklemeyi durdur simgesi](./media/user-guide/tx-events/image78.png)    | **Iş parçacığı beklemeyi durdur** (*tx_thread_wait_abort*) |
| ![Zaman al simgesi](./media/user-guide/tx-events/image79.png)    | **Zaman al** (*tx_time_get*) |
| ![Zaman kümesi simgesi](./media/user-guide/tx-events/image80.png)    | **Zaman kümesi** (*tx_time_set*) |
| ![* Süreölçer etkinleştirme simgesi](./media/user-guide/tx-events/image81.png)    | **Süreölçer etkinleştirme** (*tx_timer_activate*) |
| ![Süreölçer değişikliği simgesi](./media/user-guide/tx-events/image82.png)    | **Süreölçer değişikliği** (*tx_timer_change*) |
| ![Süreölçer oluşturma simgesi](./media/user-guide/tx-events/image83.png)    | **Süreölçer oluşturma** (*tx_timer_create*) |
| ![Zamanlayıcı devre dışı bırakma simgesi](./media/user-guide/tx-events/image84.png)    | **Süreölçer devre dışı bırakma** (*tx_timer_deactivate*) |
| ![Süreölçer silme simgesi](./media/user-guide/tx-events/image85.png)    | **Süreölçer silme** (*tx_timer_delete*) |
| ![Süreölçer bilgileri al simgesi](./media/user-guide/tx-events/image86.png)    | **Süreölçer bilgileri Get** (*tx_timer_info_get*) |
| ![Süreölçer performans bilgileri al simgesi](./media/user-guide/tx-events/image87.png)    | **Süreölçer performans bilgileri Get** (*tx_timer_performance_info_get*) |
| ![* Süreölçer performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image88.png)    | **Zamanlayıcı performansı sistem bilgileri Get** (*tx_timer_performance_system_info_get*) |
| ![User-Defined Eventicon](./media/user-guide/tx-events/image0.png)    | **Kullanıcı tanımlı olay** (bkz. Bölüm 10)    |

## <a name="event-descriptions"></a>Olay Açıklamaları

### <a name="internal-thread-resume"></a>İç iş parçacığı özgeçmişi

#### <a name="internal-thread-resume"></a>İç iş parçacığı özgeçmişi

**Simge** ![ İç iş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image1.png)

**Açıklama**

Bu olay, bir iş parçacığını yürütmeye devam eden ThreadX içindeki iç işlemeyi temsil eder. Belirtilen iş parçacığı en yüksek önceliktir ve önalım-Threshold, yürütmeyi engellemez, sistem bu yeni Ready iş parçacığını yürütmeye başlayacaktır.

**Bilgi alanları**

- Bilgi alanı 1: devam eden iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: iş parçacığının devam eden önceki durumu aşağıdaki gibi:

  |  İş parçacığı durumu                     | Değer        |
  |---------------------------------- | --------|
  |  TX_READY                         | 0       |
  |  TX_COMPLETED                     | 1       |
  |  TX_TERMINATED                    | 2       |
  |  TX_SUSPENDED                     | 3       |
  |  TX_SLEEP                         | 4       |
  |  TX_QUEUE_SUSP                    | 5       |
  |  TX_SEMAPHORE_SUSP                | 6       |
  |  TX_EVENT_FLAG                    | 7       |
  |  TX_BLOCK_MEMORY                  | 8       |
  |  TX_BYTE_MEMORY                   | 9       |
  |  TX_TCP_IP                        | 12      |
  |  TX_MUTEX_SUSP                    | 13      |

- Bilgi alanı 3: çağrı sırasında yığın işaretçisi değeri. 
- Bilgi alanı 4: yürütülecek sonraki en yüksek öncelikli iş parçacığına yönelik Işaretçi.

### <a name="internal-thread-suspend"></a>İç iş parçacığı askıya alma

#### <a name="internal-thread-suspend"></a>İç iş parçacığı askıya alma

**Simge** ![ İç iş parçacığı askıya alma simgesi](./media/user-guide/tx-events/image2.png)

**Açıklama**

Bu olay, bir iş parçacığının yürütmesini askıya alan ThreadX içindeki iç işlemeyi temsil eder. Yürütmeye hazırlanma bir sonraki en yüksek öncelikli iş parçacığı dördüncü bilgi alanına yerleştirilir. Bu değer NULL ise, yürütme için hazırlanmaya yönelik başka bir iş parçacığı yoktur ve Sistem boşta kalır.

**Bilgi alanları**

- Bilgi alanı 1: askıya alınan iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: şu şekilde askıya alınan iş parçacığının yeni durumu:

  |  İş parçacığı durumu                     | Değer        |
  |---------------------------------- | --------|
  |  TX_COMPLETED                     | 1       |
  |  TX_TERMINATED                    | 2       |
  |  TX_SUSPENDED                     | 3       |
  |  TX_SLEEP                         | 4       |
  |  TX_QUEUE_SUSP                    | 5       |
  |  TX_SEMAPHORE_SUSP                | 6       |
  |  TX_EVENT_FLAG                    | 7       |
  |  TX_BLOCK_MEMORY                  | 8       |
  |  TX_BYTE_MEMORY                   | 9       |
  |  TX_TCP_IP                        | 12      |
  |  TX_MUTEX_SUSP                    | 13      |

- Bilgi alanı 3: çağrı sırasında yığın işaretçisi değeri. Bilgi alanı 4: yürütülecek sonraki en yüksek öncelikli iş parçacığına yönelik Işaretçi. NULL ise sistem boştadır.

### <a name="interrupt-service-routine-isr-enter"></a>Kesme hizmeti yordamı (ıSR) ENTER 

#### <a name="enter-isr"></a>ISR girin 

**Simge** ![ I S R simgesini girin](./media/user-guide/tx-events/image3.png)

**Açıklama**

Bu olay, uygulamaya bir kesme hizmeti yordamı (ıSR) girmeyi temsil eder. Kesme hizmeti rutin yürütmesi, ıSR çıkış olayı gerçekleşene kadar devam eder.

**Bilgi alanları**

- Bilgi alanı 1: çağrı sırasında yığın işaretçisi değeri.
- Bilgi alanı 2: uygulama tanımlı ıSR numarası (isteğe bağlı).
- Bilgi alanı 3: Iç Içe kesme sayısı.
- Bilgi alanı 4: Iç önalım devre dışı bayrağı.

### <a name="interrupt-service-routine-isr-exit"></a>Kesme hizmeti yordamı (ıSR) çıkış 

#### <a name="exit-isr"></a>Çıkış ıSR

**Simge** ![ Çıkış ı R m simgesi](./media/user-guide/tx-events/image4.png)

**Açıklama**

Bu olay, uygulamadaki bir kesme hizmeti yordamının (ıSR) çıkış işlemini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: çağrı sırasında yığın işaretçisi değeri.
- Bilgi alanı 2: uygulama tanımlı ıSR numarası (isteğe bağlı).
- Bilgi alanı 3: Iç Içe kesme sayısı.
- Bilgi alanı 4: Iç önalım devre dışı bayrağı.

### <a name="internal-time-slice"></a>İç zaman dilimi

#### <a name="internal-time-slice"></a>İç zaman dilimi

**Simge** ![ İç zaman dilimi simgesi](./media/user-guide/tx-events/image5.png)

**Açıklama**

Bu olay, Işparçacığıx ' te zaman dilimi işlemini gerçekleştiren iç işlemeyi temsil eder. Aynı önceliğe sahip bir sonraki iş parçacığı ilk bilgi alanına yerleştirilir. Bu değer, geçerli iş parçacığıyla aynı ise, hiçbir zaman dilimi gerçekleştirilmez.

- Bilgi alanı 1: yürütülecek sonraki iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: Iç Içe kesme sayısı.
- Bilgi alanı 3: Iç önalım devre dışı bayrağı.
- Bilgi alanı 4: çağrı sırasında yığın işaretçisi değeri.

### <a name="running"></a>Çalışma

#### <a name="running-in-context"></a>Bağlamda çalıştırma

**Simge** ![ Çalışma simgesi](./media/user-guide/tx-events/image6.png)

**Açıklama**

Bu olay bir iş parçacığı bağlamı veya boşta sistem içinde çalışmayı temsil eder. Bir kesmenin sonucu olarak bağlamdaki sonraki değişiklikleri göstermek için kullanılır.

**Bilgi alanları**
- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="block-allocate"></a>Blok ayır 

#### <a name="tx_block_allocate"></a>tx_block_allocate

**Simge** ![ Blok ayırma simgesi](./media/user-guide/tx-events/image7.png)

**Açıklama**

Bu olay tx_block_allocate aracılığıyla bir bellek bloğu ayırmayı temsil eder. Başarılı olursa, ayrılan bloğun adresi ikinci bilgi alanında döndürülür.

**Bilgi alanları**
- Bilgi alanı 1: karşılık gelen blok havuzuna yönelik Işaretçi.
- Bilgi alanı 2: döndürülen bellek bloğunun Işaretçisi (başarılıysa).
- Bilgi alanı 3: tx_block_allocate çağrısına sağlanan bekleme seçeneği.
- Bilgi alanı 4: Bu ayırdıktan sonra havuzda kalan kullanılabilir bloklar.

### <a name="block-pool-create"></a>Havuz oluşturmayı engelle

#### <a name="tx_block_pool_create"></a>tx_block_pool_create

**Simge** ![ Blok Havuzu Oluştur simgesi](./media/user-guide/tx-events/image8.png)

**Açıklama**

Bu olay, tx_block_pool_create aracılığıyla bir bellek blok havuzu oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen blok havuzu denetim bloğuna yönelik Işaretçi.
- Bilgi alanı 2: havuzun başlangıç belleği alanının Işaretçisi.
- Bilgi alanı 3: havuzdaki blokların sayısı. Bilgi alanı 4: havuzdaki her bloğun bayt cinsinden boyutu.

### <a name="block-pool-delete"></a>Blok havuzunu silme

#### <a name="tx_block_pool_delete"></a>tx_block_pool_delete

**Simge** ![ Blok havuzunu silme simgesi](./media/user-guide/tx-events/image9.png)

**Açıklama**

Bu olay, tx_block_pool_delete aracılığıyla bir bellek blok havuzunu silmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: blok havuzu denetim bloğuna yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi değeri.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="block-pool-information-get"></a>Havuz bilgilerini engelle al 

#### <a name="tx_block_pool_info_get"></a>tx_block_pool_info_get

**Simge** ![ Havuz bilgilerini engelle al simgesi](./media/user-guide/tx-events/image10.png)

**Açıklama**

Bu olay, tx_block_pool_info_get aracılığıyla bir bellek blok havuzu hakkında bilgi almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: blok havuzu denetim bloğuna yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi değeri.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="block-pool-performance-information-get"></a>Blok havuzu performans bilgileri Get

#### <a name="tx_block_pool_performance_info_get"></a>tx_block_pool_performance_info_get

**Simge** ![ Blok havuzu performans bilgileri al simgesi](./media/user-guide/tx-events/image11.png)

**Açıklama**

Bu olay, tx_block_pool_performance_info_get aracılığıyla bir bellek blok havuzu hakkında performans bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: blok havuzu denetim bloğuna yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="block-pool-performance-system-information-get"></a>Blok havuz performansı sistem bilgileri Get

#### <a name="tx_block_pool_performance_system_info_get"></a>tx_block_pool_performance_system_info_get

**Simge** ![ Blok havuz performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image12.png)

**Açıklama**

Bu olay, tüm bellek bloğu havuzları hakkında tx_block_pool_performance_system_info_get aracılığıyla performans bilgilerini almayı temsil eder.

**Bilgi alanları**
- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="block-pool-prioritize"></a>Blok havuzu önceliği belirleme

#### <a name="tx_block_pool_prioritize"></a>tx_block_pool_prioritize

**Simge** ![ Blok havuzu öncelik simgeleri simgesi](./media/user-guide/tx-events/image13.png)

**Açıklama**

Bu olay, HighestPriority askıya alınan iş parçacığını blok havuzunun askıya alma listesinin önüne yerleştirmeyi temsil eder. Tx_block_release çağrılmadan önce Bu yapıldığında, en yüksek önceliğe sahip iş parçacığı yayınlanan bloğu alır.

**Bilgi alanları**
- Bilgi alanı 1: bellek blok havuz işaretçisi.
- Bilgi alanı 2: Bu blok havuzunda askıya alınan iş parçacıklarının sayısı.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="block-release"></a>Yayını engelle 

#### <a name="tx_block_release"></a>tx_block_release

**Simge** ![ Blok yayını simgesi](./media/user-guide/tx-events/image14.png)

**Açıklama**

Bu olay, daha önce ayrılmış bir bloğu blok havuzuna geri bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: bellek blok havuz işaretçisi.
- Bilgi alanı 2: serbest bırakmak için blok Işaretçisi.
- Bilgi alanı 3: Bu blok havuzunda askıya alınan iş parçacığı sayısı.
- Bilgi alanı 4: çağrı sırasında yığın işaretçisi.

### <a name="byte-allocate"></a>Bayt ayırma 

#### <a name="tx_byte_allocate"></a>tx_byte_allocate

**Simge** ![ Bayt ayırma simgesi](./media/user-guide/tx-events/image15.png)

**Açıklama**

Bu olay tx_byte_allocate aracılığıyla bellek ayırmayı temsil eder. Başarılı olursa, ayrılan bellek adresi ikinci bilgi alanında döndürülür.

**Bilgi alanları**
- Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.
- Bilgi alanı 2: döndürülen bellek Işaretçisi (başarılıysa).
- Bilgi alanı 3: istenen bayt sayısı. Bilgi alanı 4: tx_byte_allocate çağrısına sağlanan bekleme seçeneği.

### <a name="byte-pool-create"></a>Bayt havuzu oluşturma

#### <a name="tx_byte_pool_create"></a>tx_byte_pool_create

**Simge** ![ Bayt havuzu oluşturma simgesi](./media/user-guide/tx-events/image16.png)

**Açıklama**

Bu olay tx_byte_pool_create aracılığıyla bir bayt havuzu oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.
- Bilgi alanı 2: bellek alanının başlangıcına yönelik Işaretçi. Bilgi alanı 3: bayt havuzundaki bayt sayısı.
- Bilgi alanı 4: çağrı sırasında yığın işaretçisi.

### <a name="byte-pool-delete"></a>Bayt havuzu silme 

#### <a name="tx_byte_pool_delete"></a>tx_byte_pool_delete

**Simge** ![ Bayt havuzu silme simgesi](./media/user-guide/tx-events/image17.png)

**Açıklama**

Bu olay, tx_byte_pool_delete aracılığıyla bir bayt havuzunun silinmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="byte-pool-information-get"></a>Bayt havuzu bilgilerini al

#### <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

**Simge** ![ Bayt havuzu bilgileri al simgesi](./media/user-guide/tx-events/image18.png)

**Açıklama**

Bu olay, tx_byte_pool_info_get aracılığıyla bayt havuzu bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="byte-pool-performance-info-get"></a>Bayt havuzu performans bilgisi al 

#### <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

**Simge** ![ Bayt havuzu performans bilgisi al simgesi](./media/user-guide/tx-events/image19.png)

**Açıklama**

Bu olay, tx_byte_pool_performance_info_get aracılığıyla bayt havuzu performans bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="byte-pool-performance-system-info-get"></a>Bayt havuzu performans sistemi bilgilerini al 

#### <a name="tx_byte_pool_performance_system_info_get"></a>tx_byte_pool_performance_system_info_get

**Simge** ![ Bayt havuzu performans sistemi bilgileri al simgesi](./media/user-guide/tx-events/image20.png)

**Açıklama**

Bu olay, tx_byte_pool_performance_system_info_get aracılığıyla bayt havuzu performans sistemi bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="byte-pool-prioritize"></a>Bayt havuzu önceliği belirleme

#### <a name="tx_byte_pool_prioritize"></a>tx_byte_pool_prioritize

**Simge** ![ Bayt havuzu öncelik simgesi](./media/user-guide/tx-events/image21.png)

**Açıklama**

Bu olay, tx_byte_pool_prioritize aracılığıyla bayt havuzunun askıya alma listesinin önceliklerini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.
- Bilgi alanı 2: bayt havuzunda Şu anda askıya alınan iş parçacıklarının sayısı.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="byte-release"></a>Bayt yayını

#### <a name="tx_byte_release"></a>tx_byte_release

**Simge** ![ Bayt yayın simgesi](./media/user-guide/tx-events/image22.png)

**Açıklama**

Bu olay, bir bayt havuzundan ayrılan bellek bloğunu tx_byte_release aracılığıyla serbest bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen bayt havuzuna yönelik Işaretçi.
- Bilgi alanı 2: önceden ayrılmış bayt havuzu belleği Işaretçisi.
- Bilgi alanı 3: Bu bayt havuzunda askıya alınan iş parçacığı sayısı.
- Bilgi alanı 4: kullanılabilir bellek bayt sayısı.

### <a name="event-flags-create"></a>Olay bayrakları oluşturma 

#### <a name="tx_event_flags_create"></a>tx_event_flags_create

**Simge** ![ Olay bayrakları Oluştur simgesi](./media/user-guide/tx-events/image23.png)

**Açıklama**

Bu olay tx_event_flags_create aracılığıyla yeni bir olay bayrakları grubu oluşturmayı temsil eder.

**Bilgi alanları** 
- Bilgi alanı 1: olay bayrakları Grup denetim bloğuna yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="event-flags-delete"></a>Olay bayraklarını silme 

#### <a name="tx_event_flags_delete"></a>tx_event_flags_delete

**Simge** ![ Olay bayrakları silme simgesi](./media/user-guide/tx-events/image24.png)

**Açıklama**

Bu olay, tx_event_flags_delete aracılığıyla bir olay bayrakları grubunu silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="event-flags-get"></a>Olay bayrakları al 

#### <a name="tx_event_flags_get"></a>tx_event_flags_get

**Simge** ![ Olay bayrakları gt simgesi](./media/user-guide/tx-events/image25.png)

**Açıklama**

Bu olay, tx_event_flags_get aracılığıyla var olan bir olay bayrakları grubundan olay bayraklarını almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.
- Bilgi alanı 2: istenen olay bayrakları.
- Bilgi alanı 3: grupta ayarlanmış olan olay bayrakları.
- Bilgi alanı 4: Get olay bayraklarda istenen seçenek.

### <a name="event-flags-information-get"></a>Olay bayrakları bilgileri al

#### <a name="tx_event_flags_info_get"></a>tx_event_flags_info_get

**Simge** ![ Olay bayrakları bilgileri al simgesi](./media/user-guide/tx-events/image26.png)

**Açıklama**

Bu olay, tx_event_flags_info_get aracılığıyla mevcut bir olay bayrakları grubuyla ilgili bilgileri almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="event-flags-performance-information-get"></a>Olay bayrakları performans bilgileri al 

#### <a name="tx_event_flags_performance_info_get"></a>tx_event_flags_performance_info_get

**Simge** ![ Olay bayrakları performans bilgileri al simgesi](./media/user-guide/tx-events/image27.png)

**Açıklama**

Bu olay, tx_event_flags_performance_info_get aracılığıyla mevcut bir olay bayrakları grubuyla ilgili performans bilgilerini almayı temsil eder.

**Bilgi alanları** 
- Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="event-flags-performance-system-info-get"></a>Olay bayrakları performans sistem bilgileri Get

#### <a name="tx_event_flags_performance_system_info_get"></a>tx_event_flags_performance_system_info_get

**Simge** ![ Olay bayrakları performans sistem bilgileri al simgesi](./media/user-guide/tx-events/image28.png)

**Açıklama**

Bu olay, tx_event_flags_performance_system_info_get aracılığıyla mevcut bir olay bayrakları grubuyla ilgili performans bilgilerini almayı temsil eder.

**Bilgi alanları**
- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="event-flags-set"></a>Olay bayrak kümesi 

#### <a name="tx_event_flags_set"></a>tx_event_flags_set

**Simge** ![ Olay bayrakları kümesi simgesi](./media/user-guide/tx-events/image29.png)

**Açıklama**

Bu olay, tx_event_flags_set aracılığıyla var olan bir olay bayrakları grubundaki olay bayraklarını ayarlamayı (veya temizlemeyi) temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.
- Bilgi alanı 2: ayarlanacak (veya temizlenecek) olay bayrakları.
- Bilgi alanı 3: ve veya ya da olay bayrağı seçeneği.
- Bilgi alanı 4: olay bayrak grubunda askıya alınan iş parçacıklarının sayısı.

### <a name="event-flags-set-notify"></a>Olay bayrakları kümesi bildir

#### <a name="tx_event_flags_set_notify"></a>tx_event_flags_set_notify

**Simge** ![ Olay bayrakları ayarlama bildirim simgesi](./media/user-guide/tx-events/image30.png)

**Açıklama**

Bu olay, tx_event_flags_set_notify aracılığıyla var olan bir olay bayrakları grubundaki herhangi bir olay bayrağı ayarlama işlemi için bir bildirim geri çağrısının kaydedilmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: olay bayrakları grubuna yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="interrupt-control"></a>Kesme denetimi 

#### <a name="tx_interrupt_control"></a>tx_interrupt_control

**Simge** ![ Kesme denetimi simgesi](./media/user-guide/tx-events/image31.png)

**Açıklama**

Bu olay, tx_interrupt_control aracılığıyla işlemcinin kesme kilitleme duruşunu değiştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yeni kesme sonrası.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="mutex-create"></a>Mutex oluşturma 

#### <a name="tx_mutex_create"></a>tx_mutex_create

**Simge** ![ Mutex Oluştur simgesi](./media/user-guide/tx-events/image32.png)

**Açıklama**

Bu olay tx_mutex_create aracılığıyla bir mutex oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: Mutex denetim bloğu Işaretçisi.
- Bilgi alanı 2: öncelik devralma seçeneği
- (TX_INHERIT veya TX_NO_INHERIT).
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="mutex-delete"></a>Mutex silme 

#### <a name="tx_mutex_delete"></a>tx_mutex_delete

**Simge** ![ Mutex silme simgesi](./media/user-guide/tx-events/image33.png)

**Açıklama**

Bu olay bir mutex 'i tx_mutex_delete aracılığıyla silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: mutex Işaretçisi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="mutex-get"></a>Mutex al 

#### <a name="tx_mutex_get"></a>tx_mutex_get

**Simge** ![ Mutex al simgesi](./media/user-guide/tx-events/image34.png)

**Açıklama**

Bu olay tx_mutex_get aracılığıyla bir mutex elde etmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: mutex Işaretçisi.
- Bilgi alanı 2: tx_mutex_get çağrısına sağlanan bekleme seçeneği.
- Bilgi alanı 3: mutex 'e sahip iş parçacığına yönelik Işaretçi (NULL, mutex 'in sahip olmadığı anlamına gelir).
- Bilgi alanı 4: sahip olan iş parçacığının tx_mutex_get kaç kez çağırdığı.

### <a name="mutex-information-get"></a>Mutex bilgileri al

#### <a name="tx_mutex_info_get"></a>tx_mutex_info_get

**Simge** ![ Mutex bilgileri al simgesi](./media/user-guide/tx-events/image35.png)

**Açıklama**

Bu olay, tx_mutex_info_get aracılığıyla mutex bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: mutex Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="mutex-performance-information-get"></a>Mutex performans bilgileri Get 

#### <a name="tx_mutex_performance_info_get"></a>tx_mutex_performance_info_get

**Simge** ![ Mutex performans bilgileri al simgesi](./media/user-guide/tx-events/image36.png)

**Açıklama**

Bu olay, tx_mutex_performance_info_get aracılığıyla mutex performans bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: mutex Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="mutex-performance-system-info-get"></a>Mutex performans sistem bilgisi al

#### <a name="tx_mutex_performance_system_info_get"></a>tx_mutex_performance_system_info_get

**Simge** ![ Mutex performans sistem bilgileri al simgesi](./media/user-guide/tx-events/image37.png)

**Açıklama**

Bu olay, tx_mutex_performance_system_info_get aracılığıyla mutex sistem performansı bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="mutex-prioritize"></a>Mutex öncelik 

#### <a name="tx_mutex_prioritize"></a>tx_mutex_prioritize

**Simge** ![ Mutex öncelik simgesi](./media/user-guide/tx-events/image38.png)

**Açıklama**

Bu olay, mutex 'in askıya alma listesinin tx_mutex_prioritize aracılığıyla önceliklerini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen mutex Işaretçisi.
- Bilgi alanı 2: mutex üzerinde şu anda askıya alınan iş parçacıklarının sayısı.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="mutex-put"></a>Mutex put 

#### <a name="tx_mutex_put"></a>tx_mutex_put

**Simge** ![ Mutex put simgesi](./media/user-guide/tx-events/image39.png)

**Açıklama**

Bu olay, tx_mutex_put aracılığıyla daha önce sahip olunan bir mutex 'i kullanıma sunar.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen mutex Işaretçisi.
- Bilgi alanı 2: mutex 'e sahip iş parçacığı Işaretçisi.
- Bilgi alanı 3: bekleyen mutex GET isteklerinin sayısı.
- Bilgi alanı 4: çağrı sırasında yığın işaretçisi.

### <a name="queue-create"></a>Sıra oluşturma 

#### <a name="tx_queue_create"></a>tx_queue_create

**Simge** ![ Kuyruk Oluştur simgesi](./media/user-guide/tx-events/image40.png)

**Açıklama**

Bu olay tx_queue_create aracılığıyla bir ileti kuyruğu oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kuyruk denetim bloğu Işaretçisi.
- Bilgi alanı 2: ileti boyutu-32 bitlik kelimeler.
- Bilgi alanı 3: kuyruk belleği alanının başlangıcı Işaretçisi.
- Bilgi alanı 4: kuyruk belleği alanındaki bayt sayısı.

### <a name="queue-delete"></a>Kuyruğu silme 

#### <a name="tx_queue_delete"></a>tx_queue_delete

**Simge** ![ Kuyruk silme simgesi](./media/user-guide/tx-events/image41.png)

**Açıklama**

Bu olay tx_queue_delete aracılığıyla bir kuyruğu silmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="queue-flush"></a>Kuyruğu Temizleme 

#### <a name="tx_queue_flush"></a>tx_queue_flush

**Simge** ![ Kuyruğu Temizleme simgesi](./media/user-guide/tx-events/image42.png)

**Açıklama**

Bu olay, tx_queue_flush aracılığıyla bir kuyruğun Temizleme (tüm kuyruk içeriğini temizleme) işlemini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="queue-front-send"></a>Kuyruk ön gönderimi 

#### <a name="tx_queue_front_send"></a>tx_queue_front_send

**Simge** ![ Kuyruk ön Gönder simgesi](./media/user-guide/tx-events/image43.png)

**Açıklama**

Bu olay tx_queue_front_send aracılığıyla bir kuyruğun önüne ileti gönderilmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: ileti başlangıcı Işaretçisi.
- Bilgi alanı 3: bekleme seçeneği sağlandı
- tx_queue_front_send çağrısı.
- Bilgi alanı 4: zaten sıralanmış ileti sayısı.

### <a name="queue-information-get"></a>Kuyruk bilgileri alma 

#### <a name="tx_queue_info_get"></a>tx_queue_info_get

**Simge** ![ Kuyruk bilgileri alma simgesi](./media/user-guide/tx-events/image44.png)

**Açıklama**

Bu olay tx_queue_info_get aracılığıyla bir sıra hakkında bilgi almayı temsil eder.

**Bilgi alanları** 
- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="queue-performance-info-get"></a>Sıra performans bilgileri alma 

#### <a name="tx_queue_performance_info_get"></a>tx_queue_performance_info_get

**Simge** ![ Sıra performans bilgileri alma simgesi](./media/user-guide/tx-events/image45.png)

**Açıklama**

Bu olay tx_queue_performance_info_get aracılığıyla bir kuyrukla ilgili performans bilgilerini almayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="queue-performance-system-info-get"></a>Performans sistemi bilgilerini sıraya al 

#### <a name="tx_queue_performance_system_info_get"></a>tx_queue_performance_system_info_get

**Simge** ![ Sıra performansı sistem bilgileri alma simgesi](./media/user-guide/tx-events/image46.png)

**Açıklama**

Bu olay, sistemdeki tüm kuyrukların sistem performans bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="queue-prioritize"></a>Kuyruk önceliği belirleme 

#### <a name="tx_queue_prioritize"></a>tx_queue_prioritize

**Simge** ![ Sıra önceliği belirleme simgesi](./media/user-guide/tx-events/image47.png)

**Açıklama**

Bu olay, sıranın askıya alınma listesinin tx_queue_prioritize aracılığıyla önceliklerini temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: karşılık gelen sıraya yönelik Işaretçi.
- Bilgi alanı 2: sırada askıya alınmış olan iş parçacıklarının sayısı.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

#### <a name="queue-receive"></a>Kuyruk alma 

##### <a name="tx_queue_receive"></a>tx_queue_receive

**Simge** ![ Kuyruk alma simgesi](./media/user-guide/tx-events/image48.png)

**Açıklama**

Bu olay, tx_queue_receive aracılığıyla bir kuyruktan ileti almayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: ileti hedefi Işaretçisi. Bilgi alanı 3: çağrıya izin verilen bekleme seçeneği.
- Bilgi alanı 4: Şu anda sıradaki ileti sayısı.

### <a name="queue-send"></a>Kuyruğu gönder 

#### <a name="tx_queue_send"></a>tx_queue_send

**Simge** ![ Kuyruk Gönder simgesi](./media/user-guide/tx-events/image49.png)

**Açıklama**

Bu olay tx_queue_send aracılığıyla bir kuyruğa ileti göndermeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: ileti Işaretçisi.
- Bilgi alanı 3: çağrıya izin verilen bekleme seçeneği.
- Bilgi alanı 4: Şu anda sıradaki ileti sayısı.

### <a name="queue-send-notify"></a>Kuyruk gönderme bildirimi 

#### <a name="tx_queue_send_notify"></a>tx_queue_send_notify

**Simge** ![ Kuyruk gönder bildirim simgesi](./media/user-guide/tx-events/image50.png)

**Açıklama**

<p>Bu olay, bir sıraya her ileti gönderildiğinde çağrılan tx_queue_send_notify aracılığıyla geri çağırma kaydını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kuyruk Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="semaphore-ceiling-put"></a>Semafor tavan koyma 

#### <a name="tx_semaphore_ceiling_put"></a>tx_semaphore_ceiling_put

**Simge** ![ Semafor tavan koyma simgesi](./media/user-guide/tx-events/image51.png)

**Açıklama**

Bu olay tx_semaphore_ceiling_put aracılığıyla bir semafora yerleştirmeyi temsil eder. Bu, semaforun en büyük değerinin incelendiğinden ve put işleminin en büyük değer veya tavan boyutunu aşmasına izin verilmediğinden tx_semaphore_put farklıdır.

**Bilgi alanları**

- Bilgi alanı 1: semafor Işaretçisi.
- Bilgi alanı 2: geçerli semafor sayısı.
- Bilgi alanı 3: semaforda askıya alınan iş parçacığı sayısı.
- Bilgi alanı 4: çağrıya tavan sınırı sağlandı.

#### <a name="semaphore-create"></a>Semafor oluşturma 

##### <a name="tx_semaphore_create"></a>tx_semaphore_create

**Simge** ![ Semafor Oluştur simgesi](./media/user-guide/tx-events/image52.png)

**Açıklama**

Bu olay tx_semaphore_create aracılığıyla semafor oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: semafor denetim bloğu Işaretçisi.
- Bilgi alanı 2: Ilk semafor sayısı.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="semaphore-delete"></a>Semafor silme 

#### <a name="tx_semaphore_delete"></a>tx_semaphore_delete

**Simge** ![ Semafor silme simgesi](./media/user-guide/tx-events/image53.png)

**Açıklama**

Bu olay tx_semaphore_delete aracılığıyla bir semaforu silmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: semafor Işaretçisi.
- NFO alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="semaphore-get"></a>Semafor al 

#### <a name="tx_semaphore_get"></a>tx_semaphore_get

**Simge** ![ Semafor al simgesi](./media/user-guide/tx-events/image54.png)

**Açıklama**

Bu olay tx_semaphore_get aracılığıyla bir semafor edinmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: semafor Işaretçisi.
- Bilgi alanı 2: çağrıya izin verilen bekleme seçeneği.
- Bilgi alanı 3: geçerli semafor sayısı.
- Bilgi alanı 4: çağrı sırasında yığın işaretçisi.

### <a name="semaphore-information-get"></a>Semafor bilgilerini al 

#### <a name="tx_semaphore_info_get"></a>tx_semaphore_info_get

**Simge** ![ Semafor bilgileri al simgesi](./media/user-guide/tx-events/image55.png)

**Açıklama**

Bu olay, tx_semaphore_info_get aracılığıyla bir semafor hakkında bilgi edinmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: semafor Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="semaphore-performance-info-get"></a>Semafor performans bilgisi al 

#### <a name="tx_semaphore_performance_info_get"></a>tx_semaphore_performance_info_get

**Simge** ![ Semafor performans bilgisi al simgesi](./media/user-guide/tx-events/image56.png)

**Açıklama**

Bu olay, tx_semaphore_performance_info_get aracılığıyla bir semafor hakkındaki performans bilgilerini elde eder.

**Bilgi alanları**

- Bilgi alanı 1: semafor Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="semaphore-performance-system-info"></a>Semafor performansı sistem bilgileri 

#### <a name="tx_semaphore_performance_system_info_get"></a>tx_semaphore_performance_system_info_get

**Simge** ![ Semafor performansı sistem bilgisi simgesi](./media/user-guide/tx-events/image57.png)

**Açıklama**

Bu olay, tx_semaphore_performance_system_info_get aracılığıyla sistemdeki tüm Semaforlar hakkında performans bilgilerini elde eder.

**Bilgi alanları** 

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="semaphore-prioritize"></a>Semafor önceliği belirleme 

#### <a name="tx_semaphore_prioritize"></a>tx_semaphore_prioritize

**Simge** ![ Semafor önceliği belirleme simgesi](./media/user-guide/tx-events/image58.png)

**Açıklama**

Bu olay, tx_semaphore_prioritize aracılığıyla semafor askıya alma listesinin önceliklerini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: karşılık gelen semafor Işaretçisi.
- Bilgi alanı 2: semafor üzerinde şu anda askıya alınan iş parçacığı sayısı.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="semaphore-put"></a>Semafor put 

#### <a name="tx_semaphore_put"></a>tx_semaphore_put

**Simge** ![ Semafor put simgesi](./media/user-guide/tx-events/image59.png)

**Açıklama**

Bu olay tx_semaphore_put aracılığıyla bir semafor örneği serbest bırakmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: karşılık gelen semafor Işaretçisi. Bilgi alanı 2: geçerli semafor sayısı.
- Bilgi alanı 3: semaforda askıya alınan iş parçacığı sayısı.
- Bilgi alanı 4: çağrı sırasında yığın işaretçisi.

### <a name="semaphore-put-notify"></a>Semafor put bildirimi 

#### <a name="tx_semaphore_put_notify"></a>tx_semaphore_put_notify

**Simge** ![ Semafor put bildirim simgesi](./media/user-guide/tx-events/image60.png)

**Açıklama**

Bu olay, bir semafor örneği her gerçekleştiğinde çağrılan tx_semaphore_put_notify aracılığıyla geri çağırma kaydını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: semafor Işaretçisi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-create"></a>İş parçacığı oluşturma 

#### <a name="tx_thread_create"></a>tx_thread_create

**Simge** ![ İş parçacığı Oluştur simgesi](./media/user-guide/tx-events/image61.png)

**Açıklama**

Bu olay tx_thread_create aracılığıyla bir iş parçacığı oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: iş parçacığı denetim bloğu Işaretçisi.
- Bilgi alanı 2: iş parçacığının önceliği.
- Bilgi alanı 3: iş parçacığı için yığın işaretçisi.
- NFO alanı 4: yığın boyutu bayt cinsinden.

### <a name="thread-delete"></a>İş parçacığı silme 

#### <a name="tx_thread_delete"></a>tx_thread_delete

**Simge** ![ İş parçacığı silme simgesi](./media/user-guide/tx-events/image62.png)

**Açıklama**

Bu olay tx_thread_delete aracılığıyla bir iş parçacığını silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-entryexit-notify"></a>İş parçacığı giriş/çıkış bildirimi 

#### <a name="tx_thread_entry_exit_notify"></a>tx_thread_entry_exit_notify

**Simge** ![ İş parçacığı girişi/çıkış bildirimi simgesi](./media/user-guide/tx-events/image63.png)

**Açıklama**

Bu olay, bir iş parçacığı girildiğinde veya çıktığında çağrılan tx_thread_entry_exit_notify aracılığıyla geri çağırma kaydını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: kayıt sırasında Iş parçacığı durumu.
- Bilgi alanı 3: çağrı sırasında yığın Işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

#### <a name="thread-identify"></a>İş parçacığı tanımla 

##### <a name="tx_thread_identify"></a>tx_thread_identify

**Simge** ![ İş parçacığı tanımla simgesi](./media/user-guide/tx-events/image64.png)

**Açıklama**

Bu olay, geçerli iş parçacığı işaretçisinin tx_thread_identify aracılığıyla alınmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-information-get"></a>İş parçacığı bilgileri al 

#### <a name="tx_thread_info_get"></a>tx_thread_info_get

**Simge** ![ İş parçacığı bilgileri al simgesi](./media/user-guide/tx-events/image65.png)

**Açıklama**

Bu olay, tx_thread_info_get aracılığıyla belirtilen iş parçacığı hakkında bilgi almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında iş parçacığının durumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

#### <a name="thread-performance-information-get"></a>İş parçacığı performans bilgileri al 

##### <a name="tx_thread_performance_info_get"></a>tx_thread_performance_info_get

**Simge** ![ İş parçacığı performans bilgileri al simgesi](./media/user-guide/tx-events/image66.png)

**Açıklama**

Bu olay, tx_thread_performance_info_get aracılığıyla belirtilen iş parçacığıyla ilgili performans bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında iş parçacığının durumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-performance-system-info-get"></a>İş parçacığı performans sistem bilgileri al 

#### <a name="tx_thread_performance_system_info_get"></a>tx_thread_performance_system_info_get

**Simge** ![ İş parçacığı performansı sistem bilgileri al simgesi](./media/user-guide/tx-events/image67.png)

**Açıklama**

Bu olay, tüm iş parçacıkları hakkındaki tx_thread_performance_system_info_get aracılığıyla performans bilgilerini almayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-preemption-change"></a>İş parçacığı önalım değişikliği 

#### <a name="tx_thread_preemption_change"></a>tx_thread_preemption_change

**Simge** ![ İş parçacığı önalım Değiştir simgesi](./media/user-guide/tx-events/image68.png)

**Açıklama**

Bu olay, bir iş parçacığının önalım-Threshold tx_thread_preemption_change aracılığıyla değiştirilmesini temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: New önalım-Threshold.
- Bilgi alanı 3: önceki önalım-Threshold.
- Bilgi alanı 4: Iş parçacığının çağrı sırasında durumu.

### <a name="thread-priority-change"></a>İş parçacığı önceliği değişikliği 

#### <a name="tx_thread_priority_change"></a>tx_thread_priority_change

**Simge** ![ İş parçacığı önceliği değişikliği simgesi](./media/user-guide/tx-events/image69.png)

**Açıklama**

Bu olay bir iş parçacığının önceliğini tx_thread_priority_change aracılığıyla değiştirmeyi temsil eder.

- Bilgi alanları 
- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: yeni öncelik.
- Bilgi alanı 3: önceki öncelik.
- Bilgi alanı 4: Iş parçacığının çağrı sırasında durumu.

### <a name="thread-relinquish"></a>İş parçacığı Relinsi 

#### <a name="tx_thread_relinquish"></a>tx_thread_relinquish

**Simge** ![ İş parçacığı relinsi simgesi](./media/user-guide/tx-events/image70.png)

**Açıklama**

Bu olay, tx_thread_relinquish aracılığıyla bir iş parçacığından işlemciyi yeniden eğme eder.

**Bilgi alanları**

- Bilgi alanı 1: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 2: yürütülecek sonraki iş parçacığına yönelik Işaretçi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-reset"></a>İş parçacığı sıfırlama 

#### <a name="tx_thread_reset"></a>tx_thread_reset

**Simge** ![ İş parçacığı sıfırlama simgesi](./media/user-guide/tx-events/image71.png)

**Açıklama**

Bu olay, tamamlanmış veya sonlandırılmış bir iş parçacığının tx_thread_reset aracılığıyla sıfırlanmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

#### <a name="thread-resume"></a>İş parçacığı özgeçmişi 

##### <a name="tx_thread_resume"></a>tx_thread_resume

**Simge** ![ İş parçacığı özgeçmişi simgesi](./media/user-guide/tx-events/image72.png)

**Açıklama**

Bu olay, askıya alınmış bir iş parçacığının tx_thread_resume aracılığıyla sürdürülmeyi gösterir.

**Bilgi alanları**

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-sleep"></a>İş parçacığı uyuması 

#### <a name="tx_thread_sleep"></a>tx_thread_sleep

**Simge** ![ İş parçacığı uyku simgesi](./media/user-guide/tx-events/image73.png)

**Açıklama**

Bu olay, tx_thread_sleep aracılığıyla belirtilen sayıda süreölçer işareti için geçerli iş parçacığını askıya alma temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: askıya alınacak onay işareti sayısı.
- Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-stack-error-notify"></a>İş parçacığı yığını hata bildirimi 

#### <a name="tx_thread_stack_error_notify_event"></a>tx_thread_stack_error_notify_event

**Simge** ![ İş parçacığı yığını hata bildirme simgesi](./media/user-guide/tx-events/image74.png)

**Açıklama**

Bu olay, tx_thread_stack_error_notify_event aracılığıyla bir iş parçacığı yığını hata bildirimi yordamının kaydedilmesini temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-suspend"></a>İş parçacığı askıya alma 

#### <a name="tx_thread_suspend"></a>tx_thread_suspend

**Simge** ![ İş parçacığı bekletme simgesi](./media/user-guide/tx-events/image75.png)

**Açıklama**

Bu olay tx_thread_suspend aracılığıyla bir iş parçacığını askıya alma temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: askıya alınacak iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-terminate"></a>İş parçacığı Sonlandır 

#### <a name="tx_thread_terminate"></a>tx_thread_terminate

**Simge** ![ İş parçacığı Sonlandır simgesi](./media/user-guide/tx-events/image76.png)

**Açıklama**

Bu olay bir iş parçacığının tx_thread_terminate aracılığıyla sonlandırılmasını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sonlandırılacak iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-time-slice-change"></a>İş parçacığı Time-Slice değişikliği 

#### <a name="tx_thread_time_slice_change"></a>tx_thread_time_slice_change

**Simge** ![ İş parçacığı zaman dilimi değişikliği simgesi](./media/user-guide/tx-events/image77.png)

**Açıklama**

Bu olay, bir iş parçacığının zaman dilimini tx_thread_time_slice_change aracılığıyla değiştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: yeni saat dilimi.
- Bilgi alanı 3: önceki zaman dilimi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="thread-wait-abort"></a>İş parçacığı beklemeyi durdur 

#### <a name="tx_thread_wait_abort"></a>tx_thread_wait_abort

**Simge** ![ İş parçacığı beklemeyi durdur simgesi](./media/user-guide/tx-events/image78.png)

**Açıklama**

Bu olay, bir iş parçacığının askıya alınma tx_thread_wait_abort aracılığıyla iptal eder.

**Bilgi alanları**

- Bilgi alanı 1: iş parçacığına yönelik Işaretçi.
- Bilgi alanı 2: Iş parçacığının çağrı sırasında durumu.
- Bilgi alanı 3: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="time-get"></a>Zaman al 

#### <a name="tx_time_get"></a>tx_time_get

**Simge** ![ Zaman al simgesi](./media/user-guide/tx-events/image79.png)

**Açıklama**

Bu olay, tx_time_get aracılığıyla geçerli süreölçer işaret sayısını almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: geçerli süreölçer onay işaretleri sayısı.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="time-set"></a>Zaman kümesi 

#### <a name="tx_time_set"></a>tx_time_set

**Simge** ![ Zaman kümesi simgesi](./media/user-guide/tx-events/image80.png)

**Açıklama**

Bu olay, tx_time_set aracılığıyla geçerli süreölçer işareti sayısını ayarlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yeni süreölçer onay işaretleri sayısı.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="timer-activate"></a>Süreölçer etkinleştirme 

#### <a name="tx_timer_activate"></a>tx_timer_activate

**Simge** ![ Süreölçer etkinleştirme simgesi](./media/user-guide/tx-events/image81.png)

**Açıklama**

Bu olay, tx_timer_activate aracılığıyla belirtilen süreölçeri etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="timer-change"></a>Süreölçer değişikliği 

#### <a name="tx_timer_change"></a>tx_timer_change

**Simge** ![ Süreölçer değişikliği simgesi](./media/user-guide/tx-events/image82.png)

**Açıklama**

Bu olay, tx_timer_change aracılığıyla belirtilen zamanlayıcının değiştirilmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.
- Bilgi alanı 2: Ilk süre sonu işaretleri.
- Bilgi alanı 3: süre sonu işaretlerini yeniden zamanlayın.
- Bilgi alanı 4: kullanılmıyor.

### <a name="timer-create"></a>Süreölçer oluşturma 

#### <a name="tx_timer_create"></a>tx_timer_create

**Simge** ![ Süreölçer oluşturma simgesi](./media/user-guide/tx-events/image83.png)

**Açıklama**

Bu olay tx_timer_create aracılığıyla bir Zamanlayıcı oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: Zamanlayıcı denetim bloğu Işaretçisi.
- Bilgi alanı 2: Ilk süre sonu işaretleri.
- Bilgi alanı 3: süre sonu işaretlerini yeniden zamanlayın.
- Bilgi alanı 4: otomatik etkinleştir değeri — TX_AUTO_ACTIVATE (1) ya da TX_NO_ACTIVATE (0).

### <a name="timer-deactivate"></a>Zamanlayıcı devre dışı bırakma 

#### <a name="tx_timer_deactivate"></a>tx_timer_deactivate

**Simge** ![ Zamanlayıcı devre dışı bırakma simgesi](./media/user-guide/tx-events/image84.png)

**Açıklama**

Bu olay, tx_timer_deactivate aracılığıyla bir süreölçeri devre dışı bırakma temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="timer-delete"></a>Süreölçer silme 

#### <a name="tx_timer_delete"></a>tx_timer_delete

**Simge** ![ Süreölçer silme simgesi](./media/user-guide/tx-events/image85.png)

**Açıklama**

Bu olay, tx_timer_delete aracılığıyla bir süreölçeri silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="timer-information-get"></a>Süreölçer bilgilerini al 

#### <a name="tx_timer_info_get"></a>tx_timer_info_get

**Simge** ![ Süreölçer bilgi al simgesi](./media/user-guide/tx-events/image86.png)

**Açıklama**

Bu olay tx_timer_info_get aracılığıyla süreölçer bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="timer-performance-information-get"></a>Süreölçer performans bilgileri Get 

#### <a name="tx_timer_performance_info_get"></a>tx_timer_performance_info_get

**Simge** ![ Süreölçer performans bilgileri al simgesi](./media/user-guide/tx-events/image87.png)

**Açıklama** 

Bu olay, tx_timer_performance_info_get aracılığıyla Zamanlayıcı performans bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: zamanlayıcıya yönelik Işaretçi.
- Bilgi alanı 2: çağrı sırasında yığın işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="timer-system-performance-info-get"></a>Zamanlayıcı sistem performansı bilgileri al 

#### <a name="tx_timer_performance_system_info_get"></a>tx_timer_performance_system_info_get

**Simge** ![ Süreölçer sistem performansı bilgileri al simgesi](./media/user-guide/tx-events/image88.png)


**Açıklama** 

Bu olay, tx_timer_performance_system_info_get aracılığıyla tüm süreölçer performans bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.