---
title: Bölüm 5 - USBX Cihaz Sınıfı Konuları
description: USBX Cihaz Sınıfı ile ilgili dikkat edilmesi gerekenler hakkında bilgi alın.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: ea348d94e83863c0e2652df29f92d952f2242661
ms.sourcegitcommit: 62cfdf02628530807f4d9c390d6ab623e2973fee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/05/2021
ms.locfileid: "115178026"
---
# <a name="chapter-5---usbx-device-class-considerations"></a>Bölüm 5 - USBX Cihaz Sınıfı Konuları

## <a name="device-class-registration"></a>Cihaz Sınıfı kaydı

Her cihaz sınıfı kayıt için aynı ilkeyi izler. Belirli sınıf parametrelerini içeren bir yapı, sınıf başlatma işlevine geçirildi.

```c
/* Set the parameters for callback when insertion/extraction of a HID device. */

hid_parameter.ux_slave_class_hid_instance_activate = tx_demo_hid_instance_activate;

hid_parameter.ux_slave_class_hid_instance_deactivate = tx_demo_hid_instance_deactivate;

/* Initialize the hid class parameters for the device. */
hid_parameter.ux_device_class_hid_parameter_report_address = hid_device_report;

hid_parameter.ux_device_class_hid_parameter_report_length = HID_DEVICE_REPORT_LENGTH;

hid_parameter.ux_device_class_hid_parameter_report_id = UX_TRUE;
hid_parameter.ux_device_class_hid_parameter_callback = demo_thread_hid_callback;

/* Initialize the device hid class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_hid_name,
    ux_device_class_hid_entry,1,0, (VOID *)&hid_parameter);
```

Sınıfın bir örneği etkinleştirildiğinde her sınıf isteğe bağlı olarak bir geri çağırma işlevi kaydedilebilir. Ardından geri çağırma, cihaz yığını tarafından uygulamanın bir örneğin oluşturularak ilgili bilgi vermek için çağrılır.

Aşağıdaki örnekte gösterildiği gibi uygulamanın gövdesinde etkinleştirme ve devre dışı bırakma için 2 işlev olabilir.

```c
VOID tx_demo_hid_instance_activate(VOID *hid_instance)
{
    /* Save the HID instance. */
    hid_slave = (UX_SLAVE_CLASS_HID *) hid_instance;
}

VOID tx_demo_hid_instance_deactivate(VOID *hid_instance)
{
    /* Reset the HID instance. */
    hid_slave = UX_NULL;
}
```

Bu işlevlerin içinde bir şey yapmak değil, sınıfın örneğini ezberlemek ve uygulamanın geri kalanıyla eşitlemek önerilmez.

## <a name="general-considerations-for-bulk-transfer"></a>Toplu Aktarımda Dikkat Edilmesi Gereken Genel Noktalar

USB 2.0 belirtimine göre, uç nokta her zaman veri yüklerini uç noktanın bildirilen wMaxPacketSize değerinden küçük veya buna eşit bir veri alanıyla ilettiği gerekir. Veri paketinin boyutu bMaxPacketSize ile sınırlıdır. Aktarım aşağıdaki durumlarla tamamlanır
1. Uç nokta tam olarak beklenen veri miktarını aktardı
2. Bir cihaz veya konak uç noktası boyut üst paket boyutundan (wMaxPacketSize) küçük bir paket alır. Bu kısa paket, daha fazla veri paketi olmadığını ve aktarımın tamamlandıktan sonra ya da aktaracak veri paketlerinin hepsi wMaxPacketSize'a eşit olduğunda aktarım sonu belirlenemedi. Aktarımın tamamlanması için Bir Sıfır Uzunluk Paketi(ZLP) Kısa paketler ve Sıfır Uzunluk Paketleri toplu veri aktarımının sonuna işaret ediyor olmalıdır. Yukarıdaki önemli noktalar ham toplu veri aktarımı API'leri (örneğin, ux_device_class_cdc_acm_read() için geçerlidir.

## <a name="usb-device-storage-class"></a>USB Cihaz Depolama Sınıfı

USB cihazı depolama sınıfı, sisteme eklenmiş bir depolama cihazının BIR USB ana bilgisayarı tarafından görünür halelanmasına olanak sağlar.

USB cihazı depolama sınıfı tek başına bir depolama çözümü sağlamaz. Yalnızca konaktan gelen SCSI isteklerini kabul eder ve yorumlar. Bu isteklerden biri okuma veya yazma komutu olduğunda, ATA cihaz sürücüsü veya Flash cihaz sürücüsü gibi gerçek bir depolama cihazı işleyicisine önceden tanımlanmış bir çağrı çağırır.

Cihaz depolama sınıfı başlatken, gerekli tüm bilgileri içeren sınıfa bir işaretçi yapısı verilir. Aşağıda bir örnek verilmiştir.

```c
/* Initialize the storage class parameters to customize vendor strings. */

storage_parameter.ux_slave_class_storage_parameter_vendor_id
    = demo_ux_system_slave_class_storage_vendor_id;

storage_parameter.ux_slave_class_storage_parameter_product_id
    = demo_ux_system_slave_class_storage_product_id;

storage_parameter.ux_slave_class_storage_parameter_product_rev
    = demo_ux_system_slave_class_storage_product_rev;

storage_parameter.ux_slave_class_storage_parameter_product_serial
    = demo_ux_system_slave_class_storage_product_serial;

/* Store the number of LUN in this device storage instance: single LUN. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 1;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x1e6bfe;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read_only_flag
    = UX_FALSE;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read
    = tx_demo_thread_flash_media_read;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write
    = tx_demo_thread_flash_media_write;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status
    = tx_demo_thread_flash_media_status;

/* Initialize the device storage class. The class is connected with interface 0 */
status = ux_device_stack_class_register(_ux_system_slave_class_storage_name,
    ux_device_class_storage_entry, ux_device_class_storage_thread, 0, (VOID *)&storage_parameter);
```

Bu örnekte, sürücü depolama dizeleri, karşılık gelen parametreye dize işaretçileri atanarak özelleştirilebilir. Dize işaretçilerinden herhangi biri dosyanın içinde UX_NULL varsayılan Azure RTOS kullanılır.

Bu örnekte, sürücünün son blok adresi veya LBA'sı ve mantıksal kesim boyutu verilmiştir. LBA, medya –1'de kullanılabilen kesimlerin sayısıdır. Blok uzunluğu normal depolama medyası içinde 512 olarak ayarlanır. Optik sürücüler için 2048 olarak ayarlanmıştır.

Depolama sınıfının medya için okumasına, yazmasına ve durumunu eldesına izin vermek için uygulamanın üç geri çağırma işlevi işaretçisi geçmesi gerekir.

Okuma ve yazma işlevlerinin prototipleri aşağıdaki örnekte gösterilmiştir.

```c
UINT media_read( 
    VOID *storage,  
    ULONG lun,  
    UCHAR *data_pointer,
    ULONG number_blocks,  
    ULONG lba,  
    ULONG *media_status);

UINT media_write( 
    VOID *storage,  
    ULONG lun,  
    UCHAR *data_pointer,
    ULONG number_blocks,  
    ULONG lba,  
    ULONG *media_status);
```

Konum:

- *depolama,* depolama sınıfının örneğidir.
- *lun,* komutun yönlendir olduğu LUN'dır.
- *data_pointer,* okuma veya yazma için kullanılacak arabelleğin adresidir.
- *number_blocks,* okunacak/yazacak kesimlerin sayısıdır.
- *lba,* okunacak kesim adresidir.
- *media_status* tam olarak medya durumu geri çağırma dönüş değeri gibi doldurulmalıdır.

Dönüş değeri, başarılı veya başarısız UX_SUCCESS veya UX_ERROR bir değere sahip olabilir. Bu işlemlerin başka bir hata kodu dönmesine gerek yoktur. Herhangi bir işlemde hata varsa depolama sınıfı durum çağrısı işlevini çağırır.

Bu işlev aşağıdaki prototipe sahiptir.

```c
ULONG media_status( 
    VOID *storage,  
    ULONG lun,  
    ULONG media_id,  
    ULONG *media_status);
```

Çağrı parametresi media_id şu anda kullanılmaz ve her zaman 0 olmalıdır. Gelecekte, birden çok depolama cihazı veya birden çok SCSI LUN'a sahip depolama cihazlarını ayırt etmek için kullanılabilir. Depolama sınıfının bu sürümü, depolama sınıfının veya birden çok SCSI LUN'a sahip depolama cihazlarının birden çok örneğini desteklemez.

Dönüş değeri, aşağıdaki biçime sahip bir SCSI hata kodudur.

- **Bit 0-7** Sense_key
- **Bit 8-15** Ek Sense Code
- **Bit 16-23** Ek Sense Code Niteleyicisi

Aşağıdaki tablo olası Sense/ASC/ASCQ birleşimlerini sağlar.

| Sense Key | ASC | ASCQ | Description                                       |
| --------- | --- | ---- | ------------------------------------------------- |
| 00        | 00  | 00   | ANLAMI YOK                                          |
| 01        | 17  | 01   | YENIDEN DENEMELERLE KURTARıLAN VERILER                       |
| 01        | 18  | 00   | ECC ILE KURTARıLAN VERILER                           |
| 02        | 04  | 01   | MANTıKSAL SÜRÜCÜ HAZıR DEĞIL - HAZıR OLMA          |
| 02        | 04  | 02   | MANTıKSAL SÜRÜCÜ HAZıR DEĞIL - BAŞLATMA GEREKIYOR |
| 02        | 04  | 04   | MANTıKSAL BIRIM HAZıR DEĞIL - BIÇIM DEVAM EDIYOR       |
| 02        | 04  | Ff   | MANTıKSAL SÜRÜCÜ HAZıR DEĞIL - CIHAZ MEŞGUL          |
| 02        | 06  | 00   | BAŞVURU KONUMU BULUNAMADı                       |
| 02        | 08  | 00   | MANTıKSAL BIRIM ILETIŞIM HATASı                |
| 02        | 08  | 01   | MANTıKSAL BIRIM ILETIŞIM ZAMAN OUT               |
| 02        | 08  | 80   | MANTıKSAL BIRIM ILETIŞIM TAŞMASı                |
| 02        | 3a  | 00   | ORTA YOK                                |
| 02        | 54  | 00   | USB-KONAK SISTEM ARABIRIMI HATASı              |
| 02        | 80  | 00   | YETERSIZ KAYNAKLAR                            |
| 02        | Ff  | Ff   | BILINMEYEN HATA                                     |
| 03        | 02  | 00   | ARAMA TAMAMLANMADı                                  |
| 03        | 03  | 00   | YAZMA HATASı                                       |
| 03        | 10  | 00   | ID CRC ERROR                                      |
| 03        | 11  | 00   | KURTARıLMAMıŞ OKUMA HATASı                            |
| 03        | 12  | 00   | KIMLIK ALANı IÇIN ADRES IŞARETI BULUNAMADı               |
| 03        | 13  | 00   | VERI ALANı IÇIN ADRES IŞARETI BULUNAMADı             |
| 03        | 14  | 00   | KAYıTLı VARLıK BULUNAMADı                         |
| 03        | 30  | 01   | ORTA OKUNAMAZ - BILINMEYEN BIÇIM               |
| 03        | 31  | 01   | FORMAT KOMUTU BAŞARıSıZ OLDU                             |
| 04        | 40  | Nn   | BILEŞEN NN'DE TANıLAMA HATASı (80H-FFH)      |
| 05        | 1A  | 00   | PARAMETRE LISTESI UZUNLUK HATASı                       |
| 05        | 20  | 00   | GEÇERSIZ KOMUT IŞLEM KODU                    |
| 05        | 21  | 00   | MANTıKSAL BLOK ADRESI ARALıK DıŞıNDA                |
| 05        | 24  | 00   | KOMUT PAKETINDE GEÇERSIZ ALAN                   |
| 05        | 25  | 00   | MANTıKSAL BIRIM DESTEKLENMIYOR                        |
| 05        | 26  | 00   | PARAMETRE LISTESINDE GEÇERSIZ ALAN                   |
| 05        | 26  | 01   | PARAMETRE DESTEKLENMIYOR                           |
| 05        | 26  | 02   | PARAMETRE DEĞERI GEÇERSIZ                           |
| 05        | 39  | 00   | PARAMETRELERI KAYDETME DESTEKLENMIYOR                     |
| 06        | 28  | 00   | HAZıR DEĞIL GEÇIŞI – MEDYA DEĞIŞTIRILDI     |
| 06        | 29  | 00   | SıFıRLAMA VEYA BUS CIHAZı SıFıRLAMANıN GÜCÜ OLUŞTU       |
| 06        | 2f  | 00   | BAŞKA BIR BAŞLATıCı TARAFıNDAN TEMIZLI KOMUTLAR             |
| 07        | 27  | 00   | KORUMALı MEDYA YAZMA                             |
| 0B        | 4e  | 00   | ÇAKıŞAN KOMUT DENENDI                      |

Uygulamanın uygulayabiliyor olduğu iki ek, isteğe bağlı geri çağırma vardır; Biri bir GET_STATUS_NOTIFICATION **komutuna** yanıt, diğeri de SYNCHRONIZE_CACHE **için.**

Uygulama, ana bilgisayar GET_STATUS_NOTIFICATION işlemek için aşağıdaki prototiple bir geri çağırma gerçekleştirebilir.

```c
UINT ux_slave_class_storage_media_notification( 
    VOID *storage,  
    ULONG lun,
    ULONG media_id,  
    ULONG notification_class,
    UCHAR **media_notification,  
    ULONG *media_notification_length);
```

Konum:

- *depolama,* depolama sınıfının örneğidir.
- *media_id* şu anda kullanılmadı. notification_class bildirim sınıfını belirtir.
- *media_notification,* uygulama tarafından bildirime verilen yanıtı içeren arabelleğe ayar gerekir.
- *media_notification_length,* uygulama tarafından yanıt arabelleğinin uzunluğunu içermesi için ayar olmalıdır.

Dönüş değeri, komutun başarılı olup olmadığını gösterir; komutun UX_SUCCESS **veya UX_ERROR.**

Uygulama bu geri çağırmayı uygulamazsa, **GET_STATUS_NOTIFICATION** aldıktan sonra USBX, komutun uygulanmadığını ana bilgisayara bildirecek.

**Uygulama SYNCHRONIZE_CACHE** konaktan yazmalar için önbellekten faydalanıyorsa, SYNCHRONIZE_CACHE komutu iş gerekir. Depolama aygıtının bağlantısının kesilecek olduğunu bilen bir konak bu komutu gönderebilir, örneğin Windows'da, araç çubuğunda bir flash sürücü simgesine sağ tıklar ve "Depolama cihazı adını çıkar"ı seçerse, Windows bu cihaza SYNCHRONIZE_CACHE komutunu \[ \] verir. 

Uygulama, ana bilgisayar GET_STATUS_NOTIFICATION **işlemek** için aşağıdaki prototiple bir geri çağırma gerçekleştirebilir.

```c
UINT ux_slave_class_storage_media_flush(
    VOID *storage, 
    ULONG lun,
    ULONG number_blocks, 
    ULONG lba, 
    ULONG *media_status);
```

Konum:

- *depolama,* depolama sınıfının örneğidir.
- *lun* parametresi komutun hangi LUN'a yönlendir olduğunu belirtir.
- *number_blocks* eşitlenecek blok sayısını belirtir.
- *lba,* eşitlenecek ilk bloğun kesim adresidir.
- *media_status* tam olarak medya durumu geri çağırma dönüş değeri gibi doldurulmalıdır.

Dönüş değeri, komutun başarılı olup olmadığını gösterir; komutun UX_SUCCESS **veya UX_ERROR.**

### <a name="multiple-scsi-lun"></a>Birden çok SCSI LUN'u

USBX cihaz depolama sınıfı birden çok LUN'u destekler. Bu nedenle, aynı anda CD-ROM ve Flash disk gibi davranan bir depolama cihazı oluşturmak mümkündür. Böyle bir durumda başlatma biraz farklı olabilir. Flash Disk ve CD-ROM örneği:

```c
/* Store the number of LUN in this device storage instance. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 2;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x7bbff;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read = tx_demo_thread_flash_media_read;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write = tx_demo_thread_flash_media_write;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status = tx_demo_thread_flash_media_status;

/* Initialize the storage class LUN parameters for reading/writing to the CD-ROM. */

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_last_lba = 0x04caaf;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_block_length = 2048;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_type = 5;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_removable_flag = 0x80;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_read = tx_demo_thread_cdrom_media_read;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_write = tx_demo_thread_cdrom_media_write;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_status = tx_demo_thread_cdrom_media_status;

/* Initialize the device storage class for a Flash disk and CD-ROM. The class is connected with interface 0 */ status = ux_device_stack_class_register(_ux_system_slave_class_storage_name,ux_device_class_storage_entry,
    ux_device_class_storage_thread,0, (VOID *) &storage_parameter);
```

## <a name="usb-device-cdc-acm-class"></a>USB Cihazı CDC-ACM Sınıfı

USB cihazı CDC-ACM sınıfı, usb konak sisteminin cihazla seri cihaz olarak iletişim kurmasına olanak sağlar. Bu sınıf USB standardını temel alan bir sınıftır ve CDC standardını temel alan bir alt kümedir.

CDC-ACM uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildiriliyor olması gerekir. Aşağıda bir örnek bulabilirsiniz.

```c
unsigned char device_framework_full_speed[] = {

    /*
    Device descriptor 18 bytes
    0x02 bDeviceClass: CDC class code
    0x00 bDeviceSubclass: CDC class sub code 0x00 bDeviceProtocol: CDC Device protocol
    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    */

    0x12, 0x01, 0x10, 0x01,
    0xEF, 0x02, 0x01, 0x08,
    0x84, 0x84, 0x00, 0x00,
    0x00, 0x01, 0x01, 0x02,
    0x03, 0x01,

    /* Configuration 1 descriptor 9 bytes */
    0x09, 0x02, 0x4b, 0x00, 0x02, 0x01, 0x00,0x40, 0x00,

    /* Interface association descriptor. 8 bytes. */
    0x08, 0x0b, 0x00,
    0x02, 0x02, 0x02, 0x00, 0x00,

    /* Communication Class Interface Descriptor Requirement. 9 bytes. */
    0x09, 0x04, 0x00, 0x00,0x01,0x02, 0x02, 0x01, 0x00,

    /* Header Functional Descriptor 5 bytes */
    0x05, 0x24, 0x00,0x10, 0x01,

    /* ACM Functional Descriptor 4 bytes */
    0x04, 0x24, 0x02,0x0f,

    /* Union Functional Descriptor 5 bytes */
    0x05, 0x24, 0x06, 0x00,

    /* Master interface */
    0x01, /* Slave interface */

    /* Call Management Functional Descriptor 5 bytes */
    0x05, 0x24, 0x01,0x03, 0x01, /* Data interface */

    /* Endpoint 1 descriptor 7 bytes */
    0x07, 0x05, 0x83, 0x03,0x08, 0x00, 0xFF,

    /* Data Class Interface Descriptor Requirement 9 bytes */
    0x09, 0x04, 0x01, 0x00, 0x02,0x0A, 0x00, 0x00, 0x00,

    /* First alternate setting Endpoint 1 descriptor 7 bytes*/
    0x07, 0x05, 0x02,0x02,0x40, 0x00,0x00,

    /* Endpoint 2 descriptor 7 bytes */
    0x07, 0x05, 0x81,0x02,0x40, 0x00, 0x00,

};
```

CDC-ACM sınıfı, arabirimleri (denetim ve veriler) gruplama için bileşik bir cihaz çerçevesi kullanır. Sonuç olarak, cihaz tanımlayıcısı tanımlarken dikkat gerekir. USBX, arabirimlerin nasıl bağlanacağını dahili olarak bilmek için IAD tanımlayıcısına sahiptir. IAD tanımlayıcısı arabirimlerden önce bildirilmiş olmalı ve CDC-ACM sınıfının ilk arabirimini ve kaç arabirimin ekli olduğunu içermeli.

CDC-ACM sınıfı, yeni IAD tanımlayıcısıyla aynı işlevi gerçekleştiren bir birleşim işlev tanımlayıcısı da kullanır. Geçmiş nedenlerle ve konak tarafıyla uyumluluk nedeniyle bir Birleşim İşlevi tanımlayıcısı bildiriliyor olsa da, USBX tarafından kullanılmaz.

CDC-ACM sınıfının başlatması aşağıdaki parametreleri bekler.

```c
/* Set the parameters for callback when insertion/extraction of a CDC device. */

parameter.ux_slave_class_cdc_acm_instance_activate = tx_demo_cdc_instance_activate;

parameter.ux_slave_class_cdc_acm_instance_deactivate = tx_demo_cdc_instance_deactivate;

parameter.ux_slave_class_cdc_acm_parameter_change = tx_demo_cdc_instance_parameter_change;

/* Initialize the device cdc class. This class owns both interfaces starting with 0. */
status = ux_device_stack_class_register(_ux_system_slave_class_cdc_acm_name,ux_device_class_cdc_acm_entry,
    1,0, &parameter);
```

Tanımlanan 2 parametre, yığın bu sınıfı etkinleştirirken veya devre dışı bırakıldığında çağrılır kullanıcı uygulamalarına geri çağırma işaretçileridir.

Tanımlanan üçüncü parametre, satır kodlaması veya satır durumları parametre değişikliği olduğunda çağrılacak kullanıcı uygulamasına yönelik bir geri çağırma işaretçisidir. Örneğin, konaktan DTR durumunu **TRUE** olarak değiştirme isteği olduğunda geri çağırma çağrılır, içinde kullanıcı uygulaması IOCTL işlevi aracılığıyla satır durumlarını ana bilgisayar iletişim için hazır olarak kontrol eder.

CDC-ACM bir USB-IF standardını temel almaktadır ve MACO'lar ve Linux işletim sistemleri tarafından otomatik olarak tanınır. Bu Windows, 10'dan önceki bir sürüm için bir .inf Windows gerektirir. Windows 10 herhangi bir .inf dosyası gerektirmez. CDC-ACM sınıfı için bir şablon sağlaruz ve bu şablon usbx_windows_host_files ***bulunabilir.*** Daha yeni bir sürüm Windows CDC_ACM_Template_Win7_64bit.inf dosyası kullanılmalıdır (Win10 hariç). Bu dosya, cihaz tarafından kullanılan PID/VID'i yansıtacak şekilde değiştirilmelidir. PiD/VID, şirket ve ürün USB-IF kaydı olduğunda son müşteriye özgü olur. Inf dosyasında değiştirilen alanlar burada bulunur.

```INF
[DeviceList]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000

[DeviceList.NTamd64]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000
```

CDC-ACM cihazın cihaz çerçevesinde PID/VID, cihaz tanımlayıcısında depolanır (yukarıda bildirilen cihaz tanımlayıcısına bakın).

USB ana bilgisayar sistemleri USB CDC-ACM cihazını bulasa, bir seri sınıf bağlar ve cihaz herhangi bir seri terminal programıyla kullanılabilir. Başvuru için bkz. konak İşletim Sistemi.

CDC-ACM sınıfı API işlevleri aşağıda tanımlanmıştır.

### <a name="ux_device_class_cdc_acm_ioctl"></a>ux_device_class_cdc_acm_ioctl

CDC-ACM arabiriminde IOCTL gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm, 
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın cdc acm arabirimine çeşitli ioctl çağrıları gerçekleştirmesi gerekirken çağrılır

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** Gerçekleştirilecek Ioctl işlevi.
- **parameter:** ioctl çağrısına özgü bir parametrenin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) Hatası

### <a name="example"></a>Örnek

```c
/* Start cdc acm callback transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START, &callback);

if(status != UX_SUCCESS)
    return;
```

### <a name="ioctl-functions"></a>Ioctl işlevleri:

| İşlev                                        | Değer |
| ----------------------------------------------- | - |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING    | 1 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING    | 2 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE     | 3 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE         | 4 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE     | 5 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START | 6 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP  | 7 |

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_coding"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING

CDC-ACM arabiriminde IOCTL Set Line Kodlaması gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın Satır Kodlama parametrelerini ayarlaması gerekirken çağrılır.

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING
- **parameter:** Bir çizgi parametre yapısının işaretçisi:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a>Dönüş Değeri

**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.

### <a name="example"></a>Örnek

```c
/* Change the line coding values. */

line_coding.ux_slave_class_cdc_acm_line_coding_dter = 9600;
line_coding.ux_slave_class_cdc_acm_line_coding_stop_bit =
    UX_HOST_CLASS_CDC_ACM_LINE_CODING_STOP_BIT_15;

line_coding.ux_slave_class_cdc_acm_line_coding_parity =
    UX_HOST_CLASS_CDC_ACM_LINE_CODING_PARITY_EVEN;

line_coding.ux_slave_class_cdc_acm_line_coding_data_bits = 5;

status = _ux_slave_class_cdc_acm_ioctl(cdc_acm,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING, &line_coding);

if (status != UX_SUCCESS)
    break;
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_coding"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING

CDC-ACM arabiriminde IOCTL Satır Kodlaması Al gerçekleştirme

### <a name="prototype"></a>Prototype

```c
device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın Satır Kodlama parametrelerini ala ihtiyacı olduğunda çağrılır.

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_ LINE_CODING
- **parameter:** Bir çizgi parametre yapısının işaretçisi:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.

### <a name="example"></a>Örnek

```c
/* This is to retrieve BAUD rate. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING, &line_coding);

/* Any error ? */
if (status == UX_SUCCESS)
{
    /* Decode BAUD rate. */
    switch (line_coding.ux_slave_class_cdc_acm_parameter_baudrate)
    {
        case 1200 :
            status = tx_demo_thread_slave_cdc_acm_response("1200", 4);
            break;
        case 2400 :
            status = tx_demo_thread_slave_cdc_acm_response("2400", 4);
            break;
        case 4800 :
            status = tx_demo_thread_slave_cdc_acm_response("4800", 4);
            break;
        case 9600 :
            status = tx_demo_thread_slave_cdc_acm_response("9600", 4);
            break;
        case 115200 :
            status = tx_demo_thread_slave_cdc_acm_response("115200", 6);
            break;
    }
}
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_state"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE

CDC-ACM arabiriminde IOCTL Satır Durumunu Al işlemini gerçekleştirme

## <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın Satır Durumu parametrelerini ala ihtiyacı olduğunda çağrılır.

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE
- **parameter:** Bir çizgi parametre yapısının işaretçisi:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.

### <a name="example"></a>Örnek

```c
/* This is to retrieve RTS state. */
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE, &line_state);

/* Any error ? */
if (status == UX_SUCCESS)
{
/* Check state. */
    if (line_state.ux_slave_class_cdc_acm_parameter_rts == UX_TRUE)
        /* State is ON. */
        status = tx_demo_thread_slave_cdc_acm_response("RTS ON", 6);
    else
        /* State is OFF. */
        status = tx_demo_thread_slave_cdc_acm_response("RTS OFF", 7);
}
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_state"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE

CDC-ACM arabiriminde IOCTL Set Line State gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın Satır Durumu parametrelerini ala ihtiyacı olduğunda çağrılır

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE
- **parameter:** Bir çizgi parametre yapısının işaretçisi:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.

### <a name="example"></a>Örnek

```c
/* This is to set RTS state. */

line_state.ux_slave_class_cdc_acm_parameter_rts = UX_TRUE;
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE, &line_state);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_abort_pipe"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE

CDC-ACM arabiriminde IOCTL ABORT PIPE gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın kanal durdurması gereken bir durumda çağrılır. Örneğin, devam eden bir yazma işlemi durdurmak UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT parametresi olarak geçir gerekir.

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** ux_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE
- **parametresi:** Kanal yönü:

```c
UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT 1

UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_RCV 2
```

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Geçersiz kanal yönü.

### <a name="example"></a>Örnek

```c
/* This is to abort the Xmit pipe. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE,
    UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_start"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START

CDC-ACM arabiriminde IOCTL İletim Başlangıcı gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulama geri arama ile iletim kullanmak istediği zaman çağrılır.

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START
- **parameter:** Start Transmission parametre yapısının işaretçisi:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER_STRUCT
{
    UINT (*ux_device_class_cdc_acm_parameter_write_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, ULONG length);
    UINT (*ux_device_class_cdc_acm_parameter_read_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *data_pointer, ULONG length);
} UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER;
```

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) İletim zaten başlatıldı.
- **UX_MEMORY_INSUFFICIENT** (0x12) Bellek ayırma başarısız oldu.

### <a name="example"></a>Örnek

```c
/* Set the callback parameter. */

callback.ux_device_class_cdc_acm_parameter_write_callback
    = tx_demo_thread_slave_write_callback;

callback.ux_device_class_cdc_acm_parameter_read_callback
    = tx_demo_thread_slave_read_callback;

/* Program the start of transmission. */
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START, &callback);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_stop"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP

CDC-ACM arabiriminde IOCTL İletimi Durdurma gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_ioctl( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, bir uygulama geri arama ile iletimi kullanmayı durdurmak istediği zaman çağrılır.

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **ioctl_function:** ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSI ON_STOP
- **parameter**: Kullanılmaz

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) Devam eden iletim yok.

### <a name="example"></a>Örnek

```c
/* Program the stop of transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP, UX_NULL);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_read"></a>ux_device_class_cdc_acm_read

CDC-ACM kanaldan okuma

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_read( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın OUT veri kanallarından (konaktan OUT, cihazdan IN) okuması gereken zaman çağrılır. Engelliyor.

> [!Note]
> Bu işlevler konaktan ham toplu verileri okur, bu nedenle arabellek dolu olana veya konak aktarımı kısa bir paketle (Sıfır Uzunluk Paketi dahil) sonlandırana kadar beklemede tutar. Diğer ayrıntılar için toplu aktarımla ilgili [**genel konular bölümüne bakın.**](#general-considerations-for-bulk-transfer)

### <a name="parameters"></a>Parametreler

- **cdc_acm:** cdc sınıfı örneğinin işaretçisi.
- **buffer:** Verilerin depolandığı arabellek adresi.
- **requested_length:** Beklediğiniz maksimum uzunluk.
- **actual_length:** Arabelleğe döndürülen uzunluk.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Cihaz artık yapılandırılmış durumda değil.
- **UX_TRANSFER_NO_ANSWER** (0x22) cihazdan yanıt yok. Aktarım beklenirken cihazın bağlantısı kesilmiş olabilir.

### <a name="example"></a>Örnek

```c
/* Read from the CDC class. */

status = ux_device_class_cdc_acm_read(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS) return;
```

### <a name="ux_device_class_cdc_acm_write"></a>ux_device_class_cdc_acm_write

CDC-ACM kanalına yazma

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_write( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın veri kanalına (konaktan, cihazdan) yazması gerektiğinde çağrılır. Engelliyor.

### <a name="parameters"></a>Parametreler

- **cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.
- **arabellek**: verilerin depolandığı arabellek adresi.
- **requested_length**: yazılacak arabelleğin uzunluğu.
- **actual_length**: yazma gerçekleştirildikten sonra arabelleğe döndürülen uzunluk.

### <a name="return-value"></a>Dönüş Değeri
- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) cihaz artık yapılandırılmış durumda değil.
- **UX_TRANSFER_NO_ANSWER** (0x22) cihazdan yanıt yok. Aktarım beklenirken cihazın bağlantısı kesilmiş olabilir.

### <a name="example"></a>Örnek

```c
/* Write to the CDC class bulk in pipe. */

status = ux_device_class_cdc_acm_write(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS)
    return;
```

### <a name="ux_device_class_cdc_acm_write_with_callback"></a>ux_device_class_cdc_acm_write_with_callback

Geri çağırma ile CDC-ACM kanalına yazma

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_cdc_acm_write_with_callback( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın veri kanalına (konaktan, cihazdan) yazması gerektiğinde çağrılır. Bu işlev engellenmeyen ve tamamlanma UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START bir geri çağırma aracılığıyla yapılır.

### <a name="parameters"></a>Parametreler

- **cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.
- **arabellek**: verilerin depolandığı arabellek adresi.
- **requested_length**: yazılacak arabelleğin uzunluğu.
- **actual_length**: yazma gerçekleştirildikten sonra arabelleğe döndürülen uzunluk

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) cihaz artık yapılandırılmış durumda değil.
- **UX_TRANSFER_NO_ANSWER** (0x22) cihazdan yanıt yok. Aktarım beklenirken cihazın bağlantısı kesilmiş olabilir.

### <a name="example"></a>Örnek

```c
/* Write to the CDC class bulk in pipe non blocking mode. */
status = ux_device_class_cdc_acm_write_with_callback(cdc, buffer, UX_DEMO_BUFFER_SIZE);

if(status != UX_SUCCESS)
    return;
```

### <a name="usb-device-cdc-ecm-class"></a>USB cihazı CDC-ECD sınıfı

USB cihazı CDC-ece sınıfı, USB konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak tanır. Bu sınıf, USB standardını temel alır ve CDC standardının bir alt kümesidir.

CDC-ACM uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildirilmesine ihtiyacı vardır. Aşağıda aşağıda bir örnek bulunur.

```c
unsigned char device_framework_full_speed[] = {

    /* Device descriptor 18 bytes
    0x02 bDeviceClass: CDC_ECM class code
    0x06 bDeviceSubclass: CDC_ECM class sub code
    0x00 bDeviceProtocol: CDC_ECM Device protocol
    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    0x3939 idVendor: Azure RTOS test.
    */
    
    0x12, 0x01, 0x10, 0x01,
    0x02, 0x00, 0x00, 0x08,
    0x39, 0x39, 0x08, 0x08, 0x00, 0x01, 0x01, 0x02, 03,0x01,
    
    /* Configuration 1 descriptor 9 bytes. */
    0x09, 0x02, 0x58, 0x00,0x02, 0x01, 0x00,0x40, 0x00,
    
    /* Interface association descriptor. 8 bytes. */
    
    0x08, 0x0b, 0x00, 0x02, 0x02, 0x06, 0x00, 0x00,
    
    /* Communication Class Interface Descriptor Requirement 9 bytes */
    0x09, 0x04, 0x00, 0x00,0x01,0x02, 0x06, 0x00, 0x00,
    
    /* Header Functional Descriptor 5 bytes */
    0x05, 0x24, 0x00, 0x10, 0x01,
    
    /* ECM Functional Descriptor 13 bytes */
    0x0D, 0x24, 0x0F, 0x04,0x00, 0x00, 0x00, 0x00, 0xEA, 0x05, 0x00,
    0x00,0x00,
    
    /* Union Functional Descriptor 5 bytes */
    0x05, 0x24, 0x06, 0x00,0x01,
    
    /* Endpoint descriptor (Interrupt) */
    0x07, 0x05, 0x83, 0x03, 0x08, 0x00, 0x08,
    
    /* Data Class Interface Descriptor Alternate Setting 0, 0 endpoints. 9 bytes */
    0x09, 0x04, 0x01, 0x00, 0x00, 0x0A, 0x00, 0x00, 0x00,
    
    /* Data Class Interface Descriptor Alternate Setting 1, 2 endpoints. 9 bytes */
    0x09, 0x04, 0x01, 0x01, 0x02, 0x0A, 0x00, 0x00,0x00,
    
    /* First alternate setting Endpoint 1 descriptor 7 bytes */
    0x07, 0x05, 0x02, 0x02, 0x40, 0x00, 0x00,
    
    /* Endpoint 2 descriptor 7 bytes */
    0x07, 0x05, 0x81, 0x02, 0x40, 0x00,0x00

};
```

CDC-ECD sınıfı, CDC-ACM öğesine çok benzer bir cihaz tanımlayıcısı yaklaşımı kullanır ve ayrıca bir ıAD tanımlayıcısı gerektirir. Tanım için CDC-ACM sınıfına bakın.

Normal cihaz altyapısına ek olarak, CDC-ECD özel dize tanımlayıcıları gerektirir. Aşağıda bir örnek verilmiştir.

```c
unsigned char string_framework[] = {
    /* Manufacturer string descriptor: Index 1 - "Azure RTOS" */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72, 0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,
    
    /* Product string descriptor: Index 2 - "EL CDCECM Device" */
    0x09, 0x04, 0x02, 0x10,
    0x45, 0x4c, 0x20, 0x43, 0x44, 0x43, 0x45, 0x43,
    0x4d, 0x20, 0x44, 0x65, 0x76, 0x69, 0x63, 0x64,
    
    /* Serial Number string descriptor: Index 3 - "0001" */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31,
    
    /* MAC Address string descriptor: Index 4 - "001E5841B879" */
    0x09, 0x04, 0x04, 0x0C,
    0x30, 0x30, 0x31, 0x45, 0x35, 0x38,
    0x34, 0x31, 0x42, 0x38, 0x37, 0x39

};
```

MAC adresi dize tanımlayıcısı, ana bilgisayar sorgularını TCP/IP protokolünde yanıtladığı MAC adresine göre yanıtlamak için CDC-ECD sınıfı tarafından kullanılır. Cihaz seçimine ayarlanabilir, ancak burada tanımlanması gerekir.

CDC-ECD sınıfının başlatılması aşağıdaki gibidir.

```c
/* Set the parameters for callback when insertion/extraction of a CDC device. Set to NULL.*/
cdc_ecm_parameter.ux_slave_class_cdc_ecm_instance_activate = UX_NULL;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_instance_deactivate = UX_NULL;

/* Define a NODE ID. */
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[0] = 0x00;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[1] = 0x1e;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[2] = 0x58;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[3] = 0x41;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[4] = 0xb8;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[5] = 0x78;

/* Define a remote NODE ID. */
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[0] = 0x00;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[1] = 0x1e;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[2] = 0x58;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[3] = 0x41;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[4] = 0xb8;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[5] = 0x79;

/* Initialize the device cdc_ecm class. */
status = ux_device_stack_class_register(_ux_system_slave_class_cdc_ecm_name,
    ux_device_class_cdc_ecm_entry, 1,0,&cdc_ecm_parameter);
```

Bu sınıfın başlatılması, etkinleştirme ve devre dışı bırakma için aynı işlev geri aramasını bekler, ancak burada bir alıştırma yapılmaması için bir alıştırmada NULL olarak ayarlanmıştır.

Sonraki Parametreler düğüm kimliklerinin tanımına yöneliktir. 2 düğüm, CDC-ECD, yerel bir düğüm ve uzak düğüm için gereklidir. Yerel düğüm, cihazın MAC adresini belirtir, uzak düğüm ise konağın MAC adresini belirtir. Uzak düğüm, Device Framework dize tanımlayıcısında bildirildiği ile aynı olmalıdır.

CDC-ECM sınıfında, her iki şekilde de verileri aktarmaya yönelik yerleşik API 'Ler vardır ancak kullanıcı uygulaması, USB Ethernet cihazından NetX üzerinden iletişim kurduğu için bu uygulamalar uygulamaya gizlenir.

USBX CDC-ece sınıfı, Azure RTOS NetX ağ yığınına yakın bir şekilde bağlanır. Hem NetX hem de USBX CDC-ECD sınıfını kullanan bir uygulama NetX ağ yığınını her zamanki şekilde etkinleştirir ancak ek olarak, USB ağ yığınını aşağıdaki şekilde etkinleştirmek gerekir.

```c
/* Initialize the NetX system. */
nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

USB ağ yığınının yalnızca bir kez etkinleştirilmesi ve CDCECD 'ye özgü olmaması gerekir, ancak NetX hizmetleri gerektiren herhangi bir USB sınıfı için gereklidir.

CDC-ECD sınıfı, MAC OS ve Linux konakları tarafından tanınır. ancak Microsoft Windows tarafından CDC-ecd ' y i tanımak için bir sürücü sağlanmaz. Windows platformları için bazı ticari ürünler mevcuttur ve kendi. inf dosyalarını sağlarlar. Bu dosyanın, USB ağ cihazının PID/VıD 'SI ile eşleşmesi için CDC-ACM INF şablonuyla aynı şekilde değiştirilmesi gerekir.

## <a name="usb-device-hid-class"></a>USB cihaz HID sınıfı

USB cihaz HID sınıfı, bir USB konak sisteminin, belirli HID istemci özelliklerine sahip bir HID cihazına bağlanmasına izin verir.

USBX HID cihaz sınıfı, ana bilgisayar tarafı ile karşılaştırıldığında nispeten basittir. Cihazın ve HID tanımlayıcısının davranışına yakın bir şekilde bağlanır.

Herhangi bir HID istemcisi öncelikle aşağıdaki örnekte gösterildiği gibi bir HID cihaz çerçevesini tanımlamanızı gerektirir.

```c
UCHAR device_framework_full_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x08,
    0x81, 0x0A, 0x01, 0x01, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x22, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x01, 0x03, 0x00, 0x00, 0x00,

    /* HID descriptor */
    0x09, 0x21, 0x10, 0x01, 0x21, 0x01, 0x22, 0x3f, 0x00,

    /* Endpoint descriptor (Interrupt) */
    0x07, 0x05, 0x81, 0x03, 0x08, 0x00, 0x08

};
```

HID çerçevesi, HID sınıfını ve HID cihaz alt sınıfını açıklayan bir arabirim tanımlayıcısı içerir. HID arabirimi tek başına bir sınıf veya bileşik bir cihazın parçası olabilir.

Şu anda, çoğu uygulama yalnızca bir KIMLIK (KIMLIK sıfır) gerektirdiğinden, USBX HID sınıfı birden çok rapor kimliğini desteklemez. İlgilendiğiniz bir özellik olan birden çok rapor kimliği varsa lütfen bizimle iletişime geçin.

HID sınıfının başlatılması, örnek olarak bir USB klavye kullanılarak aşağıdaki gibidir.

```c
/* Initialize the hid class parameters for a keyboard. */
hid_parameter.ux_device_class_hid_parameter_report_address = hid_keyboard_report;
hid_parameter.ux_device_class_hid_parameter_report_length = HID_KEYBOARD_REPORT_LENGTH;
hid_parameter.ux_device_class_hid_parameter_callback = tx_demo_thread_hid_callback;
hid_parameter.ux_device_class_hid_parameter_report_id = 0;

/* Initialize the device hid class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_hid_name,
    ux_device_class_hid_entry, 1,0,(VOID *)&hid_parameter);
if (status!=UX_SUCCESS)
    return;
```

Uygulamanın HID sınıfına bir HID rapor tanımlayıcısı ve uzunluğu geçmesi gerekir. Rapor tanımlayıcısı, cihazı tanımlayan öğelerin bir koleksiyonudur. HID dilbilgisi hakkında daha fazla bilgi için, HID USB sınıf belirtimine bakın.

Rapor tanımlayıcısına ek olarak, bir HID olayı gerçekleştiğinde uygulama bir geri çağrı geçirir.

USBX HID sınıfı, konaktan gelen aşağıdaki standart HID komutlarını destekler.

| Komut adı                             | Değer | Açıklama                                      |
| ---------------------------------------- | ----- | ------------------------------------------------ |
| UX_DEVICE_CLASS_HID_COMMAND_GET_REPORT   | 0x01  | Cihazdan rapor alın                     |
| UX_DEVICE_CLASS_HID_COMMAND_GET_IDLE     | 0x02  | Kesme uç noktasının boşta sıklığı 'nı al |
| UX_DEVICE_CLASS_HID_COMMAND_GET_PROTOCOL | 0x03  | Cihazda çalışan Protokolü al           |
| UX_DEVICE_CLASS_HID_COMMAND_SET_REPORT   | 0x09  | Cihaza bir rapor ayarlama                       |
| UX_DEVICE_CLASS_HID_COMMAND_SET_IDLE     | 0x0A  | Kesme uç noktasının boşta sıklığını ayarla |
| UX_DEVICE_CLASS_HID_COMMAND_SET_PROTOCOL | 0x0B  | Cihazda çalışan Protokolü al           |

Get ve set raporu, ana bilgisayar ile cihaz arasında verileri geri ve İleri aktarmak üzere HID tarafından en sık kullanılan komutlardır. En yaygın olarak, konak denetim uç noktasında veri gönderir, ancak kesme uç noktasında ya da verileri denetim uç noktasında getirmek için bir GET_REPORT komutu vererek veri alabilir.

HID sınıfı, ux_device_class_hid_event_set işlevini kullanarak kesme uç noktasındaki konağa veri gönderebilir.

### <a name="ux_device_class_hid_event_set"></a>ux_device_class_hid_event_set

Bir olayı HID sınıfına ayarlama

### <a name="prototype"></a>Prototype

```c
UINT ux_device_class_hid_event_set( 
    UX_SLAVE_CLASS_HID *hid,
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın bir HID olayını konağa geri gönderebilmesi gerektiğinde çağrılır. İşlev engellenmiyor, yalnızca raporu dairesel bir sıraya koyar ve uygulamaya döndürür.

### <a name="parameters"></a>Parametreler

- **HID**: HID sınıfı örneğine yönelik işaretçi.
- **hid_event**: HID olayının yapısına yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) hata döngüsel kuyrukta kullanılabilir alan yok.

### <a name="example"></a>Örnek

```c
/* Insert a key into the keyboard event. Length is fixed to 8. */
hid_event.ux_device_class_hid_event_length = 8;

/* First byte is a modifier byte. */
hid_event.ux_device_class_hid_event_buffer[0] = 0;

/* Second byte is reserved. */
hid_event.ux_device_class_hid_event_buffer[1] = 0;

/* The 6 next bytes are keys. We only have one key here. */
hid_event.ux_device_class_hid_event_buffer[2] = key;

/* Set the keyboard event. */
ux_device_class_hid_event_set(hid, &hid_event);
```

HID sınıfının başlatılmasında tanımlanan geri çağırma, bir olay göndermenin tersini yapar. Giriş, ana bilgisayar tarafından gönderilen olayı alır. Geri aramanın prototipi aşağıdaki gibidir.

### <a name="hid_callback"></a>hid_callback

HID sınıfından bir olay alma

### <a name="prototype"></a>Prototype

```c
UINT hid_callback(
    UX_SLAVE_CLASS_HID *hid, 
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a>Description

Bu işlev, ana bilgisayar uygulamaya bir HID raporu gönderdiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **HID**: HID sınıfı örneğine yönelik işaretçi.
- **hid_event**: HID olayının yapısına yönelik işaretçi.

### <a name="example"></a>Örnek

Aşağıdaki örnek, bir HID klavyesi için bir olayın nasıl yorumlanacağı gösterilmektedir:

```c
UINT tx_demo_thread_hid_callback(UX_SLAVE_CLASS_HID *hid, UX_SLAVE_CLASS_HID_EVENT *hid_event
{
/* There was an event. Analyze it. Is it NUM LOCK ? */

if (hid_event -\ux_device_class_hid_event_buffer[0] & HID_NUM_LOCK_MASK)
    /* Set the Num lock flag. */
    num_lock_flag = UX_TRUE;
else
    /* Reset the Num lock flag. */
    num_lock_flag = UX_FALSE;

/* There was an event. Analyze it. Is it CAPS LOCK ? */

if (hid_event -\ux_device_class_hid_event_buffer[0] & HID_CAPS_LOCK_MASK)
    /* Set the Caps lock flag. */
    caps_lock_flag = UX_TRUE;
else
    /* Reset the Caps lock flag. */
    caps_lock_flag = UX_FALSE;
}
```
