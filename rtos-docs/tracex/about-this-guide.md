---
title: Azure RTOS TraceX Kullanıcı Kılavuzu
description: bu kılavuz, microsoft 'un microsoft Windows tabanlı sistem analizi aracı olan Azure rtos tracex hakkında kapsamlı bilgiler içerir.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 89a39112d6fc6d231408179ebb3867c21f927326930a1610529b142aa71a1027
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784079"
---
# <a name="about-this-guide"></a>Bu kılavuz hakkında

bu kılavuz, Microsoft Azure rtos için Microsoft Windows tabanlı sistem analizi aracı olan Azure rtos tracex hakkında kapsamlı bilgiler içerir.

Azure RTOS ThreadX Real-Time Işletim sistemi (RTOS) ve eklenti bileşenleri kullanılarak eklenmiş gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştirici standart Azure RTOS ThreadX Azure RTOS FileX ve Azure RTOS NetX kavramlarını tanımanız gerekir.

## <a name="organization"></a>Kuruluş

- [Bölüm 1](chapter1.md) -Azure RTOS tracex 'a yönelik temel bir genel bakış içerir ve gerçek zamanlı geliştirmeyle ilişkilerini açıklar.
- [Bölüm 2](chapter2.md) -uygulamanızı doğrudan kutudan çözümlemek için Azure RTOS tracex 'i yüklemek ve kullanmak üzere temel adımları sağlar.
- [Bölüm 3](chapter3.md) -Azure RTOS tracex 'nin ana özelliklerini açıklar.
- [Bölüm 4](chapter4.md) -Azure RTOS tracex 'in performans analizi özellikleri hakkında bilgi.
- [Bölüm 5](chapter5.md) -Azure RTOS tracex tarafından görüntülenebilen bir izleme arabelleği oluşturmak için Azure RTOS threadx, Azure RTOS FileX ve Azure RTOS NETX 'in nasıl ayarlanacağını açıklar.
- [Bölüm 6](chapter6.md) -Azure RTOS tracex olaylarını ayrıntılı olarak açıklar.
- [Bölüm 7](chapter7.md) -Azure RTOS FileX olaylarını ayrıntılı olarak açıklar.
- [Bölüm 8](chapter8.md) -Azure RTOS NETX olaylarını ayrıntılı olarak açıklar.
- [Bölüm 9](chapter9.md) -Azure RTOS USBX olaylarını ayrıntılı olarak açıklar.
- [Bölüm 10](chapter10.md) -özel Kullanıcı olaylarının ayrıntılı olarak oluşturulmasını açıklar.
- [Bölüm 11](chapter11.md) -iç izleme arabelleğini ayrıntılı olarak açıklar.
- [Ek A](appendix-a.md) -Azure RTOS threadx bağlantı noktasına özgü bir dosya, izleme olaylarını toplamak için zaman damgası kaynağıdır.
- [Ek B](appendix-b.md) -Azure RTOS threadx *tx_trace. h* dosyası olay izleme arabelleği ile ilgili uygulama ayrıntılarını gösterir.
- [Ek C](appendix-c.md) -çeşitli dosya biçimlerini uygun Azure RTOS tracex ikili dosyalarına dönüştürmek için komut satırı yardımcı programlarını özetler.
- [Ek D](appendix-d.md) -çeşitli geliştirme araçlarından izleme dosyalarını dökme örnekleri.

## <a name="guide-conventions"></a>Kılavuz kuralları

*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.

**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.

> [!NOTE]
> Notun bilgilerini gösterir.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.
2. Uygulamada ve/veya Azure RTOS ThreadX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.
3. *_Tx_version_id* dizesinin içeriği, dağılımının *tx_port. h* dosyasında bulunur. Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.
4. *_Tx_build_options* ulong değişkeninin RAM 'e ait içerik. Bu değişken, Azure RTOS ThreadX Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.
