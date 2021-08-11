---
title: Bölüm 1-Azure RTOS NetX DHCP Istemcisine giriş
description: NetX 'te, uygulamanın IP adresi nx_ip_create hizmet çağrısına sağlanan parametrelerden biridir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 54853fd3677b8d60b7fbe1445ca67c7e7a4a6e832683f65cbfca86158cb7fbd3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788822"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-dhcp-client"></a>Bölüm 1-Azure RTOS NetX DHCP Istemcisine giriş

NetX 'te, uygulamanın IP adresi *nx_ip_create* hizmet çağrısına sağlanan parametrelerden biridir. IP adresi, statik olarak veya Kullanıcı Yapılandırması aracılığıyla uygulama tarafından biliniyorsa, IP adresi sağlamak sorun vermez. Ancak, uygulamanın IP adresinin ne olduğunu bilmediğini veya ilgilenmediğini bir örnek vardır. Bu gibi durumlarda, *nx_ip_create* işlevine sıfır bir IP adresi verilmelidir ve Azure RTOS DHCP istemci protokolü, dinamik olarak bir IP adresi elde etmek için kullanılmalıdır.

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

DHCP, istek ve alan yanıtlarını göndermek için UDP protokolünü kullanır. IP adresine sahip olmadan önce, DHCP bilgilerini taşıyan UDP iletileri, 255.255.255.255 IP yayını adresi kullanılarak gönderilir ve alınır.

## <a name="dhcp-client-state-machine"></a>DHCP Istemci durumu makinesi

DHCP Istemcisi, bir durum makinesi olarak uygulanır. Durum makinesi, *nx_dhcp_create* işleme sırasında oluşturulan BIR iç DHCP iş parçacığı tarafından işlenir. DHCP Istemcisinin ana durumları şunlardır:


- **NX_DHCP_STATE_BOOT** Önceki bir IP adresi ile başlama

- **NX_DHCP_STATE_INIT** Önceki IP adresi değeri olmadan başlatılıyor

- **NX_DHCP_STATE_SELECTING** Herhangi bir DHCP sunucusundan yanıt bekleniyor

- **NX_DHCP_STATE_REQUESTING** DHCP sunucusu tanımlandı, IP adresi isteği gönderildi

- **NX_DHCP_STATE_BOUND** DHCP IP adresi kirası oluşturuldu

- **NX_DHCP_STATE_RENEWING** DHCP IP adresi kira yenileme süresi geçti, yenileme istendi

- **NX_DHCP_STATE_REBINDING** DHCP IP adresi kira yeniden bağlama süresi geçti, yenileme istendi

- **NX_DHCP_STATE_FORCERENEW** DHCP IP adresi kirası oluşturuldu, sunucu tarafından yenilemeyi zorla (Şu anda desteklenmiyor) veya çağıran uygulama tarafından nx_dhcp_force_renew

- **NX_DHCP_STATE_ADDRESS_PROBING** DHCP IP adresi yoklama, IP adresi çakışmasını algılamak için ARP araştırması gönderin.

## <a name="dhcp-client-multiple-interface-support"></a>DHCP Istemcisi birden çok arabirim desteği

DHCP Istemcisi daha önce yalnızca tek bir ağ arabiriminde çalışmak üzere uygulandı. DHCP Istemcisinin birincil arabirimde çalışması için varsayılan davranış (ve yine de aynıdır). *Nx_dhcp_set_interface_index* çağırarak, uygulama birincil arabirim yerine ikincil bir ağ arabiriminde DHCP çalıştırabilir (ve yine de olabilir).

Artık paralel olarak birden çok arabirimde çalışan DHCP 'yi desteklemektedir. DHCP Istemcisini birden fazla fiziksel arabirimde aynı anda çalıştırma hakkında ayrıntılı bilgi için, aynı anda **birden fazla arabirimde DHCP istemcisi** ' ne bakın.

## <a name="dhcp-user-request"></a>DHCP Kullanıcı Isteği

DHCP sunucusu bir IP adresi verdiğinde, DHCP istemci işlemesi, *nx_dhcp_user_option_request* hizmetini kullanarak ek parametreler isteyebilir (tek seferde).

## <a name="dhcp-client-socket-queue"></a>DHCP Istemci yuva kuyruğu 

DHCP Istemcisi, sunucunun kendisine yanıt vermesini beklerken, diğer DHCP Istemcilerine yönelik DHCP sunucularından gelen yayın paketlerini otomatik olarak kendi yuva alma sırasından temizler. Meşgul bir ağda, Bunun gerçekleşmemesi, Istemci için amaçlanan paketlerin bırakılmasına neden olabilir.

## <a name="dhcp-rfcs"></a>DHCP RFC 'Leri

NetX DHCP, RFC2132, RFC2131 ve ilgili RFC 'lerle uyumludur.

