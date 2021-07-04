---
title: Bölüm 3 - GUIX'e İşlevsel Genel Bakış
description: Bu bölümde, yüksek performanslı GUIX kullanıcı arabirimi ürününe işlevsel bir genel bakış yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2a53da048b18d35b6b15a4ad8d4138e1a2acd4e8
ms.sourcegitcommit: 95f4ae0842a486fec8f10d1480203695faa9592d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111875264"
---
# <a name="chapter-3---functional-overview-of-guix"></a>Bölüm 3 - GUIX'e İşlevsel Genel Bakış

Bu bölümde, yüksek performanslı GUIX kullanıcı arabirimi ürününe işlevsel bir genel bakış yer almaktadır. 

## <a name="execution-overview"></a>Yürütmeye Genel Bakış

GUIX, olay odaklı bir programlama modeli uygulama. Bu, GUIX çerçevesinin öncelikli olarak GUIX olay kuyruğuna iletilen olayların alınmasıyla yönlendirildiğini belirtir. Bu olayların işlemesi GUIX sistem başlatma sırasında oluşturulan bir ThreadX iş parçacığı olan GUIX iş parçacığı bağlamında sürer.

GUIX uygulamaları, pencere ve alt pencere öğeleri oluşturmak için GUIX API işlevlerini çağırarak kullanıcı arabirimini tanımlar ve renkleri, stilleri, yazı tiplerini ve her pencere öğesi türünün diğer çeşitli özniteliklerini tanımlamak için kullanılan ek API işlevlerini çağırarak bu pencere öğelerinin görünümünü özeller. Kullanıcı arabirimi ekranlarının görünümünü oluşturmak için GUIX Studio kullanıyorsanız, görüntülerinizi oluşturmak için GUIX API işlevlerini çağırmanın büyük bir işi GUIX Studio uygulaması tarafından sizin için yapılır.

GUIX uygulamaları, GUIX olay kuyruğundan alınan olayları işleerek sistem kullanıcısı ve dış iş mantığıyla etkileşime geçme.
Bu olaylar genellikle GUIX pencere öğeleri tarafından oluşturulur, ancak dış iş parçacıkları tarafından da oluşturulabilir. Tipik bir GUIX düğmesi gönderıldığında, bu düğme düğmenin üst penceresine bir olay gönderir. Uygulama programınız, düğme anında itme olayı için bir işleyici sağlayarak bu düğme anında basıldığında eyleme geçmektedir.

Genellikle giriş sürücüleri gibi şeyler için ek GUIX iş parçacıkları oluşturulur. Tipik bir dokunmatik ekran giriş sürücüsü, ana GUIX iş parçacığının dışında tek başına iş parçacığı olarak yürütülür. Dokunma girişi sürücüsü, GUIX olay kuyruğuna olayları göndererek dokunma bilgilerini GUIX iş parçacığına gönderir.

Animasyonlar gibi birçok kullanıcı arabirimi işlem doğru zamanlama bilgileri gerektirmesi sayesinde GUIX basit ve kullanımı kolay bir zamanlayıcı arabirimi de sunar. Bu zamanlayıcı arabirimi ThreadX zamanlayıcı hizmeti üzerine oluşturulur ve sistem başlangıcında otomatik olarak yapılandırılır.

GUIX yazılımının büyük çoğunluğu herhangi bir donanım bağımlılığına karşı bağımsızdır. Çerçeve, donanıma özgü giriş sürücüleri ve donanıma özgü grafik sürücüleri gerektirir. Bu donanıma özgü sürücülerin nasıl uygulandığının ayrıntıları 5. bölüme ertelenmiştir.

## <a name="initialization"></a>Başlatma 

Başka ***gx_system_initialize*** GUIX hizmeti çağrılmadan önce hizmetin çağrılmaları gerekir. GUIX sistem başlatması, ***ThreadX*** tx_application_define yordamından (başlatma bağlamı) veya uygulama iş parçacıklarından çağrılebilir. ***gx_system_initialize*** GUIX olay kuyruğu oluşturur, GUIX zamanlayıcı tesisini başlatıyor, ana GUIX sistem iş parçacığını oluşturuyor ve uygulamanın yürütülmesi sırasında GUIX tarafından sürdürülen çeşitli veri yapılarını başlatıyor.

Uygulama ***gx_system_initialize*** döndürdikten sonra ekranlar, tuvaller, pencereler, pencere öğeleri oluşturma ve tüm GUIX nesnelerinin özelliklerini özelleştirmeye hazırdır. GUIX nesne oluşturma API'lerinin büyük bir tx_application_define ***iş*** parçacıklarından çağrılabilirsiniz.

## <a name="application-interface-calls"></a>Uygulama Arabirimi Çağrıları 

Uygulama çağrıları büyük ölçüde tx_application_define ***(başlatma bağlamı)*** veya uygulama iş parçacıklarından yapılır. Hangi bağlamdan çağrıll tanımlan olduğunu belirlemek için lütfen Bölüm 4'te açıklanan guiX API'lerinin "İzin Verilenler" bölümüne bakın.

En çok yoğun işleme etkinlikleri, tüm olay işleme ve pencere öğesi/pencere çizimi dahil olmak üzere iç GUIX iş parçacığına ertelenmiştir.

GUIX API işlevleri herhangi bir iş parçacığından herhangi bir zamanda çağrılabilirsiniz.
Ancak, zaman açısından kritik iş mantığınızı kullanıcı arabirimi mantığından ayırmak için genellikle daha iyi bir mimari olarak kabul edilir. Kullanıcı arabirimi çizim işlemleri görüntü boyutunuz ve CPU performansınıza bağlı olarak bazen uzun sürebilir, normalde bir çizim işleminin tamamlandıktan sonra gecikmeli zaman açısından kritik iş parçacıklarının gecikmesini istemeyebilirsiniz.

## <a name="internal-guix-thread"></a>İç GUIX İş Parçacığı 

Belirtildiği gibi GUIX, GUI işlemenin toplu işlemini gerçekleştiren bir iç iş parçacığına sahip. Bu iş parçacığı , * gx_system_initialize **_** ve ardından _* gx_system_start **_çağrılarak_ oluşturulur.

İç GUIX iş parçacığının önceliği tarafından `#define GX_SYSTEM_THREAD_PRIORITY` belirlenir. Bu değer varsayılan olarak 16 (orta öncelikli) olur, ancak bu değer gx_port.h veya gx_user.h üst bilgi dosyasında belirterek varsayılan değeri geçersiz karak değiştirilebilir.

GUIX iş parçacığı zaman dilimi, varsayılan değeri `#define GX_SYSTEM_THREAD_TIMESLICE` 10 ms olan ile benzer şekilde tanımlanır.

Sistem iş parçacığının yığın sie `#define GX_THREAD_STACK_SIZE` ***değeri, gx_port.h*** üst bilgi dosyasında bulunan , ancak aynı zamanda bu değeri gx_user.h üst bilgi dosyanıza belirterek geçersiz kılınabilir tarafından belirlenir.

İç GUIX iş parçacığı yürütme döngüsü üç eylemden oluşur.
İlk olarak GUIX, GUIX olay kuyruğundan olayları alın ve GUIX pencere öğeleri ve pencere öğeleri tarafından iş için bu olayları döndürür. Olaylar genellikle düzenli aralıklarla süreerler, dokunmatik ekran veya tuş takımı gibi giriş cihazları ve kullanıcı girişini işleyene GUIX pencere öğeleri tarafından GUIX olay kuyruğuna eklenir. Ardından, tüm olaylar işlendikten sonra GUIX, ekran yenilemenin gerekli olup olmadığını belirler ve gerekirse görüntü grafik verilerini güncelleştirmek için gereken işlemeyi gerçekleştirir ve bu işlem genellikle kirli olarak işaretlenmiş pencerelerin ve pencere öğelerinin çizim işlevlerini çağırarak gerçekleştirir. Son olarak, GUIX yeni bir giriş olayı veya olayları gelene kadar GUIX iş parçacığını askıya alır.

## <a name="event-processing"></a>Olay İşleme 

Dokunma veya kalem girişi olayları, dokunma veya kalem girişi piksel konumunun altında en üstteki pencere veya pencere öğesi belirlenerek ve bu pencere/pencere öğesi olay işleme işlevi çağrılarak işlenir. Pencere öğesi kalem girişi olaylarını anlarsa, olayı bu pencere öğesi türü için uygun şekilde işler. Yoksa, en üst pencere öğesi işleme için pencere öğesi üst öğeye dokunma veya kalem girişi olayı iletir. Olayın zincire bu şekilde geçirmesi, olay işlenmeden veya olay kök pencereye gelene kadar devam eder ve bu durumda olay atılır.

Tuş takımı olayları, giriş odağı olan pencereye/pencere öğesine gönderilir. Giriş odak durumu GUIX bileşeni tarafından gx_system korunur.

Zamanlayıcı olayları her zaman iş için zamanlayıcının sahibi olan pencereye veya pencere öğesine sevk edilir.

Düğme tıklama olayları veya kaydırıcı değeri değişiklik olayları gibi dahili olarak oluşturulan olaylar her zaman olayı oluşturan pencere öğesinin üst öğesine gönderilir. Üst öğe olayı işlemezse, dokunma veya kalem giriş olaylarını gibi zincire geçirtir.

## <a name="drawing"></a>Çizim 

Tüm olay işleme tamamlandıktan sonra GUIX iç iş parçacığı herhangi bir görüntü güncelleştirmesi gerektirildiğini ve gerekli olup olmadığını belirler. Uygun pencere/pencere öğesi çizim işlevleri çağrılır. Çizim tamamlandığında GUIX iç iş parçacığı bir sonraki GUIX olayı için olay kuyruğunda bekler.

GUIX, her pencere *öğesi ve* tuval için yeniden çizilecek alanlar olan kirli alanlar kavramını uygulamaya almaktadır. Pencere öğesi yalnızca daha önce kirli olarak işaretlenmiş alanlara çizebilirsiniz. Bir pencere öğesi çizim işlevi çağrıldı mı, tüm çizim işlemleri önceden tanımlanmış kirli dikdörtgene dahili olarak kırpılır.
Bu alanı dışına çizme girişimleri yoksayılır.

Pencere öğeleri ve pencereler api işlevini çağırarak kendilerini kirli ***gx_system_dirty_mark.*** Bu işlev, pencere öğesi veya pencerenin tamamını yeniden çizildi olarak işaretler. bir pencere veya ***pencere gx_system_dirty_partial_add*** bir kısmını kirli olarak işaretlemek için alternatif olarak ikinci bir işlev olarak çağrılabilir.

Pencere öğelerini kirli olarak işaretleme ve ardından bu pencere öğelerini yalnızca tüm giriş olayları işlendiğinde yeniden çizme modeli ertelenmiş çizim *olarak adlandırılır.* GUIX ertelenmiş çizim algoritması ve kirli liste bakımı, çizim verimliliğini artırmak için tasarlanmıştır. Çizim işlemleri genellikle pahalı olduğu için GUIX gereksiz çizimleri önlemek için çok çalışır.

Çizim bir GUIX tuvale *yapılır.* Tuval, grafik verilerini tutmak için ayrılmış bir bellek alanıdır. Tuval, sistem mimarisine ve bellek kısıtlamalarına bağlı olarak donanım çerçevesi arabelleğine doğrudan bağlı olabilir veya bağlantılı değildir. Herhangi bir çizimin gerçekleşmesi için önce gx_canvas_drawing_initiate API işlevi çağrılarak ***bir tuvalin çizim için açılması*** gerekir. Bu API, tuvali çizim için hazırlar ve geçerli çizim *bağlamını oluşturur.* GUIX bir sistem tuval yenilemesi gerçekleştirerek çizim için tuval açılır ve pencere öğesi düzeyinde çizim API'leri çağrılmadan önce çizim bağlamı kurulur. Bu nedenle pencere öğelerinin pencere öğesi çizim işlevi içindeki tuvalde çizim başlatması gerekli değildir.

Ancak, bir uygulama standart GUIX ertelenmiş çizim algoritmasının akışının dışında bir tuvale hemen  çizim yapmak isterse, uygulama diğer çizim API'si işlevlerini çağırmadan önce gx_canvas_drawing_initiate'yi doğrudan çağırmalı ve hemen çizim tamamlandıktan sonra ***gx_canvas_drawing_complete'yi*** çağırmalıdır.

## <a name="user-input"></a>Kullanıcı Girişi 

GUIX, önceden tanımlanmış olay türlerine sahip dokunmatik ekran, fare ve klavye cihazlarını destekler. Özel olay türleri tanımlayarak veya özel giriş cihazı önceden tanımlanmış olay türlerine eşlerken ek giriş cihazları kullanılabilir.

Bu cihazlarla ilişkili eylemler, iç GUIX iş parçacığı tarafından işlenen olaylara çevrilir. Dokunmatik ekranı desteklemek için yazılan sürücü düzeyindeki yazılımlar, kaleme al, yukarı ve kalemle sürükleme işlemleri için GUIX olay kuyruğu olaylarını hazırlamalı ve göndermeli. Benzer şekilde, bir tuş takımı giriş sürücüsünün tuşa basma ve anahtar bırakma girişi için olaylar oluşturması gerekir.

## <a name="modal-dialog-execution"></a>Kalıcı İletişim Kutusu Yürütme 

Kalıcı iletişim kutusu yürütme, kullanıcıya diğer GUIX pencerelerinin veya pencere öğelerinin kullanıcı girişini aldan önce bir şekilde kapatılacak bir pencere sunarak ifade eder. Kalıcı iletişim kutuları, dokunma veya fare girişi olaylarının x,y konumundan bağımsız olarak iletişim kutusu görüntülenirken tüm kullanıcı girişini yakalar.

Kalıcı iletişim kutuları, uygulama yazılımı tarafından önce gx_window_create çağrılarak normal şekilde pencere oluşturulur ve ardından gx_window_create API işlevi ***çağrılarak gx_window_execute.***

İşlev ***gx_window_execute*** çağrıldı mı GUIX bir yerel olay işleme döngüsü girer. gx_window_execute  işlevi, iletişim kutusu kullanıcı girişi tarafından veya çağrısı tarafından kapatılana kadar çağırana ***gx_window_close.*** Bu nedenle, GUIX iç iş parçacığı dışında ***herhangi bir gx_window_execute*** işlevden hiçbir zaman çağrılmama önemlidir.

## <a name="periodic-processing"></a>Düzenli İşlem 

GUIX, görüntüleme etkileri, sprite animasyonu ve uygulama düzenli istekleri için destek sağlamak amacıyla bir ThreadX zamanlayıcısı kullanır. Bu tek süreölçer, GUIX zamanıyla ilgili tüm ihtiyaçların yapılması için kullanılır. Varsayılan olarak, GUIX iç süreölçeri işleme sıklığı, sabit daha önce gx_port.h veya **gx_user.h** üst bilgisinde tanımlanmamışsa, **_gx_api.h_** içinde tanımlanan sabit GX_SYSTEM_TIMER_MS aracılığıyla 20 saniye olarak ayarlanır. GuiX kitaplığını derleme sırasında veya gx_user.h içinde açıkça yeniden tanım kullanarak varsayılan sıklık uygulama tarafından bir derleme ***seçeneğiyle değiştirilebilir.***

> [!IMPORTANT]
> GUIX zamanlayıcı sıklığının RTOS süreölçer tıklarında ifade edildiklerini ve değerine göre **GX_SYSTEM_TIMER_TICKS.** değerinin **değeri GX_SYSTEM_TIMER_TICKS** ve GX_SYSTEM_TIMER_MS **kullanılarak** **TX_TIMER_TICKS_PER_SECOND.** Kullanıcı GUIX zamanlayıcı sıklığını ve çözünürlüğünü ayarlamak için ***gx_port.h** _ veya _ *_gx_user.h_** içinde bu değerlerden herhangi birini yeniden tanımlayabilir.

## <a name="display-driver"></a>Sürücü Görüntüle 

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

### <a name="guix-string-table"></a>GUIX Dize Tablosu 

GUIX dize tablosu ve dize kaynakları bir GUIX görüntüleme örneğiyle kaydedilir.

Çok görüntülemeli sistemlerde her ekran kendi dize tablosuna sahiptir ve her görüntü kendi seçili dilinde çalışmasına izin verir. Bu kaynak türleri her görüntü renk biçimine ve renk derinliğine özgü olduğu için diğer GUIX kaynak türleri (renkler, yazı tipleri ve piksel haritaları) GUIX Görüntüleme bileşeni tarafından da korunur.

Uygulama dizesi tabloyu el ile oluşturabilirsiniz ancak çoğu zaman görünen dize tablosu guiX Studio uygulaması tarafından proje kaynak dosyanız kapsamında tanımlanır. Kullanılabilir diller kaynak üst bilgi dosyasında da tanımlanır. Görünen dize tablosu, uygulama dizelerinin işaretçilerinin yer alan çok sütunlu bir tablosudur. Dize tablosu sütunlarının her biri, uygulama tarafından desteklenen bir dili temsil eder.
Uygulamanız yalnızca bir dili destekliyorsa (örneğin İngilizce) dize tablonda yalnızca bir sütun olur. Yine de, uygulama yazılımınızı değiştirmeden istediğiniz zaman ek diller için destek ebilirsiniz.

Etkin dize tablosu, api işlevi ***çağrılarak gx_display_string_table_set*** atanır. Bu işlev GUIX Studio tarafından oluşturulan başlangıç kodu tarafından otomatik olarak çağrılır, ancak etkin dize tablosu değiştirmek için doğrudan uygulama tarafından da çağrılabilir.

Etkin dil, api işlevi ***çağrılarak gx_display_active_language_set*** atanır. Bu işlev, görüntüleme dizesi tablosunda hangi sütunun etkin olduğunu belirler.

Bu işlev çağrıldığında, **GX_EVENT_LANGUAGE_CHANGE** GUIX pencere öğelerine yeni etkin dize verilerini görüntülemek üzere güncelleştirmelerine izin veren bir olay gönderilir.

Pencere öğeleri ve uygulama yazılımı, dize kimliği değerlerini ve API işlevlerini kullanarak statik ***gx_display_string_get_ext*** ***veya gx_widget_string_get_ext*** çözümler. Bu işlevler, **belirli GX_STRING** kimliği ve o anda etkin olan dille ilişkili olan verileri döndürür.

### <a name="bi-directional-text-display"></a>Çift Yönlü Metin Görüntüleme 

GUIX, çift yönlü metin desteği için iki strateji sağlar.

Seçeneklerden biri, GUIX Studio uygulamasında çift metin yeniden sıralama yapmaktır. Bu seçeneğin kullanımı GUIX Studio, çıkış dosyasına görüntüleme sırasına göre çift metin oluşturmakla sorumludur. Bu çözümün çalışma zamanı performansı üzerinde sıfır etkisi vardır ve GUIX çalışma zamanı kitaplığına herhangi bir ekleme gerektirmez. GUIX Studio'nun displayorder bidi metin dizeleri oluşturmasına izin vermek için GUIX Studio dil yapılandırması iletişim kutusundaki Görüntü Düzeninde **Bidi** Metni Oluştur onay kutusunu seçmeniz gerekir:

![Dilleri yapılandırma](./media/guix/user-guide/configure-languages.png)

Bu seçenekler seçiliyken, oluşturulan kaynak dosyası görüntüleme sırasında oluşturulan Bidi dizelerini içerir ve GUIX çalışma zamanı kitaplığında ek işlem gerekmez.

İkinci seçenek, çalışma zamanında çift metin yeniden sıralamasını yapmaktır. Bu seçenek dinamik olarak tanımlanan ve GUIX Studio uygulaması tarafından oluşturulmamış çift metin dizesini işlemesi gereken uygulamalar için de kullanılabilir. Bu durumda GUIX çalışma zamanı kitaplığı, her metin dizesini çizmeden önce bidi metnini yeniden sıralamakla sorumludur. Bu çözümün çalışma zamanı performansı ve bellek etkisi vardır. Çift metin yeniden sıralama işlemi için yeterli dinamik bellek kullanılabilir olmalıdır. Bu çözüm, GUIX kitaplığı GX_DYNAMIC_BIDI_TEXT_SUPPORT koşullu uygulamanın tanımlanmalıdır. Çalışma zamanında ***bidi*** ***gx_system_bidi_text_enable/gx_system_bidi_text_disable*** etkinleştirmek/devre dışı bırakmak için iki API işlevi sağlanır.

Hem kullanıcı adı GX_DYNAMIC_BIDI_TEXT_SUPPORT **hem** de GUIX Studio'yu görüntü sırasına göre Bidi metni oluşturmak üzere yapılandırmamalı. bidi metin dizesi işleme için bir strateji veya diğeri seçmeniz gerekir.

## <a name="memory-usage"></a>Bellek Kullanımı 

GUIX, uygulama programıyla birlikte yer almaktadır. Sonuç olarak, GUIX'in statik bellek (veya sabit bellek) kullanımı geliştirme araçları tarafından belirlenir; Örneğin, derleyici, bağlantılayıcı ve bulucu. Dinamik bellek (veya çalışma zamanı belleği) kullanımı uygulamanın doğrudan denetimi altındadır.

### <a name="static-memory-usage"></a>Statik Bellek Kullanımı 

Geliştirme araçlarının çoğu uygulama programı görüntüsünü beş temel bölüme böler: yönerge *,* *sabit,* başlatılan *veriler,* başlatılmamış *veriler* ve *GUIX iş parçacığı yığını.*  Aşağıdaki şekilde, bu bellek alanlarının olası bir düzeni gösterilmiştir:

![Bellek düzeni](./media/guix/user-guide/memory-area-example.png)

Bunun yalnızca bir örnek olduğunu anlamak önemlidir. Gerçek statik bellek düzeni işlemciye, geliştirme araçlarına, temel alınan donanıma ve uygulamanın kendisine özeldir.

Yönerge alanı, programın tüm işlemci yönergelerini içerir. Bu alan genellikle ROM'da bulunur.

Sabit alan, GUIX'te varsayılan ayarları ve tüm uygulama kaynaklarını (görüntüler, dizeler, yazı tipleri ve renkler) içeren çeşitli derlenmiş sabitler içerir. Ayrıca, bu alan başlatılan veri alanı "ilk kopyasını" içerir. Derleyicinin başlatma işlemi sırasında sabit alanı bu kısmı RAM'de genel olarak başlatılan verileri ayarlamak için kullanılır. Sabit alan genellikle en büyük olandır ve genellikle yönerge alanına sahiptir ve genellikle ROM'da bulunur.

GUIX piksel haritaları ve yazı tipleri genellikle büyük miktarlarda sabit veri depolaması gerektirir. Bu büyük statik veri alanları normalde ROM veya FLASH içinde tutulur.

GUIX iş parçacığı yığını, gx_system.h dosyasındaki ilklanmamış veri ***alanında (genel değişken*** olarak) aşağıdaki gibi tanımlanır:

```C
_gx_system_thread_stack[GX_THREAD_STACK_SIZE];
```

**GX_THREAD_STACK_SIZE** **_gx_port.h_** dosyasında tanımlanır, ancak ***gx_user.h*** üst bilgi dosyasında veya proje seçenekleri ya da komut satırı parametreleri aracılığıyla bu simge tanımlayarak uygulama tarafından geçersiz kılınabilir. Yığın boyutu en kötü olay işleme ve iç içe geçmiş çizim çağrılarını işecek kadar büyük olmalı.

### <a name="dynamic-memory-usage"></a>Dinamik Bellek Kullanımı 

Daha önce belirtildiği gibi, dinamik bellek kullanımı uygulamanın doğrudan denetimi altındadır. Tuvallerle ilişkili denetim blokları ve bellek, hedefin bellek alanı içinde herhangi bir yere yerleştirilebilir. Bu önemli bir özelliktir çünkü çalışma zamanında farklı fiziksel bellek türlerinin kolay kullanımını kolaylaştırır.

Örneğin, hedef donanım ortamının hem hızlı belleğe hem de yavaş belleğe sahip olduğunu varsayalım. Uygulamanın çizim için ek performansa ihtiyacı varsa, en iyi performans için tuval belleği açıkça yüksek hızlı bellek alanına yerleştirilebilir.

Çeşitli isteğe bağlı GUIX hizmetleri ve özellikleri, genellikle yığın olarak adlandırılan bir çalışma zamanı dinamik bellek ayırma mekanizması gerektirir. Bu hizmetler ve özellikler tamamen isteğe bağlıdır ve birçok GUIX uygulaması herhangi bir yığın kullanmaz ve çalışma zamanı bellek ayırma mekanizması tanımlamaz.

Çalışma zamanı bellek ayırması gerektiren hizmetleri kullanıyorsanız, bellek dinamik olarak ayrılmış veya serbest bırakıldığında GUIX'in çağıryacağı işlevleri yüklemeniz gerekir. Bu işlevleri istediğiniz gibi gerçekleştirebilirsiniz, böylece bu durumda bile dinamik bellek havuzunun konumu uygulama denetimi altında olur. Dinamik bellek ayırma desteğini yüklemek için uygulamanın, bellek ayırma ve bellek boş ***gx_system_memory_allocator_set*** tanımlamak üzere program başlatma sırasında API hizmetini çağırarak başlatması gerekir. Tam bir örnek için bu API'nin belgelerine bakın.

Çalışma zamanı bellek ayırma ve ayırmayı geri yükleme hizmeti gerektiren GUIX hizmetleri şunlardır:

  - Dış depolamadan GUIX çalışma zamanı ortamına ikili kaynak yükleme.

  - Yazılım çalışma zamanı jpeg görüntü kod çözücü.

  - Yazılım çalışma zamanı png görüntü kod çözücü.

  - Metin pencere öğelerini GX_STYLE_TEXT_COPY.

  - Çalışma zamanı pixemap yeniden boyutlandırma ve döndürme yardımcı programı işlevleri.
  - Çalışma zamanı ekranı ve pencere öğesi denetimi blok ayırma.

Daha küçük uygulamalar için GUIX kaynakları genellikle uygulama görüntüsünün bir parçası olarak derlenmiş ve statik olarak bağlantılıdır ve ikili kaynak yüklemesi gerekli değildir. İkili kaynaklar, bir uygulamanın çalışma zamanında flash sürücü veya URL gibi bir depolama konumdan yüklenen kaynakları (yazı tipleri, görüntüler, diller) yüklemesine olanak sağlar.

Çalışma zamanı jpeg ve png kod çözücüleri isteğe bağlı bileşenlerdir. GuiX uygulamalarının çoğu GUIX Studio aracının tüm gerekli görüntü dosyalarının kodunu önceden çözmesine ve bunları özel GUIX Pixemap veri kaynakları olarak depolamasına olanak sağlar. Bu hizmetler, jpeg ve/veya PNG görüntülerinin piksel haritası biçimine dönüştürmesini gerektiren uygulamalar için tamlık sağlar.

**GX_STYLE_TEXT_COPY,** kullanıcının belirli bir pencere öğesi veya pencere öğelerinin dinamik olarak atanan metnin kendi özel kopyasını tutacaklarını belirtmesini sağlar. Bu seçeneğin kullanımı, bellek ayırma mekanizmasının kullanımdan önce yüklü olması gerekir. Metin türü pencere öğesi **<span class="underline">oluşturulduğunda</span>** bu stil bayrağı sağlanmazsa, uygulamanın dinamik olarak oluşturulan ve atanan tüm metin dizeleri için statik depolama alanları ayırması gerekir. Bu durumda, otomatik değişkenler çalışma zamanı tarafından oluşturulan dize verilerini tutmak için kullanılmamalı. Kullanıcı **GX_STYLE_TEXT_COPY** etkinleştirilirse, her pencere öğesi atanan metnin kendi kopyasını oluşturacak olduğu için GUIX pencere öğelerine atanan dize verilerini tutmak için otomatik değişkenler kullanılabilir.

Piksel haritası yeniden boyutlandırma ve döndürme yardımcı programı işlevleri, sonuçta elde edilen piksel haritasını uygulamanın kullanımına yeni bir piksel haritası olarak döndürmektedir.
Bu hizmetler kullanılıyorsa, çalışma zamanı tarafından oluşturulan piksel haritası veri bloklarını tutmak için yeterli dinamik bellek kullanılabilir olmalıdır.

Son olarak, GUIX ekranlarının ve pencere öğelerinin denetim blokları statik veya dinamik olarak ayırabilirsiniz. Daha küçük uygulamalar için, program başlatma sırasında tüm uygulama ekranları oluşturmak ve statik olarak ayrılmış denetim blokları kullanmak yaygındır. Büyük uygulamalar için, ekran ve alt pencere öğesi denetimlerini gerektiğinde dinamik olarak oluşturmak yaygındır. Dinamik olarak ayrılan denetim blokları  GUIX Studio özellikleri görünümünde Çalışma Zamanı Ayır onay kutusu seçerek veya standart API aracılığıyla bir pencere öğesi oluştururken stil **bayrağı GX_STYLE_DYNAMICALLY_ALLOCATED** işareti geçerek belirtilir. Dinamik olarak ayrılan pencere öğesi denetim bloklarının kullanımı, bellek ayırma ve serbest ayırma hizmetlerinin yukarıda açıklandığı gibi tanımlanmalıdır.

## <a name="guix-components"></a>GUIX Bileşenleri 

GUIX API'leri, GUIX sisteminin temel bileşenlerine karşılık gelen birkaç temel gruba ayrılır ve düzenlenmiştir. Temel bileşenler şunlardır:

| Bileşenler  | Açıklama  |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GX_SYSTEM  | Başlatmadan, olaylardan, süreerlerden, dize tablolardan ve görünür pencere öğesi hiyerarşi yönetiminden sorumlu GUIX sistem bileşeni.                                                                                                                                                                                                                                                                      |
| GX_CANVAS  | Çizim alanı. Tuval, donanım çerçevesi arabelleğinin ince soyutlamaları olabileceği gibi, saf bellek tuvali de olabilir. Tuval türü, api işlevine geçirilen parametreler gx_canvas_create belirlenir.                                                                                                                                                                                   |
| GX_CONTEXT | Çizim bağlamı bileşeni. Çizim bağlamı, geçerli çizim işlemleri için ekran, tuval ve fırça ve kırpma alanı hakkında bilgi içerir.                                                                                                                                                                                                                                      |
| GX_DISPLAY | Uygulama ve GUIX pencere öğelerinin tuvalde çizim gerçekleştirmesine olanak sağlayan API'ler ve sürücü düzeyinde uygulamalar sağlar. GX_DISPLAY tuvalin gerekli renk biçimini kullanarak her tuvalde grafikleri doğru şekilde işlemek için uygulanır. Bu GX_DISPLAY, her bir görüntüye bağlı tuvallere çizilen pencere öğeleri için kullanılabilen kaynakları da (renkler, yazı tipleri ve piksel haritaları) yönetir. |
| GX_WIDGET  | Temel görünür pencere öğesi nesnesi ve ilişkili API'ler. Tüm GUIX pencere öğesi türleri temel alınan veya türetilen temel GX_WIDGET türetilen.                                                                                                                                                                                                                                                                      |
| GX_UTILITY | Dikdörtgenlerle çalışmaya yardımcı program işlevleri, dize dönüştürme işlevleri ve ANSI olmayan matematiksel işlevler bu gruba dahil edilir.                                                                                                                                                                                                                                                         |

GuiX, bu temel bileşenlere ek olarak, kitaplıkta sağlanan her pencere öğesi türüne özgü API'ler içerir. Bu API'ler, bu Kullanıcı Kılavuzu'nun 4. Bölümünde "GUIX Hizmetlerinin Açıklaması" bölümünde açıklanmıştır.

## <a name="guix-system-component"></a>GUIX Sistem Bileşeni

GUIX sistem bileşeni, kullanıcı arabirimi uygulamasına genel olan çeşitli hizmetler sağlar. Bu hizmetler *şunlardır: başlatma, olay yönetimi, görüntü yönetimi, kaynak yönetimi, zamanlayıcı yönetimi ve* *pencere öğesi yönetimi.* Her hizmet, uygulama programınız için gereklidir ve bu hizmetler aşağıdaki alt bölümlerde daha ayrıntılı olarak açıklanmıştır.

### <a name="initialization"></a>Başlatma 

GUIX başlatması, ***ThreadX*** tx_application_define yordamından (başlatma bağlamı) veya uygulama iş parçacıklarından uygulama tarafından çağrılmış gx_system_initialize hizmeti çağıran uygulama tarafından başarılı olur.  Gx_system_initialize  işlevi tüm genel GUIX veri yapılarını başlatarak GUIX sistem mutex, olay kuyruğu, zamanlayıcı ve iş parçacığı oluşturur. Bu ***gx_system_initialize,*** uygulama GUIX kullanabilir.

### <a name="thread-processing"></a>İş Parçacığı İşleme 

Başlatma sırasında oluşturulan iç GUIX iş parçacığı GUIX'te işlemenin çoğundan sorumludur. Bu iş parçacığında işlem ilk olarak, temel alınan görüntü sürücüsü için gereken ek başlatmayı tamamlar. Bu işlem tamamlandıktan sonra GUIX iş parçacığı ilk olarak GUIX olay kuyruğunda mevcut olan tüm olayları işleyin ve gerekirse ekranı yeniler bir döngü girer. Ekran yenileme, görünür olan ve kirli olarak işaretlenen ve yeniden çizilene göre gerekli GUIX çizim işlevlerini yürütür. Ekranda yenilenecek bir olay ve yenilenecek bir şey kalmadı olduğunda GUIX iş parçacığı askıya alınarak bir sonraki GUIX olayın gelmesini bekler.

### <a name="rtos-binding"></a>RTOS Bağlama 

GUIX sistem bileşeni varsayılan olarak iş parçacığı hizmetleri, olay kuyruğu hizmetleri ve zamanlayıcı hizmetleri gibi hizmetler için ThreadX gerçek zamanlı işletim sistemini kullanmak üzere yapılandırılmıştır. GUIX, guiX kitaplığını yeniden oluşturma ve önişlemci yönergesi GX_DISABLE_THREADX_BINDING kolayca diğer işletim sistemlerine taşınabilir. Bu, ThreadX bağımlılıklarını GUIX kaynak kodundan kaldırır ve uygulama geliştiricinin hedef sistem tarafından sağlanan RTOS'u kullanarak gerekli işletim sistemi hizmetlerini uygulamasına olanak sağlar. [Ek F - GUIX RTOS Bağlama](appendix-f.md) Hizmetleri, GUIX'i ThreadX işletim sistemi dışında bir işletim sistemine bağlantı noktası olarak uygulamak için uygulanması gereken hizmetleri açıklar.

### <a name="multithread-safety"></a>Çoklu İş Parçacığı Güvenliği 

GUIX API'si GUIX iş parçacığı bağlamından ve diğer uygulama iş parçacıklarından kullanılabilir. Uygulama iş parçacıkları olayları göndererek ve alarak, paylaşılan değişkenlere erişerek ve GUIX API işlevlerini kullanarak GUIX iş parçacığıyla etkileşime geçebilir. GUIX, çok iş parçacığı kaynak koruması için iç ThreadX mutex kullanır. Ayrıca GUIX, ekran yenileme işlemi başlatıldıktan sonra görünür pencere öğelerinin iç yapısının değiştirilmesini de önler. Çizim işlemleri devam ederken görünür nesnelerin ağacını değiştirebilecek API'ler engellenir ve ekran yenileme tamamlandıktan sonra yayınlanır.

### <a name="system-timers"></a>Sistem Süre süreleri 

GUIX, uygulamaya genellikle GUIX pencerelerde görüntülenen verilerin düzenli güncelleştirmeleri için kullanılan düzenli aralıklarla süre veren süreerler sağlar. Bu, ekran soldurma gibi GUIX sistem düzeyinde etkileri gerçekleştirmek için de kullanılan ThreadX düzenli aralıklarla zamanlayıcı aracılığıyla kullanılmaktadır.

Uygulama zamanlayıcılar oluşturabilir ve GUIX tarafından dahili olarak kullanılan zamanlayıcı tesisinden faydalanabilirsiniz. Elbette uygulama, gerekirse Doğrudan ThreadX sürelerini de oluşturabilir ve kullanabilir. GUIX sürelerini kullanmanın avantajı, kullanımı çok kolay ve GUIX olay odaklı işleme sistemi içinde çalışmak üzere önceden yapılandırılmışlarıdır.

Bir GUIX zamanlayıcısı oluşturmak ve başlatmak için uygulamanın işlevi ***gx_system_timer_start.*** Bu işlevin parametreleri, çağıran pencere öğesi işaretçisini, zamanlayıcı kimliğini (bir pencere öğesi birçok zamanlayıcıyı başlatmasına izin verir) ve ilk ve yeniden zaman aşımı değerlerini içerir. Yeniden zamanlama zaman aşımı değeri 0 ise, zamanlayıcı yalnızca bir kez çalıştıracak ve süresi dolduktan sonra etkin zamanlayıcı listesinden kendisini silebilir.

Başlatıldıktan sonra GUIX zamanlayıcısı GX_EVENT_TIMEOUT zamanlayıcı sahibine zamanlayıcı yeniden zamanlama değerine bağlı olarak bir kez veya düzenli aralıklarla olay gönderir. BIR GUIX zamanlayıcısı, api işlevi çağrılarak ***gx_system_timer_stop.***

### <a name="pen-speed-configuration"></a>Kalem Hızı Yapılandırması 

GUIX sistem bileşeni, kalem hızı izleme ile ilgili yapılandırma bilgilerini tutar. GUIX, GX_EVENT_VERTICAL_FLICK  ve **GX_EVENT_HORIZONTAL_FLICK** giriş sürücüsü tarafından oluşturulan PEN_DOWN hızına ve uzaklığına göre olayları dahili olarak oluştur. Uygulama, api işlevini kullanarak dahili olarak oluşturulan bu olayları tetiklemek için gereken en düşük **_mesafeyi ve gx_system_pen_configure_** yapılandırabilirsiniz.

### <a name="screen-stack"></a>Ekran Yığını 

GUIX sistem bileşeni GUIX ekran yığınıyla ilgili hizmetler sağlar. Bu, uygulama tarafından çalışma zamanında hangi ekranların alınabiliyor, hangi ekranlara alınabiliyor, sanal pencere öğesi yığınını destekleyen isteğe bağlı bir işlevdir. Ekran yığını, kullanıcının menü sisteminde çeşitli durumlara varma yolu çeşitli olduğu karmaşık menü sistemlerini yönetmek için kullanışlıdır. Menü sisteminde önceki durumuna dönmek, önce önceki ekran durumuna iterek, ardından yeni ekranı görüntüleyerek ve geçerli ekran silince yeni ekranın ekran yığınından önceki durumu görüntülemesine izin vererek kolayca yapılabilir.

### <a name="clipboard-maintenance"></a>Pano Bakımı 

GUIX, çalışma zamanı yürütme sırasında metin kopyalamak ve yapıştırmak için bir pano destekler. Bu destek GUIX Sistemi bileşeni tarafından sağlanır.

### <a name="dirty-list-maintenance"></a>Kirli Liste Bakımı 

GUIX kirli pencere öğelerinin listesini bulundurarak, durum değişiklikleri nedeniyle görünür olan ve yeniden çizilen veya yeni görünür hale gelen pencere öğeleri anlamına gelir. Bu kirli liste, GUIX'in her kullanıcı arabirimi değişikliği yapılırken tuval yenilemesi yapmak yerine kullanıcı arabirimi durumundaki tüm geçerli değişiklikleri yansıtması için bir tuval yenileme işlemi yapmalarına izin vererek çizim performansını artırır.
Bu kirli liste GUIX sistem bileşeni tarafından da korunur.

### <a name="animation-control-block-pool"></a>Animasyon Denetimi Blok Havuzu 

Uygulamalar genellikle birden çok animasyon dizisini paralel olarak yürütmek için kullanılır. GUIX, uygulamanın ayırarak kullanabileceği bir animasyon denetim blokları havuzu sağlar. Bu, uygulamayı statik olarak bu denetim bloklarını tanımlamaya karşı serbesttir ve uygulamanın tanımy olabileceği her animasyon için benzersiz bir animasyon denetim bloğu tanımlamak yerine farklı zamanlarda yeniden kullanılmasına olanak sağlar. Animasyon denetim bloğu havuzu GUIX sistem bileşeni tarafından da korunur.

### <a name="system-error-handling"></a>Sistem Hatası İşleme 

GUIX sistem hatası işleyicisi, uygulamanın API açısından daha zor olan GUIX'te iç sistem hatalarını bulma konusunda yardımcı olması için tasarlanmıştır. GUIX içinde bir sistem hatası oluştuğunda iç ***_gx_system_error_process*** çağrılır. Bu işlev, sağlanan hata kodunu kaydeder ve algılanan toplam sistem hatası sayısını artırır. Sistem hata değişkenleri aşağıdaki gibi tanımlanır:

UINT **_gx_system_last_error;**

ULONG **_gx_system_error_count;**

GUIX uygulaması garip görünüyorsa hata ayıklayıcıda hata sayısı değişkenine bakmak yararlı olur. Ayarlanırsa, sorunu gidermenin iyi bir yolu, _gx_system_error_process işlevinde  bir kesme noktası ayarlamak ve çağrılma zaman/nereden çağrıldılarını görmektir.

## <a name="guix-canvas-component"></a>GUIX Tuval Bileşeni

Tuval bileşeni, tuvalle ilgili tüm işlemelerden sorumludur. Tuval etkili bir şekilde sanal çerçeve arabelleğidir. Uygulamanın grafik çıktı üretmesi için en az bir tuval oluşturması gerekir.
Genellikle, sisteminiz tarafından desteklenen her fiziksel görüntü için en az bir tuval oluşturabilirsiniz.

Tüm GUIX çizimleri tuvalde uzer. Daha basit veya bellekle kısıtlanmış sistemlerde büyük olasılıkla görünür çerçeve arabelleğine doğrudan bağlanacak tek bir tuval olacaktır, ancak daha fazla belleğe ve daha gelişmiş grafik gereksinimlerine sahip sistemler birden çok tuvale ihtiyaç görebilir. Birden çok tuvalin tek bir görüntü için kullanılabilir hale geliyor, ekran ve pencere soldurma ve soldurma etkileri gibi özelliklere olanak sağlar.
Tuvaller basit veya yönetilen iki ana türden biri olabilir.

Basit bir tuval, uygulama tarafından kullanılan ekran dışı çizim alanıdır.
GUIX, basit bir tuvalle doğrudan bir şey yapmasa da uygulama, karmaşık çizimleri bir kapalı ekran arabelleğine işlemek için basit bir tuval kullanabilir ve ardından gerektiğinde görünür tuvali yenilemek için bu kapalı ekran arabelleği kullanabilir.

Yönetilen tuval GUIX tarafından donanım çerçevesi arabelleği içinde otomatik olarak görüntülenir. Yönetilen tuval, birden çok yönetilen tuvali desteklemek için yeterli belleğe sahip olan sistemler için bileşik tuval oluşturabilir. Yönetilen tuvaller GUIX tarafından yönetilen bir Z düzenine sahiptir ve görünüm kırpma tüm yönetilen tuvallerde uygulanır.

Tuval, daha genel olduğu için çerçeve arabelleğinden farklıdır. Bellek kısıtlı sistemlerde yalnızca bir tuval olabilir ve bu tuvalin belleği görünür çerçeve arabelleği belleği olabilir. Ancak, daha gelişmiş grafik katmanlarını ve birden çok tuvali destekleyen daha karmaşık sistemler için, yönetilen tuvallerin her biri donanım çerçevesi arabellek belleğinden ayrı kendi bellek alanları ayrılır.
Bu yönetilen tuvaller, çerçeve arabelleği yenileme veya geçiş işlemi sırasında görünür çerçeve arabelleğine işlenir.

Birden çok grafik katmanını destekleyen donanımlar (örneğin, birden çok katmanlı çerçeve arabellekleri) için uygulama, gx_canvas_hardware_layer_bind API'sini kullanarak bir ***veya daha fazla tuvali donanım grafik katmanlarına*** bağ hale gx_canvas_hardware_layer_bind. Bu hizmet tuvale belirli bir donanım grafik katmanına bağlı olduğunu ve bağlantılı bir tuvalin tuval görünürlüğü için donanım desteğini (örneğin, gx_canvas_show, gx_canvas_hide), tuval alfa karıştırma (gx_canvas_alpha_set ***)*** ve görüntü içindeki tuval uzaklığı ***(*** gx_canvas_offset_set ).

En basit tek tuval/tek çerçeve arabelleği kuruluşu dışında mimarilerde tuvalin boyutu uygulama tarafından belirlenir ve çerçeve arabelleğinin sabit boyutundan farklı olabilir.
Uygulama tarafından seçilen bir uzaklıkta da olabilir. Z düzeni gibi diğer bilgiler tuval içinde korunur. Tuval çizimi tamamlandığında, tuvalin içeriği görüntü sürücüsü tarafından fiziksel görüntüye aktarılır. Ayrı bir tuval ve çerçeve arabelleği bellek alanları için yeterli belleğe sahip olan bazı sistemlerde tuval güncelleştirmesi aslında görüntü sürücüsü aracılığıyla doğrudan fiziksel görüntüye yapılır.

### <a name="canvas-creation"></a>Tuval Oluşturma 

Bir tuval nesnesi başlatma sırasında veya uygulama iş parçacıklarının yürütülmesi sırasında herhangi bir zamanda oluşturulabilir. Bir uygulama tarafından oluşturulacak tuval nesnelerinin sayısına bir sınır yoktur. Ancak çoğu uygulama, tüm GUIX çizimi için yalnızca bir tuval nesnesi oluşturur.

### <a name="canvas-control-block"></a>Tuval Denetim Bloğu 

Her tuval nesnesinin özellikleri, denetim bloğu  GX_CANVAS bulunur ve **_gx_api.h içinde tanımlanır._** Tuval nesnesi için gereken bellek uygulama tarafından sağlanır ve bellekte herhangi bir yerde yer alıyor olabilir. Ancak, tuval nesnesi denetim bloğu ve çizim alanı, bunları herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline yaygındır.

### <a name="canvas-alpha-channel"></a>Tuval Alfa Kanalı

GUIX piksel başına karıştırma oranı belirten bit eşlem alfa kanalı, 16 bpp ve daha yüksek renk derinliğinde fırça karıştırma oranını belirten fırça alfası ve bir katman tuvali için karıştırma oranını belirten tuval alfası dahil olmak üzere birçok düzeyde ön plan ve arka plan renklerinin alfa karışımını destekler.

Bir tuvalin alfa değeri, çerçeve arabelleği içinde görüntülenmek için bir araya bir araya getirdi birden çok tuval olduğunda kullanılır. Tuval Z düzeni tuvalin diğer tuvallerin üzerinde olması gibi bir düzende ise tuval alfa değeri, tuvali arkalarında bulunanlarla karıştıran şekilde ayarlanmış olabilir. Tuvalin alfa değerinin hızla değiştirilmesi, "soldurma" ekran geçişi etkileri sağlamak için kullanılır, ancak tuval alfası birçok şekilde kullanılabilir.

Tuval, gx_canvas_hardware_layer_bind() kullanarak bir donanım grafik katmanına bağlı ise GUIX, donanım desteğini kullanarak tuval alfa karıştırması uygulamaya çalışarak katman tuvalini karıştırmayla ilişkili yazılım ek yükünü en aza indirir.

Alfa değerleri 0 ile 255 arasında değişebilir; burada 0 değeri pikselin tamamen saydam olduğu anlamına gelir ve 0'dan büyük değerler daha az saydam tuval alfa değeri artarken tuval karıştırma için donanım yardımı sağlanıyorsa yalnızca 16 bpp ve üzerinde çalışan ekran sürücüleri için destek sağlanıyor.

### <a name="canvas-offset"></a>Tuval Uzaklığı 

Bir tuval, api hizmetinin kullanımıyla birlikte gx_canvas_offset_set çerçeve ***arabelleği*** içinde kaydırabilirsiniz. Tuval uzaklıkları genellikle sprite animasyonları uygulamak için kullanılır. Bir tuval, ***gx_canvas_hardware_layer_bind*** API işlevinin çağrısıyla bir donanım grafik katmanına bağlı ise GUIX, donanım desteğini kullanarak tuval uzaklığı değişikliklerini uygulamaya çalışarak tuval konumunu kaydırmayla ilişkili yazılım ek yükünü en aza indirir.

### <a name="canvas-drawing"></a>Tuval Çizimi 

GUIX tuval bileşeni, uygulamaya tam bir çizim API'si sağlar. Gx_canvas_line_draw veya ***gx_canvas_pixelmap_draw*** gibi çizim ***API'leri*** çağrılmadan önce, gx_canvas_drawing_initiate API işlevi çağrılarak hedef ***tuvalin çizim için açılması*** gerekir. Bu işlev, tuvali çizim için hazırlar ve bir çizim ***bağlamı oluşturur.***

***gx_canvas_line_draw** _ veya _*_gx_canvas_text_draw_*_ gibi tuvale işleme alan çizim API'leri, çizgi stilini, genişliğini ve renklerini tanımlamak için geçerli çizim bağlam fırçasında bulunan parametreleri kullanır. Bu fırça parametreleri , _*__* gx_context_brush_define_*_ _* **, * _gx_context_brush_set_**gx_context_brush_style_set**_ ve benzer API işlevleri çağrılarak _* gx_canvas_drawing_initiate **_çağrılarak değiştirilir._

GUIX, pencere ve pencere öğesi çizme işlevlerini ertelenen tuval yenileme işlemi kapsamında çağırsa, hedef tuval pencere öğesi çizim işlevlerini çağırmadan önce çizim için açılır. Bu nedenle, hedef tuvali açmak için standart pencere öğesi çizim işlevleri gerekli değildir, bunlar için bu yapıldı.

Bazı durumlarda uygulama, tuvale hemen çizim yapmak istiyor olabilir. Bu durumda, uygulama aşağıdaki adımları gerçekleştirebilir.

1. Uygulamanın ***gx_canvas_drawing_initiate*** istediği tuvalin içindeki hedef tuvali ve dikdörtgeni geçerek gx_canvas_drawing_initiate API işlevini çağırma. 

2. İstenen çizimi gerçekleştirmek için istediğiniz sayıda tuval çizimi API'lerini çağırma.

3. Çizimin ***gx_canvas_drawing_complete*** için api işlevini çağırma. Bu işlem tuvali görünür çerçeve arabelleğine boşaltır ve/veya sistem belleği mimarisine bağlı olarak bir arabelleğe geçiş işlemi tetikler.

### <a name="drawing-apis"></a>Çizim API'leri 

GUIX'in ekranda tüm görsel öğeleri çizmesi için gereken birkaç temel çizim temel öğeleri vardır. Bu çizim API'leri genellikle bir özel pencere öğesi çizim işlevinin parçası olarak uygulama yazılımı tarafından da çağrılabilir. Bu GUIX tuval çizim API'leri parametre doğrulama ve kırpma işlemi gerçekleştirerek kırpılmış çizim koordinatlarını donanım ve renk biçimine özgü çizim uygulamaları için görüntü sürücüsüne iletir. Bu çizim API'si işlevleri aşağıdaki gibi tanımlanır.

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

Çizim API'si GUIX Tuval API'si aracılığıyla çağrılır ve tüm çizim gx_canvas_* API işlevleri kullanılarak yapılır. Çizim, geçerli çizim bağlamında geçerli fırça kullanılarak yapılır. Yukarıdaki şekil çizimi işlevlerden herhangi biri, geçerli fırça tarafından tanımlandığı gibi düz renk dolgulu veya piksel haritası ile doldurulan ana hatlarıyla özet olabilir. Şekil ana hat genişliğini, rengini veya dolguyu değiştirmek için gx_context_brush_* API işlevlerini kullanarak fırçayı geçerli çizim bağlamında tanımlayın.

Yukarıdaki uygulama düzeyi çizim API'leri tuvale gerçek çizim yapmaz, bunun yerine görüntü sürücüsü düzeyinde çizim işlevini çağıranın parametrelerini doğrular. Sürücü düzeyinde çizim işlevi aslında piksel verilerini tuval belleğine yazar.

GUIX, piksel başına 1, 2, 4, 8, 16, 24 ve 32 bit (bpp) dahil olmak üzere çeşitli renk derinlikleri için stok veya genel görüntü sürücüsü çizimi işlevleri sağlar. Bazı durumlarda, varsayılan yazılım çizim uygulaması, 2D çizim hızlandırıcısı sağlayan donanım hedefleri için donanım hızlandırmalı uygulamalarla değiştirilir.

### <a name="color-depth"></a>Renk Derinliği 

GUIX, 32 bpp'ye kadar renk derinliğinin yanı sıra tek renkli ve gri tonlamayı destekler. Renk derinliği desteğinin türü, temel alınan fiziksel ekranın özellikleri tarafından büyük ölçüde belirlenir ve tuval çizim alanı için ne kadar bellek gerekli olduğu üzerinde de bir etkisi vardır. Aşağıda renk derinliği desteğinin bir listesi ve bu renk derinliği içindeki varyasyonların kısa bir açıklaması ve yer almaktadır.

| Renk &nbsp; Biçimi       | Açıklama                                                                                                   |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| 1 bitlik tek renkli   | Piksel paketli biçim başına 1 bit.                                                                                                   |
| 2 bit gri tonlamalı    | 4 gri düzey, her bir bayta dört piksel paketlenir.                                                                                      |
| 4 bit gri tonlamalı    | 16 gri düzey, her bir bayta iki piksel paketlenir.                                                                                      |
| 4 bit renk        | VGA biçimli planar bellek kuruluşu.                                                                                         |
| 8 bit gri tonlamalı    | 256 gri düzey                                                                                                                  |
| 8 bit palet modu | Palet dizini olarak kullanılan piksel başına 1 byte                                                                                           |
| 8 bit r:g:b modu   | Daha az yaygın olarak kullanılan 2:3:2 r:g:b biçimi.                                                                                         |
| 16 bit             | Her piksel için iki bayt gerekir. r:g:b veya b:g:r byte sırası olabilir. Normalde 5:6:5 yapısı, ancak 5:5:5 yapısı veya 4:4:4:4 a:r:g:b yapısı da olabilir. |
| 24 bit             | Her piksel için 3 (paketlenmiş biçim) veya 4 (paketsiz biçim) bayt gerekir. Donanım için gereken r:g:b veya b:g:r byte sırasına göre olabilir. |
| 32 bit             | Her piksel için alfa kanalıyla 4 bayt gerekir. a:r:g:b veya b:g:r:a byte sırası olabilir ve donanıma göre belirlenir.              |

### <a name="mouse-support"></a>Fare Desteği 

GUIX, istenen herhangi bir tuvale fare imleci çizmeyi destekler. Fare imleci yazılımda çizili olabilir veya donanım imleç katmanlarında destek olabilir. Her iki durumda da, yazılım veya donanım fare imleç çizimi kullansanız da, uygulamaya fare imleç desteğiyle ilgili olarak sağlanan API aynıdır.

GUIX fare desteği yalnızca `#define GX_MOUSE_SUPPORT` GUIX kitaplığını oluşturmadan önce gx_user.h üst bilgi dosyasında tanımlandığı zaman etkinleştirilir.

Uygulama, api işlevini kullanarak fare imlecini ve etkin ***gx_canvas_mouse_define*** tanımlamalı. Bu API, imleç görüntüsünün çizilecek tuval işaretçisini ve **fare** imleci görüntüsünü ve fare görüntüsünün etkin noktasını tanımlayan GX_MOUSE_CURSOR_INFO yapısının işaretçisini sol üst köşedeki görüntüye göre tanımlar.

## <a name="guix-display-component"></a>GUIX Görüntüleme Bileşeni 

Görüntüleme bileşeni GUIX'te temeldir çünkü kendi içinde bir veya daha fazla tuval, pencere öğesi ve pencere içeren tüm görüntüleme nesnelerinin işlemesini yönetir. Görüntüleme bileşeni ayrıca bir dizi işlev işaretçisi aracılığıyla her bir ekranla ilişkili temel donanım ekran sürücüsüyle etkileşime geçmektedir.

### <a name="display-creation"></a>Görüntü Oluşturma 

Başlatma sırasında veya uygulama iş parçacıklarının yürütülmesi sırasında herhangi bir zamanda bir görüntüleme nesnesi oluşturulabilir. Genellikle bir uygulama, her fiziksel ekranı yönetmek için bir görüntüleme nesnesi oluşturur. Uygulama ve kullanılabilir fiziksel ekranları tanımlamak için GUIX Studio kullandıysanız, ekranlarınızı oluşturmak ve başlatmak için gx_studio_display_configure API işlevini kullanırsınız.

### <a name="display-control-block"></a>Denetim Bloğu görüntüleme 

Her görüntüleme nesnesinin özellikleri ***** GX_DISPLAY _ denetim bloğunda bulunur ve _*_gx_api.h ** içinde_ tanımlanır. Görüntüleme nesnesi için gereken bellek uygulama tarafından sağlanır ve bellekte herhangi bir yerde yer alıyor olabilir. Ancak, en yaygın olarak herhangi bir işlevin kapsamı dışında tanımlayarak görüntüleme denetimi bloğu genel bir yapı yapmaktır.

### <a name="resource-management"></a>Kaynak Yönetimi 

Kaynaklar, uygulamanın ihtiyaç kaynağı olan kullanıcı arabirimi bileşenleridir ancak uygulama kodu değildir. Kaynaklar uygulama verileridir ve genellikle statik olarak tanımlanır. Kaynak türleri piksel haritalarını, yazı tiplerini, renkleri ve dizeleri içerir. Bu kaynaklar genellikle herhangi bir uygulama yazılımı değiştirmeden herhangi bir zamanda değiştirilebilir. Uygulama yazılımında yapılan değişiklikler genellikle ilgili yeniden test ve doğrulamayı gerektirse de uygulama kodunda değişiklik yapmadan kullanıcı arabirimi görünümünün değiştirilmesine izin vermek için, ve başvurularının depolama alanını uygulama yazılımından ayrı tutmak önemlidir.

GUIX ***görüntüleme*** modülü, ekranın renk derinliğine ve biçimine bağlı olan tüm kaynaklar için kaynak yönetimi olanakları sağlar. Bu özellikler arasında etkin piksel haritası tablosu, etkin yazı tipi tablosu ve etkin renk tablosu bakımı yer alır. Dize tablosu kaynağı GUIX sistem modülü tarafından korunur, çünkü dize kaynaklarının normalde renk derinliğine ve biçimine göre değişmesi gerekli değildir.

Uygulama yazılımı kaynaklara kaynak kimliğine göre başvurur ve bu da karşılık gelen kaynak tablosuna bir dizindir. Bu, tabloyu değiştirmeye olanak sağlar. Örneğin, bir ürün "gün modundan" "gece moduna" değişse de renk kimliği değerleri aynı kalacaksa renk tablosu değiştirilebilir.

Uygulama kaynaklarınız GUIX Studio uygulaması tarafından bir kaynak dosyasına (veya kaynak dosyaları kümesine) yazılır. Varsayılan renkler, piksel haritaları ve yazı tipleri yeni bir GUIX Studio projesi oluşturma sırasında otomatik olarak sağlanır, ancak bu varsayılanlar, uygulamanın görünüm ve görünümlerini tanımladığınız şekilde kolayca değiştirilir.

Renklerin, yazı tiplerinin ve piksel haritalarının Kaynak Kimliklerinin etkin Görüntüleme bileşeni bilinene kadar gerçek renk, yazı tipi veya piksel haritası değerlerine çözümlenemediklerine dikkat edin. GUIX mimarisi birden çok etkin ekranı desteklediği için, Kaynak Kimlikleri yalnızca bir pencere öğesi ve ilişkili Kaynak Kimliği belirli bir görüntüye çözümlenemezse kaynak değerlerine çözümlenir. Bu özellik dinamik bağlama olarak bilinir. Metin rengi gibi bir özelliğin Kaynak Kimliği (örneğin, kaynak kimliği **GX_COLOR_ID_TEXT) bir** görüntüde kullanılırken beyaz için 16 bit R:G:B değerine çözümleniyor olabilir, ancak aynı renk kimliği başka bir görüntüde kullanılırken siyah renkli bir siyah renkli değere çözümleniyor olabilir.

Uygulamada, Kaynak kimliklerinin kaynak değerlerine dinamik olarak bağlanması, uygulama yazılımı ve GUIX iç bileşenlerinin genellikle kaynak kimliklerini yalnızca etkin çizim bağlamındaki kaynak değerlerine çözümlemesi gerektiği anlamına gelir. Etkin çizim bağlamı, GUIX'in her Kaynak Kimliğini belirli bir kaynak değerine çözümlemesini sağlayan o anda etkin olan ekranı belirtir. Uygulama yazılımının çizim bağlamı dışında belirli bir kaynak değerini bulmak için gerekli olması, görünür pencere öğeleri için de yapılabilir. Görünür pencere öğeleri, etkin tuvali çözümlemek ve bu pencere öğesi için görüntülemek için de kullanılabilir bir kök pencere penceresine bağlıdır.

Bir pencere öğesi oluşturulmuş ancak henüz görüntülenmemişse (başka bir kök pencereye veya diğer görünür üst öğeye bağlı değil), pencere öğesiyle ilişkili tüm kaynak kimlikleri doğrudan belirli bir görüntüye atanan kaynak tablosuna dizin oluşturma dışında belirli bir kaynak değerine çözümlenemiyor. Belirli bir kaynak tablosuna bu doğrudan erişim uygulama yazılımı tarafından güvenli bir şekilde yapılabilir, ancak iç GUIX kitaplık yazılımında hiçbir zaman yapılmaz.

### <a name="widget-defaults"></a>Pencere Öğesi Varsayılanları 

GUIX görüntüleme bileşeni ayrıca çeşitli pencere öğesi öznitelikleri için varsayılan tanımlar sağlar. Uygulama tarafından aksi belirtilmedikçe pencere öğeleri/pencereler bu sistem öznitelikleriyle oluşturulur. Bu sistem öznitelikleri genellikle sistem kaynak tablolarında bakımı yapılan yazı tipleri, renkler ve bit eşlemlerden oluşur. Varsayılan kaydırma çubuğu görünümü için ek öznitelikler GUIX görüntüleme bileşeni tarafından da korunur.

Varsayılan renk ayarları, her görüntüye atanan renk tablosu ve önceden tanımlanmış varsayılan renk kimlikleri tarafından tanımlanır. Bu varsayılan renk kimlikleri aşağıdakileri içerir.

| Renk Kimliği | Açıklama |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| GX_COLOR_ID_CANVAS | Varsayılan tuval (arka planı görüntüleme) rengi |
| GX_COLOR_ID_WIDGET_FILL | Varsayılan pencere öğesi dolgu rengi |
| GX_COLOR_ID_WINDOW_FILL | Varsayılan pencere dolgu rengi |
| GX_COLOR_ID_DISABLED_FILL | Varsayılan devre dışı bırakılmış pencere öğesi dolgu rengi |
| GX_COLOR_ID_DEFAULT_BORDER | Varsayılan pencere öğesi kenarlık rengi |
| GX_COLOR_ID_WINDOW_BORDER | Varsayılan pencere kenarlık rengi |
| GX_COLOR_ID_TEXT | Varsayılan metin rengi |
| GX_COLOR_ID_SELECTED_TEXT | Varsayılan seçilen metin rengi |
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

Etkin fırçayla **GX_BRUSH_ALIAS** flaş ayarlanarak, daha fazla diğer çizgi çizimi etkinleştirilir. Bu, doğrudan çizilen çizgilerin yanı sıra çokgen veya dairenin kenarlığı olarak çizilen çizgiler için de geçerlidir.

Diğer addan koruma metin çizimi, GUIX studio uygulaması tarafından üretilen diğer addan koruma yazı tipi kullanılarak etkinleştirilir. Yazı tipini oluşturmadan önce yazı tipinin antialiased veya ikili olarak mı oluşturul olacağını belirtirsiniz.
GUIX'te diğer adlara sahip olmayan yazı tipleri, her piksel için 16 saydamlık düzeyi kullanır.

### <a name="clipping"></a>Kırpma 

Kırpma, GUIX görüntüleme bileşeni tarafından dahili olarak ve GUIX pencere öğeleri tarafından bakımı yapılan üst-alt mimariye göre pencere ve pencere öğesi katmanları tarafından de destekleniyor. Hiçbir pencere öğesi veya pencere öğesi hiçbir zaman pencere öğesi alanı dışına çizilmiyor ve bir pencere öğesi hiçbir zaman pencere öğesi üst öğenin alanı dışına çizilmiyor.

Bu ayrıca, pencere öğelerinin tuval belleğinin dışında bulunan piksel koordinatlarına çizmesini de önler ve bu da büyük olasılıkla bellek bozulmasına veya sistem hatasına yol açabilir. Pencere öğelerinin pencere öğesi alanı, pencere öğesi üst alanı veya tuval kapsamının dışında çizmesine izin verilmez.

Ayrıca, pencere öğeleri yalnızca daha önce kirli olarak işaretlenmiş alanlara çizebilirsiniz. Bu, pencerenin yalnızca bir köşesinin ortaya çıkarması gibi bir pencerenin tamamının çizilenesini önler. Pencerenin yalnızca gerçekten yenilenmesi gereken kısmı kirli olarak işaretlenir ve bu nedenle pencere çizimi işlevi yalnızca kirli alanda pikselleri gerçekten yeniler.

GUIX görüntüleme bileşeni, sürücü düzeyinde çizim işlevlerini iptalmeden önce bu kırpma algoritmalarını zorlar.

### <a name="views"></a>Görünümler 

GUIX, her kök pencere ve kök pencerenin her alt penceresi için her zaman bir görünüm kümesi sağlar. Görünümler, pencere konumu ve Z sırası değiştirildiğinde değiştirilen dinamik, çalışma zamanı belirlenen bir kırpma alanıdır.
GUIX, arka plandaki pencere veya pencere öğelerinin ön planda bir pencere veya pencere öğesi üzerine çizmesini önlemek için görünümleri kullanır. Görünümler Z düzeni disiplini gerektirir. Ayrıca görünümler, arka planda yer alan bir pencerenin tuvalin görülen herhangi bir alanına çizimini önleme açısından verimlilik açısından önemlidir. Bir pencere başka bir pencere tarafından tamamen kapsamışsa, bunu yapmaya çalışsa bile, kaplanmış pencerenin tuvale çizmesine izin verilmez.

### <a name="display-driver-interface"></a>Sürücü Arabirimini Görüntüleme 

GUIX ekran sürücüleri, temel alınan fiziksel ekranla tüm etkileşimden sorumludur. Görüntü sürücülerinin üç temel işlevi vardır: başlatma, çizim ve çerçeve arabelleği görüntüsü.
Başlatma, fiziksel görüntüleme donanımının hazırlanmasından, GUIX'in fiziksel görüntüleme donanımının özelliklerini bilgilendirmeden ve GUIX'e hangi çizim işlevlerinin kullan gerektiğini bildirmekten sorumludur. Ana görüntü sürücüsü başlatma, ***GUIX*** gx_display_create çağrılır. Ayrıca GUIX iş parçacığı, iş parçacığı bağlamından ikincil bir görüntü sürücüsü başlatmayı da çağıracak. Bu ikincil görüntü sürücüsü yalnızca başlatma işlemi sırasında RTOS hizmetleri gerektiriyorsa (örneğin,  cihaz kesintileri veya tx_thread_sleep başlatma işlemi arasındaki gecikme istekleri için gereklidir.

Başlatma tamamlandıktan sonra, görüntüleme sürücüsü fiziksel görüntüleme donanımlarında yap yalnızca çizimden sorumludur.
Son olarak, görüntü sürücüsü çerçeve arabelleğinin görüntülenmesinden sorumludur.

## <a name="guix-widget-component"></a>GUIX Pencere Öğesi Bileşeni

GUIX pencere öğesi, görünür bir grafik öğesidir. Süreerler ve matematik yardımcı programı işlevleri gibi görünür değildir GUIX bileşenleri vardır.
Ancak tüm görünür bileşenler temel GUIX pencere öğesi bileşeninden türetilen. GUIX pencere öğesi, GUIX ekranın birincil yapı taşıdır. Diğer tüm grafik öğeler temel pencere öğesi işlevinden türetilen öğelerdir.

GUIX pencere öğeleri, tam devralma desteğiyle nesne odaklı bir şekilde uygulanır. Bu, mümkün olan en küçük bellek ve işlem gereksinimleriyle sonuçlandıran ANSI C kullanılarak gereksinimlerini karşılar. **temel** GX_WIDGET gibi başka bir pencere öğesinden türetilen GX_BUTTON gibi belirli bir pencere öğesinden söz etmek,  **GX_BUTTON** denetim yapısının GX_WIDGET'nin tüm üye değişkenlerini ve işlev işaretçilerini içerdiğini ve GX_BUTTON'a özgü bazı ek değişkenleri içerdiğini ifade **eder.**   GUIX, pencere öğelerinin katmanlarını bu şekilde biriktir, böylece daha karmaşık pencere öğeleri her zaman onlardan önce daha basit bir pencere öğesi temel almaktadır. Bu hiyerarşik türetme modeli, pencere öğesi parametrelerini değiştirmek için kullanılan API'leri öğrenmeyi kolaylaştırır. Bir düğmenin rengini değiştirmek için, pencere öğesi rengini değiştirmek için aynı API'yi kullanırsınız, yani ***gx_widget_fill_color_set.***

Görünür pencere öğelerinin organizasyonu, alt pencere öğelerinin üst öğelerine bağlantısı olan ağaç yapılandırılmış listeleri kullanılarak üst-alt öğe olarak korunur. Çocuk, üstlerinden, çizerek çizenin görünümler ve üzerinde çiz yaptıkları tuval gibi özellikleri devralabilir.
Alt pencere öğeleri, yine üst öğeden çeşitli özellikleri devralan kendi alt pencere öğelerine sahip olabilir. Herhangi bir pencere öğesi özellikleri, çeşitli GUIX API çağrıları aracılığıyla açıkça yeniden tanımlanmamış olabilir.

### <a name="widget-creation"></a>Pencere Öğesi Oluşturma 

Bir pencere öğesi nesnesi başlatma sırasında veya uygulama iş parçacıklarının yürütülmesi sırasında herhangi bir zamanda oluşturulabilir. Bir uygulama tarafından oluşturulacak pencere öğesi nesnelerinin sayısına bir sınır yoktur. Ayrıca, hedef donanımınız için bellek sınırları dahilinde herhangi bir pencere öğesi için sahip ola bir üst sınır yoktur.

Her pencere öğesi türünün * gx_button_create _ **veya** _* gx_prompt_create **_gibi kendi oluşturma işlevi_ vardır. Bu işlevlerin ilk üç parametresi her zaman aynıdır; yani pencere öğesi denetim yapısına bir işaretçi, pencere öğesi adına bir dize işaretçisi ve pencere öğesi üst öğesi işaretçisi. Her create işlevi, ilgili pencere öğesi türünün gereksinimlerine bağlı olarak herhangi bir sayıda ek parametreye sahip olabilir.

### <a name="widget-control-block"></a>Pencere Öğesi Denetim Bloğu 

Her pencere öğesi nesnesinin özellikleri, denetim bloğunda **GX_WIDGET** ve **_gx_api.h içinde tanımlanır._** Bir pencere öğesi nesnesi için gereken bellek uygulama tarafından sağlanır ve bellekte herhangi bir yerde yer alıyor olabilir. Ancak, en yaygın olarak pencere öğesi nesne denetimi bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı oluşturur. GUIX Studio kullanıyorsanız, pencere öğesi denetim bloklarınızı Studio tarafından oluşturulan belirtimler dosyanız içinde statik olarak ayırabilirsiniz veya bunlar uygulamanız tarafından dinamik olarak ayırabilirsiniz.

### <a name="dynamic-widget-control-block-allocation-and-de-allocation"></a>Dinamik Pencere Öğesi Denetimi Blok Ayırma ve Ayırmayı Geri Ayırma 

Dinamik denetim bloğu ayırma kullanıyorsanız, GUIX'in pencere öğesi denetim bloklarınız için gereken belleği ayırmak ve serbest kaldırmak için kullanabileceği iki işlev tanımlamanız gerekir. Bellek yönetimi işlevleriniz, gx_system_memory_allocator_set API işlevi aracılığıyla GUIX ***sistem bileşenine*** geçirildi. Bu işlev GUIX'e iki işlev işaretçisi geçmenizi sağlar: birincisi bellek ayırma işlevinin işaretçisi, ikincisi ise bellek boş işlevinin işaretçisi. Çoğu zaman bu işlevleri ThreadX byte havuzlarını kullanarak uygulayabilirsiniz, ancak GUIX tasarımı, dinamik bellek yönetimini tercih edilen şekilde uygulamana olanak sağlar.

Dinamik pencere öğesi ayırma, Studio pencere öğesi özellikleri alanında "dinamik olarak ayrılmış" seçeneğini belirtirseniz, en çok Studio tarafından oluşturulan uygulama belirtimleri dosyanız içinde kullanılır. Ancak, dinamik denetim bloğu ayırmayı uygulama içinde de kullanabilirsiniz. Uygulamanız içinde dinamik denetim bloğu ayırmayı kullanıyorsanız, pencere öğesi denetim bloğu ayırmak için ***gx_widget_allocate** _ API işlevini çağırmanız gerekir. Ardından, pencere öğesini oluşturdukta, pencere öğesi oluşturma işlevine _ *GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED** stil bayrağını (diğer gerekli stil bayraklarıyla birlikte) iletirsiniz. Bu bayrak, pencere öğesi durum alanında pencere öğesi dinamik olarak ayrılmış olarak işaretlemek için kullanılır. Pencere öğesi daha sonra gx_widget_delete **** kullanılarak silindiğinde ve silindiğinde GUIX bu durum alanını kontrol eder ve bellek sızıntısı olmadığının ortaya çıktısını almak için bellek ayrımcı işlevinizi otomatik olarak çağıracaktır.

> [!IMPORTANT]
> Bellek kaybını önlemek için dinamik olarak ayrılmış bir denetim bloğu kullanılarak **oluşturulan bir pencere GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED** bayrağıyla oluşturularak.

### <a name="types"></a>Türler

GUIX, zengin ve tam işlevsel bir yerleşik pencere öğesi kümesi sağlar. Daha önce belirtildiği gibi, tüm özel pencere öğeleri temel pencere öğesinden türetiliyor. GUIX'te yerleşik pencere öğelerinin listesi aşağıdadır:

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

Pencere öğesi stilleri, kenarlık özellikleri (yükseltilmiş, ince, kalın veya hiç boarder) gibi özelliklerin yanı sıra daha önce listelenmiş belirli pencere öğesi türlerine yönelik özelliklerden oluşur. Pencere öğesi stili bayrakları, herhangi bir pencere öğesi görünümünü değiştirmek için en basit yöntemi sağlar.
İlk pencere öğesi stili her zaman pencere öğesi türüne özgü create işlevine geçirilen bir parametredir.

### <a name="colors"></a>Renkler 

Pencere öğeleri, sistem renk tablosunda tanımlanan renkleri kullanarak kendilerini çizer.
Renk kimlikleri tuval arka planı, varsayılan pencere öğesi dolgu rengi, düğme dolgu rengi, metin pencere öğesi dolgu rengi, pencere dolgu rengi ve diğer birkaç varsayılan renk değeri için tanımlanır. Ayrıca, **GX_WINDOW** pencere istemcisi doldurulurken bit eşlem veya duvar kağıdı görüntülemeyi destekler.

Varsayılan renk düzenini değiştirmenin en basit yöntemi GUIX Studio'yu kullanmak ve gereksinimlerinizi karşılayacak bir renk düzeni oluşturmak veya tanımlamaktır.
Renk düzeninizi el ile tanımlamak için farklı değerlerden GX_COLOR api işlevini gx_system_color_table_set de tanımlayabilirsiniz.

### <a name="event-notification"></a>Olay Bildirimi 

GUIX olayları, kullanıcı girişi ve iç sistem durumu değişiklikleri pencere öğelerine bildirmeye yönelik belirli bir eylemi ve bildirimleri gerçekleştirmek üzere bir veya daha fazla pencere öğesine yapılan isteklerdir. Örneğin, bir pencere öğesi odağında, **GX_EVENT_FOCUS_GAINED** ***API*** hizmeti aracılığıyla pencere gx_system_event_send gönderilir.

Olaylar GUIX olay kuyruğu üzerinden geçirildiğini ve her olayın veri yapısının GX_EVENT **olduğunu.** GX_EVENT  veri yapısı ***gx_api.h*** içinde tanımlanır, ancak yapının en önemli alanları **gx_event_type**, **gx_event_sender**, **gx_event_target** ve **gx_event_payload' dır.**

Gx_event_type  alanı, belirli bir olay sınıfını tanımlamak için kullanılır. Olay türü, bunun bir olay mı yoksa GX_EVENT_PEN_DOWN **olay** mı **olduğunu** GX_EVENT_TIMER gösterir. Bu **gx_event_payload,** çeşitli veri alanlarının bir birliğidir ve her olay türü için geçerli değildir.
Diğer olay veri alanlarını incelemeden önce olay türü alanını kullanırsiniz.

Olay **gx_event_sender,** olay bir alt pencere öğesi bildirimi ise olayı oluşturan pencere öğesi kimliğini içerir.

Gx_event_target  alanı, kullanıcı tanımlı olayları belirli bir pencereye veya pencere öğesine yönlendirmek için kullanılabilir. Belirli bir pencereye olay göndermek için pencereye benzersiz bir Kimlik değeri (pozitif bir şekilde belirlenecek şekilde) vermeli ve olay 00.000.000'de pencere kimliği değerini **gx_event_target** gerekir. Hedef kimliği bilmiyorsanız veya olayın yalnızca giriş odağına sahip pencere öğesine yönlendir gx_event_target **emin** olun.

Son **olarak, gx_event_payload** alanı çeşitli veri türlerinin bir tarakıdır. Olay **GX_EVENT_PEN_DOWN** **GX_EVENT_PEN_UP** için, **gx_event_pointdata** alanı kalem konumunun x,y piksel koordinatı içerir. Zamanlayıcı olayları için **gx_event_timer_id** alanı süresi dolan zamanlayıcının kimliğini içerir. Diğer yük veri alanları diğer olay türleri için kullanılır. Önceden tanımlanmış olay türlerinin ve yük alanlarının tam listesi Ek [E - GUIX](appendix-e.md)Olay Açıklamaları içinde tanımlanır.

Uygulama ayrıca sabit değerden sonra sayısal olarak başlayan kendi özel olaylarını **GX_FIRST_APP_EVENT.** Bu sabitten sonra gelen tüm olay numaraları uygulamanın kullanımı için ayrılmıştır. Elbette, uygulamanın pencere öğesi olay işleyicisi bu tür uygulama olayları için işlemeye sahip olmalı.

### <a name="event-processing"></a>Olay İşleme 

her pencere öğesi için, her bir pencere öğesi için varsayılan bir pencere öğesi olay işleme işlevi vardır ve ***gx_<türü>_event_process.*** Çoğu durumda, uygulamanın herhangi bir pencere öğesinde olay işleme konusunda endişelenmesi gerek değildir. Ancak, uygulamanın özel veya ek olay işleme gerektirdiği durumlarda, uygulama guiX API'si aracılığıyla varsayılan işleme işlevini kendi işleviyle geçersiz ***gx_widget_event_process_set.*** Bu işlev varsayılan olay işleme işlevini API'de belirtilen olay işlevi işleme işleviyle geçersiz kılar.

> [!IMPORTANT]
> Uygulama olay işleme işlevleri, varsayılan işlemenin yalnızca varsayılan çağrılarını doğrudan çağırarak (işlemeyi yinelemeden) ***gx_widget_event_process*** faydalanabilirsiniz.

Olay işleme özel olarak iç GUIX sistem iş parçacığı bağlamından çağrılır. Bu şekilde, olay işlemeyi işlemeye göre yığın gereksinimleri yalnızca GUIX iş parçacığı için geçerlidir.

### <a name="implementing-custom-event-processing-example"></a>Özel Olay İşleme Uygulama (örnek) 

GUIX sisteminde herhangi bir pencere öğesi veya pencere için kendi olay işleme işlevinizi sebilirsiniz. Kendi özel pencere öğesi türlerinizi oluşturuyorsanız, normalde pencere öğesi oluşturma işlevine özel olay işleyicinizi yükleyebilirsiniz. Yalnızca mevcut bir pencere öğesi veya pencerenin çalışmasını genişletıyor veya değiştirerek, pencere öğesi veya pencere oluşturulduktan sonra gx_widget_event_process_set API işlevini çağırabilirsiniz. Alt denetimleriniz tarafından oluşturulan olayları işleme amacıyla üst düzey pencerelerde (Ekranlar olarak da adlandırılan) neredeyse her zaman kendi olay işlemenizi sağlayacaktır. Bir ekranın alt denetimleri tarafından oluşturulan olayı işleme, GUIX uygulamanıza işlev eklemenin ana yolu olur.

Örneğin, "main_menu" adlı bir üst düzey ekran tanımlayabilirsiniz.
Bu ekran GUIX Studio kullanılarak tanımlanabilir veya bu ekranı uygulama kodunda oluşturabilirsiniz. Ekranı GUIX Studio'da tanımlarsanız, bu ekranın Studio özellikleri alanına olay işleyicinizin adını yazmanız gerekir ve Studio tarafından oluşturulan belirtimler kodu olay işleyicinizi otomatik olarak yüklenir. Bu durumda, özel olay işleyicisini main_menu_event_handler ***ve*** aşağıdaki gibi kodla kodlamız gerekir:

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

Yukarıdaki örnekte, **GX_EVENT_SHOW** (bir durum değişikliğini bildirmek için dahili olarak oluşturulan olaylar) gibi sistem olayları için, normal işlemenin gerçekleşmesini sağlarken uygulamanın bu olayları temel pencere öğesi olay işleme işlevine geçmesi gerektiğini fark etmek önemlidir. Uygulama daha sonra istediğiniz gibi ek mantık ekleyebilir. Uygulama tarafından işlen tüm olaylar (yukarıdaki varsayılan durum) temel olay işleme işlevine de geçir gerekir. Bu örnek, GX_WINDOW tabanlı bir üst **düzey ekran** için olduğu için varsayılan olay işleme işlevi gx_window_event_process.

### <a name="drawing-function"></a>Drawing İşlevi 

Tüm pencere öğesi çizimi olay işlemeden ayrı olarak gerçekleştirilir. Çizim genellikle CPU döngüleri açısından pahalı olduğundan bu daha verimlidir. Ertelenen bir çizim algoritması uygulanarak, tüm bekleyen olaylar ve ilişkili görüntüleme değişiklikleri herhangi bir çizim tamamlanmadan tamamlanır ve böylece boşa harcanan çizim ortadan kaldırılamaz. Olay işlemeye benzer şekilde, çoğu pencere öğesi için pencere öğesi türü gx_<adlı varsayılan bir pencere öğesi çizim ***işlevi vardır>_draw*** burada xxx pencere öğesi t type'tır. Çoğu durumda, uygulamanın herhangi bir pencere öğesi için çizim işlevi konusunda endişelenmesi gerek değildir. Ancak, uygulamanın özel veya ek çizim gerektirdiği durumlarda uygulama, guiX API'si aracılığıyla varsayılan çizim işlevini kendi gx_widget_draw_set. Bu işlev, uygulamanın herhangi bir pencere öğesi için kendi özelleştirilmiş çizim işlevini sağlamasını sağlar. Bu da uygulamanın yeni pencere öğesi türlerinin tamamını tanımlamasını sağlar.

> [!IMPORTANT]
> Uygulama çizimi işlevleri, yalnızca geçersiz kılınan çizim işlevinden çağırarak varsayılan çizimin avantajından (kodlamayı yinelemeden) faydalanabilir.

Pencere öğesi çizimi özel olarak iç GUIX sistem iş parçacığı bağlamından çağrılır. Bu şekilde, çizimi gerçekleştirmek için zamanlama ve yığın gereksinimleri yalnızca GUIX iş parçacığı için geçerlidir.

### <a name="implementing-custom-drawing-example"></a>Özel Çizim Uygulama (örnek) 

Herhangi bir pencere öğesi için çizim işlevine, uygulama denetim bloğuna üye olan dolaylı işlev GX_WIDGET başvurur. Pencere öğesinizi tanımlamak için GUIX Studio kullanıyorsanız, pencere öğesi özelliklerinin "Çizim İşlevi" parametresine işlevinizin adını yazarak kendi işlev işaretçinizi yükleyebilirsiniz ve Studio, pencere öğesi oluşturulduğunda işlev işaretçinizi sizin için yükler. Uygulama kodunda pencere öğesi oluşturursanız, pencere öğesi ***oluşturulduktan sonra gx_widget_draw_set*** çizim işlevinizi yüklemek için gx_widget_draw_set API işlevini kullansanız gerekir.

Bu örnekte, bir düğmenin görünümünü özelleştirmek istediğinizi varsayalım. Düğme, GX_TEXT_BUTTON gibi görünüyor ancak düğmeye basıldığında düğmenin sağ orta kısmına küçük bir yeşil "LED_ON" bit eşlemi ve düğmeye basıldığında küçük bir "LED_OFF" bit eşlemi çizacağız. Aşağıdaki çizimlere benzer bir düğme oluşturmak istiyorum.

![On için yeşil düğmenin ekran görüntüsü.](./media/guix/image4.jpg) özel düğme "on"

![Kapalı için kırmızı düğmenin ekran görüntüsü.](./media/guix/image5.jpg) özel düğme "kapalı"

Bu örnekte aşağıdakine benzer bir düğme çizim işlevi yazabilirsiniz.

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

## <a name="guix-drawing-context-component"></a>GUIX Çizim Bağlamı Bileşeni 

GuiX her tuval yenileme işlemini gerçekleştiriyor olduğu için çizim bağlamı çalışma zamanında dinamik olarak oluşturulur. Çizim bağlamı, geçerli çizim işlemlerini gerçekleştirmek için kullanılan tuvali, ekran sürücüsünü ve fırçayı bağlar.

Çizim bağlamı, GX_DRAW_CONTEXT **tanımlanır.**
Bu yapı, geçerli çizim işlemi için kırpmayı ve görünümü tanımlayan, geçerli tuvali tanımlayan ve kullanılan geçerli ekran sürücüsünü tanımlayan değişkenleri içerir. Bu **GX_DRAW_CONTEXT,** çizim için kullanılan fırçayı da tutar. Draw bağlam fırça, doğrudan özel çizim işlevlerinde birlikte çalışabilirsiniz üyesidir. Fırça yapısı aşağıdaki kodda gösterildiği gibi tanımlanır.

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

Bu **gx_brush_pixelmap** dikdörtgen ve çokgen dolguları için kullanmak üzere bir piksel haritası tanımlar. Bu üye, gx_brush_style **stili** dahil **GX_BRUSH_PIXELMAP** kullanılmaz.

Bu **gx_brush_font,** metin çizimi için kullanılan yazı tipini tanımlar.
Bu **gx_brush_line_pattern,** kesikli çizgiler için kullanılan deseni tanımlar.
Bu **gx_brush_style,** fırça özniteliklerini tam olarak tanımlamak için BIRLIKTE VEYA olan bir stil bayrakları kümesidir. Kullanılabilir fırça stili bayrakları aşağıdakileri içerir.

**GX_BRUSH_OUTLINE**  
**GX_BRUSH_SOLID_FILL**  
**GX_BRUSH_PIXELMAP_FILL**  
**GX_BRUSH_ALIAS**  
**GX_BRUSH_UNDERLINE**  
**GX_BRUSH_ROUND**

Bu **gx_brush_width,** çizgi çizimi için ile satırı veya ana hatlı şekil çizimi için ana hat genişliğini tanımlar.

Bu **gx_brush_line_color,** çizgi çizimi ve metin çizimi için ön plan rengini tanımlar.

Bu **gx_brush_fill_color,** şekil doldurma için kullanılan düz dolgu rengini tanımlar. GUIX bağlam bileşeni, etkin bağlamda geçerli fırçayı değiştirmeyi çok kolay hale etmek için tasarlanmış bir dizi API sağlar. Bu API'ler **gx_context_brush_define**, **gx_context_line_color_set**, **gx_context_fill_color_set**, **gx_context_font_set** ve diğerleridir.

Üst nesnenin çizim bağlamı, nesnelerin alt öğesi tarafından devralınır. Aslında üst çizim bağlamının bir kopyası, çizim işlevleri çağrıldığında alt nesneler tarafından devralınır. Alt öğe, üst çizimi etkilemeden bağlamı değiştirebilir, ancak istenirse üst öğeden fırça rengi ve stili gibi bilgileri devralabilir.

## <a name="guix-window-component"></a>GUIX Pencere Bileşeni 

GuiX'te tüm pencere işlemeden pencere bileşeni sorumludur. GUIX penceresi temelde bir veya daha fazla alt pencere öğesi içeren ayrı bir görüntüleme alanıdır. GUIX'te pencere aslında temel pencere öğesi nesnesinin özel bir biçimidir.

GUIX pencereleri, devralmanın tam desteğiyle nesne odaklı bir şekilde uygulanır. Bu, mümkün olan en küçük bellek ve işlem gereksinimleriyle sonuçlandıran ANSI C kullanılarak gereksinimlerini karşılar.

GUIX pencereleri öncelikli olarak yatay ve dikey kaydırma desteği ekleyerek GUIX pencere öğesi işlevselliğini genişleter. GUIX penceresi nesneleri, kaydırma çubuklarını otomatik olarak oluşturabilir ve görüntüler ve kaydırma çubuğu girişine yanıt verir. Taşınabilir pencereler, pencerenin kalem girişi olaylarına göre taşınmasına veya sürüklenmesine olanak sağlayan yerleşik olay işlemeye de sahiptir.
Son olarak GUIX penceresi, pencereyi Z sırasına kadar hareket ettirerek giriş odağı almaya yanıt verir.

GUIX penceresi, pencere kenarlıkları ve kaydırma çubuğu gibi istemci olmayan nesneler kullanılabilir alandan kaldırıldıktan sonra pencerenin iç kısmı olan istemci alanı kavramını sürdürür. İstemci alanı alt pencere öğeleri pencere istemci alanına kırpılırken kaydırma çubukları gibi istemci olmayan alt öğeleri istemci alanı dışına çizmesine izin verilir, ancak yine de pencere dış boyutlarına kırpılır.

Windows, alt öğenin özelliklerini üst öğeden devralınan bir üst-alt öğe olarak korunur. Alt pencerelerin kendi alt pencereleri olabilir ve yine üst pencereden çeşitli özellikleri devralır. Herhangi bir pencerenin özellikleri, çeşitli GUIX API çağrıları aracılığıyla açıkça yeniden tanımlandı olabilir.

### <a name="window-creation"></a>Pencere Oluşturma 

Başlatma sırasında veya uygulama iş parçacıklarının yürütülmesi sırasında herhangi bir zamanda bir pencere nesnesi oluşturulabilir. Bir uygulama tarafından oluşturulacak pencere nesnelerinin sayısına bir sınır yoktur. Ayrıca, herhangi bir pencerenin sahip olduğu çocuk sayısıyla ilgili bir sınır da yoktur.

### <a name="window-control-block"></a>Pencere Denetim Bloğu 

Her pencere nesnesinin özellikleri, denetim bloğu  GX_WINDOW bulunur ve **_gx_api.h içinde tanımlanır._** Bir pencere nesnesi için gereken bellek uygulama tarafından sağlanır ve bellekte herhangi bir yerde yer alıyor olabilir. Ancak, pencere nesnesi denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı yapmak en yaygındır.

### <a name="root-window"></a>Kök Pencere 

GUIX, her tuval için kök pencere olarak adlandırılan bir pencere gerektirir. Kök pencere kenarlıksızdır ve ekli olduğu tuvalle aynı boyutlara sahiptir. Öncelikli olarak tüm birinci düzey pencere öğeleri ve pencereler için kapsayıcı olarak kullanılır. Kök pencere genellikle ekran ve tuval oluşturulduktan kısa bir ***süre gx_window_root_create*** API işlevi aracılığıyla uygulama tarafından oluşturulur. Studio tarafından oluşturulan işlevi gx_studio_display_configure, kök pencerenin adresi bu işleve son parametre olarak geçirilen konumda döndürülebilirsiniz.

Kök pencere varsayılan olarak taşınamaz olur ve en basit durumda kök pencere tuvalin boyutudur. Kök pencere, görünen arka plan rengini değiştirmek veya arka plan duvar kağıdını görüntülemek için kök pencereye bir renk veya duvar kağıdı atarsınız.

Bir kök pencere taşınabilir durumda ise, tuvalin alt pencere gibi konumunu değiştirerek değil tuvalin kendisini hareket ettirerek taşır.
Bu özellik, GUIX kök penceresinin donanım uzaklığı yazmazları ile birden çok çerçeve arabelleği destekleyen donanımdan faydalanmasını sağlar.

### <a name="background"></a>Arka Plan 

Pencere arka planları düz renkler veya bit eşlem görüntüleridir. Sistem düzeyinde, ilk pencere kümesi için varsayılan değeri sağlayan varsayılan bir pencere arka planı vardır. Elbette, herhangi bir pencere arka planı GUIX API'si aracılığıyla değiştirilebilir.

Bir pencerenin düz renk arka planını değiştirmek için Gx_widget_fill_color_set ***API'sini*** kullanın. Pencereye arka plan duvar kağıdı atamak için Gx_window_wallpaper_set ***API'sini*** kullanın.

### <a name="scrolling"></a>Kaydırma 

GUIX, alt pencereyi görüntülemek için gereken alan pencerenin geçerli boyutunu (yatay ve/veya dikey) aştıklarında standart pencere kaydırmayı destekler. Kaydırmayı etkinleştirmek için uygulamanın istenen kaydırma çubuklarını oluşturması ve pencereye eklemesi gerekir.

GUIX pencere bileşeni, pencere istemci alanı boyutuna ve tüm alt pencere öğelerinin kapsamına göre varsayılan bir kaydırma uygulaması sağlar. Uygulamalar ayrıca belirli bir pencere için uygulama işlevini geçersiz karak kendi gx_window_scroll_info_get ***uygulamalarını*** ve yorumlarını da sağlar.

### <a name="event-notification"></a>Olay Bildirimi 

Varsayılan pencere olay işleme işlevi, birincil olarak GX_WIDGET ve boyutlandırma olaylarının işlenmesinde olay işlemeden farklıdır. GX_WINDOW kaydırma ve boyutlandırma olayları için tek tek işleyiciler sağladınız.

Uygulama ayrıca sabit değerden sonra sayısal olarak başlayan kendi özel olaylarını **GX_FIRST_APP_EVENT.** Bu sabitten sonra gelen tüm olay numaraları uygulamanın kullanımı için ayrılmıştır. Elbette, uygulamanın pencere olay işleyicisi bu tür uygulama olayları için işlemeye sahip olmalı.

### <a name="event-processing"></a>Olay İşleme 

Diğer tüm pencere öğesi türlerinde olduğu gibi, her pencere için gx_window_event_process adlı bir ***varsayılan pencere olay işleme işlevi vardır.*** Bu olay işleme işlevini genellikle kendi olay işleyiciniz ile, kendi oluştursanız pencerelerde geçersiz kılar. Olaylara bu şekilde yanıt verir ve pencere alt denetimleri tarafından oluşturulan olaylara göre eyleme geçebilirsiniz.

Olay işleyicisine ek olarak varsayılan ***olay*** işlemenin gerçekleşmesine izin vermek üzere bu olay işleyicisini geçersiz kılarsanız GUIX sistem olayları için temel gx_window_event_process işlevini çağırmayı unutmayın. Örneğin, GX_EVENT_SHOW olayı için özel  bir işleyici sağlarsanız ve bu olayı gx_window_event_process'a geçemezsiniz, pencereniz hiçbir zaman görünür olmaz.
Bir pencereye özel olay işleyicisi sağlamak için olay ***gx_widget_event_process_set*** adresini tanımlamak üzere gx_widget_event_process_set işlevini kullanın. Bu işlev varsayılan olay işleme işlevini API'de belirtilen olay işlevi işleme işleviyle geçersiz kılar.

> [!IMPORTANT]
> Uygulama olay işleme işlevleri, varsayılan işlemden yalnızca varsayılan değeri doğrudan çağırarak (işlemeyi yinelemeden) ***gx_window_event_process*** olabilir.

Olay işleme özel olarak iç GUIX sistem iş parçacığı bağlamından çağrılır. Bu şekilde, olay işlemeyi işlemeye göre yığın gereksinimleri yalnızca GUIX iş parçacığı için geçerlidir.

## <a name="guix-image-reader-component"></a>GUIX Görüntü Okuyucu Bileşeni 

Görüntü okuyucu bileşeni ham sıkıştırılmış görüntüleri GUIX piksel haritası biçiminde sıkıştırmak için yardımcı programlar ve API işlevleri sağlar. JPEG ve PNG biçimli ham görüntü verileri, gelecek sürümler için ayrılmış ek biçimlerle birlikte de desteklemektedir.

GUIX uygulamalarının büyük çoğunluğunda GUIX Görüntü Okuyucusu bileşeninin gerekli olmadığını unutmayın. Çoğu uygulama, JPEG ve PNG biçimli grafik varlıklarını GUIX uyumlu grafik varlıklarına dönüştürmek için GUIX Studio **GX_PIXELMAP** kullanır. GUIX görüntü okuyucusu bileşeni, ham grafik varlıkları yalnızca çalışma zamanında bilindiği zaman veya sistem depolama kısıtlamaları kaynakların farklı biçimde **depolanmasına engel GX_PIXELMAP** kullanılır. JPEG ve PNG biçimli görüntü  verileri genellikle GX_PIXELMAP biçimine göre daha küçük olur, ancak bu görüntü türlerinin sıkıştırmayı ve renk alanı dönüştürmesini dinamik olarak gerçekleştirmeyle ilişkili önemli bir çalışma zamanı yükü vardır.

Ham biçimLI JPEG veya PNG görüntüleri gx_canvas_pixelmap_draw API işlevine geçirilebiliyorsa GUIX, JPEG veya PNG verilerini dinamik olarak sıkıştırmasını ve çekmesini sağlar. Bunun çalışma zamanı çizim hızı üzerinde önemli bir olumsuz etkisi olduğunu ve donanım destekli JPEG veya PNG sıkıştırmayı destekleyen bir donanım hedefi kullanmadıkça HAM biçimli görüntü verilerini gx_canvas_pixelmap_draw işlevine geçirmenin öneril olmadığını unutmayın.

> [!IMPORTANT]
> Ham JPEG veya PNG biçimli görüntülerin gx_canvas_pixelmap_draw ÇOĞU hedef donanım için önemli bir çalışma zamanı yüküne neden olur.

Alternatif olarak, ham JPEG ve PNG verileri, Görüntü Okuyucusu bileşeni GX_PIXELMAP çalışma zamanında farklı bir biçime dönüştürülebiliyor.
Bu şekilde üretilen piksel haritaları, Studio tarafından üretilen ve kaynak dosyanız içinde yer alan piksel haritaları gibi kullanılabilir ve çizilir. Bu, görüntünün her çizilirken bu işlemleri gerçekleştirmek yerine, uygulamanın görüntü sıkıştırıcı, dithering ve renk alanı dönüştürme işlemini bir kez (genellikle program başlatma sırasında) gerçekleştirmenize olanak sağlar.

Görüntü Okuyucusu bileşen işlevleri şunlardır:

***gx_image_reader_create***  
***gx_image_reader_palette_set***  
***gx_image_reader_start***

## <a name="guix-animation-component"></a>GUIX Animasyon Bileşeni 

GUIX Animasyon bileşeni, ekran ve pencere öğesi geçiş otomasyonlarını otomatikleştirmek için kullanılan işlev ve hizmetler kümesidir. GUIX Animasyon bileşeni, herhangi bir pencere öğesi türünün soğutunu, soluk sildiğini ve hareket ya da slayt türü animasyonlarını destekler.

Soldurma türü animasyonlar, soğutan pencere öğeleri iç alfa değerinin **(GX_BRUSH_ALPHA_SUPPORT** etkinse) değişiklik göstererek veya herhangi bir pencere öğesi koleksiyonunu arka planla karıştırıldıkları zaman ayrı bir bellek tuvale çizerek destek olabilir. Birden çok donanım grafik katmanını destekleyen donanım hedefleri için, düz soğutma etkilerine yönelik destek, genellikle çok az çekirdek CPU bant genişliği gereken bu tuval karıştırma yaklaşımı kullanılarak en iyi şekilde gereksinimlerini karşılar. Birden çok grafik katmanını desteklemeen donanım hedefleri için GUIX fırça alfa değerini kullanarak karıştırma, 16 bpp ve daha yüksek renk derinliğinde çalıştırıldıklarında değerini destekler.

Bir animasyonun ayrı bir çizim tuvali kullanması gerekirse GUIX Animasyon bileşeni bu amaçla API gx_animation_canvas_define hizmetini sağlar. Diğer animasyon türleri ayrı bir tuval gerektirmez, ancak varsa bunu kullanır. Bu, birden çok donanım yüzeyi için temel donanım desteğinin mümkün olan en iyi şekilde kullanımını sağlar.

Animasyonu denetleyen değişkenler iki denetim bloğu tarafından tanımlanır. İlk olarak **GX_ANIMATION** denetleyicisini tanımlayan denetim bloğu. Animasyon denetleyicisi, tanımladığınız animasyon dizisini yürüten sürücü altyapısıdır. Tek bir animasyon denetleyicisi birçok farklı animasyon dizisini çalıştırmak için birçok kez yeniden kullanılabilir. Birden çok animasyon dizisini aynı anda çalıştırmanızı gerekirse, birden çok animasyon **GX_ANIMATION** oluşturabilirsiniz.

GUIX sistem bileşeni, **ve** animasyon gerektiğinde uygulama tarafından istenebilecek ve animasyon sırası tamamlandığında otomatik olarak sistem havuzuna döndürülen GX_ANIMATION denetim yapılarının yeniden kullanılabilir bir bloğu sağlar. Bu, uygulamayı uygulanan her animasyon için **GX_ANIMATION** statik olarak bir uygulama yapısı tanımlamadan serbest bırakmaktadır. Bu GX_ANIMATION havuzu  boyutu, varsayılan değer **6** olan GX_ANIMATION_POOL_SIZE sabiti tarafından tanımlanır ve bu da varsayılan olarak sistem havuzundan varsayılan olarak 6 eş zamanlı animasyon ayırabilirsiniz. Bu sabit elbette gx_user.h üst bilgi dosyasında yeniden tanımlanabilir, daha eş zamanlı animasyonlar gerekir. Bu **GX_ANIMATION_POOL_SIZE** sıfır olarak ayarlanırsa GUIX sistem bileşeni bir animasyon havuzu veya ilgili hizmetler sağlamaz.

Animasyon tanımlamak için kullanılan ikinci denetim bloğu veya yapısı, **GX_ANIMATION_INFO** yapısıdır. Bu yapı, belirli bir animasyon dizisini tanımlamak için kullanılır. Api hizmetini kullanarak bir animasyon dizisi başlatmak için bu bilgi yapısını animasyon gx_animation_start iletirsiniz. Aşağıdaki **GX_ANIMATION_INFO** aşağıdaki alanları içerir:

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

Bu **gx_animation_target** animasyon denetleyicisinin üzerinde davranacak hedef pencere öğesi tanımlar.

Bu **gx_animation_parent,** animasyon dizisi tamamlandığında hedef pencere öğesi ekli olacak üst pencere öğesi (varsa) tanımlar. Bu gx_animation_parent, animasyon tamamlandığında oluşturulan GX_ANIMATION_COMPLETE olay da alıcıdır.

Bu **gx_animation_screen_list,** kalem girişi odaklı ekran slayt animasyonları için bir pencere öğesi listesi tanımlar. Widge listesi, GX_NULL işaretçisi ile sonlandırılmalı ve listede yer alan her pencere öğesi, gx_animation_parent.

Bu **gx_animation_style** gerçekleştirilecek animasyon türünü ve ilişkili seçenekleri tanımlayan bir bit maskesidir. Animasyon stili bayrakları aşağıdakileri içerir.

| Animasyon &nbsp; Stili &nbsp; Bayrağı | Açıklama |
| --- | --- |
| GX_ANIMATION_TRANSLATE | Slayt veya soldurma türü animasyonu ister. |
| GX_ANIMATION_SCREEN_DRAG | Kalem girişi odaklı ekran sürükleme animasyonu isteği. |

Aşağıdaki bayraklar, farklı tür **animasyonlarıyla SCREEN_DRAG** kullanılabilir.

| Ekran &nbsp; Sürükleme &nbsp; Bayrakları | Açıklama |
| --- | --- |
| GX_ANIMATION_WRAP | Ekran listesinin baştan sona kaydırarak başlaması gerekir. |
| GX_ANIMATION_HORIZONTAL | Yatay yönde izin verilen ekran sürükleme.  |
| GX_ANIMATION_VERTICAL | Dikey yönde izin verilen ekran sürükleme. |

Aşağıdaki bayrak, çevrilmiş animasyonlarla birlikte kullanılabilir.

| Animasyon &nbsp; Bayraklarını &nbsp; Çevirme | Açıklama |
| --- | --- |
| GX_ANIMATION_DETACH | Animasyon tamamlandığında animasyon hedefini animasyon üst öğesinden ayır. Hedef dinamik olarak ayrılmış ve GUIX Studio tarafından oluşturulan otomatik olay işleme tarafından oluşturulmuşsa, hedef ayrılmış durumdan sonra silinir. |
| GX_ANIMATION_TRANSLATE | Animasyon türleri zamanlayıcı odaklı animasyonlardır. Uygulama, hedef pencere öğesi için başlangıç ve bitiş konumu ile başlangıç ve bitiş alfa değerini tanımlar ve animasyon yöneticisi animasyonu yürütmeye yönelik itici güç olarak görev yapacak bir zamanlayıcı oluşturur.
| GX_ANIMATION_SCREEN_DRAG | Bu animasyon türünün **kalem** girişi olayları tarafından yönlendirilmli olduğu TRANSLATE animasyonlarından farklıdır. Bu animasyon türü, kullanıcı giriş dokunmatik ekranında bir kalem veya kalem sürüklerken hedef pencere öğesi çekmesi için dokunmatik ekran girişiyle birlikte izler. Bu animasyon türünü kullanmak için, uygulamanın bu animasyonu etkinleştirmek için **_gx_animation_drag_enable_** API'sini çağıran bir api olması gerekir. |

Gx_animation_id  değeri, event.gx_event_sender olayın GX_ANIMATION_COMPLETE **geçirebilirsiniz.** Bu değer, birkaç alt animasyondan hangilerinin tamamlanma bildiriyor olduğunu belirlemek için animasyon üst öğesi tarafından kullanılır. Bu değer 0 olabilir ve kimlik değeri 0 olan  bir animasyon hiçbir zaman ANIMATION_COMPLETE oluşturmaz.

Bu **gx_animation_start_delay,** animasyonu yürütmeden önce _ çağrılmadan önce çağrılmak istendikten sonra gx_animation_start süreölçer işaretlerinin sayısını belirten bir GUIX ***değerdir. _gx_animation_start çağrısının ardından animasyonu hemen başlatmak için değer 0*_gx_animation_start._**

Bu **gx_animation_frame_interval,** animasyon dizisinin her karesi arasında gecikmeye neden olacak GUIX zamanlayıcısı saat işaretlerinin sayısını (temel işletim sistemi onay oranının katları) tanımlar. En düşük değer 1'tir.

Bu **gx_animation_start_position,** çeviri animasyonları için hedef pencere öğesi için sol üst başlangıç noktasını tanımlar.

Bu **gx_animation_end_position,** çeviri türü animasyonları için hedef pencere öğesi için sol üst uç konumunu tanımlar.

Bu **gx_animation_start_alpha,** çeviri türü animasyonları için başlangıç tuval alfa değerini tanımlar.

Bu **gx_animation_end_alpha,** çeviri türü animasyonları için son tuval alfa değerini tanımlar.

Gx_animation_steps  alanı, denetleyicinin çeviri animasyonları için kaç adım veya kare yürütmesi gerektiğini tanımlar. Daha fazla sayıda adım daha düzgün bir slayt ve/veya soldurma görünümü üretir, ancak daha fazla sistem bant genişliği gerektirir.

Uygulamanıza animasyon etkileri uygulamak için öncelikle gx_animation_create ***çağırarak*** animasyon denetleyicinizi başlatmanız gerekir. Animasyonun ikincil tuvali kullanacaksa bu tuvali başlatmak için gx_animation_canvas_define. Ardından, gerçekleştirilecek belirli **GX_ANIMATION_INFO** türünü ve diğer animasyon parametrelerini tanımlamak için uygulama yapısını başlatmanız gerekir. Son olarak, gx_animation_start dizisini tetiklemek için bu çağrıyı kullanın.

Animasyon denetleyicisi bir animasyon dizisini tamamlayan  GX_ANIMATION_COMPLETE pencere öğesine bir olay gönderir ve animasyon tuvali için istenen temizleme işleminin o anda yapılmasına olanak sağlar.

## <a name="guix-utility-component"></a>GUIX Yardımcı Programı Bileşeni 

Yardımcı program bileşeni GUIX'te tüm yaygın yardımcı program işlevlerden sorumludur. Bunlar yararlı yardımcı programlar olan ve uygulamanın herhangi bir yerinden veya iç GUIX kodundan çağrılabilir yaygın işlevlerdir. Yardımcı program bileşeni işlevleri aşağıdakileri içerir.

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
