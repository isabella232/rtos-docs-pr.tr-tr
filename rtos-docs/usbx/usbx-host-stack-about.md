---
title: Azure RTOS USBX konak yığını Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un yüksek performanslı USB Foundation yazılımı olan Azure RTOS USBX hakkında kapsamlı bilgiler sağlar.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 243b12c4757ee945def8fea01c0d4114e39312ce
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827329"
---
# <a name="azure-rtos-usbx-host-stack-user-guide"></a>Azure RTOS USBX konak yığını Kullanıcı Kılavuzu

Bu kılavuz, Microsoft 'un yüksek performanslı USB Foundation yazılımı olan Azure RTOS USBX hakkında kapsamlı bilgiler sağlar.

Katıştırılmış gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştirici standart gerçek zamanlı işletim sistemi işlevleriyle, USB belirtimine ve C programlama diline tanıdık gelmelidir.

USB ile ilgili teknik bilgiler için, bkz. indirilebilecek USB belirtimi ve USB sınıfı belirtimleri [https://www.USB.org/developers](https://www.USB.org/developers)

## <a name="organization"></a>Kuruluş

- [**Bölüm 1**](usbx-host-stack-1.md) -Azure RTOS USBX 'e giriş içerir

- [**Bölüm 2**](usbx-host-stack-2.md) -Azure RTOS Threadx uygulamanızla Azure RTOS USBX 'i yüklemek ve kullanmak için temel adımları sağlar

- [**Bölüm 3**](usbx-host-stack-3.md) -Azure RTOS USBX ve USB hakkında temel bilgiler için işlevsel bir genel bakış sağlar

- [**Bölüm 4**](usbx-host-stack-4.md) -ana bilgisayar modunda uygulamanın Azure RTOS USBX 'e yönelik arabirimine Ayrıntılar

- [**Bölüm 5**](usbx-host-stack-5.md) -Azure RTOS USBX konak sınıflarının API 'lerini açıklar

- [**Bölüm 6**](usbx-host-stack-6.md) -Azure RTOS USBX CDC-ECD sınıfını açıklar

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin. Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin.

1. Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.
2. Uygulamada ve/veya Azure RTOS ThreadX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.
3. *_Tx_version_id* dizesinin içeriği, dağılımının *tx_port. h* dosyasında bulunur. Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.
4. *_Tx_build_options* ulong değişkeninin RAM 'e ait içerik. Bu değişken, Azure RTOS ThreadX Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.
