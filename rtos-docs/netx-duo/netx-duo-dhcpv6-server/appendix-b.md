---
title: Ek B - Azure RTOS NetX Duo DHCPv6 sunucu durum kodları
description: Bu bölümde tüm NetX Duo DHCPv6 sunucu durum kodlarının açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8b9795607c0fed80646ee01e36edf4ecd2aaadad7f0a023e6979e123b81e1660
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791796"
---
# <a name="appendix-b---azure-rtos-netx-duo-dhcpv6-server-status-codes"></a>Ek B - Azure RTOS NetX Duo DHCPv6 sunucu durum kodları

| Name              | Kod            | Description |
| ------------------- | ------------------- | --------------- |
| Başarılı | 0 | Başarılı |
| Belirtilmeyen Hata | 1 | Hata, neden belirtilmemiş; Bu durum kodu, İstemci isteğinin diğer kodlarla eşleşmesi durumunda genel bir hata olduğunu belirtmek için Sunucu tarafından ayarlanır |
| NoAddress Kullanılabilir | 2 | Sunucuda İstemciye atanan adres yok |
| NoBinding | 3 | İstemci IA adresi (bağlama) kullanılamıyor; örneğin istenen IP adresi, Sunucunun kiralanması veya başka bir İstemciye atanmada mevcut değildir. |
| NotOnLink | 4 | Adres ön eki, IP adresinin bağlantı adresi olmadığını gösterir |
| UseMulticast | 5 | Çok noktaya yayın adresi yerine Sunucunun tek noktaya yayın adresi kullanılarak İstemci iletisi almaya yanıt *olarak bir Sunucu All_DHCP_Relay_Agents_and_Servers* gönderilir |