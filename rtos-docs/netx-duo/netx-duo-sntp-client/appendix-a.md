---
title: Ek A-Azure RTOS NetX Duo SNTP önemli hata kodları
description: Aşağıdaki hata kodları, Azure RTOS NetX Duo SNTP Istemcisinin geçerli sunucu ile zaman güncellerinin iptal edilmesine neden olur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 065e7a3e65b3cf8d7fcfb34bb9568a673791609a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825762"
---
# <a name="appendix-a---azure-rtos-netx-duo-sntp-fatal-error-codes"></a>Ek A-Azure RTOS NetX Duo SNTP önemli hata kodları

Aşağıdaki hata kodları, Azure RTOS NetX Duo SNTP Istemcisinin geçerli sunucu ile zaman güncellerinin iptal edilmesine neden olur. Sunucunun, kullanılabilir sunucuların SNTP Istemci listesinden kaldırılıp kaldırılamayacağına karar vermek veya listedeki bir sonraki kullanılabilir sunucuya geçiş yapmak, uygulamaya bağlıdır. Her hata durumunun tanımı * nxd_sntp_client. h içinde tanımlanır. *

SNTP Istemcisi, aşağıdaki listeden uygulamaya bir hata döndürürse, sunucunun büyük olasılıkla başka bir sunucu ile değiştirilmeleri gerekir. NX_SNTP_KOD_REMOVE_SERVER hata durumunun, ayarlamak için bir deölüm işleyicisinin (geri çağırma işlevi) SNTP istemci öpücük 'ye kaldığını unutmayın:

- NX_SNTP_KOD_REMOVE_SERVER 0xD0C  
- NX_SNTP_SERVER_AUTH_FAIL 0xD0D  
- NX_SNTP_INVALID_NTP_VERSION 0xD11  
- NX_SNTP_INVALID_SERVER_MODE 0xD12  
- NX_SNTP_INVALID_SERVER_STRATUM 0xD15  

SNTP Istemcisi, aşağıdaki listeden uygulamaya bir hata döndürürse, sunucu yalnızca geçici olarak geçerli saat güncelleştirmeleri sağlayamayabilir ve kaldırılması gerekebilir:

- HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09  
- NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B  
- NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17  
- NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16  
- NX_SNTP_INVALID_RTT_TIME 0xD21  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24