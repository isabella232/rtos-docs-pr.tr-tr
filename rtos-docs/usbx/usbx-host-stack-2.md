---
title: Bölüm 2 - Azure RTOS USBX Konak Yığını Yüklemesi
description: USBX konak yığınını yükleme hakkında bilgi.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 77df2c4e4bf4ef38403fe78eb98f18820de4325aadb941fc69275e4c77754212
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790975"
---
# <a name="chapter-2---azure-rtos-usbx-host-stack-installation"></a>Bölüm 2 - Azure RTOS USBX Konak Yığını Yüklemesi

## <a name="host-considerations"></a>KonakLa ilgili Dikkat Edilmesi Gerekenler

### <a name="computer-type"></a>Bilgisayar Türü

Katıştırılmış geliştirme genellikle bilgisayar veya Unix Windows bilgisayarlarda gerçekleştirilir. Uygulama derledikten, bağlandıktan ve konakta bulunduktan sonra, yürütme için hedef donanıma indirilir.

### <a name="download-interfaces"></a>Arabirimleri İndirme

Genellikle, hedef indirme bir RS-232 seri arabirimi üzerinden yapılır, ancak paralel arabirimler, USB ve Ethernet daha popüler hale geliyor. Kullanılabilir seçenekler için geliştirme aracı belgelerine bakın.

### <a name="debugging-tools"></a>Hata Ayıklama Araçları

Hata ayıklama genellikle program görüntüsü indirmeyle aynı bağlantı üzerinden yapılır. Arka Plan Hata Ayıklama İzleyicisi (BDM) ve arka plan (ICE) araçları aracılığıyla hedefte çalışan küçük monitör programlarından In-Circuit Emulator çeşitli hata ayıklayıcıları vardır. ICE aracı, gerçek hedef donanımın en güçlü hata ayıklamasını sağlar.

### <a name="required-hard-disk-space"></a>Gerekli Sabit Disk Alanı

USBX kaynak kodu ASCII biçiminde teslim edilir ve konak bilgisayarın sabit diskte yaklaşık 500 KBayt alan gerektirir.

## <a name="target-considerations"></a>HedefLe ilgili Dikkat Edilmesi Gerekenler

USBX, konak modunda hedefte 24 KBayt ile 64 KBayt Arasında Salt Okunur Bellek (ROM) gerektirir. Gereken bellek miktarı, kullanılan denetleyici türüne ve USBX'e bağlı USB sınıflara bağlıdır. USBX genel veri yapıları ve bellek havuzu için hedefin Rastgele Erişim Belleği'nin (RAM) 32 KBayt daha olması gerekir. Bu bellek havuzu, USB'de beklenen cihaz sayısına ve USB denetleyicisinin türüne bağlı olarak da ayarlanabilir. USBX cihaz tarafı, cihaz denetleyicisinin türüne bağlı olarak yaklaşık 10-12 K ROM gerektirir. RAM bellek kullanımı, cihaz tarafından öykünülen sınıf türüne bağlıdır.

USBX ayrıca, birden çok iş parçacığı koruması için ThreadX semaforlarını, mutex'leri ve iş parçacıklarını ve USB veri verisi topolojisini izlemek için I/O askıya alma ve düzenli işlemeyi de kullanabilir.

### <a name="product-distribution"></a>Ürün Dağıtımı

Azure RTOS USBX, genel kaynak kodu depomuzdan <https://github.com/azure-rtos/usbx/> edinebilirsiniz.

Aşağıda, depoda yer alan birkaç önemli dosyanın listesi ve ardından yer alan liste ve bir liste ve ardından yer alan bilgileri bulabilirsiniz:

- ***ux_api.h:*** Bu C üst bilgi dosyası tüm sistem eşitlerini, veri yapılarını ve hizmet prototiplerini içerir.
- ***ux_port.h:*** Bu C üst bilgi dosyası, geliştirme aracına özgü tüm veri tanımlarını ve yapılarını içerir.
- ***ux.lib:*** Bu, USBX C kitaplığının ikili sürümüdür. Standart paketle dağıtılır.
- ***demo_usbx.c:*** Basit bir USBX demosu içeren C dosyası

Tüm dosya adlarında küçük harf vardır. Bu adlandırma kuralı komutları Unix geliştirme platformlarına dönüştürmeyi kolaylaştırır.

## <a name="usbx-installation"></a>USBX Yüklemesi

USBX, depolama GitHub yerel makinenize kopya tarafından yüklenir. Aşağıdakiler, bilgisayarınızda USBX deposunun bir kopyasını oluşturmak için tipik söz dizimidir:

```powershell
    git clone https://github.com/azure-rtos/usbx
```

Alternatif olarak, ana sayfada yer alan indirme düğmesini kullanarak deponun bir GitHub indirebilirsiniz.

UsbX kitaplığını oluşturma yönergelerini çevrimiçi deponun ön sayfasında da bulabilirsiniz.

Aşağıdaki genel yönergeler neredeyse tüm yüklemeler için geçerlidir:

1. Ana bilgisayar sabit sürücüsüne ThreadX'i daha önce yüklemiş olduğunuz dizini kullanın. Tüm USBX adları benzersizdir ve önceki USBX yüklemesini engellemez.
2. * ux_system_initialize _ **ux_system_initialize** _tx_application_define başlangıcına bir *_çağrı ekleyin._* * USBX kaynakları burada başlatılır.
3. ***ux_host_stack_initialize* çağrısı ekleyin.**
4. Gerekli USBX'i başlatmak için bir veya daha fazla çağrı ekleyin.
5. Sistemde kullanılabilen konak denetleyicilerini başlatmak için bir veya daha fazla çağrı ekleyin.
6. Düşük düzeyli donanım başlatma ve kesme vektör yönlendirmesi eklemek için tx_low_level_initialize.c dosyasını değiştirmek gerekebilir. Bu, donanım platformuna özeldir ve burada ele alınmayacaktır.
7. USB depolama sınıfı ve/veya USB ağ sınıfları içinde derlenmişse, ux.a (veya ux.lib) ve tx.a (veya tx.lib) ile uygulama kaynak kodunu ve USBX ve ThreadX çalışma zamanı kitaplıkları ile bağlantıyı derle (FileX ve/veya Netx de gerekli olabilir). Sonuçta hedefe indirilir ve yürütülür.

## <a name="configuration-options"></a>Yapılandırma Seçenekleri

USBX kitaplığını oluşturmanın çeşitli yapılandırma seçenekleri vardır. Tüm seçenekler ***ux_user.h içinde bulunur.***

Aşağıdaki listede her yapılandırma seçeneği ayrıntılı olarak verilmiştir.


- **UX_PERIODIC_RATE:** Bu değer, belirli bir donanım platformu için saniye başına kaç tık olduğunu temsil eder. Varsayılan değer, milisaniye başına bir tık olduğunu belirten 1000'tir.
- **UX_MAX_CLASS_DRIVER:** Bu değer, USBX tarafından yüklen minimum sınıf sayısıdır. Bu değer, bir sınıfın örnek sayısını değil sınıf kapsayıcısı temsil eder. Örneğin, belirli bir USBX uygulaması hub sınıfına, yazıcı sınıfına ve depolama sınıfına ihtiyaç varsa, bu sınıflara ait cihaz sayısından bağımsız olarak UX_MAX_CLASS_DRIVER değeri 3'e ayarlanır.
- **UX_MAX_HCD:** Bu değer, sistemde kullanılabilen farklı konak denetleyicilerinin sayısını temsil eder. USB 1.1 desteği için bu değer çoğunlukla 1 olur. USB 2.0 desteği için bu değer 1'den fazla olabilir. Bu değer, aynı anda çalışan eşzamanlı konak denetleyicisi sayısını temsil eder. Örneğin, çalışan iki AHCI örneği veya bir EHCI ve bir AHCI denetleyicisi çalışıyorsa, UX_MAX_HCD 2 olarak ayar gerekir. 
- **UX_MAX_DEVICES:** Bu değer, USB'ye bağlanabilirsiniz maksimum cihaz sayısını temsil eder. Normalde, tek bir USB'de teorik olarak maksimum sayı 127 cihazdır. Bu değer, bellek tasarrufu yapmak için ölçeğini aşağıya doğru ölçeklendirin. Bu değerin, sistemdaki USB veri verisi sayısından bağımsız olarak toplam cihaz sayısını temsil ettiğine emin olun.
- **UX_MAX_ED:** Bu değer denetleyici havuzunda en fazla SAYıDA ES'yi temsil eder. Bu sayı yalnızca bir denetleyiciye atanır. Birden çok denetleyici örneği varsa, bu değer her bir denetleyici tarafından kullanılır.
- **UX_MAX_TD ve UX_MAX_ISO_TD:** Bu değer denetleyici havuzunda bulunan en fazla normal ve zaman uyumsuz TD sayısını temsil eder. Bu sayı yalnızca bir denetleyiciye atanır. Birden çok denetleyici örneği varsa, bu değer her bir denetleyici tarafından kullanılır.
- **UX_THREAD_STACK_SIZE:** Bu değer, USBX iş parçacıkları için yığının bayt cinsinden boyutudur. Kullanılan işlemciye ve konak denetleyicisine bağlı olarak genellikle 1024 bayt veya 2048 bayt olabilir.
- **UX_HOST_ENUM_THREAD_STACK_SIZE:** Bu değer, USB konak numaralama iş parçacığının yığın boyutudur. Bu simgeyi ayarlamazsanız, USBX ana bilgisayar numaralama iş parçacığı yığın boyutu **UX_THREAD_STACK_SIZE.** 
- **UX_HOST_HCD_THREAD_STACK_SIZE:** Bu değer, USB ana bilgisayar HCD iş parçacığının yığın boyutudur. Bu simgeyi ayarlamazsanız, USBX ana bilgisayarı HCD iş parçacığı yığını boyutu **UX_THREAD_STACK_SIZE.**
- **UX_THREAD_PRIORITY_ENUM:** Bu, veri verisi topolojisi izleyen USBX numaralama iş parçacıkları için ThreadX öncelik değeridir.
- **UX_THREAD_PRIORITY_CLASS:** Standart USBX iş parçacıkları için ThreadX öncelik değeridir.
- **UX_THREAD_PRIORITY_KEYBOARD:** Bu, USBX KEYBOARD klavye sınıfı için ThreadX öncelik değeridir.
- **UX_THREAD_PRIORITY_HCD:** Bu, konak denetleyici iş parçacığı için ThreadX öncelik değeridir.
- **UX_NO_TIME_SLICE:** Bu değer, iş parçacıkları için kullanılacak zaman dilimini tanımlar. Örneğin, 0 olarak tanımlanırsa, ThreadX hedef bağlantı noktası zaman dilimleri kullanmaz.
- **UX_MAX_HOST_LUN:** Bu değer, konak depolama sınıfı sürücüsünde temsil edilen en fazla SCSI mantıksal birimi sayısını temsil eder.
- **UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT:** Tanımlanmışsa, bu değer CB veya CBI protokolünü (disketler gibi) kullanan depolama cihazlarını işlemek için kod içerir. Varsayılan olarak kapalıdır çünkü bu protokoller kullanımdan kaldırılmış ve neredeyse tüm modern depolama cihazlarının kullanabileceği Toplu Taşıma (BOT protokolü) ile yenisi kaldırılmış durumdadır.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE:** Tanımlandı ise, bu ux_host_class_hid_keyboard_key_get yalnızca tuş basmaları ve anahtar yayınlarını bildirmeye neden olur. Varsayılan olarak, yalnızca bir anahtar kapat olduğunda rapor sağlar.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY:** Yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** kullanılır. Tanımlanmışsa, yalnızca ux_host_class_hid_keyboard_key_get/aşağı doğru değişiklikleri bildirmeye neden olur; yayımlanan anahtar/yukarı değişiklikleri raporlanmaz.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS:** Yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** kullanılır. Tanımlanmışsa, kilit ux_host_class_hid_keyboard_key_get (CapsLock/NumLock/ScrollLock) değişiklikleri bildirmeye neden olur.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS:** Yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** kullanılır. Tanımlandı ise, ux_host_class_hid_keyboard_key_get (Ctrl/Alt/Shift/GUI) değişikliklerini bildirmeye neden olur.
- **UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES:** Tanımlanırsa, bu değer CDC-ECM konak sınıfındaki paket sayısını temsil eder. Varsayılan değer 16'dır.

## <a name="source-code-tree"></a>Kaynak Kod Ağacı

USBX dosyaları birkaç dizinde sağlanır.

![Kaynak kod ağacı](media/usbx-host-stack/source-code-tree.png)

Dosyaları adlarıyla tanınabilir hale getirmek için aşağıdaki kural benimsenmiştir:

| Dosya sonek adı | Dosya açıklaması                          |
| ---------------- | ----------------------------------------- |
| ux_host_stack    | USBX konak yığını çekirdek dosyaları                |
| ux_host_class    | USBX konak yığını sınıfları dosyaları             |
| ux_hcd           | USBX konak yığını denetleyici sürücü dosyaları   |
| ux_device_stack  | USBX cihaz yığını çekirdek dosyaları              |
| ux_device_class  | USBX cihaz yığını sınıfları dosyaları           |
| ux_dcd           | USBX cihaz yığını denetleyici sürücü dosyaları |
| ux_otg           | USBX OTG denetleyicisi sürücüyle ilgili dosyalar  |
| ux_pictbridge    | USBX PictBridge dosyaları                     |
| ux_utility       | USBX yardımcı program işlevleri                    |
| demo_usbx        | USBX için tanıtım dosyaları              |

## <a name="initialization-of-usbx-resources"></a>USBX kaynaklarının başlatılması

USBX 'in kendi bellek yöneticisi vardır. USBX 'in ana bilgisayar veya cihaz tarafı başlatılmadan önce belleğin USBX 'e ayrılması gerekir. USBX bellek Yöneticisi belleğin önbelleğe alınabilme sistemlerine uyum sağlayabilir.

Aşağıdaki işlev USBX bellek kaynaklarını 128K normal bellekle başlatır ve önbellek güvenli belleği için ayrı havuz içermez:

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

Ux_system_initialize prototipi aşağıdaki gibidir.

```c
UINT ux_system_initialize( 
    VOID *regular_memory_pool_start,
    ULONG regular_memory_size,
    VOID *cache_safe_memory_pool_start,
    ULONG cache_safe_memory_size);
```

### <a name="input-parameters"></a>Giriş parametreleri:

- **regular_memory_pool_start** Normal bellek havuzunun başlangıcı.
- **regular_memory_size** Normal bellek havuzunun boyutu.
- **cache_safe_memory_pool_start** Önbellek güvenli bellek havuzunun başlangıcı.
- **cache_safe_memory_size** Önbellek güvenli bellek havuzunun boyutu.    |

Tüm sistemler önbellek güvenli belleği tanımını gerektirmez. Böyle bir sistemde, bellek işaretçisi için başlatma sırasında geçirilen değerler UX_NULL olarak ayarlanacak ve havuzun boyutu 0 olarak ayarlanır. USBX daha sonra önbellek güvenli havuzunun yerine normal bellek havuzunu kullanacaktır.

Normal belleğin önbellek güvenli olmadığı ve bir denetleyicinin DMA belleği (örneğin, OHCı, diğer bir deyişle, diğer bir deyişle, diğer bir deyişle, EHCı denetleyicileri) gerçekleştirmesi gereken bir sistemde, önbellek güvenli bölgesinde bir bellek havuzu tanımlamak gerekir.

## <a name="uninitialization-of-usbx-resources"></a>USBX kaynaklarının başlatılması geri alınıyor

USBX, kaynakları serbest bırakarak sonlandırılabilir. USBX 'i sonlandırmadan önce tüm sınıfların ve denetleyici kaynaklarının düzgün şekilde sonlandırılması gerekir. Aşağıdaki işlev, USBX bellek kaynaklarını başlatır:

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

Ux_system_initialize prototipi aşağıdaki gibidir.

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-host-controllers"></a>USB ana bilgisayar denetleyicilerinin tanımı

USBX 'in konak modunda çalışması için en az bir USB ana bilgisayar denetleyicisi tanımlamanız gerekir. Uygulama başlatma dosyası bu tanımı içermelidir. Aşağıdaki satır bir genel ana bilgisayar denetleyicisinin tanımını gerçekleştirir.

```c
ux_host_stack_hcd_register("ux_hcd_controller",
        ux_hcd_controller_initialize, 0xd0000, 0x0a);
```

Ux_host_stack_hcd_register aşağıdaki prototiple sahiptir.

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_initialize_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

Ux_host_stack_hcd_register işlevi aşağıdaki parametrelere sahiptir.

- **hcd_name**: denetleyici adının dizesi
- **hcd_initialize_function**: denetleyicinin başlatma işlevi
- **hcd_param1**: genellikle denetleyici tarafından kullanılan GÇ değeri veya bellek
- **hcd_param2**: genellikle denetleyici tarafından kullanılan IRQ

Önceki örneğimizde:

- "ux_hcd_controller" denetleyicinin adıdır
- "ux_hcd_controller_initialize", ana bilgisayar denetleyicisi için başlatma yordamdır
- 0xD0000, ana bilgisayar denetleyicisi yazmaçlarının bellekte görünebileceği adrestir
- ve 0x0A, ana bilgisayar denetleyicisi tarafından kullanılan IRQ 'dir.

Aşağıda, ana bilgisayar denetleyicisi ve birkaç sınıf ile USBX 'in ana bilgisayar modunda başlatılmasına örnek verilmiştir.

```c
UINT status;

/* Initialize USBX. */
ux_system_initialize(memory_ptr, (128*1024),0,0);

/* The code below is required for installing the USBX host stack. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, host stack has been initialized. */

/* Register all the host classes for this USBX implementation. */
status = ux_host_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_storage", ux_host_class_storage_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_printer", ux_host_class_printer_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_audio", ux_host_class_audio_entry);

/* If status equals UX_SUCCESS, host class has been registered. */

/* Register all the USB host controllers available in this system. */ 
status = ux_host_stack_hcd_register("ux_hcd_controller", ux_hcd_controller_initialize, 0x300000, 0x0a);

/* If status equals UX_SUCCESS, USB host controllers have been registered. */
```

## <a name="definition-of-host-classes"></a>Konak sınıflarının tanımı

USBX ile bir veya daha fazla konak sınıfı tanımlanması gerekir. USB yığını USB cihazını yapılandırdıktan sonra USB bir cihaz için bir USB sınıfı gerekir. Cihaza özel bir USB sınıfı. USB cihaz tanımlayıcılarında bulunan arabirimlerin sayısına bağlı olarak bir USB cihazını yönlendirmek için bir veya daha fazla sınıf gerekebilir.

Bu, HUB sınıfının kaydına bir örnektir.

```c
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);
```

Ux_host_class_register işlevi aşağıdaki prototiple sahiptir.

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name, 
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

- **class_name** , sınıfın adıdır
- **class_entry_address** , sınıfın giriş noktasıdır

HUB sınıfı başlatma örneğinde:

- "ux_host_class_hub", hub sınıfının adıdır
- ux_host_class_hub_entry, HUB sınıfının giriş noktasıdır.

## <a name="troubleshooting"></a>Sorun giderme

USBX, bir tanıtım dosyası ve simülasyon ortamıyla birlikte sunulur. Her zaman, hedef donanımda veya belirli bir demo platformunda ilk olarak çalışan tanıtım platformunu almak iyi bir fikirdir.

Tanıtım sistemi çalışmazsa, sorunu daraltmak için aşağıdaki işlemleri deneyin.

## <a name="usbx-version-id"></a>USBX sürüm KIMLIĞI

USBX ' in geçerli sürümü, hem Kullanıcı hem de uygulama yazılımının çalışma zamanı sırasında kullanılabilir. Programcı, USBX sürümünü, ***ux_port. h** _ dosyasının inceağından elde edebilir. Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir. Uygulama yazılımı, _ *_ux_port. h_* * içinde tanımlanan _ *_ _ux_version_id_* _ genel dizesini inceleyerek USBX sürümünü alabilir.
