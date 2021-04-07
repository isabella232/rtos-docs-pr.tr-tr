---
title: Bölüm 2-Azure RTOS ThreadX SMP 'in yükleme & kullanımı
description: Bu bölümde, HighPerformance Azure RTOS ThreadX SMP çekirdeğini yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cc352ebd7965c84c341d25dfa7bff2671dfb5e66
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550261"
---
# <a name="chapter-2---installation--use-of-azure-rtos-threadx-smp"></a>Bölüm 2-Azure RTOS ThreadX SMP 'in yükleme & kullanımı

Bu bölümde, HighPerformance Azure RTOS ThreadX SMP çekirdeğini yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="host-considerations"></a>Ana bilgisayar konuları

Katıştırılmış yazılım genellikle Windows veya Linux (UNIX) ana bilgisayar bilgisayarlarında geliştirilmiştir. Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.

Genellikle hedef indirme, geliştirme aracı hata ayıklayıcısı içinden yapılır. İndirmeden sonra, hata ayıklayıcı, hedef yürütme denetimi (go, dur, kesme noktası vb.) ve bellek ve işlemci kayıtlarına erişimi sağlamaktan sorumludur.

Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar. OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.

Konakta kullanılan kaynaklar için, ThreadX SMP kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 1 MB alan gerektirir.

> [!IMPORTANT]
> Ek konak sistem konuları ve seçenekleri için lütfen sağlanan **readme_threadx.txt** dosyasını gözden geçirin.

## <a name="target-considerations"></a>Hedef konuları

ThreadX SMP, hedefte 2 Kbayt ile 20 Kbayt arasında salt okuma belleği (ROM) gerektirir. ThreadX SMP Sistem yığını ve diğer genel veri yapıları için hedefin rastgele erişim belleği (RAM) için bir adet 1 ile 2 KB gerekir.

Hizmet çağrısı zaman aşımları, zaman dilimme ve uygulama zamanlayıcıları gibi Zamanlayıcı ile ilgili işlevlerde, temeldeki hedef donanımın düzenli bir kesme kaynağı sağlaması gerekir. İşlemcinin bu özelliği varsa, bu özellik ThreadX SMP tarafından kullanılır. Aksi takdirde, hedef işlemcinin düzenli bir kesme üretme özelliği yoksa, kullanıcının donanımının bunu sağlaması gerekir. Süreölçer kesmesi kurulumu ve yapılandırması, genellikle ThreadX SMP dağıtımındaki ***tx_initialize_low_level*** derleme dosyasında bulunur.

> [!IMPORTANT]
> Dönemsel süreölçer kesme kaynağı kullanılabilir olmasa bile ThreadX SMP hala işlevsel olur. Ancak, zamanlayıcıyla ilgili hizmetlerden hiçbiri işlevsel değildir. Ek konak sistem konuları ve/veya seçenekleri için lütfen sağlanan **readme_threadx.txt** dosyasını gözden geçirin.

## <a name="product-distribution"></a>Ürün dağıtımı

Dağıtım diskinin tam içeriği hedef işlemci, geliştirme araçları ve satın alınan ThreadX SMP paketine bağlıdır. Ancak, çoğu ürün dağıtımı için ortak olan birkaç önemli dosyanın listesi aşağıda verilmiştir:

### <a name="threadx_express_startuppdf"></a>ThreadX_Express_Startup.pdf

Bu PDF, belirli bir hedef işlemci/Pano ve belirli geliştirme araçları üzerinde çalışan ThreadX SMP 'yi almak için basit ve dört adımlı bir yordam sağlar.

### <a name="readme_threadxtxt"></a>readme_threadx.txt

Hedef işlemci ve geliştirme araçları hakkında bilgiler de dahil olmak üzere ThreadX SMP bağlantı noktasıyla ilgili belirli bilgileri içeren metin dosyası.

| Araç | Açıklama |
| -------------- | ------------------------------------------------------------------------------------------------- |
| **tx_api. h**  | Tüm sistem eşlerini, veri yapılarını ve hizmet prototiplerini içeren C üstbilgi dosyası.             |
| **tx_port. h** | Tüm geliştirme araçlarını ve targetspecific veri tanımlarını ve yapılarını içeren C üstbilgi dosyası. |
|**demo_threadx. c**| Küçük bir demo uygulaması içeren C dosyası.|
|**TX. a (veya TX. lib)**| *Standart* paketiyle dağıtılan THREADX SMP C kitaplığının ikili sürümü.|

> [!IMPORTANT]
> Tüm dosya adları küçük bir durumdur. Bu adlandırma kuralı, komutların Linux (UNIX) geliştirme platformlarına dönüştürülmesini kolaylaştırır.

## <a name="threadx-smp-installation"></a>ThreadX SMP yüklemesi

ThreadX SMP yüklemesi basittir. Belirli ortamınız için ThreadX SMP yükleme hakkında ayrıntılı bilgi için, ***ThreadX_Express_Startup.pdf** _ dosyasına ve _ *_readme_threadx.txt_** dosyasına bakın.

> [!IMPORTANT]
> ThreadX SMP dağıtım diskini yedeklediğinizden ve güvenli bir yerde sakladığınızdan emin olun.

> [!IMPORTANT]
> Uygulama yazılımının ThreadX SMP kitaplık dosyası (genellikle **TX. a** veya **TX. lib**) ve C içerme dosyaları **tx_api. h** ve **tx_port. h**'a erişmesi gerekir. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaları uygulama geliştirme alanına kopyalayarak gerçekleştirilir.

## <a name="using-threadx-smp"></a>ThreadX SMP kullanma

ThreadX SMP kullanmak kolaydır. Temel olarak, uygulama kodu derleme sırasında ***tx_api. h** _ Içermeli ve THREADX SMP çalışma zamanı kitaplığı _*_TX. a_*_ (veya _ *_TX. lib)_* * ile bağlantı içermelidir.

Bir ThreadX SMP uygulaması derlemek için gereken dört adım vardır:

***Tx_api. h*** dosyasını THREADX SMP Hizmetleri veya veri yapıları kullanan tüm uygulama dosyalarına ekleyin.

Standart C ***Main** _ işlevini oluşturun. Bu işlev, ThreadX SMP 'yi başlatmak için sonunda _ *_tx_kernel_enter_** çağrısını çağırmalıdır. ThreadX SMP içermeyen uygulamaya özgü başlatma, çekirdeği girmeden önce eklenebilir.

> [!IMPORTANT]
> ThreadX SMP giriş işlevi **tx_kernel_enter** döndürmez. Bu nedenle, bundan sonra herhangi bir işlem veya işlev çağrısı yerleştirdiğinizden emin olun.

***Tx_application_define*** işlevini oluşturun. Bu, ilk sistem kaynaklarının oluşturulduğu yerdir. Sistem kaynaklarına örnek olarak iş parçacıkları, kuyruklar, bellek havuzları, olay bayrakları grupları, zaman uyumu sağlayıcılar ve semaforlar verilebilir.

Uygulama kaynağını derleyin ve ThreadX SMP çalışma zamanı kitaplığı ***TX. lib*** ile ilişkilendirin. Elde edilen görüntü hedefe indirilebilir ve yürütülür!

## <a name="small-example-system"></a>Küçük örnek sistem

Şekil 1 ' deki küçük örnek sistem, önceliği 3 olan tek bir iş parçacığının oluşturulmasını gösterir. İş parçacığı yürütülür, bir sayacı artırır, sonra bir saat çentik için uyku moduna geçer. Bu işlem süresiz olarak devam eder.

```c
#include              "tx_api.h"

unsigned long         my_thread_counter = 0;
TX_THREAD             my_thread;

main( )
{
      /* Enter the ThreadX SMP kernel. */
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

Bu basit bir örnek olsa da, gerçek uygulama geliştirmesi için iyi bir şablon sağlar. Daha fazla bilgi için lütfen ***readme_threadx.txt*** dosyasına bakın.

## <a name="troubleshooting"></a>Sorun giderme

Her ThreadX SMP bağlantı noktası, bir demo uygulaması ile birlikte dağıtılır. Her zaman, gerçek hedef donanım veya sanal ortam üzerinde tanıtım sisteminin çalışmasını sağlamak iyi bir fikirdir.

> [!IMPORTANT]
> Tanıtım sistemiyle ilgili daha ayrıntılı bilgiler için, dağıtımla birlikte sağlanan **readme_threadx.txt** dosyasına bakın.

Tanıtım sistemi düzgün yürütülemez, bazı sorun giderme ipuçları aşağıda verilmiştir:

  - Tanıtım ne kadarının çalıştırılacağını belirleme.

  - Yığın boyutlarını artırın (gerçek uygulama kodunda tanıtım için olduğundan daha önemlidir).

  - ThreadX SMP kitaplığını tanımlanan TX_ENABLE_STACK_CHECKING yeniden derleyin. Bu, yerleşik ThreadX SMP yığın denetimini etkinleştirir.

  - Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın. Bu tür bilgiler mühendislerin desteklenmesi için yararlı olmalıdır.

Sorun giderme adımlarından toplanan bilgileri göndermek için sayfa 12 ' de açıklanan yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

ThreadX SMP kitaplığı ve uygulama için ThreadX SMP kullanan çeşitli yapılandırma seçenekleri vardır. Aşağıdaki seçenekler uygulama kaynağında, komut satırında veya ***tx_user. h*** içerme dosyası içinde tanımlanabilir.

> [!IMPORTANT]
> **Tx_user. h** içinde tanımlanan seçenekler, yalnızca uygulama ve THREADX SMP kitaplığı, tanımlı **TX_INCLUDE_USER_DEFINE_FILE** ile derlenildiği takdirde uygulanır.

### <a name="smallest-configuration"></a>En küçük yapılandırma
En küçük kod boyutu için, aşağıdaki ThreadX SMP yapılandırma seçenekleri göz önünde bulundurulmalıdır (diğer tüm seçeneklerin yokluğunda):

- TX_DISABLE_ERROR_CHECKING
- TX_DISABLE_PREEMPTION_THRESHOLD
- TX_DISABLE_NOTIFY_CALLBACKS 
- TX_DISABLE_REDUNDANT_CLEARING 
- TX_DISABLE_STACK_FILLING 
- TX_NOT_INTERRUPTABLE 
- TX_TIMER_PROCESS_IN_ISR

### <a name="fastest-configuration"></a>En hızlı yapılandırma 
En hızlı yürütme için, daha önce en küçük yapılandırma için kullanılan yapılandırma seçenekleri, ancak bu seçenekle de göz önünde bulundurululur:

- TX_REACTIVATE_INLINE

Belirli bir ThreadX SMP sürümünüz için ek seçenekler için ***readme_threadx.txt*** dosyasını gözden geçirin. Ayrıntılı yapılandırma seçenekleri sayfa 28 ' den başlayarak açıklanır.

### <a name="global-time-source"></a>Küresel saat kaynağı  
Diğer Azure RTOS ürünleri (FileX, NetX, GUıDX, USBX, vb.) için ThreadX SMP, bir saniyeyi temsil eden ThreadX SMP Zamanlayıcı işareti sayısını tanımlar. Diğerleri zaman gereksinimlerini bu sabiti temel alarak türeteler. Varsayılan olarak, değer 100 ' dir ve bir 10 MS dönemsel kesmesi varsayılıyor. Kullanıcı, ***tx_port. h*** veya IDE veya komut satırı içindeki istenen değeri TX_TIMER_TICKS_PER_SECOND tanımlayarak bu değeri geçersiz kılabilir.

### <a name="detailed-configuration-options"></a>Ayrıntılı yapılandırma seçenekleri

- **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** : tanımlandığında, blok havuzlarındaki performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** : tanımlandığında, bayt havuzlarında performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_DISABLE_ERROR_CHECKING**: temel hizmet çağrısı hata denetimini atlar. Uygulama kaynağında tanımlandığında, tüm temel parametre hata denetimi devre dışı bırakılır. Bu, performansı %30 ' a kadar iyileştirebilir ve resim boyutunu da azaltabilir.

> [!NOTE]
> *Yalnızca uygulamanın tüm giriş parametrelerini, dış girişten türetilmiş giriş parametreleri de dahil olmak üzere tüm koşullarda her zaman geçerli olacağını düşünüyorsanız, hata denetimini devre dışı bırakabilirsiniz. Hata denetimi devre dışı olduğunda API için geçersiz giriş sağlanırsa, ortaya çıkan davranış tanımsızdır ve bellek bozulması veya sistem kilitlenmesiyle sonuçlanabilir.*

> [!NOTE]
> *Bir hata denetimini devre dışı bırakarak ThreadX SMP API 'SI dönüş değerleri, Bölüm 4 ' teki her API açıklamasının "dönüş değerleri" bölümünde kalın olarak listelenir. Hata denetimi TX_DISABLE_ERROR_CHECKING seçeneği kullanılarak devre dışı bırakılmışsa, kalın olmayan dönüş değerleri hükümsüz olur.*
- **TX_DISABLE_NOTIFY_CALLBACKS** : tanımlandığında, çeşitli THREADX SMP nesneleri için bildirim geri çağırmaları devre dışı bırakır. Bu seçeneğin kullanılması, kod boyutunu biraz azaltır ve performansı geliştirir. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_DISABLE_PREEMPTION_THRESHOLD** : tanımlandığında, önalım-Threshold özelliğini devre dışı bırakır ve kod boyutunu biraz azaltır ve performansı geliştirir. Kuşkusuz, preemptionthreshold özellikleri artık kullanılamaz. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_DISABLE_REDUNDANT_CLEARING** : tanımlandığında, THREADX SMP Global C veri yapılarını başlatma mantığını sıfır olarak kaldırır. Bu, yalnızca derleyicinin başlatma kodu tüm başlatılmamış C genel verilerini sıfıra ayarlarsa kullanılmalıdır. Bu seçeneğin kullanılması, kod boyutunu biraz azaltır ve başlatma sırasında performansı geliştirir. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_DISABLE_STACK_FILLING** : tanımlandığında, her iş parçacığının yığınının her baytında 0xEF değerini yerleştirmeyi devre dışı bırakır. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_ENABLE_EVENT_TRACE** : tanımlandığında THREADX SMP, bir tracex izleme arabelleği oluşturmak için olay toplama kodu sunar. Daha fazla ayrıntı için bkz. Trackingex Kullanıcı Kılavuzu.
- **TX_ENABLE_STACK_CHECKING** : tanımlandığında, THREADX SMP çalışma zamanı yığın denetimini, yığın alanından önce ve sonra ne kadar yığın kullanıldığını ve "slar" veri deseninin analizini içerir. Yığın hatası algılanırsa, kayıtlı uygulama yığını hata işleyicisi çağırılır. Bu seçenek, biraz daha fazla ek yüke ve kod boyutuna neden olur. Daha fazla bilgi için, **_tx_-thread_stack_error_notify_** API 'sini inceleyin. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** : tanımlandığında, olay bayrakları gruplarında performans bilgilerinin toplanmasında izin sağlanır. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_INLINE_THREAD_RESUME_SUSPEND** : tanımlanan THREADX SMP, satır içi kod aracılığıyla **_tx_thread_resume_*_ ve _*_tx_thread_suspend_** API çağrılarını geliştirir. Bu, kod boyutunu artırır ancak bu iki API çağrısının performansını geliştirir.
- **TX_MAX_PRIORITIES** : THREADX SMP için öncelik düzeylerini tanımlar. Yasal değerler 32 ile 1024 (dahil) arasındadır ve 32 ile eşit olarak bölünebilmelidir. Desteklenen öncelik düzeyi sayısının artırılması, her 32 öncelikteki RAM kullanımını 128 bayt kadar artırır. Ancak, performans üzerinde yalnızca göz ardı edilebilir bir efekt vardır. Varsayılan olarak, bu değer 32 öncelik düzeylerine ayarlanır.
- **TX_MINIMUM_STACK** : en düşük yığın boyutunu (bayt cinsinden) tanımlar. İş parçacıklarının oluşturulduğu zaman denetlenirken hata denetimi için kullanılır. Varsayılan değer, bağlantı noktasına özeldir ve **_tx_port. h_ içinde bulunur.**
- **TX_MISRA_ENABLE** : tanımlanan THREADX SMP, Misra C uyumlu kuralları kullanır. Ayrıntılar için **_ThreadX_MISRA_Compliance.pdf_** bakın.
- **TX_MUTEX_ENABLE_PERFORMANCE_INFO** : tanımlandığında, zaman uyumu sağlayıcılar üzerinde performans bilgilerini toplamaya izin vermez. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_NO_TIMER** : tanımlandığında, THREADX SMP Zamanlayıcı mantığı tamamen devre dışıdır. Bu, ThreadX SMP Zamanlayıcı özelliklerinin (iş parçacığı Sleep, API zaman aşımları, zaman diliminin ve uygulama zamanlayıcıları) kullanıldığı durumlarda faydalıdır.
- **TX_NOT_INTERRUPTABLE** : tanımlanan THREADX SMP, kesme kilitleme süresini en aza indirmeye çalışmaz. Bu, daha hızlı yürütmeye neden olur, ancak kesme kilitleme süresini biraz artırır.
- **TX_QUEUE_ENABLE_PERFORMANCE_INFO** : tanımlandığında, kuyruklarda performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_REACTIVATE_INLINE** : tanımlandığında, bir işlev çağrısı kullanmak yerine THREADX SMP süreölçerinin yeniden etkinleştirmeyi gerçekleştirir. Bu, performansı artırır ancak kod boyutunu biraz artırır. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** : tanımlandığında, Semaforlarda performans bilgilerinin toplanmasında izin sağlanır. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_THREAD_ENABLE_PERFORMANCE_INFO** : tanımlandığında, iş parçacıklarında performans bilgilerinin toplanması etkinleştirilir. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_THREAD_SMP_CORE_MASK** : çekirdek dışlama için bit eşleme maskesini tanımlar. Örneğin, 4 çekirdekli bir ortamda bu tanımlama için 0xF değeri bulunur.
- **TX_THREAD_SMP_DEBUG_ENABLE** : tanımlandığında, THREADX SMP hata ayıklama bilgileri döngüsel bir arabellekte kaydedilir.
- **TX_THREAD_SMP_DYNAMIC_CORE_MAX** : tanımlandığında, çalışma zamanında ayarlanoluşturulabilecek en fazla çekirdek sayısını dinamik olarak sunar.
- **TX_THREAD_SMP_EQUAL_PRIORITY** : tanımlanan THREADX SMP yalnızca paralel olarak eşit öncelikli iş parçacıklarını zamanlar. Bu, ThreadX SMP kitaplığı oluşturmadan önce tanımlanmalıdır.
- **TX_THREAD_SMP_INTER_CORE_INTERRUPT** : tanımlanan THREADX SMP, çekirdek tabanlı kesmeler oluşturur.
- **TX_THREAD_SMP_MAX_CORES** : en fazla çekirdek sayısını tanımlar.
- **TX_THREAD_SMP_ONLY_CORE_0_DEFAULT** : tanımlı olduğunda, THREADX SMP varsayılan olarak yalnızca Core 0 üzerinde yürütülecek tüm iş parçacıkları ve zamanlayıcılar belirler. Uygulama, çekirdek dışlama API 'Lerini çağırarak bunu geçersiz kılabilir. Bu, ThreadX SMP kitaplığı oluşturmadan önce tanımlanmalıdır.
- **TX_THREAD_SMP_WAKEUP_LOGIC** : tanımlandığında, "i" çekirdeğini Uyandırma için uygulama makrosu çağrılır. Bu, **_tx_port. h_ dahil etmeden önce tanımlanmalıdır.**
- **TX_THREAD_SMP_WAKEUP (i)** : "i" çekirdeğini Uyandırma için bir uygulama makrosu tanımlar. Bu, **_tx_port. h_ dahil etmeden önce tanımlanmalıdır.**
- **TX_TIMER_ENABLE_PERFORMANCE_INFO** : tanımlandığında, zamanlayıcılar üzerinde performans bilgilerini toplamaya izin vermez. Varsayılan olarak, bu seçenek tanımlı değildir.
- **TX_TIMER_PROCESS_IN_ISR** : tanımlandığında, THREADX SMP için iç sistem Zamanlayıcı iş parçacığını ortadan kaldırır. Süreölçer yığınına ve denetim bloğuna artık gerek duyulmadığından, bu durum Zamanlayıcı olaylarına ve daha küçük RAM gereksinimlerine göre performansı artırmasına neden olur. Ancak, bu seçeneğin kullanılması, tüm Zamanlayıcı süre sonu işlemesini Zamanlayıcı ıSR düzeyine kaydırır. Varsayılan olarak, bu seçenek tanımlı değildir.

    > [!NOTE]
    > Zamanlayıcılardan izin verilen hizmetlere ISRs 'den izin verilmeyebilir, bu nedenle bu seçenek kullanılırken izin verilmiyor olabilir.

- **TX_TIMER_THREAD_PRIORITY** : Iç THREADX SMP sistem Zamanlayıcı iş parçacığının önceliğini tanımlar. Varsayılan değer öncelik 0 ' dır; ThreadX SMP ' de en yüksek öncelik. Varsayılan değer **_tx_port. h_ içinde tanımlanır.**
- **TX_TIMER_THREAD_STACK_SIZE** : Iç THREADX SMP sistem Zamanlayıcı iş parçacığının yığın boyutunu (bayt olarak) tanımlar. Bu iş parçacığı tüm iş parçacığı uyku isteklerinin yanı sıra tüm hizmet çağrı zaman aşımlarını işler. Ayrıca, tüm uygulama süreölçeri geri çağırma yordamları bu içerikten çağrılır. Varsayılan değer, bağlantı noktasına özeldir ve **_tx_port. h_ içinde bulunur.**

## <a name="threadx-smp-version-id"></a>ThreadX SMP sürüm KIMLIĞI

ThreadX SMP sürüm KIMLIĞI, ***readme_threadx.txt** _ dosyasında bulunabilir. Bu dosya Ayrıca karşılık gelen bağlantı noktasının sürüm geçmişini içerir. Uygulama yazılımı, ThreadX SMP sürümünü genel dize olan _ *_ _tx_version_id_* inceleyerek alabilir.*