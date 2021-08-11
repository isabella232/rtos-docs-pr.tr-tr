---
title: Ek A - Azure RTOS NetX Duo SNTP Önemli Hata Kodları
description: Aşağıdaki hata kodları, NetX Duo Azure RTOS SNTP İstemcisi'nin geçerli sunucuyla zaman güncelleştirmelerini durdurması ile sonuç verir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e0152c1342b3edffd42f7442c51e7c5d62b199a5b38085dac06b4c0dbee9e9a8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790114"
---
# <a name="appendix-a---azure-rtos-netx-duo-sntp-fatal-error-codes"></a>Ek A - Azure RTOS NetX Duo SNTP Önemli Hata Kodları

Aşağıdaki hata kodları, NetX Duo Azure RTOS SNTP İstemcisi'nin geçerli sunucuyla zaman güncelleştirmelerini durdurması ile sonuç verir. Sunucunun kullanılabilir sunucuların SNTP İstemcisi listesinden kaldırılmasına veya listeden bir sonraki kullanılabilir sunucuya geçişe karar vermek uygulamanın kararıdır. Her hata durumunun tanımı *nxd_sntp_client.h içinde tanımlanır. *

SNTP İstemcisi aşağıdaki listeden uygulamaya bir hata döndürmüş olduğunda, Sunucu büyük olasılıkla başka bir Sunucu ile değiştir değiştir değiştiri. Hata durumunun NX_SNTP_KOD_REMOVE_SERVER SNTP İstemcisi ölüm işleyicisi (geri çağırma işlevi) işlevine bırakarak şunları ayarlay olduğunu unutmayın:

- NX_SNTP_KOD_REMOVE_SERVER 0xD0C  
- NX_SNTP_SERVER_AUTH_FAIL 0xD0D  
- NX_SNTP_INVALID_NTP_VERSION 0xD11  
- NX_SNTP_INVALID_SERVER_MODE 0xD12  
- NX_SNTP_INVALID_SERVER_STRATUM 0xD15  

SNTP İstemcisi aşağıdaki listeden uygulamaya bir hata döndürmüş olduğunda, Sunucu yalnızca geçici olarak geçerli saat güncelleştirmeleri sağlayamıyor olabilir ve kaldırılması gerek olmayabilir:

- HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09  
- NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B  
- NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17  
- NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16  
- NX_SNTP_INVALID_RTT_TIME 0xD21  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24