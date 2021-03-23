---
title: Bölüm 3-Azure RTOS NetX Duo DHCPv6 yapılandırma seçenekleri
description: Azure RTOS NetX Duo DHCPv6 'yi oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e5396b1c04581b5f79d337462368c4718ba9bb16
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826087"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-configuration-options"></a>Bölüm 3-Azure RTOS NetX Duo DHCPv6 yapılandırma seçenekleri

Azure RTOS NetX Duo DHCPv6 'yi oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:  
  
  
- **NX_DHCPV6_THREAD_PRIORITY** Istemci iş parçacığının önceliği. Varsayılan olarak, bu değer Istemci iş parçacığının öncelik 2 ' de çalıştığını belirtir.

- **NX_DHCPV6_MUTEX_WAIT** DHCPv6 Istemci mutex 'i üzerinde özel bir kilit elde etmek için zaman aşımı seçeneği. Varsayılan değer TX_WAIT_FOREVER.

- **NX_DHCPV6_TICKS_PER_SECOND** Onay işareti sayısının saniyeye oranı. Bu, işlemciye bağımlıdır. Varsayılan değer 100’dür.

- **NX_DHCPV6_IP_LIFETIME_TIMER_INTERVAL**  Saniye cinsinden IP yaşam süresinin Istemciye geçerli IP adresinin atandığı sürenin uzunluğunu güncelleştiren zaman aralığı. Varsayılan olarak, bu değer 1 ' dir.

- **NX_DHCPV6_SESSION_TIMER_INTERVAL**  Saniye cinsinden oturum süreölçerinin, Istemcinin sunucu ile iletişim kurduğu süre uzunluğunu güncelleştirme süresini güncelleştiren zaman aralığı. Varsayılan olarak, bu değer 1 ' dir.

- **NX_DHCPV6_MAX_IA_ADDRESS** Istemci kaydına eklenebilecek en fazla IA adresi sayısı. Varsayılan değer 1’dir. 

- **NX_DHCPV6_NUM_DNS_SERVERS** İstemci kaydına depolanacak DNS sunucularının sayısı. Varsayılan değer 2 ' dir.

- **NX_DHCPV6_NUM_TIME_SERVERS** İstemci kaydına depolanacak zaman sunucularının sayısı. Varsayılan değer 1’dir.

- **NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE**  İstemcinin ağ etki alanı adını tutmak için Istemci kaydındaki arabelleğin boyutu. Varsayılan değer 30’dur.

- **NX_DHCPV6_TIME_ZONE_BUFFER_SIZE**  İstemcinin saat dilimini tutmak için Istemci kaydındaki arabelleğin boyutu. Varsayılan değer 10'dur.

- **NX_DHCPV6_MAX_MESSAGE_SIZE** Sunucu yanıtında durum iletisi seçeneğini tutmak için Istemci kaydındaki arabelleğin boyutu. Varsayılan değer 100 bayttır.

- **NX_DHCPV6_PACKET_TIME_OUT** Istemci paket havuzundan bir paket ayırmak için saniye cinsinden zaman aşımı. Varsayılan değer 3 saniyedir.

- **NX_DHCPV6_TYPE_OF_SERVICE** Bu, DHCPv6 Istemci yuvasından UDP paket iletimi için hizmet türünü tanımlar. Varsayılan değer **NX_IP_NORMAL**.

- **NX_DHCPV6_TIME_TO_LIVE** Paket atılmadan önce bir ağ yönlendiricisinin Istemci paketinin iletme sayısı. Varsayılan değer 0x80 ' dır.

- **NX_DHCPV6_QUEUE_DEPTH** NetX Duo paketleri atmadan önce Istemci UDP yuvası alma kuyruğunda tutulacak paket sayısını belirtir. Varsayılan değer 5 ' tir.

## <a name="dhcpv6-message-transmission"></a>DHCPv6 Ileti Iletimi

DHCPv6 ileti iletiminde parametreleri ayarlamak için DHCPv6 Istemci seçenekleri kümesi vardır. Bunlar: 

  - ilk zaman aşımı

  - ilk iletimde maksimum gecikme

  - maksimum yeniden iletim zaman aşımı 

  - maksimum yeniden iletim sayısı 

  - Sunucu yanıtı için beklenecek en uzun süre

Bu parametreler, DHCPv6 Istemci iletilerinin her biri için geçerlidir:

- Istek

- ISTEYEN

- YENILEY

- REBIND

- Yayın

- Reddet

- GÖRÜNDÜĞÜNÜ

- YAPıLANDıRı

Aşağıda, bu yapılandırılabilir seçeneklerin ve bunların varsayılan listesi verilmiştir 

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

Yeniden aktarım zaman aşımında sınır olmaması için ileti yeniden aktarım sayısını 0 olarak ayarlayın. DHCPv6 Istemci iletisinin kaç kez yeniden denendiğinden (yeniden denemeler), ileti yeniden aktarım sayısını 0 olarak ayarlayın.

> [!NOTE]
> Zaman aşımı süresi veya yeniden deneme sayısı ne olursa olsun, geçerli bir IPv6 adresi yaşam süresi dolduğunda, IP Adresi tablosundan kaldırılır ve artık Istemci tarafından kullanılamaz. NetX Duo DHCPv6 Istemcisi, yeni bir IPv6 adresi isteyen Istem iletilerini otomatik olarak göndermeye başlayacaktır.