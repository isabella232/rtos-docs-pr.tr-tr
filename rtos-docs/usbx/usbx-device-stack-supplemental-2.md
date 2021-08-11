---
title: Bölüm 2 - USBX Cihaz Sınıfı Konuları
description: USB cihazı RNDIS sınıfı, usb konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak sağlar. Bu sınıf, Microsoft'un özel uygulamasını temel alıyor ve Windows özeldir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2a28196c8f0e29ad94ef9f2d65b143459bf0214f48c345e6bb0d4ea71d520dfd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802640"
---
# <a name="chapter-2---usbx-device-class-considerations"></a>Bölüm 2 - USBX Cihaz Sınıfı Konuları

## <a name="usb-device-rndis-class"></a>USB Cihazı RNDIS Sınıfı

USB cihazı RNDIS sınıfı, usb konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak sağlar. Bu sınıf, Microsoft'un özel uygulamasını temel alıyor ve Windows özeldir.

RNDIS uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildir yapılması gerekir. Aşağıda bir örnek verilmiştir.

```C
unsigned char device_framework_full_speed[] = {
    /* VID: 0x04b4
    PID: 0x1127
    */

    /* Device Descriptor */
    0x12, /* bLength */
    0x01, /* bDescriptorType */
    0x10, 0x01, /* bcdUSB */
    0x02, /* bDeviceClass - CDC */
    0x00, /* bDeviceSubClass */
    0x00, /* bDeviceProtocol */
    0x40, /* bMaxPacketSize0 */
    0xb4, 0x04, /* idVendor */
    0x27, 0x11, /* idProduct */
    0x00, 0x01, /* bcdDevice */
    0x01, /* iManufacturer */
    0x02, /* iProduct */
    0x03, /* iSerialNumber */
    0x01, /* bNumConfigurations */

    /* Configuration Descriptor */
    0x09, /* bLength */
    0x02, /* bDescriptorType */
    0x38, 0x00, /* wTotalLength */
    0x02, /* bNumInterfaces */
    0x01, /* bConfigurationValue */
    0x00, /* iConfiguration */
    0x40, /* bmAttributes - Self-powered */
    0x00, /* bMaxPower */

    /* Interface Association Descriptor */
    0x08, /* bLength */
    0x0b, /* bDescriptorType */
    0x00, /* bFirstInterface */
    0x02, /* bInterfaceCount */
    0x02, /* bFunctionClass - CDC - Communication */
    0xff, /* bFunctionSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bFunctionProtocol - No class specific protocol required */
    0x00, /* iFunction */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x00, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x01, /* bNumEndpoints */
    0x02, /* bInterfaceClass - CDC - Communication */
    0xff, /* bInterfaceSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x83, /* bEndpointAddress */
    0x03, /* bmAttributes - Interrupt */
    0x08, 0x00, /* wMaxPacketSize */
    0xff, /* bInterval */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x01, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x02, /* bNumEndpoints */
    0x0a, /* bInterfaceClass - CDC - Data */
    0x00, /* bInterfaceSubClass - Should be 0x00 */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x02, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x81, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */
};
```

RNDIS sınıfı CDC-ACM ve CDC-ECM'ye çok benzer bir cihaz tanımlayıcısı yaklaşımı kullanır ve ayrıca bir IAD tanımlayıcısı gerektirir. Cihaz tanımlayıcısının tanımı ve gereksinimleri için bkz. CDC-ACM sınıfı.

RNDIS sınıfının etkinleştirilmesi aşağıdaki gibidir.

```C
/* Set the parameters for callback when insertion/extraction of a CDC device. Set to NULL.*/

parameter.ux_slave_class_rndis_instance_activate = UX_NULL;
parameter.ux_slave_class_rndis_instance_deactivate = UX_NULL;

/* Define a local NODE ID. */

parameter.ux_slave_class_rndis_parameter_local_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_local_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_local_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_local_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_local_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_local_node_id[5] = 0x78;

/* Define a remote NODE ID. */

parameter.ux_slave_class_rndis_parameter_remote_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_remote_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_remote_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_remote_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_remote_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_remote_node_id[5] = 0x79;

/* Set extra parameters used by the RNDIS query command with certain OIDs. */

parameter.ux_slave_class_rndis_parameter_vendor_id = 0x04b4 ;
parameter.ux_slave_class_rndis_parameter_driver_version = 0x1127;
ux_utility_memory_copy(parameter.ux_slave_class_rndis_parameter_vendor_description,
    "ELOGIC RNDIS", 12);

/* Initialize the device rndis class. This class owns both interfaces. */
status = ux_device_stack_class_register(_ux_system_slave_class_rndis_name,
    ux_device_class_rndis_entry, 1,0, &parameter);
```

CDC-ECM'de olduğu gibi, RNDIS sınıfı bir yerel ve bir uzak olmak için 2 düğüm gerektirir, ancak uzak düğümü açıklayan bir dize tanımlayıcısına sahip olmak gerekli değildir.

Ancak Microsoft'un özel mesajlaşma mekanizması nedeniyle bazı ek parametreler gereklidir. İlk olarak satıcı kimliğinin geçir olması gerekir. Benzer şekilde, RNDIS'nin sürücü sürümü. Bir satıcı dizesi de ver gerekir.

RNDIS sınıfında her iki şekilde de veri aktarmak için yerleşik API'ler vardır, ancak kullanıcı uygulaması, USB Ethernet cihazıyla NetX üzerinden iletişim kuracak şekilde uygulamaya gizlenir.

USBX RNDIS sınıfı, NetX Ağ Azure RTOS yakından bağlanır. Hem NetX hem de USBX RNDIS sınıfını kullanan bir uygulama, NetX ağ yığınını her zamanki gibi etkinleştirir, ancak buna ek olarak USB ağ yığınını aşağıdaki gibi etkinleştirmesi gerekir.

```C
/* Initialize the NetX system. */

nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

USB ağ yığınının yalnızca bir kez etkinleştirilmesi gerekir ve RNDIS'e özgü değildir, ancak NetX hizmetleri gerektiren herhangi bir USB sınıfı için gereklidir.

RNDIS sınıfı, Microsoft işletim sistemlerine özgü olduğu için MAC OS ve Linux konakları tarafından tanınmaz. Windows platformlarında, cihaz tanımlayıcısıyla eşleşen konakta bir .inf dosyasının mevcut olması gerekir. Microsoft, RNDIS sınıfı için bir şablon sağlar ve bu şablon usbx_windows_host_files bulunabilir. Dosyanın daha yeni Windows için RNDIS_Template.inf dosyası kullanılmalıdır. Bu dosya, cihaz tarafından kullanılan PID/VID'i yansıtacak şekilde değiştirilmelidir. PiD/VID, şirket ve ürün USB-IF kaydı olduğunda son müşteriye özgü olur. Inf dosyasında değiştirilen alanlar burada bulunur.

```Inf
[DeviceList]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00

[DeviceList.NTamd64]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00
```

RNDIS cihazın cihaz çerçevesinde PID/VID, cihaz tanımlayıcısında depolanır (yukarıda bildirilen cihaz tanımlayıcısına bakın)

USB ana bilgisayar sistemleri USB RNDIS cihazını bulasa, bir ağ arabirimi bağlar ve cihaz ağ protokolü yığınıyla kullanılabilir. Başvuru için bkz. konak İşletim Sistemi.

## <a name="usb-device-dfu-class"></a>USB Cihazı DFU Sınıfı

USB cihazı DFU sınıfı, bir USB konak sisteminin cihaz üretici yazılımını bir konak uygulamasına göre güncelleştirmesini sağlar. DFU sınıfı bir USB-IF standart sınıfıdır.

USBX DFU sınıfı görece basittir. Bu cihaz tanımlayıcısı için bir denetim uç noktası değil başka bir şey gerekir. Bu sınıf çoğu zaman USB bileşik cihazına ekli olur. Cihaz bir depolama cihazı veya bir iletişim cihazı gibi herhangi bir şey olabilir ve eklenen DFU arabirimi, ana bilgisayarı cihazın üretici yazılımının hemen güncelleştirilebilir olduğu konusunda bilgilendirebilir.

DFU sınıfı 3 adımda çalışır. İlk olarak cihaz, dışarı aktarıldı sınıfını kullanarak normal şekilde bağlar. Ana bilgisayar (Windows Linux) üzerinde bir uygulama DFU sınıfına alıştırma yapıyor ve cihazı DFU moduna sıfırlamak için bir istek gönderiyor. Cihaz kısa bir süre (ana bilgisayar ve cihaz bir RESET dizisini algılamak için yeterlidir) veri yollarından kaybolur ve yeniden başlatıldıktan sonra yalnızca DFU modunda olur ve konak uygulamanın bir üretici yazılımı yükseltmesi göndermesini bekler. Üretici yazılımı yükseltmesi tamamlandığında, konak uygulaması cihazı sıfırlar ve yeniden numaralandıktan sonra cihaz yeni üretici yazılımıyla normal çalışmasına geri döner.

DFU cihaz çerçevesi şuna benzer.

```C
UCHAR device_framework_full_speed[] = {

    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x40,
    0x99, 0x99, 0x00, 0x00, 0x00, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x1b, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor for DFU. */
    0x09, 0x04, 0x00, 0x00, 0x00, 0xFE, 0x01, 0x01, 0x00,

    /* Functional descriptor for DFU. */
    0x09, 0x21, 0x0f, 0xE8, 0x03, 0x40, 0x00, 0x00,
    0x01,

};
```

Bu örnekte, DFU tanımlayıcısı başka hiçbir sınıfla ilişkili değildir. Basit bir arabirim tanımlayıcısına sahiptir ve ekli başka uç nokta yoktur. Cihazın DFU özelliklerini açıklayan bir İşlevsel tanımlayıcı vardır.

DFU yeteneklerinin açıklaması aşağıdaki gibidir.

| Name             | Uzaklık  | Boyut | tür      | Description |
|------------------|----------|------|-----------|------------|
| bmAttributes  | 2     | 1   | Bit alanı | Bit 3: Cihaz, bir veri DFU_DETACH aldığında veri DFU_DETACH gerçekleştirecek. Ana bilgisayar USB Sıfırlaması sorununa neden olmaz. (bitWillDetach) 0 = 1 yok = evet Bit 2: Cihaz, Usb üzerinden Iletişim Kura aşamasının ardından iletişim kurabilir. (bitManstationTolerant) 0 = hayır, bus sıfırlaması 1 = evet Bit 1: karşıya yükleme özellikli (bitCanUpload) 0 = hayır 1 = evet Bit 0: indirme özellikli (bitCanDnload) 0 = 1 = evet  |
| wDetachTimeOut  | 3      | 2  | sayı    | Cihazın istek alındıktan sonra bekleyeceği süre DFU_DETACH. Bu süre USB sıfırlaması olmadan sona ererse, cihaz Yeniden Yapılandırma aşamasını sonlandırılır ve normal işleme geri döner. Bu, cihazın bekleyeceği en uzun zamanı (süreye göre vb.) temsil eder. USBX bu değeri 1000 ms olarak ayarlar.  |
| wTransferSize  | 5      | 2  | sayı    | Cihazın denetim yazma işlemi başına kabul edile maksimum bayt \- sayısı. USBX bu değeri 64 bayt olarak ayarlar. |

DFU sınıfının bildirimi aşağıdaki gibidir:

```C
/* Store the DFU parameters. */

dfu_parameter.ux_slave_class_dfu_parameter_instance_activate =
    tx_demo_thread_dfu_activate;

dfu_parameter.ux_slave_class_dfu_parameter_instance_deactivate =
    tx_demo_thread_dfu_deactivate;

dfu_parameter.ux_slave_class_dfu_parameter_read =
    tx_demo_thread_dfu_read;

dfu_parameter.ux_slave_class_dfu_parameter_write =
    tx_demo_thread_dfu_write;

dfu_parameter.ux_slave_class_dfu_parameter_get_status =
    tx_demo_thread_dfu_get_status;

dfu_parameter.ux_slave_class_dfu_parameter_notify =
    tx_demo_thread_dfu_notify;

dfu_parameter.ux_slave_class_dfu_parameter_framework =
    device_framework_dfu;

dfu_parameter.ux_slave_class_dfu_parameter_framework_length =
    DEVICE_FRAMEWORK_LENGTH_DFU;

/* Initialize the device dfu class. The class is connected with interface
1 on configuration 1. */
status = ux_device_stack_class_register(_ux_system_slave_class_dfu_name,
    ux_device_class_dfu_entry, 1, 0,
    (VOID *)&dfu_parameter);

if (status!=UX_SUCCESS) return;
```

DFU sınıfının hedefe özgü bir cihaz üretici yazılımı uygulamasıyla çalışması gerekir. Bu nedenle, üretici yazılımı okuma ve yazma bloklarını geri çağırma ve üretici yazılımı güncelleştirme uygulamasından durum almak için birkaç çağrı tanımlar. DFU sınıfı ayrıca üretici yazılımının aktarımının bir başlangıç ve bitişi olduğunda uygulamayı bilgilendirmek için bir notify callback işlevine sahiptir.

Aşağıda tipik bir DFU uygulama akışının açıklaması ve ardından yer vemektedir.

![DFU uygulama akışı](./media/usbx-device-stack-supplemental/dfu-application-flow.png)

DFU sınıfının en büyük zor olduğu ana bilgisayar üzerinde üretici yazılımını indirmek için doğru uygulamayı almaktır. Microsoft veya USB-IF tarafından sağlanan bir uygulama yoktur. Bazı paylaşım yazılımları vardır ve Linux'ta makul bir şekilde ve daha az ölçüde çalışırlar Windows.

Linux'ta dfu-utils'i kullanarak buradan ulaşabilirsiniz: dfu yardımcı programıyla ilgili birçok bilgi [https://wiki.openmoko.org/wiki/Dfu-util](https://wiki.openmoko.org/wiki/Dfu-util) şu bağlantıda da bulunabilir: [https://www.libusb.org/wiki/windows_backend](https://www.libusb.org/wiki/windows_backend)

DFU'nun Linux uygulaması, konak ve cihaz arasındaki sıfırlama dizisini doğru gerçekleştirir ve bu nedenle cihazın bunu yapma ihtiyacı olmaz. Linux, bmAttributes *bitWillDetach'in* 0 olduğunu kabul eder. Windows diğer tarafta cihazın sıfırlama gerçekleştirmesi gerekir.

Bu Windows, USB kayıt defterinin USB cihazını PID/VID ile ve DFU uygulaması tarafından kullanılacak USB kitaplığıyla ilişkilendirmesi gerekir. Bu, burada bulunan ücretsiz Zadig yardımcı programıyla kolayca yapılabilir: [https://sourceforge.net/projects/libwdi/files/zadig/](https://sourceforge.net/projects/libwdi/files/zadig/) .

Zadig'i ilk kez çalıştırmanız şu ekranı gösterir:

![Zadig'i ilk kez çalıştırma](./media/usbx-device-stack-supplemental/zadig.png)

Cihaz listesinden cihazınızı bulun ve libusb Windows sürücüsüyle ilişkilendirmek. Bu, cihazın PID/VID'sini DFU yardımcı programları tarafından Windows USB kitaplığıyla bağlar.

DFU komutunu çalıştırmak için sıkıştırılmış dfu yardımcı programlarını bir dizine açıp libusb dll dosyasının da aynı dizinde mevcut olduğundan emin olun. DFU yardımcı programlarının komut satırına bir DOS kutusundan çalışması gerekir.

İlk olarak cihazın listelenmiş **olup olmadığını belirlemek için dfu-util –l** komutunu yazın. Yoksa, cihazın listelenmiş ve USB kitaplığıyla ilişkili olduğundan emin olmak için Zadig'i çalıştırın. Aşağıdaki gibi bir ekran görürsünüz:

```Command-line
C:\usb specs\DFU\dfu-util-0.6&gt;dfu-util -l dfu-util 0.6

Copyright 2005-2008 Weston Schmidt, Harald Welte and OpenMoko Inc.
Copyright 2010-2012 Tormod Volden and Stefan Schmidt
This program is Free Software and has ABSOLUTELY NO WARRANTY
Found Runtime: [0a5c:21bc] devnum=0, cfg=1, intf=3, alt=0, name="UNDEFINED"
```

Sonraki adım, indirilecek dosyayı hazırlamak olacak. USBX DFU sınıfı bu dosya üzerinde herhangi bir doğrulama gerçekleştirmez ve iç biçiminden bağımsızdır. Bu üretici yazılımı dosyası hedefe çok özeldir, ancak DFU veya USBX'e özgü değildir.

Daha sonra dfu-util'e aşağıdaki komutu yazarak dosyayı göndermesi talimatı ve ardından:

```Command-line
dfu-util –R –t 64 -D file_to_download.hex
```

Üretici yazılımı tamamen indirilene kadar dfu-util dosya indirme işlemini görüntülemeli.

## <a name="usb-device-pima-class-ptp-responder"></a>USB Cihazı PIMA Sınıfı (PTP Yanıtlayan)

USB cihazı PIMA sınıfı, bir USB ana bilgisayar sisteminin (Başlatıcı)

Medya dosyalarını aktaran PIMA cihazı (Resonder). USBX Pima Sınıfı, PTP sınıfı olarak da bilinen USB-IF PIMA 15740 sınıfına (Resim Aktarım Protokolü için) uyum sağlar.

USBX cihaz tarafı PIMA sınıfı aşağıdaki işlemleri destekler.

| İşlem kodu                                    | Değer | Açıklama                       |
|---------------------------------------------------|---------|-----------------------------------------------------|
| UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO    | 0x1001  | Cihaz tarafından desteklenen işlemleri ve olayları alma                                                         |
| UX_DEVICE_CLASS_PIMA_OC_OPEN_SESSION        | 0x1002  | Konak ve cihaz arasında oturum açma                                                            |
| UX_DEVICE_CLASS_PIMA_OC_CLOSE_SESSION       | 0x1003  | Konak ve cihaz arasındaki oturumu kapatma                                                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_IDS    | 0x1004  | Cihazın depolama kimliğini döndürür. USBX PIMA yalnızca bir depolama kimliği kullanır |
| UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_INFO   | 0x1005  | Maksimum kapasite ve boş alan gibi depolama nesnesi hakkında bilgi dönüş                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_NUM_OBJECTS    | 0x1006  | Depolama cihazında bulunan nesne sayısını iade edin                                              |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_HANDLES | 0x1007  | Depolama cihazında nesnelerin tanıtıcı dizisini döndürür                                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_INFO    | 0x1008  | Nesnenin adı, oluşturma tarihi, değiştirme tarihi gibi bir nesne hakkında bilgi dönüş |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT          | 0x1009  | Belirli bir nesneyle ilgili verileri iade                                                         |
| UX_DEVICE_CLASS_PIMA_OC_GET_THUMB           | 0x100A  | Bir nesne hakkında varsa küçük resmi gönderme                                                           |
| UX_DEVICE_CLASS_PIMA_OC_DELETE_OBJECT       | 0x100B  | Medyada bir nesneyi silme                                                                             |
| UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT_INFO   | 0x100C  | Medyada oluşturulması için cihaza bir nesne hakkında bilgi gönderme                              |
| UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT         | 0x100D  | Cihaza bir nesne için veri gönderme                                                                     |
| UX_DEVICE_CLASS_PIMA_OC_FORMAT_STORE        | 0x100F  | Cihaz medyalarını temizleme                                                                                    |
| UX_DEVICE_CLASS_PIMA_OC_RESET_DEVICE        | 0x0110  | Hedef cihazı sıfırlama                                                                                   |

| İşlem Kodu                                         | Değer | Açıklama |
|--------------------------------------------------------|-------|-----------------------------------------|
| UX_DEVICE_CLASS_PIMA_EC_CANCEL_TRANSACTION       | 0x4001  | Geçerli işlemi iptal eder                                                 |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_ADDED             | 0x4002  | Cihaz medyaya bir nesnesi eklendi ve konak tarafından alınamadı\ |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_REMOVED           | 0x4003  | Cihaz medyadan bir nesne silindi                                |
| UX_DEVICE_CLASS_PIMA_EC_STORE_ADDED              | 0x4004  | Cihaza bir medya eklendi                                            |
| UX_DEVICE_CLASS_PIMA_EC_STORE_REMOVED            | 0x4005  | Cihazdan bir medya silindi                                        |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_PROP_CHANGED     | 0x4006  | Cihaz özellikleri değişti                                                  |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_INFO_CHANGED     | 0x4007  | Nesne bilgileri değiştirildi                                               |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_INFO_CHANGE      | 0x4008  | Bir cihaz değişti                                                            |
| UX_DEVICE_CLASS_PIMA_EC_REQUEST_OBJECT_TRANSFER | 0x4009  | Cihaz, bir nesnenin konaktan aktarımını istiyor                     |
| UX_DEVICE_CLASS_PIMA_EC_STORE_FULL               | 0x400A  | Cihaz medyanın dolu olduğunu rapor ediyor                                                |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_RESET             | 0x400B  | Cihaz sıfırlandı raporlarında                                                     |
| UX_DEVICE_CLASS_PIMA_EC_STORAGE_INFO_CHANGED    | 0x400C  | Depolama bilgileri cihazda değişti                                   |
| UX_DEVICE_CLASS_PIMA_EC_CAPTURE_COMPLETE         | 0x400D  | Yakalama tamamlandı                                                            |

USBX PIMA cihaz sınıfı, konaktan PIMA komutlarını dinlemek için bir TX İş Parçacığı kullanır.

PIMA komutu bir komut bloğu, veri bloğu ve durum aşamasından oluşur.

İşlev ux_device_class_pima_thread, konak tarafından PIMA komutu almak için yığına bir istek göndermektedir. PIMA komutunun kodu çözüldü ve içerik için doğrulandı. Komut bloğu geçerli ise uygun komut işleyiciye dallar.

Çoğu PIMA komutu yalnızca konak tarafından bir oturum açıldığında yürütülebiliyor. Tek özel durum, komutunun **UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO.** USBX PIMA uygulamasıyla, başlatıcı ile Yanıtlayıcı arasında herhangi bir anda yalnızca bir oturum açılabilir. Tek oturum içindeki tüm işlemler engellidir ve önceki tamamlanmadan yeni bir işlem başlatılamayabilirsiniz.

PIMA işlemleri 3 aşamadan, komut aşamasından, isteğe bağlı bir veri aşamasından ve yanıt aşamasından oluşur. Bir veri aşaması varsa, yalnızca bir yönde olabilir.

Başlatıcı her zaman PIMA işlemlerinin akışını belirler, ancak Yanıtlayıcı bir oturum sırasında meydana gelen durum değişikliklerini bildirmek için başlatıcıya geri olayları başlatabilirsiniz.

Aşağıdaki diyagramda, bir veri nesnesinin konak ile PIMA cihaz sınıfı arasında aktarımını gösterir.

![PIMA işlemleri](./media/usbx-device-stack-supplemental/pima-transactions.png)

## <a name="initialization-of-the-pima-device-class"></a>PIMA cihaz sınıfını başlatma

PIMA cihaz sınıfı, başlatma sırasında uygulama tarafından sağlanan bazı parametrelere ihtiyaç gösterir.

Aşağıdaki parametreler cihaz ve depolama bilgilerini açıklar.

- `ux_device_class_pima_manufacturer`
- `ux_device_class_pima_model`
- `ux_device_class_pima_device_version`
- `ux_device_class_pima_serial_number`
- `ux_device_class_pima_storage_id`
- `ux_device_class_pima_storage_type`
- `ux_device_class_pima_storage_file_system_type`
- `ux_device_class_pima_storage_access_capability`
- `ux_device_class_pima_storage_max_capacity_low`
- `ux_device_class_pima_storage_max_capacity_high`
- `ux_device_class_pima_storage_free_space_low`
- `ux_device_class_pima_storage_free_space_high`
- `ux_device_class_pima_storage_free_space_image`
- `ux_device_class_pima_storage_description`
- `ux_device_class_pima_storage_volume_label`

PIMA sınıfı ayrıca belirli olayları uygulamaya bildirmek veya yerel medyadan/medyadan/medyadan veri almak/depolamak için uygulamaya geri çağırma kaydını gerektirir. Geri çağırmalar aşağıdaki gibidir.

- `ux_device_class_pima_object_number_get`
- `ux_device_class_pima_object_handles_get`
- `ux_device_class_pima_object_info_get`
- `ux_device_class_pima_object_data_get`
- `ux_device_class_pima_object_info_send`
- `ux_device_class_pima_object_data_send`
- `ux_device_class_pima_object_delete`

Aşağıdaki örnekte PIMA'nın istemci tarafının nasıl başlatılmış olduğu göstermektedir. Bu örnekte PIMA için bir istemci olarak Pictbridge 2011 ve 2012 yıllarına göre 2004'e kadar 2008'den az

```C
/* Initialize the first XML object valid in the pictbridge instance.

Initialize the handle, type and file name.

The storage handle and the object handle have a fixed value of 1 in our implementation. */

object_info = pictbridge -> ux_pictbridge_object_client;

object_info -> ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_SCRIPT;
object_info -> ux_device_class_pima_object_storage_id = 1;
object_info -> ux_device_class_pima_object_handle_id = 2;

ux_utility_string_to_unicode(_ux_pictbridge_ddiscovery_name,
    object_info -> ux_device_class_pima_object_filename);

/* Initialize the head and tail of the notification round robin buffers.
   At first, the head and tail are pointing to the beginning of the array.
*/

pictbridge -> ux_pictbridge_event_array_head =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_tail =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_end =
    pictbridge -> ux_pictbridge_event_array +
    UX_PICTBRIDGE_MAX_EVENT_NUMBER;

/* Initialialize the pima device parameter. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_manufacturer =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_model =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_serial_number =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_id = 1;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_type =
    UX_DEVICE_CLASS_PIMA_STC_FIXED_RAM;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_file_system_type =
    UX_DEVICE_CLASS_PIMA_FSTC_GENERIC_FLAT;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_access_capability =
    UX_DEVICE_CLASS_PIMA_AC_READ_WRITE;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_image = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_description =
    _ux_pictbridge_volume_description;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_volume_label =
    _ux_pictbridge_volume_label;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_number_get =
    ux_pictbridge_dpsclient_object_number_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_handles_get =
    ux_pictbridge_dpsclient_object_handles_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_get =
    ux_pictbridge_dpsclient_object_info_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_get =
    ux_pictbridge_dpsclient_object_data_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_send =
    ux_pictbridge_dpsclient_object_info_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_send =
    ux_pictbridge_dpsclient_object_data_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_delete =
    ux_pictbridge_dpsclient_object_delete;

/* Store the instance owner. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_application =
    (VOID *) pictbridge;

/* Initialize the device pima class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_pima_name,
    ux_device_class_pima_entry, 1, 0, (VOID *)&pictbridge -> ux_pictbridge_pima_parameter);

/* Check status. */
if (status != UX_SUCCESS)
```

## <a name="ux_device_class_pima_object_add"></a>ux_device_class_pima_object_add

Nesne ekleme ve olayı ana bilgisayarla gönderme

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_add(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG object_handle);
```

### <a name="description"></a>Description

PIMA sınıfının bir nesnesi eklemesi ve ana bilgisayarı bilgilendirmesi gereken bu işlev çağrılır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi
- **object_handle:** Nesnenin tanıtıcısı.

### <a name="example"></a>Örnek

```C
/* Send the notification to the host that an object has been added. */

status = ux_device_class_pima_object_add(pima, UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST);
```

## <a name="ux_device_class_pima_object_number_get"></a>ux_device_class_pima_object_number_get

Uygulamanın nesne numarasını alma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_number_get(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG *object_number);
```

### <a name="description"></a>Description

PIMA sınıfının yerel sistemdeki nesne sayısını almaları ve ana bilgisayarlarına geri göndermesi gereken bu işlev çağrılır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi
- **object_number:** Döndürülen nesne sayısının adresi

### <a name="example"></a>Örnek

```C
UINT ux_pictbridge_dpsclient_object_number_get(UX_SLAVE_CLASS_PIMA *pima, ULONG *number_objects)
{
    /* We force the number of objects to be 1 only here. This will be the XML scripts. */
    *number_objects = 1;
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_handles_get"></a>ux_device_class_pima_object_handles_get

Nesne tanıtıcı dizisini döndürür

### <a name="prototype"></a>Prototype

```C
UINT **ux_device_class_pima_object_handles_get**(
    UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number);
```

### <a name="description"></a>Description

PIMA sınıfının yerel sistemde nesne tanıtıcı dizisini almak ve ana bilgisayar geri göndermek için ihtiyacı olduğunda bu işlev çağrılır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **object_handles_format_code:** Tanıtıcılar için kodu biçimlendirme
- **object_handles_association:** Nesne ilişkilendirme kodu
- **object_handle_array:** Tanıtıcıların nerede depolan bir adrese
- **object_handles_max_number:** Dizide en fazla tanıtıcı sayısı

### <a name="example"></a>Örnek

```C
UINT ux_pictbridge_dpsclient_object_handles_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *) pima -> ux_device_class_pima_application;

    /* Set the pima pointer to the pictbridge instance. */
    pictbridge -> ux_pictbridge_pima = (VOID *) pima;

    /* We say we have one object but the caller might specify different format code and associations. */
    object_info = pictbridge -> ux_pictbridge_object_client;

    /* Insert in the array the number of found handles so far: 0. */
    ux_utility_long_put((UCHAR *)object_handles_array, 0);

    /* Check the type demanded. */

    if (object_handles_format_code == 0 || object_handles_format_code ==
        0xFFFFFFFF || object_info -> ux_device_class_pima_object_format ==
        object_handles_format_code)
    {
        /* Insert in the array the number of found handles. This handle is for the client XML script. */
        ux_utility_long_put((UCHAR *)object_handles_array, 1);

        /* Adjust the array to point after the number of elements. */
        object_handles_array++;

        /* We have a candicate. Store the handle. */
        ux_utility_long_put((UCHAR *)object_handles_array, object_info ->
            ux_device_class_pima_object_handle_id);
    }

    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_info_get"></a>ux_device_class_pima_object_info_get

Nesne bilgilerini iade edin

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_info_get(
    struct UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handle, 
    UX_SLAVE_CLASS_PIMA_OBJECT **object);
```

### <a name="description"></a>Description

PIMA sınıfının yerel sistemde nesne tanıtıcı dizisini almak ve ana bilgisayar geri göndermek için ihtiyacı olduğunda bu işlev çağrılır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **object_handles:** Nesnenin tanıtıcısı
- **object**: Nesne işaretçisi adresi

### <a name="example"></a>Örnek

```C
UINT ux_pictbridge_dpsclient_object_info_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UX_SLAVE_CLASS_PIMA_OBJECT **object)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST)) {

        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge -> ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;
    } else
        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;
    /* Return the pointer to this object. */
    *object = object_info;

    /* We are done. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_get"></a>ux_device_class_pima_object_data_get

Nesne verilerini iade

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_info_get(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length_requested,
    ULONG *object_actual_length);
```

### <a name="description"></a>Description

PIMA sınıfının yerel sistemden nesne verilerini almaları ve ana bilgisayarlarına geri göndermesi gereken bu işlev çağrılır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **object_handle:** Nesnenin tanıtıcısı
- **object_buffer:** Nesne arabellek adresi
- **object_length_requested:** İstemci tarafından uygulamaya istenen nesne veri uzunluğu
- **object_actual_length:** Uygulama tarafından döndürülen nesne veri uzunluğu

### <a name="example"></a>Örnek

```C
UINT ux_pictbridge_dpsclient_object_data_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UCHAR *object_buffer, ULONG object_offset,
    ULONG object_length_requested, ULONG *object_actual_length)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    UCHAR *pima_object_buffer;
    ULONG actual_length;
    UINT status;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST))
    {
        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;

       /* Is this the corrent handle ? */
       if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
       {
           /* Get the pointer to the object buffer. */
           pima_object_buffer = object_info -> ux_device_class_pima_object_buffer;

           /* Copy the demanded object data portion. */
           ux_utility_memory_copy(object_buffer, pima_object_buffer +
               object_offset, object_length_requested);

           /* Update the length requested. for a demo, we do not do any checking. */
           *object_actual_length = object_length_requested;

           /* What cycle are we in ? */
           if (pictbridge -> ux_pictbridge_host_client_state_machine &
               UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST)
            {
                /* Check if we are blocking for a client request. */
                if (pictbridge -> ux_pictbridge_host_client_state_machine &
                    UX_PICTBRIDGE_STATE_MACHINE_CLIENT_REQUEST_PENDING)

                    /* Yes we are pending, send an event to release the pending request. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_STATE_MACHINE_READY, TX_OR);

               /* Since we are in host request, this indicates we are done with the cycle. */
               pictbridge -> ux_pictbridge_host_client_state_machine =
                   UX_PICTBRIDGE_STATE_MACHINE_IDLE;

            }

            /* We have copied the requested data. Return OK. */
            return(UX_SUCCESS);

        }
    }
    else
    {

        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;

        /* Obtain the data from the application jobinfo callback. */
        status = pictbridge -> ux_pictbridge_jobinfo.
            ux_pictbridge_jobinfo_object_data_read(pictbridge, object_buffer, object_offset,
            object_length_requested, &actual_length);

        /* Save the length returned. */
        *object_actual_length = actual_length;

        /* Return the application status. */
        return(status);

    }

    /* Could not find the handle. */

    return(UX_DEVICE_CLASS_PIMA_RC_INVALID_OBJECT_HANDLE);
}
```

## <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

Konak nesne bilgilerini gönderir

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_info_send(
    UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, 
    ULONG *object_handle);
```

### <a name="description"></a>Description

PiMA sınıfının gelecekteki depolama için yerel sistemde nesne bilgilerini almaları gereken bu işlev çağrılır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi
- **object**: Nesnenin işaretçisi
- **object_handle:** Nesnenin tanıtıcısı

### <a name="example"></a>Örnek

```C
UINT ux_pictbridge_dpsclient_object_info_send(UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, ULONG *object_handle)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info; UCHAR
    string_discovery_name[UX_PICTBRIDGE_MAX_FILE_NAME_SIZE];

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* We only have one object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Copy the demanded object info set. */
    ux_utility_memory_copy(object_info, object,
        UX_SLAVE_CLASS_PIMA_OBJECT_DATA_LENGTH);

    /* Store the object handle. In Pictbridge we only receive XML scripts so the handle is hardwired to 1. */
    object_info -> ux_device_class_pima_object_handle_id = 1;
    *object_handle = 1;

    /* Check state machine. If we are in discovery pending mode, check file name of this object. */
    if (pictbridge -> ux_pictbridge_discovery_state ==
        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_PENDING)
    {
        /* We are in the discovery mode. Check for file name. It must match
           HDISCVRY.DPS in Unicode mode. */

        /* Check if this is a script. */
        if (object_info -> ux_device_class_pima_object_format ==
            UX_DEVICE_CLASS_PIMA_OFC_SCRIPT)
        {

            /* Yes this is a script. We need to search for the HDISCVRY.DPS file name. Get the file name in a ascii format. */
            ux_utility_unicode_to_string(object_info ->
                ux_device_class_pima_object_filename,
                string_discovery_name);

            /* Now, compare it to the HDISCVRY.DPS file name. Check length first. */
            if (ux_utility_string_length_get(_ux_pictbridge_hdiscovery_name)
                == ux_utility_string_length_get(string_discovery_name))
            {

                /* So far, the length of name of the files are the same. Compare names now. */
                if(ux_utility_memory_compare(_ux_pictbridge_hdiscovery_name,
                    string_discovery_name,
                    ux_utility_string_length_get(string_discovery_name)) == UX_SUCCESS)
                {
                    /* We are done with discovery of the printer. We can now send notifications when the camera wants to print an object. */
                    pictbridge -> ux_pictbridge_discovery_state =
                        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_COMPLETE;

                    /* Set an event flag if the application is listening. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY, TX_OR);

                    /* There is no object during th discovery cycle. */
                    return(UX_SUCCESS);
                }
            }
        }
    }
    /* What cycle are we in ? */
    if (pictbridge -> ux_pictbridge_host_client_state_machine ==
        UX_PICTBRIDGE_STATE_MACHINE_IDLE)

        /* Since we are in idle state, we must have received a request from the host. */
        pictbridge -> ux_pictbridge_host_client_state_machine =
            UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST;

    /* We have copied the requested data. Return OK. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_send"></a>ux_device_class_pima_object_data_send

Konak nesne verilerini gönderir

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_data_send(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, 
    ULONG phase, 
    UCHAR *object_buffer,
    ULONG object_offset, 
    ULONG object_length);
```

### <a name="description"></a>Description

PIMA sınıfının depolama için yerel sistemde nesne verilerini almaları gerekirken bu işlev çağrılır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi
- **object_handle:** Nesnenin tanıtıcısı
- **aşama:** aktarımın aşaması (etkin veya tamamlandı)
- **object_buffer:** Nesne arabellek adresi
- **object_offset:** Veri adresi
- **object_length:** Uygulama tarafından gönderilen nesne veri uzunluğu

### <a name="example"></a>Örnek

```C
UINT ux_pictbridge_dpsclient_object_data_send(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    ULONG phase,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length)
{
    UINT status;
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    ULONG event_flag;
    UCHAR *pima_object_buffer;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Get the pointer to the pima object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Is this the corrent handle ? */
    if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
    {
        /* Get the pointer to the object buffer. */
        pima_object_buffer = object_info ->
            ux_device_class_pima_object_buffer;

        /* Check the phase. We should wait for the object to be completed and the response sent back before parsing the object. */
        if (phase == UX_DEVICE_CLASS_PIMA_OBJECT_TRANSFER_PHASE_ACTIVE)
        {
            /* Copy the demanded object data portion. */
            ux_utility_memory_copy(pima_object_buffer + object_offset,
                object_buffer, object_length);

            /* Save the length of this object. */
            object_info -> ux_device_class_pima_object_length = object_length;

            /* We are not done yet. */
            return(UX_SUCCESS);
        }
        else
        {
            /* Completion of transfer. We are done. */
            return(UX_SUCCESS);
        }
    }
}
```

## <a name="ux_device_class_pima_object_delete"></a>ux_device_class_pima_object_delete

Yerel nesneyi silme

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_delete(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle);
```

### <a name="description"></a>Description

Bu işlev, PIMA sınıfının yerel depolamadaki bir nesneyi silmesi gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi
- **object_handle**: nesnenin tanıtıcısı

### <a name="example"></a>Örnek

```C
UINT ux_pictbridge_dpsclient_object_delete(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle)
{
    /* Delete the object pointer by the handle. */

}
```

## <a name="usb-device-audio-class"></a>USB cihaz ses sınıfı

USB cihaz ses sınıfı, USB konak sisteminin cihazla bir ses cihazı olarak iletişim kurmasına olanak tanır. Bu sınıf, USB Standart ve USB ses sınıfı 1,0 veya 2,0 standardını temel alır.

USB ses uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildirilmesine ihtiyacı vardır. Ses 2,0 konuşmacı örneği aşağıda verilmiştir:

```C
unsigned char device_framework_high_speed[] = {

    /* --- Device Descriptor 18 bytes
    0x00 bDeviceClass: Refer to interface
    0x00 bDeviceSubclass: Refer to interface
    0x00 bDeviceProtocol: Refer to interface

    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    */

    /* 0 bLength, bDescriptorType */ 18, 0x01,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00, 0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 0x08,
    /* 8 idVendor, idProduct */ 0x84, 0x84, 0x03, 0x00,
    /* 12 bcdDevice */ 0x00, 0x02,
    /* 14 iManufacturer, iProduct, iSerialNumber */ 0, 0, 0,
    /* 17 bNumConfigurations */ 1,
    /* ---------------- Device Qualifier Descriptor */
    /* 0 bLength, bDescriptorType */ 10, 0x06,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00,0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 8,
    /* 8 bNumConfigurations */ 1,
    /* 9 bReserved */ 0,
    /* --- Configuration Descriptor (9+8+73+55=145, 0x91) */
    /* 0 bLength, bDescriptorType */ 9, 0x02,
    /* 2 wTotalLength */ 145, 0,
    /* 4 bNumInterfaces, bConfigurationValue */ 2, 1,
    /* 6 iConfiguration */ 0,
    /* 7 bmAttributes, bMaxPower */ 0x80, 50,
    /* ----------- Interface Association Descriptor */
    /* 0 bLength, bDescriptorType */ 8, 0x0B,
    /* 2 bFirstInterface, bInterfaceCount */ 0, 2,
    /* 4 bFunctionClass : 0x01 (Audio) */ 0x01,
    /* 5 bFunctionSubClass : 0x00 (UNDEFINED) */ 0x00,
    /* 6 bFunctionProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 7 iFunction */ 0,
    /* --- Interface Descriptor #0: Control (9+64=73) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 0, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioControl) */ 0x01,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* --- Audio 2.0 AC Interface Header Descriptor (9+8+17+18+12=64, 0x40) */
    /* 0 bLength */ 9,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bcdADC */ 0x00, 0x02,
    /* 5 bCategory : 0x08 (IO Box) */ 0x08,
    /* 6 wTotalLength */ 64, 0,
    /* 8 bmControls */ 0x00,
    /* -------- Audio 2.0 AC Clock Source Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x0A,
    /* 3 bClockID */ 0x10,
    /* 4 bmAttributes : 0x05 (Sync|InternalFixedClk) */ 0x05,
    /* 5 bmControls : 0x01 (FreqReadOnly) */ 0x01,
    /* 6 bAssocTerminal, iClockSource */ 0x00, 0,
    /* ------ Audio 2.0 AC Input Terminal Descriptor */
    /* 0 bLength */ 17,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02, /* 3 bTerminalID */ 0x04,
    /* 4 wTerminalType : 0x0101 (USB Streaming) */ 0x01, 0x01,
    /* 6 bAssocTerminal, bCSourceID */ 0x00, 0x10,
    /* 8 bNrChannels */ 2,
    /* 9 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 13 iChannelNames, bmControls, iTerminal */ 0, 0x00, 0x00, 0,
    /* -------- Audio 2.0 AC Feature Unit Descriptor */
    /* 0 bLength */ 18,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x06,
    /* 3 bUnitID, bSourceID */ 0x05, 0x04,
    /* 5 bmaControls(0) : 0x0F (VolumeRW|MuteRW) */ 0x0F, 0x00, 0x00, 0x00,
    /* 9 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* 13 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* . iFeature */ 0,
    /* ----- Audio 2.0 AC Output Terminal Descriptor */
    /* 0 bLength */ 12,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x03, /* 3 bTerminalID */ 0x06,
    /* 4 wTerminalType : 0x0301 (Speaker) */ 0x01, 0x03,
    /* 6 bAssocTerminal, bSourceID, bCSourceID */ 0x00, 0x05, 0x10,
    /* 9 bmControls, iTerminal */ 0x00, 0x00, 0,
    /* --- Interface Descriptor #1: Stream OUT (9+9+16+6+7+8=55) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------------------- Interface Descriptor */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 1,
    /* 4 bNumEndpoints */ 1,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------- Audio 2.0 AS Interface Descriptor */
    /* 0 bLength */ 16,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bTerminalLink, bmControls */ 0x04, 0x00,
    /* 5 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 6 bmFormats : 0x000000001 (PCM) */ 0x01, 0x00, 0x00, 0x00, /* 10 bNrChannels */ 2,
    /* 11 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 15 iChannelNames */ 0, /* --------- Audio 2.0 AS Format Type Descriptor */
    /* 0 bLength */ 6,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02,
    /* 3 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 4 bSubslotSize, bBitResolution */ 2, 16,
    /* ------------------------- Endpoint Descriptor */
    /* 0 bLength, bDescriptorType */ 7, 0x05,
    /* 2 bEndpointAddress */ 0x02,
    /* 3 bmAttributes : 0x0D (Sync|ISO) */ 0x0D,
    /* 4 wMaxPacketSize : 0x0100 (256) */ 0x00, 0x01,
    /* 6 bInterval : 0x04 (1ms) */ 4,
    /* - Audio 2.0 AS ISO Audio Data Endpoint Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x25, 0x01,
    /* 3 bmAttributes, bmControls */ 0x00, 0x00,
    /* 5 bLockDelayUnits, wLockDelay */ 0x00, 0x00, 0x00,
};
```

Ses sınıfı, arabirimleri gruplamak için bir bileşik cihaz çerçevesi kullanır (denetim ve akış). Bir sonuç olarak, cihaz tanımlayıcısı tanımlanırken alınması gerekir. USBX, dahili olarak arabirimlerin nasıl bağlanacağını öğrenmek için ıAD tanımlayıcısını kullanır. IAD tanımlayıcısının, arabirimlerden önce (bir veya daha fazla AudioStreaming Interface tarafından izlenen bir veya daha fazla Audiostream arabirimi) önce bildirilmelidir ve ses sınıfının ilk arabirimini (AudioControl arabirimi) ve kaç arabirimin iliştirildiğine sahip olmalısınız.

Ses sınıfının çalışma şekli, cihazın ses gönderip almayacağı, ancak her iki durumda da ses çerçevesi arabelleklerinin depolanması için bir FıFO kullanmasına bağlıdır: cihaz konağa ses gönderiyorsa, uygulama daha sonra USBX tarafından konağa gönderilen, daha sonra FıFO 'ya ses çerçevesi arabellekleri ekler. cihaz konaktan ses alıyorsa, USBX konaktan alınan ses çerçevesi arabelleklerini daha sonra uygulama tarafından okunan FıFO 'ya ekler. Her ses akışının kendi FıFO 'u vardır ve her ses çerçevesi arabelleği birden çok örnek içerir.

Ses sınıfının başlatılması aşağıdaki parçaları bekler.

1. Ses sınıfı aşağıdaki akış parametrelerini bekliyor:

   ```C
   /* Set the parameters for Audio streams. */
   /* Set the application-defined callback that is invoked when the
      host requests a change to the alternate setting. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_change = demo_audio_read_change;

   /* Set the application-defined callback that is invoked whenever
      a USB packet (audio frame) is sent to or received from the host. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_frame_done = demo_audio_read_done;

   /* Set the number of audio frame buffers in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_nb = UX_DEMO_FRAME_BUFFER_NB;

   /* Set the maximum size of each audio frame buffer in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_size = UX_DEMO_MAX_FRAME_SIZE;

   /* Set the internally-defined audio processing thread entry pointer. If the application wishes to receive audio from the host
      (which is the case in this example), ux_device_class_audio_read_thread_entry should be used;
      if the application wishes to send data to the host, ux_device_class_audio_write_thread_entry should be used. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry = ux_device_class_audio_read_thread_entry;
   ```

2. Ses sınıfı aşağıdaki işlev parametrelerini bekliyor.

   ```C
   /* Set the parameters for Audio device. */

   /* Set the number of streams. */
   audio_parameter.ux_device_class_audio_parameter_streams_nb = 1;

   /* Set the pointer to the first audio stream parameter.
      Note that we initialized this parameter in the previous section.
      Also note that for more than one streams, this should be an array. */
   audio_parameter.ux_device_class_audio_parameter_streams = audio_stream_parameter;

   /* Set the application-defined callback that is invoked when the audio class
      is activated i.e. device is connected to host. */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_activate = demo_audio_instance_activate;

   /* Set the application-defined callback that is invoked when the audio class
      is deactivated i.e. device is disconnected from host. */

   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_deactivate = demo_audio_instance_deactivate;

   /* Set the application-defined callback that is invoked when the stack receives a control request from the host.
      See below for more details.
   */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_device_class_audio_control_process = demo_audio20_request_process;

   /* Initialize the device Audio class. This class owns interfaces starting with 0. */
   status = ux_device_stack_class_register(_ux_system_slave_class_audio_name,
       ux_device_class_audio_entry, 1, 0, &audio_parameter);
   if(status!=UX_SUCCESS)
       return;
   ```

   Yığın konaktan bir denetim isteği aldığında uygulama tanımlı denetim isteği geri araması (***ux_device_class_audio_control_process***; önceki örnekte ayarlanan) çağrılır. İstek kabul edildiğinde ve işlenirse (onaylanan veya durdurulmuş) geri çağırma başarılı döndürmelidir, aksi takdirde hata döndürülmelidir.

   Sınıfa özgü denetim isteği işlemi, bir uygulama tanımlı geri arama olarak tanımlanır çünkü denetim istekleri USB ses sürümleri arasında çok farklıdır ve istek işleminin büyük bir bölümü cihaz çerçevesiyle ilgilidir. Uygulamanın, cihazı çalışır hale getirmek için istekleri doğru işlemesi gerekir.

   Ses cihazı, ses, sessiz ve örnekleme sıklığı yaygın denetim istekleridir, ancak farklı USB ses sürümleri için basit ve dahili olarak tanımlanmış geri çağrılar, uygulamaların kullanması için sonraki bölümlerde sunulmuştur. Daha fazla ayrıntı için ***ux_device_class_audio10_control_process** _ ve _ *_ux_device_class_audio_control_request_** bölümüne bakın.

Ses cihazının cihaz çerçevesinde, PID/VIP cihaz tanımlayıcısına depolanır (yukarıda belirtilen cihaz tanımlayıcısına bakın).

Bir USB ana bilgisayar sistemi, USB ses cihazını bulur ve ses sınıfını takar, cihaz herhangi bir ses yürütücüsü veya Kaydedicisi (çerçeveye bağlı olarak) ile kullanılabilir. Başvuru için konak Işletim sistemine bakın.

Ses sınıfı API 'Leri aşağıda tanımlanmıştır.

## <a name="ux_device_class_audio_read_thread_entry"></a>ux_device_class_audio_read_thread_entry

Ses işlevine yönelik verileri okumak için iş parçacığı girişi.

### <a name="prototype"></a>Prototype

```C
VOID ux_device_class_audio_read_thread_entry(ULONG audio_stream);
```

### <a name="description"></a>Description

Bu işlev, konaktan ses okuma isteniyorsa ses akışı başlatma parametresine geçirilir. Dahili olarak, bu işlevle giriş işlevi olarak bir iş parçacığı oluşturulur; iş parçacığı, ses işlevindeki zaman aralıklı çıkış uç noktası aracılığıyla ses verilerini okur.

### <a name="parameters"></a>Parametreler

- **audio_stream**: ses akışı örneğine yönelik işaretçi.

### <a name="example"></a>Örnek

```C
/* Set parameter to initialize a stream for reading. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry
     = ux_device_class_audio_read_thread_entry;
```

## <a name="ux_device_class_audio_write_thread_entry"></a>ux_device_class_audio_write_thread_entry

Ses işlevine veri yazmak için iş parçacığı girişi

### <a name="prototype"></a>Prototype

```C
VOID ux_device_class_audio_write_thread_entry(ULONG audio_stream);
```

### <a name="description"></a>Description

Bu işlev, konağa ses yazılması isteniyorsa ses akışı başlatma parametresine geçirilir. Dahili olarak, bu işlevle giriş işlevi olarak bir iş parçacığı oluşturulur; iş parçacığı, ses işlevindeki zaman aralıklı olarak ses verileri yazar.

### <a name="parameters"></a>Parametreler

- **audio_stream**: ses akışı örneğine yönelik işaretçi.

### <a name="example"></a>Örnek

```C
/* Set parameter to initialize as stream for writing. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_en
    try = ux_device_class_audio_write_thread_entry;
```

## <a name="ux_device_class_audio_stream_get"></a>ux_device_class_audio_stream_get

Ses işlevi için belirli bir akış örneği al

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_stream_get(
    UX_DEVICE_CLASS_AUDIO *audio,
    ULONG stream_index, 
    UX_DEVICE_CLASS_AUDIO_STREAM **stream);
```

### <a name="description"></a>Description

Bu işlev, ses sınıfının akış örneğini almak için kullanılır.

### <a name="parameters"></a>Parametreler

- **Ses**: ses örneğine yönelik işaretçi
- **stream_index**: akış örneği dizini 0 ' a göre
- **Stream**: ses akışı örneği işaretçisini depolamak için arabelleğin işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Get audio stream instance. */
status = ux_device_class_audio_stream_get(audio, 0, &stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_reception_start"></a>ux_device_class_audio_reception_start

Ses akışı için ses verilerini almayı Başlat

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_reception_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Description

Bu işlev, ses akışında okuma ses verilerini başlatmak için kullanılır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği dolu.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Start stream data reception. */
status = ux_device_class_audio_reception_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read8"></a>ux_device_class_audio_sample_read8

Ses akışından 8 bit örneği oku

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_sample_read8(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    UCHAR *buffer);
```

### <a name="description"></a>Description

Bu işlev, belirtilen akıştan 8 bit ses örnek verilerini okur.

Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur. Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **buffer**: örnek baytı kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Read a byte in audio FIFO. */

status = ux_device_class_audio_sample_read8(stream, &sample_byte);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read16"></a>ux_device_class_audio_sample_read16

Ses akışından 16 bit örneği oku

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_sample_read16(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    USHORT *buffer);
```

### <a name="description"></a>Description

Bu işlev, belirtilen akıştan 16 bit ses örnek verilerini okur.

Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur. Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **buffer**: 16 bit örneği kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabelleği null.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Read a 16-bit sample in audio FIFO. */

status = ux_device_class_audio_sample_read16(stream, &sample_word);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read24"></a>ux_device_class_audio_sample_read24

Ses akışından 24 bit örneği okuma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_sample_read24(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a>Description

Bu işlev, belirtilen akıştan 24 bit ses örnek verilerini okur.

Özellikle FIFO'daki geçerli ses çerçevesi arabelleğinden örnek verileri okur. Ses çerçevesindeki son örneği okuduktan sonra, konaktan daha fazla veri kabul etmek için kullanılamayacak şekilde çerçeve otomatik olarak serbest bırakılır.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.
- **buffer:** 3 bayt örneğini kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabelleği null.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Read 3 bytes to in audio FIFO. */

status = ux_device_class_audio_sample_read24(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read32"></a>ux_device_class_audio_sample_read32

Ses akışından 32 bit örneği okuma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_sample_read32(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a>Description

Bu işlev, belirtilen akıştan 32 bit ses örnek verilerini okur.

Özellikle FIFO'daki geçerli ses çerçevesi arabelleğinden örnek verileri okur. Ses çerçevesindeki son örneği okuduktan sonra, konaktan daha fazla veri kabul etmek için kullanılamayacak şekilde çerçeve otomatik olarak serbest bırakılır.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.
- **buffer:** 4 byte verilerini kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabelleği null.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Read 4 bytes in audio FIFO. */

status = ux_device_class_audio_sample_read32(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_get"></a>ux_device_class_audio_read_frame_get

Ses akışında ses çerçevesine erişim elde etmek

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_read_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a>Description

Bu işlev, belirtilen akışın FIFO's unda ilk ses çerçevesi arabelleğini ve uzunluğunu döndürür. Uygulama, verileri işlemeyi tamamlasa ux_device_class_audio_read_frame_free FIFO'da çerçeve arabelleğinin serbest bırakılamayabilirsiniz.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.
- **frame_data:** Veri işaretçisini iade etmek için veri işaretçisinin işaretçisi.
- **frame_length:** Çerçeve uzunluğunu bayt sayısı olarak kaydetmek için arabelleğe işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabelleği null.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Get frame access. */

status = ux_device_class_audio_read_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_free"></a>ux_device_class_audio_read_frame_free

Ses akışında ses çerçevesi arabelleği serbest bırak

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_read_frame_free(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Description

Bu işlev, belirtilen akışın FIFO's un önündeki ses çerçevesi arabelleğini serbest bırakarak konaktan veri aldırıyor.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabelleği null.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Refree a frame buffer in FIFO. */

status = ux_device_class_audio_read_frame_free(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_transmission_start"></a>ux_device_class_audio_transmission_start

Ses akışı için ses veri iletimini başlatma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_transmission_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Description

Bu işlev, ses sınıfında FIFO'ya yazılan ses verilerini göndermeye başlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabelleği null.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Start stream data transmission. */

status = ux_device_class_audio_transmission_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_frame_write"></a>ux_device_class_audio_frame_write

Ses akışına ses çerçevesi yazma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_frame_write(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR *frame,
    ULONG frame_length);
```

### <a name="description"></a>Description

Bu işlev, ses akışının FIFO's una bir çerçeve yazar. Çerçeve verileri FIFO'daki kullanılabilir arabelleğe kopyalanır, böylece konakta gönderebilirsiniz.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.
- **frame:** Çerçeve verilerine işaretçi.
- **frame_length** Bayt sayısı cinsinden çerçeve uzunluğu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabellek dolu.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Get frame access. */

status = ux_device_class_audio_frame_write(stream, frame, frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_write_frame_get"></a>ux_device_class_audio_write_frame_get

Ses akışında ses çerçevesine erişim elde etmek

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_write_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a>Description

Bu işlev FIFO'nun son ses çerçevesi arabelleğinin adresini; ayrıca ses çerçevesi arabelleğinin uzunluğunu da alar. Uygulama, ses çerçevesi arabelleğini istenen  verilerle ux_device_class_audio_write_frame_commit çerçeve arabelleği fiFO'ya eklemek/işlemek için kullanılmalıdır.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.
- **frame_data:** Çerçeve veri işaretçisini iade etmek için çerçeve veri işaretçisi.
- **frame_length** Bayt sayısı cinsinden çerçeve uzunluğunu kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabellek dolu.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Get frame access. */

status = ux_device_class_audio_write_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
     return;
```

## <a name="ux_device_class_audio_write_frame_commit"></a>ux_device_class_audio_write_frame_commit

Ses akışında bir ses çerçevesi arabelleği işle.

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_write_frame_commit(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG length);
```

### <a name="description"></a>Description

Bu işlev son ses çerçevesi arabelleğini FIFO'ya ekler/işler, böylece arabellek ana bilgisayar için aktar olmaya hazır olur; Son ses çerçevesi arabelleğinin, ses çerçevesi arabelleğinin ux_device_class_write_frame_get.

### <a name="parameters"></a>Parametreler

- **stream:** Ses akışı örneğinin işaretçisi.
- **length:** Arabellekte hazır olan bayt sayısı.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Arabirim yok.
- **UX_BUFFER_OVERFLOW** (0x5d) FIFO arabelleği fssull olur.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Commit a frame after fill values in buffer. */

status = ux_device_class_audio_write_frame_commit(stream, 192);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio10_control_process"></a>ux_device_class_audio10_control_process

USB Ses 1.0 denetim isteklerini işleme

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio10_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO10_CONTROL_GROUP *group);
```

### <a name="description"></a>Description

Bu işlev, usb ses 1.0'a özgü bir tür ile denetim uç noktası üzerinde konak tarafından gönderilen temel istekleri yönetir.

Ses ve sessiz isteklerin ses 1.0 özellikleri işlevinde işlenir. İstekleri işlerken, istekleri yanıtlamak ve denetim değişikliklerini depolamak için son parametre (grup) tarafından geçirilen önceden tanımlanmış veriler kullanılır.

### <a name="parameters"></a>Parametreler

- **audio:** Ses örneğinin işaretçisi.
- **transfer:** Aktarım isteği örneğinin işaretçisi.
- **group:** İstek işlemi için veri grubu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Initialize audio 1.0 control values. */

audio_control[0].ux_device_class_audio10_control_fu_id = 2;
audio_control[0].ux_device_class_audio10_control_mute[0] = 0;
audio_control[0].ux_device_class_audio10_control_volume[0] = 0;
audio_control[1].ux_device_class_audio10_control_fu_id = 5;
audio_control[1].ux_device_class_audio10_control_mute[0] = 0;
audio_control[1].ux_device_class_audio10_control_volume[0] = 0;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio10_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio10_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```

## <a name="ux_device_class_audio20_control_process"></a>ux_device_class_audio20_control_process

USB Ses 1.0 denetim isteklerini işleme

### <a name="prototype"></a>Prototype
```C
UINT ux_device_class_audio20_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO20_CONTROL_GROUP *group);
```

### <a name="description"></a>Description

Bu işlev, usb ses 2.0'a özgü bir türle denetim uç noktası üzerinde konak tarafından gönderilen temel istekleri yönetir.

Ses 2.0 örnekleme hızı (tek bir sabit sıklık varsayılır), ses ve sessiz istek özellikleri işlevde işlenir. İstekleri işlerken, istekleri yanıtlamak ve denetim değişikliklerini depolamak için son parametre (grup) tarafından geçirilen önceden tanımlanmış veriler kullanılır.

### <a name="parameters"></a>Parametreler

- **audio:** Ses örneğinin işaretçisi.
- **transfer:** Aktarım isteği örneğinin işaretçisi.
- **group:** İstek işlemi için veri grubu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```C
/* Initialize audio 2.0 control values. */

audio_control[0].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[0].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[0].ux_device_class_audio20_control_fu_id = 2;
audio_control[0].ux_device_class_audio20_control_mute[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[0].ux_device_class_audio20_control_volume[0] = 50;
audio_control[1].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[1].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[1].ux_device_class_audio20_control_fu_id = 5;
audio_control[1].ux_device_class_audio20_control_mute[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[1].ux_device_class_audio20_control_volume[0] = 50;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio20_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio20_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```
