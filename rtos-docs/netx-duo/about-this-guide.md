---
title: Azure RTOS NetX Duo Kullanıcı Kılavuzu hakkında
description: Bu kılavuz, Microsoft yüksek performanslı IPv4/IPv6 ikili ağ yığını olan Azure RTOS NetX Duo hakkında kapsamlı bilgiler içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b1eef5bfa28f13d7a6b627792f96039b252f2355
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826237"
---
# <a name="about-the-azure-rtos-netx-duo-user-guide"></a>Azure RTOS NetX Duo Kullanıcı Kılavuzu hakkında

Bu kılavuz, Microsoft yüksek performanslı IPv4/IPv6 ikili ağ yığını olan Azure RTOS NetX Duo hakkında kapsamlı bilgiler içerir. 

Temel ağ kavramlarıyla, Azure RTOS ThreadX ve C programlama diliyle tanıdık olan gömülü gerçek zamanlı yazılım geliştiricileri için tasarlanmıştır.

## <a name="organization"></a>Kuruluş

[Bölüm 1](chapter1.md) -Azure RTOS NETX Duo 'i tanıtır

[Bölüm 2](chapter2.md) -Azure RTOS NETX Duo 'U threadx uygulamanızla yüklemek ve kullanmak için temel adımlara izin verir

[Bölüm 3](chapter3.md) -Azure RTOS NETX Duo sistemine işlevsel bir genel bakış ve TCP/IP ağ standartları hakkında temel bilgiler sağlar

[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS NETX Duo arabirimine ayrıntıları

[Bölüm 5](chapter5.md) -Azure RTOS NETX Duo için ağ sürücülerini açıklar

[Ek A](appendix-a.md) -Azure RTOS NETX Duo Hizmetleri

[Ek B](appendix-b.md) -Azure RTOS NETX Duo sabitleri

[Ek C](appendix-c.md) -Azure RTOS NETX Duo veri türleri

[Ek D](appendix-d.md) -BSD-Compatible yuvası API 'si

[Ek E](appendix-e.md) -ASCII grafik

## <a name="guide-conventions"></a>Kılavuz kuralları

İtalik yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.

**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.

> [!IMPORTANT]
> Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.
 
> [!WARNING]
> Uyarı sembolleri, önemli hatalara neden olabileceğinden, geliştiricilerin oluşmaması gereken durumlara dikkat çekecek.

## <a name="azure-rtos-netx-duo-data-types"></a>Azure RTOS NetX Duo veri türleri

Özel Azure RTOS NetX Duo denetim yapısı veri türlerine ek olarak, Azure RTOS NetX Duo hizmet çağrı arabirimlerinde kullanılan birkaç özel veri türü vardır. Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir. Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır. Tam uygulama ThreadX 'ten devralınır ve ThreadX dağıtımına dahil olan ***tx_port. h*** dosyasında bulunabilir.

Aşağıda, Azure RTOS NetX Duo hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:

**UINT**: temel işaretsiz tamsayı. Bu tür 32 bitlik işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir.  
**Ulong**: imzasız Long türü. Bu tür 32 bitlik işaretsiz verileri desteklemelidir.
**VOID**: derleyicinin VOID türüne neredeyse her zaman eşdeğerdir.  
**Char**: genellikle standart 8 bitlik bir karakter türüdür.  

Ek veri türleri, Azure RTOS NetX Duo kaynağı içinde kullanılır. Bunlar, ***tx_port. h** _ veya _ *_nx_port. h_** dosyalarında konumlardır.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.
2. Uygulamada ve/veya Azure RTOS NetX Duo üzerinde yapılan tüm değişikliklerin ayrıntılı bir açıklaması ve bundan önce sorun.
3. _Tx_version_id ve _nx_version_id dizelerinin içerikleri, dağılımının tx_port. h ve nx_port. h dosyalarında bulunur. Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.
4. Aşağıdaki ULONG değişkenlerinin RAM 'ine ait içerikler:

    **_tx_build_options**

    **_nx_system_build_options1**

    **_nx_system_build_options2**

    **_nx_system_build_options3**

    **_nx_system_build_options4**

    **_nx_system_build_options5**

    Bu değişkenler, Azure RTOS ThreadX ve Azure RTOS NetX Duo kitaplıklarının nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.

5. Sorun algılandıktan hemen sonra yakalanan bir izleme arabelleği. Bu, TX_ENABLE_EVENT_TRACE ile Azure RTOS ThreadX ve Azure RTOS NetX Duo kitaplıkları oluşturup izleme arabelleği bilgileriyle tx_trace_enable çağırarak gerçekleştirilir.
