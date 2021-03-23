---
title: Bu Kılavuz Hakkında
description: Bu kılavuzda, Azure RTOS ThreadX SMP, Microsoft yüksek performanslı gömülü gerçek zamanlı çekirdek hakkında kapsamlı bilgiler sağlanmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2399666b5b4d7c34db50d539e200c90f06f7235f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825445"
---
# <a name="about-this-guide"></a>Bu Kılavuz Hakkında

Bu kılavuzda, Azure RTOS ThreadX SMP, Microsoft yüksek performanslı gömülü gerçek zamanlı çekirdek hakkında kapsamlı bilgiler sağlanmaktadır.

Katıştırılmış gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştirici standart gerçek zamanlı işletim sistemi işlevleri ve C programlama diliyle tanıdık gelmelidir.

## <a name="organization"></a>Kuruluş

| Ele       | Genel Bakış                    |
| ------------- | ---------------------------------------------------------------------------------------------------------- |
| **Bölüm 1** | ThreadX SMP ve gerçek zamanlı gömülü geliştirmeyle ilişkisi için temel bir genel bakış sağlar.           |
| **Bölüm 2** | , Uygulamanıza yönelik olarak ThreadX SMP 'yi yüklemek ve kullanmak için temel adımları sağlar *.*           |
| **Bölüm 3** | Yüksek performanslı gerçek zamanlı SMP çekirdeği olan ThreadX SMP 'nin işlevsel işleminde ayrıntılı olarak açıklanmaktadır.    |
| **Bölüm 4** | Uygulamanın ThreadX SMP arabirimine ayrıntılarını sağlar.                                                        |
| **Bölüm 5** | ThreadX SMP uygulamaları için g/ç sürücüleri yazmayı açıklar.                                                |
| **Bölüm 6** | Her ThreadX SMP işlemci desteği paketiyle birlikte sunulan tanıtım uygulamasını açıklar. |
| **Ek A** | ThreadX SMP API 'SI        |
| **Ek B** | ThreadX SMP sabitleri  |
| **Ek C** | ThreadX SMP veri türleri |
| **Ek D** | ASCII grafik            |

## <a name="guide-conventions"></a>Kılavuz kuralları

- *İtalik*  -  *yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.*
- **Kalýn**  -  **yazı tipi dosya adlarını, anahtar sözcükleri gösterir ve önemli sözcükleri ve değişkenleri vurgular.**

> [!IMPORTANT]
> Bilgi sembolleri, performansı veya işlevi etkileyebilecek önemli veya ek bilgilere dikkat çekecek.

> [!WARNING]
> Uyarı sembolleri, geliştiricilerin önemli hatalara neden olabileceğinden kaçınmak için dikkatli olması gereken durumlara dikkat çekecek.

## <a name="threadx-smp-data-types"></a>ThreadX SMP veri türleri

Özel ThreadX SMP denetim yapısı veri türlerine ek olarak, ThreadX SMP hizmeti çağrı arabirimlerinde kullanılan bir dizi özel veri türü vardır. Bu özel veri türleri, temel alınan C derleyicisinin veri türleriyle doğrudan eşlenir. Bu, farklı C derleyicileri arasında taşınabilirliği sağlamak için yapılır. Tam uygulama, dağıtım diskine dahil olan ***tx_port. h*** dosyasında bulunabilir.

Aşağıda, ThreadX SMP hizmeti çağrı veri türleri ve bunlarla ilişkili anlamlarıyla ilgili bir liste verilmiştir:

| Veri Türü          | Anlamı                                                          |
| --------- | --------------------------------------------------------- |
| **U**  | Temel işaretsiz tamsayı. Bu tür 8 bit işaretsiz verileri desteklemelidir; Ancak, en uygun imzasız veri türüne eşlenir. |
| **'TUR** | İmzasız Long türü. Bu tür 32 bitlik işaretsiz verileri desteklemelidir.                                                                     |
| **Kağıt**  | Derleyicinin void türüne neredeyse her zaman eşdeğerdir.                                                                                |
| **CHAR**  | Genellikle standart 8 bitlik bir karakter türü.                                                                                          |

Ek veri türleri, ThreadX SMP kaynağı içinde kullanılır. Bunlar ayrıca ***tx_port. h*** dosyasında bulunur.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Destek e-postası: [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) Web sayfası: Azure.com/RTOS

### <a name="latest-product-information"></a>En son ürün bilgileri

Azure.com/rtos Web sitesini ziyaret edin ve en son ThreadX SMP ürün sürümleri hakkında bilgiler de dahil olmak üzere en son çevrimiçi destek bilgilerini bulmak için "destek" menü seçeneğini belirleyin.

### <a name="what-we-need-from-you"></a>Sizin için gerekenler

Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.
2. Uygulamanın ve/veya ThreadX SMP değişikliklerinin bundan önce sorunun ayrıntılı bir açıklaması.
3. ***_Tx_version_id** _ dizesinin içeriği, dağılımının _ *_tx_port. h_** dosyasında bulunur. Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.
4. ***_Tx_build_options*** ulong değişkeninin RAM 'e ait içerik. Bu değişken, ThreadX SMP Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.

### <a name="where-to-send-comments-about-this-guide"></a>Bu kılavuzla Ilgili yorumların nereye gönderileceği

[azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com)Konu satırına "ThreadX SMP Kullanıcı Kılavuzu" yazın ve müşteri destek merkezi 'ndeki tüm yorumları ve önerileri e-posta ile yapın.
