---
title: Bölüm 6-Azure RTOS FileX hataya dayanıklı modül
description: Bu bölümde, medya güç kaybettiğinde veya dosya yazma işleminin ortasında çıkarıldığında dosya sistemi bütünlüğünü sürdürmek üzere tasarlanan Azure RTOS FileX hata toleranslı modülünün bir açıklaması bulunur.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 68a24f0345a2c4d3e824270699b00a2daab32f8e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826506"
---
# <a name="chapter-6---azure-rtos-filex-fault-tolerant-module"></a>Bölüm 6-Azure RTOS FileX hataya dayanıklı modül

Bu bölümde, medya güç kaybettiğinde veya dosya yazma işleminin ortasında çıkarıldığında dosya sistemi bütünlüğünü sürdürmek üzere tasarlanan Azure RTOS FileX hata toleranslı modülünün bir açıklaması bulunur.

## <a name="filex-fault-tolerant-module-overview"></a>FileX hataya dayanıklı modüle genel bakış

Bir uygulama bir dosyaya veri yazdığında, FileX veri kümelerini ve sistem bilgilerini güncelleştirir. Bu güncelleştirmelerin, dosya sistemindeki bilgilerin tutarlı tutulması için atomik bir işlem olarak tamamlanması gerekir. Örneğin, bir dosyaya veri eklerken, FileX 'in medyada kullanılabilir bir kümeyi bulması, FAT zincirini güncelleştirmesi, Dizin girişinde dosyalanan uzunluğu güncelleştirmesi ve Dizin girişinde başlangıç kümesi numarasını güncelleştirmesi gerekir. Güç kesintisi veya medya çıkarma, güncelleştirme dizisini kesintiye uğratabilir, bu da dosya sistemini tutarsız bir durumda bırakır. Tutarsız durum düzeltilmemişse, güncelleştirilmekte olan veriler kaybolabilir ve sistem bilgilerine zarar verebileceğinden, sonraki dosya sistemi işlemi ortamdaki diğer dosyalara veya dizinlere zarar verebilir.

FileX hata toleransı modülü, bu adımlar dosya sistemine uygulanmadan *önce* bir dosyayı güncelleştirmek için gereken günlüğe kaydetme adımları ile işe yarar. Dosya güncelleştirmesi başarılı olursa bu günlük girdileri kaldırılır. Ancak, dosya güncelleştirmesi kesintiye uğrarsa günlük girdileri medyada depolanır. Medyanın bir sonraki takılışında, FileX bu günlük girdilerini önceki (tamamlanmamış) yazma işleminden algılar. Bu gibi durumlarda, FileX, dosya sistemine zaten yapılmış olan değişiklikleri geri alarak veya önceki işlemi tamamlamaya yönelik gerekli değişiklikleri yeniden uygulayarak bir hatadan kurtuya olabilir. Bu şekilde, bir güncelleştirme işlemi sırasında medya güç kesilirse, FileX hata toleransı modülü dosya sistemi bütünlüğünü korur.

> [!IMPORTANT]
> *FileX hata toleranslı modülü, fiziksel medya bozulmasından kaynaklanan geçerli verilerle oluşan dosya sistemi bozulmasını önleyecek şekilde tasarlanmamıştır.*

> [!IMPORTANT]
> *FileX hataya dayanıklı modül bir medyayı koruduktan sonra, hata toleransı etkinleştirilmiş olarak dosya x dışında bir şeye bağlı olmamalıdır. Bunun yapılması, dosya sistemindeki günlük girişlerinin medyada sistem bilgileriyle tutarsız olmasına neden olabilir. Medya başka bir dosya sistemi tarafından güncelleştirildikten sonra FileX hata toleranslı modülü günlük girdilerini işlemeye çalışırsa, kurtarma yordamı başarısız olabilir ve tüm dosya sistemi öngörülemeyen bir durumda bırakılır.*

## <a name="use-of-the-fault-tolerant-module"></a>Hataya dayanıklı modülün kullanımı

FileX hataya dayanıklı özelliği, FileX tarafından desteklenen FAT12, FAT16, FAT32 ve exFAT gibi tüm FAT dosya sistemleri tarafından kullanılabilir. Hataya dayanıklı özelliği etkinleştirmek için, FileX, tanımlı **FX_ENABLE_FAULT_TOLERANT** sembol ile oluşturulmalıdır. Çalışma zamanında uygulama, ***_ fx_media_open çağrısından hemen sonra fx_fault_tolerant_enable _*** çağırarak hataya dayanıklı hizmet başlatır. Hata toleransı etkinleştirildikten sonra, belirlenen medyaya tüm dosya yazma işlemleri korunur. Varsayılan olarak, hataya dayanıklı modül etkin değildir.

> [!IMPORTANT]
> * Uygulamanın dosya sistemine ***fx_fault_tolerant_enable** _ çağrılmadan önce erişilmediğinden emin olması gerekir. Uygulama, hataya dayanıklı etkinleştirilmesinden önce dosya sistemine veri yazardıysa, önceki yazma işlemleri tamamlanmıyorsa ve dosya sistemi hataya dayanıklı günlük entries._ ile geri yüklenmediğinde yazma işlemi medyayı bozabilir.

## <a name="filex-fault-tolerant-module-log"></a>FileX hataya dayanıklı modül günlüğü

FileX hata toleransı günlüğü, Flash 'ta bir mantıksal küme kullanır. Bu kümenin başlangıç kümesi numarasına olan dizin, **FX_FAULT_TOLERANT_BOOT_INDEX** sembol tarafından belirtilen bir uzaklığa sahip medyanın önyükleme kesimine kaydedilir. Varsayılan olarak, bu sembol 116 olarak tanımlanmıştır. Bu konum, FAT12/16/32 ve exFAT belirtiminde ayrılmış olarak işaretlendiğinden seçilir.

Şekil 5, "günlük yapısı düzeni", günlük yapısının genel yerleşimini gösterir. Günlük yapısı üç bölüm içerir: günlük üstbilgisi, FAT zinciri ve günlük girişleri.

> [!IMPORTANT]
> *Günlük girişlerinde depolanan tüm çok baytlı değerler little endian biçimindedir.*

![Günlük yapısı düzeni](./media/user-guide/log-structure-layout.png)

**Şekil 5. Günlük yapısı düzeni**

Günlük üstbilgisi alanı, tüm günlük yapısını açıklayan bilgileri içerir ve her bir alanı ayrıntılı olarak açıklar.

**TABLO 8. Günlük üst bilgi alanı**

|Alan|Boyut (bayt)|Description|
|-----|--------------|-----------|
|ID|4|Bir FileX hata toleransı günlük yapısını tanımlar. KIMLIK değeri 0x46544C52 değilse, günlük yapısı geçersiz olarak kabul edilir.|
|Toplam Boyut|2|Tüm günlük yapısının toplam boyutunu (bayt olarak) belirtir.|
|Üst bilgi sağlama toplamı|2|Günlük üst bilgi alanını dönüştüren sağlama toplamı. Üstbilgi alanları sağlama toplamı doğrulamasında başarısız olursa günlük yapısı geçersiz olarak kabul edilir.|
|Sürüm Numarası|2|FileX hataya dayanıklı büyük ve küçük sürüm numaraları.|
|Ayrılmıştır|2|Daha sonra genişletme için.|

Günlük üst bilgi alanının ardından FAT zinciri günlük alanı bulunur. Şekil 9 ' da, FAT zincirinin nasıl değiştirilmesi gerektiğini açıklayan bilgiler yer alır. Bu günlük alanı, bir dosyaya ayrılan kümelerle ilgili bilgiler, bir dosyadan çıkarılan kümeler ve ekleme/silmenin nerede olması gerektiğini ve FAT zinciri günlük alanındaki her alanı açıklar.

**TABLO 9. FAT zinciri günlük alanı**

|Alan|Boyut (bayt)|Açıklama|
|-----|--------------|-----------|
|FAT zinciri günlüğü sağlama toplamı|2|Tüm FAT zinciri günlük alanının sağlama toplamı. Sağlama toplamı doğrulamasında başarısız olursa FAT zinciri günlük alanı geçersiz olarak kabul edilir.|
|Bayrak|1|Geçerli bayrak değerleri şunlardır:<br/>0x01 FAT zinciri geçerli<br />0x02 BIT EŞLEMI kullanılıyor|
|Ayrılmıştır|1|Gelecekte kullanılmak üzere ayrılmış|
|Ekleme noktası – ön|4|Yeni oluşturulan zincirin eklendiği küme (orijinal FAT zincirine ait).|
|Yeni FAT zincirinin baş kümesi|4|Yeni oluşturulan FAT zincirinin ilk kümesi|
|Özgün FAT zincirinin baş kümesi|4|Kaldırılacak özgün FAT zincirinin bölümünün ilk kümesi.|
|Ekleme noktası – geri|4|Yeni oluşturulan FAT zincirinin üzerinde birleşen özgün küme.|
|Sonraki silme noktası|4|Bu alan, FAT zinciri Temizleme yordamına yardımcı olur.|

Günlük girişleri alanı, bir hatadan kurtarmak için gereken değişiklikleri tanımlayan günlük girdilerini içerir. FileX hata toleranslı modülünde desteklenen üç günlük girişi türü vardır: FAT günlük girdisi; Dizin günlüğü girişi; ve bit eşlem günlüğü girişi.

Aşağıdaki üç şekil ve üç tablo bu günlük girdilerini ayrıntılı olarak anlatmaktadır.

![FAT günlük girdisi](./media/user-guide/fat-log-entry.png)

**Şekil 6. FAT günlük girdisi**

**TABLO 10. FAT günlük girdisi**

|Alan|Boyut (bayt)|Açıklama|
|-----|--------------|-----------|
Tür|2|Giriş türü, FX_FAULT_TOLERANT_FAT_LOG_TYPE olmalıdır|
|Boyut|2|Bu girdinin boyutu|
|Küme numarası|4|Küme numarası|
|Değer|4|FAT girişine yazılacak değer|

![Dizin günlüğü girdisi](./media/user-guide/directory-log-entry.png)

**Şekil 7. Dizin günlüğü girdisi**

**TABLO 11. Dizin günlüğü girdisi**

|Alan|Boyut (bayt)|Açıklama|
|-----|--------------|-----------|
|Tür|2|Giriş türü, FX_FAULT_TOLERANT_DIRECTORY_LOG_TYPE olmalıdır|
|Boyut|2|Bu girdinin boyutu|
|Kesim boşluğu|4|Bu dizinin bulunduğu kesime (bayt cinsinden).|
|Günlük kesimi|4|Dizin girişinin bulunduğu sektör|
|Günlük Verileri|Değişken|Dizin girişinin içeriği|

![Bit eşlem günlüğü girdisi](./media/user-guide/bitmap-log-entry.png)

**Şekil 8. Bit eşlem günlüğü girdisi**

**TABLO 12. Bit eşlem günlüğü girdisi**

|Alan|Boyut (bayt)|Açıklama|
|-----|--------------|-----------|
|Tür|2|Giriş türü, FX_FAULT_TOLERANT_BITMAP_LOG_TYPE olmalıdır|
|Boyut|2|Bu girdinin boyutu|
|Küme numarası|4|Küme numarası|
|Değer|4|FAT girişine yazılacak değer|

## <a name="fault-tolerant-protection"></a>Hataya dayanıklı koruma

FileX hata toleranslı modülü başladıktan sonra, öncelikle medyada mevcut bir hataya dayanıklı günlük dosyası arar. Geçerli bir günlük dosyası bulunamazsa, FileX medyayı korumasız olarak değerlendirir. Bu durumda, FileX medyada bir hata toleranslı günlük dosyası oluşturur.

> [!IMPORTANT]
> * FileX, dosya sistemini, FileX hata toleranslı modülü başlamadan önce bozuksa koruyamaz. *

Bir hata toleranslı günlük dosyası bulunuyorsa, FileX mevcut günlük girişlerini denetler. Günlük girişi olmayan bir günlük dosyası, önceki dosya işleminin başarılı olduğunu ve tüm günlük girişlerinin kaldırıldığını gösterir. Bu durumda, uygulama hataya dayanıklı koruma ile dosya sistemini kullanmaya başlayabilir.

Ancak günlük girişleri konumlandırıldığında, FileX 'in önceki dosya işlemini tamamlaması veya dosya sistemine zaten uygulanmış olan değişiklikleri geri döndürmesinden önce, değişiklikleri etkin bir şekilde geri alın. Her iki durumda da, günlük girdileri dosya sistemine uygulandıktan sonra, dosya sistemi tutarlı bir duruma geri yüklenir ve uygulama dosya sistemini yeniden kullanmaya başlayabilir.

Dosya güncelleştirme işlemi sırasında FileX tarafından korunan medya için veri bölümü doğrudan medyaya yazılır. FileX, verileri yazdığında, Dizin girişlerine, FAT tablosuna uygulanması gereken tüm değişiklikleri de kaydeder. Bu bilgiler, dosya dayanıklı günlük girişlerine kaydedilir. Bu yaklaşım, veriler medyaya yazıldıktan sonra dosya sistemi güncelleştirmelerinin gerçekleşmesini güvence altına alır. Veri yazma aşamasında medya çıkartılamamışsa, önemli dosya sistemi bilgileri henüz değiştirilmez. Bu nedenle, dosya sistemi kesintiye karşı etkilenmez.

Tüm veriler medyaya başarıyla yazıldıktan sonra, FileX, değişiklikleri sistem bilgilerinde, tek seferde bir giriş olacak şekilde uygulamak için günlük girdilerindeki bilgileri izler. Tüm sistem bilgileri medyaya kaydedildikten sonra, günlük girişleri hataya dayanıklı günlüğünden kaldırılır. Bu noktada, FileX dosya güncelleştirme işlemini tamamlar.

Dosya güncelleştirme işlemi sırasında dosyalar yerinde güncellenmez. Hataya dayanıklı modül, verilerin yeni verileri içine yazması için bir sektör ayırır ve sonra üzerine yazılacak verilerin bulunduğu kesimi kaldırır ve yeni kesimi chça bağlamak üzere ilgili FAT girişlerini günceller. Bir kümedeki kısmi verilerin değiştirilmesi gereken durumlarda, FileX her zaman yeni kümeler ayırır, güncelleştirilmiş verilerle eski kümelerden tüm verileri yeni kümelere yazar ve ardından eski kümeleri boşaltır. Bu, dosya güncelleştirmesi kesintiye uğrarsa özgün dosyanın bozulmadan emin olur. Uygulamanın, FileX hataya dayanıklı koruma altında, bir dosyadaki verilerin güncelleştirilmesi için medyanın, eski verileri olan kesimlerin yayımlanmasından önce yeni verileri tutacak yeterli boş alana sahip olması gerektiğini bilmesi gerekir. Medyada yeni verileri tutmak için yeterli alan yoksa güncelleştirme işlemi başarısız olur.
