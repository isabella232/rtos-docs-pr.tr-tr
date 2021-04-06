---
title: Bölüm 1-ARMv8-e için Azure RTOS ThreadX 'e giriş.
description: Bu bölüm, ARMv8-ı için Azure RTOS ThreadX eki hakkında okuma için başlangıç noktasıdır.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 486466f41e64adb9e32ebbd21a22629221ffa9c1
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377626"
---
# <a name="chapter-1--overview"></a>Bölüm 1 genel bakış

ARMv8-ı mimarisi, belleğin güvenli veya güvenli olmayan şekilde etiketlenmesine izin veren TrustZone dahil yeni güvenlik özellikleri sunar. Aşağıdaki ARM 'nin yönergeleri, ThreadX (ve Kullanıcı uygulaması) güvenli olmayan modda çalışacak şekilde tasarlanmıştır. ThreadX (ve Kullanıcı uygulaması) güvenli modda da çalıştırılabilir. Güvenli mod yazılımıyla arabirim sağlamak için bazı yeni ThreadX API 'Leri gereklidir. Bu belgede Cortex-M23, Cortex-M33, Cortex-M35P ve Cortex-M55 dahil olmak üzere ARMv8-e mimarisine özgü bu ThreadX Hizmetleri açıklanmaktadır.
