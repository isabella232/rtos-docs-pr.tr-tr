---
title: Bölüm 1-Azure RTOS TraceX 'e giriş
description: Azure RTOS TraceX, bir katıştırılmış hedefte çalışan ThreadX tarafından toplanan sistem olay bilgilerini görüntüleyen bir Microsoft Sistem analizi aracıdır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 3009d13388b3b7e8eca041dc6ede569a5caf5e9b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827683"
---
# <a name="chapter-1---introduction-to-azure-rtos-tracex"></a><span data-ttu-id="1bee6-103">Bölüm 1-Azure RTOS TraceX 'e giriş</span><span class="sxs-lookup"><span data-stu-id="1bee6-103">Chapter 1 - Introduction to Azure RTOS TraceX</span></span>

<span data-ttu-id="1bee6-104">Azure RTOS TraceX, bir katıştırılmış hedefte çalışan ThreadX tarafından toplanan sistem olay bilgilerini görüntüleyen bir Microsoft Sistem analizi aracıdır.</span><span class="sxs-lookup"><span data-stu-id="1bee6-104">Azure RTOS TraceX is a Microsoft system analysis tool that displays system event information gathered by ThreadX running on an embedded target.</span></span> <span data-ttu-id="1bee6-105">Kullanıcı, katıştırılmış hedefteki RAM 'de depolanan izleme arabelleğinin ana bilgisayardaki bir ikili dosyaya aktarılmasından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="1bee6-105">The user is responsible for transferring the trace buffer stored in RAM in the embedded target to a binary file on the host computer.</span></span> <span data-ttu-id="1bee6-106">Kullanıcı daha sonra bu dosyayı TraceX ile açabilir ve hedef olayları grafiksel olarak analiz edebilir, sistem sorunlarını tanıleyebilir ve performans ve kaynak yönetimini geliştirmek için çalışan bir uygulamanın ayarlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bee6-106">The user can then open this file with TraceX and graphically analyze the target events, diagnosing system problems and tuning a working application to improve performance and resource management.</span></span>

## <a name="tracex-requirements"></a><span data-ttu-id="1bee6-107">Trackingex gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="1bee6-107">TraceX Requirements</span></span>

<span data-ttu-id="1bee6-108">TraceX, Windows XP (veya üzeri) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1bee6-108">TraceX requires Windows XP (or above).</span></span> <span data-ttu-id="1bee6-109">Sistemde en az 192 MB RAM, 2 GB kullanılabilir sabit disk alanı ve en az 256 renk içeren 1024x768 ekran görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="1bee6-109">The system should have a minimum of 192 MB of RAM, 2 GB of available hard-disk space, and a minimum display of 1024x768 with 256 colors.</span></span> <span data-ttu-id="1bee6-110">Ayrıca, uygulamanın ThreadX V 5.0 veya sonraki bir sürümde çalışıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bee6-110">In addition, the application must be running on ThreadX V5.0 or later.</span></span>

<span data-ttu-id="1bee6-111">TraceX Ayrıca, TraceX yükleyicisinin otomatik olarak çalıştığı Microsoft .NET Framework 'ün yüklenmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1bee6-111">TraceX also requires the Microsoft .NET framework be installed, which the TraceX installer does automatically.</span></span>

## <a name="tracex-constraints"></a><span data-ttu-id="1bee6-112">Trackingex kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="1bee6-112">TraceX Constraints</span></span>

<span data-ttu-id="1bee6-113">TraceX aşağıdaki kısıtlamalara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="1bee6-113">TraceX has the following constraints:</span></span>

- <span data-ttu-id="1bee6-114">TraceX dosyaları en fazla 32.768 olayla sınırlıdır (kabaca 1 MB).</span><span class="sxs-lookup"><span data-stu-id="1bee6-114">TraceX files are limited to a maximum of 32,768 events (roughly 1 MB ).</span></span>
- <span data-ttu-id="1bee6-115">Zaman damgası kaynağı makul çözünürlüğe sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1bee6-115">The time-stamp source must have reasonable resolution.</span></span> <span data-ttu-id="1bee6-116">Çözüm çok düşükse olaylar çakışacaktır.</span><span class="sxs-lookup"><span data-stu-id="1bee6-116">If the resolution is too low, the events will overlap.</span></span> <span data-ttu-id="1bee6-117">Çözünürlük çok yüksekse olaylar arasında uzun boşluklar meydana olur.</span><span class="sxs-lookup"><span data-stu-id="1bee6-117">If the resolution is too high, there is potential for long gaps between events.</span></span>
- <span data-ttu-id="1bee6-118">Trackingex, Zamanlayıcı süresinden daha büyük olaylar arasındaki aralıkları doğru şekilde ölçmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="1bee6-118">TraceX cannot accurately measure intervals between events greater than the timer period.</span></span>
