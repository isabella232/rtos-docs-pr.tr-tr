---
title: Belirli Pencere Öğesi Türlerini Düzenleme Notları
description: Belirli karmaşık pencere öğesi türleri için düzenleme yöntemlerini açıklayan ayrıntılı açıklamalar.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d57aa4034aaa6bbb3b29e79ba2b38443822ea5ce554b62af9e3c9ea874614488
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785511"
---
# <a name="chapter-8-notes-on-editing-specific-widget-types"></a>Bölüm 8: Belirli Pencere Öğesi Türlerini Düzenlemeyle Ilgili Notlar

GUIX Studio, kullanıcının uygulama kullanıcı arabirimi ekranlarını oluşturacak GUIX pencere öğelerini kolayca oluşturması ve değiştirmesini sağlar. Bu düzenleme yöntemlerinin çoğu sezgiseldir ve açıktır. Örneğin, bir pencere öğesini yeniden boyutlandırmak için fareyle pencere öğesini seçin ve pencere öğesinin kenarlıklarını sürükleyin. Ayrıca seçilen pencere öğesi için doğrudan sol/üst/genişlik/yükseklik özellik alanlarına da girebilirsiniz.

Bazı pencere öğesi türleri daha gelişmiş bir düzenleme işlemi gerektirir çünkü bu pencere öğeleri özellik desteğinde biraz daha gelişmiştir.

Bu bölümde, bu daha karmaşık pencere öğesi türleri için daha gelişmiş düzenleme özellikleri hakkında notlar yer almaktadır. GUIX Studio'nun özellikleri GUIX kitaplığında sağlanan pencere öğesi türleriyle birlikte ilerlerken bu notlar genişler.

## <a name="rich-text-view"></a>Zengin Metin Görünümü

Bu pencere öğesi, satır içi metin biçimlendirme kodlarını destekleyen zengin metin görüntülemek için kullanılır. Bu biçimlendirme kodları kalın, italik ve daha birçok kod içerir. Başlamak için, Görünüm veya Hedef Görünüm'Project ve **ekle/Metin/Zengin** Metin Görünümü menüsünü seçerek zengin metin görünümü pencere öğesi eklemek için seçili üst öğeye sağ tıklayın.  

Tüm pencere öğesi türleri tarafından desteklenen standart özellik kümesine ek olarak, Zengin Metin Görünümü pencere öğesi türü ek özellikleri destekler.

### <a name="additional-properties"></a>Ek Özellikler

| Özellik | Anlamı |
|----------|---------|
| Metin Hizala | Varsayılan metin hizalaması |
| Normal Yazı Tipi| Varsayılan metin yazı tipi |
| Kalın Yazı Tipi  | Kalın olarak etiketlenmiş metin için metin yazı tipi |
| Italik Yazı Tipi| Italik olarak etiketlenmiş metin için metin yazı tipi|
| Kalın İtalik Yazı Tipi| Kalın ve italik olarak etiketlenmiş metin için metin yazı tipi |
| Özel Metin Kopyalama | Pencere öğesi, atanmış herhangi bir metnin kendi özel kopyasını tutmak içinse denetlenir |
| Boşluk | Piksel cinsinden pencere öğesi ile görüntülenen metin arasındaki kenar boşluğu genişliği. |
| Satır Alanı | Metnin iki satırı arasındaki boşluk (piksel cinsinden). |
|||

### <a name="the-rich-text-formatting-codes"></a>Zengin Metin biçimlendirme kodları

Aşağıdaki biçim kodları metin biçimlendirme için de desteklemektedir.

|Etiket|Anlamı|
|---|---|
|\<b>\</b> | Kullanıcı tarafından belirtilen kalın yazı tipi kimliğiyle metin yazı tipini işleme|
|\<i>\</i> | Kullanıcı tarafından belirtilen italik yazı tipi kimliğiyle metin yazı tipini işleme|
|\<u>\</u> | Altı çizili metni işleme|
|\<f GX_FONT_ID>\</f> | Belirtilen yazı tipi kimliğini kullanarak metin işleme. |
|\<c GX_COLOR_ID>\</c> | Belirtilen renk kimliğini kullanarak metin işleme|
|\<hc GX_COLOR_ID>\</hc> | Belirtilen arka plan renk kimliğini kullanarak metin işleme|
|\<align left/right/center>\</align> | Metin hizalaması atama|
|||

GUIX Studio'dan zengin metin dizesini düzenlemenin iki yolu vardır:

- Önerilen ve en basit düzenleme yöntemi olan Zengin Metni Düzenle iletişim kutusunu kullanın.
- Önceki tabloda gösterilen biçimlendirme etiketlerini el ile eklemenizi sağlayan Dize Tablosu Düzenleyicisi iletişim kutusunu kullanın.

Hedef Görünüm'de Bir Zengin Metin Görünümü pencere  öğesi seçdikten  *sonra,* Şekil 8.1'de gösterilen zengin metin düzenleme iletişim kutusunu çağırmak için Özellikler GörünümündeKimliği Düzenle düğmesini seçin.

![GUIX Studio Zengin Metni Düzenle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_rich_text_dialog.png)

**Şekil 8.1**

Sol bölme zengin metin düzenleme alanıdır. Araç çubuğu simgelerini kullanarak istediğiniz etiketleri ekleyebilirsiniz. Düzenleme alanında herhangi bir metin bloğu seçin ve ardından araç çubuğu düğmelerini seçerek seçilen metin bloğuna gerekli stilleri ve renkleri uygulayabilirsiniz. Zengin Metni Düzenle iletişim kutusu, biçimlendirme kodlarını test dizesine eklemek için kolay bir yol sağlar. Ayrıca bu etiketleri el ile de ekleyebilirsiniz, hatta gerekirse çalışma zamanında da ekleyebilirsiniz.

Sağ bölme, metnin hedef görünümde nasıl işleneceklerini göstermek için pencere öğesi önizlemesidir. Pencere öğesi önizlemenin arka plan rengi sabittir ve hedef görünümde pencere öğesi tarafından atanan arka plan rengiyle eşleşmez.

Kaynak Kimliği adları, belirli yazı tipi veya renk kaynaklarına başvuru yapmak için zengin metinlerde kullanılır. Zengin metin dizesi tarafından başvurulduktan sonra yazı tipi veya rengin kaynak adı değiştirilirse GUIX Studio, zengin metin dizesini kaynak adı değişikliklerini yansıtacak şekilde otomatik olarak güncelleştirecek. Öte yandan, zengin metin pencere öğesi tarafından başvurulan bir yazı tipini veya renk kaynağını silersiniz, etkilenen zengin metni el ile düzenerek silinmiş olan kaynak kimliği adlarını kaldırmanız veya değiştirmeniz gerekir.

Bu iletişim kutusunda Kaydet düğmesini seçerek tanımlandığı zengin metin dizesi proje dizesi tablosuna eklenir.

## <a name="string-scroll-wheel"></a>Dize Kaydırma Tekerleği

Dize kaydırma tekerleği pencere öğesi, bir dize dizisinin görüntülemesini destekler. Bu dizeler dinamik olarak atanabilir veya uygulamanın birden çok dili desteklemesi durumunda, atanan dizeler etkin dize tablosundan çekebilirsiniz.

Dize kaydırma tekerleği pencere öğesi bir dize dizisini destekler. Kullanıcının bu dize dizisini atamasına izin vermek için Şekil 8.2'de gösterilen Dize Kaydırma Tekerleği Düzenleme iletişim kutusu sağlanır.

![GUIX Studio Dize Kaydırma TekerleğiNi Düzenle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/string_scroll_wheel_edit.png)

**Şekil 8.2**

Bu iletişim kutusunu çağırmak için Hedef Görünüm'de veya *Görünüm'de* bir dize kaydırma Project *seçin.* Bu pencere öğesi türü seçildikten sonra, *Özellikler Görünümü bir* Dizeleri Düzenle **düğmesi** içerir. Dize Kaydırma TekerleğiNi Düzenle iletişim kutusunu çağırmak için bu düğmeyi seçin.

Her metin dizini için bir dize atamak için, açılan listeden bir dize kimliği seçebilirsiniz veya sağdan Metin alanına yeni bir dize değeri yazabilirsiniz. Değişiklikleriniz bittiğinde, yeni veya değiştirilmiş dizeler etkin dize tablosuna kaydedilir.

## <a name="sprite"></a>Sprite

Sprite pencere öğesi, animasyon etkisi sağlamak için bir görüntü dizisi görüntülemek için kullanılır. Sprite pencere öğesi, görüntü kimlikleri dizisi olan bir çerçeve listesi ve çerçevenin her bir görüntüsüne uygulanan benzersiz parametreler gerektirir. Sprite pencere öğesi için bu çerçeve listesini oluşturmak için Şekil 8.3'te gösterilen Sprite Çerçevelerini Düzenle iletişim kutusu sağlanmıştır:

![GUIX Studio Sprite Çerçevelerini Düzenle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_sprite_frames.png)

**Şekil 8.3**

Bu iletişim kutusunu çağırmak için Hedef Görünüm içinde bir sprite pencere *öğesi seçin veya* Project *seçin.* Bu pencere öğesi türü seçildikten sonra, *Özellikler Görünümü bir* Çerçeve Listesi Düzenle **düğmesi** içerir. Dize Kaydırma TekerleğiNi Düzenle iletişim kutusunu çağırmak için bu düğmeyi seçin.

Toplam *Sprite Çerçeve sayısı alanı,* sprite pencere öğesi tarafından görüntülenecek tam kare sayısını girmenize olanak sağlayan bir giriş alanıdır. Görüntüler çerçeve listesinde yeniden kullanılabilir, yani her görüntü benzersiz olmalıdır.

Sprite Çerçeve Kimliği alanı, 1 ile Toplam Çerçeve sayısı arasında bir çerçeve dizini seçim değeridir. Bir sprite çerçevesinden bir sonrakine taşımak için bu değeri artırma ve azaltma.

Her sprite çerçevesinin birkaç parametresi vardır. Birincisi Arka Plan İşlemdir. Bu alan, popüler GIF animasyon biçiminin özelliklerini taklit ediyor. Buradaki seçenekler şunlardır:

- İşlem yok; bu, geçerli kare görüntüsünün önceki çerçeve görüntüsü üzerinde çizilir olduğu anlamına gelir.
- İlk Piksel Haritasını Geri Yükle, yani dizin 1 piksel haritası geçerli piksel haritası ve
- Düz Renk Dolgusu, sprite arka planının geçerli çerçeve çizilmeden önce sprite arka plan rengiyle doldurulması anlamına gelir.

Piksel eşlemesi kimliği alanı, daha önce proje kaynaklarına eklenmiş olan piksel haritalarını seçmenize olanak sağlar. Aynı piksel eşleme kimliği birden çok kare için kullanılabilir. Örneğin, sprite animasyonu farklı sprite görüntüleri kullanmak yerine veya yerine görüntünün hareketini (x ve y kaydırma alanlarını kullanarak) kullanabilir.

Alfa değer alanı, piksel haritası çiziminin tamamına uygulanır. Bu alanın etkisi yalnızca 8 bpp renk derinliğinde ve daha yüksekte çalıştırıldı. Alfa değer 0 tamamen saydamdır ve alfa değeri 255 opaktır.

Geçerli piksel eşlemesinin x-kayması ve Frame y-kayması alanları kullanılarak çizileceği hareketli kare içinde bir konum belirtebilirsiniz. Diğer bir deyişle, çizilen her görüntünün, Sprite pencere öğesinin tam boyutu olması gerekmez.

Gecikme süresi, sonraki Sprite çerçevesine geçmeden önce gecikme süresini belirtir. Bu değer, varsayılan Gux/ThreadX Zamanlayıcı yapılandırması için her tick 50 MS 'yi temsil eden Tick 'dır.

Değişiklikleri Sprite çerçevelerini Düzenle iletişim kutusunda kaydettiğinizde, GUıDX Studio, çıkış belirtimleri dosya oluşturmanın bir parçası olarak tüm Çerçeve listesi dizisini üretebilir.

### <a name="assign-a-sprite-widget-with-gif-resource"></a>GIF kaynağı ile bir sprite pencere öğesi atama
Bir GIF kaynağını **pixelmap** kaynak grubuna ekleyebilir ve doğrudan bir GIF kaynağı Sprite pencere öğesine atayabilirsiniz. GIF kaynağı ayarlandıktan sonra, Çerçeve listesi otomatik olarak oluşturulur ve Sprite düzenleme iletişim kutusu aracılığıyla çerçeve listesinin her bir çerçevesini daha fazla düzenleyebilirsiniz:

![GIF kaynağı için Gux Studio Sprite çerçeveleri düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_sprite_gif_frames.jpg)

**Şekil 8,4**