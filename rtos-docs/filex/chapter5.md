---
title: Bölüm 5-Azure RTOS FileX için g/ç sürücüleri
description: Bu bölümde, Azure RTOS FileX için g/ç sürücülerinin bir açıklaması yer almaktadır ve geliştiricilere uygulamaya özgü sürücüleri yazma konusunda yardımcı olmak için tasarlanmıştır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8f2ef697f68a269b24a34147a4bc076b8a2b1660
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550091"
---
# <a name="chapter-5---io-drivers-for-azure-rtos-filex"></a><span data-ttu-id="8f054-103">Bölüm 5-Azure RTOS FileX için g/ç sürücüleri</span><span class="sxs-lookup"><span data-stu-id="8f054-103">Chapter 5 - I/O Drivers for Azure RTOS FileX</span></span>

<span data-ttu-id="8f054-104">Bu bölümde, Azure RTOS FileX için g/ç sürücülerinin bir açıklaması yer almaktadır ve geliştiricilere uygulamaya özgü sürücüleri yazma konusunda yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8f054-104">This chapter contains a description of I/O drivers for Azure RTOS FileX and is designed to help developers write application-specific drivers.</span></span>

## <a name="io-driver-introduction"></a><span data-ttu-id="8f054-105">G/ç sürücüsü tanıtımı</span><span class="sxs-lookup"><span data-stu-id="8f054-105">I/O Driver Introduction</span></span>

<span data-ttu-id="8f054-106">FileX birden çok medya aygıtını destekler.</span><span class="sxs-lookup"><span data-stu-id="8f054-106">FileX supports multiple media devices.</span></span> <span data-ttu-id="8f054-107">FX_MEDIA yapısı, bir medya cihazını yönetmek için gereken her şeyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8f054-107">The FX_MEDIA structure defines everything required to manage a media device.</span></span> <span data-ttu-id="8f054-108">Bu yapı, medyaya özgü g/ç sürücüsü ve sürücü ile FileX arasında bilgi ve durum iletmek için ilişkili parametreler dahil olmak üzere tüm medya bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="8f054-108">This structure contains all media information, including the media-specific I/O driver and associated parameters for passing information and status between the driver and FileX.</span></span> <span data-ttu-id="8f054-109">Çoğu sistemde, her FileX medya örneği için benzersiz bir g/ç sürücüsü vardır.</span><span class="sxs-lookup"><span data-stu-id="8f054-109">In most systems, there is a unique I/O driver for each FileX media instance.</span></span>

## <a name="io-driver-entry"></a><span data-ttu-id="8f054-110">G/ç sürücü girdisi</span><span class="sxs-lookup"><span data-stu-id="8f054-110">I/O Driver Entry</span></span>

<span data-ttu-id="8f054-111">Her FileX g/ç sürücüsü, ***fx_media_open*** hizmet çağrısı tarafından tanımlanan tek bir giriş işlevine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8f054-111">Each FileX I/O driver has a single entry function that is defined by the ***fx_media_open*** service call.</span></span> <span data-ttu-id="8f054-112">Sürücü girdisi işlevi aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="8f054-112">The driver entry function has the following format:</span></span>

```c
void my_driver_entry(FX_MEDIA *media_ptr);
```

<span data-ttu-id="8f054-113">FileX, başlatma ve önyükleme kesimini okuma dahil tüm fiziksel medya erişimini istemek için g/ç sürücü girişi işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="8f054-113">FileX calls the I/O driver entry function to request all physical media access, including initialization and boot sector reading.</span></span> <span data-ttu-id="8f054-114">Sürücüye yapılan istekler sırayla yapılır; Yani, FileX, başka bir istek gönderilmeden önce geçerli isteğin tamamlanmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="8f054-114">Requests made to the driver are done sequentially; i.e., FileX waits for the current request to complete before another request is sent.</span></span>

## <a name="io-driver-requests"></a><span data-ttu-id="8f054-115">G/ç sürücüsü Istekleri</span><span class="sxs-lookup"><span data-stu-id="8f054-115">I/O Driver Requests</span></span>

<span data-ttu-id="8f054-116">Her g/ç sürücüsünün tek bir giriş işlevi olduğundan, FileX, medya denetim bloğu aracılığıyla belirli istekleri yapar.</span><span class="sxs-lookup"><span data-stu-id="8f054-116">Because each I/O driver has a single entry function, FileX makes specific requests through the media control block.</span></span> <span data-ttu-id="8f054-117">Özellikle, FX_MEDIA **fx_media_driver_request** üyesi tam  sürücü isteğini belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f054-117">Specifically, the  **fx_media_driver_request** member of **FX_MEDIA** is used to specify the exact driver request.</span></span> <span data-ttu-id="8f054-118">G/ç sürücüsü, **FX_MEDIA** **fx_media_driver_status** üyesi aracılığıyla isteğin başarısını veya başarısızlığını iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="8f054-118">The I/O driver communicates the success or failure of the request through the **fx_media_driver_status** member of **FX_MEDIA**.</span></span> <span data-ttu-id="8f054-119">Sürücü isteği başarılı olduysa, sürücü dönüşmeden önce bu alana **FX_SUCCESS** yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8f054-119">If the driver request was successful, **FX_SUCCESS** is placed in this field before the driver returns.</span></span> <span data-ttu-id="8f054-120">Aksi halde, bir hata algılanırsa, bu alana FX_IO_ERROR yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8f054-120">Otherwise, if an error is detected, FX_IO_ERROR is placed in this field.</span></span>

### <a name="driver-initialization"></a><span data-ttu-id="8f054-121">Sürücü başlatma</span><span class="sxs-lookup"><span data-stu-id="8f054-121">Driver Initialization</span></span>

<span data-ttu-id="8f054-122">Asıl sürücü başlatma işlemi uygulamaya özgü olsa da, genellikle veri yapısı başlatma ve büyük olasılıkla bazı ön donanım başlatma işlemleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="8f054-122">Although the actual driver initialization processing is application specific, it usually consists of data structure initialization and possibly some preliminary hardware initialization.</span></span> <span data-ttu-id="8f054-123">Bu istek, FileX tarafından yapılan ilk ilkdir ve fx_media_open hizmeti içinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="8f054-123">This request is the first made by FileX and is done from within the fx_media_open service.</span></span>

<span data-ttu-id="8f054-124">Medya yazma koruması algılanırsa, FX_MEDIA fx_media_driver_write_protect üyesi olan sürücü FX_TRUE olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8f054-124">If media write protection is detected, the driver fx_media_driver_write_protect member of FX_MEDIA should be set to FX_TRUE.</span></span>

<span data-ttu-id="8f054-125">Aşağıdaki FX_MEDIA üyeleri g/ç sürücüsü başlatma isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-125">The following FX_MEDIA members are used for the I/O driver initialization request:</span></span>

|<span data-ttu-id="8f054-126">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-126">FX_MEDIA member</span></span>|<span data-ttu-id="8f054-127">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-127">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-128">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-128">fx_media_driver_request</span></span>|<span data-ttu-id="8f054-129">FX_DRIVER_INIT</span><span class="sxs-lookup"><span data-stu-id="8f054-129">FX_DRIVER_INIT</span></span>|

<span data-ttu-id="8f054-130">FileX, kesimler artık kullanılmıyorsa uygulama sürücüsünü bilgilendirmek için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f054-130">FileX provides a mechanism to inform the application driver when sectors are no longer being used.</span></span> <span data-ttu-id="8f054-131">Bu özellikle, FLASH ile eşlenmiş tüm kullanımdaki mantıksal kesimleri yönetmesi gereken FLASH bellek yöneticileri için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="8f054-131">This is especially useful for FLASH memory managers that must manage all in-use logical sectors mapped to the FLASH.</span></span>

<span data-ttu-id="8f054-132">Bu tür ücretsiz kesimler gerekliyse, uygulama sürücüsü yalnızca ilişkili **FX_MEDIA** yapısındaki *fx_media_driver_free_sector_update* alanını **FX_TRUE** olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8f054-132">If such notification of free sectors is required, the application driver simply sets the *fx_media_driver_free_sector_update* field in the associated **FX_MEDIA** structure to **FX_TRUE**.</span></span> <span data-ttu-id="8f054-133">Ayarlandıktan sonra, FileX bir veya daha fazla ardışık kesimlerin ücretsiz hale geldiğini belirten bir **_FX_DRIVER_RELEASE_SECTORS_** g/ç sürücü çağrısı yapar.</span><span class="sxs-lookup"><span data-stu-id="8f054-133">After set, FileX makes a **_FX_DRIVER_RELEASE_SECTORS_** I/O driver call indicating when one or more consecutive sectors becomes free.</span></span>

### <a name="boot-sector-read"></a><span data-ttu-id="8f054-134">Önyükleme kesimini okuma</span><span class="sxs-lookup"><span data-stu-id="8f054-134">Boot Sector Read</span></span>

<span data-ttu-id="8f054-135">FileX, standart bir okuma isteği kullanmak yerine medyanın önyükleme kesimini okumak için belirli bir istek yapar.</span><span class="sxs-lookup"><span data-stu-id="8f054-135">Instead of using a standard read request, FileX makes a specific request to read the media's boot sector.</span></span> <span data-ttu-id="8f054-136">Aşağıdaki **FX_MEDIA** üyeleri g/ç sürücüsü önyükleme kesimi okuma isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-136">The following **FX_MEDIA** members are used for the I/O driver boot sector read request:</span></span>

|<span data-ttu-id="8f054-137">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-137">FX_MEDIA member</span></span>|<span data-ttu-id="8f054-138">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-138">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-139">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-139">fx_media_driver_request</span></span>| <span data-ttu-id="8f054-140">FX_DRIVER_BOOT_READ</span><span class="sxs-lookup"><span data-stu-id="8f054-140">FX_DRIVER_BOOT_READ</span></span>|
|<span data-ttu-id="8f054-141">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="8f054-141">fx_media_driver_buffer</span></span>| <span data-ttu-id="8f054-142">Önyükleme sektörü için hedefin adresi.</span><span class="sxs-lookup"><span data-stu-id="8f054-142">Address of destination for boot sector.</span></span>|

### <a name="boot-sector-write"></a><span data-ttu-id="8f054-143">Önyükleme kesimine yazma</span><span class="sxs-lookup"><span data-stu-id="8f054-143">Boot Sector Write</span></span>

<span data-ttu-id="8f054-144">FileX, standart bir yazma isteği kullanmak yerine medyanın önyükleme kesimini yazmak için belirli bir istek yapar.</span><span class="sxs-lookup"><span data-stu-id="8f054-144">Instead of using a standard write request, FileX makes a specific request to write the media's boot sector.</span></span> <span data-ttu-id="8f054-145">Aşağıdaki **FX_MEDIA** üyeleri g/ç sürücüsü önyükleme kesimi yazma isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-145">The following **FX_MEDIA** members are used for the I/O driver boot sector write request:</span></span>

|<span data-ttu-id="8f054-146">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-146">FX_MEDIA member</span></span>|<span data-ttu-id="8f054-147">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-147">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-148">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-148">fx_media_driver_request</span></span>| <span data-ttu-id="8f054-149">FX_DRIVER_BOOT_WRITE</span><span class="sxs-lookup"><span data-stu-id="8f054-149">FX_DRIVER_BOOT_WRITE</span></span>|
|<span data-ttu-id="8f054-150">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="8f054-150">fx_media_driver_buffer</span></span>| <span data-ttu-id="8f054-151">Önyükleme kesiminin kaynak adresi.</span><span class="sxs-lookup"><span data-stu-id="8f054-151">Address of source for boot sector.</span></span>|

### <a name="sector-read"></a><span data-ttu-id="8f054-152">Kesim okuma</span><span class="sxs-lookup"><span data-stu-id="8f054-152">Sector Read</span></span>

<span data-ttu-id="8f054-153">FileX, g/ç sürücüsüne bir okuma isteği vererek bir veya daha fazla kesimi belleğe okur.</span><span class="sxs-lookup"><span data-stu-id="8f054-153">FileX reads one or more sectors into memory by issuing a read request to the I/O driver.</span></span> <span data-ttu-id="8f054-154">Aşağıdaki **FX_MEDIA** üyeleri g/ç sürücüsü okuma isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-154">The following **FX_MEDIA** members are used for the I/O driver read request:</span></span>

|<span data-ttu-id="8f054-155">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-155">FX_MEDIA member</span></span>|<span data-ttu-id="8f054-156">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-156">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-157">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-157">fx_media_driver_request</span></span>| <span data-ttu-id="8f054-158">FX_DRIVER_READ</span><span class="sxs-lookup"><span data-stu-id="8f054-158">FX_DRIVER_READ</span></span>|
|<span data-ttu-id="8f054-159">fx_media_driver_logical_sector</span><span class="sxs-lookup"><span data-stu-id="8f054-159">fx_media_driver_logical_sector</span></span>|<span data-ttu-id="8f054-160">Okunan mantıksal kesim</span><span class="sxs-lookup"><span data-stu-id="8f054-160">Logical sector to read</span></span>|
|<span data-ttu-id="8f054-161">fx_media_driver_sectors</span><span class="sxs-lookup"><span data-stu-id="8f054-161">fx_media_driver_sectors</span></span>|<span data-ttu-id="8f054-162">Okunacak kesim sayısı</span><span class="sxs-lookup"><span data-stu-id="8f054-162">Number of sectors to read</span></span>|
|<span data-ttu-id="8f054-163">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="8f054-163">fx_media_driver_buffer</span></span>|<span data-ttu-id="8f054-164">Okunan kesimler için hedef arabellek</span><span class="sxs-lookup"><span data-stu-id="8f054-164">Destination buffer for sector(s) read</span></span>|
|<span data-ttu-id="8f054-165">fx_media_driver_data_sector_read</span><span class="sxs-lookup"><span data-stu-id="8f054-165">fx_media_driver_data_sector_read</span></span>|<span data-ttu-id="8f054-166">Bir dosya veri kesimi isteniyorsa FX_TRUE olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8f054-166">Set to FX_TRUE if a file data sector is requested.</span></span> <span data-ttu-id="8f054-167">Aksi takdirde, bir sistem kesimi (FAT veya dizin sektörü) isteniyorsa FX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="8f054-167">Otherwise, FX_FALSE if a system sector (FAT or directory sector) is requested.</span></span>|
|<span data-ttu-id="8f054-168">fx_media_driver_sector_type</span><span class="sxs-lookup"><span data-stu-id="8f054-168">fx_media_driver_sector_type</span></span>|<span data-ttu-id="8f054-169">İstenen kesime ait açık türü aşağıdaki şekilde tanımlar:</span><span class="sxs-lookup"><span data-stu-id="8f054-169">Defines the explicit type of sector requested, as follows:</span></span><br /><span data-ttu-id="8f054-170">FX_FAT_SECTOR (2)</span><span class="sxs-lookup"><span data-stu-id="8f054-170">FX_FAT_SECTOR (2)</span></span><br /><span data-ttu-id="8f054-171">FX_DIRECTORY_SECTOR (3)</span><span class="sxs-lookup"><span data-stu-id="8f054-171">FX_DIRECTORY_SECTOR (3)</span></span><br /><span data-ttu-id="8f054-172">FX_DATA_SECTOR (4)</span><span class="sxs-lookup"><span data-stu-id="8f054-172">FX_DATA_SECTOR (4)</span></span>|

### <a name="sector-write"></a><span data-ttu-id="8f054-173">Kesim yazma</span><span class="sxs-lookup"><span data-stu-id="8f054-173">Sector Write</span></span>

<span data-ttu-id="8f054-174">FileX, g/ç sürücüsüne bir yazma isteği vererek fiziksel medyaya bir veya daha fazla kesim yazar.</span><span class="sxs-lookup"><span data-stu-id="8f054-174">FileX writes one or more sectors to the physical media by issuing a write request to the I/O driver.</span></span> <span data-ttu-id="8f054-175">Aşağıdaki FX_MEDIA üyeleri g/ç sürücüsü yazma isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-175">The following FX_MEDIA members are used for the I/O driver write request:</span></span>

|<span data-ttu-id="8f054-176">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-176">FX_MEDIA member</span></span>| <span data-ttu-id="8f054-177">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-177">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-178">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-178">fx_media_driver_request</span></span>|<span data-ttu-id="8f054-179">FX_DRIVER_WRITE</span><span class="sxs-lookup"><span data-stu-id="8f054-179">FX_DRIVER_WRITE</span></span>|
|<span data-ttu-id="8f054-180">fx_media_driver_logical_sector</span><span class="sxs-lookup"><span data-stu-id="8f054-180">fx_media_driver_logical_sector</span></span>|<span data-ttu-id="8f054-181">Yazılacak mantıksal kesim</span><span class="sxs-lookup"><span data-stu-id="8f054-181">Logical sector to write</span></span>|
|<span data-ttu-id="8f054-182">fx_media_driver_sectors</span><span class="sxs-lookup"><span data-stu-id="8f054-182">fx_media_driver_sectors</span></span>|<span data-ttu-id="8f054-183">Yazılacak kesim sayısı</span><span class="sxs-lookup"><span data-stu-id="8f054-183">Number of sectors to write</span></span>|
|<span data-ttu-id="8f054-184">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="8f054-184">fx_media_driver_buffer</span></span>|<span data-ttu-id="8f054-185">Yazılacak kesimler için kaynak arabelleği</span><span class="sxs-lookup"><span data-stu-id="8f054-185">Source buffer for sector(s) to write</span></span>|
|<span data-ttu-id="8f054-186">fx_media_driver_system_write</span><span class="sxs-lookup"><span data-stu-id="8f054-186">fx_media_driver_system_write</span></span>| <span data-ttu-id="8f054-187">Bir sistem kesimi isteniyorsa (FAT veya dizin sektörü) FX_TRUE olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8f054-187">Set to FX_TRUE if a system sector is requested (FAT or directory sector).</span></span> <span data-ttu-id="8f054-188">Aksi takdirde, bir dosya veri kesimi isteniyorsa FX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="8f054-188">Otherwise, FX_FALSE if a file data sector is requested.</span></span>|
|<span data-ttu-id="8f054-189">fx_media_driver_sector_type</span><span class="sxs-lookup"><span data-stu-id="8f054-189">fx_media_driver_sector_type</span></span>|<span data-ttu-id="8f054-190">İstenen kesime ait açık türü aşağıdaki şekilde tanımlar:</span><span class="sxs-lookup"><span data-stu-id="8f054-190">Defines the explicit type of sector requested, as follows:</span></span><br> <br><span data-ttu-id="8f054-191">FX_FAT_SECTOR (2)</span><span class="sxs-lookup"><span data-stu-id="8f054-191">FX_FAT_SECTOR (2)</span></span> <br> <span data-ttu-id="8f054-192">FX_DIRECTORY_SECTOR (3)</span><span class="sxs-lookup"><span data-stu-id="8f054-192">FX_DIRECTORY_SECTOR (3)</span></span> <br><span data-ttu-id="8f054-193">FX_DATA_SECTOR (4).</span><span class="sxs-lookup"><span data-stu-id="8f054-193">FX_DATA_SECTOR (4).</span></span>|

### <a name="driver-flush"></a><span data-ttu-id="8f054-194">Sürücü temizleme</span><span class="sxs-lookup"><span data-stu-id="8f054-194">Driver Flush</span></span>

<span data-ttu-id="8f054-195">FileX, g/ç sürücüsüne bir temizleme isteği vererek sürücünün kesim önbelleğinde bulunan tüm kesimleri fiziksel medyaya boşaltır.</span><span class="sxs-lookup"><span data-stu-id="8f054-195">FileX flushes all sectors currently in the driver's sector cache to the physical media by issuing a flush request to the I/O driver.</span></span> <span data-ttu-id="8f054-196">Tabii ki, sürücü önbelleğe alma kesimleri değilse, bu istek sürücü işleme gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="8f054-196">Of course, if the driver is not caching sectors, this request requires no driver processing.</span></span> <span data-ttu-id="8f054-197">Aşağıdaki FX_MEDIA üyeleri g/ç sürücüsü temizleme isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-197">The following FX_MEDIA members are used for the I/O driver flush request:</span></span>

|<span data-ttu-id="8f054-198">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-198">FX_MEDIA member</span></span>| <span data-ttu-id="8f054-199">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-199">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-200">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-200">fx_media_driver_request</span></span>|<span data-ttu-id="8f054-201">FX_DRIVER_FLUSH</span><span class="sxs-lookup"><span data-stu-id="8f054-201">FX_DRIVER_FLUSH</span></span>|

### <a name="driver-abort"></a><span data-ttu-id="8f054-202">Sürücü Iptali</span><span class="sxs-lookup"><span data-stu-id="8f054-202">Driver Abort</span></span>

<span data-ttu-id="8f054-203">FileX, g/ç sürücüsüne bir iptal isteği vererek fiziksel medyayla tüm fiziksel g/ç etkinliklerini iptal etmek için sürücüye bildirir.</span><span class="sxs-lookup"><span data-stu-id="8f054-203">FileX informs the driver to abort all further physical I/O activity with the physical media by issuing an abort request to the I/O driver.</span></span> <span data-ttu-id="8f054-204">Sürücünün yeniden başlatılması bitinceye kadar bir g/ç işlemi gerçekleştirmemelidir.</span><span class="sxs-lookup"><span data-stu-id="8f054-204">The driver should not perform any I/O again until it is re-initialized.</span></span> <span data-ttu-id="8f054-205">Aşağıdaki FX_MEDIA üyeleri g/ç sürücü iptali isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-205">The following FX_MEDIA members are used for the I/O driver abort request:</span></span>

|<span data-ttu-id="8f054-206">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-206">FX_MEDIA member</span></span>| <span data-ttu-id="8f054-207">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-207">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-208">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-208">fx_media_driver_request</span></span>| <span data-ttu-id="8f054-209">FX_DRIVER_ABORT</span><span class="sxs-lookup"><span data-stu-id="8f054-209">FX_DRIVER_ABORT</span></span>|

### <a name="release-sectors"></a><span data-ttu-id="8f054-210">Yayın kesimleri</span><span class="sxs-lookup"><span data-stu-id="8f054-210">Release Sectors</span></span>

<span data-ttu-id="8f054-211">Başlatma sırasında sürücü tarafından daha önce seçilirse FileX, bir veya daha fazla ardışık kesim ücretsiz olduğunda sürücüyü bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="8f054-211">If previously selected by the driver during initialization, FileX informs the driver whenever one or more consecutive sectors become free.</span></span> <span data-ttu-id="8f054-212">Sürücü aslında bir FLASH Manager ise bu bilgiler, FLASH Manager 'a bu kesimlerin artık gerekli olmadığını bildirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8f054-212">If the driver is actually a FLASH manager, this information can be used to tell the FLASH manager that these sectors are no longer needed.</span></span> <span data-ttu-id="8f054-213">Aşağıdaki **FX_MEDIA** üyeleri g/ç sürüm kesimleri isteği için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8f054-213">The following **FX_MEDIA** members are used for the I/O release sectors request:</span></span>

|<span data-ttu-id="8f054-214">FX_MEDIA üyesi</span><span class="sxs-lookup"><span data-stu-id="8f054-214">FX_MEDIA member</span></span>| <span data-ttu-id="8f054-215">Anlamı</span><span class="sxs-lookup"><span data-stu-id="8f054-215">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="8f054-216">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="8f054-216">fx_media_driver_request</span></span>|<span data-ttu-id="8f054-217">FX_DRIVER_RELEASE_SECTORS</span><span class="sxs-lookup"><span data-stu-id="8f054-217">FX_DRIVER_RELEASE_SECTORS</span></span>|
|<span data-ttu-id="8f054-218">fx_media_driver_logical_sector</span><span class="sxs-lookup"><span data-stu-id="8f054-218">fx_media_driver_logical_sector</span></span>|<span data-ttu-id="8f054-219">Ücretsiz kesim başlangıcı</span><span class="sxs-lookup"><span data-stu-id="8f054-219">Start of free sector</span></span>|
|<span data-ttu-id="8f054-220">fx_media_driver_sectors</span><span class="sxs-lookup"><span data-stu-id="8f054-220">fx_media_driver_sectors</span></span>|<span data-ttu-id="8f054-221">Boş sektör sayısı</span><span class="sxs-lookup"><span data-stu-id="8f054-221">Number of free sectors</span></span>|

### <a name="driver-suspension"></a><span data-ttu-id="8f054-222">Sürücü askıya alma</span><span class="sxs-lookup"><span data-stu-id="8f054-222">Driver Suspension</span></span>

<span data-ttu-id="8f054-223">Fiziksel medyayla g/ç bir süre sürebileceğinden, çağıran iş parçacığının askıya alınması genellikle tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="8f054-223">Because I/O with physical media may take some time, suspending the calling thread is often desirable.</span></span> <span data-ttu-id="8f054-224">Tabii ki bu, temeldeki g/ç işleminin tamamlandığını kesintiye uğratan bir şekilde üstlenir.</span><span class="sxs-lookup"><span data-stu-id="8f054-224">Of course, this assumes completion of the underlying I/O operation is interrupt driven.</span></span> <span data-ttu-id="8f054-225">Bu durumda, iş parçacığı askıya alma, bir ThreadX semaforu ile kolayca uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8f054-225">If so, thread suspension is easily implemented with a ThreadX semaphore.</span></span> <span data-ttu-id="8f054-226">Giriş veya çıkış işlemini başlattıktan sonra, g/ç sürücüsü kendi iç g/ç semaforu üzerinde bekletir (sürücü başlatma sırasında başlangıç sayısı sıfır ile oluşturulur).</span><span class="sxs-lookup"><span data-stu-id="8f054-226">After starting the input or output operation, the I/O driver suspends on its own internal I/O semaphore (created with an initial count of zero during driver initialization).</span></span> <span data-ttu-id="8f054-227">Sürücü g/ç tamamlama kesme işleminin bir parçası olarak, aynı g/ç semaforu ayarlanır ve bu da askıya alınan iş parçacığını uyandırır.</span><span class="sxs-lookup"><span data-stu-id="8f054-227">As part of the driver I/O completion interrupt processing, the same I/O semaphore is set, which in turn wakes up the suspended thread.</span></span>

### <a name="sector-translation"></a><span data-ttu-id="8f054-228">Kesim çevirisi</span><span class="sxs-lookup"><span data-stu-id="8f054-228">Sector Translation</span></span>

<span data-ttu-id="8f054-229">FileX, medyayı doğrusal mantıksal kesimler olarak görüntülediğinde g/ç sürücüsüne yapılan g/ç istekleri mantıksal kesimlerle yapılır.</span><span class="sxs-lookup"><span data-stu-id="8f054-229">Because FileX views the media as linear logical sectors, I/O requests made to the I/O driver are made with logical sectors.</span></span> <span data-ttu-id="8f054-230">Mantıksal kesimler ve medyanın fiziksel geometrisi arasında çevrilecek, bu da kafa, iz ve fiziksel kesimleri içerebilen sürücü sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="8f054-230">It is the driver's responsibility to translate between logical sectors and the physical geometry of the media, which may include heads, tracks, and physical sectors.</span></span> <span data-ttu-id="8f054-231">FLASH ve RAM disk medyası için, mantıksal kesimler genellikle dizini fiziksel kesimlerde eşler.</span><span class="sxs-lookup"><span data-stu-id="8f054-231">For FLASH and RAM disk media, the logical sectors typically map directory to physical sectors.</span></span> <span data-ttu-id="8f054-232">Her durumda, g/ç sürücüsünde mantıksal to fiziksel kesim eşlemesini gerçekleştirmek için tipik formüller aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8f054-232">In any case, here are the typical formulas to perform the logical to physical sector mapping in the I/O driver:</span></span>

```c
media_ptr -> fx_media_driver_physical_sector =
    (media_ptr -> fx_media_driver_logical_sector % media_ptr -> fx_media_sectors_per_track) + 1;

media_ptr -> fx_media_driver_physical_head =
    (media_ptr -> fx_media_driver_logical_sector/ media_ptr ->
    fx_media_sectors_per_track) % media_ptr -> fx_media_heads;

media_ptr -> fx_media_driver_physical_track =(media_ptr ->
    fx_media_driver_logical_sector/ (media_ptr -> fx_media_sectors_per_track *
    media_ptr -> fx_media_heads)));
```

<span data-ttu-id="8f054-233">Fiziksel kesimlerin tek seferde başlayıp mantıksal kesimlerin sıfırdan başlaması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8f054-233">Note that physical sectors start at one, while logical sectors start at zero.</span></span>

### <a name="hidden-sectors"></a><span data-ttu-id="8f054-234">Gizli kesimler</span><span class="sxs-lookup"><span data-stu-id="8f054-234">Hidden Sectors</span></span>

<span data-ttu-id="8f054-235">Gizli kesimler, medyadaki önyükleme kaydından önce yer alır.</span><span class="sxs-lookup"><span data-stu-id="8f054-235">Hidden sectors resided prior to the boot record on the media.</span></span> <span data-ttu-id="8f054-236">Bunlar aslında FAT dosya sistemi düzeninin kapsamı dışında olduğundan, sürücünün her mantıksal kesim işleminde hesaba katılmış olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f054-236">Because they are really outside the scope of the FAT file system layout, they must be accounted for in each logical sector operation the driver does.</span></span>

### <a name="media-write-protect"></a><span data-ttu-id="8f054-237">Medya yazma koruması</span><span class="sxs-lookup"><span data-stu-id="8f054-237">Media Write Protect</span></span>

<span data-ttu-id="8f054-238">FileX sürücüsü, medya denetim bloğunda fx_media_driver_write_protect alanını ayarlayarak yazma korumasını açabilir.</span><span class="sxs-lookup"><span data-stu-id="8f054-238">The FileX driver can turn on write protect by setting the fx_media_driver_write_protect field in the media control block.</span></span> <span data-ttu-id="8f054-239">Bu, medyaya yazma girişiminde herhangi bir FileX çağrısı yapılırsa bir hata döndürülmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="8f054-239">This will cause an error to be returned if any FileX calls are made in an attempt to write to the media.</span></span>

## <a name="sample-ram-driver"></a><span data-ttu-id="8f054-240">Örnek RAM sürücüsü</span><span class="sxs-lookup"><span data-stu-id="8f054-240">Sample RAM Driver</span></span>

<span data-ttu-id="8f054-241">FileX tanıtım sistemi, fx_ram_driver. c dosyasında tanımlanan küçük bir RAM disk sürücüsüyle birlikte dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8f054-241">The FileX demonstration system is delivered with a small RAM disk driver, which is defined in the file fx_ram_driver.c.</span></span> <span data-ttu-id="8f054-242">Sürücü, bir 32K bellek alanını varsayar ve 256 128 baytlık kesimler için bir önyükleme kaydı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8f054-242">The driver assumes a 32K memory space and creates a boot record for 256 128-byte sectors.</span></span> <span data-ttu-id="8f054-243">Bu dosya, uygulamaya özel FileX g/ç sürücülerinin nasıl uygulanacağı hakkında iyi bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f054-243">This file provides a good example of how to implement application specific FileX I/O drivers.</span></span>

```c
/*FUNCTION: _fx_ram_driver
RELEASE: PORTABLE C 5.7
AUTHOR: William E. Lamie, Microsoft, Inc.
DESCRIPTION: This function is the entry point to the generic
    RAM disk driver that is delivered with all versions of FileX.
    The format of the RAM disk is easily modified by calling fx_media_format prior to opening the media.

    This driver also serves as a template for developing FileX drivers
    for actual devices. Simply replace the read/write sector logic
    with calls to read/write from the appropriate physical device.

FileX RAM/FLASH structures look like the following:
Physical Sector             Contents
    0                         Boot record
    1                         FAT Area Start
    +FAT Sectors             Root Directory Start
    +Directory Sectors         Data Sector Start

INPUT: media_ptr Media control block pointer
OUTPUT: None
CALLS:     _fx_utility_memory_copy Copy sector memory
        _fx_utility_16_unsigned_read Read 16-bit unsigned
CALLED BY: FileX System Functions
RELEASE HISTORY:

    DATE         NAME         DESCRIPTION
    12-12-2005     William E.     Lamie Initial Version 5.0
    07-18-2007     William E.     Lamie Modified comment(s),
                                resulting in version 5.1
    03-01-2009     William E.     Lamie Modified comment(s),
                                resulting in version 5.2
    11-01-2015     William E.     Lamie Modified comment(s),
                                resulting in version 5.3
    04-15-2016     William E.     Lamie Modified comment(s),
                                resulting in version 5.4
    04-03-2017     William E.     Lamie Modified comment(s),
                                fixed compiler warnings,
                                resulting in version 5.5
    12-01-2018     William E.     Lamie Modified comment(s),
                                checked buffer overflow,
                                resulting in version 5.6
    08-15-2019     William E.     Lamie Modified comment(s),
                                resulting in version 5.7
*/

VOID _fx_ram_driver(FX_MEDIA *media_ptr) { UCHAR *source_buffer;
                                           UCHAR *destination_buffer;
                                           UINT bytes_per_sector;

    /* There are several useful/important pieces of information contained
        in the media structure, some of which are supplied by FileX and
        others are for the driver to setup. The following
        is a summary of the necessary FX_MEDIA structure members:
    FX_MEDIA Member                     Meaning

    fx_media_driver_request             FileX request type.
        Valid requests from FileX are as follows:
        FX_DRIVER_READ
        FX_DRIVER_WRITE
        FX_DRIVER_FLUSH
        FX_DRIVER_ABORT
        FX_DRIVER_INIT
        FX_DRIVER_BOOT_READ
        FX_DRIVER_RELEASE_SECTORS
        FX_DRIVER_BOOT_WRITE FX_DRIVER_UNINIT

    fx_media_driver_status              This value is RETURNED by the driver.
        If the operation is successful, this field should be set to FX_SUCCESS
        for before returning. Otherwise, if an error occurred, this field should be set to FX_IO_ERROR.

    fx_media_driver_buffer              Pointer to buffer to read or write sector data. This is supplied by FileX.

    fx_media_driver_logical_sector      Logical sector FileX is requesting.
    fx_media_driver_sectors             Number of sectors FileX is requesting.

    The following is a summary of the optional FX_MEDIA structure members: FX_MEDIA Member Meaning

    fx_media_driver_info                Pointer to any additional information or memory.
        This is optional for the driver use and is setup from the fx_media_open call.
        The RAM disk uses this pointer for the RAM disk memory itself.

    fx_media_driver_write_protect       The DRIVER sets this to FX_TRUE when media is write protected.
        This is typically done in initialization, but can be done anytime.

    fx_media_driver_free_sector_update  The DRIVER sets this to FX_TRUE when it needs
        to know when clusters are released. This is important for FLASH wear-leveling drivers.

    fx_media_driver_system_write        FileX sets this flag to FX_TRUE if the sector
        being written is a system sector, e.g., a boot, FAT, or directory sector.
        The driver may choose to use this to initiate error recovery logic for greater fault
        tolerance. fx_media_driver_data_sector_read FileX sets this flag to FX_TRUE
        if the sector(s) being read are file data sectors, i.e., NOT system sectors.

    fx_media_driver_sector_type         FileX sets this variable to the specific type of
        sector being read or written. The following sector types are identified:
            FX_UNKNOWN_SECTOR
            FX_BOOT_SECTOR
            FX_FAT_SECTOR
            FX_DIRECTORY_SECTOR
            FX_DATA_SECTOR */

    /* Process the driver request specified in the media control block. */

    switch (media_ptr -> fx_media_driver_request){

        case FX_DRIVER_READ: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
            is pointed to by the fx_media_driver_info pointer, which is supplied
            by the application in the call to fx_media_open. */

            source_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the RAM sector into the destination. */

             _fx_utility_memory_copy(source_buffer,
                media_ptr -> fx_media_driver_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_WRITE: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
                is pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */

            destination_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the source to the RAM sector. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_FLUSH: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_ABORT: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_INIT: {

            /* FLASH drivers are responsible for setting several fields
                in the media structure, as follows:
                media_ptr -> fx_media_driver_free_sector_update media_ptr ->
                fx_media_driver_write_protect
                The fx_media_driver_free_sector_update flag is used to instruct
                FileX to inform the driver whenever sectors are not being used.
                This is especially useful for FLASH managers so they don't have
                maintain mapping for sectors no longer in use.
                The fx_media_driver_write_protect flag can be set anytime by
                the driver to indicate the media is not writable. Write attempts
                made when this flag is set are returned as errors. */
            /* Perform basic initialization here... since the boot record is going
                to be read subsequently and again for volume name requests. */
            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

         case FX_DRIVER_UNINIT: {

            /* There is nothing to do in this case for the RAM driver.
                For actual devices some shutdown processing may be necessary. */

            /* Successful driver request. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_READ: {
            /* Read the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is pointed
                to by the fx_media_driver_info pointer, which is supplied by the
                application in the call to fx_media_open. */

            source_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* For RAM driver, determine if the boot record is valid. */

            if ((source_buffer[0] != (UCHAR)0xEB) ||

            ((source_buffer[1] != (UCHAR)0x34) &&

            (source_buffer[1] != (UCHAR)0x76)) || /* exFAT jump code. */

            (source_buffer[2] != (UCHAR)0x90)) {

            /* Invalid boot record, return an error! */
            media_ptr -> fx_media_driver_status = FX_MEDIA_INVALID; return; }

            /* For RAM disk only, pickup the bytes per sector. */

            bytes_per_sector =
                _fx_utility_16_unsigned_read(&source_buffer[FX_BYTES_SECTOR]); #ifdef FX_ENABLE_EXFAT

            /* if byte per sector is zero, then treat it as exFAT volume. */

            if (bytes_per_sector == 0 && (source_buffer[1] == (UCHAR)0x76)) {

            /* Pickup the byte per sector shift, and calculate byte per sector. */ 
            bytes_per_sector = (UINT)(1 << source_buffer[FX_EF_BYTE_PER_SECTOR_SHIFT]);

            }

            #endif /* FX_ENABLE_EXFAT */

            /* Ensure this is less than the media memory size. */
            if (bytes_per_sector \media_ptr -> fx_media_memory_size) {

            media_ptr -> fx_media_driver_status = FX_BUFFER_ERROR; break; }

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(source_buffer, media_ptr -> fx_media_driver_buffer, bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_WRITE: {

            /* Write the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is
                pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */ 
            destination_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        default: {
            /* Invalid driver request. */
            media_ptr -> fx_media_driver_status = FX_IO_ERROR; break;}
    }
}
```
