---
title: Bölüm 3-Gux 'e Işlevsel genel bakış
description: Bu bölüm, yüksek performanslı Gux Kullanıcı arabirimi ürününe işlevsel bir genel bakış içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2057b86e6f44912fe8ca349cdf0ad2cc10f5c4cd
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827202"
---
# <a name="chapter-3---functional-overview-of-guix"></a>Bölüm 3-Gux 'e Işlevsel genel bakış

Bu bölüm, yüksek performanslı Gux Kullanıcı arabirimi ürününe işlevsel bir genel bakış içerir. 

## <a name="execution-overview"></a>Yürütmeye genel bakış

GUIX, olay odaklı bir programlama modeli uygular. Bu, Gux çerçevesinin, Gux olay kuyruğuna gönderilen olayların alınmasından öncelikli olarak yönettiği anlamına gelir. Bu olayların işlenmesi, GUıDX sistem başlatması sırasında oluşturulan bir ThreadX iş parçacığı olan Gux iş parçacığı bağlamında gerçekleşir.

GUX uygulamaları, Windows ve alt pencere öğeleri oluşturmak için Gux API işlevlerini çağırarak kullanıcı arabirimini tanımlar ve her pencere veya pencere öğesi türünün renklerini, stillerini, yazı tiplerini ve çeşitli diğer özniteliklerini tanımlamak için kullanılan ek API işlevlerini çağırarak bu pencere öğelerinin görünümünü özelleştirin. Kullanıcı arabirimi ekranlarınızın görünümünü oluşturmak için Gux Studio kullanıyorsanız, ekran oluşturma işlemi için Gux API işlevlerini çağırma işlevinin çoğu, Gux Studio uygulaması tarafından sizin için yapılır.

GUX uygulamaları, Gux olay kuyruğundan alınan olayları işleyerek sistem kullanıcısı ve dış iş mantığı ile etkileşim kurar.
Bu olaylar genellikle Gux pencere öğeleri tarafından üretilir, ancak dış iş parçacıkları tarafından da oluşturulabilir. Tipik bir Gux düğmesi gönderildiğinde, bu düğme düğmenin üst penceresine bir olay gönderir. Uygulama programınız düğme anında iletme olayı için bir işleyici sağlayarak bu düğmeye gönderim üzerinde işlem yapacak.

Ek Gux iş parçacıkları genellikle giriş sürücüleri gibi şeyler için oluşturulur. Tipik bir dokunmatik ekran giriş sürücüsü, ana Gux iş parçacığı dışında tek başına bir iş parçacığı olarak yürütülür. Dokunmatik giriş sürücüsü, Gux olay kuyruğuna olayları göndererek Gux iş parçacığına dokunma bilgileri gönderir.

Animasyonlar gibi birçok kullanıcı arabirimi işlemi için doğru zamanlama bilgileri gerektiğinden, GUıDX Ayrıca basit ve kullanımı kolay bir Zamanlayıcı arabirimi de uygular. Bu süreölçer arabirimi, ThreadX Zamanlayıcı hizmeti üzerine kurulmuştur ve sistem başlangıcında otomatik olarak yapılandırılır.

GUX yazılımının büyük çoğunluğu herhangi bir donanım bağımlılıklarından bağımsızdır. Çerçeve, donanıma özgü giriş sürücüleri ve donanıma özgü grafik sürücüleri gerektirir. Bu donanıma özgü sürücülerin uygulanma ayrıntıları Bölüm 5 ' e ertelenir.

## <a name="initialization"></a>Başlatma 

Service ***gx_system_initialize*** DIĞER BIR Gux hizmeti çağrılmadan önce çağrılmalıdır. GUX sistem başlatması, ThreadX ***tx_application_define*** yordamından (başlatma bağlamından) veya uygulama iş parçacıklarından çağrılabilir. ***Gx_system_initialize*** işlevi, Gux olay kuyruğu oluşturur, guıdx süreölçer hizmetini başlatır, ana Gux sistem iş parçacığını oluşturur ve uygulamanızın yürütülmesi sırasında Gux tarafından tutulan çeşitli veri yapılarını başlatır.

***Gx_system_initialize*** çağrıldıktan sonra, uygulama ekranlar, canvaler, pencereler, pencere öğeleri ve tüm Gux nesnelerinin özelliklerini özelleştirmek için hazırlayın. GUX nesne oluşturma API 'sinin büyük bölümü ***tx_application_define*** veya uygulama iş parçacıklarından çağrılabilir.

## <a name="application-interface-calls"></a>Uygulama arabirimi çağrıları 

Uygulamadan yapılan çağrılar büyük ölçüde ***tx_application_define*** (başlatma bağlamından) veya uygulama iş parçacıklarından yapılır. Hangi bağlamın çağrılabilecek olduğunu belirlemek için, Bölüm 4 ' te açıklanan her bir Gux API 'sinin "Izin verilen" bölümüne bakın.

Çoğu bölümde, yoğun etkinliklerin işlenmesi, tüm olay işleme ve pencere öğesi/pencere çizimi dahil olmak üzere iç Gux iş parçacığına ertelenir.

GUX API işlevleri dilediğiniz zaman herhangi bir iş parçacığından çağrılabilir.
Ancak, zaman açısından kritik iş mantığınızı Kullanıcı arabirimi mantığınızdan ayırmak için genellikle daha iyi mimari olarak değerlendirilir. Kullanıcı arabirimi çizim işlemleri bazen görüntü boyutunuza ve CPU performansına bağlı olarak uzun süre sürebileceği için, normalde bir çizim işleminin tamamlanması beklenirken zaman açısından kritik iş parçacıklarının gecikilmesine sahip olmak istemezsiniz.

## <a name="internal-guix-thread"></a>İç Gux Iş parçacığı 

Belirtildiği gibi, GUıDX 'in GUI işlemesini toplu olarak gerçekleştiren bir iç iş parçacığı vardır. Bu iş parçacığı, uygulama yazılımı tarafından, ***gx_system_initialize** _ ve arkasından _ *_gx_system_start_* * çağırarak oluşturulur.

İç Gux iş parçacığının önceliği tarafından belirlenir `#define GX_SYSTEM_THREAD_PRIORITY` . Bu değer varsayılan olarak 16 ' dır (orta öncelik), ancak bu değer gx_port. h veya gx_user. h üstbilgi dosyasında belirtilerek, varsayılan değeri geçersiz kılarak değiştirilebilir.

GUX iş parçacığı zaman dilimi benzer şekilde tarafından tanımlanır ve varsayılan olarak `#define GX_SYSTEM_THREAD_TIMESLICE` 10 MS değeridir.

Sistem iş parçacığının yığın kişisi, `#define GX_THREAD_STACK_SIZE` ***gx_port. h*** üstbilgi dosyasında bulunan öğesine göre belirlenir, ancak bu değer gx_user. h üst bilgi dosyanızda belirtilerek de geçersiz kılınabilir.

İç Gux iş parçacığı yürütme döngüsü üç eylemden oluşur.
İlk olarak, guıdx olay kuyruğundan olayları alır ve bu olayları Gux Windows ve pencere öğeleri tarafından işlenmek üzere gönderir. Olaylar genellikle, düzenli zamanlayıcılar, dokunmatik ekran veya tuş takımı gibi giriş aygıtları ve Kullanıcı girişini işlediklerinde Gux Pencere öğelerinin kendileri tarafından Gux olay kuyruğuna gönderilir. Ardından, tüm olaylar işlendikten sonra, GUıDX bir ekran yenilemenin gerekli olup olmadığını belirler ve bu durumda, bu pencerelerin ve bu pencere öğelerinin çizim işlevlerini çağırarak kirli olarak işaretlenen bir işlem için gerekli işlemleri gerçekleştirir. Son olarak, GUıDX, yeni bir giriş olayı veya olay geldikçe Gux iş parçacığını askıya alır.

## <a name="event-processing"></a>Olay Işleme 

Dokunmatik veya kalem girişi olayları, dokunmatik veya kalem giriş piksel konumu altında en üstteki pencere veya pencere öğesi belirlenerek ve bu pencere/pencere öğesinin olay işleme işlevini çağırarak işlenir. Pencere öğesi kalem giriş olaylarını anladığı takdirde, bu pencere öğesi türü için uygun şekilde olayı işler. Aksi takdirde en üstteki pencere öğesi, işlem için pencere öğesinin üst öğesine dokunma veya kalem girişi olayını iletir. Bu olayı geçirme işlemi, olay işlenene veya olay kök pencereye gelene kadar devam eder; bu durumda olay atılır.

Tuş takımı olayları, giriş odaklı pencereye/pencere öğesine gönderilir. Giriş odağı durumu, Gux gx_system bileşeni tarafından korunur.

Zamanlayıcı olayları her zaman işleme için zamanlayıcıya sahip olan pencere veya pencere öğesine dağıtılır.

Düğme tıklama olayları veya kaydırıcı değer değişiklik olayları gibi dahili olarak oluşturulan olaylar her zaman olayı oluşturan pencere öğesinin üst öğesine gönderilir. Üst öğe olayı işlemez ise, dokunma veya kalem girişi olaylarına benzer şekilde zinciri iletilir.

## <a name="drawing"></a>Çizim 

Tüm olay işleme tamamlandıktan sonra, GUıDX iç iş parçacığı herhangi bir görüntüleme güncelleştirmesinin gerekli olup olmadığını ve uygun pencere/pencere öğesi çizim işlevlerinin çağrıldığını belirler. Çizim tamamlandığında, Gux iç iş parçacığı bir sonraki Gux olayının işlenmesi için olay sırasında bekler.

GUX, her pencere öğesi ve tuval için yeniden çizilmesi gereken alan olan *kirli alan* kavramını uygular. Pencere öğesi yalnızca daha önce kirli olarak işaretlenmiş alanlara çizim yapabilir. Bir pencere öğesi çizim işlevi çağrıldığında, tüm çizim işlemleri dahili olarak önceden tanımlanmış kirli dikdörtgene kırpılır.
Bu alanın dışında çizim denemeleri yok sayılır.

Pencere öğeleri ve pencereler, ***GX_SYSTEM_DIRTY_MARK*** API işlevini çağırarak kendilerini kirli olarak işaretler. Bu işlev, yeniden çizilmesini gerektiren tüm pencere öğesini veya pencereyi işaretler. İkinci bir işlev ***gx_system_dirty_partial_add***, yalnızca pencerenin veya pencere öğesinin bir kısmını kirli olarak işaretlemek için alternatif olarak çağrılabilir.

Bu pencere öğelerini kirli olarak işaretleme ve sonra yalnızca tüm giriş olayları işlendiğinde bu pencere öğelerinin yeniden çizilmesine yönelik bu model *ertelenmiş çizim* olarak adlandırılır. GUX ertelenmiş çizim algoritması ve kirli liste bakımı, çizim verimliliğini artırmak için tasarlanmıştır. Çizim işlemleri genellikle pahalı olduğundan, Gux gereksiz çizimi engellemek için zordur.

Çizim, bir Gux *tuvaline* yapılır. Tuval, grafik verilerini tutmak için ayrılan bir bellek alanıdır. Bir tuval, sistem mimarisine ve bellek kısıtlamalarına bağlı olarak doğrudan donanım çerçeve arabelleğine bağlanabilir veya olmayabilir. Herhangi bir çizim gerçekleşebilmeniz için önce, ***gx_canvas_drawing_initiate*** API işlevini çağırarak çizim için bir tuvalin açılması gerekir. Bu API, çizim için bir tuval hazırlar ve geçerli *Çizim bağlamını* kurdu. GUIX bir sistem tuvali yenilemesi gerçekleştirdiğinde, tuval çizim için açılır ve pencere öğesi düzeyi çizim API 'Leri çağrılmadan önce oluşturulan çizim bağlamı açılır. Bu nedenle Pencere öğelerinin pencere öğesi çizim işlevindeki bir tuvalde çizim başlatması gerekmez.

Ancak, bir uygulama, standart Gux ertelenmiş çizim algoritmasının akışı dışında bir tuvalde hemen çizim gerçekleştirmeye çalışırsa, uygulamanın diğer çizim API işlevlerini çağırmadan önce ***gx_canvas_drawing_initiate*** doğrudan çağırması ve hemen çizim tamamlandıktan sonra ***gx_canvas_drawing_complete*** çağırması gerekir.

## <a name="user-input"></a>Kullanıcı girişi 

GUX, önceden tanımlanmış olay türleriyle dokunmatik ekran, fare ve klavye cihazlarını destekler. Ek giriş cihazları, özel olay türleri tanımlayarak veya özel giriş cihazını önceden tanımlanmış olay türleriyle eşleyerek kullanılabilir.

Bu cihazlarla ilişkili eylemler, iç Gux iş parçacığı tarafından işlenen olaylara çevrilir. Dokunmatik ekranı desteklemek için yazılan sürücü düzeyi yazılımlar, kalem-aşağı, kalem ve kalem sürükleme işlemleri için Gux olay kuyruğu olaylarına hazırlanmalı ve göndermelidir. Benzer şekilde, bir tuş takımı giriş sürücüsü, anahtar basma ve anahtar yayın girişi için olaylar üretmelidir.

## <a name="modal-dialog-execution"></a>Kalıcı Iletişim kutusu yürütme 

Kalıcı iletişim kutusu yürütmesi, başka bir Gux Windows veya pencere öğesi Kullanıcı girişi alabilmesi için bir şekilde kapatılması gereken kullanıcıya bir pencere sunmaya başvurur. İletişim kutusu penceresi görüntülenirken, dokunma veya fare giriş olaylarının x, y konumundan bağımsız olarak, kalıcı iletişim kutuları tüm kullanıcı girişlerini yakalar.

Kalıcı iletişim kutuları, öncelikle ***gx_window_create*** çağırarak ve ardından Gux apı işlevi gx_window_execute çağırarak pencere normal şekilde oluşturularak uygulama yazılımı tarafından tetiklenir ***.***

***Gx_window_execute*** işlevi çağrıldığında, guıdx yerel bir olay işleme döngüsü girer. ***Gx_window_execute*** işlevi, Kullanıcı girişi ya da ***gx_window_close*** çağırarak, iletişim kutusu penceresi kapatılıncaya kadar çağırana geri dönmez. Bu nedenle, ***gx_window_execute*** işlevini Gux iç iş parçacığından başka hiçbir iş parçacığından çağırmamak çok önemlidir.

## <a name="periodic-processing"></a>Düzenli Işleme 

Ekran efektlerini, Sprite animasyonunu ve uygulama düzenli istekleri için desteği sağlamak üzere, GUıDX bir ThreadX zamanlayıcısını kullanır. Bu tek Zamanlayıcı, tüm Gux saat ile ilgili ihtiyaçları sağlamak için kullanılır. Varsayılan olarak, Gux iç Zamanlayıcı işlemenin sıklığı, gx_port. h veya gx_user. h üst bilgisinde daha önce tanımlanmadığı müddetçe, **_gx_api. h_** içinde tanımlanan sabit **GX_SYSTEM_TIMER_MS** aracılığıyla 20ms olarak ayarlanır. Varsayılan sıklık, Gux kitaplığını oluştururken veya ***gx_user. h***' de açıkça yeniden tanımlayarak, uygulama tarafından bir derleme seçeneği aracılığıyla değiştirilebilir.

> [!IMPORTANT]
> GUX Zamanlayıcı sıklığının RTOS Zamanlayıcı işaretleri içinde ifade edildiği ve sabit **GX_SYSTEM_TIMER_TICKS** tarafından tanımlandığını unutmayın. **GX_SYSTEM_TIMER_TICKS** değeri **GX_SYSTEM_TIMER_MS** ve **TX_TIMER_TICKS_PER_SECOND** kullanılarak hesaplanır. Kullanıcı, Gux Zamanlayıcı sıklığını ve çözünürlüğünü ayarlamak için ***gx_port. h** _ veya _ *_gx_user. h_** içindeki bu değerlerden herhangi birini yeniden tanımlayabilir.

## <a name="display-driver"></a>Görüntü sürücüsü 

Ekran sürücüleri, çekirdek Gux koduna bir çizim işlevleri kümesi sağlamaktan sorumludur. Bu çizim işlevlerinin her birinin uygulanması sürücü tarafından belirlenir ve uygulamanın donanım hızlandırma desteğinden faydalanması mümkün olduğunda. Genel olarak çizim işlevi, fiziksel çerçeve arabelleği olabilecek bir bellek arabelleğine piksel verileri yazarak çalışır veya sürücü mimarisine bağlı olarak ikincil bir arabellek olabilir. Birçok sürücü iki çerçeve arabelleği kullanarak çift arabelleğe alma uygular ve bu arabellekler arabellek geçiş işlevi çağrılarak çalışır. GUX bu işlevleri uygun zamanlarda dahili olarak çağırır. Bellek kısıtlı sistemler için çizim işlevleri yalnızca tek bir bellek çerçeve arabelleğine yazabilir.

GUX her bir alt düzey çizim işlevinin varsayılan yazılım uygulamalarını her bir destek renk derinliğine ve biçimine sağlar. Bu işlevler, **GX_DISPLAY** yapısı içinde tutulan işlev işaretçileri aracılığıyla çağrılır. Donanıma özgü sürücüler oluşturulduğunda, genellikle bu işlev işaretçilerinden bazılarının hedef donanıma özgü işlevlerle birlikte üzerine yazılır.

Tipik bir donanım görüntüleme sürücüsü, önce gerekli renk derinliği ve biçimi için varsayılan GUıDX görüntüleme sürücüsü oluşturularak uygulanır.
Daha sonra Donanım Sürücüsü, belirli donanım uygulamaları için optimize edilmiş veya özelleştirilmek zorunda olan işlevlerin yerini alır.

GUX desteği piksel rengi biçimi 1-BPP tek renkli 32-BPP a:r: g:b biçiminde değişiyor. GUX, r:g: b ile b:g: r bayt sıralaması, paketlenmiş piksel ve sözcük hizalanmış piksel formatları ve alfa kanalları gibi her geniş renk derinliği kategorisi içinde birçok çeşitlemeyi de destekler. Şu anda 25 farklı renk biçimi destekleniyor, ancak donanım satıcıları yeni Çeşitlemeler sundukça bu liste büyür.

## <a name="display-memory-architectures"></a>Bellek mimarilerini görüntüleme

Çeşitli donanım hedefleri ve ekranlar, hedefin bellek kısıtlamalarına ve uygulamanın işlev gereksinimlerine bağlı olarak çeşitli farklı görüntü belleği mimarilerinden yararlanır. Yaygın bellek mimarilerinden bazılarını, her birinin kısa bir açıklamasıyla özetler.

Model 1) çerçeve arabelleği yok, dış GRAM 'da tutulan grafik verileri:

![Çerçeve arabelleği yok, dış GRAM 'da tutulan grafik verileri](./media/guix/user-guide/no-frame-buffer.png)

Yukarıdaki modelde, CPU 'ya yerel bellekte bir çerçeve arabelleği için bellek yok. Tüm grafik verileri, görüntünün kendisiyle birleştirilmiş bir dış GRAM 'da depolanır. Dış GRAM arabirimi paralel veya seri olabilir. Bu tür bir mimari çok düşük maliyettir; ancak grafik verileri güncelleştirilirken istenmeyen bir etkisi olabilir.

Model 2) bir yerel çerçeve arabelleği:

![Bir yerel çerçeve arabelleği](./media/guix/user-guide/one-local-frame-buffer.png)

Bu modelde, Grafik verilerinin belleği, CPU 'ya doğrudan erişilebilen Rastgele erişimli bir bellekten ayrılır. Grafik verilerini (zamanlama sinyalleriyle birlikte) yerel bellekten görüntülemeye tekrar tekrar iletmek için adanmış donanım mevcut olmalıdır. Bu model, grafik belleğinin, CPU tarafından kullanılabilen yerel SRAM veya DRAM 'nin bir bloğu olduğu model 1 ' den farklıdır. Bu, yığın ve program değişkenlerinin canlı olduğu bellekle aynı olabilir.

Model 3) yerel çerçeve arabelleği + dış GRAM:

![Yerel çerçeve arabelleği + dış GRAM](./media/guix/user-guide/local-frame-buffer-external-gram.png)

Model 3, ilk iki öğesinin bir birleşimidir. Bu modelde, bir çerçeve arabelleğini tutmak için yeterli yerel bellek vardır. Ayrıca, görüntü cihazı bir dış GRAM sağlar ve GRAM 'da sağlanan verileri kullanarak kendisini otomatik olarak yeniler. Bu mimari, gelişmiş güncelleştirme verimliliğinden faydalanır çünkü yerel çerçeve arabelleğinin değiştirilen bölümünü tek bir blok aktarımından dış GRAM 'ya aktarabiliyoruz, genellikle ekleme DMA kanallarını kullanabilir. Bu model Ayrıca, yalnızca tamamlanmış grafik içerikleri dış GRAM 'a kopyalandığı için ilk iki modelden de bulunabilecek olan araçları ve titreşimi ortadan kaldırır.

Model 4) ping-pong çerçeve arabellekleri:

![Ping-pong çerçeve arabellekleri](./media/guix/user-guide/ping-pong-frame-buffers.png)

Model 4 ' te, iki yerel çerçeve arabelleği sağlamak için yeterli bellek vardır. Bu durumda, GUıDX, bir çerçeve arabelleğini etkin çerçeve arabelleği ve diğeri ise çalışma çerçevesi arabelleği olarak değerlendirir. Bir görüntüleme güncelleştirmesi veya çizim işlemi devam ederken, çalışma arabelleğinde gerçekleşir. Çizim işlemi tamamlandığında, arabellekler çalışır ve çalışma arabelleği etkin arabellek olur ve etkin arabellek çalışma arabelleği olur. Bu model, Ayrıca, tek bir arabelleğe alınmış sistemde gözlemlenebilir ekran titreşimini ve yük korumasını ortadan kaldırır.

Model 5) tuval birleştirme ile Pong arabellekleri:

![Tuval birleştirme özellikli ping-pong arabellekleri](./media/guix/user-guide/ping-pong-buffers-canvas-composting.png)

Model 5 ' te, kullanılabilir belleğin sınırlarına kadar herhangi bir sayıda canvaya oluşturulabilir. Tuvaller, tuval bileşimini oluşturmak için uygulama tarafından tanımlanan şekilde kaplama veya karışacaktır. Bir ekran yenileme işleminden sonra yeni bir bileşik oluşturulduğunda, etkin ve çalışan bileşik arabellekler standart ping-pong arabellek mimarisine benzer bir işlem halinde yapılır. Model 5 ' i, son çıkış bileşik ' e karışarak ekran belirme ve karıştırma işlemlerini gerçekleştirme yeteneği ekler.

Model 6) dış GRAM ile tuval birleştirme:

![Dış GRAM ile tuval birleştirme](./media/guix/user-guide/canvas-compositing-external-gram.png)

Model 6, 5 ' teki hafif bir çeşittir ve yalnızca bir bileşik arabelleğin gerekli olduğu ve bileşik arabelleğin dış GRAM 'ya aktarılmasının. Bu model, tam ekran karıştırma ve yer paylaşımlarını da destekler.

## <a name="string-encoding"></a>Dize kodlama 

GUX varsayılan olarak UTF8 biçim dize kodlamasını destekler. ***Gx_user. h*** üstbilgi dosyasında **GX_DISABLE_UTF8_SUPPORT** tanımlayarak UTF8 dize kodlaması desteği devre dışı bırakılabilir. UTF8 kodlaması devre dışıysa, GUıDX yalnızca standart 8 bit ASCII ve Latin-1 kod sayfası karakter kodlamasını kullanır. UTF8 dize kodlamasının devre dışı bırakılması, biraz daha küçük bir Gux kitaplığı ayak izine ve dize işleme ve metin çizim işlevlerinin biraz daha hızlı bir şekilde yürütülmesini sağlar.

UTF8 dize kodlaması aşağıdaki nitelikleri içerir:

  - ASCII dizeleri standart 7 bit ASCII kodlamasından daha fazla depolama alanı almaz.

  - Çoğu ANSI-C dize işlevleri, hiçbir değişiklik yapılmadan UTF8 dize kodlaması ile çalışır.

Kanji karakter kümeleri de dahil olmak üzere dünyanın tüm etkin karakter kümeleri, UTF8 dize kodlaması ile gösterilebilir.

### <a name="static-and-dynamic-strings"></a>Statik ve dinamik dizeler 

Metin görüntülemeyi destekleyen GUıDX pencere öğelerinizi atanan dizeler, normalde aşağıda açıklanan Gux dize tablosunun bir parçası olarak sabit depolamaya yerleştirilmiş olan statik olarak tanımlanmış dize sabitleri ve ***sprintf** _ veya _ *_gx_utility_ltoa_* * gibi hizmetler kullanılarak çalışma zamanında oluşturulan dizeler olan dinamik olarak tanımlanmış dizeler olabilir.

Dinamik dizeler örnekleri, bir Gux istem pencere öğesi içinde sayı olarak veya kullanıcının konum ve biçim tercihlerine göre dinamik olarak biçimlendirilen bir "saat/tarih" dizesi olarak görüntülenmiş bir değer içerebilir. Çalışma zamanında **GX_PROMPT** veya **GX_TEXT_BUTTON pencere öğeleri** gibi Guix pencere sayfalarına atanacak dizeler oluşturursanız, bu çalışma zamanı tarafından oluşturulan dizeler için depolamayı statik olarak ayırmayı seçmeniz gerekir (ör.
Genel karakter dizileri) veya dinamik bir bellek ayırıcı işlevi tanımlayabilir ve yükleyebilir ve bu pencere öğelerinin atanan metin dizelerinin özel bir kopyasını oluşturmasına yönlendiren **GX_STYLE_TEXT_COPY** stilini kullanabilirsiniz.

Dinamik olarak oluşturulan bir dizeyi tutmak ve sonra bu dizeyi **GX_STYLE_TEXT_COPY** stiline sahip olmayan bir pencere öğesine atamak için, otomatik karakter dizisi gibi geçici depolamayı kullanmanın bir programlama hatasıdır. Bu stil etkin olmadığında pencere öğesi yalnızca sağlanan dize işaretçisini kopyalar ve dize verileri statik olarak ayrılmalıdır veya pencere öğesi dize işaretçisi, beklenmeyen sonuçlar üreten çöp verilerinde büyük olasılıkla bitecektir.

### <a name="passing-gx_string-arguments"></a>GX_STRING bağımsız değişkenlerini geçirme 

GX_STRING parametresini kabul eden Gux API işlevleri, **GX_STRING. gx_string_ptr** alanı tarafından işaret edilen dizenin uzunluğunun **GX_STRING. gx_string_length** alanının değeriyle eşleştiğini her zaman doğrular. İki alan tutarlı değilse, **GX_INVALID_STRING_LENGTH** bir hata döndürülür ve çağrılan API, dize atamasını kabul etmeden döndürülür.

GUX yazılımının güvenlik açısından dikkat edilmesi gereken noktalar, ***strlen** _ veya _ *_strcpy_* * gibi standart C dize işlevlerini hiçbir zaman kullanmaz. Bu işlevlerin, genellikle bağlı uygulamalarda bu durum büyük bir süredir olan dize verileri dinamik olarak elde edildiğinde kötü amaçlı saldırılara açıktır.

Bir parametre olarak kabul edilen () sürüm 5,6 tanımlı API işlevlerinden önce Gux kitaplığı yayınları `GX_CONST GX_CHAR *text` . Bu işlevler, geriye doğru uyumluluk için hala desteklenirken, bir giriş parametresi olarak kabul edilen () tercih edilen API işlevleri tarafından kullanımdan kaldırılmıştır ve değiştirilmiştir `GX_CONST GX_STRING *string` .

Varsayılan olarak, kullanım dışı bırakılan metin işleme API 'SI, önceden yazılmış tüm uygulamaların Gux kitaplığındaki en son güncelleştirmelerle düzgün bir şekilde derlenmesine olanak tanımak için etkinleştirilir. Kullanım dışı bırakılan metin işleme API 'sini devre dışı bırakmak için **GX_DISABLE_DEPRECATED_STRING_API** tanım **_gx_user. h_*_ üst bilgi dosyasına eklenmelidir. Tüm yeni uygulamalar _ GX_DISABLE_DEPRECATED_STRING_API tanımlamalıdır*** ve yalnızca değiştirme API işlevlerini kullanmalıdır. GUX kitaplığı sürüm sürüm 5,6 veya üzeri için Gux Studio tarafından oluşturulan tüm çıkış dosyaları yalnızca değiştirme API işlevlerini kullanır.

Aşağıdaki tabloda, kullanım dışı ve yeni tanımlanmış değiştirme API 'SI işlev adları listelenmektedir:

| **Kullanım dışı Işlev adı**              | **Yenisiyle değiştirilmiş**                              |
| ------------------------------------------ | ----------------------------------------------- |
| gx_binres_language_table_load          | gx_binres_language_table_load_ext          |
| gx_canvas_rotated_text_draw            | gx_canvas_rotated_text_draw_ext            |
| gx_canvas_text_draw                     | gx_canvas_text_draw_ext                     |
| gx_context_string_get                   | gx_context_string_get_ext                   |
| gx_display_language_table_get          | gx_display_language_table_get_ext          |
| gx_display_language_table_set          | gx_display_language_table_set_ext          |
| gx_display_string_get                   | gx_display_string_get_ext                   |
| gx_display_string_table_get            | gx_display_string_table_get_ext            |
| gx_multi_line_text_button_text_set   | gx_multi_line_text_button_text_set_ext   |
| gx_multi_line_text_input_char_insert | gx_multi_line_text_input_char_insert_ext |
| gx_multi_line_text_input_text_set    | gx_multi_line_text_input_text_set_ext    |
| gx_multi_line_text_view_text_set     | gx_multi_line_text_view_text_set_ext     |
| gx_prompt_text_get                      | gx_prompt_text_get_ext                      |
| gx_prompt_text_set                      | gx_prompt_text_set_ext                      |
| gx_single_line_text_input_text_set   | gx_single_line_text_input_text_set_ext   |
| gx_system_string_width_get             | gx_system_string_width_get_ext             |
| gx_system_version_string_get           | gx_system_version_string_get_ext           |
| gx_text_button_text_get                | gx_text_button_text_get_ext                |
| gx_text_button_text_set                | gx_text_button_text_set_ext                |
| gx_text_scroll_wheel_callback_set     | gx_text_scroll_wheel_callback_set_ext     |
| gx_utility_string_to_alphamap          | gx_utility_string_to_alphamap_ext          |
| gx_widget_string_get                    | gx_widget_string_get_ext                    |
| gx_widget_text_blend                    | gx_widget_text_blend_ext                    |
| gx_widget_text_draw                     | gx_widget_text_draw_ext                     |

### <a name="guix-string-table"></a>GUX dize tablosu 

GUX dize tablosu ve dize kaynakları bir GUıDX görüntüleme örneğiyle kaydedilir.

Birden çok görüntü sisteminde bulunan her ekran kendi dize tablosuna sahiptir ve her bir ekran kendi seçtiğiniz dilde çalıştırılabilir. Diğer Gux kaynak türleri (renkler, yazı tipleri ve pixelmaps), bu kaynak türleri her bir ekran renk biçimi ve renk derinliğine özgü olduğundan, Gux görüntüleme bileşeni tarafından da korunur.

Uygulama dizesi tablonuzu el ile oluşturabilirsiniz, ancak genellikle görüntüleme dizesi tablosu, proje kaynak dosyanızın bir parçası olarak Gux Studio uygulaması tarafından tanımlanır. Kullanılabilir diller, kaynak üst bilgi dosyasında da tanımlanmıştır. Görüntüleme dizesi tablosu, uygulama dizelerine yönelik işaretçilerin çok sütunlu bir tablosudur. Dize tablosunun her sütunu, uygulama tarafından desteklenen bir dili temsil eder.
Uygulamanız yalnızca bir dili destekliyorsa (örneğin Ingilizce), dize tablonuzun yalnızca bir sütunu olur. Yine de, uygulama yazılımınızı değiştirmeden istediğiniz zaman ek dil desteği ekleyebilirsiniz.

Etkin dize tablosu ***gx_display_string_table_set*** API işlevi çağırarak atanır. Bu işlev, GUıDX Studio tarafından oluşturulan başlangıç kodu tarafından otomatik olarak çağrılır, ancak aynı zamanda etkin dize tablosunu değiştirmek için doğrudan uygulama tarafından çağrılabilir.

Etkin dil ***gx_display_active_language_set*** API işlevi çağırarak atanır. Bu işlev, görüntüleme dizesi tablosunun hangi sütununun etkin olduğunu belirler.

Bu işlev çağrıldığında, tüm görünür GUıDX pencere öğeleri için **GX_EVENT_LANGUAGE_CHANGE** bir olay gönderilir ve bu da yeni etkin dize verilerini görüntüleyecek şekilde güncelleştirilmesine izin verir.

Pencere öğeleri ve uygulama yazılımı, dize KIMLIĞI değerlerini ve ***gx_display_string_get_ext*** ya da ***gx_widget_string_get_ext*** API işlevlerini kullanarak statik olarak tanımlanan dizeleri çözer. Bu işlevler, belirtilen bir dize KIMLIĞI ve şu anda etkin olan dil ile ilişkili **GX_STRING** döndürür.

### <a name="bi-directional-text-display"></a>İki yönlü metin görüntüleme 

GUX iki yönlü metin desteği için iki strateji sağlar.

Bir seçenek, Gux Studio uygulamasında bidi metin yeniden sıralamayı yapmak. Bu seçeneğin kullanılması, ekran düzeninde bidi metnini çıkış dosyasına oluşturmaktan sorumludur. Bu çözüm, çalışma zamanı performansı üzerinde sıfır etkiye sahiptir ve Gux çalışma zamanı kitaplığı için herhangi bir ekleme gerektirmez. GUX Studio 'Nun displayorder bidi metin dizeleri oluşturmasına izin vermek için, Gux Studio dil yapılandırması iletişim kutusunda, **görüntüleme düzeninde bidi metni oluştur** onay kutusunu seçmeniz gerekir:

![Dilleri yapılandırma](./media/guix/user-guide/configure-languages.png)

Bu seçenekler seçiliyken, oluşturulan kaynak dosyası görüntüleme düzeninde oluşturulan bidi dizelerini içerir ve Gux çalışma zamanı kitaplığı içinde ek işlem gerekmez.

İkinci seçenek, çalışma zamanında çift yönlü metin yeniden sıralamayı yapmak. Bu seçenek, dinamik olarak tanımlanan ve Gux Studio uygulaması tarafından oluşturulmayan bidi metin dizesini işlemesi gereken uygulamalar için desteklenir. Bu durumda, Gux çalışma zamanı kitaplığı her metin dizesini çizmadan önce çift yönlü metnin yeniden sıralanması sorumludur. Bu çözümün çalışma zamanı performansı ve bellek etkisi vardır. Bidi metin yeniden sıralama işlemi için yeterli dinamik bellek kullanılabilir olmalıdır. Bu çözüm, Gux kitaplığı oluşturulurken koşullu GX_DYNAMIC_BIDI_TEXT_SUPPORT tanımlanmasını gerektirir. ***Gx_system_bidi_text_enable*** ve ***gx_system_bidi_text_disable*** iki API işlevi, çalışma zamanında çift yönlü metin desteğini etkinleştirmek/devre dışı bırakmak için verilmiştir.

Hem **GX_DYNAMIC_BIDI_TEXT_SUPPORT** hem de Gux Studio 'yu, görüntüleme düzeninde çift yönlü metin oluşturacak şekilde yapılandırmanız gerekir. Bidi metin dizesi işleme için bir strateji veya diğerini seçmelisiniz.

## <a name="memory-usage"></a>Bellek Kullanımı 

GUX, uygulama programıyla birlikte bulunur. Sonuç olarak, GUıDX 'in statik bellek (veya sabit bellek) kullanımı geliştirme araçları tarafından belirlenir; Örneğin, derleyici, bağlayıcı ve bulucu. Dinamik bellek (veya çalışma zamanı belleği) kullanımı, uygulamanın doğrudan denetimi altındadır.

### <a name="static-memory-usage"></a>Statik bellek kullanımı 

Geliştirme araçlarının çoğu, uygulama programı görüntüsünü beş temel alana böler: *yönerge*, *sabit*, *başlatılan veriler*, *başlatılmamış veriler* ve *guıdx iş parçacığı yığını*. Şekil x sayfasında bu bellek alanlarının bir örneği gösterilir.

Bunun yalnızca bir örnek olduğunu anlamak önemlidir. Gerçek statik bellek düzeni işlemci, geliştirme araçları, temel alınan donanım ve uygulamanın kendisi için özeldir.

Yönerge alanı, programın işlemci yönergelerini içerir. Bu alan genellikle ROM ' da bulunur.

Sabit alan, varsayılan ayarları ve tüm uygulama kaynaklarını (görüntüler, dizeler, yazı tipleri ve renkler) içeren, farklı derlenmiş sabitler içerir. Ayrıca, bu alan başlatılan veri alanının "ilk kopyasını" içerir. Derleyicinin başlatma işlemi sırasında, sabit alanın bu bölümü RAM 'de Genel başlatılmış verileri ayarlamak için kullanılır. Sabit alan genellikle en büyüktür ve genellikle yönerge alanını izler ve genellikle ROM ' da bulunur.

GUX pixelmaps ve yazı tipleri genellikle büyük miktarda sabit veri depolaması gerektirir. Bu büyük statik veri alanı normalde ROM veya FLASH 'ta tutulur.

GUX iş parçacığı yığını, ***gx_system. h*** dosyasında başlatılmamış veri alanı (genel değişken olarak) içinde aşağıdaki gibi tanımlanır:

```C
_gx_system_thread_stack[GX_THREAD_STACK_SIZE];
```

**GX_THREAD_STACK_SIZE** , **_gx_port. h_** içinde tanımlanmıştır, ancak bu sembol ***gx_user. h*** üstbilgi dosyasında ya da proje seçenekleri ya da komut satırı parametreleri aracılığıyla tanımlayarak uygulama tarafından geçersiz kılınabilir. Yığın boyutu, en kötü durum olay işleme ve iç içe çizim çağrılarını işleyecek kadar büyük olmalıdır.

### <a name="dynamic-memory-usage"></a>Dinamik Bellek kullanımı 

Daha önce belirtildiği gibi, dinamik bellek kullanımı uygulamanın doğrudan denetimi altındadır. Canvaler, vb. ile ilişkili denetim blokları ve bellek, hedefin bellek alanında herhangi bir yere yerleştirilebilir. Bu önemli bir özelliktir çünkü çalışma zamanında farklı türlerdeki fiziksel belleğin kolay kullanımını kolaylaştırır.

Örneğin, bir hedef donanım ortamının hem hızlı bellek hem de yavaş bellek olduğunu varsayalım. Uygulamanın çizim için ek performansa ihtiyacı varsa, en iyi performans için tuval belleği yüksek hızlı bellek alanına açık bir şekilde yerleştirilebilir.

Birçok isteğe bağlı Gux hizmeti ve özelliği, genellikle yığın olarak adlandırılan bir çalışma zamanı dinamik bellek ayırma mekanizması gerektirir. Bu hizmetler ve özellikler tamamen isteğe bağlıdır ve birçok GUıDX uygulaması herhangi bir yığın kullanmaz ve bir çalışma zamanı bellek ayırma mekanizması tanımlamaz.

Çalışma zamanı bellek ayırmayı gerektiren hizmetleri kullanacaksanız, bellek dinamik olarak ayrıldığınızda veya serbest bırakıldığında Gux 'in çağırabileceği işlevleri yüklemelisiniz. Bu işlevleri tercih ettiğiniz şekilde uygulayabilirsiniz, böylece bu durumda dinamik bellek havuzunun konumu uygulama denetimi altındadır. Dinamik bellek ayırma desteğini yüklemek için, uygulama, bellek ayırmayı ve bellek ücretsiz hizmetlerinizi tanımlamak üzere program başlatılırken API hizmeti ***gx_system_memory_allocator_set*** çağırmalıdır. Tüm örnek için bu API 'nin belgelerine bakın.

Çalışma zamanı belleği ayırmayı ve ayırmayı kaldırma hizmetini gerektiren GUıDX Hizmetleri şunları içerir:

  - Dış depolamadan Gux çalışma zamanı ortamına ikili kaynakları yükleme.

  - Yazılım çalışma zamanı JPEG görüntü kod çözücüsü.

  - Yazılım çalışma zamanı PNG resmi kod çözücüsü.

  - GX_STYLE_TEXT_COPY ile metin pencere öğeleri kullanma.

  - Çalışma zamanı Pikselleştirme yeniden boyutlandırma ve döndürme yardımcı programı işlevleri.
  - Çalışma zamanı ekranı ve pencere öğesi denetim bloğu ayırması.

Daha küçük uygulamalar için, GUıDX kaynakları genellikle uygulama görüntüsünün parçası olarak derlenir ve statik olarak bağlanır ve ikili kaynak yüklemesi gerekli değildir. İkili kaynaklar bir uygulamanın, Flash sürücü veya URL gibi bazı depolama konumlarından yüklenen çalışma zamanında kaynakları (yazı tipleri, görüntüler, diller) yüklemesine olanak tanır.

Çalışma zamanı JPEG ve PNG kod çözücüleri isteğe bağlı bileşenlerdir. En Gux uygulamalar, Gux Studio aracının tüm gerekli görüntü dosyalarını önceden çözmelerine ve bunları özel Gux Pikselemap veri kaynakları olarak depolamasına olanak sağlar. Bu hizmetler, JPEG ve/veya PNG görüntülerinin çalışma zamanı dönüştürülmesini gerektiren uygulamalar için pixelmap biçimine yönelik olarak sağlanır.

**GX_STYLE_TEXT_COPY** , kullanıcının belirli bir pencere öğesi ya da pencere öğelerinin, dinamik olarak atanan metnin özel kopyasını tutabileceklerini belirtmesini sağlar. Bu seçeneği kullanmak için bellek ayırma mekanizmasının kullanılmadan önce yüklenmesi gerekir. Bir metin türü pencere öğesi oluşturulduğunda bu stil **<span class="underline">bayrağı sağlanmazsa,</span>** uygulamanın dinamik olarak oluşturulan ve atanan tüm metin dizeleri için statik depolama alanı ayırması gerekir. Çalışma zamanı tarafından oluşturulan dize verilerini tutmak için otomatik değişkenlerin bu durumda kullanılması gerekir. **GX_STYLE_TEXT_COPY** stili etkinse, her pencere öğesi atanan metnin kendi kopyasını oluşturduğundan, her bir pencere öğesi için otomatik değişkenler, guıdx Pencere öğelerinin atandığı dize verilerini tutmak için kullanılabilir.

Pixelmap yeniden boyutlandırma ve döndürme yardımcı programı işlevleri, elde edilen çevrilmiş pixelmap 'i uygulama için kullanılabilir yeni bir pixelmap olarak döndürür.
Bu hizmetler kullanılıyorsa, bu çalışma zamanının üretilen pixelmap veri bloklarını barındırmak için yeterli dinamik bellek kullanılabilir olmalıdır.

Son olarak, GUıDX ekranları ve pencere öğeleri için denetim blokları statik veya dinamik olarak tahsis edilebilir. Daha küçük uygulamalar için, program başlangıcında tüm uygulama ekranlarını oluşturmak ve statik olarak ayrılan denetim blokları kullanmak yaygındır. Büyük uygulamalar için, ekran ve alt pencere öğesi denetimlerini, gerekli bir tabanda dinamik olarak oluşturmak yaygındır. Dinamik olarak ayrılan denetim blokları, Gux Studio özellikleri görünümünde **çalışma zamanı ayırma** onay kutusu seçilerek veya Standart API aracılığıyla pencere öğesi oluşturulurken **GX_STYLE_DYNAMICALLY_ALLOCATED** stil bayrağına geçerek belirtilir. Dinamik olarak ayrılan pencere öğesi denetim bloklarının kullanılması, bellek ayırma ve ayırmayı kaldırma hizmetlerinin yukarıda açıklanan şekilde tanımlanmasını gerektirir.

## <a name="guix-components"></a>GUX bileşenleri 

GUX API 'Leri bölünür ve Gux sisteminin temel bileşenlerine karşılık gelen çeşitli temel gruplar halinde düzenlenir. Temel bileşenler şunlardır:

| <!-- -->    | <!-- -->    |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GX_SYSTEM  | GUX sistem bileşeni, başlatma, olaylar, zamanlayıcılar, dize tabloları ve görünür pencere öğesi hiyerarşi yönetiminden sorumludur.                                                                                                                                                                                                                                                                      |
| GX_CANVAS  | Bir çizim alanı. Bir tuval, donanım çerçeve arabelleğinin ince bir soyutlaması olabilir veya bir saf bellek tuvali de olabilir. Tuval türü gx_canvas_create API işlevine geçirilen parametrelere göre belirlenir.                                                                                                                                                                                   |
| GX_CONTEXT | Çizim bağlamı bileşeni. Çizim bağlamı, geçerli çizim işlemleri için ekran, tuval ve fırça ve kırpma alanı hakkında bilgiler içerir.                                                                                                                                                                                                                                      |
| GX_DISPLAY | , Uygulamanızın ve Gux Pencere öğelerinin tuvalde çizim gerçekleştirmesine izin vermek için API 'Ler ve sürücü düzeyi uygulamalar sağlar. GX_DISPLAY, tuvalin gerekli renk biçimini kullanarak her tuvalde grafikleri doğru şekilde işlemek için uygulanır. GX_DISPLAY bileşeni, her bir görüntüleme ile bağlantılı olarak pencere öğeleri çizimi için kullanılabilir kaynakları (renkler, yazı tipleri ve pixelharitalar) yönetir. |
| GX_WIDGET  | Temel görünür pencere öğesi nesnesi ve ilişkili API 'Ler. Tüm GUıDX pencere öğesi türleri temel GX_WIDGET türünden dayanır veya türetilir.                                                                                                                                                                                                                                                                      |
| GX_UTILITY | Dikdörtgenlerle çalışmaya yönelik yardımcı program işlevleri, dize dönüştürme işlevleri ve ANSI olmayan matematik işlevleri bu gruba dahil edilir.                                                                                                                                                                                                                                                         |

Bu temel bileşenlere ek olarak, GUıDX, kitaplıkta belirtilen her pencere öğesi türüne özgü API 'Leri içerir. Bu API 'Ler, bu kullanıcı kılavuzunun Bölüm 4 ' te "Gux Services açıklaması" bölümünde açıklanmaktadır.

## <a name="guix-system-component"></a>GUIX sistem bileşeni

GUX sistem bileşeni, UI uygulaması için genel olan çeşitli hizmetler sunar. Bu hizmetler şunları içerir: *başlatma, olay yönetimi, görüntüleme yönetimi, kaynak yönetimi, Zamanlayıcı yönetimi* ve *pencere öğesi yönetimi*. Her hizmet, uygulama programınızın organizasyonu için gereklidir ve bu hizmetler aşağıdaki alt bölümlerde daha ayrıntılı olarak açıklanmıştır.

### <a name="initialization"></a>Başlatma 

GUX başlatma, uygulama tarafından ThreadX ***tx_application_define*** yordamından (başlatma bağlamından) veya uygulama iş parçacıklarından çağrılabilen hizmet ***gx_system_initialize*** çağıran uygulama tarafından gerçekleştirilir. ***Gx_system_initialize*** işlevi tüm genel guıdx veri yapılarını başlatır ve Gux sistem mutex 'i, olay kuyruğunu, süreölçeri ve iş parçacığını oluşturur. ***Gx_system_initialize*** döndüğünde, uygulama Gux kullanabilir.

### <a name="thread-processing"></a>İş parçacığı Işleme 

Başlatma sırasında oluşturulan iç Gux iş parçacığı-Gux ' teki çoğu işlemin sorumluluğundadır. Bu iş parçacığındaki işlem ilk olarak, temel alınan görüntü sürücüsünün gerektirdiği ek başlatma işlemini tamamlar. Bu işlem tamamlandıktan sonra, GUıDX iş parçacığı, önce Gux olay kuyruğunda bulunan tüm olayları işleyen bir döngü girer ve gerekirse ekranı yeniler. Ekran yenilemesi, görünür hale ve bu işlevin yeniden çizilmesini gerektiren kirli bir anlamı temel alarak gerekli Gux çizim işlevlerini yürütür. Hiçbir olay olmadığında ve ekranda yenilenmek üzere hiçbir şey kalmadığında, Gux iş parçacığı askıya alınır ve sonraki Gux olayının gelmesi bekleniyor.

### <a name="rtos-binding"></a>RTOS bağlama 

GUX sistem bileşeni varsayılan olarak, iş parçacığı Hizmetleri, olay kuyruğu Hizmetleri ve Zamanlayıcı Hizmetleri gibi hizmetler için ThreadX gerçek zamanlı işletim sistemini kullanacak şekilde yapılandırılmıştır. GUX, Önişlemci yönergesini GX_DISABLE_THREADX_BINDING ve Gux kitaplığını yeniden oluşturarak diğer işletim sistemlerine kolayca eklenebilir. Bu, Gux kaynak kodundan alınan ThreadX bağımlılıklarını kaldırır ve uygulama geliştiricisinin hedef sistem tarafından belirtilen RTOS 'yi kullanarak gerekli işletim sistemi hizmetlerini uygulamasına izin verir. [Ek F-Gux RTOS bağlama hizmetleri](appendix-f.md) , Gux bağlantı noktası Için threadx işletim sistemi dışında bir işletim sistemine uygulanması gereken hizmetleri tanımlar.

### <a name="multithread-safety"></a>Çoklu iş parçacığı güvenliği 

GUX API 'SI, Gux iş parçacığı bağlamından ve diğer uygulama iş parçacıklarından kullanılabilir. Uygulama iş parçacıkları,, paylaşılan değişkenlere erişime ve Gux API işlevlerinin kullanılmasıyla birlikte olayları gönderip alarak, Gux iş parçacığı ile etkileşime geçebilir. GUIX, çok iş parçacığı kaynak koruması için bir iç ThreadX mutex kullanır. Ayrıca, GUıDX, ekran yenileme işlemi başladıktan sonra görünür pencere öğelerinin iç yapısının değiştirilmesini engeller. Görünür nesneler ağacını değiştirecek API 'Ler, çizim işlemleri devam ederken engellenir ve ekran yenilemesi tamamlandıktan sonra serbest bırakılır.

### <a name="system-timers"></a>Sistem süreölçerleri 

GUX, her zaman Gux Windows 'ta görüntülenen verilerin düzenli olarak güncelleştirilmesi için kullanılan dönemsel zamanlayıcılar sağlar. Bu, bir ThreadX dönemsel süreölçeri aracılığıyla yapılır, bu da ekran belirme/genişletme gibi Gux sistem düzeyi etkileri gerçekleştirmek için de kullanılır, vb.

Uygulama zamanlayıcılar oluşturabilir ve Gux tarafından dahili olarak kullanılan Zamanlayıcı özelliğini kullanabilir. Kuşkusuz, uygulama gerekirse ThreadX zamanlayıcılarını doğrudan oluşturabilir ve kullanabilir. GUX zamanlayıcıları 'nın avantajı, kullanımı çok kolay ve Gux olay odaklı işleme sistemi içinde çalışacak şekilde önceden yapılandırılmıştır.

Bir GUıDX süreölçeri oluşturup başlatmak için, uygulama ***gx_system_timer_start*** işlevi çağırmalıdır. Bu işleve yönelik parametreler, çağıran pencere öğesi, Zamanlayıcı kimliği (bir pencere öğesinin birçok Zamanlayıcı başlatmasına izin veriliyor) ve ilk ve yeniden zamanlama zaman aşımı değerlerini içerir. Yeniden zamanlama zaman aşımı değeri 0 ise, süreölçer yalnızca bir kez çalışır ve süresi dolduktan sonra etkin Zamanlayıcı listesinden kendisini siler.

Başlatıldıktan sonra, Gux süreölçeri Zamanlayıcı sahibine bir kez veya zamanlayıcı yeniden zamanlama değerine göre düzenli olarak GX_EVENT_TIMEOUT olayları gönderir. Bir Gux süreölçeri, ***GX_SYSTEM_TIMER_STOP*** API işlevi çağırarak durdurulabilir.

### <a name="pen-speed-configuration"></a>Kalem hızı yapılandırması 

GUX sistem bileşeni, kalem hızı izlemeyle ilgili yapılandırma bilgilerini içerir. GUX, varsa Touch giriş sürücüsü tarafından oluşturulan PEN_DOWN olaylarının hızına ve uzaklığa göre **GX_EVENT_VERTICAL_FLICK** ve **GX_EVENT_HORIZONTAL_FLICK** olaylarını temel alır. Uygulama, **_gx_system_pen_configure_** API işlevini kullanarak bu iç oluşturulan olayları tetiklemek için gereken en düşük uzaklık ve hızı yapılandırabilir.

### <a name="screen-stack"></a>Ekran yığını 

GUX sistem bileşeni, ekran yığınında, hangi ekranların gönderilebileceği, polamış ve çalışma zamanında alınan bir sanal pencere öğesi yığınını destekleyen isteğe bağlı bir işlevdir. Ekran yığını, kullanıcının menü sisteminde çeşitli durumlara ulaşmasına yol gösteren rotada karmaşık menü sistemlerini yönetmek için yararlıdır. Menü sisteminde önceki duruma dönmek, önce önceki ekran durumunu ileterek, sonra yeni ekranı görüntüleyerek ve geçerli ekran kapatıldığında yeni ekranın ekran yığınından önceki durumu açmasına izin vererek kolayca yapılabilir.

### <a name="clipboard-maintenance"></a>Pano Bakımı 

GUIX, çalışma zamanında yürütme sırasında metin kopyalayıp yapıştırarak bir panoyu destekler. Bu destek, GUıDX sistem bileşeni tarafından sağlanır.

### <a name="dirty-list-maintenance"></a>Kirli liste Bakımı 

GUX kirli pencere öğelerinin bir listesini, görünür olan ve durum değişiklikleri nedeniyle yeniden çizilmesini gereken ve yeni görünür hale getirilen Pencere öğelerinin bir listesini tutar. Bu kirli liste, Gux 'in her bir kullanıcı arabirimi değişikliği yapıldığından tuval yenilemesi yapmak yerine, tek bir tuval yenileme işlemi yapmasına izin vererek çizim performansını geliştirir.
Bu kirli liste, GUıDX sistem bileşeni tarafından da korunur.

### <a name="animation-control-block-pool"></a>Animasyon denetim blok havuzu 

Uygulamalar genellikle paralel olarak birden çok animasyon dizisi yürütmeyi ister. GUX, uygulamanın ayırabileceği ve kullanabileceği bir animasyon denetim bloğu havuzunu saklar. Bu, uygulamayı statik olarak tanımlayan bu denetim bloklarını serbest bırakır ve uygulamanın tanımlayabilecek her animasyon için benzersiz bir animasyon denetim bloğu tanımlamak yerine farklı zamanlarda yeniden kullanılabilmelerini sağlar. Animasyon denetim bloğu havuzu, GUıDX sistem bileşeni tarafından da korunur.

### <a name="system-error-handling"></a>Sistem hatası Işleme 

GUX sistem hatası işleyicisi, API perspektifinden belirlenmesi daha zor olabilecek ve Gux 'teki iç sistem hatalarını bulmada uygulamanın yardımcı olmaya yöneliktir. GUX içinde bir sistem hatası oluştuğunda, iç ***_gx_system_error_process*** işlevi çağırılır. Bu işlev, girilen hata kodunu kaydeder ve algılanan toplam sistem hatası sayısını artırır. Sistem hatası değişkenleri aşağıdaki gibi tanımlanır:

UINT **_gx_system_last_error**;

ULONG **_gx_system_error_count**;

GUX uygulaması Strangely çalışıyorsa hata ayıklayıcıda hata sayısı değişkenine bakmak yararlı olur. Ayarlanırsa, sorunu gidermek için iyi bir yol ***_gx_system_error_process*** işlevinde bir kesme noktası ayarlamak ve ne zaman/nerede çağrılmakta olduğunu görmeniz.

## <a name="guix-canvas-component"></a>GUX tuval bileşeni

Tuval bileşeni, tuvalle ilgili tüm işlemeden sorumludur. Tuval etkin bir şekilde sanal çerçeve arabelleği olur. Uygulamanızın grafik çıkışı oluşturmak için en az bir tuval oluşturması gerekir.
Genellikle, sisteminiz tarafından desteklenen her bir fiziksel görüntü için en az bir tuval oluşturursunuz.

Tüm Gux çizimi bir tuvalde gerçekleşir. Daha basit veya bellek kısıtlı sistemlerde, daha fazla bellek ve daha gelişmiş grafik gereksinimlerine sahip sistemler birden çok canvaı gerektirebilir. Birden çok Canun bir ekran için kullanılabilir hale getirilmesi, ekran ve pencere belirme ve soluklaştırma etkileri gibi özellikler sunar.
Canvases, basit veya yönetilen iki ana türden biri olabilir.

Basit tuval, uygulama tarafından kullanılan bir ekran çizimi alanıdır.
GUX basit bir tuval ile hiçbir şey yapmaz, ancak uygulama, karmaşık çizimi bir ekran arabelleğine işlemek için basit bir tuval kullanabilir ve sonra gerektiğinde görünür tuvali yenilemek için bu ekran arabelleğini kullanabilir.

Yönetilen bir tuval, GUıDX tarafından donanım çerçeve arabelleği içinde otomatik olarak görüntülenir. Yönetilen bir tuval, birden çok yönetilen canların desteklenmesi için yeterli belleğe sahip olan sistemler için bileşik bir tuval oluşturmaya dahildir. Yönetilen canteler, GUıDX tarafından tutulan bir Z sırasına sahiptir ve tüm yönetilen cantlarla görüntü kırpması uygulanır.

Bir tuval, daha genel olması için bir çerçeve arabelleğinden farklıdır. Bellek kısıtlı sistemlerde yalnızca bir tuval olabilir ve bu tuval için bellek, görünür çerçeve arabelleği belleği olabilir. Ancak, daha gelişmiş grafik yer paylaşımlarını ve birden çok canvalarını destekleyen daha karmaşık sistemler için, yönetilen canvaler, her biri donanım çerçevesi arabellek belleğinden farklı olan kendi bellek bölgelerini ayırmıştır.
Bu yönetilen canvaler, çerçeve arabelleği yenileme veya geçiş işlemi sırasında görünür çerçeve arabelleğine işlenir.

Birden çok grafik katmanını destekleyen donanımlar, yani birden çok fazla sayıda çerçeve arabelleği için, uygulama ***gx_canvas_hardware_layer_bind*** API 'sini kullanarak bir veya daha fazla canvaı 'yi donanım grafik katmanlarına bağlayabilir. Bu hizmet, tuvalde belirli bir donanım grafik katmanıyla bağlantılı olduğunu bildirir ve bu tuval bağlandığında tuval görünürlüğü için donanım desteğini kullanmayı dener (ör. gx_canvas_show, gx_canvas_hide), tuval Alfa karıştırma (yani ***gx_canvas_alpha_set***) ve görüntü içindeki tuval kayması (***gx_canvas_offset_set***).

En basit tek tuval/tek çerçeve arabelleği organizasyonu dışındaki mimariler için, bir tuvalin boyutu uygulama tarafından belirlenir ve bir çerçeve arabelleğinin sabit boyutundan farklı olabilir.
Ayrıca, uygulama tarafından seçilen bir uzaklığında de olabilir. Z sırası gibi diğer bilgiler tuvalde korunur. Tuval çizimi tamamlandığında, tuvalin içeriği görüntüleme sürücüsü tarafından fiziksel görüntülemeye aktarılır. Ayrı bir tuval ve çerçeve arabelleği bellek alanı için yeterli belleğe sahip olmayan bazı sistemlerde, tuval güncelleştirmesi aslında görüntü sürücüsü aracılığıyla doğrudan fiziksel görüntülemeye yapılır.

### <a name="canvas-creation"></a>Tuval oluşturma 

Bir tuval nesnesi, başlatma sırasında veya uygulama iş parçacıklarının yürütülmesi sırasında herhangi bir zamanda oluşturulabilir. Bir uygulama tarafından oluşturulabilen tuval nesneleri sayısında bir sınır yoktur. Ancak çoğu uygulama, tüm Gux çizimi için yalnızca bir tuval nesnesi oluşturur.

### <a name="canvas-control-block"></a>Tuval denetim bloğu 

Her tuval nesnesinin özellikleri, denetim bloğunda **GX_CANVAS** bulunur ve **_gx_api. h_** içinde tanımlanır. Tuval nesnesi için gereken bellek, uygulama tarafından sağlanır ve bellekte herhangi bir yerde bulunabilir. Ancak, tuval nesne denetim bloğunu ve çizim alanını herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapıya getirmek en yaygın olarak kullanılır.

### <a name="canvas-alpha-channel"></a>Tuval alfa kanalı

GUIX, her piksel için bir karıştırma oranı belirten bit eşlem ve arka plan renklerinin, 16 BPP ve daha yüksek renk derinliğinde bir fırçanın karıştırma oranını belirten ve bir kaplama tuvalinin karıştırma oranını belirten bir tuval Alpha da dahil olmak üzere çok sayıda düzeyde ön plan ve arka plan renklerini Alfa karışımı destekler.

Bir tuvalin alfa değeri, çerçeve arabelleği içinde görüntülenmek üzere bir araya eklenen birden çok canvaya olduğunda kullanılır. Tuval Z düzeni diğer canvaların üzerinde yer alıyorsa, tuval alfa değeri tuvali arkasında yer alan öğelerle Blend için ayarlanabilir. Bir tuvalin Alfa değerini hızlı bir şekilde değiştirmek, "belirme" ekran geçişi efektlerini sağlamak için kullanılır, ancak tuval Alpha birçok şekilde kullanılabilir.

Bir tuval gx_canvas_hardware_layer_bind () kullanılarak bir donanım grafik katmanına bağlıysa, GUıDX, bir kaplama tuvali karıştırma ile İlişkili Yazılım ek yükünü en aza indirerek, donanım desteğinden yararlanarak tuval Alpha karışımı uygulamayı dener.

Alfa değerleri 0 ile 255 arasında değişir; burada 0 değeri, pikselin tamamen şeffaf olduğu ve 0 ' dan büyük değerlerin daha az saydam olduğu anlamına gelir ve tuval karıştırma için donanım yardımı sağlanmamışsa yalnızca 16-BPP ve üzeri sürümlerde çalışan ekran sürücüleri için desteklenir.

### <a name="canvas-offset"></a>Tuval boşluğu 

Bir tuval, ***gx_canvas_offset_set*** API hizmetini çağırarak görünür çerçeve arabelleği içinde yer alabilir. Tuval uzaklıkları genellikle Sprite animasyonlarını uygulamak için kullanılır. Bir tuval ***gx_canvas_hardware_layer_bind*** API işlevini çağırarak bir donanım grafik katmanına bağlıysa, guıdx, tuval konumunu değiştirme ile İlişkili Yazılım ek yükünü en aza indirerek donanım desteğini kullanan tuval fark değişikliklerini uygulamaya çalışır.

### <a name="canvas-drawing"></a>Tuval çizimi 

GUX tuvali bileşeni, uygulamaya tam bir çizim API 'SI sağlar. ***Gx_canvas_line_draw*** veya ***Gx_canvas_pixelmap_draw*** gibi çizim API 'leri çağrılabilmeniz için, ***gx_canvas_drawing_initiate*** API işlevini çağırarak hedef Tuvalin çizim için açılması gerekir. Bu işlev, çizim için bir tuval hazırlar ve ***Çizim bağlamı*** oluşturur.

Tuvale işlenen, ***gx_canvas_line_draw** _ veya _*_Gx_canvas_text_draw_*_ gibi çizim API 'leri, çizgi stilini, genişliği ve renkleri tanımlamak için geçerli çizim bağlamı fırçasının içinde bulunan parametreleri kullanır. Bu fırça parametreleri, _ *_gx_canvas_drawing_initiate_* * çağırarak bir çizim bağlamı kurulduktan sonra _*_gx_context_brush_define_*_, _* _gx_context_brush_set_* *, ***gx_context_brush_style_set**_ ve benzer API işlevleri çağırarak değiştirilir.

GUIX, bir ertelenmiş tuval yenileme işleminin parçası olarak pencere ve pencere öğesi çizim işlevlerini çağırdığında, hedef tuval pencere öğesi çizim işlevleri çağrılmadan önce çizim için açılır. Bu nedenle, standart pencere öğesi çizim işlevleri hedef tuvali açmak için gerekli değildir, bu, bunlar için yapılır.

Bazı durumlarda, uygulama bir tuvale hemen çizim zorlamak isteyebilir. Bu durumda, uygulama aşağıdaki adımları gerçekleştirebilir.

1. Hedef tuvali ve uygulamanın çizmek istediği tuval içindeki dikdörtgeni geçirerek ***gx_canvas_drawing_initiate*** API işlevini çağırın. 

2. İstenen çizimi gerçekleştirmek için herhangi bir sayıda tuval çizimi API 'si çağırın.

3. Çizimin tamamlandığını bildirmek için ***gx_canvas_drawing_complete*** API işlevini çağırın. Bu, tuvali görünür çerçeve arabelleğine boşaltır ve/veya sistem belleği mimarisine bağlı olarak bir arabellek geçiş işlemi tetikler.

### <a name="drawing-apis"></a>Çizim API 'Leri 

Ekrandaki tüm görsel öğeleri çizmek için Gux 'in gerektirdiği birkaç asıl çizim temel tabanı vardır. Bu çizim API 'Leri, genellikle özel bir pencere öğesi çizim işlevinin bir parçası olarak uygulama yazılımı tarafından da çağrılabilir. Bu Gux tuval çizim API 'Leri parametre doğrulama ve kırpma işlemleri yapar ve ardından kırpılan çizim koordinatlarını, donanım ve renk biçimine özgü çizim uygulamaları için görüntü sürücüsüne iletir. Bu çizim API 'SI işlevleri aşağıdaki gibi tanımlanmıştır.

- gx_canvas_alpha_set
- gx_canvas_arc_draw
- gx_canvas_block_move
- gx_canvas_circle_draw
- gx_canvas_ellipse_draw
- gx_canvas_glyphs_draw
- gx_canvas_hardware_layer_bind
- gx_canvas_hide
- gx_canvas_line_draw
- gx_canvas_offset_set
- gx_canvas_pie_draw
- gx_canvas_pixel_draw
- gx_canvas_pixelmap_blend
- gx_canvas_pixelmap_rotate
- gx_canvas_pixelmap_tile
- gx_canvas_polygon_draw
- gx_canvas_rectangle_draw
- gx_canvas_rotated_text_draw
- gx_canvas_shift
- gx_canvas_show
- gx_canvas_text_draw

Çizim API 'si Gux tuval API 'SI aracılığıyla çağrılır ve tüm çizimler gx_canvas_ * API işlevleri kullanılarak yapılır. Çizim, geçerli çizim bağlamındaki geçerli fırça kullanılarak yapılır. Yukarıdaki şekil çizim işlevlerinden herhangi biri, geçerli fırça tarafından tanımlanan şekilde anahatlı, düz renk doldurulmuş veya pixelmap olarak doldurulmuş olabilir. Şekil ana hat genişliğini, rengini veya dolguyu değiştirmek için, geçerli çizim bağlamı içinde fırçayı tanımlamak üzere gx_context_brush_ * API işlevlerini kullanın.

Yukarıdaki uygulama düzeyi çizim API 'Leri tuvalde gerçek çizim yapmayın, ancak bunun yerine, görüntü sürücü düzeyi çizim işlevini çağırmadan önce çağıranın parametrelerini doğrulayın. Sürücü düzeyi çizim işlevi aslında bir piksel verisini tuval belleğine yazar.

GUX, 1, 2, 4, 8, 16, 24 ve piksel başına 32 bit (BPP) dahil olmak üzere çeşitli renk derinlikleri için hisse veya genel ekran sürücüsü çizim işlevleri sağlar. Bazı durumlarda, varsayılan yazılım çizimi uygulaması, 2B çizim Hızlandırıcısı sağlayan bu donanım hedefleri için donanım hızlandırmalı uygulamalarla değiştirilmiştir.

### <a name="color-depth"></a>Renk derinliği 

GUX, 32-BPP ve tek renkli ve gri tonlamalı renk derinliklerini destekler. Büyük ölçüde temel alınan fiziksel görüntünün özelliklerine göre belirlenen renk derinliği desteği ve ayrıca tuval çizim alanı için gereken bellek miktarı üzerinde bir etkisi vardır. Renk derinliği desteğinin bir listesi, bu renk derinliği içindeki çeşitlemelerin kısa bir açıklamasıyla birlikte verilmiştir.

| Renk &nbsp; biçimi       | Açıklama                                                                                                   |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| 1 bit tek renkli   | piksel olarak paketlenmiş biçim başına 1 bit.                                                                                                   |
| 2 bit gri tonlamalı    | 4 gri düzey, her bayt için dört piksel.                                                                                      |
| 4 bit gri tonlamalı    | 16 gri düzey, bayt başına iki piksel.                                                                                      |
| 4 bit renk        | VGA biçim düzlem belleği organizasyonu.                                                                                         |
| 8 bit gri tonlamalı    | 256 gri düzeyler                                                                                                                  |
| 8 bit palet modu | Palet dizini olarak kullanılan piksel başına 1 bayt                                                                                           |
| 8 bit r:g: b modu   | Daha az yaygın olarak kullanılan 2:3:2 r:g: b biçimi.                                                                                         |
| 16 bit             | Her piksel iki bayt gerektirir. R:g: b veya b:g: r bayt sıralaması olabilir. Normalde 5:6:5 yapısı, ancak 5:5:5 yapısı veya 4:4:4:4 a:r: g:b yapısı da olabilir. |
| 24 bit             | Her piksel 3 (paketlenmiş biçim) veya 4 (paketi açılmış biçim) bayt gerektirir. R:g: b veya b:g: donanım tarafından istenen şekilde r bayt sıralaması içinde olabilir. |
| 32 bit             | Her piksel bir alfa kanalı ile 4 bayt gerektirir. Can r: g:b veya b:g: r:a bayt sırası ve donanımla belirlenir.              |

### <a name="mouse-support"></a>Fare desteği 

GUIX, istenen tuvalde fare imlecini çizmeyi destekler. Fare imleci yazılımda çizilirken veya donanım imleç kaplaması tarafından destekleniyor olabilir. Her iki durumda da, fare imleç desteğiyle ilgili uygulamaya sunulan API, yazılım veya donanım fare imleç çizimi ile aynı olup olmadığına benzer.

GUX fare desteği yalnızca, `#define GX_MOUSE_SUPPORT` Gux kitaplığını oluşturmadan önce gx_user. h üstbilgi dosyasında tanımlanmışsa etkinleştirilir.

Uygulama, ***gx_canvas_mouse_define*** API işlevini kullanarak fare imlecini ve etkin noktayı tanımlamalıdır. Bu API, imleç resminin çizilmesi gereken tuvale yönelik bir işaretçi ve fare imleci görüntüsünü ve görüntünün sol üst köşesine göre fare resminin etkin olmasını tanımlayan **GX_MOUSE_CURSOR_INFO** yapısına yönelik bir işaretçi kabul eder.

## <a name="guix-display-component"></a>GUX görüntü bileşeni 

Görüntüleme bileşeni, her bir veya daha fazla canvau, pencere öğesi ve pencere içerdiği tüm görüntüleme nesnelerinin işlenmesini yönettiği için, GUıDX içinde temel bir. Görüntü bileşeni aynı zamanda bir dizi işlev işaretçisi aracılığıyla her bir ekranla ilişkili temel alınan donanım ekran sürücüsüyle etkileşime girer.

### <a name="display-creation"></a>Görüntüleme oluşturma 

Bir görüntüleme nesnesi başlatma sırasında veya uygulama iş parçacıklarının yürütülmesi sırasında herhangi bir zamanda oluşturulabilir. Genellikle bir uygulama, her fiziksel ekranı yönetmek için bir görüntüleme nesnesi oluşturur. Uygulamanızı ve kullanılabilir fiziksel ekranları tanımlamak için Gux Studio kullandıysanız, görüntülerinizin her birini oluşturmak ve başlatmak için gx_studio_display_configure API işlevini kullanırsınız.

### <a name="display-control-block"></a>Görüntüleme denetim bloğu 

Her bir görüntüleme nesnesinin özellikleri, denetim bloğunda ***GX_DISPLAY** _ bulunur ve _ *_gx_api. h_* * içinde tanımlanmıştır. Bir görüntüleme nesnesi için gereken bellek, uygulama tarafından sağlanır ve bellekte herhangi bir yerde bulunabilir. Ancak, herhangi bir işlevin kapsamı dışında tanımlayarak, görüntüleme denetiminin genel yapıyı engellemesini sağlamak en yaygın olarak kullanılır.

### <a name="resource-management"></a>Kaynak Yönetimi 

Kaynaklar, uygulamanın gerektirdiği Kullanıcı arabirimi bileşenleridir, ancak uygulama kodu değildir. Kaynaklar uygulama verileri olur ve genellikle statik olarak tanımlanır. Kaynak türleri arasında pixelmaps, yazı tipleri, renkler ve dizeler bulunur. Bu kaynaklar, genellikle herhangi bir uygulama yazılımını değiştirmeksizin herhangi bir zamanda değiştirilebilir. Uygulama yazılımında yapılan değişiklikler genellikle ilgili yazılımın yeniden test edilmesi ve doğrulanması gerektiğinden, uygulama kodunu değiştirmeden Kullanıcı arabirimi görünümü değişikliğine izin vermek için uygulama yazılımından ayrılan kaynaklara yönelik depolamanın ve başvuruların tutulması önemlidir.

GUX ***görüntüleme*** modülü, ekran renk derinliğine ve görüntü biçimine bağlı olan tüm kaynaklar için kaynak yönetimi olanakları sağlar. Bu tesisler, etkin pixelmap tablosu, etkin yazı tipi tablosu ve etkin renk tablosunun korunmasından daha fazlasını içerir. Dize kaynakları normalde renk derinliğine ve biçime göre değiştirilmemelidir, dize tablosu kaynağı Gux sistem modülü tarafından korunur.

Uygulama yazılımı kaynaklarına kaynak kimliğine göre başvurur, bu da karşılık gelen kaynak tablosuna bir dizindir. Bu, tablonun değiştirilmesine izin verir, örneğin, bir ürün "gün modu" iken "gece modu" olarak değiştiğinde ancak renk KIMLIĞI değerleri aynı kalacaksa renk tablosu değiştirilebilir.

Uygulama kaynaklarınız, GUıDX Studio uygulaması tarafından bir kaynak dosyasına (veya kaynak dosyaları kümesine) yazılır. Varsayılan renkler, pixelmaps ve yazı tipleri, yeni bir Gux Studio projesi oluşturduğunuzda otomatik olarak sağlanır, ancak uygulamanızın görünümünü ve hisyi tanımladığınızda bu varsayılanlar kolayca değiştirilmiştir.

Renkler, yazı tipleri ve pixelmaps için kaynak kimliklerinin, etkin görüntü bileşeni bilinene kadar gerçek renklerine, yazı tipine veya pixelmap değerlerine çözümlenemeyeceğini unutmayın. GUX mimarisi birden çok etkin ekranı desteklediğinden, kaynak kimlikleri yalnızca bir pencere öğesi ve ilişkili kaynak KIMLIĞI belirli bir ekranda çözümlenebiliyorsa kaynak değerlerine çözülebilir. Bu özellik dinamik bağlama olarak bilinir. Metin rengi gibi bir özelliğin kaynak KIMLIĞI, örneğin GX_COLOR_ID_TEXT kaynak KIMLIĞI **,** bir ekranda kullanıldığında beyaz için bir 16 BIT r:g: B değeri çözümleyebilir, ancak aynı renk kimliği, başka bir ekranda kullanıldığında tek renkli siyah renk değerine çözümleyebilir.

Bu uygulamada, kaynak değerlerine kaynak kimliklerinin dinamik olarak bağlanması, uygulama yazılımının ve Gux iç bileşenlerinin çoğu zaman yalnızca etkin bir çizim bağlamı içindeki kaynak değerleriyle kaynak kimliklerini çözmesi anlamına gelir. Etkin bir çizim bağlamı, Gux 'in her kaynak KIMLIĞINI belirli bir kaynak değerine çözümlemesine izin veren şu anda etkin olan ekranı belirtir. Uygulama yazılımının bir çizim bağlamı dışında belirli bir kaynak değerini bulması gerekiyorsa, bu, görünür pencere öğeleri için de yapılabilir. Görünür pencere öğeleri, etkin tuvali çözümlemek ve bu pencere öğesi için göstermek için de kullanılabilen bir kök pencereye bağlıdır.

Bir pencere öğesi oluşturulmadıysa ancak henüz görüntülenmiyorsa (yani herhangi bir kök pencereye veya başka bir görünmeyen üst öğeye bağlanmadıysa), bu pencere öğesiyle ilişkili tüm kaynak kimlikleri, belirli bir görüntülemeye atanan kaynak tablosunda doğrudan dizin oluşturma dışında, belirli bir kaynak değerine çözümlenemez. Belirli bir kaynak tablosuna doğrudan erişim uygulama yazılımı tarafından güvenli bir şekilde yapılabilir, ancak iç Gux kitaplığı yazılımında hiçbir şekilde yapılmazlar.

### <a name="widget-defaults"></a>Pencere öğesi Varsayılanları 

GUX görüntü bileşeni ayrıca çeşitli pencere öğesi öznitelikleri için varsayılan tanımlar sağlar. Aksi takdirde uygulama tarafından belirtilmediği takdirde, pencere öğeleri/pencereler bu sistem öznitelikleriyle oluşturulur. Bu sistem öznitelikleri, genellikle sistem kaynak tablolarında tutulan yazı tiplerinin, renklerin ve Bit eşlemlerin birleşiminden oluşur. Varsayılan ScrollBar görünümü görünümleri için ek öznitelikler de Gux görüntüleme bileşeni tarafından korunur.

Varsayılan renk ayarları, her bir ekran için atanan renk tablosu ve önceden tanımlanmış varsayılan renk kimliklerine göre tanımlanır. Bu varsayılan renk kimlikleri şunlardır.

| Renk KIMLIĞI | Açıklama |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| GX_COLOR_ID_CANVAS | Varsayılan tuval (örn. arka plan ekran) rengi |
| GX_COLOR_ID_WIDGET_FILL | Varsayılan pencere öğesi dolgusu rengi |
| GX_COLOR_ID_WINDOW_FILL | Varsayılan pencere dolgusu rengi |
| GX_COLOR_ID_DISABLED_FILL | Varsayılan devre dışı pencere öğesi dolgusu rengi |
| GX_COLOR_ID_DEFAULT_BORDER | Varsayılan pencere öğesi kenarlık rengi |
| GX_COLOR_ID_WINDOW_BORDER | Varsayılan pencere kenarlığı rengi |
| GX_COLOR_ID_TEXT | Varsayılan metin rengi |
| GX_COLOR_ID_SELECTED_TEXT | Varsayılan seçili metin rengi |
| GX_COLOR_ID_DISABLED_TEXT | Varsayılan devre dışı metin rengi |
| GX_COLOR_ID_SELECTED_TEXT_FILL | Varsayılan seçili metin dolgusu rengi |
| GX_COLOR_ID_READONLY_TEXT | Varsayılan salt okunur metin rengi |
| GX_COLOR_ID_READONLY_FILL | Varsayılan salt okunur metin dolgusu rengi |
| GX_COLOR_ID_SCROLL_FILL |    ScrollBar dolgusu rengi |
| GX_COLOR_ID_SCROLL_BUTTON | Kaydırma çubuğu düğme dolgusu rengi |
| GX_COLOR_ID_SHADOW | Varsayılan gölge rengi |
| GX_COLOR_ID_SHINE | Varsayılan vurgu rengi |
| GX_COLOR_ID_BUTTON_BORDER | Düğme pencere öğesi kenarlık rengi |
| GX_COLOR_ID_BUTTON_UPPER | Düğme pencere öğesi üst dolgusu rengi |
| GX_COLOR_ID_BUTTON_LOWER | Düğme pencere öğesi alt Fill Color |
| GX_COLOR_ID_BUTTON_TEXT | Düğme pencere öğesi metin rengi |
| GX_COLOR_ID_TEXT_INPUT_TEXT | Metin girişi pencere öğesi metin rengi |
| GX_COLOR_ID_TEXT_INPUT_FILL | Metin girişi dolgusu rengi |
| GX_COLOR_ID_SLIDER_TICK | Kaydırıcı değer çizgilerini çizmek için kullanılan renk. |
| GX_COLOR_ID_SLIDER_GROOVE_BOTTOM | Kaydırıcı oluk çizmek için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_OUTLINE | İğne ana hattını çizmek için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_FILL | Kaydırıcı iğne dolgusu için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE1 | İğne vurgulaması çizmek için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE2 | İğne gölgesi çizmek için kullanılan renk |

Bu renk KIMLIĞI değerleri, her bir görüntülemeye atanan renk tablosu tarafından tanımlanan belirli bir renk değerine eşlenir. Bu varsayılanlar, ***gx_display_color_table_set*** API işlevi çağırarak bir görüntüleme için Grup olarak değiştirilebilir. GUIX Studio kullanıyorsanız, uygulamanız ***gx_studio_display_configure*** işlevini çağırdığında görüntüleme rengi tablosu otomatik olarak başlatılır.

GUX görüntü bileşeni de varsayılan bir yazı tipi tablosu saklar. Varsayılan yazı tipi tablosu, uygulama tarafından özel olarak belirtilmedikçe her pencere öğesi türü tarafından kullanılan yazı tipini tanımlar. Önceden tanımlanmış görüntüleme yazı tipi tablo kimlikleri aşağıdaki değerleri içerir.

| Yazı tipi &nbsp; kimliği | Açıklama |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------|
| GX_FONT_ID_DEFAULT | Belirli bir yazı tipi tanımlanmadığında kullanılan varsayılan yazı tipi |
| GX_FONT_ID_BUTTON | Düğmelerdeki tüm metinler için kullanılan varsayılan yazı tipi |
| GX_FONT_ID_TEXT_INPUT | Metin düzenleme alanları için kullanılan varsayılan yazı tipi |

Herhangi bir metin türü pencere öğesi tarafından kullanılan yazı tipi KIMLIĞI, metin ile ilgili her pencere türü için belirtilen **gx_<widget_type>_font_set** API kullanılarak yeniden atanabilir. Tüm yazı tipi tablosu **gx_display_font_table_set** API işlevi çağırarak yeniden atanabilir.

### <a name="scrollbar-appearance"></a>Kaydırma çubuğu görünümü 

GUX ekranı Ayrıca bu görüntü için varsayılan kaydırma çubuğu görünüm ayarlarını korur. Bu ayarlar, aşağıda tanımlanan **GX_SCROLLBAR_APPEARANCE** yapısı tarafından tanımlanır. GUX görünümü dikey kaydırma çubukları için bir ScrollBar görünümü ve yatay kaydırma çubuklarının ikinci yapısını tutar. Uygulama, bir **GX_SCROLLBAR_APPEARANCE** yapısını başlatarak ve apı işlevini ***gx_display_scroll_appearance_set*** çağırarak herhangi bir görüntü için varsayılan kaydırma çubuğu görünümünü değiştirebilir.

```c
typedef struct GX_SCROLLBAR_APPEARANCE_STRUCT
{
    GX_VALUE       gx_scroll_width;
    GX_VALUE       gx_scroll_thumb_width;
    GX_VALUE       gx_scroll_thumb_travel_min;
    GX_VALUE       gx_scroll_thumb_travel_max;
    GX_UBYTE       gx_scroll_thumb_border_style;
    GX_RESOURCE_ID gx_scroll_fill_pixelmap;
    GX_RESOURCE_ID gx_scroll_thumb_pixelmap;
    GX_RESOURCE_ID gx_scroll_up_pixelmap;
    GX_RESOURCE_ID gx_scroll_down_pixelmap;
    GX_RESOURCE_ID gx_scroll_thumb_color;
    GX_RESOURCE_ID gx_scroll_thumb_border_color;
    GX_RESOURCE_ID gx_scroll_button_color;
} GX_SCROLLBAR_APPEARANCE;
```
| GX_SCROLLBAR_APPEARANCE yapısı üyesi | Açıklama |
| --- | --- |
| gx_scroll_width | Dikey kaydırma çubuğunun genişliği veya yatay kaydırma çubuğunun yüksekliği piksel cinsinden. |
| gx_scroll_thumb_width | Asansör ve bitiş düğmelerinin piksel cinsinden genişliği. |
| gx_scroll_thumb_travel_max | Kaydırma çubuğunun sonundan en fazla kaydırma düğmesi seyahat noktası arasındaki fark. |
| gx_scroll_fill_pixelmap | Kaydırma arka planını doldurmanız için pixelmap kullanıldı. |
| gx_scroll_thumb_pixelmap | Kaydırma parmak izi düğmesini çizmek için kullanılan pixelmap. |
| gx_scroll_up_pixelmap | Kaydırma düğmesini çizmek için kullanılan pixelmap. |
| gx_scroll_down_pixelmap | Kaydır aşağı kaydırma düğmesini çizmek için kullanılan pixelmap. |
| gx_scroll_fill_color | Kaydırma çubuğu arka planını doldururken kullanılan rengin renk KIMLIĞI. |
| gx_scroll_button_color | Kaydırma çubuğu düğmesini dolduracak şekilde kullanılan rengin renk KIMLIĞI. |

Yazı tipi, renk ve stiller için bu varsayılan ayarların yanı sıra, uygulama her bir pencere öğesi türü tarafından sağlanmış olan API 'YI kullanarak istediğiniz şekilde bir servis talebiyle ilgili parametrelerden herhangi birini belirtebilir.

### <a name="skinning-and-themes"></a>Kaplama ve Temalar

Kaplama, GUıDX Pencere öğelerinin ve Windows 'un temel görünümlerini kolayca değiştirmesini sağlar, yani "Skin" ın tek bir yerde değiştirilmesi, ilişkili tüm pencere öğelerinin ve pencerelerin temel görünümünü değiştirir.

GUX uygulamanızı yeniden kaplama için, GUıDX görüntüleme kaynak tablolarına yeni bir Color, font ve veya pixelmap tablosu sağlamanız gerekir. Tüm Gux pencere öğeleri, kaynak KIMLIĞINE göre rengine, bit eşlemlerine veya yazı tipine başvurduğundan, yeni bir kaynak tablosu sağlanması otomatik olarak tüm Gux Pencere öğelerinin, kendilerine istenen ekranda çizim yaparken yeni renklerinizi ve pixelmaps kullanmaya başlamasını sağlar.

Etkileyici bir görünüm sağlamak için birlikte çalışmak üzere tasarlanan yeni bir yazı tipi, renk ve pixelmaps kümesi, *Tema* olarak adlandırılır. Bir tema, kaynak tablolarının bir kümesini ve her bir kaynak tablosunun boyutunu tanımlar. Herhangi bir sayıda tema, GUıDX Studio uygulaması kullanılarak herhangi bir görüntü için tanımlanabilir. Başlangıç teması dizinini, oluşturulan ekranda ilk temayı yükleyecek olan ***gx_studio_display_configure*** Gux Studio tarafından oluşturulan işleve geçirmeniz gerekir. Herhangi bir ekran için etkin tema, ***gx_display_theme_install*** işlevi çağırarak herhangi bir zamanda değiştirilebilir.

### <a name="root-window"></a>Kök pencere

Bir uygulama tarafından oluşturulan her görünebilir tuval için, uygulamanın Ayrıca bu tuval için bir kök pencere oluşturması gerekir. Bu özel pencere, temel olarak tüm üst düzey uygulama pencereleri ve pencere öğeleri için bir kapsayıcı görevi görür. Kök pencere, tuval arka planını çizer ve kök pencere **GX_WINDOW** sınıftan türetildiğinden, kök pencerenin duvar kağıdı de olabilir. Görüntü veya tuvaliniz arka plan rengini değiştirmek için, bu tuvale eklenmiş olan kök pencerenin Fill rengini değiştirmeniz yeterlidir.

Görüntülerinizi yapılandırmak için ***gx_studio_display_configure*** adlı Guıdx Studio generated işlevini kullanırsanız, bu başlatma işlevinin bir parçası olarak her bir ekran için tuval ve kök pencere oluşturulur.

### <a name="anti-aliasing"></a>Kenar yumuşatma 

Kenar yumuşatma, çizgileri, eğrileri ve yazı tiplerini düzgünleştirmek için kullanılan, GUıDX 'teki isteğe bağlı bir özelliktir. Kenar yumuşatma yalnızca 16 BPP veya daha yüksek renk derinliğine sahip bir ekran sürücüsüyle çalışırken desteklenir.

Etkin fırçayla **GX_BRUSH_ALIAS** flaş ayarlanarak, daha fazla diğer çizgi çizimi etkinleştirilir. Bu, doğrudan çizilen çizgiler ve bir çokgen ya da dairenin kenarlığı olarak çizilen çizgiler için geçerlidir.

Kenar yumuşatma uygulanmış metin çizimi, Gux Studio uygulaması tarafından üretilen, daha fazla ad olan bir yazı tipi kullanılarak etkinleştirilir. Yazı tipini oluştururken bir yazı tipinin Antias veya binary olarak oluşturulup oluşturulmayacağını belirtirsiniz.
GUX 'teki kenar yumuşatma uygulanmış yazı tipleri her bir piksel için 16 düzeyde saydamlık kullanır.

### <a name="clipping"></a>Kırpma 

Kırpma, Gux görüntüleme bileşeni tarafından dahili olarak ve pencere ve pencere öğesi katmanlarında Gux pencere öğeleri tarafından tutulan üst-alt mimarisine göre desteklenir. Herhangi bir pencere veya pencere öğesinin, söz konusu pencere öğesinin alanının dışında çizim yapmasına izin verilmez ve bir pencere öğesinin, o pencere öğesinin üst alanının dışında hiçbir zaman çizilmesine izin verilmez.

Bu Ayrıca, pencere öğelerinin, büyük olasılıkla bellek bozulmasına veya bir sistem hatasına yol açabilecek tuval belleği dışına yerleşen piksel koordinatları çizmesini önler. Pencere öğelerinin, pencere öğesinin alanının alanı, pencere öğesinin üst alanı veya tuval uzantısı dışında çizilmesine izin verilmez.

Ayrıca, pencere öğeleri yalnızca daha önce kirli olarak işaretlenmiş alanlara çizim yapabilir. Bu, örneğin, pencerenin yalnızca bir köşesi gösterildiğinde tüm pencerenin çizilmesini önler. Yalnızca pencerenin yenilenmesi gereken kısmı kirli olarak işaretlenir ve bu nedenle pencere çizim işlevi yalnızca kirli alanındaki pikselleri gerçekten yeniler.

GUX görüntü bileşeni, sürücü düzeyi çizim işlevlerini çağırmadan önce bu kırpma algoritmalarını zorlar.

### <a name="views"></a>Görünümler 

GUX her bir kök pencere için bir görünüm kümesi ve kök penceresinin her bir alt penceresi için her zaman bir görünüm kümesi tutar. Görünümler, pencere konumu ve Z düzeni olarak değişen bir dinamik, çalışma zamanı belirlenmiş kırpma alanıdır.
GUIX, arka plandaki pencere veya pencere öğesinin ön planda bir pencere veya pencere öğesinin üzerine çizilmesini engellemek için görünümleri kullanır. Görünümler, Z sırası disiplini uygular. Ayrıca, görünümler, arka plandaki bir pencerenin, çizmeyen tuvalin herhangi bir alanına çizilmesine engel olan verimlilik açısından önemlidir. Bir pencere başka bir pencereyle tamamen ele alınsa, kapsanan pencerenin, bu işlemi gerçekleştirmeye çalışıyor olsa bile, her seferinde tuvale çizilmesine izin verilmez.

### <a name="display-driver-interface"></a>Sürücü arabirimini görüntüle 

GUX görüntüleme sürücüleri, temeldeki fiziksel ekranla tüm etkileşimlerden sorumludur. Görüntüleme sürücülerinde üç temel işlev vardır: başlatma, çizim ve çerçeve arabelleği görüntüleme.
Başlatma, fiziksel görüntü donanımının hazırlanmasından, fiziksel görüntü donanımının özelliklerinin bilgilendirilmesine ve belirli çizim işlevlerinin kullanılması gereken Gux 'e bildirmeden sorumludur. Ana görüntü sürücüsü başlatması Gux ***gx_display_create*** işlevinden çağrılır. Ayrıca, GUıDX iş parçacığı ayrıca iş parçacığı bağlamından ikincil bir görüntü sürücüsü başlatma işlemi çağırır. Bu ikincil görüntü sürücüsü yalnızca, başlatma işlemi sırasında sürücü RTOS Hizmetleri gerektiriyorsa (örneğin, cihaz kesintileri veya başlatma işlemindeki adımlar arasında gecikme için istekler ***tx_thread_sleep*** ) gereklidir.

Başlatma tamamlandıktan sonra, görüntü sürücüsü fiziksel görüntü donanımında yapılabilen herhangi bir doğrudan çizimden sorumludur.
Son olarak, görüntü sürücüsü çerçeve arabelleğinin görüntülenmesini sağlamaktan sorumludur.

## <a name="guix-widget-component"></a>GUX pencere öğesi bileşeni

Bir Gux pencere öğesi görünür bir grafik öğesidir. Süreölçerler ve Math yardımcı program işlevleri gibi görünür olmayan Gux bileşenleri vardır.
Ancak, tüm görünür bileşenler temel Gux pencere öğesi bileşeninden türetilir. Bir Gux pencere öğesi, GUıDX görüntüleme bloğunun birincil yapı taşıdır; diğer tüm grafik öğeleri temel pencere öğesi işlevlerinden türetilir.

GUX pencere öğeleri, devralmanın tam desteğiyle birlikte nesne yönelimli bir şekilde uygulanır. Bu, mümkün olan en küçük bellek ve işleme gereksinimlerine neden olan ANSI C kullanılarak gerçekleştirilir. **GX_BUTTON** gibi belirli bir pencere öğesinin konuşduğumuz, temel **GX_WIDGET** gibi başka bir pencere *öğesinden türetilmekte* olduğu anlamı olan **GX_BUTTON** denetim yapısının, **GX_BUTTON** özgü bazı ek değişkenlerle birlikte **GX_WIDGET** tüm üye değişkenlerini ve işlev işaretçilerini içerdikleridir. GUX, daha karmaşık Pencere öğelerinin her zaman daha basit bir pencere öğesine dayanmasını sağlamak üzere Pencere öğelerinin katmanlarını bu biçimde oluşturur. Bu hiyerarşik model, pencere öğesi parametrelerini değiştirmek için kullanılan API 'Leri öğrenmenizi kolaylaştırır. Bir düğmenin rengini değiştirmek istiyorsanız, bir pencere öğesinin rengini değiştirmek için kullandığınız API 'yi kullanırsınız, yani ***gx_widget_fill_color_set***.

Görünür pencere öğelerinin organizasyonu, alt pencere öğelerini üst öğeleri ile bağlayan ağaç yapılandırılmış listeler kullanılarak üst-alt öğe olarak korunur. Alt öğeler, çizdikleri görünümler ve çizdikleri tuvaller gibi üst öğelerinden Özellikler devralır.
Alt pencere öğeleri kendi alt pencere öğeleri içerebilir ve üst öğeden çeşitli özellikleri devralabilir. Herhangi bir pencere öğesinin özellikleri, çeşitli GUıDX API çağrıları aracılığıyla açıkça yeniden tanımlanabilir.

### <a name="widget-creation"></a>Pencere öğesi oluşturma 

Pencere parçacıklarının yürütülmesi sırasında veya herhangi bir zamanda, bir pencere öğesi nesnesi oluşturulabilir. Bir uygulama tarafından oluşturulabilen pencere öğesi nesnelerinin sayısında bir sınır yoktur. Ayrıca, hedef donanımınızın bellek sınırları içinde herhangi bir pencere öğesinin sahip olabileceği alt öğe sayısı için bir sınır yoktur.

Her pencere öğesi türü, ***gx_button_create** _ veya _ *_gx_prompt_create_* * gibi kendi oluşturma işlevine sahiptir. Bu işlevlerin ilk üç parametresi her zaman aynıdır, yani pencere öğesi denetim yapısına yönelik bir işaretçi, pencere öğesi adına bir dize işaretçisi ve pencere öğesinin üst öğesi için bir işaretçi. Her oluşturma işlevi, söz konusu pencere öğesi türünün gereksinimlerine bağlı olarak herhangi bir sayıda ek parametreye sahip olabilir.

### <a name="widget-control-block"></a>Pencere öğesi denetim bloğu 

Her pencere öğesi nesnesinin özellikleri, denetim bloğunda **GX_WIDGET** bulunur ve **_gx_api. h_** içinde tanımlanır. Pencere öğesi nesnesi için gereken bellek, uygulama tarafından sağlanır ve bellekte herhangi bir yerde bulunabilir. Ancak, her bir işlevin kapsamı dışında tanımlayarak pencere öğesi nesne denetimi 'nin genel yapıyı engellemesini sağlamak en yaygın olarak kullanılır. GUIX Studio kullanıyorsanız, pencere öğesi denetim bloklarınız, Studio tarafından oluşturulan belirtimlerinizin içinde statik olarak ayrılabilir veya uygulamanız tarafından dinamik olarak tahsis edilebilir.

### <a name="dynamic-widget-control-block-allocation-and-de-allocation"></a>Dinamik pencere öğesi denetim bloğu ayırma ve ayırmayı kaldırma 

Dinamik denetim bloğu ayırması kullanıyorsanız, GUIX 'in pencere öğesi Denetim bloklarında gereken belleği ayırmak ve serbest bırakmak için kullanacağı iki işlev tanımlamanız gerekir. Bellek yönetimi işlevleriniz, ***gx_system_memory_allocator_set*** API işlevi aracılığıyla Gux sistem bileşenine geçirilir. Bu işlev, GUıDX 'e iki işlev işaretçisi geçirmenize olanak sağlar: ilki bir bellek ayırma işlevine yönelik bir işaretçidir ve ikincisi ise bellek boş işlevine yönelik bir işaretçidir. Çoğu zaman, bu işlevleri ThreadX Byte havuzlarını kullanarak uygulayacaksınız, ancak Gux tasarımı, istediğiniz şekilde dinamik bellek yönetimi uygulamanıza olanak tanır.

Dinamik pencere öğesi ayırma, Studio pencere öğesi özellikleri alanında "dinamik olarak ayrılmış" seçeneğini belirlediğinizde, genellikle Studio tarafından oluşturulan uygulama belirtimleri dosyası içinde kullanılır. Ancak, uygulamanızda dinamik denetim bloğu ayırmayı de kullanabilirsiniz. Uygulamanızda dinamik denetim bloğu ayırmayı kullanırsanız, pencere öğesi denetim bloğunu ayırmak için ***gx_widget_allocate** _ API işlevini çağırmanız gerekir. Sonra, pencere öğesini oluşturduğunuzda, _ *GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED** stil bayrağını (diğer tüm gerekli stil bayraklarıyla birlikte) pencere öğesi oluşturma işlevine iletmeniz gerekir. Bu bayrak pencere öğesi durum alanında dinamik olarak ayrıldığı pencere öğesini işaretlemek için kullanılır. Pencere öğesi daha sonra **_gx_widget_delete_** kullanılarak siliniyorsa, guıdx bu durum alanını denetler ve bellek sızıntıları olmadığından bellek ayırıcı işlevinizi otomatik olarak çağırır.

> [!IMPORTANT]
> Dinamik olarak ayrılan denetim bloğu kullanılarak oluşturulan bir pencere öğesinin bellek kaybını engellemek için **GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED** stili bayrağıyla oluşturulması gerekir.

### <a name="types"></a>Türler

GUIX, yerleşik Pencere öğelerinin zengin ve tamamen işlevsel bir kümesini sağlar. Daha önce belirtildiği gibi, tüm özelleşmiş pencere öğeleri temel pencere öğesi öğesinden türetilir. Aşağıda, GUıDX 'teki yerleşik Pencere öğelerinin listesi verilmiştir:

**GX_TYPE_WIDGET**

**GX_TYPE_BUTTON**

**GX_TYPE_TEXT_BUTTON**

**GX_TYPE_MULTI_LINE_TEXT_BUTTON**

**GX_TYPE_RADIO_BUTTON**

**GX_TYPE_CHECKBOX**

**GX_TYPE_PIXELMAP_BUTTON**

**GX_TYPE_ICON_BUTTON**

**GX_TYPE_ICON**

**GX_TYPE_SPRITE**

**GX_TYPE_SLIDER**

**GX_TYPE_PIXELMAP_SLIDER**

**GX_TYPE_VERTICAL_SCROLL**

**GX_TYPE_HORIZONTAL_SCROLL**

**GX_TYPE_PROGRESS_BAR**

**GX_TYPE_PROMPT**

**GX_TYPE_NUMERIC_PROMPT**

**GX_TYPE_PIXELMAP_PROMPT**

**GX_TYPE_NUMERIC_PIXELMAP_PROMPT**

**GX_TYPE_SINGLE_LINE_TEXT_INPUT**

**GX_TYPE_MULTI_LINE_TEXT_VIEW**

**GX_TYPE_MULTI_LINE_TEXT_INPUT**

**GX_TYPE_WINDOW**

**GX_TYPE_ROOT_WINDOW**

**GX_TYPE_VERTICAL_LIST**

**GX_TYPE_HORIZONTAL_LIST**

**GX_TYPE_POPUP_LIST**

**GX_TYPE_DROP_LIST**

**GX_TYPE_LINE_CHART**

**GX_TYPE_DIALOG**

**GX_TYPE_KEYBOARD**

**GX_TYPE_SCROLL_WHEEL**

**GX_TYPE_TEXT_SCROLL_WHEEL**

**GX_TYPE_STRING_SCROLL_WHEEL**

**GX_TYPE_NUMERIC_SCROLL_WHEEL**

**GX_TYPE_CIRCULAR_GAUGE**

**GX_TYPE_RADIAL_PROGRESS_BAR**

**GX_TYPE_RADIAL_SLIDER**

**GX_TYPE_MENU_LIST**

**GX_TYPE_MENU**

**GX_TYPE_ACCORDION_MENU**

**GX_TYPE_TREE_VIEW**


### <a name="styles"></a>Stiller

Pencere öğesi stilleri, daha önce listelendiği gibi belirli pencere öğesi türlerinin özelliklerini ve kenarlık özellikleri (yükseltilen, recessed, ince, kalın veya hiç Boarder) gibi işlemlerden oluşur. Pencere öğesi stil bayrakları, herhangi bir pencere öğesinin görünümünü değiştirmek için en basit yöntemi sunar.
İlk pencere öğesi stili her zaman pencere öğesi türüne özgü oluşturma işlevine geçirilen bir parametredir.

### <a name="colors"></a>Renkler 

Pencere öğeleri, sistem renk tablosunda tanımlanan renkleri kullanarak kendilerini çizer.
Renk kimlikleri, tuval arka planı, varsayılan pencere öğesi dolgusu rengi, düğme dolgusu rengi, metin pencere öğesi dolgusu rengi, pencere dolgusu rengi ve diğer birçok varsayılan renk değeri için tanımlanır. Ayrıca, **GX_WINDOW** nesneler, pencere istemcisi doldurulduğundan bir bit eşlem veya duvar kağıdı görüntülemeyi destekler.

Varsayılan renk şemasını değiştirmenin en basit yöntemi, Gux Studio 'Yu kullanmaktır ve gereksinimlerinizi karşılayan bir renk şeması oluşturur veya tanımlar.
Ayrıca, GX_COLOR değerler dizisi oluşturarak ve gx_system_color_table_set API işlevini çağırarak renk düzeninizi el ile tanımlayabilirsiniz.

### <a name="event-notification"></a>Olay bildirimi 

GUX olayları, Kullanıcı girişi ve iç sistem durumu değişikliklerinin pencere öğelerini bilgilendirmek için bir veya daha fazla pencere öğesine yapılan isteklerdir. Örneğin, bir pencere öğesi odağı aldığında, **GX_EVENT_FOCUS_GAINED** pencere öğesine ***gx_system_event_send*** API hizmeti aracılığıyla gönderilir.

Olaylar Gux olay sırasından geçirilir ve her olay **GX_EVENT** veri yapısının bir örneğidir. **GX_EVENT** veri yapısı ***gx_api. h*** içinde tanımlanmıştır, ancak yapının en önemli alanları **gx_event_type**, **gx_event_sender**, **gx_event_target** ve **gx_event_payload**.

**Gx_event_type** alanı, belirli olay sınıfını tanımlamak için kullanılır. Olay türü, örneğin **GX_EVENT_PEN_DOWN** bir olay veya **GX_EVENT_TIMER** bir olay olduğunu gösterir. **Gx_event_payload** çeşitli veri alanlarının bir birleşimidir ve hepsi her olay türü için geçerli değildir.
Diğer olay verileri alanlarını incelemeden önce olay türü alanını kullanın.

**Gx_event_sender** alanı, olay bir alt pencere öğesi bildirimidir olayı oluşturan pencere öğesinin kimliğini içerir.

**Gx_event_target** alanı, Kullanıcı tanımlı olayları belirli bir pencere veya pencere öğesine yönlendirmek için kullanılabilir. Belirli bir pencereye bir olay göndermek istiyorsanız, pencereye benzersiz bir kimlik değeri (pozitif olarak tanımlanabilmesi için) vermeniz ve olay oluşturulurken **gx_event_target** alanına pencere kimliği değeri yerleştirmeniz gerekir. Hedef kimliği bilmiyorsanız veya olayın yalnızca giriş odaklı bir pencere öğesine yönlendirilmesini istiyorsanız, **gx_event_target** alanını 0 olarak ayarladığınızdan emin olun.

Son olarak, **gx_event_payload** alanı çeşitli veri türlerinin bir birleşimidir. **GX_EVENT_PEN_DOWN** ve **GX_EVENT_PEN_UP** olaylar için **gx_event_pointdata** alanı, kalemin konumunu koordine eden x, y pikseli içerir. Zamanlayıcı olayları için **gx_event_timer_id** alanı, süre dolma SÜREÖLÇERININ kimliğini içerir. Diğer yük verisi alanları diğer olay türleri için kullanılır. Önceden tanımlanmış olay türlerinin tam listesi ve yük alanları [ek E-Gux olay açıklamalarında](appendix-e.md)tanımlanmıştır.

Uygulama, sabit **GX_FIRST_APP_EVENT** sonra sayısal olarak başlayacak şekilde kendi özel olaylarını da ekleyebilir. Bu sabitten sonraki tüm olay numaraları, uygulamanın kullanımı için ayrılmıştır. Kuşkusuz, uygulamanın pencere öğesi olay işleyicisinin bu tür uygulama olayları için işlenmesi gerekir.

### <a name="event-processing"></a>Olay Işleme 

Her ve her pencere öğesi için varsayılan pencere öğesi olay işleme işlevi vardır; ***gx_<pencere öğesi türü>_event_process***. Çoğu durumda, uygulamanın herhangi bir söz konusu pencere öğesinin olay işlemesi hakkında endişelenmek zorunda kalmaz. Ancak, uygulamanın özel veya ek olay işleme gerektirdiği durumlarda, uygulama varsayılan işleme işlevini Gux API ***gx_widget_event_process_set*** aracılığıyla kendi kendine geçersiz kılabilir. Bu işlev, API 'de belirtilen olay işlevi işleme işlevi ile varsayılan olay işleme işlevini geçersiz kılar.

> [!IMPORTANT]
> Uygulama olay işleme işlevleri yalnızca varsayılan ***gx_widget_event_process*** işlemesini doğrudan çağırarak varsayılan işlemenin avantajlarından yararlanabilir (yani, işleme çoğaltma değil).

Olay işleme yalnızca iç Gux sistem iş parçacığı bağlamından çağrılır. Bu şekilde, olay işlemesini işlemek için yığın gereksinimleri yalnızca Gux iş parçacığı için geçerlidir.

### <a name="implementing-custom-event-processing-example"></a>Özel olay Işleme uygulama (örnek) 

GUX sisteminde herhangi bir pencere öğesi veya pencere için kendi olay işleme işlevinizi sağlayabilirsiniz. Kendi özel pencere öğesi türünü oluşturuyorsanız, normalde özel olay işleyicinizi pencere öğesi oluşturma işlevine yüklersiniz. Yalnızca var olan bir pencere öğesinin veya pencerenin işlemini genişletmeniz veya değiştiriyorsanız, pencere öğesi veya pencere oluşturulduktan sonra gx_widget_event_process_set API işlevini çağırabilirsiniz. Alt denetimleriniz tarafından oluşturulan olayları işlemek için, en üst düzey pencereler (ekranlar da denir) için neredeyse her zaman kendi olay işleme sağlarsınız. Ekranın alt denetimleri tarafından oluşturulan işleme olayı, Gux uygulamanıza işlevsellik eklemenin ana yöntemidir.

Örnek olarak, "main_menu" adlı bir üst düzey ekran tanımladığınızı varsayalım.
Bu ekran, GUıDX Studio kullanılarak tanımlanabilir veya bu ekranı uygulama kodunuzda oluşturabilirsiniz. Ekranı Gux Studio içinde tanımlarsanız, bu ekran için Studio özellikleri alanına olay işleyicinizin adını yazmanız yeterlidir ve Studio tarafından oluşturulan belirtim kodu olay işleyicinizi otomatik olarak yükler. Bu durumda, özel olay işleyicisi ***main_menu_event_handler*** çağıracağız ve aşağıdaki gibi kodlanmış olmalıdır:

```C
int main_menu_item; /* example: variable to keep track of selected item */

UINT main_menu_event_handler(GX_WINDOW *main_screen, GX_EVENT *event_ptr)
{
    UINT status = GX_SUCCESS;

    switch(event_ptr->gx_event_type)
    {
    /* this is an example for catching events from a child button */
    case GX_SIGNAL(IDB_CHILD_BUTTON, GX_EVENT_CLICKED):
        /* insert your button handler code here */
        break;

    case GX_EVENT_SHOW:
        /* add functionality to the show event handler */
        /* first, do default processing */
        status = gx_window_event_process(main_screen, event_ptr); /* note 1 */

        /* now add my own processing */
        main_menu_item = 0;
        break;

    default:
        /* pass all other events to base processing function */
        status = gx_window_event_process(main_screen, event_ptr); /* note 1 */
        break;
    }
    return status;
}
```

Yukarıdaki örnekte, **GX_EVENT_SHOW** gibi sistem olayları (bir durum değişikliğinin bir pencere öğesine bildirmek için dahili olarak oluşturulan olaylar) hakkında fark edilmesi önemlidir. uygulamanın, normal işlemenin meydana geldiğinden emin olmak için bu olayları temel pencere öğesi olay işleme işlevine iletmesinin gerekir. Uygulama daha sonra istediğiniz gibi ek mantık ekleyebilir. Uygulama tarafından işlenmemiş olan tüm olaylar (yukarıdaki varsayılan durum) Ayrıca temel olay işleme işlevine geçirilmelidir. Bu örnek **GX_WINDOW** tabanlı en üst düzey bir ekran olduğundan, varsayılan olay işleme işlevi gx_window_event_process.

### <a name="drawing-function"></a>Çizim Işlevi 

Tüm pencere öğesi çizimi olay işlemesinden ayrı olarak gerçekleştirilir. Bu daha verimlidir çünkü çizim genellikle CPU döngüleri bakımından pahalıdır. Ertelenmiş bir çizim algoritması uygulayarak, tüm bekleyen olaylar ve ilgili ekran değişiklikleri, herhangi bir çizim yapılmadan önce tamamlanabilir ve bu nedenle, boşa harcanan bir çizim yapılamaz. Olay işlemeye benzer şekilde, ***gx_<pencere öğesi türü>_draw*** adında, her pencere öğesi için varsayılan bir pencere öğesi çizim işlevi vardır; burada XXX pencere öğesi türüdür. Çoğu durumda, uygulamanın herhangi bir söz konusu pencere öğesinin çizim işleviyle uğraşmak zorunda kalmaz. Ancak, uygulamanın özel veya ek çizim gerektiren durumlarda, uygulama varsayılan çizim işlevini Gux API ***gx_widget_draw_set*** aracılığıyla kendi kendine geçersiz kılabilir. Bu işlev, uygulamanın herhangi bir pencere öğesi için kendi özelleştirilmiş çizim işlevini sağlamasına izin verir. Bu, uygulamanın tüm yeni pencere öğesi türlerini tanımlamasına olanak sağlar.

> [!IMPORTANT]
> Uygulama çizim işlevleri, doğrudan geçersiz kılınan çizim işlevinden çağırarak, varsayılan çizimin avantajlarından yararlanabilir (yani, kodlama yinelememez).

Pencere öğesi çizimi, iç Gux sistem iş parçacığı bağlamından özel olarak çağırılır. Bu şekilde, çizimi gerçekleştirmeye yönelik zamanlama ve yığın gereksinimleri yalnızca Gux iş parçacığı için geçerlidir.

### <a name="implementing-custom-drawing-example"></a>Özel çizim uygulama (örnek) 

Herhangi bir pencere öğesinin çizim işlevine, GX_WIDGET denetim bloğunun üyesi olan bir dolaylı işlev işaretçisi aracılığıyla başvurulur. Pencere öğesini tanımlamak için Gux Studio kullanırsanız, yalnızca işlevinizin adını pencere öğesi özelliklerinin "çizim Işlevi" parametresine yazarak kendi işlev işaretçinizi yükleyebilirsiniz ve Studio, pencere öğesi oluşturulduğunda işlev işaretçinizi sizin için yükler. Uygulama kodunuzda pencere öğesini oluşturursanız, pencere öğesi oluşturulduktan sonra özel çizim işlevinizi yüklemek için ***gx_widget_draw_set*** API işlevini kullanmanız gerekir.

Bu örnekte, bir düğmenin görünümünü özelleştirmek istediğinizi varsayalım. Düğme, bir **GX_TEXT_BUTTON** benzer şekilde görünecektir, ancak düğmeye basıldığında düğmenin sağ orta kısmına küçük bir yeşil "LED_ON" bit eşlem ekler ve düğmeye basıldığında küçük "LED_OFF" bit eşlemi ekleyeceğiz. Aşağıdaki çizimler gibi görünen bir düğme oluşturmak istiyoruz.

![Açık için yeşil düğmenin ekran görüntüsü.](./media/guix/image4.jpg) özel düğme "açık"

![Kapalı kırmızı düğmesinin ekran görüntüsü.](./media/guix/image5.jpg) özel düğme "kapalı"

Bu durumda, aşağıdakine benzer bir düğme çizim işlevi yazacağız.

```C
UINT my_button_draw(GX_TEXT_BUTTON *button)
{
    GX_PIXELMAP *map;
    ULONG button_style;
    INT xpos;
    INT ypos;

    /* first, do the normal text button drawing */
    gx_text_button_draw(button);

    /* now add our extra pixelmap */

    gx_widget_style_get(button, &button_style);

    if (button_style & GX_STYLE_BUTTON_PUSHED)
    {
        /* use the ON pixelmap */
        gx_context_pixelmap_get(GX_PIXELMAP_ID_LED_ON, &map);
    }
    else
    {
        /* use the OFF pixelmap */
        gx_context_pixelmap_get(GX_PIXELMAP_ID_LED_OFF, &map);
    }
    if (map)
    {
        /* draw it 20 pixels in from right edge */
        xpos = button->gx_widget_size.gx_rectangle_right;
        xpos -= map->gx_pixelmap_width + 20;

        /* and draw 10 pixels from the top edge */
        ypos = button->gx_widget_size.gx_rectangle_top + 10;

        /* draw the extra pixelmap on top of the button */
        gx_canvas_pixelmap_draw(xpos, ypos, map);
    }
}
```

## <a name="guix-drawing-context-component"></a>GUX çizim bağlamı bileşeni 

Çizim bağlamı, çalışma zamanında dinamik olarak oluşturulur ve Gux, her tuval yenileme işlemini gerçekleştirir. Çizim bağlamı, geçerli çizim işlemlerini gerçekleştirmek için kullanılan tuvali, ekran sürücüsünü ve fırçayı birlikte kullanır.

Çizim bağlamı **GX_DRAW_CONTEXT** yapısı tarafından tanımlanır.
Bu yapı, geçerli çizim işleminin kırpılmasını ve görünümünü tanımlayan değişkenleri içerir, geçerli tuvali tanımlar ve kullanımda olan geçerli ekran sürücüsünü tanımlar. **GX_DRAW_CONTEXT** yapısı, çizim için kullanılan fırçayı de barındırır. Çiz bağlam fırçası, doğrudan özel çizim işlevleriniz içinde çalışeceğiniz üyesidir. Fırça yapısı aşağıdaki kodda gösterildiği gibi tanımlanmıştır.

```C
typedef struct GX_BRUSH_STRUCT
{
    GX_PIXELMAP *gx_brush_pixelmap;
    GX_FONT     *gx_brush_font;
    ULONG        gx_brush_line_pattern;
    ULONG        gx_brush_pattern_mask;
    GX_COLOR     gx_brush_fill_color;  
    GX_COLOR     gx_brush_line_color;  
    UINT         gx_brush_style;
    GX_VALUE     gx_brush_width;
    UCHAR        gx_brush_alpha;  
} GX_BRUSH;
```

**Gx_brush_pixelmap** alanı, dikdörtgen ve çokgen dolguları için kullanılacak bir pixelmap tanımlar. **Gx_brush_style** , **GX_BRUSH_PIXELMAP** stilini içermiyorsa, bu üye kullanılmaz.

**Gx_brush_font** üyesi metin çiziminde kullanılan yazı tipini tanımlar.
**Gx_brush_line_pattern** üyesi, kesikli çizgiler için kullanılan kalıbı tanımlar.
**Gx_brush_style** üyesi, fırça özniteliklerini tamamen tanımlamak için bır arada veya ile birlikte olabilecek bir stil bayrakları kümesidir. Kullanılabilir fırça stili bayrakları aşağıdakileri içerir.

**GX_BRUSH_OUTLINE**  
**GX_BRUSH_SOLID_FILL**  
**GX_BRUSH_PIXELMAP_FILL**  
**GX_BRUSH_ALIAS**  
**GX_BRUSH_UNDERLINE**  
**GX_BRUSH_ROUND**

**Gx_brush_width** üyesi çizgi çizimi için satırı veya özetlenen şekil çiziminin ana hat genişliğini tanımlar.

**Gx_brush_line_color** üyesi, çizgi çiziminin ve metin çiziminin ön plan rengini tanımlar.

**Gx_brush_fill_color** üyesi, şekil doldurma için kullanılan düz doldurma rengini tanımlar. GUX bağlam bileşeni, etkin bağlam içindeki geçerli fırçayı değiştirmek çok kolay hale getirmek için tasarlanan bir API kümesi sağlar. Bu API 'Ler **gx_context_brush_define**, **gx_context_line_color_set**, **gx_context_fill_color_set**, **gx_context_font_set** ve diğer birçok tane içerir.

Üst nesnenin çizim bağlamı nesneler alt öğesi tarafından devralınır. Aslında, ana çizim bağlamının bir kopyası, çizim işlevleri çağrıldığında alt nesneler tarafından devralınır. Alt öğe, üst çizimi etkilemeden bağlamı değiştirebilir, ancak isterseniz fırça rengi ve stili gibi üst öğeden bilgileri de miras alabilir.

## <a name="guix-window-component"></a>GUX pencere bileşeni 

Pencere bileşeni, Gux 'teki tüm pencere işlemeden sorumludur. Bir Gux penceresi, bir veya daha fazla alt pencere öğesi içerebilen ayrı bir görüntüleme alanıdır. GUX 'te, pencere aslında yalnızca temel pencere öğesi nesnesinin özel bir biçimidir.

GUX pencereleri, devralmanın tam desteğiyle birlikte nesne yönelimli bir şekilde uygulanır. Bu, mümkün olan en küçük bellek ve işleme gereksinimlerine neden olan ANSI C kullanılarak gerçekleştirilir.

GUX Windows, yatay ve dikey kaydırma desteği ekleyerek Gux pencere öğesinin işlevselliğini esas olarak genişletir. GUX pencere nesneleri otomatik olarak, kaydırma çubukları oluşturup görüntüleyebilir ve kaydırma çubuğu girişine yanıt verebilir. Taşınabilir pencereler Ayrıca pencerenin kalem girişi olaylarına göre taşınmasına veya sürüklenip bırakılmasına izin vermek için yerleşik olay işleme de sahiptir.
Son olarak, Gux penceresi, pencereyi pencerenin Z düzeninin önüne taşıyarak giriş odağını almaya yanıt verir.

GUX penceresi, Pencere kenarlıkları ve kaydırma çubukları gibi istemci olmayan nesneler kullanılabilir alandan kaldırıldığında pencerenin iç bölümü olan *istemci alanı* kavramını korur. İstemci alanı alt öğeleri pencere istemci alanına kırpılıp, kaydırma çubukları gibi istemci olmayan alt öğelerin, istemci alanının dışında çizim yapmasına izin verilir, ancak hala pencerenin dış boyutlarına kırpılmasını sağlar.

Pencereler bir üst-alt biçimde tutulur ve bu, alt öğelerin özellikleri üst öğelerinden devraldığı yerdir. Alt Windows 'un kendi alt pencereleri olabilir, bu da üst öğeden çeşitli özellikleri devralabilir. Herhangi bir pencerenin özellikleri, çeşitli GUıDX API çağrıları aracılığıyla açıkça yeniden tanımlanabilir.

### <a name="window-creation"></a>Pencere oluşturma 

Başlatma sırasında veya uygulama iş parçacıklarının yürütülmesi sırasında her zaman bir pencere nesnesi oluşturulabilir. Bir uygulama tarafından oluşturulabilen pencere nesnelerinin sayısında bir sınır yoktur. Ayrıca herhangi bir pencerenin sahip olabileceği alt öğe sayısı için bir sınır yoktur.

### <a name="window-control-block"></a>Pencere denetim bloğu 

Her pencere nesnesinin özellikleri, denetim bloğunda **GX_WINDOW** bulunur ve **_gx_api. h_** içinde tanımlanır. Bir pencere nesnesi için gereken bellek, uygulama tarafından sağlanır ve belleğin herhangi bir yerinden bulunabilir. Ancak, herhangi bir işlevin kapsamı dışında tanımlayarak pencere nesne denetimi 'nin genel yapıyı engellemesini sağlamak en yaygın olarak kullanılır.

### <a name="root-window"></a>Kök pencere 

GUX, her tuval için kök pencere olarak adlandırılan bir değer gerektirir. Kök pencere Kenarlıksız ve eklendiği tuvalle aynı boyutlara sahiptir. Birincil olarak ilk düzey pencere öğeleri ve pencereler için bir kapsayıcı olarak kullanılır. Kök pencere, genellikle ekran ve tuval oluşturulduktan sonra ***GX_WINDOW_ROOT_CREATE*** API işlevi aracılığıyla uygulama tarafından oluşturulur. Studio tarafından oluşturulan işlevi gx_studio_display_configure kullanırsanız, kök pencerenin adresi bu işleve son parametre olarak geçirilen konumda döndürülebilir.

Kök pencere, varsayılan olarak taşınamayacak ve en basit durumda kök pencere tuvalin boyutudur. Etkin kök pencere, ekran arka planını çizer, bu nedenle ekran arka plan rengini değiştirmek veya arka plan duvar kağıdını göstermek için kök pencereye bir renk veya duvar kağıdı atamanız gerekir.

Bir kök pencere taşınabilir ise, alt pencere yaptığı, ancak tuvalin kendisini hareket ettirerek tuval üzerinde konumunu değiştirerek bu, hareket etmez.
Bu özellik, Gux kök penceresinin, donanım fark kayıtları olan birden çok çerçeve arabelleğini destekleyen donanımdan yararlanmasını sağlar.

### <a name="background"></a>Arka Plan 

Pencere arka planları düz renkler veya bit eşlem görüntüleridir. Sistem düzeyinde, ilk Windows kümesi için varsayılan değer sağlayan bir pencere arka planı vardır. Kuşkusuz, tüm pencere arka planı Gux API 'SI aracılığıyla değiştirilebilir.

Pencerenin düz renk arka planını değiştirmek için ***gx_widget_fill_color_set*** API 'sini kullanın. Bir pencereye arka plan duvar kağıdı atamak için ***gx_window_wallpaper_set*** API 'sini kullanın.

### <a name="scrolling"></a>Kaydırma 

Window alt öğelerini göstermek için gereken alan, pencerenin geçerli boyutunu (yatay ve/veya dikey olarak aşarsa), GUıDX standart pencere kaydırmayı destekler. Kaydırmayı etkinleştirmek için uygulama, istenen kaydırma çubuklarını oluşturmalı ve pencereye iliştirmelidir.

GUX pencere bileşeni, pencere istemci alanının boyutunu ve tüm alt pencere öğelerinin kapsamını temel alan varsayılan bir kayan uygulama sağlar. Uygulamalar, belirli bir pencerenin ***gx_window_scroll_info_get*** işlevini geçersiz kılarak kendi kaydırma uygulaması ve yorumlamasını de sağlayabilir.

### <a name="event-notification"></a>Olay bildirimi 

Varsayılan pencere olay işleme işlevi, birincil olarak kaydırma ve boyutlandırma olaylarının işlendiği GX_WIDGET olay işlemeden farklıdır. GX_WINDOW, kaydırma ve boyutlandırma olayları için defalt işleyicileri sağladı.

Uygulama, sabit **GX_FIRST_APP_EVENT** sonra sayısal olarak başlayacak şekilde kendi özel olaylarını da ekleyebilir. Bu sabitten sonraki tüm olay numaraları, uygulamanın kullanımı için ayrılmıştır. Kuşkusuz, uygulamanın pencere olay işleyicisinin bu tür uygulama olayları için işleme sahip olması gerekir.

### <a name="event-processing"></a>Olay Işleme 

Diğer tüm pencere öğesi türlerinde olduğu gibi, ***gx_window_event_process*** adlı her pencere için varsayılan bir pencere olay işleme işlevi vardır. Bu olay işleme işlevini genellikle oluşturduğunuz Windows 'da kendi olay işleyiciniz ile geçersiz kılacaksınız. Bu, olaylara yanıt vermek ve pencere alt denetimleri tarafından oluşturulan olaylara göre işlem yapmak için kullanılır.

Bu olay işleyicisini geçersiz kıldıysanız, varsayılan olay işlemenin olay işleyicisine eklediğiniz herhangi bir eyleme ek olarak oluşmasına izin vermek için, bu olay işleyicisini geçersiz kıldıysanız, GUıDX sistem olayları için temel ***gx_window_event_process*** işlevinin çağrılmasını unutmamak önemlidir. Örneğin, **GX_EVENT_SHOW** olayı için özel bir işleyici sağlar ve bu olayı ***gx_window_event_process*** olarak iletmezseniz, pencereniz hiçbir şekilde görünmez olmaz.
Bir pencere için özel bir olay işleyicisi sağlamak üzere, olay işleyicinizin adresini tanımlamak için ***gx_widget_event_process_set*** işlevini kullanın. Bu işlev, API 'de belirtilen olay işlevi işleme işlevi ile varsayılan olay işleme işlevini geçersiz kılar.

> [!IMPORTANT]
> Uygulama olay işleme işlevleri yalnızca varsayılan ***gx_window_event_process*** doğrudan çağırarak varsayılan işlemenin avantajlarından yararlanabilir (yani, işleme uygulanmaz).

Olay işleme yalnızca iç Gux sistem iş parçacığı bağlamından çağrılır. Bu şekilde, olay işlemesini işlemek için yığın gereksinimleri yalnızca Gux iş parçacığı için geçerlidir.

## <a name="guix-image-reader-component"></a>GUX görüntü okuyucu bileşeni 

Görüntü okuyucu bileşeni, sıkıştırılmış ham sıkıştırılmış görüntüleri GUıDX pixelmap biçimine kadar açmak için yardımcı programları ve API işlevlerini sağlar. JPEG ve PNG biçimli Ham görüntü verileri, gelecek sürümler için ayrılmış ek biçimler ile desteklenir.

GUX uygulamalarının büyük çoğunluğu için Gux görüntü okuyucu bileşeni gerekli değildir. Çoğu uygulama, JPEG ve PNG formatı grafik varlıklarını Gux uyumlu **GX_PIXELMAP** kaynaklarına dönüştürmek için Gux Studio uygulamasını kullanır. GUX görüntü okuyucu bileşeni, ham grafik varlıkları yalnızca çalışma zamanında bilindiğinde veya sistem depolama kısıtlamaları kaynakların **GX_PIXELMAP** biçimde depolanmasını engelliyorsa kullanılır. JPEG ve PNG biçimli resim verileri genellikle **GX_PIXELMAP** biçiminden daha küçüktür. ancak, bu görüntü türlerini dinamik olarak açma ve renk alanı dönüştürme işlemlerini gerçekleştirmeyle ilişkili önemli çalışma zamanı ek yükü vardır.

Ham biçim JPEG veya PNG görüntüleri gx_canvas_pixelmap_draw API işlevine geçirilirse, GUıDX dinamik olarak JPEG veya PNG verilerini açar ve çizer. Bu, çalışma zamanı çizim hızında önemli bir olumsuz etkiye sahip olacağını ve ham biçim görüntü verilerinin gx_canvas_pixelmap_draw işlevine geçirilmesini, donanım yardımlı JPEG veya PNG 'yi açmayı destekleyen bir donanım hedefi kullanmadığınız durumlar önerilmez.

> [!IMPORTANT]
> Ham JPEG veya PNG biçimli görüntülerin gx_canvas_pixelmap_draw API 'sine geçirilmesi, çoğu hedef donanım için önemli çalışma zamanı ek yüküne neden olur.

Alternatif olarak, ham JPEG ve PNG verileri, görüntü okuyucu bileşeni kullanılarak çalışma zamanında GX_PIXELMAP biçime dönüştürülebilir.
Bu şekilde üretilen pixelmaps, tıpkı Studio tarafından üretilen ve kaynak dosyanızda bulunan pixelmaps gibi kullanılabilir ve çizilir. Bu, uygulamanızın görüntü her çizildiğinde bu işlemleri gerçekleştirmek yerine bir kez (genellikle program başlangıcında) görüntü açma, titreme ve renk alanı dönüştürme işlemini gerçekleştirmesini sağlar.

Görüntü okuyucu bileşeni işlevleri şunları içerir:

***gx_image_reader_create***  
***gx_image_reader_palette_set***  
***gx_image_reader_start***

## <a name="guix-animation-component"></a>GUX animasyon bileşeni 

GUX animasyon bileşeni, ekran ve pencere öğesi geçiş otomatikleştirmelerini otomatikleştirmek için kullanılan bir işlevler ve hizmetler kümesidir. GUX animasyon bileşeni, herhangi bir pencere öğesi türünün soldurma, soldurma ve taşıma ya da slayt türü animasyonlarını destekler.

Zayıflatma türü animasyonları, soldurma Pencere öğelerinin iç alfa değeri ( **GX_BRUSH_ALPHA_SUPPORT** etkinse) veya herhangi bir pencere öğesinin herhangi bir koleksiyonunu ayrı bir bellek tuvaline çizerek, daha sonra arka planla karışarak desteklenebilir. Birden çok donanım grafik katmanını destekleyen donanım hedefleri için, bu tuval karıştırma yaklaşımının kullanılması en iyi şekilde, genellikle çok az çekirdekli CPU bant genişliğine sahip olmak için desteklenir. Birden çok grafik katmanını desteklemeyen donanım hedefleri için, 16 BPP ve daha yüksek renk derinliğinde çalışırken Gux fırçası Alpha değeri kullanılarak karıştırma desteklenir.

Bir animasyonun ayrı bir çizim tuvali kullanması gerekiyorsa, Gux animasyon bileşeni bu amaçla API hizmeti gx_animation_canvas_define sağlar. Diğer animasyon türleri ayrı bir tuval gerektirmez, ancak varsa onu kullanır. Bu, birden çok donanım için temel alınan donanım desteğinin en iyi kullanımını mümkün kılar.

Bir animasyonu denetleyen değişkenler iki denetim bloğu tarafından tanımlanır. İlk olarak, animasyon denetleyicisini tanımlayan **GX_ANIMATION** denetim bloğu. Animasyon denetleyicisi, tanımladığınız animasyon dizisini yürüten itici altyapısıdır. Tek bir animasyon denetleyicisi, birçok farklı animasyon dizisini çalıştırmak için bir kaç kez yeniden kullanılabilir. Birden çok animasyon dizisini eşzamanlı olarak çalıştırmanız gerekirse, birden çok **GX_ANIMATION** animasyon denetleyicisi oluşturabilirsiniz.

GUX sistem bileşeni, ve animasyon gerektiğinde uygulama tarafından istenen ve animasyon sırası tamamlandığında otomatik olarak sistem havuzuna döndürülen **GX_ANIMATION** denetim yapıları için yeniden kullanılabilir bir blok sağlayabilir. Bu, uygulamayı, uygulanabilir her animasyon için statik olarak bir **GX_ANIMATION** yapısını tanımlayarak serbest bırakır. Bu **GX_ANIMATION** yapıları havuzunun boyutu, varsayılan olarak 6 ' ya kadar, varsayılan 6 ' nın varsayılan olarak 6 ' ya kadar eşzamanlı animasyonların, sistem havuzundan ayrılabileceği şekilde **GX_ANIMATION_POOL_SIZE** tanımlanır. Bu sabit, gx_user. h üstbilgi dosyasında daha fazla eşzamanlı animasyon olması gerekir. **GX_ANIMATION_POOL_SIZE** sıfır olarak ayarlandıysa, guıdx sistem bileşeni bir animasyon havuzu veya ilgili hizmetler sağlamaz.

Bir animasyonu tanımlamak için kullanılan ikinci denetim bloğu veya yapısı **GX_ANIMATION_INFO** yapısıdır. Bu yapı, belirli bir animasyon sırasını tanımlamak için kullanılır. Bu bilgi yapısını, gx_animation_start API hizmetini kullanarak bir animasyon sırası başlatmak için animasyon denetleyicinize geçirirsiniz. **GX_ANIMATION_INFO** yapısı aşağıdaki alanları içerir:

```C
typedef struct GX_ANIMATION_INFO_STRUCT
{
    GX_WIDGET *gx_animation_target;
    GX_WIDGET *gx_animation_parent;
    GX_WIDGET *gx_animation_screen_list;
    USHORT gx_animation_style;
    USHORT gx_animation_id;
    USHORT gx_animation_start_delay;
    USHORT gx_animation_frame_interval;
    GX_POINT gx_animation_start_position;
    GX_POINT gx_animation_end_position;
    GX_UBYTE gx_animation_start_alpha;
    GX_UBYTE gx_animation_end_alpha;
    GX_UBYTE gx_animation_steps;
} GX_ANIMATION_INFO;
```

**Gx_animation_target** üyesi, animasyon denetleyicisinin üzerinde işlem yapması için hedef pencere öğesini tanımlar.

**Gx_animation_parent** üyesi, varsa, hedef pencere öğesinin animasyon sırası tamamlandığında eklendiği üst pencere öğesini tanımlar. Gx_animation_parent Ayrıca, bir animasyon tamamlandığında oluşturulan GX_ANIMATION_COMPLETE olayının alıcıdır.

**Gx_animation_screen_list** üyesi, kalem girişi temelli ekran slayt animasyonları için pencere öğesi listesini tanımlar. Widge listesinin GX_NULL işaretçiyle sonlandırılması gerekir ve listedeki her pencere öğesi gx_animation_parent aynı x, y boyutlarına sahip olmalıdır.

**Gx_animation_style** , gerçekleştirilecek animasyon türünü ve ilişkili seçenekleri tanımlayan bir bit dır. Animasyon stili bayrakları aşağıdakileri içerir.

| Animasyon &nbsp; stili &nbsp; bayrağı | Açıklama |
| --- | --- |
| GX_ANIMATION_TRANSLATE | Bir slayt veya belirme türü animasyonu isteyin. |
| GX_ANIMATION_SCREEN_DRAG | Kalem girişi temelli ekran sürükleme animasyonu isteme. |

Aşağıdaki bayraklar **SCREEN_DRAG** türü animasyonlarla birlikte kullanılabilir.

| Ekran &nbsp; sürükleme &nbsp; bayrakları | Açıklama |
| --- | --- |
| GX_ANIMATION_WRAP | Ekran listesi baştan itibaren başa doğru kaydırılır. |
| GX_ANIMATION_HORIZONTAL | Yatay yönde ekran sürüklemeye izin verildi.  |
| GX_ANIMATION_VERTICAL | Dikey yönde ekran sürüklemeye izin verildi. |

Aşağıdaki bayrak, animasyonları çevir ile birlikte kullanılabilir.

| &nbsp;Animasyon &nbsp; bayraklarını çevir | Açıklama |
| --- | --- |
| GX_ANIMATION_DETACH | Animasyon tamamlandığında animasyon hedefini animasyon üst öğesinden ayırın. Hedef, Gux Studio tarafından oluşturulan otomatik olay işleme tarafından dinamik olarak ayrılmışsa ve oluşturulduysa, hedef ayrıldıktan sonra silinir. |
| GX_ANIMATION_TRANSLATE | Animasyon türleri Zamanlayıcı odaklı animasyonlardır. Uygulama, hedef pencere öğesi için başlangıç ve bitiş konumunu ve başlangıç ve bitiş değerini tanımlar ve animasyon Yöneticisi, işlem yapmak için bir zamanlayıcı oluşturur ve bu işlem, animasyonu yürütmeye zorlar.
| GX_ANIMATION_SCREEN_DRAG | Bu animasyon türünün kalem giriş olayları tarafından çalıştırılmaları için **çeviri** animasyonlarından farklıdır. Bu animasyon, Kullanıcı giriş dokunmatik ekranında bir kalem veya ekran kalemi sürüklediği için, hedef pencere öğesini çekerek dokunmatik ekran girişi ile birlikte izler. Bu tür bir animasyon kullanmak için, uygulamanın bu animasyonu etkinleştirmek üzere **_gx_animation_drag_enable_** API 'sini çağırması gerekir. |

**Gx_animation_id** değeri, **GX_ANIMATION_COMPLETE** olayının Event.gx_event_sender alanındaki animasyon üst öğesine geri geçirilir. Bu değer, büyük olasılıkla çok sayıda alt animasyonun ne olduğunu raporlamak için animasyon üst öğesi tarafından kullanılır. Bu değer 0 olabilir ve KIMLIK değeri 0 olan bir animasyon, **ANIMATION_COMPLETE** bir olay oluşturmaz.

**Gx_animation_start_delay** değeri, ***animasyonu gerçekten yürütmeden önce gx_animation_start _ çağrıldıktan sonra gecikme süresi sayısını belirten bir Guix değer sayısıdır. Değer, _ gx_animation_start çağrıldıktan hemen sonra animasyonu başlatmak için 0 olabilir***.

**Gx_animation_frame_interval** alanı, animasyon dizisinin her bir çerçevesi arasında gecikmeye izin vermek için Gux Zamanlayıcı çentiklerinin sayısını (temeldeki işletim sistemi işaret hızının bir katı) tanımlar. En küçük değer 1 ' dir.

**Gx_animation_start_position** , çeviri animasyonları için hedef pencere öğesi için sol üst başlangıç noktasını tanımlar.

**Gx_animation_end_position** , çeviri türü animasyonları için hedef pencere öğesinin üst sol bitiş konumunu tanımlar.

**Gx_animation_start_alpha** alanı, çeviri türü animasyonları için başlangıç tuvali Alfa değerini tanımlar.

**Gx_animation_end_alpha** alanı, çeviri türü animasyonları için bitiş tuvali Alfa değerini tanımlar.

**Gx_animation_steps** alanı, denetleyicinin çeviri animasyonları için kaç adım veya kare yürütmesi gerektiğini tanımlar. Daha fazla sayıda adım daha yumuşak bir slayt ve/veya Soldur görünümü üretir, ancak aynı zamanda daha fazla sistem bant genişliği gerektirir.

Uygulamanızda animasyon efektlerini uygulamak için, önce animasyon denetleyicinizi başlatmak üzere ***gx_animation_create*** çağırmanız gerekir. Animasyonunuz ikincil bir tuval kullanacaksanız, gx_animation_canvas_define çağırarak bu tuvali başlatın. Daha sonra, gerçekleştirilecek belirli animasyon türünü ve diğer animasyon parametrelerini tanımlamak için **GX_ANIMATION_INFO** yapısını başlatmalısınız. Son olarak, Animasyon sırasını tetiklemek için gx_animation_start çağırın.

Animasyon denetleyicisi bir animasyon sırasını tamamladığında, bir **GX_ANIMATION_COMPLETE** olayını üst pencere öğesine gönderir ve bu sırada animasyon tuvalinin istenen Temizleme işleminin bu sırada yapılmasını sağlar.

## <a name="guix-utility-component"></a>GUIX yardımcı program bileşeni 

Yardımcı program bileşeni, Gux 'teki tüm ortak yardımcı program işlevlerinden sorumludur. Bunlar, yararlı yardımcı programlar olan ve uygulamanın herhangi bir yerinden veya iç Gux kodunda çağrılabilen yaygın işlevlerdir. Yardımcı program bileşeni işlevleri şunlardır.

***gx_utility_canvas_to_bmp***

***gx_utility_circle_point_get***

***gx_utility_alphamap_create***

***gx_utility_gradient_create***

***gx_utility_gradient_delete***

***gx_utlity_ltoa***

***gx_utility_math_acos***

***gx_utility_math_asin***

***gx_utility_math_cos***

***gx_utility_math_sin***

***gx_utility_math_sqrt***

***gx_utility_pixelmap_resize***

***gx_utility_pixelmap_rotate***

***gx_utility_pixelmap_simple_rotate***

***gx_utility_rectangle_center***

***gx_utility_rectangle_center_find***

***gx_utility_rectangle_combine***

***gx_utility_rectangle_compare***

***gx_utility_rectangle_define***

***gx_utility_rectangle_overlap_detect***

***gx_utility_rectangle_point_detect***

***gx_utility_rectangle_resize***

***gx_utility_rectangle_shift***

***gx_utility_string_to_alphamap***
