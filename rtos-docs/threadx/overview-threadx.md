---
title: ThreadX Azure RTOS anlama
description: Özellikle derin katıştırılmış uygulamalar için tasarlanmış gelişmiş bir gerçek zamanlı işletim sistemi (RTOS) olan Azure ThreadX hakkında daha fazla bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 6/9/2021
ms.service: rtos
ms.topic: overview
ms.custom: contperf-fy21q4
ms.openlocfilehash: 8c0bec2bb3b699b3a8d39d85eb322f3bbd95515a
ms.sourcegitcommit: 8b03df42920bdd544fb4195ab818043f6c71969e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/22/2021
ms.locfileid: "114436755"
---
# <a name="overview-of-azure-rtos-threadx"></a>Azure RTOS ThreadX'e genel bakış

Azure RTOS ThreadX, Microsoft'un gelişmiş endüstriyel sınıf Real-Time İşletim Sistemidir (RTOS). Özellikle derinden eklenmiş, gerçek zamanlı ve IoT uygulamaları için tasarlanmıştır. Azure RTOS ThreadX gelişmiş zamanlama, iletişim, eşitleme, zamanlayıcı, bellek yönetimi ve kesme yönetimi özellikleri sağlar. Ayrıca Azure RTOS ThreadX'in picokernel™ mimarisi™ preemption-threshold™ scheduling, event-chaining,™ yürütme profili oluşturma, performans ölçümleri ve sistem olay izleme gibi birçok gelişmiş özelliği vardır. Azure RTOS ThreadX, üstün kullanım kolaylığıyla birlikte en zorlu tümleşik uygulamalar için ideal seçimdir. Azure RTOS ThreadX'te tüketici cihazları, tıbbi elektronik cihazlar ve endüstriyel kontrol ekipmanları gibi çok çeşitli ürünlerde milyarlarca dağıtım vardır.

## <a name="threadx-footprint"></a>ThreadX ayak izi

Azure RTOS ThreadX'in oldukça küçük bir 2 KB yönerge alanı ve en az 1 KB RAM alanı vardır. Bu küçük boyutun nedeni büyük ölçüde katmanlı olmayan picokernel mimarisi ve otomatik ölçeklendirmedir. Otomatik ölçeklendirme, bağlantı zamanında son görüntüye yalnızca uygulama tarafından kullanılan hizmetlerin (ve destekleyen altyapının) dahil olduğu anlamına gelir.

Burada bazı tipik Azure RTOS ThreadX boyutu özellikleri vetir.

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

Azure RTOS ThreadX, en popüler işlemcilerde bir altmiksercond bağlam anahtarına ulaşıyor ve genel olarak diğer ticari RTOS'lara göre daha hızlıdır. ThreadX, hızlı olmanın Azure RTOS yüksek oranda belirleyicidir. Hazır 200 iş parçacığı veya yalnızca bir tane olsa da aynı hızlı performansı elde ediyor.

Azure RTOS ThreadX'in tipik performans Azure RTOS vardır:

* Hızlı önyükleme: Azure RTOS ThreadX'in önyüklemesi 120 döngüden kısadır.
* Temel hata denetimi isteğe bağlı olarak kaldırıldı: Temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir. Bu, uygulama kodu doğrulandığında ve artık her parametrede hata denetimi gerektirmeyecek şekilde yararlı olabilir. Hata denetimi atlama işlemi, sistem genelinde değil derleme biriminde yapılabilir.
* Picokernel tasarımı: Hizmetler birbirine katmanlanmaz ve gereksiz işlev çağrısı ek yükü ortadan kaldırılmış olur.
* en iyi duruma getirilmiş kesme işleme: Ön hazırlık gerekli olmadığı sürece, ISR girdisi/çıkışında yalnızca karalama yazmacı kaydedilir/geri yüklenir.
* İyileştirilmiş API işleme:

    |Azure RTOS ThreadX Hizmeti  |MikroSaniyelerde Hizmet Süresi*  |
    |---------|---------|
    |İş ParçacığıNı Askıya Alma  |0.6  |
    |İş Parçacığı Sürdürme  |0.6  |
    |Kuyruk Gönderme  |0.3  |
    |Kuyruk Alma  |0.3  |
    |Semaphore'ları al  |0,2  |
    |Semafor koy  |0,2  |
    |Bağlam Anahtarı  |0,4  |
    |Kesme Yanıtı  |0.0 – 0.6  |

    **200 MHz ile çalışan tipik işlemciye göre performans rakamları.*

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS ThreadX, ön eşik zamanlaması için önemli bir değerdir. Bu özellik, Azure RTOS ThreadX için benzersizdir ve kapsamlı akademik araştırmalara konudur. Yun Wang (Wangia Üniversitesi) ve Manas Saksena (University of Pittsburgh) tarafından kaleme alan [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf)(Zamanlama Görevleri) makalesinde daha fazla bilgi bulunabilir.

Azure RTOS ThreadX'in temel özellikleri:

* Eksiksiz ve Kapsamlı Çok Görevli Tesisler
  * İş parçacıkları, uygulama süreçleri, ileti kuyrukları, semaforları sayma, mutex'ler, olay bayrakları, blok ve byte bellek havuzları
* Priority-Based Ön Zamanlama
* Öncelik Esnekliği – En fazla 1024 Öncelik Düzeyi
* İşbirlikçi Zamanlama
* Preemption-Threshold: ThreadX'Azure RTOS benzersizdir, bağlam anahtarlarını azaltmaya ve zamanlanabilirliği garanti etmeye yardımcı olur (akademik araştırma başına)
* Azure RTOS ThreadX MODULES aracılığıyla Bellek Koruması
* Tam Belirleyici
* Olay İzleme – Son *n sistem/uygulama* olaylarını yakalama
* Olay Zinciri Oluşturma – ThreadX iletişimi veya eşitleme nesnesi için uygulamaya özgü "notify" Azure RTOS işlevini kaydetme
* Azure RTOS İsteğe Bağlı Bellek Koruması ile ThreadX MODÜLLERI
* Run-Time Performans Ölçümleri
  * İş parçacığı yeniden dizilerinin sayısı
  * İş parçacığı askıya alma sayısı
  * İstenen iş parçacığı ön emptions sayısı
  * Zaman uyumsuz iş parçacığı kesme ön emptions sayısı
  * İş parçacığı öncelik ters çevirme sayısı
  * İş parçacığı ilinquishes sayısı
* Yürütme Profili Seti (EPK)
* Kesme Yığınını Ayırma
* Run-Time Yığını Analizi
* Zamanlayıcı Kesme İşleme İyileştirilmiş

## <a name="multicore-support-amp--smp"></a>Çok çekirdekli destek (AMP & SMP)

Standart Azure RTOS ThreadX genellikle ayrı bir Azure RTOS ThreadX kopyasının ve uygulamanın (veya Linux'ın) her çekirdek üzerinde yürütülür ve paylaşılan bellek veya OpenAMP gibi bir işlemciler arası iletişim mekanizması aracılığıyla birbirleriyle iletişim kurarak OpenAMP (Azure RTOS ThreadX OpenAMP'ı destekler) asimetrik Çok İşlemcili (AMP) bir şekilde kullanılır.

İşlemcileri yüklemenin yüksek oranda dinamik olduğu ortamlarda Azure RTOS ThreadX Simetrik Çoklu İşlemci (SMP) aşağıdaki işlemci aileleri için kullanılabilir:

* ARM Cortex-Ax
* ARM Cortex-Rx
* ARM Cortex-A5x 64 bit
* MIPS 34 K, 1004 K ve interAptiv
* PowerPC
* Özet ARC HS
* x86

Azure RTOS ThreadX SMP, n işlemci arasında dinamik *yük dengeleme* gerçekleştirir. Tüm ThreadX Azure RTOS (kuyruklar, semaforlar, olay bayrakları, bellek havuzları vb.) herhangi bir çekirdek üzerinde herhangi bir iş parçacığı tarafından erişilsin. Azure RTOS ThreadX SMP, tüm çekirdeklerde Azure RTOS ThreadX API'sini tam olarak sağlar ve SMP işlemi için geçerli olan aşağıdaki yeni API'leri içerir:

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a>Azure RTOS ThreadX Modülleri aracılığıyla bellek koruması

Azure RTOS ThreadX Modülleri adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının dinamik olarak hedefte dinamik olarak yüklenemiyor ve çalıştırılana (veya yerinde yürütülebilir) bir "Modül" içinde paketlenesine olanak sağlar.

Modüller, büyük uygulamaların yalnızca etkin iş parçacıklarının ihtiyaç sahip olduğu belleği kaplayacak şekilde alan yükseltme, hata düzeltme ve program bölümlelene olanak sağlar.

Modüller ayrıca ThreadX'in kendisinde ayrı Azure RTOS alana sahiptir. Bu Azure RTOS ThreadX'in Modül'e bellek koruması (MPU veya MMU aracılığıyla) yüklemesini sağlar; böylece modülün dışından yanlışlıkla erişim başka bir yazılım bileşenini bozmaz.

## <a name="misra-compliant"></a>MISRA uyumlu

Azure RTOS ThreadX ve Azure RTOS ThreadX SMP kaynak kodu MISRA-C: 2004 ve MISRA C:2012 ile uyumludur. MISRA C, C programlama dilini kullanan kritik sistemler için bir dizi programlama kılavuzudur. Özgün MISRA C yönergeleri öncelikli olarak otomotiv uygulamalarına yönelikti; ancak, MISRA C artık güvenlik açısından kritik herhangi bir uygulama için geçerli olduğu geniş ölçüde kabul ediliyor. Azure RTOS ThreadX, MISRA-C: 2004 ve MISRA C:2012'nin tüm gerekli ve zorunlu kurallarıyla uyumludur.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Misra sertifikası":::

## <a name="supports-most-popular-tools"></a>En popüler araçları destekler

Azure RTOS ThreadX, kullanılabilir en kapsamlı iş parçacığı Azure RTOS sahip IAR Embedded Workbench dahil olmak üzere en popüler tümleşik geliştirme araçlarını destekler. Diğer araç tümleştirmesi GNU (GCC), ARM DS-5/uVision®, Green Multi®, Wind River Workbench, Imagination Codescape, Renesas e2studio, Metaware SeeCode, NXP CodeWarrior, Lauteruter TRACE32®, TI Code-Composer Studio, CrossCore ve tüm analog cihazları içerir.

## <a name="adaptation-layer-for-threadx"></a>ThreadX için uyarlama katmanı

Çeşitli eski RTOS API'leri (FreeRTOS, POSIX, OSEK vb.) için [ThreadX](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) uyarlama katmanlarını kullanarak uygulama geçiş sorunlarını daha kolay bir şekilde Azure RTOS'ye kolaylaştırabilirsiniz

> [!div class="nextstepaction"]
> [Azure RTOS ThreadX'e giriş](chapter1.md)