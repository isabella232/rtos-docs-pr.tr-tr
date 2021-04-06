---
title: Bölüm 2-Azure RTOS USBX konak yığını yüklemesi
description: USBX konak yığınını yüklemeyi öğrenin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 4c33f95b8ac268c557fd947a1303ec3af315a37e
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377093"
---
# <a name="chapter-2---azure-rtos-usbx-host-stack-installation"></a>Bölüm 2-Azure RTOS USBX konak yığını yüklemesi

## <a name="host-considerations"></a>Ana bilgisayar konuları

### <a name="computer-type"></a>Bilgisayar türü

Katıştırılmış Geliştirme genellikle Windows bılgısayar veya UNIX ana bilgisayarları üzerinde gerçekleştirilir. Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.

### <a name="download-interfaces"></a>Arabirimleri indir

Genellikle, paralel arabirimler, USB ve Ethernet daha popüler olsa da, hedef indirme bir RS-232 seri arabirimi üzerinden yapılır. Kullanılabilir seçenekler için geliştirme aracı belgelerine bakın.

### <a name="debugging-tools"></a>Hata ayıklama araçları

Hata ayıklama, genellikle program görüntüsü indirdiği bağlantıyla aynı bağlantı üzerinden yapılır. Arka plan hata ayıklama Izleyicisi (BDM) ve In-Circuit öykünücü (ıCE) araçları aracılığıyla hedefte çalışan küçük izleme programlarından farklı hata ayıklayıcılar vardır. ICE Aracı, gerçek hedef donanımının en sağlam hata ayıklamasını sağlar.

### <a name="required-hard-disk-space"></a>Gerekli sabit disk alanı

USBX için kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 500 Kbayt alan gerektirir.

## <a name="target-considerations"></a>Hedef konuları

USBX, ana bilgisayar modundaki hedefte yalnızca 24 Kbayt ve 64 Kbayt arasında salt okuma belleği (ROM) arasında olmalıdır. Gerekli bellek miktarı, kullanılan denetleyicinin türüne ve USBX ile bağlantılı USB sınıflarına bağımlıdır. USBX genel veri yapıları ve bellek havuzu için hedefin rastgele erişim belleği (RAM) için bir 32 Kbayt gerekir. Bu bellek havuzu, USB üzerindeki beklenen cihaz sayısına ve USB denetleyicisinin türüne göre de ayarlanabilir. USBX cihaz tarafı, cihaz denetleyicisinin türüne göre kabaca 10-12 K ROM gerektirir. RAM bellek kullanımı, cihaz tarafından Öykünülen sınıfın türüne bağlıdır.

USBX Ayrıca, Işparçacığıx semaforları, zaman uyumu sağlayıcılar ve birden çok iş parçacığı koruması için iş parçacıklarını ve USB veri yolu topolojisini izlemek için g/ç askıya alma ve düzenli işlemeyi kullanır.

### <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS USBX, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/usbx/> .

Depodaki birçok önemli dosyanın listesi aşağıda verilmiştir:

- ***ux_api. h***: Bu C üstbilgi dosyası tüm sistem eş, veri yapılarını ve hizmet prototiplerini içerir.
- ***ux_port. h***: Bu C üstbilgi dosyası, tüm geliştirme aracına özgü veri tanımlarını ve yapılarını içerir.
- ***UX. lib***: Bu, USBX C kitaplığının ikili sürümüdür. Standart paketiyle dağıtılır.
- ***demo_usbx. c***: basıt bır USBX tanıtımı içeren c dosyası

Tüm dosya adları küçük harfli. Bu adlandırma kuralı, komutları UNIX geliştirme platformlarına dönüştürmeyi kolaylaştırır.

## <a name="usbx-installation"></a>USBX yüklemesi

USBX, GitHub deposu yerel makinenize kopyalanarak yüklenir. Aşağıda, bilgisayarınızda USBX deposunun bir kopyasını oluşturmak için tipik sözdizimi verilmiştir:

```powershell
    git clone https://github.com/azure-rtos/usbx
```

Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında USBX kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.

Aşağıdaki genel yönergeler, neredeyse tüm yüklemeler için geçerlidir:

1. Konak sabit sürücüsüne daha önce ThreadX 'i yüklediğiniz dizini kullanın. Tüm USBX adları benzersizdir ve önceki USBX yüklemesine engel olmaz.
2. _ *_Tx_application_define_* başlangıcına veya yanına ***ux_system_initialize** _ çağrısı ekleyin. * Bu, USBX kaynaklarının başlatıldığı yerdir.
3. ***Ux_host_stack_initialize *** için bir çağrı ekleyin.
4. Gerekli USBX 'i başlatmak için bir veya daha fazla çağrı ekleyin.
5. Sistemde bulunan konak denetleyicilerini başlatmak için bir veya daha fazla çağrı ekleyin.
6. Alt düzey donanım başlatma ve kesme vektör yönlendirmesi eklemek için tx_low_level_initialize. c dosyasını değiştirmeniz gerekebilir. Bu donanım platformuna özeldir ve burada ele alınmamalıdır.
7. Uygulama kaynak kodunu derleme ve USBX ve ThreadX çalışma zamanı kitaplıkları (FileX ve/veya NETX), UX. a (veya UX. lib) ve TX. a (ya da TX. lib) ile bağlantı için gerekli olabilir. Sonuç hedefe indirilebilir ve yürütülür.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

USBX kitaplığını oluşturmak için birkaç yapılandırma seçeneği vardır. Tüm Seçenekler ***ux_user. h*** içinde bulunur.

Aşağıdaki listede her yapılandırma seçeneğinin ayrıntıları verilmiştir.


- **UX_PERIODIC_RATE**: Bu değer, belirli bir donanım platformu için saniye başına kaç saat sayısını temsil eder. Varsayılan değer, her milisaniyeye göre bir değer belirten 1000 ' dir.
- **UX_MAX_CLASS_DRIVER**: Bu değer, USBX tarafından yüklenebilen en fazla sınıf sayısıdır. Bu değer, bir sınıfın örnek sayısını değil, sınıf kapsayıcısını temsil eder. Örneğin, belirli bir USBX uygulamasının hub sınıfı, yazıcı sınıfı ve depolama sınıfı olması gerekiyorsa, bu sınıflara ait cihazların sayısından bağımsız olarak UX_MAX_CLASS_DRIVER değeri 3 olarak ayarlanabilir.
- **UX_MAX_HCD**: Bu değer, sistemde kullanılabilir olan farklı konak denetleyicilerinin sayısını temsil eder. USB 1,1 desteği için bu değer genellikle 1 olacaktır. USB 2,0 desteği için bu değer 1 ' den fazla olabilir. Bu değer aynı anda çalışan eşzamanlı konak denetleyicilerinin sayısını temsil eder. Örneğin, iki adet OHCı çalışan ya da bir EHCı ve bir adet bir EHCı denetleyicisi çalışan iki örnek varsa, UX_MAX_HCD 2 olarak ayarlanmalıdır. 
- **UX_MAX_DEVICES**: Bu değer, USB 'ye iliştirilebilecek maksimum cihaz sayısını temsil eder. Normalde, tek bir USB üzerinde teorik en büyük sayı 127 cihazlardır. Bu değer, belleği korumak için küçültülemez. Bu değerin sistemdeki USB veri yolu sayısından bağımsız olarak toplam cihaz sayısını temsil ettiğini unutmayın.
- **UX_MAX_ED**: Bu değer, denetleyici havuzundaki en fazla EDS sayısını temsil eder. Bu sayı yalnızca bir denetleyiciye atanır. Birden çok denetleyici örneği varsa, bu değer her bir denetleyici tarafından kullanılır.
- **UX_MAX_TD ve UX_MAX_ISO_TD**: Bu değer, denetleyici havuzundaki en fazla normal ve zaman aralıklı tds sayısını temsil eder. Bu sayı yalnızca bir denetleyiciye atanır. Birden çok denetleyici örneği varsa, bu değer her bir denetleyici tarafından kullanılır.
- **UX_THREAD_STACK_SIZE**: Bu değer, USBX iş parçacıklarının bayt cinsinden yığınının boyutudur. Kullanılan işlemciye ve ana bilgisayar denetleyicisine bağlı olarak genellikle 1024 bayt veya 2048 bayt olabilir.
- **UX_HOST_ENUM_THREAD_STACK_SIZE**: Bu değer, USB ana bilgisayar numaralandırma iş parçacığının yığın boyutudur. Bu sembol ayarlanmıyorum, USBX konak numaralandırma iş parçacığı yığın boyutu **UX_THREAD_STACK_SIZE** olarak ayarlanır. 
- **UX_HOST_HCD_THREAD_STACK_SIZE**: Bu değer, USB Host HCD iş parçacığının yığın boyutudur. Bu sembol ayarlanmıyorum, USBX Host HCD iş parçacığı yığın boyutu **UX_THREAD_STACK_SIZE** olarak ayarlanır.
- **UX_THREAD_PRIORITY_ENUM**: Bu, veri yolu topolojisini izleyen USBX sabit listesi Iş parçacıklarının threadx öncelik değeridir.
- **UX_THREAD_PRIORITY_CLASS**: Bu, standart USBX iş parçacıkları Için threadx öncelik değeridir.
- **UX_THREAD_PRIORITY_KEYBOARD**: Bu, USBX HID Klavye sınıfı Için threadx öncelik değeridir.
- **UX_THREAD_PRIORITY_HCD**: Bu, konak denetleyicisi iş parçacığı Için threadx öncelik değeridir.
- **UX_NO_TIME_SLICE**: Bu değer aslında iş parçacıkları için kullanılacak zaman dilimini tanımlar. Örneğin, 0 olarak tanımlanmışsa, ThreadX hedef bağlantı noktası zaman dilimlerini kullanmaz.
- **UX_MAX_HOST_LUN**: Bu değer, konak depolama sınıfı sürücüsünde temsil edilen en fazla SCSI mantıksal birim sayısını temsil eder.
- **UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT**: tanımlanmışsa, bu değer CB veya CBI protokolünü (disket gibi) kullanan depolama cihazlarını işleyecek kodu içerir. Varsayılan olarak kapalıdır çünkü bu protokoller artık neredeyse tüm modern depolama cihazlarının kullandığı toplu taşıma (BOT Protokolü) tarafından yerine geçti.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE**: tanımlanmışsa, bu değer ux_host_class_hid_keyboard_key_get yalnızca, tuş basışları ve önemli yayınlar için anahtar değişikliklerini rapor etmesine neden olur. Varsayılan olarak, yalnızca bir anahtar aşağı olduğunda bildirir.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY**: yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** tanımlanmışsa kullanılır. Tanımlandıysa, ux_host_class_hid_keyboard_key_get yalnızca tuşu basılı/aşağı değişiklikleri rapor etmesine neden olur; anahtar serbest bırakıldı/yukarı değişiklikler bildirilmedi.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS**: yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** tanımlanmışsa kullanılır. Tanımlandıysa, ux_host_class_hid_keyboard_key_get kilit anahtarını (CapsLock/NumLock/ScrollLock) değişikliklerini rapor etmesine neden olur.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS**: yalnızca **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** tanımlanmışsa kullanılır. Tanımlanmışsa, ux_host_class_hid_keyboard_key_get değiştirici anahtarı (Ctrl/Alt/Shift/GUI) değişikliklerini rapor etmesine neden olur.
- **UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**: tanımlanmışsa, bu değer CDC-ECD ana bilgisayar sınıfındaki paketlerin sayısını temsil eder. Varsayılan değer 16 ' dır.

## <a name="source-code-tree"></a>Kaynak kod ağacı

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
