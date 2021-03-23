---
title: Bölüm 5-USBX cihaz sınıfı konuları
description: USBX cihaz sınıfı değerlendirmeleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 84f215ad990a2fe185a08f3876276528787ef8bc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826542"
---
# <a name="chapter-5---usbx-device-class-considerations"></a><span data-ttu-id="eddc4-103">Bölüm 5-USBX cihaz sınıfı konuları</span><span class="sxs-lookup"><span data-stu-id="eddc4-103">Chapter 5 - USBX Device Class Considerations</span></span>

## <a name="device-class-registration"></a><span data-ttu-id="eddc4-104">Cihaz sınıfı kaydı</span><span class="sxs-lookup"><span data-stu-id="eddc4-104">Device Class registration</span></span>

<span data-ttu-id="eddc4-105">Her cihaz sınıfı, kayıt için aynı prensibi izler.</span><span class="sxs-lookup"><span data-stu-id="eddc4-105">Each device class follows the same principle for registration.</span></span> <span data-ttu-id="eddc4-106">Sınıf Initialize işlevine belirli bir sınıf parametreleri içeren bir yapı geçirilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-106">A structure containing specific class parameters is passed to the class initialize function.</span></span>

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

<span data-ttu-id="eddc4-107">Sınıfın bir örneği etkinleştirildiğinde her bir sınıf, isteğe bağlı olarak bir geri çağırma işlevi kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-107">Each class can register, optionally, a callback function when a instance of the class gets activated.</span></span> <span data-ttu-id="eddc4-108">Geri arama daha sonra, uygulamayı bir örneğin oluşturulduğunu bilgilendirmek için cihaz yığını tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-108">The callback is then called by the device stack to inform the application that an instance was created.</span></span>

<span data-ttu-id="eddc4-109">Uygulamanın, aşağıdaki örnekte gösterildiği gibi, etkinleştirme ve devre dışı bırakma için 2 işlevi gövdesinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-109">The application would have in its body the 2 functions for activation and deactivation, as shown in the following example.</span></span>

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

<span data-ttu-id="eddc4-110">Bu işlevler içinde herhangi bir şey yapmanız önerilmez, ancak sınıfın örneğini yeniden yüklemek ve uygulamanın geri kalanı ile eşitlemek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-110">It is not recommended to do anything within these functions but to memorize the instance of the class and synchronize with the rest of the application.</span></span>

## <a name="usb-device-storage-class"></a><span data-ttu-id="eddc4-111">USB cihaz depolama sınıfı</span><span class="sxs-lookup"><span data-stu-id="eddc4-111">USB Device Storage Class</span></span>

<span data-ttu-id="eddc4-112">USB cihaz depolama sınıfı, sistemde gömülü bir depolama cihazının USB ana bilgisayarına görünür hale getirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="eddc4-112">The USB device storage class allows for a storage device embedded in the system to be made visible to a USB host.</span></span>

<span data-ttu-id="eddc4-113">USB cihaz depolama sınıfı kendi kendine bir depolama çözümü sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="eddc4-113">The USB device storage class does not by itself provide a storage solution.</span></span> <span data-ttu-id="eddc4-114">Yalnızca konaktan gelen SCSI isteklerini kabul eder ve yorumlar.</span><span class="sxs-lookup"><span data-stu-id="eddc4-114">It merely accepts and interprets SCSI requests coming from the host.</span></span> <span data-ttu-id="eddc4-115">Bu isteklerden biri bir okuma veya yazma komutu olduğunda, bir ATA cihaz sürücüsü veya bir Flash cihaz sürücüsü gibi gerçek bir depolama cihazı işleyicisine önceden tanımlanmış bir çağrı çağırır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-115">When one of these requests is a read or a write command, it will invoke a pre-defined call back to a real storage device handler, such as an ATA device driver or a Flash device driver.</span></span>

<span data-ttu-id="eddc4-116">Cihaz depolama sınıfı başlatılırken, gerekli tüm bilgileri içeren sınıfa bir işaretçi yapısı verilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-116">When initializing the device storage class, a pointer structure is given to the class that contains all the information necessary.</span></span> <span data-ttu-id="eddc4-117">Aşağıda bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-117">An example is given below.</span></span>

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

<span data-ttu-id="eddc4-118">Bu örnekte, sürücü depolama dizeleri karşılık gelen parametreye dize işaretçileri atayarak özelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-118">In this example, the driver storage strings are customized by assigning string pointers to corresponding parameter.</span></span> <span data-ttu-id="eddc4-119">Dize işaretçisinden herhangi biri UX_NULL bırakılırsa, varsayılan Azure RTOS dizesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-119">If any one of the string pointer is left to UX_NULL, the default Azure RTOS string is used.</span></span>

<span data-ttu-id="eddc4-120">Bu örnekte, sürücünün son blok adresi veya LBA, mantıksal kesim boyutu ile birlikte verilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-120">In this example, the drive's last block address or LBA is given as well as the logical sector size.</span></span> <span data-ttu-id="eddc4-121">LBA, medyada bulunan kesimlerin sayısıdır – 1.</span><span class="sxs-lookup"><span data-stu-id="eddc4-121">The LBA is the number of sectors available in the media –1.</span></span> <span data-ttu-id="eddc4-122">Blok uzunluğu normal depolama medyasında 512 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-122">The block length is set to 512 in regular storage media.</span></span> <span data-ttu-id="eddc4-123">Bu, optik sürücüler için 2048 olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-123">It can be set to 2048 for optical drives.</span></span>

<span data-ttu-id="eddc4-124">Uygulamanın, depolama sınıfının medya için durum okumasına, yazmasına ve almasına izin vermek üzere üç geri çağırma işlevi işaretçisi geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-124">The application needs to pass three callback function pointers to allow the storage class to read, write and obtain status for the media.</span></span>

<span data-ttu-id="eddc4-125">Okuma ve yazma işlevlerine yönelik prototipler aşağıdaki örnekte gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-125">The prototypes for the read and write functions are shown in the example below.</span></span>

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

<span data-ttu-id="eddc4-126">Konum:</span><span class="sxs-lookup"><span data-stu-id="eddc4-126">Where:</span></span>

- <span data-ttu-id="eddc4-127">*depolama* , depolama sınıfının örneğidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-127">*storage* is the instance of the storage class.</span></span>
- <span data-ttu-id="eddc4-128">*LUN* , komutun yönlendirildiği LUN 'dur.</span><span class="sxs-lookup"><span data-stu-id="eddc4-128">*lun* is the LUN the command is directed to.</span></span>
- <span data-ttu-id="eddc4-129">*data_pointer* , okuma veya yazma için kullanılacak arabelleğin adresidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-129">*data_pointer* is the address of the buffer to be used for reading or writing.</span></span>
- <span data-ttu-id="eddc4-130">*number_blocks* okunacak/yazılacak kesimlerin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-130">*number_blocks* is the number of sectors to read/write.</span></span>
- <span data-ttu-id="eddc4-131">*LBA* , okunan kesim adresidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-131">*lba* is the sector address to read.</span></span>
- <span data-ttu-id="eddc4-132">*media_status* , tam olarak medya durumu geri çağırma dönüş değeri gibi doldurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-132">*media_status* should be filled out exactly like the media status callback return value.</span></span>

<span data-ttu-id="eddc4-133">Dönüş değeri UX_SUCCESS veya başarılı ya da başarısız bir işlemi gösteren UX_ERROR olabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-133">The return value can have either the value UX_SUCCESS or UX_ERROR indicating a successful or unsuccessful operation.</span></span> <span data-ttu-id="eddc4-134">Bu işlemlerin herhangi bir hata kodunu döndürmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="eddc4-134">These operations do not need to return any other error codes.</span></span> <span data-ttu-id="eddc4-135">Herhangi bir işlemde hata varsa, depolama sınıfı durum geri çağırma işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-135">If there is an error in any operation, the storage class will invoke the status call back function.</span></span>

<span data-ttu-id="eddc4-136">Bu işlev aşağıdaki prototipi içerir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-136">This function has the following prototype.</span></span>

```c
ULONG media_status( 
    VOID *storage,  
    ULONG lun,  
    ULONG media_id,  
    ULONG *media_status);
```

<span data-ttu-id="eddc4-137">Çağıran parametre media_id Şu anda kullanılmıyor ve her zaman 0 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-137">The calling parameter media_id is not currently used and should always be 0.</span></span> <span data-ttu-id="eddc4-138">Gelecekte birden çok depolama cihazını veya depolama cihazlarını birden çok SCSI LUN ile ayırt etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-138">In the future it may be used to distinguish multiple storage devices or storage devices with multiple SCSI LUNs.</span></span> <span data-ttu-id="eddc4-139">Depolama sınıfının bu sürümü, birden fazla SCSI LUN ile depolama sınıfının veya depolama cihazlarının birden çok örneğini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="eddc4-139">This version of the storage class does not support multiple instances of the storage class or storage devices with multiple SCSI LUNs.</span></span>

<span data-ttu-id="eddc4-140">Dönüş değeri, aşağıdaki biçime sahip olabilir bir SCSI hata kodudur.</span><span class="sxs-lookup"><span data-stu-id="eddc4-140">The return value is a SCSI error code that can have the following format.</span></span>

- <span data-ttu-id="eddc4-141">**Bıts 0-7** Sense_key</span><span class="sxs-lookup"><span data-stu-id="eddc4-141">**Bits 0-7** Sense_key</span></span>
- <span data-ttu-id="eddc4-142">**Bıts 8-15** Ek algılama kodu</span><span class="sxs-lookup"><span data-stu-id="eddc4-142">**Bits 8-15** Additional Sense Code</span></span>
- <span data-ttu-id="eddc4-143">**Bıts 16-23** Ek algılama kod niteleyicisi</span><span class="sxs-lookup"><span data-stu-id="eddc4-143">**Bits 16-23** Additional Sense Code Qualifier</span></span>

<span data-ttu-id="eddc4-144">Aşağıdaki tabloda olası Sense/ASC/ASCQ birleşimleri sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-144">The following table provides the possible Sense/ASC/ASCQ combinations.</span></span>

| <span data-ttu-id="eddc4-145">Algılama anahtarı</span><span class="sxs-lookup"><span data-stu-id="eddc4-145">Sense Key</span></span> | <span data-ttu-id="eddc4-146">ASC</span><span class="sxs-lookup"><span data-stu-id="eddc4-146">ASC</span></span> | <span data-ttu-id="eddc4-147">YOKQ</span><span class="sxs-lookup"><span data-stu-id="eddc4-147">ASCQ</span></span> | <span data-ttu-id="eddc4-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-148">Description</span></span>                                       |
| --------- | --- | ---- | ------------------------------------------------- |
| <span data-ttu-id="eddc4-149">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-149">00</span></span>        | <span data-ttu-id="eddc4-150">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-150">00</span></span>  | <span data-ttu-id="eddc4-151">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-151">00</span></span>   | <span data-ttu-id="eddc4-152">FIKIR YOK</span><span class="sxs-lookup"><span data-stu-id="eddc4-152">NO SENSE</span></span>                                          |
| <span data-ttu-id="eddc4-153">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-153">01</span></span>        | <span data-ttu-id="eddc4-154">17</span><span class="sxs-lookup"><span data-stu-id="eddc4-154">17</span></span>  | <span data-ttu-id="eddc4-155">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-155">01</span></span>   | <span data-ttu-id="eddc4-156">YENIDEN DENEMELER IÇEREN KURTARıLAN VERILER</span><span class="sxs-lookup"><span data-stu-id="eddc4-156">RECOVERED DATA WITH RETRIES</span></span>                       |
| <span data-ttu-id="eddc4-157">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-157">01</span></span>        | <span data-ttu-id="eddc4-158">18</span><span class="sxs-lookup"><span data-stu-id="eddc4-158">18</span></span>  | <span data-ttu-id="eddc4-159">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-159">00</span></span>   | <span data-ttu-id="eddc4-160">ECC ILE KURTARıLAN VERILER</span><span class="sxs-lookup"><span data-stu-id="eddc4-160">RECOVERED DATA WITH ECC</span></span>                           |
| <span data-ttu-id="eddc4-161">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-161">02</span></span>        | <span data-ttu-id="eddc4-162">04</span><span class="sxs-lookup"><span data-stu-id="eddc4-162">04</span></span>  | <span data-ttu-id="eddc4-163">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-163">01</span></span>   | <span data-ttu-id="eddc4-164">MANTıKSAL SÜRÜCÜ, HAZıRLAMA IÇIN HAZıRLANMA</span><span class="sxs-lookup"><span data-stu-id="eddc4-164">LOGICAL DRIVE NOT READY - BECOMING READY</span></span>          |
| <span data-ttu-id="eddc4-165">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-165">02</span></span>        | <span data-ttu-id="eddc4-166">04</span><span class="sxs-lookup"><span data-stu-id="eddc4-166">04</span></span>  | <span data-ttu-id="eddc4-167">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-167">02</span></span>   | <span data-ttu-id="eddc4-168">MANTıKSAL SÜRÜCÜ KULLANıMA ALıNAMADı-BAŞLATMA GEREKIYOR</span><span class="sxs-lookup"><span data-stu-id="eddc4-168">LOGICAL DRIVE NOT READY - INITIALIZATION REQUIRED</span></span> |
| <span data-ttu-id="eddc4-169">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-169">02</span></span>        | <span data-ttu-id="eddc4-170">04</span><span class="sxs-lookup"><span data-stu-id="eddc4-170">04</span></span>  | <span data-ttu-id="eddc4-171">04</span><span class="sxs-lookup"><span data-stu-id="eddc4-171">04</span></span>   | <span data-ttu-id="eddc4-172">MANTıKSAL BIRIM READY-FORMAT DEVAM EDIYOR</span><span class="sxs-lookup"><span data-stu-id="eddc4-172">LOGICAL UNIT NOT READY - FORMAT IN PROGRESS</span></span>       |
| <span data-ttu-id="eddc4-173">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-173">02</span></span>        | <span data-ttu-id="eddc4-174">04</span><span class="sxs-lookup"><span data-stu-id="eddc4-174">04</span></span>  | <span data-ttu-id="eddc4-175">BENZERI</span><span class="sxs-lookup"><span data-stu-id="eddc4-175">FF</span></span>   | <span data-ttu-id="eddc4-176">MANTıKSAL SÜRÜCÜ READY-CIHAZ MEŞGUL</span><span class="sxs-lookup"><span data-stu-id="eddc4-176">LOGICAL DRIVE NOT READY - DEVICE IS BUSY</span></span>          |
| <span data-ttu-id="eddc4-177">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-177">02</span></span>        | <span data-ttu-id="eddc4-178">06</span><span class="sxs-lookup"><span data-stu-id="eddc4-178">06</span></span>  | <span data-ttu-id="eddc4-179">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-179">00</span></span>   | <span data-ttu-id="eddc4-180">BAŞVURU KONUMU BULUNAMADı</span><span class="sxs-lookup"><span data-stu-id="eddc4-180">NO REFERENCE POSITION FOUND</span></span>                       |
| <span data-ttu-id="eddc4-181">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-181">02</span></span>        | <span data-ttu-id="eddc4-182">08</span><span class="sxs-lookup"><span data-stu-id="eddc4-182">08</span></span>  | <span data-ttu-id="eddc4-183">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-183">00</span></span>   | <span data-ttu-id="eddc4-184">MANTıKSAL BIRIM ILETIŞIM HATASı</span><span class="sxs-lookup"><span data-stu-id="eddc4-184">LOGICAL UNIT COMMUNICATION FAILURE</span></span>                |
| <span data-ttu-id="eddc4-185">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-185">02</span></span>        | <span data-ttu-id="eddc4-186">08</span><span class="sxs-lookup"><span data-stu-id="eddc4-186">08</span></span>  | <span data-ttu-id="eddc4-187">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-187">01</span></span>   | <span data-ttu-id="eddc4-188">MANTıKSAL BIRIM ILETIŞIM ZAMAN AŞıMı</span><span class="sxs-lookup"><span data-stu-id="eddc4-188">LOGICAL UNIT COMMUNICATION TIME-OUT</span></span>               |
| <span data-ttu-id="eddc4-189">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-189">02</span></span>        | <span data-ttu-id="eddc4-190">08</span><span class="sxs-lookup"><span data-stu-id="eddc4-190">08</span></span>  | <span data-ttu-id="eddc4-191">80</span><span class="sxs-lookup"><span data-stu-id="eddc4-191">80</span></span>   | <span data-ttu-id="eddc4-192">MANTıKSAL BIRIM ILETIŞIM TAŞMASı</span><span class="sxs-lookup"><span data-stu-id="eddc4-192">LOGICAL UNIT COMMUNICATION OVERRUN</span></span>                |
| <span data-ttu-id="eddc4-193">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-193">02</span></span>        | <span data-ttu-id="eddc4-194">3A</span><span class="sxs-lookup"><span data-stu-id="eddc4-194">3A</span></span>  | <span data-ttu-id="eddc4-195">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-195">00</span></span>   | <span data-ttu-id="eddc4-196">ORTA YOK</span><span class="sxs-lookup"><span data-stu-id="eddc4-196">MEDIUM NOT PRESENT</span></span>                                |
| <span data-ttu-id="eddc4-197">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-197">02</span></span>        | <span data-ttu-id="eddc4-198">54</span><span class="sxs-lookup"><span data-stu-id="eddc4-198">54</span></span>  | <span data-ttu-id="eddc4-199">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-199">00</span></span>   | <span data-ttu-id="eddc4-200">USB 'DEN KONAĞA SISTEM ARABIRIMI HATASı</span><span class="sxs-lookup"><span data-stu-id="eddc4-200">USB TO HOST SYSTEM INTERFACE FAILURE</span></span>              |
| <span data-ttu-id="eddc4-201">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-201">02</span></span>        | <span data-ttu-id="eddc4-202">80</span><span class="sxs-lookup"><span data-stu-id="eddc4-202">80</span></span>  | <span data-ttu-id="eddc4-203">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-203">00</span></span>   | <span data-ttu-id="eddc4-204">YETERSIZ KAYNAK</span><span class="sxs-lookup"><span data-stu-id="eddc4-204">INSUFFICIENT RESOURCES</span></span>                            |
| <span data-ttu-id="eddc4-205">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-205">02</span></span>        | <span data-ttu-id="eddc4-206">BENZERI</span><span class="sxs-lookup"><span data-stu-id="eddc4-206">FF</span></span>  | <span data-ttu-id="eddc4-207">BENZERI</span><span class="sxs-lookup"><span data-stu-id="eddc4-207">FF</span></span>   | <span data-ttu-id="eddc4-208">BILINMEYEN HATA</span><span class="sxs-lookup"><span data-stu-id="eddc4-208">UNKNOWN ERROR</span></span>                                     |
| <span data-ttu-id="eddc4-209">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-209">03</span></span>        | <span data-ttu-id="eddc4-210">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-210">02</span></span>  | <span data-ttu-id="eddc4-211">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-211">00</span></span>   | <span data-ttu-id="eddc4-212">ARAMA TAMAM</span><span class="sxs-lookup"><span data-stu-id="eddc4-212">NO SEEK COMPLETE</span></span>                                  |
| <span data-ttu-id="eddc4-213">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-213">03</span></span>        | <span data-ttu-id="eddc4-214">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-214">03</span></span>  | <span data-ttu-id="eddc4-215">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-215">00</span></span>   | <span data-ttu-id="eddc4-216">YAZMA HATASı</span><span class="sxs-lookup"><span data-stu-id="eddc4-216">WRITE FAULT</span></span>                                       |
| <span data-ttu-id="eddc4-217">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-217">03</span></span>        | <span data-ttu-id="eddc4-218">10</span><span class="sxs-lookup"><span data-stu-id="eddc4-218">10</span></span>  | <span data-ttu-id="eddc4-219">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-219">00</span></span>   | <span data-ttu-id="eddc4-220">KIMLIK CRC HATASı</span><span class="sxs-lookup"><span data-stu-id="eddc4-220">ID CRC ERROR</span></span>                                      |
| <span data-ttu-id="eddc4-221">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-221">03</span></span>        | <span data-ttu-id="eddc4-222">11</span><span class="sxs-lookup"><span data-stu-id="eddc4-222">11</span></span>  | <span data-ttu-id="eddc4-223">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-223">00</span></span>   | <span data-ttu-id="eddc4-224">KURTARıLAN OKUMA HATASı</span><span class="sxs-lookup"><span data-stu-id="eddc4-224">UNRECOVERED READ ERROR</span></span>                            |
| <span data-ttu-id="eddc4-225">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-225">03</span></span>        | <span data-ttu-id="eddc4-226">12</span><span class="sxs-lookup"><span data-stu-id="eddc4-226">12</span></span>  | <span data-ttu-id="eddc4-227">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-227">00</span></span>   | <span data-ttu-id="eddc4-228">KIMLIK ALANı IÇIN ADRES IŞARETI BULUNAMADı</span><span class="sxs-lookup"><span data-stu-id="eddc4-228">ADDRESS MARK NOT FOUND FOR ID FIELD</span></span>               |
| <span data-ttu-id="eddc4-229">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-229">03</span></span>        | <span data-ttu-id="eddc4-230">13</span><span class="sxs-lookup"><span data-stu-id="eddc4-230">13</span></span>  | <span data-ttu-id="eddc4-231">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-231">00</span></span>   | <span data-ttu-id="eddc4-232">VERI ALANı IÇIN ADRES IŞARETI BULUNAMADı</span><span class="sxs-lookup"><span data-stu-id="eddc4-232">ADDRESS MARK NOT FOUND FOR DATA FIELD</span></span>             |
| <span data-ttu-id="eddc4-233">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-233">03</span></span>        | <span data-ttu-id="eddc4-234">14</span><span class="sxs-lookup"><span data-stu-id="eddc4-234">14</span></span>  | <span data-ttu-id="eddc4-235">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-235">00</span></span>   | <span data-ttu-id="eddc4-236">KAYDEDILEN VARLıK BULUNAMADı</span><span class="sxs-lookup"><span data-stu-id="eddc4-236">RECORDED ENTITY NOT FOUND</span></span>                         |
| <span data-ttu-id="eddc4-237">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-237">03</span></span>        | <span data-ttu-id="eddc4-238">30</span><span class="sxs-lookup"><span data-stu-id="eddc4-238">30</span></span>  | <span data-ttu-id="eddc4-239">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-239">01</span></span>   | <span data-ttu-id="eddc4-240">ORTA BILINMEYEN BIÇIM OKUNAMıYOR</span><span class="sxs-lookup"><span data-stu-id="eddc4-240">CANNOT READ MEDIUM - UNKNOWN FORMAT</span></span>               |
| <span data-ttu-id="eddc4-241">03</span><span class="sxs-lookup"><span data-stu-id="eddc4-241">03</span></span>        | <span data-ttu-id="eddc4-242">31</span><span class="sxs-lookup"><span data-stu-id="eddc4-242">31</span></span>  | <span data-ttu-id="eddc4-243">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-243">01</span></span>   | <span data-ttu-id="eddc4-244">BIÇIMLENDIRME KOMUTU BAŞARıSıZ</span><span class="sxs-lookup"><span data-stu-id="eddc4-244">FORMAT COMMAND FAILED</span></span>                             |
| <span data-ttu-id="eddc4-245">04</span><span class="sxs-lookup"><span data-stu-id="eddc4-245">04</span></span>        | <span data-ttu-id="eddc4-246">40</span><span class="sxs-lookup"><span data-stu-id="eddc4-246">40</span></span>  | <span data-ttu-id="eddc4-247">NN</span><span class="sxs-lookup"><span data-stu-id="eddc4-247">NN</span></span>   | <span data-ttu-id="eddc4-248">NN BILEŞENINDE TANıLAMA HATASı (80H-FFH)</span><span class="sxs-lookup"><span data-stu-id="eddc4-248">DIAGNOSTIC FAILURE ON COMPONENT NN (80H-FFH)</span></span>      |
| <span data-ttu-id="eddc4-249">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-249">05</span></span>        | <span data-ttu-id="eddc4-250">1A</span><span class="sxs-lookup"><span data-stu-id="eddc4-250">1A</span></span>  | <span data-ttu-id="eddc4-251">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-251">00</span></span>   | <span data-ttu-id="eddc4-252">PARAMETRE LISTESI UZUNLUĞU HATASı</span><span class="sxs-lookup"><span data-stu-id="eddc4-252">PARAMETER LIST LENGTH ERROR</span></span>                       |
| <span data-ttu-id="eddc4-253">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-253">05</span></span>        | <span data-ttu-id="eddc4-254">20</span><span class="sxs-lookup"><span data-stu-id="eddc4-254">20</span></span>  | <span data-ttu-id="eddc4-255">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-255">00</span></span>   | <span data-ttu-id="eddc4-256">GEÇERSIZ KOMUT IŞLEMI KODU</span><span class="sxs-lookup"><span data-stu-id="eddc4-256">INVALID COMMAND OPERATION CODE</span></span>                    |
| <span data-ttu-id="eddc4-257">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-257">05</span></span>        | <span data-ttu-id="eddc4-258">21</span><span class="sxs-lookup"><span data-stu-id="eddc4-258">21</span></span>  | <span data-ttu-id="eddc4-259">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-259">00</span></span>   | <span data-ttu-id="eddc4-260">MANTıKSAL BLOK ADRESI ARALıK DıŞıNDA</span><span class="sxs-lookup"><span data-stu-id="eddc4-260">LOGICAL BLOCK ADDRESS OUT OF RANGE</span></span>                |
| <span data-ttu-id="eddc4-261">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-261">05</span></span>        | <span data-ttu-id="eddc4-262">24</span><span class="sxs-lookup"><span data-stu-id="eddc4-262">24</span></span>  | <span data-ttu-id="eddc4-263">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-263">00</span></span>   | <span data-ttu-id="eddc4-264">KOMUT PAKETINDE GEÇERSIZ ALAN</span><span class="sxs-lookup"><span data-stu-id="eddc4-264">INVALID FIELD IN COMMAND PACKET</span></span>                   |
| <span data-ttu-id="eddc4-265">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-265">05</span></span>        | <span data-ttu-id="eddc4-266">25</span><span class="sxs-lookup"><span data-stu-id="eddc4-266">25</span></span>  | <span data-ttu-id="eddc4-267">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-267">00</span></span>   | <span data-ttu-id="eddc4-268">MANTıKSAL BIRIM DESTEKLENMIYOR</span><span class="sxs-lookup"><span data-stu-id="eddc4-268">LOGICAL UNIT NOT SUPPORTED</span></span>                        |
| <span data-ttu-id="eddc4-269">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-269">05</span></span>        | <span data-ttu-id="eddc4-270">26</span><span class="sxs-lookup"><span data-stu-id="eddc4-270">26</span></span>  | <span data-ttu-id="eddc4-271">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-271">00</span></span>   | <span data-ttu-id="eddc4-272">PARAMETRE LISTESINDE GEÇERSIZ ALAN</span><span class="sxs-lookup"><span data-stu-id="eddc4-272">INVALID FIELD IN PARAMETER LIST</span></span>                   |
| <span data-ttu-id="eddc4-273">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-273">05</span></span>        | <span data-ttu-id="eddc4-274">26</span><span class="sxs-lookup"><span data-stu-id="eddc4-274">26</span></span>  | <span data-ttu-id="eddc4-275">01</span><span class="sxs-lookup"><span data-stu-id="eddc4-275">01</span></span>   | <span data-ttu-id="eddc4-276">PARAMETRE DESTEKLENMIYOR</span><span class="sxs-lookup"><span data-stu-id="eddc4-276">PARAMETER NOT SUPPORTED</span></span>                           |
| <span data-ttu-id="eddc4-277">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-277">05</span></span>        | <span data-ttu-id="eddc4-278">26</span><span class="sxs-lookup"><span data-stu-id="eddc4-278">26</span></span>  | <span data-ttu-id="eddc4-279">02</span><span class="sxs-lookup"><span data-stu-id="eddc4-279">02</span></span>   | <span data-ttu-id="eddc4-280">PARAMETRE DEĞERI GEÇERSIZ</span><span class="sxs-lookup"><span data-stu-id="eddc4-280">PARAMETER VALUE INVALID</span></span>                           |
| <span data-ttu-id="eddc4-281">05</span><span class="sxs-lookup"><span data-stu-id="eddc4-281">05</span></span>        | <span data-ttu-id="eddc4-282">39</span><span class="sxs-lookup"><span data-stu-id="eddc4-282">39</span></span>  | <span data-ttu-id="eddc4-283">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-283">00</span></span>   | <span data-ttu-id="eddc4-284">PARAMETRELERI KAYDETME DESTEĞI YOK</span><span class="sxs-lookup"><span data-stu-id="eddc4-284">SAVING PARAMETERS NOT SUPPORT</span></span>                     |
| <span data-ttu-id="eddc4-285">06</span><span class="sxs-lookup"><span data-stu-id="eddc4-285">06</span></span>        | <span data-ttu-id="eddc4-286">28</span><span class="sxs-lookup"><span data-stu-id="eddc4-286">28</span></span>  | <span data-ttu-id="eddc4-287">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-287">00</span></span>   | <span data-ttu-id="eddc4-288">BAŞLAMAYA HAZıRLANMA – MEDYA DEĞIŞTIRILDI</span><span class="sxs-lookup"><span data-stu-id="eddc4-288">NOT READY TO READY TRANSITION – MEDIA CHANGED</span></span>     |
| <span data-ttu-id="eddc4-289">06</span><span class="sxs-lookup"><span data-stu-id="eddc4-289">06</span></span>        | <span data-ttu-id="eddc4-290">29</span><span class="sxs-lookup"><span data-stu-id="eddc4-290">29</span></span>  | <span data-ttu-id="eddc4-291">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-291">00</span></span>   | <span data-ttu-id="eddc4-292">SıFıRLAMA VEYA VERI YOLU CIHAZıNı SıFıRLAMA SıRASıNDA GÜÇ GERÇEKLEŞTI</span><span class="sxs-lookup"><span data-stu-id="eddc4-292">POWER ON RESET OR BUS DEVICE RESET OCCURRED</span></span>       |
| <span data-ttu-id="eddc4-293">06</span><span class="sxs-lookup"><span data-stu-id="eddc4-293">06</span></span>        | <span data-ttu-id="eddc4-294">2F</span><span class="sxs-lookup"><span data-stu-id="eddc4-294">2F</span></span>  | <span data-ttu-id="eddc4-295">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-295">00</span></span>   | <span data-ttu-id="eddc4-296">BAŞKA BIR BAŞLATıCı TARAFıNDAN TEMIZLENMIŞ KOMUTLAR</span><span class="sxs-lookup"><span data-stu-id="eddc4-296">COMMANDS CLEARED BY ANOTHER INITIATOR</span></span>             |
| <span data-ttu-id="eddc4-297">07</span><span class="sxs-lookup"><span data-stu-id="eddc4-297">07</span></span>        | <span data-ttu-id="eddc4-298">27</span><span class="sxs-lookup"><span data-stu-id="eddc4-298">27</span></span>  | <span data-ttu-id="eddc4-299">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-299">00</span></span>   | <span data-ttu-id="eddc4-300">KORUMALı MEDYA YAZMA</span><span class="sxs-lookup"><span data-stu-id="eddc4-300">WRITE PROTECTED MEDIA</span></span>                             |
| <span data-ttu-id="eddc4-301">0B</span><span class="sxs-lookup"><span data-stu-id="eddc4-301">0B</span></span>        | <span data-ttu-id="eddc4-302">4E</span><span class="sxs-lookup"><span data-stu-id="eddc4-302">4E</span></span>  | <span data-ttu-id="eddc4-303">00</span><span class="sxs-lookup"><span data-stu-id="eddc4-303">00</span></span>   | <span data-ttu-id="eddc4-304">ÇAKıŞAN KOMUT DENENDI</span><span class="sxs-lookup"><span data-stu-id="eddc4-304">OVERLAPPED COMMAND ATTEMPTED</span></span>                      |

<span data-ttu-id="eddc4-305">Uygulamanın uygulayamayacağı iki ek, isteğe bağlı geri çağırma vardır; biri **GET_STATUS_NOTIFICATION** komutuna yanıt vermek ve diğeri **SYNCHRONIZE_CACHE** komutuna yanıt vermek içindir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-305">There are two additional, optional callbacks the application may implement; one is for responding to a **GET_STATUS_NOTIFICATION** command and the other is for responding to the **SYNCHRONIZE_CACHE** command.</span></span>

<span data-ttu-id="eddc4-306">Uygulama konaktan GET_STATUS_NOTIFICATION komutu işlemek istiyorsanız, aşağıdaki prototiple bir geri çağırma uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-306">If the application would like to handle the GET_STATUS_NOTIFICATION command from the host, it should implement a callback with the following prototype.</span></span>

```c
UINT ux_slave_class_storage_media_notification( 
    VOID *storage,  
    ULONG lun,
    ULONG media_id,  
    ULONG notification_class,
    UCHAR **media_notification,  
    ULONG *media_notification_length);
```

<span data-ttu-id="eddc4-307">Konum:</span><span class="sxs-lookup"><span data-stu-id="eddc4-307">Where:</span></span>

- <span data-ttu-id="eddc4-308">*depolama* , depolama sınıfının örneğidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-308">*storage* is the instance of the storage class.</span></span>
- <span data-ttu-id="eddc4-309">*media_id* Şu anda kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="eddc4-309">*media_id* is not currently used.</span></span> <span data-ttu-id="eddc4-310">notification_class bildirim sınıfını belirtir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-310">notification_class specifies the class of notification.</span></span>
- <span data-ttu-id="eddc4-311">*media_notification* , uygulama tarafından bildirimin yanıtını içeren arabelleğe ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-311">*media_notification* should be set by the application to the buffer containing the response for the notification.</span></span>
- <span data-ttu-id="eddc4-312">*media_notification_length* , yanıt arabelleğinin uzunluğunu içermesi için uygulama tarafından ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-312">*media_notification_length* should be set by the application to contain the length of the response buffer.</span></span>

<span data-ttu-id="eddc4-313">Dönüş değeri, komutun başarılı olup olmadığını gösterir – **UX_SUCCESS** veya **UX_ERROR** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-313">The return value indicates whether or not the command succeeded – should be either **UX_SUCCESS** or **UX_ERROR**.</span></span>

<span data-ttu-id="eddc4-314">Uygulama bu geri aramayı uygulamadıklarında, **GET_STATUS_NOTIFICATION** komutu alındıktan sonra, USBX ana bilgisayara komutun uygulanmadığından haberdar olur.</span><span class="sxs-lookup"><span data-stu-id="eddc4-314">If the application does not implement this callback, then upon receiving the **GET_STATUS_NOTIFICATION** command, USBX will notify the host that the command is not implemented.</span></span>

<span data-ttu-id="eddc4-315">Uygulama konaktan yazma işlemleri için bir önbellek kullanıyorsa, **SYNCHRONIZE_CACHE** komutu işlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-315">The **SYNCHRONIZE_CACHE** command should be handled if the application is utilizing a cache for writes from the host.</span></span> <span data-ttu-id="eddc4-316">Depolama cihazının bağlantısının kesilmek üzere olduğunu biliyorsa, bir ana bilgisayar bu komutu gönderebilir. Örneğin, Windows 'ta, araç çubuğunda bir flash sürücü simgesine sağ tıklayıp " \[ depolama cihazı adını çıkar" seçeneğini belirlerseniz \] , Windows bu cihazda **SYNCHRONIZE_CACHE** komutunu ister.</span><span class="sxs-lookup"><span data-stu-id="eddc4-316">A host may send this command if it knows the storage device is about to be disconnected, for example, in Windows, if you right click a flash drive icon in the toolbar and select "Eject \[storage device name\]", Windows will issue the **SYNCHRONIZE_CACHE** command to that device.</span></span>

<span data-ttu-id="eddc4-317">Uygulama konaktan **GET_STATUS_NOTIFICATION** komutu işlemek istiyorsanız, aşağıdaki prototiple bir geri çağırma uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-317">If the application would like to handle the **GET_STATUS_NOTIFICATION** command from the host, it should implement a callback with the following prototype.</span></span>

```c
UINT ux_slave_class_storage_media_flush(
    VOID *storage, 
    ULONG lun,
    ULONG number_blocks, 
    ULONG lba, 
    ULONG *media_status);
```

<span data-ttu-id="eddc4-318">Konum:</span><span class="sxs-lookup"><span data-stu-id="eddc4-318">Where:</span></span>

- <span data-ttu-id="eddc4-319">*depolama* , depolama sınıfının örneğidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-319">*storage* is the instance of the storage class.</span></span>
- <span data-ttu-id="eddc4-320">*LUN* parametresi, komutun yönlendirildiği LUN 'u belirtir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-320">*lun* parameter specifies which LUN the command is directed to.</span></span>
- <span data-ttu-id="eddc4-321">*number_blocks* eşitleyeceğiniz blokların sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-321">*number_blocks* specifies the number of blocks to synchronize.</span></span>
- <span data-ttu-id="eddc4-322">*LBA* , eşitlenmesi yapılacak ilk bloğun kesim adresidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-322">*lba* is the sector address of the first block to synchronize.</span></span>
- <span data-ttu-id="eddc4-323">*media_status* , tam olarak medya durumu geri çağırma dönüş değeri gibi doldurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-323">*media_status* should be filled out exactly like the media status callback return value.</span></span>

<span data-ttu-id="eddc4-324">Dönüş değeri, komutun başarılı olup olmadığını gösterir – **UX_SUCCESS** veya **UX_ERROR** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-324">The return value indicates whether or not the command succeeded – should be either **UX_SUCCESS** or **UX_ERROR**.</span></span>

### <a name="multiple-scsi-lun"></a><span data-ttu-id="eddc4-325">Birden çok SCSI LUN</span><span class="sxs-lookup"><span data-stu-id="eddc4-325">Multiple SCSI LUN</span></span>

<span data-ttu-id="eddc4-326">USBX cihaz depolama sınıfı birden çok LUN 'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="eddc4-326">The USBX device storage class supports multiple LUNs.</span></span> <span data-ttu-id="eddc4-327">Bu nedenle, aynı anda bir CD-ROM ve flash disk görevi gören bir depolama cihazı oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="eddc4-327">It is therefore possible to create a storage device that acts as a CD-ROM and a Flash disk at the same time.</span></span> <span data-ttu-id="eddc4-328">Böyle bir durumda, başlatma biraz farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-328">In such a case, the initialization would be slightly different.</span></span> <span data-ttu-id="eddc4-329">Flash disk ve CD-ROM için bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="eddc4-329">Here is an example for a Flash Disk and CD-ROM:</span></span>

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

## <a name="usb-device-cdc-acm-class"></a><span data-ttu-id="eddc4-330">USB cihazı CDC-ACM sınıfı</span><span class="sxs-lookup"><span data-stu-id="eddc4-330">USB Device CDC-ACM Class</span></span>

<span data-ttu-id="eddc4-331">USB aygıtı CDC-ACM sınıfı, USB konak sisteminin cihazla bir seri cihaz olarak iletişim kurmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-331">The USB device CDC-ACM class allows for a USB host system to communicate with the device as a serial device.</span></span> <span data-ttu-id="eddc4-332">Bu sınıf, USB standardını temel alır ve CDC standardının bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-332">This class is based on the USB standard and is a subset of the CDC standard.</span></span>

<span data-ttu-id="eddc4-333">CDC-ACM uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildirilmesine ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-333">A CDC-ACM compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="eddc4-334">Aşağıda aşağıda bir örnek bulunur.</span><span class="sxs-lookup"><span data-stu-id="eddc4-334">An example is found here below.</span></span>

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

<span data-ttu-id="eddc4-335">CDC-ACM sınıfı, arabirimleri gruplamak için bir bileşik cihaz çerçevesi kullanır (denetim ve veri).</span><span class="sxs-lookup"><span data-stu-id="eddc4-335">The CDC-ACM class uses a composite device framework to group interfaces (control and data).</span></span> <span data-ttu-id="eddc4-336">Bir sonuç olarak, cihaz tanımlayıcısı tanımlanırken alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-336">As a result care should be taken when defining the device descriptor.</span></span> <span data-ttu-id="eddc4-337">USBX, dahili olarak arabirimlerin nasıl bağlanacağını öğrenmek için ıAD tanımlayıcısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-337">USBX relies on the IAD descriptor to know internally how to bind interfaces.</span></span> <span data-ttu-id="eddc4-338">IAD tanımlayıcısı arabirimlerden önce bildirilmelidir ve CDC-ACM sınıfının ilk arabirimini ve kaç arabirimin iliştirildiğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-338">The IAD descriptor should be declared before the interfaces and contain the first interface of the CDC-ACM class and how many interfaces are attached.</span></span>

<span data-ttu-id="eddc4-339">CDC-ACM sınıfı ayrıca, daha yeni ıAD tanımlayıcısı ile aynı işlevi gerçekleştiren bir bileşim işlev tanımlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-339">The CDC-ACM class also uses a union functional descriptor which performs the same function as the newer IAD descriptor.</span></span> <span data-ttu-id="eddc4-340">Bir birleşim Işlevsel tanımlayıcısının geçmiş nedenlerle bildirilmesini ve konak tarafında uyumluluğu olması gerekse de, bu, USBX tarafından kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="eddc4-340">Although a Union Functional descriptor must be declared for historical reasons and compatibility with the host side, it is not used by USBX.</span></span>

<span data-ttu-id="eddc4-341">CDC-ACM sınıfının başlatılması aşağıdaki parametreleri bekler.</span><span class="sxs-lookup"><span data-stu-id="eddc4-341">The initialization of the CDC-ACM class expects the following parameters.</span></span>

```c
/* Set the parameters for callback when insertion/extraction of a CDC device. */

parameter.ux_slave_class_cdc_acm_instance_activate = tx_demo_cdc_instance_activate;

parameter.ux_slave_class_cdc_acm_instance_deactivate = tx_demo_cdc_instance_deactivate;

parameter.ux_slave_class_cdc_acm_parameter_change = tx_demo_cdc_instance_parameter_change;

/* Initialize the device cdc class. This class owns both interfaces starting with 0. */
status = ux_device_stack_class_register(_ux_system_slave_class_cdc_acm_name,ux_device_class_cdc_acm_entry,
    1,0, &parameter);
```

<span data-ttu-id="eddc4-342">Tanımlanan 2 parametresi, yığın bu sınıfı etkinleştirdiğinde veya devre dışı bırakıldığında çağrılacak Kullanıcı uygulamalarına geri çağırma işaretçileridir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-342">The 2 parameters defined are callback pointers into the user applications that will be called when the stack activates or deactivate this class.</span></span>

<span data-ttu-id="eddc4-343">Tanımlı üçüncü parametre, satır kodlama veya satır durumları parametre değişikliği olduğunda çağrılacak Kullanıcı uygulamasına yönelik bir geri çağırma işaretçisidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-343">The third parameter defined is a callback pointer to the user application that will be called when there is line coding or line states parameter change.</span></span> <span data-ttu-id="eddc4-344">Örneğin, konaktan DTR durumunu **true** olarak değiştirmek için bir istek olduğunda, geri çağırma çağrılır, BT Kullanıcı uygulamasında, bir Işlev için IOCTL işlevi aracılığıyla satır durumlarını kontrol edebilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-344">E.g., when there is request from host to change DTR state to **TRUE**, the callback is invoked, in it user application can check line states through IOCTL function to kow host is ready for communication.</span></span>

<span data-ttu-id="eddc4-345">CDC-ACM, bir USB-IF standardını temel alır ve MACOs ve Linux işletim sistemleri tarafından otomatik olarak tanınır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-345">The CDC-ACM is based on a USB-IF standard and is automatically recognized by MACOs and Linux operating systems.</span></span> <span data-ttu-id="eddc4-346">Windows platformlarında, bu sınıf 10 ' dan önceki Windows sürümü için bir. inf dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-346">On Windows platforms, this class requires a .inf file for Windows version prior to 10.</span></span> <span data-ttu-id="eddc4-347">Windows 10 ' da herhangi bir. inf dosyası gerekmez.</span><span class="sxs-lookup"><span data-stu-id="eddc4-347">Windows 10 does not require any .inf files.</span></span> <span data-ttu-id="eddc4-348">CDC-ACM sınıfı için bir şablon sağlamamız ve ***usbx_windows_host_files*** dizininde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-348">We supply a template for the CDC-ACM class and it can be found in the ***usbx_windows_host_files*** directory.</span></span> <span data-ttu-id="eddc4-349">Windows 'un daha yeni sürümü için CDC_ACM_Template_Win7_64bit. inf dosyası kullanılmalıdır (win10 dışında).</span><span class="sxs-lookup"><span data-stu-id="eddc4-349">For more recent version of Windows the file CDC_ACM_Template_Win7_64bit.inf should be used (except Win10).</span></span> <span data-ttu-id="eddc4-350">Bu dosyanın, cihaz tarafından kullanılan PID/VıD 'yi yansıtacak şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-350">This file needs to be modified to reflect the PID/VID used by the device.</span></span> <span data-ttu-id="eddc4-351">Şirket ve ürün USB-IF ile kaydettirilirse, PID/VıD son müşteriye özgü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-351">The PID/VID will be specific to the final customer when the company and the product are registered with the USB-IF.</span></span> <span data-ttu-id="eddc4-352">INF dosyasında, değiştirilecek alanlar burada bulunur.</span><span class="sxs-lookup"><span data-stu-id="eddc4-352">In the inf file, the fields to modify are located here.</span></span>

```INF
[DeviceList]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000

[DeviceList.NTamd64]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000
```

<span data-ttu-id="eddc4-353">CDC-ACM cihazının cihaz çerçevesinde, PID/VıD cihaz tanımlayıcısına depolanır (yukarıda belirtilen cihaz tanımlayıcısına bakın).</span><span class="sxs-lookup"><span data-stu-id="eddc4-353">In the device framework of the CDC-ACM device, the PID/VID are stored in the device descriptor (see the device descriptor declared above).</span></span>

<span data-ttu-id="eddc4-354">USB ana bilgisayar sistemleri, USB CDC-ACM cihazını bulduğunda, bir seri sınıf bağlayacaktır ve cihaz herhangi bir seri Terminal programıyla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-354">When a USB host systems discovers the USB CDC-ACM device, it will mount a serial class and the device can be used with any serial terminal program.</span></span> <span data-ttu-id="eddc4-355">Başvuru için konak Işletim sistemine bakın.</span><span class="sxs-lookup"><span data-stu-id="eddc4-355">See the host Operating System for reference.</span></span>

<span data-ttu-id="eddc4-356">CDC-ACM sınıfı API işlevleri aşağıda tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-356">The CDC-ACM class API functions are defined below.</span></span>

### <a name="ux_device_class_cdc_acm_ioctl"></a><span data-ttu-id="eddc4-357">ux_device_class_cdc_acm_ioctl</span><span class="sxs-lookup"><span data-stu-id="eddc4-357">ux_device_class_cdc_acm_ioctl</span></span>

<span data-ttu-id="eddc4-358">CDC-ACM arabiriminde ıOCTL gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="eddc4-358">Perform IOCTL on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-359">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-359">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm, 
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-360">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-360">Description</span></span>

<span data-ttu-id="eddc4-361">Bu işlev, bir uygulamanın CDC ACM arabirimine çeşitli IOCTL çağrıları gerçekleştirmesi gerektiğinde çağrılır</span><span class="sxs-lookup"><span data-stu-id="eddc4-361">This function is called when an application needs to perform various ioctl calls to the cdc acm interface</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-362">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-362">Parameters</span></span>

- <span data-ttu-id="eddc4-363">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-363">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-364">**ioctl_function**: gerçekleştirilecek IOCTL işlevi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-364">**ioctl_function**: Ioctl function to be performed.</span></span>
- <span data-ttu-id="eddc4-365">**Parameter**: IOCTL çağrısına özgü bir parametreye yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-365">**parameter**: Pointer to a parameter specific to the ioctl call.</span></span>

### <a name="return-value"></a><span data-ttu-id="eddc4-366">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-366">Return Value</span></span>

- <span data-ttu-id="eddc4-367">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-367">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-368">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="eddc4-368">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-369">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-369">Example</span></span>

```c
/* Start cdc acm callback transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START, &callback);

if(status != UX_SUCCESS)
    return;
```

### <a name="ioctl-functions"></a><span data-ttu-id="eddc4-370">IOCTL işlevleri:</span><span class="sxs-lookup"><span data-stu-id="eddc4-370">Ioctl functions:</span></span>

| <span data-ttu-id="eddc4-371">İşlev</span><span class="sxs-lookup"><span data-stu-id="eddc4-371">Function</span></span>                                        | <span data-ttu-id="eddc4-372">Değer</span><span class="sxs-lookup"><span data-stu-id="eddc4-372">Value</span></span> |
| ----------------------------------------------- | - |
| <span data-ttu-id="eddc4-373">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="eddc4-373">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>    | <span data-ttu-id="eddc4-374">1</span><span class="sxs-lookup"><span data-stu-id="eddc4-374">1</span></span> |
| <span data-ttu-id="eddc4-375">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="eddc4-375">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span></span>    | <span data-ttu-id="eddc4-376">2</span><span class="sxs-lookup"><span data-stu-id="eddc4-376">2</span></span> |
| <span data-ttu-id="eddc4-377">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="eddc4-377">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span></span>     | <span data-ttu-id="eddc4-378">3</span><span class="sxs-lookup"><span data-stu-id="eddc4-378">3</span></span> |
| <span data-ttu-id="eddc4-379">UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span><span class="sxs-lookup"><span data-stu-id="eddc4-379">UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span></span>         | <span data-ttu-id="eddc4-380">4</span><span class="sxs-lookup"><span data-stu-id="eddc4-380">4</span></span> |
| <span data-ttu-id="eddc4-381">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="eddc4-381">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>     | <span data-ttu-id="eddc4-382">5</span><span class="sxs-lookup"><span data-stu-id="eddc4-382">5</span></span> |
| <span data-ttu-id="eddc4-383">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span><span class="sxs-lookup"><span data-stu-id="eddc4-383">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span></span> | <span data-ttu-id="eddc4-384">6</span><span class="sxs-lookup"><span data-stu-id="eddc4-384">6</span></span> |
| <span data-ttu-id="eddc4-385">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span><span class="sxs-lookup"><span data-stu-id="eddc4-385">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span></span>  | <span data-ttu-id="eddc4-386">7</span><span class="sxs-lookup"><span data-stu-id="eddc4-386">7</span></span> |

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_coding"></a><span data-ttu-id="eddc4-387">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="eddc4-387">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>

<span data-ttu-id="eddc4-388">CDC-ACM arabiriminde ıOCTL kümesi satırı kodlaması gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="eddc4-388">Perform IOCTL Set Line Coding on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-389">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-389">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-390">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-390">Description</span></span>

<span data-ttu-id="eddc4-391">Bu işlev, bir uygulamanın satır kodlama parametrelerini ayarlaması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-391">This function is called when an application needs to Set the Line Coding parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-392">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-392">Parameters</span></span>

- <span data-ttu-id="eddc4-393">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-393">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-394">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="eddc4-394">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>
- <span data-ttu-id="eddc4-395">**Parameter**: bir satır parametre yapısına yönelik işaretçi:</span><span class="sxs-lookup"><span data-stu-id="eddc4-395">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="eddc4-396">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-396">Return Value</span></span>

<span data-ttu-id="eddc4-397">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-397">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-398">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-398">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_coding"></a><span data-ttu-id="eddc4-399">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="eddc4-399">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span></span>

<span data-ttu-id="eddc4-400">CDC-ACM arabiriminde ıOCTL Get satırı kodlaması gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="eddc4-400">Perform IOCTL Get Line Coding on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-401">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-401">Prototype</span></span>

```c
device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-402">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-402">Description</span></span>

<span data-ttu-id="eddc4-403">Bu işlev, bir uygulamanın satır kodlama parametrelerini alması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-403">This function is called when an application needs to Get the Line Coding parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-404">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-404">Parameters</span></span>

- <span data-ttu-id="eddc4-405">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-405">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-406">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_ LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="eddc4-406">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_ LINE_CODING</span></span>
- <span data-ttu-id="eddc4-407">**Parameter**: bir satır parametre yapısına yönelik işaretçi:</span><span class="sxs-lookup"><span data-stu-id="eddc4-407">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="eddc4-408">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-408">Return Value</span></span>

- <span data-ttu-id="eddc4-409">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-409">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-410">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-410">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_state"></a><span data-ttu-id="eddc4-411">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="eddc4-411">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span></span>

<span data-ttu-id="eddc4-412">CDC-ACM arabiriminde ıOCTL al satır durumu gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="eddc4-412">Perform IOCTL Get Line State on the CDC-ACM interface</span></span>

## <a name="prototype"></a><span data-ttu-id="eddc4-413">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-413">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-414">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-414">Description</span></span>

<span data-ttu-id="eddc4-415">Bu işlev, bir uygulamanın satır durumu parametrelerini alması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-415">This function is called when an application needs to Get the Line State parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-416">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-416">Parameters</span></span>

- <span data-ttu-id="eddc4-417">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-417">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-418">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="eddc4-418">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span></span>
- <span data-ttu-id="eddc4-419">**Parameter**: bir satır parametre yapısına yönelik işaretçi:</span><span class="sxs-lookup"><span data-stu-id="eddc4-419">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="eddc4-420">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-420">Return Value</span></span>

- <span data-ttu-id="eddc4-421">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-421">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-422">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-422">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_state"></a><span data-ttu-id="eddc4-423">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="eddc4-423">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>

<span data-ttu-id="eddc4-424">CDC-ACM arabiriminde ıOCTL kümesi satırı durumu gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="eddc4-424">Perform IOCTL Set Line State on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-425">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-425">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-426">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-426">Description</span></span>

<span data-ttu-id="eddc4-427">Bu işlev, bir uygulamanın satır durumu parametrelerini alması gerektiğinde çağrılır</span><span class="sxs-lookup"><span data-stu-id="eddc4-427">This function is called when an application needs to Get the Line State parameters</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-428">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-428">Parameters</span></span>

- <span data-ttu-id="eddc4-429">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-429">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-430">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="eddc4-430">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>
- <span data-ttu-id="eddc4-431">**Parameter**: bir satır parametre yapısına yönelik işaretçi:</span><span class="sxs-lookup"><span data-stu-id="eddc4-431">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="eddc4-432">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-432">Return Value</span></span>

- <span data-ttu-id="eddc4-433">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-433">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-434">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-434">Example</span></span>

```c
/* This is to set RTS state. */

line_state.ux_slave_class_cdc_acm_parameter_rts = UX_TRUE;
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE, &line_state);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_abort_pipe"></a><span data-ttu-id="eddc4-435">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span><span class="sxs-lookup"><span data-stu-id="eddc4-435">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span></span>

<span data-ttu-id="eddc4-436">CDC-ACM arabiriminde ıOCTL Iptal kanalı gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="eddc4-436">Perform IOCTL ABORT PIPE on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-437">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-437">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-438">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-438">Description</span></span>

<span data-ttu-id="eddc4-439">Bu işlev, bir uygulamanın bir kanalı iptal etmek gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-439">This function is called when an application needs to abort a pipe.</span></span> <span data-ttu-id="eddc4-440">Örneğin, devam eden bir yazma işlemini durdurmak için UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT parametresi olarak geçirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-440">For example, to abort an ongoing write, UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT should be passed as the parameter.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-441">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-441">Parameters</span></span>

- <span data-ttu-id="eddc4-442">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-442">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-443">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span><span class="sxs-lookup"><span data-stu-id="eddc4-443">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span></span>
- <span data-ttu-id="eddc4-444">**parametre**: kanal yönü:</span><span class="sxs-lookup"><span data-stu-id="eddc4-444">**parameter**: The pipe direction:</span></span>

```c
UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT 1

UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_RCV 2
```

### <a name="return-value"></a><span data-ttu-id="eddc4-445">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-445">Return Value</span></span>

- <span data-ttu-id="eddc4-446">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-446">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-447">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) geçersiz kanal yönü.</span><span class="sxs-lookup"><span data-stu-id="eddc4-447">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Invalid pipe direction.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-448">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-448">Example</span></span>

```c
/* This is to abort the Xmit pipe. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE,
    UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_start"></a><span data-ttu-id="eddc4-449">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span><span class="sxs-lookup"><span data-stu-id="eddc4-449">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span></span>

<span data-ttu-id="eddc4-450">CDC-ACM arabiriminde ıOCTL Iletimi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="eddc4-450">Perform IOCTL Transmission Start on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-451">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-451">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-452">Description</span></span>

<span data-ttu-id="eddc4-453">Bu işlev, bir uygulama geri çağırma ile iletim kullanmak istediğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-453">This function is called when an application wants to use transmission with callback.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-454">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-454">Parameters</span></span>

- <span data-ttu-id="eddc4-455">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-455">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-456">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span><span class="sxs-lookup"><span data-stu-id="eddc4-456">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span></span>
- <span data-ttu-id="eddc4-457">**parametre**: başlangıç iletimi parametre yapısına yönelik işaretçi:</span><span class="sxs-lookup"><span data-stu-id="eddc4-457">**parameter**: Pointer to the Start Transmission parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER_STRUCT
{
    UINT (*ux_device_class_cdc_acm_parameter_write_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, ULONG length);
    UINT (*ux_device_class_cdc_acm_parameter_read_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *data_pointer, ULONG length);
} UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="eddc4-458">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-458">Return Value</span></span>

- <span data-ttu-id="eddc4-459">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-459">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-460">**UX_ERROR** (0xFF) iletimi zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="eddc4-460">**UX_ERROR** (0xFF) Transmission already started.</span></span>
- <span data-ttu-id="eddc4-461">**UX_MEMORY_INSUFFICIENT** (0x12) bir bellek ayırma başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-461">**UX_MEMORY_INSUFFICIENT** (0x12) A memory allocation failed.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-462">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-462">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_stop"></a><span data-ttu-id="eddc4-463">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span><span class="sxs-lookup"><span data-stu-id="eddc4-463">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span></span>

<span data-ttu-id="eddc4-464">CDC-ACM arabiriminde ıOCTL Iletimi gerçekleştirmeyi durdur</span><span class="sxs-lookup"><span data-stu-id="eddc4-464">Perform IOCTL Transmission Stop on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-465">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-465">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="eddc4-466">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-466">Description</span></span>

<span data-ttu-id="eddc4-467">Bu işlev, bir uygulama geri çağırma ile iletim kullanmayı durdurmak istediğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-467">This function is called when an application wants to stop using transmission with callback.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-468">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-468">Parameters</span></span>

- <span data-ttu-id="eddc4-469">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-469">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-470">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSI ON_STOP</span><span class="sxs-lookup"><span data-stu-id="eddc4-470">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSI ON_STOP</span></span>
- <span data-ttu-id="eddc4-471">**parametre**: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="eddc4-471">**parameter**: Not used</span></span>

### <a name="return-value"></a><span data-ttu-id="eddc4-472">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-472">Return Value</span></span>

- <span data-ttu-id="eddc4-473">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-473">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-474">**UX_ERROR** (0xFF) devam eden iletim yok.</span><span class="sxs-lookup"><span data-stu-id="eddc4-474">**UX_ERROR** (0xFF) No ongoing transmission.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-475">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-475">Example</span></span>

```c
/* Program the stop of transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP, UX_NULL);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_read"></a><span data-ttu-id="eddc4-476">ux_device_class_cdc_acm_read</span><span class="sxs-lookup"><span data-stu-id="eddc4-476">ux_device_class_cdc_acm_read</span></span>

<span data-ttu-id="eddc4-477">CDC-ACM kanalından oku</span><span class="sxs-lookup"><span data-stu-id="eddc4-477">Read from CDC-ACM pipe</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-478">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-478">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_read( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="eddc4-479">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-479">Description</span></span>

<span data-ttu-id="eddc4-480">Bu işlev, bir uygulamanın çıkış veri kanalından okuması gerektiğinde çağrılır (cihazdan içinden konaktan).</span><span class="sxs-lookup"><span data-stu-id="eddc4-480">This function is called when an application needs to read from the OUT data pipe (OUT from the host, IN from the device).</span></span> <span data-ttu-id="eddc4-481">Engelliyor.</span><span class="sxs-lookup"><span data-stu-id="eddc4-481">It is blocking.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-482">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-482">Parameters</span></span>

- <span data-ttu-id="eddc4-483">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-483">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-484">**arabellek**: verilerin depolanacağı arabellek adresi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-484">**buffer**: Buffer address where data will be stored.</span></span>
- <span data-ttu-id="eddc4-485">**requested_length**: beklediğimiz maksimum uzunluk.</span><span class="sxs-lookup"><span data-stu-id="eddc4-485">**requested_length**: The maximum length we expect.</span></span>
- <span data-ttu-id="eddc4-486">**actual_length**: arabelleğe döndürülen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="eddc4-486">**actual_length**: The length returned into the buffer.</span></span>

### <a name="return-value"></a><span data-ttu-id="eddc4-487">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-487">Return Value</span></span>

- <span data-ttu-id="eddc4-488">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-488">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-489">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) cihaz artık yapılandırılmış durumda değil.</span><span class="sxs-lookup"><span data-stu-id="eddc4-489">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Device is no longer in the configured state.</span></span>
- <span data-ttu-id="eddc4-490">**UX_TRANSFER_NO_ANSWER** (0x22) cihazdan yanıt yok.</span><span class="sxs-lookup"><span data-stu-id="eddc4-490">**UX_TRANSFER_NO_ANSWER** (0x22) No answer from device.</span></span> <span data-ttu-id="eddc4-491">Aktarım beklenirken cihazın bağlantısı kesilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-491">The device was probably disconnected while the transfer was pending.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-492">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-492">Example</span></span>

```c
/* Read from the CDC class. */

status = ux_device_class_cdc_acm_read(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS) return;
```

### <a name="ux_device_class_cdc_acm_write"></a><span data-ttu-id="eddc4-493">ux_device_class_cdc_acm_write</span><span class="sxs-lookup"><span data-stu-id="eddc4-493">ux_device_class_cdc_acm_write</span></span>

<span data-ttu-id="eddc4-494">CDC-ACM kanalına yazma</span><span class="sxs-lookup"><span data-stu-id="eddc4-494">Write to a CDC-ACM pipe</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-495">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-495">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_write( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="eddc4-496">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-496">Description</span></span>

<span data-ttu-id="eddc4-497">Bu işlev, bir uygulamanın veri kanalına (konaktan, cihazdan) yazması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-497">This function is called when an application needs to write to the IN data pipe (IN from the host, OUT from the device).</span></span> <span data-ttu-id="eddc4-498">Engelliyor.</span><span class="sxs-lookup"><span data-stu-id="eddc4-498">It is blocking.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-499">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-499">Parameters</span></span>

- <span data-ttu-id="eddc4-500">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-500">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-501">**arabellek**: verilerin depolandığı arabellek adresi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-501">**buffer**: Buffer address where data is stored.</span></span>
- <span data-ttu-id="eddc4-502">**requested_length**: yazılacak arabelleğin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-502">**requested_length**: The length of the buffer to write.</span></span>
- <span data-ttu-id="eddc4-503">**actual_length**: yazma gerçekleştirildikten sonra arabelleğe döndürülen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="eddc4-503">**actual_length**: The length returned into the buffer after write is performed.</span></span>

### <a name="return-value"></a><span data-ttu-id="eddc4-504">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-504">Return Value</span></span>
- <span data-ttu-id="eddc4-505">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-505">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-506">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) cihaz artık yapılandırılmış durumda değil.</span><span class="sxs-lookup"><span data-stu-id="eddc4-506">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Device is no longer in the configured state.</span></span>
- <span data-ttu-id="eddc4-507">**UX_TRANSFER_NO_ANSWER** (0x22) cihazdan yanıt yok.</span><span class="sxs-lookup"><span data-stu-id="eddc4-507">**UX_TRANSFER_NO_ANSWER** (0x22) No answer from device.</span></span> <span data-ttu-id="eddc4-508">Aktarım beklenirken cihazın bağlantısı kesilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-508">The device was probably disconnected while the transfer was pending.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-509">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-509">Example</span></span>

```c
/* Write to the CDC class bulk in pipe. */

status = ux_device_class_cdc_acm_write(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS)
    return;
```

### <a name="ux_device_class_cdc_acm_write_with_callback"></a><span data-ttu-id="eddc4-510">ux_device_class_cdc_acm_write_with_callback</span><span class="sxs-lookup"><span data-stu-id="eddc4-510">ux_device_class_cdc_acm_write_with_callback</span></span>

<span data-ttu-id="eddc4-511">Geri çağırma ile CDC-ACM kanalına yazma</span><span class="sxs-lookup"><span data-stu-id="eddc4-511">Writing to a CDC-ACM pipe with callback</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-512">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-512">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_write_with_callback( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length);
```

### <a name="description"></a><span data-ttu-id="eddc4-513">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-513">Description</span></span>

<span data-ttu-id="eddc4-514">Bu işlev, bir uygulamanın veri kanalına (konaktan, cihazdan) yazması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-514">This function is called when an application needs to write to the IN data pipe (IN from the host, OUT from the device).</span></span> <span data-ttu-id="eddc4-515">Bu işlev engellenmeyen ve tamamlanma UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START bir geri çağırma aracılığıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-515">This function is non-blocking and the completion will be done through a callback set in UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-516">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-516">Parameters</span></span>

- <span data-ttu-id="eddc4-517">**cdc_acm**: CDC sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-517">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="eddc4-518">**arabellek**: verilerin depolandığı arabellek adresi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-518">**buffer**: Buffer address where data is stored.</span></span>
- <span data-ttu-id="eddc4-519">**requested_length**: yazılacak arabelleğin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-519">**requested_length**: The length of the buffer to write.</span></span>
- <span data-ttu-id="eddc4-520">**actual_length**: yazma gerçekleştirildikten sonra arabelleğe döndürülen uzunluk</span><span class="sxs-lookup"><span data-stu-id="eddc4-520">**actual_length**: The length returned into the buffer after write is performed</span></span>

### <a name="return-value"></a><span data-ttu-id="eddc4-521">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-521">Return Value</span></span>

- <span data-ttu-id="eddc4-522">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-522">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-523">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) cihaz artık yapılandırılmış durumda değil.</span><span class="sxs-lookup"><span data-stu-id="eddc4-523">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Device is no longer in the configured state.</span></span>
- <span data-ttu-id="eddc4-524">**UX_TRANSFER_NO_ANSWER** (0x22) cihazdan yanıt yok.</span><span class="sxs-lookup"><span data-stu-id="eddc4-524">**UX_TRANSFER_NO_ANSWER** (0x22) No answer from device.</span></span> <span data-ttu-id="eddc4-525">Aktarım beklenirken cihazın bağlantısı kesilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-525">The device was probably disconnected while the transfer was pending.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-526">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-526">Example</span></span>

```c
/* Write to the CDC class bulk in pipe non blocking mode. */
status = ux_device_class_cdc_acm_write_with_callback(cdc, buffer, UX_DEMO_BUFFER_SIZE);

if(status != UX_SUCCESS)
    return;
```

### <a name="usb-device-cdc-ecm-class"></a><span data-ttu-id="eddc4-527">USB cihazı CDC-ECD sınıfı</span><span class="sxs-lookup"><span data-stu-id="eddc4-527">USB Device CDC-ECM Class</span></span>

<span data-ttu-id="eddc4-528">USB cihazı CDC-ece sınıfı, USB konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-528">The USB device CDC-ECM class allows for a USB host system to communicate with the device as a ethernet device.</span></span> <span data-ttu-id="eddc4-529">Bu sınıf, USB standardını temel alır ve CDC standardının bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-529">This class is based on the USB standard and is a subset of the CDC standard.</span></span>

<span data-ttu-id="eddc4-530">CDC-ACM uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildirilmesine ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-530">A CDC-ACM compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="eddc4-531">Aşağıda aşağıda bir örnek bulunur.</span><span class="sxs-lookup"><span data-stu-id="eddc4-531">An example is found here below.</span></span>

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

<span data-ttu-id="eddc4-532">CDC-ECD sınıfı, CDC-ACM öğesine çok benzer bir cihaz tanımlayıcısı yaklaşımı kullanır ve ayrıca bir ıAD tanımlayıcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-532">The CDC-ECM class uses a very similar device descriptor approach to the CDC-ACM and also requires an IAD descriptor.</span></span> <span data-ttu-id="eddc4-533">Tanım için CDC-ACM sınıfına bakın.</span><span class="sxs-lookup"><span data-stu-id="eddc4-533">See the CDC-ACM class for definition.</span></span>

<span data-ttu-id="eddc4-534">Normal cihaz altyapısına ek olarak, CDC-ECD özel dize tanımlayıcıları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-534">In addition to the regular device framework, the CDC-ECM requires special string descriptors.</span></span> <span data-ttu-id="eddc4-535">Aşağıda bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-535">An example is given below.</span></span>

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

<span data-ttu-id="eddc4-536">MAC adresi dize tanımlayıcısı, ana bilgisayar sorgularını TCP/IP protokolünde yanıtladığı MAC adresine göre yanıtlamak için CDC-ECD sınıfı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-536">The MAC address string descriptor is used by the CDC-ECM class to reply to the host queries as to what MAC address the device is answering to at the TCP/IP protocol.</span></span> <span data-ttu-id="eddc4-537">Cihaz seçimine ayarlanabilir, ancak burada tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-537">It can be set to the device choice but must be defined here.</span></span>

<span data-ttu-id="eddc4-538">CDC-ECD sınıfının başlatılması aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-538">The initialization of the CDC-ECM class is as follows.</span></span>

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

<span data-ttu-id="eddc4-539">Bu sınıfın başlatılması, etkinleştirme ve devre dışı bırakma için aynı işlev geri aramasını bekler, ancak burada bir alıştırma yapılmaması için bir alıştırmada NULL olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-539">The initialization of this class expects the same function callback for activation and deactivation, although here as an exercise they are set to NULL so that no callback is performed.</span></span>

<span data-ttu-id="eddc4-540">Sonraki Parametreler düğüm kimliklerinin tanımına yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-540">The next parameters are for the definition of the node IDs.</span></span> <span data-ttu-id="eddc4-541">2 düğüm, CDC-ECD, yerel bir düğüm ve uzak düğüm için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-541">2 Nodes are necessary for the CDC-ECM, a local node and a remote node.</span></span> <span data-ttu-id="eddc4-542">Yerel düğüm, cihazın MAC adresini belirtir, uzak düğüm ise konağın MAC adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-542">The local node specifies the MAC address of the device, while the remote node specifies the MAC address of the host.</span></span> <span data-ttu-id="eddc4-543">Uzak düğüm, Device Framework dize tanımlayıcısında bildirildiği ile aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-543">The remote node must be the same one as the one declared in the device framework string descriptor.</span></span>

<span data-ttu-id="eddc4-544">CDC-ECM sınıfında, her iki şekilde de verileri aktarmaya yönelik yerleşik API 'Ler vardır ancak kullanıcı uygulaması, USB Ethernet cihazından NetX üzerinden iletişim kurduğu için bu uygulamalar uygulamaya gizlenir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-544">The CDC-ECM class has built-in APIs for transferring data both ways but they are hidden to the application as the user application will communicate with the USB Ethernet device through NetX.</span></span>

<span data-ttu-id="eddc4-545">USBX CDC-ece sınıfı, Azure RTOS NetX ağ yığınına yakın bir şekilde bağlanır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-545">The USBX CDC-ECM class is closely tied to Azure RTOS NetX Network stack.</span></span> <span data-ttu-id="eddc4-546">Hem NetX hem de USBX CDC-ECD sınıfını kullanan bir uygulama NetX ağ yığınını her zamanki şekilde etkinleştirir ancak ek olarak, USB ağ yığınını aşağıdaki şekilde etkinleştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-546">An application using both NetX and USBX CDC-ECM class will activate the NetX network stack in its usual way but in addition needs to activate the USB network stack as follows.</span></span>

```c
/* Initialize the NetX system. */
nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

<span data-ttu-id="eddc4-547">USB ağ yığınının yalnızca bir kez etkinleştirilmesi ve CDCECD 'ye özgü olmaması gerekir, ancak NetX hizmetleri gerektiren herhangi bir USB sınıfı için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-547">The USB network stack needs to be activated only once and is not specific to CDCECM but is required by any USB class that requires NetX services.</span></span>

<span data-ttu-id="eddc4-548">CDC-ECD sınıfı, MAC OS ve Linux konakları tarafından tanınır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-548">The CDC-ECM class will be recognized by MAC OS and Linux hosts.</span></span> <span data-ttu-id="eddc4-549">Ancak Microsoft Windows tarafından CDC-ECD tanımak için bir sürücü sağlanmaz.</span><span class="sxs-lookup"><span data-stu-id="eddc4-549">But there is no driver supplied by Microsoft Windows to recognize CDC-ECM natively.</span></span> <span data-ttu-id="eddc4-550">Bazı ticari ürünler Windows platformları için mevcuttur ve kendi. inf dosyalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="eddc4-550">Some commercial products do exist for Windows platforms and they supply their own .inf file.</span></span> <span data-ttu-id="eddc4-551">Bu dosyanın, USB ağ cihazının PID/VıD 'SI ile eşleşmesi için CDC-ACM INF şablonuyla aynı şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-551">This file will need to be modified the same way as the CDC-ACM inf template to match the PID/VID of the USB network device.</span></span>

## <a name="usb-device-hid-class"></a><span data-ttu-id="eddc4-552">USB cihaz HID sınıfı</span><span class="sxs-lookup"><span data-stu-id="eddc4-552">USB Device HID Class</span></span>

<span data-ttu-id="eddc4-553">USB cihaz HID sınıfı, bir USB konak sisteminin, belirli HID istemci özelliklerine sahip bir HID cihazına bağlanmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-553">The USB device HID class allows for a USB host system to connect to a HID device with specific HID client capabilities.</span></span>

<span data-ttu-id="eddc4-554">USBX HID cihaz sınıfı, ana bilgisayar tarafı ile karşılaştırıldığında nispeten basittir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-554">USBX HID device class is relatively simple compared to the host side.</span></span> <span data-ttu-id="eddc4-555">Cihazın ve HID tanımlayıcısının davranışına yakın bir şekilde bağlanır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-555">It is closely tied to the behavior of the device and its HID descriptor.</span></span>

<span data-ttu-id="eddc4-556">Herhangi bir HID istemcisi öncelikle aşağıdaki örnekte gösterildiği gibi bir HID cihaz çerçevesini tanımlamanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-556">Any HID client requires first to define a HID device framework as the example below.</span></span>

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

<span data-ttu-id="eddc4-557">HID çerçevesi, HID sınıfını ve HID cihaz alt sınıfını açıklayan bir arabirim tanımlayıcısı içerir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-557">The HID framework contains an interface descriptor that describes the HID class and the HID device subclass.</span></span> <span data-ttu-id="eddc4-558">HID arabirimi tek başına bir sınıf veya bileşik bir cihazın parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-558">The HID interface can be a standalone class or part of a composite device.</span></span>

<span data-ttu-id="eddc4-559">Şu anda, çoğu uygulama yalnızca bir KIMLIK (KIMLIK sıfır) gerektirdiğinden, USBX HID sınıfı birden çok rapor kimliğini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="eddc4-559">Currently, the USBX HID class does not support multiple report IDs, as most applications only require one ID (ID zero).</span></span> <span data-ttu-id="eddc4-560">İlgilendiğiniz bir özellik olan birden çok rapor kimliği varsa lütfen bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="eddc4-560">If multiple report IDs is a feature you are interested in, please contact us.</span></span>

<span data-ttu-id="eddc4-561">HID sınıfının başlatılması, örnek olarak bir USB klavye kullanılarak aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-561">The initialization of the HID class is as follow, using a USB keyboard as an example.</span></span>

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

<span data-ttu-id="eddc4-562">Uygulamanın HID sınıfına bir HID rapor tanımlayıcısı ve uzunluğu geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-562">The application needs to pass to the HID class a HID report descriptor and its length.</span></span> <span data-ttu-id="eddc4-563">Rapor tanımlayıcısı, cihazı tanımlayan öğelerin bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="eddc4-563">The report descriptor is a collection of items that describe the device.</span></span> <span data-ttu-id="eddc4-564">HID dilbilgisi hakkında daha fazla bilgi için, HID USB sınıf belirtimine bakın.</span><span class="sxs-lookup"><span data-stu-id="eddc4-564">For more information on the HID grammar refer to the HID USB class specification.</span></span>

<span data-ttu-id="eddc4-565">Rapor tanımlayıcısına ek olarak, bir HID olayı gerçekleştiğinde uygulama bir geri çağrı geçirir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-565">In addition to the report descriptor, the application passes a call back when a HID event happens.</span></span>

<span data-ttu-id="eddc4-566">USBX HID sınıfı, konaktan gelen aşağıdaki standart HID komutlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="eddc4-566">The USBX HID class supports the following standard HID commands from the host.</span></span>

| <span data-ttu-id="eddc4-567">Komut adı</span><span class="sxs-lookup"><span data-stu-id="eddc4-567">Command name</span></span>                             | <span data-ttu-id="eddc4-568">Değer</span><span class="sxs-lookup"><span data-stu-id="eddc4-568">Value</span></span> | <span data-ttu-id="eddc4-569">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-569">Description</span></span>                                      |
| ---------------------------------------- | ----- | ------------------------------------------------ |
| <span data-ttu-id="eddc4-570">UX_DEVICE_CLASS_HID_COMMAND_GET_REPORT</span><span class="sxs-lookup"><span data-stu-id="eddc4-570">UX_DEVICE_CLASS_HID_COMMAND_GET_REPORT</span></span>   | <span data-ttu-id="eddc4-571">0x01</span><span class="sxs-lookup"><span data-stu-id="eddc4-571">0x01</span></span>  | <span data-ttu-id="eddc4-572">Cihazdan rapor alın</span><span class="sxs-lookup"><span data-stu-id="eddc4-572">Get a report from the device</span></span>                     |
| <span data-ttu-id="eddc4-573">UX_DEVICE_CLASS_HID_COMMAND_GET_IDLE</span><span class="sxs-lookup"><span data-stu-id="eddc4-573">UX_DEVICE_CLASS_HID_COMMAND_GET_IDLE</span></span>     | <span data-ttu-id="eddc4-574">0x02</span><span class="sxs-lookup"><span data-stu-id="eddc4-574">0x02</span></span>  | <span data-ttu-id="eddc4-575">Kesme uç noktasının boşta sıklığı 'nı al</span><span class="sxs-lookup"><span data-stu-id="eddc4-575">Get the idle frequency of the interrupt endpoint</span></span> |
| <span data-ttu-id="eddc4-576">UX_DEVICE_CLASS_HID_COMMAND_GET_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="eddc4-576">UX_DEVICE_CLASS_HID_COMMAND_GET_PROTOCOL</span></span> | <span data-ttu-id="eddc4-577">0x03</span><span class="sxs-lookup"><span data-stu-id="eddc4-577">0x03</span></span>  | <span data-ttu-id="eddc4-578">Cihazda çalışan Protokolü al</span><span class="sxs-lookup"><span data-stu-id="eddc4-578">Get the protocol running on the device</span></span>           |
| <span data-ttu-id="eddc4-579">UX_DEVICE_CLASS_HID_COMMAND_SET_REPORT</span><span class="sxs-lookup"><span data-stu-id="eddc4-579">UX_DEVICE_CLASS_HID_COMMAND_SET_REPORT</span></span>   | <span data-ttu-id="eddc4-580">0x09</span><span class="sxs-lookup"><span data-stu-id="eddc4-580">0x09</span></span>  | <span data-ttu-id="eddc4-581">Cihaza bir rapor ayarlama</span><span class="sxs-lookup"><span data-stu-id="eddc4-581">Set a report to the device</span></span>                       |
| <span data-ttu-id="eddc4-582">UX_DEVICE_CLASS_HID_COMMAND_SET_IDLE</span><span class="sxs-lookup"><span data-stu-id="eddc4-582">UX_DEVICE_CLASS_HID_COMMAND_SET_IDLE</span></span>     | <span data-ttu-id="eddc4-583">0x0A</span><span class="sxs-lookup"><span data-stu-id="eddc4-583">0x0a</span></span>  | <span data-ttu-id="eddc4-584">Kesme uç noktasının boşta sıklığını ayarla</span><span class="sxs-lookup"><span data-stu-id="eddc4-584">Set the idle frequency of the interrupt endpoint</span></span> |
| <span data-ttu-id="eddc4-585">UX_DEVICE_CLASS_HID_COMMAND_SET_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="eddc4-585">UX_DEVICE_CLASS_HID_COMMAND_SET_PROTOCOL</span></span> | <span data-ttu-id="eddc4-586">0x0B</span><span class="sxs-lookup"><span data-stu-id="eddc4-586">0x0b</span></span>  | <span data-ttu-id="eddc4-587">Cihazda çalışan Protokolü al</span><span class="sxs-lookup"><span data-stu-id="eddc4-587">Get the protocol running on the device</span></span>           |

<span data-ttu-id="eddc4-588">Get ve set raporu, ana bilgisayar ile cihaz arasında verileri geri ve İleri aktarmak üzere HID tarafından en sık kullanılan komutlardır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-588">The Get and Set report are the most commonly used commands by HID to transfer data back and forth between the host and the device.</span></span> <span data-ttu-id="eddc4-589">En yaygın olarak, konak denetim uç noktasında veri gönderir, ancak kesme uç noktasında ya da verileri denetim uç noktasında getirmek için bir GET_REPORT komutu vererek veri alabilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-589">Most commonly the host sends data on the control endpoint but can receive data either on the interrupt endpoint or by issuing a GET_REPORT command to fetch the data on the control endpoint.</span></span>

<span data-ttu-id="eddc4-590">HID sınıfı, ux_device_class_hid_event_set işlevini kullanarak kesme uç noktasındaki konağa veri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-590">The HID class can send data back to the host on the interrupt endpoint by using the ux_device_class_hid_event_set function.</span></span>

### <a name="ux_device_class_hid_event_set"></a><span data-ttu-id="eddc4-591">ux_device_class_hid_event_set</span><span class="sxs-lookup"><span data-stu-id="eddc4-591">ux_device_class_hid_event_set</span></span>

<span data-ttu-id="eddc4-592">Bir olayı HID sınıfına ayarlama</span><span class="sxs-lookup"><span data-stu-id="eddc4-592">Setting an event to the HID class</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-593">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-593">Prototype</span></span>

```c
UINT ux_device_class_hid_event_set( 
    UX_SLAVE_CLASS_HID *hid,
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a><span data-ttu-id="eddc4-594">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-594">Description</span></span>

<span data-ttu-id="eddc4-595">Bu işlev, bir uygulamanın bir HID olayını konağa geri gönderebilmesi gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-595">This function is called when an application needs to send a HID event back to the host.</span></span> <span data-ttu-id="eddc4-596">İşlev engellenmiyor, yalnızca raporu dairesel bir sıraya koyar ve uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="eddc4-596">The function is not blocking, it merely puts the report into a circular queue and returns to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-597">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-597">Parameters</span></span>

- <span data-ttu-id="eddc4-598">**HID**: HID sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-598">**hid**: Pointer to the hid class instance.</span></span>
- <span data-ttu-id="eddc4-599">**hid_event**: HID olayının yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-599">**hid_event**: Pointer to structure of the hid event.</span></span>

### <a name="return-value"></a><span data-ttu-id="eddc4-600">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="eddc4-600">Return Value</span></span>

- <span data-ttu-id="eddc4-601">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="eddc4-601">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="eddc4-602">**UX_ERROR** (0xFF) hata döngüsel kuyrukta kullanılabilir alan yok.</span><span class="sxs-lookup"><span data-stu-id="eddc4-602">**UX_ERROR** (0xFF) Error no space available in circular queue.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-603">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-603">Example</span></span>

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

<span data-ttu-id="eddc4-604">HID sınıfının başlatılmasında tanımlanan geri çağırma, bir olay göndermenin tersini yapar.</span><span class="sxs-lookup"><span data-stu-id="eddc4-604">The callback defined at the initialization of the HID class performs the opposite of sending an event.</span></span> <span data-ttu-id="eddc4-605">Giriş, ana bilgisayar tarafından gönderilen olayı alır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-605">It gets as input the event sent by the host.</span></span> <span data-ttu-id="eddc4-606">Geri aramanın prototipi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="eddc4-606">The prototype of the callback is as follows.</span></span>

### <a name="hid_callback"></a><span data-ttu-id="eddc4-607">hid_callback</span><span class="sxs-lookup"><span data-stu-id="eddc4-607">hid_callback</span></span>

<span data-ttu-id="eddc4-608">HID sınıfından bir olay alma</span><span class="sxs-lookup"><span data-stu-id="eddc4-608">Getting an event from the HID class</span></span>

### <a name="prototype"></a><span data-ttu-id="eddc4-609">Prototype</span><span class="sxs-lookup"><span data-stu-id="eddc4-609">Prototype</span></span>

```c
UINT hid_callback(
    UX_SLAVE_CLASS_HID *hid, 
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a><span data-ttu-id="eddc4-610">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eddc4-610">Description</span></span>

<span data-ttu-id="eddc4-611">Bu işlev, ana bilgisayar uygulamaya bir HID raporu gönderdiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eddc4-611">This function is called when the host sends a HID report to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="eddc4-612">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eddc4-612">Parameters</span></span>

- <span data-ttu-id="eddc4-613">**HID**: HID sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-613">**hid**: Pointer to the hid class instance.</span></span>
- <span data-ttu-id="eddc4-614">**hid_event**: HID olayının yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="eddc4-614">**hid_event**: Pointer to structure of the hid event.</span></span>

### <a name="example"></a><span data-ttu-id="eddc4-615">Örnek</span><span class="sxs-lookup"><span data-stu-id="eddc4-615">Example</span></span>

<span data-ttu-id="eddc4-616">Aşağıdaki örnek, bir HID klavyesi için bir olayın nasıl yorumlanacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="eddc4-616">The following example shows how to interpret an event for a HID keyboard:</span></span>

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
