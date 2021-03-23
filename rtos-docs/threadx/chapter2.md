---
title: Bölüm 2-Azure RTOS ThreadX yükleme ve kullanımı
description: Bu bölümde, yüksek performanslı Azure RTOS ThreadX çekirdeğinin yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e1bf85d363b07c81f226d494107eae9ba18114a7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825456"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-threadx"></a>Bölüm 2-Azure RTOS ThreadX yükleme ve kullanımı

Bu bölümde, yüksek performanslı Azure RTOS ThreadX çekirdeğinin yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="host-considerations"></a>Ana bilgisayar konuları

Katıştırılmış yazılım genellikle Windows veya Linux (UNIX) ana bilgisayar bilgisayarlarında geliştirilmiştir. Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.

Genellikle hedef indirme, geliştirme aracı hata ayıklayıcısı içinden yapılır. İndirme tamamlandıktan sonra, hata ayıklayıcı hedef yürütme denetimi (go, dur, kesme noktası, vb.) sağlamaktan ve bellek ve işlemci kayıtlarına erişime karşı sorumludur.

Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar. OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.

Konakta kullanılan kaynaklar için, ThreadX kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 1 MB alan gerektirir.

## <a name="target-considerations"></a>Hedef konuları

ThreadX, hedefte 2 Kbayt ile 20 Kbayt arasında salt okuma belleği (ROM) gerektirir. Ayrıca, ThreadX Sistem yığını ve diğer genel veri yapıları için hedefin rastgele erişim belleği (RAM) için bir 1 ile 2 kilobayt daha gerektirir.

Hizmet çağrısı zaman aşımları, zaman dilimme ve uygulama zamanlayıcıları gibi Zamanlayıcı ile ilgili işlevlerde, temeldeki hedef donanımın düzenli bir kesme kaynağı sağlaması gerekir. İşlemcinin bu özelliği varsa, ThreadX tarafından kullanılır. Aksi takdirde, hedef işlemcinin düzenli bir kesme üretme özelliği yoksa, kullanıcının donanımının bunu sağlaması gerekir. Süreölçer kesmesi kurulumu ve yapılandırması, genellikle ThreadX dağıtımındaki ***tx_initialize_low_level*** derleme dosyasında bulunur.

> [!NOTE]
> *Dönemsel süreölçer kesme kaynağı kullanılabilir olmasa bile ThreadX hala işlevsel olur. Ancak, zamanlayıcıyla ilgili hizmetlerden hiçbiri işlevsel değildir.*

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS ThreadX, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/threadx/> .

Aşağıda, depodaki birçok önemli dosyanın bir listesi verilmiştir.

| Kısaltın | Açıklama |
|------------------- | ----------- |
| **tx_api. h**                      | Tüm sistem eşlerini, veri yapılarını ve hizmet prototiplerini içeren C üstbilgi dosyası.                                                             |
| **tx_port. h**                     | Tüm geliştirme araçlarını ve targetspecific veri tanımlarını ve yapılarını içeren C üstbilgi dosyası.                                                 |
| **demo_threadx. c**                | Küçük bir demo uygulaması içeren C dosyası.                                                                                                       |
| **TX. a (veya TX. lib)**              | *Standart* paketiyle dağıtılan Threadx C kitaplığının ikili sürümü.                                                          |
|                                   |                                                                                                                                                   |

>[!NOTE]
>*Tüm dosya adları küçük bir durumdur. Bu adlandırma kuralı, komutların Linux (UNIX) geliştirme platformlarına dönüştürülmesini kolaylaştırır.*

## <a name="threadx-installation"></a>ThreadX yüklemesi

ThreadX, GitHub deposu yerel makinenize kopyalanarak yüklenir. Bilgisayarınızda ThreadX deposunun bir kopyasını oluşturmak için tipik sözdizimi aşağıda verilmiştir.

```c
    git clone https://github.com/azure-rtos/threadx
```

Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında ThreadX kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.

> [!NOTE]
> * Uygulama yazılımının ThreadX kitaplık dosyasına (genellikle **TX. a** veya **TX. lib**) ve C içerme dosyalarına **_tx_api. h_* _ ve _*_tx_port. h_*_ erişimi olması gerekir. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaların uygulama geliştirme area._ kopyalanarak gerçekleştirilir.

## <a name="using-threadx"></a>ThreadX kullanma

ThreadX kullanmak için, uygulama kodu derleme sırasında ***tx_api. h** _ Içermeli ve threadx çalışma zamanı kitaplığı _*_TX. a_*_ (veya _ *_TX. lib_* *) ile bağlantı içermelidir.

Bir ThreadX uygulaması derlemek için gereken dört adım vardır.

1. ***Tx_api. h*** dosyasını threadx Hizmetleri veya veri yapıları kullanan tüm uygulama dosyalarına ekleyin.

1. Standart C ***Main** _ işlevini oluşturun. Bu işlev, ThreadX 'i başlatmak için sonunda _ *_tx_kernel_enter_** çağırmalıdır. Çekirdek girilmeden önce, ThreadX içermeyen uygulamaya özgü başlatma eklenebilir.

      > [!IMPORTANT]
      > * ThreadX giriş işlevi ***tx_kernel_enter** _ döndürmüyor. Bu nedenle, it._ sonra herhangi bir işlem veya işlev çağrısı yerleştirmediğinden emin olun

1. ***Tx_application_define*** işlevini oluşturun. Bu, ilk sistem kaynaklarının oluşturulduğu yerdir. Sistem kaynaklarına örnek olarak iş parçacıkları, kuyruklar, bellek havuzları, olay bayrakları grupları, zaman uyumu sağlayıcılar ve semaforlar verilebilir.

1. Uygulama kaynağını derleyin ve ThreadX çalışma zamanı kitaplığı ***TX. lib*** ile bağlayın. Elde edilen görüntü hedefe indirilebilir ve yürütülür!

## <a name="small-example-system"></a>Küçük örnek sistem

Şekil 1 ' deki küçük örnek sistem, önceliği 3 olan tek bir iş parçacığının oluşturulmasını gösterir. İş parçacığı yürütülür, bir sayacı artırır, sonra bir saat çentik için uyku moduna geçer.
Bu işlem süresiz olarak devam eder.

```c
#include "tx_api.h"
unsigned long my_thread_counter = 0;
TX_THREAD my_thread;
main( )
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter( );
}
void tx_application_define(void *first_unused_memory)
{
    /* Create my_thread! */
    tx_thread_create(&my_thread, "My Thread",
    my_thread_entry, 0x1234, first_unused_memory, 1024,
    3, 3, TX_NO_TIME_SLICE, TX_AUTO_START);
}
void my_thread_entry(ULONG thread_input)
{
    /* Enter into a forever loop. */
    while(1)
    {
        /* Increment thread counter. */
        my_thread_counter++;
        /* Sleep for 1 tick. */
        tx_thread_sleep(1);
    }
}
```

**ŞEKIL 1. Uygulama geliştirme şablonu**

Bu basit bir örnek olsa da, gerçek uygulama geliştirmesi için iyi bir şablon sağlar.

## <a name="troubleshooting"></a>Sorun giderme

Her ThreadX bağlantı noktası, bir demo uygulaması ile birlikte dağıtılır. Her zaman, gerçek hedef donanım veya sanal ortam üzerinde tanıtım sisteminin çalışmasını sağlamak iyi bir fikirdir.

Tanıtım sistemi düzgün yürütülemez, bazı sorun giderme ipuçları aşağıda verilmiştir.

1. Tanıtım 'in ne kadarının çalıştığını belirleme.
1. Yığın boyutlarını artırın (gerçek uygulama kodunda tanıtım için olduğundan daha önemlidir).
1. ThreadX kitaplığını tanımlanan TX_ENABLE_STACK_CHECKING yeniden derleyin. Bu, yerleşik ThreadX yığın denetimini sunar.
1. Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın. Bu tür bilgiler mühendislerin desteklenmesi için yararlı olmalıdır.

Sorun giderme adımlarından toplanan bilgileri göndermek için "[Müşteri Destek Merkezi](about-this-guide.md#customer-support-center)" bölümünde özetlenen yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

Threadx kitaplığı ve uygulama için ThreadX kullanarak birkaç yapılandırma seçeneği vardır. Aşağıdaki seçenekler uygulama kaynağında, komut satırında veya ***tx_user. h*** içerme dosyası içinde tanımlanabilir.

> [!IMPORTANT]
> * ***Tx_user. h** _ ' de tanımlanan seçenekler, yalnızca uygulama ve threadx kitaplığı _ *TX_INCLUDE_USER_DEFINE_FILE** tanımlı ile derlenme uygulandığında uygulanır.*

### <a name="smallest-configuration"></a>En küçük yapılandırma

En küçük kod boyutu için, aşağıdaki ThreadX yapılandırma seçenekleri göz önünde bulundurulmalıdır (diğer tüm seçeneklerin yokluğu olarak).

```c
TX_DISABLE_ERROR_CHECKING
TX_DISABLE_PREEMPTION_THRESHOLD
TX_DISABLE_NOTIFY_CALLBACKS
TX_DISABLE_REDUNDANT_CLEARING
TX_DISABLE_STACK_FILLING
TX_NOT_INTERRUPTABLE
TX_TIMER_PROCESS_IN_ISR
```

### <a name="fastest-configuration"></a>En hızlı yapılandırma

En hızlı yürütme için, daha önce en küçük yapılandırma için kullanılan yapılandırma seçenekleri, ancak bu seçeneklerle aynı zamanda göz önünde bulundurululur.

```c
TX_REACTIVATE_INLINE
TX_INLINE_THREAD_RESUME_SUSPEND
```

[Ayrıntılı yapılandırma seçenekleri](#detailed-configuration-options) açıklanmaktadır.

### <a name="global-time-source"></a>Küresel saat kaynağı

Diğer Microsoft Azure RTOS ürünleri (FileX, NetX, GUıDX, USBX, vb.) için ThreadX, bir saniye temsil eden ThreadX Zamanlayıcı işareti sayısını tanımlar. Diğerleri zaman gereksinimlerini bu sabiti temel alarak türeteler. Varsayılan olarak, değer 100 ' dir ve bir 10 MS dönemsel kesmesi varsayılıyor. Kullanıcı, ***tx_port. h*** veya IDE veya komut satırı içindeki istenen değeri TX_TIMER_TICKS_PER_SECOND tanımlayarak bu değeri geçersiz kılabilir.

### <a name="detailed-configuration-options"></a>Ayrıntılı yapılandırma seçenekleri

**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**

Bu seçenek tanımlandığı zaman, bayt havuzlarındaki performans bilgilerinin toplanmasında izin vermez. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**

Bu seçenek tanımlandığı zaman, bayt havuzlarındaki performans bilgilerinin toplanmasında izin vermez. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_DISABLE_ERROR_CHECKING**

Temel hizmet çağrısı hata denetimini atlar. Uygulama kaynağında tanımlandığında, tüm temel parametre hata denetimi devre dışı bırakılır. Bu, performansı %30 ' a kadar iyileştirebilir ve resim boyutunu da azaltabilir.

> [!NOTE]
> *Yalnızca uygulamanın tüm giriş parametrelerini, dış girişten türetilmiş giriş parametreleri de dahil olmak üzere tüm koşullarda her zaman geçerli olacağını düşünüyorsanız, hata denetimini devre dışı bırakabilirsiniz. Hata denetimi devre dışı olduğunda API için geçersiz giriş sağlanırsa, ortaya çıkan davranış tanımsızdır ve bellek bozulması veya sistem kilitlenmesiyle sonuçlanabilir.*

> [!NOTE]
> *Bir hata denetimini devre dışı bırakarak etkilenmeyen ThreadX API dönüş değerleri, Bölüm 4 ' teki her API açıklamasının "dönüş değerleri" bölümünde kalın olarak listelenir. Hata denetimi TX_DISABLE_ERROR_CHECKING seçeneği kullanılarak devre dışı bırakılmışsa, kalın olmayan dönüş değerleri hükümsüz olur.*

**TX_DISABLE_NOTIFY_CALLBACKS**

Tanımlandığında, çeşitli ThreadX nesneleri için bildirim geri aramalarını devre dışı bırakır. Bu seçeneğin kullanılması, kod boyutunu biraz azaltır ve performansı geliştirir. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_DISABLE_PREEMPTION_THRESHOLD**

Tanımlandığında, önalım-Threshold özelliğini devre dışı bırakır ve kod boyutunu biraz azaltır ve performansı geliştirir. Kuşkusuz, önalım-Threshold özellikleri artık kullanılamaz. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_DISABLE_REDUNDANT_CLEARING**

Tanımlandığında, ThreadX Global C veri yapılarını sıfıra başlatma mantığını kaldırır. Bu, yalnızca derleyicinin başlatma kodu tüm başlatılmamış C genel verilerini sıfıra ayarlarsa kullanılmalıdır. Bu seçeneğin kullanılması, kod boyutunu biraz azaltır ve başlatma sırasında performansı geliştirir. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_DISABLE_STACK_FILLING**

Tanımlandığında, her iş parçacığının yığınının her baytında 0xEF değerini yerleştirmeyi devre dışı bırakır. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_ENABLE_EVENT_TRACE**

Tanımlandığında ThreadX, bir TraceX izleme arabelleği oluşturmak için olay toplama kodu sunar.

**TX_ENABLE_STACK_CHECKING**

Tanımlandığında,, yığın alanından önce ve sonra ne kadar yığın kullanıldığını ve bu veri deseninin "sınırlarını" incelemesini içeren ThreadX çalışma zamanı yığın denetimini mümkün olur. Yığın hatası algılanırsa, kayıtlı uygulama yığını hata işleyicisi çağırılır. Bu seçenek, biraz daha fazla ek yüke ve kod boyutuna neden olur. Daha fazla bilgi için ***tx_thread_stack_error_notify*** API işlevini gözden geçirin. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO**

Tanımlandığında, olay bayrakları gruplarında performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_INLINE_THREAD_RESUME_SUSPEND**

Tanımlandığında, ThreadX, satır içi kod aracılığıyla ***tx_thread_resume** _ ve _ *_tx_thread_suspend_** API çağrılarını geliştirir. Bu, kod boyutunu artırır ancak bu iki API çağrısının performansını geliştirir.

**TX_MAX_PRIORITIES**

ThreadX için öncelik düzeylerini tanımlar. Yasal değerler 32 ile 1024 (dahil) arasındadır ve 32 ile eşit olarak *bölünebilmelidir.* Desteklenen öncelik düzeyi sayısının artırılması, her 32 öncelikteki RAM kullanımını 128 bayt kadar artırır. Ancak, performans üzerinde yalnızca göz ardı edilebilir bir efekt vardır. Varsayılan olarak, bu değer 32 öncelik düzeylerine ayarlanır.

**TX_MINIMUM_STACK**

Minimum yığın boyutunu (bayt cinsinden) tanımlar. İş parçacıklarının oluşturulduğu zaman denetlenirken hata denetimi için kullanılır. Varsayılan değer, bağlantı noktasına özeldir ve ***tx_port. h*** içinde bulunur.

**TX_MISRA_ENABLE**

Tanımlandığında, ThreadX, MISRA C uyumlu kuralları kullanır. Ayrıntılar için  ***ThreadX_MISRA_Compliance.pdf*** bakın.

**TX_MUTEX_ENABLE_PERFORMANCE_INFO**

Tanımlandığında, zaman uyumu sağlayıcılar üzerinde performans bilgilerinin toplanması sağlanır. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_NO_TIMER**

Tanımlandığında, ThreadX Zamanlayıcı mantığı tamamen devre dışıdır. Bu, ThreadX Zamanlayıcı özelliklerinin (iş parçacığı Sleep, API zaman aşımları, zaman Dilimleme ve uygulama zamanlayıcıları) kullanıldığı durumlarda faydalıdır. **TX_NO_TIMER** belirtilirse, **TX_TIMER_PROCESS_IN_ISR** seçeneğinin de tanımlanması gerekir.

**TX_NOT_INTERRUPTABLE**

Tanımlandığında, ThreadX kesme kilitleme süresini en aza indirmeye çalışmaz. Bu, daha hızlı yürütmeye neden olur, ancak kesme kilitleme süresini biraz artırır.

**TX_QUEUE_ENABLE_PERFORMANCE_INFO**

Tanımlandığında, kuyruklarda performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_REACTIVATE_INLINE**

Tanımlandığında, bir işlev çağrısı kullanmak yerine ThreadX süreölçerinin satır içi yeniden etkinleştirmeyi gerçekleştirir. Bu, performansı artırır ancak kod boyutunu biraz artırır. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO**

Tanımlandığında, Semaforlarda performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_THREAD_ENABLE_PERFORMANCE_INFO**

Tanımlandığında, iş parçacıklarında performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_TIMER_ENABLE_PERFORMANCE_INFO**

Tanımlandığında, zamanlayıcılar üzerinde performans bilgilerini toplamaya izin vermez. Varsayılan olarak, bu seçenek tanımlı değildir.

**TX_TIMER_PROCESS_IN_ISR**

Tanımlandığında, ThreadX için iç sistem süreölçeri iş parçacığını ortadan kaldırır. Süreölçer yığınına ve denetim bloğuna artık gerek duyulmadığından, bu durum Zamanlayıcı olaylarına ve daha küçük RAM gereksinimlerine göre performansı artırmasına neden olur. Ancak, bu seçeneğin kullanılması, tüm Zamanlayıcı süre sonu işlemesini Zamanlayıcı ıSR düzeyine kaydırır. Varsayılan olarak, bu seçenek tanımlı değildir.

> [!NOTE]
> *Zamanlayıcılardan izin verilen hizmetlere ISRs 'den izin verilmeyebilir, bu nedenle bu seçenek kullanılırken izin verilmiyor olabilir.*

**TX_TIMER_THREAD_PRIORITY**

İç ThreadX sistem Zamanlayıcı iş parçacığının önceliğini tanımlar. Varsayılan değer öncelik 0 ' dır; ThreadX için en yüksek öncelik. Varsayılan değer ***tx_port. h*** içinde tanımlanır.

**TX_TIMER_THREAD_STACK_SIZE**

İç ThreadX sistem Zamanlayıcı iş parçacığının yığın boyutunu (bayt cinsinden) tanımlar. Bu iş parçacığı tüm iş parçacığı uyku isteklerinin yanı sıra tüm hizmet çağrı zaman aşımlarını işler. Ayrıca, tüm uygulama süreölçeri geri çağırma yordamları bu içerikten çağrılır. Varsayılan değer, bağlantı noktasına özeldir ve ***tx_port. h*** içinde bulunur.

## <a name="threadx-version-id"></a>ThreadX sürüm KIMLIĞI

Programcı, Işparçacığıx sürümünü, ***tx_port. h** _ dosyasının inceağından elde edebilir. Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir. Uygulama yazılımı,/_ * _tx_version_id * * genel dizesini inceleyerek ThreadX sürümünü alabilir.
