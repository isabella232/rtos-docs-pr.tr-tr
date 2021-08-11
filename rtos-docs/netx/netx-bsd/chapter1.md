---
title: Bölüm 1 - NetX BSD Azure RTOS ye giriş
description: NetX Azure RTOS API'si Derleme Sarmalayıcı, bazı sınırlamalarla temel BSD Yuvaları API çağrılarını destekler ve altında NetX temelleri kullanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b58283a38a25ffdd438d7853999f3b6e390f280a947aa45101d8df86447bf3dd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796755"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-bsd"></a>Bölüm 1 - NetX BSD Azure RTOS ye giriş

NetX BSD Yuvaları API'si Derleme Sarmalayıcı, bazı sınırlamalarla temel BSD YuvaLARı API çağrılarını destekler ve altında NetX temelleri kullanır. Bu Sarmalayıcı iç NetX temellerini kullanır ve temel NetX hata denetimlerini atlar. Bu BSD Yuvaları API'si uyumluluk katmanı, tipik BSD uygulamalarına göre daha hızlı veya biraz daha hızlı çalışmalı.

## <a name="bsd-sockets-api-compliancy-wrapper-source"></a>BSD Yuva API'si Derleme Sarmalayıcı Kaynağı

BSD Sarmalayıcı kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur: *nx_bsd.h* ve *nx_bsd.c*. *nx_bsd.h* dosyası tüm gerekli BSD Yuvaları API Sarmalayıcı sabitlerini ve alt yol prototiplerini *tanımlarken, nx_bsd.c* gerçek BSD Yuvaları API uyumluluk kaynak kodunu içerir. Bu BSD Sarmalayıcı kaynak dosyaları tüm NetX destek paketleri için ortaktır.

Paket şunları içerir:

- **nx_bsd.c:** Sarmalayıcı kaynak kodu
- **nx_bsd.h:** Ana üst bilgi dosyası

Örnek tanıtım programları:

- **bsd_demo_tcp.c:** Tek *bir TCP sunucusu ve istemcisi ile tanıtım*
- **bsd_demo_udp.c:** İki *UDP istemci ve bir UDP sunucusu ile tanıtım*
