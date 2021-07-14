---
title: USBX Azure RTOS anlama
description: Azure RTOS USBX yüksek performanslı bir USB ana bilgisayar, cihaz ve devam ediyor (OTG) tümleşik yığınıdır. Azure RTOS USBX, Azure RTOS ThreadX ile tamamen tümleşiktir ve tüm Azure RTOS ThreadX tarafından desteklenen işlemciler için kullanılabilir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 3c214a49f7dd1af20c20f07412fb072dd785b16f
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754837"
---
# <a name="overview-of-azure-rtos-usbx"></a>AZURE RTOS USBX'e genel bakış

Azure RTOS USBX, yüksek performanslı bir USB ana bilgisayarı, cihaz ve devam ediyor (OTG) tümleşik yığınıdır. Azure RTOS USBX, Azure RTOS ThreadX ile tamamen tümleşiktir ve ThreadX tarafından desteklenen tüm işlemciler için kullanılabilir. ThreadX gibi, Azure RTOS USBX de küçük bir ayak izine ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da USB cihazlarıyla arabirim gerektiren derin tümleşik uygulamalar için idealdir.

## <a name="host-device-otg--extensive-class-support"></a>Konak, Cihaz, OTG & Kapsamlı Sınıf Desteği

Azure RTOS USBX Ana Bilgisayarı/Cihaz tümleşik USB protokol yığını, derinden gömülü, gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanmış endüstriyel sınıf bir tümleşik USB çözümüdür. Azure RTOS USBX, konak, cihaz ve OTG desteğinin yanı sıra kapsamlı sınıf desteği sağlar. Azure RTOS USBX, ThreadX Real-Time İşletim Sistemi, Azure RTOS FileX embedded FAT uyumlu dosya sistemi, Azure RTOS NetX ve Azure RTOS NetX Duo ekli TCP/IP yığınları ile tamamen tümleşiktir. Bunların hepsi son derece küçük bir ayak izi, hızlı yürütme ve üstün kullanım kolaylığı ile birlikte, Azure RTOS USBX'i USB bağlantısı gerektiren en zorlu tümleşik IoT uygulamaları için ideal seçenek yapın.

### <a name="usbx-memory-footprint"></a>USBX bellek ayak izi

Azure RTOS USBX, 10,5 KB FLASH ve Azure RTOS USBX Cihazı CDC/ACM desteği için 5,1 KB RAM olmak üzere oldukça küçük bir ayak izine sahip. Azure RTOS USBX Ana Bilgisayarı için CDC/ACM desteği için en az 18 KB FLASH ve 25 KB RAM gerekir.

TCP işlevselliği için 10 KB ile 13 KB arasında yönerge alanı belleği gerekir. Azure RTOS USBX RAM kullanımı genellikle 2,6 KB ile 3,6 KB arasında ve uygulama tarafından tanımlanan paket havuzu belleğidir.

ThreadX'te olduğu gibi, Azure RTOS USBX'in boyutu da uygulama tarafından gerçekten kullanılan hizmetlere göre otomatik olarak ölçeklendirilir. Bu, karmaşık yapılandırma ve derleme parametrelerine olan ihtiyacı neredeyse ortadan kaldırarak geliştirici için işleri kolaylaştırır.

### <a name="usb-interoperability-verification"></a>USB Birlikte Çalışabilirlik doğrulaması

Azure RTOS USBX Cihaz Yığını, USB belirtimleriyle tam uyumluluğu ve farklı konak sistemleriyle birlikte çalışabilirliği sağlamak için USB IF standart test aracı USBCV ile sıkı bir şekilde test edilmiştir.
Ayrıca USBX AZURE RTOS yığını, Tayvan'daki bağımsız test laboratuvarı Allion tarafından doğrulanmış ve onaylanmıştır.

### <a name="usb-host-controller-support"></a>USB Konak denetleyicisi desteği

Azure RTOS USBX, AHCI ve EHCI gibi önemli USB standartlarını destekler. Ayrıca, Azure RTOS USBX; Atmel, Microchip, Yazıcı, Renesas, ST, TI ve diğer satıcılardan özel ayrık USB konak denetleyicilerini destekler. Azure RTOS USBX aynı uygulamada birden çok konak denetleyicisini de destekler.
USB Cihaz denetleyicisi desteği Azure RTOS USBX; Analog Cihazlar, Atmel, Microchip, NXP, Analog, Renesas, ST, TI ve diğer satıcılardan popüler USB cihaz denetleyicilerini destekler.

### <a name="extensive-host-class-support"></a>Kapsamlı Konak Sınıfı desteği

Azure RTOS USBX Ana Bilgisayarı ASIX, AUDIO, CDC/ACM, CDC/ECM, GSER, KEYBOARD (klavye, fare ve uzaktan denetim), HUB, PIMA (PTP/MTP), PRINTER, PROLIFIC ve STORAGE gibi popüler sınıfların çoğu için destek sağlar.

### <a name="extensive-usb-device-class-support"></a>Kapsamlı USB Cihaz Sınıfı desteği

Azure RTOS USBX Cihazı CDC/ACM, CDC/ECM, DFU, GIZLI, PIMA (PTP/MTP) (w/MTP), RNDIS ve STORAGE gibi popüler sınıfların çoğu için destek sağlar. Özel sınıflar için destek de mevcuttur.

### <a name="pictbridge-support"></a>Pictbridge desteği

Azure RTOS USBX, hem konakta hem de cihazda tam Pictbridge uygulamasını destekler. Pictbridge, her iki Azure RTOS USBX PIMA (PTP/MTP) sınıfının üzerinde yer almaktadır. PictBridge standardı, bir dijital hala kamera veya akıllı telefonun bilgisayar olmadan doğrudan yazıcıya bağlantısına olanak sağlayarak, Belirli Pictbridge'e bağlı yazıcılara doğrudan yazdırmayı sağlar. Yazıcıya bir kamera veya telefon bağlandığında yazıcı USB ana bilgisayarı, kamera ise USB cihazıdır. Ancak, Pictbridge ile kamera ana bilgisayar olarak görünür ve komutlar kameradan çalıştırılır. Kamera depolama sunucusu, yazıcı ise depolama istemcisidir. Kamera yazdırma istemcisidir ve yazıcı elbette yazdırma sunucusudur. Pictbridge aktarım katmanı olarak USB kullanır, ancak iletişim protokolü için PTP 'yi (Resim Aktarım Protokolü) kullanır.

### <a name="custom-class-support"></a>Özel sınıf desteği

Azure RTOS USBX Ana Bilgisayarı ve Cihazı özel sınıfları destekler. UsbX dağıtımında örnek bir özel Azure RTOS sağlanır. Bu basit veri pompası sınıfı DPUMP olarak adlandırılan ve özel uygulama sınıfları için model olarak kullanılabilir.
USBX Azure RTOS ve Cihaz için gelişmiş teknoloji özel sınıfları destekler. UsbX dağıtımında örnek bir özel Azure RTOS sağlanır. Azure RTOS USBX, şunları içeren gelişmiş bir teknolojidir:

* Konak, Cihaz ve OTG desteği
* USB düşük, tam ve yüksek hızlı destek
* Otomatik ölçeklendirme
* ThreadX, Azure RTOS FileX ve NetX ile Azure RTOS tümleşiktir
* İsteğe bağlı performans ölçümleri
* Azure RTOS TraceX sistem analizi desteği

## <a name="azure-rtos-usbx-apis"></a>Azure RTOS USBX API'leri

### <a name="azure-rtos-usbx-host-api"></a>Azure RTOS USBX Ana Bilgisayar API'si

USBX Azure RTOS API'si, isim-fiil adlandırma kuralının ardından sezgisel ve tutarlı bir API'dir. Tüm API'ler USBX ux_host_* önde gelen veri noktalarına* sahip olur. Engelleyici API'ler isteğe bağlı iş parçacığı zaman aşımına neden olur.

* ASIX
    - En az 0,3 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'leri şu şekilde sezgiseldir: *ux_host_class_asix_**
* Ses
    - En az 1,2 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_host_class_audio_**
* CDC/ACM
    - En az 1,4 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'leri şu şekilde sezgiseldir: *ux_host_class_cdc_acm_**
* Sakladı
    - En az 0,3 KB FLASH, 4 KB RAM
    - Klavye, fare ve uzaktan destek
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'leri şu şekilde sezgiseldir: *ux_host_class_hid_** 
* Hub
    - En az 1,7 KB FLASH, 2 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_host_class_hub_**
* PIMA (PTP/MTP)
    - En az 0,9 KB FLASH, 8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'leri şu şekilde sezgiseldir: *ux_host_class_pima_**
* Yazıcı
    - En az 0,8 KB FLASH, 8 KB RAM
    - Otomatik ölçeklendirme
    -  Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    -  UsbX Azure RTOS API'leri şu şekilde sezgiseldir: *ux_host_class_printer_**
* Üretken
    - En az 1,5 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'leri şu şekilde sezgiseldir: *ux_host_class_prolific_**
* STORAG
    - En az 5,6 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme<br> Azure RTOS FileX ile tümleşiktir
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_host_class_storage_**
* USB Ana Bilgisayar YıĞıNı
    - Birçok konak denetleyicisini destekler
    - En az 18 KB FLASH, 25 KB RAM
    - Otomatik ölçeklendirme
    - Aynı platformda birden çok konak denetleyicisi desteği
    -  USB düşük, tam ve yüksek hızlı destek
    -  Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    -  UsbX Azure RTOS API'leri şu şekilde sezgiseldir: *ux_host_stack_* * 
* AHCI, EHCI, ÖZEL KONAK DENETLEYICILERI 

### <a name="azure-rtos-usbx-device-api"></a>Azure RTOS USBX Cihaz API'si

USBX Azure RTOS API'si, isim-fiil adlandırma kuralının ardından sezgisel ve tutarlı bir API'dir. Tüm API'ler USBX ux_device_* önde gelen veri noktalarına* sahip olur. Engelleme API'lerinde isteğe bağlı iş parçacığı zaman aşımı vardır. Daha fazla [Azure RTOS usbx ana bilgisayar kullanıcı kılavuzuna](usbx-host-stack-about.md) bakın.

* CDC/ACM
    - En az 0,8 KB FLASH, 2 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Sezgisel Azure RTOS USBX cihaz API'leri şu şekildedir: *ux_device_class_cdc_acm_**.
* CDC/ECM
    - En az 1,5 KB FLASH, 4 KB ile 8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme<br> UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_device_class_cdc_ecm_**.
* Dfu
    - En az 1,1 KB FLASH, 2 KB RAM
    -  Otomatik ölçeklendirme
    -  Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_device_class_dfu_** 
* GSER
    - En az 0,6 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_device_class_gser_**
* Sakladı
    - En az 0,9 KB FLASH, 2 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu Azure RTOS USBX cihaz API'lerinin kullanımı kolay: *ux_device_class_hid_** PIMA (PTP/MTP)
    - En az 5,2 KB FLASH, 8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_device_class_pima_** 
* DEPOLAMA
    - En az 2,3 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_device_class_storage_**
* RNDIS
    - En az 2,3 KB FLASH, 4 KB ile 8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS NetX ve Azure RTOS NetX DUO ile tümleşiktir
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_device_class_rndls_**
* Azure RTOS USBX Cihaz YıĞıNı
    - En az 2,3 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - UsbX Azure RTOS API'lerini şu şekilde sezgisel hale getirir: *ux_device_class_storage_**
* ÖZEL KONAK DENETLEYICILERI

## <a name="next-steps"></a>Sonraki adımlar

Konak Yığını Kullanıcı Kılavuzu Azure RTOS Cihaz Yığını Kullanıcı [](usbx-host-stack-about.md) Kılavuzu'mızı takip edin ve USBX Ana Bilgisayarı ve Cihaz Yığını [ile çalışmaya başlama.](usbx-device-stack-about.md)