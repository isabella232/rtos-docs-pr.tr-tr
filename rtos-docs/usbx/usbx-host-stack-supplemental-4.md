---
title: USBX Pictbridge uygulaması
description: UBSX hem konakta hem de cihazda tam Pictbridge uygulamasını destekler. Pictbridge, iki tarafta da USBX PIMA sınıfının üzerinde yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9f4ba97741d2fc5f93afe6866b9ae6e9dc1e98a977eb3d6050c4a7489804c93c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790721"
---
# <a name="chapter-4-usbx-pictbridge-implementation"></a>Bölüm 4: USBX Pictbridge uygulaması

UBSX hem konakta hem de cihazda tam Pictbridge uygulamasını destekler. Pictbridge, iki tarafta da USBX PIMA sınıfının üzerinde yer almaktadır. 

PictBridge standartları, dijital bir halat kamerasının veya akıllı telefonun bilgisayar olmadan doğrudan yazıcıya bağlantısına olanak sağlayarak, Belirli Pictbridge uyumlu yazıcılara doğrudan yazdırmayı sağlar.

Yazıcıya bir kamera veya telefon bağlandığında yazıcı USB ana bilgisayarı, kamera ise USB cihazıdır. Ancak, Pictbridge ile kamera ana bilgisayar olarak görünür ve komutlar kameradan çalıştırılır. Kamera depolama sunucusu, yazıcı ise depolama istemcisidir. Kamera yazdırma istemcisidir ve yazıcı elbette yazdırma sunucusudur.

Pictbridge aktarım katmanı olarak USB kullanır, ancak iletişim protokolü için PTP 'yi (Resim Aktarım Protokolü) kullanır.

Aşağıda, bir yazdırma işi oluştuğunda DPS istemcisi ile DPS sunucusu arasındaki komutların/yanıtların diyagramı yer almaktadır.

![Yazdırma işi oluştuğunda D P S istemcisi ile D P S sunucusu arasındaki komutların/yanıtların diyagramı.](./media/usbx-host-stack-supplemental/dps-client-server.png)

## <a name="pictbridge-client-implementation"></a>Pictbridge istemci uygulaması

İstemcide Pictbridge, önce USBX cihaz yığınının ve PIMA sınıfının çalışıyor olması gerekir.

Cihaz çerçevesi PIMA sınıfını aşağıdaki şekilde açıklar.

```C
UCHAR device_framework_full_speed[] =
{
    /* Device descriptor */
       0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x20,
       0xA9, 0x04, 0xB6, 0x30, 0x00, 0x00, 0x00, 0x00,
       0x00, 0x01,
    /* Configuration descriptor */
       0x09, 0x02, 0x27, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,
    /* Interface descriptor */
       0x09, 0x04, 0x00, 0x00, 0x03, 0x06, 0x01, 0x01, 0x00,
    /* Endpoint descriptor (Bulk Out) */
       0x07, 0x05, 0x01, 0x02, 0x40, 0x00, 0x00,
    /* Endpoint descriptor (Bulk In) */
       0x07, 0x05, 0x82, 0x02, 0x40, 0x00, 0x00,
    /* Endpoint descriptor (Interrupt) */
       0x07, 0x05, 0x83, 0x03, 0x08, 0x00, 0x60
};
```

Pima sınıfı, 0x06 ID alanını kullanıyor ve hala Görüntü için 0x01 alt sınıfına sahip ve protokol PIMA 15740 için 0x01 olarak sınıflandırıldı.

Bu sınıfta 3 uç nokta tanımlanmıştır, veri göndermek/almak için 2 toplu ve olaylar için bir kesme vardır.

Diğer USBX cihaz uygulamalarının aksine, Pictbridge uygulamasının bir sınıfın kendisini tanımlaması gerek yoktur. Bunun yerine işlevi ***ux_pictbridge_dpsclient_start.*** Aşağıda bir örnek verilmiştir:

```C
/* Initialize the Pictbridge string components. */
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name,
    "Azure RTOS",10);
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name,
    "EL_Pictbridge_Camera",21);
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no, "ABC_123",7);
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions,
    "1.0 1.1",7);

pictbridge.ux_pictbridge_dpslocal.
    ux_pictbridge_devinfo_vendor_specific_version = 0x0100;

/* Start the Pictbridge client. */
status = ux_pictbridge_dpsclient_start(&pictbridge);

if(status != UX_SUCCESS)
    return;
```

pictbridge istemcisine geçirilen parametreler aşağıdaki gibidir:

```C
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name
    : String of Vendor name pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name
    : String of product name pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no,
    : String of serial number pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions
    : String of version pictbridge.ux_pictbridge_dpslocal. ux_pictbridge_devinfo_vendor_specific_version
    : Value set to 0x0100;
```

Sonraki adım, cihazın ve ana bilgisayar tarafından eşitlenmesi ve bilgi alışverişi için hazır olmasıdır.

Bu, aşağıdaki gibi bir olay bayrağı beklenerek yapılır:

```C
/* We should wait for the host and the client to discover one another. */
status = ux_utility_event_flags_get
    (&pictbridge.ux_pictbridge_event_flags_group,
    UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY,TX_AND_CLEAR, &actual_flags,
    UX_PICTBRIDGE_EVENT_TIMEOUT);
```

Durum makinesi DISCOVERY_COMPLETE **durumda** ise, kamera tarafı (DPS istemcisi) yazıcı ve özellikleriyle ilgili bilgi toplar.

DPS istemcisi yazdırma işini kabul etmeye hazırsa, durumu **UX_PICTBRIDGE_NEW_JOB_TRUE.** Aşağıdan denetlenebilirsiniz:

```C
/* Check if the printer is ready for a print job. */
if (pictbridge.ux_pictbridge_dpsclient.ux_pictbridge_devinfo_newjobok ==
    UX_PICTBRIDGE_NEW_JOB_TRUE)

    /* We can print something … */
```

Sonraki adımlarda bazı yazdırma joib tanımlayıcıları aşağıdaki gibi doldurulmalıdır:

```C
/* We can start a new job. Fill in the JobConfig and PrintInfo structures. */
jobinfo = &pictbridge.ux_pictbridge_jobinfo;

/* Attach a printinfo structure to the job. */
jobinfo ->ux_pictbridge_jobinfo_printinfo_start = &printinfo;

/* Set the default values for print job. */
jobinfo ->ux_pictbridge_jobinfo_quality =
    UX_PICTBRIDGE_QUALITIES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_papersize =
    UX_PICTBRIDGE_PAPER_SIZES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_papertype =
    UX_PICTBRIDGE_PAPER_TYPES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_filetype =
    UX_PICTBRIDGE_FILE_TYPES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_dateprint =
    UX_PICTBRIDGE_DATE_PRINTS_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_filenameprint =
    UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_imageoptimize =
    UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF;
jobinfo ->ux_pictbridge_jobinfo_layout =
    UX_PICTBRIDGE_LAYOUTS_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_fixedsize =
    UX_PICTBRIDGE_FIXED_SIZE_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_cropping =
    UX_PICTBRIDGE_CROPPINGS_DEFAULT;

/* Program the callback function for reading the object data. */
jobinfo ->ux_pictbridge_jobinfo_object_data_read =
    ux_demo_object_data_copy;

/* This is a demo, the fileID is hardwired (1 and 2 for scripts, 3 for photo to be printed. */

printinfo.ux_pictbridge_printinfo_fileid =
    UX_PICTBRIDGE_OBJECT_HANDLE_PRINT;

ux_utility_memory_copy(printinfo.ux_pictbridge_printinfo_filename,
    "Pictbridge demo file", 20);
ux_utility_memory_copy(printinfo.ux_pictbridge_printinfo_date, "01/01/2008",
    10);

/* Fill in the object info to be printed. First get the pointer to the object container in the job info structure. */
object = (UX_SLAVE_CLASS_PIMA_OBJECT *) jobinfo ->
    ux_pictbridge_jobinfo_object;

/* Store the object format: JPEG picture. */
object ->ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_EXIF_JPEG;
object ->ux_device_class_pima_object_compressed_size = IMAGE_LEN; object ->ux_device_class_pima_object_offset = 0;
object ->ux_device_class_pima_object_handle_id =
    UX_PICTBRIDGE_OBJECT_HANDLE_PRINT;
object ->ux_device_class_pima_object_length = IMAGE_LEN;

/* File name is in Unicode. */
ux_utility_string_to_unicode("JPEG Image", object ->
    ux_device_class_pima_object_filename);

/* And start the job. */
status =ux_pictbridge_dpsclient_api_start_job(&pictbridge);
```

Pictbridge istemcisinin artık yapacak bir yazdırma işi vardır ve alanda tanımlanan geri arama aracılığıyla görüntü bloklarını uygulamadan aynı anda getirir.

```C
jobinfo ->ux_pictbridge_jobinfo_object_data_read
```

Bu işlevin prototipi aşağıdaki gibi tanımlanır.

## <a name="ux_pictbridge_jobinfo_object_data_read"></a>ux_pictbridge_jobinfo_object_data_read

Yazdırma için kullanıcı alanı veri bloğu kopyalama.

### <a name="prototype"></a>Prototype

```C
UINT **ux_pictbridge_jobinfo_object_data_read(
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length,
    ULONG *actual_length)
```

### <a name="description"></a>Description

Bu işlev, DPS istemcisinin hedef Pictbridge yazıcıya yazdırmak için bir veri bloğu almaları gerekende çağrılır.

### <a name="parameters"></a>Parametreler

- **pictbridge:** pictbridge sınıf örneğinin işaretçisi.
- **object_buffer:** Nesne arabelleği işaretçisi
- **object_offset:** Veri bloğu okumaya başlamamız
- **object_length:** Döndürülen uzunluk
- **actual_length:** Gerçek uzunluk döndürüldü

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Bu işlem başarılı oldu.
- **UX_ERROR:**(0x01) Uygulama verileri aamadı.

### <a name="example"></a>Örnek

```C
/* Copy the object data. */

UINT ux_demo_object_data_copy(UX_PICTBRIDGE *pictbridge,UCHAR *object_buffer,
    ULONG object_offset, ULONG object_length, ULONG *actual_length)
{
    /* Copy the demanded object data portion. */
    ux_utility_memory_copy(object_buffer, image + object_offset,
        object_length);

    /* Update the actual length. */
    *actual_length = object_length;

    /* We have copied the requested data. Return OK. */
    return(UX_SUCCESS);
}
```

## <a name="pictbridge-host-implementation"></a>Pictbridge konak uygulaması

Pictbridge'in konak uygulaması istemciden farklıdır.

Pictbridge konak ortamında ilk olarak aşağıdaki örnekte olduğu gibi Pima sınıfını kaydetmek gerekir:

```C
status = ux_host_stack_class_register(ux_system_host_class_pima_name,
    ux_host_class_pima_entry);
if(status != UX_SUCCESS)
    return;
```

Bu sınıf, USB konak yığını ile Pictbridge katmanı arasında bulunan genel PTP katmanıdır.

Sonraki adım, yazdırma hizmetleri için Pictbridge varsayılan değerlerini aşağıdaki gibi başlatmaktır.

| Pictbridge alanı       | Değer                                  |
|------------------------|----------------------------------------|
| DpsVersion[0]          | 0x00010000                             |
| DpsVersion[1]          | 0x00010001                             |
| DpsVersion[2]          | 0x00000000                             |
| VendorSpecificVersion  | 0x00010000                             |
| PrintServiceAvailable  | 0x30010000                             |
| Kaliteler[0]           | UX_PICTBRIDGE_QUALITIES_DEFAULT        |
| Kaliteler[1]           | UX_PICTBRIDGE_QUALITIES_NORMAL         |
| Kaliteler[2]           | UX_PICTBRIDGE_QUALITIES_DRAFT          |
| Kaliteler[3]           | UX_PICTBRIDGE_QUALITIES_FINE           |
| PaperSizes[0]          | UX_PICTBRIDGE_PAPER_SIZES_DEFAULT      |
| PaperSizes[1]          | UX_PICTBRIDGE_PAPER_SIZES_4IX6I        |
| PaperSizes[2]          | UX_PICTBRIDGE_PAPER_SIZES_L            |
| PaperSizes[3]          | UX_PICTBRIDGE_PAPER_SIZES_2L           |
| PaperSizes[4]          | UX_PICTBRIDGE_PAPER_SIZES_LETTER       |
| PaperTypes[0]          | UX_PICTBRIDGE_PAPER_TYPES_DEFAULT      |
| PaperTypes[1]          | UX_PICTBRIDGE_PAPER_TYPES_PLAIN        |
| PaperTypes[2]          | UX_PICTBRIDGE_PAPER_TYPES_PHOTO        |
| FileTypes[0]           | UX_PICTBRIDGE_FILE_TYPES_DEFAULT       |
| FileTypes[1]           | UX_PICTBRIDGE_FILE_TYPES_EXIF_JPEG     |
| FileTypes[2]           | UX_PICTBRIDGE_FILE_TYPES_JFIF          |
| FileTypes[3]           | UX_PICTBRIDGE_FILE_TYPES_DPOF          |
| DatePrints[0]          | UX_PICTBRIDGE_DATE_PRINTS_DEFAULT      |
| DatePrints[1]          | UX_PICTBRIDGE_DATE_PRINTS_OFF          |
| DatePrints[2]          | UX_PICTBRIDGE_DATE_PRINTS_ON           |
| FileNamePrints[0]      | UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT |
| FileNamePrints[1]      | UX_PICTBRIDGE_FILE_NAME_PRINTS_OFF     |
| FileNamePrints[2]      | UX_PICTBRIDGE_FILE_NAME_PRINTS_ON      |
| ImageOptimizes[0]      | UX_PICTBRIDGE_IMAGE_OPTIMIZES_DEFAULT  |
| ImageOptimizes[1]      | UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF      |
| ImageOptimizes[2]      | UX_PICTBRIDGE_IMAGE_OPTIMIZES_ON       |
| Düzenler[0]             | UX_PICTBRIDGE_LAYOUTS_DEFAULT          |
| Düzenler[1]             | UX_PICTBRIDGE_LAYOUTS_1_UP_BORDER      |
| Düzenler[2]             | UX_PICTBRIDGE_LAYOUTS_INDEX_PRINT      |
| Düzenler[3]             | UX_PICTBRIDGE_LAYOUTS_1_UP_BORDERLESS  |
| FixedSizes[0]          | UX_PICTBRIDGE_FIXED_SIZE_DEFAULT       |
| FixedSizes[1]          | UX_PICTBRIDGE_FIXED_SIZE_35IX5I        |
| FixedSizes[2]          | UX_PICTBRIDGE_FIXED_SIZE_4IX6I         |
| FixedSizes[3]          | UX_PICTBRIDGE_FIXED_SIZE_5IX7I         |
| FixedSizes[4]          | UX_PICTBRIDGE_FIXED_SIZE_7CMX10CM      |
| FixedSizes[5]          | UX_PICTBRIDGE_FIXED_SIZE_LETTER        |
| FixedSizes[6]          | UX_PICTBRIDGE_FIXED_SIZE_A4            |
| Kırpmalar[0]           | UX_PICTBRIDGE_CROPPINGS_DEFAULT        |
| Kırpmalar[1]           | UX_PICTBRIDGE_CROPPINGS_OFF            |
| Kırpmalar[2]           | UX_PICTBRIDGE_CROPPINGS_ON             |

DPS ana bilgisayarının durum makinesi Boşta olarak ayarlanır ve yeni yazdırma işini kabul etmeye hazır olur.

Pictbridge'in konak bölümü artık aşağıdaki örnekte olduğu gibi başlatabilirsiniz.

```C
/* Activate the pictbridge dpshost. */

status = ux_pictbridge_dpshost_start(&pictbridge, pima);
if (status != UX_SUCCESS)
    return;
```

Veriler yazdırılabilir hale geldiğinde Pictbridge konak işlevi için bir geri çağırma gerekir. Bu, pictbridge konak yapısında aşağıdaki gibi bir işlev işaretçisi geçerek yapılır.

```C
/* Set a callback when an object is being received. */

pictbridge.ux_pictbridge_application_object_data_write =
    tx_demo_object_data_write;
```

Bu işlev aşağıdaki özelliklere sahiptir:

## <a name="ux_pictbridge_application_object_data_write"></a>ux_pictbridge_application_object_data_write

Yazdırma için bir veri bloğu yazma.

### <a name="prototype"></a>Prototype

```C
UINT **ux_pictbridge_application_object_data_write(
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,
    ULONG offset,
    ULONG total_length,
    ULONG length);
```

### <a name="description"></a>Description

Bu işlev, DPS sunucusunun yerel yazıcıya yazdırmak için DPS istemciden bir veri bloğu almaları gerekirken çağrılır.

### <a name="parameters"></a>Parametreler

- **pictbridge:** pictbridge sınıf örneğinin işaretçisi.
- **object_buffer:** Nesne arabelleği işaretçisi
- **object_offset:** Veri bloğu okumaya başlamamız
- **total_length:** Nesnenin tüm uzunluğu
- **length:** Bu arabelleğin uzunluğu

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Bu işlem başarılı oldu.
- **UX_ERROR:**(0x01) Uygulama verileri yazdıramdı.

### <a name="example"></a>Örnek

```C
/* Copy the object data. */

UINT tx_demo_object_data_write(UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer, ULONG offset, ULONG total_length, ULONG length);
{
    UINT status;

    /* Send the data to the local printer. */
    status = local_printer_data_send(object_buffer, length);

    /* We have printed the requested data. Return status. */
    return(status);
}
```
