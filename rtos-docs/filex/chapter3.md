---
title: Bölüm 3-Azure RTOS FileX 'in Işlevsel bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS FileX katıştırılmış dosya sisteminin bir açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a94344a7079e3f0e3e451bc678c369fee543aef6
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550176"
---
# <a name="chapter-3---functional-components-of-azure-rtos-filex"></a>Bölüm 3-Azure RTOS FileX 'in Işlevsel bileşenleri

Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS FileX katıştırılmış dosya sisteminin bir açıklaması yer almaktadır.

## <a name="media-description"></a>Medya açıklaması

FileX, FAT dosya sistemi biçimine uyan, yüksek performanslı bir katıştırılmış dosya sistemidir. FileX fiziksel medyayı mantıksal kesimlerin bir dizisi olarak görüntüler. Bu kesimlerin temel alınan fiziksel medyaya nasıl eşlendiği, ***fx_media_open*** çağrısı sırasında FileX medyasına bağlı g/ç sürücüsüne göre belirlenir.

### <a name="fat121632-logical-sectors"></a>FAT12/16/32 mantıksal kesim

Medyanın mantıksal kesimlerinin tam organizasyonu, fiziksel medyanın önyükleme kaydı içeriğine göre belirlenir. Medyanın mantıksal kesimlerinin genel düzeni Şekil 1 ' de gösterilmiştir.

FileX mantıksal kesimleri, medyanın ilk ayrılmış kesimine işaret eden mantıksal sektör 1 ' den başlar. Ayrılmış kesimler isteğe bağlıdır, ancak kullanımda olduğunda genellikle önyükleme kodu gibi sistem bilgilerini içerir.

### <a name="fat121632-media-boot-record"></a>FAT12/16/32 medya önyükleme kaydı

Medyanın mantıksal sektör görünümündeki diğer alanların tam kesim boşluğu, *medya önyükleme kaydının* içeriğinden türetilir. Önyükleme kaydının konumu genellikle 0 kesiminde olur. Öte yandan, medyada *gizli kesimler* varsa, önyükleme kesiminin bu hesaba göre olması gerekir (önyükleme KESIMININ hemen öncesinde bulunur). Tablo 1, medyanın önyükleme kaydı bileşenlerini listeler ve bileşenler paragraflarda açıklanmıştır.

- **Sıçrama yönergesi** *Sıçrama yönergesi* alanı, bir işlemci atlamanın Intel x86 makinesi yönergesini temsil eden üç baytlık bir alandır. Bu çoğu durumda eski bir alandır.

  ![FileX medya mantıksal sektör görünümü](./media/user-guide/filex-media-logical-sector-view.png)

  **ŞEKIL 1. FileX medya mantıksal sektör görünümü**

- **OEM adı** *OEM adı* alanı, üreticilerin adına veya adına cihaz adını yerleştirmelerini sağlamak için ayrılmıştır.
- **Kesim başına bayt sayısı** Medya önyükleme kaydındaki *kesim başına bayt* alanı, her bir sektörün (medyanın temel öğesi) kaç baytlık olduğunu tanımlar.
- **Küme başına kesim sayısı** Medya önyükleme kaydındaki *küme başına kesim* alanı, bir kümeye atanan kesimlerin sayısını tanımlar. Küme, bir FAT uyumlu dosya sistemindeki temel ayırma öğesidir. Tüm dosya bilgileri ve alt dizinleri, dosya ayırma tablosu (FAT) tarafından belirlendiği şekilde medyanın kullanılabilir kümelerinden ayrılır.

    **TABLO 1. FileX medya önyükleme kaydı**
    
    |Uzaklık  |Alan  |Bayt sayısı|
    |----------|-----------|------------|
    |-|Atma yönergesi (E9, xx, xx veya EB, xx, 90)|3|
    |0x03|OEM adı|8|
    |0x0B|Kesim başına bayt sayısı|2|
    |0x0D|Küme başına kesim sayısı|1|
    |0x0E|Ayrılmış sektör sayısı|2|
    |0x10|FATs sayısı|1|
    |0x11|Kök dizinin boyutu|2|
    |0x13|FAT-12 &amp; FAT-16 kesim sayısı|2|
    |0x15|Ortam Türü|1|
    |0x16|FAT başına kesim sayısı|2|
    |0x18|Iz başına kesim sayısı|2|
    |0x1A|Kafa sayısı|2|
    |0x1C|Gizli sektör sayısı|4|
    |0x20|Kesim sayısı-FAT-32|4|
    |0x24|FAT başına kesim (FAT-32)|4|
    |0x2C|Kök dizin kümesi|4|
    |0x3E|Sistem önyükleme kodu|448
    |0x1FE|0x55AA|2|

- **Ayrılmış kesimler** Medya önyükleme kaydındaki *ayrılmış kesimler* alanı, önyükleme kaydı ve FAT alanının ilk kesimi arasında ayrılan kesimlerin sayısını tanımlar. Çoğu durumda bu giriş sıfırdır.
- **FATs sayısı** Medya önyükleme kaydındaki *Fats girişi sayısı* , medyadaki Fats sayısını tanımlar. Medyada her zaman en az bir adet FAT olması gerekir. Ek FATs 'ler yalnızca birincil (ilk) FAT kopyası olan ve genellikle tanılama veya kurtarma yazılımı tarafından kullanılır.
- **Kök dizin boyutu** Medya önyükleme kaydındaki *kök dizin boyutu* girişi, medyanın kök dizinindeki sabit giriş sayısını tanımlar. Bu alan, her ikisi de medyanın kümelerinden ayrıldığından, alt dizinler ve FAT-32 kök dizini için geçerli değildir.
- **Kesim sayısı FAT-12 & FAT-16** Medya önyükleme kaydındaki *kesim sayısı* alanı, medyadaki toplam kesim sayısını içerir. Bu alan sıfırsa, toplam kesim sayısı, önyükleme kaydında daha sonra bulunan *kesim sayısı FAT-32* alanına dahil edilir.
- **Medya türü** *Medya türü* alanı, aygıt sürücüsü için mevcut medya türünü belirlemek için kullanılır. Bu, eski bir alandır.
- **FAT başına kesim sayısı** Medya önyükleme kaydındaki *FAT başına düşen kesimler* , FAT alanındaki her bir FAT ile ilişkili kesimlerin sayısını içerir. FAT kesimlerinin sayısı, medyada ayrılabilecek olabilecek en yüksek küme sayısı için hesaba yetecek kadar büyük olmalıdır.
- **Iz başına kesim sayısı** Medya önyükleme kaydındaki *izleme başına kesim* alanı, iz başına kesim sayısını tanımlar. Bu, genellikle gerçek disk türü medyayla geçerlidir. FLASH cihazları bu eşlemeyi kullanmaz.
- **Kafa sayısı** Medya önyükleme kaydındaki *kafa sayısı* alanı, medyadaki kafa sayısını tanımlar. Bu, genellikle gerçek disk türü medyayla geçerlidir. FLASH cihazları bu eşlemeyi kullanmaz.
- **Gizli kesimler** Medya önyükleme kaydındaki *gizli kesimler* alanı, önyükleme kaydından önceki kesimlerin sayısını tanımlar. Bu alan **FX_MEDIA** denetim bloğunda tutulur ve FileX tarafından yapılan tüm okuma ve yazma Isteklerindeki FileX g/ç sürücülerinde hesaba katılmış olmalıdır.
- **Bölüm sayısı FAT-32** Medya önyükleme kaydındaki *kesim sayısı* alanı yalnızca iki baytlık *sektör* alanı sıfır olduğunda geçerlidir. Böyle bir durumda, bu dört baytlık alan medyadaki kesimlerin sayısını içerir.
- **FAT başına kesim (FAT-32)** *FAT başına kesim (FAT-32)* alanı yalnızca fat-32 biçiminde geçerlidir ve medyanın her bir FAT alanı için ayrılan kesimlerin sayısını içerir.
- **Kök dizin kümesi** *Kök dizin kümesi* alanı yalnızca FAT-32 biçiminde geçerlidir ve kök dizinin başlangıç kümesi numarasını içerir.
- **Sistem önyükleme kodu** *Sistem önyükleme kodu* alanı, önyükleme kodunun küçük bir bölümünü depolamak için bir alandır. Günümüzde bu çoğu cihazda eski bir alandır.
- **Imza 0x55AA** *İmza* alanı, önyükleme kaydını tanımlamak için kullanılan bir veri modelidir. Bu alan yoksa, önyükleme kaydı geçerli değildir.

### <a name="exfat"></a>exFAT

FAT32 'teki en büyük dosya boyutu 4 GB 'dir ve bu, yüksek tanımlı multimedya dosyalarının geniş benimseme sayısını sınırlar. Varsayılan olarak FAT32, en fazla 32GB'A kadar depolama medyasını destekler. Flash ve SD kart kapasitesini artırarak, FAT32 büyük birimleri yönetirken daha verimli hale gelir. exFAT, bu sınırlamaları aşmak için tasarlanmıştır. exFAT, yaklaşık 1.000.000.000 GB olan bir Exabyte 'e (EB) kadar dosya boyutunu destekler. ExFAT ve FAT32 arasındaki diğer önemli fark, exFAT 'in birimdeki kullanılabilir alanı yönetmek için bit eşlem kullandığından, verileri dosyaya yazarken kullanılabilir alanı bulmada daha verimli hale getirir. Bitişik kümeler içinde depolanan dosya için, exFAT, FAT zincirinin tüm kümeleri bulmasını ve büyük dosyalara erişirken daha verimli olmasını sağlar. 32 ' den büyük Flash depolama ve SD kartları için exFAT gereklidir.

### <a name="exfat-logical-sectors"></a>exFAT mantıksal kesimleri

Medyanın exFAT 'teki mantıksal kesimlerinin genel düzeni Şekil 2 ' de gösterilmiştir. ExFAT 'de önyükleme bloğunda ve FAT alanı sistem alanına aittir. Kümelerin geri kalanı Kullanıcı alanıdır. Gerekli olmasa da, exFAT Standard, ayırma bit eşlemin Kullanıcı alanının başlangıcında ve ardından büyük/küçük harf ve kök dizin olması önerilir.

### <a name="exfat-media-boot-record"></a>exFAT medya önyükleme kaydı

ExFAT 'deki medya önyükleme kaydının içeriği FAT12/16/32 ' den farklı. Bunlar tablo 2 ' de listelenir. Karışıklık oluşmasını önlemek için, FAT12/16/32 ' de çeşitli medya parametreleri içeren 0x0B ve 0x40 arasındaki alan exFAT 'de *ayrılmış* olarak işaretlenir. Bu ayrılmış alan sıfırlarla programlanmalıdır ve medya önyükleme kaydının yanlış yorumlanması önlenir.

![exFAT mantıksal kesimleri](./media/user-guide/exfat-logical-sectors.png)

**ŞEKIL 2. exFAT mantıksal kesimleri**

- **Sıçrama yönergesi** *Sıçrama yönergesi* alanı, bir işlemci atlamanın Intel x86 makinesi yönergesini temsil eden üç baytlık bir alandır. Bu çoğu durumda eski bir alandır.

    **TABLO 2. exFAT medya önyükleme kaydı**

    |Uzaklık  |Alan  |Bayt sayısı|
    |----------|-----------|------------|
    |-|Sıçrama yönergesi|3|
    |0x03|Dosya sistemi adı|8|
    |0x0B|Ayrılmıştır|53|
    |0x40|Bölüm boşluğu|8|
    |0x48|Birim uzunluğu|8|
    |0x50|FAT kayması|4|
    |0x54|FAT uzunluğu|4|
    |0x58|Küme yığın boşluğu|4|
    |0x5C|Küme sayısı|4|
    |0x60|İlk kök dizin kümesi|4|
    |0x64|Birim seri numarası|4|
    |0x68|Dosya sistemi düzeltmesi|2|
    |0x6A|Birim bayrakları|2|
    |0x6C|Kesim kaydırma başına bayt|1|
    |0x6D|Küme başına kesim kaydırma|1|
    |0x6E|FATs sayısı|1|
    |0x6F|Sürücü seçme|1|
    |0x70|Kullanımdaki yüzde|7|
    |0x71|Ayrılmıştır|1|
    |0x78|Önyükleme kodu|390|
    |0x1FE|Önyükleme Imzası|2|

- **Dosya sistemi adı** ExFAT için *dosya sistemi adı* alanı "exFAT" ve ardından üç sondaki boşluk olmalıdır.
- **Ayrılmış** *Ayrılmış* alanın içeriği sıfır olmalıdır. Bu bölge FAT12/16/32 içindeki önyükleme kayıtlarıyla örtüşüyor. Bu alanın sıfır olması, dosya sistemlerinin bu birimi yanlış yorumlaması durumunda olmasını önler.
- **Bölüm boşluğu** *Bölüm boşluğu boşluğu* alanı, bu bölümün başlangıcını gösterir.
- **Birim uzunluğu** *Birim uzunluğu* alanı, bu bölümün kesim sayısını, boyutunu tanımlar.
- **FAT kayması** *FAT konum* alanı, bu bölümün FAT tablosunda, bu bölümün başlangıcına göre başlangıç sektör numarasını tanımlar.
- **FAT uzunluğu** *FAT uzunluğu* alanı, FAT tablosunun boyutunu kesim sayısı cinsinden tanımlar.
- **Küme yığın boşluğu** *Küme yığını konum* alanı, küme yığınının bölüm başlangıcına göre başlangıç sektör numarasını tanımlar. Küme yığını, dizin bilgilerinin ve dosya verilerinin depolandığı alandır.
- **Küme sayısı** *Küme sayısı* alanı, bu bölümün sahip olduğu küme sayısını tanımlar.
- **Ilk kök dizin kümesi** *İlk kök dizin alanı kümesi* , kök dizinin başlangıç konumunu tanımlar, bu, ayırma bit eşlemi ve baş durum tablosundan hemen sonra olması önerilir.
- **Birim seri numarası** *Birim seri numarası* alanı, bu bölümün seri numarasını tanımlar.
- **Dosya sistemi düzeltmesi** *Dosya sistemi düzeltme* alanı, exFAT 'in birincil ve ikincil sürümünü tanımlar.
- **Birim bayrakları** *Birim bayrakları* alanı, bu birimin durumunu gösteren bayraklar içerir.
- **Kesim kaydırma başına bayt** *Kesim kaydırma alanı başına bayt* sayısı, kesim başına bayt sayısını, log2 (n) cinsinden tanımlar; burada n, kesim başına bayt sayısıdır. Örneğin, SD kartında sektör boyutu 512 bayttır. Bu nedenle bu alan 9 (log2 (512) = 9) olacaktır.
- **Küme başına kesim kaydırma** *Küme kaydırma alanı başına kesim* sayısı, kümedeki kesimlerin sayısını tanımlar, burada n, küme başına kesim sayısıdır.
- **FATs sayısı** *FATs alanı sayısı* , bu bölümdeki FAT tablolarının sayısını tanımlar. ExFAT için, bir FAT tablosu için değerin 1 olması önerilir.
- **Sürücü seçme** *Sürücü seçme* alanı, genişletilmiş Int 13h sürücü numarasını tanımlar.
- **Kullanımdaki yüzde** *Kullanım alanı yüzdesi* , küme yığınındaki kümelerin yüzdesini tanımlar. Geçerli değerler 0 ile 100 (dahil) arasındadır.
- **Ayrılmış** Bu alan gelecekte kullanılmak üzere ayrılmıştır.
- **Önyükleme kodu** *Önyükleme kodu* alanı, önyükleme kodunun küçük bir bölümünü depolayan bir alandır. Günümüzde bu çoğu cihazda eski bir alandır.
- **Imza 0x55AA** *Önyükleme imzası* alanı, önyükleme kaydını tanımlamak için kullanılan bir veri modelidir. Bu alan yoksa, önyükleme kaydı geçerli değildir.

### <a name="file-allocation-table-fat"></a>Dosya ayırma tablosu (FAT)

*Dosya ayırma tablosu (FAT)* , medyadaki ayrılmış kesimlerden sonra başlar. FAT alanı temel olarak, kümenin ayrılmadığını veya bir alt dizin ya da bir dosya içeren küme zincirinin bir parçasını oluşturan 12 bit, 16 bit veya 32 bitlik girdilerden oluşan bir dizidir. Her bir FAT girişinin boyutu, temsil edilebilmesi gereken küme sayısına göre belirlenir. Küme sayısı (Toplam kesimlerden küme başına kesim sayısı), 4.086 değerinden küçük veya bu değere eşitse, 12 bit FAT girişleri kullanılır. Toplam küme sayısı 4.086 ' den büyükse ve 65.525 ' den küçükse, 16 bit FAT girişleri kullanılır. Aksi takdirde, toplam küme sayısı 65.525 ' e eşit veya daha büyükse, 32-bit FAT veya exFAT kullanılır.

FAT12/16/32 için FAT tablosu yalnızca küme zincirini korumadığından, küme ayırma hakkında bilgi de sağlar: bir kümenin kullanılabilir olup olmadığı. ExFAT 'de, küme ayırma bilgileri bir ayırma bit eşlem Dizin girişi tarafından korunur. Her bölümün kendi ayırma bit eşlemi vardır. Bit eşlemin boyutu, tüm kullanılabilir kümeleri kapsayacak kadar büyük. Bir küme ayırma için kullanılabiliyorsa, ayırma bit eşlemdeki ilgili bit 0 olarak ayarlanır. Aksi takdirde, bit 1 olarak ayarlanır. Ardışık kümeleri kaplayan bir dosya için exFAT, tüm kümelerin izlenmesini sağlamak için bir FAT zinciri gerektirmez. Ancak, ardışık küme içermeyen bir dosya için, bir FAT zincirinin hala tutulması gerekir.

### <a name="fat-entry-contents"></a>FAT giriş Içeriği

FAT tablosundaki ilk iki giriş kullanılmaz ve genellikle aşağıdaki içeriğe sahiptir.

|FAT girdisi |12 bit FAT|16 bit FAT|32-bit FAT| exFAT|
|----------|-----------|------------|-------|------|
|Giriş 0|0x0F0|0x00F0|0x000000F0|0xF8FFFFFF|
|Girdi 1|0xFFF|0xFFFF|0x0FFFFFFF|Ffffffff|

FAT giriş numarası 2, medyanın veri alanındaki ilk kümeyi temsil eder. Her küme girişinin içeriği, bir dosya veya alt dizin için ayrılmış kümelerin bağlı listesinin boş veya bir parçası olup olmadığını belirler. Küme girişi başka bir geçerli küme girişi içeriyorsa, küme ayrılır ve değeri küme zincirinde ayrılan sonraki kümeye işaret eder.

Olası küme girdileri aşağıdaki gibi tanımlanmıştır.

|Anlamı|12 bit FAT|16 bit FAT|32-bit FAT| exFAT|
|----------|-----------|------------|-------|------|
|Boş küme|0x000|0x0000|0x00000000|0x00000000|
|Kullanılmıyor|0x001|0x0001|0x00000001|0x00000001|
|Ayrılmıştır|0xFF0-FF6|0xFFF0-FFF6|0x0FFFFFF0-6|ClusterCounter + 2 ile 0xFFFFFFF6|
|Hatalı küme|0xFF7|0xFFF7|0x0FFFFFF7|0xFFFFFFF7|
|Ayrılmıştır| - | - | - | 0xFFFFFFF8-E|
|Son küme| 0xFF8-FFF| 0xFFF8-FFFF| 0x0FFFFFF8-F| Ffffffff|
|Küme bağlantısı| 0x002-0xFEF| 0x0002-FFEF| 0x2-0x0FFFFFEF | 0x2-ClusterCount + 1|

Ayrılmış bir küme zincirindeki son küme, son küme değerini (yukarıda tanımlanan) içerir. İlk küme numarası, dosya veya alt dizinin dizin girdisinde bulunur.

### <a name="internal-logical-cache"></a>İç mantıksal önbellek

FileX, her açılan medya için *en son kullanılan* mantıksal kesim önbelleğini korur. Mantıksal kesim önbelleğinin en büyük boyutu, sabit **FX_MAX_SECTOR_CACHE** tarafından tanımlanır ve **_fx_api. h_**' de bulunur. Bu, iç mantıksal kesim önbelleğinin boyutunu belirleyen ilk etkendir.

Mantıksal kesim önbelleğinin boyutunu belirleyen diğer faktör, uygulama tarafından ***fx_media_open** _ çağrısına sağlanan bellek miktarıdır. En az bir mantıksal kesim için yeterli bellek olmalıdır. _ *FX_MAX_SECTOR_CACHE** mantıksal kesim gerekliyse, **_fx_api. h_** ' de sabit değiştirilmelidir ve tüm FileX kitaplığı yeniden oluşturulmalıdır.

> [!IMPORTANT]
> *FileX 'teki her açık medya, açma çağrısı sırasında sağlanan belleğe bağlı olarak farklı bir önbellek boyutuna sahip olabilir.*

### <a name="write-protect"></a>Yazma koruması

FileX, uygulama sürücüsüne medyada dinamik olarak yazma koruması ayarlama yeteneği sağlar. Yazma koruması gerekliyse, sürücü, ilişkili FX_MEDIA yapısındaki *fx_media_driver_write_protect* alanı FX_TRUE olarak ayarlanır. Ayarlandığında, uygulamanın medyayı değiştirmesi için yaptığı tüm denemeler reddedilir ve dosyaları yazmak için açmaya çalışır. Sürücü, bu alanı temizleyerek yazma korumasını de devre dışı bırakabilir.

### <a name="free-sector-update"></a>Ücretsiz sektör güncelleştirmesi

FileX, kesimler artık kullanımda olmadığında uygulama sürücüsünü bilgilendirmek için bir mekanizma sağlar. Bu özellikle, FileX tarafından kullanılan tüm mantıksal kesimleri yöneten FLASH bellek yöneticileri için yararlıdır.

Boş kesimlerin bildirimi gerekliyse, uygulama sürücüsü ilişkili FX_MEDIA yapısındaki *fx_media_driver_free_sector_update* alanı FX_TRUE olarak ayarlanır. Bu atama genellikle sürücü başlatma sırasında yapılır.

Bu alan ayarlandığında, FileX bir veya daha fazla ardışık kesimlerin ücretsiz hale geldiğini belirten bir **FX_DRIVER_RELEASE_SECTORS** sürücü çağrısı yapar.

### <a name="media-control-block-fx_media"></a>Medya denetim bloğu FX_MEDIA

FileX 'teki her bir açık medyanın özellikleri, medya denetim bloğunda bulunur. Bu yapı ***fx_api. h*** dosyasında tanımlanmıştır.

Medya denetim bloğu bellekte herhangi bir yerde bulunabilir, ancak her bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

Diğer alanlardaki denetim bloğunun bulunması, dinamik olarak ayrılan tüm bellekte olduğu gibi biraz daha dikkatli olmalıdır. Bir denetim bloğu bir C işlevi içinde ayrılmışsa, onunla ilişkili bellek, çağıran iş parçacığının yığınının bir parçasıdır.

> [!WARNING]
>*Genel olarak, denetim blokları için yerel depolama kullanmaktan kaçının çünkü işlev dönmesinden sonra, hala kullanımda olup olmadığından bağımsız olarak tüm yerel değişken yığın alanı serbest bırakılır!*

## <a name="fat121632-directory-description"></a>**FAT12/16/32 dizin açıklaması**

FileX, hem 8,3 hem de Windows Long dosya adı (LFN) ad biçimlerini destekler. Adın yanı sıra, her bir dizin girişi girişin özniteliklerini, son değiştirilme tarihi ve tarihini, başlangıç kümesi dizinini ve girişin bayt cinsinden boyutunu içerir. Tablo 3, bir FileX 8,3 dizin girişinin içeriğini ve boyutunu gösterir.

- **Dizin adı**

    FileX, 1 ile 255 arasında karakter büyüklüğünde dosya adlarını destekler. Standart sekiz karakterlik dosya adları, medyada tek bir dizin girişinde temsil edilir. Dizin adı alanında hizalı olarak sola alınır ve boş olarak doldurulur. Ayrıca, adı oluşturan ASCII karakterleri her zaman büyük harfle alınır.

    Uzun dosya adları (LFNs), birbirini izleyen bir 8,3 standart dosya adı tarafından ardışık dizin girişleriyle, ters sırada ve hemen temsil edilir. Oluşturulan 8,3 adı, adla ilişkili tüm anlamlı dizin bilgilerini içerir. Tablo 4, uzun dosya adı bilgilerini tutmak için kullanılan dizin girişlerinin içeriğini gösterir ve tablo 5, toplam dört Dizin girişi gerektiren 39 karakterlik LFN bir örneğini gösterir.

> [!IMPORTANT]
> ***Fx_api. h** içinde tanımlanan sabit **FX_MAX_LONG_NAME_LEN**, FileX tarafından desteklenen uzunluk üst sınırını içerir.*

- **Dizin dosya adı uzantısı**

    Standart 8,3 dosya adları için, FileX isteğe bağlı üç karakterli *Dizin dosya adı uzantısını* da destekler. Sekiz karakterlik dosya adı gibi, dosya adı uzantıları dizin dosya adı uzantısı alanında, boş doldurulmuş ve her zaman büyük harfle hizalı olarak kalır.

    **TABLO 3. FileX 8,3 dizin girişi**

    |Uzaklık|Alan|Bayt sayısı|
    |------------|-----------|------------|
    |-|Dizin girişi adı|8|
    |0x08|Dizin uzantısı|3|
    |0x0B|Öznitelikler|1|
    |0x0C|NT (uzun dosya adı biçimiyle tanıtılan ve NT için ayrılmıştır [Always 0])|1|
    |0x0D|Milisaniye cinsinden oluşturulma zamanı (uzun dosya adı biçimiyle tanıtılan ve dosyanın oluşturulduğu milisaniye sayısını temsil eder.)|1|
    |0x0E|Saat dakika cinsinden oluşturulma zamanı &amp; (uzun dosya adı biçimiyle tanıtılan ve dosyanın oluşturulduğu saati ve dakikayı temsil eder)|2|
    |0x10|Oluşturulma tarihi (uzun dosya adı biçimiyle tanıtılan ve dosyanın oluşturulduğu tarihi temsil eder.)|2|
    |0x12|Son erişim tarihi (uzun dosya adı biçimiyle tanıtılan ve dosyanın en son erişildiği tarihi temsil eder.)|2|
    |0x14|Küme başlatılıyor (yalnızca üst 16 bit FAT-32)|2|
    |0x16|Değiştirilme zamanı|2|
    |0x18|Değiştirme Tarihi|2|
    |0x1A|Küme başlatılıyor (düşük 16 bit FAT-32 veya FAT-12 veya FAT-16)|2|
    |0x1C|Dosya Boyutu|4|


- **Dizin öznitelikleri**

    Tek baytlık *dizin özniteliği* alan girişi, dizin girişinin çeşitli özelliklerini belirten bir bit serisi içerir. Dizin öznitelik tanımları aşağıdaki gibidir:

    |Öznitelik biti|Anlamı|
    |------------|-----------|
    |0x01|Giriş salt okunurdur.|
    |0x02|Giriş gizlidir.|
    |0x04|Giriş bir sistem girişi.|
    |0x08|Giriş bir birim etikettir|
    |0x10|Giriş bir dizindir.|
    |0x20|Giriş değiştirildi.|

    Tüm öznitelik bitleri birbirini dışlamalı olduğundan, bir seferde birden fazla öznitelik bit kümesi olabilir.

- **Dizin saati**

    İki baytlık *Dizin zamanı* alanı, belirtilen dizin girişinde yapılan son değişikliğin saat, dakika ve saniye sayısını içerir. Bit 15 ile 11 arasında saat varsa, bit 10 ' da dakikalar, 5 ' i de yarım saniye içeren bit 4 ' ü içerir. Gerçek saniyeler bu alana yazılmadan önce iki olarak bölünür.

- **Dizin tarihi**

    İki baytlık *Dizin tarihi* alanı, belirtilen dizin girişinde yılı (1980 ' dan fazla), ayı ve son değişikliğin gününü içerir. 15 ' ten 9 ' a kadar olan bit, yıl farkını içerir, 8 ila 5 bit, ay farkını içerir ve bit 4 ile 0 arasında bir gün içerir.

- **Dizin başlatma kümesi**

    Bu alan, FAT-12 ve FAT-16 için 2 bayt kaplar. FAT-32 için bu alan 4 bayt kaplar. Bu alan, girdiye ayrılan ilk küme numarasını (alt dizin veya dosya) içerir.

    > [!NOTE]
    > * FileX 'in, yeni oluşturulan bir dosya için isteğe bağlı olarak sürekli sayıda küme ayırmasına izin vermek üzere ilk küme olmadan (küme alanı sıfıra kadar başlar) yeni dosyalar oluşturduğunu unutmayın. *

- **Dizin dosyası boyutu**

    Dört baytlık *Dizin* *dosyası boyutu* alanı, dosyadaki bayt sayısını içerir. Giriş gerçekten bir alt dizinindeyse, boyut alanı sıfırdır.

### <a name="long-file-name-directory"></a>Uzun dosya adı dizini

- **Sıralı**

    LFN girişinin sayısını belirten bir baytlık *sıra* alanı. LFN girdileri ters sırada konumlandırıldığından, tek bir LFN 'nin bulunduğu LFN dizin girişlerinin sıra değerleri bir tarafından azalmıştır. Ayrıca, 8,3 dosya adından önce, LFN 'nin sıra değeri bir olmalıdır.

    **TABLO 4. Uzun dosya adı Dizin girişi**

    | Uzaklık | Alan | Bayt sayısı |
    |------------|-----------|------------|
    | - | Ordinal alanı | 1 |
    | 0x01 | Unicode karakter 1 | 2 |
    | 0x03 | Unicode karakter 2 | 2 |
    | 0x05 | Unicode karakter 3 | 2 |
    | 0x07 | Unicode karakter 4 | 2 |
    | 0x09 | Unicode karakter 5 | 2 |
    | 0x0B | LFN öznitelikleri | 1 |
    | 0x0C | LFN türü (ayrılmış her zaman 0) | 1 |
    | 0x0D | LFN sağlama toplamı | 1 |
    | 0x0E | Unicode karakteri 6 | 2 | 
    | 0x10 | Unicode karakter 7 | 2 |
    | 0x12 | Unicode karakter 8 | 2 |
    | 0x14 | Unicode karakter 9 | 2 |
    | 0x16 | Unicode karakter 10 | 2 |
    | 0x18 | Unicode karakter 11 | 2 |
    | 0x1A | LFN kümesi (kullanılmamış her zaman 0) | 2 |
    | 0x1C | Unicode karakter 12 | 2 |
    | Dosyasında | Unicode karakter 13 | 2 |

- **Unicode karakteri**

    İki baytlık *Unicode karakter* alanları, birçok farklı dilin karakterlerini destekleyecek şekilde tasarlanmıştır. Standart ASCII karakterleri, Unicode karakterinin ilk baytında depolanan ASCII karakteri ve ardından bir boşluk karakteri ile temsil edilir.

- **LFN öznitelikleri**

    Tek baytlık *LFN öznitelikleri* alanı, BIR LFN Dizin girişi olarak dizin girişini tanımlayan öznitelikleri içerir. Bu, salt okunurdur, sistem, gizli ve birim özniteliklerinin tümünün ayarlandığı bir şekilde gerçekleştirilir.

- **LFN türü**

    Tek baytlık *LFN türü* alanı ayrılmıştır ve her zaman 0 ' dır.

- **LFN sağlama toplamı**

    Tek baytlık *LFN sağlama toplamı* alanı, ilişkili Msdos 8,3 dosya adının 11 karakterlik sağlama toplamını temsil eder. Bu sağlama toplamı, LFN girişinin uygun 8,3 dosya adına karşılık geldiğinden emin olmak için her LFN girdisinde saklanır.

- **LFN kümesi**

    İki baytlık *LFN kümesi* alanı kullanılmamış ve her zaman 0 ' dır.

    **TABLO 5. 39 karakter LFN kapsayan dizin girişleri**

    |Giriş|Anlamı|
    |------------|-----------|
    |1|LFN Dizin girdisi 3|
    |2|LFN Dizin girişi 2|
    |3|LFN Dizin girdisi 1|
    |4|8,3 dizin girişi (ttttt ~ n. xx)|

### <a name="exfat-directory-description"></a>exFAT dizin açıklaması

exFAT dosya sistemi, Dizin girişini ve dosya adını farklı şekilde depolar. Dizin girişi, girişin özniteliklerini, girişin oluşturulduğu, değiştirildiği ve erişildiği zaman içindeki çeşitli zaman damgalarını içerir. Dosya boyutu ve küme başlatma gibi diğer bilgiler, birincil dizin girişini hemen izleyen akış uzantısı Dizin girişinde depolanır. exFAT yalnızca uzun dosya adı (LFN) ad biçimini destekler. Dosya adı Dizin girişinde depolanan, tablo 2 ' de gösterildiği gibi, akış uzantısı Dizin girişini hemen izler.

### <a name="exfat-file-directory-entry"></a>exFAT dosya dizini girdisi

ExFAT dosya dizini girişinin açıklaması ve içeriği aşağıdaki tablo ve paragraflara dahildir.

- **Giriş Türü**

    Giriş türü alanı bu girişin türünü gösterir. Dosya dizini girişi için bu alan 0x85 olmalıdır.

- **İkincil giriş sayısı**

    *İkincil girdi sayısı* alanı, bu birincil girdinin hemen altındaki ikincil girdi sayısını gösterir. Dosya dizini girdisiyle ilişkili ikincil girişler, bir akış uzantısı Dizin girişi ve bir veya daha fazla dosya adı Dizin girişi içerir.

    **TABLO 6. exFAT dosya dizini girdisi**

    |Uzaklık|Alan|Bayt sayısı|
    |----|-----------|-|
    |-|Giriş Türü|1|
    |0x01|İkincil girdi|1|
    |0x02|Sağlama|2|
    |0x04|Dosya Öznitelikleri|2|
    |0x06|Ayrılmış 1|2|
    |0x08|Zaman Damgası Oluştur|4|
    |0x0C|Son değiştirme zaman damgası|4|
    |0x10|Son erişme zaman damgası|4|
    |0x14|10 MS artışı oluştur|1|
    |0x15|Son değiştirme 10ms artış|1|
    |0x16|UTC boşluğu oluştur|1|
    |0x17|Son değiştirme UTC kayması|1|
    |0x18|Son erişim UTC kayması|1|
    |0x19|Ayrılmış 2|7|

- **Toplam**

    *Sağlama toplamı* alanı, Dizin giriş kümesindeki tüm girişler üzerindeki sağlama toplamı değerini (dosya dizini girişi ve ikincil girdileri) içerir.

- **Dosya Öznitelikleri**

    Tek baytlı öznitelikler alan girişi, dizin girişinin çeşitli özelliklerini belirten bir bit serisi içerir. Çoğu öznitelik bitlerinin tanımı, FAT 12/16/32 ile aynıdır. Dizin öznitelik tanımları aşağıdaki gibidir:

    |Öznitelik biti|Anlamı|
    |------------|-----------|
    |0x01| Giriş salt okunurdur|
    |0x02|Giriş gizli|
    |0x04|Giriş bir sistem girdisi|
    |0x08|Girdi ayrıldı|
    |0x10|Giriş bir dizin|
    |0x20|Giriş değiştirildi|
    |Diğer tüm bitleri|Ayrılmıştır|

- **Reserved1**

    Bu alan sıfır olmalıdır.

- **Zaman Damgası Oluştur**

    *Zaman damgası oluştur* alanı, *10 MS artış oluştur* alanındaki bilgileri birleştirerek, dosyanın veya dizinin oluşturulduğu yerel tarih ve saati açıklar.

- **Son değiştirme zaman damgası**

    Son değişiklik *zaman damgası* alanı, *son değiştirilen 10 MS artış* alanından bilgileri birleştiren, dosyanın veya dizinin en son değiştirildiği yerel tarih ve saati açıklıyor. Zaman damgalarındaki aşağıdaki notlara bakın.

- **Son erişme zaman damgası**

    *Son erişilen zaman damgası* alanı, dosyanın veya dizinin en son erişildiği yerel tarih ve saati açıklar. Zaman damgalarındaki aşağıdaki notlara bakın.

- **10 MS artışı oluştur**

    *Zaman damgası oluştur* alanındaki bilgileri birleştiren *10ms artışı oluştur* alanı, dosyanın veya dizinin oluşturulduğu yerel tarih ve saati açıklar. Zaman damgalarındaki aşağıdaki notlara bakın.

- **Son değiştirme 10ms artış**

    Son değiştirilen *10ms artış* alanı, *son değiştirme zaman damgası* alanından bilgileri birleştiren, dosyanın veya dizinin en son değiştirildiği yerel tarih ve saati açıklama. Zaman damgalarındaki aşağıdaki notlara bakın.

- **UTC boşluğu oluştur**

    *UTC farkı oluştur* alanı, dosya veya dizin oluşturulduğunda yerel saat ile UTC saati arasındaki farkı açıklar. Zaman damgalarındaki aşağıdaki notlara bakın.

- **Son değiştirme UTC kayması**

    *Son DEĞIŞTIRILEN UTC farkı* alanı, dosyanın veya dizinin en son değiştirildiği yerel saat ile UTC saati arasındaki farkı açıklar. Zaman damgalarındaki aşağıdaki notlara bakın.

- **Son erişildiği UTC kayması**

    *Son ERIŞILEN UTC farkı* alanı, dosyaya veya dizine son erişildiği zamana göre yerel saat ile UTC saati arasındaki farkı açıklar. Zaman damgalarındaki aşağıdaki notlara bakın.

- **Reserved2**

    Bu alan sıfır olmalıdır.

### <a name="notes-on-timestamps"></a>Zaman damgalarıyla ilgili notlar

- **Zaman damgası girişi** Zaman damgası alanları aşağıdaki gibi yorumlanır:

- **10 MS artış alanı** 10ms artış alanındaki değer, zaman damgası değerine daha ayrıntılı bir ayrıntı düzeyi sağlar. Geçerli değerler 0 (0ms) ile 199 (1990ms) arasındadır.

     ![10 MS artış alanı](./media/user-guide/10ms-increment-fields.png)

- **UTC fark alanı**

     ![UTC fark alanı](./media/user-guide/utc-offset-field.png)

- **Konum değeri**

    7 bit işaretli tamsayı, 15 dakikalık artışlarla UTC zamanının sapmasını temsil eder.

- **Geçerli**

    Konum alanındaki değerin geçerli olup olmadığı. 0, fark değeri alanındaki değerin geçersiz olduğunu gösterir. 1 değerin geçerli olduğunu gösterir.

### <a name="stream-extension-directory-entry"></a>Akış uzantısı Dizin girişi

Akış uzantısı dizin girişinin açıklaması ve içeriği aşağıdaki tabloya dahildir.

**TABLO 7. Akış uzantısı Dizin girişi**

|Uzaklık|Alan| Bayt sayısı|
|------------|-----------|-------|
|-|Giriş Türü|1|
|0x01|Bayraklar|1|
|0x02|Ayrılmış 1|1|
|0x03|Ad uzunluğu|1|
|0x04|Ad karması|2|
|0x06|Ayrılmış 2|2|
|0x08|Geçerli veri uzunluğu|8|
|0x10|Ayrılmış 3|4|
|0x14|İlk küme|4|
|0x18|Veri uzunluğu|8|

- **Giriş Türü**

    *Giriş türü* alanı bu girişin türünü gösterir. Akış uzantısı Dizin girişi için bu alan 0xC0 olmalıdır.

- **Larına**

    Bu alan, çeşitli özellikleri belirten bir bit serisi içerir:
    
    |Bayrak biti|Anlamı    |
    |-----------------|-----------|
    |0x01            |Bu alan, kümelerin ayrılmasının mümkün olup olmadığını gösterir. Bu alan 1 olmalıdır.|
    |0x02            |Bu alan, ilişkili kümelerin bitişik olup olmadığını gösterir. 0 değeri, FAT girişinin geçerli olduğu ve FileX 'in FAT zincirini takip eden anlamına gelir. 1 değeri, FAT girişinin geçersiz olduğu ve kümelerin bitişik olduğu anlamına gelir.|
    |Diğer tüm bitleri    |Ayrılmış.|

- **Ayrılmış 1**

    Bu alan 0 olmalıdır.

- **Ad uzunluğu**

    *Ad uzunluğu* alanı, her topluca içeren dosya adı Dizin girişlerinde Unicode dizesinin uzunluğunu içerir. Dosya adı Dizin girdileri hemen bu akış uzantısı Dizin girişini izler.

- **Ad karması**

    *Ad karması* alanı, yukarı yönlü dosya adının karma değerini içeren 2 baytlık bir giriştir. Karma değeri daha hızlı dosya/dizin adı aramasına izin verir: karma değerleri eşleşmezse, bu girişle ilişkili dosya adı bir eşleşme değildir.

- **Ayrılmış 2**

    Bu alan 0 olmalıdır.

- **Geçerli veri uzunluğu**

    *Geçerli veri uzunluğu* alanı, dosyadaki geçerli veri miktarını gösterir.

- **Ayrılmış 3**

    Bu dosyalanmış 0 olmalıdır.

- **İlk küme**

    *İlk küme* alanı, veri akışı ilk kümesinin dizinini içerir.

- **Veri uzunluğu**

    *Veri uzunluğu* alanı, ayrılan kümelerdeki toplam bayt sayısını içerir. ExFAT, veri kümelerinin önceden ayrılmasına izin verdiğinden bu değer *geçerli veri uzunluğundan* daha büyük olabilir.

### <a name="root-directory"></a>Kök Dizin

FAT 12 ve 16 bit biçimlerinde *kök dizin* , ORTAMDAKI tüm Fat kesimlerinden hemen sonra bulunur ve açık bir _ *FX_MEDIA** denetim bloğunda ***fx_media_root_sector_start** _ ' i inceleyerek bulunabilir. Kök dizinin, Dizin girişi sayısı (her 32 bayt boyutunda) cinsinden boyutu, medyanın önyükleme kaydındaki karşılık gelen girdiye göre belirlenir.

FAT-32 ve exFAT içindeki kök dizin, kullanılabilir kümelerin herhangi bir yerinden bulunabilir. Medya açıldığında önyükleme kaydından konum ve boyut belirlenir. Medya açıldıktan sonra, ***fx_media_root_sector_start*** alanı, FAT-32 veya exFAT kök dizininin başlangıç kümesini bulmak için kullanılabilir.

### <a name="subdirectories"></a>Klasörleri

Bir FAT sisteminde herhangi bir sayıda alt dizin bulunur. Alt dizinin adı, bir dosya adı gibi bir dizin girdisinde bulunur. Ancak, Dizin öznitelik belirtimi (0x10) girişin bir alt dizin olduğunu ve dosya boyutunun her zaman sıfır olduğunu belirtecek şekilde ayarlanır.
Şekil 3 ' te, * Sample adlı yeni bir singlecluster alt dizini için tipik bir alt dizin yapısının nasıl göründüğü gösterilmektedir **. DıR** _, _ *_FILE.TXT_* * adlı bir dosya ile.
Çoğu şekilde, alt dizinler dosya girdilerine çok benzer. İlk küme alanı, bağlantılı kümeler listesinin ilk kümesini işaret eder. Bir alt dizin oluşturulduğunda, ilk iki dizin girişi varsayılan dizinleri içerir; yani "." dizini ve ".." dizinidir. "." Dizini alt dizinin kendisini işaret ederken, ".." dizini önceki veya üst dizine işaret eder.

### <a name="global-default-path"></a>Genel varsayılan yol

FileX, medya için genel bir varsayılan yol sağlar. Varsayılan yol, açıkça tam yol belirtmeyen herhangi bir dosya veya dizin hizmetinde kullanılır.

Başlangıçta genel varsayılan dizin medyanın kök dizinine ayarlanır. Bu, ***fx_directory_default_set*** çağırarak uygulama tarafından değiştirilebilir.

Medyanın geçerli varsayılan yolu, ***fx_directory_default_get** _ çağırarak incelenebilir. Bu yordam, _ *FX_MEDIA** denetim bloğunun içinde tutulan varsayılan yol dizesine bir dize işaretçisi sağlar.

### <a name="local-default-path"></a>Yerel varsayılan yol

FileX, farklı iş parçacıklarının çakışma olmadan benzersiz yollara sahip olmasına izin veren, iş parçacığına özgü bir varsayılan yol da sağlar. **FX_LOCAL_PATH** yapısı, çağıran iş parçacığının yerel yolunu değiştirmek için **_fx_directory_local_path_set_*_ ve _*_fx_directory_local_path_restore_** çağrıları sırasında uygulama tarafından sağlanır.

Yerel bir yol varsa, yerel yol genel varsayılan medya yolundan önceliklidir. Yerel yol ayarlanmamış veya ***fx_directory_local_path_clear*** hizmetiyle silinirse, medyanın genel varsayılan yolu bir kez daha kullanılır.

## <a name="file-description"></a>Dosya açıklaması

FileX, standart 8,3 karakteri ve üç karakterli uzantılara sahip uzun dosya adlarını destekler. ASCII adının yanı sıra, her bir dosya girişi girişin özniteliklerini, son değiştirilme tarihi ve tarihini, başlangıç kümesi dizinini ve girişin bayt cinsinden boyutunu içerir.

### <a name="file-allocation"></a>Dosya ayırma

FileX, FAT biçiminin standart küme ayırma düzenini destekler. Ayrıca, FileX bitişik kümelerin ön küme ayırmasını destekler. Buna uyum sağlamak için, her FileX dosyası ayrılmış kümeler olmadan oluşturulur. Kümeler, izleyen yazma isteklerinde veya ***fx_file_allocate*** isteklerinde bitişik kümelerin önceden ayrılması için ayrılır.

Şekil 4 ' te, "FileX FAT-16 dosya örneği", küme 101 ' den başlayarak ayrılmış iki sıralı kümeyle ***FILE.TXT*** adlı bir dosya gösterir, örneğin, dosyanın ilk veri kümesi numarası 101.

### <a name="file-access"></a>Dosya erişimi

Bir FileX dosyası, okuma erişimi için aynı anda birden çok kez açılabilir. Ancak, bir dosya yazmak için yalnızca bir kez açılabilir. Dosya erişimini desteklemek için kullanılan bilgiler ***FX_FILE*** dosya denetim bloğunda bulunur.

> [!NOTE]
> *Medya sürücüsünün dinamik olarak yazma koruması ayarlayabileceğini unutmayın. Bu durumda, tüm yazma istekleri reddedilir ve yazma için bir dosyayı açmaya çalışır.*

### <a name="file-layout-in-exfat"></a>ExFAT 'de dosya düzeni

Veri KİRLİK kümelerinde depolanıyorsa, exFAT 'in tasarımı bir dosya için FAT zincirinin korunmasını gerektirmez. Stream uzantısı Dizin girişinde bulunan *Nofatzincirine* bit, dosyadaki VERILERI okurken FAT zincirinin kullanılıp kullanılmayacağını belirtir. *Nofatzinciri* ayarlandıysa, FileX akış uzantısı dizin girdisindeki *ilk küme* alanında belirtilen kümeden sırayla okur.

Öte yandan, *Nofatzinciri* açık Ise, FILEX, FAT12/16/32 içindeki FAT zincirine benzer şekilde dosyanın tamamının çapraz geçiş yapmak için FAT zincirini izler.

Şekil 3 ' te, biri FAT zinciri gerektirmeyen ve diğeri bir FAT zinciri gerektiren iki örnek dosya gösterilmektedir.

## <a name="system-information"></a>Sistem Bilgileri

FileX sistem bilgileri, açık medya örneklerinin izlemesinin yanı sıra genel sistem saatini ve tarihini sakdan oluşur.

![Bitişik kümeler ve FAT bağlantısı gerektiren dosya içeren dosya](./media/user-guide/system-information.png)

**ŞEKIL 3. Bitişik kümeler ve FAT bağlantısı gerektiren dosya içeren dosya**

Varsayılan olarak, sistem tarihi ve saati FileX 'in son yayın tarihine ayarlanır. Doğru sistem tarih ve saatine sahip olmak için, uygulamanın başlatma sırasında ***fx_system_time_set** _ ve _ *_fx_system_date_set_** çağrısı gerekir.

### <a name="system-date"></a>Sistem tarihi

FileX sistem tarihi genel ***_fx_system_date*** değişkeninde tutulur. 15 ' ten 9 ' a kadar olan bit, 1980 arasındaki yılı içerir, 1 ile 5 arasındaki bit, ay sapmasını içerir |

### <a name="system-time"></a>Sistem saati

FileX sistem saati genel ***_fx_system_time*** değişkeninde tutulur. Bit 15 ile 11 arasında saat varsa, bit 10 ' da dakikalar, 5 ' i de yarım saniye içeren bit 4 ' ü içerir.

### <a name="periodic-time-update"></a>Düzenli saat güncelleştirme

Sistem başlatma sırasında, FileX sistem tarihini ve saatini düzenli aralıklarla güncelleştirmek için bir ThreadX uygulama süreölçeri oluşturur. Sistem tarih ve saat güncelleştirmesinin ***_fx_system_initialize*** işlevi tarafından kullanılan iki sabitle belirlendiği oran.

**FX_UPDATE_RATE_IN_SECONDS** ve **FX_UPDATE_RATE_IN_TICKS** sabitleri aynı süreyi temsil eder. Sabit **FX_UPDATE_RATE_IN_TICKS** , sabit **FX_UPDATE_RATE_IN_SECONDS** belirtilen saniye sayısını temsil eden threadx Zamanlayıcı onay işareti sayısıdır. **FX_UPDATE_RATE_IN_SECONDS** sabiti, her bir FileX saat güncelleştirmesi arasındaki saniye sayısını belirtir. Bu nedenle, iç FileX süresi **FX_UPDATE_RATE_IN_SECONDS** aralıklarla artar. Bu sabitler fx_system_initialize _ derlemesi sırasında sağlanabilir veya geliştirici, FileX sürümünün **_ _fx_port. h_ dosyasında *bulunan Varsayılanları değiştirebilir*** .

Düzenli FileX süreölçeri yalnızca dosya zaman damgalaması için kullanılan genel sistem tarih ve saatini güncelleştirmek için kullanılır. Zaman damgalaması gerekli değilse, FileX dönemsel zamanlayıcısını oluşturmayı ortadan kaldırmak için **_fx_system_initialize. c_** derlerken **FX_NO_TIMER** tanımlamanız yeterlidir.

![FileX FAT-16 dosya örneği](./media/user-guide/fat-16-file-example.png)

**ŞEKIL 4. FileX FAT-16 dosya örneği**
