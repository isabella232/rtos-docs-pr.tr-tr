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
# <a name="overview-of-azure-rtos-threadx"></a>Azure RTOS ThreadX'e genel bakış

Azure RTOS ThreadX, Microsoft'un ayrıntılı, gerçek zamanlı Real-Time IoT uygulamaları için tasarlanmış gelişmiş endüstriyel sınıf işletim sistemidir (RTOS). Azure RTOS ThreadX gelişmiş zamanlama, iletişim, eşitleme, zamanlayıcı, bellek yönetimi ve kesme yönetimi özellikleri sağlar. Ayrıca Azure RTOS ThreadX'in picokernel™ mimarisi™ preemption-threshold™ scheduling, event-chaining, ™ execution profiling, performance metrics ve system event tracing gibi birçok gelişmiş özelliği vardır. Azure RTOS ThreadX, üstün kullanım kolaylığıyla birlikte en zorlu tümleşik uygulamalar için ideal seçimdir. Azure RTOS ThreadX, 2017 yılında tüketici cihazları, tıbbi elektronik cihazlar ve endüstriyel kontrol ekipmanları gibi çok çeşitli ürünlerde 6,2 milyardan fazla dağıtıma sahiptir.

## <a name="api-protocols"></a>API Protokolleri

### <a name="azure-rtos-threadx-services"></a>Azure RTOS ThreadX Services

* Dinamik iş parçacığı oluşturma
* İş parçacığı sayısıyla ilgili sınır yok
* Ana iş parçacığı API'leri şunlardır:
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
* Ek bilgiler ve performans API'leri

### <a name="message-queues"></a>İleti Kuyrukları

* Dinamik kuyruk oluşturma
* Kuyruk sayısıyla ilgili sınır yok
* Değere (veya işaretçi aracılığıyla başvuruya göre) kopyalanan iletiler
* 1 ile 16 32 bit sözcük arasında ileti boyutları
* Boş ve dolu isteğe bağlı iş parçacığı askıya alındı
* Tüm askıya almada isteğe bağlı zaman aşımı
* Ana ileti kuyruğu API'leri şunlardır:
  * tx_queue_create
  * tx_queue_delete
  * tx_queue_flush
  * tx_queue_front_send
  * tx_queue_receive
  * tx_queue_send_notify
* Ek bilgiler ve performans API'leri

### <a name="counting-semaphores"></a>Semaforları Sayma

* Dinamik semafor oluşturma
* Semafor sayısına sınırlama yoktur
* 32 bit sayma semaforları (0-4.294.967.295)
* Tüketici üreticisini veya kaynak korumasını destekler
* Semafor kullanılamıyorsa isteğe bağlı iş parçacığının askıya alınması
* Tüm askıya almada isteğe bağlı zaman aşımı
* Ana semafor API'leri şunlardır:
  * tx_semaphore_create
  * tx_semaphore_delete
  * tx_semaphore_get
  * tx_semaphore_put
  * tx_semaphore_put_notify
* Ek bilgiler ve performans API'leri

### <a name="mutexes"></a>Zaman Uyumu Sağlayıcılar

* Dinamik mutex oluşturma
* Mutex sayısı için sınır yok
* İç içe kaynak koruması desteği
* desteklenen isteğe bağlı öncelik devralma
* Mutex kullanılamıyorsa isteğe bağlı iş parçacığının askıya alınması
* Tüm askıya almada isteğe bağlı zaman aşımı
* Ana mutex API'leri şunlardır:
  * tx_mutex_create
  * tx_mutex_delete
  * tx_mutex_get
  * tx_mutex_put
* Ek bilgiler ve performans API'leri

### <a name="event-flags"></a>Olay Bayrakları

* Dinamik olay bayrağı grubu oluşturma
* Olay bayrağı gruplarının sayısıyla ilgili sınır yok
* Bir iş parçacığını veya birden çok iş parçacığını eşitleme
* Atomik get ve clear desteği
* AND/OR olay kümesi üzerinde isteğe bağlı çok iş parçacıklı askıya alma
* Tüm askıya almada isteğe bağlı zaman aşımı
* Ana olay bayrağı API'leri şunlardır:
  * tx_event_flags_create
  * tx_event_flags_delete
  * tx_event_flags_get
  * tx_event_flags_set
  * tx_event_flags_set_notify
* Ek bilgiler ve performans API'leri

### <a name="block-memory-pools"></a>Bellek Havuzlarını Engelleme

* Dinamik blok havuzu oluşturma
* Blok havuzu sayısıyla ilgili sınır yok
* Sabit boyutlu blokların veya havuzun boyutuyla ilgili sınır yok
* Mümkün olan en hızlı bellek ayırma/anlaşma konumu
* Boş havuzda isteğe bağlı iş parçacığının askıya alınması
* Tüm askıya almada isteğe bağlı zaman aşımı
* Ana blok havuzu API'leri şunlardır:
  * tx_block_pool_create
  * tx_block_pool_delete
  * tx_block_allocate
  * tx_block_release
* Ek bilgiler ve performans API'leri

### <a name="byte-memory-pools"></a>Byte Memory Pools

* Dinamik byte havuzu oluşturma
* Byte havuzlarının sayısına sınırlama yoktur
* Byte havuzunun boyutuyla ilgili sınır yok
* En esnek değişken uzunluklu bellek ayırma/ayırma
* Ayırma boyutu yerelliği destekle
* Boş havuz üzerinde isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Ana bayt havuzu API 'Leri şunları içerir:
  * tx_byte_pool_create
  * tx_byte_pool_delete
  * tx_byte_allocate
  * tx_byte_release
* Ek bilgi ve performans API 'Leri

### <a name="application-timers"></a>Uygulama zamanlayıcıları

* Dinamik süreölçer oluşturma
* Zamanlayıcılar sayısında sınırsız
* Düzenli veya tek atışı Zamanlayıcı destekleniyor
* Düzenli zamanlayıcılar farklı başlangıç son kullanma değerine sahip olabilir
* Süreölçer etkinleştirme veya devre dışı bırakma üzerinde arama yok
* Bir donanım Zamanlayıcı kesmesinin yönettiği tüm zamanlayıcılar
* Ana Zamanlayıcı API 'Leri şunları içerir:
  * tx_timer_create
  * tx_timer_delete
  * tx_timer_activate
  * tx_timer_change
  * tx_timer_deactivate
* Ek bilgi ve performans API 'Leri

### <a name="azure-rtos-threadx-core-scheduler"></a>Azure RTOS ThreadX çekirdek Zamanlayıcı

* Minimum 2 KB FLASH, 1KB RAM ayak izi
* Fast, Sub-mikro ikinci bağlam-anahtar
* İş parçacığı sayısından bağımsız olarak tam belirleyici
* Öncelik temelli, tam preemptive-zamanlama
* 32 varsayılan öncelik düzeyleri, isteğe bağlı olarak 1024 düzeye kadar
* Öncelik düzeyi (FıFO) içinde ortak zamanlama
* Önalım-Threshold teknolojisi
* Aşağıdakiler dahil isteğe bağlı Zamanlayıcı Hizmetleri:
  * İş parçacığı başına isteğe bağlı saat dilimi
  * Tüm engellemede isteğe bağlı zaman aşımı
  * API 'Ler donanım süreölçer kesmesi gerektirir
* Yürütme profili oluşturma
* Sistem düzeyinde Izleme
* Birçok standartlara yönelik güvenlik sertifikalı

## <a name="most-deployed-rtos"></a>En çok dağıtılan RTOS

Azure RTOS ThreadX, önde gelen 'U M2M Market Intelligence firması, VDC Research 'e göre dünya genelinde 6.200.000.000 dağıtımlara sahiptir. Azure RTOS ThreadX 'in popülerliği, güvenilirliği, kalitesi, boyutu, performansı, gelişmiş özellikler, kullanım kolaylığı ve genel kullanım süresi avantajına yönelik bir testdir.

> *"Şirketin temelleri ile bu yana kablosuz ve IoT pazarlarında THREADX 'in büyüme tratrumuzu izliyoruz ve THREADX 'in yaygın sektör benimsemesi tarafından giderek daha da artmaktadır."* – Chris Rommel, Executive Başkan Yardımcısı, VDC Research

## <a name="small-footprint"></a>Küçük ayak izi

Azure RTOS ThreadX, en az bir kaplama için remarkalı küçük 2KB yönerge alanı ve 1KB RAM gerektirir. Bu, büyük bir olasılıkla katmanlı olmayan picokernel™ mimarisi ve otomatik ölçeklendirmesinden kaynaklanır. Otomatik ölçeklendirme, uygulama tarafından kullanılan hizmetlerin (ve destekleyici altyapının) bağlantı zamanında son görüntüye dahil olduğu anlamına gelir.

Bazı tipik Azure RTOS ThreadX boyut özellikleri aşağıda verilmiştir.

|Azure RTOS ThreadX hizmeti  |Bayt cinsinden normal boyut  |
|---------|---------|
|Çekirdek hizmetler (gerekli) |2.000  |
|Kuyruk Hizmetleri  |900  |
|Olay bayrağı Hizmetleri  |900  |
|Semafor Hizmetleri  |450  |
|Mutex Hizmetleri  |1.200  |
|Bellek hizmetlerini engelle  |550  |
|Bayt bellek Hizmetleri  |900  |

## <a name="fast-execution"></a>Hızlı yürütme

Azure RTOS ThreadX, en popüler işlemciler üzerinde bir alt mikro ikinci bağlam anahtarına erişir ve diğer ticari ortamlarından çok daha hızlı bir şekilde genel olarak daha hızlıdır. Hızlı olmasının yanı sıra Azure RTOS ThreadX de oldukça belirleyici bir niteliğindedir. Yalnızca bir tane veya tek bir 200 iş parçacığı olup olmadığı için aynı hızlı performansa erişir.

Azure RTOS ThreadX 'in bazı tipik performans özellikleri aşağıda verilmiştir:

* Hızlı önyükleme: 120 ' den az Döngülerde Azure RTOS ThreadX önyüklemeleri.
* Temel hata denetimi için isteğe bağlı kaldırma: temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir. Bu, uygulama kodu doğrulandığında ve her parametreye artık hata denetimi gerektirmeyen yararlı olabilir. Bunun, sistem genelinde değil, bir derleme birimi üzerinde yapılabileceğini unutmayın.
* Picokernel™ tasarımı: hizmetler birbirlerine katmanlı değildir, bu nedenle gereksiz işlev çağrısı yükünü ortadan kaldırır.
* * İyileştirilmiş kesme Işleme: önalım gerekli değilse, yalnızca karalama kayıtları ıSR girdisi/çıkış üzerine kaydedilir/geri yüklenir.
* İyileştirilmiş API Işleme:

    |Azure RTOS ThreadX hizmeti  |Mikrosaniye cinsinden Hizmet Süresi *  |
    |---------|---------|
    |İş parçacığı askıya alma  |0.6  |
    |İş parçacığı özgeçmişi  |0.6  |
    |Kuyruğu gönder  |0.3  |
    |Kuyruk alma  |0.3  |
    |Semafor al  |0,2  |
    |Semaforu koy  |0,2  |
    |Bağlam anahtarı  |0,4  |
    |Kesme yanıtı  |0,0 – 0,6  |

    **200 MHz hızında çalışan normal işlemciyi temel alan performans rakamları*.

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS ThreadX, en önemli özelliği önalım-Threshold zamanlaması olan gelişmiş bir teknolojidir. Bu özellik Azure RTOS ThreadX için benzersizdir ve kapsamlı akademik araştırma konusu. Örneğin, bkz. [önalım Threshold ile Fixed-Priority görevleri zamanlama](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), Yıun Wang, Concorçya University ve Manas Saksena, tas haburi Üniversitesi.

Azure RTOS ThreadX 'in yeteneklerini göz önünde bulundurun.

* Eksiksiz ve kapsamlı çoklu görev olanakları
  * İş parçacıkları, uygulama süreçleri, ileti kuyrukları, semaforları sayma, mutex'ler, olay bayrakları, blok ve byte bellek havuzları
* Priority-Based Ön Zamanlama
* Öncelik Esnekliği – En fazla 1024 Öncelik Düzeyi
* İşbirlikçi Zamanlama
* Preemption-Threshold™ – Azure RTOS ThreadX'e özeldir, bağlam geçişlerini azaltmaya ve zamanlanabilirliği garanti etmeye yardımcı olur (akademik araştırma başına)
* Azure RTOS ThreadX MODULES aracılığıyla Bellek Koruması
* Tam Belirleyici
* Olay İzleme – Son *n sistem/uygulama* olaylarını yakalama
* Olay Zincirleme™ – ThreadX iletişimini veya eşitleme nesnesini her bir Azure RTOS uygulamaya özgü "notify" geri çağırma işlevini kaydetme
* Azure RTOS İsteğe Bağlı Bellek Koruması ile ThreadX MODÜLLERI
* Run-Time Performans Ölçümleri
  * İş parçacığı yeniden dizilerinin sayısı
  * İş parçacığı askıya alma sayısı
  * İstenen iş parçacığı önhizmelerinin sayısı
  * Zaman uyumsuz iş parçacığı kesme önemptions sayısı
  * İş parçacığı öncelik ters çevirme sayısı
  * İş parçacığı ilinquishes sayısı
* Yürütme Profili Seti (EPK)
* Kesme Yığınını Ayırma
* Run-Time Yığını Analizi
* Zamanlayıcı Kesme İşleme İyileştirilmiş

## <a name="multicore-support-amp--smp"></a>Çok çekirdekli destek (AMP & SMP)

Standart Azure RTOS ThreadX genellikle ayrı bir Azure RTOS ThreadX kopyasının ve uygulamanın (veya Linux'ın) her çekirdekte yürütülür ve paylaşılan bellek veya OpenAMP gibi bir işlemciler arası iletişim mekanizması aracılığıyla birbirleriyle iletişim kurarak OpenAMP (Azure RTOS ThreadX OpenAMP'ı destekler) asimetrik Çok İşlemcili (AMP) bir şekilde kullanılır. Bu, Azure RTOS ThreadX kullanan en tipik çok çekirdekli yapılandırmadır ve uygulama işlemcileri etkili bir şekilde yükleyene kadar en verimli yapılandırma olabilir.

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

Ayrıca modüller, ThreadX'in kendi kendine Azure RTOS adres alanı içerir. Bu Azure RTOS ThreadX'in Modül'e bellek koruması (MPU veya MMU aracılığıyla) yüklemesini sağlar; böylece modülün dışından yanlışlıkla erişim başka bir yazılım bileşenini bozmaz.

## <a name="misra-compliant"></a>MISRA uyumlu

Azure RTOS ThreadX ve Azure RTOS ThreadX SMP souce kodu MISRA-C:2004 ve MISRA C:2012 ile uyumludur. MISRA C, C programlama dilini kullanan kritik sistemler için bir dizi programlama kılavuzudur. Özgün MISRA C yönergeleri öncelikli olarak otomotiv uygulamalarına yönelikti; ancak, MISRA C artık güvenlik açısından kritik herhangi bir uygulama için geçerli olduğu geniş ölçüde kabul ediliyor. Azure RTOS ThreadX, MISRA-C:2004 ve MISRA C:2012'nin tüm gerekli ve zorunlu kurallarıyla uyumludur.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Misra sertifikası":::

## <a name="supports-most-popular-architectures"></a>En popüler mimarileri destekler

Azure RTOS ThreadX, en popüler 32/64 bit mikro işlemciler, hazır, tam olarak test edilmiş ve tam olarak desteklenen mikro işlemcilerde çalışır. Aşağıdakiler de dahil olmak üzere:

* Analog Cihazlar: SHARC, Blackfin, CM4xx
* Andes Core: RISC-V
* Ambiqmicro: Apollo MUS
* ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M
* Tempo: Xtensa, Diamond
* CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi
* Cypress: RISC-V
* EnSilica: eSi-RISC
* Infineon: XMC1000, XMC4000, TriCore
* Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10
* Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32
* Microsemi: RISC-V
* NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4
* Renesas: SH, HS, V850, RX, RZ, Synergy
* Silikon Laboratuvarları: EFM32
* Özetler: ARC 600, 700, ARC EM, ARC HS
* ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7
* Tl: C5xxx, C6xxx,Xxxris, Sitara, Tiva-C
* Dalga Bilişimi: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interApula, proAptiv, M Sınıfı
* Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE

## <a name="supports-most-popular-tools"></a>En popüler araçları destekler

Azure RTOS ThreadX, kullanılabilir en kapsamlı Azure RTOS ThreadX çekirdek farkındalığını da içeren IAR Embedded Workbench™ dahil olmak üzere en popüler tümleşik geliştirme araçlarını destekler. Ek araç tümleştirmesi GNU (GCC), ARM DS-5/uVision®, Green Multi®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauteruter TRACE32®, TI Code-Composer Studio, CrossCore ve tüm analog cihazları içerir.

## <a name="adaptation-layer-for-threadx"></a>ThreadX için uyarlama katmanı

Azure RTOS ThreadX, özellikle sağlam bir şekilde eklenmiş uygulamalar için tasarlanan gelişmiş bir gerçek zamanlı işletim sistemidir (RTOS). ThreadX, Auzre RTOS'a uygulama [](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) geçişini kolaylaştırmanıza yardımcı olmak için çeşitli eski RTOS API'leri (FreeRTOS, POSIX, OSEK vb.) için uyarlama katmanları sağlar
