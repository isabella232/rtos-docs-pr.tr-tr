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
# <a name="chapter-1--overview"></a><span data-ttu-id="5501b-103">Bölüm 1 genel bakış</span><span class="sxs-lookup"><span data-stu-id="5501b-103">Chapter 1  Overview</span></span>

<span data-ttu-id="5501b-104">ARMv8-ı mimarisi, belleğin güvenli veya güvenli olmayan şekilde etiketlenmesine izin veren TrustZone dahil yeni güvenlik özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="5501b-104">The ARMv8-M architecture introduces new security features, including TrustZone, which allows memory to be tagged as secure or non-secure.</span></span> <span data-ttu-id="5501b-105">Aşağıdaki ARM 'nin yönergeleri, ThreadX (ve Kullanıcı uygulaması) güvenli olmayan modda çalışacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5501b-105">Following ARM's guidelines, ThreadX (and the user application) is designed to be run in non-secure mode.</span></span> <span data-ttu-id="5501b-106">ThreadX (ve Kullanıcı uygulaması) güvenli modda da çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5501b-106">ThreadX (and the user application) can also be run in secure mode.</span></span> <span data-ttu-id="5501b-107">Güvenli mod yazılımıyla arabirim sağlamak için bazı yeni ThreadX API 'Leri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5501b-107">In order to interface with secure mode software, some new ThreadX APIs are necessary.</span></span> <span data-ttu-id="5501b-108">Bu belgede Cortex-M23, Cortex-M33, Cortex-M35P ve Cortex-M55 dahil olmak üzere ARMv8-e mimarisine özgü bu ThreadX Hizmetleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5501b-108">This document describes these ThreadX services that are specific to the ARMv8-M architecture, including the Cortex-M23, Cortex-M33, Cortex-M35P, and Cortex-M55.</span></span>
