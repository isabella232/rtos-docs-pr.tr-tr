---
title: Bölüm 1-Azure RTOS LevelX 'e genel bakış
description: Azure RTOS LevelX, gömülü uygulamalara NAND ve Flash giyme seviyelendirme olanakları sağlar.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 045446fec74164f125bc0ad27e8b7a904be14ab2
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826273"
---
# <a name="chapter-1---overview-of-azure-rtos-levelx"></a>Bölüm 1-Azure RTOS LevelX 'e genel bakış

Azure RTOS LevelX, gömülü uygulamalara NAND ve Flash giyme seviyelendirme olanakları sağlar. Hem NHEM de hem de Flash belleği yalnızca sınırlı sayıda silinebileceğinizden, Flash bellek kullanımını eşit bir şekilde dağıtmak önemlidir. Bu genellikle "giyme seviyelendirme" olarak adlandırılır ve LevelX 'in arkasındaki amaç olur.

Hangi Flash bloğunun yeniden kullanılmasını seçen algoritma öncelikle silme sayımına dayanır, ancak tamamen değil. En düşük silme sayısı içinde, kabul edilebilir bir Delta içinde silme sayısına sahip başka bir blok varsa ve daha fazla kullanılmayan eşlemeye sahip olan bir blok sayısı, en düşük silme sayısına sahip olan blok seçilemez. Bu gibi durumlarda, en fazla Kullanımdan kaldırılmış eşlemelerin bulunduğu blok silinir ve yeniden kullanılır ve bu nedenle geçerli eşleme girdilerini taşırken ek yük tasarrufu yapılır.

LevelX, nve ve/veya bölümlerinin birden çok örneğini destekler, yani uygulama aynı uygulama içinde farklı LevelX örneklerini kullanabilir. Her örnek, uygulamanın yanı sıra kendi Flash sürücü tarafından sağlanmış kendi denetim bloğunu gerektirir.

LevelX, Kullanıcı tarafından LevelX 'in içindeki fiziksel Flash bellekle eşlenmiş bir dizi mantıksal sektör sunar. LevelX, performansı artırmak için, en son mantıksal kesim eşlemelerinin bir önbelleğini de sağlar. Bu önbelleğin boyutu programcı tarafından tanımlanır. Uygulamalar, FileX ile birlikte LevelX kullanabilir veya mantıksal kesimleri doğrudan okuyabilir/yazabilir. LevelX 'in dosya x 'e bağımlılığı yoktur ve ThreadX üzerinde çok az bağımlılığı vardır (yalnızca temel ThreadX veri türleri kullanılır).

LevelX, hata toleransı için tasarlanmıştır. Flash güncelleştirmeleri, her adımda kesintiye uğratıluygulanabilecek çok adımlı bir işlemde gerçekleştirilir. LevelX, bir sonraki işlem sırasında en iyi duruma otomatik olarak kurtarır.

LevelX, temeldeki flash belleğe fiziksel erişim için bir Flash sürücüsü gerektirir. Örnek nve ve ve sanal sürücüler sağlanır ve gerçek LevelX sürücülerini uygulamak için iyi bir başlangıç noktası olarak kullanılabilir. Ayrıca, bu belgelerde daha sonra sürücü gereksinimleri ayrıntılı olarak açıklanmıştır.

Aşağıdaki bölümlerde, nve ve veya LevelX desteği için işlevsel işlem açıklanır.
