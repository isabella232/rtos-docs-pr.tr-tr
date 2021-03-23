---
title: Ek B-Azure RTOS NetX Duo DHCPv6 sunucusu durum kodları
description: Bu bölümde tüm NetX Duo DHCPv6 sunucusu durum kodlarının açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7c79a0c0bc9acfcfca69c7333d30cd7cab35ba5f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826057"
---
# <a name="appendix-b---azure-rtos-netx-duo-dhcpv6-server-status-codes"></a>Ek B-Azure RTOS NetX Duo DHCPv6 sunucusu durum kodları

| Name              | Kod            | Açıklama |
| ------------------- | ------------------- | --------------- |
| Başarılı | 0 | Başarılı |
| Belirtilmeyen hata | 1 | Hata, neden belirtilmemiş; Bu durum kodu, Istemci isteğine diğer kodlarla eşleşmeyen genel bir hata olduğunu göstermek için sunucu tarafından ayarlanır |
| NoAddress kullanılabilir | 2 | Sunucu, Istemciye atanacak bir adrese sahip değil |
| NoBinding | 3 | İstemci IA adresi (bağlama) kullanılamıyor, örneğin, istenen IP adresi sunucunun kiralanmasını veya başka bir Istemciye atanabileceği için kullanılamıyor. |
| NotOnLink | 4 | Adresin ön eki, IP adresinin bir açık bağlantı adresi olmadığını belirtir |
| UseMulticast | 5 | *All_DHCP_Relay_Agents_and_Servers* çok noktaya yayın adresi yerine sunucunun tek noktaya yayın adresini kullanarak istemci iletisi almak için yanıt olarak bir sunucu tarafından gönderilir |