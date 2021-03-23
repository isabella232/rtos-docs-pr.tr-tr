---
title: Microsoft Azure RTOS nedir?
description: Azure RTOS, mikro denetleyici birimleri (MCUs) tarafından desteklenen IoT ve Edge cihazları için gerçek zamanlı bir işletim sistemidir (RTOS).
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 3b1c63135f6069652d7f66fc976b9d770a4dfeb2
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826597"
---
# <a name="what-is-microsoft-azure-rtos"></a>Microsoft Azure RTOS nedir?

Azure RTOS, mikro denetleyici birimleri (MCUs) tarafından desteklenen IoT ve Edge cihazları için gerçek zamanlı bir işletim sistemidir (RTOS). Azure RTOS, en yüksek düzeyde kısıtlanmış cihazları desteklemek için tasarlanmıştır (pil gücüyle ve 64 KB 'den az Flash belleği vardır).
 
Azure RTOS, çeşitli güvenlik standartları için önceden sertifikalandırilmiştir. Bunlar, ıEC 61508 SIL 4, ıEC 62304 Class C ve ISO 26262 asıl D sertifikalarını içerir. Azure RTOS ThreadX de DO-178 sertifikalıdır.

Azure RTOS, TLS ve DTLS aracılığıyla IPSec ve yuva katmanı güvenliği aracılığıyla tam IP katmanı güvenliği de dahil olmak üzere, EAL4 + ortak ölçütlere sahip güvenlik sertifikalı bir ortam sağlar. Yazılım şifreleme kitaplığımız FIPS 140-2 sertifikası elde etti. Ayrıca, donanım şifreleme özellikleri, ThreadX MODÜLLERI ile bellek koruması ve ARM 'nin TrustZone ARMv8-msecurity özellikleri için destek de faydalanır.

## <a name="components-of-azure-rtos"></a>Azure RTOS bileşenleri

Azure RTOS platformu, Azure RTOS ThreadX, Azure RTOS FileX, Azure RTOS Gux, Azure RTOS NetX, Azure RTOS NetX Duo ve Azure RTOS USBX gibi çalışma zamanı çözümlerinin koleksiyonudur.

### <a name="azure-rtos-threadx"></a>Azure RTOS ThreadX

Azure RTOS ThreadX, özellikle sağlam bir şekilde eklenmiş uygulamalar için tasarlanan gelişmiş bir Gerçek Zamanlı İşletim Sistemidir (RTOS). Azure RTOS ThreadX 'in sunduğu birçok avantaj arasında gelişmiş zamanlama olanakları, ileti geçirme, kesme yönetimi ve mesajlaşma hizmetleri sağlanmaktadır. Azure RTOS ThreadX, picokernel mimarisi, önalım-Threshold zamanlaması, olay zincirleme ve zengin bir sistem hizmeti kümesi gibi birçok gelişmiş özelliğe sahiptir.

### <a name="azure-rtos-filex"></a>Azure RTOS FileX

Azure RTOS FileX, yüksek performanslı bir FAT uyumlu dosya sistemidir. Azure RTOS ThreadX ile tamamen tümleşiktir ve desteklenen tüm işlemciler için kullanılabilir. Azure RTOS ThreadX gibi Azure RTOS FileX, küçük bir kaplama ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da dosya işlemleri gerektiren, günümüzün derin eklenmiş uygulamalar için ideal hale getirir. Azure RTOS FileX, Azure RTOS LevelX aracılığıyla RAM disk, USBX, SD kartı ve nve/veya Flash anıları dahil olmak üzere çoğu fiziksel medyayı destekler.

### <a name="azure-rtos-guix"></a>Azure RTOS GUIX

Azure RTOS Gux, katıştırılmış sistem geliştiricilerin ihtiyaçlarını karşılamak üzere oluşturulan, profesyonel kalitede bir grafik kullanıcı arabirimi paketidir. Alternatiflerden farklı olarak, Azure RTOS Gux küçük, hızlı ve grafiksel çıktıyı destekleyebilen neredeyse her türlü donanım yapılandırmasına kolayca eklenir. Azure RTOS Gux Ayrıca, uygulama düzeyinde kullanıcı arabirimi geliştirmesi için olağanüstü bir görsel bakış ve sezgisel ve güçlü bir API sunar.

### <a name="azure-rtos-netx"></a>Azure RTOS NetX

Azure RTOS NetX, TCP/IP protokol standartlarının yüksek performanslı bir uygulamasıdır. Azure RTOS ThreadX ile tamamen tümleşiktir ve desteklenen tüm işlemciler için kullanılabilir. Azure RTOS NetX 'in benzersiz bir piconet mimarisi vardır. Sıfır kopyalama API 'siyle birlikte kullanıldığında, bu, ağ bağlantısı gerektiren son derece eklenmiş uygulamalar için mükemmel bir uyum sağlar.

### <a name="azure-rtos-netx-duo"></a>Azure RTOS NetX Duo

Azure RTOS NetX Duo, özellikle de gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, gelişmiş, endüstriyel bir TCP/IP ağı yığınlarıdır. Azure RTOS NetX Duo, iki IPv4 ve IPv6 ağ yığınıdır. NetX, temel olarak Azure RTOS NetX Duo bir alt kümesi olan özgün IPv4 ağ yığınıdır.

### <a name="azure-rtos-usbx"></a>Azure RTOS USBX

Azure RTOS USBX, yüksek performanslı bir USB ana bilgisayar, cihaz ve-go (OTG) katıştırılmış Stack 'tir. ThreadX ile tamamen tümleşiktir ve tüm Azure RTOS ThreadX desteklenen işlemcilerde kullanılabilir. Azure RTOS ThreadX gibi Azure RTOS USBX, küçük bir parmak izi ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da USB cihazlarıyla bir arabirim gerektiren çok sayıda gömülü uygulama için idealdir.

### <a name="windows-tools"></a>Windows araçları

Azure RTOS Gux Studio, uygulamanın GUI 'si içindeki tüm grafik öğelerinin oluşturulmasını ve bakımını kolaylaştırmanın yanı sıra, tümüyle bir GUI uygulama tasarım ortamı sağlar. Azure RTOS Gux Studio otomatik olarak Azure RTOS Gux kitaplığı ile uyumlu C kodu oluşturur ve hedefte derlenmeye ve çalıştırılmaya çalışır.

Azure RTOS TraceX, geliştiricilere gerçek zamanlı sistem olaylarının grafik bir görünümünü sağlayan ve gerçek zamanlı sistemlerinin davranışını görselleştirmesini ve daha iyi anlamasına olanak tanıyan ana bilgisayar tabanlı bir analiz aracıdır.

## <a name="in-the-context-of-azure-iot"></a>Azure IoT bağlamında

Azure IoT 'ye doğrudan bağlanmayı veya Azure IoT Edge aracılığıyla dolaylı olarak bağlamayı ek olarak, Azure RTOS Azure Sphere cihazlarda da kullanılabilir. Azure RTOS ve Azure Sphere birleşimi, tek bir cihazda sınıf gerçek zamanlı işleme ve güvenliği birlikte getirir.
