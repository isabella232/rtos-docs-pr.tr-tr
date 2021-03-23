---
title: Azure RTOS Gux ve Azure RTOS Gux Studio 'Yu anlama
description: Azure RTOS Gux, katıştırılmış sistem geliştiricilerin ihtiyaçlarını karşılamak için oluşturulmuş bir profesyonel kalite paketidir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0d0ff37784673f851ab918e20b255d19ddf98b0f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827094"
---
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a>Azure RTOS Gux ve Azure RTOS Gux Studio 'ya genel bakış

Azure Gux Embedded GUI, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf GUI çözümüdür. Microsoft ayrıca, Azure RTOS Gux Studio adlı tam özellikli bir WYSıWYG masaüstü tasarım aracı sağlar. bu sayede, geliştiricilerin masaüstündeki GUI 'sini tasarlamalarını ve hedefe aktarılabilecek Azure RTOS Gux Embedded GUI kodunu oluşturmasını sağlar. Azure RTOS Gux Azure RTOS ThreadX RTOS ile tamamen tümleşiktir ve Azure RTOS ThreadX tarafından desteklenen işlemcilerin birçoğu için kullanılabilir. Bunun hepsi son derece küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla, Azure RTOS Gux 'i bir kullanıcı arabirimi gerektiren en zorlu eklenmiş IoT uygulamalarına yönelik ideal seçim haline getirir. 

## <a name="azure-rtos-guix-api"></a>Azure RTOS Gux API 'SI

### <a name="intuitive-and-consistent-api"></a>Sezgisel ve tutarlı API

* İsim-fiil adlandırma kuralı

* Tüm API 'Lerde Azure RTOS Gux olarak kolayca tanımlanabilmesi için önde gelen *gx_* vardır

* Olay odaklı programlama modeli (API)

* Gerektiğinde doğrudan tuval çizimi için tam destek

* Azure RTOS Gux Studio tarafından üretilen kodla kolay bir şekilde etkileşim kurma

* Çizgi, dikdörtgen, çokgen vb. için API 'Ler

* Daire, yay, pasta, kii, elips, vb. için API 'Ler.

* Metin çizme ve konumlandırma için API 'Ler

* Kenar yumuşatma, doku dolguları ve düz dolgular

* Ekranları ve pencere öğelerini oluşturmak ve yeniden oluşturmak için API 'Ler

### <a name="azure-rtos-guix-studio-generated-files"></a>Azure RTOS Gux Studio tarafından oluşturulan dosyalar

* Otomatik olarak oluşturulan ANSI C kaynak dosyaları

* Düzen ayrıntılarından uygulama yazılımını yalıtılmış olarak

* Kullanıcı arabirimi tasarımı için gereken yazı tiplerini ve görüntüleri içerir

* Uygulama koduyla derlenen oluşturulan dosyalar

* Ekran düzeni, uygulama mantığını etkilemeden güncelleştirilebilen

* Kaynak kimlikleri dil ve tema bağımsızlık oluşturma

* Kullanıcı tarafından sağlanan özel çizim ve olay işleme işlevleri

### <a name="widget-library"></a>Pencere öğesi kitaplığı

* Önceden tanımlanmış ancak özelleştirilebilir ortak arabirim öğeleri kümesi

* Son derece küçük, kompakt ve verimli

* Kitaplık, düğme, ölçer, liste, pencere, kaydırma, kaydırıcı, ilerleme çubuğu, istem ve çok daha fazlasını içerir

* Tamamen özelleştirilebilir çizim ve görünüm

* Tamamen özelleştirilebilir işlem ve olay işleme

* Yalnızca kullanılan pencere öğeleri uygulama yazılımıyla bağlantılı

### <a name="math-and-utilities"></a>Matematik ve yardımcı programlar

* Sin, cos, Arcsin, arccos, tanjant, kare kök işlevleri

* Ekran bölgelerini düzenleme işlevleri

* Sistem Yapılandırması ve başlangıç

* Bellek havuzu tanımı (isteğe bağlı)

* Zamanlayıcı yönetimi

* Animasyon yönetimi

* Kirli liste Bakımı

### <a name="image-processing"></a>Görüntü işleme

* JPEG ve PNG görüntülerinin çalışma zamanı kodunu çözme işlevleri

* Titreme ve renk alanı dönüştürmeyi Uygula

* Görüntü döndürme

* Görüntü ölçeklendirme

* Görüntü karıştırma

### <a name="event-processing"></a>Olay işleme

* Boştayken Azure RTOS Gux iş parçacığını otomatik olarak askıya alır

* UI tasarımında popüler olay odaklı programlama modeli

* Azure RTOS Gux çizim iş parçacığından giriş sürücülerini yalıtılmış olarak

* Olayları gönderme ve alma işlevleri

* Tüm Azure RTOS Gux pencere öğesi türleri için önceden tanımlanmış olay türleri

* Kullanıcı tanımlı özel olaylar destekleniyor

### <a name="canvas-processing"></a>Tuval işleme

* Kırpma ve Z düzeninde bakım

* Donanım ayrıntılarından pencere öğesi kitaplığını yalıtılmış olarak

* Uygulamanın donanım ayrıntılarından yalıtılmış olması

* Kirli alanların otomatik arka plan yenilemesi

* Katmanlama ve karıştırma desteği ile birden çok canvaya

* Uygulama yazılımı tarafından doğrudan çağrılabilir

### <a name="input-device-drivers"></a>Giriş cihazı sürücüleri

* Donanıma özel destek, Azure RTOS Gux ve donanım ayrıntılarından yalıtılmış uygulama

* Dirensel dokunma, uç Touch ve tuş takımı destekleniyor

* Azure RTOS Gux olay kuyruğuna geçirilen giriş olayları

### <a name="display-drivers"></a>Görüntü sürücüleri

* Donanıma özgü destek

* Tüm renk derinliği ve biçimleri için sunulan genel sürücüler

* Kullanılabilir grafik hızlandırıcılarını kullanacak şekilde özelleştirilmiş

### <a name="target-hardware"></a>Hedef donanım

* Grafik çıkışı yapabilen neredeyse tüm donanımlar, GUıDX ile uyumludur

* Birden çok fiziksel görüntüleme destekleniyor

* En az RAM ve Flash gereksinimleri

## <a name="create-elegant-user-interfaces"></a>Zarif Kullanıcı arabirimleri oluşturma

Azure RTOS Gux ve Azure RTOS Gux Studio, benzersiz şekilde zarif Kullanıcı arabirimleri oluşturmak için gereken tüm özellikleri sağlar. Standart Azure RTOS Gux paketi, tıbbi cihaz başvurusu, akıllı bir izleme başvurusu, bir giriş otomasyon başvurusu, endüstriyel denetim başvurusu, bir otomatik Molem başvurusu ve çeşitli sprite ve animasyon örnekleri dahil olmak üzere çeşitli örnek kullanıcı arabirimlerini içerir. Lütfen aşağıda gösterilen başvuru örneklerine tıklayın.

### <a name="home-automation"></a>Ana Otomasyon

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a>Birinin

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a>Tüketici

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a>Beyaz mallar

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a>Otomotiv

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a>Sanayi

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

Her Azure RTOS Gux başvurusunda, başvuru tasarımının tüm grafik öğelerini tanımlayan karşılık gelen bir Azure RTOS Gux Studio projesi bulunur. Başvuru tasarımını değiştirmek kolaydır. Yalnızca ilgili Azure RTOS Gux projesini açın, istenen değişiklikleri yapın, projeyi kaydedin ve *Proje*' yi seçin.

Azure RTOS Gux için C kodu oluşturmak üzere tüm çıkış dosyalarını oluşturun. Ardından hedef uygulamayı yeniden oluşturup değiştirilen başvuru tasarımını gözlemleyecek şekilde çalıştırın.

### <a name="small-footprint"></a>Küçük ayak izi

Azure RTOS Gux, bir tuval için gereken belleği dahil etmez ve temel destek için 13.2 KB 'lık FLASH ve 4KB RAM 'in daha az küçük bir ayak izine sahiptir.

Dahili GRAM ve kendi kendini yenileme teknolojisine sahip bir ekran için tuval belleği gerekli değildir. Ancak, çizim performansını artırmak veya görüntüleme için yerel olarak kullanılan bir görüntüleme yapılandırması için, uygulama tarafından bir tuval bellek alanı tanımlanmıştır.

Tuval bellek gereksinimleri, Tuval boyutunun ve renk derinliğinin bir işlevidir ve formül tarafından tanımlanır:

<i>Tuval RAM (bayt) = (x * y * (BPP/8))</i>

Burada "x" ve "y", tuvalin boyutlarıdır (görüntü).

Çoğu uygulama, temel Azure RTOS Gux kitaplığı depolama gereksinimlerine dahil olmayan grafik kaynakları da kullanır. Bu kaynaklar, yazı tiplerini, grafik simgelerini (pixelmaps) ve statik dizeleri içerir. Bu veriler, const bellek bölümünde (örn. FLASH) depolanabilir.

Bu bellek alanının boyutu, kullanılan benzersiz yazı tiplerinin sayısını ve boyutunu, kullanılan grafik simgelerinin sayısını ve boyutunu, çıkış rengi biçimini ve her bir kaynağın sıkıştırılmış verileri kullanıp kullanmadığını, her iki yazı tipinin ve pixelmap verilerinin RLE sıkıştırmasını desteklediğinden bu yana bir dizi etkene bağımlıdır. Her kaynak için depolama gereksinimleri, Azure RTOS Gux Studio uygulamasında görüntülenir ve kullanıcının uygulama kaynakları tarafından tüketilen Flash bellek miktarını izlemesine ve izlemesine olanak sağlar.

Azure RTOS ThreadX gibi Azure RTOS Gux boyutu, uygulama tarafından gerçekten kullanılan hizmetlere göre otomatik olarak ölçeklendirilir. Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.

### <a name="fast-execution"></a>Hızlı yürütme

Azure RTOS Gux, özel olarak C dilinde yazılır ve hız için tasarlanmıştır. Azure RTOS Gux, en az iç işlev çağrısı katmanlanmıştır.

Ayrıca, Azure RTOS Gux, iyileştirilmiş kırpma, çizim ve olay işleme sağlar. Tüm bu ve genel performansa dayalı bir tasarım felsesı, Azure RTOS Gux 'in olası en hızlı performansı elde etmenize yardımcı olur.

### <a name="pre-certified--by-tuv-to-many-safety-standards"></a>TUV tarafından birçok güvenlik standartlarına önceden sertifikalı

Azure RTOS Gux, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW güvenlik sınıfı C, ISO 26262 ASIL D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir. Sertifika, Azure RTOS Gux 'in, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımların geliştirilmesinde kullanılabileceğini onaylar. Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir. Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenlik düzeyini güvence altına almak için kullanılır.

<img alt="SGS-TUV Saar" class="img-responsive" src="https://rtos.com/wp-content/uploads/2017/10/partener-logo-sgs-tuv-saar-2.png"/>

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

Azure RTOS Gux, hedef panoda çalışan tam olarak aynı çizim kitaplığını kullanarak bir Windows bilgisayarında çalışır. Azure RTOS Gux ile, bılgısayarda GUI uygulaması oluşturup çalıştırabilir ve hata ayıklama, hızlı prototipleme, tanıtım ve WYSıWYG hedefi işlemi için Hedefinizdeki aynı uygulama kodunu kullanabilirsiniz.

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

### <a name="fastest-time-to-market"></a>En hızlı pazar süresi

Azure RTOS Gux 'i yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır. Azure RTOS Gux Studio, yerleşik GUI tasarımının ve uygulamasının daha kolay yapılmasına de yardımcı olur. Sonuç olarak, Azure RTOS Gux, katıştırılmış IoT cihazları için en popüler GUI çözümlerinden biridir. Tutarlı Pazar süresi avantajımız, şu şekilde oluşturulmuştur:

* Kalite belgeleri: lütfen [Azure RTOS Gux Kullanıcı Kılavuzumuzu](about-guix.md) gözden geçirin ve kendiniz görün!

* Tüm kaynak kodu kullanılabilirliği

* Kullanımı kolay API

* Kapsamlı ve gelişmiş özellik kümesi

## <a name="one-simple-license"></a>Tek bir basit lisans

Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.

## <a name="full-highest-quality-source-code"></a>Tam, en yüksek kaliteli kaynak kodu

Yıl boyunca, Azure RTOS NetX kaynak kodu, çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı. Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.

## <a name="supports-most-popular-architectures"></a>Popüler mimarilerin çoğunu destekler

Azure RTOS Gux, en popüler 32/64 bit mikro işlemciler, kullanıma hazır, tam olarak sınanmış ve aşağıdakiler dahil olmak üzere tam olarak desteklenmiş şekilde çalışır:

Gelişmiş mimariler:

**Analog cihazlar**: parça, BlackICE, CM4xx

**Andes Core**: RISC-V

**Ambiqmicro**: Apollo MCUs

**ARM**: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı

**Temposunda**: xtensa, elmas

**Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi

**Cypress**: RISC-V

**Ensilica**: ESI-RISC

**Infineon**: XMC1000, XMC4000, kanore

**Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, varış a 10

**Mikro yonga**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32

**Mikro yarı**: RISC-V

**NXP**: LPC, ARM7, ARM9, PowerPC, 68K, I.MX, ColdFire, Kinetis Cortex-M3/M4

**Renesas**: SH, HS, v850, RX, Rz, Synergy

**Silicon Labs**: EFM32

**Synopsys**: Arc 600, 700, Arc Em, Arc HS

**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

**TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C

**Dalga bilgi işlem**: MIPS32 4k, 24K, 34K, 1004K, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M sınıfı

**Xilinx**: mikro Blaze, PowerPC 405, zynq, Zynq UltraSCALE
