---
title: NetX Duo Azure RTOS anlama
description: Azure RTOS NetX Duo gelişmiş ve endüstriyel düzeyde bir TCP/IP ağ yığınıdır. Bu yığın özellikle derin eklenmiş gerçek zamanlı ve IoT uygulamaları için tasarlanmıştır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 6112ab5cb711ca1a5c83fd5cd4b43abc0302c6c5
ms.sourcegitcommit: f9d8cf23becf96d5bd6d31dd54f89c48962fd09b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549347"
---
# <a name="overview-of-azure-rtos-netx-duo"></a>Azure RTOS NetX Duo'ya genel bakış

Azure RTOS NetX Duo ekli TCP/IP ağ yığını, Microsoft'un ayrıntılı, gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanmış gelişmiş, endüstriyel sınıf çift IPv4 ve IPv6 TCP/IP ağ yığınıdır. NetX Duo; IPv4, IPv6, TCP ve UDP gibi temel ağ protokollerinin yanı sıra ek, üst düzey eklenti protokollerinin eksiksiz bir paketini içeren tümleşik uygulamalar sağlar. Azure RTOS NetX Duo, Azure RTOS NetX Secure IPsec ve Azure RTOS NetX Secure SSL/TLS/DTLS gibi ek ek güvenlik ürünleri aracılığıyla güvenlik sunar. Bunların hepsi küçük bir ayak izi, hızlı yürütme ve üstün kullanım kolaylığıyla bir araya Azure RTOS NetX Duo'yu en zorlu tümleşik IoT uygulamaları için ideal seçenektir.

## <a name="api-protocols"></a>API protokolleri

### <a name="mqtt"></a>MQTT

* Mesajlaşma Kuyruğu Telemetri Taşıma (MQTT)
* En az 2,7 KB FLASH

### <a name="auto-ip"></a>Otomatik IP

* Otomatik IPv4 adres ataması
* En az 1,2 KB, 300 bayt RAM

### <a name="http-https"></a>HTTP, HTTPS

#### <a name="http-10"></a>HTTP 1.0

* Köprü Metni Aktarım Protokolü (HTTP)
* En az 2,8 KB - 4,8 KB FLASH / 0,4 KB ile 1,0 KB RAM
* İstemci ve sunucu desteği

#### <a name="httphttps-11"></a>HTTP/HTTPS 1.1

* Köprü Metni Aktarım Protokolü (HTTP)
* En az 3,0 KB ile 9,5 KB FLASH / 0,5 KB ile 2 KB RAM arasında
* İstemci ve sunucu desteği
* Birden çok gelen istemci oturumu
* Düz metin ve şifrelenmiş HTTPS
* Kalıcı bağlantı desteği
* Çok parçalı dosyayı karşıya yükleme
* NetX Secure TLS Azure RTOS tam olarak tümleştirilmiştir

### <a name="smtp"></a>SMTP

* Basit Alışveriş Aktarım Protokolü (SMTP)
* En az 4,1 KB ve 0,6 KB RAM ayak izi
* İstemci desteği

### <a name="dhcp"></a>DHCP

* Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)
* En az 3,6 KB ile 4,6 KB FLASH, 2,7 KB RAM ayak izi
* İstemci ve sunucu desteği
* IPv4 ve IPv6 desteği

### <a name="nat"></a>NAT

* Ağ Adresi Çevirisi (NAT)
* En az 3,5K6 ve 0,6 KB RAM ayak izi
* IPv4 adres desteği
* NAT yalnızca NetX Duo Azure RTOS kullanılabilir

### <a name="snmp"></a>SNMP

* Basit Ağ Yönetim Protokolü (SNMP)
* En az 10,9 KB ve 2,6 KB RAM ayak izi
* VI, V2 ve V3 için aracı desteği

### <a name="dns-mdns-dns-sd"></a>DNS, mDNS, DNS-SD

* Etki Alanı Adı Sistemi (DNS)
* Çok Noktaya Yayın Etki Alanı Adı Sistemi (mDNS)
* DNS tabanlı hizmet bulma (DNS-SD)
* DNS En Az 2,4 KB ile 3 KB FLASH, 1 KB RAM ayak izi
* İstemci desteği
* mDNS ve DNS-SD yalnızca NetX Duo Azure RTOS kullanılabilir

### <a name="pop3"></a>POP3

* Post Office Protocol Version 3 (POP3)
* En az 8,1 KB ve 1,4 KB RAM ayak izi
* İstemci desteği

### <a name="telnet"></a>Telnet

* En az 0,5 KB ve 0,3 KB RAM ayak izi
* İstemci ve sunucu desteği
* Sezgisel Telnet API'leri: *nx_telnet_ \**

### <a name="ftp-tftp"></a>FTP, TFTP

* Dosya Aktarım Protokolü (FTP)
* Önemsiz Dosya Aktarım İletişim Kuralı (TFTP)
* FTP En Az 1,8 KB ile 7,2 KB FLASH, 0,6 KB ile 2,1 KB RAM ayak izi
* TFTP En Az 1,7 KB ile 2,4 KB FLASH, 0,3 KB ile 1,8 KB RAM ayak izi
* İstemci ve sunucu desteği
* Sezgisel FTP ve TFTP *API'leri: nx_ftp_ \** veya *nx_tftp_ \**

### <a name="ppp-pppoe"></a>PPP, PPPoE

* Polnt-to-PoInt Protokolü (PPP)
* Noktadan Noktaya Protokolü Ethernet (PPPoE) üzerinden bağlantı
* En az 7,1 KB ve 3,8 KB RAM ayak izi
* Sezgisel PPP API'leri: *nx_ppp_ \**

* PPPoE yalnızca NetX Duo Azure RTOS kullanılabilir

### <a name="sntp"></a>SNTP

* Basit Ağ Zamanı Protokolü (SNTP)
* En az 4 KB ve 0,5 KB RAM
* İstemci desteği
* Sezgisel SNTP API'leri: *nx_sntp_ \**

### <a name="azure-rtos-netx-duo-api"></a>Azure RTOS NetX Duo API'si

* Sezgisel ve tutarlı API
* İsim-fiil adlandırma kuralı
* Hızlı, sıfır kopya API'si uygulaması
* Tüm API'ler NetX <i>nx_ kolayca</i> tanımlamak için önde gelen Azure RTOS* sahip
* Engelleme API'lerinde isteğe bağlı iş parçacığı zaman aşımı var
* Daha [Azure RTOS için bkz. NetX Duo](about-this-guide.md) Kullanıcı Kılavuzu
* Eski yuva kodunun taşınabilirliği için isteğe bağlı BSD katmanı

### <a name="igmp"></a>ıgmp

* Internet Grup Yönetimi Protokolü (IGMP)
* En az 2,5 KB FLASH
* IPv4 çok noktaya yayın grubu desteği
* I HIP IxANVL doğrulandı
* İsteğe bağlı IGMP istatistikleri
* Azure RTOS ThreadX aracılığıyla sistem düzeyinde izleme
* Sezgisel IGMP API'leri: *nx_igmp_ \**

### <a name="azure-rtos-netx-secure-dtls"></a>Azure RTOS NetX Secure DTLS

* Veri Birimi Aktarım Katmanı Güvenliği (DTLS) 1.0 ve 1.2
* En az 11 KB FLASH
* Hızlı, yazılım RSA 2048 bit anahtar boyutu ~1 saniye @120MHz
* Kolaylaştırılmış X.509 Uygulaması
* NetX Duo UDP Azure RTOS tam olarak tümleştirilmiştir
* Donanım Şifreleme Desteği
* Yazılım Şifreleme Desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* P eğrileri 192/224/256/384/521 dahil ECDSA (imzalama) ve ECDH (şifreleme) ile Üç Nokta Eğri Şifrelemesi (ECC)
* Şifrelenmiş Anahtar Desteği (donanıma bağımlı)

### <a name="azure-rtos-netx-secure-tls"></a>Azure RTOS NetX Secure TLS

* Aktarım Katmanı Güvenliği (TLS) 1.0, 1.1 ve 1.2
* En az 8,8 KB FLASH
* Hızlı, yazılım RSA 2048 bit anahtar boyutu ~1 saniye @120MHz
* Kolaylaştırılmış X.509 Uygulaması
* NetX Duo TCP Azure RTOS tam olarak tümleştirilmiştir
* Donanım Şifreleme Desteği
* Yazılım Şifreleme Desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* P eğrileri 192/224/256/384/521 dahil ECDSA (imzalama) ve ECDH (şifreleme) ile Üç Nokta Eğri Şifrelemesi (ECC)
* Şifrelenmiş Anahtar Desteği (donanıma bağımlı)

### <a name="icmp"></a>ICMP

* İnternet Denetim İletisi Protokolü (ICMP)
* En az 2,5 KB FLASH
* IPv4 ve IPv6 desteği
* I HIP IxANVL doğrulandı
* Ping isteği ve ping yanıtı
* Ping istekleri üzerinde isteğe bağlı iş parçacığının askıya alınması
* Tüm askıya almada isteğe bağlı zaman aşımı
* İsteğe bağlı ICMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel ICMP API'leri: *nx_icmp_ \**

### <a name="udp"></a>UDP

* Kullanıcı Veri Birimi Protokolü (UDP)
* Yuva başına en az 2,5 KB FLASH, 124 yuva bayt RAM
* Hızlı, kabloya yakın TCP paketi işleme:
    * 100 Mb/sn Ethernet üzerinde RX 95 Mb/sn, MCU @100MHz , %14 MCU kullanımı
    * 100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %10 MCU kullanımı
* UDP Hızlı Yolu™ teknolojisi
* UDP sayısıyla ilgili sınır yok
* I HIP IxANVL doğrulandı
* Yuva almada isteğe bağlı askıya alma
* Tüm askıya almada isteğe bağlı zaman aşımı
* İsteğe bağlı UDP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel UDP API'leri: *nx_udp_ \**

### <a name="tcp"></a>TCP

* İletim Denetimi Protokolü (TCP)
* En az 10,5K8 ile 12,5 KB FLASH, yuva başına 280 bayt RAM
* Hızlı, neredeyse wlrespeed TCP paket işleme:
    * 100 Mb/sn Ethernet üzerinde RX 93 Mb/sn, MCU @100MHz , %20 MCU kullanımı
    * 100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %27 MCU kullanımı
* Güvenilir bağlantı
* TCP yuvalarının sayısıyla ilgili sınır yok
* I HIP IxANVL doğrulandı
* Yuva alma/iletmede isteğe bağlı askıya alma
* Tüm askıya almada isteğe bağlı zaman aşımı
* İsteğe bağlı TCP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel TCP API'leri: *nx_tcp_ \**

### <a name="arprarp"></a>ARP/RARP

* Adres Çözümleme Protokolü (ARP)
* Ters Adres Çözümleme Protokolü (RARP)
* En az 1,7 KB FLASH, RAM boyutu
* 32 blt IPv4 ve 48 blt MAC adreslerinin dinamik çözümlemesi
* I HIP IxANVL doğrulandı
* Esnek, kullanıcı tanımlı ARP önbelleği
* Gratuitous ARP desteği
* Uygulama tarafından belirlenen isteğe bağlı ARP/RARP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel ARP/RARP *API'leri: \* nx_arp_*, *\* nx_rarp_*

### <a name="ipv4-amp-ipv6"></a>IPv4 &amp; IPv6

* İnternet Protokolü (IP)
* En az 3,5 KB ile 8,5 KB FLASH, 2 KB ile 3 KB RAM ayak izi
* Piconet™ mimarisi
* Hızlı, kablolara yakın performans
* Birden çok arabirim desteği
* Birden çok ana bilgisayar desteği
* Statik yönlendirme desteği
* IP parçalanması/yeniden değerlendirme desteği
* IPv4 ve IPv6 adresi desteği
* I HIP IxANVL doğrulandı
* Aşama II IPv6 Hazır Logo Sertifikası
* İsteğe bağlı IP istatistikleri
* İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
* Sezgisel IP katmanı *API'leri: nx_ip_, \** *nxd_ip_ \** *\** , nxd_ipv6_
* TTROP ve UL tarafından IEC 61508 SIL 4, IEC 62304 Sınıf C, ISO 26262 SONA D ve EN 50128 SW-SIL4 için önceden sertifikalıdır

### <a name="azure-rtos-netx-secure-ipsec"></a>Azure RTOS NetX Güvenli IPSEC

* İnternet Protokolü Güvenliği (IPSEC)
* IP katmanı
* Donanım şifreleme desteği
* Yazılım şifreleme desteği, şunları içerir:
    * DES, 3DES
    * AES
    * HMAC-MD5
    * HMAC-SHA1
* İnternet Anahtar Exchange (IKE) Sürüm 2 desteği
* Sezgisel IPsec API'leri: *nx_ipsec_ \**
* IPsec yalnızca NetX Duo Azure RTOS kullanılabilir

## <a name="safe-and-secure"></a>Kasa ve güvenli

Azure RTOS NetX Duo güvenlidir. Bu güvenlik IPsec, SSL, TLS ve DTLS gibi eklenti güvenlik ürünleri aracılığıyla sağlanır. Ayrıca uygulamanın NetX Duo'ya tüm dış erişim üzerinde tam Azure RTOS güvenlik riski belirlemeyi çok daha kolay hale getirmiştir.

Microsoft Azure RTOS, OEM'lere iletişimin güvenliğini sağlamak ve temel MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenler sağlar. Son olarak cihaz oluşturucusu, cihazın kendi özel kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşılamasını sağlamaktır.


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

### <a name="azure-iot"></a>Azure IoT

NetX Duo, Azure IoT hizmetlerine bağlanmayı kolaylaştırmak amacıyla Azure RTOS ve Embedded C için Azure SDK arasında bağlama katmanı görevi gören platforma özel bir kitaplık olan Azure [RTOS Için Azure IoT ara yazılımı](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md)içerir. Azure IoT ara yazılımı amaçları şunlardır.
* Geliştiricilerin uygulamaları için ihtiyaç duyduğu akıllı istemci arabirimlerini (IoTHub_Client, DeviceProvisioning_Client) sağlayın.
* Gömülü C SDK 'Sı ve platformu arasındaki etkileşimi düzenleyin.
* Azure RTOS platformu başlatma sağlayın.
* IoT Tak ve Kullan desteği.
* Güvenlik özellikleri.
* Kaynak sınırlaması fark edilir.
* Protokol desteği.

![Azure RTOS NetX Duo ile Ilgili hizmetler](./media/overview-netx-duo/related-services.png)

### <a name="azure-defender"></a>Azure Defender

IoT için Azure Defender güvenlik modülü, Azure RTOS cihazları için kapsamlı bir güvenlik çözümü sağlar. Azure RTOS için güvenlik modülü, kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı taban çizgisi sağlar ve cihaz güvenliği Hygiene 'ın artırılmasına yardımcı olur. [Azure RTOS güvenlik modülü](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) hakkında daha fazla bilgi edinin veya [Azure RTOS hızlı başlangıç Için güvenlik yapılandırması modülünü](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) kullanmaya başlayın.

### <a name="device-update-for-iot-hub"></a>IoT Hub için cihaz güncelleştirmesi

[IoT Hub Için Azure cihaz güncelleştirmesi](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) , IoT cihazlarınız için kablosuz güncelleştirmeleri (OTA) dağıtmanıza olanak sağlayan bir hizmettir. IoT Hub modülü için cihaz güncelleştirmesi, Azure RTOS NetX Duo 'da IoT Hub aracısının cihaz güncelleştirme uygulamasıdır. Cihaz oluşturucuların, uygulamasındaki cihaz güncelleştirme yeteneklerini tümleştirmeleri için basit API 'Ler sağlar.

Cihazlarda AIR (OTA) güncelleştirmelerini yapılandırma, oluşturma ve dağıtma hakkında bilgi edinmek için Başlarken kılavuzlarını içeren anahtar yarı iletkeni değerlendirme panoları örneklerine bakın.

[Azure RTOS ile IoT Hub Için cihaz güncelleştirme](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system)kullanma hakkında daha fazla bilgi edinebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

NetX Duo hakkında daha fazla bilgi edinmek için [Azure RTOS NetX Duo Kullanıcı kılavuzuyla](about-this-guide.md)başlayın.
