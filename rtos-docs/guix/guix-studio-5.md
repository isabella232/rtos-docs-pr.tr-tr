---
title: GUIX Studio Ekran Tasarımcısı
description: Uygulama ekranları tasarlamak GUIX Studio'nun birincil amacıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d7a4ffca7d49a82b75ed756fc360a2f543faa8a9fe9d31e5a5ace39087c96568
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785790"
---
# <a name="chapter-5-guix-studio-screen-designer"></a>Bölüm 5: GUIX Studio Ekran Tasarımcısı

Uygulama ekranları tasarlamak GUIX Studio'nun birincil amacıdır. Ekran tasarımı, daha önce Bölüm 3'te açıklanan tüm çeşitli görünümler aracılığıyla lanmıştır. Ancak, GUIX Studio'daki ekran tasarımının ana ***öğesi,*** tüm ekran öğelerinin görsel olarak ve katıştırılmış hedef ekranda tam olarak aynı şekilde gösterildiği Hedef Görünüm'leridir. Bu ekran öğeleri basit fare ve düğme işlemleri aracılığıyla seçilebilir, taşınabilir, yeniden boyutlandırılabilir vb. Ayrıca, seçilen nesnelerde hizalama ve Z düzeni düğme işlemleri kullanılabilir. Aşağıdaki alt bölümlerde GUIX Studio ekran tasarımının çeşitli özellikleri açıklanmaktadır. 

## <a name="creatingconfiguring-projects"></a>Projeleri Oluşturma/Yapılandırma

GUIX Studio'da proje oluşturmak oldukça kolaydır. * Yeni Project _ düğmesini **veya** yeni Project _*_menü Project._*_ Ardından GUIX Studio *_,_* _ Yapılandırma Project * iletişim kutusunu sunar. Bu iletişim kutusunda temel görüntü ayarlarının yanı sıra GUIX Studio tarafından oluşturulan kodun yerini belirleme yol bilgileri belirtilir.

Yeni bir proje oluşturulduğunda projeyi yapılandır iletişim kutusu görüntülenir. Burası geliştiricinin hedefte kullanılabilen donanım ekranlarının sayısını ve her bir ekranın özelliklerini belirtir. Özellikler, ekranın mantıksal adını, x/y çözünürlüğünü, renk derinliğini ve biçimini ve diğer görüntüleme özelliklerini içerir. GUIX Studio aynı projede birden çok ekran destekler. Ek ekranlar **gerekirse*** Ekran Sayısı _ alanı, katıştırılmış cihaza eklenmiş olan ekran sayısıyla eş değer olarak değiştir gerekir. Bir projede en fazla 4 görüntüleme sayısıdır. _ *_Şekil 21_** Uygulama yapılandırma iletişim Project gösterir.

Projeyi ve/veya görüntüleme ayarlarını değiştirme, ***Yapılandır, Project/Görüntüle** _ menü seçeneğiyle ya da projeyi veya ekranı seçerek, sağ tıklar ve Yapılandır, tamamla/Görüntüle'yi _*_seçerek Project ekleyebilirsiniz._*_ Her iki durumda da, proje *_ayarlarında Project_* veya görüntülerde değişiklikleri kolaylaştırmak için _ Yapılandırma Project * iletişim kutusu gösterilir.

![Yapılandırma Yapılandırma iletişim kutusunun Project görüntüsü.](./media/guix-studio/config_project.png)

**Şekil 21**

Dizinler grubu, Studio tarafından üretilen C kaynağı ve üst bilgi dosyaları için varsayılan çıkış dizinlerini belirtebilirsiniz. Bu dizinler, projelerin bir bilgisayardan diğerine veya bir dosya sisteminden diğerine taşınmayı kolaylaştıracak şekilde proje konumuyla ilgili olarak normalde kaydedilir.

Ek Üst Bilgiler alanı, özel üst bilgi dosyalarını belirtebilirsiniz. Birden fazla üst bilgi dosyası gerekirse, listeyi sınırlandırma için noktalı virgül kullanın.

Studio "Uygulama Oluştur" veya "Kaynakları Oluştur" komutlarını çağırarak bu kaynak dosyalarının yazıldığı varsayılan dizinlerdir. Elbette, Çıkış Dizini iletişim kutusuna yeni konumlar girerek istediğiniz zaman bu dizin konumlarını geçersiz kılabilirsiniz.

## <a name="selecting-widgets"></a>Pencere Öğelerini Seçme

Pencere öğeleri seçerek ***** Görünüm _ pencere öğesi ağacında Project pencere öğesine tıklar veya Hedef Görünüm alanında görünen pencere _*_öğesine tıklar._*_ Tek bir pencere öğesi seçildiğinde, özellikleri Özellik Görünümü _*_alanında_*_ görüntülenir. _*_Şekil 22'de_*_ "_* düğmesi **"_öğesinin_ seçili olduğu pencere öğesi görüntülenir.

![Seçilen pencere öğesi ekran görüntüsü.](./media/guix-studio/select_button.png)

**Şekil 22**

## <a name="using-properties"></a>Özellikleri Kullanma

Daha önce belirtildiği gibi, seçilen pencere öğesinin özellikleri * Özellikler Görünümü **_ içinde sunulmuştur.** Tüm pencere öğeleri ortak bir özellik kümesine ve belirli pencere öğesi türüne özgü bazı özelliklere sahiptir. Örneğin, bir düğme pencere öğesi _ *_Ertelendi_** özelliğine sahipken pencere pencere öğesi yok. Aşağıdakiler ortak pencere öğesi özellikleri kümesidir:

| Özellik         | Anlamı                                                                               |
| ---------------- | ------------------------------------------------------------------------------------- |
| Pencere Öğesi Türü    | Başvuru için pencere öğesi türü                                                                               |
| Pencere Öğesi Adı      | Pencere öğesi oluşturma işlevine geçirilen ve oluşturulan kaynak dosyalarda değişken adlandırması için kullanılan pencere öğesi adı.               |
| Pencere Öğesi Kimliği        | Pencere öğesi kimliği. Bu kimlik değeri, alt pencere öğelerinden üst ekranlarına sinyaller oluşturmak için kullanılır.                            |
| Sol             | Pencere öğesi en sol koordinatı                                                                                                 |
| Üst              | Pencere öğesi en üst koordinatı                                                                                                  |
| Width            | Piksel cinsinden pencere öğesi genişliği                                                                                                      |
| Height           | Piksel cinsinden pencere öğesi yüksekliği                                                                                                     |
| Kenarlık           | Pencere öğesi kenarlığı türü                                                                                                          |
| Geçirgen      | Pencere öğesi kısmen saydamsa denetlenir                                                                       |
| Seçili Çizim    | Pencere öğesi başlangıçta seçili durumda kendisini çizecekse denetlenir.                                            |
| Etkinleştir           | Pencere öğesinin son kullanıcı tarafından seçilep seçilenebilmelidir veya tıklanabilmelidir.                                                    |
| Odağı Kabul Eder    | Pencere öğesi odağı kabul ediyorsa denetlenir.                                                                                 |
| Çalışma Zamanı Ayırma | Pencere öğesi denetim bloğu dinamik olarak ayrılırsa denetlenir.                                                 |
| Normal Dolgu      | Normal dolgu rengi kaynak kimliği                                                                                                  |
| Seçilen Dolgu    | Seçilen dolgu rengi kaynak kimliği                                                                                                |
| Draw İşlevi    | Kullanıcı tanımlı özel çizim işlevi Adı. Bu alan boşsa, bu pencere öğesi türü için standart çizim işlevi kullanılır. |
| Event İşlevi   | Kullanıcı tanımlı özel olay işleme işlevi adı. Boşsa, bu pencere öğesi türü için standart olay işleme kullanılır.          |

***Şekil 23'te*** basit bir pencere pencere öğesi özellikleri gösterilir.

![Basit bir pencere pencere öğesi özelliklerinin ekran görüntüsü.](./media/guix-studio/image57.jpg)

**Şekil 23**

Birçok pencere öğesi türünün her pencere öğesi türüne özgü ek özellikleri vardır.

Örneğin yukarıdaki Şekil 23'te Pencere pencere öğesi türü duvar kağıdı piksel haritası kimliğini ve duvar kağıdının orta mı yoksa kutucuklu mu olacağını belirten bir stil ayarını destekler.

Metin pencere öğeleri, metin hizalama stilleri ve yazı tipi belirtimi ile birlikte bir dize kimliği alanını destekler. Her pencere öğesi türünün açıklamasını ve kullanılabilir stilleri ve Bu pencere öğesi türü için işlev parametreleri oluştur'ları okuduğuktan sonra, ek pencere öğesi özellikleri normalde çok sezgiseldir.

## <a name="manipulating-widgets"></a>Pencere Öğelerinin Yönlendirerek

Bir pencere öğesi işlemek için önce seçili olması gerekir. Bu, * Hedef Görünüm _ içinde doğrudan pencere öğesinin üzerine tıklayarak veya **_** Görünüm * pencere öğesi ağacında *_Project seçerek_* yapılır. Seçildikten sonra pencere öğesi kesikli bir ana hat içerir. Bu durumda, pencere öğesine tıklar ve üst öğesinde istenen konuma sürükleyerek taşıyabilir. Pencere öğesi üst düzey bir pencere öğesi ise, pencere öğesi sürüklenerek pencere öğesi hedef görüntüde pencere öğesi ilk konumunu etkin bir şekilde ayarlanır. Elbette GUIX API'sini kullanarak herhangi bir pencere öğesi her zaman taşınabilir veya yeniden boyutlandırılabilir.

Pencere öğesi yüksekliğini yeniden boyutlandırmak için fareyi pencere öğesi üst kenarına getirin ve fare işaretçisinin yukarı aşağı oka değişmesini bekleyin. Bu noktada, farenin sağ düğmesi hareket ederken pencere öğesi yüksekliği yalnızca fareyi hareket ettirerek değiştirilebilir. Farenin genişliği, fare işaretçisi pencere öğesinde sol kenarına konumlara göre benzer şekilde yeniden boyutlandırılabilir. ***Şekil 24** _ üstpencerenin sol/üst alanına taşınan "_* düğme **" pencere öğesini yeniden boyutlandırır ve gösterir.

![Düğme pencere öğesi ekran görüntüsü.](./media/guix-studio/resize_button.png)

**Şekil 24**

## <a name="manipulating-multiple-widgets"></a>Birden çok pencere öğesini düzenleme

Birden çok pencere öğesi seçilmesi, ***CTRL*** tuşunu basılı tutarken hedef görünümde birden çok pencere öğesine tıklanarak gerçekleştirilir. Bunu yapmak, her bir pencere öğesinin etrafında kesik çizgili bir anahatlarla seçili olduğunu gösterir. Birden çok pencere öğesi seçerken seçim grubundaki her bir pencere öğesinin aynı üst öğenin alt öğesi olması gerektiğini unutmayın.

Birden çok pencere öğesi seçildikten sonra, seçilen Pencere öğelerinin içine tıklanarak ve fareyi sağ fare düğmesi aşağı doğru hareket ettirilerek aynı anda taşınmış olabilir. Ayrıca, ***araç çubuğu** _ üzerindeki hizalama düğmeleri Seçilen pencere öğelerinin grubunu hizalamak için kullanılabilir. _*_Şekil 25_*_ ' i "_*_Button_*_" ve "_*_New Button_*_" seçili pencere öğelerinin her ikisini de gösterir ve _*_Şekil 26_*_ , bu pencere öğeleri seçiliyken _ *_ALIGN-Left_** düğme seçiminin sonucunu gösterir.

![Düğme ve yeni düğme pencere öğeleri seçiliyken ekran görüntüsü](./media/guix-studio/multiple_select.png)

**Şekil 25**

![Align-Left düğmesi seçiminin sonucunun ekran görüntüsü.](./media/guix-studio/align_left.png)

**Şekil 26**

## <a name="cutcopypaste-operations"></a>Kesme/kopyalama/yapıştırma Işlemleri

***Target View** _ içindeki seçili bir pencere öğesi kesilebilir, kopyalanabilir ve standart biçimde yapıştırılabiliriz. Pencere öğeleri ve ekranlar bir proje içinde kopyalanabilir veya bir projeden kopyalanıp diğerine yapıştırılamaz. _*_Araç çubuğunda_*_ kes, Kopyala ve Yapıştır düğmeleri vardır. Ayrıca, Düzenle menü seçeneğinde aynı seçenekler de vardır. Pencere öğesi yapıştırırken, yeni pencere öğesi yapıştırmadan önce üst pencere öğesinin seçilmesi gerektiğini unutmayın. _*_Şekil 27_*_ , "_ *_Button_* *" pencere öğesinin seçilmesi, kopyalanmasını ve kopyanın aynı pencerede yapıştırılması sonucunu gösterir.

![Kes/kopyala/yapıştır işlemlerinin ekran görüntüsü.](./media/guix-studio/copy_paste_button.png)

**Şekil 27**

Tek bir projede çalışırken, kopyalanmış pencere öğesi (ler) için gerekli olabilecek kaynaklar her zaman mevcut olduğundan, bir proje içinde kopyalama/yapıştırma işlemi genellikle basittir. Ancak, projeden bir pencere öğesi kopyalarsanız ve bu pencere öğesini proje B 'ye yapıştırırsanız, kaynak bağımlılıklarıyla ilgili bazı sorunlar ortaya çıkabilir.

Studio 'daki pencere öğelerini kopyaladığınızda, Studio uygulaması kopyalanmış pencere öğeleri için gereken kaynakların bir listesini yapar ve Windows panosuna kopyalanmış olan XML biçiminde taşınabilir bir kaynak bağımlılığı tablosu oluşturur ve bu, gerçek kopyalanmış pencere öğesi bilgileri ile birlikte kopyalanır. Pencere öğeleri farklı bir projeye yapıştırdığınızda, önce bu kaynak bağımlılığı listesini inceler ve gerekli kaynakları henüz yoksa açık projeye ekler. Studio, kaynak KIMLIĞI adlarına göre eşleşen kaynakları tanımlar ve dize kaynakları için de dize içeriğini karşılaştırır. Eşleşen kaynaklar bulunursa, yeni projedeki kaynakları düzgün şekilde kullanmak için Studio, yapıştırılan Pencere öğelerinin kaynak kimliklerini güncelleştirir. Kaynaklar bulunamazsa, bunlar eklenir.

Studio, bir pencere öğesi yapıştırma işleminin bir parçası olarak projenize bir kaynak eklediğinde, yazı tipi ve pixelmap kaynakları söz konusu olduğunda Studio gerçekten kaynağa bir bağlantı ekliyor. Bu bağlantı, kaynak projeden oluşturulur ve bu kaynaklar, yapıştırdığınız projenin proje konumuna göre bulunamazsa uyarı iletileri alırsınız. Kaynak bağlantıları projeye ne olursa olsun eklenir, ancak kaynak yükleme hatalarını ortadan kaldırmak için yazı tiplerini ve resim dosyalarını yeni proje ağacınızdaki doğru konumlara el ile kopyalamanız gerekebilir. Studio. ttf, .png veya .jpg dosyalarını bir konumdan diğerine kopyalamaz.

Bu şekilde herhangi bir problemi önlemenin kolay yolu, paylaşmak istediğiniz projeler arasında tutarlı bir dizin yapısı tutmaktır. Project A 'dan Project B 'e kolayca taşımak istiyorsanız, her iki proje klasörü için de tutarlı bir alt dizinde bulunan grafik görüntülerini ve yazı tiplerini saklayın.

## <a name="changing-z-order"></a>Z düzenini değiştirme

Pencere öğeleri, diğer pencere öğelerinin önüne veya arkasına kolayca taşınabilir. Bu, pencere öğesi seçilerek ve _*_araç çubuğundaki_*_***öne taşı** _ veya _*_Geri düğmelerine git_*_ seçilerek gerçekleştirilir. _ *_Şekil 28_** İkinci düğmenin geri taşınmasını gösterir.

![Düğme z düzeninin ekran görüntüsü.](./media/guix-studio/change_z_order.png)

**Şekil 28**

## <a name="assigning-colors-fonts-and-pixelmaps"></a>Renkler, yazı tipleri ve pixelmaps atama

Seçili bir pencere öğesi için Özellikler görünümünde renkler, yazı tipleri ve pixelmaps seçmeye ek olarak, pencere öğeleri için kaynak atamaya yönelik bir tam sürükleme ve bırakma yöntemi de desteklenir. Bu özelliği kullanmak için, kaynak görünümündeki bir yazı tipi rengi gibi bir kaynağa sağ tıklayıp kaynağı hedef görünümde istenen pencere öğesi üzerine sürükleyin. Sol fare düğmesini pencere öğesi üzerine bırakarak kaynağı bırakın.

Sürükleme ve bırakma yöntemi kullanılırken, renk kaynakları her zaman pencere öğesi normal arka plan rengine atanır. Seçilen renk veya seçili metin rengi gibi diğer renkler Özellikler Görünümü kullanılarak atanmalıdır.

Benzer şekilde, pixelmap kaynakları, pixelmap görüntüsünü destekleyen bir pencere öğesinin "normal" veya "Fill" pixelmap alanına atanır. Birden çok pixelmaps destekleyen bir pencere öğesine başka alanlar atamak için Özellikler görünümünü kullanmanız gerekir.

## <a name="using-templates"></a>Şablonları kullanma

Studio 'da tasarlamanızı sağlayan herhangi bir ekran veya alt pencere öğesi koleksiyonu, yeni ekranlar ve yeni alt denetimler için şablon olarak kullanılabilir. Bir şablonu, normal kullanım örneği veya başka bir pencere öğesi türü olan pencere türü pencere öğesi üzerinde temel alabilirsiniz. Şablon kullanmak, bir pencere öğesini kopyalamaya ve yapıştırmaya benzer, ancak bir şablondan türetilmiş her şey, temel aldığı şablon değiştirildiğinde otomatik olarak değiştirilir. Türetilmiş bir ekranla veya şablonun devralınmış örneğiyle çalışırken şablon pencere öğesi özelliklerini değiştirmenize izin verilmiyor. Bununla birlikte, şablon özelliklerini herhangi bir şekilde değiştirdiğinizde, şablona başvuran tüm örnekler bu şablondan türetildiklerinden otomatik olarak güncelleştirilir.

Yinelenen öğeler için şablon kullanmanın başka bir avantajı da, her kullanıldıkları zaman yinelenen öğeleri yeniden oluşturduysanız, Studio tarafından üretilen belirtim dosyasının boyut olarak daha küçük olmasını sağlayacaktır.

Bir ekran veya alt pencere öğesi koleksiyonunun şablon olarak kullanılacağını belirlemek için pencere öğesi özellikleri görünümünde "şablon" onay kutusunu açın. "Şablon" onay kutusunu açtığınızda, şablon pencere öğesi ***ekleme | Şablon*** çekme menüsü (ler).

Şablon kullanmanın bir örneği olarak, düğme çubuğu olarak kullanılan bir pencere tanımlayabilirsiniz. Bu pencere tek başına birkaç alt düğme içerebilir ve bu düğme çubuğu sık sık çeşitli ekranlarda kullanılır. Studio projenizde gerekli alt düğmeleri tutan ve bu pencereye "button_bar" adını veren küçük bir tek başına pencere tanımlayabilirsiniz. Sonra bu pencereyi seçin ve "şablon" özelliğini açın. Ardından, bu düğme çubuğunu eklemek istediğiniz bir ekran seçin. Ekle | Ekranınızdaki button_bar penceresinin bir örneğini eklemek için şablon | button_bar menü komutu. Düğme çubuğunun konumunu değiştirebileceğinizi, ancak çoğu özelliği değiştirmenize izin verilmeyeceğini unutmayın. Ancak, önceden tanımlanmış diğer bir Gux pencere öğesi türü gibi button_bar pencere öğesini (ve tüm alt öğeleri) kullanabilirsiniz. Button_bar değiştirmek için, değişikliklerinizi yapmak üzere button_bar şablonunu seçmeniz gerekir.

Tipik şablon kullanımının başka bir örneği de birçok benzer ekran içeren bir uygulamadır. Örneğin, uygulamanın tüm ortak bir başlık çubuğunu, Fill rengini, boyutunu, vb. paylaştığı 10 farklı ekranı olabilir. Bu durumda, başlık çubuğu alt pencere öğelerinizi içeren bir şablon ekranı tanımlayabilir ve ekran boyutunu, Fill rengini ve diğer özellikleri yapılandırabilirsiniz. Bu şablon ekranı tanımlandıktan sonra, bu şablondan 10 farklı ekranınızdan türetebilirsiniz. INSERT 'i kullandığınızda | Şablon | \<base_screen> menü komutu, ekranınız, şablon ekranınızın tüm alt pencere öğeleri ve ayarları ile başlatılır. Şablon ekranından türettiğiniz her ekran şablonun bir kopyası değildir ancak şablon ekranının gerçekten türetilmiş bir örneğidir. Daha sonra her bir türetilmiş ekranı, ek içeriğin gerekli olduğu her şeyi içerecek şekilde özelleştirebilirsiniz.

Oluşturulan belirtim dosyasının boyutunun kaydedilmesine ek olarak, şablonların kullanılması uygulama görünümünüzdeki değişikliklerin yönetimini kolaylaştırabilir. Yukarıdaki örnekte, 10 benzer ekranlarınızın arka plan rengini değiştirmeniz gerektiğini varsayalım. Her bir ekranı seçmek ve renk dolgusu ayarlarını değiştirmek zorunda olmak yerine, yalnızca temel şablonu seçmeniz ve onun doldur rengini değiştirmeniz yeterlidir ve bu değişiklik tüm türetilmiş ekranlarda anında yansıtılır.

Şablonlarla ilgili daha fazla yorum: olay işleme akışının korunduğundan emin olmanız gerekir, yani hem temel ekran için (ortak pencere öğesi olaylarını işlemek için) hem de türetilmiş bir ekran için bir olay işleyicisi sağlarsanız, türetilen ekran olay işleyicisi varsayılan durumda base_screen olay işleyicisini çağırmalıdır. Bu, temel ekran olay işleyicisinin bu şablon tabanından türetilmiş tüm ekranlarda ortak pencere öğeleri tarafından oluşturulan olayları işlemesini sağlar.

## <a name="record-and-playback-macro"></a>Kayıt ve kayıttan yürütme makrosu

Makro kaydı ve kayıttan yürütme işlevleri, tuş vuruşlarını ve fare olaylarını kaydetmenize ve oynatgetirmenize yardımcı olur.

Makro dosyasına kaydetme işlemi, ***makroyu kaydet** _ araç çubuğu düğmesine veya _*_Düzenle, Kaydet makrosunu_*_ seçen menü kullanılarak gerçekleştirilir. GUX Studio, makro dosyanız için yol adını belirtmenize olanak sağlayan _*_kayıt makrosu_*_ iletişim kutusunu gösterir. Bu seçimi yaptıktan sonra, kayda başlamak için _*_Kaydet_*_ düğmesine tıklayın. Kaydetmeyi bitirdikten sonra, _*_makro kayıt_*_ çubuğunu yeniden seçin veya _ *_Düzenle, makroyu Sonlandır * ' ı_* seçerek Makro kaydını sona erdirmek için açılan menüyü kullanın.

Makro dosyasını kayıttan yürütme işlemi _*_,_*_ ana açılan menü menüsünü kullanarak ***Kayıttan** yürütme makrosu _ araç çubuğu düğmesi seçilerek gerçekleştirilir. GUX Studio, daha önce kaydedilen makro dosyasını belirtmenizi sağlayan _ *_oynatma makrosu_** iletişim kutusunu gösterir.

Yazı tipi veya resim ekleme gibi giriş veya çıkış dosyalarını seçerek makroları kaydederken, dosya tarayıcısından seçmek için fareyi kullanmak yerine, klavyeyi kullanmak önemlidir. Makro kaydedicisi fare ve klavye olaylarını kaydettiği ve dosya tarayıcınız zaman içinde değişebileceğinden, dosyayı grafik olarak seçenden daha güvenilir bir dosya adı yazmak daha güvenilirdir.

## <a name="zooming-target-view"></a>Yakınlaştırma hedefi görünümü

Yakınlaştırma işlevi, hedef ekranın yakından bir görünümünü almanıza yardımcı olur.

* Yapılandır | ' da istediğiniz yakınlaştırma ayarını seçebilirsiniz.**Hedef görünüm | Yakınlaştır** _ menü seçeneği. _ *_Araç çubuğunun_** yakınlaştırma/kapatma düğmeleri de vardır.

## <a name="gridsnap-settings"></a>kılavuz/yaslama Ayarlar

***grid ve snap Ayarlar** _ iletişim kutusu, grid ve snap için bazı ayarları ve seçenekleri içerir. _*_Şekil 29_*_ , menü _ _*_congiayarınızı yaparken kılavuz ve yapışma ayarı_*_ iletişim kutusunu gösterir.*_Hedef görünüm | Grid/Snap_** seçilidir.

![Grid ve Snap Ayarlar ekran görüntüsü.](./media/guix-studio/image63.jpg)

**Şekil 29**

Aç ***Kılavuzu göster** _ seçeneği, kılavuzu hedef ekranda görüntüleyecektir, ızgara _*_aralığı_*_ alanında ızgara artışı (piksel cinsinden) belirtebilirsiniz. _ *_Kılavuza yapış_** seçeneği bir pencere öğesini doğru konuma almanıza yardımcı olur. bu seçeneği etkinleştirmek etkin olacak şekilde yaslanır.

***Kılavuz ve yaslama*** seçeneği etkin olduğunda:

- Bir nesneyi hedef görünümde fareyle sürüklerseniz, nesne ızgara artışını taşır.
- Yeniden boyutlandırmak için bir nesnenin kenarını sürüklerseniz, sürüklediğiniz kenar kılavuz konumuna yaslanacak.
- Bir nesne seçer ve yukarı/aşağı/aşağı/sağ tuşlarını kullanıyorsanız, seçilen pencere öğesi yapışma artışına göre hareket edebilir, yaslama artışını (piksel cinsinden) ***yaslama boşluğu*** alanında belirtebilirsiniz.
