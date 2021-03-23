---
title: Azure RTOS TraceX Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un Microsoft Windows tabanlı Sistem Analizi Aracı olan Azure RTOS TraceX hakkında kapsamlı bilgiler içerir.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 92d886b19a0c67292cd4f6a5f8bd7f9d3106374b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827869"
---
# <a name="about-this-guide"></a>Bu kılavuz hakkında

Bu kılavuz, Microsoft Azure RTOS için Microsoft Windows tabanlı Sistem Analizi Aracı olan Azure RTOS TraceX hakkında kapsamlı bilgiler içerir.

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
