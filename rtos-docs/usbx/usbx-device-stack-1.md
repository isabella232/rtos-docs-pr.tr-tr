---
title: Bölüm 1-Azure RTOS USBX cihaz yığınına giriş
description: Bu bölümde, uygulamaları ve avantajları açıklanarak USBX cihaz yığını tanıtılmaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 383651bb0af42842329ad15b212e597f63a916aa
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377076"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-device-stack"></a>Bölüm 1-Azure RTOS USBX cihaz yığınına giriş

USBX, derin eklenmiş uygulamalar için tam özellikli bir USB yığınıdır. Bu bölümde, uygulamaları ve avantajları açıklanarak USBX tanıtılmaktadır 

## <a name="usbx-features"></a>USBX özellikleri

USBX var olan üç USB belirtimini destekler: 1,1, 2,0 ve OTG. Ölçeklenebilir olacak şekilde tasarlanmıştır ve tek bir bağlı cihazla basit USB Topolojilerine ve birden çok cihaz ve basamaklı hub 'lara sahip karmaşık topolojilerle uyum sağlar. USBX, USB protokollerinin tüm veri aktarımı türlerini destekler: denetim, toplu, kesme ve zaman aralıklı.

USBX hem ana bilgisayar tarafını hem de cihaz tarafını destekler. Her bir kenar üç katmandan oluşur.

- Denetleyici katmanı
- Yığın katmanı
- Sınıf katmanı

USB katmanları arasındaki ilişki aşağıdaki gibidir:

![USB katmanları](media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a>Ürün vurguları

- Tüm ThreadX işlemci desteğini
- Hiçbir çatı yok
- Tamamen ANSI C kaynak kodu
- Gerçek zamanlı performans
- Yanıt veren teknik destek
- Birden çok sınıf desteği
- Birden çok sınıf örneği
- ThreadX, FileX ve NetX ile sınıfların tümleştirilmesi
- Birden çok yapılandırmaya sahip USB cihazları için destek
- USB Bileşik cihazları için destek
- USB güç yönetimi desteği
- USB OTG desteği
- Trackingex için izleme olaylarını dışarı aktarma

## <a name="powerful-services-of-usbx"></a>USBX güçlü Hizmetleri

### <a name="complete-usb-device-framework-support"></a>Tüm USB cihaz çerçevesi desteğini

USBX, birden çok yapılandırma, birden çok arabirim ve birden çok farklı ayar dahil olmak üzere en zorlu USB cihazlarını destekleyebilir.

### <a name="easy-to-use-apis"></a>Kullanımı kolay API 'Ler

USBX, anlaşılması ve kullanılması kolay bir şekilde, en iyi şekilde gömülü USB yığınını sağlar. USBX API 'SI, Hizmetleri sezgisel ve tutarlı hale getirir. Belirtilen USBX sınıfı API 'Lerini kullanarak, Kullanıcı uygulamasının USB protokollerinin karmaşıklığını anlaması gerekmez.
