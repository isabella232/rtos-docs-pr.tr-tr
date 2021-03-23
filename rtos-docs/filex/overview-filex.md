---
title: Azure RTOS FileX 'i anlama
description: Azure RTOS FileX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen yüksek performanslı, dosya ayırma tablosu (FAT) ile uyumlu bir dosya sistemidir. Azure RTOS ThreadX gibi Azure RTOS FileX, küçük bir ayak izi ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da dosya yönetimi işlemleri gerektiren, günümüzün derin eklenmiş uygulamalar için idealdir. FileX, RAM, Azure RTOS USBX, SD kartı ve nve/veya Flash anıları dahil olmak üzere çoğu fiziksel medyayı Azure RTOS LevelX aracılığıyla destekler.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: a3a20c8ced3426399ceedf6994c872ce7aec93c3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827322"
---
# <a name="overview-of-azure-rtos-filex"></a>Azure RTOS FileX 'e genel bakış

Azure RTOS FileX Embedded dosya sistemi, özel olarak gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft FAT dosya biçimleri için Azure RTOS 'ın gelişmiş, endüstriyel sınıf çözümüdür. Azure RTOS FileX, FAT12, FAT16, FAT32 ve exFAT gibi Microsoft 'un dosya biçimlerini destekler. FileX, [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/)adlı bir eklenti ürünü aracılığıyla isteğe bağlı hata TOLERANSı ve Flash giyme seviyelendirme de sunar. Tüm bu, küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla birlikte Azure RTOS dosya x ' i en zorlu ekli IoT uygulamalarına yönelik ideal bir seçenek haline getirir.

## <a name="api-protocols"></a>API protokolleri

### <a name="azure-rtos-filex-api"></a>Azure RTOS FileX API 'SI

- Sezgisel ve tutarlı API
- İsim-fiil adlandırma kuralı
- Tüm API 'Ler, FileX olarak kolayca tanımlanabilmesi için önde gelen *fx_* sahiptir
- API 'Lerin engellenmesi isteğe bağlı iş parçacığı zaman aşımına uğradı
- Medya ve dosya işlemleri için isteğe bağlı Kullanıcı bildirimi geri çağırmaları
- Daha fazla ayrıntı için lütfen bkz. [Azure RTOS Fılex Kullanıcı Kılavuzu](about-this-guide.md)

### <a name="media-services"></a>Media Services

- FAT 12/16/32 ve exFAT desteği
- Minimum 6KB FLASH, 2,5 KB RAM
- Medya erişim Hizmetleri 'ni doldurun
- Sınırsız sayıda medya örneği
- Basit okuma/yazma mantıksal sektör sürücü arabirimi
- Birden çok bölüm desteği
- Mantıksal kesim önbelleği
- FAT giriş önbelleği
- İsteğe bağlı hata toleransı desteği
- Ertelenmiş Ikincil FAT güncelleştirmesi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
- Aşağıdakiler dahil, sezgisel medya erişim API 'Leri:
  - fx_media_open
  - fx_media_close
  - fx_media_format
  - fx_media_space_available

### <a name="directory-services"></a>Dizin Hizmetleri

- En fazla 256 bayt yolu
- Uzun ve 8,3 dizin adları destekleniyor
- Dizin oluşturma & silme
- Dizin gezintisi ve geçişi
- Dizin öznitelikleri yönetimi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
- Aşağıdakiler dahil, sezgisel dizin erişimi API 'Leri:
  - fx_directory_create
  - fx_directory_delete
  - fx_directory_attributes_set
  - fx_directory_attributes_read
  - fx_directory_first_entry_find
  - fx_directory_next_entry_find

### <a name="file-services"></a>Dosya Hizmetleri

- Minimum 3.3 KB FLASH
- Sınırsız açık dosya
- Salt okuma dosyaları birden çok kez açılabilir
- Uzun ve 8,3 dizin adları destekleniyor
- Ardışık dosya desteği
- Hızlı arama mantığı
- Kümelerin ön ayırması
- Dosya oluşturma, silme ve yeniden adlandırma
- Dosya okuma, yazma ve görme
- Dosya öznitelikleri yönetimi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
- Aşağıdakiler dahil, sezgisel dosya erişim API 'Leri:
  - fx_file_create
  - fx_file_delete
  - fx_file_attributes_set
  - fx_file_attributes_read
  - fx_file_read
  - fx_file_seek
  - fx_file_write

## <a name="small-footprint"></a>Küçük ayak izi

Azure RTOS FileX Embedded dosya sistemi, temel dosya okuma/yazma desteği için 8,6 KB ile 12 KB arasında bir remarkalı küçük boyut içerir. En az Azure RTOS FileX RAM kullanımı, tek bir medya örneği için 1,8 KB ve yalnızca 512 baytlık bir mantıksal kesim önbelleğidir. Azure RTOS ThreadX gibi Azure RTOS dosya x boyutu, uygulama tarafından kullanılan hizmetlere göre otomatik olarak ölçeklendirilir. Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.

## <a name="fast-execution"></a>Hızlı yürütme

Azure RTOS FileX, bir mantıksal kesim önbelleğinin yanı sıra bir FAT giriş önbelleği de sağlar. Her ikisinin de boyutları uygulamanın doğrudan denetimi altındadır. Ayrıca, Azure RTOS FileX, ardışık küme ayırma ve doğrudan ardışık küme okuma ve yazma sağlar. Bütün kesimlerin okuma/yazma istekleri doğrudan uygulama arabelleği ve medya arasında yapılır; diğer bir deyişle, ara belleğe alma yapılmaz. Tüm bu ve genel performans odaklı bir tasarım felseno, Azure RTOS dosya x 'in olası en hızlı performansı elde etmesine yardımcı olur.

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS FileX, aşağıdakiler de dahil olmak üzere gelişmiş bir teknolojidir.

- FAT 12/16/32 ve exFAT desteği
- Birden çok bölüm desteği
- Otomatik ölçeklendirme
- Endian nötr
- Uzun dosya adı ve 8,3 desteği
- İsteğe bağlı hata toleransı desteği
- Mantıksal kesim önbelleği
- FAT giriş önbelleği
- Kümelerin ön ayırması
- Ardışık dosya desteği
- İsteğe bağlı performans ölçümleri
- Azure RTOS TraceX sistem analizi desteği

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a>VEYA/nve aşınma dengeleme (Azure RTOS LevelX)

Azure RTOS LevelX, Microsoft 'un veya/nve FLASH giyme Dengeleme ürünüdür. Azure RTOS LevelX, FileX ile birlikte veya uygulama için tek başına, doğrudan okuma/yazma FLASH sektör kitaplığı olarak kullanılabilir.

## <a name="fastest-time-to-market"></a>En hızlı pazar süresi

Azure RTOS FileX 'i yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır. Sonuç olarak, Azure RTOS FileX, katıştırılmış IoT cihazları için en popüler FAT dosya sistemlerinden biridir. Aşağıda, tutarlı bir pazar süresi avantajımız için bazı nedenler verilmiştir:

- Kalite belgeleri: lütfen [Azure RTOS FileX Kullanıcı Kılavuzumuzu](about-this-guide.md) gözden geçirin ve kendiniz görün!
- Tüm kaynak kodu kullanılabilirliği
- Kullanımı kolay API
- Kapsamlı ve gelişmiş özellik kümesi

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a>TUV ve UL ile birçok güvenlik standartlarına ön sertifikalı

![SGS-TUV Saar](./media/overview-filex/partener-logo-sgs-tuv-saar-2.png)

Azure RTOS FileX, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW Safety Class C, ISO 26262 asıl D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir. Sertifika, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için, FileX 'in güvenlik açısından ilgili yazılımlar geliştirmesinde kullanılabileceğini onaylar. Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir. Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenlik düzeyini güvence altına almak için kullanılır.

:::image type="content" source="media/overview-filex/cru-logo-certification.png" alt-text="CRU UL sertifikası":::

Azure RTOS Fılex, ınımg 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R 1998 ve programlanabilir. UL, en fazla uzman sürmek güvenlik çözümleri sunan küresel, bağımsız bir güvenlik bilimi şirketidir. Bu, elektrik, yenilenebilir enerji ve Nanotechnology için genel olarak elektrik 'yi benimseme özelliğine sahiptir.

TUV ve UL sertifikalarıyla ilişkili yapıtlar (sertifika, güvenlik el kitabı, test raporu vb.) satış için kullanılabilir.

Uygulamanın ek sertifikaya ihtiyacı olduğu durumlarda, gerçek donanım platformunu kullanarak ve hatta uygulama kodunu kapsayan çeşitli standartlara anahtar sertifikası sağlamak için Microsoft aracılığıyla bir sertifika hizmeti kullanılabilir.

## <a name="one-simple-license"></a>Tek bir basit lisans

Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.

## <a name="full-highest-quality-source-code"></a>Tam, en yüksek kaliteli kaynak kodu

Yıl boyunca, FileX kaynak kodu çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı. Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.

## <a name="supports-most-popular-architectures"></a>Popüler mimarilerin çoğunu destekler

Azure RTOS FileX, en popüler 32/64 bit mikro işlemciler, kullanıma hazır, tam olarak sınanmış ve aşağıdakiler dahil olmak üzere tam olarak desteklenmiş şekilde çalışır:

**Analog cihazlar**: parça, BlackICE, CM4xx

**Andes Core**: RISC-V

**Ambiqmicro**: Apollo MCUs

**ARM**: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı

**Temposunda**: xtensa, elmas

**Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi

**Cypress**: RISC-V

**Ensilica**: ESI-RISC

**Infineon**: XMC1000, XMC4000, kanore

**Intel**; **Intel FPGA**: X36/Pentium, XSCALE, NIOS II, Cyclone, varış a 10

**Mikro yonga**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32

**Mikro yarı**: RISC-V

**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4

**Renesas**: SH, HS, v850, RX, Rz, Synergy

**Silicon** Labs: EFM32

**Synopsys**: Arc 600, 700, Arc Em, Arc HS

**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

**TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C

**Dalga bilgi işlem**: MIPS32 4k, 24 K, 34 k, 1004 k, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M-class

**Xilinx**: mikro Blaze, PowerPC 405, zynq, Zynq UltraSCALE

*Listelenen tüm zamanlama ve boyut rakamları tahminlerdir ve geliştirme platformunuzun farklı olabilir.*
