---
title: Azure RTOS NetX Duo 'i anlama
description: Azure RTOS NetX Duo, özellikle de gömülü gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanan bir gelişmiş, endüstriyel sınıf TCP/IP ağ yığını.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 2339da391e52b437a2111ae439cccf41e038bdcf
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826926"
---
# <a name="overview-of-azure-rtos-netx-duo"></a>Azure RTOS NetX Duo 'e genel bakış

Azure RTOS NetX Duo katıştırılmış TCP/IP ağ yığını, özellikle de daha fazla gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf ikili IPv4 ve IPv6 TCP/IP ağ yığınıdır. NetX Duo, IPv4, IPv6, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketini içeren katıştırılmış uygulamalar sağlar. Azure RTOS NetX Duo, Azure RTOS NetX güvenli IPSec ve Azure RTOS NetX güvenli SSL/TLS/DTLS dahil ek eklenti güvenlik ürünleri aracılığıyla güvenlik sağlar. Bunun hepsi küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla Azure RTOS NetX Duo, en zorlu ekli IoT uygulamalarına yönelik ideal seçenektir.

## <a name="api-protocols"></a>API protokolleri

### <a name="mqtt"></a>MQTT

* Mesajlaşma kuyruğu telemetri aktarımı (MQTT)
* En az 2,7 KB FLASH
* Sezgisel MQTT API 'Leri: *nx_mqtt_*\*

### <a name="auto-ip"></a>Otomatik IP

* Otomatik IPv4 adresi ataması
* En az 1,2 KB, 300 bayt RAM
* Sezgisel Oto IP API 'Leri *: \* nx_autoip_*

### <a name="http-https"></a>HTTP, HTTPS

#### <a name="http-10"></a>HTTP 1,0

* Köprü Metni Aktarım Protokolü (HTTP)
* Minimum 2,8 KB-4,8 KB, FLASH/0,4 KB ile 1,0 KB arasında
* İstemci ve sunucu desteği
* Sezgisel API 'Ler *: \* nx_http_*

#### <a name="httphttps-11"></a>HTTP/HTTPS 1,1

* Köprü Metni Aktarım Protokolü (HTTP)
* Minimum 3,0 KB-9,5 KB FLASH/0,5 KB-2 KB RAM
* İstemci ve sunucu desteği
* Birden çok gelen istemci oturumu
* Düz metin ve şifreli HTTPS
* Kalıcı bağlantı desteği
* Çok parçalı dosya yükleme
* Azure RTOS NetX güvenli TLS ile tam olarak tümleşik
* Sezgisel API 'Ler *: \* nx_web_http*

### <a name="smtp"></a>SMTP

* Basit küçük/küçük Aktarım Protokolü (SMTP)
* En az 4,1 KB ve 0,6 KB RAM ayak izi
* İstemci desteği
* Sezgisel SMTP API 'Leri *: \* nx_smtp_*

### <a name="dhcp"></a>DHCP

* Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)
* Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi
* İstemci ve sunucu desteği
* IPv4 ve IPv6 desteği
* Sezgisel DHCP API 'Leri *: \* nx_dhcp_*

### <a name="nat"></a>NAT

* Ağ Adresi Çevirisi (NAT)
* Minimum 3,5 K6 ve 0,6 KB RAM ayak izi
* IPv4 adresi desteği
* Sezgisel NAT API 'Leri *: \* nx_nat_*
* NAT yalnızca Azure RTOS NetX Duo ile kullanılabilir

### <a name="snmp"></a>SNMP

* Basit Ağ Yönetim Protokolü (SNMP)
* En az 10,9 KB ve 2,6 KB RAM ayak izi
* VI, v2 ve v3 için aracı desteği
* Sezgisel SNMP API 'Leri *: \* nx_snmp_*

### <a name="dns-mdns-dns-sd"></a>DNS, mDNS, DNS-SD

* Etki Alanı Adı Sistemi (DNS)
* Çok noktaya yayın etki alanı adı sistemi (mDNS)
* DNS tabanlı hizmet bulma (DNS-SD)
* DNS en az 2,4 KB-3 KB FLASH, 1 KB RAM ayak
* İstemci desteği
* Sezgisel API 'Ler *: \* nx_dns_*
* mDNS ve DNS-SD yalnızca Azure RTOS NetX Duo ile kullanılabilir

### <a name="p0p3"></a>P0P3

* Postane Protokolü sürüm 3 (POP3)
* En az 8,1 KB ve 1,4 KB RAM ayak izi
* İstemci desteği
* Sezgisel P0P3 API 'Leri *: \* nx_pop3_*

### <a name="telnet"></a>Sun

* En az 0,5 KB ve 0,3 KB RAM ayak izi
* İstemci ve sunucu desteği
* Sezgisel Telnet API 'Leri *: \* nx_telnet_*

### <a name="ftp-tftp"></a>FTP, TFTP

* Dosya Aktarım Protokolü (FTP)
* Önemsiz Dosya Aktarım İletişim Kuralı (TFTP)
* FTP en az 1,8 KB-7,2 KB FLASH, 0,6 KB ile 2,1 KB RAM ayak izi
* TFTP en az 1,7 KB-2,4 KB FLASH, 0,3 KB ile 1,8 KB RAM ayak izi
* İstemci ve sunucu desteği
* Sezgisel FTP ve TFTP API 'Leri *: \* nx_ftp_* veya *nx_tftp_ \**

### <a name="ppp-pppoe"></a>PPP, PPPoE

* POlNT noktadan noktaya Protokolü (PPP)
* Ethernet üzerinden Noktadan Noktaya Protokolü (PPPoE)
* En az 7,1 KB ve 3,8 KB RAM ayak izi
* Sezgisel PPP API 'Leri *: \* nx_ppp_*

* PPPoE yalnızca Azure RTOS NetX Duo ile kullanılabilir

### <a name="sntp"></a>SNTP

* Basit ağ zaman Protokolü (SNTP)
* En az 4 KB ve 0,5 KB RAM
* İstemci desteği
* Sezgisel SNTP API 'Leri *: \* nx_sntp_*

### <a name="azure-rtos-netx-duo-api"></a>Azure RTOS NetX Duo API 'SI

* Sezgisel ve tutarlı API
* İsim-fiil adlandırma kuralı
* Hızlı, sıfır kopya API 'SI uygulama
* Azure RTOS NetX olarak kolayca tanımlanabilmesi için tüm API 'Lerin önde gelen <i>nx_ *</i>
* API 'Lerin engellenmesi isteğe bağlı iş parçacığı zaman aşımına uğradı
* Daha fazla bilgi için bkz. [Azure RTOS NetX Duo Kullanıcı Kılavuzu](about-this-guide.md)
* Eski yuva kodu taşıma için isteğe bağlı BSD katmanı

### <a name="igmp"></a>IGMP

* Internet Grup Yönetimi Protokolü (IGMP)
* En az 2,5 KB FLASH
* IPv4 çok noktaya yayın grubu desteği
* IXIA IxANVL doğrulanan
* İsteğe bağlı ıGMP istatistikleri
* Azure RTOS ThreadX aracılığıyla sistem düzeyinde izleme
* Sezgisel ıGMP API 'Leri *: \* nx_igmp_*

### <a name="azure-rtos-netx-secure-dtls"></a>Azure RTOS NetX güvenli DTLS

* Veri birimi Aktarım Katmanı Güvenliği (DTLS) 1,0 ve 1,2
* En az 11 KB FLASH
* Fast, Software RSA 2048-bit anahtar boyutu ~ 1-saniye @120MHz
* Kolaylaştırılmış X. 509.440 uygulama
* Azure RTOS NetX Duo UDP yuvaları ile tam olarak tümleşik
* Donanım şifreleme desteği
* Yazılım şifreleme desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* P eğrileri 192/224/256/384/521 dahil olmak üzere ECDSA (imzalama) ve ECDH (şifreleme) ile Eliptik Eğri Şifreleme (ECC)
* Şifrelenmiş anahtar desteği (donanıma bağımlı)

### <a name="azure-rtos-netx-secure-tls"></a>Azure RTOS NetX güvenli TLS

* Aktarım Katmanı Güvenliği (TLS) 1,0, 1,1 ve 1,2
* En az 8,8 KB FLASH
* Fast, Software RSA 2048-bit anahtar boyutu ~ 1-saniye @120MHz
* Kolaylaştırılmış X. 509.440 uygulama
* Azure RTOS NetX Duo TCP yuvaları ile tam olarak tümleşik
* Donanım şifreleme desteği
* Yazılım şifreleme desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* P eğrileri 192/224/256/384/521 dahil olmak üzere ECDSA (imzalama) ve ECDH (şifreleme) ile Eliptik Eğri Şifreleme (ECC)
* Şifrelenmiş anahtar desteği (donanıma bağımlı)

### <a name="icmp"></a>ICMP

* Internet Denetim Iletisi Protokolü (ıCMP)
* En az 2,5 KB FLASH
* IPv4 ve IPv6 desteği
* IXIA IxANVL doğrulanan
* Ping isteği ve ping yanıtı
* Ping isteklerinde isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* İsteğe bağlı ıCMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel ıCMP API 'Leri *: \* nx_icmp_*

### <a name="udp"></a>UDP

* Kullanıcı veri birimi Protokolü (UDP)
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
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel UDP API 'Leri *: \* nx_udp_*

### <a name="tcp"></a>TCP

* İletim Denetimi Protokolü (TCP)
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
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel TCP API 'Leri *: \* nx_tcp_*

### <a name="arprarp"></a>ARP/RARP

* Adres Çözümleme Protokolü (ARP)
* Ters Adres Çözümleme Protokolü (RARP)
* Minimum 1,7 KB FLASH, RAM boyutu
* 32-blt IPv4 ve 48-blt MAC adreslerinin dinamik çözünürlüğü
* IXIA IxANVL doğrulanan
* Esnek, Kullanıcı tanımlı ARP önbelleği
* Gereksiz ARP desteği
* Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel ARP/RARP API 'leri *: \* nx_arp_*, *nx_rarp_ \**

### <a name="ipv4-amp-ipv6"></a>IPv4 &amp; IPv6

* Internet Protokolü (IP)
* Minimum 3,5 KB-8,5 KB FLASH, 2 KB-3 KB RAM ayak
* Piconet™ mimarisi
* Hızlı, neredeyse wafklu performans
* Birden çok arabirim desteği
* Çok sayfalı destek
* Statik yönlendirme desteği
* IP parçalama/yeniden birleştirme desteği
* IPv4 ve IPv6 adresi desteği
* IXIA IxANVL doğrulanan
* Phase II IPv6 Ready Logo sertifikası
* İsteğe bağlı IP istatistikleri
* İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel IP katmanı API 'leri *: \* nx_ip_*, *nxd_ip_ \**, *nxd_ipv6_ \**
* TUV ve UL-ıEC 61508 SIL 4, ıEC 62304 Class C, ISO 26262 asıl D ve EN 50128 SW-SIL4 tarafından ön sertifikalı

### <a name="azure-rtos-netx-secure-ipsec"></a>Azure RTOS NetX güvenli ıPSEC

* Internet Protokolü güvenliği (ıPSEC)
* IP katmanı
* Donanım şifreleme desteği
* Aşağıdakiler dahil olmak üzere yazılım şifreleme desteği:
    * DES, 3DES
    * AES
    * HMAC-MD5
    * HMAC-SHA1
* İnternet Anahtar Değişimi (ıKE) sürüm 2 desteği
* Sezgisel IPSec API 'Leri *: \* nx_ipsec_*
* IPSec yalnızca Azure RTOS NetX Duo ile kullanılabilir

## <a name="small-footprint"></a>Küçük ayak izi

Azure RTOS NetX Duo, temel IP ve UDP desteği için 9 KB 'den 15 KB 'a kadar bir renetme sahiptir. TCP işlevselliği için 10 KB ila 13 KB 'lık yönerge alanı belleği gerekir. Azure RTOS NetX Duo RAM kullanımı, genellikle 2,6 KB 'den 3,6 KB 'ye ve uygulama tarafından tanımlanan paket havuzu belleğine göre değişir. Azure RTOS ThreadX gibi Azure RTOS NetX Duo boyutu, uygulama tarafından kullanılan hizmetlere göre otomatik olarak ölçeklendirilir. Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.

## <a name="fast-execution"></a>Hızlı yürütme

Azure RTOS NetX Duo, en hızlı olası performansı elde etmek için Azure RTOS ThreadX ile yüksek düzeyde tümleştirilmiş, sıfır kopya bir paket gönderme/alma uygulamasını sağlar. Örneğin, Azure RTOS NetX Duo, genellikle işlemci döngülerinin yalnızca küçük bir yüzdesini kullanarak 80 MHz (veya daha az) bir işlemcide neredeyse Won 'a yönelik veri aktarımları elde edebilir.

## <a name="simple-easy-to-use"></a>Basit, kullanımı kolay

Azure RTOS NetX Duo API 'SI sezgisel, kolay ve yüksek işlevselliğe sahiptir.

API adları, diğer ağ ürünlerinde yaygın olarak kullanılan "alfabe dışı" veya son derece kısaltılmış adlarla değil, gerçek sözcüklerden oluşur. Tüm Azure RTOS NetX Duo API 'Lerinde önde gelen bir *nx_* ve bir ad fiil adlandırma kuralı takip ediyoruz. Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır. Örneğin, askıya aldığı tüm API işlevlerinin aynı şekilde çalışan isteğe bağlı bir zaman aşımı vardır.

Eski uygulamalar için, Azure RTOS NetX Duo, ek bir BSD soketi uyumlu katman sağlar. Bu katman, geliştiricilerin büyük ağ uygulamalarını kolayca geçirmelerine yardımcı olur.

## <a name="safe-and-secure"></a>Güvenli ve güvenli

Azure RTOS NetX Duo güvenlidir. Bu güvenlik, IPSec, SSL, TLS ve DTLS dahil eklenti güvenlik ürünleri aracılığıyla sağlanır. Ayrıca, uygulamanın Azure RTOS NetX Duo 'e yönelik tüm dış erişimlere yönelik tümüyle denetimi vardır ve güvenlik riski belirleme çok daha kolay hale getirir.

Microsoft Azure RTOS, OEM 'Lere iletişim sağlamak ve temel alınan MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenleri sağlar. Cihazın, belirli kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşıladığından emin olmak için, bu son olarak cihaz oluşturucunun sorumluluğundadır.

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a>TUV ve UL ile birçok güvenlik standartlarına ön sertifikalı

Azure RTOS NetX Duo, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW Safety Class C, ISO 26262 asıl D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir. Sertifika, Azure RTOS NetX Duo 'un, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için, ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımlar geliştirmede kullanılabileceğini onaylar. Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir. Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenlik düzeyini güvence altına almak için kullanılır.

:::image type="content" source="media/overview-netx-duo/partener-logo-sgs-tuv-saar.png" alt-text="SGS-TUV sertifikası":::

Azure RTOS NetX Duo, UL 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R ve, programlanabilir bileşenlerde yazılım için ul 1998 güvenlik standartları ile uyumlu bir şekilde tanınıyor. UL, en fazla uzman sürmek güvenlik çözümleri sunan küresel, bağımsız bir güvenlik bilimi şirketidir. Bu, elektrik, yenilenebilir enerji ve Nanotechnology için genel olarak elektrik 'yi benimseme özelliğine sahiptir.

:::image type="content" source="media/overview-netx-duo/cru-logo-certification.png" alt-text="CRU UL sertifikası":::

TUV ve UL sertifikalarıyla ilişkili yapıtlar (sertifika, güvenlik el kitabı, test raporu vb.) satış için kullanılabilir.

Uygulamanın ek sertifikaya ihtiyacı olduğu durumlarda, gerçek donanım platformunu kullanarak ve hatta uygulama kodunu kapsayan çeşitli standartlara anahtar sertifikası sağlamak için Microsoft aracılığıyla bir sertifika hizmeti kullanılabilir. Sertifika hizmetimiz hakkında daha fazla bilgi için bizimle iletişime geçin.

## <a name="eal4-common-criteria-security-certification"></a>EAL4 + ortak ölçütler güvenlik sertifikası

Azure RTOS, EAL4 + ortak ölçütler güvenlik sertifikası elde etti. Evalution (TOE) hedefi Azure RTOS ThreadX, Azure RTOS NetX Duo, Azure RTOS NetX güvenli TLS ve Azure RTOS NetX MQTT ' i içerir. Bu, derin eklenmiş sensörler, cihazlar, uç yönlendiriciler ve ağ geçitleri için gereken en yaygın IoT protokollerini temsil eder.

:::image type="content" source="media/overview-netx-duo/eal-logo-certification.png" alt-text="EAL sertifikası":::

Microsoft Azure RTOS SC güvenlik sertifikası için kullanılan BT güvenlik değerlendirme olanağı, en parlama BV ' dir ve sertifika yetkilisi de bir Ttıt.

## <a name="fips-140-2-validated"></a>FIPS 140-2 doğrulanan

Azure RTOS NetX şifre kitaplıkları, şifreleme modülleri için gereksinimleri belirten, yazılım için Federal bilgi Işleme standartlaştırma 140-2 (FIPS 140-2) sertifikası elde edin. FIPS 140-2, şifreleme gücü ve özellikleri ile ilgili belirli standartları karşılamak için şifreleme tabanlı güvenlik kullanan tüm federal kamu kuruluşlarını ve departmanları gerektirir. Bu şifreleme tabanlı güvenlik standartları, Kanada ve Avrupa Birliği 'nde de tanınır.

Azure RTOS NetX şifre kitaplıkları için kullanılan bilgi güvenliği değerlendirme laboratuvarı atsec idi ve sertifika yetkilisi ulusal standartlar ve Teknoloji Enstitüsü (NıST). Ek ayrıntılar için [NIST Web sitesini](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394) gözden geçirin.

## <a name="interoperability-verification"></a>Birlikte çalışabilirlik doğrulaması

NetX Duo, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar.

![IPv6 Ready logosu](./media/overview-netx-duo/ipv6-ready-logo.png)

Azure RTOS NetX Duo, kapsamlı IPv6-Ready logo sertifikasına ulaşmak için yalnızca katıştırılmış TCP/IP yığınlarından biridir. Bu, IPv6 Forumu tarafından yönetilen ve doğrulanan uyumluluk ve birlikte çalışabilirlik testlerini geçti olduğunu kanıtlayın. NetX Duo Ayrıca, NetX Duo çekirdek TCP/IP protokol uygulamasının sektör standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.

## <a name="comprehensive-iot-solution"></a>Kapsamlı IoT çözümü

Azure RTOS NetX Duo, temel IP ve UDP desteği için 9 KB 'den 15 KB 'a kadar bir renetme sahiptir. NetX Duo, derin eklenmiş IoT uygulamaları için en kapsamlı TCP/IP ağıyla biridir. Bu destek, aşağıdaki eklenti protokol ürünlerini içerir:

MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPSec, Oto IP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPSec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS NetX Duo, şunları içeren gelişmiş bir teknolojidir:

* Piconet™ mimarisi
* Otomatik ölçeklendirme
* UDP Fast-Path teknolojisi™
* Esnek paket yönetimi
* Sıfır-API ve uygulama kopyalama
* Çok sayfalı destek
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* Statik yönlendirme desteği
* IPsec
* SSL/TLS/DTLS
* Azure RTOS TraceX sistem analizi desteği

## <a name="fastest-time-to-market"></a>En hızlı pazar süresi

Azure RTOS NetX Duo yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır. Sonuç olarak, NetX Duo, Broadcom ve Gainspan gibi birçok SoCs dahil olmak üzere, gömülü IoT cihazları için en popüler TCP/IP yığınlarından biridir. Tutarlı Pazar süresi avantajımız, şu şekilde oluşturulmuştur:

* Kalite belgeleri: lütfen [Azure RTOS NetX Duo Kullanıcı Kılavuzumuzu](about-this-guide.md) gözden geçirin ve kendiniz görün!
* Tüm kaynak kodu kullanılabilirliği
* Kullanımı kolay API
* Kapsamlı ve gelişmiş özellik kümesi

## <a name="one-simple-license"></a>Tek bir basit lisans

Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.

## <a name="full-highest-quality-source-code"></a>Tam, en yüksek kaliteli kaynak kodu

Yıl boyunca, Azure RTOS NetX Duo kaynak kodu, çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı. Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.

## <a name="supports-most-popular-architectures"></a>Popüler mimarilerin çoğunu destekler

Azure RTOS NetX Duo, aşağıdaki gelişmiş mimariler de dahil olmak üzere en popüler 32/64 bit mikro işlemciler üzerinde çalışır ve tamamen sınanmış ve tam olarak desteklenmektedir:

**Analog cihazlar**: parça, BlackICE, CM4xx

**Andes Core**: RISC-V

**Ambiqmicro**: Pollo MCUs

**ARM**: RM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı

**Temposunda**: xtensa, elmas

**Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi

**Cypress**: RISC-V

**Ensilica**: ESI-RISC

**Infineon**: XMC1000, XMC4000, kanore

**Intel & Intel FPGA**: X36/Pentium, XSCALE, NIOS II, Cyclone, varış a 10

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

## <a name="related-services"></a>İlgili hizmetler

IoT RTOS güvenlik modülü için Azure Güvenlik Merkezi, Azure RTOS cihazları için kapsamlı bir güvenlik çözümü sağlar. Azure RTOS için güvenlik modülü, kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı taban çizgisi sağlar ve cihaz güvenliği Hygiene 'ın artırılmasına yardımcı olur. [Azure RTOS güvenlik modülü](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) hakkında daha fazla bilgi edinin veya [Azure RTOS hızlı başlangıç Için güvenlik yapılandırması modülünü](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) kullanmaya başlayın.

## <a name="next-steps"></a>Sonraki adımlar

NetX Duo hakkında daha fazla bilgi edinmek için [Azure RTOS NetX Duo Kullanıcı kılavuzuyla](about-this-guide.md)başlayın.
