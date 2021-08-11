---
title: Bölüm 1-Azure RTOS NetX Duo mDNS/DNS-SD 'ye giriş
description: Azure RTOS NetX Duo mDNS/DNS-SD geleneksel DNS hizmetini genişletmektedir.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7cde8e81809dcc74ee5d0b09d8e7a8d2ae96850cd84250a5bf003fdd5763925a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796455"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mdnsdns-sd"></a>Bölüm 1-Azure RTOS NetX Duo mDNS/DNS-SD 'ye giriş

MDNS ve DNS-SD, geleneksel DNS hizmetini artırmak için tasarlanan protokollerdir. mDNS, yerel ağdaki düğümlere konak adı ve hizmet araması sağlar. Her düğüm, komşuları için sunduğu Hizmetleri duyurmak, komşularından sorgulara yanıt vermek ve uygulama uygulamalarında sorgu göndermesi için IPv4 veya IPv6 çok noktaya yayın kanalını kullanır. Tasarım gereği, mDNS dağıtılmış bir ortamda çalışır ve bu sayede merkezi bir hizmeti ortadan kaldırır.

DNS-SD, mDNS 'in üzerine kurulmuştur. DNS-SD, düğümlerin yerel ağa sağladıkları Hizmetleri bildirmesini veya yerel ağdaki diğer düğümler tarafından sunulan hizmetleri keşfetmesini sağlar. Belge boyunca *MDNs* terimi hem MDNs belirtimini hem de DNS-SD belirtimini kapsayan Hizmetleri ifade eder.

## <a name="mdns-standard"></a>mDNS standardı

NetX Duo mDNS/DNS-SD uygulamasının aşağıdaki RFC 'Lerle uyumlu olması:

- RFC 6762: mDNS belirtimi
- RFC 6763: DNS-SD belirtimi