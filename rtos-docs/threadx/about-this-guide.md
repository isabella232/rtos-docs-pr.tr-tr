---
title: Azure RTOS ThreadX Kılavuzu hakkında
description: Bu kılavuz, Microsoft yüksek performanslı gerçek zamanlı çekirdek olan Azure RTOS ThreadX hakkında kapsamlı bilgiler sağlar.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ad9f782942bcdbb2dc49a9c841d865d97bcb1d4e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826591"
---
# <a name="about-the-azure-rtos-threadx-guide"></a>Azure RTOS ThreadX Kılavuzu hakkında

Bu kılavuz, Microsoft yüksek performanslı gerçek zamanlı çekirdek olan Azure RTOS ThreadX hakkında kapsamlı bilgiler sağlar. 

Katıştırılmış gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştirici standart gerçek zamanlı işletim sistemi işlevleri ve C programlama diliyle tanıdık gelmelidir.

## <a name="organization"></a>Kuruluş

[Bölüm 1](chapter1.md) -Azure RTOS threadx için temel bir genel bakış ve gerçek zamanlı gömülü geliştirmeyle ilişkisi sağlar

[Bölüm 2](chapter2.md) -uygulamanızda Azure RTOS threadx 'i yüklemek ve kullanmak için temel adımlara izin verir 

[Bölüm 3](chapter3.md) -Azure RTOS threadx 'in işlevsel işlemi ayrıntılı olarak, yüksek performanslı gerçek zamanlı çekirdek

[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS threadx 'e ait arabiriminin ayrıntıları

[Bölüm 5](chapter5.md) -Azure RTOS threadx uygulamaları için g/ç sürücülerinin yazılmasını açıklar

[Bölüm 6](chapter6.md) -her Azure RTOS threadx işlemci desteği paketiyle birlikte sunulan tanıtım uygulamasını açıklar

[Ek A](appendix-a.md) -Azure RTOS THREADX API 'si

[Ek B](appendix-b.md) -Azure RTOS threadx sabitleri

[Ek C](appendix-c.md) -Azure RTOS threadx veri türleri

[Ek D](appendix-d.md) -ASCII grafik

## <a name="guide-conventions"></a>Kılavuz kuralları

*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve parametreleri gösterir.

**Kalın** yazı tipi, anahtar sözcükler, sabitler, tür adları, Kullanıcı arabirimi öğeleri, değişken adları ve önemli sözcükleri daha fazla vurgular.

***İtalik ve kalın*** yazı tipi dosya adlarını ve işlev adlarını gösterir.

> [!IMPORTANT]
> Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.

> [!WARNING]
> Uyarı sembolleri, geliştiricilerin önemli hatalara neden olabileceğinden kaçınmak için dikkatli olması gereken durumlara dikkat çekecek.

## <a name="azure-rtos-threadx-data-types"></a>Azure RTOS ThreadX veri türleri

Özel Azure RTOS ThreadX denetim yapısı veri türlerine ek olarak, Azure RTOS ThreadX hizmet çağrı arabirimlerinde kullanılan bir dizi özel veri türü vardır. Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir. Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır. Tam uygulama, kaynağa dahil olan ***tx_port. h*** dosyasında bulunabilir.

Aşağıda, Azure RTOS ThreadX hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:

| Veri türü  | Açıklama |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **U** | Temel işaretsiz tamsayı. Bu tür 8 bit işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir. |
| **'TUR** | İmzasız Long türü. Bu tür 32 bitlik işaretsiz verileri desteklemelidir. |
| **Kağıt** | Derleyicinin void türüne neredeyse her zaman eşdeğerdir. |
| **CHAR** | Genellikle standart 8 bitlik bir karakter türü. |
|  |  |

Ek veri türleri, Azure RTOS ThreadX kaynağı içinde kullanılır. Bunlar ayrıca ***tx_port. h*** dosyasında bulunur.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.
2. Uygulamada ve/veya Azure RTOS ThreadX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.
3. *_Tx_version_id* dizesinin içeriği, dağılımının *tx_port. h* dosyasında bulunur. Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.
4. **_Tx_build_options** **ulong** değişkeninin RAM 'e ait içerik. Bu değişken, Azure RTOS ThreadX Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.
