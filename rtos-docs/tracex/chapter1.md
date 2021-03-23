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
# <a name="chapter-1---introduction-to-azure-rtos-tracex"></a>Bölüm 1-Azure RTOS TraceX 'e giriş

Azure RTOS TraceX, bir katıştırılmış hedefte çalışan ThreadX tarafından toplanan sistem olay bilgilerini görüntüleyen bir Microsoft Sistem analizi aracıdır. Kullanıcı, katıştırılmış hedefteki RAM 'de depolanan izleme arabelleğinin ana bilgisayardaki bir ikili dosyaya aktarılmasından sorumludur. Kullanıcı daha sonra bu dosyayı TraceX ile açabilir ve hedef olayları grafiksel olarak analiz edebilir, sistem sorunlarını tanıleyebilir ve performans ve kaynak yönetimini geliştirmek için çalışan bir uygulamanın ayarlanmasını sağlar.

## <a name="tracex-requirements"></a>Trackingex gereksinimleri

TraceX, Windows XP (veya üzeri) gerektirir. Sistemde en az 192 MB RAM, 2 GB kullanılabilir sabit disk alanı ve en az 256 renk içeren 1024x768 ekran görüntülenebilir. Ayrıca, uygulamanın ThreadX V 5.0 veya sonraki bir sürümde çalışıyor olması gerekir.

TraceX Ayrıca, TraceX yükleyicisinin otomatik olarak çalıştığı Microsoft .NET Framework 'ün yüklenmesini gerektirir.

## <a name="tracex-constraints"></a>Trackingex kısıtlamaları

TraceX aşağıdaki kısıtlamalara sahiptir:

- TraceX dosyaları en fazla 32.768 olayla sınırlıdır (kabaca 1 MB).
- Zaman damgası kaynağı makul çözünürlüğe sahip olmalıdır. Çözüm çok düşükse olaylar çakışacaktır. Çözünürlük çok yüksekse olaylar arasında uzun boşluklar meydana olur.
- Trackingex, Zamanlayıcı süresinden daha büyük olaylar arasındaki aralıkları doğru şekilde ölçmeyebilir.
