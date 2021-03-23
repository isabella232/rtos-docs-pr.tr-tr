---
title: GUX Studio ekran Tasarımcısı
description: Uygulama ekranları tasarlamak, GUıDX Studio 'nun birincil amacıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 318e68ab5ab7d841057d65565dfda263597d03e4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826332"
---
# <a name="chapter-5-guix-studio-screen-designer"></a>Bölüm 5: GUıDX Studio ekran Tasarımcısı

Uygulama ekranları tasarlamak, GUıDX Studio 'nun birincil amacıdır. Ekran tasarımı, Bölüm 3 ' te daha önce açıklanan çeşitli görünümler aracılığıyla gerçekleştirilir. Ancak, GUıDX Studio 'daki ekran tasarımının ana öğesi, tüm ekran öğelerinin görsel olarak görüntülendiği ve gömülü hedef ekranda göründükleri şekilde tam olarak gösterildiği ***hedef görünümlüdür***. Bu ekran öğeleri basit fare ve düğme işlemleri aracılığıyla seçilebilir, taşınabilir, yeniden boyutlandırılabilir, vb. olabilir. Ayrıca, hizalama ve Z düzeni düğme işlemleri seçili nesneler üzerinde kullanılabilir. Aşağıdaki alt bölümlerde, Gux Studio ekran tasarımının çeşitli özellikleri açıklanır. 

## <a name="creatingconfiguring-projects"></a>Projeleri oluşturma/yapılandırma

GUX Studio 'da proje oluşturma basittir. yalnızca ***Yeni proje** _ düğmesini veya menü seçimi _*_projesini, yeni projeyi_*_ seçin. Ardından, GUıDX Studio, _ *_projeyi Yapılandır_** iletişim kutusunu gösterir. Bu iletişim kutusunda, temel görüntü ayarlarının yanı sıra, GUıDX Studio tarafından oluşturulan kodun yerini almak için yol bilgileri belirtilir.

Yeni bir proje oluşturulduğunda, projeyi Yapılandır iletişim kutusu görüntülenir. Geliştirici, hedefte kullanılabilen donanım görüntüleme sayısını ve her bir görüntüleme özelliğini belirtir. Özellikler, ekran mantıksal adı, x/y çözünürlüğü, renk derinliği ve biçimi ve diğer görüntü özelliklerini içerir. GUX Studio aynı projede birden çok ekranları destekler. Ek ekranlar gerekliyse, ***ekran sayısı** _ alanının gömülü cihazdaki ekran sayısıyla eşleşecek şekilde değiştirilmesi gerekir. Bir projedeki en fazla ekran sayısı 4 ' dir. _ *_Şekil 21_** projeyi Yapılandır iletişim kutusunu gösterir.

Proje ve/veya görüntü ayarlarını değiştirmek, menü seçeneği ***yapılandırma, proje/görüntüleme** _ veya proje ya da görüntüleme, sağ tıklama ve _*_Yapılandır, proje/görüntü_*_ seçeneklerini belirleyerek gerçekleştirilir. Her iki durumda da, proje ayarları ve/veya görüntüleme değişikliklerini kolaylaştırmak için _ *_projeyi Yapılandır_** iletişim kutusu gösterilir.

![Projeyi Yapılandır iletişim kutusunun ekran görüntüsü.](./media/guix-studio/config_project.png)

**Şekil 21**

Dizinler grubu, Studio tarafından üretilen C kaynağı ve üstbilgi dosyaları için varsayılan çıkış dizinlerini belirtebileceğiniz yerdir. Bu dizinler normalde proje konumuna göre kaydedilir ve projeleri bir bilgisayardan diğerine veya bir FileSystem 'tan diğerine taşımayı kolaylaştırır.

Ek üstbilgiler alanı, özel üstbilgi dosyalarını belirtebileceğiniz yerdir. Birden fazla üstbilgi dosyası gerekiyorsa, listeyi sınırlandırmak için noktalı virgül kullanın.

Studio "uygulama oluşturma" veya "kaynak oluşturma" komutlarını çağırdığınızda, bunlar bu kaynak dosyalarının yazılacağı varsayılan dizinlerdir. Tabii ki, çıkış dizini iletişim kutusuna yeni konumlar girerek bu dizin konumlarını dilediğiniz zaman geçersiz kılabilirsiniz.

## <a name="selecting-widgets"></a>Pencere öğelerini seçme

Pencere öğelerinin seçilmesi, ***proje görünümü** _ pencere öğesi ağacındaki pencere öğesine tıklayarak ya da _*_hedef görünüm_*_ alanında görünür pencere öğesine tıklayarak yapılır. Tek bir pencere öğesi seçildiğinde, özellikleri _*_Özellik görünümü_*_ alanında görüntülenir. _*_Şekil 22_*_ "_ *_Button_* *" öğesinin seçili pencere öğesini gösterir.

![Seçilen pencere öğesinin ekran görüntüsü.](./media/guix-studio/select_button.png)

**Şekil 22**

## <a name="using-properties"></a>Özellikleri Kullanma

Daha önce belirtildiği gibi, seçili bir pencere öğesinin özellikleri ***Özellikler Görünümü** _ içinde sunulur. Tüm pencere öğelerinin ortak bir özellikler kümesi ve belirli pencere öğesi türüne özgü bazı özellikler vardır. Örneğin, bir pencere pencere öğesi olmasa da bir düğme pencere öğesinin _ *_Itilmiş_** özelliği vardır. Aşağıda, pencere öğesi özelliklerinin ortak kümesi verilmiştir:

| Özellik         | Anlamı                                                                               |
| ---------------- | ------------------------------------------------------------------------------------- |
| Pencere öğesi türü    | Pencere öğesinin türü, başvuru için                                                                               |
| Pencere öğesi adı      | Pencere öğesi oluşturma işlevine geçilen ve oluşturulan kaynak dosyalarında değişken adlandırma için kullanılan pencere öğesinin adı.               |
| Pencere öğesi KIMLIĞI        | Pencere öğesinin KIMLIĞI. Bu KIMLIK değeri, alt pencere öğelerinin üst ekranlarına sinyaller oluşturmak için kullanılır.                            |
| Sol             | Pencere öğesinin en sol koordinatı                                                                                                 |
| Üst              | En üst-pencere öğesi koordinatı                                                                                                  |
| Width            | Pencere öğesinin piksel cinsinden genişliği                                                                                                      |
| Height           | Pencere öğesinin piksel cinsinden yüksekliği                                                                                                     |
| Kenarlık           | Pencere öğesi kenarlığının türü                                                                                                          |
| Geçirgen      | Pencere öğesi kısmen saydam ise, denetlenmesi gerekir                                                                       |
| Seçili çiz    | Pencere öğesinin başlangıçta kendisini seçili durumda çizmesi gerekiyorsa, denetlenmesi gerekir.                                            |
| Etkinleştir           | Pencere öğesi son kullanıcı tarafından seçilebiliyorsanız veya tıklanmıyorsa, denetlenmesi gerekir.                                                    |
| Odağı kabul eder    | Pencere öğesi odağı kabul ediyorsa, denetlenmesi gerekir.                                                                                 |
| Çalışma zamanı ayırma | Pencere öğesi denetim bloğunun dinamik olarak ayrılması gerekiyorsa, denetlenmesi gerekir.                                                 |
| Normal dolgusu      | Normal Fill Color kaynak kimliği                                                                                                  |
| Seçili Fill    | Seçili Fill Color kaynak kimliği                                                                                                |
| Draw Işlevi    | Kullanıcı tanımlı özel çizim işlevi adı. Bu alan boşsa, bu pencere öğesi türü için standart çizim işlevi kullanılır. |
| Event Işlevi   | Kullanıcı tanımlı özel olay işleme işlevi adı. Boşsa, bu pencere öğesi türü için Standart olay işleme kullanılır.          |

***Şekil 23*** basit pencere pencere öğesinin özelliklerini gösterir.

![Basit pencere pencere öğesinin özelliklerinin ekran görüntüsü.](./media/guix-studio/image57.jpg)

**Şekil 23**

Birçok pencere öğesi türü her pencere öğesi türüne özgü ek özelliklere sahiptir.

Örneğin, yukarıdaki Şekil 23 ' te pencere pencere öğesi türü bir duvar kağıdı pixelmap kimliğini ve duvar kağıdının ortalanmış veya döşeli olması gerektiğini belirten bir stil ayarı destekler.

Metin pencere öğeleri, metin hizalama stilleriyle birlikte bir dize KIMLIĞI alanını ve bir yazı tipi belirtimini destekler. Ek pencere öğesi özellikleri, her bir pencere öğesi türünün açıklamasını ve kullanılabilir stilleri okuduktan ve bu pencere öğesi türü için işlev parametreleri oluştururken genellikle oldukça sezgisel hale ayarlanır.

## <a name="manipulating-widgets"></a>Pencere öğelerini düzenleme

Bir pencere öğesini işlemek için önce ' nin seçilmesi gerekir. Bu işlem, ***hedef görünümü** _ ' de doğrudan pencere öğesine tıklanarak veya _ *_proje görünümü_** pencere öğesi ağacı içinde seçilerek yapılır. Seçildikten sonra pencere öğesi kesikli bir anahatta sahip olur. Bu durumda, yalnızca pencere öğesine tıklanarak taşınabilir ve onun üst öğesinde istenen konuma sürüklenerek taşınmış olabilir. Pencere öğesi üst düzey pencere öğesi ise pencere öğesini sürüklemek, hedef ekranda pencere öğesinin ilk konumunu etkin bir şekilde ayarlıyor. Kuşkusuz, her zaman pencere öğesi Gux API 'sini kullanarak herhangi bir pencere öğesini taşımak veya yeniden boyutlandırmak mümkündür.

Pencere öğesinin yüksekliğini yeniden boyutlandırmak için, fareyi pencere öğesinin üst kenarına konumlandırın ve fare işaretçisinin aşağı doğru bir oka değiştirilmesini bekleyin. Bu noktada pencere öğesi yüksekliği, sağ fare düğmesi basılı durumdayken fare hareket ettirilerek değiştirilebilir. Fare işaretçisini pencere öğesinin sol kenarına konumlandırarak farenin genişliği benzer bir biçimde yeniden boyutlandırılabilir. ***Şekil 24** _ "_ *_Button_* *" pencere öğesinin yeniden boyutlandırıldığını ve üst pencerenin sol/üst bölgesine taşındığını gösterir.

![Düğme pencere öğesinin ekran görüntüsü.](./media/guix-studio/resize_button.png)

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

Studio, bir pencere öğesi yapıştırma işleminin bir parçası olarak projenize bir kaynak eklediğinde, yazı tipi ve pixelmap kaynakları söz konusu olduğunda Studio gerçekten kaynağa bir bağlantı ekliyor. Bu bağlantı, kaynak projeden oluşturulur ve bu kaynaklar, yapıştırdığınız projenin proje konumuna göre bulunamazsa uyarı iletileri alırsınız. Kaynak bağlantıları projeye ne olursa olsun eklenir, ancak kaynak yükleme hatalarını ortadan kaldırmak için yazı tiplerini ve resim dosyalarını yeni proje ağacınızdaki doğru konumlara el ile kopyalamanız gerekebilir. Studio. ttf,. png veya. jpg dosyalarını bir konumdan diğerine kopyalamaz.

Bu şekilde herhangi bir problemi önlemenin kolay yolu, paylaşmak istediğiniz projeler arasında tutarlı bir dizin yapısı tutmaktır. Proje A 'dan proje B 'ye kolayca taşımak istiyorsanız, her iki proje klasörü için tutarlı bir alt dizinde bulunan grafik görüntülerini ve yazı tiplerini saklayın.

## <a name="changing-z-order"></a>Z düzenini değiştirme

Pencere öğeleri, diğer pencere öğelerinin önüne veya arkasına kolayca taşınabilir. Bu, pencere öğesi seçilerek ve _*_araç çubuğundaki_*_***öne taşı** _ veya _*_Geri düğmelerine git_*_ seçilerek gerçekleştirilir. _ *_Şekil 28_** İkinci düğmenin geri taşınmasını gösterir.

![Düğme z düzeninin ekran görüntüsü.](./media/guix-studio/change_z_order.png)

**Şekil 28**

## <a name="assigning-colors-fonts-and-pixelmaps"></a>Renkler, yazı tipleri ve pixelmaps atama

Seçili bir pencere öğesi için Özellikler görünümünde renkler, yazı tipleri ve pixelmaps seçmeye ek olarak, pencere öğeleri için kaynak atamaya yönelik bir tam sürükleme ve bırakma yöntemi de desteklenir. Bu özelliği kullanmak için, kaynak görünümündeki bir yazı tipi rengi gibi bir kaynağa sağ tıklayıp kaynağı hedef görünümde istenen pencere öğesi üzerine sürükleyin. Sol fare düğmesini pencere öğesi üzerine bırakarak kaynağı bırakın.

Sürükleme ve bırakma yöntemi kullanılırken, renk kaynakları her zaman pencere öğesi normal arka plan rengine atanır. Seçilen renk veya seçili metin rengi gibi diğer renkler Özellikler Görünümü kullanılarak atanmalıdır.

Benzer şekilde, pixelmap kaynakları, pixelmap görüntüsünü destekleyen bir pencere öğesinin "normal" veya "Fill" pixelmap alanına atanır. Birden çok pixelmaps destekleyen bir pencere öğesine başka alanlar atamak için Özellikler görünümünü kullanmanız gerekir.

## <a name="using-templates"></a>Şablonları kullanma

Studio 'da tasarlamanızı sağlayan herhangi bir ekran veya alt pencere öğesi koleksiyonu, yeni ekranlar ve yeni alt denetimler için şablon olarak kullanılabilir. Şablon kullanmak, bir pencere öğesini kopyalamaya ve yapıştırmaya benzer, ancak bir şablondan türetilmiş her şey, temel aldığı şablon değiştirildiğinde otomatik olarak değiştirilir. Türetilmiş bir ekranla veya şablonun devralınmış örneğiyle çalışırken şablon pencere öğesi özelliklerini değiştirmenize izin verilmiyor. Bununla birlikte, şablon özelliklerini herhangi bir şekilde değiştirdiğinizde, şablona başvuran tüm örnekler bu şablondan türetildiklerinden otomatik olarak güncelleştirilir.

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

## <a name="gridsnap-settings"></a>Kılavuz/yaslama ayarları

***Grid ve Snap Settings** _ iletişim kutusu, Grid ve Snap için bazı ayarları ve seçenekleri içerir. _*_Şekil 29_*_ , menü _ _*_congiayarınızı yaparken kılavuz ve yapışma ayarı_*_ iletişim kutusunu gösterir.*_Hedef görünüm | Grid/Snap_** seçilidir.

![Kılavuz ve yaslama ayarlarının ekran görüntüsü.](./media/guix-studio/image63.jpg)

**Şekil 29**

Aç ***Kılavuzu göster** _ seçeneği, kılavuzu hedef ekranda görüntüleyecektir, ızgara _*_aralığı_*_ alanında ızgara artışı (piksel cinsinden) belirtebilirsiniz. _ *_Kılavuza yapış_** seçeneği bir pencere öğesini doğru konuma almanıza yardımcı olur. bu seçeneği etkinleştirmek etkin olacak şekilde yaslanır.

***Kılavuz ve yaslama*** seçeneği etkin olduğunda:

- Bir nesneyi hedef görünümde fareyle sürüklerseniz, nesne ızgara artışını taşır.
- Yeniden boyutlandırmak için bir nesnenin kenarını sürüklerseniz, sürüklediğiniz kenar kılavuz konumuna yaslanacak.
- Bir nesne seçer ve yukarı/aşağı/aşağı/sağ tuşlarını kullanıyorsanız, seçilen pencere öğesi yapışma artışına göre hareket edebilir, yaslama artışını (piksel cinsinden) ***yaslama boşluğu*** alanında belirtebilirsiniz.
