---
title: Azure RTOS GUIX Kullanıcı Kılavuzu
description: Bu kılavuzda, Microsoft 'un yüksek performanslı GUI ürünü olan Azure RTOS Gux hakkında kapsamlı bilgiler yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: b7af0fba59b599c9c8db3ab80a3271eacfd11992
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827292"
---
# <a name="about-guix-user-guide"></a>GUX Kullanıcı Kılavuzu hakkında

Bu kılavuzda, Microsoft 'un yüksek performanslı GUI ürünü olan Azure RTOS Gux hakkında kapsamlı bilgiler yer almaktadır. Temel GUI kavramlarını, Azure RTOS ThreadX ve C programlama dilini bilen, yerleşik gerçek zamanlı yazılım geliştiricileri için tasarlanmıştır.

## <a name="organization"></a>Kuruluş

[Bölüm 1-Azure RTOS Gux 'e giriş](chapter-1.md)

[Bölüm 2-Azure RTOS Gux 'i yükleme ve kullanma](chapter-2.md)

[Bölüm 3-Azure RTOS Gux 'e Işlevsel genel bakış](chapter-3.md)

[Bölüm 4-Azure RTOS GUıDX hizmetlerinin açıklaması](chapter-4.md)

[Bölüm 5-Azure RTOS Gux görüntüleme sürücüleri](chapter-5.md)  

[Azure RTOS Gux örneği](guix-example.md)

[Ek A-Azure RTOS Gux renk tanımları](appendix-a.md)

[Ek B-Azure RTOS Gux renk biçimleri](appendix-b.md)

[Ek C-Azure RTOS Gux pencere öğesi stilleri](appendix-c.md)

[Ek D-Azure RTOS Gux fırçası, tuval ve gradyan öznitelikleri](appendix-d.md)

[Ek E-Azure RTOS Gux olay açıklaması](appendix-e.md)

[Ek F-Azure RTOS Gux RTOS bağlama hizmetleri](appendix-f.md)

[Ek G-Azure RTOS Gux yazı tipi yapısı](appendix-g.md)

[Ek H-Azure RTOS Gux Build-Time yapılandırma bayrakları](appendix-h.md)

[Ek ı-Azure RTOS Gux bilgi yapıları](appendix-i.md)

## <a name="guide-conventions"></a>Kılavuz kuralları

*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.

**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.

> [!IMPORTANT]
> Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.

## <a name="azure-rtos-guix-data-types"></a>Azure RTOS Gux veri türleri

Özel Azure RTOS Gux denetim yapısı veri türlerine ek olarak, Azure RTOS Gux hizmet çağrı arabirimlerinde kullanılan birkaç özel veri türü vardır. Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir. Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır. Tam uygulama ThreadX 'ten devralınır ve ThreadX dağıtımına dahil olan ***tx_port. h*** dosyasında bulunabilir.

Aşağıda, Azure RTOS Gux hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:

| <!-- --> | <!-- --> |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **U**             | Temel işaretsiz tamsayı. Bu tür, en uygun imzasız veri türüyle eşlenir.                                |
| **INT**              | Temel işaretli tamsayı. Bu tür, en uygun imzalı veri türüyle eşlenir.                                    |
| **'TUR**            | İmzasız Long türü. Bu tür 32 bitlik işaretsiz verileri desteklemelidir.                                                      |
| **Kağıt**             | Derleyicinin void türüne neredeyse her zaman eşdeğerdir.                                                                 |
| **GX_CHAR**         | En yaygın olarak, derleyici tarafından tanımlanan char türü olarak yazın.                                                               |
| **GX_BYTE**          | 8 bit imzalı tür.                                                                                                    |
| **GX_UBYTE**         | 8 bit işaretsiz tür.                                                                                                  |
| **GX_VALUE**        | 16 veya 32 bit imzalı tür. Hedef sistemde en iyi performans için gereken şekilde tanımlanır.                                |
| **GX_FIXED_VAL**   | Sabit noktalı sayısal veri türü.                                                                                        |
| **GX_RESOURCE_ID** | İmzasız Long türü.                                                                                                   |
| **GX_COLOR**        | İmzasız Long türü.                                                                                                   |
| **GX_STRING**       | GX_CHAR \* gx_string_ptr ve UINT gx_string_length içeren yapı.                                          |
| **GX_POINT**        | Gx_point_x ve gx_point_y içeren yapı.                                                                   |
| **GX_RECTANGLE**    | Gx_rectangle_left, gx_rectangle_top, gx_rectangle_right ve gx_rectangle_bottom alanları içeren yapı. |
| **GX_GLYPH**        | Glif ölçümleri içeren yapı.                                                                                   |
| **GX_FONT**         | Yazı tipi ölçümlerini içeren yapı.                                                                                    |
| **GX_BRUSH**        | Fırça ölçümlerini içeren yapı.                                                                               |
**GX_PIXELMAP**       | Pixelmap ölçümlerini içeren yapı.

Ek veri türleri, Azure RTOS Gux kaynağı içinde kullanılır. Bunlar, ***tx_port. h** _ veya _ *_gx_port. h_** dosyalarında konumlardır.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.

2. Uygulamada ve/veya Azure RTOS Gux ' te yapılan tüm değişikliklerin ayrıntılı bir açıklaması.

3. _Tx_version_id ve gx_version_id dizelerinin içeriği, _**tx_port. h**_ ve _ *_gx_port. h_**, dağıtım dosyalarınızın dosyalarında bulunur. Bu dizeler, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.

4. Aşağıdaki ULONG değişkenlerinin RAM 'ine ait içerikler:

    **_tx_build_options** **_gx_system_build_options**

    Bu değişkenler, Azure RTOS ThreadX ve Azure RTOS Gux kitaplıklarının nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.

5. Aşağıdaki ULONG değişkenlerinin RAM 'ine ait içerikler:

    **_gx_system_last_error** **_gx_system_error_count**

    Bu değişkenler, Azure RTOS Gux 'teki iç sistem hatalarını izler. _Gx_system_error_count sıfırdan büyükse, lütfen _gx_system_error_process işlevinde döndürülen işlev için bir kesme noktası ayarlayın ve bu noktada _gx_system_last_error değerini sağlayın. Bu, birinci iç Azure RTOS Gux sistem hatasını verir.

6. Sorun algılandıktan hemen sonra yakalanan bir izleme arabelleği. Bu, TX_ENABLE_EVENT_TRACE ile Azure RTOS ThreadX ve Azure RTOS Gux kitaplıkları oluşturup izleme arabelleği bilgileriyle tx_trace_enable çağırarak gerçekleştirilir.

7. Kullandığınız Azure RTOS Gux Studio projesi, varsa veya en düşük bir proje rapor ettiğiniz eksiklikleri göstermek için yeterlidir.
