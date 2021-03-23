---
title: Bölüm 1-Azure RTOS NetX PPPoE sunucusuna giriş
description: Bu belge, Azure RTOS NetX PPPoE modülünün ayrıntılarına odaklanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 85a762f669e31c7e753f78b270ced15677a87c4c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826609"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-server"></a>Bölüm 1-Azure RTOS NetX PPPoE sunucusuna giriş

Ethernet üzerinden PPP (PPPoE), ana bilgisayarların geleneksel karakter tabanlı seri hat iletişimi yerine Ethernet aracılığıyla PPP sunucusuna bağlanmasına olanak sağlar. PPPoE teknik ayrıntıları, RFC 2516: Ethernet üzerinden PPP (PPPoE) Iletmek için bir yöntem olarak açıklanmaktadır. Bu belge, Azure RTOS NetX PPPoE modülünün ayrıntılarına odaklanır.

Ethernet üzerinden noktadan noktaya bağlantı sağlamak için her PPP oturumunun, uzak eşin Ethernet adresini öğrenmeli ve benzersiz bir oturum tanımlayıcısı kurması gerekir.

RFC 2516 ' e göre, PPPoE iki aşamadan oluşur: bulma aşaması ve PPPoE oturum aşaması. Bir ana bilgisayar (istemci) bir PPP oturumu başlatmak isterse, önce PPPoE sunucusunu bulmak için bulma işlemini gerçekleştirmelidir. Bu adım Ayrıca, sunucunun ve istemcinin diğer Ethernet MAC adreslerini ve SESSION_ID belirlemesine izin verir ve bu da PPP oturumunun geri kalanı için kullanılacaktır.

Ethernet çerçevesi aşağıdaki gibidir:

![Bir Ethernet çerçevesini gösteren diyagram.](media/netx-pppoe-server-01.png)

PPPoE için Ethernet yükü aşağıdaki gibidir:

![PPPoE için bir Ethernet yükü gösteren diyagram.](media/netx-pppoe-server-02.png)

## <a name="pppoe-discovery-stage"></a>PPPoE bulma aşaması

PPPoE bulma aşaması, istemcilerin, değiştirilen PPP çerçevelerinden önce bir oturum oluşturmak için ağ üzerindeki tüm kullanılabilir sunuculardan bir sunucu seçmesine olanak sağlar. Keşif aşamasının sonunda, hem istemci hem de sunucu benzersiz bir oturum KIMLIĞI üzerinde anlaşacaktır ve her iki taraf da eşin MAC adresini bilmelidir.

| Bulma Iletisi                                  | Kod | Yön                                     |
| -------------------------------------------------- | ---- | --------------------------------------------- |
| PPPoE etkin bulma başlatma (PADı)           | 0x09 | Istemciden yayına                      |
| PPPoE etkin bulma teklifi (PADO)                | 0x07 | Sunucudan Istemciye                         |
| PPPoE etkin bulma Isteği (PADR)              | 0x19 | Istemciden sunucuya                         |
| PPPOE etkin bulma oturumu-onay (Pad) | 0x65 | Sunucudan Istemciye                         |
| PPPoE etkin bulma sona erdir (TıT)            | 0xa7 | , Sunucu veya istemciden başlatılabilir |

Tüm bulma Ethernet çerçevelerinin ETHER_TYPE alanı 0x8863 değerine ayarlanır.

## <a name="pppoe-session-message"></a>PPPoE oturum Iletisi

İstemci ve sunucu bir oturum oluşturduktan sonra, PPP çerçeveleri, PPPoE oturum iletileri olarak aktarılabilir. Bir oturum sırasında, SESSION_ID değişmemelidir ve bulma aşamasında sunucunun atandığı değer olmalıdır.

Tüm PPPoE oturum Ethernet çerçevelerinin ETHER_TYPE alanı 0x8864 değerine ayarlanır.