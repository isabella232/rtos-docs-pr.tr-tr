---
title: Bölüm 2-Azure RTOS USBX cihaz yığını yüklemesi
description: USBX 'i yüklemeyi öğrenin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 097fdd3c6f09c666ec3ad6eda9e5ba3fa159cb4d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828450"
---
# <a name="chapter-2---azure-rtos-usbx-device-stack-installation"></a>Bölüm 2-Azure RTOS USBX cihaz yığını yüklemesi

## <a name="host-considerations"></a>Ana bilgisayar konuları

### <a name="computer-type"></a>Bilgisayar türü

Katıştırılmış Geliştirme genellikle Windows bılgısayar veya UNIX ana bilgisayarları üzerinde gerçekleştirilir. Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.

### <a name="download-interfaces"></a>Arabirimleri indir

Genellikle, paralel arabirimler, USB ve Ethernet daha popüler olsa da, hedef indirme bir RS-232 seri arabirimi üzerinden yapılır. Kullanılabilir seçenekler için geliştirme aracı belgelerine bakın.

### <a name="debugging-tools"></a>Hata ayıklama araçları

Hata ayıklama, genellikle program görüntüsü indirdiği bağlantıyla aynı bağlantı üzerinden yapılır. Arka plan hata ayıklama Izleyicisi (BDM) ve In-Circuit öykünücü (ıCE) araçları aracılığıyla hedefte çalışan küçük izleme programlarından farklı hata ayıklayıcılar vardır. ICE Aracı, gerçek hedef donanımının en sağlam hata ayıklamasını sağlar.

### <a name="required-hard-disk-space"></a>Gerekli sabit disk alanı

USBX için kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 500 Kbayt alan gerektirir.

### <a name="target-considerations"></a>Hedef konuları

USBX, ana bilgisayar modundaki hedefte yalnızca 24 Kbayt ve 64 Kbayt arasında salt okuma belleği (ROM) arasında olmalıdır. Gerekli bellek miktarı, kullanılan denetleyicinin türüne ve USBX ile bağlantılı USB sınıflarına bağımlıdır. USBX genel veri yapıları ve bellek havuzu için hedefin rastgele erişim belleği (RAM) için bir 32 Kbayt gerekir. Bu bellek havuzu, USB üzerindeki beklenen cihaz sayısına ve USB denetleyicisinin türüne göre de ayarlanabilir. USBX cihaz tarafı, cihaz denetleyicisinin türüne göre kabaca 10-12 K ROM gerektirir. RAM bellek kullanımı, cihaz tarafından Öykünülen sınıfın türüne bağlıdır.

USBX Ayrıca, Işparçacığıx semaforları, zaman uyumu sağlayıcılar ve birden çok iş parçacığı koruması için iş parçacıklarını ve USB veri yolu topolojisini izlemek için g/ç askıya alma ve düzenli işlemeyi kullanır.

### <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS USBX, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/usbx/> .

Aşağıda, depodaki birçok önemli dosyanın bir listesi verilmiştir.

* ***ux_api. h***: Bu C üstbilgi dosyası tüm sistem eş, veri yapılarını ve hizmet prototiplerini içerir.
* ***ux_port. h***: Bu C üstbilgi dosyası, tüm geliştirme aracına özgü veri tanımlarını ve yapılarını içerir.
* ***UX. lib***: Bu, USBX C kitaplığının ikili sürümüdür. Standart paketiyle dağıtılır.
* ***demo_usbx. c***: basıt bır USBX tanıtımı içeren c dosyası

Tüm dosya adları küçük harfli. Bu adlandırma kuralı, komutları UNIX geliştirme platformlarına dönüştürmeyi kolaylaştırır.

## <a name="usbx-installation"></a>USBX yüklemesi

USBX, GitHub deposu yerel makinenize kopyalanarak yüklenir. Aşağıda, bilgisayarınızda USBX deposunun bir kopyasını oluşturmak için tipik sözdizimi verilmiştir:

```c
    git clone https://github.com/azure-rtos/usbx
```

Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında USBX kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.

Aşağıdaki genel yönergeler, neredeyse tüm yüklemeler için geçerlidir:

1. Konak sabit sürücüsüne daha önce ThreadX 'i yüklediğiniz dizini kullanın. Tüm USBX adları benzersizdir ve önceki USBX yüklemesine engel olmaz.
1. _ *_Tx_application_define_* * başlangıcına veya yanına ***ux_system_initialize** _ çağrısı ekleyin. Bu, USBX kaynaklarının başlatıldığı yerdir.
1. ***Ux_device_stack_initialize *** için bir çağrı ekleyin.
1. Gerekli USBX sınıflarını (konak ve/veya cihazlar sınıfları) başlatmak için bir veya daha fazla çağrı ekleyin
1. Sistemde kullanılabilir olan cihaz denetleyicisini başlatmak için bir veya daha fazla çağrı ekleyin.
1. Alt düzey donanım başlatma ve kesme vektör yönlendirmesi eklemek için tx_low_level_initialize. c dosyasını değiştirmeniz gerekebilir. Bu, donanım platformuna özeldir ve burada ele alınmayacak. |
1. Uygulama kaynak kodunu derleme ve USBX ve ThreadX çalışma zamanı kitaplıkları (FileX ve/veya NETX), UX. a (veya UX. lib) ve TX. a (ya da TX. lib) ile bağlantı için gerekli olabilir. Sonuç hedefe indirilebilir ve yürütülür!

## <a name="configuration-options"></a>Yapılandırma seçenekleri

USBX kitaplığını oluşturmak için birkaç yapılandırma seçeneği vardır. Tüm Seçenekler ***ux_user. h*** içinde bulunur.

Aşağıdaki listede her yapılandırma seçeneğinin ayrıntıları verilmiştir.

| Yapılandırma &nbsp; seçeneği | Açıklama |
| --- | --- |
| **UX_PERIODIC_RATE** | Bu değer, belirli bir donanım platformu için saniye başına kaç saat sayısını temsil eder. Varsayılan değer, milisaniye başına 1 değer belirten 1000 ' dir. |
| **UX_THREAD_STACK_SIZE** | Bu değer, USBX iş parçacıklarının bayt cinsinden yığınının boyutudur. Kullanılan işlemciye ve ana bilgisayar denetleyicisine bağlı olarak genellikle 1024 bayt veya 2048 bayt olabilir. |
| **UX_THREAD_PRIORITY_ENUM** | Bu, veri yolu topolojisini izleyen USBX sabit listesi iş parçacıklarının ThreadX öncelik değeridir. |
| **UX_THREAD_PRIORITY_CLASS** | Bu, standart USBX iş parçacıkları için ThreadX öncelik değeridir. |
| **UX_THREAD_PRIORITY_KEYBOARD** | Bu, USBX HID Klavye sınıfı için ThreadX öncelik değeridir. |
| **UX_THREAD_PRIORITY_DCD** | Bu, cihaz denetleyicisi iş parçacığı için ThreadX öncelik değeridir. |
| **UX_NO_TIME_SLICE** | Bu değer aslında iş parçacıkları için kullanılacak zaman dilimini tanımlar. Örneğin, 0 olarak tanımlanmışsa, ThreadX hedef bağlantı noktası zaman dilimlerini kullanmaz. |
| **UX_MAX_SLAVE_CLASS_DRIVER** | Bu, ux_device_stack_class_register aracılığıyla kaydedilenebilir en fazla USBX sınıfı sayısıdır. |
| **UX_MAX_SLAVE_LUN** | Bu değer, cihaz depolama sınıfı sürücüsünde temsil edilen SCSI Mantıksal birimlerinin geçerli sayısını temsil eder. |
| **UX_SLAVE_CLASS_STORAGE_INCLUDE_MMC** | Tanımlı ise, depolama sınıfı, DVD-ROM olan çok ortamlı komutları (MMC) işleymeyecektir. |
| **UX_DEVICE_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES** | Bu değer, CDC-ECD sınıfı ' paket havuzundaki NetX paketlerinin sayısını temsil eder. Varsayılan değer 16 ' dır. |
| **UX_SLAVE_REQUEST_CONTROL_MAX_LENGTH** | Bu değer, cihaz yığınındaki bir denetim uç noktasında alınan en fazla bayt sayısını temsil eder. Varsayılan değer 256 bayttır, ancak bellek kısıtlama ortamlarında azaltılabilir. |
| **UX_DEVICE_CLASS_HID_EVENT_BUFFER_LENGTH** | Bu değer, bir HID raporunun bayt cinsinden uzunluk üst sınırını temsil eder. |
| **UX_DEVICE_CLASS_HID_MAX_EVENTS_QUEUE** | Bu değer, bir kerede sıraya alınabilen en fazla HID raporu sayısını temsil eder. |
| **UX_SLAVE_REQUEST_DATA_MAX_LENGTH** | Bu değer, cihaz yığınındaki bir toplu bitiş noktasında alınan en fazla bayt sayısını temsil eder. Varsayılan değer 4096 bayttır, ancak bellek kısıtlama ortamlarında azaltılabilir. |

## <a name="source-code-tree"></a>Kaynak kod ağacı

USBX dosyaları birkaç dizinde sağlanır.

![Kaynak kod ağacı](media/usbx-device-stack/source-code-tree.png)

Dosyaları adlarıyla tanınabilir hale getirmek için aşağıdaki kural benimsenmiştir:

| Dosya sonek adı  | Dosya açıklaması                          |
| ----------------- | ----------------------------------------- |
| ux_host_stack   | USBX konak yığını çekirdek dosyaları                |
| ux_host_class   | USBX konak yığını sınıfları dosyaları             |
| ux_hcd           | USBX konak yığını denetleyici sürücü dosyaları   |
| ux_device_stack | USBX cihaz yığını çekirdek dosyaları              |
| ux_device_class | USBX cihaz yığını sınıfları dosyaları           |
| ux_dcd           | USBX cihaz yığını denetleyici sürücü dosyaları |
| ux_otg           | USBX OTG denetleyicisi sürücüyle ilgili dosyalar  |
| ux_pictbridge    | USBX PictBridge dosyaları                     |
| ux_utility       | USBX yardımcı program işlevleri                    |
| demo_usbx        | USBX için tanıtım dosyaları              |

## <a name="initialization-of-usbx-resources"></a>USBX kaynaklarının başlatılması

USBX 'in kendi bellek yöneticisi vardır. USBX 'in ana bilgisayar veya cihaz tarafı başlatılmadan önce belleğin USBX 'e ayrılması gerekir. USBX bellek Yöneticisi belleğin önbelleğe alınabilme sistemlerine uyum sağlayabilir.

Aşağıdaki işlev, 128 K normal bellek ile USBX bellek kaynaklarını başlatır ve önbellek güvenli belleği için ayrı bir havuz yoktur:

```c
/* Initialize USBX Memory */
ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

Ux_system_initialize prototipi aşağıdaki gibidir:

```c
UINT ux_system_initialize(VOID *regular_memory_pool_start,
        ULONG regular_memory_size,
        VOID *cache_safe_memory_pool_start,
        ULONG cache_safe_memory_size);
```

Giriş parametreleri:

| Parametre                          | Açıklama                             |
| ---------------------------------- | --------------------------------------- |
| VOID * regular_memory_pool_start    | Normal bellek havuzunun başlangıcı    |
| ULONG regular_memory_size          | Normal bellek havuzunun boyutu         |
| VOID * cache_safe_memory_pool_start | Önbellek güvenli bellek havuzunun başlangıcı |
| ULONG cache_safe_memory_size       | Önbellek güvenli bellek havuzunun boyutu      |

Tüm sistemler önbellek güvenli belleği tanımını gerektirmez. Böyle bir sistemde, bellek işaretçisi için başlatma sırasında geçirilen değerler UX_NULL olarak ayarlanacak ve havuzun boyutu 0 olarak ayarlanır. USBX daha sonra önbellek güvenli havuzunun yerine normal bellek havuzunu kullanacaktır.

Normal belleğin önbellek güvenli olmadığı ve bir denetleyicinin DMA belleği gerçekleştirmesi gereken bir sistemde, önbellek güvenli bölgesinde bir bellek havuzu tanımlamanız gerekir.

## <a name="uninitialization-of-usbx-resources"></a>USBX kaynaklarının başlatılması geri alınıyor

USBX, kaynakları serbest bırakarak sonlandırılabilir. USBX 'i sonlandırmadan önce tüm sınıfların ve denetleyici kaynaklarının düzgün şekilde sonlandırılması gerekir. Aşağıdaki işlev, USBX bellek kaynaklarını başlatır:

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

Ux_system_initialize prototipi aşağıdaki gibidir:

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-device-controller"></a>USB cihaz denetleyicisinin tanımı

Cihaz modunda çalışmak için herhangi bir zamanda yalnızca bir USB cihaz denetleyicisi tanımlanabilir. Uygulama başlatma dosyası bu tanımı içermelidir. Aşağıdaki satır genel bir USB denetleyicisinin tanımını gerçekleştirir:

```c
ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);
```

USB cihazının başlatılması aşağıdaki prototiple sahiptir:

```c
UINT ux_dcd_controller_initialize(ULONG dcd_io,
    ULONG dcd_irq, ULONG dcd_vbus_address);
```

Şu parametrelerle birlikte:

| Pararmetre               | Açıklama                      |
| ------------------------ | -------------------------------- |
| ULONG dcd_io            | Denetleyici GÇ adresi     |
| ULONG dcd_irq           | Denetleyici tarafından kullanılan kesme |
| ULONG dcd_vbus_address | VBUS GıO adresi         |

Aşağıdaki örnek, Storage cihaz sınıfı ve genel bir denetleyici ile USBX 'in cihaz modunda başlatılması örneğidir:

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024), 0, 0);

/* The code below is required for installing the device portion of USBX */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, installation was successful. */

/* Store the number of LUN in this device storage instance: single LUN. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 1;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x1e6bfe;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read = tx_demo_thread_flash_media_read;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write = tx_demo_thread_flash_media_write;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status = tx_demo_thread_flash_media_status;

/* Initialize the device storage class. The class is connected with interface 0 */
status = ux_device_stack_class_register(ux_system_slave_class_storage_name ux_device_class_storage_entry,
    ux_device_class_storage_thread,0, (VOID *)&storage_parameter);

/* Register the device controllers available in this system */
status = ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);

/* If status equals UX_SUCCESS, registration was successful. */
```

## <a name="troubleshooting"></a>Sorun giderme

USBX, bir tanıtım dosyası ve simülasyon ortamıyla birlikte sunulur. Her zaman, hedef donanımda veya belirli bir demo platformunda ilk olarak çalışan tanıtım platformunu almak iyi bir fikirdir.

## <a name="usbx-version-id"></a>USBX sürüm KIMLIĞI

USBX ' in geçerli sürümü, hem Kullanıcı hem de uygulama yazılımının çalışma zamanı sırasında kullanılabilir. Programcı, USBX sürümünü, ***ux_port. h** _ dosyasının inceağından elde edebilir. Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir. Uygulama yazılımı, _ *_ux_port. h_* * içinde tanımlanan _ *_ _ux_version_id_* _ genel dizesini inceleyerek USBX sürümünü alabilir.
