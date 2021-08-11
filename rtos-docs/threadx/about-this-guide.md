---
title: Azure RTOS ThreadX Kılavuzu Hakkında
description: Bu kılavuz, Microsoft yüksek performanslı Azure RTOS ThreadX çekirdek hakkında kapsamlı bilgi sağlar.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 28f088409fdd5e2c075cbf90b21d3d260c811806066e74bffc395207cde0239c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802133"
---
# <a name="about-the-azure-rtos-threadx-guide"></a>Azure RTOS ThreadX Kılavuzu Hakkında

Bu kılavuz, Microsoft yüksek performanslı Azure RTOS ThreadX çekirdeği hakkında kapsamlı bilgi sağlar. 

Eklenmiş gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştiricinin standart gerçek zamanlı işletim sistemi işlevlerine ve C programlama diline aşina olması gerekir.

## <a name="organization"></a>Kuruluş

[Bölüm 1](chapter1.md) - ThreadX'Azure RTOS gerçek zamanlı tümleşik geliştirmeyle ilişkisine ilişkin temel bir genel bakış sağlar

[2.](chapter2.md) Bölüm : Uygulamanıza Azure RTOS ThreadX'i yüklemek ve kullanmak için *gereken temel adımları verir*

[Bölüm 3](chapter3.md) - Yüksek performanslı gerçek zamanlı çekirdek olan Azure RTOS ThreadX'in işlevsel işlemi ayrıntılı olarak açıklanmaktadır

[Bölüm 4](chapter4.md) - Uygulamanın ThreadX'i Azure RTOS ayrıntıları

[5.](chapter5.md) Bölüm - ThreadX uygulamaları için Azure RTOS yazmayı açıklar

[Bölüm 6](chapter6.md) - ThreadX işlemcisi destek paketinin her biri Azure RTOS tanıtım uygulamasını açıklar

[Ek A](appendix-a.md) - Azure RTOS ThreadX API'si

[Ek B](appendix-b.md) - Azure RTOS ThreadX sabitleri

[Ek C](appendix-c.md) - Azure RTOS ThreadX veri türleri

[Ek D](appendix-d.md) - ASCII grafiği

## <a name="guide-conventions"></a>Kılavuz Kuralları

*Italik* - yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve parametreleri belirtir.

**Kalın-** yazı tipi, anahtar sözcükleri, sabitleri, tür adlarını, kullanıcı arabirimi öğelerini, değişken adlarını belirtir ve önemli sözcükleri daha da vurgular.

***İtalik ve Kalın- yazı*** tipi, dosya adlarını ve işlev adlarını belirtir.

> [!IMPORTANT]
> Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çeker.

> [!WARNING]
> Uyarı sembolleri, geliştiricilerin önemli hatalara neden olduğu için kaçınmaları gereken durumlara dikkat eder.

## <a name="azure-rtos-threadx-data-types"></a>Azure RTOS ThreadX Veri Türleri

ThreadX denetim Azure RTOS veri türlerine ek olarak, ThreadX hizmeti çağrı arabirimlerinde Azure RTOS özel veri türleri de vardır. Bu özel veri türleri doğrudan temel alınan C derleyicisi veri türleriyle eşler. Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır. Tam uygulama, kaynakta bulunan ***tx_port.h*** dosyasında bulunabilir.

Aşağıda, ThreadX hizmeti Azure RTOS veri türlerini ve ilişkili anlamlarını listelemektedir:

| Veri türü  | Açıklama |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Uint** | Temel imzasız tamsayı. Bu tür 8 bit imzasız verileri desteklemeli; ancak, en kullanışlı imzasız veri türüyle eşlenmiş. |
| **Ulong** | Imzasız uzun tür. Bu tür, 32 bit imzasız verileri desteklemeli. |
| **Void** | Neredeyse her zaman derleyicinin void türüne eşdeğerdir. |
| **Char** | Genellikle standart bir 8 bit karakter türü. |
|  |  |

ThreadX kaynağında ek veri Azure RTOS kullanılır. Bunlar ayrıca ***tx_port.h dosyasında*** bulunur.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Buradaki adımları kullanarak sorularınız veya yardım için lütfen Azure Portal üzerinden bir destek bileti gönderin. Destek isteğinizi daha verimli bir şekilde çözüme kavuşturmamızı sağlamak için lütfen bir e-posta iletisinde aşağıdaki bilgileri bize iletin:

1. Oluşma sıklığı ve güvenilir bir şekilde yeniden üretilip üretilileyil olmadığı da dahil olmak üzere sorunun ayrıntılı açıklaması.
2. Uygulamada yapılan değişikliklerin ve/veya sorundan önce Azure RTOS ThreadX'in ayrıntılı açıklaması.
3. Dağıtım dizenizin *_tx_version_id.h* dosyasında *bulunan tx_port* dizenin içeriği. Bu dize, çalışma zamanı ortamınız hakkında değerli bilgiler sağlar.
4. **ULONG** değişkeninin **RAM'_tx_build_options** içeriği. Bu değişken, iş parçacığı threadx kitaplığınızı Azure RTOS hakkında bilgi sağlar.
