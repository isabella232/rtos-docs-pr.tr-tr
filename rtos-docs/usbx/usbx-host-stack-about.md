---
title: Azure RTOS USBX Konak Yığını Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft'un Azure RTOS USB foundation yazılımı olan USBX hakkında kapsamlı bilgi sağlar.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: a41f1b386156be6f8fa773fe2b90bb873cff0fd0e8636bc4d3d8f75295bf7f19
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802558"
---
# <a name="azure-rtos-usbx-host-stack-user-guide"></a>Azure RTOS USBX Konak Yığını Kullanıcı Kılavuzu

Bu kılavuz, Microsoft'un Azure RTOS USB foundation yazılımı olan USBX hakkında kapsamlı bilgi sağlar.

Eklenmiş gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştiricinin standart gerçek zamanlı işletim sistemi işlevleri, USB belirtimi ve C programlama dili hakkında bilgi sahibi olması gerekir.

USB ile ilgili teknik bilgiler için bkz. şu bağlantıda indirilebilen USB belirtimi ve USB Sınıfı belirtimleri: [https://www.USB.org/developers](https://www.USB.org/developers)

## <a name="organization"></a>Kuruluş

- [**Bölüm 1**](usbx-host-stack-1.md) - USBX'e Azure RTOS içerir

- [**2.**](usbx-host-stack-2.md) Bölüm : Azure RTOS ThreadX uygulamanıza USBX'Azure RTOS i yüklemek ve kullanmak için Azure RTOS adımlarını verir

- [**Bölüm 3**](usbx-host-stack-3.md) - USBX ile ilgili Azure RTOS genel bakış ve USB hakkında temel bilgiler sağlar

- [**Bölüm 4**](usbx-host-stack-4.md) - USBX'i konak modunda Azure RTOS için uygulama arabiriminin ayrıntılarını içerir

- [**Bölüm 5**](usbx-host-stack-5.md) - USBX Konak sınıflarının Azure RTOS API'lerini açıklar

- [**Bölüm 6**](usbx-host-stack-6.md) - USBX CDC-ECM Azure RTOS sınıfını açıklar

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Buradaki adımları kullanarak sorularınız veya yardım için lütfen Azure Portal üzerinden bir destek bileti gönderin. Destek isteğinizi daha verimli bir şekilde çözüme kavuşturmamızı sağlamak için lütfen aşağıdaki bilgileri bir e-posta iletisinde bize iletin.

1. Oluşma sıklığı ve güvenilir bir şekilde yeniden üretilip üretilileyil olmadığı da dahil olmak üzere sorunun ayrıntılı açıklaması.
2. Uygulamada yapılan değişikliklerin ve/veya sorundan önce Azure RTOS ThreadX'in ayrıntılı açıklaması.
3. Dağıtım dizenizin *_tx_version_id.h* dosyasında *bulunan tx_port* dizenin içeriği. Bu dize, çalışma zamanı ortamınız hakkında değerli bilgiler sağlar.
4. ULONG değişkeninin *RAM'_tx_build_options* içeriği. Bu değişken, iş parçacığı threadx kitaplığınızı Azure RTOS hakkında bilgi sağlar.
