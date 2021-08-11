---
title: Bölüm 1 - AZURE RTOS USBX Cihaz Yığınına Giriş
description: USBX, derinden eklenmiş uygulamalar için tam özellikli bir USB yığınıdır. Bu bölümde USBX tanıtarak avantajlarını ve uygulamasını anlatabilirsiniz.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 0ec49e88c8dcb8ca200bc376da2f33eb5ddac340bf3693368dc3508f68220765
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791474"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-device-stack"></a>Bölüm 1 - AZURE RTOS USBX Cihaz Yığınına Giriş

USBX, derinden eklenmiş uygulamalar için tam özellikli bir USB yığınıdır. Bu bölümde, uygulamalarını ve avantajlarını açıklayan USBX tanıtılmalı 

## <a name="usbx-features"></a>USBX özellikleri

USBX, mevcut üç USB belirtimlerini destekler: 1.1, 2.0 ve OTG. Ölçeklenebilir olacak şekilde tasarlanmıştır ve yalnızca bir bağlı cihaza sahip basit USB topolojilerini ve birden çok cihaz ve basamaklı hub'lar içeren karmaşık topolojileri barındıracak. USBX, USB protokollerinin tüm veri aktarımı türlerini destekler: denetim, toplu, kesme ve zaman uyumsuz.

USBX hem konak tarafını hem de cihaz tarafını destekler. Her taraf üç katmandan oluşur.

- Denetleyici katmanı
- Yığın katmanı
- Sınıf katmanı

USB katmanları arasındaki ilişki aşağıdaki gibidir:

![USB katmanları](media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a>Ürün Öne Çıkanları

- Tam ThreadX işlemci desteği
- Telif yok
- ANSI C kaynak kodunu tamamlama
- Gerçek zamanlı performans
- Yanıt veren teknik destek
- Birden çok sınıf desteği
- Birden çok sınıf örneği
- ThreadX, FileX ve NetX ile sınıfların tümleştirmesi
- Birden çok yapılandırmaya sahip USB cihazları için destek
- USB bileşik cihazları için destek
- USB güç yönetimi desteği
- USB OTG desteği
- TraceX için izleme olaylarını dışarı aktarma

## <a name="powerful-services-of-usbx"></a>USBX'in Güçlü Hizmetleri

### <a name="complete-usb-device-framework-support"></a>Tam USB Cihaz Çerçevesi Desteği

USBX, birden çok yapılandırma, birden çok arabirim ve birden çok alternatif ayar dahil olmak üzere en zorlu USB cihazlarını desteklemektedir.

### <a name="easy-to-use-apis"></a>Kullanımı Kolay API'ler

USBX, kolay anlaşılır ve kullanımı kolay bir şekilde en iyi şekilde eklenmiş USB yığınını sağlar. USBX API'si hizmetleri sezgisel ve tutarlı hale getirir. Sağlanan USBX sınıf API'lerini kullanarak, kullanıcı uygulamasının USB protokollerinin karmaşıklığını anlayacaktır.
