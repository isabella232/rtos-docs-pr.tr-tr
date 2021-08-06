---
title: GUX Studio ekran Tasarımcısı
description: Uygulama ekranları tasarlamak, GUıDX Studio 'nun birincil amacıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 91377a663dfb605caa33ab019f437f2c3ed1adc7
ms.sourcegitcommit: 62cfdf02628530807f4d9c390d6ab623e2973fee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/05/2021
ms.locfileid: "115178315"
---
# <a name="chapter-5-guix-studio-screen-designer"></a>Bölüm 5: GUıDX Studio ekran Tasarımcısı

Uygulama ekranları tasarlamak, GUıDX Studio 'nun birincil amacıdır. Ekran tasarımı, Bölüm 3 ' te daha önce açıklanan çeşitli görünümler aracılığıyla gerçekleştirilir. Ancak, GUıDX Studio 'daki ekran tasarımının ana öğesi, tüm ekran öğelerinin görsel olarak görüntülendiği ve gömülü hedef ekranda göründükleri şekilde tam olarak gösterildiği ***hedef görünümlüdür***. Bu ekran öğeleri basit fare ve düğme işlemleri aracılığıyla seçilebilir, taşınabilir, yeniden boyutlandırılabilir, vb. olabilir. Ayrıca, hizalama ve Z düzeni düğme işlemleri seçili nesneler üzerinde kullanılabilir. Aşağıdaki alt bölümlerde, Gux Studio ekran tasarımının çeşitli özellikleri açıklanır. 

## <a name="creatingconfiguring-projects"></a>Projeleri oluşturma/yapılandırma

gux Studio 'da proje oluşturma basittir. yalnızca ***yeni Project** _ düğmesini veya menü seçimini _*_Project yeni Project_*_ seçmeniz yeterlidir. ardından, guıdx Studio _ *_Configure Project_** iletişim kutusunu gösterir. Bu iletişim kutusunda, temel görüntü ayarlarının yanı sıra, GUıDX Studio tarafından oluşturulan kodun yerini almak için yol bilgileri belirtilir.

Yeni bir proje oluşturulduğunda, projeyi Yapılandır iletişim kutusu görüntülenir. Geliştirici, hedefte kullanılabilen donanım görüntüleme sayısını ve her bir görüntüleme özelliğini belirtir. Özellikler, ekran mantıksal adı, x/y çözünürlüğü, renk derinliği ve biçimi ve diğer görüntü özelliklerini içerir. GUX Studio aynı projede birden çok ekranları destekler. Ek ekranlar gerekliyse, ***ekran sayısı** _ alanının gömülü cihazdaki ekran sayısıyla eşleşecek şekilde değiştirilmesi gerekir. Bir projedeki en fazla ekran sayısı 4 ' dir. _ *_şekil 21_** yapılandırma Project iletişim kutusunu gösterir.

proje ve/veya görüntü ayarlarını değiştirmek, menü seçeneği ***yapılandır, Project/display** _ veya proje ya da görüntüleme, sağ tıklama ve _*_yapılandır, Project/display_*_ seçeneklerini belirleyerek gerçekleştirilir. her iki durumda da, _ *_Configure Project_** iletişim kutusu, proje ayarları ve/veya görüntüleme değişikliklerini kolaylaştırmak için sunulur.

![yapılandırma Project iletişim kutusunun ekran görüntüsü.](./media/guix-studio/config_project.png)

**Şekil 21**

Dizinler grubu, Studio tarafından üretilen C kaynağı ve üstbilgi dosyaları için varsayılan çıkış dizinlerini belirtebileceğiniz yerdir. Bu dizinler normalde proje konumuna göre kaydedilir ve projeleri bir bilgisayardan diğerine veya bir FileSystem 'tan diğerine taşımayı kolaylaştırır.

Ek üstbilgiler alanı, özel üstbilgi dosyalarını belirtebileceğiniz yerdir. Birden fazla üstbilgi dosyası gerekiyorsa, listeyi sınırlandırmak için noktalı virgül kullanın.

Studio "uygulama oluşturma" veya "kaynak oluşturma" komutlarını çağırdığınızda, bunlar bu kaynak dosyalarının yazılacağı varsayılan dizinlerdir. Tabii ki, çıkış dizini iletişim kutusuna yeni konumlar girerek bu dizin konumlarını dilediğiniz zaman geçersiz kılabilirsiniz.

## <a name="selecting-widgets"></a>Pencere öğelerini seçme

pencere öğelerinin seçilmesi, ***Project View** _ pencere öğesi ağacındaki pencere öğesine tıklayarak ya da _*_hedef görünüm_*_ alanında görünür pencere öğesine tıklayarak yapılır. Tek bir pencere öğesi seçildiğinde, özellikleri _*_Özellik görünümü_*_ alanında görüntülenir. _*_Şekil 22_*_ "_ *_Button_* *" öğesinin seçili pencere öğesini gösterir.

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

Bir pencere öğesini işlemek için önce ' nin seçilmesi gerekir. bu, ***hedef görünümü** _ ' de doğrudan pencere öğesine tıklanarak veya _ *_Project görünümü_** pencere öğesi ağacı içinde seçilerek yapılır. Seçildikten sonra pencere öğesi kesikli bir anahatta sahip olur. Bu durumda, yalnızca pencere öğesine tıklanarak taşınabilir ve onun üst öğesinde istenen konuma sürüklenerek taşınmış olabilir. Pencere öğesi üst düzey pencere öğesi ise pencere öğesini sürüklemek, hedef ekranda pencere öğesinin ilk konumunu etkin bir şekilde ayarlıyor. Kuşkusuz, her zaman pencere öğesi Gux API 'sini kullanarak herhangi bir pencere öğesini taşımak veya yeniden boyutlandırmak mümkündür.

Pencere öğesinin yüksekliğini yeniden boyutlandırmak için, fareyi pencere öğesinin üst kenarına konumlandırın ve fare işaretçisinin aşağı doğru bir oka değiştirilmesini bekleyin. Bu noktada pencere öğesi yüksekliği, sağ fare düğmesi basılı durumdayken fare hareket ettirilerek değiştirilebilir. Fare işaretçisini pencere öğesinin sol kenarına konumlandırarak farenin genişliği benzer bir biçimde yeniden boyutlandırılabilir. ***Şekil 24** _ "_ *_Button_* *" pencere öğesinin yeniden boyutlandırıldığını ve üst pencerenin sol/üst bölgesine taşındığını gösterir.

![Düğme pencere öğesinin ekran görüntüsü.](./media/guix-studio/resize_button.png)

**Şekil 24**

## <a name="manipulating-multiple-widgets"></a>Birden Çok Pencere Öğesi'nin Manipüle Ing

Birden çok pencere öğesinin seçimi, Ctrl tuşunu basılı tutarak hedef görünümde birden çok pencere öğesi ***tıklar.*** Bunu yapmak, seçili pencere öğelerinin her biri çevresinde kesikli bir ana hat ile birlikte gösterir. Birden çok pencere öğesi seçerek seçim grubu içindeki her pencere öğesinin aynı üst öğenin alt öğesi olması gerektiğini unutmayın.

Birden çok pencere öğesi seçildikten sonra, seçilen pencere öğelerinin içine tıklar ve farenin sağ fare düğmesi aşağı doğru hareket ettirilir. Ayrıca* Araç Çubuğu _ üzerindeki hizalama **düğmeleri,** seçili pencere öğeleri grubunu hizalamak için kullanılabilir. _*_Şekil 25'te_*_ _*_hem_*_" düğmesi " hem de "_*_yeni_*_ düğme " pencere öğeleri seçili ve _*_Şekil 26'da_*_ bu pencere öğeleri seçiliyken _ *_Sola_* Hizala * düğme seçiminin sonucu görüntülenir.

![Düğmenin ve yeni düğme pencere öğelerinin seçili olduğu ekran görüntüsü](./media/guix-studio/multiple_select.png)

**Şekil 25**

![Uygulama düğmesinin seçiminin Align-Left görüntüsü.](./media/guix-studio/align_left.png)

**Şekil 26**

## <a name="cutcopypaste-operations"></a>Kesme/Kopyalama/Yapıştırma İşlemleri

* Hedef Görünümde _ **seçili bir pencere** öğesi standart şekilde kesilmelidir, kopyalanır ve yapıştırılabilmelidir. Pencere öğeleri ve ekranlar bir proje içinde kopyalanır veya bir projeden kopyalanır ve başka bir projeye yapıştırabilirsiniz. Araç _*_Çubuğunda kesme,_*_ kopyalama ve yapıştırma düğmeleri bulunur. Düzenle menü seçeneğinde de aynı seçenekler vardır. Bir pencere öğesi yapıştırırken, yeni pencere öğesi yapıştırılamadan önce üst pencere öğesi seçilmelidir. _*_Şekil 27'de_*_ "_* düğmesi**" pencere öğesinin seçerek, kopyalayıp kopyayı aynı pencereye yapıştırarak elde edilen sonuç gösterilir.

![Kes/kopyala/yapıştır işlemlerinin ekran görüntüsü.](./media/guix-studio/copy_paste_button.png)

**Şekil 27**

Bir proje içinde çalışırken kopyalanan pencere öğeleri için gerekli olan kaynaklar her zaman mevcut olduğundan, bir proje içinde kopyalama/yapıştırma genellikle basittir. Ancak, A projesinden bir pencere öğesi kopyalayıp bu pencere öğesi B projesine yapıştırıyorsanız kaynak bağımlılıkları ile ilgili bazı sorunlar ortaya çıkabilir.

Studio'nun içinde pencere öğelerini kopyalayarak, Studio uygulaması kopyalanan pencere öğeleri için gereken kaynakların listesini yapar ve xml biçiminde, windows panosuna kopyalanan ve kopyalanan gerçek pencere öğesi bilgileriyle birlikte taşınabilir bir kaynak bağımlılık tablosu üretir. Pencere öğelerini farklı bir projeye yapıştırsanız, Studio ilk olarak kaynak bağımlılık listesini inceler ve henüz mevcut olmayan açık projeye gerekli kaynakları ekler. Studio eşleşen kaynakları kaynak kimliği adlarına göre tanımlar ve dize kaynakları için Studio da dize içeriğini karşılar. Eşleşen kaynaklar bulunursa Studio, yapıştırilen pencere öğelerinin kaynak kimliklerini yeni projede kaynakları düzgün şekilde kullanmak için günceller. Kaynaklar bulunamasa eklenir.

Studio, pencere öğesi yapıştırma işlemi kapsamında projenize bir kaynak eklerken, Studio yazı tipi ve piksel haritası kaynakları söz olduğunda kaynağa bir bağlantı ekler. Bu bağlantı kaynak projeden oluşturulur ve bu kaynaklar yapıştırmakta olan projenin proje konumuyla ilgili olarak bulunamazsa uyarı iletileri alırsınız. Kaynak bağlantıları projeye ne olursa olsun eklenir, ancak kaynak yükleme hatalarını ortadan kaldırmak için yazı tiplerini ve görüntü dosyalarını yeni proje ağacınız altındaki uygun konumlara el ile kopyalamanız gerekebilir. Studio .ttf, .png veya .jpg bir konumdan diğerine kopyalamaz.

Bu konuda herhangi bir sorundan kaçınmanın kolay yolu, paylaşmak istediğiniz projeler arasında tutarlı bir dizin yapısı tutmaktır. A'dan B'ye Project kolayca Project, her iki proje tarafından kullanılan grafik görüntülerini ve yazı tiplerini her proje klasörünün tutarlı bir alt dizininde tutabilirsiniz.

## <a name="changing-z-order"></a>Z Sıralamayı Değiştirme

Pencere öğeleri, diğer pencere öğelerinin önüne veya arkasına kolayca taşınabilir. Bu, pencere öğesi seçerek ve Araç Çubuğunda ***** Öne Taşı _ veya Geri Taşı _*_düğmeleri_*_ seçerek _*_başarılı olur._*_ _ *_Şekil 28_** ikinci düğmeyi geri taşımayı gösterir.

![z-order düğmesinin ekran görüntüsü.](./media/guix-studio/change_z_order.png)

**Şekil 28**

## <a name="assigning-colors-fonts-and-pixelmaps"></a>Renkleri, Yazı Tiplerini ve Piksel Haritalarını Atama

Seçili bir pencere öğesi için Özellikler Görünümünde renkleri, yazı tiplerini ve piksel haritalarını seçmeye ek olarak, pencere öğelerine kaynak atamanın kısa bir sürükle ve bırak yöntemi de de de kullanılabilir. Bu özelliği kullanmak için kaynak görünümünde yazı tipi rengi gibi bir kaynağa sol tıklamanız ve kaynağı hedef görünümde istenen pencere öğesinin üzerine sürüklemeniz gerekir. Sol fare düğmesini pencere öğesi üzerine bırakarak kaynağı bırakın.

Sürükleme ve bırakma yöntemi kullanırken renk kaynakları her zaman pencere öğesi normal arka plan rengine atanır. Seçilen renk veya seçili metin rengi gibi diğer renkler, Özellikler Görünümü kullanılarak atanabilir.

Benzer şekilde, piksel haritası kaynakları piksel haritası görüntülemeyi destekleyen bir pencere öğesinde "normal" veya "dolgu" piksel haritası alanına atanır. Birden çok piksel haritasını destekleyen bir pencere öğesine başka alanlar atamak için Özellikler Görünümü'ne sahipsiniz.

## <a name="using-templates"></a>Şablonları kullanma

Studio'da tasarlasanız herhangi bir ekran veya alt pencere öğesi koleksiyonu, yeni ekranlar ve yeni alt denetimler için şablon olarak kullanılabilir. Bir şablonu, normal kullanım durumu olan Pencere türü pencere öğesi veya diğer pencere öğesi türlerine göre oluşturabilirsiniz. Şablon kullanmak, temel alınan şablon değiştirildiğinde şablondan türetilen her şeyin otomatik olarak değiştirilmeleri dışında pencere öğesi kopyalayıp yapıştırarak benzerdir. Türetilmiş bir ekranla veya şablonun devralınmış örneğiyle çalışırken şablon pencere öğesi özelliklerini değiştirmenize izin verilmez. Ancak, şablon özelliklerini herhangi bir şekilde değiştirerek şablona başvurulan tüm örnekler otomatik olarak güncelleştirilir çünkü bunlar bu şablondan türetilir.

Yinelenen öğeler için şablonları kullanmanın bir diğer avantajı, Studio tarafından oluşturulan belirtimler dosyasının genellikle her kullanıldıklarında yinelenen öğeleri yeniden oluşturmanızdan daha küçük olmasıdır.

Bir ekran veya alt pencere öğesi koleksiyonunun şablon olarak kullanılabını görmek için pencere öğesi özellikleri görünümünde "Şablon" onay kutusunu açabilirsiniz. "Şablon" onay kutusunu açsanız, şablon pencere öğesi Ekle'de ***görünür| Şablon*** aşağı çekme menüleri.

Şablon kullanma örneği olarak, düğme çubuğu olarak kullanılan bir pencere tanımlayabilirsiniz. Bu pencerenin kendisi birkaç alt düğme içerebilir ve bu düğme çubuğu çeşitli ekranlarda sık kullanılır. Studio projenizin içinde gerekli alt düğmeleri tutan küçük bir tek başına pencere tanımlayabilir ve bu pencereye "button_bar". Ardından bu pencereyi seçin ve "Template" özelliğini açın. Ardından bu düğme çubuğunu eklemek istediğiniz ekranı seçin. Ekle'yi kullanın| Template|button_bar menü komutuyla ekran button_bar bir örneğini ekleyebilirsiniz. Düğme çubuğunu yeniden konumlandırabilirsiniz ancak çoğu özelliği değiştirme iznine sahip olmadığınız unutmayın. Ancak, diğer önceden button_bar GUIX pencere öğesi türleri gibi bir pencere öğesi (ve herhangi bir button_bar) kullanabilirsiniz. Değişiklik button_bar, değişikliklerinizi yapmak için button_bar şablonu seçmeniz gerekir.

Tipik bir şablon kullanımına bir diğer örnek de birçok benzer ekran içeren bir uygulamadır. Örneğin uygulamanın ortak başlık çubuğunu, dolgu rengini, boyutunu, vb. paylaştığı 10 farklı ekran olabilir. Bu durumda, başlık çubuğu alt pencere öğelerinizi içeren ve ekran boyutunu, dolgu rengini ve diğer özellikleri yapılandıran bir şablon ekranı tanımlayabilirsiniz. Bu şablon ekranı tanımlandığı zaman bu şablondan 10 farklı ekran türetebilirsiniz. Ekle'yi kullanırken| Şablon| \<base_screen> menü komutuyla ekranınız, şablon ekranınız için tüm alt pencere öğeleri ve ayarlarla başlar. Şablon ekranından türetilen her ekranın, şablonun bir kopyası olmadığını, ancak şablon ekranından türetilmiş bir örnek olduğunu unutmayın. Ardından, türetilen her ekranı, gerekli ek içerikleri tutmak için özelleştirebilirsiniz.

Oluşturulan belirtimler dosyasının boyutunu kaydetmeye ek olarak şablonların kullanımı, uygulama görünümünüzde yapılan değişiklikleri yönetmeyi kolaylaştıracaktır. Yukarıdaki örnekte, benzer 10 ekran için arka plan rengini değiştirmenizin gerekli olduğunu varsayalım. Her ekranı seçmek ve dolgu rengi ayarlarını değiştirmek için gerekli olmak yerine yalnızca temel şablonu seçmeniz ve dolgu rengini değiştirmeniz gerekir ve bu değişiklik hemen tüm türetilmiş ekranlara yansıtılmalıdır.

Şablonlarla ilgili başka bir açıklama: Olay işleme akışının korunarak, yani hem temel ekran (ortak pencere öğesi olaylarını işleme için) hem de türetilmiş bir ekran için olay işleyicisi sağlarsanız türetilmiş ekran olay işleyicisi varsayılan durumda base_screen olay işleyicisini çağıracak. Bu, temel ekran olayı işleyicinin bu şablon tabanından türetilen tüm ekranlarda ortak pencere öğeleri tarafından oluşturulan olayları işlemesine olanak sağlar.

## <a name="record-and-playback-macro"></a>Kayıt ve Kayıttan Yürütme Makrosu

Makro kaydı ve kayıttan yürütme işlevleri, tuş vuruşlarını ve fare olaylarını kaydetmenizi ve kayıttan yürütmenizi sağlar.

Bir makro dosyasına kayıt,***** Makroyu Kayıt _ araç çubuğu düğmesi veya Düzenle, Makroyu _*_Kayded'i seçerek musunuz?_*_ GUIX Studio, makro _*_dosyanız_*_ için yol adını belirtmenize olanak sağlayan Kayıt Makrosu iletişim kutusunu sunar. Bu seçimi yaptıktan sonra kaydı _*_başlatmak için_*_ Kayıt düğmesine tıklayın. Kaydı tamamladikten sonra, _**_ makro kaydını sona ererken makroyu kaydetmek için Makroyu Kayded araç çubuğu düğmesini yeniden seçin veya _ *_Düzenle, Makroyu_* Sona Bırak * seçeneğini belirleyin.

Makro dosyasının kayıttan yürütmesi,**ana** açılır menüyü kullanarak * Makroyu Kayıttan Yürüt _ araç çubuğu düğmesi seçerek Ve makroyu Düzenle, Makroyu Yürüt _*_komutu seçerek_*_ musunuz? GUIX Studio,*_çalıştıracak önceden kaydedilmiş_* makro dosyasını belirtmenize olanak sağlayan _ Kayıttan Yürütme Makrosu * iletişim kutusunu sunar.

Yazı tipi veya görüntü ekleme gibi giriş veya çıkış dosyalarını seçen makroları kaydederken, dosya tarayıcısını seçmek için fare kullanmak yerine klavyeyi kullanarak dosya adını yazmanız önemlidir. Makro kaydedici fare ve klavye olaylarını kaydettikten ve dosya tarayıcınız zaman içinde değişene kadar dosya adını yazmanın, dosyayı grafiksel olarak seçmekten daha güvenilir olmasıdır.

## <a name="zooming-target-view"></a>Hedef Görünümü Yakınlaştırma

Yakınlaştırma işlevi, hedef ekranın yakın bir görünümünü elde etmeye yardımcı olur.

* Yapılandır'da istediğiniz yüzde yakınlaştırma ayarını **seçebilirsiniz| Hedef Görünüm| Yakınlaştırma** _ menü seçeneği. _ *_Araç Çubuğu_** ayrıca yakınlaştırma/uzaklaştırma düğmelerine de sahip.

## <a name="gridsnap-settings"></a>Kılavuz/Yas Ayarlar

* Kılavuz **ve Yasla Ayarlar** _ iletişim kutusunda kılavuz ve yasla için bazı ayarlar ve seçenekler yer alıyor. _*_Şekil 29'da_*_ _*_menü_*_ _ Congigure olduğunda Kılavuz ve *_Yasla Ayarı iletişim kutusu görüntülenir| Hedef Görünüm| Kılavuz/Yasla_** seçilidir.

![Kılavuz ve Yasla ekran Ayarlar.](./media/guix-studio/image63.jpg)

**Şekil 29**

* Kılavuzu **Göster** _ seçeneğinin açık olduğu kılavuz hedef ekranda görüntülenir; Kılavuz Aralığı alanında kılavuz artışını (piksel cinsinden) _*_belirtebilirsiniz._*_ _ *_Kılavuza Yasla_** seçeneği, bir pencere öğesinin doğru konumunu alamanıza yardımcı olur; bu seçeneğin aç olması anlık ekleri etkin olarak belirler.

Kılavuz ***ve Yasla*** seçeneği etkinleştirildiğinde:

- Fareyle hedef görünümde bir nesneyi sürüklersiniz, nesne kılavuz artırımına göre hareket eder.
- Yeniden boyutlandırmak için bir nesnenin kenarını sürüklersiniz, sürüklersiniz kenar kılavuz konuma yaslar.
- Bir nesneyi seçer ve yukarı/sol/aşağı/sağ anahtarları kullanırsanız, seçili pencere öğesi yaslama artışa göre hareket eder, Yaslama Aralığı alanında yaslama artışını (piksel cinsinden) ***belirtebilirsiniz.***
