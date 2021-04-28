---
title: Azure RTOS NetX Duo 'i anlama
description: Azure RTOS NetX Duo, özellikle de gömülü gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanan bir gelişmiş, endüstriyel sınıf TCP/IP ağ yığını.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: e3fe3bcc602f409cc76f3be47aca865bf8116697
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171344"
---
# <a name="overview-of-azure-rtos-netx-duo"></a>Azure RTOS NetX Duo 'e genel bakış

Azure RTOS NetX Duo katıştırılmış TCP/IP ağ yığını, özellikle de daha fazla gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf ikili IPv4 ve IPv6 TCP/IP ağ yığınıdır. NetX Duo, IPv4, IPv6, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketini içeren katıştırılmış uygulamalar sağlar. Azure RTOS NetX Duo, Azure RTOS NetX güvenli IPSec ve Azure RTOS NetX güvenli SSL/TLS/DTLS dahil ek eklenti güvenlik ürünleri aracılığıyla güvenlik sağlar. Bunun hepsi küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla Azure RTOS NetX Duo, en zorlu ekli IoT uygulamalarına yönelik ideal seçenektir.

## <a name="api-protocols"></a>API protokolleri

### <a name="mqtt"></a>MQTT

* Mesajlaşma kuyruğu telemetri aktarımı (MQTT)
* En az 2,7 KB FLASH

### <a name="auto-ip"></a>Otomatik IP

* Otomatik IPv4 adresi ataması
* En az 1,2 KB, 300 bayt RAM

### <a name="http-https"></a>HTTP, HTTPS

#### <a name="http-10"></a>HTTP 1,0

* Köprü Metni Aktarım Protokolü (HTTP)
* Minimum 2,8 KB-4,8 KB, FLASH/0,4 KB ile 1,0 KB arasında
* İstemci ve sunucu desteği

#### <a name="httphttps-11"></a>HTTP/HTTPS 1,1

* Köprü Metni Aktarım Protokolü (HTTP)
* Minimum 3,0 KB-9,5 KB FLASH/0,5 KB-2 KB RAM
* İstemci ve sunucu desteği
* Birden çok gelen istemci oturumu
* Düz metin ve şifreli HTTPS
* Kalıcı bağlantı desteği
* Çok parçalı dosya yükleme
* Azure RTOS NetX güvenli TLS ile tam olarak tümleşik

### <a name="smtp"></a>SMTP

* Basit küçük/küçük Aktarım Protokolü (SMTP)
* En az 4,1 KB ve 0,6 KB RAM ayak izi
* İstemci desteği

### <a name="dhcp"></a>DHCP

* Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)
* Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi
* İstemci ve sunucu desteği
* IPv4 ve IPv6 desteği

### <a name="nat"></a>NAT

* Ağ Adresi Çevirisi (NAT)
* Minimum 3,5 K6 ve 0,6 KB RAM ayak izi
* IPv4 adresi desteği
* NAT yalnızca Azure RTOS NetX Duo ile kullanılabilir

### <a name="snmp"></a>SNMP

* Basit Ağ Yönetim Protokolü (SNMP)
* En az 10,9 KB ve 2,6 KB RAM ayak izi
* VI, v2 ve v3 için aracı desteği

### <a name="dns-mdns-dns-sd"></a>DNS, mDNS, DNS-SD

* Etki Alanı Adı Sistemi (DNS)
* Çok noktaya yayın etki alanı adı sistemi (mDNS)
* DNS tabanlı hizmet bulma (DNS-SD)
* DNS en az 2,4 KB-3 KB FLASH, 1 KB RAM ayak
* İstemci desteği
* mDNS ve DNS-SD yalnızca Azure RTOS NetX Duo ile kullanılabilir

### <a name="p0p3"></a>P0P3

* Postane Protokolü sürüm 3 (POP3)
* En az 8,1 KB ve 1,4 KB RAM ayak izi
* İstemci desteği

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

## <a name="safe-and-secure"></a>Güvenli ve güvenli

Azure RTOS NetX Duo güvenlidir. Bu güvenlik, IPSec, SSL, TLS ve DTLS dahil eklenti güvenlik ürünleri aracılığıyla sağlanır. Ayrıca, uygulamanın Azure RTOS NetX Duo 'e yönelik tüm dış erişimlere yönelik tümüyle denetimi vardır ve güvenlik riski belirleme çok daha kolay hale getirir.

Microsoft Azure RTOS, OEM 'Lere iletişim sağlamak ve temel alınan MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenleri sağlar. Cihazın, belirli kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşıladığından emin olmak için, bu son olarak cihaz oluşturucunun sorumluluğundadır.


## <a name="interoperability-verification"></a>Birlikte çalışabilirlik doğrulaması

NetX Duo, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar.

![IPv6 Ready logosu](./media/overview-netx-duo/ipv6-ready-logo.png)

Azure RTOS NetX Duo, kapsamlı IPv6-Ready logo sertifikasına ulaşmak için yalnızca katıştırılmış TCP/IP yığınlarından biridir. Bu, IPv6 Forumu tarafından yönetilen ve doğrulanan uyumluluk ve birlikte çalışabilirlik testlerini geçti olduğunu kanıtlayın. NetX Duo Ayrıca, NetX Duo çekirdek TCP/IP protokol uygulamasının sektör standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.

## <a name="comprehensive-iot-solution"></a>Kapsamlı IoT çözümü

NetX Duo, derin eklenmiş IoT uygulamaları için en kapsamlı TCP/IP ağıyla biridir. Bu destek, aşağıdaki eklenti protokol ürünlerini içerir.

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

## <a name="related-services"></a>İlgili hizmetler

IoT RTOS güvenlik modülü için Azure Güvenlik Merkezi, Azure RTOS cihazları için kapsamlı bir güvenlik çözümü sağlar. Azure RTOS için güvenlik modülü, kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı taban çizgisi sağlar ve cihaz güvenliği Hygiene 'ın artırılmasına yardımcı olur. [Azure RTOS güvenlik modülü](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) hakkında daha fazla bilgi edinin veya [Azure RTOS hızlı başlangıç Için güvenlik yapılandırması modülünü](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) kullanmaya başlayın.

## <a name="next-steps"></a>Sonraki adımlar

NetX Duo hakkında daha fazla bilgi edinmek için [Azure RTOS NetX Duo Kullanıcı kılavuzuyla](about-this-guide.md)başlayın.
