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
  * İş parçacıkları, uygulama zamanlayıcılar, ileti kuyrukları, sayma semaforları, zaman uyumu sağlayıcılar, olay bayrakları, blok ve bayt bellek havuzları
* Priority-Based preemptive zamanlaması
* Öncelik esnekliği – 1024 öncelik düzeyine kadar
* Cooperative zamanlaması
* Önalım-Threshold™ – Azure RTOS ThreadX için benzersizdir, bağlam anahtarlarının azaltılmasına yardımcı olur ve schedulability (akademik araştırma başına) garantisi sağlar
* Azure RTOS ThreadX MODÜLLERI aracılığıyla bellek koruması
* Tam belirleyici
* Olay Izleme – son *n* sistem/uygulama olaylarını yakala
* Olay zincirleme™ – her bir Azure RTOS ThreadX iletişimi veya eşitleme nesnesi için uygulamaya özgü "bildirim" geri çağırma işlevini kaydetme
* Isteğe bağlı bellek koruması ile Azure RTOS ThreadX MODÜLLERI
* Run-Time performans ölçümleri
  * İş parçacığı bağlantının sürdürülmesi sayısı
  * İş parçacığı getirilmesi sayısı
  * İstek iş parçacığı preemptions sayısı
  * Zaman uyumsuz iş parçacığı kesme preemptions sayısı
  * İş parçacığı önceliği ınsürümlerin sayısı
  * İş parçacığı relinkler sayısı
* Yürütme profili seti (EPK)
* Kesme yığınını ayır
* Run-Time Stack Analizi
* İyileştirilmiş Zamanlayıcı kesme Işlemi

## <a name="multicore-support-amp--smp"></a>Birden çok Ore desteği (AMP & SMP)

Standart Azure RTOS ThreadX genellikle asimetrik çoklu Işlem (AMP) ile birlikte kullanılır, burada Azure RTOS ThreadX ve uygulamanın (veya Linux) her çekirdek üzerinde yürütülür ve paylaşılan bellek aracılığıyla birbirleriyle iletişim kurar veya OpenAMP (Azure RTOS ThreadX, OpenAMP gibi işlemciler arası bir iletişim mekanizması) vardır. Bu, Azure RTOS ThreadX kullanan en yaygın çok sayıda yapılandırmadır ve uygulama, işlemcileri etkin bir şekilde yükleyebiliyor olması halinde en etkili olabilir.

İşlemcilerin yüklenmesi çok dinamik olduğundan, aşağıdaki işlemci aileleri için Azure RTOS ThreadX Symetric çok Işlem (SMP) kullanılabilir:

* ARM Cortex-Ax
* ARM Cortex-Rx
* ARM Cortex-A5x 64 bit
* MIPS 34K, 1004K ve ınteraptiv
* PowerPC
* Synopsys ARC HS
* x86

Azure RTOS ThreadX SMP, *n* işlemciler genelinde dinamik yük dengeleme gerçekleştirir ve tüm Azure RTOS threadx kaynaklarına (kuyruklar, Semaforlar, olay bayrakları, bellek havuzları vb.) tüm çekirdeklerde herhangi bir iş parçacığı tarafından erişilmesine izin verir. Azure RTOS ThreadX SMP tüm çekirdekler için tam Azure RTOS ThreadX API 'sini sağlar ve SMP işlemi için geçerli olan aşağıdaki yeni API 'yi tanıtır:

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a>Azure RTOS ThreadX modülleri aracılığıyla bellek koruması

Azure RTOS ThreadX MODÜLLERI adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının, hedefte dinamik olarak yüklenebilen ve çalıştırılabilen (veya yerinde yürütülen) bir "Module" içine paketlenmiş olmasını sağlar.

Modüller, büyük uygulamaların yalnızca etkin iş parçacıkları tarafından gereken belleği kaplamasına izin vermek için alan yükseltmeyi, hata düzeltmeyi ve program bölümlemesini etkinleştirir.

Modüller Ayrıca Azure RTOS ThreadX öğesinden tamamen ayrı bir adres alanına sahiptir. Bu, Azure RTOS ThreadX 'in, modülün dışında yanlışlıkla erişiminin diğer yazılım bileşenlerini bozmayacak şekilde bellek korumasını (MPU veya MMU aracılığıyla) yerleştirmesini sağlar.


## <a name="misra-compliant"></a>Hatalı ra uyumlu

Azure RTOS ThreadX ve Azure RTOS ThreadX SMP souce Code yanlış ra-C:2004 ve MISRA C:2012 uyumludur. MISRA C, C programlama dilini kullanan kritik sistemler için bir programlama yönergeleri kümesidir. Özgün MISRA C yönergeleri öncelikli olarak, ilk olarak bir oto ve uygulamaları hedeflenmiştir; Ancak, MISRA C artık güvenlik açısından kritik uygulamalar için geçerli olduğu şekilde çok daha tanınır. Azure RTOS ThreadX, tüm gerekli ve zorunlu, MISRA-C:2004 ve MISRA c:2012'nin tüm kuralları ile uyumludur.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Hatalı ra sertifikası":::

## <a name="supports-most-popular-architectures"></a>Popüler mimarilerin çoğunu destekler

Azure RTOS ThreadX, en popüler 32/64 bit mikro işlemciler üzerinde çalışır, kullanıma hazır, tamamen sınanmış ve aşağıdakiler dahil olmak üzere tam olarak desteklenmektedir:

* Analog cihazlar: parça, BlackICE, CM4xx
* Andes Core: RıSC-V
* Ambiqmicro: Apollo MCUs
* ARM: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı
* Temposunda: Xtensa, elmas
* CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WERWIFI
* Cypress: RıSC-V
* EnSilica: eSi-RıSC
* Infineon: XMC1000, XMC4000, Kanore
* Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, varış a 10
* Mikro yonga: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32
* Mikro yarı: RıSC-V
* NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4
* Renesas: SH, HS, v850, RX, RZ, Synergy
* Silicon Labs: EFM32
* Synopsys: ARC 600, 700, ARC EM, ARC HS
* ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7
* TL: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C
* Dalga Bilgi Işlem: MıPS32 4K, 24K, 34K, 1004K, ver 5K, mikro Aptiv, ınteraptiv, proAptiv, M sınıfı
* Xilinx: mikro Blaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE

## <a name="supports-most-popular-tools"></a>Popüler araçların çoğunu destekler

Azure RTOS ThreadX, en kapsamlı Azure RTOS ThreadX çekirdek tanıma 'yı de içeren ıAR 'ın Embedded çalışma ekranı™ dahil olmak üzere en popüler katıştırılmış geliştirme araçlarını destekler. Ek araç tümleştirmesi, GNU (GCC), ARM DS-5/uVision®, yeşil Tepls MULTI®, Rüzgar River çalışma ekranı™, hayal Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Defterbach TRACE32®, TI Code-Composer Studio, çapraz puan ve tüm örneksel cihazları içerir.
