---
title: Azure RTOS NetX Duo 'i anlama
description: Azure RTOS NetX Duo, özellikle de gömülü gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanan bir gelişmiş, endüstriyel sınıf TCP/IP ağ yığını.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: b40a57bf385ddcf623ff7cbe0d2e798c547227d7
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754905"
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
NetX Duo, aşağıdaki HTTP/HTTPS protokollerini destekler.

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

### <a name="pop3"></a>POP3

* Post Office protokolü sürüm 3 (POP3)
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

### <a name="legacy-code-support"></a>Eski kod desteği

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
* En az 2,5 KB FLASH, yuva başına 124 yuva bayt RAM
* Hızlı, kabloya yakın TCP paket işleme:
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

Azure RTOS NetX Duo güvenlidir. Bu güvenlik, IPsec, SSL, TLS ve DTLS gibi ek güvenlik ürünleri aracılığıyla sağlanır. Ayrıca uygulamanın NetX Duo'ya tüm dış erişim üzerinde tam Azure RTOS güvenlik riski belirlemeyi çok daha kolay hale getirmiştir.

Microsoft Azure RTOS, OEM'lere iletişimin güvenliğini sağlamak ve temel MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenler sağlar. Son olarak cihaz oluşturucusu, cihazın kendi özel kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşılamasını sağlamaktır.

## <a name="interoperability-verification"></a>Birlikte çalışabilirlik doğrulaması

NetX Duo RFC standartlarına uygundur ve çoğu satıcı için cihazlarla tam birlikte çalışabilirlik sunar.

![IPv6 Hazır Logosu](./media/overview-netx-duo/ipv6-ready-logo.png)

Azure RTOS NetX Duo, sıkı IPv6-Ready Logo sertifikası elde etmek için ekli tek TCP/IP yığınlarından biri, uyumluluk ve birlikte çalışabilirlik testlerinden geçmiş olduğuna dair kanıt, IPv6 Forumu tarafından yönetildi ve doğrulandı. NetX Duo ayrıca NetX Duo çekirdek TCP/IP protokolü uygulaması için endüstri standardı IxANVL (Otomatik Ağ Doğrulama Kitaplığı) kullanır.

## <a name="comprehensive-iot-solution"></a>Kapsamlı IoT çözümü

NetX Duo, derinden eklenmiş IoT uygulamaları için en kapsamlı TCP/IP ağlarından birini içerir. Bu destek aşağıdaki eklenti protokol ürünlerini içerir.

* MQTT
* CoAP
* LWM2M
* 6LoWPAN
* SSL/TLS/DTLS
* IPsec
* AutoIP
* DHCP
* DNS
* Mdns
* DNS-SD
* FTP
* HTTP
* IPsec
* NAT
* POP3
* Ppp
* Pppoe
* SMTP
* SNMP v1/2/3
* Telnet
* Tftp

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS NetX Duo, aşağıdakilere sahip gelişmiş bir teknolojidir.

* Piconet™ mimarisi
* Otomatik ölçeklendirme
* UDP Fast-Path Technology™
* Esnek paket yönetimi
* Sıfır kopya API'si ve uygulaması
* Birden çok ana bilgisayar desteği
* Tüm askıya almada isteğe bağlı zaman aşımı
* Statik yönlendirme desteği
* IPsec
* SSL/TLS/DTLS
* Azure RTOS TraceX sistem analizi desteği

## <a name="related-services"></a>İlgili hizmetler

NetX Duo aşağıdaki ek hizmetleri sağlar.

* Azure IoT Ara Yazılımı
* Azure Defender
* IoT Hub için cihaz güncelleştirmesi.

### <a name="azure-iot-middleware"></a>Azure IoT Ara Yazılımı

NetX Duo, Azure IoT hizmetleriyle bağlantıyı kolaylaştırmak için Azure RTOS ile Embedded C için Azure SDK arasında bağlama katmanı olarak hareket eden platforma özgü bir kitaplık olan Azure RTOS için [Azure IoT Ara](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md)Yazılımı'na sahiptir. Azure IoT Ara Yazılımı'nın hedefleri aşağıdaki gibidir.
* Geliştiricilerin uygulamaları için ihtiyaç IoTHub_Client (DeviceProvisioning_Client, uygulama arabirimi) akıllı istemci arabirimlerini sağlar.
* Embedded C SDK'sı ile platform arasındaki etkileşimi düzenleme.
* Platform Azure RTOS sağlama.
* IoT Tak Çalıştır desteği.
* Güvenlik özellikleri.
* Kaynak sınırlamaya dikkat.
* Protokol desteği.

![Azure RTOS NetX Duo ile İlgili Hizmetler](./media/overview-netx-duo/related-services.png)

### <a name="azure-defender"></a>Azure Defender

Yeni IoT için Azure Defender modülü, cihazlarınız için kapsamlı bir güvenlik Azure RTOS sağlar. Azure RTOS için Güvenlik Modülü kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı temel oluşturma ve cihaz güvenlik durumu iyileştirmeye yardımcı olur. Azure RTOS için [Güvenlik Modülü hakkında](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) daha fazla bilgi edinmek veya hızlı başlangıç için Güvenlik [Modülünü Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) başlama.

### <a name="device-update-for-iot-hub"></a>IoT Hub için Cihaz Güncelleştirmesi

IoT Hub için [Azure Cihaz](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) Güncelleştirmesi, IoT cihazlarınız için havadan güncelleştirmeleri (OTA) dağıtmanıza olanak sağlayan bir hizmettir. IoT Hub için Cihaz Güncelleştirmesi modülü, NetX Duo'da IoT Hub Agent için Cihaz Azure RTOS uygulamasıdır. Cihaz oluşturucularının Cihaz Güncelleştirmesi özelliğini uygulamalarıyla tümleştiren basit API'ler sağlar.

Cihazlara havadan (OTA) güncelleştirmeleri yapılandırmayı, derlemeyi ve dağıtmayı öğrenmek için başlama kılavuzlarını içeren temel yarı iletken değerlendirme panoları örneklerine bakın.

Ayrıca, Azure RTOS ile cihaz için [Cihaz Güncelleştirmesi'IoT Hub kullanma hakkında daha fazla Azure RTOS.](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system)

## <a name="next-steps"></a>Sonraki adımlar

NetX Duo hakkında daha fazla bilgi edinmek için netx [duo Azure RTOS kılavuzu ile çalışmaya başlayabilirsiniz.](about-this-guide.md)
