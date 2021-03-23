---
title: Bölüm 3-Azure RTOS NetX Duo DHCPv6 sunucu yapılandırma seçenekleri
description: Bu bölümde, Azure RTOS NetX Duo DHCPv6 sunucu yapılandırma seçeneklerinin bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 30f6e1c657eb62ebec48d6bb8caafac320727146
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827004"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-server-configuration-options"></a>Bölüm 3-Azure RTOS NetX Duo DHCPv6 sunucu yapılandırma seçenekleri

NetX Duo DHCPv6 sunucu uygulaması oluşturmak için birkaç yapılandırma seçeneği vardır. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:
  
- **NX_DISABLE_ERROR_CHECKING** Bu seçenek, DHCPv6 hata denetimini kaldırır. Bu, genellikle uygulamanın hatası ayıklandığında etkinleştirilir.  
  
- **NX_DHCPV6_SERVER_THREAD_STACK_SIZE** Bu, DHCPv6 iş parçacığı yığınının boyutunu tanımlar. Varsayılan olarak, boyut en fazla NetX Duo uygulaması için yeterince fazla olan 4096 bayttır.

- **NX_DHCPV6_SERVER_THREAD_PRIORITY** Bu, DHCPv6Server iş parçacığı önceliğini tanımlar. Bu, DHCPv6 sunucusunun IP iş parçacığı görev önceliğinden daha düşük olmalıdır. Varsayılan değer 2 ' dir.

- **NX_DHCPV6_IP_LEASE_TIMER_INTERVAL** Timer Zamanlayıcı girişi işlevinin ThreadX Scheduler tarafından çağrılmasının saniye cinsinden süreölçer aralığı. Giriş işlevi, DHCPv6 sunucusu için, Zamanlayıcı aralığı tarafından kiralamasında tüm Istemcilerin tahakkuk eden süresini artırmasını sağlamak üzere bir bayrak ayarlar. Varsayılan olarak, bu değer 60 ' dir.

- **NX_DHCPV6_SESSION_TIMER_INTERVAL** Oturum Zamanlayıcı girişi işlevinin ThreadX Zamanlayıcı tarafından çağrılmasının saniye cinsinden süreölçer aralığı. Giriş işlevi, DHCPv6 sunucusu için Zamanlayıcı aralığı tarafından tahakkuk edilen tüm etkin Istemci oturumu süresini artırmak üzere bir bayrak ayarlar. Varsayılan olarak, bu değer 3 ' dir.

Aşağıdaki tanımlar durum seçeneği ileti türü ve kullanıcı yapılandırılabilir iletisi için geçerlidir. Durum seçeneği, bir Istemci isteğinin sonucunu gösterir:

- **NX_DHCPV6_STATUS_MESSAGE_SUCCESS** *"IA seçeneği verildi"*

- **NX_DHCPV6_STATUS_NO_ADDRS_AVAILABLE** *"IA SEÇENEĞI VERILMEDI-kullanılabilir adres yok"*

- **NX_DHCPV6_STATUS_MESSAGE_NO_BINDING** *"IA SEÇENEĞI VERILMEDI-geçersiz istemci isteği"*

- **NX_DHCPV6_STATUS_MESSAGE_NOT_ON_LINK** *"IA SEÇENEĞI VERILMEDI-istemci bağlantıda değil"*

- **NX_DHCPV6_STATUS_MESSAGE_USE_MULTICAST** *"IA seçeneğine ızın VERILMEDI-ISTEMCI çok noktaya yayın kullanmalıdır"*

- **NX_DHCPV6_STATUS_MESSAGE_NO_ADDRS_AVAILABLE** *IA SEÇENEĞI VERILMEMIŞ-kullanılabilir adres yok*

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID** Satıcı tarafından atanan KIMLIĞE sahip bir sunucu DUıD 'si oluşturun. Bu, DUıD türü NX_DHCPV6_DUID_TYPE_VENDOR_ASSIGNED ayarlanmalıdır.

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_LENGTH** Satıcının atandığı KIMLIğIN üst sınırını ayarlar. Varsayılan değer 48 ' dir.

- **NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID** DUıD 'nin kuruluş türünü özel satıcı türüne ayarlar.

- **NX_DHCPV6_PACKET_WAIT_OPTION** Bu, sunucu *nx_udp_socket_receive* çağrısı için bekleme seçeneğini tanımlar. Bu, yuvanın NetX Duo 'den bir alma bildirimi geri çağırması olduğundan, DHCPv6 sunucusu Receive işlevini çağırdığında paket zaten kuyruğa alındığından, bu, bu şekilde çalışır. Varsayılan değer 1 saniyedir (1 * NX_IP_PERIODIC_RATE).

- **NX_DHCPV6_SERVER_DUID_TYPE** Bu, sunucunun Istemcilere tüm iletilere dahil olduğu sunucu DUıD türünü tanımlar. Varsayılan değer bağlantı katmanı ve zaman (NX_DHCPV6_SERVER_DUID_TYPE_LINK_TIME).

- **NX_DHCPV6_SERVER_HW_TYPE** Bu, DUıD bağlantı katmanındaki donanım türünü ve bağlantı katmanını ve zaman seçeneklerini tanımlar. Varsayılan değer NX_DHCPV6_SERVER_HARDWARE_TYPE_ETHERNET.

- **NX_DHCPV6_PREFERENCE_VALUE** Bu, değeri 0 ile 255 arasında tanımlar; burada değerin ne kadar yüksek olması, aynı ada sahip DHCPv6 seçeneğinde değerinin daha yüksektir. Bu, Istemciye, IP adresleri atamak için birden çok DHCPv6 sunucusunun kullanılabildiği bu sunucunun teklifine ne kadar tercih yerleştirileceğini bildirir. 255 değeri, Istemcinin bu sunucuyu seçmesini ister. Sıfır değeri, Istemcinin seçebileceğiniz boş olduğunu gösterir. Varsayılan değer sıfırdır.

- **NX_DHCPV6_MAX_OPTION_REQUEST_OPTIONS** Bu, bir istemci isteğine bir Istemci kaydına Kaydedilebilecek maksimum seçenek isteği sayısını tanımlar. Varsayılan değer 6 ' dır.

- **NX_DHCPV6_DEFAULT_T1_TIME** İstemcinin IP adresini yenilemeye başlaması gereken zamana yönelik Istemci adresi kirası üzerinde sunucu tarafından atanan saniye cinsinden süre. Varsayılan değer 2000 saniyedir.

- **NX_DHCPV6_DEFAULT_T2_TIME** İstemcinin, yenileme girişimi başarısız olduğu varsayılarak, IP adresini yeniden bağlanmaya başlaması gereken süre için Istemci adresi kirası üzerinde sunucu tarafından atanan saniye cinsinden süre. Varsayılan değer 3000 saniyedir.

- **NX_DHCPV6_DEFAULT_PREFERRED_TIME** Bu, atanan bir Istemci IP adresi kirası kullanım dışı olduğunda, sunucu tarafından atanan saniye cinsinden süreyi tanımlar. Varsayılan değer 2 NX_DHCPV6_DEFAULT_T1_TIME.

- **NX_DHCPV6_DEFAULT_VALID_TIME** Bu, atanan Istemci IP adresi kirası üzerinde sunucu tarafından atanan süre sonu süresini tanımlar. Bu süre dolduktan sonra Istemci IP adresi geçersiz olur. Varsayılan değer 2 NX_DHCPV6_DEFAULT_PREFERRED_TIME.

- **NX_DHCPV6_STATUS_MESSAGE_MAX** Durum seçeneği ileti alanındaki en büyük sunucu iletisi boyutunu tanımlar. Varsayılan değer 100 bayttır.

- **NX_DHCPV6_MAX_LEASES** Sunucunun IP kira tablosunun boyutunu tanımlar (örneğin, kiralanabilir en fazla IPv6 adresi sayısı). Varsayılan olarak, bu değer 100 ' dir.

- **NX_DHCPV6_MAX_CLIENTS** Sunucunun Istemci kayıt tablosu boyutunu tanımlar (örneğin, depolanabilecek en fazla Istemci sayısı). Bu değer NX_DHCPV6_MAX_LEASES değerden küçük veya bu değere eşit olmalıdır. Varsayılan olarak, bu değer 120 ' dir.

- **NX_DHCPV6_PACKET_TIME_OUT** DHCPv6 sunucusunun paket ayırmaları üzerinde beklemesi için süreölçer onay işaretleri içindeki bekleme seçeneğini tanımlar. Varsayılan değer 3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND.

- **NX_DHCPV6_PACKET_RECEIVE_WAIT** Sunucu paket havuzundaki paket ayırma çağrılarında bekle seçeneğini tanımlar. Varsayılan değer (3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND) veya 3 saniyedir.

- **NX_DHCPV6_PACKET_SIZE** Bu, sunucu paket havuzu paketlerinin paket yükünü tanımlar. Varsayılan değer 500 bayttır.

- **NX_DHCPV6_PACKET_POOL_SIZE** Sunucunun DHCPv6 iletileri göndermek için ayırabilecek paketlerin sunucu paket havuzu boyutunu tanımlar. Varsayılan değer (10 * NX_DHCPV6_PACKET_SIZE).

- **NX_DHCPV6_TYPE_OF_SERVICE** Bu, UDP paket iletimi için hizmet türünü tanımlar. Varsayılan olarak, bu değer NX_IP_NORMAL.

- **NX_DHCPV6_FRAGMENT_OPTION** Bu, sunucu yuvası parçalama seçeneğini tanımlar. Varsayılan değer NX_DON ' T_FRAGMENT

- **NX_DHCPV6_TIME_TO_LIVE** Paketler atılmadan önce sunucudan DHCPv6 paketlerinin DHCPv6 paketlerinin ' atlama ' geçişi olabileceği yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır.

- **NX_DHCPV6_QUEUE_DEPTH** NetX Duo paketleri atmadan önce sunucu UDP yuvası alma kuyruğunda tutulacak paket sayısını belirtir.