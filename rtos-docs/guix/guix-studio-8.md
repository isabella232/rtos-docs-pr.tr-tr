---
title: Belirli pencere öğesi türlerini düzenlemeyle ilgili notlar
description: Belirli karmaşık pencere öğesi türleri için Düzenle yöntemlerini açıklayan ayrıntılı açıklamalar.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 3194a1b8c8965bf821631a8c34ac5e9961f8c8ff
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827125"
---
# <a name="chapter-8-notes-on-editing-specific-widget-types"></a>Bölüm 8: belirli pencere öğesi türlerini düzenlemeyle ilgili notlar

GUX Studio, kullanıcının uygulama kullanıcı arabirimi ekranlarını oluşturacak olan Gux pencere öğelerini kolayca oluşturmasını ve değiştirmesini sağlar. Bu düzenlemenin çoğu sezgisel ve açıktır. Örneğin, bir pencere öğesini yeniden boyutlandırmak için fare ile pencere öğesini seçebilir ve pencere öğesi kenarlıklarını sürükleyebilirsiniz. Ayrıca, seçilen pencere öğesinin sol/üst/genişlik/yükseklik özellik alanlarına doğrudan yazabilirsiniz.

Bazı pencere öğesi türleri daha gelişmiş bir Düzenle işlemi gerektirir, çünkü bu pencere öğeleri kendi özellik desteğiyle bir bit daha karmaşıktır.

Bu bölümde, bu daha karmaşık pencere öğesi türleri için daha gelişmiş Düzenle özelliklerine ilişkin notlar sağlanmaktadır. Bu notlar, Guix kitaplığı 'nda sunulan pencere öğesi türleriyle birlikte Gux Studio 'nun özellikleri ile ileriye yönelik özellikler olarak genişletilir.

## <a name="rich-text-view"></a>Zengin metin görünümü

Bu pencere öğesi, satır içi metin biçimlendirme kodlarını destekleyen zengin metinleri göstermek için kullanılır. Bu biçimlendirme kodları kalın, italik ve diğer birkaç tane içerir. Başlamak için *proje görünümü* veya *hedef görünümü* ' nden seçilen üst öğeye sağ tıklayın ve zengin metin görünümü pencere öğesi eklemek Için menü **Ekle/metin/zengin metin görünümü** ' nü seçin.

Tüm pencere öğesi türleri tarafından desteklenen standart özellik kümesine ek olarak, zengin metin görünümü pencere öğesi türü ek özellikleri destekler.

### <a name="additional-properties"></a>Ek özellikler

| Özellik | Anlamı |
|----------|---------|
| Metin Hizala | Varsayılan metin hizalaması |
| Normal yazı tipi| Varsayılan metin yazı tipi |
| Kalın yazı tipi  | Kalın olarak etiketlenen metnin metin yazı tipi |
| İtalik yazı tipi| İtalik olarak etiketlenen metnin metin yazı tipi|
| Kalın Italik yazı tipi| Kalın ve italik olarak etiketlenen metnin metin yazı tipi |
| Özel metin kopyalama | Pencere öğesi atanmış metinlerin kendisine ait özel kopyasını tutmadıysanız, denetlenmesi gerekir |
| Boşluk | Pencere öğesi ile görüntülenmiş metin arasındaki kenar boşluğunun piksel cinsinden genişliği. |
| Satır alanı | Metnin iki satırı arasındaki boşluk (piksel cinsinden). |
|||

### <a name="the-rich-text-formatting-codes"></a>Zengin metin biçimlendirme kodları

Metin biçimlendirme için aşağıdaki biçim kodları desteklenir.

|Etiket|Anlamı|
|---|---|
|\<b>\</b> | Metin yazı tipini Kullanıcı tarafından belirtilen kalın yazı tipi KIMLIĞIYLE işle|
|\<i>\</i> | Metin yazı tipini Kullanıcı tarafından belirtilen italik yazı tipi KIMLIĞIYLE işle|
|\<u>\</u> | Altı çizili metni işle|
|\<f GX_FONT_ID>\</f> | Belirtilen yazı tipi KIMLIĞINI kullanarak metni işle. |
|\<c GX_COLOR_ID>\</c> | Belirtilen renk KIMLIĞINI kullanarak metni işle|
|\<hc GX_COLOR_ID>\</hc> | Belirtilen arka plan rengi KIMLIĞINI kullanarak metin işle|
|\<align left/right/center>\</align> | Metin hizalaması ata|
|||

GUX Studio içinden zengin metin dizesini düzenlemenin iki yolu vardır:

- Önerilen ve en basit düzenleme yöntemi olan zengin metin Düzenle iletişim kutusunu kullanın.
- Yukarıdaki tabloda gösterilen biçimlendirme etiketlerini el ile eklemenize olanak tanıyan dize tablosu Düzenleyicisi iletişim kutusunu kullanın.

*Hedef görünümde* zengin metin görünümü pencere öğesi seçildikten sonra, Şekil 8,1 ' de gösterilen zengin metin düzenleme iletişim kutusunu çağırmak Için *Özellikler görünümündeki* **zengin metin Düzenle** düğmesini seçin.

![GUX Studio zengin metin düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_rich_text_dialog.png)

**Şekil 8,1**

Sol bölme zengin metin düzenleme alanıdır. Araç çubuğu simgelerini, ihtiyacınız olan etiketleri eklemeye yardımcı olması için kullanabilirsiniz. Düzenleme alanında herhangi bir metin bloğunu seçin ve ardından gerekli stilleri ve renkleri seçili metin bloğuna uygulamak için araç çubuğu düğmelerini seçin. Zengin metin Düzenle iletişim kutusu, biçimlendirme kodlarını test dizesine eklemenin kolay bir yoludur. Ayrıca, bu etiketleri el ile ekleyebilir veya gerekirse çalışma zamanında oluşturabilirsiniz.

Sağ bölme, metnin hedef görünümde nasıl işleneceğini göstermek için pencere öğesi önizlemesidir. Pencere öğesi önizlemenin arka plan rengi düzeltildi, bu işlem, hedef görünümdeki pencere öğesinin atanan arka plan rengiyle eşleşmeyebilir.

Kaynak KIMLIĞI adları, belirli yazı tipine veya renk kaynaklarına başvurmak için zengin metin halinde kullanılır. Bir fontun veya rengin kaynak adı, zengin metin dizesi tarafından başvurulduktan sonra değiştirilirse, GUıDX Studio zengin metin dizesini kaynak adı değişikliklerini yansıtacak şekilde otomatik olarak güncelleştirir. Diğer taraftan, bir zengin metin pencere öğesi tarafından başvurulan bir yazı tipini veya renk kaynağını silerseniz, silinen kaynak KIMLIĞI adlarını kaldırmak veya değiştirmek için etkilenen zengin metni el ile düzenlemeniz gerekir.

Bu iletişim kutusunda Kaydet düğmesini seçtiğinizde, tanımladığınız zengin metin dizesi proje dizesi tablosuna eklenir.

## <a name="string-scroll-wheel"></a>Dize kaydırma tekerleği

Bir dize kaydırma tekerleği pencere öğesi dizeler dizisinin görüntülenmesini destekler. Bu dizeler dinamik olarak atanabilir veya uygulamanın birden çok dili desteklemesi durumunda, atanan dizelerin etkin dize tablosundan çekbir şekilde atanabilmesini sağlayabilir.

Dize kaydırma tekerleği pencere öğesi bir dizi dizeyi destekler. Şekil 8,2 ' de gösterilen dize kaydırma tekerleği düzenleme iletişim kutusu, kullanıcının bu dize dizisini atamasına izin vermek için verilmiştir.

![GUX Studio dize kaydırma tekerleği düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/string_scroll_wheel_edit.png)

**Şekil 8,2**

Bu iletişim kutusunu çağırmak için *hedef görünüm* veya *proje görünümü* içinde bir dize kaydırma tekerleği pencere öğesi seçin. Bu pencere öğesi türü seçildikten sonra, *Özellikler Görünümü* **dizeleri Düzenle** düğmesi içerecektir. Dize kaydırma tekerleği düzenleme iletişim kutusunu çağırmak için bu düğmeyi seçin.

Her metin dizini için bir dize atamak üzere, açılan listeden bir dize KIMLIĞI seçebilir veya sağdaki metin alanına yeni bir dize değeri yazabilirsiniz. Yaptığınız değişikliklerle işiniz bittiğinde, tüm yeni veya değiştirilmiş dizeler etkin dize tablosuna kaydedilir.

## <a name="sprite"></a>Öğesini

Bir sprite pencere öğesi, bir animasyon efekti sağlamak üzere bir görüntü dizisini göstermek için kullanılır. Bir sprite pencere öğesi, çerçevedeki her bir görüntüye uygulanan bir resim kimlikleri ve benzersiz parametreler dizisi olan bir çerçeve listesi gerektirir. Hareketli pencere öğesi için bu çerçeve listesini oluşturmak için Şekil 8,3 ' de gösterilen Sprite çerçevelerini Düzenle iletişim kutusu sağlanır:

![GUX Studio Sprite çerçeveleri düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_sprite_frames.png)

**Şekil 8,3**

Bu iletişim kutusunu çağırmak için *hedef görünüm* veya *proje görünümü* içinde bir sprite pencere öğesi seçin. Bu pencere öğesi türü seçildikten sonra, *Özellikler Görünümü* bir **Framelist düğmesini Düzenle** düğmesi içerecektir. Dize kaydırma tekerleği düzenleme iletişim kutusunu çağırmak için bu düğmeyi seçin.

*Toplam Sprite çerçevesi sayısı* alanı, Sprite pencere öğesi tarafından görüntülenecek toplam çerçeve sayısını girmenize olanak sağlayan bir giriş alanıdır. Görüntüler çerçeve listesi içinde yeniden kullanılabilir, yani her görüntü benzersiz olmalıdır.

Sprite çerçeve KIMLIĞI alanı, 1 ' den toplam çerçeve sayısıyla değişen bir çerçeve dizini seçim değeridir. Bir sprite çerçevesinin yanına ilerlemek için bu değeri artırın ve azaltır.

Her Sprite çerçevesinin çeşitli parametreleri vardır. Birincisi, arka plan Işlemidir. Bu alan popüler GIF animasyon biçiminin yeteneklerini taklit eder. Buradaki seçimler şunları içerir:

- Işlem yok, bu, geçerli çerçeve görüntüsünün önceki çerçeve görüntüsünün üzerine çizildiği anlamına gelir.
- Ilk piksel eşlemesini geri yükle, yani 1 piksel eşlemesinin geçerli piksel eşlemesinden önce çizildiği ve
- Düz renk dolgusu, bu, Sprite arka planının, geçerli çerçevenin çizilmeden önce Sprite arka plan rengiyle doldurulduğu anlamına gelir.

Pixel-Map KIMLIĞI alanı, daha önce proje kaynaklarına eklenmiş herhangi bir piksel eşlemesini seçmenizi sağlar. Aynı piksel eşleme KIMLIĞI birden çok çerçeve için kullanılabilir. Örneğin, Sprite animasyonunuz, farklı Sprite görüntülerini kullanmanın yanı sıra görüntünün hareketini (x ve y boşluğu alanlarını kullanarak) kullanabilir.

Alfa değeri alanı piksel eşleme çiziminin tamamına uygulanır. Bu alanın yalnızca 8 BPP renk derinliği ve üzeri sürümlerde çalıştığı bir etkisi vardır. Alfa değeri 0 tamamen saydamdır ve alfa değeri 255 donuk olur.

Geçerli piksel eşlemesinin x-kayması ve Frame y-kayması alanları kullanılarak çizileceği hareketli kare içinde bir konum belirtebilirsiniz. Diğer bir deyişle, çizilen her görüntünün, Sprite pencere öğesinin tam boyutu olması gerekmez.

Gecikme süresi, sonraki Sprite çerçevesine geçmeden önce gecikme süresini belirtir. Bu değer, varsayılan Gux/ThreadX Zamanlayıcı yapılandırması için her tick 50 MS 'yi temsil eden Tick 'dır.

Değişiklikleri Sprite çerçevelerini Düzenle iletişim kutusunda kaydettiğinizde, GUıDX Studio, çıkış belirtimleri dosya oluşturmanın bir parçası olarak tüm Çerçeve listesi dizisini üretebilir.
