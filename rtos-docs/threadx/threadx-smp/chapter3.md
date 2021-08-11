---
title: Bölüm 3 - Azure RTOS ThreadX SMP'nin İşlevsel Bileşenleri
description: Bu bölümde, işlevsel bir perspektiften ThreadX SMP Azure RTOS yüksek performans düzeyinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 04676491f8ccaa98fa9ad396c221c38901c188b420ed710da3c96d863b49e6c5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799336"
---
# <a name="chapter-3---functional-components-of-azure-rtos-threadx-smp"></a>Bölüm 3 - Azure RTOS ThreadX SMP'nin İşlevsel Bileşenleri

Bu bölümde, işlevsel bir perspektiften ThreadX SMP Azure RTOS yüksek performans düzeyinin açıklaması yer almaktadır. Her işlevsel bileşen kolay anlaşılır bir şekilde sunulmaktadır.

## <a name="execution-overview"></a>Yürütmeye Genel Bakış

Bir ThreadX SMP uygulamasında dört tür program yürütmesi vardır: Başlatma, İş Parçacığı Yürütme, Kesinti Hizmeti Yordamları (ISR) ve Uygulama Süreyerleri.

Şekil 1'in 45. sayfasında her farklı program yürütme türü görüntülenir. Bu türlerin her biri hakkında daha ayrıntılı bilgiler bu bölümün sonraki bölümlerinde bulunabilir.

### <a name="initialization"></a>Başlatma
Addan da anlaşılacağı gibi bu, bir ThreadX SMP uygulamasında program yürütmenin ilk t t'tir. Başlatma, işlemci sıfırlaması ile iş parçacığı zamanlama döngüsü giriş noktası arasındaki tüm program *yürütmesini içerir.*

> [!IMPORTANT]
> Başlatma, sıfırlama sonrasında varsayılan çalışan çekirdek olan çekirdek 0 tarafından gerçekleştirilir veya başlatılır.

### <a name="thread-execution"></a>İş Parçacığı Yürütme
Başlatma tamamlandıktan sonra, ThreadX SMP çalıştıran her çekirdek iş parçacığı zamanlama döngüsüne girer. Zamanlama döngüsü, bu çekirdek üzerinde yürütme için hazır bir uygulama iş parçacığını okur. Hazır bir iş parçacığı bulunursa, ThreadX SMP denetimi bu iş parçacığına iletır. İş parçacığı tamam olduktan (veya başka bir yüksek öncelikli iş parçacığı hazır hale gelir), yürütme her çekirdekte bir sonraki en yüksek öncelikli hazır iş parçacığını bulmak için iş parçacığı zamanlama döngüsüne geri aktarıyor.

İş parçacıklarını sürekli olarak yürütme ve zamanlama işlemi, ThreadX SMP uygulamalarında program yürütmenin en yaygın t t t'leridir.

![İş Parçacığı Yürütme](media/image4.png)

**ŞEKIL 1. Program Yürütme Türleri**

### <a name="interrupt-service-routines-isr"></a>Hizmet Yordamlarını Kesme (ISR)
Kesmeler, gerçek zamanlı sistemlerin temel taşıdır. Kesintiler olmadan dış dünyada yapılan değişikliklere zamanında yanıt vermek son derece zor olabilir. Bir kesme algılanmasında, işlemci geçerli program yürütmesi hakkında önemli bilgileri kaydeder (genellikle yığında), ardından denetimi önceden tanımlanmış bir program alanına iletir. Önceden tanımlanmış bu program alanı genellikle Kesme Hizmeti Yordamı olarak da adlandırılan bir alandır.

Çoğu durumda, kesintiler iş parçacığı yürütme sırasında (veya iş parçacığı zamanlama döngüsünde) oluşur. Ancak, kesintiler yürütülen bir ISR veya Uygulama Süreölçeri içinde de oluşabilir.

Tüm çekirdeklerin kesmeleri işlemesine izin verilir. Kesmeleri çekirdeklere eşleme, uygulamanın doğrudan denetimi altındadır. ThreadX SMP zamanlayıcı kesintisi, işleme için çekirdek 0'a varsayılan olarak atanır. Lütfen aşağıdaki koda *tx_timer_interrupt. Bu* atamanın uygulanması için S.

### <a name="application-timers"></a>Uygulama Süre süreleri
Uygulama Süre süreleri ISR'lere benzer, ancak donanım uygulaması (genellikle tek bir düzenli donanım kesintisi kullanılır) uygulamanın dışında gizlenir. Bu tür süreler, uygulamalar tarafından zaman aralıklarını, düzenli aralıklarla ve/veya izleme hizmetlerini gerçekleştirmek için kullanılır. ISR'ler gibi Uygulama Süre süreleri de genellikle iş parçacığı yürütmeyi kesintiye uğratmaz. Ancak ISR'lerin aksine, Uygulama Süreleri birbirini kesintiye uğratmaz.

> [!NOTE]
> Bu da iş parçacıkları gibi uygulama süre sürelerini de herhangi bir çekirdekte yürütmenin dışında bırakabilirsiniz.

## <a name="memory-usage"></a>Bellek Kullanımı

ThreadX SMP, uygulama programıyla birlikte yer almaktadır. Sonuç olarak, ThreadX SMP'nin statik bellek (veya sabit bellek) kullanımı geliştirme araçları tarafından belirlenir; Örneğin, derleyici, bağlantılayıcı ve bulucu. Dinamik bellek (veya çalışma zamanı belleği) kullanımı uygulamanın doğrudan denetimi altındadır.

> [!NOTE]
> ThreadX SMP tarafından erişilen tüm bellek, Önbellek tutarlı olmalı ve ThreadX SMP yürüten tüm çekirdeklerden erişilebilir durumdadır.

### <a name="static-memory-usage"></a>Statik Bellek Kullanımı
Geliştirme araçlarının çoğu uygulama programı görüntüsünü beş temel bölüme böler: *yönerge,* *sabit,* başlatılan *veriler,* başlatılmamış *veriler* ve *sistem yığını.* Şekil 2'de sayfa 47'de bu bellek alanlarının bir örneği görüntülenir.

![Statik Bellek Kullanımı](media/image5.png)

**ŞEKIL 2. Bellek Alanı Örneği**

Bunun yalnızca bir örnek olduğunu anlamak önemlidir. Gerçek statik bellek düzeni işlemciye, geliştirme araçlarına ve temel alınan donanıma özeldir.

Yönerge alanı, programın tüm işlemci yönergelerini içerir. Bu alan genellikle en büyük alandır ve genellikle ROM'da bulunur.

Sabit alanı, program içinde tanımlanan veya başvurulan dizeler de dahil olmak üzere çeşitli derlenmiş sabitler içerir. Ayrıca, bu alan başlatılan veri alanı "ilk kopyasını" içerir. Derleyicinin başlatma işlemi sırasında sabit alanı bu kısmı RAM'de başlatılan veri alanı ayarlamak için kullanılır. Sabit alan genellikle yönerge alanına göredir ve genellikle ROM'da bulunur.

Başlatılan veriler ve başlatılmamış veri alanları genel ve statik değişkenlerin hepsini içerir. Bu alanlar her zaman RAM'de bulunur.

Sistem yığını genellikle başlatılan ve başlatılmamış veri alanlarının hemen ardından ayarlanır. Sistem yığını, başlatma sırasında derleyici tarafından, ardından başlatma sırasında ThreadX SMP ve daha sonra ISR işlemesinde kullanılır.

### <a name="dynamic-memory-usage"></a>Dinamik Bellek Kullanımı
Daha önce belirtildiği gibi, dinamik bellek kullanımı uygulamanın doğrudan denetimi altındadır. Yığınlar, kuyruklar ve bellek havuzları ile ilişkili denetim blokları ve bellek alanları hedefin bellek alanı içinde herhangi bir yere yerleştirilebilirsiniz. Bu önemli bir özelliktir çünkü farklı fiziksel bellek türlerinin kolay kullanımını kolaylaştırır.

Örneğin, hedef donanım ortamının hem hızlı belleğe hem de yavaş belleğe sahip olduğunu varsayalım. Uygulamanın yüksek öncelikli bir iş parçacığı için ek performansa ihtiyacı varsa, denetim bloğu (TX_THREAD) ve yığını hızlı bellek alanına yerleştirilebilir ve bu da performansını önemli ölçüde geliştirebilir.

## <a name="initialization"></a>Başlatma 
Başlatma işlemini anlamak önemlidir. İlk donanım ortamı burada ayarlanır. Buna ek olarak, uygulamaya ilk kişiliği de burada verilir.

> [!IMPORTANT]
> ThreadX SMP, geliştirme aracının başlatma işleminin tamamlandıktan sonra (mümkün olduğunca) yararlanmaya çalışır. Bu, gelecekte geliştirme araçlarının yeni sürümlerine yükseltmeyi kolaylaştırır.

### <a name="system-reset-vector"></a>Sistem Sıfırlama Vektörü 
Tüm mikro işlemcilerin sıfırlama mantığı vardır. Sıfırlama (donanım veya yazılım) oluştuğunda, uygulamanın giriş noktasının adresi belirli bir bellek konumdan alınır. Giriş noktası alındıktan sonra işlemci denetimi bu konuma iletir. 

Uygulama giriş noktası genellikle yerel derleme dilinde yazılır ve genellikle geliştirme araçları tarafından sağlanır (en azından şablon formunda). Bazı durumlarda, giriş programının özel bir sürümü ThreadX SMP ile sağlanır. 

### <a name="development-tool-initialization"></a>Geliştirme Aracı Başlatma
Alt düzey başlatma tamamlandıktan sonra denetim aktarımları geliştirme aracının üst düzey başlatması olur. Bu genellikle başlatılmış genel ve statik C değişkenlerinin ayar bulunduğu yerdir. İlk değerlerinin sabit alandan alın olduğunu unutmayın. Tam başlatma işlemi geliştirme aracına özeldir.

### <a name="main-function"></a>main İşlevi 
Geliştirme aracını başlatma işlemi tamamlandığında, kullanıcı tarafından sağlanan ana işleve *aktarımları kontrol* edin. Bu noktada, bundan sonra ne olacağını uygulama kontrol eder. Çoğu uygulama için main işlevi, ThreadX *SMP'tx_kernel_enter* girişi olan tx_kernel_enter çağrısında kullanılmaktadır. Ancak, uygulamalar ThreadX SMP girmeden önce ön işlemleri (genellikle donanım başlatma için) gerçekleştirebilirsiniz.

> [!IMPORTANT]
> Tx_kernel_enter çağrısı geri dönmez, bu nedenle sonrasında herhangi bir işlem yapma!

### <a name="tx_kernel_enter"></a>tx_kernel_enter 
Giriş işlevi çeşitli iç ThreadX SMP veri yapılarının başlatmasını koordine ediyor ve ardından uygulamanın tanım işlevini *tx_application_define.*

Bu *tx_application_define,* denetim iş parçacığı zamanlama döngüsüne aktarılır. Bu, başlatmanın sonuna işaret ediyor!

### <a name="application-definition-function"></a>Uygulama Tanımı İşlevi
Tx_application_define  işlevi tüm ilk uygulama iş parçacıklarını, kuyrukları, semaforları, mutex'leri, olay bayraklarını, bellek havuzlarını ve süreçerleri tanımlar. Uygulamanın normal çalışması sırasında iş parçacıklarından sistem kaynakları oluşturmak ve silmek de mümkündür. Ancak, tüm ilk uygulama kaynakları burada tanımlanır.

bu *tx_application_define* tek bir giriş parametresine sahiptir ve kesinlikle bahsetmeye değer. Kullanılabilir ilk RAM *adresi,* bu işlevin tek giriş parametresidir. Genellikle iş parçacığı yığınlarının, kuyrukların ve bellek havuzlarının ilk çalışma zamanı bellek ayırmaları için bir başlangıç noktası olarak kullanılır.

> [!IMPORTANT]
> Başlatma tamamlandıktan sonra, yalnızca bir çalışan iş parçacığı, diğer iş parçacıkları dahil olmak üzere sistem kaynaklarını oluşturabilir ve silebilir. Bu nedenle, başlatma sırasında en az bir iş parçacığının oluşturulması gerekir.

### <a name="interrupts"></a>Kesmelerini 
Kesmeler, başlatma işleminin tamamı sırasında devre dışı bırakılır. Uygulama kesintiye yol açabilir, öngörülemeyen bir davranış meydana gelebilir. Şekil 3 ' 52 te, uygulama özel başlatma aracılığıyla sistem sıfırlamalarından tüm başlatma sürecini gösterir.

## <a name="thread-execution"></a>İş parçacığı yürütme

Uygulama iş parçacıklarını zamanlama ve yürütme, ThreadX SMP 'nin en önemli etkinliğidir. İş parçacığı genellikle adanmış bir amaçla yarı bağımsız program segmenti olarak tanımlanır. Tüm iş parçacıklarının birleştirilmiş işleme bir uygulama oluşturur.

İş parçacıkları, başlatma sırasında veya iş parçacığı yürütme sırasında *tx_thread_create* çağırarak dinamik olarak oluşturulur. İş parçacıkları, *Ready* veya *askıya alınmış* durumda oluşturulur.

![SMP başlatma Işlemi](media/image6.png)

**ŞEKIL 3. SMP başlatma Işlemi**

### <a name="thread-execution-states"></a>İş parçacığı yürütme durumları  
İş parçacıklarının farklı işleme durumlarını anlamak, çok iş parçacıklı ortamın tamamını anlamak için önemli bir ortamdır. ThreadX SMP ' de, beş farklı iş parçacığı durumu vardır: *hazırlanıyor*, *askıya alındı*, *yürütülüyor*, *sonlandırıldı* ve *tamamlandı*. Şekil 4 ' te ThreadX SMP için iş parçacığı durum geçişi diyagramı gösterilmektedir.

![İş parçacığı yürütme durumları](media/image7.png)

**ŞEKIL 4. İş parçacığı durum geçişi**

İş parçacığı, yürütülmeye hazırlanmaya hazırsa, *hazırlık* durumundadır. Hazırlık durumunda en yüksek öncelikli iş parçacığı olana kadar, Ready iş parçacığı yürütülmez. Bu durumda, ThreadX SMP iş parçacığını yürütür ve sonra durumunu *yürütülüyor* olarak değiştirir.

Daha yüksek öncelikli bir iş parçacığı hazır hale gelirse, çalıştırılan iş parçacığı *hazır* duruma geri döner. Daha sonra yeni, yüksek öncelikli iş parçacığı yürütülür ve bu, mantıksal durumu *yürütülüyor* olarak değiştirir. Hazırlama *ve* *yürütme* durumları arasındaki bu geçiş, iş parçacığı önalım her gerçekleştiğinde oluşur.

Herhangi bir anda yalnızca bir iş parçacığı *yürütülüyor* durumundadır. Bunun nedeni, *yürütme* durumundaki bir iş parçacığının temeldeki işlemcinin denetimine sahip olmasından kaynaklanır.

*Askıya alınmış* durumdaki iş parçacıkları yürütme için uygun değildir. *Askıya* alınma durumunda olma nedenleri, zaman, kuyruk iletileri, Semaforlar, zaman uyumu sağlayıcılar, olay bayrakları, bellek ve temel iş parçacığı askıya alma için askıya alma içerir. Askıya alma *işlemine* neden kaldırıldıktan sonra, iş parçacığı, hazırlama durumuna geri yerleştirilir.

*Tamamlanmış* durumdaki bir iş parçacığı, işlemini tamamlamış ve giriş işlevinden döndürülen bir iş parçacığıdır. Giriş işlevi iş parçacığı oluşturma sırasında belirtilir. *Tamamlanmış* durumdaki bir iş parçacığı yeniden çalıştırılamaz.

Başka bir iş parçacığı veya iş parçacığının kendisi *tx_thread_terminate* hizmeti olarak adlandırıldığından, iş parçacığı *sonlandırılmış* durumda olur. *Sonlandırılmış* durumdaki bir iş parçacığı yeniden çalıştırılamaz.

> [!IMPORTANT]
> Tamamlanmış veya sonlandırılmış bir iş parçacığının yeniden başlatılması istenirse, uygulamanın iş parçacığını silmesi gerekir. Daha sonra yeniden oluşturulup yeniden başlatılabilir.

### <a name="thread-entryexit-notification"></a>İş parçacığı giriş/çıkış bildirimi  
Bazı uygulamalar, belirli bir iş parçacığının ilk kez girildiği, tamamlandığında veya sonlandırıldığı zaman bildirilmeye yönelik avantajı bulabilir. ThreadX SMP, *tx_thread_entry_exit_notify* hizmeti aracılığıyla bu yeteneği sağlar. Bu hizmet, iş parçacığı çalışmaya başladığında, tamamlandığında veya sonlandırıldığı zaman, ThreadX SMP tarafından çağrılan belirli bir iş parçacığı için bir uygulama bildirim işlevi kaydeder. Çağrıldıktan sonra, uygulama bildirim işlevi applicationspecific işlemini gerçekleştirebilir. Bu genellikle, bir ThreadX SMP eşitleme temel aracılığıyla olayın başka bir uygulama iş parçacığının bilgilendirmesi içerir.

### <a name="thread-priorities"></a>İş parçacığı öncelikleri  
Daha önce bahsedildiği gibi, iş parçacığı adanmış bir amaca sahip yarı bağımsız bir program segmentine sahip olur. Ancak, tüm iş parçacıkları eşit olarak oluşturulmaz! Bazı iş parçacıklarının adanmış amacı diğerlerine göre çok daha önemlidir. Bu heterojen iş parçacığı önemi türü, gömülü gerçek zamanlı uygulamaların bir Hallmark.

ThreadX SMP, bir iş parçacığının *önceliğini* temsil eden bir sayısal değer atanarak oluşturulduğu zaman bir iş parçacığının önemini belirler. ThreadX SMP önceliklerinin en yüksek sayısı, 32 ile 1024 arasındaki 32 artışlarla arasında yapılandırılabilir. Fiili en yüksek öncelik sayısı, ThreadX SMP kitaplığı derlenirken *TX_MAX_PRIORITIES* sabiti tarafından belirlenir. Daha fazla sayıda öncelik olması, işleme ek yükünü önemli ölçüde artırmaz. Ancak, her 32 öncelik düzeyindeki bir grup için, bunları yönetmek için ek 128 baytlık RAM gerekir. Örneğin, 32 öncelik düzeyleri 128 bayt RAM gerektirir, 64 öncelik düzeyi 256 bayt RAM gerektirir ve 96 öncelik düzeyleri, 384 bayt RAM gerektirir.

Varsayılan olarak, ThreadX SMP 32 öncelik düzeylerine sahiptir ve öncelik 0 ile öncelik 31 arasında değişir.

Sayısal olarak daha küçük değerler daha yüksek önceliğe sahiptir. Bu nedenle öncelik 0 en yüksek önceliği temsil ederken öncelik (*TX_MAX_PRIORITIES*-1) en düşük önceliği temsil eder.

Birden çok iş parçacığı, ortak zamanlamaya göre veya zaman dilimlemeye bağlı olarak aynı önceliğe sahip olabilir. Ayrıca, iş parçacığı öncelikleri çalışma zamanı sırasında değiştirilebilir.

### <a name="thread-scheduling"></a>İş parçacığı zamanlaması 
ThreadX SMP, iş parçacıklarını önceliklerine göre zamanlar. En yüksek önceliğe sahip olan Ready iş parçacığı önce yürütülür. Aynı önceliğe sahip birden çok iş parçacığı hazır ise, ilk *çıkar* (FIFO) şekilde yürütülür.

Varsayılan olarak, ThreadX SMP, "n" kullanılabilir işlemcilerde "n" en yüksek öncelikli iş parçacıklarını zamanlar. Eşzamanlı işleme yalnızca aynı önceliğe sahip hazır iş parçacıklarında gerekliyse, ThreadX SMP kitaplığı tanımlı **TX_THREAD_SMP_EQUAL_PRIORITY** oluşturulmalıdır.

> [!NOTE]
> Tüm iş parçacıklarının başlangıçta yalnızca Core 0 üzerinde çalışması için, tanımlanan **TX_THREAD_SMP_ONLY_CORE_0_DEFAULT** Ile THREADX SMP kitaplığı oluşturulur.

### <a name="round-robin-scheduling"></a>Hepsini bir kez deneme zamanlaması  
ThreadX SMP, aynı önceliğe sahip birden çok iş parçacığının *hepsini bir kez deneme* zamanlamasını destekler. Bu, *tx_thread_relinquish* için birlikte gerçekleştirilen çağrılar aracılığıyla yapılır. Bu hizmet, *tx_thread_relinquish* çağıranı yeniden yürütmeden önce yürütülmesi için aynı önceliğe sahip diğer tüm diğer iş parçacıklarını sağlar.

### <a name="time-slicing"></a>Time-Slicing 
*Zaman Dilimleme* , bir hepsini bir kez deneme zamanlama biçimidir. Zaman dilimi, bir iş parçacığının işlemciyi vermeden yürütebilmesi için en fazla Zamanlayıcı sayısını (süreölçer kesmesi) belirtir. ThreadX SMP ' de zaman dilimbir iş parçacığı temelinde kullanılabilir. İş parçacığının zaman dilimi oluşturma sırasında atanır ve çalışma zamanında değiştirilebilir. Bir zaman dilimi süresi dolmuşsa, aynı öncelik düzeyindeki tüm diğer hazırlık iş parçacıklarının, saat dilimlenmiş iş parçacığı yeniden yürütülmeden önce yürütülmesi için bir şans verilir.

Yeni bir iş parçacığı zaman dilimi, askıya alındıktan sonra bir iş parçacığına verildiğinde, yeniden, önalım neden olan veya kendi zaman zaman yaptığı bir ThreadX SMP hizmeti çağrısını yapar.

Zaman dilimlenmiş bir iş parçacığı önceden boşaltıldı, zaman diliminin geri kalanı için eşit önceliğe sahip diğer iş parçacıklarından önce devam edecektir.

> [!IMPORTANT]
> Zaman dilimletmek, daha hafif bir sistem yükü miktarına neden olur. Zaman dilimi yalnızca birden fazla iş parçacığının aynı önceliğe sahip olduğu durumlarda faydalıdır, benzersiz önceliğe sahip iş parçacıkları zaman dilimine atanmamalıdır.

### <a name="preemption"></a>Önalım 
Önalım, yürütülen bir iş parçacığını daha yüksek öncelikli bir iş parçacığına göre geçici olarak kesintiye uğratma işlemidir. Bu işlem yürütülmekte olan iş parçacığında görünmez. Yüksek öncelikli iş parçacığı tamamlandığında, denetim, önalım gerçekleştiği konuma doğru konuma aktarılır.

Bu, önemli uygulama olaylarına hızlı yanıt sağladığından gerçek zamanlı sistemlerdeki çok önemli bir özelliktir. Önalım çok önemli bir özellik olsa da,, aşırı yük ve öncelik Inversion gibi çeşitli sorunların bir kaynağı olabilir.

### <a name="preemption-threshold"></a>Önalım-Threshold™ 
ThreadX SMP, önalım 'in bazı sorunlarından bazılarını kolaylaştırmak için *önalım-Threshold* adlı benzersiz ve gelişmiş bir özellik sunar.

Bir önalım-Threshold, bir iş parçacığının önalım 'yi devre dışı bırakmak için öncelikli *tavan* belirlemesine izin verir. Tavan genişliğinden daha yüksek öncelikler olan iş parçacıklarının hala preempt olmasına izin verilmez.

Örneğin, 20 önceliğiyle bir iş parçacığının yalnızca 15 ile 20 arasında öncelikler olan bir iş parçacığı grubuyla etkileşimde bulunduğunu varsayalım. Kritik bölümleri sırasında 20 öncelikli iş parçacığı, önalım eşiğini 15 olarak ayarlayabilir, böylece etkileşime girdiği tüm iş parçacıklarından önalım önler. Bu, gerçekten önemli iş parçacıklarının (0 ve 14 arasındaki öncelikler), kritik bölüm işleme sırasında bu iş parçacığını hafiflemesine izin verir ve bu da daha fazla yanıt vermeye devam eder.

Tabii ki, önalım eşiğini 0 olarak ayarlayarak bir iş parçacığının tüm önalım devre dışı bırakılması yine de mümkündür. Ayrıca, önalım-Threshold, çalışma zamanı sırasında değiştirilebilir.

> [!IMPORTANT]
> Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.

### <a name="priority-inheritance"></a>Öncelikli devralma 
ThreadX SMP, bu bölümün ilerleyen kısımlarında açıklanan mutex Hizmetleri içinde isteğe bağlı öncelik devralmayı da destekler. Öncelikli devralma, düşük öncelikli iş parçacığına ait olan bir mutex için bekleyen yüksek öncelikli bir iş parçacığının önceliğini geçici olarak kabul etmesine olanak tanır. Bu özellik, ara iş parçacığı önceliklerinin önlenliğini ortadan kaldırarak uygulamanın belirlenemeyen öncelik tersini önlemeye yardımcı olur. Elbette benzer *bir sonuç elde etmek için* ön-ön eşik kullanılabilir.

### <a name="thread-creation"></a>İş Parçacığı Oluşturma 
Uygulama iş parçacıkları başlatma sırasında veya diğer uygulama iş parçacıklarının yürütülmesi sırasında oluşturulur. Bir uygulama tarafından oluşturulacak iş parçacığı sayısına bir sınır yoktur.

### <a name="thread-control-block-tx_thread"></a>İş Parçacığı Denetim Bloğu TX_THREAD 
Her iş parçacığının özellikleri denetim bloğunda yer almaktadır. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

Bir iş parçacığının denetim bloğu bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı yapmaktır.

Tüm dinamik olarak ayrılan bellekler gibi, diğer alanlarda denetim bloğu bulmak için biraz daha özenli olmak gerekir. Bir denetim bloğu bir C işlevi içinde ayrılırsa, bu işlevle ilişkili bellek, çağıran iş parçacığı yığınının bir parçası olur. Genel olarak, başka bir iş parçacığının bunu bir denetim bloğu için kullanıp kullanmamasından bağımsız olarak işlev döndürdikten sonra tüm yerel değişken yığın alanı serbest bırakılana kadar denetim blokları için yerel depolamayı kullanmaktan kaçının!

Çoğu durumda uygulama, iş parçacığının denetim bloğunun içeriğine karşı görünmez. Ancak, özellikle hata ayıklama sırasında belirli üyelere bakmanın yararlı olduğu bazı durumlar vardır. Aşağıda, daha kullanışlı denetim bloğu üyelerinden bazıları ve daha fazladır:

- **tx_thread_run_count,** iş parçacığının zamanlandığı sayıda sayacı içerir. Artan sayaç, iş parçacığının zamanlandığı ve yürütülmakta olduğunu gösterir.

- **tx_thread_state** iş parçacığının durumunu içerir. Olası iş parçacığı durumları aşağıda listelemektedir:

    - TX_READY(0x00)
    - TX_COMPLETED(0x01)
    - TX_TERMINATED(0x02)
    - TX_SUSPENDED(0x03)
    - TX_SLEEP(0x04)
    - TX_QUEUE_SUSP(0x05)
    - TX_SEMAPHORE_SUSP(0x06)
    - TX_EVENT_FLAG (0x07)
    - TX_BLOCK_MEMORY(0x08)
    - TX_BYTE_MEMORY (0x09)
    - TX_MUTEX_SUSP(0x0D)

> [!IMPORTANT]
> Elbette iş parçacığı denetim bloğunda yığın işaretçisi, zaman dilimi değeri, öncelikler vb. gibi birçok ilgi çekici alan daha vardır. Kullanıcılar denetim bloğu üyelerini gözden geçirebilirsiniz, ancak değişiklikler kesinlikle yasaktır!

> [!IMPORTANT]
> Bu bölümün önceki kısımlarında bahsedilen "yürütme" durumunun bir eşitliği yoktur. Belirli bir zamanda yalnızca bir yürüten iş parçacığı olduğundan bu gerekli değildir. Yürütülen iş parçacığının durumu da ***TX_READY.***

### <a name="currently-executing-thread"></a>Şu Anda Yürütülen İş Parçacığı 
Daha önce belirtildiği gibi, herhangi bir zamanda yürütülen yalnızca bir iş parçacığı vardır. İstekte bulunan iş parçacığına bağlı olarak, yürüten iş parçacığını tanımlamanın birkaç yolu vardır.

Bir program kesimi, tx_thread_identify çağırarak yürütülen iş parçacığının denetim ***bloğu adresini tx_thread_identify.*** Bu, uygulama kodunun birden çok iş parçacığından yürütülen paylaşılan kısımlarında kullanışlıdır.

Hata ayıklama oturumlarında, kullanıcılar iç ThreadX SMP işaretçi dizisi ***_tx_thread_current_ptr[core] inceler.*** O anda yürütülen iş parçacığının denetim bloğu adresini içerir. Bu işaretçi NULL ise, hiçbir uygulama iş parçacığı yürütülmektedir; Diğer bir ifadeyle, ThreadX SMP bir iş parçacığının hazır olması için zamanlama döngüsünde bekler.

### <a name="thread-stack-area"></a>İş Parçacığı Yığın Alanı 
Her iş parçacığının son yürütme ve derleyici kullanımının bağlamını kaydeden kendi yığınına sahip olması gerekir. C derleyicilerinin çoğu, işlev çağrıları yapmak ve yerel değişkenleri geçici olarak kullanmak için yığını kullanır. Şekil 5'te 61. sayfa tipik bir iş parçacığı yığınını gösterir.

![İş Parçacığı Yığın Alanı](media/image8.png)

**ŞEKIL 5. Tipik İş Parçacığı Yığını**

Bellekte bir iş parçacığı yığınının bulunduğu yer uygulamaya bağlı olur. Yığın alanı iş parçacığı oluşturma sırasında belirtilir ve hedefin adres alanında herhangi bir yere yer olabilir. Uygulamaların yığınlarını yüksek hızlı RAM'e yerleştirerek önemli iş parçacıklarının performansını artırmalarına olanak sağlayan bu önemli bir özelliktir.

Yığının ne kadar büyük olması gerektiği, iş parçacıkları hakkında en sık sorulan sorulardan biri. Bir iş parçacığının yığın alanı iç içe yerleştirme, yerel değişken ayırma ve son yürütme bağlamını kaydetme gibi en kötü durum işlev çağrılarına uyum sağlayacak kadar büyük olması gerekir.

en düşük yığın boyutu **(TX_MINIMUM_STACK,** ThreadX SMP tarafından tanımlanır. Bu boyutta bir yığın, bir iş parçacığının bağlamını ve minimum işlev çağrısı miktarını ve yerel değişken ayırmayı kaydetmeyi destekler.

Ancak çoğu iş parçacığı için minimum yığın boyutu çok küçüktür ve kullanıcının işlev çağrısı iç içe geçme ve yerel değişken ayırmayı inceleerek en kötü harf boyutu gereksinimini tespitsi gerekir. Elbette daha büyük bir yığın alanıyla başlamak her zaman daha iyidir.

Uygulama hata ayıklandıktan sonra, bellek azsa iş parçacığı yığını boyutlarını ayarlamak mümkündür. Sık kullanılan bir püf noktası, iş parçacıklarını oluşturmadan önce tüm yığın alanlarını (0xEFEF) gibi kolayca tanımlanabilir bir veri deseniyle önceden ayar yapmaktır. Uygulamanın hızı ayrıntılı bir şekilde incelendikten sonra yığın alanları incelendikten sonra, yığında veri deseninin hala bozulmamış olduğu alanı bularak ne kadar yığının gerçekten kullanılmış olduğunu görebilir. Şekil 6'da, kapsamlı iş parçacığı yürütme 0xEFEF için önceden ayarlanmış bir yığın vardır.

> [!IMPORTANT]
> Varsayılan olarak, ThreadX SMP her bir iş parçacığı yığınının her bayta değerini 0xEF.

### <a name="memory-pitfalls"></a>Bellek Tuzakları 
İş parçacıkları için yığın gereksinimleri büyük olabilir. Bu nedenle, uygulamayı makul sayıda iş parçacığına sahip olacak şekilde tasarlamak önemlidir. Ayrıca, iş parçacıklarında aşırı yığın kullanımından kaçınmak için bazı dikkatler gerekir. Cursive algoritmalardan ve büyük yerel veri yapılarından kaçınılmalıdır.

Çoğu durumda taşan yığın, iş parçacığı yürütmenin bitişik belleği bozmasını sağlar (genellikle 

![Bellek Tuzakları](media/image9.png)

**ŞEKIL 6. 0xEFEF için Stack Ön 0xEFEF**

önce) yığma alanı. Sonuçlar tahmin edilemez ancak genellikle program sayacında doğal olmayan bir değişiklikle sonuçlanabilirsiniz. Buna genellikle "atlayanlar" denir. Elbette bunu önlemenin tek yolu tüm iş parçacığı yığınlarının yeterince büyük olduğundan emin olmaktır.

### <a name="optional-run-time-stack-checking"></a>İsteğe Bağlı Çalışma Zamanı Yığın Denetimi  
ThreadX SMP, çalışma zamanı sırasında her iş parçacığının yığınında bozulma olup oluğu denetleme olanağı sağlar. Varsayılan olarak, ThreadX SMP oluşturma sırasında iş parçacığı yığınlarının her 0xEF veri deseniyle doldurur. Uygulama ***** TX_ENABLE_STACK_CHECKING _ tanımlı ile ThreadX SMP kitaplığını derlemesi, askıya alınan veya sürdürülen her bir iş parçacığının yığınında bozulma olduğunu inceler. Yığın bozulması algılanırsa ThreadX SMP, _tx_thread_stack_error_notify* çağrısı tarafından belirtilen şekilde uygulamanın yığın hatası işleme yordamını çağıracak. Aksi takdirde, yığın hatası işleyicisi belirtilmemişse, ThreadX SMP iç hata *_tx_thread_stack_error_handler* çağıracak.

### <a name="reentrancy"></a>Yeniden giriş 
Çoklu iş parçacığının gerçek nedenlerinden biri, aynı C işlevinin birden çok iş parçacığından çağrıl olmasıdır. Bu, harika bir güç sağlar ve kod alanı azaltmaya da yardımcı olur. Ancak, birden çok iş parçacığından çağrılan C işlevlerinin yeniden *çağrılmalarını gerektirir.*

Temel olarak, bir yenidenentrant işlevi çağıranın dönüş adresini geçerli yığında depolar ve daha önce ayarlayan genel veya statik C değişkenlerine güvenmez. Çoğu derleyici, dönüş adresini yığına yer alıyor. Bu nedenle, uygulama geliştiricilerinin yalnızca genel ve statik *kullanımı konusunda* *endişelenmesi gerekir.*

Standart C kitaplığında bulunan "strtok" dize belirteci işlevi, yeniden kabul olmayan bir işleve örnektir. Bu işlev, sonraki çağrılarda önceki dize işaretçisini anımsar. Bunu statik dize işaretçisi ile yapar. Bu işlev birden çok iş parçacığından çağrılsa, büyük olasılıkla geçersiz bir işaretçisi olacaktır.

### <a name="thread-priority-pitfalls"></a>İş Parçacığı Önceliği Tuzakları 
İş parçacığı önceliklerini seçmek, çoklu iş parçacığının en önemli yönlerinden birisidir. Bazen çalışma zamanında tam olarak nelerin gerekli olduğunu belirlemek yerine iş parçacığı önemi algılanmasına dayalı olarak öncelik atamak çok cazip olabilir. İş parçacığı önceliklerinin kötüye kullanılması diğer iş parçacıklarını tüketebilir, öncelik ters çevirmesi oluşturabilir, işleme bant genişliğini azaltır ve uygulamanın çalışma zamanı davranışını anlamak zorlaştırabilirsiniz.

Daha önce belirtildiği gibi, ThreadX SMP öncelik tabanlı, ön hazırlıklı bir zamanlama algoritması sağlar. Düşük öncelikli iş parçacıkları, yürütme için hazır daha yüksek öncelikli iş parçacıklarına sahip olana kadar yürütülmez. Daha yüksek öncelikli bir iş parçacığı her zaman hazırsa, düşük öncelikli iş parçacıkları hiçbir zaman yürütülmez. Bu koşul, iş *parçacığını açma olarak adlandırılan bir durumdur.*

Çoğu iş parçacığı açma sorunu, hata ayıklamanın erken bir zamanlarında algılanır ve yüksek öncelikli iş parçacıklarının sürekli olarak yürütülmeyebileceğini sağlayarak çözülebilir. Alternatif olarak, yürütme şansı alınana kadar, mantıksal olarak yürütülen iş parçacıklarının önceliğini kademeli olarak başlatan uygulamaya de bir mantık eklenebilir.

İş parçacığı öncelikleriyle ilişkili başka bir *giriş ise öncelikli bir sürümdür*. Düşük öncelikli bir iş parçacığında gerekli bir kaynak olduğundan, yüksek öncelikli bir iş parçacığı askıya alındığında öncelik Inversion gerçekleşir. Kuşkusuz, bazı örneklerde, farklı öncelikteki iki iş parçacığının ortak bir kaynağı paylaşması gerekir. Bu iş parçacıkları etkin tek bir sürümse, öncelik Inversion saati, düşük öncelikli iş parçacığı kaynağı tutan zamana göre sınırlanır. Bu koşul hem belirleyici hem de oldukça normaldir. Bununla birlikte, bu öncelik geçersiz kılma sırasında ara öncelikteki iş parçacıkları etkin hale gelirse, öncelik Inversion süresi artık belirleyici değildir ve bir uygulama hatasına neden olabilir.

ThreadX SMP ' de belirleyici olmayan öncelikli öncelikli sürümü önlemek için önemli ölçüde üç farklı yöntem vardır. İlk olarak, uygulama önceliği seçimleri ve çalışma zamanı davranışı, öncelik sürümü sorununun önlenebilmesini sağlayacak şekilde tasarlanabilir. İkincisi, daha yüksek öncelikli iş parçacıklarıyla kaynakları paylaştıklarında, daha düşük öncelikli iş parçacıkları *önalım-Threshold* ' ı kullanarak ara iş parçacıklarından önalım engelleyebilir. Son olarak, sistem kaynaklarını korumak için ThreadX SMP mutex nesnelerini kullanan iş parçacıkları, belirleyici olmayan öncelikli bir sürümü ortadan kaldırmak için isteğe bağlı mutex *önceliği devrmasından* yararlanabilir.

### <a name="priority-overhead"></a>Öncelik ek yükü 
Çoklu iş parçacığı içindeki ek yükü azaltmanın en fazla belirgin yolu, bağlam anahtarlarının sayısını azaltmaktır. Daha önce belirtildiği gibi, daha yüksek öncelikli bir iş parçacığının yürütülmesi yürütülen iş parçacığının üzerinde daha kırmızıysa bir bağlam anahtarı oluşur. Yüksek öncelikli iş parçacıklarının, hem dış olayların (kesmeler gibi) hem de yürütülen iş parçacığı tarafından yapılan hizmet çağrılarının bir sonucu olarak hazırlanabileceğini bahsetmek çok önemlidir.

Efekt iş parçacığı önceliklerinin bağlam anahtarı ek yükü üzerinde olduğunu göstermek için, *thread_1*, *thread_2* ve *thread_3* adlı iş parçacıklarından oluşan üç iş parçacığı ortamı olduğunu varsayalım. Tüm iş parçacıklarının bir ileti bekleyen askıya alınma durumunda olduğunu varsayalım. Thread_1 bir ileti aldığında, bunu hemen thread_2 gönderir. Thread_2 sonra iletiyi thread_3 iletir. Thread_3 yalnızca iletiyi atar. Her iş parçacığı iletisini tamamladıktan sonra, geri döner ve başka bir ileti bekler.

Bu üç iş parçacığını yürütmek için gereken işlem önceliklerinden büyük ölçüde farklılık gösterir. Tüm iş parçacıkları aynı önceliğe sahip ise, her iş parçacığının yürütülmesinden önce tek bir bağlam anahtarı oluşur. Bağlam anahtarı, her iş parçacığı boş bir ileti kuyruğu üzerinde askıya aldığında oluşur.

Ancak, thread_2 thread_1 kıyasla daha yüksek önceliktir ve thread_3 thread_2 kıyasla daha yüksek önceliktir, bağlam anahtarlarının sayısı iki katına çıkar. Bunun nedeni, daha yüksek öncelikli bir iş parçacığının artık hazır olduğunu algıladığında *tx_queue_send* hizmetinin içinde başka bir bağlam anahtarının gerçekleşmesinden kaynaklanır.

ThreadX SMP önalım-Threshold mekanizması, bu ek bağlam anahtarlarından kaçınabilir ve yine de yukarıda bahsedilen öncelik seçimlerine izin verebilir. Zamanlama sırasında birkaç iş parçacığı önceliklerinin sağladığından bu önemli bir özelliktir, ancak aynı zamanda iş parçacığı yürütme sırasında aralarında bazı istenmeyen bağlamla geçiş yapmayı ortadan kaldırır.

### <a name="run-time-thread-performance-information"></a>Çalışma zamanı Iş parçacığı performans bilgileri 
ThreadX SMP isteğe bağlı çalışma zamanı iş parçacığı performans bilgilerini sağlar. ThreadX SMP kitaplığı ve uygulaması tanımlanmış ***TX_THREAD_ENABLE_PERFORMANCE_INFO*** ile derlenip, threadx SMP aşağıdaki bilgileri biriktirir:

Genel sistem için toplam sayı:

- iş parçacığı bağlantının sürdürülmesi
- iş parçacığı getirilmesi
- hizmet çağrısı preemptions
- kesme preemptions
- öncelikli Inversions 'ları
- zaman dilimleri
- relinquishes
- iş parçacığı zaman aşımları
- askıya alma iptal edilecek
- Boştaki sistem geri dönüşler
- boşta olmayan sistem dönüşleri

Her iş parçacığının toplam sayısı:

- bağlantının sürdürülmesi
- getirilmesi
- hizmet çağrısı preemptions
- kesme preemptions
- öncelikli Inversions 'ları
- zaman dilimleri
- iş parçacığı relinkler
- iş parçacığı zaman aşımları
- askıya alma iptal edilecek

Bu bilgiler, Hizmetler *tx_thread_performance_info_get* ve *tx_thread_performance_system_info_get* aracılığıyla çalışma zamanında kullanılabilir. İş parçacığı performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda hizmet çağrısı preemptions iş parçacığının önceliğini önerebilir ve/veya önalım eşiği çok düşüktür. Ayrıca, görece düşük sayıda boşta sistem döndürmesi, daha düşük öncelikli iş parçacıklarının yeterince askıya alınması önerisinde bulunabilir.

### <a name="debugging-pitfalls"></a>Hata ayıklama sınırları 
Birden çok iş parçacığından aynı program kodu yürütülemediğinden çok iş parçacıklı uygulamalarda hata ayıklama biraz daha zordur. Böyle durumlarda, bir kesme noktası tek başına yeterli olmayabilir. Hata ayıklayıcı, çağıran iş parçacığının hata ayıklaması için bir tane olup olmadığını görmek üzere bir koşullu kesme noktası kullanarak geçerli iş parçacığı işaretçisi dizisi _tx_thread_current_ptr de ( ***çekirdek]*** görüntülemesi gerekir.

Bunun çoğu, çeşitli geliştirme aracı satıcıları aracılığıyla sunulan çoklu iş parçacıklı destek paketlerinde işlenir. Basit tasarımı nedeniyle, ThreadX SMP 'yi farklı geliştirme araçlarıyla tümleştirmek oldukça kolaydır.

Yığın boyutu her zaman çoklu iş parçacığı oluşturma konusunun önemli bir hata ayıklama konusu. Açıklanamayan davranış gözlemlendiğinde, genellikle her iş parçacığı için yığın boyutlarını artırmak iyi bir ilk tahmindir; özellikle de son iş parçacığının yığın boyutu.

> [!IMPORTANT]
> Ayrıca, TX_ENABLE_STACK_CHECKING tanımlı olan ThreadX SMP kitaplığını oluşturmak iyi bir fikirdir. Bu, yığın bozulma sorunlarını işleme sırasında olabildiğince erken ayırmaya yardımcı olur!

## <a name="message-queues"></a>İleti kuyrukları

İleti kuyrukları, ThreadX SMP içindeki ınterthread iletişiminin birincil yöntemidir. Bir veya daha fazla ileti bir ileti kuyruğunda bulunabilir. Tek bir iletiyi tutan bir ileti kuyruğu genellikle *posta kutusu* olarak adlandırılır.

Mesajlar *tx_queue_send* tarafından kuyruğa kopyalanır ve *tx_queue_receive* bir kuyruktan kopyalanır. Bunun tek istisnası, boş bir kuyruktaki bir ileti beklenirken bir iş parçacığının askıya alındığı durumdur. Bu durumda, sıraya gönderilen sonraki ileti, iş parçacığının hedef alanına doğrudan yerleştirilir.

Her ileti kuyruğu ortak bir kaynaktır. ThreadX SMP, ileti sıralarının nasıl kullanıldığına ilişkin bir kısıtlama vermez.

### <a name="creating-message-queues"></a>Ileti kuyrukları oluşturma 
İleti kuyrukları, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Bir uygulamadaki ileti kuyruğu sayısı için bir sınır yoktur. 

### <a name="message-size"></a>İleti boyutu 
Her ileti kuyruğu, birkaç sabit boyutlu iletiyi destekler. Kullanılabilir ileti boyutları, dahil olmak üzere 1 ile 16 32 bitlik sözcüklerdir. İleti boyutu, sıra oluşturulduğunda belirtilir. 

16 sözcükten daha büyük uygulama iletilerinin işaretçiden geçirilmesi gerekir. Bu, 1 sözcük boyutuna sahip bir sıra (bir işaretçiyi tutmak için yeterli) ve ardından ileti işaretçilerini tüm ileti yerine gönderip alarak gerçekleştirilir.

### <a name="message-queue-capacity"></a>İleti sırası kapasitesi 
Bir kuyruğun tutabilecek ileti sayısı, ileti boyutunun bir işlevidir ve oluşturma sırasında sağlanan bellek alanının boyutudur. Kuyruğun toplam ileti kapasitesi, her iletideki bayt sayısı, sağlanan bellek alanındaki toplam bayt sayısına bölünerek hesaplanır.

Örneğin, 100 baytlık bir bellek alanı ile 1 32 bitlik bir sözcüğün (4 bayt) ileti boyutunu destekleyen bir ileti kuyruğu oluşturulduysa, kapasitesi 25 mesaj olur.

### <a name="queue-memory-area"></a>Kuyruk belleği alanı 
Daha önce belirtildiği gibi, ileti arabelleğe alma bellek alanı sıra oluşturma sırasında belirtilir. ThreadX SMP içindeki diğer bellek alanları gibi, hedefin adres alanında herhangi bir yerde bulunabilir.

Bu önemli bir özelliktir çünkü uygulamanın önemli ölçüde esnekliğini sağlar. Örneğin, bir uygulama performansı artırmak için yüksek hızda RAM 'teki önemli bir kuyruğun bellek alanını bulabilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma  
Bir kuyruktan ileti gönderilmeye ya da almaya çalışırken uygulama iş parçacıkları askıya alabilir. Genellikle, iş parçacığı askıya alma, boş bir kuyruktan ileti bekletmeyi içerir. Ancak, bir iş parçacığının bir iletiyi tam sıraya gönderme girişimi de askıya alınması mümkündür. 

Askıya alma koşulu çözümlendikten sonra, istenen hizmet tamamlanır ve bekleyen iş parçacığı sürdürülür. Aynı kuyrukta birden çok iş parçacığı askıya alınırsa, bunlar askıya alındıklarına (FIFO) göre devam eder.

Ancak, uygulama iş parçacığının askıya alınmasına neden ***olan kuyruk tx_queue_prioritize*** önce çağrılsa öncelik verme de mümkündür. Kuyruk önceliklerini belirleme hizmeti, askıya alma listesinin önüne en yüksek öncelikli iş parçacığını, diğer tüm askıya alınmış iş parçacıklarını aynı FIFO sırasına bırakarak yer alıyor.

Zaman zaman zaman zaman tüm kuyruk askıya almaları için de kullanılabilir. Temel olarak, bir zaman out iş parçacığının askıya alınmayacak en fazla zamanlayıcı saat sayısı belirtir. Bir zaman out oluşursa, iş parçacığı sürdürür ve hizmet uygun hata kodu ile döndürür.

### <a name="queue-send-notification"></a>Kuyruk Gönderme Bildirimi  
Bazı uygulamalar, kuyruğa ileti yerleştirilemeyen durumlarda bunun bildirilma avantajına sahip olduğunu bulabilir. ThreadX SMP, bu özelliği tx_queue_send_notify *sağlar.* Bu hizmet, sağlanan uygulama bildirimi işlevini belirtilen kuyruğa kaydettirmektedir. ThreadX SMP daha sonra kuyruğa her ileti gönderilmesi sırasında bu uygulama bildirim işlevini çağırır. Uygulama bildirim işlevi içindeki tam işlem uygulama tarafından belirlenir; ancak, genellikle yeni iletiyi işlemeye uygun iş parçacığını devamdan oluşur.

### <a name="queue-event-chaining"></a>Kuyruk Olay zinciri™  
ThreadX SMP'de bildirim özellikleri, çeşitli eşitleme olaylarını zincirleme için kullanılabilir. Bu genellikle tek bir iş parçacığının birden çok eşitleme olaylarını işlemesi gereken durumlarda kullanışlıdır.

Örneğin, tek bir iş parçacığının beş farklı kuyruktan iletileri işlemeden sorumlu olduğunu ve hiçbir ileti kullanılabilir olduğunda da askıya alınması gerektiğini varsayalım. Bu, her kuyruk için bir uygulama bildirimi işlevi kaydederek ve ek bir sayma semaforu ile kolayca gerçekleştirebilirsiniz. Özellikle, uygulama bildirimi işlevi çağrıldı *tx_semaphore_put* bir hata gerçekleştirir (semafor sayısı beş kuyrukta da toplam ileti sayısını temsil eder). İşleme iş parçacığı, bu semaforda tx_semaphore_get *askıya* alır. Semafor kullanılabilir olduğunda (bu durumda, bir ileti olduğunda!), işleme iş parçacığı devam eder. Ardından bir ileti için her kuyruğu sorgular, bulunan iletiyi işler ve sonraki *iletiyi tx_semaphore_get* başka bir ileti gerçekleştirir. Bunu olay zincirleme olmadan gerçekleştirmek oldukça zordur ve büyük olasılıkla daha fazla iş parçacığı ve/veya ek uygulama kodu gerektirir.

Genel olarak, *olay zinciri daha az iş* parçacığına, daha az ek yüke ve daha küçük RAM gereksinimlerine neden olur. Ayrıca, daha karmaşık sistemlerin eşitleme gereksinimlerini işlemek için son derece esnek bir mekanizma sağlar.

### <a name="run-time-queue-performance-information"></a>Çalışma Zamanı Kuyruğu Performans Bilgileri  
ThreadX SMP, isteğe bağlı çalışma zamanı kuyruk performansı bilgileri sağlar. ThreadX SMP kitaplığı ve uygulaması  tanımlı TX_QUEUE_ENABLE_PERFORMANCE_INFO, ThreadX SMP aşağıdaki bilgileri birikiyor:

Genel sistemin toplam sayısı:

- gönderilen iletiler
- alınan iletiler
- kuyruk boş askıya almalar
- kuyruk tam askıya almaları
- kuyruk tam hatası döndüren (askıya alma değil speci-fied)
- kuyruk zaman aşımı

Her kuyruk için toplam sayı:

- gönderilen iletiler
- alınan iletiler
- kuyruk boş askıya almalar
- kuyruk tam askıya almaları
- kuyruk tam hatası döndüren (askıya alma değil speci-fied)
- kuyruk zaman aşımı

Bu bilgiler, çalışma zamanında tx_queue_performance_info_get ve *tx_queue_performance_system_info_get.*  Kuyruk performansı bilgileri, uygulamanın düzgün bir şekilde performans gösterip sergilene olmadığını belirlemek için yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, görece yüksek sayıda "kuyrukta tam askıya alma" kuyruğun boyutunun artması yararlı olabilir.

### <a name="queue-control-block-tx_queue"></a>Kuyruk Denetim Bloğu TX_QUEUE 
Her ileti kuyruğun özellikleri denetim bloğunda bulunur. Kuyrukta ileti sayısı gibi ilginç bilgiler içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

İleti kuyruğu denetim blokları bellekte herhangi bir yerde de yer alır, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi.

### <a name="message-destination-pitfall"></a>İleti Hedefi Tuzakları  
Daha önce belirtildiği gibi iletiler kuyruk alanı ve uygulama veri alanları arasında kopyalanır. Alınan iletinin hedefinin, iletinin tamamını tutacak kadar büyük olduğundan emin olmak önemlidir. Yoksa, ileti hedeflerini takip eden bellek büyük olasılıkla bozuk olur. 

> [!WARNING]
> Bu özellikle yığında çok küçük bir ileti hedefi olduğunda çok lethal olur; bir işlevin dönüş adresini bozmak gibi bir şey yoktur!

## <a name="counting-semaphores"></a>Semaforları Sayma

ThreadX SMP, 0 ile 4.294.967.295 arasında bir değer aralığındaki 32 bit sayma semaforları sağlar. Semaforları saymak için iki işlem vardır: *tx_semaphore_get* ve *tx_semaphore_put.* Get işlemi semaforu bir azaltıyor. Semafor 0 ise, get işlemi başarılı olmaz. Get işlemi, put işlemidir. Semaforu bir artırır.

Her sayma semaforu genel bir kaynaktır. ThreadX SMP, semaforların sayma ile ilgili bir kısıtlamaya neden olmaz.

Sayma semaforları genellikle karşılıklı *dışlama için kullanılır.* Ancak sayma semaforları olay bildirimi için bir yöntem olarak da kullanılabilir.

### <a name="mutual-exclusion"></a>Karşılıklı Dışlama 
Karşılıklı dışlama, iş parçacıklarının belirli uygulama alanlarına (kritik bölümler veya uygulama kaynakları *olarak* da adlandırılan) erişimini *denetlemeyle ilgilidir.* Karşılıklı dışlama için kullanılan semaforların "geçerli sayısı", erişime izin verilen toplam iş parçacığı sayısını temsil eder. Çoğu durumda, karşılıklı dışlama için kullanılan semaforların sayma değeri 1 olur; başka bir ifadeyle aynı anda ilişkili kaynağa yalnızca bir iş parçacığı erişebilirsiniz. Yalnızca 0 veya 1 değerlerine sahip olan semaforları sayma yaygın olarak ikili *semaforlar olarak ifade eder.*

> [!IMPORTANT]
> İkili semafor kullanılıyorsa, kullanıcı aynı iş parçacığının sahip olduğu bir semafor üzerinde bir get işlemi gerçekleştirmesini engellemesi gerekir. İkinci bir alma başarısız olur ve çağıran iş parçacığının süresiz askıya alınmasına ve kaynağın kalıcı olarak kullanılamamasına neden olabilir.

### <a name="event-notification"></a>Olay Bildirimi 
Sayma semaforlarını olay bildirimi olarak üretici-tüketici olarak da kullanabilirsiniz. Tüketici, bir şey kullanılabilir olduğunda semaforu artırırken sayma semaforu almaya çalışır. Bu tür semaforlar genellikle başlangıç değeri 0'dır ve üretici tüketici için hazır bir şeye sahip olana kadar artmaz. Olay bildirimi için kullanılan semaforlar, hizmet çağrısının tx_semaphore_ceiling_put *yararlanabilir.* Bu hizmet, semafor sayımının çağrıda sağlanan değeri hiçbir zaman aşmasını sağlar.

### <a name="creating-counting-semaphores"></a>Sayma Semaforları Oluşturma 
Sayma semaforları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Semaforların ilk sayısı oluşturma sırasında belirtilir. Bir uygulamada semafor sayma sayısına bir sınır yoktur. 

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma  
Uygulama iş parçacıkları, geçerli sayı 0 olan bir semafor üzerinde alma işlemi gerçekleştirmeye çalışırken askıya alabilir. 

Bir koyma işlemi gerçekleştirildikten sonra, askıya alınan iş parçacığının get işlemi gerçekleştirilir ve iş parçacığı devam eder. Aynı sayma semaforu üzerinde birden çok iş parçacığı askıya alınırsa, bunlar askıya alındıklarına (FIFO) aynı sırayla devam eder.

Ancak, uygulama iş parçacığının askıya alınmasını kaldıran semafor ***koyma çağrısından tx_semaphore_prioritize*** çağrısından önce çağrılsa da öncelik verme mümkündür. Semafor öncelik belirleme hizmeti, askıya alma listesinin önüne en yüksek öncelikli iş parçacığını, diğer tüm askıya alınmış iş parçacıklarını aynı FIFO sırasına göre bırakarak yer alıyor.

### <a name="semaphore-put-notification"></a>Semaphore Put Bildirimi 
Bazı uygulamalar, semafor konan durumlarda bu durumu bildirmiş olabilir. ThreadX SMP, bu özelliği tx_semaphore_put_notify *sağlar.* Bu hizmet, sağlanan uygulama bildirimi işlevini belirtilen semafora kaydedmektedir. ThreadX SMP daha sonra semafor her ekinde bu uygulama bildirim işlevini çağırır. Uygulama bildirim işlevi içindeki tam işlem uygulama tarafından belirlenir; ancak, genellikle yeni semafor koyma olayı iş için uygun iş parçacığını devamdan oluşur.

### <a name="semaphore-eventchaining"></a>Semaphore OlayChaining™ 
ThreadX SMP'de bildirim özellikleri, çeşitli eşitleme olaylarını zincirleme için kullanılabilir. Bu genellikle tek bir iş parçacığının birden çok eşitleme olaylarını işlemesi gereken durumlarda kullanışlıdır.

Örneğin, bir kuyruk iletisi, olay bayrakları ve semafor için ayrı iş parçacıklarının askıya alınması yerine, uygulama her nesne için bir bildirim yordamını kaydedebilir. Çağrıldığında, uygulama bildirim yordamı tek bir iş parçacığını sürdürebilir ve bu da yeni olayı bulmak ve işlemek için her nesneyi sorgular.

Genel olarak, *olay zincirleme* daha az iş parçacığı, daha az ek yük ve daha küçük RAM gereksinimlerine neden olur. Ayrıca, daha karmaşık sistemlerin eşitleme gereksinimlerini işlemek için yüksek düzeyde esnek bir mekanizma sağlar.

### <a name="run-time-semaphore-performance-information"></a>Çalışma zamanı semaforu performans bilgileri 
ThreadX SMP isteğe bağlı çalışma zamanı semaforu performans bilgilerini sağlar. ThreadX SMP kitaplığı ve uygulaması tanımlanmış ***TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO*** ile derlenip, threadx SMP aşağıdaki bilgileri biriktirir. 

Genel sistem için toplam sayı:

- semafor koyar
- semafor alır
- semafor Get getirilmesi
- Semafor zaman aşımlarını al

Her semaforun toplam sayısı:

- semafor koyar
- semafor alır
- semafor Get getirilmesi
- Semafor zaman aşımlarını al

Bu bilgiler, Hizmetler *tx_semaphore_performance_info_get* ve *tx_semaphore_performance_system_info_get* aracılığıyla çalışma zamanında kullanılabilir. Semafor performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda "semafor Get zaman aşımları", diğer iş parçacıklarının kaynakları çok uzun süre olarak tuttuklarından kaynaklanabilir.

### <a name="semaphore-control-block-tx_semaphore"></a>Semafor denetim bloğu TX_SEMAPHORE 
Her sayım semaforun özellikleri denetim bloğunda bulunur. Geçerli semafor sayısı gibi bilgileri içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır. 

Semafor denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır. 

### <a name="deadly-embrace"></a>Dar küme 
Karşılıklı dışlama için kullanılan semaforlarla ilişkili en ilgi çekici ve tehlikeli her bir tane, büyük *küme ayracı* olur. , *Bir veya daha* fazla iş parçacığının, birbirini zaten sahip olan Semaforlar alınmaya çalışılırken süresiz olarak askıya alındığı bir durumdur.

Bu koşul en iyi iki iş parçacığı, iki semafor örneği tarafından gösterilmiştir. İlk iş parçacığının ilk semafora sahip olduğunu ve ikinci iş parçacığının ikinci semafora sahip olduğunu varsayalım. İlk iş parçacığı ikinci semaforu almayı denerse ve ikinci iş parçacığı ilk semaforu almaya çalışırsa, her iki iş parçacığı de bir kilitlenme koşulu girer. Ayrıca, bu iş parçacıkları sonsuza kadar askıya alınırsa, ilişkili kaynakları da süresiz olarak kilitlenir. Şekil 78 sayfasında Bu örnek gösterilmektedir.

![Dar küme](media/image10.png)

**ŞEKIL 7. Askıya alınan Iş parçacıkları örneği**

Gerçek zamanlı sistemler için, iş parçacıklarının Semaforlar tarafından nasıl elde edileceği hakkında bazı kısıtlamalar yerleştirilerek, kilitlenmeleri engellenebilir. İş parçacıkları tek seferde yalnızca bir semafora sahip olabilir. Alternatif olarak, iş parçacıkları bunları aynı sırada topladıklarında birden fazla semafora sahip olabilir. Önceki örnekte, ilk ve ikinci semaforu sırayla ilk ve ikinci semaforu elde alıyorsa, bu, geçersiz ayraç engellenir.

> [!IMPORTANT]
> Ayrıca, bir küme ayracından kurtarmak üzere alma işlemiyle ilişkili askıya alma zaman aşımını kullanmak da mümkündür.

### <a name="priority-inversion"></a>Öncelikli Inversion 
Karşılıklı dışlama semaforları ile ilişkili başka bir giriş de öncelikli bir sürümdür. Bu konu, sayfa 64 ' de "Iş parçacığı önceliği önem derecesi" içinde daha ayrıntılı olarak ele alınmıştır.

Temel sorun, düşük öncelikli bir iş parçacığının daha yüksek öncelikli iş parçacığı gerektiren bir semafora sahip olduğu bir durumdan kaynaklanır. Bu, normal bir. Bununla birlikte, aralarında önceliklere sahip olan iş parçacıkları öncelik inen son kararlı olmayan bir süreye neden olabilir. Bu, iş parçacığı önceliklerinin dikkatli bir şekilde seçilebileceği, önalım-Threshold kullanılarak işlenebilir ve kaynağın sahibi olan iş parçacığının önceliği yüksek öncelikli iş parçacığından daha geçici olarak oluşturulur.

## <a name="mutexes"></a>Zaman Uyumu Sağlayıcılar

Semafora ek olarak, ThreadX SMP Ayrıca bir mutex nesnesi de sağlar. Bir mutex, temelde bir iş parçacığının tek seferde bir mutex 'e sahip olabileceği anlamına gelen bir ikili semafor olur. Ayrıca, aynı iş parçacığı, sahip olunan bir mutex üzerinde başarılı bir mutex Get işlemini birden çok kez gerçekleştirebilir, 4.294.967.295 tam olarak olur. Mutex nesnesinde iki işlem vardır: ***tx_mutex_get** _ ve _ *_tx_mutex_put_* *. Get işlemi, başka bir iş parçacığına ait bulunmayan bir mutex edinir, PUT işlemi daha önce edinilen bir mutex 'i serbest bırakır. Bir mutex 'i serbest bırakmak için bir iş parçacığında, put işlemlerinin sayısı önceki Get işlemlerinin sayısına eşit olmalıdır.

Her Mutex ortak bir kaynaktır. ThreadX SMP, zaman uyumu kapsamalar üzerinde bir kısıtlama yoktur.

ThreadX *mukapsamalarla yalnızca karşılıklı dışlama* için kullanılır. Sayma semaforlarından farklı olarak, zaman uyumu sağlayıcılar olay bildirimi için bir yöntem olarak kullanılamaz.

### <a name="mutex-mutual-exclusion"></a>Mutex karşılıklı dışlaması 
Sayım semaforu bölümündeki tartışmaya benzer şekilde, karşılıklı dışlama, iş parçacıklarının belirli uygulama bölgelerine erişimini denetlemeyle ( *kritik bölümler* veya *uygulama kaynakları* olarak da bilinir) ilgilidir. Kullanılabilir olduğunda, bir ThreadX SMP mutex 'in sahiplik sayısı 0 olur. Mutex bir iş parçacığı tarafından alındıktan sonra, mutex üzerinde gerçekleştirilen başarılı alma işlemleri için bir kez, her başarılı Put işlemi için azaltılır.

### <a name="creating-mutexes"></a>Birbirini kapsamayan oluşturma 
ThreadX SMP zaman uyumu sağlayıcılar, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma sırasında oluşturulur. Bir mutex 'in ilk koşulu her zaman "kullanılabilir" dır. Ayrıca, *Öncelik devralma* seçili olarak bir mutex oluşturulabilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma 
Uygulama iş parçacıkları, zaten başka bir iş parçacığına ait olan bir mutex üzerinde alma işlemi gerçekleştirmeye çalışırken askıya alabilir.

Sahip iş parçacığı tarafından aynı sayıda Put işlemi gerçekleştirildikten sonra, askıya alınan iş parçacığının alma işlemi gerçekleştirilir, bu da mutex 'in sahipliğini verir ve iş parçacığı sürdürülür. Aynı mutex üzerinde birden fazla iş parçacığı askıya alınırsa, bunlar askıya alındığı sırada sürdürülür (FıFO).

Ancak, bir öncelik sürdürme, oluşturma sırasında mutex önceliği devralımı seçildiyse otomatik olarak yapılır. Uygulama, iş parçacığı askıya alma çağrısını askıya alan mutex put çağrısından önce ***tx_mutex_prioritize*** çağırdığında öncelik sürdürme de mümkündür. Mutex öncelik sıralaması hizmeti, en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar, diğer tüm askıya alınan iş parçacıklarını aynı FıFO sırasıyla bırakır.

### <a name="run-time-mutex-performance-information"></a>Çalışma zamanı mutex performans bilgileri 
ThreadX SMP isteğe bağlı çalışma zamanı mutex performans bilgilerini sağlar. ThreadX SMP kitaplığı ve uygulaması tanımlanmış ***TX_MUTEX_ENABLE_PERFORMANCE_INFO*** ile derlenip, threadx SMP aşağıdaki bilgileri biriktirir.

Genel sistem için toplam sayı:

- mutex koyar
- Mutex zaman alır
- mutex Get getirilmesi
- Mutex zaman aşımlarını al
- mutex öncelik Inversions 'ları
- mutex öncelik Inheritances

Her bir mutex için toplam sayı:

- mutex koyar
- Mutex zaman alır
- mutex Get getirilmesi
- Mutex zaman aşımlarını al
- mutex öncelik Inversions 'ları
- mutex öncelik Inheritances

Bu bilgiler, Hizmetler *tx_mutex_performance_info_get* ve *tx_mutex_performance_system_info_get* aracılığıyla çalışma zamanında kullanılabilir. Mutex performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda "mutex Get zaman aşımları", diğer iş parçacıklarının kaynakları çok uzun tuttuklarından kaynaklanabilir.

### <a name="mutex-control-block-tx_mutex"></a>Mutex denetim bloğu TX_MUTEX 
Her bir mutex 'in özellikleri denetim bloğunda bulunur. Mutex sahibi olan iş parçacığının işaretçisi ile birlikte geçerli mutex sahiplik sayısı gibi bilgileri içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

Mutex denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

### <a name="deadly-embrace"></a>Dar küme  
Mutex sahipliğiyle ilişkili en ilgi çekici ve tehlikeli her bir tane, büyük *küme ayracı* olur. Bir kucaklama ya da *çıkmaz,* diğer iş parçacıklarının sahip olduğu bir mutex'i almaya çalışırken iki veya daha fazla iş parçacığının süresiz olarak askıya alınarak askıya alınan bir koşuldur. Benimseme *tartışmaları ve* 77. sayfada bulunan çözümleri, mutex nesnesi için de tamamen geçerlidir.

### <a name="priority-inversion"></a>Öncelik Ters Çevirme 
Daha önce belirtildiği gibi, karşılıklı dışlama ile ilişkili önemli bir tuzak öncelik ters çevirmedir. Bu konu, 64. sayfada yer alan "İş Parçacığı Önceliği Tuzakları" başlığında daha tam olarak ele alınmıştır. 

Temel sorun, daha düşük öncelikli bir iş parçacığının daha yüksek öncelikli bir iş parçacığına gereken semafora sahip olduğu bir durumdan sonuç verir. Bu kendi içinde normaldir. Ancak, aralarında öncelikleri olan iş parçacıkları, öncelik ters çevirmenin belirsiz bir süreye kadar devam esnettiğine neden olabilir. Daha önce tartışılan semaforların aksine, ThreadX SMP mutex nesnesinin isteğe bağlı öncelik *devralması vardır.* Öncelik devralmanın ardındaki temel fikir, düşük öncelikli bir iş parçacığının önceliğini geçici olarak, aynı mutex'in düşük öncelikli iş parçacığına ait olması gereken yüksek öncelikli iş parçacığının önceliğe yükseltmiş olmasıdır. Düşük öncelikli iş parçacığı mutex'i serbest bıraksa, özgün önceliği geri yüklenir ve yüksek öncelikli iş parçacığına mutex sahipliği verilir. Bu özellik, ters çevirme miktarını düşük öncelikli iş parçacığının mutex'i tutarken sınırlaarak belirlenemeyen öncelik ters çevirmeyi ortadan kaldırıyor. Elbette, bu bölümün önceki kısımlarında tartışılan ve belirlenimci olmayan öncelik ters çevirmeyi işlemek için kullanılan teknikler de mutex'lerde geçerlidir.

## <a name="event-flags"></a>Olay Bayrakları

Olay bayrakları, iş parçacığı eşitleme için güçlü bir araç sağlar. Her olay bayrağı tek bir bitle temsil edildi. Olay bayrakları 32 grup halinde düzenlenmiştir.

İş parçacıkları bir gruptaki 32 olay bayrağının hepsinde aynı anda çalışır. Olaylar, *tx_event_flags_set* tarafından ayarlanır ve tarafından *tx_event_flags_get.*

Olay bayraklarını ayarlama, geçerli olay bayrakları ile yeni olay bayrakları arasında mantıksal bir AND/OR işlemiyle yapılır. Mantıksal işlem türü (AND veya OR) çağrıda tx_event_flags_set *belirtilir.*

Olay bayraklarının alınması için benzer mantıksal seçenekler vardır. Bir get isteği, belirtilen tüm olay bayraklarının gerekli olduğunu (mantıksal AND) belirtebiliyor. Alternatif olarak, bir get isteği belirtilen olay bayraklarının herhangi biri isteği (mantıksal VEYA) karşılar. Olay bayraklarını alma işlemiyle ilişkili mantıksal işlem türü, tx_event_flags_get *belirtilir.*

> [!IMPORTANT]
> Bir get isteğini karşılayan olay bayrakları, istek tarafından belirtilirse TX_OR_CLEAR veya  **TX_AND_CLEAR** olarak ayarlanır.

Her olay bayrak grubu genel bir kaynaktır. ThreadX SMP, olay bayraklarının nasıl kullanıldıklarıyla ilgili hiçbir kısıtlamaya neden olmaz.

### <a name="creating-event-flags-groups"></a>Olay Bayrakları Grupları Oluşturma
Olay bayrakları grupları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Oluşturma sırasında, gruptaki tüm olay bayrakları sıfır olarak ayarlanır. Bir uygulamanın olay bayraklarının sayısıyla ilgili bir sınır yoktur.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma 
Uygulama iş parçacıkları, bir gruptan herhangi bir mantıksal olay bayrağı birleşimini almaya çalışırken askıya alabilir. Bir olay bayrağı ayarlandıktan sonra, askıya alınan tüm iş parçacıklarının alma istekleri gözden geçirildi. Artık gerekli olay bayraklarına sahip olan tüm iş parçacıkları devam eder.

> [!IMPORTANT]
> Bir olay bayrakları grubunda askıya alınan tüm iş parçacıkları, olay bayrakları ayarlandıklarına göre gözden geçirildi. Elbette bu ek yük getirir. Bu nedenle, aynı olay bayrakları grubunu kullanarak iş parçacığı sayısını makul bir sayıyla sınırlamak iyi bir uygulamadır.

### <a name="event-flags-set-notification"></a>Olay Bayrakları Bildirim Kümesi 
Bazı uygulamalar, bir olay bayrağı her ayar olduğunda bunun bildirilecek bir avantaj olduğunu bulabilir. ThreadX SMP, bu özelliği tx_event_flags_set_notify *sağlar.* Bu hizmet, sağlanan uygulama bildirim işlevini belirtilen olay bayrakları grubuna kaydediyor. ThreadX SMP daha sonra grupta bir olay bayrağı ayarlandığında bu uygulama bildirim işlevini çağırır. Uygulama bildirim işlevi içindeki tam işlem uygulama tarafından belirlenir, ancak genellikle yeni olay bayrağını işlemeye uygun iş parçacığını devamdan oluşur. 

### <a name="event-flags-event-chaining"></a>Olay Bayrakları Olay zinciri™ 
ThreadX SMP'de bildirim özellikleri, çeşitli eşitleme olaylarını birlikte "zincirleme" yapmak için kullanılabilir. Bu genellikle tek bir iş parçacığının birden çok eşitleme olaylarını işlemesi gereken durumlarda kullanışlıdır. 

Örneğin, bir kuyruk iletisi, olay bayrakları ve semafor için ayrı iş parçacıklarının askıya alınması yerine, uygulama her nesne için bir bildirim yordamını kaydedebilir. Çağrıldığında, uygulama bildirim yordamı tek bir iş parçacığını sürdürebilir ve bu da yeni olayı bulmak ve işlemek için her nesneyi sorgular. 

Genel olarak, *olay zinciri daha az iş* parçacığına, daha az ek yüke ve daha küçük RAM gereksinimlerine neden olur. Ayrıca, daha karmaşık sistemlerin eşitleme gereksinimlerini işlemek için son derece esnek bir mekanizma sağlar. 

### <a name="run-time-event-flags-performance-information"></a>Çalışma Zamanı Olay Bayrakları Performans Bilgileri 
ThreadX SMP, isteğe bağlı çalışma zamanı olay bayrakları performans bilgileri sağlar. ThreadX SMP kitaplığı ve uygulaması tanımlı bir ***TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO,*** ThreadX SMP aşağıdaki bilgileri birikmektedir.

Genel sistemin toplam sayısı:

- olay bayrakları kümeleri
- olay bayrakları
- olay bayrakları askıya alındı
- olay bayrakları zaman aşımına neden olur

Her olay bayrak grubu için toplam sayı:

- olay bayrakları kümeleri
- olay bayrakları
- olay bayrakları askıya alındı
- olay bayrakları zaman aşımına neden olur

Bu bilgiler, çalışma zamanında, tx_event_flags_performance_info_get *ve tx_event_flags_performance_system_info_get.*  Event Flags performans bilgileri, uygulamanın düzgün bir şekilde performans gösterip sergilene olmadığını belirlemek için yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, tx_event_flags_get hizmette görece yüksek sayıda  zaman aşımı olması, olay bayraklarının askıya alınma zaman aşımının çok kısa olduğunu önermiş olabilir.

### <a name="event-flags-group-control-block-tx_event_flags_group"></a>Event Flags Grup Denetim Bloğu TX_EVENT_FLAGS_GROUP
Her olay bayrak grubunun özellikleri denetim bloğunda bulunur. Geçerli olay bayrakları ayarları ve olaylar için askıya alınan iş parçacığı sayısı gibi bilgileri içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır. 

Olay grubu denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline yaygındır.

## <a name="memory-block-pools"></a>Bellek Blok Havuzları  

Belleğin hızlı ve belirlenimci bir şekilde belirlenmesi, gerçek zamanlı uygulamalarda her zaman bir zorlukdur. ThreadX SMP, sabit boyutlu birden çok bellek bloğu havuzu oluşturma ve yönetme olanağı sağlar.

Bellek bloğu havuzları sabit boyutlu bloklardan oluşan olduğundan, hiçbir zaman parçalanma sorunu oluşturmaz. Elbette parçalanma, doğası gereği belirlenemeyen davranışlara neden olur. Ayrıca, sabit boyutlu bir bellek bloğu ayırmak ve serbest bırakma süresi, basit bağlantılı liste işlemesi ile karşılaştırılabilir. Ayrıca, kullanılabilir listenin başında bellek bloğu ayırma ve ayırmayı geri alır. Bu, mümkün olan en hızlı bağlantılı liste işlemeyi sağlar ve gerçek bellek bloğun önbellekte tutmaya yardımcı olabilir.

Esneklik eksikliği, sabit boyutlu bellek havuzlarının temel dezavantajıdır. Bir havuzun blok boyutu, kullanıcılarının en kötü durum bellek gereksinimlerini işecek kadar büyük olmalı. Elbette, aynı havuza çok sayıda farklı boyutta bellek isteği yapılırsa bellek boşa harcanmış olabilir. Olası bir çözüm, farklı boyutlu bellek blokları içeren birkaç farklı bellek bloğu havuzu yapmaktır.

Her bellek bloğu havuzu genel bir kaynaktır. ThreadX SMP, havuzların nasıl kullanıldıklarına hiçbir kısıtlama uygulamaz.

### <a name="creating-memory-block-pools"></a>Bellek Blok Havuzları Oluşturma  
Bellek bloğu havuzları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Bir uygulamanın bellek bloğu havuzlarının sayısına bir sınır yoktur.

### <a name="memory-block-size"></a>Bellek Bloğu Boyutu  
Daha önce belirtildiği gibi, bellek blok havuzları bir dizi sabit boyutlu blok içerir. Bayt cinsinden blok boyutu, havuzun oluşturulması sırasında belirtilir.

> [!IMPORTANT]
> ThreadX SMP, havuza her bellek bloğuna küçük miktarda ek yük (C işaretçisinin boyutu) ekler. Buna ek olarak, ThreadX SMP'nin her bellek bloğunun başlangıcını düzgün hizalamada tutmak için blok boyutunu dolguya eklemesi gerekir.

### <a name="pool-capacity"></a>Havuz Kapasitesi 
Havuzdaki bellek bloklarının sayısı, blok boyutuna ve oluşturma sırasında sağlanan bellek alanında sağlanan toplam bayt sayısına sahip bir işlevdir. Bir havuzun kapasitesi, blok boyutu (doldurma ve işaretçi ek yükü baytları dahil) sağlanan bellek alanında toplam bayt sayısına bölünerek hesaplanır.

### <a name="pools-memory-area"></a>Havuzun Bellek Alanı 
Daha önce belirtildiği gibi, blok havuzunun bellek alanı oluşturma sırasında belirtilir. ThreadX SMP'nin diğer bellek alanlarında olduğu gibi hedefin adres alanı içinde herhangi bir yerde yer alıyor olabilir.

Sağladığı önemli esneklik nedeniyle bu önemli bir özelliktir. Örneğin, bir iletişim ürününün, I/O için yüksek bir bellek alanına sahip olduğunu varsayalım. Bu bellek alanı, bir ThreadX SMP bellek bloğu havuzuna dönüştürerek kolayca yönetilir.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma 
Uygulama iş parçacıkları boş bir havuzdan bellek bloğu beklerken askıya alabilir. Havuza bir blok döndürüldü, askıya alınan iş parçacığına bu blok verilir ve iş parçacığı devam eder.

Aynı bellek bloğu havuzunda birden çok iş parçacığı askıya alınırsa, bunlar askıya alındıklarına (FIFO) göre devam eder.

Ancak uygulama, iş parçacığının askıya alınmasına neden ***olan blok tx_block_pool_prioritize*** çağrısından önce çağrılsa öncelik verme de mümkündür. Blok havuzu öncelik belirleme hizmeti en yüksek öncelikli iş parçacığını askıya alma listesinin önüne, diğer tüm askıya alınmış iş parçacıklarını da aynı FIFO sırasına göre bırakarak yer alıyor.

### <a name="run-time-block-pool-performance-information"></a>Çalışma Zamanı Blok Havuzu Performans Bilgileri  
ThreadX SMP, isteğe bağlı çalışma zamanı blok havuzu performans bilgileri sağlar. ThreadX SMP kitaplığı ve uygulaması tanımlı bir ***TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO,*** ThreadX SMP aşağıdaki bilgileri birikiyor.

Genel sistemin toplam sayısı:

- ayrılan bloklar
- yayımlanan bloklar
- ayırma askıya almaları
- ayırma zaman aşımı

Her blok havuzu için toplam sayı:

- ayrılan bloklar
- yayımlanan bloklar
- ayırma askıya almaları
- ayırma zaman aşımı

Bu bilgiler, çalışma zamanında, tx_block_pool_performance_info_get *ve tx_block_pool_performance_system_info_get.*  Blok havuzu performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, görece yüksek sayıda "ayırma askıya alma" blok havuzunun çok küçük olduğunu önerebiliriz.

### <a name="memory-block-pool-control-block-tx_block_pool"></a>Bellek Blok Havuzu Denetim Bloğu TX_BLOCK_POOL  
Her bellek bloğu havuzunun özellikleri denetim bloğunda bulunur. Kullanılabilir bellek bloğu sayısı ve bellek havuzu blok boyutu gibi bilgileri içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır. 

Havuz denetim blokları bellekte herhangi bir yerde de yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi. 

### <a name="overwriting-memory-blocks"></a>Bellek Bloklarının Üzerine Yazma  
Ayrılmış bir bellek bloğu kullanıcılarının sınırlarının dışına yazmaması önemlidir. Bu durumda bozulma bitişik (genellikle sonraki) bir bellek alanında oluşur. Sonuçlar tahmin edilemez ve genellikle önemlidir! 

## <a name="memory-byte-pools"></a>Bellek Byte Havuzları

ThreadX SMP bellek bayt havuzları standart bir C yığınına benzer. Standart C yığınının aksine, birden çok bellek bayt havuzu olabilir. Ayrıca, istenen bellek kullanılabilir olana kadar iş parçacıkları bir havuzda askıya alabilir.

Bellek bayt havuzlarından ayırmalar,  istenen bellek miktarını (bayt cinsinden) içeren geleneksel yanlış konum çağrılarına benzer. Bellek havuzdan ilk uygun *şekilde* ayrılır; Başka bir ifadeyle isteği yerine gelen ilk boş bellek bloğu kullanılır. Bu bloktan fazla bellek yeni bir bloka dönüştürülür ve boş bellek listesine geri yerleştirilir. Bu işleme parçalanma *denir.*

Bitişik boş bellek blokları, *yeterli* sayıda boş bellek bloğu için sonraki ayırma araması sırasında birleştirilir. Bu işleme *parçalanmayı yoklama denir.*

Her bellek bayt havuzu genel bir kaynaktır. ThreadX SMP, isr'lerden bellek bayt hizmetlerinin çağrılanama dışında havuzların kullanımına kısıtlama uygulamaz.

### <a name="creating-memory-byte-pools"></a>Bellek Byte Havuzları Oluşturma 
Bellek bayt havuzları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Bir uygulamanın bellek bayt havuzlarının sayısına bir sınır yoktur.  

### <a name="pool-capacity"></a>Havuz Kapasitesi 
Bir bellek bayt havuzu içinde allocatable bayt sayısı, oluşturma sırasında belirtilenden biraz daha azdır. Bunun nedeni, boş bellek alanı yönetiminin bazı ek yükler ortaya çıktısı. Havuzdaki her boş bellek bloğu, iki ek yük C işaretçisinin eşdeğerini gerektirir. Ayrıca havuz iki blokla oluşturulur: büyük bir boş blok ve bellek alanı sonunda kalıcı olarak ayrılan küçük bir blok. Ayrılan bu blok, ayırma algoritmasının performansını geliştirmek için kullanılır. Birleştirme sırasında havuz alanı sonunu sürekli denetleme ihtiyacı ortadan kaldırıyor.  

Çalışma süresi sırasında havuza ek yük miktarı genellikle artar. Bir sonraki bellek bloğunda düzgün hizalama sağlamak için tek sayıda bayt ayırmaları dolgulu olarak gelir. Buna ek olarak, havuz daha parçalı hale geldi olarak ek yük artar.

### <a name="pools-memory-area"></a>Havuzun Bellek Alanı  
Bir bellek bayt havuzunun bellek alanı oluşturma sırasında belirtilir. ThreadX SMP'nin diğer bellek alanlarında olduğu gibi hedefin adres alanı içinde herhangi bir yerde yer alıyor olabilir. 

Sağladığı önemli esneklik nedeniyle bu önemli bir özelliktir. Örneğin, hedef donanım yüksek hızlı bir bellek alanına ve düşük hızlı bir bellek alanına sahipse, kullanıcı her iki alanda da bir havuz oluşturarak her iki alan için bellek ayırmayı yönetebilir. 

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma  
Bir havuzdan bellek baytları beklerken uygulama iş parçacıkları askıya alabilir. Yeterli bitişik bellek kullanılabilir duruma geldiğinde, askıya alınan iş parçacıklarına istenen bellek verilir ve iş parçacıkları devam eder. 

Aynı bellek byte havuzunda birden çok iş parçacığı askıya alınırsa, askıya alındıklarına (FIFO) göre bellek verilir (sürdürür). 

Ancak, uygulama iş parçacığının askıya alınmasına neden ***olan tx_byte_pool_prioritize*** yayın çağrısından önce çağrılsa öncelik verme de mümkündür. Bayt havuzu hizmeti öncelik sırasına göre en yüksek öncelikli iş parçacığını askıya alma listesinin önüne, diğer tüm askıya alınmış iş parçacıklarını aynı FIFO sırasına göre bırakarak yer alıyor.

### <a name="run-time-byte-pool-performance-information"></a>Çalışma Zamanı Byte Havuzu Performans Bilgileri  
ThreadX SMP, isteğe bağlı çalışma zamanı byte havuzu performans bilgileri sağlar. ThreadX SMP kitaplığı ve uygulaması tanımlı bir ***TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO,*** ThreadX SMP aşağıdaki bilgileri birikiyor.

Genel sistemin toplam sayısı:

- Tahsisatları
- yayınlar
- parçalar arandı
- birleştirilen parçalar
- oluşturulan parçalar
- ayırma askıya almaları
- ayırma zaman aşımı

Her bir byte havuzu için toplam sayı:

- Tahsisatları
- yayınlar
- parçalar arandı
- birleştirilen parçalar
- oluşturulan parçalar
- ayırma askıya almaları
- ayırma zaman aşımı

Bu bilgiler, çalışma zamanında tx_byte_pool_performance_info_get ve *tx_byte_pool_performance_system_info_get.*  Byte havuzu performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, görece yüksek sayıda "ayırma askıya alma" bayt havuzunun çok küçük olduğunu önerebiliriz.

### <a name="memory-byte-pool-control-block-tx_byte_pool"></a>Bellek Byte Havuzu Denetim Bloğu TX_BYTE_POOL  
Her bellek bayt havuzunun özellikleri denetim bloğunda bulunur. Havuza kullanılabilir bayt sayısı gibi yararlı bilgiler içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır. 

Havuz denetim blokları bellekte herhangi bir yerde de yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi. 

### <a name="nondeterministic-behavior"></a>Belirsiz Davranış 
Bellek bayt havuzları en esnek bellek ayırmayı sağlasa da, belirsiz bir davranıştan da zarar alırlar. Örneğin, bir bellek bayt havuzu 2.000 bayt kullanılabilir belleğe sahip olabilir, ancak 1.000 baytlık bir ayırma isteğini karşılayamayabilirsiniz. Bunun nedeni, boş baytların kaç tane bitişik olduğuyla ilgili bir garanti yoktur. 1.000 bayt boş blok olsa bile, bloğun bulunamaz hale ne kadar sürecesi garanti edilemez. 1.000 bayt bloğu bulmak için bellek havuzunun tamamının aranmış olması tamamen mümkündür. 

> [!IMPORTANT]
> Bu nedenle, belirlenmci, gerçek zamanlı davranışın gerekli olduğu alanlarda bellek bayt hizmetlerini kullanmaktan kaçınmak genellikle iyi bir uygulamadır. Birçok uygulama başlatma veya çalışma zamanı yapılandırması sırasında gerekli belleklerini önceden ayırır.

### <a name="overwriting-memory-blocks"></a>Bellek Bloklarının Üzerine Yazma 
Ayrılan bellek kullanıcılarının sınırlarının dışına yazmaması önemlidir. Bu durumda bozulma bitişik (genellikle sonraki) bir bellek alanında oluşur. Sonuçlar tahmin edilemez ve genellikle önemlidir! 

## <a name="application-timers"></a>Uygulama Süre süreleri

Zaman uyumsuz dış olaylara hızlı yanıt, gerçek zamanlı, tümleşik uygulamaların en önemli işlevidir. Ancak, bu uygulamaların birçoğu önceden belirlenen zaman aralıklarında belirli etkinlikleri de gerçekleştirecektir.

ThreadX SMP uygulama süreçerleri, uygulamalara belirli aralıklarla uygulama C işlevlerini yürütme olanağı sağlar. Bir uygulama zamanlayıcının süresinin yalnızca bir kez dolması da mümkündür. Aralık süreölçerleri yinelenen düzenli *süreölçerler olarak* çağrılırken, bu tür bir zamanlayıcı tek *atışlı zamanlayıcı olarak çağrılır.*

Her uygulama zamanlayıcısı genel bir kaynaktır. ThreadX SMP, uygulama süre sürelerini kısıtlamaz.

> [!IMPORTANT]
> Uygulama süre süreleri, api'si aracılığıyla herhangi bir çekirdekte tx_timer_smp_core_exclude dışlandırabilirsiniz.

### <a name="timer-intervals"></a>Zamanlayıcı Aralıkları 
ThreadX SMP zaman aralıkları, düzenli aralıklarla zamanlayıcı kesintileri ile ölçülür. Her zamanlayıcı kesintisi, zamanlayıcı değer işareti *olarak adlandırılan bir değerdir.* Zamanlayıcı saat değerleri arasındaki gerçek süre uygulama tarafından belirtilir, ancak çoğu uygulama için 10 m'ler normdur. Düzenli süreölçer kurulumu genellikle tx_initialize_low_level ***dosyasında*** bulunur.

Temel alınan donanımın, uygulama süre önceleri için düzenli aralıklarla kesintiler oluşturabilme özelliğine sahip olması gerektiğini de ifade etmek gerekir. Bazı durumlarda işlemcinin yerleşik düzenli aralıklarla kesme özelliği vardır. İşlemcinin bu özelliği yoksa, kullanıcının panosunda düzenli aralıklarla kesintiler oluşturan bir çevre cihazı olması gerekir.

> [!IMPORTANT]
> ThreadX SMP, düzenli aralıklarla kesme kaynağı olmadan bile işleve devam ediyor. Ancak, zamanlayıcıyla ilgili tüm işlemler devre dışı bırakılır. Buna zaman, askıya alma zaman zamanları ve zamanlayıcı hizmetleri dahildir.

### <a name="timer-accuracy"></a>Zamanlayıcı Doğruluğu 
Zamanlayıcı süre sonu, saat işareti olarak belirtilir. Belirtilen süre sonu değeri, her zamanlayıcı değer değerinde bir azaltıldı. Bir uygulama süreölçeri, zamanlayıcı kesintisi (veya zamanlayıcı onay işareti) öncesinde etkinleştirilenene kadar, gerçek süre sonu erken bir değere kadar olabilir.

Süreölçer onay hızı 10 dakika ise, uygulama süreölçerleri 10 dakika erken sona erebilir. Bu, 10 m süreye sahip olan süreler için 1 saniyelik süreye göre daha önemlidir. Elbette zamanlayıcı kesme sıklığının artırılması bu hata marjını azaltıyor.

### <a name="timer-execution"></a>Zamanlayıcı Yürütme 
Uygulama sürelerini etkin hale geldiklerinde yürütürler. Örneğin, aynı süre sonu değeriyle üç süre sonu oluşturulur ve etkinleştirilirse, karşılık gelen süre sonu işlevlerinin etkinleştiril edildiklerine göre yürütülmesi garanti edilir. 

### <a name="creating-application-timers"></a>Uygulama Süre sürelerini oluşturma 
Uygulama süre sürelerini başlatma sırasında veya çalışma zamanında uygulama iş parçacıkları tarafından oluşturulur. Bir uygulamanın uygulama süre sürelerini sınırlamaz. 

### <a name="run-time-application-timer-performance-information"></a>Çalışma Zamanı Uygulama Süreölçeri Performans Bilgileri  
ThreadX SMP, isteğe bağlı çalışma zamanı uygulama süreölçeri performans bilgileri sağlar. ThreadX SMP kitaplığı ve uygulaması tanımlı bir ***TX_TIMER_ENABLE_PERFORMANCE_INFO,*** ThreadX SMP aşağıdaki bilgileri birikiyor. 

Genel sistemin toplam sayısı:

- Etkinleştirme
- devre dışı bırakmalar
- yeniden etkinleştirmeler (düzenli süreerler)
- Süre sonu
- süre sonu ayarlamaları

Her uygulama zamanlayıcısı için toplam sayı:

- Etkinleştirme
- devre dışı bırakmalar
- yeniden etkinleştirmeler (düzenli süreerler)
- Süre sonu
- süre sonu ayarlamaları

Bu bilgiler, çalışma zamanında, tx_timer_performance_info_get *ve tx_timer_performance_system_info_get.*  Uygulama Süreölçeri performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır.

### <a name="application-timer-control-block-tx_timer"></a>Uygulama Süreölçeri Denetim Bloğu TX_TIMER 
Her uygulama zamanlayıcının özellikleri denetim bloğunda bulunur. 32 bit süre sonu tanımlama değeri gibi yararlı bilgiler içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

Uygulama süreölçer denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğunun herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapıya sahip olmasıdır. 

### <a name="excessive-timers"></a>Aşırı Süreye Neden Olan Süre 
Varsayılan olarak, uygulama süreleri genellikle herhangi bir uygulama iş parçacığından daha yüksek olan, öncelik sıfırda çalışan gizli bir sistem iş parçacığı içinde yürütülür. Bu nedenle, uygulama sürelerini içinde işleme en düşük düzeyde tutulmalıdır. 

Ayrıca, mümkün olan her zamanlayıcının süresinin dolması gibi bir süreölçerden kaçınmak da önemlidir. Böyle bir durum uygulamada aşırı yüke neden olabilir.

> [!WARNING]
> Daha önce belirtildiği gibi, uygulama süre sürelerini gizli bir sistem iş parçacığından yürütülür. Bu nedenle, uygulama zamanlayıcının süre sonu işlevinden yapılan herhangi bir ThreadX SMP hizmet çağrısında askıya alma seçeneğinin seçmemesi önemlidir.

## <a name="relative-time"></a>Göreli Saat

ThreadX SMP, daha önce bahsedilen uygulama süre tutuculara ek olarak sürekli artan tek bir 32 bitlik değer sayacı sağlar. Her zamanlayıcı kesintisi *için* değer işareti sayacı veya süresi bir artırıldı.

Uygulama, bu 32 bit sayacı sırasıyla tx_time_get *ve* tx_time_set aracılığıyla okuyabilir veya ayarlayabilirsiniz. Bu değer işareti sayacının kullanımı tamamen uygulama tarafından belirlenir. ThreadX SMP tarafından dahili olarak kullanılmaz.

### <a name="interrupts"></a>Kesme 
Zaman uyumsuz olaylara hızlı yanıt, gerçek zamanlı, katıştırılmış uygulamaların asıl işlevidir. Uygulama böyle bir olayın donanım kesintileri aracılığıyla mevcut olduğunu bilir. 

Kesme, işlemci yürütmesinde zaman uyumsuz bir değişikliktir. Genellikle, bir kesme oluştuğunda, işlemci geçerli yürütmenin küçük bir kısmını yığına kaydeder ve denetimi uygun kesme vektörüne iletir. Kesme vektörü temelde belirli tür kesintilerini işlemeden sorumlu olan yordamın adresidir. Tam kesme işleme yordamı işlemciye özgüdür. 

### <a name="interrupt-control"></a>Kesme Denetimi 
Tx_interrupt_control *hizmeti,* uygulamaların kesmeleri etkinleştirmesini ve devre dışı bırakmasını sağlar. Önceki kesme etkinleştirme/devre dışı bırakma duruşu bu hizmet tarafından döndürülür. Kesme denetimi yalnızca o anda yürütülen program kesimini etkiler. Örneğin, bir iş parçacığı kesmeleri devre dışı bırakıyorsa, bunlar yalnızca o iş parçacığının yürütülmesi sırasında devre dışı kalır. 

> [!WARNING]
> Maskelenebilir Olmayan Kesinti (NMI), donanım tarafından devre dışı bırakılamaz bir kesintidir. Böyle bir kesinti ThreadX SMP uygulamaları tarafından kullanılabilir. Ancak, uygulamanın NMI işleme yordamının ThreadX SMP bağlam yönetimini veya herhangi bir API hizmetlerini kullanmasına izin verilmez. ThreadX SMP Yönetilen Kesintileri

ThreadX SMP, uygulamalara tam kesme yönetimi sağlar. Bu yönetim, kesintiye neden olan yürütme bağlamını kaydetmeyi ve geri yüklemeyi içerir. Ayrıca, ThreadX SMP, bazı hizmetlerin kesme hizmeti yordamları (ISRS) içinden çağrılmasına izin verir. Aşağıda, uygulama ISRs 'den izin verilen ThreadX SMPservices listesi verilmiştir:

- tx_block_allocate 
- tx_block_pool_info_get 
- tx_block_pool_prioritize 
- tx_block_pool_performance_info_get 
- tx_block_pool_performance_system_info_get 
- tx_block_release 
- tx_byte_pool_info_get 
- tx_byte_pool_performance_info_get 
- tx_byte_pool_performance_system_info_get 
- tx_byte_pool_prioritize 
- tx_event_flags_info_get 
- tx_event_flags_get 
- tx_event_flags_set 
- tx_event_flags_performance_info_get 
- tx_event_flags_performance_system_info_get 
- tx_event_flags_set_notify 
- tx_interrupt_control 
- tx_mutex_performance_info_get 
- tx_mutex_performance_system_info_get 
- tx_queue_front_send 
- tx_queue_info_get 
- tx_queue_performance_info_get 
- tx_queue_performance_system_info_get 
- tx_queue_prioritize 
- tx_queue_receive 
- tx_queue_send 
- tx_semaphore_get 
- tx_queue_send_notify 
- tx_semaphore_ceiling_put 
- tx_semaphore_info_get 
- tx_semaphore_performance_info_get 
- tx_semaphore_performance_system_info_get 
- tx_semaphore_prioritize 
- tx_semaphore_put 
- tx_thread_identify 
- tx_semaphore_put_notify 
- tx_thread_entry_exit_notify 
- tx_thread_info_get 
- tx_thread_resume 
- tx_thread_performance_info_get 
- tx_thread_performance_system_info_get 
- tx_thread_stack_error_notify 
- tx_thread_wait_abort 
- tx_time_get 
- tx_time_set 
- tx_timer_activate 
- tx_timer_change 
- tx_timer_deactivate 
- tx_timer_info_get 
- tx_timer_performance_info_get 
- tx_timer_performance_system_info_get

> [!WARNING]
> ISRs 'den askıya alma yapılmasına izin verilmez. Bu nedenle, bir ıSR 'den yapılan tüm ThreadX SMP hizmet çağrılarının **wait_option** parametresi **TX_NO_WAIT** olarak ayarlanmalıdır.

### <a name="isr-template"></a>ISR şablonu 
Uygulama kesmelerini yönetmek için uygulama ISRs 'nin başında ve sonunda birkaç ThreadX SMP yardımcı programı çağrılmalıdır. Kesme işleme için tam biçim, bağlantı noktaları arasında farklılık gösterir. ISRs 'yi yönetme hakkında belirli yönergeler için dağıtım diskindeki ***readme_threadx.txt*** dosyasını gözden geçirin.

Aşağıdaki küçük kod segmenti, en çok ThreadX SMP yönetilen ISRs 'nin tipik bir parçasıdır. Çoğu durumda, bu işlem derleme dilidir.

**_application_ISR_vector_entry**:  
; Bağlam Kaydet ve hazırla  
; ISR 'yi çağırarak ThreadX SMP kullanımı  
; Giriş işlevi.  
**_TX_THREAD_CONTEXT_SAVE** çağrısı  

; ISR artık ThreadX SMP ' i çağırabilir  
; Hizmetler ve kendi C işlevleri  

; ISR tamamlandığında bağlam  
; geri yüklendi (veya iş parçacığı önalım)  
; bağlam geri yüklemeyi çağırarak  
; çalışmayacaktır. Denetim döndürmüyor!  
**_TX_THREAD_CONTEXT_RESTORE** atlayın

### <a name="high-frequency-interrupts"></a>Yüksek frekanslı kesmeler  
Bazı kesmeler, her kesme sırasında tam bağlam kaydetme ve geri yükleme işlemlerinin çok fazla işlem bant genişliği tükettiği bir sıklıkta oluşur. Böyle durumlarda, uygulamanın bu highfrequency kesmelerinin çoğunluğu için sınırlı miktarda işleme yapan küçük bir derleme dili ıSR olması yaygındır. 

Belirli bir noktadan sonra, küçük ıSR 'nin ThreadX SMP ile etkileşimde olması gerekebilir. Bu, yukarıdaki şablonda açıklanan giriş ve çıkış işlevleri çağırarak gerçekleştirilir. 

### <a name="interrupt-latency"></a>Kesme gecikmesi  
ThreadX SMP, kısa bir süre içinde kesmeleri kilitler. En fazla süre kesmesi devre dışı, bir iş parçacığının bağlamını kaydetmek veya geri yüklemek için gereken sürenin sıraındadır. 