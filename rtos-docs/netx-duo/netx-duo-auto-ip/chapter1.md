---
title: Bölüm 1-Azure RTOS NetX Duo Oto-IP 'sine giriş
description: Otomatik IP protokolü, yerel bir ağ üzerinde IPv4 adreslerini dinamik olarak yapılandırmak için tasarlanan bir protokoldür. Azure RTOS NetX Duo Oto IP paketinin düzgün çalışması için bir NetX IP örneğinin zaten oluşturulmuş olması gerekir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 24fb514b71f7812266de23ec6d485dca9769a2bef491fc773a90f9945885f3df
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784912"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-autoip"></a>Bölüm 1-Azure RTOS NetX Duo Oto-IP 'sine giriş

Otomatik IP protokolü, yerel bir ağ üzerinde IPv4 adreslerini dinamik olarak yapılandırmak için tasarlanan bir protokoldür. Otomatikten otomatik IP adresi atama işlevini gerçekleştirmek için ARP yeteneklerini kullanan basit bir protokoldür. Oto, 169.254.1.0 ile 169.254.254.255 arasındaki adresleri ayırır.

## <a name="autoip-requirements"></a>Oto IP gereksinimleri

Azure RTOS NetX Duo Oto IP paketinin düzgün çalışması için bir NetX IP örneğinin zaten oluşturulmuş olması gerekir. Ayrıca, ARP aynı IP örneğinde etkinleştirilmelidir. NetX Oto IP paketinin daha fazla gereksinimi yoktur.

## <a name="autoip-constraints"></a>Oto IP kısıtlamaları

NetX Oto IP protokolü RFC3927 standart gereksinimlerini uygular. Ancak, aşağıdaki kısıtlamalar vardır:

1. NetX DHCP kullanılıyorsa, DHCP iş parçacığının hem NetX IP örneği iş parçacığından hem de Oto IP iş parçacığından daha yüksek bir önceliğe sahip oluşturulması gerekir.

1. NetX Oto, eski IP adreslerinin kullanılmaya devam etmesi için bir mekanizma sağlamaz.

1. IP adresi değiştiğinde, uygulama var olan herhangi bir TCP bağlantısını kapatmaktan ve yeni IP adresinde yeniden oluşturmaya sorumludur.

## <a name="autoip-protocol-implementation"></a>Oto IP protokol uygulamasını

NetX Oto IP Protokolü ilk olarak 169.254.1.0 ile 169.254.254.255 arasındaki Oto IP IPv4 adres aralığı içinde bir rastgele adres seçer. Alternatif olarak, uygulama bir başlangıç IP adresini ***nx_auto_ip_start*** işlevine vererek zorlayabilir. Bu, bir önceki çalıştırmada bir Oto IP adresinin başarıyla kullanıldığı durumlarda faydalıdır.

Bir Oto IP adresi seçildikten sonra NetX Oto, seçili adres için bir dizi ARP araştırmalarını gönderir. Bir ARP araştırması, gönderen adresi 0.0.0.0 olarak ayarlanmış bir ARP isteği iletisinden ve hedef adres istenen bir IP adresine ayarlı. Bu ARP araştırmalarının bir serisi gönderilir (gerçek sayı, tanımlama NX_AUTO_IP_PROBE_NUM tarafından belirlenir). Başka bir ağ düğümü bu araştırmasına yanıt verirse veya aynı adres için aynı araştırma gönderirse, Oto IP IPv4 adres aralığı içinde yeni bir Oto IP adresi rastgele seçilir ve araştırma işlemi yinelenir.

NX_AUTO_IP_PROBE_NUM araştırmaları herhangi bir yanıt olmadan gönderilirse, NetX Oto, seçili adres için bir dizi ARP duyuruları yayınlar. Bir ARP duyurusu, ARP iletisinde hem gönderen hem de hedef adresi olan bir ARP istek iletisinden, seçili Oto IP adresine ayarlanmış olarak oluşur. Tanımlama NX_AUTO_IP_ANNOUNCE_NUM karşılık gelen bir dizi ARP duyurusu iletisi gönderilir. Başka bir ağ düğümü bir bildirme iletisine yanıt verirse veya aynı adres için özdeş bir duyuru gönderirse, Oto IP IPv4 adres aralığı içinde yeni bir Oto IP adresi rastgele seçilir ve araştırma işlemi baştan başlar.

Araştırma ve duyuru algılanan herhangi bir çakışma olmadan tamamlandığında, seçilen Oto IP adresi geçerli kabul edilir ve ilişkili IP örneği bu adresle birlikte ayarlanır.

## <a name="autoip-address-change"></a>Oto IP adresi değişikliği

Daha önce bahsedildiği gibi, NetX Oto, başarılı araştırma ve duyuru işlemeden sonra IP örnek adresini değiştirir. Bu durum için izleme, önemli değildir. Ancak, daha sonra, Oto IP adresinin değiştirilmesini sağlamak mümkündür. Olası nedenler, gelecekteki Oto IP adresi çakışmalarını ve DHCP adres çözümlemesini de kapsar. Bu olası durumları düzgün bir şekilde işlemek için, uygulamanın herhangi bir IP adresi değişikliğini ve tümünü uyarmak üzere aşağıdaki NetX API 'sini kullanması gerekir:

```c
nx_ip_address_change_notify(NX_IP *ip_ptr,
            VOID (*ip_address_change_notify)(NX_IP *,VOID*),
            VOID *additional_info);
```

Sağlanan *ip_address_change_notify* Işlevindeki Işleme NETX yeniden BAŞLATıLMALıDıR veya DHCP 'nin IP adresini daha sonra çözümlediği takdirde devre dışı bırakmalıdır. Örnek işleme için lütfen *küçük örnek sistem* bölümüne bakın.

## <a name="autoip-rfcs"></a>Oto IP RFC 'Leri

NetX oto RFC3927 ve ilgili RFC 'Ler ile uyumludur.