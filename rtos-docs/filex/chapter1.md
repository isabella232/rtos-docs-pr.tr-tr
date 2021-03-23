---
title: Bölüm 1-Azure RTOS FileX 'e giriş
description: Azure RTOS FileX, çok daha fazla eklenmiş uygulamalar için tamamen FAT biçimli bir medya ve dosya yönetimi sistemidir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be7e6f9cd9fbc69ac0908d1de733dac1c4f73bf6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825517"
---
# <a name="chapter-1---introduction-to-azure-rtos-filex"></a>Bölüm 1-Azure RTOS FileX 'e giriş

Azure RTOS FileX, çok daha fazla eklenmiş uygulamalar için tamamen FAT biçimli bir medya ve dosya yönetimi sistemidir. Bu bölümde, uygulamaları ve avantajları açıklanarak FileX tanıtılmaktadır.

## <a name="filex-unique-features"></a>FileX benzersiz özellikleri

Azure RTOS FileX, RAM diskler, FLASH yöneticileri ve gerçek fiziksel cihazlar dahil olmak üzere sınırsız sayıda medya cihazını destekler. 12-, 16 ve 32-bit dosya ayırma tablosu (FAT) biçimlerini destekler ve ayrıca genişletilmiş dosya ayırma tablosu (exFAT), bitişik dosya ayırmayı destekler ve her iki boyut ve performans için yüksek oranda iyileştirilmiştir. FileX Ayrıca hataya dayanıklı destek, medya açma/kapatma ve dosya yazma geri çağırma işlevlerini içerir.

FLASH cihazlarına yönelik büyümekte olan ihtiyacı karşılayacak şekilde tasarlanan FileX, ThreadX ile aynı tasarım ve kodlama yöntemlerini kullanır. Tüm Microsoft ürünleri gibi, FileX tam ANSI C kaynak kodu ile dağıtılır ve hiçbir çalışma zamanı ile birlikte çalışır.

### <a name="product-highlights"></a>Ürün vurguları

- Tüm ThreadX işlemci desteğini
- Hiçbir çatı yok
- Tamamen ANSI C kaynak kodu
- Gerçek zamanlı performans
- Yanıt veren teknik destek
- Sınırsız FileX nesneleri (medya, dizinler ve dosyalar)
- Dinamik FileX nesnesi oluşturma/silme
- Esnek bellek kullanımı
- Boyut otomatik olarak ölçeklendirilir
- Küçük ayak izi (6 Kbayt kadar) yönerge alanı boyutu: 6-30K
- ThreadX ile tamamen tümleştirme
- Endian nötr
- Kullanımı kolay FileX g/ç sürücüleri
- 12-, 16-ve 32 bit FAT desteği
- exFAT desteği
- Uzun dosya adı desteği
- İç FAT giriş önbelleği
- Unicode ad desteği
- Bitişik dosya ayırma
- Ardışık kesim ve küme okuma/yazma
- İç mantıksal kesim önbelleği
- RAM disk gösterimi kullanıma hazır çalışır
- Medya biçimi özelliği
- Hata algılama ve kurtarma
- Hataya dayanıklı seçenekler
- Yerleşik performans istatistikleri
- Tek başına destek (Azure RTOS yok)

## <a name="safety-certifications"></a>Güvenlik sertifikaları

### <a name="tv-certification"></a>TÜV Sertifikası

FileX, SGS-TÜV Saar tarafından, ıEC-61508 ve ıEC-62304 ' e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir. Sertifika, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için Uluslararası Elektroteknik Komisyonu (ıEC) 61508 ve ıEC 62304 ' nin en yüksek güvenlik bütünlüğü düzeylerine yönelik güvenlik ile ilgili yazılımların geliştirilmesinde, FileX 'in kullanılabileceğini onaylar. Almanya 'nın SGS-Group ve TÜV Saarland 'ın bir Joint girişim aracılığıyla oluşturulan SGS-TÜV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir. Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, 62304 IEC, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin ve demiryolu denetim sistemlerinin işlevsel güvenliğini güvence altına almak için kullanılır.

SGS-TÜV Saar, ISO 26262 standardına göre güvenlik açısından kritik bir oto dili sisteminde kullanılmak üzere sertifikalı FileX 'e sahiptir. Ayrıca, FileX, en yüksek ISO 26262 sertifikası düzeyini temsil eden, g/v güvenlik bütünlüğü düzeyi (asıl) D 'ye sertifikalıdır.

Ayrıca, SGS-TÜV Saar, güvenlik açısından kritik demiryolu uygulamalarında kullanılmak üzere sertifikalı FileX 'e sahiptir ve en fazla 50128 standart, en fazla ' a kadar 2.

![SGS TUV Saar logosu](./media/user-guide/sgs-tuv-saar-logo.png)

- IEC 61508, SIL 4 ' e kadar
- IEC 62304 en fazla SW güvenlik sınıfı C
- ISO 26262 ASIL D
- EN 50128 SW-SıL 4

> [!IMPORTANT]
> Dosya veya test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği için TÜV tarafından hangi dosya sürümlerinin sertifikalandırılabileceği hakkında daha fazla bilgi için lütfen bizimle iletişime geçin. *

### <a name="ul-certification"></a>UL sertifikası

Dosya x,, programlanabilir bileşenlerinde yazılım için ul 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 603351 ek R ve UL 1998 güvenlik standartları ile uyumluluk için UL tarafından sertifikalandırilmiştir. Ek H 'de "yazılım kullanan denetimler" için gereksinimleri olan ıEC/UL 60730-1 ile birlikte ıEC 60335-1 standardı, ek R. ıEC 60730 ek H ve ıEC 60335-1 ek R içindeki "programlanabilir elektronik devreler" için gereksinimleri açıklar. Örneğin, yıkama makineleri, dishörler, kurutma, kurutıcılar, freezers ve ovens gibi gereçlerde kullanılan MCU donanım ve yazılımlarının güvenliğini ele.

![C RU US 2](./media/user-guide/c-ru-us-logo.png)

*UL/ıEC 60730, UL/ıEC 60335, UL 1998*

> [!IMPORTANT]
>*Dosya ve test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği için hangi FileX sürümlerinin sertifikalandırılabileceği hakkında daha fazla bilgi için lütfen bizimle iletişime geçin.*

## <a name="powerful-services-of-filex"></a>Dosya x 'in güçlü Hizmetleri

### <a name="multiple-media-management"></a>Birden çok medya yönetimi

FileX, sınırsız sayıda fiziksel ortamı destekleyebilir. Her medya örneğinin kendi farklı bellek alanı ve ***fx_media_open*** çağrısında belirtilen ilişkili sürücüsü vardır. FileX 'in varsayılan dağıtımı, bu RAM diski kullanan bir basit RAM medya sürücüsüyle ve bir demo sistemiyle birlikte gelir.

### <a name="logical-sector-cache"></a>Mantıksal kesim önbelleği

Tüm kesim aktarımlarının sayısını, hem medyaya hem de medyadan azaltarak, FileX mantıksal kesim önbelleği, performansı önemli ölçüde artırır. FileX, her açılan medya için bir mantıksal kesim önbelleği tutar. Mantıksal kesim önbelleğinin derinliği, ***fx_media_open*** API çağrısıyla FileX 'e sağlanan bellek miktarına göre belirlenir.

### <a name="contiguous-file-support"></a>Ardışık dosya desteği

FileX, dosya erişimi zaman belirleyici hale getirmek ve bunları geliştirmek için API hizmeti ***fx_file_allocate*** aracılığıyla ardışık dosya desteği sunar. Bu yordam, istenen bellek miktarını alır ve isteği karşılamak üzere bir dizi bitişik küme için arama yapar. Bu tür kümeler bulunursa, dosyanın ayrılmış kümeler zincirinin bir parçası yapılarak önceden ayrılır. Fiziksel medyayı taşırken, FileX bitişik dosya desteği önemli bir performans iyileştirilmesine neden olur ve erişim süresini belirleyici hale getirir.

### <a name="dynamic-creation"></a>Dinamik oluşturma

FileX, sistem kaynaklarını dinamik olarak oluşturmanıza olanak tanır. Uygulamanızda birden çok veya dinamik yapılandırma gereksinimi varsa bu özellikle önemlidir. Ayrıca, kullanabileceğiniz FileX kaynakları sayısında (medya veya dosya) önceden tanımlı bir sınır yoktur. Ayrıca, sistem nesnelerinin sayısı performans üzerinde herhangi bir etkiye sahip değildir.

## <a name="easy-to-use-api"></a>Kullanımı kolay API

FileX, kolayca anlaşılması ve kullanımı kolay bir şekilde, en iyi şekilde eklenmiş dosya sistemi teknolojisini sağlar! FileX uygulama programlama arabirimi (API), Hizmetleri sezgisel ve tutarlı hale getirir. Diğer dosya sistemleriyle çok ortak olan "alfabede" hizmetlerini çözebilmeniz gerekmez.

FileX sürüm 5 hizmetlerinin tüm listesi için bkz. [ek a](appendix-a.md).

## <a name="exfat-support"></a>exFAT desteği

exFAT (genişletilmiş dosya ayırma tablosu), dosya boyutunun, FAT32 dosya sistemleri tarafından uygulanan bir sınırı GB ile aşmasına izin vermek için Microsoft tarafından tasarlanan bir dosya sistemidir. Bu, 32 ' den fazla kapasiteye sahip SD kartları için varsayılan dosya sistemidir. SD kartlar veya FileX exFAT biçimiyle biçimlendirilen Flash sürücüleri Windows ile uyumludur. exFAT, yaklaşık 1.000.000.000 GB olan bir Exabyte 'e (EB) kadar dosya boyutunu destekler.

ExFAT kullanması gereken kullanıcılar FileX kitaplığını ***FX_ENABLE_EXFAT** _ tanımlı simgesiyle yeniden derlemeniz gerekir. Medya açılırken, FileX medya türünü algılar. Medya exFAT ile biçimlendirildiyse, FileX dosya sistemini exFAT standardına göre okur ve yazar. Yeni medyayı exFAT ile biçimlendirmek için _ *_fx_media_exFAT_format_* * hizmetini kullanın. Varsayılan olarak exFAT etkin değildir.

## <a name="fault-tolerant-support"></a>Hataya dayanıklı destek

FileX hata toleranslı modülü, dosya veya dizin güncelleştirme sırasında kesintiden kaynaklanan dosya sistemi bozulmasını engellemek için tasarlanmıştır. Örneğin, bir dosyaya veri eklerken, FileX dosyasının içeriğini, Dizin girişini ve muhtemelen FAT girdilerini güncelleştirmesi gerekir. Bu güncelleştirme sırası kesintiye uğrarsa (örneğin, güç hatası gibi), dosya sistemi, tüm dosya sisteminin bütünlüğünü etkileyebilecek, diğer dosyaların bozulmasıyla başa çıkabilir, tutarsız bir durumda olur.

FileX hata toleranslı modülü, bir dosya veya dizini bir şekilde güncelleştirmek için gereken tüm adımları kaydederek işe yarar. Bu günlük girişi, FileX 'in bulabileceği ve erişebileceği adanmış kesimlerde (bloklar) medyada depolanır. Günlük verilerinin konumuna uygun bir dosya sistemi olmadan bile erişebilirsiniz. Bu nedenle, dosya sistemi bozuksa, FileX yine de günlük girişini bulabilir ve dosya sistemini iyi bir duruma geri yükleyebilir.

Dosya veya dizin güncelleştirmeleri olduğundan, günlük girdileri oluşturulur. Güncelleştirme işlemi başarıyla tamamlandıktan sonra, günlük girdileri kaldırılır. Başarılı bir dosya güncelleştirmesinden sonra günlük girdileri doğru şekilde kaldırılmazsa, kurtarma işlemi günlük girdisindeki içeriğin dosya sistemiyle eşleşip eşleşmediğini belirlerse, hiçbir şeyin gerçekleştirilmesi gerekmez ve günlük girişleri temizlenebilir.

Dosya sistemi güncelleştirme işleminin kesintiye uğratılışında, medya FileX tarafından bir daha bağlandığında, hataya dayanıklı modül günlük girdilerini analiz eder. Günlük girdilerindeki bilgiler, FileX 'in dosya sistemine zaten uygulanmış olan kısmi değişiklikleri geri yüklemesine olanak tanır (hatanın dosya güncelleştirme işleminin erken aşamasında olması durumunda) veya günlük girişleri yeniden do bilgileri içeriyorsa, FileX, önceki işlemi tamamlaması için gereken değişiklikleri uygulayabilir.

Bu hataya dayanıklı özelliği, FileX tarafından desteklenen FAT12, FAT16, FAT32 ve exFAT gibi tüm FAT dosya sistemleri tarafından kullanılabilir. Varsayılan olarak, hata toleranslı, FileX içinde etkinleştirilmemiştir. Hataya dayanıklı özelliği etkinleştirmek için, FileX,  **FX_ENABLE_FAULT_TOLERANT** sembol ve **FX_FAULT_TOLERANT** tanımlı olarak oluşturulmalıdır. Çalışma zamanında uygulama, **_fx_fault_tolerant_enable_** çağırarak hataya dayanıklı bir hizmet başlatır.
Hizmet başladıktan sonra, tüm dosya ve Dizin yazma işlemleri hataya dayanıklı modüle gider.

Hataya dayanıklı hizmet başladığında, önce medyanın hataya dayanıklı modül altında korunup korunmadığını algılar. Değilse, FileX dosya sisteminin bütünlüğünü varsayar ve dosya sisteminden günlüğe kaydetme ve önbelleğe alma için kullanılacak serbest bloklar ayırarak korumayı başlatır. Dosya sisteminde hataya dayanıklı modül günlükleri bulunursa, günlük girdilerini analiz eder. FileX, önceki işlemi geri alır veya günlük girdilerinin içeriğine bağlı olarak önceki işlemi yeniden yapar. Dosya sistemi, önceki tüm günlük girdileri işlendikten sonra kullanılabilir hale gelir. Bu, FIleX 'in bilinen iyi bir durumdan başlamasını sağlar.

Bir medya, FileX hataya dayanıklı bir modül altında korunduktan sonra, medya başka bir dosya sistemiyle güncellenmez. Bunun yapılması, dosya sistemindeki günlük girdilerinin, FAT tablosundaki, Dizin girişi olan içerikle uyumsuz olarak kalmasını sağlayacak. Medya, hataya dayanıklı modülle Fılex 'e geri taşınmadan önce başka bir dosya sistemi tarafından güncelleştirilirse, sonuç tanımsızdır.

## <a name="callback-functions"></a>Geri Çağırma İşlevleri

Aşağıdaki üç geri çağırma işlevi FileX 'e eklenir:

- Medya açma geri araması
- Medya kapatma geri araması
- Dosya yazma geri çağırması

Kaydolduktan sonra bu işlevler, bu olaylar gerçekleştiğinde uygulamayı bilgilendirir.

## <a name="easy-integration"></a>Kolay tümleştirme

FileX, neredeyse her türlü FLASH veya medya aygıtıyla kolayca tümleşiktir. FileX taşıma basittir. Bu kılavuzda işlem ayrıntılı olarak açıklanmaktadır ve tanıtım sisteminin RAM sürücüsü, başlamak için çok iyi bir yer sağlar!
