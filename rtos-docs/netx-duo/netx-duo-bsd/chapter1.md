---
title: Bölüm 1-Azure RTOS NetX Duo BSD 'ye giriş
description: BSD yuvası API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalar içeren ve Azure RTOS NetX Duo temel sürümlerini kullanan bazı temel BSD yuvası API çağrılarını destekler.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e89018dffd2f9f9065efab2ecabdf4364c4f89a3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826159"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-bsd"></a>Bölüm 1-Azure RTOS NetX Duo BSD 'ye giriş

BSD yuvası API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalar içeren ve Azure RTOS NetX Duo temel sürümlerini kullanan bazı temel BSD yuvası API çağrılarını destekler.

## <a name="bsd-socket-api-compliancy-wrapper-source"></a>BSD yuvası API 'SI karmaşık pozisyon sarmalayıcı kaynağı

Sarmalayıcı kaynak kodu basitlik için tasarlanmıştır ve iki dosyadan oluşur; yani *nxd_bsd. h* ve *nxd_bsd. c*. *Nxd_bsd. h* dosyası, tüm gerekli BSD yuvası API sarmalayıcı sabitlerini ve alt yordam prototiplerini tanımlar, ancak *nxd_bsd. c* gerçek BSD yuvası API 'si uyumluluk kaynak kodunu içerir. Bu sarmalayıcı kaynak dosyaları tüm NetX Duo destek paketlerinde ortaktır.

Paket aşağıdakilerden oluşur:

- **nxd_bsd. c**: sarmalayıcı kaynak kodu
- **nxd_bsd. h**: Ana üstbilgi dosyası

Örnek demo programları:

- **bsd_demo_udp. c**: *iki UDP eşiyle demo (yalnızca IPv4)*
- **bsd_demo_tcp. c**: *tek bir TCP sunucusu ve istemcisiyle demo*
- **bsd_demo_raw. c**: *iki ham eş ile demo*