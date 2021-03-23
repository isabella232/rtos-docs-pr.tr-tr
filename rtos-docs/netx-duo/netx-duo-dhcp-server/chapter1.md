---
title: Bölüm 1-Azure RTOS NetX Duo DHCP sunucusuna giriş
description: NetX Duo sürümünde, uygulamanın IP adresi *nx_ip_create* hizmet çağrısına sağlanan parametrelerden biridir.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 678b9ed77f07d0b526525c740f0fae7adc6d2c95
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826116"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcp-server"></a>Bölüm 1-Azure RTOS NetX Duo DHCP sunucusuna giriş

NetX Duo sürümünde, uygulamanın IP adresi *nx_ip_create* hizmet çağrısına sağlanan parametrelerden biridir. IP adresi, statik olarak veya Kullanıcı Yapılandırması aracılığıyla uygulama tarafından biliniyorsa, IP adresi sağlamak sorun vermez. Ancak, uygulamanın IP adresinin ne olduğunu bilmediğini veya ilgilenmediğini bir örnek vardır. Bu gibi durumlarda, *nx_ip_create* işlevine sıfır bir IP adresi verilmelidir ve uygulama, dinamik olarak istek ve bir IP adresi almak için DHCP sunucusuyla iletişim kurar.

## <a name="dynamic-ip-address-assignment"></a>Dinamik IP adresi ataması

Ağdan dinamik bir IP adresi elde etmek için kullanılan temel hizmet, ters adres çözümleme protokolüdür (RARP). Bu protokol ARP ile benzerdir, ancak başka bir ağ düğümünün MAC adresini bulmak yerine kendisi için bir IP adresi almak üzere tasarlanmıştır. Düşük düzey RARP iletisi yerel ağda yayınlanır ve ağ üzerindeki bir sunucunun, dinamik olarak ayrılan IP adresi içeren bir RARP yanıtıyla yanıt vermesi için bir sorumluluğudur.

RARP, IP adreslerinin dinamik ayırması için bir hizmet sunmakla birlikte, birkaç eksiklikleri vardır. En çok kullanılan eksiklik, RARP 'nin yalnızca IP adresinin dinamik olarak ayrılmasını sağlar. Çoğu durumda, bir cihazın ağa doğru bir şekilde katılması için daha fazla bilgi gereklidir. Bir IP adresine ek olarak, çoğu cihaz ağ maskesine ve ağ geçidi IP adresine ihtiyaç duyar. Bir DNS sunucusunun IP adresi ve diğer ağ bilgileri de gerekli olabilir. RARP 'nin bu bilgileri sağlama yeteneği yoktur.

## <a name="rarp-alternatives"></a>RARP alternatifleri

RARP 'nin eksiklikleri aşılabilmesi için, araştırmacılar Önyükleme Protokolü (BOOTP) adlı daha kapsamlı bir IP adresi ayırma mekanizması geliştirmiştir. Bu protokol, IP adresi dinamik olarak tahsis etme ve ayrıca ek önemli ağ bilgileri sağlama yeteneğine sahiptir. Ancak, BOOTP 'nin statik ağ yapılandırmalarına yönelik olarak tasarlanma dezavantajı vardır. Hızlı veya otomatik adres atamaya izin vermez.

Dinamik ana bilgisayar Yapılandırma Protokolü (DHCP) son derece yararlı olacaktır. DHCP, belirli bir süre boyunca istemciye bir IP adresi "kiralamaya" kadar, tam otomatik IP sunucusu ayırması ve tamamen dinamik IP adresi ayırmayı içerecek şekilde, BOOTP 'nin temel işlevlerini genişletmek için tasarlanmıştır. DHCP, IP adreslerini BOOTP gibi statik bir şekilde ayırmak üzere de yapılandırılabilir.

## <a name="dhcp-messages"></a>DHCP Iletileri

DHCP, BOOTP işlevselliğini önemli ölçüde iyileştirse de DHCP, BOOTP ile aynı ileti biçimini kullanır ve BOOTP ile aynı satıcı seçeneklerini destekler. DHCP, işlevini gerçekleştirmek için aşağıdaki şekilde DHCP 'ye özgü yedi seçenek sunar:

- BUL (1) (DHCP Istemcisi tarafından gönderilen)
- TEKLIF (2) (DHCP sunucusu tarafından gönderilen)
- Istek (3) (DHCP Istemcisi tarafından gönderilen)
- Reddet (4) (DHCP Istemcisi tarafından gönderilen)
- ACK (5) (DHCP sunucusu tarafından gönderilen)
- NACK (6) (DHCP sunucusu tarafından gönderilen)
- Yayın (7) (DHCP Istemcisi tarafından gönderilen)
- BILDIR (8) (DHCP Istemcisi tarafından gönderilir)
- FORCERENEW (9) (DHCP Istemcisi tarafından gönderilen)

## <a name="dhcp-communication"></a>DHCP Iletişimi

DHCP sunucusu, DHCP Istemci isteklerini almak ve yanıtları iletmek için UDP protokolünü kullanır. IP adresine sahip olmadan önce, DHCP bilgilerini taşıyan UDP iletileri, 255.255.255.255 IP yayını adresi kullanılarak gönderilir ve alınır. Ancak, Istemci DHCP sunucusunun adresini biliyorsa, tek noktaya yayın iletilerini kullanarak DHCP iletileri gönderebilir.

## <a name="dhcp-server-state-machine"></a>DHCP sunucusu durum makinesi

DHCP sunucusu, *nx_dhcp_server_create* işleme sırasında oluşturulan BIR iç DHCP iş parçacığı tarafından işlenen iki adımlı bir durum makinesi olarak uygulanır. DHCP sunucusunun ana durumları 1) bir DHCP istemcisinden bulma iletisi alıyor ve 2) Istek iletisi alıyor.

Aşağıda karşılık gelen DHCP Istemci durumları verilmiştir:

- **NX_DHCP_STATE_BOOT** Önceki bir IP adresi ile başlama
- **NX_DHCP_STATE_INIT** Önceki IP adresi değeri olmadan başlatılıyor
- **NX_DHCP_STATE_SELECTING** Herhangi bir DHCP sunucusundan yanıt bekleniyor
- **NX_DHCP_STATE_REQUESTING** DHCP sunucusu tanımlandı, IP adresi isteği gönderildi
- **NX_DHCP_STATE_BOUND** DHCP IP adresi kirası oluşturuldu
- **NX_DHCP_STATE_RENEWING** DHCP IP adresi kira yenileme süresi geçti, yenileme istendi
- **NX_DHCP_STATE_REBINDING** DHCP IP adresi kira yeniden bağlama süresi geçti, yenileme istendi
- **NX_DHCP_STATE_FORCERENEW** DHCP IP adresi kirası oluşturuldu, sunucu veya uygulamaya göre yenilemeyi zorla
- **NX_DHCP_STATE_FAILED** Sunucu bulunamadı veya sunucudan yanıt alınmadı

## <a name="dhcp-additional-parameters"></a>DHCP ek parametreleri

NetX Duo DHCP sunucusu, DHCP Istemcisi için ortak/kritik ağ yapılandırma parametreleri (örneğin, yönlendirici veya ağ geçidi adresi ve DNS sunucusu) ile DHCP Istemcileri sağlamak üzere *nxd_dhcp_server. h* içindeki yapılandırılabilir NX_DHCP_DEFAULT_SERVER_OPTION_LIST seçeneğinde ayarlanan varsayılan bir seçenek parametreleri listesine sahiptir.

## <a name="dhcp-rfcs"></a>DHCP RFC 'Leri

NetX Duo DHCP sunucusu RFC2132, RFC2131 ve ilgili RFC 'lerle uyumludur.
