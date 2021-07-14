---
title: Microsoft Azure rtos nedir?
description: Azure RTOS, mikro denetleyici birimleri (MCUs) tarafından desteklenen IoT ve Edge cihazları için gerçek zamanlı bir işletim sistemidir (RTOS).
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: b099a5f18accfbe467a2a8fa680c0c76666a9ff3
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754922"
---
# <a name="what-is-microsoft-azure-rtos"></a>Microsoft Azure rtos nedir?

Azure RTOS, mikro denetleyici birimleri (MCUs) tarafından desteklenen Nesnelerin İnterneti (IoT) ve Edge cihazları için gerçek zamanlı bir işletim sistemidir (RTOS). Azure RTOS, en yüksek düzeyde kısıtlanmış cihazları desteklemek için tasarlanmıştır (pil gücüyle ve 64 KB 'den az Flash belleği vardır).

Azure RTOS, çeşitli güvenlik standartları için önceden sertifikalandırilmiştir. Bunlar, ıEC 61508 SIL 4, ıEC 62304 Class C ve ISO 26262 asıl D sertifikalarını içerir. Azure RTOS ThreadX de DO-178 sertifikalıdır.

Azure RTOS, TLS ve DTLS aracılığıyla IPSec ve yuva katmanı güvenliği aracılığıyla tam IP katmanı güvenliği de dahil olmak üzere, EAL4 + ortak ölçütlere sahip güvenlik sertifikalı bir ortam sağlar. Yazılım şifreleme kitaplığımız FIPS 140-2 sertifikası elde etti. Ayrıca, donanım şifreleme özellikleri, ThreadX MODÜLLERI ile bellek koruması ve ARM 'nin TrustZone ARMv8-msecurity özellikleri için destek de faydalanır.

## <a name="components-of-azure-rtos"></a>Azure RTOS bileşenleri

Azure RTOS platformu, Azure RTOS ThreadX, Azure RTOS FileX, Azure RTOS Gux, Azure RTOS NetX, Azure RTOS NetX Duo ve Azure RTOS USBX gibi çalışma zamanı çözümlerinin koleksiyonudur.

### <a name="azure-rtos-threadx"></a>Azure RTOS ThreadX

Azure [RTOS ThreadX](threadx/overview-threadx.md) , özellikle derin eklenmiş uygulamalar için tasarlanan gelişmiş bir Real-Time işletim sistemidir (RTOS). Azure RTOS ThreadX 'in sunduğu birçok avantaj arasında gelişmiş zamanlama olanakları, ileti geçirme, kesme yönetimi ve mesajlaşma hizmetleri sağlanmaktadır. Azure RTOS ThreadX, picokernel mimarisi, önalım-Threshold zamanlaması, olay zincirleme ve zengin bir sistem hizmeti kümesi gibi birçok gelişmiş özelliğe sahiptir.

### <a name="azure-rtos-filex"></a>Azure RTOS FileX

Azure [RTOS FileX](filex/overview-filex.md) , yüksek PERFORMANSLı bir FAT uyumlu dosya sistemidir. Azure RTOS ThreadX ile tamamen tümleşiktir ve desteklenen tüm işlemciler için kullanılabilir. Azure RTOS ThreadX gibi Azure RTOS FileX, küçük bir kaplama ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da dosya işlemleri gerektiren, günümüzün derin eklenmiş uygulamalar için ideal hale getirir. Azure RTOS FileX, Azure RTOS LevelX aracılığıyla RAM disk, USBX, SD kartı ve nve/veya Flash anıları dahil olmak üzere çoğu fiziksel medyayı destekler.

### <a name="azure-rtos-guix"></a>Azure RTOS GUIX

Azure [RTOS Gux](guix/overview-guix.md) , katıştırılmış sistem geliştiricilerin ihtiyaçlarını karşılamak üzere oluşturulan, profesyonel kalitede bir grafik kullanıcı arabirimi paketidir. Alternatiflerden farklı olarak, Azure RTOS Gux küçük, hızlı ve grafiksel çıktıyı destekleyebilen neredeyse her türlü donanım yapılandırmasına kolayca eklenir. Azure RTOS Gux Ayrıca, uygulama düzeyinde kullanıcı arabirimi geliştirmesi için olağanüstü bir görsel bakış ve sezgisel ve güçlü bir API sunar.

### <a name="azure-rtos-netx"></a>Azure RTOS NetX

Azure [RTOS NetX](netx/overview-netx.md) , TCP/IP protokol standartlarının yüksek performanslı bir uygulamasıdır. Azure RTOS ThreadX ile tamamen tümleşiktir ve desteklenen tüm işlemciler için kullanılabilir. Azure RTOS NetX 'in benzersiz bir piconet mimarisi vardır. Sıfır kopyalama API 'siyle birlikte kullanıldığında, bu, ağ bağlantısı gerektiren son derece eklenmiş uygulamalar için mükemmel bir uyum sağlar.

### <a name="azure-rtos-netx-duo"></a>Azure RTOS NetX Duo

Azure [RTOS NetX](netx-duo/overview-netx-duo.md) Duo, özellikle de gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, gelişmiş, ENDÜSTRIYEL bir TCP/IP ağı yığınlarıdır. Azure RTOS NetX Duo, iki IPv4 ve IPv6 ağ yığınıdır. NetX, temel olarak Azure RTOS NetX Duo bir alt kümesi olan özgün IPv4 ağ yığınıdır.

### <a name="azure-rtos-usbx"></a>Azure RTOS USBX

Azure [RTOS USBX](usbx/overview-usbx.md) , yüksek PERFORMANSLı bir USB ana bilgisayar, cihaz ve-go (OTG) katıştırılmış Stack 'tir. ThreadX ile tamamen tümleşiktir ve tüm Azure RTOS ThreadX desteklenen işlemcilerde kullanılabilir. Azure RTOS ThreadX gibi Azure RTOS USBX, küçük bir parmak izi ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da USB cihazlarıyla bir arabirim gerektiren çok sayıda gömülü uygulama için idealdir.

### <a name="windows-tools"></a>Windows araçları

Azure [RTOS Gux Studio](guix/about-guix-studio.md) , uygulamanın GUI 'si içindeki tüm grafik öğelerinin oluşturulmasını ve bakımını kolaylaştırmanın yanı sıra, tümüyle bir GUI uygulama tasarım ortamı sağlar. Azure RTOS Gux Studio otomatik olarak Azure RTOS Gux kitaplığı ile uyumlu C kodu oluşturur ve hedefte derlenmeye ve çalıştırılmaya çalışır.

Azure [RTOS TraceX](tracex/overview-tracex.md) , geliştiricilere gerçek zamanlı sistem olaylarının grafik bir görünümünü sağlayan ve gerçek zamanlı sistemlerinin davranışını görselleştirmesini ve daha iyi anlamasına olanak tanıyan ana bilgisayar tabanlı bir analiz aracıdır.

## <a name="the-azure-rtos-advantage"></a>Azure RTOS avantajı
Azure RTOS, diğer gerçek zamanlı işletim sistemleri için aşağıdaki avantajları sağlar.

### <a name="most-deployed-rtos"></a>En çok dağıtılan RTOS

Önde gelen 'U M2M Market Intelligence firması, VDC Research 'e göre Azure RTOS 'ın dünya genelinde 6.200.000.000 dağıtımı vardır. Azure RTOS 'ın popülerliği, güvenilirliği, kalitesi, boyutu, performansı, gelişmiş özellikler, kullanım kolaylığı ve genel kullanım süresi avantajına yönelik bir testdir.

> *"Şirketin temelleri ile bu yana kablosuz ve IoT pazarlarında THREADX 'in büyüme tratrumuzu izliyoruz ve THREADX 'in yaygın sektör benimsemesi tarafından giderek daha da artmaktadır."* – Chris Rommel, Executive Başkan Yardımcısı, VDC Research

### <a name="intuitive-and-consistent-api-design"></a>Sezgisel ve tutarlı API tasarımı

* Sezgisel ve tutarlı API.
* Ad-fiil adlandırma kuralı.
* Tüm API 'Lerin, ait oldukları Azure RTOS bileşenini kolayca belirlemek için ThreadX *fx_* ve filex için *tx_* gibi önde gelen öneki vardır.
* API 'Ler genelinde işlevsel tutarlılık. Örneğin, askıya aldığı tüm API işlevlerinin aynı şekilde işlev gösteren isteğe bağlı bir zaman aşımı vardır.
* Birçok API, uygulama ISRs 'den doğrudan kullanılabilir.
- Medya ve dosya işlemleri için isteğe bağlı Kullanıcı bildirimi geri çağırmaları.
* Olay odaklı programlama modeli (API).

### <a name="high-efficiency"></a>Yüksek verimlilik

- Küçük kod parmak izi.
- Kullanılan Hizmetleri temel alan ölçeklenebilir kod kaplama.
- TUV ve UL-ıEC 61508 SIL 4, ıEC 62304 Class C, ISO 26262 asıl D ve EN 50128 SW-SIL4 tarafından önceden onaylanmış.
- Hızlı yürütme. Azure RTOS hız için tasarlanmıştır ve en hızlı olası performansa ulaşmak için en az sayıda iç işlev çağrısı katmanlanıyor.

### <a name="fastest-time-to-market"></a>En hızlı pazar süresi

Azure RTOS 'ın yüklenmesi, öğrenilmesi, kullanılması, hata ayıklaması, doğrulanması, onaylamak ve bakımını yapmak kolaydır. Sonuç olarak, Azure RTOS, farklı bir deyişle, Broadcom, Gainspan ve benzeri birçok SoCs dahil olmak üzere, yerleşik IoT cihazları için en popüler gerçek zamanlı işletim sistemlerinden biridir. Tutarlı Pazar süresi avantajımız, şu şekilde oluşturulmuştur:

* Tüm kaynak kodu kullanılabilirliği.
* Kullanımı kolay API.
* Kapsamlı ve gelişmiş özellik kümesi.
* Kalite belgeleri.

### <a name="one-simple-license"></a>Tek bir basit lisans

Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.

### <a name="full-highest-quality-source-code"></a>Tam, en yüksek kaliteli kaynak kodu

Yıl boyunca Azure RTOS kaynak kodu, çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı. Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.

### <a name="pre-certified-by-tuv-and-ul-to-many-safety-standards"></a>TUV ve UL ile birçok güvenlik standartlarına ön sertifikalı

Azure RTOS, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW Safety Class C, ISO 26262 asıl D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir. Sertifika, Azure RTOS 'ın, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımların geliştirilmesinde kullanılabileceğini onaylar. Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir. Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenlik düzeyini güvence altına almak için kullanılır.

:::image type="content" source="media/partener-logo-sgs-tuv-saar.png" alt-text="SGS-TUV sertifikası":::

Azure RTOS, bir ınımı 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R ve, programlanabilir bileşenlerinde yazılım için UL 1998 güvenlik standartları ile uyumlu bir şekilde tanınıyor. UL, en fazla uzman sürmek güvenlik çözümleri sunan küresel, bağımsız bir güvenlik bilimi şirketidir. Bu, elektrik, yenilenebilir enerji ve Nanotechnology için genel olarak elektrik 'yi benimseme özelliğine sahiptir.

:::image type="content" source="media/cru-logo-certification.png" alt-text="CRU UL sertifikası":::

tuv ve UL sertifikalarla ilişkili Artifacts (sertifika, güvenlik el kitabı, Test raporu vb.) satış için kullanılabilir.

Uygulamanın ek sertifikaya ihtiyacı olduğu durumlarda, gerçek donanım platformunu kullanarak ve hatta uygulama kodunu kapsayan çeşitli standartlara anahtar sertifikası sağlamak için Microsoft aracılığıyla bir sertifika hizmeti kullanılabilir. Sertifika hizmetimiz hakkında daha fazla bilgi için bizimle iletişime geçin.

### <a name="eal4-common-criteria-security-certification"></a>EAL4 + ortak ölçütler güvenlik sertifikası

Azure RTOS, EAL4 + ortak ölçütler güvenlik sertifikası elde etti. Değerlendirme hedefi (TOE), Azure RTOS ThreadX, Azure RTOS NetX Duo, Azure RTOS NetX güvenli TLS ve Azure RTOS NetX MQTT 'yi içerir. Bu, derin eklenmiş sensörler, cihazlar, uç yönlendiriciler ve ağ geçitleri için gereken en yaygın IoT protokollerini temsil eder.

:::image type="content" source="media/eal-logo-certification.png" alt-text="EAL sertifikası":::

Microsoft Azure rtos SC güvenlik sertifikası için kullanılan bt güvenlik değerlendirme olanağı, en parlama BV ' dir ve sertifika yetkilisi de bir ttıt.

### <a name="fips-140-2-validated"></a>FIPS 140-2 doğrulanan

Azure RTOS şifre kitaplıkları, şifreleme modülleri için gereksinimleri belirten, yazılım için Federal bilgi Işleme standartlaştırma 140-2 (FIPS 140-2) sertifikası elde edin. FIPS 140-2, şifreleme gücü ve özellikleri ile ilgili belirli standartları karşılamak için şifreleme tabanlı güvenlik kullanan tüm federal kamu kuruluşlarını ve departmanları gerektirir. Bu şifreleme tabanlı güvenlik standartları, Kanada ve Avrupa Birliği 'nde de tanınır.

Azure RTOS şifre kitaplıkları için kullanılan bilgi güvenliği değerlendirme laboratuvarı atsec idi ve sertifika yetkilisi [ulusal standartlar ve Teknoloji Enstitüsü (NIST)](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394).

### <a name="supports-most-popular-architectures"></a>Popüler mimarilerin çoğunu destekler

Aşağıdaki gelişmiş mimarilere dahil olmak üzere en popüler 32/64 bit mikro işlemcilerin, kullanıma hazır, tam olarak sınanmış ve tam olarak desteklenen Azure RTOS.

- **Analog cihazlar**: parça, BlackICE, CM4xx

- **Andes Core**: RISC-V

- **Ambiqmicro**: Apollo MCUs

- **ARM**: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı

- **Temposunda**: xtensa, elmas

- **Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi

- **Cypress**: RISC-V

- **Ensilica**: ESI-RISC

- **Infineon**: XMC1000, XMC4000, kanore

- **Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, varış a 10

- **Mikro yonga**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32

- **Mikro yarı**: RISC-V

- **nxp**: LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, coldfire, Kinetis cortex-M3/M4

- **Renesas**: SH, HS, v850, RX, Rz, Synergy

- **Silicon Labs**: EFM32

- **Synopsys**: Arc 600, 700, Arc Em, Arc HS

- **St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

- **TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C

- **Dalga bilgi işlem**: MIPS32 4k, 24 K, 34 k, 1004 k, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M-class

- **xilinx**: mikro blaze, PowerPC 405, zynq, zynq UltraSCALE

*Listelenen tüm zamanlama ve boyut rakamları tahminlerdir ve geliştirme platformunuzun farklı olabilir.*

## <a name="in-the-context-of-azure-iot"></a>Azure IoT bağlamında

Azure IoT 'ye doğrudan bağlanmayı veya Azure IoT Edge aracılığıyla dolaylı olarak bağlamayı ek olarak, Azure RTOS Azure Sphere cihazlarda da kullanılabilir. Azure RTOS ve Azure Sphere birleşimi, tek bir cihazda sınıf gerçek zamanlı işleme ve güvenliği birlikte getirir.
