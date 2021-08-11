---
title: Bölüm 3 - Azure RTOS NetX Duo DHCPv6 sunucu yapılandırma seçenekleri
description: Bu bölümde NetX Duo DHCPv6 Azure RTOS yapılandırması seçeneklerinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1dc0d6e41118a2f67fe98758f1f31f84d074d7af342b9db93162ffe6354077ea
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792137"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-server-configuration-options"></a>Bölüm 3 - Azure RTOS NetX Duo DHCPv6 sunucu yapılandırma seçenekleri

NetX Duo DHCPv6 Server uygulaması için çeşitli yapılandırma seçenekleri vardır. Aşağıdaki listede her biri ayrıntılı olarak açıklanmaktadır:
  
- **NX_DISABLE_ERROR_CHECKING** Bu seçenek DHCPv6 hata denetimlerini kaldırır. Genellikle uygulama hata ayıklaması sırasında etkinleştirilir.  
  
- **NX_DHCPV6_SERVER_THREAD_STACK_SIZE** Bu, DHCPv6 iş parçacığı yığınının boyutunu tanımlar. Varsayılan olarak, boyut 4096 bayttır ve bu da çoğu NetX Duo uygulaması için yeterlidir.

- **NX_DHCPV6_SERVER_THREAD_PRIORITY** Bu, DHCPv6Server iş parçacığı önceliğini tanımlar. Bu, DHCPv6 Sunucusunun IP iş parçacığı görev önceliğini daha düşük olmalıdır. Varsayılan değer 2'dir.

- **NX_DHCPV6_IP_LEASE_TIMER_INTERVAL** ThreadX zamanlayıcı tarafından kira süreölçeri giriş işlevinin çağrıldı olduğu saniye olarak süreölçer aralığı. Giriş işlevi, DHCPv6 Sunucusu'nun tüm İstemcilerin kira sürelerini zamanlayıcı aralığına kadar artırması için bir bayrak ayarlar. Varsayılan olarak bu değer 60'tır.

- **NX_DHCPV6_SESSION_TIMER_INTERVAL** Oturum süreölçeri giriş işlevinin ThreadX zamanlayıcısı tarafından çağrıldı olduğu saniye olarak zamanlayıcı aralığı. Giriş işlevi, zamanlayıcı aralığına göre tahakkuk eden tüm etkin İstemci oturumu sürelerini artıracak şekilde DHCPv6 Sunucusu için bir bayrak ayarlar. Varsayılan olarak bu değer 3'tir.

Aşağıdaki tanımlar durum seçeneği ileti türü ve kullanıcı yapılandırılabilir iletisi için geçerlidir. Durum seçeneği, bir İstemci isteğinin sonucunu gösterir:

- **NX_DHCPV6_STATUS_MESSAGE_SUCCESS** *"IA OPTION GRANTED" (IA OPTION GRANTED)*

- **NX_DHCPV6_STATUS_NO_ADDRS_AVAILABLE** *"IA OPTION NOT GRANTED-NO ADDRESSES AVAILABLE" (IA SEÇENEĞI VERMİ YOK-KULLANıLABILIR ADRES YOK)*

- **NX_DHCPV6_STATUS_MESSAGE_NO_BINDING** *"IA SEÇENEĞI VERNMİ-GEÇERSIZ İSTEMCI İSTEĞI"*

- **NX_DHCPV6_STATUS_MESSAGE_NOT_ON_LINK** *"IA SEÇENEĞI VERNMİ-İSTEMCI BAĞLANTıSıNDA YOK"*

- **NX_DHCPV6_STATUS_MESSAGE_USE_MULTICAST** *"IA SEÇENEĞI VERMİLMİ-İSTEMCI ÇOK NOKTAYA YAYıN KULLANLI"*

- **NX_DHCPV6_STATUS_MESSAGE_NO_ADDRS_AVAILABLE** *IA SEÇENEĞI VERMİ YOK-ADRES YOK*

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID** Satıcı tarafından atanan kimlikle bir Sunucu DUID'i oluşturun. DUID türünün NX_DHCPV6_DUID_TYPE_VENDOR_ASSIGNED.

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_LENGTH** Satıcı tarafından atanan kimliğin üst sınırını ayarlar. Varsayılan değer 48'tir.

- **NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID** DUID'nin kuruluş türünü özel satıcı türüne ayarlar.

- **NX_DHCPV6_PACKET_WAIT_OPTION** Bu, Sunucu Hizmeti çağrısı için *bekleme nx_udp_socket_receive* tanımlar. Bu işlev, yuvada NetX Duo'dan bir alma bildirimi geri çağırma özelliğine sahip olduğu için DHCPv6 sunucusu receive işlevini çağıran paket zaten sıralandı. Varsayılan değer 1 saniyedir (1 * NX_IP_PERIODIC_RATE).

- **NX_DHCPV6_SERVER_DUID_TYPE** Bu, Sunucunun İstemciler'e tüm iletilerde dahil olduğu Sunucu DUID türünü tanımlar. Varsayılan değer bağlantı katmanı artı saattir (NX_DHCPV6_SERVER_DUID_TYPE_LINK_TIME).

- **NX_DHCPV6_SERVER_HW_TYPE** Bu, DUID bağlantı katmanı ve bağlantı katmanı artı saat seçeneklerinde donanım türünü tanımlar. Varsayılan değer, NX_DHCPV6_SERVER_HARDWARE_TYPE_ETHERNET.

- **NX_DHCPV6_PREFERENCE_VALUE** Bu, 0 ile 255 arasındaki tercih seçeneği değerini tanımlar. Burada, aynı adla DHCPv6 seçeneğinde tercih ne kadar yüksek değere sahip olursanız o kadar yüksek olur. Bu, İstemci'ye ip adresleri atamak için birden çok DHCPv6 Sunucusunun kullanılabilir olduğu bu Sunucunun teklifine hangi tercihi ekley olduğunu söyler. 255 değeri, İstemciye bu sunucuyu seçmesini belirtir. Sıfır değeri, İstemci'nin seç ücretsiz olduğunu gösterir. Varsayılan değer sıfırdır.

- **NX_DHCPV6_MAX_OPTION_REQUEST_OPTIONS** Bu, bir İstemci isteğinde bir İstemci kaydına kaydedilebilir maksimum seçenek isteği sayısını tanımlar. Varsayılan değer 6'dır.

- **NX_DHCPV6_DEFAULT_T1_TIME** İstemci adresi kiralaması için Sunucu tarafından atanan saniye olarak, İstemcinin IP adresini yenilemeye başlaması gereken süre. Varsayılan değer 2000 saniyedir.

- **NX_DHCPV6_DEFAULT_T2_TIME** İstemci adresi kiralaması için Sunucu tarafından atanan saniyeler içinde, yenileme girişiminin başarısız olduğu varsayarak İstemcinin IP adresini yeniden bağlamaya başlaması gereken süre. Varsayılan değer 3000 saniyedir.

- **NX_DHCPV6_DEFAULT_PREFERRED_TIME** Bu, atanan bir İstemci IP adresi kiralamanın kullanım dışı olduğu için Sunucu tarafından atanan saniye olarak saati tanımlar. Varsayılan değer 2 NX_DHCPV6_DEFAULT_T1_TIME.

- **NX_DHCPV6_DEFAULT_VALID_TIME** Bu, atanan bir İstemci IP adresi kirası üzerinde Sunucu tarafından atanan saniye olarak süre sonu tanımlar. Bu süre dolsa da İstemci IP adresi geçersiz olur. Varsayılan değer 2 NX_DHCPV6_DEFAULT_PREFERRED_TIME.

- **NX_DHCPV6_STATUS_MESSAGE_MAX** Durum seçeneği ileti alanında Sunucu iletisi en büyük boyutunu tanımlar. Varsayılan değer 100 bayttır.

- **NX_DHCPV6_MAX_LEASES** Sunucunun IP kira tablosu boyutunu tanımlar (örneğin, kira için depolanacak en fazla IPv6 adresi sayısı). Varsayılan olarak bu değer 100'dır.

- **NX_DHCPV6_MAX_CLIENTS** Sunucunun İstemci kayıt tablosu boyutunu tanımlar (örneğin depolanacak en fazla İstemci sayısı). Bu değer, değerden küçük veya bu değere eşit NX_DHCPV6_MAX_LEASES. Varsayılan olarak bu değer 120'dir.

- **NX_DHCPV6_PACKET_TIME_OUT** Paket ayırmalarında DHCPv6 Sunucusu bekleme süreölçer tıklarında bekleme seçeneğini tanımlar. Varsayılan değer 3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND.

- **NX_DHCPV6_PACKET_RECEIVE_WAIT** Sunucu paket havuzu üzerinde paket ayırma çağrılarında bekleme seçeneğini tanımlar. Varsayılan değer (3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND) veya 3 saniyedir.

- **NX_DHCPV6_PACKET_SIZE** Bu, Sunucu paket havuzu paketlerinin paket yükünü tanımlar. Varsayılan değer 500 bayttır.

- **NX_DHCPV6_PACKET_POOL_SIZE** Sunucunun DHCPv6 iletilerini göndermek için ayıracakları paketler için Sunucu paket havuzu boyutunu tanımlar. Varsayılan değer (10 * NX_DHCPV6_PACKET_SIZE).

- **NX_DHCPV6_TYPE_OF_SERVICE** Bu, UDP paket iletimi için hizmet türünü tanımlar. Varsayılan olarak, bu değer NX_IP_NORMAL.

- **NX_DHCPV6_FRAGMENT_OPTION** Bu, Sunucu yuvası parçalanma seçeneğini tanımlar. Varsayılan değer, NX_DON'T_FRAGMENT

- **NX_DHCPV6_TIME_TO_LIVE** Sunucudan geçen DHCPv6 yönlendiricilerinin sayısını, paketler atmadan önce 'atlar' geçişlerini belirtir. Varsayılan değer, 0x80.

- **NX_DHCPV6_QUEUE_DEPTH** NetX Duo paketleri atmadan önce Sunucu UDP yuvası alma kuyruğunda tutılacak paket sayısını belirtir.