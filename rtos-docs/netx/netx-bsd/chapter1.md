---
title: Bölüm 1-Azure RTOS NetX BSD 'ye giriş
description: Azure RTOS NetX BSD yuvaları API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalara sahip temel BSD yuvaları API çağrılarının bazılarını destekler ve altındaki NetX temel öğelerini kullanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fce781ac97ae75c4148614453eeb35c3064f8849
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825607"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-bsd"></a>Bölüm 1-Azure RTOS NetX BSD 'ye giriş

NetX BSD yuvaları API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalara sahip olan temel BSD yuvaları API çağrılarının bazılarını destekler ve altındaki NetX temelleri kullanır. Bu sarmalayıcı iç NetX temelleri kullandığından ve temel NetX hata denetimini atladığı için bu BSD yuvaları API Uyumluluk katmanının tipik BSD uygulamalarından hızlı veya biraz daha hızlı olması gerekir.

## <a name="bsd-sockets-api-compliancy-wrapper-source"></a>BSD yuvaları API Karmaşıkkonum sarmalayıcı kaynağı

BSD sarmalayıcısı kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur *nx_bsd. h* ve *nx_bsd. c*. *Nx_bsd. h* dosyası tüm gerekli BSD yuvaları API sarmalayıcı sabitlerini ve alt yordam prototiplerini tanımlar, ancak *nx_bsd. c* gerçek BSD yuvaları API uyumluluğu kaynak kodunu içerir. Bu BSD sarmalayıcı kaynak dosyaları tüm NetX destek paketlerinde ortaktır.

Paket aşağıdakilerden oluşur:

- **nx_bsd. c**: sarmalayıcı kaynak kodu
- **nx_bsd. h**: Ana üstbilgi dosyası

Örnek demo programları:

- **bsd_demo_tcp. c**: *tek bir TCP sunucusu ve istemcisiyle demo*
- **bsd_demo_udp. c**: *iki UDP ISTEMCISI ve bir UDP sunucusu ile demo*
