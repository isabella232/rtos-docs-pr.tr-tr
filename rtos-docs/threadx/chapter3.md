---
title: Bölüm 3-Azure RTOS ThreadX 'in Işlevsel bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS ThreadX çekirdeğinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 906ccb4fb69925f5244192f06521bf508bd15ced2076fb03031649fea638171c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789987"
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

Çoğu durumda, uygulama iş parçacığının denetim bloğunun içeriğine göre yükümlülüğü olur. Ancak, özellikle hata ayıklama sırasında bazı durumlar vardır, bu da bazı üyelere göz at yararlı olur. Aşağıda, daha kullanışlı denetim bloğu üyelerinden bazıları ve ardından yer alan bilgiler ve daha faydalıdır.

**tx_thread_run_count,** iş parçacığının zamanlandığı sayıda sayacı içerir. Artan sayaç, iş parçacığının zamanlandığı ve yürütülmakta olduğunu gösterir.

**tx_thread_state** iş parçacığının durumunu içerir. Olası iş parçacığı durumları aşağıda listelemektedir.

|  İş parçacığı durumu   | Değer |
| --------------- | ------ |
| TX_READY       | (0x00) |
| TX_COMPLETED   | (0x01) |
| TX_TERMINATED  | (0x02) |
| TX_SUSPENDED   | (0x03) |
| TX_SLEEP       | (0x04) |
| TX_QUEUE_SUSP | (0x05) |
| TX_SEMAPHORE_SUSP | (0x06) |
| TX_EVENT_FLAG   | (0x07) |
| TX_BLOCK_MEMORY | (0x08) |
| TX_BYTE_MEMORY  | (0x09) |
| TX_MUTEX_SUSP   | (0x0D) |

> [!NOTE]
> *Elbette iş parçacığı denetim bloğunda yığın işaretçisi, zaman dilimi değeri, öncelikler vb. gibi birçok ilgi çekici alan daha vardır. Kullanıcılar denetim bloğu üyelerini gözden geçirebilirsiniz, ancak değişiklikler kesinlikle yasaktır!*

> [!IMPORTANT]
> *Bu bölümün önceki kısımlarında bahsedilen "yürütme" durumunun bir eşitliği yoktur. Belirli bir zamanda yalnızca bir yürüten iş parçacığı olduğundan bu gerekli değildir. Yürütülen iş parçacığının durumu da TX_READY.* 

### <a name="currently-executing-thread"></a>Şu Anda Yürütülen İş Parçacığı

Daha önce belirtildiği gibi, herhangi bir zamanda yürütülen yalnızca bir iş parçacığı vardır. İstekte bulunan iş parçacığına bağlı olarak, yürüten iş parçacığını tanımlamanın birkaç yolu vardır.
Bir program kesimi, tx_thread_identify çağırarak yürütülen iş parçacığının denetim ***bloğu adresini tx_thread_identify.*** Bu, uygulama kodunun birden çok iş parçacığından yürütülen paylaşılan kısımlarında kullanışlıdır.

Hata ayıklama oturumlarında, kullanıcılar iş parçacığında iç ThreadX işaretçisini ***_tx_thread_current_ptr.*** O anda yürütülen iş parçacığının denetim bloğu adresini içerir. Bu işaretçi NULL ise, hiçbir uygulama iş parçacığı yürütülmektedir; Diğer bir ifadeyle, ThreadX bir iş parçacığının hazır olması için zamanlama döngüsünde bekler.

### <a name="thread-stack-area"></a>İş Parçacığı Yığın Alanı

Her iş parçacığının son yürütme ve derleyici kullanımının bağlamını kaydeden kendi yığınına sahip olması gerekir. C derleyicilerinin çoğu, işlev çağrıları yapmak ve yerel değişkenleri geçici olarak kullanmak için yığını kullanır. Şekil 6'da tipik bir iş parçacığı yığınını gösterir.

Bellekte bir iş parçacığı yığınının bulunduğu yer uygulamaya bağlı olur. Yığın alanı iş parçacığı oluşturma sırasında belirtilir ve hedefin adres alanında herhangi bir yere yer olabilir. Uygulamaların yığınlarını yüksek hızlı RAM'e yerleştirerek önemli iş parçacıklarının performansını artırmalarına olanak sağlayan bu önemli bir özelliktir.

**Yığın Bellek Alanı** (örnek)

![Tipik İş Parçacığı Yığını](./media/user-guide/typical-thread-stack.png)

**ŞEKIL 6. Tipik İş Parçacığı Yığını**

Yığının ne kadar büyük olması gerektiği, iş parçacıkları hakkında en sık sorulan sorulardan biri. Bir iş parçacığının yığın alanı iç içe yerleştirme, yerel değişken ayırma ve son yürütme bağlamını kaydetme gibi en kötü durum işlev çağrılarına uyum sağlayacak kadar büyük olması gerekir.

en düşük yığın boyutu **TX_MINIMUM_STACK** ThreadX tarafından tanımlanır. Bu boyutta bir yığın, bir iş parçacığının bağlamını ve minimum işlev çağrısı miktarını ve yerel değişken ayırmayı kaydetmeyi destekler.

Ancak çoğu iş parçacığı için en düşük yığın boyutu çok küçüktür ve kullanıcının işlev çağrısı iç içe geçme ve yerel değişken ayırmayı inceerek en kötü durum boyutu gereksinimini tespitsi gerekir. Elbette daha büyük bir yığın alanıyla başlamak her zaman daha iyidir.

Uygulama hata ayıklandıktan sonra, bellek azsa iş parçacığı yığını boyutlarını ayarlamak mümkündür. Sık kullanılan bir püf noktası, iş parçacıklarını oluşturmadan önce tüm yığın alanlarını (0xEFEF) gibi kolayca tanımlanabilir bir veri deseniyle önceden ayar yapmaktır. Uygulamanın hızı ayrıntılı bir şekilde incelendikten sonra yığın alanları incelendikten sonra, yığında veri deseninin hala bozulmamış olduğu alanı bularak ne kadar yığının gerçekten kullanılmış olduğunu görebilir. Şekil 7'de, kapsamlı iş parçacığı yürütmeden sonra 0xEFEF için önceden ayarlanmış bir yığın gösterir.

**Yığın Bellek Alanı** (başka bir örnek)

![0xEFEF* için Yığın Ön Ayarı](./media/user-guide/stack-preset.png)

**ŞEKIL 7. 0xEFEF için Stack Ön 0xEFEF**

> [!IMPORTANT]
> *Varsayılan olarak, ThreadX her bir iş parçacığı yığınının her bayta değerini 0xEF.*

### <a name="memory-pitfalls"></a>Bellek Tuzakları

İş parçacıkları için yığın gereksinimleri büyük olabilir. Bu nedenle, uygulamayı makul sayıda iş parçacığına sahip olacak şekilde tasarlamak önemlidir. Ayrıca, iş parçacıklarında aşırı yığın kullanımından kaçınmak için bazı dikkatler gerekir. Cursive algoritmalardan ve büyük yerel veri yapılarından kaçınılmalıdır.

Çoğu durumda taşan yığın, iş parçacığı yürütmenin yığın alanıyla bitişik belleği bozmasını (genellikle önce) sağlar. Sonuçlar tahmin edilemez ancak genellikle program sayacında doğal olmayan bir değişiklikle sonuçlandır. Buna genellikle "atlayanlar" denir. Elbette bunu önlemenin tek yolu tüm iş parçacığı yığınlarının yeterince büyük olduğundan emin olmaktır.

### <a name="optional-run-time-stack-checking"></a>İsteğe Bağlı Çalışma Zamanı Yığın Denetimi

ThreadX, çalışma zamanı sırasında her iş parçacığının yığınında bozulma olup oluğu denetleme olanağı sağlar. Varsayılan olarak, ThreadX oluşturma sırasında iş parçacığı yığınlarının her bayta 0xEF veri deseniyle doldurur. Uygulama, iş parçacığı tanımlı TX_ENABLE_STACK_CHECKING  ThreadX kitaplığını derlemesi, askıya alınan veya sürdürülen her bir iş parçacığı yığınında bozulma olup olduğunu inceler. Yığın bozulması algılanırsa ThreadX, tx_thread_stack_error_notify _ çağrısı tarafından belirtilen şekilde uygulamanın yığın hatası işleme **_yordamını_*tx_thread_stack_error_notify. Aksi takdirde, yığın hatası işleyicisi belirtilmemişse ThreadX iç _ _* tx_thread_stack_error_handler** çağıracak.

### <a name="reentrancy"></a>Yeniden giriş

Çoklu iş parçacığının gerçek nedenlerinden biri, aynı C işlevinin birden çok iş parçacığından çağrıl olmasıdır. Bu, harika bir güç sağlar ve kod alanı azaltmaya da yardımcı olur. Ancak, birden çok iş parçacığından çağrılan C işlevlerinin yeniden *çağrılmalarını gerektirir.*

Temel olarak, bir yenidenentrant işlevi çağıranın dönüş adresini geçerli yığında depolar ve daha önce ayarlayan genel veya statik C değişkenlerine güvenmez. Çoğu derleyici, dönüş adresini yığına yer alıyor. Bu nedenle, uygulama geliştiricilerinin yalnızca genel ve statik *kullanımı konusunda* *endişelenmesi gerekir.*

Standart C kitaplığında bulunan ***strtok*** dize belirteci işlevi, yeniden kabul olmayan bir işleve örnektir. Bu işlev, sonraki çağrılarda önceki dize işaretçisini "anımsar". Bunu statik dize işaretçisi ile yapar. Bu işlev birden çok iş parçacığından çağrılsa, büyük olasılıkla geçersiz bir işaretçisi olacaktır.

### <a name="thread-priority-pitfalls"></a>İş Parçacığı Önceliği Tuzakları

İş parçacığı önceliklerini seçmek, çoklu iş parçacığının en önemli yönlerinden birisidir. Bazen çalışma zamanında tam olarak nelerin gerekli olduğunu belirlemek yerine iş parçacığı önemi algılanmasına dayalı olarak öncelik atamak çok cazip olabilir. İş parçacığı önceliklerinin kötüye kullanılması diğer iş parçacıklarını tüketebilir, öncelik ters çevirmesi oluşturabilir, işleme bant genişliğini azaltır ve uygulamanın çalışma zamanı davranışını anlamak zorlaştırabilirsiniz.

Daha önce belirtildiği gibi ThreadX, öncelik tabanlı, ön hazırlıklı bir zamanlama algoritması sağlar. Düşük öncelikli iş parçacıkları, yürütme için hazır daha yüksek öncelikli iş parçacıklarına sahip olana kadar yürütülmez. Daha yüksek öncelikli bir iş parçacığı her zaman hazırsa, düşük öncelikli iş parçacıkları hiçbir zaman yürütülmez. Bu koşul, iş *parçacığını açma olarak adlandırılan bir durumdur.*

Çoğu iş parçacığı açma sorunu, hata ayıklamanın erken bir zamanlarında algılanır ve yüksek öncelikli iş parçacıklarının sürekli olarak yürütülmeyebileceğini sağlayarak çözülebilir. Alternatif olarak, yürütme şansı elde edilene kadar yavaş yavaş iş parçacıklarının önceliğini yükselten uygulamaya mantık eklenebilir.

İş parçacığı öncelikleriyle ilişkili başka bir tuzak, *öncelikli ters çevirmedir.* Daha düşük öncelikli bir iş parçacığının gerekli bir kaynağa sahip olması nedeniyle daha yüksek öncelikli bir iş parçacığı askıya alınarak öncelik ters çevirmesi askıya alınır. Kuşkusuz, bazı örneklerde, farklı öncelikteki iki iş parçacığının ortak bir kaynağı paylaşması gerekir. Bu iş parçacıkları etkin tek bir sürümse, öncelik Inversion saati, düşük öncelikli iş parçacığı kaynağı tutan zamana göre sınırlanır. Bu koşul hem belirleyici hem de oldukça normaldir. Bununla birlikte, bu öncelik geçersiz kılma sırasında ara öncelikteki iş parçacıkları etkin hale gelirse, öncelik Inversion süresi artık belirleyici değildir ve bir uygulama hatasına neden olabilir.

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

Genel sistemin toplam sayısı:

  - semafor koyar

  - semafor alır

  - semafor askıya alma

  - semafor zaman aşımı alma

Her semafor için toplam sayı:

  - semafor koyar

  - semafor alır

  - semafor askıya alma

  - semafor zaman aşımı alma

Bu bilgiler * tx_semaphore_performance_info_get **_** ve _* tx_semaphore_performance_system_info_get **_hizmetleri aracılığıyla çalışma zamanında_ kullanılabilir. Semafor performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, görece yüksek sayıda "semafor zaman aşımı" olması, diğer iş parçacıklarının kaynakları çok uzun süre tutması önerisinde olabilir.

### <a name="semaphore-control-block-tx_semaphore"></a>Semaphore Denetim Bloğu TX_SEMAPHORE

Her sayma semaforu özellikleri denetim bloğunda bulunur. Geçerli semafor sayısı gibi bilgileri içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

Semafor denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi.

### <a name="deadly-embrace"></a>Embrace'i Benimseme

Karşılıklı dışlama için kullanılan semaforlarla ilişkili en ilginç ve tehlikeli tuzaklardan biri, ile *kucaklamadır.* İki veya daha *fazla* iş parçacığının birbirine ait olan semaforları almaya çalışırken süresiz olarak askıya alınarak askıya alınan bir koşuldur.

Bu koşul en iyi şekilde iki iş parçacığı tarafından gösterildi, iki semafor örneği. İlk iş parçacığının ilk semafora, ikinci iş parçacığının ise ikinci semafora sahip olduğunu varsayalım. İlk iş parçacığı ikinci semaforu almaya çalışır ve aynı zamanda ikinci iş parçacığı ilk semaforu almaya çalışırsa, her iki iş parçacığı da kilitlenme koşulu girer. Ayrıca, bu iş parçacıkları sonsuza kadar askıya alınırsa, ilişkili kaynakları da sonsuza kadar kilitlenir. Şekil 8'de bu örnek yer almaktadır.

**Embrace (örnek)**

![Askıya Alınan İş Parçacıkları Örneği](./media/user-guide/example-suspended-threads.png)

**ŞEKIL 8. Askıya Alınan İş Parçacıkları Örneği**

Gerçek zamanlı sistemlerde, iş parçacıklarının semaforları nasıl elde etmek için belirli kısıtlamalar koyarak kucaklamalar önlenebilir. İş parçacıkları aynı anda yalnızca bir semafora sahip olabilir. Alternatif olarak, iş parçacıkları aynı sırayla toplayarak birden çok semafora sahip olabilir. Önceki örnekte, birinci ve ikinci iş parçacığı sırasıyla birinci ve ikinci semaforu elde ettiyse, kucaklama engellenebilir.

> [!TIP]
> *Ayrıca alma işlemiyle ilişkili askıya alma zaman zamanlarını kullanarak bir kucaklamadan kurtulabilirsiniz.*

### <a name="priority-inversion"></a>Öncelik Ters Çevirme

Karşılıklı dışlama semaforları ile ilişkili başka bir tuzak, öncelik ters çevirmedir. Bu konu , " İş Parçacığı Önceliği[Tuzakları" başlığında daha tam olarak ele alınmıştır.](#thread-priority-pitfalls)

Temel sorun, düşük öncelikli bir iş parçacığının daha yüksek öncelikli bir iş parçacığına gereken semafora sahip olduğu bir durumdan sonuç verir. Bu kendi içinde normaldir. Ancak, aralarında öncelikleri olan iş parçacıkları, öncelik ters çevirmenin belirsiz bir süreye kadar devam esnettiğine neden olabilir. Bu, iş parçacığı önceliklerinin dikkatli bir şekilde seçerek, ön atma eşiği kullanılarak ve kaynağın sahibi olan iş parçacığının önceliğini geçici olarak yüksek öncelikli iş parçacığının önceliğini yükselterek iş parçacığı önceliklerini ele alacağız.

## <a name="mutexes"></a>Zaman Uyumu Sağlayıcılar

ThreadX, semaforlara ek olarak bir mutex nesnesi de sağlar. Bir mutex temelde ikili semafordan meydana gelir ve bu da aynı anda yalnızca bir iş parçacığının bir mutex'e sahip olduğu anlamına gelir. Ayrıca, aynı iş parçacığı sahip olunan bir mutex üzerinde tam olarak 4.294.967.295 olmak üzere birden çok kez başarılı bir mutex get işlemi gerçekleştirebilirsiniz. Mutex nesnesinde iki işlem var: ***tx_mutex_get** _ ve _*_tx_mutex_put_**. Alma işlemi başka bir iş parçacığına ait değil bir mutex elde ederken, put işlemi daha önce elde edilen bir mutex'i serbest bıraktır. Bir iş parçacığının bir mutex'i serbest bırakması için, put işlemlerinin sayısı önceki get işlemlerinin sayısına eşit olması gerekir.

Her mutex genel bir kaynaktır. ThreadX, mutex'lerin nasıl kullanıldıklarını kısıtlamaz.

ThreadX mutex'leri yalnızca karşılıklı *dışlama için kullanılır.* Sayma semaforların aksine, mutex'ler olay bildirimi için yöntem olarak kullanmaz.

### <a name="mutex-mutual-exclusion"></a>Karşılıklı Dışlama Mutex

Sayma semaforu bölümündeki tartışmaya benzer şekilde, karşılıklı dışlama belirli uygulama alanlarına (kritik  bölümler veya uygulama kaynakları olarak da adlandırılan) iş parçacıklarının erişimini *denetlemeyle ilgilidir.* Kullanılabilir olduğunda, ThreadX mutex'in sahiplik sayısı 0 olur. Mutex bir iş parçacığı tarafından alındıktan sonra, mutex üzerinde gerçekleştirilen her başarılı alma işlemi için sahiplik sayısı bir kez artırılır ve her başarılı koyma işlemi için azaltılır.

### <a name="creating-mutexes"></a>Mutex'ler Oluşturma

ThreadX mutex'leri başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Bir mutex'in ilk koşulu her zaman "kullanılabilir" olur. Öncelik devralma seçiliyken bir mutex *de oluşturulabilir.*

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Uygulama iş parçacıkları, zaten başka bir iş parçacığına ait olan bir mutex üzerinde alma işlemi gerçekleştirmeye çalışırken askıya alabilir.

Aynı sayıda koyma işlemi sahip olan iş parçacığı tarafından gerçekleştirildikten sonra, askıya alınan iş parçacığının alma işlemi gerçekleştirilir, buna mutex sahipliği ve iş parçacığı devam ettirir. Aynı mutex üzerinde birden çok iş parçacığı askıya alınırsa, bunlar askıya alındıklarına (FIFO) aynı sırayla devam eder.

Ancak, oluşturma sırasında mutex öncelik devralması seçildiyse öncelik yeniden verme işlemi otomatik olarak yapılır. Uygulama, iş parçacığının askıya alınmasına neden ***olan mutex put çağrısından tx_mutex_prioritize*** çağrısından önce çağrılsa da öncelik verme mümkündür. Mutex öncelik belirleme hizmeti en yüksek öncelikli iş parçacığını askıya alma listesinin önüne, diğer tüm askıya alınmış iş parçacıklarını aynı FIFO sırasına göre bırakarak yer alıyor.

### <a name="run-time-mutex-performance-information"></a>Çalışma Zamanı Mutex Performans Bilgileri

ThreadX, isteğe bağlı çalışma zamanı mutex performans bilgileri sağlar. ThreadX kitaplığı ve uygulaması tanımlı bir **TX_MUTEX_ENABLE_PERFORMANCE_INFO,** ThreadX aşağıdaki bilgileri birikmektedir.

Genel sistemin toplam sayısı:

- mutex puts

- mutex alır

- mutex get suspensions

- mutex get timeouts

- mutex öncelik ters çevirmeleri

- mutex öncelik devralmaları

Her bir mutex için toplam sayı:

  - mutex puts

  - mutex alır

  - mutex get suspensions

  - mutex get timeouts

  - mutex öncelik ters çevirmeleri

  - mutex öncelik devralmaları

Bu bilgiler * tx_mutex_performance_info_get **_** ve _* tx_mutex_performance_system_info_get ** hizmetleri aracılığıyla _çalışma zamanında_ kullanılabilir. Mutex performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemek için yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, görece yüksek sayıda "mutex get timeouts" diğer iş parçacıklarının kaynakları çok uzun süre tutması önerisinde olabilir.

### <a name="mutex-control-block-tx_mutex"></a>Mutex Denetim Bloğu TX_MUTEX

Her bir mutex'in özellikleri denetim bloğunda bulunur. Geçerli mutex sahipliği sayısı gibi bilgileri ve mutex'in sahibi olan iş parçacığının işaretçisini içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır. Mutex denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geliyor.

### <a name="deadly-embrace"></a>Embrace'i Benimseme

Mutex sahipliğiyle ilişkili en ilginç ve tehlikeli tuzaklardan biri, *benimsemektir.* Bir kucaklama ya da *çıkmaz,* diğer iş parçacıklarının sahip olduğu bir mutex'i almaya çalışırken iki veya daha fazla iş parçacığının süresiz olarak askıya alınarak askıya alınan bir koşuldur. Benimseme *tartışmaları ve* çözüm yolları, mutex nesnesi için de tamamen geçerlidir.

### <a name="priority-inversion"></a>Öncelik Ters Çevirme

Daha önce belirtildiği gibi, karşılıklı dışlama ile ilişkili önemli bir tuzak öncelik ters çevirmedir. Bu konu , " İş Parçacığı Önceliği[Tuzakları" başlığında daha tam olarak ele alınmıştır.](#thread-priority-pitfalls)

Temel sorun, daha düşük öncelikli bir iş parçacığının daha yüksek öncelikli bir iş parçacığına gereken semafora sahip olduğu bir durumdan sonuç verir. Bu kendi içinde normaldir. Ancak, aralarında öncelikleri olan iş parçacıkları, öncelik ters çevirmenin belirsiz bir süreye kadar devam esnettiğine neden olabilir. Daha önce tartışılan semaforların aksine, ThreadX mutex nesnesinin isteğe bağlı öncelik *devralması vardır.* Öncelik devralmanın ardındaki temel fikir, düşük öncelikli bir iş parçacığının önceliğini geçici olarak, aynı mutex'in düşük öncelikli iş parçacığına ait olması gereken yüksek öncelikli iş parçacığının önceliğe yükseltmiş olmasıdır. Düşük öncelikli iş parçacığı mutex'i serbest bıraksa, özgün önceliği geri yüklenir ve yüksek öncelikli iş parçacığına mutex sahipliği verilir. Bu özellik, ters çevirme miktarını düşük öncelikli iş parçacığının mutex'i tutarken sınırlaarak belirlenemeyen öncelik ters çevirmeyi ortadan kaldırıyor. Elbette, bu bölümün önceki kısımlarında tartışılan ve belirlenimci olmayan öncelik ters çevirmeyi işlemek için kullanılan teknikler de mutex'lerde geçerlidir.

## <a name="event-flags"></a>Olay Bayrakları

Olay bayrakları, iş parçacığı eşitleme için güçlü bir araç sağlar. Her olay bayrağı tek bir bitle temsil edildi. Olay bayrakları 32 grup halinde düzenlenmiştir. İş parçacıkları bir gruptaki 32 olay bayrağının hepsinde aynı anda çalışır. Olaylar * tx_event_flags_set **_** tarafından ayarlanır ve _* tx_event_flags_get **_tarafından_ alınır.

Olay bayraklarını ayarlama, geçerli olay bayrakları ile yeni olay bayrakları arasında mantıksal bir AND/OR işlemiyle yapılır. Mantıksal işlem türü (AND veya OR) çağrıda tx_event_flags_set ***belirtilir.***

Olay bayraklarının alınması için benzer mantıksal seçenekler vardır. Bir get isteği, belirtilen tüm olay bayraklarının gerekli olduğunu (mantıksal AND) belirtebiliyor.

Alternatif olarak, bir get isteği belirtilen olay bayraklarının herhangi biri isteği (mantıksal VEYA) karşılar. Olay bayraklarını alma işlemiyle ilişkili mantıksal işlem türü, tx_event_flags_get ***belirtilir.***

> [!IMPORTANT]
> *Bir get isteğini karşılayan* olay bayrakları, istek tarafından belirtilirse TX_OR_CLEAR veya **TX_AND_CLEAR**   *olarak ayarlanır.*

Her olay bayrak grubu genel bir kaynaktır. ThreadX, olay bayraklarının nasıl kullanıldıklarıyla ilgili hiçbir kısıtlama uygulamaz.

### <a name="creating-event-flags-groups"></a>Olay Bayrakları Grupları Oluşturma

Olay bayrakları grupları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Oluşturma sırasında, gruptaki tüm olay bayrakları sıfır olarak ayarlanır. Bir uygulamanın olay bayraklarının sayısıyla ilgili bir sınır yoktur.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Uygulama iş parçacıkları, bir gruptan herhangi bir mantıksal olay bayrağı birleşimini almaya çalışırken askıya alabilir. Bir olay bayrağı ayarlandıktan sonra, askıya alınan tüm iş parçacıklarının alma istekleri gözden geçirildi. Artık gerekli olay bayraklarına sahip olan tüm iş parçacıkları devam eder.

> [!NOTE]
> *Bir olay bayrağı grubunda askıya alınan tüm iş parçacıkları, olay bayrakları ayarlanırken gözden geçirildi. Elbette bu ek yük getirir. Bu nedenle, aynı olay bayrağı grubunu kullanarak iş parçacığı sayısını makul bir sayıyla sınırlamak iyi bir uygulamadır.*

### <a name="event-flags-set-notification"></a>Olay Bayrakları Bildirim Kümesi

Bazı uygulamalar, bir olay bayrağı her ayar olduğunda bunun bildirilecek bir avantaj olduğunu bulabilir. ThreadX, bu özelliği tx_event_flags_set_notify ***sağlar.*** Bu hizmet, sağlanan uygulama bildirim işlevini belirtilen olay bayrakları grubuna kaydediyor. ThreadX daha sonra grupta bir olay bayrağı ayarlandığında bu uygulama bildirim işlevini çağırır. Uygulama bildirim işlevi içindeki tam işlem uygulama tarafından belirlenir, ancak genellikle yeni olay bayrağını işlemeye uygun iş parçacığını devamdan oluşur.

### <a name="event-flags-event-chainingtrade"></a>Olay Bayrakları Olay zinciri&trade;

ThreadX'in bildirim özellikleri çeşitli eşitleme olaylarını birlikte "zincirleme" için kullanılabilir. Bu genellikle tek bir iş parçacığının birden çok eşitleme olaylarını işlemesi gereken durumlarda kullanışlıdır.

Örneğin, bir kuyruk iletisi, olay bayrakları ve semafor için ayrı iş parçacıklarının askıya alınması yerine, uygulama her nesne için bir bildirim yordamını kaydedebilir. Çağrıldığında, uygulama bildirim yordamı tek bir iş parçacığını sürdürebilir ve bu da yeni olayı bulmak ve işlemek için her nesneyi sorgular.

Genel olarak, *olay zinciri daha az iş* parçacığına, daha az ek yüke ve daha küçük RAM gereksinimlerine neden olur. Ayrıca, daha karmaşık sistemlerin eşitleme gereksinimlerini işlemek için son derece esnek bir mekanizma sağlar.

### <a name="run-time-event-flags-performance-information"></a>Çalışma Zamanı Olay Bayrakları Performans Bilgileri

ThreadX, isteğe bağlı çalışma zamanı olay bayrakları performans bilgileri sağlar. ThreadX kitaplığı ve uygulaması tanımlı bir **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO,** ThreadX aşağıdaki bilgileri birikiyor.

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

Bu bilgiler çalışma zamanında * tx_event_flags_performance_info_get _ **ve tx_event_flags_performance_system_info_get.** _**_ Olay bayraklarının performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin,*___* tx_event_flags_get * hizmette görece yüksek sayıda zaman aşımı olması, olay bayraklarının askıya alınma zaman aşımının çok kısa olduğunu önermiş olabilir.

### <a name="event-flags-group-control-block-tx_event_flags_group"></a>Event Flags Grup Denetim Bloğu TX_EVENT_FLAGS_GROUP

Her olay bayrak grubunun özellikleri denetim bloğunda bulunur. Geçerli olay bayrakları ayarları ve olaylar için askıya alınan iş parçacığı sayısı gibi bilgileri içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

Olay grubu denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline yaygındır.

### <a name="memory-block-pools"></a>Bellek Blok Havuzları

Belleğin hızlı ve belirlenimci bir şekilde belirlenmesi, gerçek zamanlı uygulamalarda her zaman bir zorlukdur. ThreadX, sabit boyutlu bellek bloklarından birden çok havuz oluşturma ve yönetme olanağı sağlar.

Bellek bloğu havuzları sabit boyutlu bloklardan oluşan olduğundan, hiçbir zaman parçalanma sorunu oluşturmaz. Elbette parçalanma, doğası gereği belirlenemeyen davranışlara neden olur. Ayrıca, sabit boyutlu bir bellek bloğu ayırmak ve serbest bırakma süresi, basit bağlantılı liste işlemesi ile karşılaştırılabilir. Ayrıca, kullanılabilir listenin başında bellek bloğu ayırma ve ayırmayı geri alır. Bu, mümkün olan en hızlı bağlantılı liste işlemeyi sağlar ve gerçek bellek bloğun önbellekte tutmaya yardımcı olabilir.

Esneklik eksikliği, sabit boyutlu bellek havuzlarının temel dezavantajıdır. Bir havuzun blok boyutu, kullanıcılarının en kötü durum bellek gereksinimlerini işecek kadar büyük olmalı. Elbette, aynı havuza çok sayıda farklı boyutta bellek isteği yapılırsa bellek boşa harcanmış olabilir. Olası bir çözüm, farklı boyutlu bellek blokları içeren birkaç farklı bellek bloğu havuzu yapmaktır.

Her bellek bloğu havuzu genel bir kaynaktır. ThreadX, havuzların nasıl kullanıldıklarına hiçbir kısıtlama uygulamaz.

### <a name="creating-memory-block-pools"></a>Bellek Blok Havuzları Oluşturma

Bellek bloğu havuzları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Bir uygulamanın bellek bloğu havuzlarının sayısına bir sınır yoktur.

### <a name="memory-block-size"></a>Bellek Bloğu Boyutu

Daha önce belirtildiği gibi, bellek blok havuzları bir dizi sabit boyutlu blok içerir. Bayt cinsinden blok boyutu, havuzun oluşturulması sırasında belirtilir.

> [!NOTE]
> *ThreadX, havuza her bir bellek bloğuna küçük miktarda ek yük (C işaretçisi boyutu) ekler. Buna ek olarak, ThreadX'in her bellek bloğunun başlangıcını düzgün hizalamada tutmak için blok boyutunun hizalanması da gerekli olabilir.*

### <a name="pool-capacity"></a>Havuz Kapasitesi

Havuzdaki bellek bloklarının sayısı, blok boyutuna ve oluşturma sırasında sağlanan bellek alanında sağlanan toplam bayt sayısına sahip bir işlevdir. Bir havuzun kapasitesi, blok boyutu (doldurma ve işaretçi ek yükü baytları dahil) sağlanan bellek alanında toplam bayt sayısına bölünerek hesaplanır.

### <a name="pools-memory-area"></a>Havuzun Bellek Alanı

Daha önce belirtildiği gibi, blok havuzunun bellek alanı oluşturma sırasında belirtilir. ThreadX'in diğer bellek alanlarında olduğu gibi, hedefin adres alanı içinde herhangi bir yerde yer alıyor olabilir.

Sağladığı önemli esneklik nedeniyle bu önemli bir özelliktir. Örneğin, bir iletişim ürününün, I/O için yüksek bir bellek alanına sahip olduğunu varsayalım. Bu bellek alanı, bir ThreadX bellek bloğu havuzuna dönüştürerek kolayca yönetilir.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Uygulama iş parçacıkları boş bir havuzdan bellek bloğu beklerken askıya alabilir. Havuza bir blok döndürüldü, askıya alınan iş parçacığına bu blok verilir ve iş parçacığı devam eder.

Aynı bellek bloğu havuzunda birden çok iş parçacığı askıya alınırsa, bunlar askıya alındıklarına (FIFO) göre devam eder.

Ancak uygulama, iş parçacığının askıya alınmasına neden ***olan blok tx_block_pool_prioritize*** çağrısından önce çağrılsa öncelik verme de mümkündür. Blok havuzu öncelik belirleme hizmeti en yüksek öncelikli iş parçacığını askıya alma listesinin önüne, diğer tüm askıya alınmış iş parçacıklarını da aynı FIFO sırasına göre bırakarak yer alıyor.

### <a name="run-time-block-pool-performance-information"></a>Çalışma Zamanı Blok Havuzu Performans Bilgileri

ThreadX, isteğe bağlı çalışma zamanı blok havuzu performans bilgileri sağlar. ThreadX kitaplığı ve uygulaması tanımlı bir **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO,** ThreadX aşağıdaki bilgileri birikiyor.

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

Bu bilgiler * tx_block_pool_performance_info_get **_** ve _* tx_block_pool_performance_system_info_get **_hizmetleri aracılığıyla çalışma zamanında_ kullanılabilir. Blok havuzu performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, görece yüksek sayıda "ayırma askıya alma" blok havuzunun çok küçük olduğunu önerebiliriz.

### <a name="memory-block-pool-control-block-tx_block_pool"></a>Bellek Blok Havuzu Denetim Bloğu TX_BLOCK_POOL

Her bellek bloğu havuzunun özellikleri denetim bloğunda bulunur. Kullanılabilir bellek bloğu sayısı ve bellek havuzu blok boyutu gibi bilgileri içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

Havuz denetim blokları bellekte herhangi bir yerde de yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi.

### <a name="overwriting-memory-blocks"></a>Bellek Bloklarının Üzerine Yazma

Ayrılmış bir bellek bloğu kullanıcılarının sınırlarının dışına yazmaması önemlidir. Bu durumda bozulma bitişik (genellikle sonraki) bir bellek alanında oluşur. Sonuçlar tahmin edilemez ve genellikle uygulama için önemli olur.

## <a name="memory-byte-pools"></a>Bellek Byte Havuzları

ThreadX bellek bayt havuzları standart bir C yığınına benzer. Standart C yığınının aksine, birden çok bellek bayt havuzu olabilir. Ayrıca, istenen bellek kullanılabilir olana kadar iş parçacıkları bir havuzda askıya alabilir.

Bellek bayt havuzlarından ayırmalar, istenen bellek miktarını (bayt cinsinden) içeren geleneksel ***malloc** _ çağrılarına benzer. Bellek havuzdan uygun* _first ayrılır; Başka bir ifadeyle isteği yerine gelen ilk boş bellek bloğu kullanılır. Bu bloktan fazla bellek yeni bir bloka dönüştürülür ve boş bellek listesine geri yerleştirilir. Bu işleme parçalanma *denir.*

Bitişik boş bellek blokları, *yeterli* sayıda boş bellek bloğu için sonraki ayırma araması sırasında birleştirilir. Bu işleme birleştirme *adı verilmektedir.*

Her bellek bayt havuzu genel bir kaynaktır. ThreadX, havuzların nasıl kullanıldıklarına hiçbir kısıtlama uygulamaz ancak bellek bayt hizmetleri ISR'lerden çağrılanamaz.

### <a name="creating-memory-byte-pools"></a>Bellek Byte Havuzları Oluşturma

Bellek bayt havuzları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanında oluşturulur. Bir uygulamanın bellek bayt havuzlarının sayısına bir sınır yoktur.

### <a name="pool-capacity"></a>Havuz Kapasitesi

Bir bellek bayt havuzu içinde allocatable bayt sayısı, oluşturma sırasında belirtilenden biraz daha azdır. Bunun nedeni, boş bellek alanı yönetiminin bazı ek yükler ortaya çıktısı. Havuzdaki her boş bellek bloğu, iki ek yük C işaretçisinin eşdeğerini gerektirir. Ayrıca havuz iki blokla oluşturulur: büyük bir boş blok ve bellek alanı sonunda kalıcı olarak ayrılan küçük bir blok. Ayrılan bu blok, ayırma algoritmasının performansını geliştirmek için kullanılır. Birleştirme sırasında havuz alanı sonunu sürekli denetleme ihtiyacı ortadan kaldırıyor.

Çalışma süresi sırasında havuza ek yük miktarı genellikle artar. Bir sonraki bellek bloğunda düzgün hizalama sağlamak için tek sayıda bayt ayırmaları dolgulu olarak gelir. Buna ek olarak, havuz daha parçalı hale geldi olarak ek yük artar.

### <a name="pools-memory-area"></a>Havuzun Bellek Alanı

Bir bellek bayt havuzunun bellek alanı oluşturma sırasında belirtilir. ThreadX'in diğer bellek alanlarında olduğu gibi, hedefin adres alanı içinde herhangi bir yerde yer alıyor olabilir. Sağladığı önemli esneklik nedeniyle bu önemli bir özelliktir. Örneğin, hedef donanım yüksek hızlı bir bellek alanına ve düşük hızlı bir bellek alanına sahipse, kullanıcı her iki alanda da bir havuz oluşturarak her iki alan için bellek ayırmayı yönetebilir.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Bir havuzdan bellek baytları beklerken uygulama iş parçacıkları askıya alabilir. Yeterli bitişik bellek kullanılabilir duruma geldiğinde, askıya alınan iş parçacıklarına istenen bellek verilir ve iş parçacıkları devam eder.

Aynı bellek byte havuzunda birden çok iş parçacığı askıya alınırsa, askıya alındıklarına (FIFO) göre bellek verilir (sürdürür).

Ancak, uygulama iş parçacığının askıya alınmasına neden ***olan tx_byte_pool_prioritize*** yayın çağrısından önce çağrılsa öncelik verme de mümkündür. Bayt havuzu hizmeti öncelik sırasına göre en yüksek öncelikli iş parçacığını askıya alma listesinin önüne, diğer tüm askıya alınmış iş parçacıklarını aynı FIFO sırasına göre bırakarak yer alıyor.

### <a name="run-time-byte-pool-performance-information"></a>Çalışma Zamanı Byte Havuzu Performans Bilgileri

ThreadX, isteğe bağlı çalışma zamanı baytı havuzu performans bilgileri sağlar. ThreadX kitaplığı ve uygulaması tanımlı bir ***TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO,*** ThreadX aşağıdaki bilgileri birikiyor.

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

Bu bilgiler * tx_byte_pool_performance_info_get **_** ve _* tx_byte_pool_performance_system_info_get **_hizmetleri aracılığıyla çalışma zamanında_ kullanılabilir. Byte havuzu performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır. Örneğin, görece yüksek sayıda "ayırma askıya alma" bayt havuzunun çok küçük olduğunu önerebiliriz.

### <a name="memory-byte-pool-control-block-tx_byte_pool"></a>Bellek Byte Havuzu Denetim Bloğu TX_BYTE_POOL

Her bellek bayt havuzunun özellikleri denetim bloğunda bulunur. Havuza kullanılabilir bayt sayısı gibi yararlı bilgiler içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

Havuz denetim blokları bellekte herhangi bir yerde de yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi.

### <a name="nondeterministic-behavior"></a>Belirsiz Davranış

Bellek bayt havuzları en esnek bellek ayırmayı sağlasa da, belirsiz bir davranıştan da zarar alırlar. Örneğin, bir bellek bayt havuzu 2.000 bayt kullanılabilir belleğe sahip olabilir, ancak 1.000 baytlık bir ayırma isteğini karşılayamayabilirsiniz. Bunun nedeni, boş baytların kaç tane bitişik olduğuyla ilgili bir garanti yoktur. 1.000 bayt boş blok olsa bile, bloğun bulunamaz hale ne kadar sürecesi garanti edilemez. 1.000 bayt bloğu bulmak için bellek havuzunun tamamının aranmış olması tamamen mümkündür.

> [!TIP]
> *Bellek bayt havuzlarının belirleyici olmayan davranışının bir sonucu olarak, belirlenici, gerçek zamanlı davranışın gerekli olduğu alanlarda bellek bayt hizmetlerini kullanmaktan kaçınmak genellikle iyi bir yöntemdir. Birçok uygulama başlatma veya çalışma zamanı yapılandırması sırasında gerekli belleklerini önceden ayırır.*

### <a name="overwriting-memory-blocks"></a>Bellek Bloklarının Üzerine Yazma

Ayrılan bellek kullanıcılarının sınırlarının dışına yazmaması önemlidir. Bu durumda bozulma bitişik (genellikle sonraki) bir bellek alanında oluşur. Sonuçlar öngörülemez ve genellikle program yürütme için yıkıcıdır.

## <a name="application-timers"></a>Uygulama Süre süreleri

Zaman uyumsuz dış olaylara hızlı yanıt, gerçek zamanlı, tümleşik uygulamaların en önemli işlevidir. Ancak, bu uygulamaların çoğu belirli etkinlikleri önceden belirlenecek zaman aralıklarında da gerçekleştirmesi gerekir.

ThreadX uygulama süreçerleri, uygulamalara belirli aralıklarla uygulama C işlevlerini yürütme olanağı sağlar. Bir uygulama zamanlayıcının süresinin yalnızca bir kez dolması da mümkündür. Aralık süreölçerleri yinelenen düzenli *süreölçerler olarak* çağrılırken, bu tür bir zamanlayıcı tek *atışlı zamanlayıcı olarak çağrılır.*

Her uygulama zamanlayıcısı genel bir kaynaktır. ThreadX, uygulama süre sürelerini kısıtlamaz.

### <a name="timer-intervals"></a>Zamanlayıcı Aralıkları

ThreadX zaman aralıklarında düzenli süreölçer kesintileri ölçülür. Her zamanlayıcı kesintisi, zamanlayıcı değer işareti *olarak adlandırılan bir değerdir.* Zamanlayıcı saat değerleri arasındaki gerçek süre uygulama tarafından belirtilir, ancak çoğu uygulama için 10 m'ler normdur. Düzenli süreölçer kurulumu genellikle tx_initialize_low_level ***dosyasında*** bulunur.

Temel alınan donanımın, uygulama süre önceleri için düzenli aralıklarla kesintiler oluşturabilme özelliğine sahip olması gerektiğini de ifade etmek gerekir. Bazı durumlarda işlemcinin yerleşik düzenli aralıklarla kesme özelliği vardır. İşlemcinin bu özelliği yoksa, kullanıcının panosunda düzenli aralıklarla kesintiler oluşturan bir çevre cihazı olması gerekir.

> [!IMPORTANT]
> *ThreadX, düzenli aralıklarla kesme kaynağı olmadan bile işleve devam ediyor. Ancak, zamanlayıcıyla ilgili tüm işlemler devre dışı bırakılır. Buna zaman, askıya alma zaman zamanları ve zamanlayıcı hizmetleri dahildir.*

### <a name="timer-accuracy"></a>Zamanlayıcı Doğruluğu

Zamanlayıcı süre sonu, saat işareti olarak belirtilir. Belirtilen süre sonu değeri, her zamanlayıcı değer değerinde bir azaltıldı. Bir uygulama süreölçeri, zamanlayıcı kesintisi (veya zamanlayıcı onay işareti) öncesinde etkinleştirilenene kadar, gerçek süre sonu erken bir değere kadar olabilir.

Süreölçer onay hızı 10 dakika ise, uygulama süreölçerleri 10 dakika erken sona erebilir. Bu, 10 m süreye sahip olan süreler için 1 saniyelik süreye göre daha önemlidir. Elbette zamanlayıcı kesme sıklığının artırılması bu hata marjını azaltıyor.

### <a name="timer-execution"></a>Zamanlayıcı Yürütme

Uygulama sürelerini etkin hale geldiklerinde yürütürler. Örneğin, aynı süre sonu değeriyle üç süre sonu oluşturulur ve etkinleştirilirse, karşılık gelen süre sonu işlevlerinin etkinleştiril edildiklerine göre yürütülmesi garanti edilir.

### <a name="creating-application-timers"></a>Uygulama Süre sürelerini oluşturma

Uygulama süre sürelerini başlatma sırasında veya çalışma zamanında uygulama iş parçacıkları tarafından oluşturulur. Bir uygulamanın uygulama süre sürelerini sınırlamaz.

### <a name="run-time-application-timer-performance-information"></a>Çalışma Zamanı Uygulama Süreölçeri Performans Bilgileri

ThreadX, isteğe bağlı çalışma zamanı uygulama süreölçeri performans bilgileri sağlar. ThreadX kitaplığı ve uygulaması tanımlı bir **TX_TIMER_ENABLE_PERFORMANCE_INFO,** ThreadX aşağıdaki bilgileri birikiyor.

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

Bu bilgiler * tx_timer_performance_info_get **_** ve _* tx_timer_performance_system_info_get **_hizmetleri aracılığıyla çalışma zamanında_ kullanılabilir. Uygulama Süreölçeri performans bilgileri, uygulamanın düzgün şekilde olup olmadığını belirlemede yararlıdır. Ayrıca uygulamayı iyileştirmede de yararlıdır.

### <a name="application-timer-control-block-tx_timer"></a>Uygulama Süreölçeri Denetim Bloğu TX_TIMER

Her uygulama zamanlayıcının özellikleri denetim bloğunda bulunur. 32 bit süre sonu tanımlama değeri gibi yararlı bilgiler içerir. Bu yapı, ***tx_api.h dosyasında*** tanımlanır.

Uygulama süreölçer denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğunun herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapıya sahip olmasıdır.

### <a name="excessive-timers"></a>Aşırı Süreye Neden Olan Süre

Varsayılan olarak, uygulama süreleri genellikle herhangi bir uygulama iş parçacığından daha yüksek olan, öncelik sıfırda çalışan gizli bir sistem iş parçacığı içinde yürütülür. Bu nedenle, uygulama sürelerini içinde işleme en düşük düzeyde tutulmalıdır.

Ayrıca, mümkün olan her zamanlayıcının süresinin dolması gibi bir süreölçerden kaçınmak da önemlidir. Böyle bir durum uygulamada aşırı yüke neden olabilir.

> [!IMPORTANT]
> *Daha önce belirtildiği gibi, uygulama süre sürelerini gizli bir sistem iş parçacığından yürütülür. Bu nedenle, uygulama süreölçeri süre sonu işlevinden yapılan hiçbir ThreadX hizmet çağrısında askıya alma seçmemesi önemlidir.*

## <a name="relative-time"></a>Göreli Saat

ThreadX, daha önce bahsedilen uygulama süre tutuculara ek olarak sürekli artan tek bir 32 bitlik onay sayacı sağlar. Her zamanlayıcı kesintisi *için* değer işareti sayacı veya süresi bir artırıldı.

Uygulama bu 32 bit sayacı sırasıyla * tx_time_get _ **ve** _* tx_time_set _**'a_ yapılan çağrılar aracılığıyla okuyabilir veya ayarlayabilirsiniz. Bu değer işareti sayacının kullanımı tamamen uygulama tarafından belirlenir. ThreadX tarafından dahili olarak kullanılmaz.

## <a name="interrupts"></a>Kesme

Zaman uyumsuz olaylara hızlı yanıt, gerçek zamanlı, katıştırılmış uygulamaların asıl işlevidir. Uygulama böyle bir olayın donanım kesintileri aracılığıyla mevcut olduğunu bilir.

Kesme, işlemci yürütmesinde zaman uyumsuz bir değişikliktir. Genellikle, bir kesme oluştuğunda, *Kesmeler* işlemcisi geçerli yürütmenin küçük bir kısmını yığına kaydeder ve denetimi uygun kesme vektörüne iletir. Kesme vektörü temelde belirli tür kesintilerini işlemeden sorumlu olan yordamın adresidir. Tam kesme işleme yordamı işlemciye özgüdür.

### <a name="interrupt-control"></a>Kesme Denetimi

Tx_interrupt_control ***hizmeti,*** uygulamaların kesmeleri etkinleştirmesini ve devre dışı bırakmasını sağlar. Önceki kesme etkinleştirme/devre dışı bırakma duruşu bu hizmet tarafından döndürülür. Kesme denetimi yalnızca o anda yürütülen program kesimini etkiler. Örneğin, bir iş parçacığı kesmeleri devre dışı bırakıyorsa, bunlar yalnızca o iş parçacığının yürütülmesi sırasında devre dışı kalır.

> [!NOTE]
> *Maskelenebilir Olmayan Kesinti (NMI), donanım tarafından devre dışı bırakılamaz bir kesintidir. Böyle bir kesinti ThreadX uygulamaları tarafından kullanılabilir. Ancak, uygulamanın NMI işleme yordamının ThreadX bağlam yönetimini veya api hizmetlerini kullanmasına izin verilmez.*

### <a name="threadx-managed-interrupts"></a>ThreadX Yönetilen Kesintileri

ThreadX, uygulamalara tam kesme yönetimi sağlar. Bu yönetim, kesintiye neden olan yürütme bağlamını kaydetmeyi ve geri yüklemeyi içerir. Ayrıca ThreadX, Bazı hizmetlerin Kesme Hizmeti Yordamları (ISR) içinde çağrılmalarını sağlar. Aşağıda uygulama ISR'lerinden izin verilen ThreadX hizmetlerinin bir listesi ve ardından yer vemektedir.

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
> *ISR'lerden askıya alınmaya izin verilmez. Bu **nedenle, wait_option** ISR'den yapılan tüm ThreadX hizmet çağrıları için **TX_NO_WAIT.***

### <a name="isr-template"></a>ISR Şablonu

Uygulama kesintilerini yönetmek için, uygulama ISR'lerinin başında ve sonunda birkaç ThreadX yardımcı programı çağrılmalı. Kesme işlemenin tam biçimi bağlantı noktaları arasında değişiklik gösterir.

Aşağıdaki küçük kod kesimi, Çoğu ThreadX tarafından yönetilen ISR'ler için tipiktir. Çoğu durumda, bu işlem derleme dilindedir.

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

### <a name="high-frequency-interrupts"></a>Yüksek Sıklık Kesintileri

Bazı kesintiler çok yüksek sıklıkta gerçekleşir ve her kesintiden sonra tam bağlamın kaydedilmesi ve geri yükleniyor olması aşırı işlem bant genişliği kullanır. Bu gibi durumlarda, uygulamanın bu yüksek sıklık kesmelerinin çoğu için sınırlı miktarda işleme işlemi yapmak için küçük bir derleme dili ISR'sine sahip olması yaygındır.

Belirli bir noktadan sonra, küçük ISR'nin ThreadX ile etkileşim kurması gerekir. Bu, yukarıdaki şablonda açıklanan giriş ve çıkış işlevleri çağrılarak başarılı olur.

### <a name="interrupt-latency"></a>Kesinti Gecikmesi

ThreadX, kısa bir süre içinde kesmeleri kilitler. En fazla süre kesmesi devre dışı, bir iş parçacığının bağlamını kaydetmek veya geri yüklemek için gereken sürenin sıraındadır.
