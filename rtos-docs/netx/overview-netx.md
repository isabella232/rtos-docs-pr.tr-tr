---
title: Azure RTOS NetX 'i anlama
description: Azure RTOS NetX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen TCP/IP protokol standartlarının yüksek performanslı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 7c864c23f019e4841ddb3096fde663c8039baf44
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171327"
---
# <a name="overview-of-azure-rtos-netx"></a>Azure RTOS NetX 'e genel bakış

Azure RTOS NetX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan bir endüstriyel sınıf TCP/IP IPv4 Embedded ağ yığınıdır. Azure RTOS NetX, Microsoft 'un özgün IPv4 ağ yığınıdır ve aslında Azure RTOS 'ın bir alt kümesidir. NetX, IPv4, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketine sahip gömülü uygulamalar sağlar. Küçük bir kaplama, Hızlı yürütme ve üstün kullanım kolaylığı, Azure RTOS NetX 'i en zorlu ekli IoT uygulamaları için ideal bir seçenek haline getirir.

## <a name="api-protocols"></a>API protokolleri

### <a name="telnet"></a>Sun

* Minimum 0,5 KB ve 0,3 KB RAM parmak izi.
* İstemci ve sunucu desteği.

### <a name="auto-ip"></a>Otomatik IP

* Otomatik IPv4 adresi ataması.
* Minimum 1,2 KB, 300 bayt RAM.

### <a name="http---hypertext-transfer-protocolhttp"></a>HTTP-Köprü Metni Aktarım Protokolü (HTTP)

* En az 2,8 KB-4.8 KBFLASH, 0,4 KB-1,0 KB-RAM ayak izi.
* İstemci ve sunucu desteği.

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a>SMTP-Basit Posta Aktarım Protokolü (SMTP)

* En az 4,1 KB ve 0,6 KB RAM ayak izi
* İstemci desteği

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a>DHCP-dinamik ana bilgisayar Yapılandırma Protokolü (DHCP)

* Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi
* İstemci ve sunucu desteği
* IPv4 desteği

### <a name="p0p3---post-office-protocol-version-3-pop3"></a>P0P3-Postane Protokolü sürüm 3 (POP3)

* En az 8,1 KB ve 1,4 KB RAM ayak izi
* İstemci desteği

### <a name="snmp---simple-network-management-protocol-snmp"></a>SNMP-basit ağ Yönetim Protokolü (SNMP)

* En az 10,9 KB ve 2,6 KB RAM ayak izi
* VI, v2 ve v3 için aracı desteği

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a>FTP, TFTP-Dosya Aktarım Protokolü (FTP), Önemsiz Dosya Aktarım Protokolü (TFTP)

* FTP en az 1,8 KB-7.2 KBFLASH, 0,6 KB-2,1 KB RAM ayak izi
* TFTP en az 1,7 KB-2,4 KBFLASH, 0,3 KB-1,8 KB RAM ayak
* İstemci ve sunucu desteği

### <a name="ppp---polnt-to-point-protocol-ppp"></a>PPP-POlNT noktadan noktaya Protokolü (PPP)

* En az 7,1 KB ve 3,8 KB RAM ayak izi
* Güvenilir ve güvenilir.

### <a name="sntp---simple-network-time-protocol-sntp"></a>SNTP-basit ağ zaman Protokolü (SNTP)

* En az 4 KB ve 0,5 KB RAM
* İstemci desteği

### <a name="azure-rtos-netx-api"></a>Azure RTOS NetX API 'SI

* Hızlı, sıfır kopya API 'SI uygulama
* Eski yuva kodu taşıma için isteğe bağlı BSD katmanı

### <a name="igmp---internet-group-management-protocol-igmp"></a>IGMP-Internet Grup Yönetimi Protokolü (ıGMP)

* En az 2,5 KB FLASH
* IPv4 çok noktaya yayın grubu desteği
* IXIA IxANVL doğrulanan
* İsteğe bağlı ıGMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme

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

### <a name="icmp---internet-control-message-protocol-icmp"></a>ICMP-Internet Denetim Iletisi Protokolü (ıCMP)

* En az 2,5 KB FLASH
* IPv4 desteği
* IXIA IxANVL doğrulanan
* Ping isteği ve ping yanıtı
* Ping isteklerinde isteğe bağlı iş parçacığı askıya alma
* Tüm askıya alma sırasında isteğe bağlı zaman aşımı
* İsteğe bağlı ıCMP istatistikleri
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme

### <a name="ipv4---internet-protocol-ip"></a>IPv4-Internet Protokolü (IP)

* Minimum 3,5 KB-8,5 KB FLASH, 2 KB-3 KB RAM ayak.
* Piconet™ mimarisi.
* Hızlı, neredeyse wafklu performans.
* Birden çok arabirim desteği.
* Çoklu bilgisayarlı destek.
* Statik yönlendirme desteği.
* IP parçalama/yeniden birleştirme desteği.
* IPv4 desteği.
* IXIA IxANVL doğrulanmadı.
* Aşama II Ready Logo sertifikası.
* İsteğe bağlı IP istatistikleri.
* İyi tanımlanmış, sezgisel fiziksel katman sürücüsü arabirimi.
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme.

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a>ARP/RARP-Adres Çözümleme Protokolü (ARP), ters Adres Çözümleme Protokolü (RARP)

* Minimum 1,7 KB FLASH, RAM boyutu.
* 32-blt IPv4 ve 48-blt MAC adreslerinin dinamik çözünürlüğü.
* IXIA IxANVL doğrulanmadı.
* Esnek, Kullanıcı tanımlı ARP önbelleği.
* Gereksiz ARP desteği.
* Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri.
* Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme.

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a>ETHERNET, WiFi, BLUETOOTH LE, 15,4, vb.

## <a name="interoperability-verification"></a>Birlikte çalışabilirlik doğrulaması

Azure RTOS NetX, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar. Azure RTOS NetX, Azure RTOS NetX Core TCP/IP protokol uygulamasının endüstri standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.

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
