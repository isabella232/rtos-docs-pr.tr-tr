---
title: Bölüm 3 - Azure RTOS NetX Duo DHCPv6 yapılandırma seçenekleri
description: NetX Duo DHCPv6'Azure RTOS çeşitli yapılandırma seçenekleri vardır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 129d1421215452448b1de4626fdeda530a5466bd63ed0c758676c3ad60f9d6fb
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782430"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-configuration-options"></a>Bölüm 3 - Azure RTOS NetX Duo DHCPv6 yapılandırma seçenekleri

NetX Duo DHCPv6'Azure RTOS çeşitli yapılandırma seçenekleri vardır. Aşağıdaki listede her biri ayrıntılı olarak açıklanmaktadır:  
  
  
- **NX_DHCPV6_THREAD_PRIORITY** İstemci iş parçacığının önceliği. Varsayılan olarak, bu değer İstemci iş parçacığının 2 önceliğini çalıştırarak belirtir.

- **NX_DHCPV6_MUTEX_WAIT** DHCPv6 İstemcisi mutex üzerinde özel bir kilit almak için zaman out seçeneği. Varsayılan değer, TX_WAIT_FOREVER.

- **NX_DHCPV6_TICKS_PER_SECOND** Saat işaretlerinin saniyelere oranı. Bu işlemciye bağımlıdır. Varsayılan değer 100’dür.

- **NX_DHCPV6_IP_LIFETIME_TIMER_INTERVAL**  IP yaşam süresi zamanlayıcının geçerli IP adresinin İstemciye atandığı sürenin uzunluğunu güncelleştirmesi için saniye olarak geçen zaman aralığı. Varsayılan olarak bu değer 1'tir.

- **NX_DHCPV6_SESSION_TIMER_INTERVAL**  Oturum zamanlayıcının, İstemcinin Sunucu ile iletişim kurarken oturumda olduğu sürenin uzunluğunu güncelleştirmesi için saniye olarak zaman aralığı. Varsayılan olarak bu değer 1'tir.

- **NX_DHCPV6_MAX_IA_ADDRESS** İstemci kaydına eklen en fazla IA adresi sayısı. Varsayılan değer 1’dir. 

- **NX_DHCPV6_NUM_DNS_SERVERS** İstemci kaydına depo için DNS sunucularının sayısı. Varsayılan değer 2'dir.

- **NX_DHCPV6_NUM_TIME_SERVERS** sunucuların istemci kaydında depolayacakları zaman sayısı. Varsayılan değer 1’dir.

- **NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE**  İstemcinin ağ etki alanı adını tutmak için İstemci kaydında arabelleğin boyutu. Varsayılan değer 30’dur.

- **NX_DHCPV6_TIME_ZONE_BUFFER_SIZE**  İstemcinin saat dilimini tutmak için İstemci kaydında arabelleğin boyutu. Varsayılan değer 10'dur.

- **NX_DHCPV6_MAX_MESSAGE_SIZE** Sunucu yanıtta seçenek durumu iletisi tutmak için İstemci kaydında arabelleğin boyutu. Varsayılan değer 100 bayttır.

- **NX_DHCPV6_PACKET_TIME_OUT** İstemci paket havuzundan bir paket için saniyeler içinde zaman aşımları. Varsayılan değer 3 saniyedir.

- **NX_DHCPV6_TYPE_OF_SERVICE** Bu, DHCPv6 İstemci yuvasından UDP paket iletimi için hizmet türünü tanımlar. Varsayılan değer olarak **NX_IP_NORMAL.**

- **NX_DHCPV6_TIME_TO_LIVE** Bir İstemci paketinin, paket atmadan önce bir ağ yönlendiricisi tarafından kaç kez iletildi? Varsayılan değer, 0x80.

- **NX_DHCPV6_QUEUE_DEPTH** NetX Duo paketleri atmadan önce İstemci UDP yuvası alma kuyruğunda tutılacak paket sayısını belirtir. Varsayılan değer 5'tir.

## <a name="dhcpv6-message-transmission"></a>DHCPv6 İleti İletimi

DHCPv6 ileti iletiminde parametreleri ayarlamak için bir dizi DHCPv6 İstemci seçeneği vardır. Bunlar: 

  - ilk zaman aşımı

  - ilk iletimde maksimum gecikme süresi

  - en fazla yeniden iletim zaman aşımı 

  - en fazla yeniden iletim sayısı 

  - sunucu yanıtını beklemek için en uzun süre

Bu parametreler DHCPv6 İstemci iletilerinin her biri için geçerlidir:

- Istemek

- Istek

- Yenilemek

- REBIND

- Sürüm

- Düşüş

- Onaylamak

- Bilgilendir

Aşağıda, bu yapılandırılabilir seçeneklerin ve bunların varsayılanlarının tam listesi ve ardından 

values:

```C
NX_DHCPV6_FIRST_SOL_MAX_DELAY                   (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_INIT_SOL_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_TIMEOUT        (120 *
                                                NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_COUNT          0
NX_DHCPV6_MAX_SOL_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_REQ_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_TIMEOUT        (30 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_COUNT          10
NX_DHCPV6_MAX_REQ_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_RENEW_TRANSMISSION_TIMEOUT       (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_TIMEOUT      (600*   
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_COUNT        0

NX_DHCPV6_INIT_REBIND_TRANSMISSION_TIMEOUT      (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_TIMEOUT     (600*  
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_COUNT       0 

NX_DHCPV6_INIT_RELEASE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_TIMEOUT    0 
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_DURATION   0

NX_DHCPV6_INIT_DECLINE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_TIMEOUT    0
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_DURATION   0
NX_DHCPV6_FIRST_CONFIRM_MAX_DELAY               (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_CONFIRM_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_TIMEOUT    (4*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_COUNT      0  
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_DURATION   10

NX_DHCPV6_FIRST_INFORM_MAX_DELAY                (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_INFORM_TRANSMISSION_TIMEOUT      (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_TIMEOUT     (120*   
                                                NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_COUNT       0 
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_DURATION    0
```

Yeniden iletim zaman aşımında sınır yok için ileti yeniden iletim sayısını 0 olarak ayarlayın. Bir DHCPv6 İstemcisi iletinin kaç kez yeniden aktarılacağı (yeniden denemeler) sayısıyla ilgili bir sınır yoktur, ileti yeniden iletim sayısını 0 olarak ayarlayın.

> [!NOTE]
> Zaman aşımı veya yeniden deneme sayısı uzunluğu ne olursa olsun, IPv6 adresi geçerli yaşam süresi dolduğunda, IP adresi tablosundan kaldırılır ve artık İstemci tarafından kullanılamaz. NetX Duo DHCPv6 İstemcisi otomatik olarak yeni bir IPv6 adresi isteği gönderen SOLICIT iletileri göndermeye başlar.