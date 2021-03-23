---
title: Azure RTOS NetX 'i anlama
description: Azure RTOS NetX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen TCP/IP protokol standartlarının yüksek performanslı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 029f73b755d5c40279125fb010ec35baaaf7f38d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825583"
---
# <a name="overview-of-azure-rtos-netx"></a>Azure RTOS NetX 'e genel bakış

Azure RTOS NetX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan bir endüstriyel sınıf TCP/IP IPv4 Embedded ağ yığınıdır. Azure RTOS NetX, Microsoft 'un özgün IPv4 ağ yığınıdır ve aslında Azure RTOS 'ın bir alt kümesidir. NetX, IPv4, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketine sahip gömülü uygulamalar sağlar. Küçük bir kaplama, Hızlı yürütme ve üstün kullanım kolaylığı, Azure RTOS NetX 'i en zorlu ekli IoT uygulamaları için ideal bir seçenek haline getirir.

## <a name="api-protocols"></a>API protokolleri

### <a name="telnet"></a>Sun

* En az 0,5 KB ve 0,3 KB RAM ayak izi
* İstemci ve sunucu desteği
* Sezgisel Telnet API 'Leri *: \* nx_telnet_*

### <a name="auto-ip"></a>Otomatik IP

* Otomatik IPv4 adresi ataması
* En az 1,2 KB, 300 bayt RAM
* Sezgisel Oto IP API 'Leri *: \* nx_autoip_*

### <a name="http---hypertext-transfer-protocolhttp"></a>HTTP-Köprü Metni Aktarım Protokolü (HTTP)

* En az 2,8 KB-4.8 KBFLASH, 0,4 KB-1,0 KB RAM ayak
* İstemci ve sunucu desteği
* Sezgisel HTTP API 'Leri *: \* nx_http_*

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a>SMTP-Basit Posta Aktarım Protokolü (SMTP)

* En az 4,1 KB ve 0,6 KB RAM ayak izi
* İstemci desteği
* Sezgisel SMTP API 'Leri *: \* nx_smtp_*

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a>DHCP-dinamik ana bilgisayar Yapılandırma Protokolü (DHCP)

* Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi
* İstemci ve sunucu desteği
* IPv4 desteği
* Sezgisel DHCP API 'Leri *: \* nx_dhcp_*

### <a name="p0p3---post-office-protocol-version-3-pop3"></a>P0P3-Postane Protokolü sürüm 3 (POP3)

* En az 8,1 KB ve 1,4 KB RAM ayak izi
* İstemci desteği
* Sezgisel P0P3 API 'Leri *: \* nx_pop3_*

### <a name="snmp---simple-network-management-protocol-snmp"></a>SNMP-basit ağ Yönetim Protokolü (SNMP)

* En az 10,9 KB ve 2,6 KB RAM ayak izi
* VI, v2 ve v3 için aracı desteği
* Sezgisel SNMP API 'Leri *: \* nx_snmp_*

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a>FTP, TFTP-Dosya Aktarım Protokolü (FTP), Önemsiz Dosya Aktarım Protokolü (TFTP)

* FTP en az 1,8 KB-7.2 KBFLASH, 0,6 KB-2,1 KB RAM ayak izi
* TFTP en az 1,7 KB-2,4 KBFLASH, 0,3 KB-1,8 KB RAM ayak
* İstemci ve sunucu desteği
* Sezgisel FTP ve TFTP API 'Leri: <i>nx_ftp_ *</i> veya <i>nx_tftp_*</i>

### <a name="ppp---polnt-to-point-protocol-ppp"></a>PPP-POlNT noktadan noktaya Protokolü (PPP)

* En az 7,1 KB ve 3,8 KB RAM ayak izi
* Sezgisel PPP API 'Leri *: \* nx_ppp_*

### <a name="sntp---simple-network-time-protocol-sntp"></a>SNTP-basit ağ zaman Protokolü (SNTP)

* En az 4 KB ve 0,5 KB RAM
* İstemci desteği
* Sezgisel SNTP API 'Leri *: \* nx_sntp_*

### <a name="azure-rtos-netx-api"></a>Azure RTOS NetX API 'SI

* Sezgisel ve tutarlı API
* İsim-fiil adlandırma kuralı
* Hızlı, sıfır kopya API 'SI uygulama
* Azure RTOS NetX olarak kolayca tanımlanması için tüm API işlevlerinin önde gelen <i>nx_ *</i> vardır
* API işlevlerinin engellenmesi isteğe bağlı bir iş parçacığı zaman aşımına sahiptir
* Eski yuva kodu taşıma için isteğe bağlı BSD katmanı

### <a name="igmp---internet-group-management-protocol-igmp"></a>IGMP-Internet Grup Yönetimi Protokolü (ıGMP)

* En az 2,5 KB FLASH
* IPv4 çok noktaya yayın grubu desteği
* IXIA IxANVL doğrulanan
* İsteğe bağlı ıGMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
* Sezgisel ıGMP API 'Leri *: \* nx_igmp_*

### <a name="udp---user-datagram-protocol-udp"></a>UDP-Kullanıcı veri birimi Protokolü (UDP)

* Yuva başına en az 2,5 KB FLASH, 124 yuva baytı
* Hızlı, neredeyse wıned TCP paket işleme:
* 100 Mbps Ethernet, MCU @100MHz , 14% MCU kullanımı ÜZERINDE RX 95 Mbps
* TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 10% MCU kullanımı
* UDP hızlı yol™ teknolojisi
* UDP sayısıyla ilgili sınır yok
* IXIA IxANVL doğrulanan
* Yuva alma sırasında isteğe bağlı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* İsteğe bağlı UDP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
* Sezgisel UDP API 'Leri *: \* nx_udp_*

### <a name="tcp---transmission-control-protocol-tcp"></a>TCP-Iletim Denetim Protokolü (TCP)

* Minimum 10,5 K8-12,5 KB FLASH, her yuva için 280 bayt RAM
* Hızlı, neredeyse wlrespeed TCP paket işleme:
* 100 Mbps Ethernet, MCU @100MHz , 20% MCU ÜZERINDE RX 93 Mbps
* TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 27% MCU kullanımı
* Güvenilir bağlantı
* TCP yuvaları sayısında sınırsız
* IXIA IxANVL doğrulanan
* Yuva alma/iletme sırasında isteğe bağlı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* İsteğe bağlı TCP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
* Sezgisel TCP API 'Leri *: \* nx_tcp_*

### <a name="icmp---internet-control-message-protocol-icmp"></a>ICMP-Internet Denetim Iletisi Protokolü (ıCMP)

* En az 2,5 KB FLASH
* IPv4 desteği
* IXIA IxANVL doğrulanan
* Ping isteği ve ping yanıtı
* Ping isteklerinde isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* İsteğe bağlı ıCMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
* Sezgisel ıCMP API 'Leri *: \* nx_icmp_*

### <a name="ipv4---internet-protocol-ip"></a>IPv4-Internet Protokolü (IP)

* Minimum 3,5 KB-8,5 KB FLASH, 2 KB-3 KB RAM ayak
* Piconet™ mimarisi
* Hızlı, neredeyse wafklu performans
* Birden çok arabirim desteği
* Çok sayfalı destek
* Statik yönlendirme desteği
* IP parçalama/yeniden birleştirme desteği
* IPv4 desteği
* IXIA IxANVL doğrulanan
* Aşama II Ready Logo sertifikası
* İsteğe bağlı IP istatistikleri
* İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
* Sezgisel IP katmanı API 'leri *: \* nx_ip_*, *nxd_ip_ \**
* TUV ve UL-ıEC 61508 SIL 4, ıEC 62304 Class C, ISO 26262 asıl D ve EN 50128 SW-SIL4 tarafından ön sertifikalı

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a>ARP/RARP-Adres Çözümleme Protokolü (ARP), ters Adres Çözümleme Protokolü (RARP)

* Minimum 1,7 KB FLASH, RAM boyutu
* 32-blt IPv4 ve 48-blt MAC adreslerinin dinamik çözünürlüğü
* IXIA IxANVL doğrulanan
* Esnek, Kullanıcı tanımlı ARP önbelleği
* Gereksiz ARP desteği
* Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
* Sezgisel ARP/RARP API 'leri *: \* nx_arp_*, *nx_rarp_ \**

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a>ETHERNET, WiFi, BLUETOOTH LE, 15,4, vb.

## <a name="small-footprint"></a>Küçük ayak izi

Azure RTOS NetX, temel IP ve UDP desteği için 9 KB 'den 15 KB 'a kadar yeniden küçük bir parmak izine sahiptir. TCP işlevselliği için 10 KB ila 13 KB 'lık yönerge alanı belleği gerekir. Azure RTOS NetX RAM kullanımı, genellikle 2,6 KB 'den 3,6 KB 'ye ve uygulama tarafından tanımlanan paket havuzu belleğine göre değişir. Azure RTOS ThreadX gibi Azure RTOS NetX boyutu, uygulama tarafından kullanılan hizmetlere göre otomatik olarak ölçeklendirilir. Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.

## <a name="fast-execution"></a>Hızlı yürütme

Azure RTOS NetX, sıfır kopya bir paket gönderme/alma uygulamasını sağlar ve en hızlı olası performansı elde etmek için Azure RTOS ThreadX ile büyük ölçüde tümleşiktir. Örneğin, Azure RTOS NetX genellikle işlemci döngülerinin yalnızca küçük bir yüzdesini kullanarak 80 MHz bir işlemcide (veya daha az) neredeyse Won 'a yönelik veri aktarımlarını elde edebilir.

## <a name="simple-easy-to-use"></a>Basit, kullanımı kolay

Azure RTOS NetX kullanımı basittir. Azure RTOS NetX API 'SI sezgisel ve yüksek işlevselliğe sahiptir. API adları gerçek sözcüklerden oluşur ve "alfabe sonunda" değil, diğer ağ ürünlerinde ortak olan çok daha fazla kısaltılmış adlar değildir. Tüm Azure RTOS NetX API 'Lerinin önde bir *nx_* vardır ve bir ad fiil adlandırma kuralını takip edin. Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır. Örneğin, askıya aldığı tüm API işlevlerinin aynı şekilde işlev gösteren isteğe bağlı bir zaman aşımı vardır. Eski uygulamalar için, Azure RTOS NetX, ek bir BSD soketi uyumlu katman sağlar. Bu katman, geliştiricilerin büyük ağ uygulamalarını kolayca geçirmelerine yardımcı olur.

## <a name="interoperability-verification"></a>Birlikte çalışabilirlik doğrulaması

Azure RTOS NetX, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar. Azure RTOS NetX, Azure RTOS NetX Core TCP/IP protokol uygulamasının endüstri standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS NetX, şunları içeren gelişmiş bir teknolojidir:

* Piconet™ mimarisi
* Otomatik ölçeklendirme
* UDP Fast-Path teknolojisi™
* esnek paket yönetimi
* sıfır-API ve uygulama kopyalama
* çok sayfalı destek
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Statik yönlendirme desteği
* Azure RTOS TraceX sistem analizi desteği

## <a name="fastest-time-to-market"></a>En hızlı pazar süresi

Azure RTOS NetX 'i yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır. Sonuç olarak, Azure RTOS NetX, Broadcom, Gainspan ve benzeri birçok SoCs dahil olmak üzere katıştırılmış IoT cihazları için en popüler TCP/IP yığınlarından biridir. Tutarlı Pazar süresi avantajımız, şu şekilde oluşturulmuştur:

* kalite belgeleri: lütfen [Azure RTOS NetX Kullanıcı Kılavuzumuzu](about-this-guide.md) gözden geçirin ve kendiniz görün!
* Tüm kaynak kodu kullanılabilirliği
* kullanımı kolay API
* kapsamlı ve gelişmiş özellik kümesi

## <a name="one-simple-license"></a>Tek bir basit lisans

Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.

## <a name="full-highest-quality-source-code"></a>Tam, en yüksek kaliteli kaynak kodu

Yıl boyunca, Azure RTOS NetX kaynak kodu, çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı. Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.

## <a name="supports-most-popular-architectures"></a>Popüler mimarilerin çoğunu destekler

Azure RTOS NetX, en popüler 32/64 bit mikro işlemciler, kullanıma hazır, tam olarak sınanmış ve aşağıdaki gelişmiş mimariler dahil olmak üzere tam olarak desteklenmiş şekilde çalışır:

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

**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4

**Renesas**: SH, HS, v850, RX, Rz, Synergy

**Silicon Labs**: EFM32

**Synopsys**: Arc 600, 700, Arc Em, Arc HS

**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

**TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C

**Dalga bilgi işlem**: MIPS32 4k, 24 K, 34 k, 1004 k, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M-class

**Xilinx**: mikro Blaze, PowerPC 405, zynq, Zynq UltraSCALE

*Listelenen tüm zamanlama ve boyut rakamları tahminlerdir ve geliştirme platformunuzun farklı olabilir.*
