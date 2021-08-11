---
title: Bölüm 1 - ARMv8-M Azure RTOS ThreadX'e giriş.
description: Bu bölüm, ARMv8-M için Azure RTOS ThreadX Eki hakkında bilgi edinen başlangıç noktasıdır.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1f0d87ec562c7fcfa6af5d2240655ef526f6e0611d509fe60c745436371413d7
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798257"
---
# <a name="chapter-1--overview"></a>Bölüm 1'e Genel Bakış

ARMv8-M mimarisi, belleğin güvenli veya güvenli olmayan olarak etiketlenmiş olması için TrustZone da dahil olmak üzere yeni güvenlik özellikleri sunar. ARM yönergelerini takip eden ThreadX (ve kullanıcı uygulaması), güvenli olmayan modda çalıştıracak şekilde tasarlanmıştır. ThreadX (ve kullanıcı uygulaması) güvenli modda da çalışır. Güvenli mod yazılımıyla arabirim sağlamak için bazı yeni ThreadX API'leri gereklidir. Bu belgede, Cortex-M23, Cortex-M33, Cortex-M35P ve Cortex-M55 gibi ARMv8-M mimarisine özgü bu ThreadX hizmetleri açıklandı.
