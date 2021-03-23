---
title: Bölüm 4-USBX PictBridge uygulama
description: UBSX hem konakta hem de cihazda tam PictBridge uygulamasını destekler. PictBridge, her iki tarafta da USBX PIMA sınıfının üstünde yer alır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2ef1809dac046d49b15aba000cabed6c9fd458a3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828553"
---
# <a name="chapter-4---usbx-pictbridge-implementation"></a><span data-ttu-id="88ecc-104">Bölüm 4-USBX PictBridge uygulama</span><span class="sxs-lookup"><span data-stu-id="88ecc-104">Chapter 4 - USBX Pictbridge implementation</span></span>

<span data-ttu-id="88ecc-105">UBSX hem konakta hem de cihazda tam PictBridge uygulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="88ecc-105">UBSX supports the full Pictbridge implementation both on the host and the device.</span></span> <span data-ttu-id="88ecc-106">PictBridge, her iki tarafta da USBX PIMA sınıfının üstünde yer alır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-106">Pictbridge sits on top of USBX PIMA class on both sides.</span></span>

<span data-ttu-id="88ecc-107">PictBridge standartları, dijital bir kamera veya akıllı telefonun doğrudan bılgısayar olmadan bir yazıcıya bağlantısının yapılmasına izin verir ve belirli bir PictBridge kullanan yazıcılara doğrudan yazdırmayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-107">The PictBridge standards allows the connection of a digital still camera or a smart phone directly to a printer without a PC, enabling direct printing to certain Pictbridge aware printers.</span></span>

<span data-ttu-id="88ecc-108">Bir kamera veya telefon bir yazıcıya bağlıyken, yazıcı USB ana bilgisayarı ve kamera USB aygıtıdır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-108">When a camera or phone is connected to a printer, the printer is the USB host and the camera is the USB device.</span></span> <span data-ttu-id="88ecc-109">Ancak, PictBridge ile kamera ana bilgisayar olarak görünür ve bu da komutlar kameradan çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-109">However, with Pictbridge, the camera will appear as being the host and commands are driven from the camera.</span></span> <span data-ttu-id="88ecc-110">Kamera, depolama istemcisini yazıcı olan depolama sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="88ecc-110">The camera is the storage server, the printer the storage client.</span></span> <span data-ttu-id="88ecc-111">Kamera, yazdırma istemcsahiptir ve yazıcı, yazdırma sunucusu kursta.</span><span class="sxs-lookup"><span data-stu-id="88ecc-111">The camera is the print client and the printer is of course the print server.</span></span>

<span data-ttu-id="88ecc-112">PictBridge, USB 'yi bir aktarım katmanı olarak kullanır, ancak iletişim protokolüne ait PTP (resim aktarma protokolü) kullanır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-112">Pictbridge uses USB as a transport layer but relies on PTP (Picture Transfer Protocol) for the communication protocol.</span></span>

<span data-ttu-id="88ecc-113">Aşağıda, bir yazdırma işi gerçekleştiğinde DPS istemcisi ile DPS sunucusu arasındaki komutların/yanıtların bir diyagramı verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="88ecc-113">The following is a diagram of the commands/responses between the DPS client and the DPS server when a print job occurs:</span></span>

![DPS komutları ve yanıtları](./media/usbx-device-stack-supplemental/dps-client-server.png)

## <a name="pictbridge-client-implementation"></a><span data-ttu-id="88ecc-115">PictBridge istemci uygulama</span><span class="sxs-lookup"><span data-stu-id="88ecc-115">Pictbridge client implementation</span></span>

<span data-ttu-id="88ecc-116">İstemci üzerindeki PictBridge, USBX cihaz yığınını ve PIMA sınıfının önce çalıştırılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-116">The Pictbridge on the client requires the USBX device stack and the PIMA class to be running first.</span></span>

<span data-ttu-id="88ecc-117">Bir cihaz çerçevesi, PIMA sınıfını aşağıdaki şekilde açıklar.</span><span class="sxs-lookup"><span data-stu-id="88ecc-117">A device framework describes the PIMA class in the following way.</span></span>

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

<span data-ttu-id="88ecc-118">Pima sınıfı, 0x06 ID alanını kullanıyor ve alt sınıfı hala görüntü için 0x01 ve ıZMA 15740 için, protokol 0x01.</span><span class="sxs-lookup"><span data-stu-id="88ecc-118">The Pima class is using the ID field 0x06 and has its subclass is 0x01 for Still Image and the protocol is 0x01 for PIMA 15740.</span></span>

<span data-ttu-id="88ecc-119">Bu sınıfta üç uç nokta tanımlanmıştır; veri gönderme/alma ve olaylar için bir kesme için iki bulur.</span><span class="sxs-lookup"><span data-stu-id="88ecc-119">Three endpoints are defined in this class; two bulks for sending/receiving data and one interrupt for events.</span></span>

<span data-ttu-id="88ecc-120">Diğer USBX cihaz uygulamalarından farklı olarak, PictBridge uygulamasının bir sınıfın kendisini tanımlamasına gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="88ecc-120">Unlike other USBX device implementations, the Pictbridge application does not need to define a class itself.</span></span> <span data-ttu-id="88ecc-121">Bunun yerine ***ux_pictbridge_dpsclient_start*** işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-121">Rather it invokes the function ***ux_pictbridge_dpsclient_start***.</span></span> <span data-ttu-id="88ecc-122">Aşağıda bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-122">An example is below.</span></span>

```C
/* Initialize the Pictbridge string components. */
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name,
    "ExpressLogic",13);

ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name,
    "EL_Pictbridge_Camera",21);

ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no, "ABC_123",7);

ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions,
    "1.0 1.1",7);

pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_specific_version = 0x0100;

/* Start the Pictbridge client. */
status = ux_pictbridge_dpsclient_start(&pictbridge);

if(status != UX_SUCCESS)
    return;
```

<span data-ttu-id="88ecc-123">PictBridge istemcisine geçirilen parametreler aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-123">The parameters passed to the pictbridge client are as follows.</span></span>

```C
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name
    : String of Vendor name
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name
    : String of product name
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no
    : String of serial number
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions
    : String of version
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_specific_version
    : Value set to 0x0100;
```

<span data-ttu-id="88ecc-124">Sonraki adım cihaz ve ana bilgisayarın eşitlenmesi ve bilgi alışverişi için hazırlanmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-124">The next step is for the device and the host to synchronize and be ready to exchange information.</span></span>

<span data-ttu-id="88ecc-125">Bu, aşağıdaki gibi bir olay bayrağına karşı bekleyerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-125">This is done by waiting on an event flag as follows.</span></span>

```C
/* We should wait for the host and the client to discover one another. */
status = ux_utility_event_flags_get(&pictbridge.ux_pictbridge_event_flags_group,
    UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY,TX_AND_CLEAR,
    &actual_flags, UX_PICTBRIDGE_EVENT_TIMEOUT);
```

<span data-ttu-id="88ecc-126">Durum makinesi **DISCOVERY_COMPLETE** durumundaysa, kamera tarafı (DPS istemcisi) yazıcıyla ve özellikleri hakkında bilgi toplar.</span><span class="sxs-lookup"><span data-stu-id="88ecc-126">If the state machine is in the **DISCOVERY_COMPLETE** state, the camera side (the DPS client) will gather information regarding the printer and its capabilities.</span></span>

<span data-ttu-id="88ecc-127">DPS istemcisi bir yazdırma işini kabul etmeye hazırsanız, durumu **UX_PICTBRIDGE_NEW_JOB_TRUE** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-127">If the DPS client is ready to accept a print job, its status will be set to **UX_PICTBRIDGE_NEW_JOB_TRUE**.</span></span> <span data-ttu-id="88ecc-128">Aşağıda denetlenebilirler.</span><span class="sxs-lookup"><span data-stu-id="88ecc-128">It can be checked below.</span></span>

```C
/* Check if the printer is ready for a print job. */
if (pictbridge.ux_pictbridge_dpsclient.ux_pictbridge_devinfo_newjobok ==
    UX_PICTBRIDGE_NEW_JOB_TRUE)
/* We can print something … */
```

<span data-ttu-id="88ecc-129">Sonraki bazı Print joıb tanımlayıcılarının aşağıdaki şekilde doldurulması gerekir:</span><span class="sxs-lookup"><span data-stu-id="88ecc-129">Next some print joib descriptors need to be filled as follows:</span></span>

```C
/* We can start a new job. Fill in the JobConfig and PrintInfo structures. */
jobinfo = &pictbridge.ux_pictbridge_jobinfo;

/* Attach a printinfo structure to the job. */
jobinfo -> ux_pictbridge_jobinfo_printinfo_start = &printinfo;

/* Set the default values for print job. */
jobinfo -> ux_pictbridge_jobinfo_quality =
    UX_PICTBRIDGE_QUALITIES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_papersize =
    UX_PICTBRIDGE_PAPER_SIZES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_papertype =
    UX_PICTBRIDGE_PAPER_TYPES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_filetype =
    UX_PICTBRIDGE_FILE_TYPES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_dateprint =
    UX_PICTBRIDGE_DATE_PRINTS_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_filenameprint =
    UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_imageoptimize =
    UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF;
jobinfo -> ux_pictbridge_jobinfo_layout =
    UX_PICTBRIDGE_LAYOUTS_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_fixedsize =
    UX_PICTBRIDGE_FIXED_SIZE_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_cropping =
    UX_PICTBRIDGE_CROPPINGS_DEFAULT;

/* Program the callback function for reading the object data. */
jobinfo -> ux_pictbridge_jobinfo_object_data_read =
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
object -> ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_EXIF_JPEG;
object -> ux_device_class_pima_object_compressed_size = IMAGE_LEN;
object -> ux_device_class_pima_object_offset = 0;
object -> ux_device_class_pima_object_handle_id =
    UX_PICTBRIDGE_OBJECT_HANDLE_PRINT;
object -> ux_device_class_pima_object_length = IMAGE_LEN;

/* File name is in Unicode. */
ux_utility_string_to_unicode("JPEG Image", object ->
    ux_device_class_pima_object_filename);

/* And start the job. */
status =ux_pictbridge_dpsclient_api_start_job(&pictbridge);
```

<span data-ttu-id="88ecc-130">PictBridge istemcisinin şimdi bir yazdırma işi vardır ve alanda tanımlanan geri çağırma yoluyla görüntü bloklarını uygulamadan bir seferde bir kerede getirecek</span><span class="sxs-lookup"><span data-stu-id="88ecc-130">The Pictbridge client now has a print job to do and will fetch the image blocks at a time from the application through the callback defined in the field</span></span>

```C
jobinfo -> ux_pictbridge_jobinfo_object_data_read
```

<span data-ttu-id="88ecc-131">Bu işlevin prototipi şöyle tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="88ecc-131">The prototype of that function is defined as:</span></span>

## <a name="ux_pictbridge_jobinfo_object_data_read"></a><span data-ttu-id="88ecc-132">ux_pictbridge_jobinfo_object_data_read</span><span class="sxs-lookup"><span data-stu-id="88ecc-132">ux_pictbridge_jobinfo_object_data_read</span></span>

<span data-ttu-id="88ecc-133">Yazdırma için Kullanıcı alanından bir veri bloğunu kopyalama</span><span class="sxs-lookup"><span data-stu-id="88ecc-133">Copying a block of data from user space for printing</span></span>

### <a name="prototype"></a><span data-ttu-id="88ecc-134">Prototype</span><span class="sxs-lookup"><span data-stu-id="88ecc-134">Prototype</span></span>

```C
UINT ux_pictbridge_jobinfo_object_data_read( 
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,  
    ULONG object_offset,  
    ULONG object_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="88ecc-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88ecc-135">Description</span></span>

<span data-ttu-id="88ecc-136">Bu işlev, DPS istemcisinin hedef PictBridge yazıcısına yazdırmak için bir veri bloğu alması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-136">This function is called when the DPS client needs to retrieve a data block to print to the target Pictbridge printer.</span></span>

### <a name="parameters"></a><span data-ttu-id="88ecc-137">Parametreler</span><span class="sxs-lookup"><span data-stu-id="88ecc-137">Parameters</span></span>

- <span data-ttu-id="88ecc-138">**PictBridge**: PictBridge sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="88ecc-138">**pictbridge**: Pointer to the pictbridge class instance.</span></span>
- <span data-ttu-id="88ecc-139">**object_buffer**: nesne arabelleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="88ecc-139">**object_buffer**: Pointer to object buffer</span></span>
- <span data-ttu-id="88ecc-140">**object_offset**: veri bloğunu okumaya başlıyoruz</span><span class="sxs-lookup"><span data-stu-id="88ecc-140">**object_offset**: Where we are starting to read the data block</span></span>
- <span data-ttu-id="88ecc-141">**object_length**: döndürülecek uzunluk</span><span class="sxs-lookup"><span data-stu-id="88ecc-141">**object_length**: Length to be returned</span></span>
- <span data-ttu-id="88ecc-142">**actual_length**: gerçek uzunluk döndürüldü</span><span class="sxs-lookup"><span data-stu-id="88ecc-142">**actual_length**: Actual length returned</span></span>

### <a name="return-value"></a><span data-ttu-id="88ecc-143">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="88ecc-143">Return Value</span></span>

- <span data-ttu-id="88ecc-144">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="88ecc-144">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="88ecc-145">**UX_ERROR** (0x01) uygulama verileri alamadı.</span><span class="sxs-lookup"><span data-stu-id="88ecc-145">**UX_ERROR** (0x01) The application could not retrieve data.</span></span>

### <a name="example"></a><span data-ttu-id="88ecc-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="88ecc-146">Example</span></span>

```C
/* Copy the object data. */
UINT ux_demo_object_data_copy(
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length,
    ULONG *actual_length)
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

## <a name="pictbridge-host-implementation"></a><span data-ttu-id="88ecc-147">PictBridge ana bilgisayar uygulama</span><span class="sxs-lookup"><span data-stu-id="88ecc-147">Pictbridge host implementation</span></span>

<span data-ttu-id="88ecc-148">PictBridge 'nin ana bilgisayar uygulanması istemciden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-148">The host implementation of Pictbridge is different from the client.</span></span>

<span data-ttu-id="88ecc-149">Bir PictBridge ana bilgisayar ortamında yapmanız gereken ilk şey, aşağıdaki örnekte gösterildiği gibi Pima sınıfını kaydetmeişdir:</span><span class="sxs-lookup"><span data-stu-id="88ecc-149">The first thing to do in a Pictbridge host environment is to register the Pima class as the example below shows:</span></span>

```C
status = ux_host_stack_class_register(_ux_system_host_class_pima_name,
    ux_host_class_pima_entry);
if(status != UX_SUCCESS)
    return;
```

<span data-ttu-id="88ecc-150">Bu sınıf, USB yığını ve PictBridge katmanı arasında oturan genel PTP katmanıdır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-150">This class is the generic PTP layer sitting between the USB stack and the Pictbridge layer.</span></span>

<span data-ttu-id="88ecc-151">Sonraki adım, yazdırma hizmetleri için PictBridge varsayılan değerlerini aşağıda gösterildiği gibi başlatmalıdır:</span><span class="sxs-lookup"><span data-stu-id="88ecc-151">The next step is to initialize the Pictbridge default values for print services as follows:</span></span>

| <span data-ttu-id="88ecc-152">PictBridge alanı</span><span class="sxs-lookup"><span data-stu-id="88ecc-152">Pictbridge field</span></span>       | <span data-ttu-id="88ecc-153">Değer</span><span class="sxs-lookup"><span data-stu-id="88ecc-153">Value</span></span>                                  |
|------------------------|----------------------------------------|
| <span data-ttu-id="88ecc-154">DpsVersion [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-154">DpsVersion[0]</span></span>          | <span data-ttu-id="88ecc-155">0x00010000</span><span class="sxs-lookup"><span data-stu-id="88ecc-155">0x00010000</span></span>                             |
| <span data-ttu-id="88ecc-156">DpsVersion [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-156">DpsVersion[1]</span></span>          | <span data-ttu-id="88ecc-157">0x00010001</span><span class="sxs-lookup"><span data-stu-id="88ecc-157">0x00010001</span></span>                             |
| <span data-ttu-id="88ecc-158">DpsVersion [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-158">DpsVersion[2]</span></span>          | <span data-ttu-id="88ecc-159">0x00000000</span><span class="sxs-lookup"><span data-stu-id="88ecc-159">0x00000000</span></span>                             |
| <span data-ttu-id="88ecc-160">VendorSpecificVersion</span><span class="sxs-lookup"><span data-stu-id="88ecc-160">VendorSpecificVersion</span></span>  | <span data-ttu-id="88ecc-161">0x00010000</span><span class="sxs-lookup"><span data-stu-id="88ecc-161">0x00010000</span></span>                             |
| <span data-ttu-id="88ecc-162">PrintServiceAvailable</span><span class="sxs-lookup"><span data-stu-id="88ecc-162">PrintServiceAvailable</span></span>  | <span data-ttu-id="88ecc-163">0x30010000</span><span class="sxs-lookup"><span data-stu-id="88ecc-163">0x30010000</span></span>                             |
| <span data-ttu-id="88ecc-164">Kaliteleri [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-164">Qualities[0]</span></span>           | <span data-ttu-id="88ecc-165">UX_PICTBRIDGE_QUALITIES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-165">UX_PICTBRIDGE_QUALITIES_DEFAULT</span></span>        |
| <span data-ttu-id="88ecc-166">Kaliteleri [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-166">Qualities[1]</span></span>           | <span data-ttu-id="88ecc-167">UX_PICTBRIDGE_QUALITIES_NORMAL</span><span class="sxs-lookup"><span data-stu-id="88ecc-167">UX_PICTBRIDGE_QUALITIES_NORMAL</span></span>         |
| <span data-ttu-id="88ecc-168">Kaliteleri [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-168">Qualities[2]</span></span>           | <span data-ttu-id="88ecc-169">UX_PICTBRIDGE_QUALITIES_DRAFT</span><span class="sxs-lookup"><span data-stu-id="88ecc-169">UX_PICTBRIDGE_QUALITIES_DRAFT</span></span>          |
| <span data-ttu-id="88ecc-170">Kaliteleri [3]</span><span class="sxs-lookup"><span data-stu-id="88ecc-170">Qualities[3]</span></span>           | <span data-ttu-id="88ecc-171">UX_PICTBRIDGE_QUALITIES_FINE</span><span class="sxs-lookup"><span data-stu-id="88ecc-171">UX_PICTBRIDGE_QUALITIES_FINE</span></span>           |
| <span data-ttu-id="88ecc-172">Kağıt boyutları [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-172">PaperSizes[0]</span></span>          | <span data-ttu-id="88ecc-173">UX_PICTBRIDGE_PAPER_SIZES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-173">UX_PICTBRIDGE_PAPER_SIZES_DEFAULT</span></span>      |
| <span data-ttu-id="88ecc-174">Kağıt boyutları [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-174">PaperSizes[1]</span></span>          | <span data-ttu-id="88ecc-175">UX_PICTBRIDGE_PAPER_SIZES_4IX6I</span><span class="sxs-lookup"><span data-stu-id="88ecc-175">UX_PICTBRIDGE_PAPER_SIZES_4IX6I</span></span>        |
| <span data-ttu-id="88ecc-176">Kağıt boyutları [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-176">PaperSizes[2]</span></span>          | <span data-ttu-id="88ecc-177">UX_PICTBRIDGE_PAPER_SIZES_L</span><span class="sxs-lookup"><span data-stu-id="88ecc-177">UX_PICTBRIDGE_PAPER_SIZES_L</span></span>            |
| <span data-ttu-id="88ecc-178">Kağıt boyutları [3]</span><span class="sxs-lookup"><span data-stu-id="88ecc-178">PaperSizes[3]</span></span>          | <span data-ttu-id="88ecc-179">UX_PICTBRIDGE_PAPER_SIZES_2L</span><span class="sxs-lookup"><span data-stu-id="88ecc-179">UX_PICTBRIDGE_PAPER_SIZES_2L</span></span>           |
| <span data-ttu-id="88ecc-180">Kağıt boyutları [4]</span><span class="sxs-lookup"><span data-stu-id="88ecc-180">PaperSizes[4]</span></span>          | <span data-ttu-id="88ecc-181">UX_PICTBRIDGE_PAPER_SIZES_LETTER</span><span class="sxs-lookup"><span data-stu-id="88ecc-181">UX_PICTBRIDGE_PAPER_SIZES_LETTER</span></span>       |
| <span data-ttu-id="88ecc-182">PaperTypes [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-182">PaperTypes[0]</span></span>          | <span data-ttu-id="88ecc-183">UX_PICTBRIDGE_PAPER_TYPES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-183">UX_PICTBRIDGE_PAPER_TYPES_DEFAULT</span></span>      |
| <span data-ttu-id="88ecc-184">PaperTypes [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-184">PaperTypes[1]</span></span>          | <span data-ttu-id="88ecc-185">UX_PICTBRIDGE_PAPER_TYPES_PLAIN</span><span class="sxs-lookup"><span data-stu-id="88ecc-185">UX_PICTBRIDGE_PAPER_TYPES_PLAIN</span></span>        |
| <span data-ttu-id="88ecc-186">PaperTypes [2</span><span class="sxs-lookup"><span data-stu-id="88ecc-186">PaperTypes[2</span></span>           | <span data-ttu-id="88ecc-187">UX_PICTBRIDGE_PAPER_TYPES_PHOTO</span><span class="sxs-lookup"><span data-stu-id="88ecc-187">UX_PICTBRIDGE_PAPER_TYPES_PHOTO</span></span>        |
| <span data-ttu-id="88ecc-188">Fıletypes [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-188">FileTypes[0]</span></span>           | <span data-ttu-id="88ecc-189">UX_PICTBRIDGE_FILE_TYPES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-189">UX_PICTBRIDGE_FILE_TYPES_DEFAULT</span></span>       |
| <span data-ttu-id="88ecc-190">Fıletypes [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-190">FileTypes[1]</span></span>           | <span data-ttu-id="88ecc-191">UX_PICTBRIDGE_FILE_TYPES_EXIF_JPEG</span><span class="sxs-lookup"><span data-stu-id="88ecc-191">UX_PICTBRIDGE_FILE_TYPES_EXIF_JPEG</span></span>     |
| <span data-ttu-id="88ecc-192">Fıletypes [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-192">FileTypes[2]</span></span>           | <span data-ttu-id="88ecc-193">UX_PICTBRIDGE_FILE_TYPES_JFIF</span><span class="sxs-lookup"><span data-stu-id="88ecc-193">UX_PICTBRIDGE_FILE_TYPES_JFIF</span></span>          |
| <span data-ttu-id="88ecc-194">Fıletypes [3]</span><span class="sxs-lookup"><span data-stu-id="88ecc-194">FileTypes[3]</span></span>           | <span data-ttu-id="88ecc-195">UX_PICTBRIDGE_FILE_TYPES_DPOF</span><span class="sxs-lookup"><span data-stu-id="88ecc-195">UX_PICTBRIDGE_FILE_TYPES_DPOF</span></span>          |
| <span data-ttu-id="88ecc-196">Tarih baskılar [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-196">DatePrints[0]</span></span>          | <span data-ttu-id="88ecc-197">UX_PICTBRIDGE_DATE_PRINTS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-197">UX_PICTBRIDGE_DATE_PRINTS_DEFAULT</span></span>      |
| <span data-ttu-id="88ecc-198">Tarih baskılar [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-198">DatePrints[1]</span></span>          | <span data-ttu-id="88ecc-199">UX_PICTBRIDGE_DATE_PRINTS_OFF</span><span class="sxs-lookup"><span data-stu-id="88ecc-199">UX_PICTBRIDGE_DATE_PRINTS_OFF</span></span>          |
| <span data-ttu-id="88ecc-200">Tarih baskılar [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-200">DatePrints[2]</span></span>          | <span data-ttu-id="88ecc-201">UX_PICTBRIDGE_DATE_PRINTS_ON</span><span class="sxs-lookup"><span data-stu-id="88ecc-201">UX_PICTBRIDGE_DATE_PRINTS_ON</span></span>           |
| <span data-ttu-id="88ecc-202">Filenamebaskılar [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-202">FileNamePrints[0]</span></span>      | <span data-ttu-id="88ecc-203">UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-203">UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT</span></span> |
| <span data-ttu-id="88ecc-204">Dosyaadı[1] yazdırılıyor</span><span class="sxs-lookup"><span data-stu-id="88ecc-204">FileNamePrints[1]</span></span>      | <span data-ttu-id="88ecc-205">UX_PICTBRIDGE_FILE_NAME_PRINTS_OFF</span><span class="sxs-lookup"><span data-stu-id="88ecc-205">UX_PICTBRIDGE_FILE_NAME_PRINTS_OFF</span></span>     |
| <span data-ttu-id="88ecc-206">Filenamebaskılar [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-206">FileNamePrints[2]</span></span>      | <span data-ttu-id="88ecc-207">UX_PICTBRIDGE_FILE_NAME_PRINTS_ON</span><span class="sxs-lookup"><span data-stu-id="88ecc-207">UX_PICTBRIDGE_FILE_NAME_PRINTS_ON</span></span>      |
| <span data-ttu-id="88ecc-208">Imageoptimize [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-208">ImageOptimizes[0]</span></span>      | <span data-ttu-id="88ecc-209">UX_PICTBRIDGE_IMAGE_OPTIMIZES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-209">UX_PICTBRIDGE_IMAGE_OPTIMIZES_DEFAULT</span></span>  |
| <span data-ttu-id="88ecc-210">Imageoptimize [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-210">ImageOptimizes[1]</span></span>      | <span data-ttu-id="88ecc-211">UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF</span><span class="sxs-lookup"><span data-stu-id="88ecc-211">UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF</span></span>      |
| <span data-ttu-id="88ecc-212">Imageoptimize [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-212">ImageOptimizes[2]</span></span>      | <span data-ttu-id="88ecc-213">UX_PICTBRIDGE_IMAGE_OPTIMIZES_ON</span><span class="sxs-lookup"><span data-stu-id="88ecc-213">UX_PICTBRIDGE_IMAGE_OPTIMIZES_ON</span></span>       |
| <span data-ttu-id="88ecc-214">Düzenler [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-214">Layouts[0]</span></span>             | <span data-ttu-id="88ecc-215">UX_PICTBRIDGE_LAYOUTS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-215">UX_PICTBRIDGE_LAYOUTS_DEFAULT</span></span>          |
| <span data-ttu-id="88ecc-216">[1] düzenleri</span><span class="sxs-lookup"><span data-stu-id="88ecc-216">Layouts[1]</span></span>             | <span data-ttu-id="88ecc-217">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDER</span><span class="sxs-lookup"><span data-stu-id="88ecc-217">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDER</span></span>      |
| <span data-ttu-id="88ecc-218">[2] düzenleri</span><span class="sxs-lookup"><span data-stu-id="88ecc-218">Layouts[2]</span></span>             | <span data-ttu-id="88ecc-219">UX_PICTBRIDGE_LAYOUTS_INDEX_PRINT</span><span class="sxs-lookup"><span data-stu-id="88ecc-219">UX_PICTBRIDGE_LAYOUTS_INDEX_PRINT</span></span>      |
| <span data-ttu-id="88ecc-220">[3] düzenleri</span><span class="sxs-lookup"><span data-stu-id="88ecc-220">Layouts[3]</span></span>             | <span data-ttu-id="88ecc-221">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDERLESS</span><span class="sxs-lookup"><span data-stu-id="88ecc-221">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDERLESS</span></span>  |
| <span data-ttu-id="88ecc-222">Sabit boyutlar [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-222">FixedSizes[0]</span></span>          | <span data-ttu-id="88ecc-223">UX_PICTBRIDGE_FIXED_SIZE_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-223">UX_PICTBRIDGE_FIXED_SIZE_DEFAULT</span></span>       |
| <span data-ttu-id="88ecc-224">Sabit boyutlar [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-224">FixedSizes[1]</span></span>          | <span data-ttu-id="88ecc-225">UX_PICTBRIDGE_FIXED_SIZE_35IX5I</span><span class="sxs-lookup"><span data-stu-id="88ecc-225">UX_PICTBRIDGE_FIXED_SIZE_35IX5I</span></span>        |
| <span data-ttu-id="88ecc-226">Sabit boyutlar [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-226">FixedSizes[2]</span></span>          | <span data-ttu-id="88ecc-227">UX_PICTBRIDGE_FIXED_SIZE_4IX6I</span><span class="sxs-lookup"><span data-stu-id="88ecc-227">UX_PICTBRIDGE_FIXED_SIZE_4IX6I</span></span>         |
| <span data-ttu-id="88ecc-228">Sabit boyutlar [3]</span><span class="sxs-lookup"><span data-stu-id="88ecc-228">FixedSizes[3]</span></span>          | <span data-ttu-id="88ecc-229">UX_PICTBRIDGE_FIXED_SIZE_5IX7I</span><span class="sxs-lookup"><span data-stu-id="88ecc-229">UX_PICTBRIDGE_FIXED_SIZE_5IX7I</span></span>         |
| <span data-ttu-id="88ecc-230">Sabit boyutlar [4]</span><span class="sxs-lookup"><span data-stu-id="88ecc-230">FixedSizes[4]</span></span>          | <span data-ttu-id="88ecc-231">UX_PICTBRIDGE_FIXED_SIZE_7CMX10CM</span><span class="sxs-lookup"><span data-stu-id="88ecc-231">UX_PICTBRIDGE_FIXED_SIZE_7CMX10CM</span></span>      |
| <span data-ttu-id="88ecc-232">Sabit boyutlar [5]</span><span class="sxs-lookup"><span data-stu-id="88ecc-232">FixedSizes[5]</span></span>          | <span data-ttu-id="88ecc-233">UX_PICTBRIDGE_FIXED_SIZE_LETTER</span><span class="sxs-lookup"><span data-stu-id="88ecc-233">UX_PICTBRIDGE_FIXED_SIZE_LETTER</span></span>        |
| <span data-ttu-id="88ecc-234">Sabit boyutlar [6]</span><span class="sxs-lookup"><span data-stu-id="88ecc-234">FixedSizes[6]</span></span>          | <span data-ttu-id="88ecc-235">UX_PICTBRIDGE_FIXED_SIZE_A4</span><span class="sxs-lookup"><span data-stu-id="88ecc-235">UX_PICTBRIDGE_FIXED_SIZE_A4</span></span>            |
| <span data-ttu-id="88ecc-236">Croppings [0]</span><span class="sxs-lookup"><span data-stu-id="88ecc-236">Croppings[0]</span></span>           | <span data-ttu-id="88ecc-237">UX_PICTBRIDGE_CROPPINGS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="88ecc-237">UX_PICTBRIDGE_CROPPINGS_DEFAULT</span></span>        |
| <span data-ttu-id="88ecc-238">Croppings [1]</span><span class="sxs-lookup"><span data-stu-id="88ecc-238">Croppings[1]</span></span>           | <span data-ttu-id="88ecc-239">UX_PICTBRIDGE_CROPPINGS_OFF</span><span class="sxs-lookup"><span data-stu-id="88ecc-239">UX_PICTBRIDGE_CROPPINGS_OFF</span></span>            |
| <span data-ttu-id="88ecc-240">Croppings [2]</span><span class="sxs-lookup"><span data-stu-id="88ecc-240">Croppings[2]</span></span>           | <span data-ttu-id="88ecc-241">UX_PICTBRIDGE_CROPPINGS_ON</span><span class="sxs-lookup"><span data-stu-id="88ecc-241">UX_PICTBRIDGE_CROPPINGS_ON</span></span>             |

<span data-ttu-id="88ecc-242">DPS ana bilgisayarının durum makinesi, boşta olarak ayarlanacak ve yeni bir yazdırma işini kabul etmeye hazırlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-242">The state machine of the DPS host will be set to Idle and ready to accept a new print job.</span></span>

<span data-ttu-id="88ecc-243">Aşağıdaki örnekte gösterildiği gibi, PictBridge 'nin konak bölümü artık başlatılabilir:</span><span class="sxs-lookup"><span data-stu-id="88ecc-243">The host portion of Pictbridge can now be started as the example below shows:</span></span>

```C
/* Activate the pictbridge dpshost. */
status = ux_pictbridge_dpshost_start(&pictbridge, pima);

if (status != UX_SUCCESS)
    return;
```

<span data-ttu-id="88ecc-244">PictBridge ana bilgisayar işlevi, veriler yazdırılmaya hazırlandığı zaman bir geri çağırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-244">The Pictbridge host function requires a callback when data is ready to be printed.</span></span> <span data-ttu-id="88ecc-245">Bu, aşağıdaki gibi, PictBridge ana bilgisayar yapısında bir işlev işaretçisi geçirerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-245">This is accomplished by passing a function pointer in the pictbridge host structure as follows.</span></span>

```C
/* Set a callback when an object is being received. */
pictbridge.ux_pictbridge_application_object_data_write =
    tx_demo_object_data_write;
```

<span data-ttu-id="88ecc-246">Bu işlev aşağıdaki özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="88ecc-246">This function has the following properties.</span></span>

## <a name="ux_pictbridge_application_object_data_write"></a><span data-ttu-id="88ecc-247">ux_pictbridge_application_object_data_write</span><span class="sxs-lookup"><span data-stu-id="88ecc-247">ux_pictbridge_application_object_data_write</span></span>

<span data-ttu-id="88ecc-248">Yazdırma için bir veri bloğu yazma</span><span class="sxs-lookup"><span data-stu-id="88ecc-248">Writing a block of data for printing</span></span>

### <a name="prototype"></a><span data-ttu-id="88ecc-249">Prototype</span><span class="sxs-lookup"><span data-stu-id="88ecc-249">Prototype</span></span>

```C
UINT ux_pictbridge_application_object_data_write(
    UX_PICTBRIDGE *pictbridge, 
    UCHAR *object_buffer,
    ULONG offset,
    ULONG total_length,
    ULONG length);
```

### <a name="description"></a><span data-ttu-id="88ecc-250">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88ecc-250">Description</span></span>

<span data-ttu-id="88ecc-251">Bu işlev, DPS sunucusunun yerel yazıcıya yazdırmak için DPS istemcisinden bir veri bloğu alması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="88ecc-251">This function is called when the DPS server needs to retrieve a data block from the DPS client to print to the local printer.</span></span>

### <a name="parameters"></a><span data-ttu-id="88ecc-252">Parametreler</span><span class="sxs-lookup"><span data-stu-id="88ecc-252">Parameters</span></span>

- <span data-ttu-id="88ecc-253">**PictBridge**: PictBridge sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="88ecc-253">**pictbridge**: Pointer to the pictbridge class instance.</span></span>
- <span data-ttu-id="88ecc-254">**object_buffer**: nesne arabelleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="88ecc-254">**object_buffer**: Pointer to object buffer</span></span>
- <span data-ttu-id="88ecc-255">**object_offset**: veri bloğunu okumaya başlıyoruz</span><span class="sxs-lookup"><span data-stu-id="88ecc-255">**object_offset**: Where we are starting to read the data block</span></span>
- <span data-ttu-id="88ecc-256">**total_length**: tüm nesne uzunluğu</span><span class="sxs-lookup"><span data-stu-id="88ecc-256">**total_length**: Entire length of object</span></span>
- <span data-ttu-id="88ecc-257">**uzunluk**: Bu arabelleğin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="88ecc-257">**length**: Length of this buffer</span></span>

### <a name="return-value"></a><span data-ttu-id="88ecc-258">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="88ecc-258">Return Value</span></span>

- <span data-ttu-id="88ecc-259">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="88ecc-259">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="88ecc-260">**UX_ERROR** (0x01) uygulama verileri yazdıramadı.</span><span class="sxs-lookup"><span data-stu-id="88ecc-260">**UX_ERROR** (0x01) The application could not print data.</span></span>

### <a name="example"></a><span data-ttu-id="88ecc-261">Örnek</span><span class="sxs-lookup"><span data-stu-id="88ecc-261">Example</span></span>

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
