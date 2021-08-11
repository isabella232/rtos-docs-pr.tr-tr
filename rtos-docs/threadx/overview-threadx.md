---
title: Azure RTOS ThreadX 'i anlama
description: Özellikle derin eklenmiş uygulamalar için tasarlanan gelişmiş gerçek zamanlı bir işletim sistemi (RTOS) olan Azure ThreadX hakkında daha fazla bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 6/9/2021
ms.service: rtos
ms.topic: overview
ms.custom: contperf-fy21q4
ms.openlocfilehash: 300307a82cfde9c74ec0a2499528898b384076676f75bd592fa2840bc5ac53a8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796313"
---
# <a name="overview-of-azure-rtos-threadx"></a>Azure RTOS ThreadX 'e genel bakış

Azure RTOS ThreadX, Microsoft 'un gelişmiş endüstriyel sınıf Real-Time Işletim sistemidir (RTOS). Özellikle de gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanmıştır. Azure RTOS ThreadX, Gelişmiş zamanlama, iletişim, eşitleme, süreölçer, bellek yönetimi ve kesme yönetim olanakları sağlar. Ayrıca, Azure RTOS ThreadX 'in birçok gelişmiş özelliği vardır: picokernel™ mimarisi, önalım-Threshold™ zamanlama, olay zincirleme,™ yürütme profili oluşturma, performans ölçümleri ve sistem olay izleme. En üstün kullanım kolaylığıyla birlikte, Azure RTOS ThreadX, katıştırılmış uygulamaların en zorlu kullanımı için ideal seçenektir. Azure RTOS ThreadX, tüketici cihazları, tıbbi elektronik aygıtlar ve endüstriyel denetim donatımı dahil olmak üzere çok çeşitli ürünlerde milyarlarca dağıtım içerir.

## <a name="threadx-footprint"></a>ThreadX ayak izi

Azure RTOS ThreadX 'in bir remarkada küçük 2 KB yönerge alanı ve 1 KB 'lık RAM en az ayak izi vardır. Bu küçük boyut büyük ölçüde katmanlı olmayan picokernel mimarisi ve otomatik ölçeklendirmeyle kaynaklanmaktadır. Otomatik ölçeklendirme, uygulama tarafından kullanılan hizmetlerin (ve destekleyici altyapının) bağlantı zamanında son görüntüye dahil olduğu anlamına gelir.

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

## <a name="threadx-execution-speed"></a>ThreadX yürütme hızı

Azure RTOS ThreadX, en popüler işlemciler üzerinde bir alt mikro ikinci bağlam anahtarına erişir ve diğer ticari RTOSs 'den daha hızlıdır. Hızlı olmasının yanı sıra Azure RTOS ThreadX de oldukça belirleyici bir niteliğindedir. Yalnızca bir tane veya tek bir 200 iş parçacığı olup olmadığı için aynı hızlı performansa erişir.

Azure RTOS ThreadX 'in bazı tipik performans özellikleri aşağıda verilmiştir:

* Hızlı önyükleme: Azure RTOS ThreadX önyüklemesi 120 ' den az Döngülerde.
* Temel hata denetimi için isteğe bağlı kaldırma: temel Azure RTOS ThreadX hata denetimi derleme zamanında atlanabilir. Bu, uygulama kodu doğrulandığında ve her parametreye artık hata denetimi gerektirmeyen yararlı olabilir. Hata denetimi atlama, sistem genelinde değil, bir derleme biriminde yapılabilir.
* Picokernel tasarımı: hizmetler, gereksiz işlev çağrı yükünü ortadan kaldırarak birbirleriyle katmanlanmış değildir.
* İyileştirilmiş kesme işleme: önalım gerekmedikçe yalnızca karalama kayıtları ıSR girdisi/çıkış üzerine kaydedilir/geri yüklenir.
* İyileştirilmiş API işleme:

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

Azure RTOS ThreadX, önalım-Threshold zamanlaması için önemli bir tablodur. Bu özellik Azure RTOS ThreadX için benzersizdir ve kapsamlı akademik araştırma konusu. [Önalım eşiğine sahip Fixed-Priority görevlerden](https://ieeexplore.ieee.org/document/811269), urun Wang (Concorçya University) ve Manas Saksena (University of Estsburgh) Ile bilgi zamanlarından daha fazla bilgi edinebilirsiniz.

Azure RTOS ThreadX 'in temel özellikleri:

* Eksiksiz ve kapsamlı çoklu görev olanakları
  * İş parçacıkları, uygulama zamanlayıcılar, ileti kuyrukları, sayım semaforları, zaman uyumu sağlayıcılar, olay bayrakları, blok ve bayt bellek havuzları
* Priority-Based preemptive zamanlaması
* Öncelik esnekliği – 1024 öncelik düzeyine kadar
* Cooperative zamanlaması
* Preemption-Threshold – Azure RTOS ThreadX 'e özgü, bağlam anahtarlarının azaltılmasına yardımcı olur ve schedulability garanti sağlanmasına yardımcı olur (akademik araştırma başına)
* Azure RTOS ThreadX MODÜLLERI aracılığıyla bellek koruması
* Tam belirleyici
* Olay Izleme – son *n* sistem/uygulama olaylarını yakala
* Olay zincirleme – her bir Azure RTOS ThreadX iletişimi veya eşitleme nesnesi için uygulamaya özgü "bildirim" geri çağırma işlevini kaydetme
* Isteğe bağlı bellek koruması ile Azure RTOS ThreadX MODÜLLERI
* Run-Time performans ölçümleri
  * İş parçacığı bağlantının sürdürülmesi sayısı
  * İş parçacığı getirilmesi sayısı
  * İstek iş parçacığı ön onayları sayısı
  * Zaman uyumsuz iş parçacığı kesme ön onayları sayısı
  * İş parçacığı önceliği ınsürümlerin sayısı
  * İş parçacığı relinkler sayısı
* Yürütme profili seti (EPK)
* Kesme yığınını ayır
* Run-Time Stack Analizi
* İyileştirilmiş Zamanlayıcı kesme Işlemi

## <a name="multicore-support-amp--smp"></a>Birden çok Ore desteği (AMP & SMP)

Standart Azure RTOS ThreadX genellikle asimetrik çoklu Işlem (AMP) ile birlikte kullanılır; burada Azure RTOS ThreadX 'in ayrı bir kopyası ve uygulama (veya Linux) her çekirdek üzerinde yürütülür ve paylaşılan bellek aracılığıyla birbirleriyle iletişim kurar veya OpenAMP (Azure RTOS ThreadX, OpenAMP 'yı destekler).

Yükleme işlemcilerin yüksek dinamik olduğu ortamlarda, aşağıdaki işlemci aileleri için Azure RTOS ThreadX simetrik çoklu Işlem (SMP) kullanılabilir:

* ARM Cortex-Ax
* ARM Cortex-Rx
* ARM Cortex-A5x 64 bit
* MIPS 34 K, 1004 K ve ınteraptiv
* PowerPC
* Synopsys ARC HS
* x86

Azure RTOS ThreadX SMP, *n* işlemciler genelinde dinamik yük dengeleme gerçekleştirir. Tüm Azure RTOS ThreadX kaynaklarına (kuyruklar, Semaforlar, olay bayrakları, bellek havuzları vb.) herhangi bir çekirdek üzerinde herhangi bir iş parçacığı tarafından erişilebilmesini sağlar. Azure RTOS ThreadX SMP tüm çekirdekler için tam Azure RTOS ThreadX API 'sini sağlar ve SMP işlemi için geçerli olan aşağıdaki yeni API 'Leri tanıtır:

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a>Azure RTOS ThreadX modülleri aracılığıyla bellek koruması

Azure RTOS ThreadX modülleri adlı bir eklenti ürünü, bir veya daha fazla uygulama iş parçacığının, hedefte dinamik olarak yüklenebilen ve çalıştırılabilen (veya yerinde yürütülen) bir "Module" içine paketlenmiş olmasını sağlar.

Modüller, büyük uygulamaların yalnızca etkin iş parçacıkları tarafından gereken belleği kaplamasına izin vermek için alan yükseltmeyi, hata düzeltmeyi ve program bölümlemesini etkinleştirir.

Modüller Ayrıca Azure RTOS ThreadX öğesinden ayrı bir adres alanına sahiptir. Bu, Azure RTOS ThreadX 'in, modülün dışında yanlışlıkla erişiminin diğer yazılım bileşenlerini bozmayacak şekilde bellek korumasını (MPU veya MMU aracılığıyla) yerleştirmesini sağlar.

## <a name="misra-compliant"></a>Hatalı ra uyumlu

Azure RTOS ThreadX ve Azure RTOS ThreadX SMP kaynak kodu hatalı ra-C: 2004 ve MISRA C:2012 uyumludur. MISRA C, C programlama dilini kullanan kritik sistemler için bir programlama yönergeleri kümesidir. Özgün MISRA C yönergeleri öncelikli olarak, ilk olarak bir oto ve uygulamaları hedeflenmiştir; Ancak, MISRA C artık güvenlik açısından kritik uygulamalar için geçerli olduğu şekilde çok daha tanınır. Azure RTOS ThreadX, tüm gerekli ve zorunlu, MISRA-C: 2004 ve MISRA c:2012ile uyumludur.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Hatalı ra sertifikası":::

## <a name="supports-most-popular-tools"></a>Popüler araçların çoğunu destekler

Azure RTOS ThreadX, en kapsamlı Azure RTOS ThreadX çekirdek tanıma 'yı de içeren ıAR 'ın Embedded çalışma ekranı dahil olmak üzere en popüler Embedded geliştirme araçlarının çoğunu destekler. diğer araç tümleştirmesi, GNU (GCC), ARM DS-5/uvision®, yeşil tepls MULTI®, rüzgar river çalışma ekranı, hayal Codescape, Renesas e2studio, metaware seecode, nxp CodeWarrior, defterbach TRACE32®, tı Code-Composer Studio, çapraz puan ve tüm örneksel cihazları içerir.

## <a name="adaptation-layer-for-threadx"></a>ThreadX için uyarlama katmanı

Çeşitli eski RTOS API 'Leri (FreeRTOS, POSIX, OSEK vb.) için ThreadX [uyarlayan katmanlarını](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) kullanarak, uygulama geçişi sorunlarını Azure RTOS 'a kolayca izleyebilirsiniz.

> [!div class="nextstepaction"]
> [Azure RTOS ThreadX 'e giriş](chapter1.md)