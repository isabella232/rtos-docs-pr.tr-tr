---
title: Bölüm 3-Azure RTOS ThreadX 'in Işlevsel bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS ThreadX çekirdeğinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: aa66ad392171958e5d2cc765992fd1a9e41250a6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827371"
---
# <a name="chapter-3---functional-components-of-azure-rtos-threadx"></a>Bölüm 3-Azure RTOS ThreadX 'in Işlevsel bileşenleri

Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS ThreadX çekirdeğinin açıklaması yer almaktadır. Her işlevsel bileşen kolay anlaşılır bir şekilde sunulur.

## <a name="execution-overview"></a>Yürütmeye genel bakış

Bir ThreadX uygulaması içinde dört tür program yürütme vardır: başlatma, Iş parçacığı yürütme, kesme hizmeti yordamları (IRS) ve uygulama zamanlayıcıları.

Şekil 2 ' de her farklı program yürütme türü gösterilmektedir. Bu bölümün sonraki bölümlerinde bu türlerin her biri hakkında daha ayrıntılı bilgi bulabilirsiniz.

### <a name="initialization"></a>Başlatma

Adından da anlaşılacağı gibi, bu, bir ThreadX uygulamasında program yürütmenin ilk türüdür. Başlatma, işlemci sıfırlaması ve *iş parçacığı zamanlama döngüsünün* giriş noktası arasındaki tüm program yürütmesini içerir.

### <a name="thread-execution"></a>İş parçacığı yürütme

Başlatma tamamlandıktan sonra ThreadX iş parçacığı zamanlama döngüsüne girer. Zamanlama döngüsü, bir uygulama iş parçacığını yürütmeye hazırsa bakar. Bir ready iş parçacığı bulunduğunda, ThreadX denetimi buna aktarır. İş parçacığı tamamlandıktan sonra (veya daha yüksek öncelikli bir iş parçacığı hazır hale gelirse), yürütme sonraki en yüksek önceliğe hazır iş parçacığını bulmak için iş parçacığı zamanlama döngüsüne geri aktarılır.

İş parçacıklarını sürekli olarak yürüten ve zamanlıyor olan bu işlem, ThreadX uygulamalarında en yaygın program yürütme türüdür.

### <a name="interrupt-service-routines-isr"></a>Kesme hizmeti yordamları (ıSR)

Kesmeler gerçek zamanlı sistemlerin temel taşıdır. Kesmeler olmadan dış dünyadaki değişikliklere zamanında yanıt vermek son derece zor olur. Bir kesmeyi algılamada, İşlemci geçerli program yürütme (genellikle yığında) hakkındaki önemli bilgileri kaydeder ve sonra denetimi önceden tanımlanmış bir program alanına aktarır. Bu önceden tanımlanmış program alanı, genellikle bir kesme hizmeti yordamı olarak adlandırılır. Çoğu durumda, iş parçacığı yürütme sırasında (veya iş parçacığı zamanlama döngüsünde) kesmeler oluşur. Ancak, kesmeler yürütülen bir ıSR veya bir uygulama süreölçeri içinde de gerçekleşebilir.

![Program yürütme türleri](./media/user-guide/types-program-execution.png)

**ŞEKIL 2. Program yürütme türleri**

### <a name="application-timers"></a>Uygulama zamanlayıcıları

Uygulama Zamanlayıcılarına benzer şekilde, donanım uygulaması (genellikle tek bir düzenli donanım kesmesi kullanıldığında) uygulamadan gizlenir. Bu tür zamanlayıcılar, uygulamalar tarafından zaman aşımları, dönems ve/veya izleme hizmetleri gerçekleştirmek için kullanılır. ISRs gibi, uygulama zamanlayıcılar çoğu zaman iş parçacığı yürütmeyi keser. Ancak, IRS 'nin aksine, uygulama zamanlayıcıları birbirini kesintiye uğratabilir.

## <a name="memory-usage"></a>Bellek Kullanımı

ThreadX, uygulama programıyla birlikte bulunur. Sonuç olarak, ThreadX 'in statik bellek (veya sabit bellek) kullanımı geliştirme araçları tarafından belirlenir; Örneğin, derleyici, bağlayıcı ve bulucu. Dinamik bellek (veya çalışma zamanı belleği) kullanımı, uygulamanın doğrudan denetimi altındadır.

### <a name="static-memory-usage"></a>Statik bellek kullanımı

Geliştirme araçlarının çoğu, uygulama programı görüntüsünü beş temel alana böler: *yönerge*, *sabit*, *başlatılan veriler*, *başlatılmamış veriler* ve *Sistem yığını*. Şekil 3 ' te bu bellek alanlarının bir örneği gösterilmektedir.

Bunun yalnızca bir örnek olduğunu anlamak önemlidir. Gerçek statik bellek düzeni işlemci, geliştirme araçları ve temel alınan donanıma özeldir.

Yönerge alanı, programın işlemci yönergelerini içerir. Bu alan genellikle en büyüktür ve genellikle ROM ' da bulunur.

Sabit alan, program içinde tanımlanan veya başvurulan dizeler dahil olmak üzere çeşitli derlenmiş sabitler içerir. Ayrıca, bu alan başlatılan veri alanının "ilk kopyasını" içerir. *Bellek kullanımı* derleyicisinin başlatma işlemi sırasında, sabit alanın bu bölümü RAM 'de başlatılmış veri alanını ayarlamak için kullanılır. Sabit alan genellikle yönerge alanını izler ve genellikle ROM 'da bulunur.

Başlatılmış veriler ve başlatılmamış veri alanlarında tüm genel ve statik değişkenler bulunur. Bu bölgeler her zaman RAM olarak bulunur.

Sistem yığını genellikle başlatılmış ve başlatılmamış veri alanlarından hemen sonra ayarlanır.

Sistem yığını başlatma sırasında derleyici tarafından, başlatma sırasında ThreadX ve daha sonra ıSR işleminde kullanılır.

![Bellek alanı örneği](./media/user-guide/memory-area-example.png)

**ŞEKIL 3. Bellek alanı örneği**

### <a name="dynamic-memory-usage"></a>Dinamik Bellek kullanımı

Daha önce belirtildiği gibi, dinamik bellek kullanımı uygulamanın doğrudan denetimi altındadır. Yığınlar, kuyruklar ve bellek havuzlarıyla ilişkili denetim blokları ve bellek alanları, hedefin bellek alanında herhangi bir yere yerleştirilebilir. Bu önemli bir özelliktir çünkü farklı türlerdeki fiziksel belleğin kolay kullanımını kolaylaştırır.

Örneğin, bir hedef donanım ortamının hem hızlı bellek hem de yavaş bellek olduğunu varsayalım. Uygulamanın yüksek öncelikli bir iş parçacığı için ek performansa ihtiyacı varsa, denetim bloğu (TX_THREAD) ve Stack hızlı bellek alanına yerleştirilebilir ve bu da performansını önemli ölçüde geliştirebilir.

## <a name="initialization"></a>Başlatma

Başlatma işlemini anlamak önemlidir. İlk donanım ortamı burada ayarlanır. Buna ek olarak, uygulama ilk kişiliğine verilirler.

> [!NOTE]
> *ThreadX, tüm geliştirme aracının başlatma sürecini (mümkün olduğunda) kullanmaya çalışır. Bu, gelecekte geliştirme araçlarının yeni sürümlerine yükseltmeyi kolaylaştırır.*

### <a name="system-reset-vector"></a>Sistem sıfırlama vektörü

Tüm mikro işlemcilerin sıfırlama mantığı vardır. Bir sıfırlama gerçekleştiğinde (donanım ya da yazılım), uygulamanın giriş noktasının adresi belirli bir bellek konumundan alınır. Giriş noktası alındıktan sonra, işlemci denetimi bu konuma aktarır. Uygulama giriş noktası genellikle yerel derleme dilinde yazılır ve genellikle geliştirme araçları (en azından şablon biçiminde) tarafından sağlanır. Bazı durumlarda, bir giriş programının özel bir sürümü ThreadX ile birlikte sağlanır.

### <a name="development-tool-initialization"></a>Geliştirme aracı başlatma

Düşük düzey başlatma işlemi tamamlandıktan sonra, geliştirme aracının üst düzey başlatmasına yönelik denetimleri aktarır. Bu genellikle başlatılmış Global ve statik C değişkenlerinin ayarlandığı yerdir. İlk değerlerinin sabit alandan alındığını unutmayın. Tam başlatma işlemi, geliştirme aracına özgüdür.

### <a name="main-function"></a>Main Işlevi

Geliştirme aracı başlatması tamamlandığında, Kullanıcı tarafından sağlanan *ana* işleve yapılan aktarımları denetler. Bu noktada, uygulama ileri ' yi denetler. Çoğu uygulama için, Main işlevi yalnızca ThreadX girişi olan *tx_kernel_enter* çağırır. Ancak, uygulamalar, ThreadX girmeden önce ön işleme (genellikle donanım başlatma için) gerçekleştirebilir.

> [!IMPORTANT]
> *Tx_kernel_enter çağrısı döndürmez, bu nedenle işlemden sonra herhangi bir işlem yerleştirmeyin.*

### <a name="tx_kernel_enter"></a>tx_kernel_enter

Giriş işlevi, çeşitli iç ThreadX veri yapılarının başlatılmasını koordine eder ve ardından uygulamanın tanım işlevini ***tx_application_define*** çağırır.

***Tx_application_define*** döndüğünde denetim iş parçacığı zamanlama döngüsüne aktarılır. Bu, başlatma sonunu işaretler.

### <a name="application-definition-function"></a>Uygulama tanımı Işlevi

***Tx_application_define*** işlevi, tüm ilk uygulama iş parçacıkları, kuyruklar, Semaforlar, zaman uyumu sağlayıcılar, olay bayrakları, bellek havuzları ve zamanlayıcılar tanımlar. Uygulamanın normal işlemi sırasında iş parçacıklarında sistem kaynakları oluşturmak ve silmek de mümkündür. Ancak, tüm ilk uygulama kaynakları burada tanımlanmıştır.

***Tx_application_define** _ işlevinin tek bir giriş parametresi vardır ve bu parametre kesinlikle önemlidir. _First kullanılabilir * RAM adresi, bu işleve yönelik tek giriş parametresidir. Genellikle iş parçacığı yığınlarının, kuyruklarının ve bellek havuzlarının ilk çalışma zamanı bellek ayırmaları için başlangıç noktası olarak kullanılır.

> [!NOTE]
> *Başlatma tamamlandıktan sonra, yalnızca bir çalışan iş parçacığı, diğer iş parçacıkları dahil olmak üzere sistem kaynaklarını oluşturabilir ve silebilir. Bu nedenle, başlatma sırasında en az bir iş parçacığının oluşturulması gerekir.*

### <a name="interrupts"></a>Kesmelerini

Kesmeler, başlatma işleminin tamamı sırasında devre dışı bırakılır. Uygulama kesintiye yol açabilir, öngörülemeyen bir davranış meydana gelebilir. Şekil 4 ' te, uygulama özel başlatma aracılığıyla sistem sıfırlamalarından başlatma işleminin tamamı gösterilmektedir.

## <a name="thread-execution"></a>İş parçacığı yürütme

Uygulama iş parçacıklarını zamanlama ve yürütme, ThreadX 'in en önemli etkinliğidir. İş parçacığı genellikle adanmış bir amaçla yarı bağımsız program segmenti olarak tanımlanır. Tüm iş parçacıklarının birleştirilmiş işleme bir uygulama oluşturur.

İş parçacıkları, başlatma sırasında veya iş parçacığı yürütme sırasında ***tx_thread_create** _ çağırarak dinamik olarak oluşturulur. İş parçacıkları _ready * veya *askıya alınma* durumunda oluşturulur.

![Başlatma Işlemi](./media/user-guide/initialization-process.png)

**ŞEKIL 4. Başlatma Işlemi**

### <a name="thread-execution-states"></a>İş parçacığı yürütme durumları

İş parçacıklarının farklı işleme durumlarını anlamak, çok iş parçacıklı ortamın tamamını anlamak için önemli bir ortamdır. ThreadX 'de, beş farklı iş parçacığı durumu vardır: *hazırlanıyor*, *askıya alındı*, *yürütülüyor*, *sonlandırıldı* ve *tamamlandı*. Şekil 5 ' te ThreadX iş parçacığı durum geçişi diyagramı gösterilmektedir.

![İş parçacığı durum geçişi](./media/user-guide/thread-state-transition.png)

**ŞEKIL 5. İş parçacığı durum geçişi**

İş parçacığı, yürütülmeye hazırlanmaya hazırsa, *hazırlık* durumundadır. Hazırlık durumunda en yüksek öncelikli iş parçacığı olana kadar, Ready iş parçacığı yürütülmez. Bu durumda, ThreadX iş parçacığını yürütür ve sonra durumunu *yürütülüyor* olarak değiştirir.

Daha yüksek öncelikli bir iş parçacığı hazır hale gelirse, çalıştırılan iş parçacığı *hazır* duruma geri döner. Daha sonra yeni, yüksek öncelikli iş parçacığı yürütülür ve bu, mantıksal durumu *yürütülüyor* olarak değiştirir. Hazırlama *ve* *yürütme* durumları arasındaki bu geçiş, iş parçacığı önalım her gerçekleştiğinde oluşur.

Herhangi bir anda yalnızca bir iş parçacığı *yürütülüyor* durumundadır. Bunun nedeni, *yürütme* durumundaki bir iş parçacığının temeldeki işlemcinin denetimine sahip olmasından kaynaklanır.

*Askıya alınmış* durumdaki iş parçacıkları yürütme için uygun değildir. *Askıya* alınma durumunda olma nedenleri, zaman, kuyruk iletileri, Semaforlar, zaman uyumu sağlayıcılar, olay bayrakları, bellek ve temel iş parçacığı askıya alma için askıya alma içerir. Askıya alma *işlemine* neden kaldırıldıktan sonra, iş parçacığı, hazırlama durumuna geri yerleştirilir.

*Tamamlanmış* durumdaki bir iş parçacığı, işlemini tamamlamış ve giriş işlevinden döndürülen bir iş parçacığıdır. Giriş işlevi iş parçacığı oluşturma sırasında belirtilir. *Tamamlanmış* durumdaki bir iş parçacığı yeniden çalıştırılamaz.

Başka bir iş parçacığı veya iş parçacığının kendisi *tx_thread_terminate* hizmeti olarak adlandırıldığından, iş parçacığı *sonlandırılmış* durumda olur. *Sonlandırılmış* durumdaki bir iş parçacığı yeniden çalıştırılamaz.

> [!IMPORTANT]
> *Tamamlanmış veya sonlandırılmış bir iş parçacığının yeniden başlatılması istenirse, uygulamanın iş parçacığını silmesi gerekir. Daha sonra yeniden oluşturulup yeniden başlatılabilir.*

### <a name="thread-entryexit-notification"></a>İş parçacığı giriş/çıkış bildirimi

Bazı uygulamalar, belirli bir iş parçacığının ilk kez girildiği, tamamlandığında veya sonlandırıldığı zaman bildirilmeye yönelik avantajı bulabilir. ThreadX, ***tx_thread_entry_exit_notify*** hizmeti aracılığıyla bu yeteneği sağlar. Bu hizmet, iş parçacığı çalışmaya başladığında, tamamlandığında veya sonlandırıldığı zaman, ThreadX tarafından çağrılan belirli bir iş parçacığı için bir uygulama bildirim işlevi kaydeder. Çağrıldıktan sonra, uygulama bildirim işlevi uygulamaya özgü işlemleri gerçekleştirebilir. Bu genellikle, bir ThreadX eşitleme temel aracılığıyla olayın başka bir uygulama iş parçacığını bilgilendirmektir.

### <a name="thread-priorities"></a>İş parçacığı öncelikleri

Daha önce bahsedildiği gibi, iş parçacığı adanmış bir amaca sahip yarı bağımsız bir program segmentine sahip olur. Ancak, tüm iş parçacıkları eşit olarak oluşturulmaz! Bazı iş parçacıklarının adanmış amacı diğerlerine göre çok daha önemlidir. Bu heterojen iş parçacığı önemi türü, gömülü gerçek zamanlı uygulamaların bir Hallmark.

ThreadX, *önceliğini* temsil eden bir sayısal değer atanarak iş parçacığı oluşturulduğu zaman bir iş parçacığının önemini belirler. En fazla ThreadX öncelik sayısı, 32 ile 1024 arasında 32 arasında yapılandırılabilir. Fiili en fazla öncelik sayısı, ThreadX kitaplığı derlenirken **TX_MAX_PRIORITIES** sabiti tarafından belirlenir. Daha fazla sayıda öncelik olması, işleme ek yükünü önemli ölçüde artırmaz. Ancak, her 32 öncelik düzeyindeki bir grup için, bunları yönetmek için ek 128 baytlık RAM gerekir. Örneğin, 32 öncelik düzeyleri 128 bayt RAM gerektirir, 64 öncelik düzeyi 256 bayt RAM gerektirir ve 96 öncelik düzeyleri, 384 bayt RAM gerektirir.

Varsayılan olarak, ThreadX 32 öncelik düzeylerine sahiptir ve öncelik 0 ile öncelik 31 arasında değişir. Sayısal olarak daha küçük değerler daha yüksek önceliğe sahiptir. Bu nedenle öncelik 0 en yüksek önceliği temsil ederken öncelik (**TX_MAX_PRIORITIES**-1) en düşük önceliği temsil eder.

Birden çok iş parçacığı, ortak zamanlamaya göre veya zaman dilimlemeye bağlı olarak aynı önceliğe sahip olabilir. Ayrıca, iş parçacığı öncelikleri çalışma zamanı sırasında değiştirilebilir.

### <a name="thread-scheduling"></a>İş parçacığı zamanlaması

ThreadX iş parçacıklarını önceliklerine göre zamanlar. En yüksek önceliğe sahip olan Ready iş parçacığı önce yürütülür. Aynı önceliğe sahip birden çok iş parçacığı hazır ise, ilk *çıkar* (FIFO) şekilde yürütülür.

### <a name="round-robin-scheduling"></a>Hepsini bir kez deneme zamanlaması

ThreadX, aynı önceliğe sahip birden çok iş parçacığının *hepsini bir kez deneme* zamanlamasını destekler. Bu, ***tx_thread_relinquish** _ öğesine yönelik birlikte gerçekleştirilen çağrılar aracılığıyla gerçekleştirilir. Bu hizmet, _ *_tx_thread_relinquish_** çağıranı yeniden yürütmeden önce yürütülmesi için aynı önceliğe sahip diğer tüm diğer iş parçacıklarını sağlar.

### <a name="time-slicing"></a>Time-Slicing

*Zaman Dilimleme* , bir hepsini bir kez deneme zamanlama biçimidir. Zaman dilimi, bir iş parçacığının işlemciyi vermeden yürütebilmesi için en fazla Zamanlayıcı sayısını (süreölçer kesmesi) belirtir. ThreadX ' te, zaman dilimliğine iş parçacığı başına olarak erişilebilir. İş parçacığının zaman dilimi oluşturma sırasında atanır ve çalışma zamanında değiştirilebilir. Bir zaman dilimi süresi dolmuşsa, aynı öncelik düzeyindeki tüm diğer hazırlık iş parçacıklarının, saat dilimlenmiş iş parçacığı yeniden yürütülmeden önce yürütülmesi için bir şans verilir.

Yeni bir iş parçacığı zaman dilimi, askıya alındıktan sonra bir iş parçacığına verildiğinde, yeniden, önalım veya kendi zaman dilimine neden olan bir ThreadX hizmeti çağrısı yapar.

Zaman dilimlenmiş bir iş parçacığı önceden boşaltıldı, zaman diliminin geri kalanı için eşit önceliğe sahip diğer iş parçacıklarından önce devam edecektir.

> [!NOTE]
> *Zaman dilimletmek, daha hafif bir sistem yükü miktarına neden olur. Zaman dilimi yalnızca birden fazla iş parçacığının aynı önceliğe sahip olduğu durumlarda faydalıdır, benzersiz önceliğe sahip iş parçacıkları zaman dilimine atanmamalıdır.*

### <a name="preemption"></a>Önalım

Önalım, yürütülen bir iş parçacığını daha yüksek öncelikli bir iş parçacığına göre geçici olarak kesintiye uğratma işlemidir. Bu işlem yürütülmekte olan iş parçacığında görünmez. Yüksek öncelikli iş parçacığı tamamlandığında, denetim, önalım gerçekleştiği konuma doğru konuma aktarılır. Bu, önemli uygulama olaylarına hızlı yanıt sağladığından gerçek zamanlı sistemlerdeki çok önemli bir özelliktir. Önalım çok önemli bir özellik olsa da,, aşırı yük ve öncelik Inversion gibi çeşitli sorunların bir kaynağı olabilir.

### <a name="preemption-thresholdtrade"></a>Önalım eşiği&trade;

ThreadX, önalım 'in bazı sorunlarından bazılarını kolaylaştırmak için *önalım-Threshold* adlı benzersiz ve gelişmiş bir özellik sunar.

Bir önalım-Threshold, bir iş parçacığının önalım 'yi devre dışı bırakmak için öncelikli *tavan* belirlemesine izin verir. Tavan genişliğinden daha yüksek öncelikler olan iş parçacıklarının hala preempt olmasına izin verilmez.

Örneğin, 20 önceliğiyle bir iş parçacığının yalnızca 15 ile 20 arasında öncelikler olan bir iş parçacığı grubuyla etkileşimde bulunduğunu varsayalım. Kritik bölümleri sırasında 20 öncelikli iş parçacığı, önalım eşiğini 15 olarak ayarlayabilir, böylece etkileşime girdiği tüm iş parçacıklarından önalım önler. Bu, gerçekten önemli iş parçacıklarının (0 ve 14 arasındaki öncelikler), kritik bölüm işleme sırasında bu iş parçacığını hafiflemesine izin verir ve bu da daha fazla yanıt vermeye devam eder.

Tabii ki, önalım eşiğini 0 olarak ayarlayarak bir iş parçacığının tüm önalım devre dışı bırakılması yine de mümkündür. Ayrıca, önalım-Threshold, çalışma zamanı sırasında değiştirilebilir.

> [!NOTE]
> *Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.*

### <a name="priority-inheritance"></a>Öncelikli devralma

ThreadX, bu bölümün ilerleyen kısımlarında açıklanan mutex Hizmetleri içinde isteğe bağlı öncelik devralmayı da destekler. Öncelikli devralma, düşük öncelikli iş parçacığına ait olan bir mutex için bekleyen yüksek öncelikli bir iş parçacığının önceliğini geçici olarak kabul etmesine olanak tanır. Bu özellik, ara iş parçacığı önceliklerinin önalım ortadan kaldırarak, uygulamanın belirleyici olmayan öncelikli bir sürümden kaçınmanıza yardımcı olur. Kuşkusuz, *önalım-Threshold* , benzer bir sonuç elde etmek için kullanılabilir.

### <a name="thread-creation"></a>İş parçacığı oluşturma

Uygulama iş parçacıkları, başlatma sırasında veya diğer uygulama iş parçacıklarının yürütülmesi sırasında oluşturulur. Bir uygulama tarafından oluşturulabilen iş parçacığı sayısı için bir sınır yoktur.

### <a name="thread-control-block-tx_thread"></a>İş parçacığı denetim bloğu TX_THREAD

Her bir iş parçacığının özellikleri denetim bloğunda bulunur. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

Bir iş parçacığının denetim bloğu bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel yapıyı engellemesini sağlamak en yaygın olarak kullanılır.

Diğer alanlardaki denetim bloğunun bulunması, dinamik olarak ayrılan tüm bellekte olduğu gibi biraz daha dikkatli bir değer gerektirir. Bir denetim bloğu bir C işlevi içinde ayrılmışsa, onunla ilişkili bellek, çağıran iş parçacığının yığınının bir parçasıdır. Genel olarak, denetim blokları için yerel depolama kullanmaktan kaçının çünkü işlev dönmesinden sonra, başka bir iş parçacığının bir denetim bloğu için kullanıp kullanmadığını bağımsız olarak tüm yerel değişken yığın alanı serbest bırakılır.

Çoğu durumda, uygulama iş parçacığının denetim bloğunun içeriğine göre yükümlülüğü olur. Ancak, özellikle hata ayıklama sırasında bazı durumlar vardır, bu da bazı üyelere göz at yararlı olur. Daha kullanışlı denetim bloğu üyelerinden bazıları aşağıda verilmiştir.

**tx_thread_run_count** , iş parçacığının zamanlandığı birçok kez bir sayaç içerir. Artan bir sayaç, iş parçacığının zamanlandığını ve yürütüldüğünü belirtir.

**tx_thread_state** ilişkili iş parçacığının durumunu içerir. Aşağıdaki, olası iş parçacığı durumlarını listeler.

|  İş parçacığı durumu   | Değer |
| --------------- | ------ |
| TX_READY       | - |
| TX_COMPLETED   | 0x01 |
| TX_TERMINATED  | 0x02 şeklindedir |
| TX_SUSPENDED   | (0x03) |
| TX_SLEEP       | (0x04) |
| TX_QUEUE_SUSP | (0x05) |
| TX_SEMAPHORE_SUSP | (0x06) |
| TX_EVENT_FLAG   | (0x07) |
| TX_BLOCK_MEMORY | (0x08) |
| TX_BYTE_MEMORY  | 0x09 |
| TX_MUTEX_SUSP   | 0x0D |

> [!NOTE]
> *Tabii ki, yığın işaretçisi, saat dilimi değeri, öncelikler vb. dahil olmak üzere iş parçacığı denetim bloğunda çok sayıda ilginç alan vardır. Kullanıcılar denetim bloğu üyelerini incelemeye hoş geldiniz, ancak değişikliklere kesinlikle izin verilmez!*

> [!IMPORTANT]
> *Bu bölümde daha önce bahsedilen "yürütülüyor" durumu için bir eş yoktur. Belirli bir zamanda yalnızca bir çalışan iş parçacığı olduğundan bu gerekli değildir. Yürütülen iş parçacığının durumu da* **TX_READY**.

### <a name="currently-executing-thread"></a>Yürütülmekte olan Iş parçacığı

Daha önce bahsedildiği gibi, belirli bir zamanda yalnızca bir iş parçacığı yürütüyordur. Yürütülen iş parçacığını, isteği yapan iş parçacığına bağlı olarak belirlemenin birkaç yolu vardır.
Program kesimi, ***tx_thread_identify*** çağırarak yürütülen iş parçacığının denetim bloğu adresini alabilir. Bu, birden çok iş parçacığından yürütülen uygulama kodunun paylaşılan bölümlerinde yararlıdır.

Hata ayıklama oturumlarında, kullanıcılar iç ThreadX işaretçisini ***_tx_thread_current_ptr*** inceleyebilir. Şu anda yürütülmekte olan iş parçacığının denetim bloğu adresini içerir. Bu işaretçi NULL ise, uygulama iş parçacığı yürütülmüyor; Yani, ThreadX bir iş parçacığının hazırlanması için zamanlama döngüsünde bekliyor.

### <a name="thread-stack-area"></a>İş parçacığı yığın alanı

Her iş parçacığının en son yürütme ve derleyici kullanımı bağlamını kaydetmek için kendi yığınına sahip olması gerekir. Çoğu C derleyicileri, işlev çağrıları yapmak ve yerel değişkenleri geçici olarak ayırmak için yığın kullanır. Şekil 6 ' da tipik bir iş parçacığının yığını gösterilmektedir.

Bir iş parçacığı yığınının bellekte bulunduğu yer, uygulamaya göre yapılır. Yığın alanı, iş parçacığı oluşturma sırasında belirtilir ve hedefin adres alanının herhangi bir yerinden bulunabilir. Bu önemli bir özelliktir çünkü, yığınlarını yüksek hızlı RAM 'e yerleştirerek uygulamaların önemli iş parçacıklarının performansını artırmasına olanak tanır.

**Yığın bellek alanı** (örnek)

![Tipik Iş parçacığı yığını](./media/user-guide/typical-thread-stack.png)

**ŞEKIL 6. Tipik Iş parçacığı yığını**

Yığının ne kadar büyük olması, iş parçacıkları hakkında en sık sorulan sorulardan biridir. Bir iş parçacığının yığın alanı, en kötü durum işlevi çağrısı iç içe geçme, yerel değişken ayırma ve son yürütme bağlamını kaydetmeye yetecek kadar büyük olmalıdır.

Minimum yığın boyutu **TX_MINIMUM_STACK**, threadx tarafından tanımlanmıştır. Bu boyuttaki bir yığın, bir iş parçacığının bağlamını kaydetmeyi ve minimum işlev çağrısı sayısını ve yerel değişken ayırmayı destekler.

Ancak, çoğu iş parçacığı için, en düşük yığın boyutu çok küçük olur ve Kullanıcı, işlev çağrısı iç içe ve yerel değişken ayırmayı inceleyerek en kötü durum boyutu gereksinimini yoklamayı sağlamalıdır. Kuşkusuz, daha büyük bir yığın alanıyla başlamak her zaman daha iyidir.

Uygulamanın hataları ayıklandıktan sonra, bellek scarce ise iş parçacığı yığın boyutlarını ayarlamak mümkündür. Sık kullanılan bir yol, iş parçacıklarını oluşturmadan önce (0xEFEF) gibi kolay tanımlanabilir bir veri düzeniyle tüm yığın alanlarının önceden ayarlanmasıdır. Uygulama, Paces üzerinden tamamen gerçekleştirildikten sonra, yığın alanlarının ne kadar yığın kullandığını görmek için veri deseninin hala bozulmakta olduğu yığının alanını buluyor. Şekil 7 ' de, tam iş parçacığı yürütme sonrasında 0xEFEF için bir yığın ön ayarı gösterilmektedir.

**Yığın bellek alanı** (başka bir örnek)

![0xEFEF * için yığın önayarı](./media/user-guide/stack-preset.png)

**ŞEKIL 7. Yığın önayarı 0xEFEF**

> [!IMPORTANT]
> *Varsayılan olarak, ThreadX her bir iş parçacığı yığınının her baytını bir 0xEF değeri ile başlatır.*

### <a name="memory-pitfalls"></a>Bellek sınırları

İş parçacıkları için yığın gereksinimleri büyük olabilir. Bu nedenle, uygulamayı makul sayıda iş parçacığına sahip olacak şekilde tasarlamak önemlidir. Ayrıca, iş parçacıkları içinde aşırı yığın kullanımını önlemek için bazı dikkatli olunmalıdır. Özyinelemeli algoritmalar ve büyük yerel veri yapıları önlenmelidir.

Çoğu durumda, taşan bir yığın, iş parçacığı yürütmesinin yığın alanının bitişik (genellikle daha önce) bellek alanına ayrılmasına neden olur. Sonuçlar tahmin edilemez, ancak çoğu zaman program sayacında doğal olmayan bir değişikliğe neden olur. Bu, genellikle "Weeds 'e atlama" olarak adlandırılır. Kuşkusuz, bunu önlemenin tek yolu tüm iş parçacığı yığınlarının yeterince büyük olmasını sağlamaktır.

### <a name="optional-run-time-stack-checking"></a>İsteğe bağlı çalışma zamanı yığın denetimi

ThreadX, çalışma zamanı sırasında her bir iş parçacığının yığınını bozulma için denetleme olanağı sağlar. Varsayılan olarak, ThreadX, oluşturma sırasında bir 0xEF veri düzeniyle iş parçacığı yığınlarının her baytını doldurur. Uygulama, ThreadX kitaplığını tanımlı **TX_ENABLE_STACK_CHECKING** ile oluşturmazsa, threadx her iş parçacığının yığınını, askıya alındığından veya sürdürüldüğünde bozulma için inceler. Yığın bozulması algılanırsa, ThreadX, uygulamanın yığın hata işleme yordamını tx_thread_stack_error_notify _ çağrısıyla belirtilen şekilde çağırır ***. Aksi halde, yığın hata işleyicisi belirtilmemişse, ThreadX iç _* _ _tx_thread_stack_error_handler_ yordamını çağırır** .

### <a name="reentrancy"></a>Yeniden giriş

Çoklu iş parçacıklı gerçek Beauties biri aynı C işlevinin birden çok iş parçacığından çağrılabilir olması olabilir. Bu harika bir güç sağlar ve ayrıca kod alanını azaltmaya yardımcı olur. Ancak, birden çok iş parçacığından çağrılan C işlevlerinin *yeniden kullanılabilir olmasını* gerektirir.

Temel olarak, bir yeniden alan işlevi çağıranın dönüş adresini geçerli yığında depolar ve daha önce ayarlamış olduğu genel veya statik C değişkenlerine bağlı değildir. Çoğu derleyiciler, dönüş adresini yığına yerleştirir. Bu nedenle, uygulama geliştiricileri yalnızca *genel* ve *statiklerin* kullanımı konusunda endişelenmelidir.

Standart C Kitaplığı 'nda bulunan ***strtok*** dize belirteci, yeniden yer olmayan bir işleve bir örnektir. Bu işlev, sonraki çağrılarındaki önceki dize işaretçisini "anımsar". Bunu bir statik dize işaretçisi ile yapar. Bu işlev birden çok iş parçacığından çağrılırsa, büyük olasılıkla geçersiz bir işaretçi döndürür.

### <a name="thread-priority-pitfalls"></a>İş parçacığı önceliği sınırları

İş parçacığı önceliklerinin seçilmesi, çoklu iş parçacığı oluşturma 'nın en önemli özelliklerinden biridir. Çalışma zamanı sırasında tam olarak gerekli olanları belirlemek yerine, algılanan iş parçacığı önem derecesine göre öncelikler atamak çok önemlidir. İş parçacığı önceliklerinin kötüye kullanılması, diğer iş parçacıklarını gerçekleştirebilir, öncelik sürümü oluşturabilir, işlem bant genişliğini azaltabilir ve uygulamanın çalışma zamanı davranışını anlamayı zorlaştırır.

Daha önce bahsedildiği gibi, ThreadX, öncelik temelli bir preemptive zamanlama algoritması sağlar. Düşük öncelikli iş parçacıkları, yürütmeye yönelik daha yüksek öncelikli iş parçacığı kalmayana kadar yürütülmez. Daha yüksek öncelikli iş parçacığı her zaman hazırsa, düşük öncelikli iş parçacıkları hiçbir zaman yürütülmez. Bu koşul, *iş parçacığı başlangıçadı* olarak adlandırılır.

Çoğu iş parçacığı sorunu hata ayıklamada erken algılanır ve daha yüksek öncelikli iş parçacıklarının sürekli yürütülmeyeceğinden çözülebilirler. Alternatif olarak, yürütme şansı alınana kadar, mantıksal olarak yürütülen iş parçacıklarının önceliğini kademeli olarak başlatan uygulamaya de bir mantık eklenebilir.

İş parçacığı öncelikleriyle ilişkili başka bir *giriş ise öncelikli bir sürümdür*. Düşük öncelikli bir iş parçacığında gerekli bir kaynak olduğundan, yüksek öncelikli bir iş parçacığı askıya alındığında öncelik Inversion gerçekleşir. Kuşkusuz, bazı örneklerde, farklı öncelikteki iki iş parçacığının ortak bir kaynağı paylaşması gerekir. Bu iş parçacıkları etkin tek bir sürümse, öncelik Inversion saati, düşük öncelikli iş parçacığı kaynağı tutan zamana göre sınırlanır. Bu koşul hem belirleyici hem de oldukça normaldir. Bununla birlikte, bu öncelik geçersiz kılma sırasında ara öncelikteki iş parçacıkları etkin hale gelirse, öncelik Inversion süresi artık belirleyici değildir ve bir uygulama hatasına neden olabilir.

ThreadX 'te belirleyici olmayan öncelikli öncelikli sürümü önlemek için önemli ölçüde üç farklı yöntem vardır. İlk olarak, uygulama önceliği seçimleri ve çalışma zamanı davranışı, öncelik sürümü sorununun önlenebilmesini sağlayacak şekilde tasarlanabilir. İkincisi, daha yüksek öncelikli iş parçacıklarıyla kaynakları paylaştıklarında, daha düşük öncelikli iş parçacıkları *önalım eşiğini* kullanarak ara iş parçacıklarından önalım 'i engelleyebilir. Son olarak, sistem kaynaklarını korumak için ThreadX mutex nesnelerini kullanan iş parçacıkları, belirleyici olmayan öncelikli bir sürümü ortadan kaldırmak için isteğe bağlı mutex *önceliği devrmasından* yararlanabilir.

### <a name="priority-overhead"></a>Öncelik ek yükü

Çoklu iş parçacığı içindeki ek yükü azaltmanın en fazla belirgin yolu, bağlam anahtarlarının sayısını azaltmaktır. Daha önce belirtildiği gibi, daha yüksek öncelikli bir iş parçacığının yürütülmesi yürütülen iş parçacığının üzerinde daha kırmızıysa bir bağlam anahtarı oluşur. Yüksek öncelikli iş parçacıklarının, hem dış olayların (kesmeler gibi) hem de yürütülen iş parçacığı tarafından yapılan hizmet çağrılarının bir sonucu olarak hazırlanabileceğini bahsetmek çok önemlidir.

Efekt iş parçacığı önceliklerinin bağlam anahtarı ek yükü üzerinde olduğunu göstermek için, *thread_1*, *thread_2* ve *thread_3* adlı iş parçacıklarından oluşan üç iş parçacığı ortamı olduğunu varsayalım. Tüm iş parçacıklarının bir ileti bekleyen askıya alınma durumunda olduğunu varsayalım. Thread_1 bir ileti aldığında, bunu hemen thread_2 gönderir. Thread_2 sonra iletiyi thread_3 iletir. Thread_3 yalnızca iletiyi atar. Her iş parçacığı iletisini tamamladıktan sonra, geri döner ve başka bir ileti bekler.

Bu üç iş parçacığını yürütmek için gereken işlem önceliklerinden büyük ölçüde farklılık gösterir. Tüm iş parçacıkları aynı önceliğe sahip ise, her iş parçacığının yürütülmesinden önce tek bir bağlam anahtarı oluşur. Bağlam anahtarı, her iş parçacığı boş bir ileti kuyruğu üzerinde askıya aldığında oluşur.

Ancak, thread_2 thread_1 kıyasla daha yüksek önceliktir ve thread_3 thread_2 kıyasla daha yüksek önceliktir, bağlam anahtarlarının sayısı iki katına çıkar. Bunun nedeni, daha yüksek öncelikli bir iş parçacığının artık hazır olduğunu algıladığında *tx_queue_send* hizmetinin içinde başka bir bağlam anahtarının gerçekleşmesinden kaynaklanır.

ThreadX önalım-Threshold mekanizması, bu ek bağlam anahtarlarından kaçınabilir ve yine de yukarıda bahsedilen öncelik seçimlerini sağlayabilir. Zamanlama sırasında birkaç iş parçacığı önceliklerinin sağladığından bu önemli bir özelliktir, ancak aynı zamanda iş parçacığı yürütme sırasında aralarında bazı istenmeyen bağlamla geçiş yapmayı ortadan kaldırır.

### <a name="run-time-thread-performance-information"></a>Çalışma zamanı Iş parçacığı performans bilgileri

ThreadX isteğe bağlı çalışma zamanı iş parçacığı performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış **TX_THREAD_ENABLE_PERFORMANCE_INFO** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

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

Bu bilgiler, ***tx_thread_performance_info_get** _ ve _ *_tx_thread_performance_system_info_get_* * Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. İş parçacığı performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda hizmet çağrısı preemptions iş parçacığının önceliğini önerebilir ve/veya önalım eşiği çok düşüktür. Ayrıca, görece düşük sayıda boşta sistem döndürmesi, daha düşük öncelikli iş parçacıklarının yeterince askıya alınması önerisinde bulunabilir.

### <a name="debugging-pitfalls"></a>Hata ayıklama sınırları

Birden çok iş parçacığından aynı program kodu yürütülemediğinden çok iş parçacıklı uygulamalarda hata ayıklama biraz daha zordur. Böyle durumlarda, bir kesme noktası tek başına yeterli olmayabilir. Hata ayıklayıcı, çağıran iş parçacığının hata ayıklaması için bir tane olup olmadığını görmek üzere bir koşullu kesme noktası kullanarak geçerli iş parçacığı işaretçisini **_tx_thread_current_ptr** de görüntülemesi gerekir.

Bunun çoğu, çeşitli geliştirme aracı satıcıları aracılığıyla sunulan çoklu iş parçacıklı destek paketlerinde işlenir. Basit tasarımı nedeniyle, ThreadX 'i farklı geliştirme araçlarıyla tümleştirmek oldukça kolaydır.

Yığın boyutu her zaman çoklu iş parçacığı oluşturma konusunun önemli bir hata ayıklama konusu. Açıklanamayan davranış gözlemlendiğinde, genellikle her iş parçacığı için yığın boyutlarını artırmak iyi bir ilk tahmindir; özellikle de son iş parçacığının yığın boyutu.

> [!TIP]
> *Ayrıca, **TX_ENABLE_STACK_CHECKING** tanımlı olan threadx kitaplığını oluşturmak iyi bir fikirdir. Bu, yığın bozulması sorunlarını işleme mümkün olduğunca erken yalıtmak için yardımcı olur.*

## <a name="message-queues"></a>İleti kuyrukları

İleti kuyrukları, ThreadX 'de iş parçacıkları arası iletişimin birincil yöntemidir. Bir veya daha fazla ileti bir ileti kuyruğunda bulunabilir. Tek bir iletiyi tutan bir ileti kuyruğu genellikle *posta kutusu* olarak adlandırılır.

İletiler bir kuyruğa ***tx_queue_send** _ tarafından kopyalanır ve _ *_tx_queue_receive_* * tarafından bir kuyruktan kopyalanır. Bunun tek istisnası, boş bir kuyruktaki bir ileti beklenirken bir iş parçacığının askıya alındığı durumdur. Bu durumda, sıraya gönderilen sonraki ileti, iş parçacığının hedef alanına doğrudan yerleştirilir.

Her ileti kuyruğu ortak bir kaynaktır. ThreadX, ileti sıralarının nasıl kullanıldığına ilişkin bir kısıtlama yoktur.

### <a name="creating-message-queues"></a>Ileti kuyrukları oluşturma

İleti kuyrukları, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Bir uygulamadaki ileti kuyruğu sayısı için bir sınır yoktur.

### <a name="message-size"></a>İleti boyutu

Her ileti kuyruğu, bir dizi sabit boyutlu iletiyi destekler. Kullanılabilir ileti boyutları, dahil olmak üzere 1 ile 16 32 bitlik sözcüklerdir. İleti boyutu, sıra oluşturulduğunda belirtilir. 16 sözcükten daha büyük uygulama iletilerinin işaretçiden geçirilmesi gerekir. Bu, 1 sözcük boyutuna sahip bir sıra (bir işaretçiyi tutmak için yeterli) ve ardından ileti işaretçilerini tüm ileti yerine gönderip alarak gerçekleştirilir.

### <a name="message-queue-capacity"></a>İleti sırası kapasitesi

Bir kuyruğun tutabilecek ileti sayısı, ileti boyutunun bir işlevidir ve oluşturma sırasında sağlanan bellek alanının boyutudur. Kuyruğun toplam ileti kapasitesi, her iletideki bayt sayısı, sağlanan bellek alanındaki toplam bayt sayısına bölünerek hesaplanır.

Örneğin, 100 baytlık bir bellek alanı ile 1 32 bitlik bir sözcüğün (4 bayt) ileti boyutunu destekleyen bir ileti kuyruğu oluşturulduysa, kapasitesi 25 mesaj olur.

### <a name="queue-memory-area"></a>Kuyruk belleği alanı

Daha önce belirtildiği gibi, ileti arabelleğe alma bellek alanı sıra oluşturma sırasında belirtilir. ThreadX içindeki diğer bellek alanları gibi, hedefin adres alanında herhangi bir yerde bulunabilir.

Bu önemli bir özelliktir çünkü uygulamanın önemli ölçüde esnekliğini sağlar. Örneğin, bir uygulama performansı artırmak için yüksek hızda RAM 'teki önemli bir kuyruğun bellek alanını bulabilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Bir kuyruktan ileti gönderilmeye ya da almaya çalışırken uygulama iş parçacıkları askıya alabilir. Genellikle, iş parçacığı askıya alma, boş bir kuyruktan ileti bekletmeyi içerir. Ancak, bir iş parçacığının bir iletiyi tam sıraya gönderme girişimi de askıya alınması mümkündür.

Askıya alma koşulu çözümlendikten sonra, istenen hizmet tamamlanır ve bekleyen iş parçacığı sürdürülür. Aynı sırada birden çok iş parçacığı askıya alınırsa, bunlar askıya alındığı sırada sürdürülür (FıFO).

Ancak, uygulama, iş parçacığı askıya alma işlemi için kuyruğa alma hizmeti 'nden önce ***tx_queue_prioritize*** çağırdığında öncelik sürdürme de mümkündür. Sıra önceliği belirleme hizmeti, en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar, diğer tüm askıya alınan iş parçacıklarını aynı FıFO sırasıyla bırakır.

Zaman aşımları tüm sıra getirilmesi için de kullanılabilir. Temel olarak bir zaman aşımı, iş parçacığının askıya alınmayacak en fazla Zamanlayıcı sayısını belirtir. Bir zaman aşımı oluşursa, iş parçacığı sürdürülür ve hizmet uygun hata kodu ile birlikte geri döner.

### <a name="queue-send-notification"></a>Kuyruk gönderme bildirimi

Bazı uygulamalar, bir sıraya her ileti yerleştirildiğinde bildirim almak için bu avantaja sahip olabilir. ThreadX, ***tx_queue_send_notify*** hizmeti aracılığıyla bu yeteneği sağlar. Bu hizmet belirtilen sıraya sahip sağlanan uygulama bildirimi işlevini kaydeder. Daha sonra ThreadX, kuyruğa her ileti gönderildiğinde bu uygulama bildirim işlevini çağırır. Uygulama bildirim işlevi içindeki tam işlem uygulama tarafından belirlenir; Bununla birlikte, genellikle yeni iletiyi işlemek için uygun iş parçacığını sürdürmeden oluşur.

### <a name="queue-event-chainingtrade"></a>Olay zincirlemesini sıraya al&trade;

ThreadX içindeki bildirim özellikleri, çeşitli eşitleme olaylarını birbirine zincirlemek için kullanılabilir. Bu, genellikle tek bir iş parçacığının birden çok eşitleme olayını işlemesi gerektiğinde faydalıdır.

Örneğin, tek bir iş parçacığının beş farklı kuyruktan gelen iletileri işlemekten sorumlu olduğunu ve kullanılabilir bir ileti olmadığında da askıya alınması gerektiğini varsayalım. Bu, her sıra için bir uygulama bildirim işlevi kaydederek ve ek bir sayma semaforu ile kolayca gerçekleştirilir. Özellikle, uygulama bildirim işlevi çağrıldığında bir *tx_semaphore_put* gerçekleştirir (semafor sayısı, beş kuyrumdan gelen toplam ileti sayısını temsil eder). İşleme iş parçacığı, *tx_semaphore_get* hizmeti aracılığıyla bu semaforda askıya alınır. Semafor kullanılabilir olduğunda (Bu durumda, bir ileti kullanılabilir olduğunda!), işleme iş parçacığı sürdürülür. Ardından bir ileti için her kuyruğu birbirine kullanır, bulunan iletiyi işler ve sonraki iletiyi beklemek için başka bir ***tx_semaphore_get*** gerçekleştirir. Bunu olay zincirleme olmadan yapmak oldukça zordur ve büyük olasılıkla daha fazla iş parçacığı ve/veya ek uygulama kodu gerektirir.

Genel olarak, *olay zincirleme* daha az iş parçacığı, daha az ek yük ve daha küçük RAM gereksinimlerine neden olur. Ayrıca, daha karmaşık sistemlerin eşitleme gereksinimlerini işlemek için yüksek düzeyde esnek bir mekanizma sağlar.

### <a name="run-time-queue-performance-information"></a>Çalışma zamanı sıra performans bilgileri
ThreadX isteğe bağlı çalışma zamanı sıra performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış ***TX_QUEUE_ENABLE_PERFORMANCE_INFO*** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

Genel sistem için toplam sayı:

  - gönderilen iletiler

  - alınan iletiler

  - kuyruk boş getirilmesi

  - sıra Full getirilmesi

  - Tam sıra hatası döndürür (askıya alma belirtilmemiş)

  - sıra zaman aşımları

Her kuyruğun toplam sayısı:

  - gönderilen iletiler

  - alınan iletiler

  - kuyruk boş getirilmesi

  - sıra Full getirilmesi

  - Tam sıra hatası döndürür (askıya alma belirtilmemiş)

  - sıra zaman aşımları

Bu bilgiler, ***tx_queue_performance_info_get** _ ve _ *_tx_queue_performance_system_info_get_* * Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. Sıra performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda "Queue Full getirilmesi", kuyruk boyutunun artışına bir artış önerisinde bulunabilir.

### <a name="queue-control-block-tx_queue"></a>Sıra denetim bloğu TX_QUEUE

Her ileti sırasının özellikleri denetim bloğunda bulunur. Kuyruktaki ileti sayısı gibi ilginç bilgiler içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

İleti kuyruğu denetim blokları ayrıca bellekte herhangi bir yerde bulunabilir, ancak her bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak en yaygın olarak kullanılır.

### <a name="message-destination-pitfall"></a>İleti hedefi gizli

Daha önce belirtildiği gibi, iletiler kuyruk alanı ve uygulama veri alanı arasında kopyalanır. Alınan bir iletinin hedefinin tüm iletiyi tutabilecek kadar büyük olduğundan emin olmak önemlidir. Aksi takdirde, ileti hedefini izleyen bellek muhtemelen bozulmuş olur.

> [!NOTE]
> *Bu, yığında çok küçük bir ileti hedefi olduğunda (bir işlevin dönüş adresini bozmaya benzer bir şey), özellikle de oldukça zaman alır!*

## <a name="counting-semaphores"></a>Semafor sayma

ThreadX, 0 ile 4.294.967.295 arasında değer olarak kullanılan 32 bitlik sayım semaforları sağlar. Semaforları saymak için iki işlem vardır: *tx_semaphore_get* ve *tx_semaphore_put*. Get işlemi semaforu bir azaltır. Semafor 0 ise, get işlemi başarılı olmaz. Get işleminin tersi, put işlemidir.
Semaforu bir tane artırır.

Her sayım semaforu ortak bir kaynaktır. ThreadX, sayım semaforlarıyla ilgili hiçbir kısıtlama vermez.

Sayım semaforları genellikle *karşılıklı dışlama* için kullanılır. Ancak, sayım semaforları olay bildirimi için bir yöntem olarak da kullanılabilir.

### <a name="mutual-exclusion"></a>Karşılıklı dışlama

 Karşılıklı dışlama, iş parçacıklarının belirli uygulama bölümlerine erişimini denetlemeyle ilgilidir ( *kritik bölümler* veya *uygulama kaynakları* da denir). Karşılıklı dışlama için kullanıldığında, semaforun "geçerli sayısı", erişim izni verilen toplam iş parçacığı sayısını temsil eder. Çoğu durumda, karşılıklı dışlama için kullanılan sayım Semaforlar ilk değeri 1 olur, yani yalnızca bir iş parçacığının aynı anda ilişkili kaynağa erişebileceği anlamına gelir. Yalnızca 0 veya 1 değerlerine sahip olan Semaforlar genellikle *ikili Semaforlar* olarak adlandırılır.

> [!IMPORTANT]
> *Bir ikili semafor kullanılıyorsa, kullanıcının sahip olduğu bir semaforda aynı iş parçacığının bir get işlemi gerçekleştirmesini önlemesi gerekir. İkinci bir get başarısız olur ve çağıran iş parçacığının sınırsız şekilde askıya alınmasına ve kaynağın kalıcı olmamasından oluşmasına neden olabilir.*

### <a name="event-notification"></a>Olay bildirimi

Ayrıca, bir üretici TÜKETİCİSİNDE bir olay bildirimi olarak sayma semaforları kullanmak da mümkündür. Üretici, her şey kullanılabilir olduğunda semaforu artırırken, Kullanıcı sayma semaforu almayı dener. Bu tür Semaforlar genellikle 0 ' ın başlangıç değerine sahiptir ve üretici tüketiciye hazırlanmaya bir şey yapana kadar artmaz. Olay bildirimi için kullanılan Semaforlar ***tx_semaphore_ceiling_put*** hizmeti çağrısının kullanımı da avantajlı olabilir. Bu hizmet, semafor sayısının çağrıda sağlanan değeri hiçbir şekilde aşmamasını sağlar.

### <a name="creating-counting-semaphores"></a>Sayım semaforları oluşturma

Sayım semaforları, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Semaforun ilk sayısı oluşturma sırasında belirtilir. Bir uygulamadaki sayım semaforları sayısı için bir sınır yoktur.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Geçerli 0 sayısı ile bir semafor üzerinde alma işlemi gerçekleştirmeye çalışırken uygulama iş parçacıkları askıya alabilir.

Bir put işlemi gerçekleştirildikten sonra, askıya alınan iş parçacığının alma işlemi gerçekleştirilir ve iş parçacığı sürdürülür. Aynı sayım semaforu üzerinde birden çok iş parçacığı askıya alınırsa, bunlar askıya alındıkları sırada sürdürülür (FıFO).

Ancak, uygulama iş parçacığı askıya alma çağrısından önce tx_semaphore_prioritize, uygulamanın semafor put çağrısından önce  , öncelik sürdürme de mümkündür. Semafor öncelik sıralaması hizmeti, en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar, diğer tüm askıya alınan iş parçacıklarını aynı FıFO sırasıyla bırakır.

### <a name="semaphore-put-notification"></a>Semafor put bildirimi

Bazı uygulamalar, bir semafor her gerçekleştiğinde bildirimde bulunulmaya yönelik avantajın olduğunu fark edebilir. ThreadX, ***tx_semaphore_put_notify*** hizmeti aracılığıyla bu yeteneği sağlar. Bu hizmet, belirtilen semafor ile sağlanan uygulama bildirimi işlevini kaydeder. Artık ThreadX, semafor her gerçekleştiğinde bu uygulama bildirim işlevini çağırır. Uygulama bildirim işlevi içindeki tam işlem uygulama tarafından belirlenir; Bununla birlikte, genellikle yeni semafor put olayını işlemek için uygun iş parçacığını sürdürmeden oluşur.

### <a name="semaphore-event-chainingtrade"></a>Semafor olay zinciri&trade;

ThreadX içindeki bildirim özellikleri, çeşitli eşitleme olaylarını birbirine zincirlemek için kullanılabilir. Bu, genellikle tek bir iş parçacığının birden çok eşitleme olayını işlemesi gerektiğinde faydalıdır.

Örneğin, bir kuyruk iletisi, olay bayrakları ve semafor için ayrı iş parçacıkları askıya almak yerine, uygulama her nesne için bir bildirim yordamı kaydedebilir. Çağrıldığında, uygulama bildirimi yordamı tek bir iş parçacığını sürdürür, bu da her bir nesneye sorgulanamıyor, bu da yeni olayı bulup işleyebilir.

Genel olarak, *olay zincirleme* daha az iş parçacığı, daha az ek yük ve daha küçük RAM gereksinimlerine neden olur. Ayrıca, daha karmaşık sistemlerin eşitleme gereksinimlerini işlemek için yüksek düzeyde esnek bir mekanizma sağlar.

### <a name="run-time-semaphore-performance-information"></a>Çalışma zamanı semaforu performans bilgileri

ThreadX isteğe bağlı çalışma zamanı semaforu performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

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

Bu bilgiler, ***tx_semaphore_performance_info_get** _ ve _ *_tx_semaphore_performance_system_info_get_* * Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. Semafor performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda "semafor Get zaman aşımları", diğer iş parçacıklarının kaynakları çok uzun süre olarak tuttuklarından kaynaklanabilir.

### <a name="semaphore-control-block-tx_semaphore"></a>Semafor denetim bloğu TX_SEMAPHORE

Her sayım semaforun özellikleri denetim bloğunda bulunur. Geçerli semafor sayısı gibi bilgileri içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

Semafor denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

### <a name="deadly-embrace"></a>Dar küme

Karşılıklı dışlama için kullanılan semaforlarla ilişkili en ilgi çekici ve tehlikeli her bir tane, büyük *küme ayracı* olur. , *Bir veya daha* fazla iş parçacığının, birbirini zaten sahip olan Semaforlar alınmaya çalışılırken süresiz olarak askıya alındığı bir durumdur.

Bu koşul en iyi iki iş parçacığı, iki semafor örneği tarafından gösterilmiştir. İlk iş parçacığının ilk semafora sahip olduğunu ve ikinci iş parçacığının ikinci semafora sahip olduğunu varsayalım. İlk iş parçacığı ikinci semaforu almayı denerse ve ikinci iş parçacığı ilk semaforu almaya çalışırsa, her iki iş parçacığı de bir kilitlenme koşulu girer. Ayrıca, bu iş parçacıkları sonsuza kadar askıya alınırsa, ilişkili kaynakları da süresiz olarak kilitlenir. Şekil 8 ' de bu örnek gösterilmektedir.

**Dar** (örnek)

![Askıya alınan Iş parçacıkları örneği](./media/user-guide/example-suspended-threads.png)

**ŞEKIL 8. Askıya alınan Iş parçacıkları örneği**

Gerçek zamanlı sistemler için, iş parçacıklarının Semaforlar tarafından nasıl elde edileceği hakkında bazı kısıtlamalar yerleştirilerek, kilitlenmeleri engellenebilir. İş parçacıkları tek seferde yalnızca bir semafora sahip olabilir. Alternatif olarak, iş parçacıkları bunları aynı sırada topladıklarında birden fazla semafora sahip olabilir. Önceki örnekte, ilk ve ikinci semaforu sırayla ilk ve ikinci semaforu elde alıyorsa, bu, geçersiz ayraç engellenir.

> [!TIP]
> *Ayrıca, bir küme ayracından kurtarmak üzere alma işlemiyle ilişkili askıya alma zaman aşımını kullanmak da mümkündür.*

### <a name="priority-inversion"></a>Öncelikli Inversion

Karşılıklı dışlama semaforları ile ilişkili başka bir giriş de öncelikli bir sürümdür. Bu konu, "[Iş parçacığı önceliği](#thread-priority-pitfalls)konusundaki" bölümünde daha ayrıntılı olarak ele alınmıştır.

Temel sorun, düşük öncelikli bir iş parçacığının daha yüksek öncelikli iş parçacığı gerektiren bir semafora sahip olduğu bir durumdan kaynaklanır. Bu, normal bir. Bununla birlikte, aralarında önceliklere sahip olan iş parçacıkları öncelik inen son kararlı olmayan bir süreye neden olabilir. Bu, iş parçacığı önceliklerinin dikkatli bir şekilde seçilebileceği, önalım-Threshold kullanılarak işlenebilir ve kaynağın sahibi olan iş parçacığının önceliği yüksek öncelikli iş parçacığından daha geçici olarak oluşturulur.

## <a name="mutexes"></a>Zaman Uyumu Sağlayıcılar

Semafora ek olarak, ThreadX bir mutex nesnesi de sağlar. Bir mutex, temelde bir iş parçacığının tek seferde bir mutex 'e sahip olabileceği anlamına gelen bir ikili semafor olur. Ayrıca, aynı iş parçacığı, sahip olunan bir mutex üzerinde başarılı bir mutex Get işlemini birden çok kez gerçekleştirebilir, 4.294.967.295 tam olarak olur. Mutex nesnesinde iki işlem vardır: ***tx_mutex_get** _ ve _ *_tx_mutex_put_* *. Get işlemi, başka bir iş parçacığına ait bulunmayan bir mutex edinir, PUT işlemi daha önce edinilen bir mutex 'i serbest bırakır. Bir mutex 'i serbest bırakmak için bir iş parçacığında, put işlemlerinin sayısı önceki Get işlemlerinin sayısına eşit olmalıdır.

Her Mutex ortak bir kaynaktır. ThreadX, zaman uyumu sağlayıcılar için kullanım kısıtlamaları yoktur.

ThreadX *mukapsamalarla yalnızca karşılıklı dışlama* için kullanılır. Sayma semaforlarından farklı olarak, zaman uyumu sağlayıcılar olay bildirimi için bir yöntem olarak kullanılamaz.

### <a name="mutex-mutual-exclusion"></a>Mutex karşılıklı dışlaması

Sayım semaforu bölümündeki tartışmaya benzer şekilde, karşılıklı dışlama, iş parçacıklarının belirli uygulama bölgelerine erişimini denetlemeyle ( *kritik bölümler* veya *uygulama kaynakları* olarak da bilinir) ilgilidir. Kullanılabilir olduğunda, bir ThreadX mutex 'in sahiplik sayısı 0 olur. Mutex bir iş parçacığı tarafından alındıktan sonra, mutex üzerinde gerçekleştirilen başarılı alma işlemleri için bir kez, her başarılı Put işlemi için azaltılır.

### <a name="creating-mutexes"></a>Birbirini kapsamayan oluşturma

ThreadX muizlik, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Bir mutex 'in ilk koşulu her zaman "kullanılabilir" dır. Ayrıca, *Öncelik devralma* seçili olarak bir mutex oluşturulabilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Uygulama iş parçacıkları, zaten başka bir iş parçacığına ait olan bir mutex üzerinde alma işlemi gerçekleştirmeye çalışırken askıya alabilir.

Sahip iş parçacığı tarafından aynı sayıda Put işlemi gerçekleştirildikten sonra, askıya alınan iş parçacığının alma işlemi gerçekleştirilir, bu da mutex 'in sahipliğini verir ve iş parçacığı sürdürülür. Aynı mutex üzerinde birden fazla iş parçacığı askıya alınırsa, bunlar askıya alındığı sırada sürdürülür (FıFO).

Ancak, bir öncelik sürdürme, oluşturma sırasında mutex önceliği devralımı seçildiyse otomatik olarak yapılır. Uygulama, iş parçacığı askıya alma çağrısını askıya alan mutex put çağrısından önce ***tx_mutex_prioritize*** çağırdığında öncelik sürdürme de mümkündür. Mutex öncelik sıralaması hizmeti, en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar, diğer tüm askıya alınan iş parçacıklarını aynı FıFO sırasıyla bırakır.

### <a name="run-time-mutex-performance-information"></a>Çalışma zamanı mutex performans bilgileri

ThreadX isteğe bağlı çalışma zamanı mutex performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış **TX_MUTEX_ENABLE_PERFORMANCE_INFO** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

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

Bu bilgiler, ***tx_mutex_performance_info_get** _ ve _ *_tx_mutex_performance_system_info_get_* * Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. Mutex performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda "mutex Get zaman aşımları", diğer iş parçacıklarının kaynakları çok uzun tuttuklarından kaynaklanabilir.

### <a name="mutex-control-block-tx_mutex"></a>Mutex denetim bloğu TX_MUTEX

Her bir mutex 'in özellikleri denetim bloğunda bulunur. Mutex sahibi olan iş parçacığının işaretçisi ile birlikte geçerli mutex sahiplik sayısı gibi bilgileri içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır. Mutex denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

### <a name="deadly-embrace"></a>Dar küme

Mutex sahipliğiyle ilişkili en ilgi çekici ve tehlikeli her bir tane, büyük *küme ayracı* olur. Bir veya daha fazla iş parçacığının, diğer iş parçacıklarından zaten sahip olan bir mutex alınmaya çalışılırken *süresiz olarak askıya* alındığı bir durumdur. Geçersiz kılmadan *ve düzeltmelerinin* tartışılması, mutex nesnesi için de tamamen geçerlidir.

### <a name="priority-inversion"></a>Öncelikli Inversion

Daha önce belirtildiği gibi, karşılıklı dışlamaya ilişkin büyük bir ana hat öncelik Inversion olur. Bu konu, "[Iş parçacığı önceliği](#thread-priority-pitfalls)konusundaki" bölümünde daha ayrıntılı olarak ele alınmıştır.

Temel sorun, düşük öncelikli bir iş parçacığının daha yüksek öncelikli iş parçacığı gerektiren bir semafora sahip olduğu bir durumdan kaynaklanır. Bu, normal bir. Bununla birlikte, aralarında önceliklere sahip olan iş parçacıkları öncelik inen son kararlı olmayan bir süreye neden olabilir. Daha önce tartışılan Semaforlardan farklı olarak, ThreadX mutex nesnesi isteğe bağlı *öncelikli devralıma* sahiptir Öncelikli mirasın arkasındaki temel düşünce, düşük öncelikli bir iş parçacığının önceliği geçici olarak, düşük öncelikli iş parçacığına ait olan aynı mutex 'i isteyen yüksek öncelikli bir iş parçacığının önceliği olarak yükseltilir. Düşük öncelikli iş parçacığı mutex 'i serbest bıraktığında, özgün önceliği geri yüklenir ve daha yüksek öncelikli iş parçacığına mutex 'in sahipliği verilir. Bu özellik, düşük öncelikli iş parçacığının mutex 'i tuttuğu zamana kadar Inversion miktarı arasında sınırlama yaparak belirleyici olmayan öncelikli sürümü ortadan kaldırır. Tabii ki, bu bölümde daha önce ele alınan önemli olmayan öncelik Inversion 'ı ele almak için bahsedilen teknikler de de aynı zamanda zaman uyumu sağlayıcılar ile de geçerlidir.

## <a name="event-flags"></a>Olay bayrakları

Olay bayrakları, iş parçacığı eşitlemesi için güçlü bir araç sağlar. Her olay bayrağı tek bir bit ile temsil edilir. Olay bayrakları 32 gruplar halinde düzenlenir. İş parçacıkları bir gruptaki tüm 32 olay bayraklarıyla aynı anda çalışabilir. Olaylar ***tx_event_flags_set** _ tarafından ayarlanır ve _ *_tx_event_flags_get_* * tarafından alınır.

Olay bayraklarını ayarlama, geçerli olay bayrakları ve yeni olay bayrakları arasındaki mantıksal bir ve/veya işlemle yapılır. ***Tx_event_flags_set*** çağrısında mantıksal işlemin türü (bir ve veya veya ya da) belirtilir.

Olay bayraklarının alınması için benzer mantıksal seçenekler vardır. Get isteği, belirtilen tüm olay bayraklarının gerektiğini (mantıksal ve) belirtebilir.

Alternatif olarak, bir get isteği, belirtilen olay bayraklarının herhangi birinin isteği (mantıksal veya) yerine getireceğini belirtebilir. Olay bayrakları almayla ilişkili mantıksal işlemin türü ***tx_event_flags_get*** çağrısında belirtilmiştir.

> [!IMPORTANT]
> *Bir get isteğini karşılayan olay bayrakları* , *istek tarafından* **TX_OR_CLEAR** *veya* **TX_AND_CLEAR** belirtilmişse, yani sıfır olarak ayarlanır.

Her olay bayrakları grubu, ortak bir kaynaktır. ThreadX, olay bayrakları gruplarının nasıl kullanıldığına ilişkin bir kısıtlama yoktur.

### <a name="creating-event-flags-groups"></a>Olay bayrakları grupları oluşturma

Olay bayrakları grupları, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Oluşturma sırasında, gruptaki tüm olay bayrakları sıfır olarak ayarlanır. Bir uygulamadaki olay bayrakları gruplarının sayısı için bir sınır yoktur.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Uygulama iş parçacıkları bir gruptan olay bayraklarının herhangi bir mantıksal birleşimini almaya çalışırken askıya alabilir. Bir olay bayrağı ayarlandıktan sonra, askıya alınmış tüm iş parçacıklarının get istekleri gözden geçirilir. Artık gerekli olay bayraklarına sahip olan tüm iş parçacıkları sürdürülür.

> [!NOTE]
> *Olay bayrağı grubundaki askıya alınmış tüm iş parçacıkları, olay bayrakları ayarlandığında gözden geçirilir. Kuşkusuz bu, ek yük getirir. Bu nedenle, aynı olay bayrağı grubunu kullanan iş parçacığı sayısını makul bir sayıyla sınırlamak iyi bir uygulamadır.*

### <a name="event-flags-set-notification"></a>Olay bayrakları ayarlama bildirimi

Bazı uygulamalar, bir olay bayrağı her ayarlandığında bildirim almak için yararlı bulabilir. ThreadX, ***tx_event_flags_set_notify*** hizmeti aracılığıyla bu yeteneği sağlar. Bu hizmet, belirtilen olay bayrakları grubuyla sağlanan uygulama bildirim işlevini kaydeder. Daha sonra ThreadX, gruptaki bir olay bayrağı ayarlandığında, bu uygulama bildirim işlevini çağırır. Uygulama bildirim işlevi içindeki tam işlem uygulama tarafından belirlenir, ancak genellikle yeni olay bayrağını işlemek için uygun iş parçacığını sürdürmeden oluşur.

### <a name="event-flags-event-chainingtrade"></a>Olay bayrakları olay zinciri&trade;

ThreadX içindeki bildirim özellikleri, çeşitli eşitleme olaylarını birlikte "zincirleme" için kullanılabilir. Bu, genellikle tek bir iş parçacığının birden çok eşitleme olayını işlemesi gerektiğinde faydalıdır.

Örneğin, bir kuyruk iletisi, olay bayrakları ve semafor için ayrı iş parçacıkları askıya almak yerine, uygulama her nesne için bir bildirim yordamı kaydedebilir. Çağrıldığında, uygulama bildirimi yordamı tek bir iş parçacığını sürdürür, bu da her bir nesneye sorgulanamıyor, bu da yeni olayı bulup işleyebilir.

Genel olarak, *olay zincirleme* daha az iş parçacığı, daha az ek yük ve daha küçük RAM gereksinimlerine neden olur. Ayrıca, daha karmaşık sistemlerin eşitleme gereksinimlerini işlemek için yüksek düzeyde esnek bir mekanizma sağlar.

### <a name="run-time-event-flags-performance-information"></a>Çalışma zamanı olay bayrakları performans bilgileri

ThreadX isteğe bağlı çalışma zamanı olay bayrakları performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

Genel sistem için toplam sayı:

  - olay bayrakları kümeleri

  - olay bayrakları alır

  - olay bayrakları getirilmesi al

  - olay bayrakları zaman aşımlarını al

Her olay bayrakları grubu için toplam sayı:

  - olay bayrakları kümeleri

  - olay bayrakları alır

  - olay bayrakları getirilmesi al

  - olay bayrakları zaman aşımlarını al

Bu bilgiler, ***tx_event_flags_performance_info_get** _ ve _*_tx_event_flags_performance_system_info_get_*_ Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. Olay bayraklarının performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, _ *_tx_event_flags_get_** hizmetindeki görece yüksek sayıda zaman aşımı, olay bayrakları askıya alma zaman aşımı değerinin çok kısa olduğunu önerebilir.

### <a name="event-flags-group-control-block-tx_event_flags_group"></a>Olay bayrakları Grup denetim bloğu TX_EVENT_FLAGS_GROUP

Her olay bayrakları grubunun özellikleri denetim bloğunda bulunur. Geçerli olay bayrakları ayarları ve olaylar için askıya alınan iş parçacığı sayısı gibi bilgileri içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

Olay grubu denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

### <a name="memory-block-pools"></a>Bellek blok havuzları

Bellek hızlı ve belirleyici bir şekilde ayrılırken gerçek zamanlı uygulamalarda her zaman bir zorluk vardır. Bu aklınızda, ThreadX, birden çok sabit boyutlu bellek bloğu havuzu oluşturma ve yönetme olanağı sağlar.

Bellek blok havuzları sabit boyutlu bloklardan oluştuğundan hiçbir parçalama sorunu yoktur. Tabii ki parçalama, doğal olarak belirleyici olmayan davranışa neden olur. Ayrıca, sabit boyutlu bir bellek bloğunu ayırmak ve serbest bırakmak için gereken süre, basit bağlantılı liste işleme ile karşılaştırılabilir. Ayrıca, bellek bloğu ayırma ve ayırmayı kaldırma, kullanılabilir listenin başında yapılır. Bu, mümkün olan en hızlı bağlantılı liste işlemesini sağlar ve gerçek bellek bloğunu önbellekte tutmaya yardımcı olabilir.

Esneklik olmaması, sabit boyutlu bellek havuzlarının başlıca dezavantajıdır. Havuzun blok boyutu, kullanıcılarının en kötü durum bellek gereksinimlerini karşılayacak kadar büyük olmalıdır. Tabii ki aynı havuza çok sayıda farklı bellek isteği yapılırsa bellek harcanmayabilir. Olası bir çözüm, farklı boyutlardaki bellek blokları içeren birkaç farklı bellek bloğu havuzu oluşturmak olur.

Her bellek blok havuzu bir ortak kaynaktır. ThreadX, havuzların nasıl kullanıldığına ilişkin bir kısıtlama yoktur.

### <a name="creating-memory-block-pools"></a>Bellek blok havuzları oluşturma

Bellek blok havuzları, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Bir uygulamadaki bellek bloğu havuzlarının sayısı için bir sınır yoktur.

### <a name="memory-block-size"></a>Bellek blok boyutu

Daha önce belirtildiği gibi, bellek blok havuzları bir dizi sabit boyutlu blok içerir. Havuzun oluşturulması sırasında blok boyutu bayt cinsinden belirtilir.

> [!NOTE]
> *ThreadX, havuzdaki her bir bellek bloğuna küçük bir ek yük (C işaretçisi boyutu) ekler. Ayrıca, ThreadX ' in her bir bellek bloğunun başlangıcını doğru hizalamadan korumak için blok boyutunu doldurma gerekebilir.*

### <a name="pool-capacity"></a>Havuz kapasitesi

Bir havuzdaki bellek bloklarının sayısı, blok boyutunun bir işlevidir ve oluşturma sırasında sağlanan bellek alanındaki toplam bayt sayısıdır. Havuzun kapasitesi, blok boyutu (doldurma ve işaretçi ek yükü baytları dahil), sağlanan bellek alanındaki toplam bayt sayısına bölünerek hesaplanır.

### <a name="pools-memory-area"></a>Havuzun bellek alanı

Daha önce belirtildiği gibi, blok havuzu için bellek alanı oluşturma sırasında belirtilir. ThreadX içindeki diğer bellek alanları gibi, hedefin adres alanında herhangi bir yerde bulunabilir.

Bu, sağladığı önemli esneklik nedeniyle önemli bir özelliktir. Örneğin, bir iletişim ürününün g/ç için bir Highspeed bellek alanı olduğunu varsayalım. Bu bellek alanı, bir ThreadX bellek blok havuzunda yapılarak kolayca yönetilebilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Uygulama iş parçacıkları boş havuzdan bir bellek bloğunun beklediği sırada askıya alabilir. Havuza bir blok döndürüldüğünde, askıya alınan iş parçacığına bu blok verilir ve iş parçacığı sürdürülür.

Aynı bellek bloğu havuzunda birden çok iş parçacığı askıya alınırsa, bunlar askıya alındığı sırada sürdürülür (FıFO).

Ancak, uygulama, iş parçacığı askıya alma işleminden önce blok yayın çağrısından önce ***tx_block_pool_prioritize*** çağırırsa öncelik sürdürme de mümkündür. Blok havuzu öncelik sıralaması hizmeti, en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar, diğer tüm askıya alınan iş parçacıklarını aynı FıFO sırasıyla bırakır.

### <a name="run-time-block-pool-performance-information"></a>Çalışma zamanı blok havuzu performans bilgileri

ThreadX isteğe bağlı çalışma zamanı blok havuzu performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

Genel sistem için toplam sayı:

  - ayrılan bloklar

  - çıkarılan bloklar

  - ayırma getirilmesi

  - ayırma zaman aşımları

Her blok havuzu için toplam sayı:

  - ayrılan bloklar

  - çıkarılan bloklar

  - ayırma getirilmesi

  - ayırma zaman aşımları

Bu bilgiler, ***tx_block_pool_performance_info_get** _ ve _ *_tx_block_pool_performance_system_info_get_* * Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. Blok havuzu performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda "Allocation getirilmesi", blok havuzunun çok küçük olmasını önerebilir.

### <a name="memory-block-pool-control-block-tx_block_pool"></a>Bellek blok havuzu denetim bloğu TX_BLOCK_POOL

Her bir bellek bloğu havuzunun özellikleri denetim bloğunda bulunur. Kullanılabilir bellek bloğu sayısı ve bellek havuzu blok boyutu gibi bilgileri içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

Havuz denetim blokları ayrıca bellekte herhangi bir yerde bulunabilir, ancak her bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak en yaygın hale gelir.

### <a name="overwriting-memory-blocks"></a>Bellek bloklarının üzerine yazma

Ayrılmış bir bellek bloğunun kullanıcısının sınırlarının dışına yazmadığından emin olmak önemlidir. Bu durumda, bir komşu (genellikle sonraki) bellek alanında bozulma oluşur. Sonuçlar tahmin edilemez ve genellikle uygulama için önemli olur.

## <a name="memory-byte-pools"></a>Bellek bayt havuzları

ThreadX bellek bayt havuzları standart C yığınına benzer. Standart C yığınının aksine, birden çok bellek bayt havuzu olması mümkündür. Ayrıca, iş parçacıkları istenen bellek kullanılabilir olana kadar bir havuzda askıda olabilir.

Bellek bayt havuzlarından ayırmalar, istenen bellek miktarını (bayt cinsinden) içeren geleneksel ***malloc** _ çağrılarına benzerdir. Bellek, havuzdan bir _first uyacak şekilde ayrılır; Yani, isteği karşılayan ilk boş bellek bloğu kullanılır. Bu bloktaki aşırı bellek yeni bir bloğa dönüştürülür ve boş bellek listesine geri yerleştirilir. Bu işleme *parçalanma* adı verilir.

Bitişik boş bellek blokları, daha sonraki bir ayırma araması sırasında, çok sayıda boş bellek bloğu için birlikte *birleştirilir* . Bu işleme *birleştirme* adı verilir.

Her bellek bayt havuzu ortak bir kaynaktır. ThreadX, havuzların nasıl kullanıldığına ilişkin hiçbir kısıtlama vermez, bu da bellek bayt Hizmetleri ISRs 'den çağrılamaz.

### <a name="creating-memory-byte-pools"></a>Bellek bayt havuzları oluşturma

Bellek bayt havuzları, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Bir uygulamadaki bellek baytı havuzlarının sayısı için bir sınır yoktur.

### <a name="pool-capacity"></a>Havuz kapasitesi

Bellek bayt havuzunda ayrılan ayrıtı bayt sayısı, oluşturma sırasında belirtilenden biraz daha düşüktür. Bunun nedeni, boş bellek alanının yönetiminde bazı ek yük tanıtılmaktadır. Havuzdaki her bir boş bellek bloğu, iki C ek yük işaretçinin eşdeğerini gerektirir. Ayrıca havuz, büyük bir boş blok ve bellek alanının sonunda küçük bir kalıcı olarak ayrılmış blok ile oluşturulur. Bu ayrılmış blok, ayırma algoritmasının performansını geliştirmek için kullanılır. Birleştirme sırasında havuz alanının sonuna sürekli denetleme gereksinimini ortadan kaldırır.

Çalışma zamanı sırasında havuzdaki ek yük miktarı genellikle artar. Bir sonraki bellek bloğunun doğru hizalamasını sağlamak için tek sayılı baytların ayırmaları doldurulur. Ayrıca, havuz daha parçalanmış hale geldiği için ek yük artar.

### <a name="pools-memory-area"></a>Havuzun bellek alanı

Bellek bayt havuzu için bellek alanı oluşturma sırasında belirtilir. ThreadX içindeki diğer bellek alanları gibi, hedefin adres alanında herhangi bir yerde bulunabilir. Bu, sağladığı önemli esneklik nedeniyle önemli bir özelliktir. Örneğin, hedef donanımın yüksek hızlı bellek alanı ve düşük hızlı bellek alanı varsa, her birinde bir havuz oluşturarak Kullanıcı her iki alan için bellek ayırmayı yönetebilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Bir havuzdan bellek baytları beklenirken uygulama iş parçacıkları askıya alabilir. Yeterli bitişik bellek kullanılabilir olduğunda, askıya alınan iş parçacıklarına istenen bellek verilir ve iş parçacıkları sürdürülür.

Aynı bellek bayt havuzunda birden çok iş parçacığı askıya alınırsa, bunlar askıya alınan (FıFO) sırada bellek olarak verilir (devam ettirildi).

Ancak, uygulama, iş parçacığı askıya alma işlemi için bayt yayın çağrısından önce ***tx_byte_pool_prioritize*** çağırdığında öncelik sürdürme de mümkündür. Bayt havuzu öncelik sıralaması hizmeti, en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar, diğer tüm askıya alınan iş parçacıklarını aynı FıFO sırasıyla bırakır.

### <a name="run-time-byte-pool-performance-information"></a>Çalışma zamanı bayt havuzu performans bilgileri

ThreadX isteğe bağlı çalışma zamanı bayt havuzu performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış ***TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO*** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

Genel sistem için toplam sayı:

  - ayırmalarını

  - yayınlar

  - Aranan parçalar

  - Birleştirilen parçalar

  - oluşturulan parçalar

  - ayırma getirilmesi

  - ayırma zaman aşımları

Her bayt havuzunun toplam sayısı:

  - ayırmalarını

  - yayınlar

  - Aranan parçalar

  - Birleştirilen parçalar

  - oluşturulan parçalar

  - ayırma getirilmesi

  - ayırma zaman aşımları

Bu bilgiler, ***tx_byte_pool_performance_info_get** _ ve _ *_tx_byte_pool_performance_system_info_get_* * Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. Bayt havuzu performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır. Örneğin, görece yüksek sayıda "Allocation getirilmesi", bayt havuzunun çok küçük olduğunu önerebilir.

### <a name="memory-byte-pool-control-block-tx_byte_pool"></a>Bellek bayt havuzu denetim bloğu TX_BYTE_POOL

Her bir bellek bayt havuzunun özellikleri denetim bloğunda bulunur. Havuzdaki kullanılabilir bayt sayısı gibi yararlı bilgiler içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

Havuz denetim blokları ayrıca bellekte herhangi bir yerde bulunabilir, ancak her bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak en yaygın hale gelir.

### <a name="nondeterministic-behavior"></a>Belirleyici olmayan davranış

Bellek bayt havuzları en esnek bellek ayırmayı sağlasa da, önemli olmayan davranışlardan de zarar verir. Örneğin, bir bellek bayt havuzunda 2.000 baytlık bellek bulunabilir, ancak 1.000 baytlık bir ayırma isteğini karşılayamayabilir. Bunun nedeni, boş baytların kaç tane bitişik olduğunu garanti etmez. 1.000 baytlık boş bir blok mevcut olsa bile, bloğu bulmak için ne kadar süreceğine ilişkin garanti yoktur. Tüm bellek havuzunun, 1.000 bayt bloğunu bulmak için aranması gerekebilir.

> [!TIP]
> *Bellek bayt havuzlarının belirleyici olmayan davranışının bir sonucu olarak, belirleyici ve gerçek zamanlı davranışın gerekli olduğu alanlarda bellek bayt hizmetlerini kullanmaktan kaçınmak genellikle iyi bir uygulamadır. Birçok uygulama başlatma veya çalışma zamanı yapılandırması sırasında gereken belleği önceden ayırır.*

### <a name="overwriting-memory-blocks"></a>Bellek bloklarının üzerine yazma

Ayrılan bellek kullanıcısının sınırlarının dışına yazmadığından emin olmak önemlidir. Bu durumda, bir komşu (genellikle sonraki) bellek alanında bozulma oluşur. Sonuçlar tahmin edilemez ve genellikle program yürütmesi için çok zararlı olur.

## <a name="application-timers"></a>Uygulama zamanlayıcıları

Zaman uyumsuz dış olaylara hızlı yanıt gerçek zamanlı, katıştırılmış uygulamaların en önemli işlevidir. Ancak, bu uygulamaların birçoğu önceden belirlenen zaman aralıklarında belirli etkinlikler gerçekleştirmelidir.

ThreadX uygulama zamanlayıcıları, uygulamalar için belirli zaman aralıklarında uygulama C işlevlerini yürütme yeteneği sağlar. Ayrıca, bir uygulama süreölçerinin yalnızca bir kez kullanım süreleri de mümkündür. Bu tür bir zamanlayıcıya tek bir *Zamanlayıcı* denir, ancak yineleme aralığı zamanlayıcıları *düzenli* zamanlayıcı olarak adlandırılır.

Her uygulama süreölçeri ortak bir kaynaktır. ThreadX, uygulama süreölçerlerine ilişkin bir kısıtlama yoktur.

### <a name="timer-intervals"></a>Süreölçer aralıkları

ThreadX zaman aralıklarında düzenli Zamanlayıcı kesintileri ile ölçülür. Her süreölçer kesmeye Zamanlayıcı *onay* işareti denir. Zamanlayıcı işaretleri arasındaki gerçek süre uygulama tarafından belirtilir, ancak 10 MS çoğu uygulamanın norm olur. Düzenli süreölçer kurulumu genellikle ***tx_initialize_low_level*** derleme dosyasında bulunur.

Temel alınan donanımın, uygulama zamanlayıcılarının çalışması için düzenli kesmeler oluşturma yeteneğinin olması gerekir. Bazı durumlarda, işlemcinin yerleşik bir düzenli kesme özelliği vardır. İşlemcinin bu özelliği yoksa, kullanıcının panosunun düzenli kesmeler oluşturabilen bir çevresel cihaz olması gerekir.

> [!IMPORTANT]
> *ThreadX, düzenli bir kesme kaynağı olmadan bile çalışmaya devam edebilir. Ancak, süreölçer ile ilgili tüm işlemler devre dışı bırakılır. Bu, zaman aşımlama, askıya alınma süresi ve Zamanlayıcı hizmetleri içerir.*

### <a name="timer-accuracy"></a>Süreölçer doğruluğu

Süreölçer süre sonları, onay işaretleri bakımından belirtilir. Belirtilen süre sonu değeri her bir Zamanlayıcı Tick 'i için azaltılır. Bir uygulama süreölçeri bir Zamanlayıcı kesmesinden (veya zamanlayıcı Tick 'ten) önce etkinleştirilemediğinden, gerçek süre sonu süresi erken bir kısa süre önce olabilir.

Süreölçer değer oranı 10ms ise, uygulama zamanlayıcıları yaklaşık 10 MS 'ye kadar zaman alabilir. Bu, 1 saniyelik zamanlayıcıdan daha fazla 10 MS Zamanlayıcı için daha önemlidir. Tabii ki Zamanlayıcı kesme sıklığını artırmak hatanın bu kenar boşluğunu düşürür.

### <a name="timer-execution"></a>Süreölçer yürütme

Uygulama zamanlayıcıları etkin hale geldiği sırada yürütülür. Örneğin, aynı süre sonu değeri ile üç Zamanlayıcı oluşturulursa ve etkinleştirilirse, karşılık gelen süre sonu işlevlerinin etkinleştirildikleri sırada yürütülmesi garanti edilir.

### <a name="creating-application-timers"></a>Uygulama zamanlayıcıları oluşturma

Uygulama zamanlayıcıları, başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Bir uygulamadaki uygulama süreölçerinin sayısı için bir sınır yoktur.

### <a name="run-time-application-timer-performance-information"></a>Çalışma zamanı uygulama süreölçeri performans bilgileri

ThreadX isteğe bağlı çalışma zamanı uygulama süreölçeri performans bilgilerini sağlar. ThreadX kitaplığı ve uygulaması tanımlanmış **TX_TIMER_ENABLE_PERFORMANCE_INFO** ile derlenip, threadx aşağıdaki bilgileri biriktirir.

Genel sistem için toplam sayı:

- etkinleştir

- etkinleştirme kaldırma

- yeniden etkinleştirme (dönemsel zamanlayıcılar)

- süreleri

- süre sonu ayarlamaları

Her uygulama süreölçerinin toplam sayısı:

- etkinleştir

- etkinleştirme kaldırma

- yeniden etkinleştirme (dönemsel zamanlayıcılar)

- süreleri

- süre sonu ayarlamaları

Bu bilgiler, ***tx_timer_performance_info_get** _ ve _ *_tx_timer_performance_system_info_get_* * Hizmetleri aracılığıyla çalışma zamanında kullanılabilir. Uygulama süreölçer performans bilgileri, uygulamanın düzgün çalışıp çalışmadığını belirlemek için faydalıdır. Ayrıca, uygulamayı iyileştirmek için de kullanışlıdır.

### <a name="application-timer-control-block-tx_timer"></a>Uygulama Zamanlayıcı denetim bloğu TX_TIMER

Her bir uygulama süreölçerinin özellikleri denetim bloğunda bulunur. 32 bitlik süre sonu tanımlama değeri gibi yararlı bilgiler içerir. Bu yapı ***tx_api. h*** dosyasında tanımlanmıştır.

Uygulama Zamanlayıcı denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

### <a name="excessive-timers"></a>Aşırı Zamanlayıcı

Varsayılan olarak, uygulama zamanlayıcıları, genellikle herhangi bir uygulama iş parçacığından daha yüksek olan bir gizli sistem iş parçacığı içinden yürütülür. Bu nedenle, uygulama zamanlayıcıları içinde işleme en az bir olmalıdır.

Mümkün olduğunda, her zaman Zamanlayıcı Tick 'i dolan zamanlayıcılar olmaması da önemlidir. Böyle bir durum, uygulamada aşırı yüke neden olur.

> [!IMPORTANT]
> *Daha önce belirtildiği gibi, uygulama zamanlayıcıları gizli bir sistem iş parçacığından yürütülür. Bu nedenle, uygulama süreölçerinin süre sonu işlevinin içinden yapılan tüm ThreadX hizmeti çağrılarında askıya alma ' yı seçmemelidir.*

## <a name="relative-time"></a>Göreli saat

ThreadX, daha önce bahsedilen uygulama zamanlayıcılar ' ne ek olarak tek bir sürekli artan 32 bit onay sayacı sağlar. Onay sayacı veya saati her bir Zamanlayıcı *kesilmesinde* bir artırılır.

Uygulama, sırasıyla ***tx_time_get** _ ve _ *_tx_time_set_* * çağrıları aracılığıyla bu 32 bitlik sayacı okuyabilir veya ayarlayabilir. Bu onay sayacının kullanımı, uygulama tarafından tamamen belirlenir. Bu, Işparçacığıx tarafından dahili olarak kullanılmaz.

## <a name="interrupts"></a>Kesmelerini

Zaman uyumsuz olaylara hızlı yanıt gerçek zamanlı, katıştırılmış uygulamaların asıl işlevidir. Uygulama, donanım kesintileri aracılığıyla böyle bir olayın mevcut olduğunu bilir.

Kesme, işlemci yürütmede zaman uyumsuz bir değişiklik olur. Genellikle, bir kesme gerçekleştiğinde, *kesmeler* işlemcisi yığında geçerli yürütmenin küçük bir bölümünü kaydeder ve denetimi uygun kesme vektörüne aktarır. Kesme vektörü temel olarak yalnızca belirli tür kesmeyi işlemekten sorumlu olan yordamın adresidir. Kesin kesme işleme yordamı, işlemciye özeldir.

### <a name="interrupt-control"></a>Kesme denetimi

***Tx_interrupt_control*** hizmeti, uygulamaların kesmeleri etkinleştirmesine ve devre dışı bırakmasına izin verir. Önceki kesme etkinleştirme/devre dışı bırakma, bu hizmet tarafından döndürülür. Kesme denetiminin yalnızca yürütülmekte olan program segmentini etkileyeceğini bahsetmek önemlidir. Örneğin, bir iş parçacığı kesintileri devre dışı bırakırsa, bu iş parçacığının yürütülmesi sırasında yalnızca devre dışı kalır.

> [!NOTE]
> *Maskelenemeyen kesme (NMI), donanım tarafından devre dışı bırakılamaz. Bu tür bir kesme, ThreadX uygulamaları tarafından kullanılabilir. Ancak, uygulamanın NMI işleme yordamının ThreadX bağlam yönetimini veya herhangi bir API hizmetini kullanmasına izin verilmez.*

### <a name="threadx-managed-interrupts"></a>ThreadX yönetilen kesmeler

ThreadX, tüm kesme yönetimine sahip uygulamalar sağlar. Bu yönetim, kesilen yürütmenin bağlamını kaydetmeyi ve geri yüklemeyi içerir. Ayrıca, ThreadX, belirli hizmetlerin kesme hizmeti yordamları (ISRS) içinden çağrılmasına izin verir. Aşağıda, uygulama ISRs 'den izin verilen ThreadX hizmetlerinin bir listesi verilmiştir.

```c
tx_block_allocate
tx_block_pool_info_get tx_block_pool_prioritize
tx_block_pool_performance_info_get
tx_block_pool_performance_system_info_get tx_block_release
tx_byte_pool_info_get tx_byte_pool_performance_info_get
tx_byte_pool_performance_system_info_get
tx_byte_pool_prioritize tx_event_flags_info_get
tx_event_flags_get tx_event_flags_set
tx_event_flags_performance_info_get
tx_event_flags_performance_system_info_get
tx_event_flags_set_notify tx_interrupt_control
tx_mutex_performance_info_get
tx_mutex_performance_system_info_get tx_queue_front_send
tx_queue_info_get tx_queue_performance_info_get
tx_queue_performance_system_info_get tx_queue_prioritize
tx_queue_receive tx_queue_send tx_semaphore_get
tx_queue_send_notify tx_semaphore_ceiling_put
tx_semaphore_info_get tx_semaphore_performance_info_get
tx_semaphore_performance_system_info_get
tx_semaphore_prioritize tx_semaphore_put tx_thread_identify
tx_semaphore_put_notify tx_thread_entry_exit_notify
tx_thread_info_get tx_thread_resume
tx_thread_performance_info_get
tx_thread_performance_system_info_get
tx_thread_stack_error_notify tx_thread_wait_abort tx_time_get
tx_time_set tx_timer_activate tx_timer_change
tx_timer_deactivate tx_timer_info_get
tx_timer_performance_info_get
tx_timer_performance_system_info_get
```

> [!IMPORTANT]
> *ISRs 'den askıya alma yapılmasına izin verilmez. Bu nedenle, bir ıSR 'den yapılan tüm ThreadX hizmeti çağrılarının **wait_option** parametresi **TX_NO_WAIT** olarak ayarlanmalıdır.*

### <a name="isr-template"></a>ISR şablonu

Uygulama kesmelerini yönetmek için uygulama ISRs 'nin başında ve sonunda birkaç ThreadX yardımcı programı çağrılmalıdır. Kesme işleme için tam biçim, bağlantı noktaları arasında farklılık gösterir.

Aşağıdaki küçük kod segmenti, en çok ThreadX yönetilen ISRs 'nin tipik bir parçasıdır. Çoğu durumda, bu işlem derleme dilidir.

```c
_application_ISR_vector_entry:

; Save context and prepare for

; ThreadX use by calling the ISR

; entry function.

CALL _tx_thread_context_save

; The ISR can now call ThreadX

; services and its own C functions

; When the ISR is finished, context

; is restored (or thread preemption)

; by calling the context restore ; function. Control does not return!

JUMP _tx_thread_context_restore
```

### <a name="high-frequency-interrupts"></a>Yüksek frekanslı kesmeler

Bazı kesmeler, her kesme sırasında tam bağlam kaydetme ve geri yükleme işlemlerinin çok fazla işlem bant genişliği tükettiği bir sıklıkta oluşur. Bu gibi durumlarda, uygulamanın bu yüksek frekanslı kesmelerin çoğu için sınırlı miktarda işleme yapan küçük bir derleme dili ıSR olması yaygındır.

Belirli bir noktadan sonra, küçük ıSR 'nin ThreadX ile etkileşimde olması gerekebilir. Bu, yukarıdaki şablonda açıklanan giriş ve çıkış işlevleri çağırarak gerçekleştirilir.

### <a name="interrupt-latency"></a>Kesme gecikmesi

ThreadX, kısa bir süre içinde kesmeleri kilitler. En fazla süre kesmesi devre dışı, bir iş parçacığının bağlamını kaydetmek veya geri yüklemek için gereken sürenin sıraındadır.
