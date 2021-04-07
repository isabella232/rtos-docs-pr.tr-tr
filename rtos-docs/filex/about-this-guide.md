---
title: Azure RTOS FileX Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un yüksek performanslı gerçek zamanlı dosya sistemi olan Azure RTOS FileX hakkında kapsamlı bilgiler içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 640d9ed4c8037d3af6c5f45158c9496ad1258a3c
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550108"
---
# <a name="about-this-filex-user-guide"></a>Bu FileX Kullanıcı Kılavuzu hakkında

Bu kılavuz, Microsoft 'un yüksek performanslı ve gerçek zamanlı katıştırılmış dosya sistemi olan Azure RTOS FileX hakkında kapsamlı bilgiler içerir. Bu kılavuzdan en iyi şekilde kazanmak için standart gerçek zamanlı işletim sistemi işlevleri, FAT dosya sistemi hizmetleri ve C programlama dili hakkında bilgi sahibi olmanız gerekir.

## <a name="organization"></a>Kuruluş

[Bölüm 1](chapter1.md) -Azure RTOS FileX 'i tanıtır

[Bölüm 2](chapter2.md) -Azure RTOS threadx uygulamanızla Azure RTOS FileX 'i yüklemek ve kullanmak için temel adımları sağlar

[Bölüm 3](chapter3.md) -Azure RTOS FileX SISTEMINE ve FAT dosya sistemi biçimleriyle ilgili temel bilgilere yönelik işlevsel bir genel bakış sağlar

[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS FileX 'e ait arabiriminin ayrıntıları

[Bölüm 5](chapter5.md) -sağlanan Azure RTOS FILEX RAM sürücüsünü ve kendi özel Azure RTOS FileX sürücülerinizi yazmayı açıklar

[Bölüm 6](chapter6.md) -Azure RTOS FileX hata dayanıklı modülünü açıklar

[Ek A](appendix-a.md) -Azure RTOS FileX Hizmetleri

[Ek B](appendix-b.md) -Azure RTOS FileX sabitleri

[Ek C](appendix-c.md) -Azure RTOS FileX veri türleri

[Ek D](appendix-d.md) -ASCII grafik

## <a name="guide-conventions"></a>Kılavuz kuralları

*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.

**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.

> [!NOTE]
> Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.

> [!IMPORTANT]
> Uyarı sembolleri, önemli hatalara neden olabileceğinden, geliştiricilerin oluşmaması gereken durumlara dikkat çekecek.

## <a name="filex-data-types"></a>FileX veri türleri

Özel Azure RTOS FileX denetim yapısı veri türlerine ek olarak, Azure RTOS FileX hizmet çağrı arabirimlerinde kullanılan bir dizi özel veri türü vardır. Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir. Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır. Tam uygulama Azure RTOS ThreadX 'ten devralınmıştır ve Azure RTOS ThreadX dağıtımına eklenen tx_port. h dosyasında bulunabilir.

Aşağıda, Azure RTOS FileX hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir.

| Tür  | Açıklama  |
|---|---|
| **U** | Temel işaretsiz tamsayı. Bu tür 8 bit işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir. |
| **'TUR** | İmzasız Long türü. Bu tür 32 bitlik işaretsiz verileri desteklemelidir. |
| **Kağıt** | Derleyicinin void türüne neredeyse her zaman eşdeğerdir. |
| **CHAR** | Genellikle standart 8 bitlik bir karakter türü. |
| **ULONG64** | 64-bit işaretsiz tamsayı veri türü. |

Ek veri türleri, FileX kaynağı içinde kullanılır. Bunlar, ***tx_port. h** _ veya _ *_fx_port. h_** dosyalarında konumlardır.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin.

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.
2. Uygulamada ve/veya FileX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.
3. _Tx_version_id ve fx_version_id dizelerinin içeriği, _**tx_port. h**_ ve _ *_fx_port. h_**, dağıtım dosyalarınızın dosyalarında bulunur. Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.
4. Aşağıdaki **ulong** değişkenlerinin RAM 'e ait içerik. Bu değişkenler, ThreadX ve FileX kitaplıklarınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir:

    **_tx_build_options**

    **_fx_system_build_options1**

    **_fx_system_build_options2**

    **_fx_system_build_options3**
