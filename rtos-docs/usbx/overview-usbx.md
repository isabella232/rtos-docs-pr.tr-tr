---
title: Azure RTOS USBX 'i anlama
description: Azure RTOS USBX, yüksek performanslı bir USB ana bilgisayar, cihaz ve açık Go (OTG) eklenmiş Stack 'tir, Azure RTOS USBX Azure RTOS ThreadX ile tamamen tümleşiktir ve tüm Azure RTOS ThreadX tarafından desteklenen işlemcilerde kullanılabilir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 8950e7573bf705feb16de6ac1adb5f55559ea4b04b453944c5a24baddc6ae7b9
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791457"
---
# <a name="overview-of-azure-rtos-usbx"></a>Azure RTOS USBX 'e genel bakış

Azure RTOS USBX, yüksek performanslı bir USB ana bilgisayar, cihaz ve-go (OTG) katıştırılmış Stack 'tir. Azure RTOS USBX, Azure RTOS ThreadX ile tamamen tümleşiktir ve tüm ThreadX tarafından desteklenen işlemciler için kullanılabilir. ThreadX gibi Azure RTOS USBX, küçük bir ayak izi ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da USB cihazlarıyla bir arabirim gerektiren çok sayıda gömülü uygulama için idealdir.

## <a name="host-device-otg--extensive-class-support"></a>Konak, cihaz, OTG & kapsamlı sınıf desteği

Azure RTOS USBX konak/cihaz Embedded USB protokol yığını, özellikle de gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan bir endüstriyel sınıf Embedded USB çözümüdür. Azure RTOS USBX, ana bilgisayar, cihaz ve OTG desteğinin yanı sıra kapsamlı sınıf desteği sağlar. Azure RTOS USBX, ThreadX Real-Time Işletim sistemiyle tamamen tümleşiktir, Azure RTOS FileX Embedded FAT uyumlu dosya sistemi, Azure RTOS NetX ve Azure RTOS NetX Duo Embedded TCP/IP yığınları. Bunun hepsi, son derece küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla birlikte Azure RTOS USBX ' i, USB bağlantısı gerektiren en zorlu eklenmiş IoT uygulamalarına yönelik ideal seçenektir.

### <a name="usbx-memory-footprint"></a>USBX bellek ayak izi

Azure RTOS USBX, Azure RTOS USBX cihaz CDC/ACM desteği için 10,5 KB 'lık FLASH ve 5,1 KB RAM 'in daha hızlı küçük bir ayak izine sahiptir. Azure RTOS USBX ana bilgisayarı, CDC/ACM desteği için en az 18 KB FLASH ve 25 KB RAM gerektirir.

TCP işlevselliği için 10 KB ila 13 KB 'lık yönerge alanı belleği gerekir. Azure RTOS USBX RAM kullanımı, genellikle 2,6 KB 'den 3,6 KB 'ye ve uygulama tarafından tanımlanan paket havuzu belleğine göre değişir.

ThreadX gibi, Azure RTOS USBX boyutu, uygulama tarafından gerçekten kullanılan hizmetlere göre otomatik olarak ölçeklendirilir. Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.

### <a name="usb-interoperability-verification"></a>USB birlikte çalışabilirlik doğrulaması

Azure RTOS USBX cihaz yığını, USB belirtimleri ve farklı konak sistemleriyle birlikte çalışabilirlik ile tam uyumluluk sağlamak için USB IF standart test aracı USBV ile bir daha dikkatli test edilmiştir.
Ayrıca, Azure RTOS USBX OTG yığını, Tayvan 'daki bağımsız test laboratuvarı tarafından doğrulanır ve sertifikalandırilmiştir.

### <a name="usb-host-controller-support"></a>USB ana bilgisayar denetleyicisi desteği

Azure RTOS USBX, OHCı ve EHCı gibi ana USB standartlarını destekler. Ayrıca, Azure RTOS USBX, Atmel, mikro yonga, Philips, Renesas, ST, TI ve diğer satıcılardan özel ayrı USB ana bilgisayar denetleyicilerini destekler. Azure RTOS USBX aynı uygulamadaki birden çok konak denetleyicisini da destekler.
USB cihaz denetleyicisi desteği Azure RTOS USBX, analog cihazlardan, Atmel, mikro yonga, NXP, Philips, Renesas, ST, TI ve diğer satıcılardan popüler USB cihaz denetleyicilerini destekler.

### <a name="extensive-host-class-support"></a>Kapsamlı konak sınıfı desteği

Azure RTOS USBX ana bilgisayarı, ASIX, AUDIO, CDC/ACM, CDC/ECM, GSER, HID (klavye, fare ve Uzaktan denetim), Merkez, PIMA (PTP/MTP), yazıcı, PROLIFIC ve depolama gibi popüler sınıfların çoğu için destek sağlar.

### <a name="extensive-usb-device-class-support"></a>Kapsamlı USB cihaz sınıfı desteği

Azure RTOS USBX cihazı, CDC/ACM, CDC/ECD, DFU, HID, PIMA (PTP/MTP) (w/MTP), RNDIS ve depolama gibi popüler sınıfların çoğu için destek sağlar. Özel sınıflar için destek de mevcuttur.

### <a name="pictbridge-support"></a>PictBridge desteği

Azure RTOS USBX, hem konakta hem de cihazda tam PictBridge uygulamasını destekler. PictBridge, her iki tarafta Azure RTOS USBX PIMA (PTP/MTP) sınıfının üzerinde yer alır. PictBridge standardı, dijital bir kamera veya akıllı telefonun doğrudan bılgısayar olmadan bir yazıcıya bağlantısının yapılmasına izin verir ve belirli bir PictBridge kullanan yazıcılara doğrudan yazdırmayı etkinleştirir. Bir kamera veya telefon bir yazıcıya bağlıyken, yazıcı USB ana bilgisayarı ve kamera USB aygıtıdır. Ancak, PictBridge ile kamera ana bilgisayar olarak görünür ve bu da komutlar kameradan çalıştırılır. Kamera, depolama istemcisini yazıcı olan depolama sunucusudur. Kamera, yazdırma istemcsahiptir ve yazıcı, yazdırma sunucusu kursta. PictBridge, USB 'yi bir aktarım katmanı olarak kullanır, ancak iletişim protokolüne ait PTP (resim aktarma protokolü) kullanır.

### <a name="custom-class-support"></a>Özel sınıf desteği

Azure RTOS USBX Konağı ve cihazı özel sınıfları destekler. Azure RTOS USBX dağıtımında örnek bir özel sınıf verilmiştir. Bu basit veri pompa sınıfı DPUMP olarak adlandırılır ve özel uygulama sınıfları için bir model olarak kullanılabilir.
Gelişmiş teknoloji Azure RTOS USBX Konağı ve cihaz özel sınıfları destekler. Azure RTOS USBX dağıtımında örnek bir özel sınıf verilmiştir. Azure RTOS USBX, şunları içeren gelişmiş bir teknolojidir:

* Konak, cihaz ve OTG desteği
* USB düşük, tam ve yüksek hızlı destek
* Otomatik ölçeklendirme
* ThreadX, Azure RTOS FileX ve Azure RTOS NetX ile tam tümleşik
* İsteğe bağlı performans ölçümleri
* Azure RTOS TraceX sistem analizi desteği

## <a name="azure-rtos-usbx-apis"></a>Azure RTOS USBX API 'Leri

### <a name="azure-rtos-usbx-host-api"></a>Azure RTOS USBX konak API 'SI

Azure RTOS USBX ana bilgisayar API 'SI, bir ad fiil adlandırma kuralını izleyen sezgisel ve tutarlı bir API 'dir. Tüm API 'Ler, USBX olarak kolayca tanımlanabilmesi için önde gelen ux_host_ *. Tüm engelleyici API 'Lerde isteğe bağlı iş parçacığı zaman aşımı vardır.

* ASIX
    - En az 0,3 KB FLASH, 4 KB RAM
    - Azure RTOS TraceX aracılığıyla otomatik scalingSystem-Level izleme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_asix_**
* MÜZIK
    - En az 1,2 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_audio_**
* CDC/ACM
    - En az 1,4 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_cdc_acm_**
* CIHAZDAN
    - En az 0,3 KB FLASH, 4 KB RAM
    - Klavye, fare ve uzaktan destek
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_hid_** 
* HUB
    - Minimum 1,7 KB FLASH, 2 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_hub_**
* PIMA (PTP/MTP)
    - En az 0,9 KB FLASH, 8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_pima_**
* YAZıCıDA
    - En az 0,8 KB FLASH, 8 KB RAM
    - Otomatik ölçeklendirme
    -  Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    -  Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_printer_**
* PROLIFIC
    - En az 1,5 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_prolific_**
* Lama
    - En az 5,6 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme<br> Azure RTOS FileX ile tümleşik
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_class_storage_**
* USB ana bilgisayar YıĞıNı
    - Birçok konak denetleyicisini destekler
    - En az 18 KB FLASH, 25 KB RAM
    - Otomatik ölçeklendirme
    - Aynı platformda birden çok konak denetleyicisi desteği
    -  USB düşük, tam ve yüksek hızlı destek
    -  Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    -  Bu biçimde sezgisel Azure RTOS USBX konak API 'Leri: *ux_host_stack_* * 
* OHCı, EHCı, özel ana bilgisayar DENETLEYICILERI 

### <a name="azure-rtos-usbx-device-api"></a>Azure RTOS USBX cihaz API 'SI

Azure RTOS USBX cihaz API 'SI, bir ad fiil adlandırma kuralını izleyen sezgisel ve tutarlı bir API 'dir. Tüm API 'Ler, USBX olarak kolayca tanımlanabilmesi için önde gelen ux_device_ *. API 'Lerin engellenmesi isteğe bağlı iş parçacığı zaman aşımına uğradı. Daha fazla ayrıntı için lütfen bkz. [Azure RTOS USBX konak Kullanıcı Kılavuzu](usbx-host-stack-about.md) .

* CDC/ACM
    - Minimum 0,8 KB FLASH, 2 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX cihaz API 'Leri: * ux_device_class_cdc_acm_ * *.
* CDC/ECD
    - Minimum 1,5 KB FLASH, 4 KB-8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme<br> Bu biçimde sezgisel Azure RTOS USBX cihaz API 'Leri: * ux_device_class_cdc_ecm_ * *.
* DFU
    - Minimum 1,1 KB FLASH, 2 KB RAM
    -  Otomatik ölçeklendirme
    -  Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimdeki sezgisel Azure RTOS USBX cihaz API 'Leri: *ux_device_class_dfu_** 
* GSER
    - En az 0,6 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimdeki sezgisel Azure RTOS USBX cihaz API 'Leri: *ux_device_class_gser_**
* CIHAZDAN
    - Minimum 0,9 KB FLASH, 2 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimde sezgisel Azure RTOS USBX cihaz API 'Leri: *ux_device_class_hid_** Pima (PTP/MTP)
    - En az 5,2 KB FLASH, 8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimdeki sezgisel Azure RTOS USBX cihaz API 'Leri: *ux_device_class_pima_** 
* DEPOLAMA
    - En az 2,3 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimdeki sezgisel Azure RTOS USBX cihaz API 'Leri: *ux_device_class_storage_**
* RNDIS
    - Minimum 2,3 KB FLASH, 4 KB-8 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS NetX ve Azure RTOS NetX DUO ile tümleşik
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimdeki sezgisel Azure RTOS USBX cihaz API 'Leri: *ux_device_class_rndls_**
* Azure RTOS USBX cihaz YıĞıNı
    - En az 2,3 KB FLASH, 4 KB RAM
    - Otomatik ölçeklendirme
    - Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
    - Bu biçimdeki sezgisel Azure RTOS USBX cihaz API 'Leri: *ux_device_class_storage_**
* ÖZEL konak DENETLEYICILERI

## <a name="next-steps"></a>Sonraki adımlar

[Ana bilgisayar yığını Kullanıcı Kılavuzumuzu](usbx-host-stack-about.md) veya [cihaz yığını Kullanıcı Kılavuzumuzu](usbx-device-stack-about.md)izleyerek Azure RTOS USBX Konağı ve cihaz Stack ile çalışmaya başlayın.