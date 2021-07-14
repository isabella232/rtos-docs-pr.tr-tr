---
title: GUIX Azure RTOS GUIX Studio'Azure RTOS anlama
description: Azure RTOS GUIX, ekli sistem geliştiricilerinin ihtiyaçlarını karşılamak için oluşturulmuş profesyonel kaliteli bir pakettir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0a6ac2c7a76893d516b9beae9b893c9764de60ba
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754939"
---
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a>GUIX Azure RTOS GUIX Studio'Azure RTOS genel bakış

Azure GUIX embedded GUI, Microsoft'un derinden eklenmiş, gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanmış gelişmiş, endüstriyel sınıf GUI çözümüdür. Microsoft ayrıca, geliştiricilerin GUI'lerini masaüstünde tasarlamalarına ve daha sonra hedefe aktarılamayacak Azure RTOS GUIX ekli GUI kodu oluşturmalarına olanak sağlayan Azure RTOS GUIX Studio adlı tam özellikli WYSIWYG masaüstü tasarım aracı sağlar. Azure RTOS GUIX, Azure RTOS ThreadX RTOS ile tamamen tümleşiktir ve Azure RTOS ThreadX tarafından desteklenen birçok işlemcide kullanılabilir. Bunların hepsi son derece küçük bir ayak izi, hızlı yürütme ve üstün kullanım kolaylığı ile birlikte, Azure RTOS GUIX'i kullanıcı arabirimi gerektiren en zorlu tümleşik IoT uygulamaları için ideal seçenek yapın. 

## <a name="azure-rtos-guix-api"></a>Azure RTOS GUIX API'si

### <a name="powerful-apis"></a>Güçlü API'ler

* Gerektiğinde doğrudan tuval çizimi için tam destek
* GUIX Studio tarafından Azure RTOS basit etkileşim kurma
* Çizgi, dikdörtgen, çokgen vb. için API'ler.
* Daire, yay, pasta, chord, üç nokta gibi API'ler
* Metin çizme ve konumlandırma api'leri
* Diğer ad koruma, doku dolguları ve düz dolgular
* Ekranlar ve pencere öğeleri oluşturmaya ve bu öğeleri değiştiren API'ler

### <a name="azure-rtos-guix-studio-generated-files"></a>Azure RTOS GUIX Studio Tarafından Oluşturulan Dosyalar

* Otomatik olarak oluşturulan ANSI C kaynak dosyaları
* Uygulama yazılımını düzen ayrıntılarından uzaktır
* Ui tasarımı için gereken yazı tiplerini ve görüntüleri içerir
* Uygulama koduyla derlenmiş oluşturulan dosyalar
* Ekran düzeni, uygulama mantığını etkilemeden güncelleştirilebilir
* Kaynak kimlikleri dil ve tema bağımsızlığı oluşturma
* Kullanıcı tarafından sağlanan özel çizim ve olay işleme işlevleri

### <a name="widget-library"></a>Pencere öğesi kitaplığı

* Ortak arabirim öğelerinin önceden tanımlanmış ancak özelleştirilebilir kümesi
* Son derece küçük, sıkıştırılmış ve verimli
* Kitaplık düğme, ölçer, liste, pencere, kaydırma, kaydırıcı, ilerleme çubuğu, istemi ve çok daha fazlasını içerir
* Tamamen özelleştirilebilir çizim ve görünüm
* Tamamen özelleştirilebilir işlem ve olay işleme
* Yalnızca kullanılan pencere öğeleri uygulama yazılımıyla bağlantılıdır

### <a name="math-and-utilities"></a>Matematik ve yardımcı programlar

* Sin, cos, arcsin, arccos, tangent, square root işlevleri
* Ekran bölgelerini işleye işlevler
* Sistem yapılandırması ve başlatma
* Bellek havuzu tanımı (isteğe bağlı)
* Zamanlayıcı Yönetimi
* Animasyon Yönetimi
* Kirli liste bakımı

### <a name="image-processing"></a>Görüntü işleme

* Jpeg ve png görüntülerinin çalışma zamanı kodunu çözme işlevleri
* Dithering ve renk alanı dönüştürme uygulama
* Görüntü döndürme
* Görüntü ölçeklendirme
* Görüntü karıştırma

### <a name="event-processing"></a>Olay işleme

* Boştayken GUIX Azure RTOS iş parçacığını otomatik olarak askıya alır
* Kullanıcı arabirimi tasarımında popüler olan olay odaklı programlama modeli
* GuiX çizim iş parçacığından Azure RTOS sürücülerini zorlar
* Olay gönderme ve alma işlevleri
* GuiX pencere öğesi türleri için tüm Azure RTOS önceden tanımlanmış olay türleri
* Desteklenen kullanıcı tanımlı özel olaylar

### <a name="canvas-processing"></a>Tuval işleme

* Kırpma ve Z Düzeni bakımı
* Donanım ayrıntılarından pencere öğesi kitaplığını sağlar
* Uygulamayı donanım ayrıntılarından uzaktır
* Kirli alanların otomatik arka plan yenilemesi
* Katmanlama ve karıştırma desteğine sahip birden çok tuval
* Doğrudan uygulama yazılımı tarafından çağrılabilir

### <a name="input-device-drivers"></a>Giriş cihazı sürücülerini

* Donanıma özgü destek, Azure RTOS ayrıntılarından uzak GUIX ve uygulama
* Touch, Cap Touch ve tuş takımı desteği
* GUIX olay kuyruğuna Azure RTOS giriş olayları

### <a name="display-drivers"></a>Sürücüleri görüntüleme

* Donanıma özgü destek
* Tüm renk derinliği ve biçimleri için sağlanan genel sürücüler
* Kullanılabilir grafik hızlandırıcılarını kullanmak için özelleştirilmiş

### <a name="target-hardware"></a>Hedef donanım

* Grafik çıkış özellikli neredeyse tüm donanımlar GUIX ile uyumludur
* Desteklenen birden çok fiziksel ekran
* Minimum RAM ve Flash gereksinimleri

## <a name="create-elegant-user-interfaces"></a>Şık Kullanıcı Arabirimleri Oluşturma

Azure RTOS GUIX ve Azure RTOS GUIX Studio, benzersiz şekilde zarif kullanıcı arabirimleri oluşturmak için gereken tüm özellikleri sağlar. Standart Azure RTOS GUIX paketi tıbbi cihaz başvurusu, akıllı saat başvurusu, ev otomasyonu başvurusu, endüstriyel denetim başvurusu, otomobil başvurusu ve çeşitli sprite ve animasyon örnekleri gibi çeşitli örnek kullanıcı arabirimlerini içerir. Lütfen aşağıda gösterilen başvuru örneklerine tıklayın.

### <a name="home-automation"></a>Ev Otomasyonu

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a>Tıbbi

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a>Tüketici

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a>Beyaz Ürünler

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a>Otomotiv

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a>Endüstriyel

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

Her Azure RTOS GUIX başvurusu, başvuru Azure RTOS tüm grafik öğelerini tanımlayan ilgili bir GUIX Studio projesine sahiptir. Başvuru tasarımını değiştirmek kolaydır. İlgili GUIX Azure RTOS ilgili dosyayı açın, istediğiniz değişiklikleri yapın, projeyi kaydedin ve ardından *Project.*

GUIX için C kodunu oluşturmak için Tüm Çıkış Azure RTOS oluştur. Ardından, değiştirilmiş başvuru tasarımını gözlemlemek için hedef uygulamayı yeniden oluşturmanız ve çalıştırmanız gerekir.

### <a name="guix-memory-footprint"></a>GUIX Bellek ayak izi

Azure RTOS GUIX,tuval için gereken bellek dahil olmak üzere temel destek için 13,2 KB FLASH ve 4 KB RAM olmak üzere oldukça küçük bir ayak izine sahip.

İç GRAM ve kendi kendine yenileme teknolojisine sahip bir ekran için tuval belleği gerekmez. Ancak, çizim performansını geliştirmek için veya ekranda yerel GRAM kullanmaan bir görüntü yapılandırması için, uygulama tarafından bir tuval bellek alanı tanımlanır.

Tuval belleği gereksinimleri, tuval boyutunun yanı sıra renk derinliğine sahip bir işlevdir ve formülle tanımlanır:

<i>Tuval RAM'i (bayt) = (x * y * (bpp/8))</i>

Burada "x" ve "y" tuvalin boyutlarıdır (display).

Çoğu uygulama, GUIX kitaplığı depolama gereksinimlerinin temel gereksinimlerine dahil Azure RTOS grafik kaynaklarını da kullanır. Bu kaynaklar yazı tiplerini, grafik simgelerini (piksel haritaları) ve statik dizeleri içerir. Bu veriler sabit bellek bölümünde (flash) depolanmış olabilir.

Azure RTOS GUIX hem yazı tipi hem de piksel haritası verilerinde RLE sıkıştırmasını desteklediği için bu bellek alanı boyutu, kullanılan benzersiz yazı tiplerinin sayısı ve boyutu, kullanılan grafik simgelerinin sayısı ve boyutu, çıkış rengi biçimi ve her kaynağın sıkıştırılmış veri kullanıp kullanmama gibi çeşitli faktörlere bağlıdır. Her kaynağın depolama gereksinimleri Azure RTOS GUIX Studio uygulamasında görüntülenir ve bu da kullanıcının uygulama kaynakları tarafından tüketilen flash bellek miktarını izlemesi ve izlemesi için kullanılabilir.

ThreadX Azure RTOS de olduğu gibi GUIX Azure RTOS nin boyutu da uygulama tarafından gerçekten kullanılan hizmetlere göre otomatik olarak ölçeklendirilir. Bu, karmaşık yapılandırma ve derleme parametrelerine olan ihtiyacı neredeyse ortadan kaldırarak geliştirici için işleri kolaylaştırır.

#### <a name="simple-easy-to-use"></a>Basit, kullanımı kolay

Azure RTOS Gux kullanımı çok basittir ve Azure RTOS Gux Studio, geliştiricilerin masaüstünü görsel olarak tasarlamasına ve gerçek hedefte çalışan C kodu oluşturmasına izin vererek daha da kolay hale gelir. Uygulamalar daha sonra kendi özel olay işleme ve çizim işlevlerini ekleyerek GUI 'sini tamamlamalarını sağlayabilir.

Azure RTOS Gux API 'SI kullanımı basittir. Azure RTOS Gux API 'SI sezgisel ve yüksek işlevselliğe sahiptir. API adları, gerçek sözcüklerden oluşur ve "alfabe adı" ve/veya diğer dosya sistemi ürünlerinde ortak olan çok sayıda kısaltılmış isimlerdir. Tüm Azure RTOS Gux API 'Lerinin önde bir *gx_* vardır ve bir ad fiil adlandırma kuralını takip edin. Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır. Örneğin, bir pencere öğesi denetim bloğunu başlatacak tüm API 'Ler &lt; widget_type &gt; _Create olarak adlandırılır ve her pencere öğesi türü için oluşturma işlevi parametreleri her zaman aynı sırada tanımlanır.

### <a name="comprehensive-set-of-built-in-widgets"></a>Kapsamlı yerleşik pencere öğeleri kümesi

* Azure RTOS Gux, aşağıdakiler dahil olmak üzere zengin bir yerleşik pencere öğesi kümesi sağlar:
* Accordion menüsü
* Düğme
* Onay kutusu
* Dairesel ölçer
* Açılan liste
* Yatay liste
* Yatay kaydırma çubuğu penceresi
* Simge
* Simge düğmesi
* Çizgi grafik
* Menü
* Çok satırlı metin düğmesi
* Çok satırlı metin girişi
* Çok satırlı metin görünümü
* Sayısal pixelmap Istemi
* Sayısal Istem
* Sayısal kaydırma tekerleği
* Pixelmap düğmesi
* Pixelmap Istemi
* Pixelmap kaydırıcısı
* Pixelmap Sprite
* İlerleme Çubuğu
* İstem
* Radyal Ilerleme çubuğu
* Radyo Düğmesi
* Tekerleği kaydır
* Tek satırlık metin girişi
* Kaydırıcı
* Dize kaydırma tekerleği
* Metin düğmesi
* Ağacı Görünümü
* Dikey Liste
* Dikey kaydırma çubuğu

Uygulamanın kendi müşteri pencere öğelerini de oluşturması kolay bir işlemdir.

### <a name="complete-low-level-drawing-api"></a>Düşük düzey çizim API 'sini doldurun

Azure RTOS Gux sağlam bir tuval çizimi API 'SI sağlar ve uygulamanın karmaşık grafik şekillerini işlemesine izin verir.

Tüm işlevler, yüksek renk derinliği hedefleri üzerinde kenar yumuşatmasını destekler ve Solid ve pixelmap örüntüsünün dolgusu dahil olmak üzere tüm şekiller ana hatlarıyla doldurulabilir. Tüm çizim temelleri 16 BPP ve daha yüksek renk derinliğinde çalışırken fırça Alpha 'ı destekler. Çizim işlevleri şunları içerir:

* Yay çiz
* Daire çiz
* Çizgi çizme
* Pasta çiz
* Pixelmap Blend
* Pixelmap kutucuğu
* Çokgen Çiz
* Metin çizme
* Chun çiz
* Elips çizme
* Piksel çizimi
* Pixelmap çiz
* Pixelmap döndürme
* Dikdörtgen çiz
* Metin Blend

### <a name="default-free-fonts-and-easy-to-add-more"></a>Varsayılan ücretsiz yazı tipleri ve ekleme daha kolay

Azure RTOS Gux, ücretsiz bir TrueType yazı tipi kümesi sağlar. Geliştiriciler, istediğiniz gibi ek TrueType yazı tipleri ekleyebilir.

Azure RTOS Gux yazı tipi biçimi, 8bpp Anti-düzgünleştirme, 4bpp düzgünleştirme ve 1bpp tek renkli yazı tiplerini destekler. En fazla kaynak sınırlamalı uygulamalar için, Azure RTOS Gux önceden TrueType yazı tiplerini Gux Studio Desktop aracımızı kullanarak sıkıştırılmış bir bit eşlem biçimine göre işler.

### <a name="custom-jpg-and-png-decoder-implementation"></a>Özel JPG ve PNG kod çözücü uygulama

Özel JPG ve PNG kod çözücü uygulama JPG ve PNG dosya kod çözücü uygulama. Bu uygulama, Azure RTOS GUıDX uyumlu pixelmap biçim görüntülerinin renk alanı dönüştürmeyi, titreme ve çalışma zamanı oluşturmayı destekler.

### <a name="extensive-display-and-touchscreen-support"></a>Kapsamlı ekran ve dokunmatik ekran desteği

Azure RTOS Gux, 1bpp tek renkli, 8 BPP palet, 8 BPP 3:3:2 biçimi de dahil olmak üzere neredeyse tüm renk biçimleri için genel görüntüleme sürücüleri sağlar

16 BPP 565 RGB biçimi, 16 BPP 4:4:4:4 biçimi, 32 BPP x:r: g:b biçimi ve 32 BPP a:r: g:b biçimi. Ayrıca, Azure RTOS Gux, en popüler LCD denetleyiciler ve donanım hızlandırıcılarının (ST Kmesanat, Renesas Synergy, vb.) çoğuyla tümleşiktir.

Azure RTOS Gux, dokunmatik ekranı (hareket desteği dahil), kalemi ve sanal klavye girişi cihazlarını tam olarak destekler.

### <a name="azure-rtos-guix-studio-desktop-wysiwyg-tool"></a>Azure RTOS Gux Studio masaüstü WYSıWYG aracı

Azure RTOS Gux Studio, kullanıcının GUI ekranlarını oluşturmak için kullanılan grafik öğelerini sürükleyip bırakması için tam bir WYSıWYG ekranı tasarım ortamı sağlar. Azure RTOS Gux Studio otomatik olarak Azure RTOS Gux kitaplığı ile uyumlu C kodu oluşturur ve hedefte derlenmeye ve çalıştırılmaya çalışır. Geliştiriciler, tümleşik Azure RTOS Gux Studio yazı tipi oluşturma aracı 'nı kullanarak bir uygulama içinde kullanılmak üzere önceden oluşturulmuş yazı tiplerini oluşturabilir. Yazı tipleri, tek renkli veya kenar yumuşatma uygulanmış biçimlerde oluşturulabilir ve hedefte yer kazanmak için iyileştirilmiştir. Yazı tiplerinde, çok dilli uygulamalar için Unicode karakterler de dahil olmak üzere herhangi bir karakter kümesi bulunabilir.

<img alt="Diagram of SGS-TUV Saar certification logo" class="alignnone size-full wp-image-1500" height="341" sizes="(max-width: 535px) 100vw, 535px" src="./media/overview/studio_screen_shot.png"/>

Azure RTOS Gux Studio, hedef sistemde kullanılmak üzere sıkıştırılan Azure RTOS Gux pixelmaps 'e dönüştürme ile PNG veya JPG dosyalarından grafiklerin içeri aktarılacağını kolaylaştırır. Azure RTOS Gux pencere öğesi türlerinin birçoğu, özel bir görünüm ve kullanım için Kullanıcı grafiklerini içerecek şekilde tasarlanmıştır. Ayrıca, Azure RTOS Gux Studio, Azure RTOS Gux pencere öğeleri tarafından kullanılan varsayılan renklerin ve çizim stillerinin özelleştirilmesine olanak tanıyarak, geliştiricilerin Azure RTOS Gux 'in görünüşünü çok kolay bir şekilde ayarlamasına olanak tanır. Uygulama dizelerinin oluşturulması ve bakımı, Azure RTOS Gux Studio 'nun başka bir yerleşik tesisinden oluşur. Bu, geliştiricilerin geliştirme için bir dil kullanarak bir uygulama tasarlamasını ve ürün yayımlandıktan sonra hızlı ve kolay bir şekilde ek dil desteği eklemesini sağlar. Azure RTOS Gux Studio ortamındaki bir BILGISAYAR masaüstünde, GUI kavramlarının ve ekran akışlarının test edilmesine ve ekran geçişlerinin ve animasyonların gözlemlerine yönelik bir hızlı ve kolay bir şekilde oluşturulmasına ve bu uygulamanın tamamına yönelik kapsamlı bir Azure RTOS Gux uygulaması çalıştırılabilir. İşlem tamamlandığında tasarım, hedef Ready C veri yapıları olarak verilebildiğinden, Azure RTOS Gux ve Azure RTOS ThreadX kitaplıklarıyla derlenmeye ve bunlarla bağlantı kurulabilir.

Azure RTOS Gux ve Azure RTOS Gux Studio birden çok kaynak teması destekler ve bir uygulamanın çalışma zamanında kolayca yeniden başlatılmasına izin verir. Yazı tipleri, renkler ve pixelmaps, tek bir basit API ile çalışma zamanında değiştirilebilir.

GUX Studio hakkında daha fazla bilgi

### <a name="complete-win32-simulation"></a>Win32 simülasyonu

Azure rtos gux, hedef panoda çalışan tam olarak aynı çizim kitaplığını kullanarak Windows bir bilgisayarda çalışır. Azure RTOS Gux ile, bılgısayarda GUI uygulaması oluşturup çalıştırabilir ve hata ayıklama, hızlı prototipleme, tanıtım ve WYSıWYG hedefi işlemi için Hedefinizdeki aynı uygulama kodunu kullanabilirsiniz.

### <a name="advanced-technology"></a>Gelişmiş teknoloji

* Azure RTOS Gux 'in gelişmiş teknolojisi şunları içerir:
* Alfa karıştırma
* Kenar yumuşatma
* Otomatik ölçeklendirme
* Bit eşlem sıkıştırması
* Tuval karışımı
* Özel pencere öğesi desteği
* Ertelenmiş çizim desteği
* Titreme desteği
* Endian bağımsız programlama
* Donanım hızlandırıcısı desteği
* Çok dilli destek ve UTF-8 kodlaması
* Birden çok görüntü ve tuval desteği
* En iyi duruma getirilmiş kırpma, çizim ve olay işleme
* Çalışma zamanı JPEG ve PNG kod çözücü
* Kaplama ve Temalar
* Tek renkli 32 bitlik gerçek renk ile alfa grafik biçimlerini destekler
* Geçişler, sprites ve animasyon desteği
* Win32 simülasyonu
* Viewports ve Z düzeninde bakım dahil olmak üzere pencere yönetimi
