---
title: Azure RTOS NetX Kullanıcı Kılavuzu hakkında
description: Bu kılavuz, Microsoft yüksek performanslı ağ yığını olan Azure RTOS NetX hakkında kapsamlı bilgiler içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 01077e3315e87b918cdfd47423d8e0c1b6bbdbbd
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550278"
---
# <a name="about-the-azure-rtos-netx-user-guide"></a>Azure RTOS NetX Kullanıcı Kılavuzu hakkında

Bu kılavuz, Microsoft yüksek performanslı ağ yığını olan Azure RTOS NetX hakkında kapsamlı bilgiler içerir.

Temel ağ kavramlarıyla, Azure RTOS ThreadX ve C programlama diliyle tanıdık olan gömülü gerçek zamanlı yazılım geliştiricileri için tasarlanmıştır.

## <a name="organization"></a>Kuruluş

[Bölüm 1](chapter1.md) -Azure RTOS NETX 'i tanıtır

[Bölüm 2](chapter2.md) -Threadx uygulamanızla Azure RTOS NETX 'i yüklemek ve kullanmak için temel adımları sağlar.

[Bölüm 3](chapter3.md) -Azure RTOS NETX sistemine yönelik işlevsel bir genel bakış ve TCP/IP ağ standartları hakkında temel bilgiler sağlar.

[Bölüm 4](chapter4.md) -uygulamanın Azure RTOS NETX 'e ait arabiriminin ayrıntılarını.

[Bölüm 5](chapter5.md) -Azure RTOS NETX için ağ sürücülerini açıklar.

[Ek A](appendix-a.md) -Azure RTOS NETX Hizmetleri

[Ek B](appendix-b.md) -Azure RTOS NETX sabitleri

[Ek C](appendix-c.md) -Azure RTOS NETX veri türleri

[Ek D](appendix-d.md) -BSD-Compatible yuvası API 'si

[Ek E](appendix-e.md) -ASCII grafik

## <a name="azure-rtos-netx-data-types"></a>Azure RTOS NetX veri türleri

Özel Azure RTOS NetX denetim yapısı veri türlerine ek olarak, Azure RTOS NetX hizmet çağrı arabirimlerinde kullanılan birkaç özel veri türü vardır. Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir. Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır. Tam uygulama ThreadX 'ten devralınır ve ThreadX dağıtımına dahil olan ***tx_port. h*** dosyasında bulunabilir.

Aşağıda, Azure RTOS NetX hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:

| Veri Türleri | Açıklama  |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **U**  | Temel işaretsiz tamsayı. Bu tür 32 bitlik işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir. |
| **'TUR** | İmzasız Long türü. Bu tür 32 bitlik işaretsiz verileri desteklemelidir.                                                                      |
| **Kağıt**  | Derleyicinin void türüne neredeyse her zaman eşdeğerdir.                                                                                 |
| **CHAR**  | Genellikle standart 8 bitlik bir karakter türü.                                                                                           |

Ek veri türleri, Azure RTOS NetX kaynağı içinde kullanılır. Bunlar, ***tx_port. h** _ veya _ *_nx_port. h_** dosyalarında konumlardır.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.

2. Uygulamada ve/veya Azure RTOS NetX üzerinde yapılan tüm değişikliklerin ayrıntılı bir açıklaması.

3. **_Tx_version_id** ve **_nx_version_id** dizelerinin içerikleri, dağılımının **_tx_port. h_*_ ve _*_nx_port. h_** dosyalarında bulunur. Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.

4. Aşağıdaki **ulong** değişkenlerinin RAM 'ine ait içerikler:

    **_tx_build_options**

    **_nx_system_build_options1**

    **_nx_system_build_options2**

    **_nx_system_build_options3**

    **_nx_system_build_options4**

    **_nx_system_build_options5**

    Bu değişkenler, Azure RTOS ThreadX ve Azure RTOS NetX kitaplıklarının nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.

5. Sorun algılandıktan hemen sonra yakalanan bir izleme arabelleği. Bu, **TX_ENABLE_EVENT_TRACE** Ile Azure RTOS threadx ve Azure RTOS NETX kitaplıkları oluşturup izleme arabelleği bilgileriyle **tx_trace_enable** çağırarak yapılır. Ayrıntılar için Azure RTOS TraceX Kullanıcı kılavuzuna bakın.
