---
title: Azure RTOS USBX Cihaz Yığını Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft'un Azure RTOS usb temel yazılımı olan USBX ile ilgili kapsamlı bilgiler sağlar
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 042398377766a3e73f72d4dbba0478ba707d378a379fd33de7808675eb96f257
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788771"
---
# <a name="azure-rtos-usbx-device-stack-user-guide"></a>Azure RTOS USBX Cihaz Yığını Kullanıcı Kılavuzu

Bu kılavuz, Microsoft'un Azure RTOS USB foundation yazılımı olan USBX hakkında kapsamlı bilgi sağlar.

Eklenmiş gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştiricinin standart gerçek zamanlı işletim sistemi işlevleri, USB belirtimi ve C programlama dili hakkında bilgi sahibi olması gerekir.

USB ile ilgili teknik bilgiler için bkz. şu bağlantıda indirilebilen USB belirtimi ve USB Sınıfı belirtimleri: https://www.USB.org/developers

## <a name="organization"></a>Kuruluş

- [**Bölüm 1**](usbx-device-stack-1.md) - USBX'e Azure RTOS içerir

- [**2.**](usbx-device-stack-2.md) Bölüm: ThreadX uygulamanıza USBX Azure RTOS yüklemek ve kullanmak için temel adımları verir

- [**Bölüm 3**](usbx-device-stack-3.md) - USBX cihaz yığınının Azure RTOS bileşenlerini açıklar

- [**Bölüm 4**](usbx-device-stack-4.md) - USBX cihaz Azure RTOS hizmetlerini açıklama

- [**Bölüm 5**](usbx-device-stack-5.md) - API'leri dahil olmak Azure RTOS USBX cihaz sınıfını açıklar

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Buradaki adımları kullanarak sorularınız veya yardım için lütfen Azure Portal üzerinden bir destek bileti gönderin. Destek isteğinizi daha verimli bir şekilde çözüme kavuşturmamızı sağlamak için lütfen bir e-posta iletisinde aşağıdaki bilgileri bize iletin:

1. Oluşma sıklığı ve güvenilir bir şekilde yeniden üretilip üretilileyil olmadığı da dahil olmak üzere sorunun ayrıntılı açıklaması.
2. Uygulamada yapılan değişikliklerin ve/veya sorundan önce Azure RTOS ThreadX'in ayrıntılı açıklaması.
3. Dağıtım dizenizin **_tx_version_id.h** dosyasında **_bulunan tx_port_** dizenin içeriği. Bu dize, çalışma zamanı ortamınız hakkında değerli bilgiler sağlar.
4. **ULONG** değişkeninin *RAM'_tx_build_options* içeriği. Bu değişken, iş parçacığı threadx kitaplığınızı Azure RTOS hakkında bilgi sağlar.
