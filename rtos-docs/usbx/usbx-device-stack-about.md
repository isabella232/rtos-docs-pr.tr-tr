---
title: Azure RTOS USBX cihaz yığını Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un yüksek performanslı USB Foundation yazılımı olan Azure RTOS USBX hakkında kapsamlı bilgiler sağlar
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: c8e9360c8b72adbc41f840a48e333668c489399e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825427"
---
# <a name="azure-rtos-usbx-device-stack-user-guide"></a>Azure RTOS USBX cihaz yığını Kullanıcı Kılavuzu

Bu kılavuz, Microsoft 'un yüksek performanslı USB Foundation yazılımı olan Azure RTOS USBX hakkında kapsamlı bilgiler sağlar.

Katıştırılmış gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştirici standart gerçek zamanlı işletim sistemi işlevleriyle, USB belirtimine ve C programlama diline tanıdık gelmelidir.

USB ile ilgili teknik bilgiler için, bkz. indirilebilecek USB belirtimi ve USB sınıfı belirtimleri https://www.USB.org/developers

## <a name="organization"></a>Kuruluş

- [**Bölüm 1**](usbx-device-stack-1.md) -Azure RTOS USBX 'e giriş içerir

- [**Bölüm 2**](usbx-device-stack-2.md) -Azure RTOS USBX 'ı threadx uygulamanızla birlikte yüklemek ve kullanmak için temel adımları sağlar

- [**Bölüm 3**](usbx-device-stack-3.md) -Azure RTOS USBX cihaz yığınının işlevsel bileşenlerini açıklar

- [**Bölüm 4**](usbx-device-stack-4.md) -Azure RTOS USBX cihaz yığını hizmetlerini açıklar

- [**Bölüm 5**](usbx-device-stack-5.md) -API 'leri dahil olmak üzere her BIR Azure RTOS USBX cihaz sınıfını açıklar

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.
2. Uygulamada ve/veya Azure RTOS ThreadX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.
3. **_Tx_version_id** dizesinin içeriği, dağılımının **_tx_port. h_** dosyasında bulunur. Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.
4. *_Tx_build_options* **ulong** değişkeninin RAM 'e ait içerik. Bu değişken, Azure RTOS ThreadX Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.
