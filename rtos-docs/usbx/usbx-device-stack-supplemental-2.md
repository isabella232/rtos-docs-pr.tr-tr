---
title: Bölüm 2-USBX cihaz sınıfı konuları
description: USB cihaz RNDIS sınıfı, USB konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak tanır. Bu sınıf, Microsoft özel uygulamasına dayalıdır ve Windows platformları için özeldir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8104f00e192486f57fe9c22b2c83aa9a22954739
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828414"
---
# <a name="chapter-2---usbx-device-class-considerations"></a>Bölüm 2-USBX cihaz sınıfı konuları

## <a name="usb-device-rndis-class"></a>USB cihazı RNDIS sınıfı

USB cihaz RNDIS sınıfı, USB konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak tanır. Bu sınıf, Microsoft özel uygulamasına dayalıdır ve Windows platformları için özeldir.

RNDIS uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildirilmesine ihtiyacı vardır. Aşağıda bir örnek bulunur.

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

RNDIS sınıfı, CDC-ACM ve CDC-ECD için çok benzer bir cihaz tanımlayıcısı yaklaşımı kullanır ve ayrıca bir ıAD tanımlayıcısı gerektirir. Cihaz tanımlayıcısının tanımı ve gereksinimleri için CDC-ACM sınıfına bakın.

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

CDC-ECD için, RNDIS sınıfı 2 düğüm, bir yerel ve bir uzak, ancak uzak düğümü tanımlayan bir dize tanımlayıcısına sahip olmak için gerekli değildir.

Ancak, Microsoft özel mesajlaşma mekanizmasından dolayı bazı ek parametreler gereklidir. Önce satıcı KIMLIĞININ geçirilmesi gerekir. Benzer şekilde, RNDIS 'in sürücü sürümü. Bir satıcı dizesi de verilmelidir.

RNDIS sınıfında, her iki şekilde de verileri aktarmaya yönelik yerleşik API 'Ler vardır ancak kullanıcı uygulaması, USB Ethernet cihazından NetX üzerinden iletişim kurduğu için bu uygulamalar uygulamaya gizlenir.

USBX RNDIS sınıfı, Azure RTOS NetX ağ yığınına yakın bir şekilde bağlanır. NetX ve USBX RNDIS sınıfını kullanan bir uygulama, NetX ağ yığınını olağan şekilde etkinleştirir ancak ek olarak, USB ağ yığınını aşağıdaki şekilde etkinleştirmek gerekir.

```C
/* Initialize the NetX system. */

nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

USB ağ yığınının yalnızca bir kez etkinleştirilmesi ve RNDIS 'e özgü olmaması, ancak NetX hizmetleri gerektiren herhangi bir USB sınıfı için gerekli olması gerekir.

RNDIS sınıfı, Microsoft işletim sistemlerine özgü olan MAC OS ve Linux konakları tarafından tanınmaz. Windows platformlarında, cihaz tanımlayıcısıyla eşleşen konakta bir. inf dosyası bulunması gerekir. Microsoft, RNDIS sınıfı için bir şablon sağlar ve usbx_windows_host_files dizininde bulunabilir. Windows 'un daha yeni sürümü için RNDIS_Template. inf dosyası kullanılmalıdır. Bu dosyanın, cihaz tarafından kullanılan PID/VıD 'yi yansıtacak şekilde değiştirilmesi gerekir. Şirket ve ürün USB-IF ile kaydettirilirse, PID/VıD son müşteriye özgü olacaktır. INF dosyasında, değiştirilecek alanlar burada bulunur.

```Inf
[DeviceList]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00

[DeviceList.NTamd64]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00
```

RNDIS cihazının cihaz çerçevesinde, PID/VıD cihaz tanımlayıcısına depolanır (yukarıda belirtilen cihaz tanımlayıcısına bakın)

USB ana bilgisayar sistemleri, USB RNDIS cihazını bulduğunda, bir ağ arabirimi bağlayacaktır ve cihaz ağ protokol yığını ile birlikte kullanılabilir. Başvuru için konak Işletim sistemine bakın.

## <a name="usb-device-dfu-class"></a>USB cihaz DFU sınıfı

USB cihaz DFU sınıfı, bir USB konak sisteminin bir konak uygulamasına bağlı olarak cihaz bellenimini güncelleştirmesine izin verir. DFU sınıfı, bir USB-IF standart sınıfıdır.

USBX DFU sınıfı nispeten basittir. BT cihaz tanımlayıcısı, bir denetim uç noktası olmak üzere hiçbir şey gerektirmez. Çoğu zaman, bu sınıf bir USB Bileşik cihazına gömülecektir. Cihaz, bir depolama cihazı veya bir iletişim cihazı gibi herhangi bir şey olabilir ve eklenen DFU arabirimi, ana bilgisayara cihazın belleniminin güncelleştirilmesini sağlayabilir.

DFU sınıfı 3 adımda çalışmaktadır. İlk olarak, aygıt, dışarıya aktarılmış sınıfı kullanarak normal şekilde takar. Konaktaki (Windows veya Linux) bir uygulama DFU sınıfını oluşturacak ve cihazı DFU moduna sıfırlamaya yönelik bir istek gönderecek. Cihaz, veri yolundan kısa bir süre (konak ve cihaz için bir SıFıRLAMA sırasını algılamaya yetecek kadar) kaybolur ve yeniden başlatıldığında cihaz, ana bilgisayar uygulamasının bir bellenim yükseltmesi göndermesini beklemek için özel olarak DFU modunda olur. Üretici yazılımı yükseltmesi tamamlandığında, ana bilgisayar uygulaması cihazı sıfırlar ve yeniden numaralandırdıktan sonra cihaz yeni üretici yazılımıyla normal işlemine döndürülür.

DFU cihaz çerçevesi şuna benzeyecektir.

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

Bu örnekte, DFU tanımlayıcısı diğer sınıflarla ilişkili değildir. Basit bir arabirim tanımlayıcısına sahiptir ve kendisine bağlı başka uç noktalar yoktur. Cihazın DFU özelliklerinin ayrıntılarını açıklayan bir Işlevsel tanımlayıcı vardır.

DFU yeteneklerinin açıklaması aşağıdaki gibidir.

| Name             | Uzaklık  | Boyut | tür      | Açıklama |
|------------------|----------|------|-----------|------------|
| bmAttributes  | 2     | 1   | Bit alanı | Bit 3: cihaz, bir DFU_DETACH isteği aldığında bir veri yolu ayırma-iliştirme sırası gerçekleştirir. Konağın USB sıfırlaması yayınlamamalıdır. (bitWillDetach) 0 = Hayır 1 = Evet bit 2: cihaz, bildirim aşamasından sonra USB üzerinden iletişim kurabilir. (Bitbildirimli Estationdayanıklı) 0 = Hayır, veri yolu sıfırlaması 1 = Evet bit 1: karşıya yükleme özellikli (bitCanUpload) 0 = Hayır 1 = Evet bit 0: indirme özelliği (bitCanDnload) 0 = Hayır 1 = Evet  |
| Wçıkarılabilir zaman aşımı  | 3      | 2  | sayı    | Milisaniye cinsinden, cihazın DFU_DETACH isteği alındıktan sonra bekleyeceği süre. Bu süre USB sıfırlaması olmadan geçtiğinde cihaz, yeniden yapılandırma aşamasını sonlandırır ve normal işleme geri döndürülür. Bu, cihazın bekleneceği maksimum süreyi (zamanlayıcılar, vb.) temsil eder. USBX bu değeri 1000 ms olarak ayarlar.  |
| wTransferSize  | 5      | 2  | sayı    | Cihazın her denetim yazma işlemi için kabul edebileceği en fazla bayt sayısı \- . USBX bu değeri 64 bayt olarak ayarlar. |

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

DFU sınıfının hedefe özgü bir cihaz üretici yazılımı uygulamasıyla çalışması gerekir. Bu nedenle, üretici yazılımının okuma ve yazma blokları ve bellenim güncelleştirme uygulamasından durum almak için birkaç geri çağrı tanımlar. DFU sınıfında Ayrıca, bellenimin bir başlangıç ve bitiş sonu gerçekleştiğinde uygulamayı bilgilendirmek için bir bildirim geri araması işlevi bulunur.

Tipik bir DFU uygulama akışının açıklaması aşağıda verilmiştir.

![DFU uygulama akışı](./media/usbx-device-stack-supplemental/dfu-application-flow.png)

DFU sınıfının önemli zorluğu, bellenime indirme işlemini gerçekleştirmek için konakta doğru uygulamayı almaktır. Microsoft veya USB-IF tarafından sağlanan bir uygulama yok. Bazı paylaşılan yazılım var ve Linux 'ta ve Windows 'da daha düşük bir ölçüde iyi çalışır.

Linux 'ta, bir tane DFU-utils kullanarak burada bulunabilir: [https://wiki.openmoko.org/wiki/Dfu-util](https://wiki.openmoko.org/wiki/Dfu-util) Bu bağlantıda DFU yardımcı programları hakkında çok fazla bilgi bulunabilir: [https://www.libusb.org/wiki/windows_backend](https://www.libusb.org/wiki/windows_backend)

DFU 'nin Linux uygulamasına, ana bilgisayar ile cihaz arasındaki sıfırlama sırası doğru şekilde gerçekleştirilir ve bu nedenle cihazın bunu yapmasına gerek yoktur. Linux, bmAttributes *Bitwilldetach* 0 olması için kabul edebilir. Diğer taraftan Windows, cihazın sıfırlamayı gerçekleştirmesini gerektirir.

Windows 'da, USB kayıt defteri, USB cihazını PID/VıD ve USB kitaplığı ile ilişkilendirebilmelidir ve bu da DFU uygulaması tarafından kullanılacaktır. Bu, burada bulunabilerek ücretsiz yardımcı program ile kolayca yapılabilir: [https://sourceforge.net/projects/libwdi/files/zadig/](https://sourceforge.net/projects/libwdi/files/zadig/) .

Zadig 'yi ilk kez çalıştırmak bu ekranı gösterecektir:

![Zadig 'yi ilk kez çalıştırma](./media/usbx-device-stack-supplemental/zadig.png)

Cihaz listesinden cihazınızı bulun ve lıbusb Windows sürücüsüyle ilişkilendirin. Bu işlem, cihazın PID/VıD 'sini DFU yardımcı programları tarafından kullanılan Windows USB kitaplığıyla bağlar.

DFU komutunu çalıştırmak için, yalnızca daraltılmış DFU yardımcı programlarının bir dizine paketini açmanız yeterlidir ve bu DLL 'nin aynı dizinde de bulunduğundan emin olun. DFU yardımcı programlarının komut satırındaki bir DOS kutusundan çalıştırılması gerekir.

İlk olarak, cihazın listelenip listelenmediğini öğrenmek için **DFU-Util – l** komutunu yazın. Aksi takdirde, cihazın listelenmiş ve USB kitaplığıyla ilişkili olduğundan emin olmak için Zadig 'yi çalıştırın. Aşağıdaki gibi bir ekran görmeniz gerekir:

```Command-line
C:\usb specs\DFU\dfu-util-0.6&gt;dfu-util -l dfu-util 0.6

Copyright 2005-2008 Weston Schmidt, Harald Welte and OpenMoko Inc.
Copyright 2010-2012 Tormod Volden and Stefan Schmidt
This program is Free Software and has ABSOLUTELY NO WARRANTY
Found Runtime: [0a5c:21bc] devnum=0, cfg=1, intf=3, alt=0, name="UNDEFINED"
```

Sonraki adım, dosyayı indirilecek şekilde hazırlanacaktır. USBX DFU sınıfı, bu dosya üzerinde herhangi bir doğrulama gerçekleştirmez ve iç biçiminin bağımsız olduğunu göstermez. Bu üretici yazılımı dosyası hedefe özgü değildir ancak DFU 'ye veya USBX 'e uygulanmaz.

Ardından, aşağıdaki komutu yazarak DFU-Util 'e dosyayı göndermek için talimat uygulanabilir:

```Command-line
dfu-util –R –t 64 -D file_to_download.hex
```

Yazılım yazılımı tamamen indirilene kadar DFU-Util dosya indirme işlemini görüntülemelidir.

## <a name="usb-device-pima-class-ptp-responder"></a>USB cihaz PIMA sınıfı (PTP Yanıtlayıcısı)

USB cihaz PIMA sınıfı, bir USB ana bilgisayar sisteminin (Başlatıcı) bir cihaza bağlanmasını sağlar

Medya dosyalarını aktarmak için PIMA cihazı (Resonder). USBX Pima sınıfı, PTP class (resim aktarma protokolü için) olarak da bilinen USB-IF PIMA 15740 sınıfına yöneliktir.

USBX Device Side PIMA sınıfı aşağıdaki işlemleri destekler.

| İşlem kodu                                    | Değer | Açıklama                       |
|---------------------------------------------------|---------|-----------------------------------------------------|
| UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO    | 0x1001  | Desteklenen cihaz işlemlerini ve olayları edinin                                                         |
| UX_DEVICE_CLASS_PIMA_OC_OPEN_SESSION        | 0x1002  | Konak ve cihaz arasında bir oturum açın                                                            |
| UX_DEVICE_CLASS_PIMA_OC_CLOSE_SESSION       | 0x1003  | Konak ve cihaz arasında bir oturumu kapatma                                                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_IDS    | 0x1004  | Cihazın depolama KIMLIĞINI döndürür. USBX PIMA yalnızca bir depolama KIMLIĞI kullanır |
| UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_INFO   | 0x1005  | Depolama nesnesi hakkında en fazla kapasite ve boş alan gibi bilgileri döndür                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_NUM_OBJECTS    | 0x1006  | Depolama cihazında bulunan nesne sayısını döndür                                              |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_HANDLES | 0x1007  | Depolama cihazında nesnelerin bir tanıtıcı dizisini döndürür                                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_INFO    | 0x1008  | Nesnenin adı, Oluşturulma tarihi, değiştirilme tarihi gibi bir nesneyle ilgili bilgileri döndürür |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT          | 0x1009  | Belirli bir nesneyle ilgili verileri döndürür                                                         |
| UX_DEVICE_CLASS_PIMA_OC_GET_THUMB           | 0x100A  | Bir nesne hakkında kullanılabiliyorsa küçük resmi gönder                                                           |
| UX_DEVICE_CLASS_PIMA_OC_DELETE_OBJECT       | 0x100B  | Medyadaki bir nesneyi silme                                                                             |
| UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT_INFO   | 0x100C  | Medyada oluşturulması için bir nesneyle ilgili cihaz bilgilerine gönderin                              |
| UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT         | 0x100D  | Bir nesne için verileri cihaza gönderme                                                                     |
| UX_DEVICE_CLASS_PIMA_OC_FORMAT_STORE        | 0x100F  | Cihaz medyasını Temizleme                                                                                    |
| UX_DEVICE_CLASS_PIMA_OC_RESET_DEVICE        | 0x0110  | Hedef cihazı sıfırlayın                                                                                   |

| İşlem kodu                                         | Değer | Açıklama |
|--------------------------------------------------------|-------|-----------------------------------------|
| UX_DEVICE_CLASS_PIMA_EC_CANCEL_TRANSACTION       | 0x4001  | Geçerli işlemi iptal eder                                                 |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_ADDED             | 0x4002  | Cihaz medyasına bir nesne eklenmiştir ve bu, host\tarafından alınabilir. |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_REMOVED           | 0x4003  | Cihaz medyasından bir nesne silindi                                |
| UX_DEVICE_CLASS_PIMA_EC_STORE_ADDED              | 0x4004  | Cihaza medya eklendi                                            |
| UX_DEVICE_CLASS_PIMA_EC_STORE_REMOVED            | 0x4005  | Cihazdan bir medya silindi                                        |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_PROP_CHANGED     | 0x4006  | Cihaz özellikleri değiştirildi                                                  |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_INFO_CHANGED     | 0x4007  | Bir nesne bilgisi değişti                                               |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_INFO_CHANGE      | 0x4008  | Bir cihaz değiştirildi                                                            |
| UX_DEVICE_CLASS_PIMA_EC_REQUEST_OBJECT_TRANSFER | 0x4009  | Cihaz, konaktan bir nesne aktarımını ister                     |
| UX_DEVICE_CLASS_PIMA_EC_STORE_FULL               | 0x400A  | Ortam dolu cihaz raporları                                                |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_RESET             | 0x400B  | Sıfırlanan cihaz raporları                                                     |
| UX_DEVICE_CLASS_PIMA_EC_STORAGE_INFO_CHANGED    | 0x400C  | Cihazda depolama bilgileri değişti                                   |
| UX_DEVICE_CLASS_PIMA_EC_CAPTURE_COMPLETE         | 0x400D  | Yakalama tamamlandı                                                            |

USBX PIMA cihaz sınıfı, konaktan PIMA komutlarını dinlemek için bir TX Iş parçacığı kullanır.

Bir PIMA komutu bir komut bloğundan, bir veri bloğundan ve bir durum aşamasından oluşur.

İşlev ux_device_class_pima_thread, ana bilgisayar tarafında bir PIMA komutu almak için yığına bir istek gönderir. PIMA komutunun kodu çözüldü ve içerik için doğrulanır. Komut bloğu geçerliyse, uygun komut işleyicisine dallandırır.

Çoğu PIMA komutları yalnızca, ana bilgisayar tarafından bir oturum açıldığında yürütülebilir. Tek özel durum, komut **UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO**. USBX PIMA uygulamasıyla, her zaman bir başlatıcı ve Yanıtlayıcı arasında yalnızca bir oturum açılabilir. Tek oturumdaki tüm işlemler engelleniyor ve önceki işlem tamamlanmadan önce yeni bir işlem başlayabilirler.

PIMA işlemleri 3 aşamadan, bir komut aşamasına, isteğe bağlı bir veri aşamasına ve bir yanıt aşamasına göre oluşur. Bir veri aşaması varsa, yalnızca bir yönde olabilir.

Başlatıcı her zaman PIMA işlemlerinin akışını belirler ancak Yanıtlayıcı, bir oturum sırasında gerçekleşen durum değişikliklerini bilgilendirmek için olayları başlatıcıya geri başlatabilir.

Aşağıdaki diyagramda, ana bilgisayar ve PIMA cihaz sınıfı arasında bir veri nesnesinin aktarımı gösterilmektedir.

![PIMA işlemleri](./media/usbx-device-stack-supplemental/pima-transactions.png)

## <a name="initialization-of-the-pima-device-class"></a>PIMA cihaz sınıfının başlatılması

PIMA cihaz sınıfı, başlatma sırasında uygulama tarafından sağlanan bazı parametrelere ihtiyaç duyuyor.

Aşağıdaki parametreler cihaz ve depolama bilgilerini anlatmaktadır.

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

IZMA sınıfı ayrıca belirli olayları bilgilendirmek veya yerel medyadan veri almak/depolamak için uygulamaya geri çağırma kaydı yapılmasını gerektirir. Geri çağrılar aşağıdaki gibidir.

- `ux_device_class_pima_object_number_get`
- `ux_device_class_pima_object_handles_get`
- `ux_device_class_pima_object_info_get`
- `ux_device_class_pima_object_data_get`
- `ux_device_class_pima_object_info_send`
- `ux_device_class_pima_object_data_send`
- `ux_device_class_pima_object_delete`

Aşağıdaki örnekte, PIMA 'nın istemci tarafının nasıl başlatıldığı gösterilmektedir. Bu örnek, PIMA için istemci olarak PictBridge kullanır.

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

Bir nesne ekleme ve olayı konağa gönderme

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_add(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG object_handle);
```

### <a name="description"></a>Açıklama

Bu işlev, PIMA sınıfının bir nesne eklemesi ve Konağı bilgilendirilmesi gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi
- **object_handle**: nesnenin tanıtıcısı.

### <a name="example"></a>Örnek

```C
/* Send the notification to the host that an object has been added. */

status = ux_device_class_pima_object_add(pima, UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST);
```

## <a name="ux_device_class_pima_object_number_get"></a>ux_device_class_pima_object_number_get

Uygulamadan nesne numarası alma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_number_get(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG *object_number);
```

### <a name="description"></a>Açıklama

Bu işlev, PIMA sınıfının yerel sistemdeki nesne sayısını alması ve konağa geri göndermek için gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi
- **object_number**: döndürülecek nesne sayısının adresi

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

Nesne tutamacı dizisini döndürün

### <a name="prototype"></a>Prototype

```C
UINT **ux_device_class_pima_object_handles_get**(
    UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number);
```

### <a name="description"></a>Açıklama

Bu işlev, PIMA sınıfının, yerel sistemde nesne işleyicileri dizisini alması ve konağa geri gönderebilmesi gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **object_handles_format_code**: tutamaçlar için kodu Biçimlendir
- **object_handles_association**: nesne ilişkilendirme kodu
- **object_handle_array**: tanıtıcıların depolanacağı adres
- **object_handles_max_number**: dizideki en fazla tanıtıcı sayısı

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

Nesne bilgilerini döndürme

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_info_get(
    struct UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handle, 
    UX_SLAVE_CLASS_PIMA_OBJECT **object);
```

### <a name="description"></a>Açıklama

Bu işlev, PIMA sınıfının, yerel sistemde nesne işleyicileri dizisini alması ve konağa geri gönderebilmesi gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **object_handles**: nesnenin tanıtıcısı
- **nesne**: nesne işaretçisi adresi

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

Nesne verilerini döndürme

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

### <a name="description"></a>Açıklama

Bu işlev, PIMA sınıfının, yerel sistemdeki nesne verilerini alması ve konağa geri gönderilmesi gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **object_handle**: nesnenin tanıtıcısı
- **object_buffer**: nesne arabellek adresi
- **object_length_requested**: istemci tarafından uygulamaya istenen nesne veri uzunluğu
- **object_actual_length**: uygulama tarafından döndürülen nesne veri uzunluğu

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

Ana bilgisayar nesne bilgilerini gönderir

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_info_send(
    UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, 
    ULONG *object_handle);
```

### <a name="description"></a>Açıklama

Bu işlev, PIMA sınıfının daha sonra depolama için yerel sistemdeki nesne bilgilerini alması gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi
- **nesne**: nesnenin işaretçisi
- **object_handle**: nesnenin tanıtıcısı

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

### <a name="description"></a>Açıklama

Bu işlev, PIMA sınıfının depolama için yerel sistemdeki nesne verilerini alması gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi
- **object_handle**: nesnenin tanıtıcısı
- **aşama**: aktarımın aşaması (etkin veya tamamlanmış)
- **object_buffer**: nesne arabellek adresi
- **object_offset**: verilerin adresi
- **object_length**: uygulama tarafından gönderilen nesne veri uzunluğu

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

Yerel bir nesneyi silme

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_pima_object_delete(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle);
```

### <a name="description"></a>Açıklama

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
   status = ux_device_stack_class_register(_ux_system_slave_class_cdc_acm_name,
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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Bu işlev, belirtilen akıştan 16 bit ses örnek verilerini okur.

Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur. Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **buffer**: 16 bit örneği kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Read a 16-bit sample in audio FIFO. */

status = ux_device_class_audio_sample_read16(stream, &sample_word);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read24"></a>ux_device_class_audio_sample_read24

Ses akışından 24 bit örnek okuyun

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_sample_read24(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a>Açıklama

Bu işlev, belirtilen akıştan alınan 24 bit ses örnek verilerini okur.

Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur. Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **buffer**: 3 baytlık örneği kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Read 3 bytes to in audio FIFO. */

status = ux_device_class_audio_sample_read24(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read32"></a>ux_device_class_audio_sample_read32

Ses akışından 32 bitlik örnek okuyun

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_sample_read32(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a>Açıklama

Bu işlev, belirtilen akıştan 32 bitlik ses örnek verilerini okur.

Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur. Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **buffer**: 4 baytlık verileri kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Read 4 bytes in audio FIFO. */

status = ux_device_class_audio_sample_read32(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_get"></a>ux_device_class_audio_read_frame_get

Ses akışındaki ses çerçevesine erişim sağlayın

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_read_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a>Açıklama

Bu işlev, ilk ses çerçevesi arabelleğini ve belirtilen akışın FıFO uzunluğunu döndürür. Uygulama verileri işlemeyi tamamladıktan sonra FıFO 'daki çerçeve arabelleğini serbest bırakmak için ux_device_class_audio_read_frame_free kullanılmalıdır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **frame_data**: veri işaretçisini döndürmek için veri işaretçisine yönelik işaretçi.
- **frame_length**: çerçeve uzunluğunu bayt sayısıyla kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Get frame access. */

status = ux_device_class_audio_read_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_free"></a>ux_device_class_audio_read_frame_free

Ses akışında ses çerçevesi arabelleğini serbest bırakma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_read_frame_free(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Açıklama

Bu işlev, ana bilgisayardan veri alabilmesi için belirtilen akışın FıFO önünde ses çerçevesi arabelleğini serbest bırakır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Refree a frame buffer in FIFO. */

status = ux_device_class_audio_read_frame_free(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_transmission_start"></a>ux_device_class_audio_transmission_start

Ses akışı için ses veri aktarımını Başlat

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_transmission_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Açıklama

Bu işlev, ses sınıfında FıFO 'ya yazılmış ses verileri göndermeye başlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Start stream data transmission. */

status = ux_device_class_audio_transmission_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_frame_write"></a>ux_device_class_audio_frame_write

Ses akışına bir ses çerçevesi yazma

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_frame_write(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR *frame,
    ULONG frame_length);
```

### <a name="description"></a>Açıklama

Bu işlev, ses akışının FıFO ' a bir çerçeve yazar. Çerçeve verileri, konağa gönderilebilmesi için FıFO 'daki kullanılabilir arabelleğe kopyalanır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **çerçeve**: çerçeve verileri işaretçisi.
- **frame_length** Bayt sayısıyla çerçeve uzunluğu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği dolu.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Get frame access. */

status = ux_device_class_audio_frame_write(stream, frame, frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_write_frame_get"></a>ux_device_class_audio_write_frame_get

Ses akışındaki ses çerçevesine erişim sağlayın

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_write_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a>Açıklama

Bu işlev, FıFO 'nun son ses çerçevesi arabelleğinin adresini alır; Ayrıca, ses çerçevesi arabelleğinin uzunluğunu da alır. Uygulama, ses çerçevesi arabelleğini istenen verilerle doldurduktan sonra, ***ux_device_class_audio_write_frame_commit*** kare arabelleği eklemek/FIFO 'ya uygulamak için kullanılmalıdır.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **frame_data**: çerçeve verisi işaretçisini döndürmek için çerçeve verisi işaretçisine yönelik işaretçi.
- **frame_length** Çerçeve uzunluğunu bayt sayısıyla kaydetmek için arabelleğin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği dolu.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Get frame access. */

status = ux_device_class_audio_write_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
     return;
```

## <a name="ux_device_class_audio_write_frame_commit"></a>ux_device_class_audio_write_frame_commit

Ses akışına ses çerçevesi arabelleği yürütün.

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio_write_frame_commit(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG length);
```

### <a name="description"></a>Açıklama

Bu işlev, arabellek konağa aktarılmaya hazırlandığından, son ses çerçevesi arabelleğini FıFO 'ya ekler/kaydeder; son ses çerçevesi arabelleğinin ux_device_class_write_frame_get ile doldurulmuş olması gerektiğini göz önünde bulabilirsiniz.

### <a name="parameters"></a>Parametreler

- **Stream**: ses akışı örneğine yönelik işaretçi.
- **uzunluk**: arabellekte Ready bayt sayısı.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.
- **UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği fssull şeklindedir.
- İşlevden **UX_ERROR** (0xFF) hatası

### <a name="example"></a>Örnek

```C
/* Commit a frame after fill values in buffer. */

status = ux_device_class_audio_write_frame_commit(stream, 192);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio10_control_process"></a>ux_device_class_audio10_control_process

USB ses 1,0 denetim isteklerini işle

### <a name="prototype"></a>Prototype

```C
UINT ux_device_class_audio10_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO10_CONTROL_GROUP *group);
```

### <a name="description"></a>Açıklama

Bu işlev, denetim uç noktasındaki ana bilgisayar tarafından gönderilen temel istekleri, USB ses 1,0 'e özgü bir türle yönetir.

Birim ve sessiz isteklerin ses 1,0 özellikleri işlevinde işlenir. İstekleri işlerken, istekleri yanıtlamak ve denetim değişikliklerini depolamak için son parametre (Grup) tarafından geçirilen önceden tanımlanmış veriler kullanılır.

### <a name="parameters"></a>Parametreler

- **Ses**: ses örneğine yönelik işaretçi.
- **Transfer**: aktarım isteği örneğine yönelik işaretçi.
- **Grup**: istek işlemi için veri grubu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- İşlevden **UX_ERROR** (0xFF) hatası

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

USB ses 1,0 denetim isteklerini işle

### <a name="prototype"></a>Prototype
```C
UINT ux_device_class_audio20_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO20_CONTROL_GROUP *group);
```

### <a name="description"></a>Açıklama

Bu işlev, denetim uç noktasındaki ana bilgisayar tarafından gönderilen temel istekleri, USB ses 2,0 'e özgü bir türle yönetir.

Ses 2,0 örnekleme hızı (tek sabit sıklık varsayıldı), birim ve sessiz isteklerin özellikleri işlevinde işlenir. İstekleri işlerken, istekleri yanıtlamak ve denetim değişikliklerini depolamak için son parametre (Grup) tarafından geçirilen önceden tanımlanmış veriler kullanılır.

### <a name="parameters"></a>Parametreler

- **Ses**: ses örneğine yönelik işaretçi.
- **Transfer**: aktarım isteği örneğine yönelik işaretçi.
- **Grup**: istek işlemi için veri grubu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- İşlevden **UX_ERROR** (0xFF) hatası

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
