---
title: RTOS Microsoft Azure nedir?
description: Azure RTOS, mikrodenetleyici birimleri (MCU) tarafından desteklenen IoT ve uç cihazlar için gerçek zamanlı bir işletim sistemidir (RTOS).
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: d9bd7cfda454e73e9bd270b86616780ab7ceab1a76160a66cf49a9ef82efae05
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792409"
---
# <a name="what-is-microsoft-azure-rtos"></a>RTOS Microsoft Azure nedir?

Azure RTOS, mikrodenetleyici birimleri (MCU) tarafından desteklenen Nesnelerin İnterneti (IoT) ve uç cihazlar için gerçek zamanlı bir işletim sistemidir (RTOS). Azure RTOS, en fazla kısıtlanmış cihazları (pil destekli ve 64 KB'tan az flash belleğe sahip) destekleyecek şekilde tasarlanmıştır.

Azure RTOS çeşitli güvenlik standartları için önceden sertifikalıdır. Bunlar IEC 61508 SIL 4, IEC 62304 Sınıf C ve ISO 26262 ISO D sertifikalarıdır.

Azure RTOS, IPsec aracılığıyla tam IP katmanı güvenliği ve TLS ve DTLS aracılığıyla yuva katmanı güvenliği de dahil olmak üzere EAL4+ Ortak Ölçütler güvenlik sertifikalı bir ortam sağlar. Yazılım şifreleme kitaplığımız FIPS 140-2 sertifikasına ulaştı. Ayrıca donanım şifreleme özelliklerinden, ThreadX MODULES aracılığıyla bellek korumadan ve ARM'nin TrustZone ARMv8-M güvenlik özelliklerine yönelik destekten de yararlaniyoruz.

## <a name="components-of-azure-rtos"></a>Azure RTOS bileşenleri

Azure RTOS platformu, Azure RTOS ThreadX, Azure RTOS FileX, Azure RTOS GUIX, Azure RTOS NetX, Azure RTOS NetX Duo ve Azure RTOS USBX gibi çalışma zamanı çözümleri koleksiyonudur.

### <a name="azure-rtos-threadx"></a>Azure RTOS ThreadX

Azure [RTOS ThreadX,](threadx/overview-threadx.md) özellikle derin Real-Time için tasarlanmış gelişmiş bir İşletim Sistemi (RTOS) işletim sistemidir. ThreadX'in sağladığı Azure RTOS arasında gelişmiş zamanlama özellikleri, ileti geçirme, kesinti yönetimi ve mesajlaşma hizmetleri yer alır. Azure RTOS ThreadX'in picokernel mimarisi, ön üretim eşiği zamanlaması, olay zincirleme ve zengin bir sistem hizmetleri kümesi gibi birçok gelişmiş özelliği vardır.

### <a name="azure-rtos-filex"></a>Azure RTOS FileX

Azure [RTOS FileX,](filex/overview-filex.md) yüksek performanslı FAT uyumlu bir dosya sistemidir. Azure RTOS ThreadX ile tamamen tümleştirilmiştir ve desteklenen tüm işlemciler için kullanılabilir. ThreadX Azure RTOS gibi Azure RTOS FileX de küçük bir ayak izine ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu nedenle dosya işlemleri gerektiren günümüzün derin tümleşik uygulamaları için idealdir. Azure RTOS FileX, LevelX aracılığıyla RAM diski, USBX, SD CARD ve NAND/NOR flash bellekler dahil olmak üzere çoğu fiziksel medyayı Azure RTOS destekler.

### <a name="azure-rtos-guix"></a>Azure RTOS GUIX

Azure [RTOS GUIX,](guix/overview-guix.md) tümleşik sistem geliştiricilerinin ihtiyaçlarını karşılamak için oluşturulmuş profesyonel bir grafik kullanıcı arabirimi paketidir. Alternatiflerin aksine, Azure RTOS GUIX küçüktür, hızlıdır ve grafik çıkış desteğine sahip neredeyse tüm donanım yapılandırmalarına kolayca taşınabilir. Azure RTOS GUIX ayrıca olağanüstü bir görsel çekicilik ve uygulama düzeyinde kullanıcı arabirimi geliştirme için sezgisel ve güçlü bir API sunar.

### <a name="azure-rtos-netx"></a>Azure RTOS NetX

Azure [RTOS NetX,](netx/overview-netx.md) TCP/IP protokolü standartlarının yüksek performanslı bir uygulamasıdır. Azure RTOS ThreadX ile tamamen tümleşiktir ve desteklenen tüm işlemciler için kullanılabilir. Azure RTOS NetX'in benzersiz bir Piconet mimarisi vardır. Sıfır kopya api'si ile birlikte, ağ bağlantısı gerektiren, günümüzün derinden eklenmiş uygulamaları için mükemmel bir uyum sağlar.

### <a name="azure-rtos-netx-duo"></a>Azure RTOS NetX Duo

Azure [RTOS NetX](netx-duo/overview-netx-duo.md) Duo, derin katıştırılmış, gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanmış gelişmiş, Endüstriyel Sınıf TCP/IP ağ yığınlarıdır. Azure RTOS NetX Duo ikili bir IPv4 ve IPv6 ağ yığınıyken NetX, Azure RTOS NetX Duo'nın bir alt kümesi olan özgün IPv4 ağ yığınıdır.

### <a name="azure-rtos-usbx"></a>Azure RTOS USBX

Azure [RTOS USBX,](usbx/overview-usbx.md) yüksek performanslı bir USB ana bilgisayarı, cihazı ve On-The-Go (OTG) tümleşik yığınıdır. ThreadX ile tamamen tümleşiktir ve ThreadX tarafından desteklenen tüm Azure RTOS kullanılabilir. ThreadX Azure RTOS gibi, Azure RTOS USBX de küçük bir ayak izine ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da USB cihazlarıyla arabirim gerektiren derin tümleşik uygulamalar için idealdir.

### <a name="windows-tools"></a>Windows araçları

Azure [RTOS GUIX Studio,](guix/about-guix-studio.md) uygulamanın GUI'sinde tüm grafik öğelerinin oluşturulmasını ve bakımını kolaylaştıran eksiksiz bir GUI uygulaması tasarım ortamı sağlar. Azure RTOS GUIX Studio, otomatik olarak Azure RTOS GUIX kitaplığıyla uyumlu, derlenir ve hedefte çalıştır olmaya hazır C kodu üretir.

Azure [RTOS TraceX,](tracex/overview-tracex.md) geliştiricilere gerçek zamanlı sistem olaylarının grafik görünümünü sağlayan ve gerçek zamanlı sistemlerinin davranışını görselleştirmelerine ve daha iyi anlamalarına olanak sağlayan konak tabanlı bir analiz aracıdır.

## <a name="the-azure-rtos-advantage"></a>Azure RTOS Avantajı
Azure RTOS gerçek zamanlı işletim sistemlerine göre aşağıdaki avantajları sağlar.

### <a name="most-deployed-rtos"></a>En çok dağıtılan RTOS

Azure RTOS M2M pazar zekası firması VDC Research'e göre dünya çapında 6,2 milyardan fazla dağıtım var. Bu Azure RTOS popülerliği güvenilirlik, kalite, boyut, performans, gelişmiş özellikler, kullanım kolaylığı ve genel pazara satış süresi avantajlarının bir dezavantajıdır.

> *"Şirketin kurulduğundan bu yana kablosuz ve IoT pazarlarında THREADX'in büyüme rotası takip edildi ve THREADX'in sektör genelinde benimsenmesi giderek daha çok etkileniyor."* – Chris Rommel, VDC Research Başkan Yardımcısı

### <a name="intuitive-and-consistent-api-design"></a>Sezgisel ve tutarlı API tasarımı

* Sezgisel ve tutarlı API.
* İsim-fiil adlandırma kuralı.
* Tüm API'ler, ait *olduğu* tx_ kolayca  tanımlamak için ThreadX için fx_ ön eke ve FileX için Azure RTOS ön eke sahip olur.
* API'ler genelinde işlevsel tutarlılık. Örneğin, askıya alan tüm API işlevleri aynı şekilde işlev alan isteğe bağlı bir zaman aşımına sahiptir.
* Birçok API doğrudan uygulama ISR'lerinden kullanılabilir.
- Medya ve dosya işlemleri için isteğe bağlı kullanıcı bildirimi geri çağırmaları.
* Olay odaklı programlama modeli (API).

### <a name="high-efficiency"></a>Yüksek verimlilik

- Küçük kod ayak izi.
- Kullanılan hizmetlere göre ölçeklenebilir kod ayak izi.
- TTROP ve UL tarafından IEC 61508 SIL 4, IEC 62304 Sınıf C, ISO 26262 SONA D ve EN 50128 SW-SIL4 için önceden sertifikalıdır.
- Hızlı yürütme. Azure RTOS hız için tasarlanmıştır ve mümkün olan en hızlı performansı elde etmeye yardımcı olmak için minimum iç işlev çağrısı katmanına sahiptir.

### <a name="fastest-time-to-market"></a>En hızlı pazara satış süresi

Azure RTOS yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve bakımını yapmak kolaydır. Sonuç olarak, Azure RTOS, Broadcom, Gainspan ve benzeri birçok SoC dahil olmak üzere tümleşik IoT cihazları için en popüler gerçek zamanlı işletim sistemlerinden birisidir. Tutarlı pazara satış süresi avantajımız şu şekildedir:

* Kaynak kodu kullanılabilirliğini tamamlama.
* Kullanımı kolay API.
* Kapsamlı ve gelişmiş özellik kümesi.
* Kalite belgeleri.

### <a name="one-simple-license"></a>Tek Bir Basit Lisans

Kaynak kodu kullanmanın ve test etmek için bir maliyeti ve önceden lisanslı cihazlara dağıtıldığında üretim lisansları için maliyet yoktur, diğer tüm cihazların basit bir yıllık lisansı olması gerekir.

### <a name="full-highest-quality-source-code"></a>Tam, en yüksek kaliteli kaynak kodu

Yıllar boyunca Azure RTOS kodu, kalite ve anlama kolaylığı çıtasını ayarladı. Ayrıca, dosya başına bir işleve sahip olmak, kolay kaynak gezintisi sağlar.

### <a name="pre-certified-by-tuv-and-ul-to-many-safety-standards"></a>TUV ve UL tarafından birçok güvenlik standartlarına önceden onaylandı

Azure RTOS, IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 SATıR D ve EN 50128'e göre güvenlik açısından kritik sistemlerde kullanım için VEZİP-TTROP Saar tarafından sertifikalandı. Sertifikasyon, Azure RTOS'nin IEC-61508, IEC-62304, ISO 26262 ve EN 50128'in "Elektrik, elektronik ve programlanabilir elektronik güvenlikle ilgili sistemlerin işlevsel güvenliği" için en yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımların geliştirilmesinde kullanılablı olduğunu onaylar. Almanya'nın SGS-Group ve TTAB Saarland'ın ortak girişimiyle oluşturulan VEPÜS-TTAB Saar, dünya çapında güvenlikle ilgili sistemler için ekli yazılımları test etme, denetleme, doğrulama ve onaylama konusunda yetkilendirilmiş, bağımsız lider şirket haline gelmiştir. Endüstriyel güvenlik standardı IEC 61508 ve IEC-62304, ISO 26262 ve EN 50128 dahil olmak üzere bu standarttan türetilen tüm standartlar elektrik, elektronik ve programlanabilir elektronik güvenlikle ilgili tıbbi cihazların, işlem kontrol sistemlerinin, endüstriyel makinelerin, otomobillerin ve demir yolu kontrol sistemlerinin işlevsel güvenliğini sağlamak için kullanılır.

:::image type="content" source="media/partener-logo-sgs-tuv-saar.png" alt-text="YERİNE-TUV sertifikası":::

Azure RTOS UL tarafından UL 60730-1 Ek H, CSA E60730-1 Ek H, IEC 60730-1 Ek H, UL 60335-1 Ek R, IEC 60335-1 Ek R ve PROGRAMlanabilir bileşenlerde yazılım için UL 1998 güvenlik standartları ile uyumluluk için kabul edilmiştir. UL, elektriğin genel olarak benimsenmesinden sürdürülebilirlik, yenilenebilir enerji ve nanoteknolojiye kadar uzanan, yüz yıllık uzmanlık alanında yenilik niteliğinde güvenlik çözümlerine sahip küresel, bağımsız bir güvenlik bilimi şirketidir.

:::image type="content" source="media/cru-logo-certification.png" alt-text="CRU UL sertifikası":::

Artifacts (Sertifika, Güvenlik Kılavuzu, Test Raporu vb.) ve UL sertifikaları satışa sunuldu.

Uygulamanın ek sertifikasyona ihtiyacı olduğu durumlarda, gerçek donanım platformunu kullanarak ve hatta uygulama kodunu kapsayan çeşitli standartlara anahtar teslim sertifikasyon sağlamak için Microsoft aracılığıyla bir sertifikasyon hizmeti kullanılabilir. Sertifikasyon hizmetimiz hakkında daha fazla bilgi için bizimle iletişime geçin.

### <a name="eal4-common-criteria-security-certification"></a>EAL4+ Ortak Ölçütler güvenlik sertifikası

Azure RTOS EAL4+ Ortak Ölçütler güvenlik sertifikası elde etti. Değerlendirme Hedefi (TOE), Azure RTOS, Azure RTOS NetX Duo, Azure RTOS NetX Secure TLS ve NetX MQTT Azure RTOS kapsar. Bu, derin katıştırılmış algılayıcılar, cihazlar, uç yönlendiriciler ve ağ geçitleri için gereken en tipik IoT protokollerini temsil eder.

:::image type="content" source="media/eal-logo-certification.png" alt-text="EAL sertifikası":::

RTOS SC güvenlik sertifikası için Microsoft Azure IT Güvenlik Değerlendirme Tesisi Brightsight BV, Sertifika Yetkilisi ise SERTIT'tir.

### <a name="fips-140-2-validated"></a>FIPS 140-2 Doğrulandı

Azure RTOS Şifreleme kitaplıkları, şifreleme modüllerinin gereksinimlerini belirten Yazılım için Federal Bilgi İşleme Standartlaştırma 140-2 (FIPS 140-2) Sertifikası elde etti. FIPS 140-2, şifreleme gücü ve özellikleriyle ilgili belirli standartları karşılamak için şifreleme tabanlı güvenlik kullanan tüm federal kamu kurumları ve departmanlarını gerektirir. Bu şifreleme tabanlı güvenlik standartları Kanada ve Avrupa Birliği'nde de tanınır.

Şifreleme kitaplıkları için kullanılan Information Security Azure RTOS laboratuvarı güvenli bir şekilde, sertifika yetkilisi ise Ulusal Standartlar ve Teknoloji [Enstitüsü(NIST) 'dır.](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394)

### <a name="supports-most-popular-architectures"></a>En popüler mimarileri destekler

Azure RTOS gelişmiş mimariler de dahil olmak üzere en popüler 32/64 bit mikro işlemcileri, hazır, tamamen test edilmiş ve tam olarak desteklenen mikro işlemcileri destekler.

- **Analog Cihazlar:** SHARC, Blackfin, CM4xx

- **Andes Core**: RISC-V

- **Ambiqmicro:** Apollo MUS

- **ARM:** ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M

- **Tempo:** Xtensa, Diamond

- **CEVA:** PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi

- **Cypress:** RISC-V

- **EnSilica**: eSi-RISC

- **Infineon:** XMC1000, XMC4000, TriCore

- **Intel; Intel FPGA:** x36/Pentium, XScale, NIOS II, Cyclone, Arria 10

- **Microchip:** AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32

- **Microsemi:** RISC-V

- **NXP:** LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4

- **Renesas:** SH, HS, V850, RX, RZ, Synergy

- **Silikon Laboratuvarları:** EFM32

- **Özet:** ARC 600, 700, ARC EM, ARC HS

- **ST:** STM32, ARM7, ARM9, Cortex-M3/M4/M7

- **Tl:** C5xxx, C6xxx,Xxxris, Sitara, Tiva-C

- **Dalga Bilişimi:** MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interApula, proAptiv, M Sınıfı

- **Xilinx:** MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE

*Listelenen tüm zamanlama ve boyut rakamları tahminlerdendir ve geliştirme platformda farklı olabilir.*

## <a name="in-the-context-of-azure-iot"></a>Azure IoT bağlamında

Azure IoT'ye doğrudan bağlanmanın veya Azure IoT Edge üzerinden dolaylı olarak bağlanmanın yanı sıra Azure RTOS cihazlarda da Azure Sphere kullanılabilir. Cihaz ve Azure RTOS Azure Sphere, en iyi gerçek zamanlı işleme ve güvenliği tek bir cihazda bir araya getirir.
