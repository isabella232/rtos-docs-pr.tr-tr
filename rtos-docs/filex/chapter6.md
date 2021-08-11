---
title: Bölüm 6 - Azure RTOS FileX hataya karşı iyi bir modül
description: Bu bölüm, medyanın güç kaybetmesi veya bir dosya yazma işlemi sırasında çıkarılırsa dosya sistemi bütünlüğünü korumak için tasarlanmış Azure RTOS FileX Hataya Karşı Koruma Modülü'ne ilişkin bir açıklama içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 66bffa2dbf52bc458bfaf124aa006a79e810100ac2e926c17444daf090519e66
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783794"
---
# <a name="chapter-6---azure-rtos-filex-fault-tolerant-module"></a>Bölüm 6 - Azure RTOS FileX hataya karşı iyi bir modül

Bu bölüm, medyanın güç kaybetmesi veya bir dosya yazma işlemi sırasında çıkarılırsa dosya sistemi bütünlüğünü korumak için tasarlanmış Azure RTOS FileX Hataya Karşı Koruma Modülü'ne ilişkin bir açıklama içerir.

## <a name="filex-fault-tolerant-module-overview"></a>FileX Hataya Karşı TolereAnt Modülüne Genel Bakış

Bir uygulama bir dosyaya veri yazdığında FileX hem veri kümelerini hem de sistem bilgilerini günceller. Bu güncelleştirmelerin, bilgileri dosya sisteminde tutarlı tutmak için atomik bir işlem olarak tamamlanması gerekir. Örneğin, bir dosyaya veri eklerken FileX'in medyada kullanılabilir bir küme bulması, FAT zincirini güncelleştirmesi, dizin girdisinde dosya uzunluğu güncelleştirmesi ve muhtemelen dizin girdisinde başlangıç küme numarasını güncelleştirmesi gerekir. Güç hatası veya medya çıkarma, güncelleştirme dizisini kesintiye uğratmaya neden olabilir ve bu da dosya sistemini tutarsız bir durumda bırakır. Tutarsız durum düzeltilmişse, güncelleştirilen veriler kaybolabilir ve sistem bilgilerine zarar verdiği için sonraki dosya sistemi işlemi medyanın diğer dosyalarına veya dizinlere zarar verebilir.

FileX Hataya Karşı İlke Modülü, bu adımlar  dosya sistemine uygulanmadan önce bir dosyayı güncelleştirmek için gereken adımların günlüklerini ayalar. Dosya güncelleştirmesi başarılı olursa, bu günlük girişleri kaldırılır. Ancak dosya güncelleştirmesi kesintiye uğrarsa günlük girişleri medyada depolanır. Medya bir sonraki takışında FileX, önceki (tamamlanmamış) yazma işlemiyle ilgili bu günlük girişlerini algılar. Böyle durumlarda FileX, dosya sisteminde zaten yapılan değişiklikleri geri göndererek veya önceki işlemi tamamlamak için gerekli değişiklikleri yeniden kullanarak bir hatadan kurtarılabilir. Bu şekilde, bir güncelleştirme işlemi sırasında medya güç kaybederse FileX Hataya Karşı Koruma Modülü dosya sistemi bütünlüğünü sürdürür.

> [!IMPORTANT]
> *FileX Hataya Karşı Koruma Modülü, içinde geçerli verilerle fiziksel medya bozulmasının neden olduğu dosya sistemi bozulmasını önlemek için tasarlanmamıştı.*

> [!IMPORTANT]
> *FileX Hataya Karşı Koruma modülü bir medyayı korumaya başladıktan sonra, medya, Hataya Karşı Özellikli DosyaX dışında hiçbir şey tarafından bağlı değildir. Bunu yapmak, dosya sistemideki günlük girişlerinin medyada sistem bilgileriyle tutarsız olmasına neden olabilir. Medya başka bir dosya sistemi tarafından güncelleştirildikten sonra FileX Hataya Karşı Tepkili modülü günlük girdilerini işlemeye çalışırsa, kurtarma yordamı başarısız olabilir ve dosya sisteminin tamamını öngörülemez bir durumda bırakabilirsiniz.*

## <a name="use-of-the-fault-tolerant-module"></a>Hataya Karşı İlke Modülünün Kullanımı

FileX Hataya Karşı İlke özelliği FAT12, FAT16, FAT32 ve exFAT dahil olmak üzere FileX tarafından desteklenen tüm FAT dosya sistemlerinde kullanılabilir. Hataya karşı tolere eden özelliği etkinleştirmek için FileX, tanımlandığı şekilde **FX_ENABLE_FAULT_TOLERANT** gerekir. Çalışma zamanında uygulama, _fx_fault_tolerant_enable _ çağrısının hemen ardından _ çağrısıyla ***hataya karşı fx_media_open.*** Hataya karşı korumalı etkinleştirildikten sonra, belirlenen medyaya yönelik tüm dosya yazma işlemleri korunur. Hataya karşı özellikli modül varsayılan olarak etkin değildir.

> [!IMPORTANT]
> *Uygulamanın, * uygulama _ çağrısından önce dosya sistemine **erişil fx_fault_tolerant_enable** emin olması gerekir. Uygulama, hataya karşı korumayı etkinleştirmeden önce dosya sistemine veri yazarsa, önceki yazma işlemleri tamamlanmamışsa ve dosya sistemi hataya karşı koruma günlük kaydı kullanılarak geri entries._

## <a name="filex-fault-tolerant-module-log"></a>FileX Hataya Karşı KarşıTlı Modül Günlüğü

FileX hataya karşı karşı olan günlük, bir mantıksal kümeyi flash olarak alır. Bu kümenin başlangıç küme numarasının dizini medyanın önyükleme kesimine kaydedilir ve simgesi tarafından belirtilen uzaklık değeri **FX_FAULT_TOLERANT_BOOT_INDEX.** Varsayılan olarak bu simge 116 olarak tanımlanır. Fat12/ 16/32 ve exFAT belirtimleri içinde ayrılmış olarak işaretlenen bu konum seçilir.

Şekil 5,"Günlük Yapısı Düzeni", günlük yapısının genel düzenini gösterir. Günlük yapısı üç bölüm içerir: Günlük Üst Bilgisi, FAT Zinciri ve Günlük Girişleri.

> [!IMPORTANT]
> *Günlük girişlerinde depolanan tüm çoklu bayt değerleri Little Endian biçimindedir.*

![Günlük Yapısı Düzeni](./media/user-guide/log-structure-layout.png)

**Şekil 5. Günlük Yapısı Düzeni**

Günlük Üst Bilgisi alanı, günlük yapısının tamamını açıklayan ve her alanı ayrıntılı olarak açıklayan bilgiler içerir.

**TABLO 8. Günlük Üst Bilgisi Alanı**

|Alan|Boyut (bayt cinsinden)|Description|
|-----|--------------|-----------|
|ID|4|FileX Hataya Karşı KarşıTlı Günlük yapısını tanımlar. Kimlik değeri doğrulanmazsa günlük yapısı geçersiz 0x46544C52.|
|Toplam Boyut|2|Günlük yapısının tamamının toplam boyutunu (bayt cinsinden) gösterir.|
|Üst Bilgi SağlamaLarı|2|Günlük üst bilgisi alanına dönüştüren sağlamalar. Üst bilgi alanları sağlama tam sayı doğrulamasında başarısız olursa günlük yapısı geçersiz olarak kabul edilir.|
|Sürüm Numarası|2|FileX Hataya Karşı Büyük ve Küçük Sürüm Numaraları.|
|Ayrılmıştır|2|Gelecekteki genişleme için.|

Günlük Üst Bilgisi alanı, FAT Zincir Günlüğü alanı tarafından takip ediliyor. Şekil 9'da FAT zincirinin nasıl değiştirileceklerini açıklayan bilgiler yer almaktadır. Bu günlük alanı bir dosyaya ayrılan kümeler, bir dosyadan kaldırılan kümeler ve ekleme/silmenin nerede olması gerektiği hakkında bilgiler içerir ve FAT Zincir Günlüğü alanında her alanı açıklar.

**TABLO 9. FAT Zincir Günlüğü Alanı**

|Alan|Boyut (bayt cinsinden)|Description|
|-----|--------------|-----------|
|FAT Zincir Günlüğü SağlamaLarı|2|FAT Zinciri Günlük alanı tamamının sağlamaları. SAĞLAMA tam sayı doğrulaması başarısız olursa FAT Zincir Günlüğü alanı geçersiz olarak kabul edilir.|
|Bayrak|1|Geçerli bayrak değerleri:<br/>0x01 FAT Chain Valid<br />0x02 BITMAP kullanılıyor|
|Ayrılmıştır|1|Gelecekteki kullanım için ayrılmıştır|
|Ekleme Noktası – Ön|4|Yeni oluşturulan zincirin ekli olduğu küme (özgün FAT zincirine ait olan).|
|Yeni FAT Zincirinin Baş Kümesi|4|Yeni oluşturulan FAT Zincirinin ilk kümesi|
|Özgün FAT Zincirinin Baş Kümesi|4|Kaldırılacak özgün FAT Zinciri bölümünün ilk kümesi.|
|Ekleme Noktası – Geri|4|Yeni oluşturulan FAT zincirinin bulunduğu özgün küme.|
|Sonraki Silme Noktası|4|Bu alan FAT zinciri temizleme yordamına yardımcı olur.|

Günlük Girişleri Alanı, bir hatadan kurtarmak için gereken değişiklikleri açıklayan günlük girdilerini içerir. FileX hataya karşı olan modülde desteklenen üç tür günlük girişi vardır: FAT Günlük Girişi; Dizin Günlüğü Girişi; ve Bit Eşlem Günlüğü Girişi.

Aşağıdaki üç rakam ve üç tablo, bu günlük girişlerini ayrıntılı olarak açıklar.

![FAT Günlük Girdisi](./media/user-guide/fat-log-entry.png)

**Şekil 6. FAT Günlük Girdisi**

**TABLO 10. FAT Günlük Girdisi**

|Alan|Boyut (bayt cinsinden)|Açıklama|
|-----|--------------|-----------|
Tür|2|Giriş türü, FX_FAULT_TOLERANT_FAT_LOG_TYPE|
|Boyut|2|Bu girişin boyutu|
|Küme Numarası|4|Küme numarası|
|Değer|4|FAT girdisine yazıldığı değer|

![Dizin Günlüğü Girişi](./media/user-guide/directory-log-entry.png)

**Şekil 7. Dizin Günlüğü Girişi**

**TABLO 11. Dizin Günlüğü Girişi**

|Alan|Boyut (bayt cinsinden)|Açıklama|
|-----|--------------|-----------|
|Tür|2|Giriş türü, FX_FAULT_TOLERANT_DIRECTORY_LOG_TYPE|
|Boyut|2|Bu girişin boyutu|
|Kesim Farkı|4|Bu dizinin bulunduğu kesime uzaklık (bayt cinsinden).|
|Günlük Kesimi|4|Dizin girişinin bulunduğu kesim|
|Günlük Verileri|Değişken|Dizin girişinin içeriği|

![Bit Eşlem Günlüğü Girişi](./media/user-guide/bitmap-log-entry.png)

**Şekil 8. Bit Eşlem Günlüğü Girişi**

**TABLO 12. Bit Eşlem Günlüğü Girişi**

|Alan|Boyut (bayt cinsinden)|Açıklama|
|-----|--------------|-----------|
|Tür|2|Giriş türü, FX_FAULT_TOLERANT_BITMAP_LOG_TYPE|
|Boyut|2|Bu girişin boyutu|
|Küme Numarası|4|Küme numarası|
|Değer|4|FAT girdisine yazıldığı değer|

## <a name="fault-tolerant-protection"></a>Hataya Karşı Koruma

FileX Hataya Karşı İlke Modülü başladıktan sonra, ilk olarak medyada mevcut hataya karşı tepkili bir günlük dosyasını arar. Geçerli bir günlük dosyası bulunamazsa, FileX medyayı korumasız olarak kabul ediyor. Bu durumda FileX, medya üzerinde hataya karşı tepkili bir günlük dosyası oluşturacak.

> [!IMPORTANT]
> *FileX Hataya Karşı Koruma Modülü başlamadan önce dosya sistemi bozuksa FileX koruyamaz. *

Hataya karşı karşı bir günlük dosyası bulunuyorsa, FileX var olan günlük girdilerini denetler. Günlük girişi olmadan bir günlük dosyası, önceki dosyanın başarılı olduğunu ve tüm günlük girdilerinin kaldırılmış olduğunu gösterir. Bu durumda uygulama, hataya karşı koruma ile dosya sistemini kullanmaya başlayabilir.

Ancak günlük girişleri bulunursa, FileX'in önceki dosya işlemini tamamlaması veya dosya sistemine zaten uygulanmış değişiklikleri geri döndürmesi, değişiklikleri etkili bir şekilde geri alması gerekir. Her iki durumda da, günlük girişleri dosya sistemine uygulandıktan sonra, dosya sistemi tutarlı bir durumda geri yüklenir ve uygulama dosya sistemini yeniden kullanmaya başlayabilir.

FileX tarafından korunan medyalarda, dosya güncelleştirme işlemi sırasında veri kısmı doğrudan medyaya yazılır. FileX verileri yazdığında, dizin girişlerine (FAT tablosu) uygulanması gereken tüm değişiklikleri de kaydedmektedir. Bu bilgiler, dosyanın karşıt günlük girişlerine kaydedilir. Bu yaklaşım, veriler medyaya yazıldığı zaman dosya sistemi güncelleştirmelerinin gerçekleşmesini garantiler. Medya veri yazma aşamasında çıkarılırsa, önemli dosya sistemi bilgileri henüz değişmemiştir. Bu nedenle dosya sistemi kesintiden etkilenmez.

Tüm veriler medyaya başarıyla yazıldıktan sonra FileX, değişiklikleri sistem bilgilerine tek tek bir girdi olarak uygularken günlük girişlerinde yer alan bilgileri izler. Tüm sistem bilgileri medyaya işlendikten sonra, günlük girişleri hataya karşı tepkili günlükten kaldırılır. Bu noktada, FileX dosya güncelleştirme işlemini tamamlar.

Dosya güncelleştirme işlemi sırasında dosyalar yerinde güncelleştirilmez. Hataya karşı koruma modülü, yeni verilerin yazılacak verileri yazması için bir kesim ayırır ve ardından üzerine yazılacak verileri içeren kesimi kaldırır ve yeni kesimi chian'a bağlaması için ilgili FAT girişlerini güncelleştirin. Bir kümede kısmi verilerin değiştirilmesi gereken durumlarda FileX her zaman yeni kümeler ayırır, güncelleştirilmiş verilerle eski kümelerden tüm verileri yeni kümelere yazar ve ardından eski kümeleri serbest yazar. Bu, dosya güncelleştirmesi kesintiye uğrarsa özgün dosyanın bozulmamış olduğunu garantiler. Uygulamanın FileX hataya karşı koruma altında, bir dosyada verileri güncelleştirmek için medyanın eski verilere sahip kesimlerin serbest bırakılamadan önce yeni verileri tutmak için yeterli boş alana sahip olması gerektiğinin farkında olması gerekir. Medyada yeni verileri tutmak için yeterli alan yoksa güncelleştirme işlemi başarısız olur.
