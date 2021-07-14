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
# <a name="overview-of-azure-rtos-threadx"></a>Azure RTOS ThreadX 'e genel bakış

Azure RTOS ThreadX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft 'un gelişmiş endüstriyel sınıf Real-Time Işletim sistemidir (RTOS). Azure RTOS ThreadX, Gelişmiş zamanlama, iletişim, eşitleme, süreölçer, bellek yönetimi ve kesme yönetim olanakları sağlar. Ayrıca, Azure RTOS ThreadX 'in picokernel™ mimarisi, önalım-Threshold™ zamanlama, olay zincirleme,™ yürütme profili oluşturma, performans ölçümleri ve sistem olay izleme dahil birçok gelişmiş özelliği vardır. En üstün kullanım kolaylığıyla birlikte, Azure RTOS ThreadX, katıştırılmış uygulamaların en zorlu kullanımı için ideal seçenektir. 2017 itibariyle, Azure RTOS ThreadX, tüketici cihazları, tıbbi elektronik ve endüstriyel denetim ekipmanı dahil olmak üzere çok çeşitli ürünlerde 6.200.000.000 ' den fazla dağıtıma sahiptir.

## <a name="api-protocols"></a>API protokolleri

### <a name="azure-rtos-threadx-services"></a>Azure RTOS ThreadX Hizmetleri

* Dinamik iş parçacığı oluşturma
* İş parçacığı sayısında sınırsız
* Ana iş parçacığı API 'Leri şunları içerir:
  * tx_thread_create
  * tx_thread_delete
  * tx_thread_preemption_change
  * tx_thread_priority_change
  * tx_thread_relinquish
  * tx_thread_reset
  * tx_thread_resume
  * tx_thread_sleep
  * tx_thread_suspend
  * tx_thread_terminate
  * tx_thread_wait_abort
* Ek bilgi ve performans API 'Leri

### <a name="message-queues"></a>İleti kuyrukları

* Dinamik sıra oluşturma
* Sıra sayısında sınırlama yoktur
* Değer (veya işaretçi aracılığıyla başvuruya göre) tarafından kopyalanmış iletiler
* 1 ile 16 32 bitlik sözcüklerden oluşan ileti boyutları
* Empty ve Full üzerinde isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Ana ileti kuyruğu API 'Leri şunları içerir:
  * tx_queue_create
  * tx_queue_delete
  * tx_queue_flush
  * tx_queue_front_send
  * tx_queue_receive
  * tx_queue_send_notify
* Ek bilgi ve performans API 'Leri

### <a name="counting-semaphores"></a>Semafor sayma

* Dinamik semafor oluşturma
* Semafor sayısında sınırsız
* 32-bit sayma semaforları (0-4.294.967.295)
* Tüketici-üretici veya kaynak korumasını destekler
* Semafor kullanılamadığında isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Ana semafor API 'Leri şunlardır:
  * tx_semaphore_create
  * tx_semaphore_delete
  * tx_semaphore_get
  * tx_semaphore_put
  * tx_semaphore_put_notify
* Ek bilgi ve performans API 'Leri

### <a name="mutexes"></a>Zaman Uyumu Sağlayıcılar

* Dinamik mutex oluşturma
* Birbirini kapsamayan sayısında sınırsız
* İç içe kaynak koruması destekleniyor
* İsteğe bağlı öncelikli devralma destekleniyor
* Mutex kullanılamadığında isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Ana mutex API 'Leri şunları içerir:
  * tx_mutex_create
  * tx_mutex_delete
  * tx_mutex_get
  * tx_mutex_put
* Ek bilgi ve performans API 'Leri

### <a name="event-flags"></a>Olay bayrakları

* Dinamik olay bayrağı Grup oluşturma
* Olay bayrak grupları sayısında sınırlama yok
* Bir iş parçacığının veya birden çok iş parçacığının eşitlenmesi
* Atomik get ve Clear destekleniyor
* İsteğe bağlı çoklu iş parçacığı açma ve/veya olay kümesi askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Ana olay bayrağı API 'Leri şunları içerir:
  * tx_event_flags_create
  * tx_event_flags_delete
  * tx_event_flags_get
  * tx_event_flags_set
  * tx_event_flags_set_notify
* Ek bilgi ve performans API 'Leri

### <a name="block-memory-pools"></a>Bellek havuzlarını engelle

* Dinamik blok havuzu oluşturma
* Blok havuzları sayısında sınırsız
* Sabit boyutlu blokların boyutu veya havuzun boyutu için sınır yok
* En hızlı olası bellek ayırma/anlaşma konumu
* Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Ana blok havuzu API 'Leri şunları içerir:
  * tx_block_pool_create
  * tx_block_pool_delete
  * tx_block_allocate
  * tx_block_release
* Ek bilgi ve performans API 'Leri

### <a name="byte-memory-pools"></a>Bayt bellek havuzları

* Dinamik bayt havuzu oluşturma
* Bayt havuzları sayısında sınır yoktur
* Bayt havuzunun boyutu için sınır yok
* En esnek değişken uzunluklu bellek ayırma/ayırmayı kaldırma
* Ayırma boyutu yerleşim destekleniyor
* Boş havuzda isteğe bağlı iş parçacığının askıya alınması
* Tüm askıya almada isteğe bağlı zaman aşımı
* Ana byte havuzu API'leri şunlardır:
  * tx_byte_pool_create
  * tx_byte_pool_delete
  * tx_byte_allocate
  * tx_byte_release
* Ek bilgiler ve performans API'leri

### <a name="application-timers"></a>Uygulama Süre süreleri

* Dinamik zamanlayıcı oluşturma
* Süre kaç kez süreyle ilgili sınır yoktur?
* Düzenli aralıklarla veya tek seferlik süreerler desteklensin
* Düzenli süre sonu değerleri farklı başlangıç süre sonu değerlerine sahip olabilir
* Zamanlayıcı etkinleştirme veya devre dışı bırakmada arama yok
* Bir donanım zamanlayıcı kesintisi ile yönlendiren tüm süreölçerler
* Ana zamanlayıcı API'leri şunlardır:
  * tx_timer_create
  * tx_timer_delete
  * tx_timer_activate
  * tx_timer_change
  * tx_timer_deactivate
* Ek bilgiler ve performans API'leri

### <a name="azure-rtos-threadx-core-scheduler"></a>Azure RTOS ThreadX Core Scheduler

* En az 2 KB FLASH,1 KB RAM ayak izi
* Hızlı, mikrosaniye altı bağlam anahtarı
* İş parçacığı sayısından bağımsız olarak tam olarak belirlenimci
* Öncelik tabanlı, tamamen ön hazırlıklı zamanlama
* İsteğe bağlı olarak 1024 düzeye kadar olan 32 varsayılan öncelik düzeyi
* Öncelik düzeyinde işbirliğine açık zamanlama (FIFO)
* Ön üretim eşiği teknolojisi
* İsteğe bağlı zamanlayıcı hizmetleri, şunları da içeren:
  * İş parçacığı başına isteğe bağlı zaman dilimi
  * Tüm engellemede isteğe bağlı zaman aşımı
  * API'ler donanım süreölçer kesintisi için gerektirir
* Yürütme profili oluşturma
* Sistem düzeyinde izleme
* Güvenlik birçok standart tarafından onaylandı

## <a name="threadx-footprint"></a>ThreadX ayak izi

Azure RTOS ThreadX için çok küçük bir 2 KB yönerge alanı ve en az ayak izi için 1 KB RAM gerekir. Bunun nedeni büyük ölçüde katmanlı olmayan picokernel mimarisi ™ otomatik ölçeklendirmedir. Otomatik ölçeklendirme, bağlantı zamanında son görüntüye yalnızca uygulama tarafından kullanılan hizmetlerin (ve destekleyen altyapının) dahil olduğu anlamına gelir.

Burada Bazı tipik Azure RTOS ThreadX boyutu özellikleri vetir.

|Azure RTOS ThreadX Hizmeti  |Bayt Cinsinden Tipik Boyut  |
|---------|---------|
|Temel Hizmetler (Gerekli) |2.000  |
|Kuyruk Hizmetleri  |900  |
|Olay Bayrağı Hizmetleri  |900  |
|Semaphore Hizmetleri  |450  |
|Mutex Services  |1.200  |
|Bellek Hizmetlerini Engelleme  |550  |
|Byte Memory Services  |900  |

## <a name="threadx-execution-speed"></a>ThreadX yürütme hızı

Azure RTOS ThreadX, en popüler işlemcilerde mikrosaniyenin altında bir bağlam anahtarına sahip olur ve genel olarak diğer ticari RTOS'lara göre önemli ölçüde daha hızlıdır. ThreadX, hızlı olmanın Azure RTOS yüksek oranda belirleyicidir. Hazır 200 iş parçacığı veya yalnızca bir tane olsa da aynı hızlı performansı elde ediyor.

Azure RTOS ThreadX'in tipik performans Azure RTOS vardır:

* Hızlı Önyükleme: Azure RTOS ThreadX'in önyüklemesi 120 döngüden kısadır.
* İsteğe bağlı Temel hata denetimi kaldırıldı: Temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir. Bu, uygulama kodu doğrulandığında ve artık her parametrede hata denetimi gerektirmeyecek şekilde yararlı olabilir. Bunun sistem genelinde değil bir derleme biriminde yapl olduğunu unutmayın.
* Picokernel™ Tasarım: Hizmetler birbirine katmanlanmaz, bu nedenle gereksiz işlev çağrısı ek yükünü ortadan kaldırmış olur.
* *İyileştirilmiş Kesme İşlemesi: Ön hazırlık gerekli olmadığı sürece ISR girdisi/çıkışında yalnızca karalama yazmacı kaydedilir/geri yüklenir.
* İyileştirilmiş API İşleme:

    |Azure RTOS ThreadX Hizmeti  |MikroSaniyelerde Hizmet Süresi*  |
    |---------|---------|
    |İş ParçacığıNı Askıya Alma  |0.6  |
    |İş Parçacığı Sürdürme  |0.6  |
    |Kuyruk Gönderme  |0.3  |
    |Kuyruk Alma  |0.3  |
    |Semaphore'ları al  |0,2  |
    |Semaphore koyma  |0,2  |
    |Bağlam Anahtarı  |0,4  |
    |Kesme Yanıtı  |0.0 – 0.6  |

    **200 MHz hızında çalışan tipik işlemciye göre performans rakamları.*

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS ThreadX, en önemli özelliği ön eşik zamanlaması olan gelişmiş bir teknolojidir. Bu özellik, ThreadX Azure RTOS benzersizdir ve kapsamlı akademik araştırmaların konusudur. Örneğin, Yun Wang, Wangia Üniversitesi ve Manas Saksena, University of Pittsburgh tarafından Fixed-Priority Tasks with [Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf)ile Scheduling Fixed-Priority( Zamanlama).

Azure RTOS ThreadX'in özelliklerini göz önünde bulundurabilirsiniz.

* Eksiksiz ve Kapsamlı Çok Görevli Tesisler
  * İş parçacıkları, uygulama süreçleri, ileti kuyrukları, semaforları sayma, mutex'ler, olay bayrakları, blok ve byte bellek havuzları
* Priority-Based Ön Zamanlama
* Öncelik Esnekliği – En fazla 1024 Öncelik Düzeyi
* İşbirlikçi Zamanlama
* Preemption-Threshold™ – Azure RTOS ThreadX'e özeldir, bağlam geçişlerini azaltmaya ve zamanlanabilirliği garanti etmeye yardımcı olur (akademik araştırma başına)
* Azure RTOS ThreadX MODULES aracılığıyla Bellek Koruması
* Tam Belirleyici
* Olay İzleme – Son *n sistem/uygulama* olaylarını yakalama
* Olay Zincirleme™ – ThreadX iletişimini veya eşitleme nesnesini her bir uygulama için Azure RTOS "notify" geri çağırma işlevini kaydetme
* Azure RTOS İsteğe Bağlı Bellek Koruması ile ThreadX MODÜLLERI
* Run-Time Performans Ölçümleri
  * İş parçacığı yeniden dizilerinin sayısı
  * İş parçacığı askıya alma sayısı
  * İstenen iş parçacığı önempsi sayısı
  * Zaman uyumsuz iş parçacığı kesme önemptions sayısı
  * İş parçacığı öncelik ters çevirme sayısı
  * İş parçacığı ilinquishes sayısı
* Yürütme Profili Seti (EPK)
* Kesme Yığınını Ayırma
* Run-Time Yığını Analizi
* Zamanlayıcı Kesme İşleme İyileştirilmiş

## <a name="multicore-support-amp--smp"></a>Çok çekirdekli destek (AMP & SMP)

Standart Azure RTOS ThreadX genellikle ayrı bir Azure RTOS ThreadX kopyasının ve uygulamanın (veya Linux'un) her çekirdekte yürütülür ve paylaşılan bellek veya OpenAMP gibi bir işlemciler arası iletişim mekanizması aracılığıyla birbirleriyle iletişim kurarak OpenAMP (Azure RTOS ThreadX OpenAMP'ı destekler) asimetrik Çok İşlemcili (AMP) bir şekilde kullanılır. Bu, Azure RTOS ThreadX kullanan en tipik çok çekirdekli yapılandırmadır ve uygulama işlemcileri etkili bir şekilde yükleyene kadar en verimli yapılandırma olabilir.

İşlemcileri yüklemenin yüksek oranda dinamik olduğu ortamlar için Azure RTOS ThreadX Symetric Multiprocessing (SMP) aşağıdaki işlemci aileleri için kullanılabilir:

* ARM Cortex-Ax
* ARM Cortex-Rx
* ARM Cortex-A5x 64 bit
* MIPS 34K, 1004K ve interAptiv
* PowerPC
* Özet ARC HS
* x86

Azure RTOS ThreadX *SMP, n* işlemci arasında dinamik yük dengeleme gerçekleştirir ve tüm Azure RTOS ThreadX kaynaklarına (kuyruklar, semaforlar, olay bayrakları, bellek havuzları vb.) herhangi bir çekirdek üzerindeki herhangi bir iş parçacığı tarafından erişim sağlar. Azure RTOS ThreadX SMP, tüm çekirdeklerde Azure RTOS ThreadX API'sini tam olarak sağlar ve aşağıdaki yeni API'nin SMP işlemi için geçerli olduğunu gösterir:

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a>Azure RTOS ThreadX Modülleri aracılığıyla bellek koruması

Azure RTOS ThreadX MODULES adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının dinamik olarak hedefte dinamik olarak yüklenemiyor ve çalıştırılana (veya yerinde yürütülebilir) bir "Modül" içinde paketlenesine olanak sağlar.

Modüller, büyük uygulamaların yalnızca etkin iş parçacıklarının ihtiyaç sahip olduğu belleği kaplayacak şekilde alan yükseltme, hata düzeltme ve program bölümlelene olanak sağlar.

Ayrıca modüller, ThreadX'in kendi kendine Azure RTOS adres alanı içerir. Bu Azure RTOS ThreadX'in modüle bellek koruması (MPU veya MMU aracılığıyla) yer açmasını sağlar. Bu sayede modülün dışından yanlışlıkla erişilenler başka bir yazılım bileşenini bozmaz.

## <a name="misra-compliant"></a>MISRA uyumlu

Azure RTOS ThreadX ve Azure RTOS ThreadX SMP kaynak kodu MISRA-C:2004 ve MISRA C:2012 ile uyumludur. MISRA C, C programlama dilini kullanan kritik sistemler için bir dizi programlama kılavuzudur. Özgün MISRA C yönergeleri öncelikli olarak otomotiv uygulamalarına yönelikti; ancak, MISRA C artık güvenlik açısından kritik herhangi bir uygulama için geçerli olduğu geniş ölçüde kabul ediliyor. Azure RTOS ThreadX, MISRA-C:2004 ve MISRA C:2012'nin tüm gerekli ve zorunlu kurallarıyla uyumludur.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Misra sertifikası":::

## <a name="supports-most-popular-tools"></a>En popüler araçları destekler

Azure RTOS ThreadX, kullanılabilir en kapsamlı Azure RTOS ThreadX çekirdek farkındalığını da içeren IAR Embedded Workbench™ dahil olmak üzere en popüler tümleşik geliştirme araçlarını destekler. Ek araç tümleştirmesi gnu (GCC), ARM DS-5/uVision®, Green River MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauteruter trace32®, TI Code-Composer Studio, CrossCore ve tüm analog cihazları içerir.

## <a name="adaptation-layer-for-threadx"></a>ThreadX için uyarlama katmanı

Azure RTOS ThreadX, özellikle sağlam bir şekilde eklenmiş uygulamalar için tasarlanan gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS). ThreadX, Auzre RTOS'a uygulama [](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) geçişini kolaylaştırmanıza yardımcı olmak için çeşitli eski RTOS API'leri (FreeRTOS, POSIX, OSEK vb.) için uyarlama katmanları sağlar
