---
title: Bölüm 1 - NetX Duo DHCP Azure RTOS'ne giriş
description: NetX Duo'da uygulamanın IP adresi, nx_ip_create hizmeti *çağrısı için sağlanan parametrelerdendir.*
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a56f692059cbd3e2a72d64cf80ee90a917b80987add8130d3a1df70b3b0c3a71
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788482"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcp-server"></a>Bölüm 1 - NetX Duo DHCP Azure RTOS'a giriş

NetX Duo'da uygulamanın IP adresi, nx_ip_create hizmeti *çağrısı için sağlanan parametrelerdendir.* IP adresinin uygulama tarafından statik olarak veya kullanıcı yapılandırması aracılığıyla bilindiği için IP adresini sağlamak sorun oluşturmaz. Ancak, uygulamanın IP adresinin ne olduğunu bilmiyor veya önemser olduğu bazı örnekler vardır. Böyle durumlarda, nx_ip_create işlevine sıfır IP  adresi sağlanmalıdır ve uygulama dinamik olarak bir IP adresi talep etmek ve almak için DHCP sunucusuyla iletişim oluşturur.

## <a name="dynamic-ip-address-assignment"></a>Dinamik IP Adresi Ataması

Ağdan dinamik IP adresi almak için kullanılan temel hizmet, Ters Adres Çözümleme Protokolü'dür (RARP). Bu protokol ARP'ye benzer, ancak başka bir ağ düğümü için MAC adresini bulmak yerine kendisi için bir IP adresi almak üzere tasarlanmıştır. Alt düzey RARP iletisi yerel ağ üzerinde yayındır ve ağ üzerinde dinamik olarak ayrılmış bir IP adresi içeren bir RARP yanıtıyla yanıt vermek bir sunucunun sorumluluğundadır.

RARP, IP adreslerinin dinamik olarak ayırması için bir hizmet sağlar ancak birçok farklı eksiklik vardır. En önemli eksiklik, RARP'nin yalnızca IP adresinin dinamik ayırmayı sağladığıdır. Çoğu durumda, cihazın ağa düzgün bir şekilde katılması için daha fazla bilgi gereklidir. Bir IP adresine ek olarak, çoğu cihaz için ağ maskesi ve ağ geçidi IP adresi gerekir. Dns sunucusunun IP adresi ve diğer ağ bilgileri de gerekli olabilir. RARP'nin bu bilgileri sağlayabilme özelliği yok.

## <a name="rarp-alternatives"></a>RARP Alternatifleri

Araştırmacılar, RARP'nin eksikliklerini aşmak için Bootstrap Protokolü (BOOTP) adlı daha kapsamlı bir IP adresi ayırma mekanizması geliştirmiştir. Bu protokol dinamik olarak bir IP adresi ayırabilmenin yanı sıra ek önemli ağ bilgileri de sağlar. Ancak BOOTP, statik ağ yapılandırmaları için tasarlanma dezavantajı sunar. Hızlı veya otomatik adres atamasına izin vermez.

Burada Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP) son derece yararlıdır. DHCP, BOOTP'in temel işlevselliğini, bir IP adresini belirli bir süre boyunca istemciye "kiralama" yoluyla tamamen otomatik IP sunucusu ayırmayı ve tamamen dinamik IP adresi ayırmayı içerecek şekilde genişletmek için tasarlanmıştır. DHCP, IP adreslerini BOOTP gibi statik bir şekilde ayıracak şekilde de yalıtabilirsiniz.

## <a name="dhcp-messages"></a>DHCP İletileri

DHCP, BOOTP işlevselliğini büyük ölçüde geliştirse de, DHCP BOOTP ile aynı ileti biçimini kullanır ve BOOTP ile aynı satıcı seçeneklerini destekler. DHCP, işlevini gerçekleştirmek için aşağıdaki gibi yedi yeni DHCP'ye özgü seçenek sunar:

- DISCOVER (1) (DHCP İstemcisi tarafından gönderilir)
- OFFER (2) (DHCP Sunucusu tarafından gönderilir)
- REQUEST (3) (DHCP İstemcisi tarafından gönderilir)
- REDDİkLE (4) (DHCP İstemcisi tarafından gönderilir)
- ACK (5) (DHCP Sunucusu tarafından gönderilir)
- NACK (6) (DHCP Sunucusu tarafından gönderilir)
- YAYıN (7) (DHCP İstemcisi tarafından gönderilir)
- INFORM (8) (DHCP İstemcisi tarafından gönderilir)
- FORCERENEW (9) (DHCP İstemcisi tarafından gönderilir)

## <a name="dhcp-communication"></a>DHCP İletişimi

DHCP Sunucusu, DHCP İstemcisi isteklerini almak ve yanıtları iletmek için UDP protokolünü kullanır. BIR IP adresine sahip olmadan önce, DHCP bilgilerini taşıyan UDP iletileri 255.255.255.255.255 IP yayın adresi kullanılarak gönderilir ve alınmıştır. Ancak, İstemci DHCP Sunucusunun adresini biliyorsa, tek noktaya yayın iletileri kullanarak DHCP iletileri gönderebilir.

## <a name="dhcp-server-state-machine"></a>DHCP Sunucusu Durum Makinesi

DHCP Sunucusu, işlenme sırasında oluşturulan bir iç DHCP iş parçacığı tarafından işlenen iki adımlı bir *durum nx_dhcp_server_create* uygulanır. DHCP Sunucusunun ana durumları 1) DHCP istemciden DISCOVER iletisi alır ve 2) request iletisi alır.

İlgili DHCP İstemcisi durumları aşağıda verilmiştir:

- **NX_DHCP_STATE_BOOT** Önceki BIR IP adresiyle başlayarak
- **NX_DHCP_STATE_INIT** Önceki IP adresi değeriyle başlayarak
- **NX_DHCP_STATE_SELECTING** Herhangi bir DHCP sunucusundan yanıt bekleme
- **NX_DHCP_STATE_REQUESTING** DHCP Sunucusu tanımlandı, IP adresi isteği gönderildi
- **NX_DHCP_STATE_BOUND** DHCP IP Adresi kiralaması kuruldu
- **NX_DHCP_STATE_RENEWING** DHCP IP Adresi kira yenileme süresi sona erdi, yenileme isteği
- **NX_DHCP_STATE_REBINDING** DHCP IP Adresi kiralama yeniden bağlantı süresi sona erdi, yenileme isteği
- **NX_DHCP_STATE_FORCERENEW** DHCP IP Adresi kirası kuruldu, sunucu veya uygulama tarafından yenilemeye zorlandı
- **NX_DHCP_STATE_FAILED** Sunucu bulunamadı veya sunucudan yanıt alınamadı

## <a name="dhcp-additional-parameters"></a>DHCP Ek Parametreleri

NetX Duo DHCP Sunucusu, DHCP İstemcisi için yönlendirici veya ağ geçidi adresi ve DNS sunucusu gibi ortak/kritik ağ yapılandırma parametreleri sağlamak için *nxd_dhcp_server.h'de* NX_DHCP_DEFAULT_SERVER_OPTION_LIST'daki yapılandırılabilir seçenek parametrelerinde ayarlanmış varsayılan seçenek parametreleri listesine sahip.

## <a name="dhcp-rfcs"></a>DHCP RFC'leri

NetX Duo DHCP Sunucusu RFC2132, RFC2131 ve ilgili RFC'ler ile uyumludur.
