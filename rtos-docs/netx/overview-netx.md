---
title: NetX Azure RTOS anlama
description: Azure RTOS NetX, Azure RTOS ThreadX ile tamamen tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen, TCP/IP protokolü standartlarının yüksek performanslı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: a5dd020daeb336f264bf611fc3a515e55dbc5dab6f9afbcfdbf3733baa66de26
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782787"
---
# <a name="overview-of-azure-rtos-netx"></a>Azure RTOS NetX'e genel bakış

Azure RTOS NetX, özellikle derin katıştırılmış, gerçek zamanlı ve IoT uygulamaları için tasarlanmış bir endüstriyel sınıf TCP/IP IPv4 tümleşik ağ yığınıdır. Azure RTOS NetX, Microsoft'un özgün IPv4 ağ yığınıdır ve temel olarak bir ağ Azure RTOS. NetX; IPv4, TCP ve UDP gibi temel ağ protokollerinin yanı sıra ek, daha üst düzey ek protokollerden oluşan eksiksiz bir paket ile tümleşik uygulamalar sağlar. Küçük bir ayak izi, hızlı yürütme ve üstün kullanım kolaylığı, NetX Azure RTOS en zorlu tümleşik IoT uygulamaları için ideal bir seçenektir.

## <a name="api-protocols"></a>API protokolleri
Azure RTOS NetX aşağıdakiler için destek sağlar.

### <a name="telnet"></a>Telnet

* En az 0,5 KB ve 0,3 KB RAM ayak izi.
* İstemci ve sunucu desteği.

### <a name="auto-ip"></a>Otomatik IP

* Otomatik IPv4 adres ataması.
* En az 1,2 KB, 300 bayt RAM.

### <a name="http---hypertext-transfer-protocolhttp"></a>HTTP - Köprü Metni Aktarım Protokolü (HTTP)

* En az 2,8 KB ile 4,8KBFLASH, 0,4 KB ile 1,0 KB RAM ayak izi.
* İstemci ve sunucu desteği.

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a>SMTP - Basit Posta Aktarım Protokolü (SMTP)

* En az 4,1 KB ve 0,6 KB RAM ayak izi
* İstemci desteği

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a>DHCP - Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)

* En az 3,6 KB ile 4,6 KB FLASH, 2,7 KB RAM ayak izi
* İstemci ve sunucu desteği
* IPv4 desteği

### <a name="p0p3---post-office-protocol-version-3-pop3"></a>P0P3 - Office Protokolü Sürüm 3 (POP3) Sonrası

* En az 8,1 KB ve 1,4 KB RAM ayak izi
* İstemci desteği

### <a name="snmp---simple-network-management-protocol-snmp"></a>SNMP - Basit Ağ Yönetimi Protokolü (SNMP)

* En az 10,9 KB ve 2,6 KB RAM ayak izi
* VI, V2 ve V3 için aracı desteği

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a>FTP, TFTP - Dosya Aktarım Protokolü (FTP), Önemsiz Dosya Aktarım Protokolü (TFTP)

* FTP En Az 1,8 KB ile 7,2KBFLASH, 0,6 KB ile 2,1 KB RAM ayak izi
* TFTP Minimal 1,7 KB ile 2,4KBFLASH, 0,3 KB ile 1,8 KB RAM ayak izi
* İstemci ve sunucu desteği

### <a name="ppp---polnt-to-point-protocol-ppp"></a>PPP - Polnt-To-PoInt Protokolü (PPP)

* En az 7,1 KB ve 3,8 KB RAM ayak izi
* Güvenilir ve güvenilir.

### <a name="sntp---simple-network-time-protocol-sntp"></a>SNTP - Basit Ağ Zamanı Protokolü (SNTP)

* En az 4 KB ve 0,5 KB RAM
* İstemci desteği

### <a name="azure-rtos-netx-api"></a>Azure RTOS NetX API'si

* Hızlı, sıfır kopya API'si uygulaması
* Eski yuva kodunun taşınabilirliği için isteğe bağlı BSD katmanı

### <a name="igmp---internet-group-management-protocol-igmp"></a>IGMP - İnternet Grup Yönetimi Protokolü (IGMP)

* En az 2,5 KB FLASH
* IPv4 çok noktaya yayın grubu desteği
* I HIP IxANVL Doğrulandı
* İsteğe bağlı IGMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme

### <a name="udp---user-datagram-protocol-udp"></a>UDP - Kullanıcı Veri Birimi Protokolü (UDP)

* Yuva başına en az 2,5 KB FLASH, 124 yuva bayt RAM
* Hızlı, kabloya yakın TCP paketi işleme:
* 100 Mb/sn Ethernet üzerinde RX 95 Mb/sn, MCU @100MHz , %14 MCU Kullanımı
* 100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %10 MCU Kullanımı
* UDP Hızlı Yolu™ teknolojisi
* UDP sayısıyla ilgili sınır yok
* I HIP IxANVL Doğrulandı
* Yuva almada isteğe bağlı askıya alma
* Tüm askıya almada isteğe bağlı zaman aşımı
* İsteğe bağlı UDP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme

### <a name="tcp---transmission-control-protocol-tcp"></a>TCP - İletim Denetimi Protokolü (TCP)

* En az 10,5K8 ile 12,5 KB FLASH, yuva başına 280 bayt RAM
* Hızlı, neredeyse wlrespeed TCP paket işleme:
* 100 Mb/sn Ethernet üzerinde RX 93 Mb/sn, MCU @100MHz , %20 MCU Kullanımı
* 100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %27 MCU Kullanımı
* Güvenilir bağlantı
* TCP yuvalarının sayısıyla ilgili sınır yok
* I HIP IxANVL Doğrulandı
* Yuva alma/iletmede isteğe bağlı askıya alma
* Tüm askıya almada isteğe bağlı zaman aşımı
* İsteğe bağlı TCP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme

### <a name="icmp---internet-control-message-protocol-icmp"></a>ICMP - İnternet Denetim İletisi Protokolü (ICMP)

* En az 2,5 KB FLASH
* IPv4 desteği
* I HIP IxANVL Doğrulandı
* Ping isteği ve ping yanıtı
* Ping istekleri üzerinde isteğe bağlı iş parçacığının askıya alınması
* Tüm askıya almada isteğe bağlı zaman aşımı
* İsteğe bağlı ICMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme

### <a name="ipv4---internet-protocol-ip"></a>IPv4 - İnternet Protokolü (IP)

* En az 3,5 KB ile 8,5 KB FLASH, 2 KB ile 3 KB RAM ayak izi.
* Piconet™ Mimarisi.
* Hızlı, kablolara yakın performans.
* Birden çok arabirim desteği.
* Çok girişli destek.
* Statik yönlendirme desteği.
* IP parçalanması/yeniden değerlendirme desteği.
* IPv4 Desteği.
* I HIP IxANVL Doğrulandı.
* Aşama II Hazır Logo Sertifikası.
* İsteğe bağlı IP istatistikleri.
* İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi.
* Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme.

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a>ARP/RARP - Adres Çözümleme Protokolü (ARP), Ters Adres Çözümleme Protokolü (RARP)

* En az 1,7 KB FLASH, RAM boyutu.
* 32 blt IPv4 ve 48 blt MAC adreslerinin dinamik çözünürlüğü.
* IXIA IxANVL doğrulanmadı.
* Esnek, Kullanıcı tanımlı ARP önbelleği.
* Gereksiz ARP desteği.
* Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri.
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme.

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a>ETHERNET, WiFi, BLUETOOTH LE, 15,4, vb.

## <a name="interoperability-verification"></a>Birlikte çalışabilirlik doğrulaması

Azure RTOS NetX, RFC standartlarına uyar ve birçok satıcının cihazlarından tüm birlikte çalışabilirlik olanağı sunar. Azure RTOS NetX, Azure RTOS NetX Core TCP/IP protokol uygulamasının endüstri standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS NetX, aşağıdakileri içeren gelişmiş bir teknolojidir.
* Piconet™ mimarisi.
* Otomatik ölçeklendirme.
* UDP Fast-Path teknolojisi™.
* Esnek paket yönetimi.
* Sıfır-API ve uygulama kopyalama.
* Çoklu bilgisayarlı destek.
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı.
* Statik yönlendirme desteği.
* Azure RTOS TraceX sistem analizi desteği.
