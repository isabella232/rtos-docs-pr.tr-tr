---
title: Bölüm 3 - GUIX'e İşlevsel Genel Bakış
description: Bu bölümde, yüksek performanslı GUIX kullanıcı arabirimi ürününe işlevsel bir genel bakış yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 37c1103d6b690350b6fa0794b9c719f31a112ff3babf88f125d3735f8ef935b6
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785275"
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

Geliştirme araçlarının çoğu, uygulama programı görüntüsünü beş temel alana böler: *yönerge*, *sabit*, *başlatılan veriler*, *başlatılmamış veriler* ve *guıdx iş parçacığı yığını*.  Aşağıdaki şekilde, bu bellek alanlarının olası bir düzeni gösterilmektedir:

![Bellek düzeni](./media/guix/user-guide/memory-area-example.png)

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

| Bileşenler  | Description  |
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

| Renk &nbsp; Biçimi       | Description                                                                                                   |
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

| Renk Kimliği | Description |
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
| GX_COLOR_ID_SELECTED_TEXT_FILL | Varsayılan seçilen metin dolgusu rengi |
| GX_COLOR_ID_READONLY_TEXT | Varsayılan salt okunur metin rengi |
| GX_COLOR_ID_READONLY_FILL | Varsayılan salt okunur metin dolgu rengi |
| GX_COLOR_ID_SCROLL_FILL |    Kaydırma çubuğu dolgu rengi |
| GX_COLOR_ID_SCROLL_BUTTON | Kaydırma çubuğu düğmesi dolgu rengi |
| GX_COLOR_ID_SHADOW | Varsayılan gölge renk |
| GX_COLOR_ID_SHINE | Varsayılan vurgulama rengi |
| GX_COLOR_ID_BUTTON_BORDER | Düğme pencere öğesi kenarlık rengi |
| GX_COLOR_ID_BUTTON_UPPER | Düğme pencere öğesi üst dolgu rengi |
| GX_COLOR_ID_BUTTON_LOWER | Düğme pencere öğesi alt dolgu rengi |
| GX_COLOR_ID_BUTTON_TEXT | Düğme pencere öğesi metin rengi |
| GX_COLOR_ID_TEXT_INPUT_TEXT | Metin girişi pencere öğesi metin rengi |
| GX_COLOR_ID_TEXT_INPUT_FILL | Metin girişi dolgu rengi |
| GX_COLOR_ID_SLIDER_TICK | Kaydırıcı onay işareti çizmek için kullanılan renk. |
| GX_COLOR_ID_SLIDER_GROOVE_BOTTOM | Kaydırıcı kaydırıcısını çizmek için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_OUTLINE | Iğne ana hatlarını çizmek için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_FILL | Kaydırıcı iğnesini doldurmak için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE1 | Iğne vurgusu çizmek için kullanılan renk |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE2 | Iğne gölgesi çizmek için kullanılan renk |

Bu renk kimliği değerleri, her bir görüntüye atanan renk tablosu tarafından tanımlandığı şekilde belirli bir renk değeriyle eşlenmiş olur. Bu varsayılanlar, api işlevi çağrılarak tek bir görüntü için ***grup gx_display_color_table_set*** değiştirilebilir. GUIX Studio kullanıyorsanız, uygulamanız gx_studio_display_configure işlevini çağıran görüntü ***rengi tablosu*** otomatik olarak başlatılır.

GUIX görüntüleme bileşeni, varsayılan yazı tipi tablosu da sağlar. Varsayılan yazı tipi tablosu, uygulama tarafından özel olarak belirtilmedidikçe her pencere öğesi türü tarafından kullanılan yazı tipini tanımlar. Önceden tanımlanmış görünen yazı tipi tablosu kimlikleri aşağıdaki değerleri içerir.

| Yazı Tipi &nbsp; Kimliği | Description |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------|
| GX_FONT_ID_DEFAULT | Belirli bir yazı tipi tanımlanmamışsa kullanılan varsayılan yazı tipi |
| GX_FONT_ID_BUTTON | Tüm metin düğmeleri için kullanılan varsayılan yazı tipi |
| GX_FONT_ID_TEXT_INPUT | Metin düzenleme alanları için kullanılan varsayılan yazı tipi |

Herhangi bir metin türü pencere öğesi tarafından kullanılan yazı tipi kimliği, metinle ilgili her pencere öğesi **türü gx_<widget_type>_font_set** API'si kullanılarak yeniden atanabilir. Tüm yazı tipi tablosu, api işlevi çağrılarak **gx_display_font_table_set** atanabilir.

### <a name="scrollbar-appearance"></a>Kaydırma Çubuğu Görünümü 

GUIX Görüntüsü ayrıca bu ekran için varsayılan kaydırma çubuğu görünüm ayarlarını da sürdürür. Bu ayarlar aşağıda tanımlanan **GX_SCROLLBAR_APPEARANCE** yapısı tarafından tanımlanır. GUIX Ekranı, dikey kaydırma çubukları için bir kaydırma çubuğu görünüm yapısı ve yatay kaydırma çubukları için ikinci bir yapı sağlar. Uygulama, herhangi bir görüntü için varsayılan kaydırma çubuğu  görünümünü, bir GX_SCROLLBAR_APPEARANCE başlatarak ve api işlevini ***gx_display_scroll_appearance_set.***

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
| GX_SCROLLBAR_APPEARANCE Yapısı Üyesi | Description |
| --- | --- |
| gx_scroll_width | Dikey kaydırma çubuğunun genişliği veya piksel cinsinden yatay kaydırma çubuğunun yüksekliği. |
| gx_scroll_thumb_width | Piksel cinsinden asansör ve bitiş düğmelerinin genişliği. |
| gx_scroll_thumb_travel_max | Kaydırma çubuğunun sonundan başparmak düğmesi seyahat noktası üst noktasına kaydırma. |
| gx_scroll_fill_pixelmap | Kaydırma arka planını doldurmak için kullanılan piksel haritası. |
| gx_scroll_thumb_pixelmap | Piksel haritası, kaydırma başparmak düğmesini çizmek için kullanılır. |
| gx_scroll_up_pixelmap | Yukarı kaydırma düğmesini çizmek için kullanılan Piksel Haritası. |
| gx_scroll_down_pixelmap | Piksel haritası, aşağı kaydırma düğmesini çizmek için kullanılır. |
| gx_scroll_fill_color | Kaydırma çubuğu arka planını doldurmak için kullanılan rengin renk kimliği. |
| gx_scroll_button_color | Kaydırma çubuğu parmak düğmesini doldurmak için kullanılan rengin renk kimliği. |

Uygulama, yazı tipleri, renk ve stiller için bu varsayılan ayarlara ek olarak, her pencere öğesi türü tarafından sağlanan API'yi kullanarak bir olayda büyük/küçük harfe göre parametrelerin herhangi birini de belirtebilir.

### <a name="skinning-and-themes"></a>Dış görünüm ve temalar

Dışlama, GUIX pencere öğelerinin ve pencere öğelerinin temel görünümünü kolayca değiştirmesini sağlar. Başka bir ifadeyle "dış görünüm" tek bir yerde değiştirerek ilişkili tüm pencere öğelerinin ve pencerelerin temel görünümünü değiştirir.

GUIX uygulamanıza yeniden görünüm oluşturma, GUIX Display kaynak tablolarına yeni bir renk, yazı tipi ve piksel haritası tablosu sağlarsınız. Tüm GUIX pencere öğeleri renklerine, bit eşlemlerine veya yazı tipine kaynak kimliğine göre başvurduklarından, yeni bir kaynak tablosu sağlamak otomatik olarak tüm GUIX pencere öğelerinin kendilerini istenen görüntüye çizerek yeni renklerinizi ve piksel haritalarınızı kullanmaya başlamasına neden olur.

Çekici bir görünüm sağlamak için birlikte çalışmak üzere tasarlanmış yeni yazı tipleri, renkler ve piksel haritaları kümesi tema olarak adlandırılan bir *dizi.* Tema, bir kaynak tablosu kümesi ve her bir kaynak tablosu boyutunu tanımlar. GUIX Studio uygulaması kullanılarak herhangi bir görüntü için herhangi bir sayıda tema tanımlanabilir. Başlangıç tema dizinini, oluşturulan görüntüye ilk temayı ***yük gx_studio_display_configure*** GUIX Studio tarafından oluşturulan işleve geçmelisiniz. Herhangi bir görüntü için etkin tema, herhangi bir zamanda işlevi ***gx_display_theme_install.***

### <a name="root-window"></a>Kök Pencere

Bir uygulama tarafından oluşturulan her görünür tuval için uygulamanın bu tuval için bir Kök Pencere de oluşturması gerekir. Bu özel pencere temelde tüm üst düzey uygulama pencereleri ve pencere öğeleri için kapsayıcı olarak kullanılır. Kök pencere tuval arka planını çizer ve kök pencere, GX_WINDOW sınıfından türetilene kadar duvar kağıdına da sahip olabilir.  Görüntü veya tuvalin arka plan rengini değiştirmek için, yalnızca bu tuvale eklenmiş kök pencerenin dolgu rengini değiştirebilirsiniz.

Görüntülerinizi yapılandırmak için ***gx_studio_display_configure*** ADLı GUIX Studio tarafından oluşturulan işlevi kullanırsanız, bu başlatma işlevinin bir parçası olarak her bir görüntü için tuval ve kök pencere oluşturulur.

### <a name="anti-aliasing"></a>Diğer AdDan Koruma 

Diğer AdDan Koruma, GUIX'te çizgileri, eğrileri ve yazı tiplerini düz hale etmek için kullanılan isteğe bağlı bir özelliktir. Diğer addan koruma yalnızca 16 bpp veya daha yüksek renk derinliği kullanan bir görüntü sürücüsüyle çalıştırıldıklarda değerleniyor.

Diğer adlara sahip çizgi çizimi, etkin fırçada **GX_BRUSH_ALIAS** flash ayarıyla etkinleştirilir. Bu, doğrudan çizilen çizgilerin yanı sıra çokgen veya dairenin kenarlığı olarak çizilen çizgiler için de geçerlidir.

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

Windows, alt öğelerin üst öğelerinden özellikler devraldığı bir üst-alt biçimde tutulur. Alt Windows 'un kendi alt pencereleri olabilir, bu da üst öğeden çeşitli özellikleri devralabilir. Herhangi bir pencerenin özellikleri, çeşitli GUıDX API çağrıları aracılığıyla açıkça yeniden tanımlanabilir.

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

| Animasyon &nbsp; Stili &nbsp; Bayrağı | Description |
| --- | --- |
| GX_ANIMATION_TRANSLATE | Slayt veya soldurma türü animasyonu ister. |
| GX_ANIMATION_SCREEN_DRAG | Kalem girişi odaklı ekran sürükleme animasyonu isteği. |

Aşağıdaki bayraklar, farklı tür **animasyonlarıyla SCREEN_DRAG** kullanılabilir.

| Ekran &nbsp; Sürükleme &nbsp; Bayrakları | Description |
| --- | --- |
| GX_ANIMATION_WRAP | Ekran listesinin baştan sona kaydırarak başlaması gerekir. |
| GX_ANIMATION_HORIZONTAL | Yatay yönde izin verilen ekran sürükleme.  |
| GX_ANIMATION_VERTICAL | Dikey yönde izin verilen ekran sürükleme. |

Aşağıdaki bayrak, çevrilmiş animasyonlarla birlikte kullanılabilir.

| Animasyon &nbsp; Bayraklarını &nbsp; Çevirme | Description |
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
