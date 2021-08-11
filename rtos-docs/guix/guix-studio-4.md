---
title: GUX Studio kaynakları
description: GUX Studio, uygulamanın renkler, yazı tipleri, piksel haritaları ve dizeler için kullanacağı tüm UI kaynaklarının yönetimini sağlar. Aşağıdaki bölümlerde, Kullanıcı arabirimi ekran tasarımınızda kaynak ekleme, değiştirme ve silme işlemlerinin nasıl yapılacağı açıklanır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: dd694cb7d34df7ecae206c3dcaf7d75a20bd4bd4e26471bb94da4129897ef727
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116786329"
---
# <a name="chapter-4-guix-studio-resources"></a>Bölüm 4: Gux Studio kaynakları

GUX Studio, uygulamanın renkler, yazı tipleri, piksel haritaları ve dizeler için kullanacağı tüm UI kaynaklarının yönetimini sağlar. Aşağıdaki bölümlerde, Kullanıcı arabirimi ekran tasarımınızda kaynak ekleme, değiştirme ve silme işlemlerinin nasıl yapılacağı açıklanır. 

Tüm kaynak yönetimi, aşağıdaki _ *_Şekil 8_* * ' de gösterildiği gıbı, Gux STUDIO Kullanıcı arabirimindeki ***kaynak görünümü** _ içinde yapılır.

![GUX Studio Kaynak Görünümü ekran görüntüsü.](./media/guix-studio/image38.jpg)

**Şekil 8**

## <a name="color-resources"></a>Renk kaynakları

_*_Kaynak görünümü_*_ 'ın ***Colors** _ bölümü, renk kaynaklarınızı yönetmenizi sağlar. Görünüm üstbilgisindeki _ * alanına tıklayarak bu görünümü genişleterek *+* **_Şekil 9_**' da aşağıda gösterildiği gibi görünüm elde edebilirsiniz:

![Kaynak Görünümü renkler bölümünün ekran görüntüsü](./media/guix-studio/image_39.png)

**Şekil 9**

Renk kaynakları, her biri benzersiz bir mantıksal ada sahip bir veya daha fazla renkten oluşur. Örneğin **Şekil 9** ' da, ekran arkaplan dolgusu rengi için SISTEM renk kimliği olan mantıksal ad **tuvali** , fiziksel renkli siyah ile ilişkilendirilir. Bu renk kaynağı, uygulama nesne özelliklerindeki renk olarak **GX_COLOR_ID_CANVAS** her belirttiğinde kullanılır.

Renk RGB değerini gösteren "renk örneği" rengi, daha sonra renk KIMLIĞI adı tarafından gösterilir. Herhangi bir KIMLIK adıyla ilişkili RGB değerini dilediğiniz zaman değiştirebilirsiniz. Bu değerler Gux kitaplığı tarafından dahili olarak kullanıldığından, önceden tanımlı sistem renk KIMLIĞI adlarını değiştiremezsiniz. Ancak, renk değerlerinden herhangi birini değiştirebilirsiniz. Bir sistem renk değerinin değiştirilmesi genel bir **değişiklik** olur. Bu, belirli bir renk ataması olmayan herhangi bir pencere öğesinin yeni sistem renk değerini alacak anlamına gelir.

Temaya eklediğiniz özel renkler için hem renk adını hem de renk değerini değiştirebilirsiniz.

Renk kaynağını değiştirmek için, renk kaynağında çift tıklayın (veya sağ tıklama ve menü seçimi). Bu eylem, renk tanımı iletişim kutusunu getirir. Bu iletişim kutusunda, renk kaynağı uygulamanın kullanıcı arabirimi gereksinimleriyle eşleşecek şekilde değiştirilebilir. ***Şekil 10** _, _ *Canvas** çift tıklandığında değişiklik iletişim kutusunu gösterir. Bu iletişim kutusunun görünümü hedef görünümün renk biçimi ayarlarına bağlı olarak değişecektir.

![Renk düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_color.png)

**Şekil 10**

Renk düzenleme iletişim kutusunun görünümü geçerli görünümün renk derinliği ve renk biçimi yapılandırmasına bağlı olarak değişecektir.

Yeni bir renk kaynağı eklemek için _ *_kaynak görünümü_** 'Nin ***Colors** _ bölümünden aşağıdaki düğmeyi seçin:

![Yeni renk Ekle düğmesi](./media/guix-studio/image41.jpg)

Aşağıda gösterildiği gibi, yeni bir renk kaynağı eklemek için ortaya çıkan renk iletişim kutusunu **kullanın:***

![Renk düzenleme iletişim kutusundaki yeni rengin ekran görüntüsü.](./media/guix-studio/new_color.png)

**Şekil 11**

Bu adımları tamamladıktan sonra, uygulamanın kullanması için yeşil renkte **NEW_COLOR** adı ile yeni bir renk kaynağı **Kaydet** ' i seçmeniz gerekir.

**Görüntü renk biçimi ayarlarını değiştirirken dikkat edilecek özel noktalar:**

Yeni bir proje oluşturduğunuzda, otomatik olarak projenin ekran görüntüsünü ve her bir görüntüleme renk biçimini yapılandırmanız istenir. Çoğu zaman, bu seçimleri bir kez yaparsınız ve bu yapılandırma ayarlarını değiştirmeniz gerekmez.

Görüntüleme rengi biçim ayarlarınızı daha sonra değiştirmek için gerekli olduğunu belirleyebilirsiniz. Bu durumda, GUıDX Studio geçerli sisteminizin ve Kullanıcı rengi RGB değerlerinizin, eski renk biçiminden yeni renk biçimine en iyi şekilde dönüştürülmesini sağlayacak. Bu dönüştürme birkaç mantıksal kurala uyar.

Kullanıcı tanımlı renkler için, GUıDX Studio her zaman önceki rengi yeni renk biçimindeki en yakın eşleşen renge dönüştürmeye çalışır. 16 BPP 5:6:5 Color biçimi gibi yüksek renk derinliğine gri tonlamalı veya tek renkli bir biçimde dönüştürüyorsanız, bu değişiklik istenmeyen renk dönüştürmelerine neden olabilir. Görüntü renk derinliği ayarlarında büyük bir değişiklik yaparken, Kullanıcı tanımlı yeni renk tablosu için bazı el ile güncelleştirmeler gerekebilir.

Önceden tanımlanmış sistem renkleri için, GUıDX Studio dahili olarak üç benzersiz varsayılan renk tablosu tanımlar. Tek bir varsayılan renk tablosu, 4-BPP gri ölçeğe eşit tüm renk derinlikleri için kullanıldığında, gri ölçekli renk biçimleri (1 BPP < display_color_format <= 4bpp) için ikinci bir varsayılan renk tablosu kullanılır ve son olarak tek renkli renk biçimi için üçüncü bir varsayılan sistem renk tablosu kullanılır.

Project yapılandırma iletişim kutusunu kullanarak ekran renk biçimini değiştirdiğinizde aşağıdaki kurallar uygulanır:

1) Eski ve yeni ekran renk biçimleri yukarıda tanımlandığı gibi farklı varsayılan sistem renk tabloları kullanıyorsa, sistem renkleri her biri önceden tanımlanmış varsayılan renklere sıfırlanır. Diğer bir deyişle, renkten gri ölçeğe veya gri ölçeğe göre tek renkli derinliğe geçiş yaparsanız, sistem renkleriniz yeni renk derinliği için dahili olarak tanımlanan varsayılan değerlere sıfırlanır. Bu, bazı özelleştirilmiş renk bilgilerinin kaybedilmesine neden olabilir, ancak görüntü renk biçimi ayarlarınızda etkileyici bir değişiklik yaptığınızda bu çözüm size makul bir başlangıç noktası sağlar.

2) Eski ve yeni renk biçimleri aynı varsayılan renk tablosunu kullanıyorsa, daha az çarpıcı bir renk biçimi değişikliği yaptığınız anlamına gelir, GUıDX Studio her sistem rengini test eder ve sistem rengi RGB değerini varsayılan değerinden değiştirip değiştirmediğine göre belirlenir. Sistem rengi RGB değeri değiştirilmişse, GUıDX Studio eski renk biçiminden yeni renk biçimine bir en iyi eşleşme dönüştürmesi yapılır. Sistem rengi değiştirilmediyse, yeni renk biçimi için varsayılan renge sıfırlanır.

**Palet modu işlemine özel hususlar:**

Bir proje 256 renk paleti modu renk biçimi için yapılandırıldığında, Kullanıcı paletin nasıl yükleneceğini ve kullanılacağını yapılandırabilir. Yapılandırma kullanarak palet tanımına erişebilir ve bunları düzenleyebilirsiniz | Temalar iletişim kutusu ve projeniz 8 BPP için ayarlandıysa "paleti Düzenle" düğmesini görmeniz gerekir. Paleti Düzenle iletişim kutusunu açmak için bu düğmeye tıklayın:

![Palet düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_palette.png)

GUX Studio, paleti iki bölüme böler: "Kullanıcı tanımlı" bölümü ve "otomatik oluşturulan" bölümü. GUX Studio, her Temada bulunan görüntüleri görüntülemek için en iyi paleti oluşturmak üzere gelişmiş bir en iyi Palet oluşturma algoritması çalıştırır. "Önceden tanımlı palet girişleri" alanına bir sayı yazarak tanımlamanız gereken sayıda palet girişini girebilir ve bu yuvalardan herhangi biri için istediğiniz herhangi bir RGB değerini girin. Kalan yuvalar, görüntülerinizi görüntülemek için en uygun renk paletini oluşturmak üzere Studio 'ya ayrılacaktır.

Bu modda çalışırken, kaynak görünümünde tanımlanan bir rengi düzenlemek isterseniz, renk düzenleyici yalnızca tanımladığınız önceden tanımlanmış palet girişlerinden seçim yapmanıza izin verir. Bunun nedeni, kalan palet girişlerinin Gux Studio tarafından otomatik olarak oluşturulması ve projenize eklenen görüntülerin değiştirilmesi nedeniyle değişecektir.

8bpp palet modunda çalışırken, izin verilen fontların görüntülenmesini istiyorsanız her bir ön plan/arka plan rengi kullanımı için bir gradyan oluşturan palet girişi dizisini tanımlamanız gerekir. Her renk birleşimi için gradyan için 8 palet girişi ya da daha yumuşak bir gradyan için 16 palet girişi kullanabilirsiniz. kullanılan bu sayıda palet girişi, Project yapılandırma iletişim kutusundaki "palet modu, diğer ad-diğer metin rengi sayısı" onay kutusu tarafından belirlenir. Her renk birleşimi için kullanılan palet girdilerini en aza indirmek için yalnızca sekiz girişli bir degradeyi kullanabilir veya en iyi şekilde daha fazla izin verilen metin görünümünü sağlamak için 16 giriş degradeleri kullanabilirsiniz.

Bir renk degradesini daha fazla veya daha fazla olan metinlerin görüntülenmesini kolaylaştırmak için ya da kendi kullanımınız için bir renk gradyanı oluşturmak üzere paleti Düzenle iletişim kutusu bir gradyan oluştur düğmesi sağlar. Bu özelliği kullanmak için öncelikle başlangıç ve bitiş gradyanı renklerinin r:g: b değerlerini atamanız gerekir.

Örneğin, 50 dizininden itibaren sekiz palet girişi kullanarak orta gri arka planda daha fazla tercih edilen kırmızı metin göstermek istiyorsanız,. palet 50 dizinine 255:0:0 değerini ve 57 128:128:128 değerini paletle dizinine atayabilirsiniz. Bu iletişim kutusundaki başlangıç dizini ve son dizin alanlarına bu palet dizin değerlerini girin ve gradyan Oluştur düğmesine tıklayın. 51 ile 56 arasındaki palet girdileri, sınırlayıcı renklerinizde düzgün bir gradyan geçişi tanımlamak için başlatılır.

## <a name="font-resources"></a>Yazı tipi kaynakları

**Yazı tipi** _*_kaynak görünümü_*_ kaynaklarını yönetmek için, öncelikle _ * alanına tıklanması gerekir ve bu, *+* aşağıda **_Şekil 12_**' de gösterilen iletişim kutusuna yol açar:

![Kaynak Görünümü yazı tipi bölümünün ekran görüntüsü.](./media/guix-studio/image44.jpg)

**Şekil 12**

Yazı tipi kaynakları, her biri benzersiz bir mantıksal ada sahip bir veya daha fazla yazı tiplerinden oluşur. Örneğin, **Şekil 12** ' de mantıksal ad **sistemi** belirli bir yazı tipiyle ilişkilendirilir. Bu yazı tipi kaynağı, uygulama her ne zaman nesne özelliklerinde yazı tipi olarak **System** belirttiğinde kullanılır. Yazı tipi grubu, sol taraftaki yazı tipi karakterlerinin WYSıWYG önizlemesini, yazı tipi yüksekliğini piksel, yazı tipi KIMLIĞI adını ve yazı tipi boyutunu (KB cinsinden) gösterir.

Yukarıdaki görünümde, ilk dört yazı tipi, GUıDX kitaplığı için gereken önceden tanımlanmış varsayılan yazı tipleridir. Bu yazı tipleriyle ilişkili yazı tipi verilerini değiştirebilirsiniz, ancak bu yazı tipi KIMLIĞI adlarını değiştiremezsiniz.

Yukarıda gösterilen son yazı tipi, "Italik" adlı, projeye Kullanıcı tarafından eklenmiş özel bir yazı tipidir.

Yazı tipi kaynağını değiştirmek için, yazı tipi kaynağında çift tıklayın (veya sağ tıklama ve menü seçimi). Bu iletişim kutusunda, yazı tipi kaynağı uygulamanın kullanıcı arabirimi gereksinimleriyle eşleşecek şekilde değiştirilebilir. ***Şekil 13** _ _ *sistem** çift tıklandığında değişiklik iletişim kutusunu gösterir.

! [[Sistem çift tıklatıldığında değiştirme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_system_font.png)

**Şekil 13**

Yeni bir yazı tipi kaynağı eklemek için _ *_kaynak görünümü_** öğesinin ***Fonts** _ bölümünden aşağıdaki düğmeyi seçin:

![Yeni yazı tipi Ekle düğmesi](./media/guix-studio/image46.jpg)

Bu işlem `Font Edit` , ***Şekil 14***' te aşağıda gösterildiği gibi yeni bir yazı tipi kaynağı eklemek için iletişim kutusunu çağırır:

![Yeni bir yazı tipi kaynağı eklemek için değiştirme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/add_new_font.png)

**Şekil 14**

Yeni Gux yazı tipleri, bir TrueType yazı tipinin belirli bir boyutta işlenerek Gux Studio tarafından oluşturulur. Bu nedenle, yukarıdaki iletişim kutusu bir TrueType yazı tipi yolu gerektirir. Geliştirme sisteminizde yazı tipi dosyalarını içeren bir dizine gitmek için, Araştır düğmesini kullanabilirsiniz. Her türlü TrueType yazı tipi, GUıDX Studio 'Yu yüklediğiniz her yerde Gux/Fonts alt klasörüne de dahildir.

Mümkünse, TrueType yazı tipi dosyasının konumu proje göreli bir yol kullanılarak dahili olarak depolanır. Bu nedenle, her yazı tipi dosyanızı ortak bir konumda tutmanız ve Gux Studio projelerini bir geliştirme istasyonundan diğerine taşımanıza olanak tanımak için projeleriniz ve yazı tipi dosyalarınız için ortak bir dizin ağacı yapısı kullanmanız önemlidir.

Yazı tipi adı alanı, yazı tipi kaynak KIMLIĞI adını belirtmenize olanak tanır. Bu, GUıDX Studio tarafından oluşturulan kodda kullanılacak ve ayrıca yazı tipine başvururken uygulamanız tarafından kullanılan kaynak KIMLIĞIDIR. Bu ad, C değişken adlandırma sözdizimi gereksinimlerine uymalıdır.

Giriş olarak kullanılacak bir TrueType yazı tipi dosyasını seçtikten sonra, bir yazı tipi mantıksal adı girin.

"**Karakter aralığı bilgisi oluştur**" onay kutusu, Guıdx Studio 'ya, bir dizedeki art arda gelen karakterlerin göreli konumlarını ayarlamak için kullanılan yazı tipi içinde karakter aralığı bilgilerini içermesini sağlar. Dizelerinizle karakter aralığı uygulamak istiyorsanız, karakter aralığı bilgilerini içeren bir yazı tipi kullanmanız ve bu onay kutusunu açmanız gerekir. Ayrıca, metin karakter aralığı bilgileriyle işlemeyi desteklemek için "GX_FONT_KERNING_SUPPORT" Gux kitaplık derleme seçeneğini de tanımlamanız gerekir.

"**Dize tablosu tarafından tanımlanan karakter kümesini içer**" onay kutusu, Gux Studio 'nun oluşturulan yazı tipi içindeki statik dize tablonuz tarafından başvurulan glifleri içermesini sağlar. Aşağıda listelenen karakter aralıklarını seçip düzenleyerek ek Glifler ekleyebilirsiniz, ancak bu seçenek, dize tablonuzda tanımlanan dizeleri göstermek için gereken en düşük karakter kümesini hızlıca oluşturmak üzere seçilebilir. Tabii ki, dize tablonuz TrueType kaynak yazı tipinde bulunmayan Glifler kullanıyorsa, bu karakterler Gux yazı tipinde kullanılamaz ve hedef sisteminizde gösterilmez.

Daha kapsamlı bir yazı tipi veya statik olarak tanımlanmış dize tablonuz içinde kullanılamayan karakterler içeren bir yazı tipi oluşturmak için aşağıdaki listeden karakter aralıklarını de seçebilirsiniz. Herhangi bir sayıda karakter aralığı seçebilir ve seçili her aralığa dahil edilecek gerçek başlangıç ve bitiş karakter kodunu düzenleyebilirsiniz.

Önceden tanımlanmış karakter aralıkları ve sayfa adları yalnızca, günümüzde kullanımda olan Etkin diller için gereken karakter kümesini kolayca seçmenizi sağlayan önerilerdir. Listelenen dil adları, oluşturulan Gux yazı tipi üzerinde herhangi bir etkiye sahip değildir ve herhangi bir etkin veya seçili karakter aralığı için istediğiniz herhangi bir onaltılı karakter aralığını yazmanız ücretsizdir.

Örneğin, yalnızca sayısal karakterler içeren bir yazı tipi oluşturmak isterseniz, "ASCII" kod sayfasını seçebilirsiniz, ancak başlangıç değeri 0030 ve yalnızca sayısal karakterleri içeren bir yazı tipi oluşturmak için 0039 değerini girin. Unicode karakter tablolarının normal gösterimi olan, karakter aralığı değerlerinin onaltılık olarak kodlandığını unutmayın.

Varsayılan olarak, GUıDX Studio ve Gux kitaplığı, tüm etkin dilleri, matematik formlarını ve günümüzde kullanılan diğer sembolleri kapsayan, 0x0000 ile 0xFFFF karakter kodlarını destekler. Belirli özel kullanım alanı dahil olmak üzere 0xFFFF değerinin üzerinde karakter kodlarının kullanılmasını gerekiyorsa, "Genişletilmiş karakter aralığını destekleme" onay kutusunu açmanız gerekir. Bu onay kutusu seçildiğinde, GUıDX Studio, kullanıcının 0x0000 'den, Unicode özel kullanım karakter aralıklarını içeren bir karakter aralığı belirtmesini sağlar. Bu Genişletilmiş karakter aralığına ihtiyacınız varsa, Gux kitaplığı 'nın 16 bit karakter kodlarını destekleyen varsayılan yapılandırma yerine 32 bitlik karakter kodlarını dahili olarak desteklemesi için "GX_EXTENDED_UNICODE_SUPPORT" Gux kitaplık derleme seçeneğini de tanımlamanız gerekir.

Aşağıdaki listede yer alan "dize tablosu tarafından tanımlanan karakter kümesini dahil et" onay kutusunu ve bir veya daha fazla karakter aralığından birini seçerseniz, GUıDX Studio bu seçimleri hem seçili aralıkların hem de dize tablonuzda kullanılan karakterlerin üst kümesiyle birleştirir. Kuşkusuz, Gux Studio 'nun istenen her karakter değeri için anlamlı Glifler üretmesi için Seçili TrueType kaynak yazı tipi de gerekli karakterleri içermelidir.

Karakter aralığı belirlendikten sonra, yazı tipi yüksekliğini piksel ve yazı tipi biçimini belirtin. Hem kenar yumuşatma hem de ikili yazı tipleri desteklenir. İkili yazı tiplerinde daha az statik veri depolama alanı gerekir, ancak daha fazla diğer ad fontları 4-BPP gri tonlamalı veya daha yüksek renk derinliğinde çalışan hedeflerin en iyi görünümünü oluşturur.

>[!NOTE]  
> *"Yazı tipi yüksekliği", yazı tipinin EM karesini ifade eder. Geleneksel metal türünde EM karesi, her bir harfin ve her bir metal gövdenin aynı boyutta olduğu metal gövdenin çizgi yüksekliğine eşittir. Metal türünde, bir mektubun fiziksel boyutu normal olarak EM karesini aşamadı. Dijital türde EM, dijital bir yazı tipinin tasarım alanı olarak kullanılan rastgele bir çözünürlük ızgarasıdır. Bu dijital yazı tiplerinde, aksan ve açıklama gibi bazı glif özelliklerinin EM kare limitlerinin ötesine uzatasi yaygındır. Nihai sonuç, belirli bir fontu tam olarak görüntülemesi gereken pencere öğesi yüksekliğinin genellikle istenen yazı tipi piksel yüksekliğinin biraz daha büyük olması gerekir.*

Tüm yazı tipi yapılandırma alanları tamamlandıktan sonra, yeni bir yazı tipi kaynağı oluşturmak için Tamam düğmesine tıklayın. GUX Studio, seçilen özelliklerle birlikte bir Gux uyumlu yazı tipi oluşturur, bu yazı tipini Proje kaynaklarına ekler ve yazı tipini uygulamanın kullanması için kullanılabilir hale getirir.

## <a name="pixel-map-resources"></a>Piksel eşleme kaynakları

Pixel-Map kaynaklarını yönetmek için, önce _*_kaynak görünümü_*_ "**pixel-Maps** _" bölümünün, öncelikle _ * alanına tıklanması gerekir ve *+* aşağıda **_Şekil 15_**' te aşağıdaki iletişim kutusu görüntülenir:

`Pixelmap`Grup genişletildiğinde şuna benzer bir önizleme görmeniz gerekir:

![Kaynak Görünümü piksel eşlemeleri bölümünün ekran görüntüsü.](./media/guix-studio/pixelmap_view.png)

**Şekil 15**

Piksel eşleme kaynakları, bir veya daha fazla piksel eşlemden oluşur ve her biri sol taraftaki piksel eşleme resminin önizlemesini, piksel cinsinden piksel eşleme boyutlarını, benzersiz bir mantıksal adı ve çıkış kaynak dosyasındaki piksel eşleme depolama boyutunu (KB cinsinden) içerir.

İlk piksel haritaları grubu, radyo düğmeleri ve onay kutuları gibi Gux pencere öğeleri için gereken önceden tanımlanmış sistem piksel haritalarını içerir. Sistem piksel eşlemleriyle ilişkili piksel eşleme verilerini değiştirebilirsiniz, ancak bu piksel eşleme KIMLIĞI adlarını değiştiremezsiniz. Yukarıda da gösterildiği gibi, "BACKGROUND" ve "BUTTON_ACTIVE" gibi adlara sahip çeşitli özel piksel haritaları vardır. Bunlar, bir kullanıcının projeye eklediği bir GX_PIXELMAP_BUTTON pencere öğesini işlemek için kullanılabilecek piksel eşlemeleri örnekleridir.

Birçok proje çok sayıda piksel Haritası içerdiğinden, piksel eşleme görünümü piksel eşlem görüntülerini düzenlemek için istediğiniz sayıda piksel eşleme klasörü tanımlamanızı sağlar. 

Yeni bir piksel eşleme klasörü eklemek `Pixelmaps` , ***kaynak görünümü*** "klasör ekle" seçeneğinin bölüm başlığına sağ tıklanarak yapılır.

Piksel eşleme kaynağını değiştirmek için piksel eşleme kaynağında çift tıklayın (veya sağ tıklama ve menü seçimi). Bu iletişim kutusundan piksel eşleme kaynağı uygulamanın kullanıcı arabirimi gereksinimleriyle eşleşecek şekilde değiştirilebilir. ***Şekil 16** _ _ *RADIO_ON** çift tıklandığında değişiklik iletişim kutusunu gösterir.

![Piksel haritaları düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/image49.jpg)

**Şekil 16**

`Edit Pixelmap`İletişim kutusu, yeni bir piksel eşleme tanımlamanızı veya var olan bir piksel eşlemesinin içeriğini değiştirmenizi sağlar. Perde arkasında, GUıDX Studio giriş görüntüsünü okur ve resmi `GUIX GX_PIXELMAP` Gux kitaplığı tarafından kullanılabilecek biçime dönüştürür. GUX Studio Ayrıca, gelen görüntünün renk alanını bu piksel haritasının kullanacağı görüntünün renk alanına dönüştürür.

Bu iletişim kutusunun ilk alanı, kaynak görüntünün yoludur. GUX Studio, PNG (.png) veya JPEG (.jpg) biçimli görüntü dosyalarını destekler. Yerel dosya sisteminizde istenen giriş dosyasını bulmak için "araştır" düğmesini kullanabilirsiniz.

Mümkünse, giriş görüntü dosyasının konumu proje göreli bir yol kullanılarak dahili olarak depolanır. Bu nedenle, tüm görüntü dosyalarınızı ortak bir konumda tutmanın yanı sıra, Gux Studio projelerini bir geliştirme istasyonundan diğerine taşımanızı sağlamak ve giriş resim verilerini izlememek için ortak bir dizin ağacı yapısını kullanmak önemlidir.

`Pixelmap ID`Alanlar, piksel eşleme kaynağının mantıksal adını belirtmenize olanak tanır. Buraya yazılan bu ad benzersiz olmalıdır ve C değişkeni adlandırma sözdizimi kurallarını izlemelidir.

Çıkış dosyası belirt onay kutusu her piksel eşlemesi için benzersiz bir çıkış dosyası belirtmenize olanak tanır. Bu onay kutusu seçili değilse, pixel-Map verileri bu görüntü için varsayılan kaynak dosyasına yazılır. Onay kutusu işaretliyse, bu piksel eşlemesi için verilerin yazılacağı özel bir dosya adı yazabilirsiniz. Bu seçeneğin amacı, çok büyük C dizileri olan piksel eşleme verilerinizi birden çok çıkış dosyasına bölmenize imkan sağlamaktır. Belirli derleyiciler yüzlerce binlerce kaynak satırı olan C dosyalarını işlemek için uğraşşır.

"Çıktıyı Sıkıştır" onay kutusu, piksel eşleme çıktısının özel bir GUıDX sıkıştırma algoritması kullanıp kullanmadığını belirtmenize olanak tanır. Sıkıştırılmış çıkış dosyaları genellikle küçüktür, ancak aynı zamanda, hedefte işlenmesi için işlemci süresi gerekir. Çoğu zaman, büyük piksel Haritalarınız için sıkıştırmayı seçer ve daha küçük piksel haritaları için sıkıştırılmış olmayan biçim kullanır.

`Include Alpha Channel`CheckBox, GUıDX Studio 'nun alfa kanal bilgilerini .png biçimlendirme giriş dosyalarında bazen nasıl kullanacağını belirler. Bu onay kutusu işaretliyse ve ekran 16 BPP renk derinliğinde veya üstünde çalışıyorsa, GUıDX Studio çıkış dosyasındaki tam gelen Alpha verilerini korur. Bu onay kutusu işaretli değilse, GUıDX biraz daha küçük bir çıkış dosyası oluşturur. Bu çıkış dosyası saydamlık içerebilir, ancak tam alfa karışım bilgileri içermez.

`Dither`CheckBox, Gux Studio 'ya, giriş görüntüsünü daha düşük bir renk derinliği görüntüsüyle kullanılmak üzere dönüştürürken gelişmiş bir titreme algoritması uygulamaya yöneltir. Titreme genellikle etkinleştirilir, ancak daha az yinelenen piksel olacağı için sıkıştırma kullanılıyorsa daha büyük çıkış dosyalarına neden olabilir.

Tüm seçenekler istendiği gibi ayarlandıktan sonra, yeni bir piksel eşleme kaynağı oluşturmak için Tamam düğmesine tıklayın. GUX Studio, giriş resim dosyasını okur, sıkıştırmasını açın, renk alanı dönüştürme ve titreme gerçekleştirir, isteğe bağlı olarak verileri yeniden sıkıştırır ve verileri Gux uyumlu `GX_PIXELMAP` biçimde kaydeder. Yeni pixel-Map Proje kaynaklarına eklenir ve uygulamanın kullanması için kullanılabilir hale getirilir.

Kaynak Görünümü bölümündeki yeni bir piksel eşleme kaynağı eklemek için `Pixelmaps` aşağıdaki düğmeyi seçin: 

![Yeni piksel eşleme düğmesi ekleyin.](./media/guix-studio/image50.jpg)

**Batch pixelmap düzenleme**

Bir veya daha fazla pixelmaps 'ın özelliklerini değiştirmek için, pixelmap grubuna veya klasöre sağ tıklayın ve pixelmap **'leri Düzenle iletişim kutusunu** çağırmak için pixelmap **(s) menüsünü Düzenle** ' yi seçin.

![Çok pikselli haritalar düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/batch_pixelmap_edit.jpg)

CheckBox durum açıklaması:

![İşaretli düğme.](./media/guix-studio/checkbox_checked.jpg)
Bu durum tüm pixelmaps özelliğinin işaretli olduğu anlamına gelir, tüm pixelmaps için özelliği değiştirmek üzere düğmenin işaretini kaldırabilirsiniz.

![İşaretlenmemiş düğme.](./media/guix-studio/checkbox_unchecked.jpg)
Bu durum tüm pixelmaps özelliğinin işaretlenmediği anlamına gelir, tüm pixelmaps için özelliği değiştirmek üzere düğmeyi kontrol edebilirsiniz.

![Belirlenmeyen düğme.](./media/guix-studio/checkbox_undetermined.jpg)
Bu durum, pixelmaps özelliğinin özelliği için farklı bir duruma sahip olduğu anlamına gelir, bu durumda tüm pixelmaps için özelliği değiştirmek üzere düğmeyi denetleyebilir veya işaretini kaldırabilirsiniz, aksi takdirde Özellik değişmeden kalır.


## <a name="string-resources"></a>Dize kaynakları

Dizeler grubu genişletildiğinde, aşağıda gösterildiği gibi proje dize tablosunun bir önizlemesini görmeniz gerekir:

![Genişletilen dizeler grubunun ekran görüntüsü.](./media/guix-studio/string_res_view.png)

**Şekil 17**

Dize kaynakları, her biri benzersiz bir mantıksal ada sahip bir veya daha fazla dizeden oluşur. Örneğin, **Şekil 17** ' de "PATIENT_LIST" mantıksal adı, sağ tarafta gösterilen "hasta listesi" dizesi ile ilişkilendirilir. Bu dize kaynağı, uygulama nesne özelliklerinde dize olarak PATIENT_LIST her belirttiğinde kullanılır.

Her zaman, tüm kaynak türleri için KIMLIK adlarınızın C sözdizimi uyumlu değişken adları olması gerektiğini unutmayın. Bu adlar, proje kaynak dosyalarınız ve belirtim dosyalarınız Studio tarafından üretildiğinde kapsamlı bir şekilde kullanılacaktır.

Bir dize kaynağını değiştirmek için, ***dize tablosu Düzenleyicisi** _ iletişim kutusunu çağırmak üzere dize kaynağında çift tıklayın (veya sağ tıklama ve menü seçimi). Dize _*_tablosu Düzenleyicisi_*_ iletişim kutusunda dize kaynağı, uygulamanın UI gereksinimleriyle eşleşecek şekilde değiştirilebilir. _*_Şekil 18_*_ ' de _ *STRING_13** çift tıklandığında değişiklik iletişim kutusu gösterilir.

Bu durumda, dize KIMLIK adı sol tarafta, birinci veya başvuru dilinin dize içeriğinin sağda gösterildiği anlamına gelir. Elbette tam dize içeriği uygulamanıza çok özeldir, ancak Dize grubu önizlemesi düzeni tutarlıdır.

GUIX Studio, bir Dize Tablosu tanımlayarak ve koruyarak statik metin ve çok dilli uygulamayı destekler. Dize Tablosu, her kayıt için bir dize kimliği ve desteklenen her dil için her kayıt için bir dize sabiti tanımlar.

Uygulamanız tarafından desteklenen diller Dil Yapılandırması İletişim Kutusu kullanılarak tanımlanır ve burada gösterebilirsiniz:

![Dil Yapılandırması iletişim kutusunun ekran görüntüsü.](./media/guix-studio/config_languages.png)

**Şekil 18**

Dil Yapılandırması İletişim Kutusu, Yapılandırma Sihirbazı kullanılarak | Uygulama menüsündeki Diller komutu. Bu iletişim kutusu, uygulamanız tarafından desteklenen dil sayısını ve her dille ilişkilendirilen ad veya dil kimliğini tanımlamanızı sağlar. Desteklenen diller projeniz oluşturulduktan sonra değiştirilebilir, ancak bir dil kaldırılırsa, bu dille ilişkili dize verilerinde de kaldırıldığına ve alınamayıldığına dikkat gerekir.

"Statik Olarak **Tanımlanmış" onay** kutusu, seçilen dilin oluşturulan kaynak dosyasında kaynak kodu biçiminde statik olarak tanımlandığına işaret ediyor. Hiçbir dil statik olarak tanımlanmamışsa, dil tablosu işaretçisi oluşturulan görüntüleme tablosunda NULL olarak ayarlanır ve GUIX kitaplığı tarafından sağlanan ikili kaynak yükleyici API'leri kullanılarak uygulama tarafından bir dil yükleniyor ve yükleniyor olmalıdır.

"Support **Bidi Text"** onay kutusu GUIX Studio'ya çift yönlü metin işleme desteğini etkinleştirmesini sağlar. Bu dil için girmeniz gereken dizeler çift yönlü metin işlemesi gerektirirse bu onay kutusunu açsanız iyi olur.

"Görüntü Düzeninde **Bidi Metni** Oluştur" onay kutusu, GUIX Studio'ya çıkış dosyasına görüntüleme sırasına göre çift yönlü metin oluşturma talimatı verir. Bu seçenek seçilirse, çift yönlü metni düzgün bir şekilde işlemek için GUIX kitaplığında çalışma zamanı işlemesi gerekmez. Bu seçenek seçildiğinde, GUIX kitaplığında çift yönlü metin işleme ETKINLEŞTIRILMEZ. Bu yapılandırma en iyi çalışma zamanı performansını verir, ancak dinamik olarak tanımlanmış çift yönlü metin dizelerinin işlemesini desteklemez.

İlk dil veya "Dizin 1" dili , "başvuru diliniz" olarak adlandırılır. Bu, KULLANıCı arabirimi tasarımınızı tanımlarken ve düzenlerken GUIX Studio'nun kullanabileceği dildir. Dize tablodaki diğer tüm diller Çeviri Dilleri olarak adlandırılır. GUIX Studio, dize tablosu verilerini endüstri standardı XLIFF veya CSV biçimli veri dosyalarında dışarı ve içeri aktarmayı destekler. Bu dosyalar, başvuru dili dışında desteklenen diller için çeviri ekleme konusunda uygulama geliştiriciye yardımcı olan çevirmenlerle dize bilgisi alışverişi yapmak için kullanışlıdır. GUIX dize tablosu bir XLIFF veya CSV dosyasına dışarı aktarıldıklarında, başvuru dili ve bir çeviri dili XLIFF veya CSV dizesi veri değişimi dosyasına dahil edilir. Benzer şekilde, bir XLIFF veya CSV dosyasını içeri aktarırsanız, içeri aktarılan veriler GUIX Dize tablonda bir çeviri dilini doldurmak için kullanılır.

![Dize tablosu Düzenleyicisi'nin ekran görüntüsü.](./media/guix-studio/image53.jpg)

**Şekil 19**

Dize Tablosu Düzenleyicisi iletişim kutusunda önce solda bir dize kimlikleri listesi ve ardından başvuru dili dizesi verileri görüntülenir. Birden fazla dil tanımlanmışsa, üçüncü sütunda desteklenen çeviri dillerinden herhangi biri görüntülenir. Başvuru dili sütunlarının sağ üst kısmında yer alan küçük oka tıklayarak üçüncü sütunu açıp kapatabilirsiniz.

Çeviri dili sütunu görünür olduğunda, dize listesinin çeviri dili sütununu sağ üst kısmında yer alan küçük oklara tıklayarak projede yer alan çeviri dillerinde döngüye geçebilirsiniz.

Bir dize kaydını seçmek için tablodaki kayda tıklayarak düzenleyebilirsiniz. Bir kayıt seçildiğinde, kayıt Dize Kimliği ve dize içeriği tablo görünümünün altındaki alanlarda gösterilir. Dize kimliğini ve dize içeriğini değiştirmek için bu alanlara yeni değerler girebilirsiniz.

Tablo görünümünün sağ tarafındaki kutu, seçili dizeye başvurulan pencere öğelerinin önizlemelerini gösterir. Bu, düzenlenen bir dizenin belirli bir pencere öğesi alanı aşıp aşmaymayacaklarını söylemek için kullanışlıdır.

Dize içeriğinin sağ tarafından sağdan alanlar şunlardır:

- "Başvuru sayısı": Bu alan, GUIX Studio projesi içinde belirli bir dize kimliğinin ne sıklıkta kullanildiğini gösterir. Başvuru sayısı 0 ise, bu dize kullanımdan kaldırılmış olabilir ve kullanıcı tarafından isteğe bağlı olarak kaldırılabilir.
- Dize Genişliği (piksel), belirtilen yazı tipini kullanarak dizenin görüntüleme genişliğini gösterir.
- "Notlar" alanı, her dizenin amacı veya kullanımı hakkında bilgi eklemenize olanak sağlayan isteğe bağlı bir açıklama alanıdır. Bu notlar, çevirmenlerin doğru ve anlamlı dize çevirileri yapmalarına yardımcı olmak için dışarı aktarıldı xlIFF dize veri dosyalarına dahildir.

Dize Tablosu Düzenleyicisi ***iletişim kutusunu her*** açıkken, iletişim kutusunun üst kısmında yer alan Dize Ekle düğmesine tıklayarak projenize başka dizeler ebilirsiniz. Kullanılmayan veya kullanılmayan dizeler önce dizeyi seçerek ve ardından iletişim kutusunun üst kısmında Bulunan Dizeyi Sil düğmesine tıklayarak projeden kaldırılabilir.

Dize Tablosu Düzenleyicisi iletişim kutusunu kullanarak projenize el ile yeni dizeler eklemenin yanı sıra, metni destekleyen herhangi bir pencere öğesinin Özellikler Görünümü'nde "Metin" alanına dize içeriği yazarak dolaylı olarak da yeni dizeler ekleyebilirsiniz. Başka bir deyişle, hedef görünüme yeni pencere öğeleri eklerken veya özellikler görünümünde metin bilgileri yazarken, bu eylemler proje dizesi tablosunda otomatik olarak yeni girişler oluşturuyor.

## <a name="adding-language-translations"></a>Dil Çevirileri Ekleme

GUIX Studio dize tablosu düzenleyicisi, geliştiricinin birincil dilini kullanarak bir uygulama oluşturmasını ve ardından dize verilerini standart bir şema XML'ine veya CSV dosyasına dışarı aktararak dil çevirisi uzmanına göndermesini sağlayan bir dil tanımı iş akışını destekler. Çeviri dosyası daha sonra geliştiriciye döndürülür ve bu geliştirici, dil çevirilerini Studio projesine geri aktararak uygulamasına yeni bir dil desteği ekler.

Bu tesis, Dize Tablosu Düzenleyicisi'nin üst kısmında yer alan Dışarı Aktar (dize verilerini bir dosyaya yazmak için) ve İçeri Aktar (çevrilmiş dizeleri okumak için) düğmeleri kullanılarak çağrılır. Dışarı Aktar düğmesi, başvuru dili dizelerinizi içeren bir XLIFF şema XML veya CSV dosyası oluşturmak için kullanılır. Bu dosya, standart XLIFF veya CSV dosya biçimini destekleyen araçlar ve düzenleyiciler kullanılarak bir çevirmen tarafından kullanılabilir.

Bir çeviri uzmanı xliff dosyasını size yeni dize çevirileriyle döndürtçe, verileri bu XLIFF veya CSV dosyasından okumak için İçeri Aktar düğmesini kullanabilirsiniz. XLIFF veya CSV dosyası yeni bir dil içeriyorsa, yeni dil projenize eklenir. XLIFF dosyası mevcut bir dil için yeni dize verileri içeriyorsa, bu yeni veriler projenize aktarılır. Başvuru dili dizeleri İçeri Aktarma işlemi tarafından değiştirilmez.

Dışarı Aktar düğmesine tıklarken XLIFF/CSV Dışarı Aktarma Denetimi iletişim kutusu aşağıda gösterilir:

![XLIFF/CSV Dışarı Aktarma Denetimi iletişim kutusunun ekran görüntüsü.](./media/guix-studio/image54.jpg)

**Şekil 20**

Kaynak Dil ve Hedef Dil alanları, HANGI dize tablosu sütunlarının BAŞVURU dili ve çeviri dili olarak XLIFF veya CSV dosyasına yaz olacağını belirtir. Kaynak dil, başvuru dizeleri, Hedef Dil ise çeviricinizin çevrilmiş dize verilerini sağlayacak dilidir.

XLIFF sürüm alanı iki ana XLIFF dosya biçimi sürümünden birini belirtir: sürüm 1.2 veya sürüm 2.0 (ve sonrası). Bu XLIFF dosya biçimi standartları uyumsuzdur ve XLIFF Dışarı Aktarma/İçeri Aktarma komutlarını kullanmadan önce araçlarınızı hangi sürümü kullanacağız? XLIFF şeması ve XLIFF standartları hakkında daha fazla bilgiyi burada bulunabilir:

- sürüm 1.2: [https://docs.oasis-open.org/xliff/xliff-core/xliff-core.html](https://docs.oasis-open.org/xliff/xliff-core/xliff-core.html)
- sürüm 2.0: [https://docs.oasis-open.org/xliff/xliff-core/v2.0/os/xliff-core-v2.0os.pdf](https://docs.oasis-open.org/xliff/xliff-core/v2.0/os/xliff-core-v2.0-os.pdf)

Çıktı dosya adı ve çıkış yolu alanları, çıkış dosyasının yazıldığı dosya adını ve konumu belirtmenize olanak sağlar. Dosya adı tamamen kullanıcıya yöneliktir, ancak dışarı aktaran dosyanın içinde yer alan kaynak ve hedef dilleri belirten adlar kullanmanızı öneririz.
