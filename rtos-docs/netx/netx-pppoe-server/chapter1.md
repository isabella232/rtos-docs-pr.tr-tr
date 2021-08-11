---
title: Bölüm 1 - NetX PPPoE Sunucusu Azure RTOS ya giriş
description: Bu belge, NetX PPPoE Azure RTOS ayrıntılarına odaklanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2f79cba35991555f7f8d10e589aa251387ce25c48c3b729da371b548f13321bd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798336"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-server"></a>Bölüm 1 - NetX PPPoE Sunucusu Azure RTOS ya giriş

Ethernet üzerinden PPP (PPPoE), konakların geleneksel karakter tabanlı seri hat iletişimi yerine Ethernet üzerinden PPP sunucusuna bağlanmasına olanak sağlar. PPPoE'nin teknik ayrıntıları RFC 2516: Ethernet üzerinden PPP İletim yöntemi (PPPoE) konusunda açıklanmıştır. Bu belge, NetX PPPoE Azure RTOS ayrıntılarına odaklanır.

Ethernet üzerinden noktadan noktaya bağlantı sağlamak için her PPP oturumunun uzak eşlenin Ethernet adresini öğrenmesi ve benzersiz bir oturum tanımlayıcısı kurması gerekir.

RFC 2516'ya göre PPPoE iki aşamadan oluşur: Bulma aşaması ve PPPoE Oturumu aşaması. Bir konak (istemci) PPP oturumu başlatmak isterse, PPPoE sunucusunu bulmak için önce Bulma işlemini gerçekleştirmesi gerekir. Bu adım ayrıca sunucunun ve istemcinin ppP oturumunun geri kalanı için kullanılacak ethernet MAC adresini ve SESSION_ID adresini tanımlaması için de izin verir.

Ethernet çerçevesi aşağıdaki gibidir:

![Ethernet çerçevesini gösteren diyagram.](media/netx-pppoe-server-01.png)

PPPoE için Ethernet yükü aşağıdaki gibidir:

![PPPoE için Ethernet yükünü gösteren diyagram.](media/netx-pppoe-server-02.png)

## <a name="pppoe-discovery-stage"></a>PPPoE Bulma Aşaması

PPPoE Bulma aşaması, istemcilerin, PPP çerçeveleri alışverişten önce etkili bir şekilde oturum oluşturmak için ağ üzerinde kullanılabilir tüm sunuculardan bir sunucu seçmelerine olanak sağlar. Bulma aşamasının sonunda, hem istemci hem de sunucu benzersiz bir oturum kimliği üzerinde anlaşmalı ve her iki tarafın da eş mac adresini biliyor olması gerekir.

| Bulma İletisi                                  | Kod | Yön                                     |
| -------------------------------------------------- | ---- | --------------------------------------------- |
| PPPoE Etkin Bulma Başlatı (PADI)           | 0x09 | İstemciden yayına                      |
| PPPoE Etkin Bulma Teklifi (PADO)                | 0x07 | Sunucudan İstemciye                         |
| PPPoE Etkin Bulma İsteği (PADR)              | 0x19 | İstemciden Sunucuya                         |
| PPPOE Etkin Bulma Oturum Onayı (PADS) | 0x65 | Sunucudan İstemciye                         |
| PPPoE Etkin Bulma Sonlandırma (PADT)            | 0xa7 | Sunucudan veya istemciden başlatabilirsiniz |

Tüm Bulma Ethernet çerçeveleri, ETHER_TYPE alanı varsayılan değere 0x8863.

## <a name="pppoe-session-message"></a>PPPoE Oturum İletisi

İstemci ve sunucu bir oturum oluşturdukta PPP çerçeveleri PPPoE Oturumu iletileri olarak aktarabilirsiniz. Oturum sırasında, SESSION_ID ve Bulma aşamasında atanan sunucunun değeri olması gerekir.

Tüm PPPoE Oturumu Ethernet çerçeveleri, ETHER_TYPE alanı varsayılan değere 0x8864.