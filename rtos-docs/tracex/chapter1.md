---
title: Bölüm 1 - Azure RTOS TraceX'e giriş
description: Azure RTOS TraceX, katıştırılmış bir hedefte çalışan ThreadX tarafından toplanan sistem olay bilgilerini görüntüleyen bir Microsoft sistem analizi aracıdır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 70eb06341e5d57f59c74888046bda3bbf95dc88cac56332be640d9576551796f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785065"
---
# <a name="chapter-1---introduction-to-azure-rtos-tracex"></a>Bölüm 1 - Azure RTOS TraceX'e giriş

Azure RTOS TraceX, katıştırılmış bir hedefte çalışan ThreadX tarafından toplanan sistem olay bilgilerini görüntüleyen bir Microsoft sistem analizi aracıdır. Kullanıcı, RAM'de depolanan izleme arabelleğinin katıştırılmış hedefte konak bilgisayarda bir ikili dosyaya aktarılmasından sorumludur. Kullanıcı daha sonra TraceX ile bu dosyayı açabilir ve hedef olayları grafiksel olarak analiz edip sistem sorunlarını tanılar ve performansı ve kaynak yönetimini geliştirmek için çalışan bir uygulamayı ayarlar.

## <a name="tracex-requirements"></a>TraceX Gereksinimleri

TraceX için Windows XP (veya üzeri) gerekir. Sistemde en az 192 MB RAM, 2 GB kullanılabilir sabit disk alanı ve 256 renkle en az 1024x768 görüntüsü olmalıdır. Ayrıca uygulamanın ThreadX V5.0 veya sonraki bir üzerinde çalışıyor olması gerekir.

TraceX ayrıca Microsoft .NET çerçevesinin de yüklü olması gerekir. Bu çerçeve, TraceX yükleyicisi tarafından otomatik olarak yüklenir.

## <a name="tracex-constraints"></a>TraceX Kısıtlamaları

TraceX aşağıdaki kısıtlamalara sahip:

- TraceX dosyaları en fazla 32.768 olayla sınırlıdır (yaklaşık 1 MB).
- Zaman damgası kaynağının makul bir çözüme sahip olması gerekir. Çözüm çok düşükse olaylar çakışır. Çözüm çok yüksekse olaylar arasında uzun boşluklar olabilir.
- TraceX, süreölçer süresinden büyük olaylar arasındaki aralıkları doğru bir şekilde ölçebilir.
