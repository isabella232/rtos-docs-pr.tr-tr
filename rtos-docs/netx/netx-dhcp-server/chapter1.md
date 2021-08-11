---
title: Bölüm 1 - NetX DHCP Azure RTOS'ne giriş
description: Uygulama, dinamik olarak istekte Azure RTOS ip adresi almak için net netx DHCP sunucusuyla iletişim oluşturur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f7a286118caf9bca9876d40ecdd176a3f4cb711e9cba39325808bfb6c09c2644
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799566"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-dhcp-server"></a>Bölüm 1 - NetX DHCP Azure RTOS'ne giriş

NetX'te uygulamanın IP adresi, nx_ip_create hizmeti çağrısı *için sağlanan parametrelerden* birisidir. IP adresinin uygulama tarafından statik olarak veya kullanıcı yapılandırması aracılığıyla bilindiği için IP adresini sağlamak sorun oluşturmaz. Ancak, uygulamanın IP adresinin ne olduğunu bilmiyor veya önemser olduğu bazı örnekler vardır. Böyle durumlarda, *nx_ip_create* işlevine sıfır BIR IP adresi sağlanmalıdır ve uygulama dinamik olarak bir IP adresi isteğinde Azure RTOS ve almak için Azure RTOS NetX DHCP sunucusuyla iletişim kuracak.

## <a name="dynamic-ip-address-assignment"></a>Dinamik IP Adresi Ataması

Ağdan dinamik IP adresi almak için kullanılan temel hizmet, Ters Adres Çözümleme Protokolü'dür (RARP). Bu protokol ARP'ye benzer, ancak başka bir ağ düğümü için MAC adresini bulmak yerine kendisi için bir IP adresi almak üzere tasarlanmıştır. Alt düzey RARP iletisi yerel ağ üzerinde yayındır ve ağ üzerinde dinamik olarak ayrılmış bir IP adresi içeren bir RARP yanıtıyla yanıt vermek bir sunucunun sorumluluğundadır.

RARP, IP adreslerinin dinamik olarak ayırması için bir hizmet sağlar ancak birçok farklı eksiklik vardır. En önemli eksiklik, RARP'nin yalnızca IP adresinin dinamik ayırmayı sağladığıdır. Çoğu durumda, cihazın ağa düzgün bir şekilde katılması için daha fazla bilgi gereklidir. Bir IP adresine ek olarak, çoğu cihaz için ağ maskesi ve ağ geçidi IP adresi gerekir. Dns sunucusunun IP adresi ve diğer ağ bilgileri de gerekli olabilir. RARP'nin bu bilgileri sağlayabilme özelliği yok.

## <a name="rarp-alternatives"></a>RARP Alternatifleri

Araştırmacılar, RARP'nin eksikliklerini aşmak için Bootstrap Protokolü (BOOTP) adlı daha kapsamlı bir IP adresi ayırma mekanizması geliştirmiştir. Bu protokol dinamik olarak bir IP adresi ayırabilmenin yanı sıra ek önemli ağ bilgileri de sağlar. Ancak BOOTP, statik ağ yapılandırmaları için tasarlanma dezavantajı sunar. Hızlı veya otomatik adres atamasına izin vermez.

Burada Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP) son derece yararlıdır. DHCP, BOOTP'in temel işlevselliğini, bir IP adresini belirli bir süre boyunca istemciye "kiralama" yoluyla tamamen otomatik IP sunucusu ayırmayı ve tamamen dinamik IP adresi ayırmayı içerecek şekilde genişletmek için tasarlanmıştır. DHCP, IP adreslerini BOOTP gibi statik bir şekilde ayıracak şekilde de yalıtabilirsiniz.

## <a name="dhcp-messages"></a>DHCP İletileri

DHCP, BOOTP işlevselliğini büyük ölçüde geliştirse de, DHCP BOOTP ile aynı ileti biçimini kullanır ve BOOTP ile aynı satıcı seçeneklerini destekler. DHCP, işlevini gerçekleştirmek için aşağıdaki gibi yedi yeni DHCP'ye özgü seçenek sunar:

| Seçenek     | Değer | Kaynak                |
| ---------- | ----- | --------------------- |
| Keşfetmek   | (1)   | (DHCP İstemcisi tarafından gönderilir) |
| Teklif      | (2)   | (DHCP Sunucusu tarafından gönderilir) |
| Istek    | (3)   | (DHCP İstemcisi tarafından gönderilir) |
| Düşüş    | (4)   | (DHCP İstemcisi tarafından gönderilir) |
| Ack        | (5)   | (DHCP Sunucusu tarafından gönderilir) |
| Nack       | (6)   | (DHCP Sunucusu tarafından gönderilir) |
| Sürüm    | (7)   | (DHCP İstemcisi tarafından gönderilir) |
| Bilgilendir     | (8)   | (DHCP İstemcisi tarafından gönderilir) |
| FORCERENEW | (9)   | (DHCP İstemcisi tarafından gönderilir) |

## <a name="dhcp-communication"></a>DHCP İletişimi

DHCP Sunucusu, DHCP İstemcisi isteklerini almak ve yanıtları iletmek için UDP protokolünü kullanır. BIR IP adresine sahip olmadan önce, DHCP bilgilerini taşıyan UDP iletileri 255.255.255.255.255 IP yayın adresi kullanılarak gönderilir ve alınmıştır. Ancak, İstemci DHCP Sunucusunun adresini biliyorsa, tek noktaya yayın iletileri kullanarak DHCP iletileri gönderebilir.

## <a name="dhcp-server-state-machine"></a>DHCP Sunucusu Durum Makinesi

DHCP Sunucusu, işlenme sırasında oluşturulan bir iç DHCP iş parçacığı tarafından işlenen iki adımlı bir *durum nx_dhcp_server_create* uygulanır. DHCP Sunucusunun ana durumları 1) DHCP istemciden DISCOVER iletisi alır ve 2) request iletisi alır.

İlgili DHCP İstemcisi durumları aşağıda verilmiştir:

- **NX_DHCP_STATE_BOOT:** Önceki bir IP adresiyle başlayarak
- **NX_DHCP_STATE_INIT:** Önceki IP adresi değeriyle başlayarak
- **NX_DHCP_STATE_SELECTING:** Herhangi bir DHCP sunucusundan yanıt bekliyor
- **NX_DHCP_STATE_REQUESTING:** DHCP Sunucusu tanımlandı, IP adresi isteği gönderildi
- **NX_DHCP_STATE_BOUND:** DHCP IP Adresi kirası kuruldu
- **NX_DHCP_STATE_RENEWING:** DHCP IP Adresi kira yenileme süresi sona erdi, yenileme isteği
- **NX_DHCP_STATE_REBINDING:** DHCP IP Adresi kirası yeniden bağlantı süresi sona erdi, yenileme isteği
- **NX_DHCP_STATE_FORCERENEW:** DHCP IP Adresi kirası kuruldu, sunucu veya uygulama tarafından yenilemeye zorlama
- **NX_DHCP_STATE_FAILED:** Sunucu bulunamadı veya sunucudan yanıt alınamadı

## <a name="dhcp-additional-parameters"></a>DHCP Ek Parametreleri

NetX DHCP Sunucusu, DHCP İstemcisi için yönlendirici veya ağ geçidi adresi ve DNS sunucusu gibi genel/kritik ağ yapılandırma parametreleriyle DHCP İstemcilerine sağlamak için NX_DHCP_DEFAULT_SERVER_OPTION_LISTin *nx_dhcp_server.h* yapılandırılabilir seçeneğinde ayarlanmış varsayılan seçenek parametreleri listesine sahip olur.

## <a name="dhcp-rfcs"></a>DHCP RFC'leri

NetX DHCP Sunucusu RFC2132, RFC2131 ve ilgili RFC'ler ile uyumludur.
