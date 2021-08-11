---
title: Bölüm 3-Azure RTOS FileX 'in Işlevsel bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS FileX katıştırılmış dosya sisteminin bir açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bb2e1d7f10d71ed01a040cea63e9e469855525d89dd6318f3147c61ed166ee4c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783082"
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
- **Tura Sayısı** Medya *önyükleme kaydında* tura sayısı alanı, medyada tura sayısını tanımlar. Bu genellikle yalnızca gerçek disk türü medyayla ilgilidir. FLASH cihazları bu eşlemeyi kullanmaz.
- **Gizli Kesimler** Medya *önyükleme kaydında* gizli kesimler alanı, önyükleme kaydı öncesinde kesim sayısını tanımlar. Bu alan, dosya **denetim FX_MEDIA** korunur ve FileX tarafından yapılan tüm okuma ve yazma isteklerinde FileX I/O sürücülerde hesaba katları gerekir.
- **Sektör Sayısı FAT-32** Medya *önyükleme kaydında* kesim sayısı alanı yalnızca kesimlerin iki baytı alanı *sıfırsa* geçerlidir. Böyle bir durumda, bu dört bayt alanı medyada kesim sayısını içerir.
- **FAT başına kesim sayısı (FAT-32)** *FAT (FAT-32)* alanı başına kesimler yalnızca FAT-32 biçiminde geçerlidir ve medyanın her FAT'sı için ayrılan kesim sayısını içerir.
- **Kök Dizin Kümesi** Kök *dizin kümesi alanı* yalnızca FAT-32 biçiminde geçerlidir ve kök dizinin başlangıç küme numarasını içerir.
- **Sistem Önyükleme Kodu** Sistem *önyükleme kodu alanı,* önyükleme kodunun küçük bir kısmını depolamak için bir alandır. Günümüzde çoğu cihaz için bu eski bir alandır.
- **İmza 0x55AA** İmza *alanı,* önyükleme kaydını tanımlamak için kullanılan bir veri desenidir. Bu alan yoksa önyükleme kaydı geçerli değildir.

### <a name="exfat"></a>Exfat

FAT32'de dosya boyutu üst sınırı 4 GB'tır ve bu da yüksek tanımlı multimedya dosyalarının geniş kapsamlı benimsenmelerini sınırlar. Fat32 varsayılan olarak 32 GB'a kadar depolama medyası destekler. Flash ve SD kart kapasitesi artarak FAT32, büyük hacimleri yönetmede daha az verimli hale gelir. exFAT, bu sınırlamaları aşmak için tasarlanmıştır. exFAT, yaklaşık bir milyar GB olan en fazla bir Exabayt (EB) dosya boyutunu destekler. exFAT ile FAT32 arasındaki bir diğer önemli fark da exFAT'ın bir birim içinde kullanılabilir alanı yönetmek için bit eşlem kullanması ve bu da exFAT'nin dosyaya veri yazarken kullanılabilir alan bulma konusunda daha verimli hale bulunmasıdır. Bitişik kümelerde depolanan dosyalarda exFAT, tüm kümeleri bulmak için FAT zincirinde aşağı doğru ilerler ve büyük dosyalara erişirken daha verimli hale getirir. exFAT, 32 GB'tan büyük flash depolama ve SD kartları için gereklidir.

### <a name="exfat-logical-sectors"></a>exFAT Mantıksal Kesimleri

ExFAT'ta medyanın mantıksal kesimlerinin genel düzeni Şekil 2'de gösterildiği gibi. ExFAT'ta önyükleme bloğu ve FAT alanı Sistem Alanına aittir. Kümelerin geri kalanı Kullanıcı Alanı'dır. Gerekli değildir, ancak exFAT standardı, Ayırma Bit Eşlemi'nin Kullanıcı Alanı'nın başında ve ardından Up-case Table ve kök dizinde olması önerilir.

### <a name="exfat-media-boot-record"></a>exFAT Medya Önyükleme Kaydı

exFAT'daki Medya Önyükleme Kaydı içeriği FAT12/16/32'de bulunanlardan farklıdır. Bunlar Tablo 2'de listelenir. Karışıklığı önlemek için, FAT12/16/32 0x40 de çeşitli medya parametreleri içeren 0x0B ve 0x40 arasındaki alan exFAT içinde *Ayrılmış* olarak işaretlenir. Bu ayrılmış alan sıfırlarla programlanmış olmalı ve Medya Önyükleme Kaydı'nın yanlış yorumlandırılmasından kaçınılmalıdır.

![exFAT Mantıksal Kesimleri](./media/user-guide/exfat-logical-sectors.png)

**ŞEKIL 2. exFAT Mantıksal Kesimleri**

- **Atlama Yönergesi** Atlama *yönergesi* alanı, işlemci atlama için Intel x86 makine yönergesini temsil eden üç baytlık bir alandır. Bu, çoğu durumda eski bir alandır.

    **TABLO 2. exFAT Medya Önyükleme Kaydı**

    |Uzaklık  |Alan  |Bayt Sayısı|
    |----------|-----------|------------|
    |0x00|Atlama Yönergesi|3|
    |0x03|Dosya Sistemi Adı|8|
    |0x0B|Ayrılmıştır|53|
    |0x40|Bölüm Uzaklığı|8|
    |0x48|Birim Uzunluğu|8|
    |0x50|FAT Uzaklığı|4|
    |0x54|FAT Uzunluğu|4|
    |0x58|Küme Yığını Uzaklığı|4|
    |0x5C|Küme Sayısı|4|
    |0x60|Kök Dizinin İlk Kümesi|4|
    |0x64|Birim Seri Numarası|4|
    |0x68|Dosya Sistemi Düzeltmesi|2|
    |0x6A|Birim Bayrakları|2|
    |0x6C|Kesim Başına Bayt Kaydırma|1|
    |0x6D|Küme Başına Kesim Kaydırma|1|
    |0x6E|SSS Sayısı|1|
    |0x6F|Sürücü Seçme|1|
    |0x70|Kullanım Yüzde|7|
    |0x71|Ayrılmıştır|1|
    |0x78|Önyükleme Kodu|390|
    |0x1FE|Önyükleme İmzası|2|

- **Dosya Sistemi Adı** exFAT için *dosya sistemi adı alanı* "EXFAT" ve ardından üç boşluk eksildi.
- **Ayrılmış** Ayrılmış alanın *içeriği* sıfır olmalıdır. Bu bölge FAT12/16/ 32'de önyükleme kayıtlarıyla çakışıyor. Bu alanı sıfıra yapmak, dosya sistemlerinin bu birimi yanlış yorumlamalarını önler.
- **Bölüm Uzaklığı** Bölüm *uzaklığı alanı* bu bölümün başlatı olduğunu gösterir.
- **Birim Uzunluğu** Birim *uzunluğu* alanı, bu bölümün kesim sayısı olarak boyutunu tanımlar.
- **FAT Uzaklığı** *FAT kaydırma* alanı, bu bölümün FAT tablosuna göre bu bölümün başlangıcına göre başlangıç kesim numarasını tanımlar.
- **FAT Uzunluğu** *FAT uzunluğu* alanı, FAT tablosu boyutunu kesim sayısı olarak tanımlar.
- **Küme Yığını Uzaklığı** Küme *yığını kaydırma* alanı, küme yığınının bölüm başlangıcına göre başlangıç kesim numarasını tanımlar. Küme yığını, dizin bilgilerini ve dosya verilerini depolandığı alandır.
- **Küme Sayısı** Küme *sayısı* alanı, bu bölümün sahip olduğu küme sayısını tanımlar.
- **Kök Dizinin İlk Kümesi** İlk *kök dizin alanı kümesi,* kök dizinin başlangıç konumunu tanımlar. Bu konumun ayırma bit eşlemi ve büyük/büyük/büyük harf tablosundan hemen sonra olması önerilir.
- **Birim Seri Numarası** Birim *seri numarası* alanı bu bölümün seri numarasını tanımlar.
- **Dosya Sistemi Düzeltmesi** Dosya *sistemi düzeltme alanı* exFAT'nin ana ve ikincil sürümünü tanımlar.
- **Birim Bayrakları** Birim *bayrakları* alanı, bu birimin durumunu belirten bayraklar içerir.
- **Kesim Başına Bayt Kaydırma** Kesim *kaydırma alanı başına bayt* sayısı, kesim başına bayt sayısını (log2(n) tanımlar; burada n, kesim başına bayt sayısıdır. Örneğin, SD kartında kesim boyutu 512 bayttır. Bu nedenle bu alan 9 (log2(512) = 9) olur.
- **Küme Başına Kesim Kaydırma** Küme *başına kesim kaydırma* alanı, log2(n) içinde küme başına kesim sayısını tanımlar; burada n, küme başına kesim sayısıdır.
- **SSS Sayısı** *SSS alanı,* bu bölümdeki FAT tablolarının sayısını tanımlar. ExFAT için, bir FAT tablosu için değerin 1 olması önerilir.
- **Sürücü Seçme** Sürücü *seçme alanı* genişletilmiş INT 13h sürücü numarasını tanımlar.
- **Kullanım Yüzde** Kullanım *alanında yüzde* değeri, küme yığınında ayrılan kümelerin yüzdesini tanımlar. Geçerli değerler 0 ile 100 (dahil) arasındadır.
- **Ayrılmış** Bu alan gelecekte kullanılmak üzere ayrılmıştır.
- **Önyükleme Kodu** Önyükleme *kodu alanı,* önyükleme kodunun küçük bir kısmını depolamak için bir alandır. Günümüzde çoğu cihaz için bu eski bir alandır.
- **İmza 0x55AA** Önyükleme *imzası alanı,* önyükleme kaydını tanımlamak için kullanılan bir veri desenidir. Bu alan yoksa önyükleme kaydı geçerli değildir.

### <a name="file-allocation-table-fat"></a>Dosya Ayırma Tablosu (FAT)

Dosya *Ayırma Tablosu (FAT),* medyadaki ayrılmış kesimlerden sonra başlar. FAT alanı temelde bu kümenin ayrılmış olup olmadığını veya alt dizin ya da dosyadan oluşan bir küme zincirinin parçası olup olmadığını belirleyen 12 bit, 16 bit veya 32 bit girişlerden oluşan bir dizidir. Her FAT girişinin boyutu, temsili gereken küme sayısına göre belirlenir. Küme sayısı (küme başına kesimlere bölünen toplam kesimden türetilen) 4.086'dan küçükse veya ona eşitse, 12 bit FAT girişleri kullanılır. Toplam küme sayısı 4.086'dan büyükse ve 65.525'in altında ise 16 bit FAT girişleri kullanılır. Aksi takdirde, toplam küme sayısı 65.525'den büyük veya bu sayıya eşitse 32 bit FAT veya exFAT kullanılır.

FAT12/16/32 için FAT tablosu yalnızca küme zincirini korumakla birlikte küme ayırma hakkında da bilgi sağlar: bir kümenin kullanılabilir olup olmadığı. exFAT'ta, küme ayırma bilgileri bir Ayırma Bit Eşlem Dizini Girdisi tarafından korunur. Her bölümün kendi ayırma bit eşlemi vardır. Bit eşlem boyutu, kullanılabilir tüm kümeleri kapsayacak kadar büyüktür. Bir küme ayırma için kullanılabilirse, bit eşlem ayırmada karşılık gelen bit 0 olarak ayarlanır. Aksi takdirde bit 1 olarak ayarlanır. Ardışık kümeleri kapladığı bir dosya için exFAT, tüm kümeleri izlemek için FAT zinciri gerektirmez. Ancak art arda kümeler kap etmeyen bir dosya için FAT zincirinin yine de korunması gerekir.

### <a name="fat-entry-contents"></a>FAT Giriş İçeriği

FAT tablosundaki ilk iki giriş kullanılmaz ve genellikle aşağıdaki içeriklere sahip olur.

|FAT Girişi |12 bit FAT|16 bit FAT|32 bit FAT| Exfat|
|----------|-----------|------------|-------|------|
|Giriş 0|0x0F0|0x00F0|0x000000F0|0xF8FFFFFF|
|Giriş 1|0xFFF|0xffff|0x0FFFFFFF|0xffffffff|

FAT giriş numarası 2, medyanın veri alanında ilk kümeyi temsil eder. Her küme girişinin içeriği, bunun ücretsiz olup olmadığını veya bir dosya veya alt dizin için ayrılmış bağlı küme listesinin bir parçası olup olmadığını belirler. Küme girdisi başka bir geçerli küme girdisi içeriyorsa, küme ayrılır ve değeri küme zincirinde ayrılan sonraki kümeyi gösterir.

Olası küme girişleri aşağıdaki gibi tanımlanır.

|Anlamı|12 bit FAT|16 bit FAT|32 bit FAT| Exfat|
|----------|-----------|------------|-------|------|
|Ücretsiz Küme|0x000|0x0000|0x00000000|0x00000000|
|Kullanılmaz|0x001|0x0001|0x00000001|0x00000001|
|Ayrılmıştır|0xFF0-FF6|0xFFF0-FFF6|0x0FFFFFF0-6|ClusterCounter +2'den 0xFFFFFFF6|
|Hatalı Küme|0xFF7|0xFFF7|0x0FFFFFF7|0xFFFFFFF7|
|Ayrılmıştır| - | - | - | 0xFFFFFFF8-E|
|Son Küme| 0xFF8-FFF| 0xFFF8-FFFF| 0x0FFFFFF8-F| 0xffffffff|
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

filex, hem 8,3 hem de Windows uzun dosya adı (lfn) ad biçimlerini destekler. Adın yanı sıra, her bir dizin girişi girişin özniteliklerini, son değiştirilme tarihi ve tarihini, başlangıç kümesi dizinini ve girişin bayt cinsinden boyutunu içerir. Tablo 3, bir FileX 8,3 dizin girişinin içeriğini ve boyutunu gösterir.

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

    İki bayt *LFN Kümesi* alanı kullanılmaz ve her zaman 0'dır.

    **TABLO 5. 39 Karakterli LFN'den Oluşan Dizin Girişleri**

    |Giriş|Anlamı|
    |------------|-----------|
    |1|LFN Dizin Girişi 3|
    |2|LFN Dizin Girişi 2|
    |3|LFN Dizin Girişi 1|
    |4|8.3 Dizin Girişi (ttttt~n.xx)|

### <a name="exfat-directory-description"></a>exFAT Dizin Açıklaması

exFAT dosya sistemi dizin girişini ve dosya adını farklı depolar. Dizin girdisi, girişin özniteliklerini, girişin ne zaman oluşturulduğunda, değiştirildiğinde ve erişildiğinde çeşitli zaman damgasını içerir. Dosya boyutu ve kümeyi başlatma gibi diğer bilgiler, birincil dizin girişinin hemen ardından geçen Stream Uzantısı Dizin Girdisi'ne depolanır. exFAT yalnızca Uzun Dosya Adı (LFN) ad biçimini destekler. Dosya Adı Dizin Girdisi'ne depolanmış olan dizin, Tablo 2'de gösterildiği gibi Stream Extension Directory Girdisi'nin hemen ardından gelir.

### <a name="exfat-file-directory-entry"></a>exFAT Dosya Dizini Girişi

Aşağıdaki tabloda ve paragraflarda exFAT dosya dizini girişinin ve içeriğinin açıklaması yer alır.

- **Giriş Türü**

    Giriş türü alanı bu girişin türünü gösterir. Dosya Dizini Girişi için bu alanın 0x85.

- **İkincil Giriş Sayısı**

    İkincil *giriş sayısı* alanı, bu birincil girdiden hemen sonra ikincil giriş sayısını gösterir. Dosya dizini girdisi ile ilişkili ikincil girişler, bir akış uzantısı dizin girişi ve bir veya daha fazla dosya adı dizin girdisi içerir.

    **TABLO 6. exFAT Dosya Dizini Girişi**

    |Uzaklık|Alan|Bayt Sayısı|
    |----|-----------|-|
    |0x00|Giriş Türü|1|
    |0x01|İkincil Giriş|1|
    |0x02|Sağlama|2|
    |0x04|Dosya Öznitelikleri|2|
    |0x06|Ayrılmış 1|2|
    |0x08|Zaman Damgası Oluştur|4|
    |0x0C|Son Değiştirilen Zaman Damgası|4|
    |0x10|Son Erişilen Zaman Damgası|4|
    |0x14|10 m'lik Artış Oluşturma|1|
    |0x15|Son Değiştirme 10 saniyeLik Artış|1|
    |0x16|UTC Farkı Oluşturma|1|
    |0x17|Son Değiştirilen UTC Farkı|1|
    |0x18|Son Erişim UTC Farkı|1|
    |0x19|Ayrılmış 2|7|

- **Sağlama toplamı**

    Sağlama *listesi* alanı, dizin giriş kümesinde (dosya dizini girdisi ve ikincil girdileri) tüm girişler üzerinde sağlama listesi değerini içerir.

- **Dosya Öznitelikleri**

    Tek bir bayt öznitelikler alan girdisi, dizin girişinin çeşitli özelliklerini belirten bir dizi bit içerir. Çoğu öznitelik biti, FAT 12/16/32 ile aynıdır. Dizin özniteliği tanımları aşağıdaki gibidir:

    |Öznitelik Biti|Anlamı|
    |------------|-----------|
    |0x01| Giriş salt okunur|
    |0x02|Girdi gizli|
    |0x04|Girdi bir sistem girişidir|
    |0x08|Girdi ayrılmış|
    |0x10|Girdi bir dizindir|
    |0x20|Girdi değiştirildi|
    |Diğer tüm bitler|Ayrılmıştır|

- **Ayrılmış1**

    Bu alan sıfır olmalıdır.

- **Zaman Damgası Oluştur**

    Create  *10ms Increment* alanından alınan bilgileri birleştiren oluşturma zaman damgası alanı, dosyanın veya dizinin oluşturularak yerel tarihi ve saati açıklar.

- **Son Değiştirilen Zaman Damgası**

    Son *değiştirilen zaman damgası alanı,* son değiştirilen *10 m'lik* artış alanından alınan bilgileri birleştirerek dosyanın veya dizinin en son değiştiril olduğu yerel tarihi ve saati açıklar. Zaman damgası hakkında aşağıdaki notlara bakın.

- **Son Erişilen Zaman Damgası**

    Son *erişilen zaman damgası* alanında, dosyanın veya dizinin son erişilen yerel tarihi ve saati açıklanır. Zaman damgası hakkında aşağıdaki notlara bakın.

- **10 m'lik Artış Oluşturma**

    Create *10ms artırma* alanı, *oluşturma zaman damgası* alanından alınan bilgileri birleştirerek dosyanın veya dizinin oluşturularak yerel tarihi ve saati açıklar. Zaman damgası hakkında aşağıdaki notlara bakın.

- **Son Değiştirme 10 saniyeLik Artış**

    Son değiştirilen zaman damgası alanından bilgileri birleştirerek  son değiştirilen *10 saniyelik* artış alanı, dosyanın veya dizinin en son değiştirildiğinde yerel tarihi ve saati açıklar. Zaman damgası hakkında aşağıdaki notlara bakın.

- **UTC Farkı Oluşturma**

    UTC *farkı oluşturma* alanı, dosyanın veya dizinin oluşturulduğunda yerel saatle UTC saati arasındaki farkı açıklar. Zaman damgası hakkında aşağıdaki notlara bakın.

- **Son Değiştirilen UTC Farkı**

    Son *değiştirilen UTC kaydırma alanı,* dosyanın veya dizinin son değiştirildiğinde yerel saatle UTC saati arasındaki farkı açıklar. Zaman damgası hakkında aşağıdaki notlara bakın.

- **Son Erişilen UTC Farkı**

    Son *erişilen UTC uzaklığı* alanı, dosya veya dizine en son erişilen yerel saat ile UTC saati arasındaki farkı açıklar. Zaman damgası hakkında aşağıdaki notlara bakın.

- **Ayrılmış2**

    Bu alan sıfır olmalıdır.

### <a name="notes-on-timestamps"></a>Zaman Damgası Notları

- **Zaman Damgası Girişi** Zaman damgası alanları aşağıdaki gibi yorumlanır:

- **10 m'lik Artış Alanları** 10 m'lik artış alanında yer alan değer, zaman damgası değerine daha ince ayrıntı sağlar. Geçerli değerler 0 (0ms) ile 199 (1990ms) arasındadır.

     ![10 m'lik Artış Alanları](./media/user-guide/10ms-increment-fields.png)

- **UTC Uzaklık Alanı**

     ![UTC Uzaklık Alanı](./media/user-guide/utc-offset-field.png)

- **Uzaklık Değeri**

    7 bit imzalı tamsayı, UTC saatiyle uzaklığı 15 dakikalık artışlarla temsil eder.

- **Geçerli**

    Uzaklık alanı değerinin geçerli olup olmadığı. 0, uzaklık değeri alanında yer alan değerin geçersiz olduğunu gösterir. 1 değerin geçerli olduğunu gösterir.

### <a name="stream-extension-directory-entry"></a>Stream Uzantısı Dizin Girişi

Stream Uzantısı Dizin Girdisi'nin ve içeriğinin açıklaması aşağıdaki tabloya ek olarak ek açıklamadır.

**TABLO 7. Stream Uzantısı Dizin Girişi**

|Uzaklık|Alan| Bayt Sayısı|
|------------|-----------|-------|
|0x00|Giriş Türü|1|
|0x01|Bayraklar|1|
|0x02|Ayrılmış 1|1|
|0x03|Ad Uzunluğu|1|
|0x04|Ad Karması|2|
|0x06|Ayrılmış 2|2|
|0x08|Geçerli Veri Uzunluğu|8|
|0x10|Ayrılmış 3|4|
|0x14|İlk Küme|4|
|0x18|Veri Uzunluğu|8|

- **Giriş Türü**

    Giriş *türü alanı* bu girişin türünü gösterir. Akış uzantısı Dizin Girişi için bu alanın 0xC0.

- **Bayrak**

    Bu alan çeşitli özellikleri belirten bir dizi bit içerir:
    
    |Bayrak Biti|Anlamı    |
    |-----------------|-----------|
    |0x01            |Bu alan, küme ayırmanın mümkün olup olmadığını gösterir. Bu alan 1 olabilir.|
    |0x02            |Bu alan, ilişkili kümelerin bitişik olup olmadığını gösterir. 0 değeri FAT girişinin geçerli olduğu ve FileX'in FAT zincirini izlemesi gerekir. 1 değeri FAT girişinin geçersiz olduğu ve kümelerin bitişik olduğu anlamına gelir.|
    |Diğer tüm bitler    |Ayrılmış.|

- **Ayrılmış 1**

    Bu alan 0'dır.

- **Ad Uzunluğu**

    Ad *uzunluğu alanı,* dosya adı dizin girişlerinin topluca içerdiği unicode dizesinin uzunluğunu içerir. Dosya adı dizin girdileri bu akış uzantısı dizin girişini hemen takip eder.

- **Ad Karması**

    Ad *karması* alanı, büyük/küçük harfli dosya adının karma değerini içeren bir 2 bayt girişidir. Karma değeri dosya/dizin adı aramasını daha hızlı sağlar: Karma değerleri eşlenemse, bu girişle ilişkili dosya adı eşleşmez.

- **Ayrılmış 2**

    Bu alan 0'dır.

- **Geçerli Veri Uzunluğu**

    Geçerli *veri uzunluğu* alanı dosyada geçerli veri miktarını gösterir.

- **Ayrılmış 3**

    Bu dosya 0 olmalı.

- **İlk Küme**

    İlk *küme alanı,* veri akışının ilk kümesi dizinini içerir.

- **Veri Uzunluğu**

    Veri *uzunluğu alanı,* ayrılan kümelerde toplam bayt sayısını içerir. ExFAT, veri *kümelerinin önceden ayırmaya* izin verir çünkü bu değer Geçerli Veri Uzunluğu'dan büyük olabilir.

### <a name="root-directory"></a>Kök Dizin

FAT 12 ve 16 bit biçimlerinde kök dizin, medyada tüm FAT kesimlerinden hemen sonra bulunur ve açık *_* FX_MEDIA * denetim bloğunda *  **fx_media_root_sector_start** _ inceler. Kök dizinin boyutu, dizin girişlerinin sayısı bakımından (her 32 bayt boyutunda), medyanın önyükleme kaydındaki ilgili giriş tarafından belirlenir.

FAT-32 ve exFAT'daki kök dizin, kullanılabilir kümelerin herhangi bir yerinde yer alıyor olabilir. Konumu ve boyutu, medya açıldığında önyükleme kaydından belirlenir. Medya açıldıktan sonra, ***fx_media_root_sector_start*** alanı FAT-32 veya exFAT kök dizininin başlangıç kümelerini bulmak için kullanılabilir.

### <a name="subdirectories"></a>Altdizin

FAT sisteminde herhangi bir sayıda alt dizin vardır. Alt dizinin adı, tıpkı dosya adı gibi bir dizin girdisinde bulunur. Ancak dizin özniteliği belirtimi (0x10), girişin bir alt dizin olduğunu ve dosya boyutunun her zaman sıfır olduğunu belirtmek için ayarlanır.
Şekil 3'te * SAMPLE adlı yeni bir tekli alt dizin için tipik bir alt dizin yapısının nasıl göründüğünü **gösterir. DIR** _ _* adlı bir dosya ile _FILE.TXT_** .
Çoğu şekilde, alt dizinler dosya girişlerine çok benzer. İlk küme alanı, bağlantılı bir küme listesinin ilk kümesine puanlar. Bir alt dizin oluşturulduğunda, ilk iki dizin girdisi varsayılan dizinleri ( "." dizini ve ".." dizini) içerir. "." dizini alt dizinin kendisini, ".." dizini ise önceki veya üst dizini gösterir.

### <a name="global-default-path"></a>Genel Varsayılan Yol

FileX, medya için genel bir varsayılan yol sağlar. Varsayılan yol, açıkça tam yol belirtmeen herhangi bir dosya veya dizin hizmeti için kullanılır.

Başlangıçta, genel varsayılan dizin medyanın kök dizinine ayarlanır. Bu, fx_directory_default_set çağrılarak ***uygulama tarafından değiştirilebilir.***

Medyanın geçerli varsayılan yolu * fx_directory_default_get _ **çağrılarak incelendi.** Bu yordam, _ FX_MEDIA * denetim bloğu içinde bakımı yapılan varsayılan *yol dizesine bir dize* işaretçisi sağlar.

### <a name="local-default-path"></a>Yerel Varsayılan Yol

FileX ayrıca farklı iş parçacıklarının çakışma olmadan benzersiz yollara sahip olması için iş parçacığına özgü bir varsayılan yol sağlar. Çağrı **FX_LOCAL_PATH,** çağrı iş parçacığının yerel yolunu değiştirmek için **_fx_directory_local_path_set_*_* ve _ _fx_directory_local_path_restore_** çağrısı sırasında uygulama tarafından sağlanır.

Yerel yol varsa, yerel yol genel varsayılan medya yolundan önceliklidir. Yerel yol ayarlanmazsa veya fx_directory_local_path_clear ile temizlirse, medyanın genel varsayılan yolu bir kez daha kullanılır. 

## <a name="file-description"></a>Dosya Açıklaması

FileX, standart 8.3 karakterini ve üç karakterli uzantılara sahip uzun dosya adlarını destekler. ASCII adına ek olarak, her dosya girişi girdinin özniteliklerini, son değiştirme tarihini ve tarihini, başlangıç küme dizinini ve girişin bayt cinsinden boyutunu içerir.

### <a name="file-allocation"></a>Dosya Ayırma

FileX, FAT biçiminin standart küme ayırma şemasını destekler. FileX ayrıca bitişik kümelerin küme öncesi ayırmayı da destekler. Bunu karşılamak için, her FileX dosyası ayrılmış kümeler ile oluşturulur. Kümeler sonraki yazma isteklerinde veya bitişik ***fx_file_allocate*** önceden ayırma isteklerinde ayrılır.

Şekil 4'te "FileX FAT-16 Dosya Örneği", ***küme*** 101'den başlayarak ayrılmış iki sıralı kümeyle birlikteFILE.TXTadlı bir dosyayı, 26 boyutunda ve dosyanın ilk veri kümesi numarası 101'de yer alan veriler olarak alfabeyi gösterir.

### <a name="file-access"></a>Dosya Erişimi

Bir FileX dosyası, okuma erişimi için aynı anda birden çok kez açılabilir. Ancak, bir dosya yazmak için yalnızca bir kez açılabilir. Dosya erişimini desteklemek için kullanılan bilgiler, dosya denetim ***bloğunda FX_FILE*** içerir.

> [!NOTE]
> *Medya sürücüsünün dinamik olarak yazma koruması ayarlayana dikkat eder. Bu durumda tüm yazma istekleri reddedilir ve yazma için bir dosya açma girişimleri de reddedilir.*

### <a name="file-layout-in-exfat"></a>exFAT'ta Dosya Düzeni

ExFAT tasarımı, veriler sıkıcı kümelerde depolanıyorsa bir dosya için FAT zincirinin korunmasını gerektirmez. Stream Uzantısı *Dizin Girdisi'nin NoFATChain* biti, dosyadan veri okurken FAT zincirinin kullanıla mı olacağını belirtir. *NoFATChain* ayarlanırsa, FileX Stream Uzantısı Dizin Girdisi'nin  İlk Küme alanında belirtilen kümeden sırayla okur.

Öte *yandan, NoFATChain* netse FileX, FAT12/16/32'de FAT zincirine benzer şekilde dosyanın tamamını çapraz geçiş yapmak için FAT zincirini takip eder.

Şekil 3'te biri FAT zinciri gerektirmeyen ve diğeri FAT zinciri gerektiren iki örnek dosya vardır.

## <a name="system-information"></a>Sistem Bilgileri

FileX sistem bilgileri, açık medya örneklerini takip etmek ve genel sistem saat ve tarihini korumakla oluşur.

![Bitişik Kümelere Sahip Dosya ile FAT Bağlantısı Gerektiren Dosya karşılaştırması](./media/user-guide/system-information.png)

**ŞEKIL 3. Bitişik Kümelere Sahip Dosya ile FAT Bağlantısı Gerektiren Dosya karşılaştırması**

Varsayılan olarak, sistem tarihi ve saati FileX'in son yayın tarihine ayarlanır. Doğru sistem tarihi ve saati olması için, uygulama başlatma sırasında ***fx_system_time_set** _ ve _ *_fx_system_date_set_** çağrısında olmalıdır.

### <a name="system-date"></a>Sistem Tarihi

FileX sistem tarihi, genel değişkende ***_fx_system_date*** korunur. Bit 15 ile 9 arasında 1980'den yıl uzaklığı, 8 ile 5 arasında bitler ay farkı ve 4 ile 0 arasında bitler günü içerir. |

### <a name="system-time"></a>Sistem Saati

FileX sistem zamanı genel değişkende ***_fx_system_time*** korunur. Bit 15 ile 11 arasında saat, 10 ile 5 arası bitler dakika, 4 ile 0 arası bitler ise yarım saniyeyi içerir.

### <a name="periodic-time-update"></a>Düzenli Aralıklarla Zaman Güncelleştirmesi

Sistem başlatma sırasında FileX, sistem tarih ve saatlerini düzenli aralıklarla güncelleştirmek için bir ThreadX uygulama zamanlayıcısı oluşturur. Sistem tarih ve saat güncelleştirme hızı, _fx_system_initialize işlevi tarafından ***kullanılan iki sabit tarafından*** belirlenir.

Aynı zaman **FX_UPDATE_RATE_IN_SECONDS** **FX_UPDATE_RATE_IN_TICKS** sabitleri aynı dönemi temsil ediyor. Bu **FX_UPDATE_RATE_IN_TICKS** sabiti, FX_UPDATE_RATE_IN_SECONDS sabiti tarafından belirtilen saniye sayısını temsil eden ThreadX zamanlayıcı tık **sayısıdır.** Yeni **FX_UPDATE_RATE_IN_SECONDS** sabiti, her FileX saat güncelleştirmesi arasında kaç saniye olduğunu belirtir. Bu nedenle, iç FileX süresi aralıklarla artarak **FX_UPDATE_RATE_IN_SECONDS.** Bu sabitler, fx_system_initialize _ derlemesi sırasında sağlanmalıdır veya geliştirici, FileX yayınlarının ***_*_fx_port.h_** dosyasında bulunan varsayılanları değiştirebilir.

Düzenli FileX zamanlayıcısı yalnızca yalnızca dosya zaman damgası için kullanılan genel sistem tarih ve saati güncelleştirmek için kullanılır. Zaman damgası gerekli yoksa, FileX **FX_NO_TIMER zamanlayıcısının** oluşturulmasını ortadan kaldırmak için **_fx_system_initialize.c derlemesi_** sırasında tek yapmanız gereken bu işlemi tanımlamaktır.

![FileX FAT-16 Dosya Örneği](./media/user-guide/fat-16-file-example.png)

**ŞEKIL 4. FileX FAT-16 Dosya Örneği**
