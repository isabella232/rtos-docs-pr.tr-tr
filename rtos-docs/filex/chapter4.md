---
title: Bölüm 4- FileX Azure RTOS açıklaması
description: Bu bölümde, FileX hizmetleriyle Azure RTOS alfabetik olarak sıralanmış bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c24259fb9b6b212dda99422e3ee1ad0e2fd970ce
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754888"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a><span data-ttu-id="34ea1-103">Bölüm 4- FileX Azure RTOS açıklaması</span><span class="sxs-lookup"><span data-stu-id="34ea1-103">Chapter 4- Description of Azure RTOS FileX services</span></span>

<span data-ttu-id="34ea1-104">Bu bölümde, FileX hizmetleriyle Azure RTOS alfabetik olarak sıralanmış bir açıklama yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-104">This chapter contains a description of all Azure RTOS FileX services in alphabetic order.</span></span> <span data-ttu-id="34ea1-105">Hizmet adları, benzer hizmetlerin hepsi birlikte grup olacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-105">Service names are designed so all similar services are grouped together.</span></span>

## <a name="fx_directory_attributes_read"></a><span data-ttu-id="34ea1-106">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-106">fx_directory_attributes_read</span></span>

<span data-ttu-id="34ea1-107">Dizin özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="34ea1-107">Reads directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-108">Prototype</span></span>

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a><span data-ttu-id="34ea1-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-109">Description</span></span>

<span data-ttu-id="34ea1-110">Bu hizmet, dizinin özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-110">This service reads the directory's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-111">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-111">Input Parameters</span></span>

- <span data-ttu-id="34ea1-112">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-112">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-113">**directory_name:** İstenen dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-113">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="34ea1-114">**öznitelikler** _ptr: Dizinin özniteliklerinin yerleştirilecek hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-114">**attributes** _ptr: Pointer to the destination for the directory's attributes to be placed.</span></span> <span data-ttu-id="34ea1-115">Dizin öznitelikleri, aşağıdaki olası ayarlarla bit eşlemesi biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="34ea1-115">The directory attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="34ea1-116">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-116">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="34ea1-117">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-117">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="34ea1-118">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="34ea1-118">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="34ea1-119">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="34ea1-119">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="34ea1-120">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="34ea1-120">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="34ea1-121">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="34ea1-121">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-122">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-122">Return Values</span></span>

- <span data-ttu-id="34ea1-123">**FX_SUCCESS** (0x00) Başarılı dizin öznitelikleri okundu</span><span class="sxs-lookup"><span data-stu-id="34ea1-123">**FX_SUCCESS** (0x00) Successful directory attributes read</span></span>
- <span data-ttu-id="34ea1-124">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-124">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-125">**FX _NOT BULUNDU** (0x04) Belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="34ea1-125">**FX _NOT FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="34ea1-126">**FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-126">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="34ea1-127">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-127">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-128">**FX_FILE_CORRUPT** 0x08) Dosya bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-128">**FX_FILE_CORRUPT** 0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-129">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-129">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-130">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-130">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-131">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-131">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-132">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="34ea1-132">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="34ea1-133">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-133">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="34ea1-134">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-134">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-135">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-135">Allowed From</span></span>

<span data-ttu-id="34ea1-136">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-136">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-137">Example</span></span>

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-138">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-138">See Also</span></span>

- <span data-ttu-id="34ea1-139">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-139">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-140">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-140">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-141">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-141">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-142">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-142">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-143">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-143">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-144">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-144">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-145">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-145">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-146">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-146">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-147">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-147">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-148">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-148">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-149">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-149">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-150">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-150">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-151">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-151">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-152">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-152">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-153">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-153">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-154">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-154">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-155">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-155">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-156">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-156">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-157">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-157">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-158">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-158">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_attributes_set"></a><span data-ttu-id="34ea1-159">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-159">fx_directory_attributes_set</span></span>

<span data-ttu-id="34ea1-160">Dizin özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-160">Sets directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-161">Prototype</span></span>

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a><span data-ttu-id="34ea1-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-162">Description</span></span>

<span data-ttu-id="34ea1-163">Bu hizmet, dizinin özniteliklerini çağıranın belirttiğiniz özniteliklere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-163">This service sets the directory's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-164">*Bu uygulamanın yalnızca bu hizmetle dizin özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlama girişimi hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-164">*This application is only allowed to modify a subset of the directory's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-165">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-165">Input Parameters</span></span>

- <span data-ttu-id="34ea1-166">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-166">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-167">**directory_name:** İstenen dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-167">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="34ea1-168">**attributes:** Bu dizine yeni öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-168">**attributes**: The new attributes to this directory.</span></span> <span data-ttu-id="34ea1-169">Geçerli dizin öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-169">The valid directory attributes are defined as follows:</span></span>
  - <span data-ttu-id="34ea1-170">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-170">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="34ea1-171">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-171">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="34ea1-172">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="34ea1-172">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="34ea1-173">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="34ea1-173">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-174">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-174">Return Values</span></span>

- <span data-ttu-id="34ea1-175">**FX_SUCCESS** (0x00) Başarılı dizin öznitelik kümesi</span><span class="sxs-lookup"><span data-stu-id="34ea1-175">**FX_SUCCESS** (0x00) Successful directory attribute set</span></span>
- <span data-ttu-id="34ea1-176">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-176">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-177">**FX_NOT_FOUND** (0x04) Belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="34ea1-177">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="34ea1-178">**FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-178">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="34ea1-179">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-179">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-180">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="34ea1-180">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="34ea1-181">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-181">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-182">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-182">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-183">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-183">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-184">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-184">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-185">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="34ea1-185">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="34ea1-186">**FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-186">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="34ea1-187">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-187">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="34ea1-188">**FX_INVALID_ATTR** (0x19) Geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-188">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="34ea1-189">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-190">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-190">Allowed From</span></span>

<span data-ttu-id="34ea1-191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-192">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-192">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-193">See Also</span></span>

- <span data-ttu-id="34ea1-194">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-194">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-195">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-195">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-196">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-196">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-197">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-197">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-198">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-198">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-199">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-199">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-200">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-200">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-201">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-201">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-202">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-202">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-203">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-203">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-204">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-204">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-205">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-205">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-206">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-206">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-207">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-207">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-208">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-208">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-209">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-209">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-210">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-210">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-211">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-211">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-212">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-212">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-213">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-213">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_create"></a><span data-ttu-id="34ea1-214">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-214">fx_directory_create</span></span>

<span data-ttu-id="34ea1-215">Alt dizin oluşturur</span><span class="sxs-lookup"><span data-stu-id="34ea1-215">Creates subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-216">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-216">Prototype</span></span>

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-217">Description</span></span>

<span data-ttu-id="34ea1-218">Bu hizmet, geçerli varsayılan dizinde veya dizin adında sağlanan yolda bir alt dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-218">This service creates a subdirectory in the current default directory or in the path supplied in the directory name.</span></span> <span data-ttu-id="34ea1-219">Kök dizinden farklı olarak, alt dizinlerin tutabilecekleri dosya sayısı için bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-219">Unlike the root directory, subdirectories do not have a limit on the number of files they can hold.</span></span> <span data-ttu-id="34ea1-220">Kök dizin yalnızca önyükleme kaydı tarafından belirlenen girdi sayısını tutabilirler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-220">The root directory can only hold the number of entries determined by the boot record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-221">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-221">Input Parameters</span></span>

- <span data-ttu-id="34ea1-222">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-222">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-223">**directory_name**: Oluşturulacak dizinin adına yönelik işaretçi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-223">**directory_name**: Pointer to the name of the directory to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-224">Return Values</span></span>

- <span data-ttu-id="34ea1-225">**FX_SUCCESS** (0x00) başarılı dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-225">**FX_SUCCESS** (0x00) Successful directory create.</span></span>
- <span data-ttu-id="34ea1-226">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-226">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-227">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="34ea1-227">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="34ea1-228">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-228">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="34ea1-229">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-229">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-230">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-230">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-231">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-231">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-232">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-232">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-233">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-233">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-234">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="34ea1-234">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="34ea1-235">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-235">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="34ea1-236">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-236">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="34ea1-237">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-237">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="34ea1-238">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-238">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-239">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-239">Allowed From</span></span>

<span data-ttu-id="34ea1-240">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-240">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-241">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-242">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-242">See Also</span></span>

- <span data-ttu-id="34ea1-243">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-243">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-244">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-244">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-245">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-245">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-246">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-246">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-247">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-247">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-248">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-248">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-249">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-249">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-250">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-250">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-251">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-251">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-252">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-252">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-253">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-253">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-254">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-254">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-255">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-255">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-256">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-256">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-257">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-257">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-258">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-258">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-259">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-259">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-260">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-260">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-261">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-261">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-262">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-262">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_get"></a><span data-ttu-id="34ea1-263">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-263">fx_directory_default_get</span></span>

<span data-ttu-id="34ea1-264">Son varsayılan dizini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-264">Gets last default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-265">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-265">Prototype</span></span>

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-266">Description</span></span>

<span data-ttu-id="34ea1-267">Bu hizmet, ***fx_directory_default_set*** tarafından en son ayarlanan yola yönelik işaretçiyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-267">This service returns the pointer to the path last set by ***fx_directory_default_set***.</span></span> <span data-ttu-id="34ea1-268">Varsayılan dizin ayarlanmamışsa veya geçerli varsayılan dizin kök dizin ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-268">If the default directory has not been set or if the current default directory is the root directory, a value of FX_NULL is returned.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-269">*İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-269">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-270">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-270">Input Parameters</span></span>

- <span data-ttu-id="34ea1-271">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-271">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-272">**return_path_name**: son varsayılan dizin dizesinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-272">**return_path_name**: Pointer to the destination for the last default directory string.</span></span> <span data-ttu-id="34ea1-273">Varsayılan dizinin geçerli ayarı kök ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-273">A value of FX_NULL is returned if the current setting of the default directory is the root.</span></span> <span data-ttu-id="34ea1-274">Medya açıldığında, kök varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-274">When the media is opened, root is the default.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-275">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-275">Return Values</span></span>

- <span data-ttu-id="34ea1-276">**FX_SUCCESS** (0x00) başarılı varsayılan dizin Al</span><span class="sxs-lookup"><span data-stu-id="34ea1-276">**FX_SUCCESS** (0x00) Successful default directory get</span></span>
- <span data-ttu-id="34ea1-277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-278">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-278">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="34ea1-279">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-279">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-280">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-280">Allowed From</span></span>

<span data-ttu-id="34ea1-281">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-282">Example</span></span>

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a><span data-ttu-id="34ea1-283">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-283">See Also</span></span>

- <span data-ttu-id="34ea1-284">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-284">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-285">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-285">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-286">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-286">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-287">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-287">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-288">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-288">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-289">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-289">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-290">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-290">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-291">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-291">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-292">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-292">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-293">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-293">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-294">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-294">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-295">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-295">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-296">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-296">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-297">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-297">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-298">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-298">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-299">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-299">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-300">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-300">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-301">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-301">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-302">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-302">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-303">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-303">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_set"></a><span data-ttu-id="34ea1-304">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-304">fx_directory_default_set</span></span>

<span data-ttu-id="34ea1-305">Varsayılan dizini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-305">Sets default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-306">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-306">Prototype</span></span>

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-307">Description</span></span>

<span data-ttu-id="34ea1-308">Bu hizmet, medyanın varsayılan dizinini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-308">This service sets the default directory of the media.</span></span> <span data-ttu-id="34ea1-309">FX_NULL değeri sağlanırsa, varsayılan dizin medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-309">If a value of FX_NULL is supplied, the default directory is set to the media's root directory.</span></span> <span data-ttu-id="34ea1-310">Açıkça bir yol belirtmeyen tüm sonraki dosya işlemleri bu dizine varsayılan olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-310">All subsequent file operations that do not explicitly specify a path will default to this directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-311">*İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-311">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-312">*Uygulama tarafından sağlanan adlar için, FileX, \\ dizinler, alt dizinler ve dosya adlarına ayrı ters eğik çizgi () ve eğik çizgi (/) karakterlerini destekler. Ancak, FileX yalnızca uygulamaya döndürülen yollarda ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-312">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-313">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-313">Input Parameters</span></span>

- <span data-ttu-id="34ea1-314">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-314">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-315">**new_path_name**: yeni varsayılan dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-315">**new_path_name**: Pointer to new default directory name.</span></span> <span data-ttu-id="34ea1-316">Bir FX_NULL değeri sağlanırsa, medyanın varsayılan dizini medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-316">If a value of FX_NULL is supplied, the default directory of the media is set to the media's root directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-317">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-317">Return Values</span></span>

- <span data-ttu-id="34ea1-318">**FX_SUCCESS** (0x00) başarılı varsayılan dizin kümesi</span><span class="sxs-lookup"><span data-stu-id="34ea1-318">**FX_SUCCESS** (0x00)  Successful default directory set</span></span>
- <span data-ttu-id="34ea1-319">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-319">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-320">**FX_INVALID_PATH** (0x0D) yeni dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="34ea1-320">**FX_INVALID_PATH** (0x0D) New directory could not be found</span></span>
- <span data-ttu-id="34ea1-321">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-321">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-322">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-322">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-323">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-323">Allowed From</span></span>

<span data-ttu-id="34ea1-324">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-324">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-325">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-325">Example</span></span>

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-326">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-326">See Also</span></span>

- <span data-ttu-id="34ea1-327">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-327">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-328">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-328">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-329">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-329">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-330">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-330">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-331">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-331">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-332">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-332">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-333">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-333">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-334">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-334">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-335">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-335">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-336">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-336">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-337">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-337">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-338">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-338">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-339">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-339">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-340">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-340">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-341">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-341">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-342">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-342">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-343">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-343">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-344">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-344">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-345">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-345">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-346">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-346">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_delete"></a><span data-ttu-id="34ea1-347">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-347">fx_directory_delete</span></span>

<span data-ttu-id="34ea1-348">Alt dizini siler</span><span class="sxs-lookup"><span data-stu-id="34ea1-348">Deletes subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-349">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-349">Prototype</span></span>

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-350">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-350">Description</span></span>

<span data-ttu-id="34ea1-351">Bu hizmet belirtilen dizini siler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-351">This service deletes the specified directory.</span></span> <span data-ttu-id="34ea1-352">Silmek için dizinin boş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="34ea1-352">Note that the directory must be empty to delete it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-353">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-353">Input Parameters</span></span>

- <span data-ttu-id="34ea1-354">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-354">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-355">**directory_name**: silinecek dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-355">**directory_name**: Pointer to name of directory to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-356">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-356">Return Values</span></span>

- <span data-ttu-id="34ea1-357">**FX_SUCCESS** (0x00) başarılı dizin silme</span><span class="sxs-lookup"><span data-stu-id="34ea1-357">**FX_SUCCESS** (0x00) Successful directory delete</span></span>
- <span data-ttu-id="34ea1-358">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-358">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-359">**FX_NOT_FOUND** (0x04) belirtilen dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="34ea1-359">**FX_NOT_FOUND** (0x04) Specified directory was not found</span></span>
- <span data-ttu-id="34ea1-360">**FX_DIR_NOT_EMPTY** (0x10) belirtilen dizin boş değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-360">**FX_DIR_NOT_EMPTY** (0x10) Specified directory is not empty</span></span>
- <span data-ttu-id="34ea1-361">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-361">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-362">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="34ea1-362">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="34ea1-363">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-363">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-364">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-364">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-365">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-365">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-366">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-366">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-367">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="34ea1-367">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="34ea1-368">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-368">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="34ea1-369">**FX_NOT_DIRECTORY** (0x0E) dizin girişi değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-369">**FX_NOT_DIRECTORY** (0x0E) Not a directory entry</span></span>
- <span data-ttu-id="34ea1-370">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-370">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="34ea1-371">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-371">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-372">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-372">Allowed From</span></span>

<span data-ttu-id="34ea1-373">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-373">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-374">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-374">Example</span></span>
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-375">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-375">See Also</span></span>

- <span data-ttu-id="34ea1-376">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-376">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-377">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-377">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-378">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-378">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-379">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-379">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-380">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-380">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-381">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-381">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-382">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-382">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-383">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-383">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-384">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-384">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-385">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-385">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-386">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-386">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-387">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-387">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-388">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-388">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-389">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-389">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-390">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-390">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-391">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-391">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-392">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-392">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-393">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-393">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-394">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-394">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-395">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-395">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_entry_find"></a><span data-ttu-id="34ea1-396">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-396">fx_directory_first_entry_find</span></span>

<span data-ttu-id="34ea1-397">İlk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-397">Gets first directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-398">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-398">Prototype</span></span>

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-399">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-399">Description</span></span>

<span data-ttu-id="34ea1-400">Bu hizmet, varsayılan dizindeki ilk giriş adını alır ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-400">This service retrieves the first entry name in the default directory and copies it to the specified destination.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-401">*Belirtilen hedef, FX_MAX_LONG_NAME_LEN tarafından tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır **.***</span><span class="sxs-lookup"><span data-stu-id="34ea1-401">*The specified destination must be large enough to hold the maximum sized FileX name, as defined by **FX_MAX_LONG_NAME_LEN.***</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-402">*Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-402">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-403">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-403">Input Parameters</span></span>

- <span data-ttu-id="34ea1-404">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-404">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-405">**return_entry_name**: varsayılan dizindeki ilk giriş adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-405">**return_entry_name**: Pointer to destination for the first entry name in the default directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-406">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-406">Return Values</span></span>

- <span data-ttu-id="34ea1-407">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="34ea1-407">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="34ea1-408">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-408">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-409">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-409">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="34ea1-410">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-410">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-411">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-411">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-412">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-412">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-413">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-413">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-414">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-414">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer</span></span>
- <span data-ttu-id="34ea1-415">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-415">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-416">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-416">Allowed From</span></span>

<span data-ttu-id="34ea1-417">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-417">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-418">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-418">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-419">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-419">See Also</span></span>

- <span data-ttu-id="34ea1-420">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-420">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-421">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-421">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-422">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-422">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-423">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-423">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-424">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-424">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-425">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-425">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-426">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-426">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-427">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-427">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-428">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-428">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-429">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-429">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-430">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-430">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-431">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-431">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-432">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-432">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-433">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-433">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-434">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-434">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-435">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-435">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-436">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-436">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-437">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-437">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-438">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-438">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-439">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-439">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="34ea1-440">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-440">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="34ea1-441">Tüm bilgileri içeren ilk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-441">Gets first directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-442">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-442">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="34ea1-443">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-443">Input Parameters</span></span>

- <span data-ttu-id="34ea1-444">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-444">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-445">**directory_name**: bir dizin girişi adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-445">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="34ea1-446">En az FX_MAX_LONG_NAME_LEN kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-446">Must be at least as big as FX_MAX_LONG_NAME_LEN.</span></span>
- <span data-ttu-id="34ea1-447">**öznitelikler**: null olmayan, girişin özniteliklerinin yerleştirileceği hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-447">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.</span></span> <span data-ttu-id="34ea1-448">Öznitelikler, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="34ea1-448">The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="34ea1-449">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-449">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="34ea1-450">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-450">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="34ea1-451">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="34ea1-451">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="34ea1-452">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="34ea1-452">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="34ea1-453">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="34ea1-453">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="34ea1-454">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="34ea1-454">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="34ea1-455">**Boyut**: null olmayan, girdinin bayt cinsinden boyutu için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-455">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="34ea1-456">**yıl**: null olmayan, girişin değiştirilme yılından hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-456">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="34ea1-457">**ay**: null olmayan, girişin değiştirilme ayı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-457">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="34ea1-458">**gün**: null olmayan, girişin değiştirilme günü için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-458">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="34ea1-459">**saat**: null olmayan, girişin değiştirilme saati için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-459">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="34ea1-460">**dakika**: null olmayan, girişin değiştirilme dakikası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-460">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="34ea1-461">**ikinci**: null olmayan, girişin değiştirilme saniyesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-461">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-462">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-462">Return Values</span></span>

- <span data-ttu-id="34ea1-463">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="34ea1-463">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="34ea1-464">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-464">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-465">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-465">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="34ea1-466">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-466">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-467">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="34ea1-467">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="34ea1-468">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-468">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-469">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-469">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-470">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-470">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-471">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-471">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-472">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="34ea1-472">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="34ea1-473">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-473">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="34ea1-474">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-474">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-475">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-475">Allowed From</span></span>

<span data-ttu-id="34ea1-476">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-476">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-477">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-477">Example</span></span>

```c
FX_MEDIA     my_media;
UINT         status;
CHAR         entry_name[FX_MAX_LONG_NAME_LEN];
UINT         attributes;
ULONG        size;
UINT         year;
UINT         month;
UINT         day;
UINT         hour;
UINT         minute;
UINT         second;
/* Get the first directory entry in the default directory with full information. */
status = fx_directory_first_full_entry_find(&my_media, entry_name,
    &attributes, &size, &year, &month, &day, &hour, &minute, &second);

/* If status equals FX_SUCCESS, the entry's information is in the local variables. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-478">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-478">See Also</span></span>

- <span data-ttu-id="34ea1-479">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-479">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-480">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-480">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-481">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-481">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-482">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-482">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-483">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-483">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-484">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-484">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-485">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-485">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-486">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-486">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-487">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-487">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-488">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-488">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-489">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-489">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-490">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-490">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-491">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-491">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-492">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-492">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-493">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-493">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-494">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-494">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-495">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-495">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-496">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-496">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-497">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-497">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-498">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-498">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_information_get"></a><span data-ttu-id="34ea1-499">fx_directory_information_get:</span><span class="sxs-lookup"><span data-stu-id="34ea1-499">fx_directory_information_get:</span></span>

<span data-ttu-id="34ea1-500">Dizin girişi bilgilerini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-500">Gets directory entry information</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-501">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-501">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="34ea1-502">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-502">Input Parameters</span></span>

- <span data-ttu-id="34ea1-503">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-503">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-504">**directory_name:** Dizin girişinin adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-504">**directory_name**: Pointer to name of the directory entry.</span></span>
- <span data-ttu-id="34ea1-505">**attributes:** Öznitelikler için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-505">**attributes**: Pointer to the destination for the attributes.</span></span>
- <span data-ttu-id="34ea1-506">**size:** Boyut için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-506">**size**: Pointer to the destination for the size.</span></span>
- <span data-ttu-id="34ea1-507">**year:** Yılın hedefine işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-507">**year**: Pointer to the destination for the year.</span></span>
- <span data-ttu-id="34ea1-508">**month:** Ay için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-508">**month**: Pointer to the destination for the month.</span></span>
- <span data-ttu-id="34ea1-509">**day:** Günün hedefine işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-509">**day**: Pointer to the destination for the day.</span></span>
- <span data-ttu-id="34ea1-510">**hour:** Bir saat için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-510">**hour**: Pointer to the destination for the hour.</span></span>
- <span data-ttu-id="34ea1-511">**minute:** Dakika için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-511">**minute**: Pointer to the destination for the minute.</span></span>
- <span data-ttu-id="34ea1-512">**second:** saniye için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-512">**second**: Pointer to the destination for the second.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-513">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-513">Return Values</span></span>

- <span data-ttu-id="34ea1-514">**FX_SUCCESS** (0x00) Başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="34ea1-514">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="34ea1-515">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-515">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-516">**FX_NOT_FOUND** (0x04) Belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="34ea1-516">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="34ea1-517">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-517">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-518">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="34ea1-518">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="34ea1-519">**FX_FILE _CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-519">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-520">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-520">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-521">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-521">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-522">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-522">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-523">**FX_PTR_ERROR** (0x18) Geçersiz medya veya hedef işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-523">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="34ea1-524">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-524">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-525">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-525">Allowed From</span></span>

<span data-ttu-id="34ea1-526">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-526">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-527">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-527">Example</span></span>

```c
FX_MEDIA     my_media;
UINT         status; attributes; year; month; day;
CHAR         entry_name[FX_MAX_LONG_NAME_LEN];
ULONG        size;
UINT         hour; minute; second;
/* Retrieve information about the directory entry "myfile.txt".*/
status = fx_directory_information_get(&my_media, "myfile.txt", &attributes, &size,
                                      &year, &month, &day,
                                      &hour, &minute, &second);
/* If status equals FX_SUCCESS, the directory entry information is available in the local variables. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-528">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-528">See Also</span></span>

- <span data-ttu-id="34ea1-529">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-529">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-530">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-530">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-531">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-531">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-532">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-532">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-533">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-533">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-534">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-534">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-535">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-535">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-536">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-536">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-537">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-537">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-538">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-538">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-539">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-539">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-540">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-540">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-541">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-541">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-542">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-542">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-543">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-543">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-544">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-544">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-545">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-545">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-546">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-546">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-547">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-547">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-548">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-548">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_clear"></a><span data-ttu-id="34ea1-549">fx_directory_local_path_clear:</span><span class="sxs-lookup"><span data-stu-id="34ea1-549">fx_directory_local_path_clear:</span></span>

<span data-ttu-id="34ea1-550">Varsayılan yerel yolu temizler</span><span class="sxs-lookup"><span data-stu-id="34ea1-550">Clears default local path</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-551">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-551">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="34ea1-552">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-552">Description</span></span>

<span data-ttu-id="34ea1-553">Bu hizmet, çağıran iş parçacığı için ayarlanmış önceki yerel yolu temizler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-553">This service clears the previous local path set up for the calling thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-554">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-554">Input Parameters</span></span>

- <span data-ttu-id="34ea1-555">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-555">**media_ptr**: Pointer to a previously opened media.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-556">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-556">Return Values</span></span>

- <span data-ttu-id="34ea1-557">**FX_SUCCESS** (0x00) Başarılı yerel yol temiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-557">**FX_SUCCESS** (0x00) Successful local path clear.</span></span>
- <span data-ttu-id="34ea1-558">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-558">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="34ea1-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlı</span><span class="sxs-lookup"><span data-stu-id="34ea1-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined</span></span>
- <span data-ttu-id="34ea1-560">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-560">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-561">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-561">Allowed From</span></span>

<span data-ttu-id="34ea1-562">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-562">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-563">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-563">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-564">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-564">See Also</span></span>

- <span data-ttu-id="34ea1-565">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-565">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-566">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-566">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-567">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-567">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-568">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-568">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-569">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-569">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-570">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-570">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-571">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-571">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-572">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-572">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-573">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-573">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-574">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-574">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-575">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-575">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-576">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-576">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-577">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-577">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-578">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-578">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-579">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-579">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-580">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-580">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-581">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-581">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-582">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-582">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-583">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-583">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-584">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-584">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_get"></a><span data-ttu-id="34ea1-585">fx_directory_local_path_get:</span><span class="sxs-lookup"><span data-stu-id="34ea1-585">fx_directory_local_path_get:</span></span>

<span data-ttu-id="34ea1-586">Geçerli yerel yol dizesini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-586">Gets the current local path string</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-587">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-587">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-588">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-588">Description</span></span>

<span data-ttu-id="34ea1-589">Bu hizmet, belirtilen medyanın yerel yol işaretçisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-589">This service returns the local path pointer of the specified media.</span></span> <span data-ttu-id="34ea1-590">Yerel yol kümesi yoksa, çağırana NULL döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-590">If there is no local path set, a NULL is returned to the caller.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-591">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-591">Input Parameters</span></span>

- <span data-ttu-id="34ea1-592">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-592">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-593">**return_path_name:** Depoilecek yerel yol dizesi için hedef dize işaretçisinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-593">**return_path_name**: Pointer to the destination string pointer for the local path string to be stored.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-594">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-594">Return Values</span></span>

- <span data-ttu-id="34ea1-595">**FX_SUCCESS** (0x00) Başarılı yerel yol get.</span><span class="sxs-lookup"><span data-stu-id="34ea1-595">**FX_SUCCESS** (0x00) Successful local path get.</span></span>
- <span data-ttu-id="34ea1-596">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-596">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="34ea1-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="34ea1-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="34ea1-598">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-598">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>


### <a name="allowed-from"></a><span data-ttu-id="34ea1-599">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-599">Allowed From</span></span>

<span data-ttu-id="34ea1-600">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-600">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-601">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-601">Example</span></span>

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-602">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-602">See Also</span></span>

- <span data-ttu-id="34ea1-603">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-603">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-604">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-604">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-605">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-605">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-606">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-606">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-607">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-607">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-608">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-608">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-609">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-609">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-610">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-610">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-611">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-611">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-612">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-612">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-613">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-613">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-614">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-614">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-615">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-615">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-616">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-616">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-617">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-617">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-618">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-618">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-619">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-619">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-620">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-620">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-621">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-621">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-622">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-622">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_restore"></a><span data-ttu-id="34ea1-623">fx_directory_local_path_restore:</span><span class="sxs-lookup"><span data-stu-id="34ea1-623">fx_directory_local_path_restore:</span></span>

<span data-ttu-id="34ea1-624">Önceki yerel yolu geri yükleme</span><span class="sxs-lookup"><span data-stu-id="34ea1-624">Restores previous local path</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-625">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-625">Prototype</span></span>

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a><span data-ttu-id="34ea1-626">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-626">Description</span></span>

<span data-ttu-id="34ea1-627">Bu hizmet daha önce ayarlanmış bir yerel yolu geri yüklemektedir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-627">This service restores a previously set local path.</span></span> <span data-ttu-id="34ea1-628">Bu yerel yolda yapılan dizin arama konumu da geri yüklenir ve bu da bu yordamı uygulama tarafından yapılan yinelemeli dizin geçişlerinde yararlı yapar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-628">The directory search position made on this local path is also restored, which makes this routine useful in recursive directory traversals by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-629">*Her yerel yol, varsayılan olarak 256 **FX_MAXIMUM_PATH** bir yerel yol dizesi içerir. Bu iç yol dizesi FileX tarafından kullanılmaz ve yalnızca uygulamanın kullanımı için sağlanır. Bu **FX_LOCAL_PATH** yerel değişken olarak bildirilemezse, kullanıcılar bu yapının boyutuna göre büyüyen yığından dikkatli olması gerekir. Kullanıcıların dosya boyutunu azaltması ve **FileX FX_MAXIMUM_PATH** yeniden oluşturması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-629">*Each local path contains a local path string of **FX_MAXIMUM_PATH** in size, which by default is 256 characters. This internal path string is not used by FileX and is provided only for the application's use. If **FX_LOCAL_PATH** is going to be declared as a local variable, users should beware of the stack growing by the size of this structure. Users are welcome to reduce the size of **FX_MAXIMUM_PATH** and rebuild the FileX library source.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-630">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-630">Input Parameters</span></span>

- <span data-ttu-id="34ea1-631">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-631">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-632">**local_path_ptr:** Önceden ayarlanmış yerel yolun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-632">**local_path_ptr**: Pointer to the previously set local path.</span></span> <span data-ttu-id="34ea1-633">Bu işaretçinin daha önce kullanılan ve hala bozulmamış bir yerel yola işaret etmelerinden emin olmak çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-633">It's very important to ensure that this pointer does indeed point to a previously used and still intact local path.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-634">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-634">Return Values</span></span>

- <span data-ttu-id="34ea1-635">**FX_SUCCESS** (0x00) Başarılı yerel yol geri yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-635">**FX_SUCCESS** (0x00) Successful local path restore.</span></span>
- <span data-ttu-id="34ea1-636">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open.</span></span>
- <span data-ttu-id="34ea1-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined.</span></span>
- <span data-ttu-id="34ea1-638">**FX_PTR_ERROR** (0x18) Geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-638">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-639">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-639">Allowed From</span></span>

<span data-ttu-id="34ea1-640">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-640">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-641">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-641">Example</span></span>

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-642">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-642">See Also</span></span>

- <span data-ttu-id="34ea1-643">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-643">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-644">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-644">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-645">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-645">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-646">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-646">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-647">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-647">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-648">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-648">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-649">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-649">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-650">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-650">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-651">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-651">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-652">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-652">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-653">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-653">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-654">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-654">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-655">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-655">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-656">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-656">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-657">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-657">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-658">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-658">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-659">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-659">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-660">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-660">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-661">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-661">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-662">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-662">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_set"></a><span data-ttu-id="34ea1-663">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-663">fx_directory_local_path_set</span></span>

<span data-ttu-id="34ea1-664">İş parçacığına özgü bir yerel yol ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-664">Sets up a thread-specific local path</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-665">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-665">Prototype</span></span>

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-666">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-666">Description</span></span>

<span data-ttu-id="34ea1-667">Bu hizmet , \* new_path_string _ tarafından belirtilen iş **parçacığına özgü bir yol** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-667">This service sets up a thread-specific path as specified by the \***new_path_string** _.</span></span> <span data-ttu-id="34ea1-668">Bu yordam başarıyla tamamlandıktan sonra, _ *_local_path_ptr_*\* içinde depolanan yerel yol bilgileri, bu iş parçacığı tarafından yapılan tüm dosya ve dizin işlemleri için genel medya yolundan önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-668">After successful completion of this routine, the local path information stored in _ *_local_path_ptr_*\* will take precedence over the global media path for all file and directory operations made by this thread.</span></span> <span data-ttu-id="34ea1-669">Bunun sistem üzerindeki diğer iş parçacığı üzerinde hiçbir etkisi olmaz</span><span class="sxs-lookup"><span data-stu-id="34ea1-669">This will have no impact on any other thread in the system</span></span> 
> [!IMPORTANT]
> <span data-ttu-id="34ea1-670">*Yerel yol dizesinin varsayılan boyutu 256 karakterdir; fx_api.h **dosyasındaki** FX_MAXIMUM_PATH **değiştirerek** ve FileX kitaplığının tamamını yeniden oluşturarak değiştirilebilir. Karakter dizesi yolu uygulama için korunur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-670">*The default size of the local path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-671">*Uygulama tarafından sağlanan adlar için FileX hem ters eğik çizgi ( ) hem de eğik çizgi (/) karakterlerini ayrı dizinlere, alt dizinlere ve dosya \\ adlarına destekler. Ancak FileX, uygulamaya döndürülen yollarda yalnızca ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-671">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-672">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-672">Input Parameters</span></span>

- <span data-ttu-id="34ea1-673">**media_ptr:** Önceden açılmış olan medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-673">**media_ptr**: Pointer to the previously opened media.</span></span>
- <span data-ttu-id="34ea1-674">**local_path_ptr:** İş parçacığına özgü yerel yol bilgilerini tutmak için hedef.</span><span class="sxs-lookup"><span data-stu-id="34ea1-674">**local_path_ptr**: Destination for holding the thread-specific local path information.</span></span> <span data-ttu-id="34ea1-675">Bu yapının adresi gelecekte yerel yol geri yükleme işlevine sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-675">The address of this structure may be supplied to the local path restore function in the future.</span></span>
- <span data-ttu-id="34ea1-676">**new_path_name:** Kurulumun yerel yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-676">**new_path_name**: Specifies the local path to setup.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-677">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-677">Return Values</span></span>

- <span data-ttu-id="34ea1-678">**FX_SUCCESS** (0x00) Başarılı varsayılan dizin kümesi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-678">**FX_SUCCESS** (0x00) Successful default directory set.</span></span>
- <span data-ttu-id="34ea1-679">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-679">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="34ea1-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="34ea1-681">**FX_INVALID_PATH** (0x0D) Yeni dizin bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-681">**FX_INVALID_PATH** (0x0D) New directory could not be found.</span></span>
- <span data-ttu-id="34ea1-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH is defined.</span></span>
- <span data-ttu-id="34ea1-683">**FX_PTR_ERROR** (0x18) Geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-683">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-684">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-684">Allowed From</span></span>

<span data-ttu-id="34ea1-685">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-685">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-686">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-686">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
FX_LOCAL_PATH     my_previous_local_path;
/* Set the local path to \abc\def\ghi. */
status = fx_directory_local_path_set (&my_media,&local_path,"\\abc\\def\\ghi");

/* If status equals FX_SUCCESS, the default directory for this thread
is \abc\def\ghi. All subsequent file operations that do not explicitly
specify a path will default to this directory. Note that the character
"\" serves as an escape character in a string. To represent the
character "\", use the construct "\\".*/
```

### <a name="see-also"></a><span data-ttu-id="34ea1-687">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-687">See Also</span></span>

- <span data-ttu-id="34ea1-688">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-688">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-689">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-689">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-690">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-690">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-691">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-691">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-692">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-692">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-693">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-693">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-694">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-694">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-695">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-695">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-696">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-696">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-697">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-697">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-698">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-698">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-699">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-699">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-700">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-700">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-701">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-701">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-702">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-702">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-703">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-703">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-704">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-704">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-705">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-705">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-706">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-706">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-707">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-707">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get"></a><span data-ttu-id="34ea1-708">fx_directory_long_name_get:</span><span class="sxs-lookup"><span data-stu-id="34ea1-708">fx_directory_long_name_get:</span></span>

<span data-ttu-id="34ea1-709">Kısa addan uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-709">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-710">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-710">Prototype</span></span>

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-711">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-711">Description</span></span>

<span data-ttu-id="34ea1-712">Bu hizmet, sağlanan kısa (8.3 biçim) adıyla ilişkili uzun adı (varsa) verir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-712">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="34ea1-713">Kısa ad bir dosya adı veya dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-713">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-714">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-714">Input Parameters</span></span>

- <span data-ttu-id="34ea1-715">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-715">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-716">**short_name:** Kaynak kısa adının işaretçisi (8.3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="34ea1-716">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="34ea1-717">**long_name:** Uzun ad için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-717">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="34ea1-718">Uzun ad yoksa kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-718">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="34ea1-719">Uzun adın hedefinin, uzun karakterlerin tutulacak kadar büyük FX_MAX_LONG_NAME_LEN unutmayın.</span><span class="sxs-lookup"><span data-stu-id="34ea1-719">Note that the destination for the long name must be large enough to hold FX_MAX_LONG_NAME_LEN characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-720">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-720">Return Values</span></span>

- <span data-ttu-id="34ea1-721">**FX_SUCCESS** (0x00) Başarılı uzun ad get</span><span class="sxs-lookup"><span data-stu-id="34ea1-721">**FX_SUCCESS** (0x00) Successful long name get</span></span>
- <span data-ttu-id="34ea1-722">**FX_NOT_FOUND** (0x04) Kısa ad bulunamadı</span><span class="sxs-lookup"><span data-stu-id="34ea1-722">**FX_NOT_FOUND** (0x04) Short name was not found</span></span>
- <span data-ttu-id="34ea1-723">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="34ea1-723">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="34ea1-724">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="34ea1-724">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="34ea1-725">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-725">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-726">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="34ea1-726">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="34ea1-727">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-727">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="34ea1-728">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-728">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-729">**FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-729">**FX_PTR_ERROR** (0x18) Invalid media or name pointer</span></span>
- <span data-ttu-id="34ea1-730">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-730">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-731">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-731">Allowed From</span></span>

<span data-ttu-id="34ea1-732">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-733">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-733">Example</span></span>

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-734">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-734">See Also</span></span>

- <span data-ttu-id="34ea1-735">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-735">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-736">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-736">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-737">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-737">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-738">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-738">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-739">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-739">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-740">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-740">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-741">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-741">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-742">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-742">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-743">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-743">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-744">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-744">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-745">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-745">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-746">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-746">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-747">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-747">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-748">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-748">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-749">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-749">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-750">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-750">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-751">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-751">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-752">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-752">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-753">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-753">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-754">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-754">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get_extended"></a><span data-ttu-id="34ea1-755">fx_directory_long_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="34ea1-755">fx_directory_long_name_get_extended</span></span>

<span data-ttu-id="34ea1-756">Kısa addan uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-756">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-757">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-757">Prototype</span></span>

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="34ea1-758">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-758">Description</span></span>

<span data-ttu-id="34ea1-759">Bu hizmet, sağlanan kısa (8.3 biçim) adıyla ilişkili uzun adı (varsa) verir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-759">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="34ea1-760">Kısa ad bir dosya adı veya dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-760">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-761">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-761">Input Parameters</span></span>

- <span data-ttu-id="34ea1-762">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-762">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-763">**short_name:** Kaynak kısa adının işaretçisi (8.3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="34ea1-763">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="34ea1-764">**long_name:** Uzun ad için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-764">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="34ea1-765">Uzun ad yoksa kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-765">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="34ea1-766">Not: Uzun adın hedefi, uzun karakterlerin tutulacak **FX_MAX_LONG_NAME_LEN** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-766">Note: Destination for the long name must be large enough to hold **FX_MAX_LONG_NAME_LEN** characters.</span></span>
- <span data-ttu-id="34ea1-767">**long_file_name_buffer_length:** Uzun ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-767">**long_file_name_buffer_length**: Length of the long name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-768">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-768">Return Values</span></span>

- <span data-ttu-id="34ea1-769">**FX_SUCCESS** (0x00) Başarılı uzun ad get.</span><span class="sxs-lookup"><span data-stu-id="34ea1-769">**FX_SUCCESS** (0x00) Successful long name get.</span></span>
- <span data-ttu-id="34ea1-770">**FX_NOT_FOUND** (0x04) Kısa ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-770">**FX_NOT_FOUND** (0x04) Short name was not found.</span></span>
- <span data-ttu-id="34ea1-771">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-771">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-772">**FX_MEDIA_INVALID** (0x02) Geçersiz medya.</span><span class="sxs-lookup"><span data-stu-id="34ea1-772">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-773">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-773">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-774">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-774">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-775">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-775">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-776">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-776">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="34ea1-777">**FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-777">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="34ea1-778">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-778">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-779">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-779">Allowed From</span></span>

<span data-ttu-id="34ea1-780">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-780">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-781">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-781">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name, sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-782">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-782">See Also</span></span>

- <span data-ttu-id="34ea1-783">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-783">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-784">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-784">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-785">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-785">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-786">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-786">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-787">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-787">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-788">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-788">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-789">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-789">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-790">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-790">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-791">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-791">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-792">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-792">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-793">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-793">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-794">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-794">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-795">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-795">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-796">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-796">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-797">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-797">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-798">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-798">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-799">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-799">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-800">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-800">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-801">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-801">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-802">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-802">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_name_test"></a><span data-ttu-id="34ea1-803">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-803">fx_directory_name_test</span></span>

<span data-ttu-id="34ea1-804">Dizin için testler</span><span class="sxs-lookup"><span data-stu-id="34ea1-804">Tests for directory</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-805">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-805">Prototype</span></span>

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-806">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-806">Description</span></span>

<span data-ttu-id="34ea1-807">Bu hizmet, belirtilen adın bir dizin olup olmadığını sınar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-807">This service tests whether or not the supplied name is a directory.</span></span> <span data-ttu-id="34ea1-808">Öyleyse, bir FX_SUCCESS döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-808">If so, a FX_SUCCESS is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-809">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-809">Input Parameters</span></span>

- <span data-ttu-id="34ea1-810">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-810">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-811">**directory_name**: Dizin girişinin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-811">**directory_name**: Pointer to name of the directory entry.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-812">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-812">Return Values</span></span>

- <span data-ttu-id="34ea1-813">**FX_SUCCESS** (0x00) sağlanan ad bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-813">**FX_SUCCESS** (0x00) Supplied name is a directory.</span></span>
- <span data-ttu-id="34ea1-814">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-814">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="34ea1-815">**FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-815">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="34ea1-816">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="34ea1-816">**FX_NOT_DIRECTORY** (0x0E)  Entry is not a directory</span></span>
- <span data-ttu-id="34ea1-817">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-817">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-818">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-818">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-819">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-819">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-820">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-820">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-821">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-821">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-822">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-822">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="34ea1-823">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-823">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="34ea1-824">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-824">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-825">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-825">Allowed From</span></span>

<span data-ttu-id="34ea1-826">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-826">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-827">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-827">Example</span></span>

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-828">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-828">See Also</span></span>

- <span data-ttu-id="34ea1-829">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-829">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-830">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-830">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-831">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-831">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-832">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-832">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-833">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-833">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-834">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-834">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-835">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-835">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-836">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-836">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-837">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-837">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-838">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-838">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-839">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-839">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-840">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-840">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-841">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-841">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-842">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-842">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-843">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-843">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-844">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-844">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-845">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-845">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-846">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-846">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-847">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-847">fx_unicode_directory_create</span></span>

## <a name="fx_directory_next_entry_find"></a><span data-ttu-id="34ea1-848">fx_directory_next_entry_find:</span><span class="sxs-lookup"><span data-stu-id="34ea1-848">fx_directory_next_entry_find:</span></span>

<span data-ttu-id="34ea1-849">Sonraki dizin girişini seçer</span><span class="sxs-lookup"><span data-stu-id="34ea1-849">Picks up next directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-850">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-850">Prototype</span></span>

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-851">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-851">Description</span></span>

<span data-ttu-id="34ea1-852">Bu hizmet, geçerli varsayılan dizindeki bir sonraki giriş adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-852">This service returns the next entry name in the current default directory.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-853">*Yerel olmayan bir yol kullanılıyorsa, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek için de önemlidir (bir ThreadX semaforu veya iş parçacığı öncelik düzeyiyle). Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-853">*If using a non-local path, it is also important to prevent (with a ThreadX semaphore or thread priority level) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-854">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-854">Input Parameters</span></span>

- <span data-ttu-id="34ea1-855">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-855">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-856">**return_entry_name**: varsayılan dizindeki bir sonraki giriş adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-856">**return_entry_name**: Pointer to destination for the next entry name in the default directory.</span></span> <span data-ttu-id="34ea1-857">Bu işaretçinin işaret ettiği arabellek, **_FX_MAX_LONG_NAME_LEN_** tarafından tanımlanan en büyük FileX adı boyutunu tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-857">The buffer this pointer points to must be large enough to hold the maximum size of FileX name, defined by **_FX_MAX_LONG_NAME_LEN_**.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-858">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-858">Return Values</span></span>

- <span data-ttu-id="34ea1-859">**FX_SUCCESS** (0x00) başarılı bir sonraki giriş bul</span><span class="sxs-lookup"><span data-stu-id="34ea1-859">**FX_SUCCESS** (0x00) Successful next entry find</span></span>
- <span data-ttu-id="34ea1-860">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-860">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-861">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-861">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="34ea1-862">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-862">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-863">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-863">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-864">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-864">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-865">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-865">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-866">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-866">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-867">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-867">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-868">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-868">**FX_CALLER_ERROR** (0x20)     Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-869">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-869">Allowed From</span></span>

<span data-ttu-id="34ea1-870">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-871">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-871">Example</span></span>

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-872">See Also</span></span>

- <span data-ttu-id="34ea1-873">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-873">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-874">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-874">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-875">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-875">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-876">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-876">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-877">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-877">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-878">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-878">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-879">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-879">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-880">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-880">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-881">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-881">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-882">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-882">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-883">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-883">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-884">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-884">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-885">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-885">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-886">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-886">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-887">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-887">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-888">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-888">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-889">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-889">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-890">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-890">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-891">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-891">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-892">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-892">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="34ea1-893">fx_directory_next_full_entry_find:</span><span class="sxs-lookup"><span data-stu-id="34ea1-893">fx_directory_next_full_entry_find:</span></span>

<span data-ttu-id="34ea1-894">Tam bilgi içeren bir sonraki dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-894">Gets next directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-895">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-895">Prototype</span></span>

```c
UINT fx_directory_next_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes, 
    ULONG *size,
    UINT *year, 
    UINT *month, 
    UINT *day,
    UINT *hour, 
    UINT *minute, 
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="34ea1-896">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-896">Description</span></span>

<span data-ttu-id="34ea1-897">Bu hizmet, varsayılan dizindeki bir sonraki giriş adını alır ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-897">This service retrieves the next entry name in the default directory and copies it to the specified destination.</span></span> <span data-ttu-id="34ea1-898">Ayrıca, ek giriş parametreleriyle belirtilen girdi hakkında tam bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-898">It also returns full information about the entry as specified by the additional input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-899">\* Belirtilen hedef, \* \* \* FX_MAX_LONG_NAME_LEN \* \* \* \* ile tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır</span><span class="sxs-lookup"><span data-stu-id="34ea1-899">\*The specified destination must be large enough to hold the maximum sized FileX name, as defined by \*\*\*FX_MAX_LONG_NAME_LEN\*\*\*\*</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-900">*Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-900">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-901">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-901">Input Parameters</span></span>

- <span data-ttu-id="34ea1-902">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-902">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-903">**directory_name**: bir dizin girişi adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-903">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="34ea1-904">En az **FX_MAX_LONG_NAME_LEN** kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-904">Must be at least as big as **FX_MAX_LONG_NAME_LEN**.</span></span>
- <span data-ttu-id="34ea1-905">**öznitelikler**: null olmayan, girişin özniteliklerinin yerleştirileceği hedefe yönelik işaretçi. Öznitelikler, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="34ea1-905">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="34ea1-906">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-906">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="34ea1-907">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-907">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="34ea1-908">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="34ea1-908">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="34ea1-909">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="34ea1-909">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="34ea1-910">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="34ea1-910">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="34ea1-911">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="34ea1-911">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="34ea1-912">**Boyut**: null olmayan, girdinin bayt cinsinden boyutu için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-912">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="34ea1-913">**ay**: null olmayan, girişin değiştirilme ayı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-913">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="34ea1-914">**yıl**: null olmayan, girişin değiştirilme yılından hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-914">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="34ea1-915">**gün**: null olmayan, girişin değiştirilme günü için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-915">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="34ea1-916">**saat**: null olmayan, girişin değiştirilme saati için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-916">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="34ea1-917">**dakika**: null olmayan, girişin değiştirilme dakikası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-917">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="34ea1-918">**ikinci**: null olmayan, girişin değiştirilme saniyesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-918">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-919">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-919">Return Values</span></span>

- <span data-ttu-id="34ea1-920">**FX_SUCCESS** (0x00) başarılı Dizin sonraki giriş bul.</span><span class="sxs-lookup"><span data-stu-id="34ea1-920">**FX_SUCCESS** (0x00) Successful directory next entry find.</span></span>
- <span data-ttu-id="34ea1-921">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-921">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-922">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-922">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="34ea1-923">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-923">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-924">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-924">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-925">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-925">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-926">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-926">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-927">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-927">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="34ea1-928">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-928">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-929">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya tüm GIRIŞ parametreleri null.</span><span class="sxs-lookup"><span data-stu-id="34ea1-929">**FX_PTR_ERROR** (0x18) Invalid media pointer or all input parameters are NULL.</span></span>
- <span data-ttu-id="34ea1-930">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-930">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-931">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-931">Allowed From</span></span>

<span data-ttu-id="34ea1-932">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-932">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-933">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-933">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
CHAR        entry_name[FX_MAX_LONG_NAME_LEN];
UINT        attributes;
ULONG       size;
UINT        year;
UINT        month;
UINT        day;
UINT        hour;
UINT        minute;
UINT        second;

/* Get the next directory entry in the default directory with full information. */
status = fx_directory_next_full_entry_find(&my_media, entry_name, &attributes, &size,
                                           &year, &month, &day,
                                           &hour, &minute, &second);

/* If status equals FX_SUCCESS, the entry's information is in the local variables. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-934">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-934">See Also</span></span>

- <span data-ttu-id="34ea1-935">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-935">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-936">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-936">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-937">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-937">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-938">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-938">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-939">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-939">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-940">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-940">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-941">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-941">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-942">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-942">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-943">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-943">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-944">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-944">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-945">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-945">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-946">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-946">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-947">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-947">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-948">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-948">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-949">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-949">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-950">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-950">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-951">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-951">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-952">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-952">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-953">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-953">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-954">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-954">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_rename"></a><span data-ttu-id="34ea1-955">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-955">fx_directory_rename</span></span>

<span data-ttu-id="34ea1-956">Dizini yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="34ea1-956">Renames directory</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-957">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-957">Prototype</span></span>

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-958">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-958">Description</span></span>

<span data-ttu-id="34ea1-959">Bu hizmet dizin adını belirtilen yeni dizin adıyla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-959">This service changes the directory name to the specified new directory name.</span></span> <span data-ttu-id="34ea1-960">Yeniden adlandırma işlemi, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-960">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="34ea1-961">Yeni Dizin adında bir yol belirtilmişse, yeniden adlandırılan dizin, belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-961">If a path is specified in the new directory name, the renamed directory is effectively moved to the specified path.</span></span> <span data-ttu-id="34ea1-962">Yol belirtilmemişse, yeniden adlandırılan dizin geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-962">If no path is specified, the renamed directory is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-963">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-963">Input Parameters</span></span>

- <span data-ttu-id="34ea1-964">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-964">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-965">**old_directory_name**: geçerli dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-965">**old_directory_name**: Pointer to current directory name.</span></span>
- <span data-ttu-id="34ea1-966">**new_directory_name**: yeni dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-966">**new_directory_name**: Pointer to new directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-967">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-967">Return Values</span></span>

- <span data-ttu-id="34ea1-968">**FX_SUCCESS** (0x00) başarılı dizin yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-968">**FX_SUCCESS** (0x00) Successful directory rename.</span></span>
- <span data-ttu-id="34ea1-969">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-969">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-970">**FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-970">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="34ea1-971">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-971">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory.</span></span>
- <span data-ttu-id="34ea1-972">**FX_INVALID_NAME** (0x0C) yeni dizin adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-972">**FX_INVALID_NAME** (0x0C) New directory name is invalid.</span></span>
- <span data-ttu-id="34ea1-973">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-973">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-974">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-974">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-975">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-975">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-976">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-976">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-977">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-977">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-978">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-978">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="34ea1-979">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-979">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-980">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-980">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="34ea1-981">**FX_INVALID_PATH** (0x0D) dizin adıyla belirtilen yol geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-981">**FX_INVALID_PATH** (0x0D) Invalid path supplied with directory name.</span></span>
- <span data-ttu-id="34ea1-982">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin zaten oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-982">**FX_ALREADY_CREATED** (0x0B) Specified directory was already created.</span></span>
- <span data-ttu-id="34ea1-983">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-983">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-984">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-984">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-985">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-985">Allowed From</span></span>

<span data-ttu-id="34ea1-986">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-986">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-987">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-987">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-988">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-988">See Also</span></span>

- <span data-ttu-id="34ea1-989">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-989">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-990">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-990">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-991">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-991">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-992">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-992">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-993">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-993">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-994">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-994">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-995">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-995">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-996">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-996">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-997">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-997">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-998">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-998">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-999">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-999">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-1000">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-1000">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-1001">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1001">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-1002">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1002">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-1003">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-1003">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-1004">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1004">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-1005">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1005">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-1006">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1006">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-1007">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1007">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-1008">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1008">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get"></a><span data-ttu-id="34ea1-1009">fx_directory_short_name_get:</span><span class="sxs-lookup"><span data-stu-id="34ea1-1009">fx_directory_short_name_get:</span></span>

<span data-ttu-id="34ea1-1010">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-1010">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1011">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1011">Prototype</span></span>

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-1012">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1012">Description</span></span>

<span data-ttu-id="34ea1-1013">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1013">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="34ea1-1014">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1014">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1015">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1015">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1016">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1016">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-1017">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1017">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="34ea1-1018">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1018">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="34ea1-1019">Kısa ad hedefinin 14 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1019">Note that the destination for the short name must be large enough to hold 14 characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1020">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1020">Return Values</span></span>

- <span data-ttu-id="34ea1-1021">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1021">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="34ea1-1022">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1022">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="34ea1-1023">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1023">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1024">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1024">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1025">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1025">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1026">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1026">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1027">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1027">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1028">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1028">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1029">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1029">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-1030">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1030">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="34ea1-1031">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1031">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1032">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1032">Allowed From</span></span>

<span data-ttu-id="34ea1-1033">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1033">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1034">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1034">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1035">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1035">See Also</span></span>

- <span data-ttu-id="34ea1-1036">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1036">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-1037">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1037">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-1038">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1038">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-1039">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1039">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-1040">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1040">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-1041">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1041">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-1042">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1042">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-1043">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1043">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-1044">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1044">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-1045">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-1045">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-1046">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1046">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-1047">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-1047">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-1048">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1048">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-1049">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1049">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-1050">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-1050">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-1051">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1051">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-1052">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1052">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-1053">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1053">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-1054">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1054">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-1055">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1055">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get_extended"></a><span data-ttu-id="34ea1-1056">fx_directory_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="34ea1-1056">fx_directory_short_name_get_extended</span></span>

<span data-ttu-id="34ea1-1057">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-1057">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1058">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1058">Prototype</span></span>

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a><span data-ttu-id="34ea1-1059">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1059">Description</span></span>

<span data-ttu-id="34ea1-1060">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1060">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="34ea1-1061">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1061">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1062">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1062">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1063">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1063">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-1064">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1064">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="34ea1-1065">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1065">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="34ea1-1066">Note: kısa ad hedefi 14 karakter tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1066">Note: Destination for the short name must be large enough to hold 14 characters.</span></span>
- <span data-ttu-id="34ea1-1067">**short_file_name_length**: kısa ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1067">**short_file_name_length**: Length of short name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1068">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1068">Return Values</span></span>

- <span data-ttu-id="34ea1-1069">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1069">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="34ea1-1070">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1070">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="34ea1-1071">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1071">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1072">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1072">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1073">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1074">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1075">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1075">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1076">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1076">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1077">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1077">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-1078">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1078">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="34ea1-1079">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1079">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1080">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1080">Allowed From</span></span>

<span data-ttu-id="34ea1-1081">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1081">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1082">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1082">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1083">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1083">See Also</span></span>

- <span data-ttu-id="34ea1-1084">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1084">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-1085">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1085">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-1086">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1086">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-1087">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1087">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-1088">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1088">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-1089">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1089">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-1090">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1090">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-1091">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1091">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-1092">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1092">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-1093">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-1093">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-1094">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1094">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-1095">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-1095">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-1096">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1096">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-1097">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1097">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-1098">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-1098">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-1099">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1099">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-1100">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-1100">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-1101">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1101">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-1102">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1102">fx_unicode_directory_create</span></span>
- <span data-ttu-id="34ea1-1103">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1103">fx_unicode_directory_rename</span></span>

## <a name="fx_fault_tolerant_enable"></a><span data-ttu-id="34ea1-1104">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-1104">fx_fault_tolerant_enable</span></span>

<span data-ttu-id="34ea1-1105">Hataya dayanıklı hizmeti sunar</span><span class="sxs-lookup"><span data-stu-id="34ea1-1105">Enables the fault tolerant service</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1106">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1106">Prototype</span></span>

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a><span data-ttu-id="34ea1-1107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1107">Description</span></span>

<span data-ttu-id="34ea1-1108">Bu hizmet, hataya dayanıklı modüle izin vermez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1108">This service enables the fault tolerant module.</span></span> <span data-ttu-id="34ea1-1109">Başlamadan sonra, hataya dayanıklı modül dosya sisteminin FileX hataya dayanıklı koruma altında olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1109">Upon starting, the fault tolerant module detects whether or not the file system is under FileX fault tolerant protection.</span></span> <span data-ttu-id="34ea1-1110">Aksi takdirde, hizmet, dosya sistemi işlemlerinde günlükleri depolamak için dosya sisteminde kullanılabilir kesimleri bulur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1110">If it is not, the service finds available sectors on the file system to store logs on file system transactions.</span></span> <span data-ttu-id="34ea1-1111">Dosya sistemi, FileX hataya dayanıklı koruma altındaysa, bütünlüğünü sürdürmek için günlükleri dosya sistemine uygular.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1111">If the file system is under FileX fault tolerant protection, it applies the logs to the file system to maintain its integrity.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1112">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1112">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1113">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1113">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-1114">**memory_ptr**: hataya dayanıklı modül tarafından karalama belleği olarak kullanılan bir bellek bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1114">**memory_ptr**: Pointer to a block of memory used by the fault tolerant module as scratch memory.</span></span>
- <span data-ttu-id="34ea1-1115">**memory_size**: karalama belleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1115">**memory_size**: The size of the scratch memory.</span></span> <span data-ttu-id="34ea1-1116">Hata toleranslı 'nin düzgün çalışması için, karalama belleği boyutu en az 3072 bayt olur ve sektör boyutunun katı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1116">In order for fault tolerant to work properly, the scratch memory size shall be at least 3072 bytes,- and must be multiple of sector size.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1117">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1117">Return Values</span></span>

- <span data-ttu-id="34ea1-1118">**FX_SUCCESS** (0x00) hata dayanıklılığını başarıyla etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1118">**FX_SUCCESS** (0x00) Successfully enabled fault tolerant.</span></span>
- <span data-ttu-id="34ea1-1119">**FX_NOT_ENOUGH_MEMORY** (0x91) bellek boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1119">**FX_NOT_ENOUGH_MEMORY** (0x91)    memory size too small.</span></span>
- <span data-ttu-id="34ea1-1120">**FX_BOOT_ERROR** (0x01) önyükleme kesimi hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1120">**FX_BOOT_ERROR** (0x01) Boot sector error.</span></span>
- <span data-ttu-id="34ea1-1121">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1121">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1122">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1122">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="34ea1-1123">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1123">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="34ea1-1124">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="34ea1-1124">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="34ea1-1125">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1125">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1126">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1126">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-1127">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1127">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1128">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1128">Allowed From</span></span>

<span data-ttu-id="34ea1-1129">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1129">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1130">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1130">Example</span></span>

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a><span data-ttu-id="34ea1-1131">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1131">See Also</span></span>

- <span data-ttu-id="34ea1-1132">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-1132">fx_system_initialize</span></span>
- <span data-ttu-id="34ea1-1133">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-1133">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-1134">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1134">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-1135">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-1135">fx_media_check</span></span>
- <span data-ttu-id="34ea1-1136">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1136">fx_media_close</span></span>
- <span data-ttu-id="34ea1-1137">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1137">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-1138">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-1138">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-1139">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-1139">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-1140">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-1140">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-1141">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-1141">fx_media_format</span></span>
- <span data-ttu-id="34ea1-1142">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1142">fx_media_open</span></span>
- <span data-ttu-id="34ea1-1143">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1143">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-1144">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1144">fx_media_read</span></span>
- <span data-ttu-id="34ea1-1145">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-1145">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-1146">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1146">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-1147">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1147">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-1148">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1148">fx_media_write</span></span>

## <a name="fx_file_allocate"></a><span data-ttu-id="34ea1-1149">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1149">fx_file_allocate</span></span>

<span data-ttu-id="34ea1-1150">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="34ea1-1150">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1151">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1151">Prototype</span></span>

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="34ea1-1152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1152">Description</span></span>

<span data-ttu-id="34ea1-1153">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1153">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="34ea1-1154">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1154">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="34ea1-1155">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1155">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="34ea1-1156">4 GB 'den daha fazla alan ayırmak için, uygulama Service *fx_file_extended_allocate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1156">To allocate space beyond 4GB, application shall use the service *fx_file_extended_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1157">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1158">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1158">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-1159">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1159">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1160">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1160">Return Values</span></span>

- <span data-ttu-id="34ea1-1161">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1161">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="34ea1-1162">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1162">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-1163">**FX_FAT_READ_ERROR** (0x03), FAT girişini okuyamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1163">**FX_FAT_READ_ERROR** (0x03) Failed to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1164">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1164">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1165">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1165">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-1166">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1166">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="34ea1-1167">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1167">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="34ea1-1168">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="34ea1-1168">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="34ea1-1169">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1169">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1170">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1170">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1171">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1171">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-1172">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1172">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1173">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1173">Allowed From</span></span>

<span data-ttu-id="34ea1-1174">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1175">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1175">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1176">See Also</span></span>

- <span data-ttu-id="34ea1-1177">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1177">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1178">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1178">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1179">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1179">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1180">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1180">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="34ea1-1181">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1181">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1182">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1182">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1183">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1183">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1184">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1184">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1185">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1185">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1186">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1186">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1187">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1187">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1188">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1188">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1189">fx_file_open fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1189">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="34ea1-1190">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1190">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1191">fx_file_rename fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1191">fx_file_rename- fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1192">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1192">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1193">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1193">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1194">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1194">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1195">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1195">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1196">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1196">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1197">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1197">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1198">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1198">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1199">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1199">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_read"></a><span data-ttu-id="34ea1-1200">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1200">fx_file_attributes_read</span></span>

<span data-ttu-id="34ea1-1201">Dosya özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="34ea1-1201">Reads file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1202">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1202">Prototype</span></span>

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-1203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1203">Description</span></span>

<span data-ttu-id="34ea1-1204">Bu hizmet, dosyanın özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1204">This service reads the file's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1205">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1206">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1206">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-1207">**file_name**: istenen dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1207">**file_name**: Pointer to the name of the requested file (directory path is optional).</span></span>
- <span data-ttu-id="34ea1-1208">**attributes_ptr**: dosyaya yerleştirilecek özniteliklerin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1208">**attributes_ptr**: Pointer to the destination for the file's attributes to be placed.</span></span> <span data-ttu-id="34ea1-1209">Dosya öznitelikleri, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="34ea1-1209">The file attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="34ea1-1210">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1210">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="34ea1-1211">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1211">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="34ea1-1212">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1212">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="34ea1-1213">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1213">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="34ea1-1214">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1214">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="34ea1-1215">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1215">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1216">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1216">Return Values</span></span>

- <span data-ttu-id="34ea1-1217">**FX_SUCCESS** (0x00) başarılı özniteliği okundu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1217">**FX_SUCCESS** (0x00) Successful attribute read.</span></span>
- <span data-ttu-id="34ea1-1218">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1218">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-1219">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1219">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="34ea1-1220">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1220">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="34ea1-1221">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1221">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1222">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1222">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1223">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1223">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1224">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1224">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1225">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1225">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1226">**FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1226">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="34ea1-1227">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1227">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1228">Allowed From</span></span>

<span data-ttu-id="34ea1-1229">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1230">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1230">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-1231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1231">See Also</span></span>

- <span data-ttu-id="34ea1-1232">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1232">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1233">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1233">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1234">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1234">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1235">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1235">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="34ea1-1236">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1236">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1237">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1237">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1238">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1238">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1239">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1239">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1240">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1240">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1241">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1241">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1242">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1242">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1243">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1243">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1244">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1244">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1245">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1245">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1246">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1246">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1247">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1247">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1248">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1248">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1249">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1249">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1250">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1250">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1251">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1251">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1252">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1252">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1253">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1253">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1254">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1254">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1255">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1255">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1256">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1256">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_set"></a><span data-ttu-id="34ea1-1257">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1257">fx_file_attributes_set</span></span>

<span data-ttu-id="34ea1-1258">Dosya özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-1258">Sets file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1259">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1259">Prototype</span></span>

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a><span data-ttu-id="34ea1-1260">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1260">Description</span></span>

<span data-ttu-id="34ea1-1261">Bu hizmet, dosyanın özniteliklerini çağıran tarafından belirtilen olanlarla ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1261">This service sets the file's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-1262">*Uygulamanın yalnızca bu hizmetle birlikte dosyanın özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlamaya yönelik her türlü girişim bir hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-1262">*The application is only allowed to modify a subset of the file's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1263">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1263">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1264">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1264">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-1265">**file_name**: istenen dosyanın adı işaretçisi \* \* (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1265">**file_name**: Pointer to the name of the requested file\*\* (directory path is optional).</span></span>
- <span data-ttu-id="34ea1-1266">**öznitelikler**: dosyanın yeni öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1266">**attributes**: The new attributes for the file.</span></span> <span data-ttu-id="34ea1-1267">Geçerli dosya öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-1267">The valid file attributes are defined as follows:</span></span>
  - <span data-ttu-id="34ea1-1268">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1268">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="34ea1-1269">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1269">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="34ea1-1270">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1270">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="34ea1-1271">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1271">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1272">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1272">Return Values</span></span>

- <span data-ttu-id="34ea1-1273">**FX_SUCCESS** (0x00) başarılı öznitelik kümesi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1273">**FX_SUCCESS** (0x00) Successful attribute set.</span></span>
- <span data-ttu-id="34ea1-1274">**FX_ACCESS_ERROR** (0x06) dosyası açık ve öznitelikleri ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1274">**FX_ACCESS_ERROR** (0x06) File is open and cannot have its attributes set.</span></span>
- <span data-ttu-id="34ea1-1275">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1275">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1276">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1276">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-1278">**FX_NO_MORE_ENTRIES** (0x0F) FAT tablosunda veya exFAT Cluster eşlemesinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1278">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in the FAT table or exFAT cluster map.</span></span>
- <span data-ttu-id="34ea1-1279">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1279">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="34ea1-1280">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1280">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="34ea1-1281">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1281">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="34ea1-1282">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="34ea1-1282">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="34ea1-1283">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1283">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1284">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1284">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1285">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1285">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-1286">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1286">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-1287">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1287">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="34ea1-1288">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1288">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1289">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1289">Allowed From</span></span>

<span data-ttu-id="34ea1-1290">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1290">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1291">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1291">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-1292">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1292">See Also</span></span>

- <span data-ttu-id="34ea1-1293">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1293">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1294">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1294">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1295">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1295">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1296">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1296">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1297">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1297">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1298">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1298">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1299">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1299">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1300">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1300">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1301">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1301">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1302">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1302">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1303">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1303">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1304">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1304">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1305">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1305">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1306">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1306">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1307">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1307">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1308">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1308">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1309">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1309">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1310">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1310">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1311">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1311">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1312">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1312">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1313">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1313">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1314">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1314">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1315">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1315">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1316">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1316">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1317">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1317">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1318">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1318">fx_unicode_short_name_get</span></span>

## <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="34ea1-1319">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1319">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="34ea1-1320">Bir dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="34ea1-1320">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1321">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1321">Prototype</span></span>

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="34ea1-1322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1322">Description</span></span>

<span data-ttu-id="34ea1-1323">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1323">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="34ea1-1324">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1324">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="34ea1-1325">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1325">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="34ea1-1326">Medyada yeterli sayıda ardışık küme yoksa, bu hizmet birbirini izleyen en büyük küme bloğunu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1326">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="34ea1-1327">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1327">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="34ea1-1328">4 GB 'den daha fazla alan ayırmak için, uygulama Service *fx_file_extended_best_effort_allocate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1328">To allocate space beyond 4GB, application shall use the service *fx_file_extended_best_effort_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1329">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1329">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1330">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1330">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-1331">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1331">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1332">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1332">Return Values</span></span>

- <span data-ttu-id="34ea1-1333">**FX_SUCCESS** (0x00) başarılı en iyi çaba dosya ayırması.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1333">**FX_SUCCESS** (0x00) Successful best-effort file allocation.</span></span>
- <span data-ttu-id="34ea1-1334">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1334">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-1335">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1335">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-1336">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1336">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="34ea1-1337">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1337">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1338">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1338">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1339">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1339">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1340">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1340">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1341">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1341">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1342">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1342">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1343">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi veya hedef.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1343">**FX_PTR_ERROR** (0x18) Invalid file pointer or destination.</span></span>
- <span data-ttu-id="34ea1-1344">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1344">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1345">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1345">Allowed From</span></span>

<span data-ttu-id="34ea1-1346">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1346">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1347">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1347">Example</span></span>

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-1348">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1348">See Also</span></span>

- <span data-ttu-id="34ea1-1349">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1349">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1350">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1350">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1351">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1351">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1352">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1353">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1354">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1355">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1359">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1362">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1363">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1364">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1365">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1366">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1367">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1368">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1369">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1371">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1371">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1372">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1372">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1373">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1373">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1374">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1374">fx_unicode_short_name_get</span></span>

## <a name="fx_file_close"></a><span data-ttu-id="34ea1-1375">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1375">fx_file_close</span></span>

<span data-ttu-id="34ea1-1376">Dosyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="34ea1-1376">Closes file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1377">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1377">Prototype</span></span>

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-1378">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1378">Description</span></span>

<span data-ttu-id="34ea1-1379">Bu hizmet, belirtilen dosyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1379">This service closes the specified file.</span></span> <span data-ttu-id="34ea1-1380">Dosya yazmak için açıksa ve değiştirilmişse, bu hizmet Dizin girişini yeni boyut ve geçerli sistem saati ve tarihi ile güncelleştirerek dosya değiştirme işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1380">If the file was open for writing and if it was modified, this service completes the file modification process by updating its directory entry with the new size and the current system time and date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1381">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1381">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1382">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1382">**file_ptr**: Pointer to a previously opened file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1383">Return Values</span></span>

- <span data-ttu-id="34ea1-1384">**FX_SUCCESS** (0x00) başarılı dosya kapatma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1384">**FX_SUCCESS** (0x00) Successful file close.</span></span>
- <span data-ttu-id="34ea1-1385">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1385">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="34ea1-1386">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1386">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1387">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1387">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1388">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1388">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1389">**FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1389">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="34ea1-1390">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1390">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1391">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1391">Allowed From</span></span>

<span data-ttu-id="34ea1-1392">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1392">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1393">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1393">Example</span></span>

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1394">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1394">See Also</span></span>

- <span data-ttu-id="34ea1-1395">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1395">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1396">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1396">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1397">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1397">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1398">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1398">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1399">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1399">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1400">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1400">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1401">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1401">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1402">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1402">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1403">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1403">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1404">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1404">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1405">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1405">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1406">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1406">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1407">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1407">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1408">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1408">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1409">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1409">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1410">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1410">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1411">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1411">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1412">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1412">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1413">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1413">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1414">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1414">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1415">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1415">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1416">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1416">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1417">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1417">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1418">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1418">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1419">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1419">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1420">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1420">fx_unicode_short_name_get</span></span>

## <a name="fx_file_create"></a><span data-ttu-id="34ea1-1421">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1421">fx_file_create</span></span>

<span data-ttu-id="34ea1-1422">Dosya oluşturur</span><span class="sxs-lookup"><span data-stu-id="34ea1-1422">Creates file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1423">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1423">Prototype</span></span>

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-1424">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1424">Description</span></span>

<span data-ttu-id="34ea1-1425">Bu hizmet, belirtilen dosyayı varsayılan dizinde veya dosya adıyla sağlanan dizin yolunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1425">This service creates the specified file in the default directory or in the directory path supplied with the file name.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-1426">*Bu hizmet sıfır uzunlukta bir dosya oluşturur, başka bir ifadeyle küme ayrılır. Ayırma, sonraki dosya yazmalarında otomatik olarak yapılır veya fx_file_allocate hizmetiyle veya 4 GB'ın fx_file_extended_allocate alan için önceden yapılabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-1426">*This service creates a file of zero length, i.e., no clusters allocated. Allocation will automatically take place on subsequent file writes or can be done in advance with the fx_file_allocate service or fx_file_extended_allocate for space beyond 4GB) service.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1427">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1427">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1428">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1428">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-1429">**file_name:** Oluşturulacak dosyanın adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1429">**file_name**: Pointer to the name of the file to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1430">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1430">Return Values</span></span>

- <span data-ttu-id="34ea1-1431">**FX_SUCCESS** (0x00) Başarılı dosya oluşturma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1431">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="34ea1-1432">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1432">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-1433">**FX_ALREADY_CREATED** (0x0B) Belirtilen dosya zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1433">**FX_ALREADY_CREATED** (0x0B) Specified file was already created.</span></span>
- <span data-ttu-id="34ea1-1434">**FX_NO_MORE_SPACE** (0x0A) Kök dizinde daha fazla giriş yok veya kullanılabilir başka küme yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1434">**FX_NO_MORE_SPACE** (0x0A)    Either there are no more entries in the root directory or there are no more clusters available.</span></span>
- <span data-ttu-id="34ea1-1435">**FX_INVALID_PATH** (0x0D) Dosya adıyla sağlanan geçersiz yol.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1435">**FX_INVALID_PATH** (0x0D) Invalid path supplied with file name.</span></span>
- <span data-ttu-id="34ea1-1436">**FX_INVALID_NAME** (0x0C) Dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1436">**FX_INVALID_NAME** (0x0C) File name is invalid.</span></span>
- <span data-ttu-id="34ea1-1437">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1437">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1438">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1438">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1439">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1439">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1440">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1440">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1441">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1441">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1442">**FX_MEDIA_INVALID** (0x02)Geçersiz medya.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1442">**FX_MEDIA_INVALID** (0x02)Invalid media.</span></span>
- <span data-ttu-id="34ea1-1443">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1443">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1444">**FX_WRITE_PROTECT** (0x23) Temel medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1444">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="34ea1-1445">**FX_PTR_ERROR** (0x18) Geçersiz medya veya dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1445">**FX_PTR_ERROR** (0x18) Invalid media or file name pointer.</span></span>
- <span data-ttu-id="34ea1-1446">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1446">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1447">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1447">Allowed From</span></span>

<span data-ttu-id="34ea1-1448">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1448">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1449">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1449">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1450">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1450">See Also</span></span>
- <span data-ttu-id="34ea1-1451">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1451">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1452">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1452">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1453">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1453">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1454">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1454">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1455">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1455">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1456">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1456">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1457">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1457">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1458">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1458">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1459">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1459">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1460">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1460">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1461">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1461">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1462">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1462">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1463">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1463">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1464">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1464">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1465">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1465">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1466">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1466">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1467">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1467">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1468">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1468">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1469">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1469">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1470">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1470">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1471">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1471">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1472">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1472">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1473">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1473">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1474">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1474">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1475">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1475">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1476">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1476">fx_unicode_short_name_get</span></span>

## <a name="fx_file_date_time_set"></a><span data-ttu-id="34ea1-1477">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1477">fx_file_date_time_set</span></span>

### <a name="sets-file-date-and-time"></a><span data-ttu-id="34ea1-1478">Dosya tarih ve saati ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-1478">Sets file date and time</span></span>

<span data-ttu-id="34ea1-1479">Dosya Tarihi ve Saati Ayarlama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1479">Setting File Date and Time</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1480">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1480">Prototype</span></span>

```c
UINT fx_file_date_time_set(
    FX_MEDIA *media_ptr, 
    CHAR *file_name,
    UINT year, 
    UINT month, 
    UINT day,
    UINT hour, 
    UINT minute, 
    UINT second);
```
### <a name="description"></a><span data-ttu-id="34ea1-1481">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1481">Description</span></span>

<span data-ttu-id="34ea1-1482">Bu hizmet, belirtilen dosyanın tarih ve saati ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1482">This service sets the date and time of the specified file.</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1483">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1483">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1484">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1484">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-1485">**file_name:** Dosyanın adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1485">**file_name**: Pointer to name of the file.</span></span>
- <span data-ttu-id="34ea1-1486">**year:** Yılın değeri (1980-2107 dahil).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1486">**year**: Value of year (1980-2107 inclusive).</span></span>
- <span data-ttu-id="34ea1-1487">**month:** Ayın değeri (1-12 dahil).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1487">**month**: Value of month (1-12 inclusive).</span></span>
- <span data-ttu-id="34ea1-1488">**day:** Günün değeri (1-31 dahil).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1488">**day**: Value of day (1-31 inclusive).</span></span>
- <span data-ttu-id="34ea1-1489">**hour:** Saat değeri (0-23 dahil).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1489">**hour**: Value of hour (0-23 inclusive).</span></span>
- <span data-ttu-id="34ea1-1490">**minute:** Dakika değeri (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1490">**minute**: Value of minute (0-59 inclusive).</span></span>
- <span data-ttu-id="34ea1-1491">**second:** Saniyenin değeri (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1491">**second**: Value of second (0-59 inclusive).</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1492">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1492">Return Values</span></span>

- <span data-ttu-id="34ea1-1493">**FX_SUCCESS** (0x00) Başarılı tarih/saat kümesi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1493">**FX_SUCCESS** (0x00) Successful date/time set.</span></span>
- <span data-ttu-id="34ea1-1494">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1494">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-1495">**FX_NOT_FOUND** (0x04) Dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1495">**FX_NOT_FOUND** (0x04)    File was not found.</span></span>
- <span data-ttu-id="34ea1-1496">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1496">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1497">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1497">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1498">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1498">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1499">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1499">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1500">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1500">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="34ea1-1501">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1501">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1502">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1502">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1503">**FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1503">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="34ea1-1504">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1504">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="34ea1-1505">**FX_INVALID_YEAR** (0x12) Yıl geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1505">**FX_INVALID_YEAR** (0x12) Year is invalid.</span></span>
- <span data-ttu-id="34ea1-1506">**FX_INVALID_MONTH** (0x13) Ay geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1506">**FX_INVALID_MONTH** (0x13) Month is invalid.</span></span>
- <span data-ttu-id="34ea1-1507">**FX_INVALID_DAY** (0x14) Günü geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1507">**FX_INVALID_DAY** (0x14) Day is invalid.</span></span>
- <span data-ttu-id="34ea1-1508">**FX_INVALID_HOUR** (0x15) Saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1508">**FX_INVALID_HOUR** (0x15)    Hour is invalid.</span></span>
- <span data-ttu-id="34ea1-1509">**FX_INVALID_MINUTE** (0x16) Dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1509">**FX_INVALID_MINUTE** (0x16) Minute is invalid.</span></span>
- <span data-ttu-id="34ea1-1510">**FX_INVALID_SECOND** (0x17) Saniye geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1510">**FX_INVALID_SECOND** (0x17) Second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1511">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1511">Allowed From</span></span>

<span data-ttu-id="34ea1-1512">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1512">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1513">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1513">Example</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1514">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1514">See Also</span></span>

- <span data-ttu-id="34ea1-1515">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1515">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1516">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1516">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1517">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1517">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1518">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1518">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1519">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1519">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1520">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1520">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1521">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1521">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1522">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1522">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1523">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1523">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1524">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1524">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1525">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1525">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1526">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1526">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1527">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1527">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1528">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1528">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1529">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1529">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1530">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1530">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1531">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1531">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1532">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1532">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1533">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1533">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1534">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1534">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1535">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1535">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1536">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1536">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1537">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1537">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1538">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1538">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1539">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1539">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1540">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1540">fx_unicode_short_name_get</span></span>

## <a name="fx_file_delete"></a><span data-ttu-id="34ea1-1541">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1541">fx_file_delete</span></span>

### <a name="deletes-file"></a><span data-ttu-id="34ea1-1542">Dosyayı siler</span><span class="sxs-lookup"><span data-stu-id="34ea1-1542">Deletes file</span></span>

<span data-ttu-id="34ea1-1543">Dosya Silme</span><span class="sxs-lookup"><span data-stu-id="34ea1-1543">File Deletion</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1544">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1544">Prototype</span></span>

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-1545">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1545">Description</span></span>

<span data-ttu-id="34ea1-1546">Bu hizmet belirtilen dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1546">This service deletes the specified file.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="34ea1-1547">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1547">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1548">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1548">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-1549">**file_name:** Silinecek dosyanın adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1549">**file_name**: Pointer to the name of the file to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1550">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1550">Return Values</span></span>

- <span data-ttu-id="34ea1-1551">**FX_SUCCESS** (0x00) Başarılı dosya silme.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1551">**FX_SUCCESS** (0x00) Successful file delete.</span></span>
- <span data-ttu-id="34ea1-1552">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1552">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-1553">**FX_NOT_FOUND** (0x04) Belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1553">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="34ea1-1554">**FX_NOT_A_FILE** (0x05) Belirtilen dosya adı bir dizin veya birimdi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1554">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="34ea1-1555">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya şu anda açık.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1555">**FX_ACCESS_ERROR** (0x06) Specified file is currently open.</span></span>
- <span data-ttu-id="34ea1-1556">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1556">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1557">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1557">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1558">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1558">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1559">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1559">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1560">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1560">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1561">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1561">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1562">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1562">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1563">**FX_MEDIA_INVALID** (0x02) Geçersiz medya.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1563">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-1564">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1564">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-1565">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1565">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1566">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1566">Allowed From</span></span>

<span data-ttu-id="34ea1-1567">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1568">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1568">Example</span></span>

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1569">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1569">See Also</span></span>

- <span data-ttu-id="34ea1-1570">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1570">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1571">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1571">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1572">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1572">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1573">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1573">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1574">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1574">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1575">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1575">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1576">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1576">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1577">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1577">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1578">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1578">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1579">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1579">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1580">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1580">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1581">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1581">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1582">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1582">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1583">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1583">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1584">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1584">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1585">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1585">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1586">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1586">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1587">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1587">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1588">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1588">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1589">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1589">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1590">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1590">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1591">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1591">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1592">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1592">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1593">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1593">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1594">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1594">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1595">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1595">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_allocate"></a><span data-ttu-id="34ea1-1596">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1596">fx_file_extended_allocate</span></span>

<span data-ttu-id="34ea1-1597">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="34ea1-1597">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1598">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1598">Prototype</span></span>

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="34ea1-1599">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1599">Description</span></span>

<span data-ttu-id="34ea1-1600">Bu hizmet, bir veya daha fazla bitişik kümeyi belirtilen dosyanın sonuna ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1600">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="34ea1-1601">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1601">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="34ea1-1602">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1602">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="34ea1-1603">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1603">This service is designed for exFAT.</span></span> <span data-ttu-id="34ea1-1604">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1604">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1605">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1605">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1606">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1606">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-1607">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1607">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1608">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1608">Return Values</span></span>

- <span data-ttu-id="34ea1-1609">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1609">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="34ea1-1610">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1610">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-1611">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1611">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-1612">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1612">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="34ea1-1613">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1613">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1614">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1614">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1615">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1615">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1616">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1616">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1617">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1617">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1618">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1618">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1619">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1619">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-1620">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1620">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1621">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1621">Allowed From</span></span>

<span data-ttu-id="34ea1-1622">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1622">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1623">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1623">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1624">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1624">See Also</span></span>

- <span data-ttu-id="34ea1-1625">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1625">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1626">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1626">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1627">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1627">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1628">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1628">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1629">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1629">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1630">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1630">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1631">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1631">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1632">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1632">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1633">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1633">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1634">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1634">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1635">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1635">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1636">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1636">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1637">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1637">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1638">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1638">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1639">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1639">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1640">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1640">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1641">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1641">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1642">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1642">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1643">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1643">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1644">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1644">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1645">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1645">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1646">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1646">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1647">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1647">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1648">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1648">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1649">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1649">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1650">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1650">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_best_effort_allocate"></a><span data-ttu-id="34ea1-1651">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1651">fx_file_extended_best_effort_allocate</span></span>

<span data-ttu-id="34ea1-1652">Bir dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="34ea1-1652">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1653">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1653">Prototype</span></span>

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="34ea1-1654">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1654">Description</span></span>

<span data-ttu-id="34ea1-1655">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1655">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="34ea1-1656">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1656">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="34ea1-1657">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1657">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="34ea1-1658">Medyada yeterli sayıda ardışık küme yoksa, bu hizmet birbirini izleyen en büyük küme bloğunu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1658">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="34ea1-1659">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1659">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="34ea1-1660">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1660">This service is designed for exFAT.</span></span> <span data-ttu-id="34ea1-1661">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1661">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1662">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1662">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1663">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1663">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-1664">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1664">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1665">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1665">Return Values</span></span>

- <span data-ttu-id="34ea1-1666">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1666">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="34ea1-1667">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1667">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-1668">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1668">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-1669">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1669">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="34ea1-1670">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1670">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1671">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1671">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1672">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1672">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1673">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1673">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1674">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1674">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1675">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1675">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1676">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1676">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-1677">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1677">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1678">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1678">Allowed From</span></span>

<span data-ttu-id="34ea1-1679">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1679">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1680">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1680">Example</span></span>

```c

FX_FILE my_file;
UINT             status;
ULONG64         actual_allocation;

/* Attempt to allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_best_effort_allocate(&my_file,
    0x100000000, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1681">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1681">See Also</span></span>

- <span data-ttu-id="34ea1-1682">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1682">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1683">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1683">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1684">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1684">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1685">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1685">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1686">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1686">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1687">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1688">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1688">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1689">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1689">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1690">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1690">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1691">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1691">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1692">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1692">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1693">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1693">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1694">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1694">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1695">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1695">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1696">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1696">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1697">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1697">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1698">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1698">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1699">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1699">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1700">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1700">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1701">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1701">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1702">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1702">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1703">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1703">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1704">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1704">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1705">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1705">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1706">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1706">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1707">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1707">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_relative_seek"></a><span data-ttu-id="34ea1-1708">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1708">fx_file_extended_relative_seek</span></span>

<span data-ttu-id="34ea1-1709">Göreli bayt uzaklığına pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-1709">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1710">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1710">Prototype</span></span>

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="34ea1-1711">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1711">Description</span></span>

<span data-ttu-id="34ea1-1712">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1712">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="34ea1-1713">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1713">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="34ea1-1714">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1714">This service is designed for exFAT.</span></span> <span data-ttu-id="34ea1-1715">*Byte_offset* parametresi, çağıranın 4 Aralık dışında okuma/yazma işaretçisini yeniden konumlandırmasına olanak tanıyan bir bit-bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1715">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-1716">*Arama işlemi dosyanın sonundan sonra arama yapmayı denerse, dosyanın okuma/yazma işaretçisi dosyanın sonuna yerleştirilir. Buna karşılık, arama işlemi dosyanın başlangıcını aşan konuma çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başlangıcına yerleştirilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-1716">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1717">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1717">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1718">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1718">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-1719">**byte_offset**: dosyada istenen göreli bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1719">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="34ea1-1720">**seek_from**: göreli arama yapılacak yönün yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1720">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="34ea1-1721">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-1721">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="34ea1-1722">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1722">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="34ea1-1723">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1723">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="34ea1-1724">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1724">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="34ea1-1725">FX_SEEK_BACK (0x03) FX_SEEK_BEGIN belirtilmişse, arama işlemi dosyanın başından yapılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1725">FX_SEEK_BACK (0x03) If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="34ea1-1726">FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1726">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="34ea1-1727">FX_SEEK_FORWARD belirtilirse, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1727">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="34ea1-1728">FX_SEEK_BACK belirtilirse, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1728">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1729">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1729">Return Values</span></span>

- <span data-ttu-id="34ea1-1730">**FX_SUCCESS** (0x00) başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1730">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="34ea1-1731">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1731">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-1732">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1732">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1733">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1733">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1734">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1734">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1735">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1735">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1736">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1736">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-1737">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1737">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1738">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1738">Allowed From</span></span>

<span data-ttu-id="34ea1-1739">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1740">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1740">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1741">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1741">See Also</span></span>

- <span data-ttu-id="34ea1-1742">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1742">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1743">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1743">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1744">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1744">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1745">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1745">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1746">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1746">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1747">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1747">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1748">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1748">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1749">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1749">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1750">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1750">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1751">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1751">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1752">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1752">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1753">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1753">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1754">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1754">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1755">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1755">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1756">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1756">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1757">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1757">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1758">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1758">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1759">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1759">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1760">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1760">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1761">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1761">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1762">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1762">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1763">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1763">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1764">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1764">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1765">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1765">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1766">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1766">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1767">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1767">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_seek"></a><span data-ttu-id="34ea1-1768">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1768">fx_file_extended_seek</span></span>

<span data-ttu-id="34ea1-1769">Bayt uzaklığa pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-1769">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1770">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1770">Prototype</span></span>

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a><span data-ttu-id="34ea1-1771">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1771">Description</span></span>

<span data-ttu-id="34ea1-1772">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen bayt uzaklığa konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1772">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="34ea1-1773">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1773">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="34ea1-1774">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1774">This service is designed for exFAT.</span></span> <span data-ttu-id="34ea1-1775">*Byte_offset* parametresi, çağıranın 4 Aralık dışında okuma/yazma işaretçisini yeniden konumlandırmasına olanak tanıyan bir bit-bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1775">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1776">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1776">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1777">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1777">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-1778">**byte_offset**: dosyada istenen bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1778">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="34ea1-1779">Sıfır değeri, dosyanın başındaki okuma/yazma işaretçisini konumlandırır, ancak dosyanın boyutundan büyük bir değer, dosyanın sonundaki okuma/yazma işaretçisini konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1779">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1780">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1780">Return Values</span></span>

- <span data-ttu-id="34ea1-1781">**FX_SUCCESS** (0x00) başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1781">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="34ea1-1782">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1782">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="34ea1-1783">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1783">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1784">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1784">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1785">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1785">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1786">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1786">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1787">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1787">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-1788">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1788">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1789">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1789">Allowed From</span></span>

<span data-ttu-id="34ea1-1790">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1790">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1791">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1791">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1792">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1792">See Also</span></span>

- <span data-ttu-id="34ea1-1793">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1793">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1794">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1794">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1795">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1795">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1796">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1796">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1797">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1797">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1798">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1798">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1799">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1799">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1800">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1800">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1801">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1801">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1802">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1802">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1803">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1803">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1804">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1804">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1805">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1805">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1806">fx_file_open- fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1806">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="34ea1-1807">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1807">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1808">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1808">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1809">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1809">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1810">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1810">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1811">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1811">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1812">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1812">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1813">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1813">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1814">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1814">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1815">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1815">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1816">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1816">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1817">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1817">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate"></a><span data-ttu-id="34ea1-1818">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1818">fx_file_extended_truncate</span></span>

<span data-ttu-id="34ea1-1819">Kesilir dosyası</span><span class="sxs-lookup"><span data-stu-id="34ea1-1819">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1820">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1820">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="34ea1-1821">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1821">Description</span></span>

<span data-ttu-id="34ea1-1822">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar kısaltır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1822">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="34ea1-1823">Sağlanan boyut gerçek dosya boyutundan büyükse bu hizmet herhangi bir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1823">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="34ea1-1824">Dosyayla ilişkili medya kümelerinin hiçbiri yayımlenmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1824">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-1825">*Aynı anda okuma için açık olan dosyaları kesme konusunda dikkatli olun. Ayrıca okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-1825">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="34ea1-1826">Bu hizmet exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1826">This service is designed for exFAT.</span></span> <span data-ttu-id="34ea1-1827">Size *parametresi,* çağıranın 4 GB'ın ötesinde çalışmasına olanak sağlayan 64 bit tamsayı değerini alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1827">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1828">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1828">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1829">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1829">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-1830">**size:** Yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1830">**size**: New file size.</span></span> <span data-ttu-id="34ea1-1831">Bu yeni dosya boyutunu geçen baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1831">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1832">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1832">Return Values</span></span>

- <span data-ttu-id="34ea1-1833">**FX_SUCCESS** (0x00) Başarılı dosya kesme.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1833">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="34ea1-1834">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1834">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="34ea1-1835">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1835">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-1836">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1836">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1837">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1837">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1838">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1838">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1839">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1839">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1840">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1840">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1841">**FX_WRITE_PROTECT** (0x23) Temel medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1841">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="34ea1-1842">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1842">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-1843">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1843">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1844">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1844">Allowed From</span></span>

<span data-ttu-id="34ea1-1845">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1845">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1846">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1846">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1847">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1847">See Also</span></span>

- <span data-ttu-id="34ea1-1848">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1848">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1849">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1849">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1850">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1850">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1851">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1851">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1852">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1852">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1853">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1853">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1854">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1854">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1855">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1855">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1856">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1856">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1857">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1857">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1858">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1858">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1859">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1859">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1860">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1860">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1861">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1861">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1862">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1862">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1863">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1863">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1864">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1864">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1865">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1865">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1866">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1866">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1867">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1867">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1868">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1868">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1869">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1869">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1870">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1870">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1871">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1871">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1872">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1872">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1873">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1873">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate_release"></a><span data-ttu-id="34ea1-1874">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1874">fx_file_extended_truncate_release</span></span>

<span data-ttu-id="34ea1-1875">Dosya ve yayın kümelerini keser</span><span class="sxs-lookup"><span data-stu-id="34ea1-1875">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1876">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1876">Prototype</span></span>

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a><span data-ttu-id="34ea1-1877">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1877">Description</span></span>

<span data-ttu-id="34ea1-1878">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar kısaltır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1878">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="34ea1-1879">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet herhangi bir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1879">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="34ea1-1880">Bu ***hizmet fx_file_extended_truncate*** kullanılmayan kümeleri serbest bırakmaz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1880">Unlike the ***fx_file_extended_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-1881">*Aynı anda okuma için açık olan dosyaları kesme konusunda dikkatli olun. Ayrıca okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-1881">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="34ea1-1882">Bu hizmet exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1882">This service is designed for exFAT.</span></span> <span data-ttu-id="34ea1-1883">Size *parametresi,* çağıranın 4 GB'ın ötesinde çalışmasına olanak sağlayan 64 bit tamsayı değerini alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1883">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1884">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1884">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1885">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1885">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-1886">**size:** Yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1886">**size**: New file size.</span></span> <span data-ttu-id="34ea1-1887">Bu yeni dosya boyutunu geçen baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1887">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1888">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1888">Return Values</span></span>

- <span data-ttu-id="34ea1-1889">**FX_SUCCESS** (0x00) Başarılı dosya kesme.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1889">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="34ea1-1890">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1890">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-1891">**FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1891">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-1892">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1892">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1893">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1893">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-1894">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1894">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1895">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1895">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-1896">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1896">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1897">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1897">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1898">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1898">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-1899">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1899">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-1900">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1900">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1901">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1901">Allowed From</span></span>

<span data-ttu-id="34ea1-1902">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1902">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1903">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1903">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1904">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1904">See Also</span></span>

- <span data-ttu-id="34ea1-1905">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1905">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1906">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1906">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1907">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1907">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1908">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1908">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1909">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-1909">fx_file_close</span></span>
- <span data-ttu-id="34ea1-1910">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1910">fx_file_create</span></span>
- <span data-ttu-id="34ea1-1911">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1911">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1912">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1912">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1913">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1913">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1914">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1914">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1915">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1915">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1916">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1916">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1917">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1917">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1918">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1918">fx_file_open</span></span>
- <span data-ttu-id="34ea1-1919">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1919">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1920">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1920">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1921">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1921">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1922">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1922">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1923">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1923">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1924">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1924">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1925">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1925">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1926">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1926">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1927">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1927">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1928">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1928">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1929">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1929">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1930">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1930">fx_unicode_short_name_get</span></span>

## <a name="fx_file_open"></a><span data-ttu-id="34ea1-1931">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-1931">fx_file_open</span></span>

<span data-ttu-id="34ea1-1932">Dosyayı açar</span><span class="sxs-lookup"><span data-stu-id="34ea1-1932">Opens file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1933">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1933">Prototype</span></span>

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a><span data-ttu-id="34ea1-1934">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1934">Description</span></span>

<span data-ttu-id="34ea1-1935">Bu hizmet, belirtilen dosyayı okuma ya da yazma için açar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1935">This service opens the specified file for either reading or writing.</span></span> <span data-ttu-id="34ea1-1936">Bir dosya birden çok kez okumak için açılabilir, ancak bir dosya yalnızca yazıcı dosyayı kapatana kadar bir kez yazmak üzere açılabilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1936">A file may be opened for reading multiple times, while a file can only be opened for writing once until the writer closes the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-1937">*Dosya okuma ve yazma için eşzamanlı olarak açıksa dikkatli olunmalıdır. Bir dosya okuma için eşzamanlı olarak açıldığında gerçekleştirilen dosya yazma işlemi, okuyucu kapanmadığı ve dosyayı okumak üzere yeniden açtığından, okuyucu tarafından görülemeyebilir. Benzer şekilde, dosya Truncate Services kullanılırken dosya yazıcısı dikkatli olmalıdır. Bir dosya yazıcı tarafından kesilmişse, aynı dosyanın okuyucuları geçersiz veri döndürebilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-1937">*Care must be taken if a file is concurrently open for reading and writing. File writing performed when a file is simultaneously opened for reading may not be seen by the reader, unless the reader closes and reopens the file for reading. Similarly, the file writer should be careful when using file truncate services. If a file is truncated by the writer, readers of the same file could return invalid data.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-1938">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1938">Input Parameters</span></span>

- <span data-ttu-id="34ea1-1939">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1939">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-1940">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1940">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-1941">**file_name**: açılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-1941">**file_name**: Pointer to the name of the file to open (directory path is optional).</span></span>
- <span data-ttu-id="34ea1-1942">**open_type**: dosya açma türü.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1942">**open_type**: Type of file open.</span></span> <span data-ttu-id="34ea1-1943">Geçerli açık tür seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-1943">Valid open type options are:</span></span>
  - <span data-ttu-id="34ea1-1944">FX_OPEN_FOR_READ (0x00)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1944">FX_OPEN_FOR_READ (0x00)</span></span>
  - <span data-ttu-id="34ea1-1945">FX_OPEN_FOR_WRITE (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1945">FX_OPEN_FOR_WRITE (0x01)</span></span>
  - <span data-ttu-id="34ea1-1946">FX_OPEN_FOR_READ_FAST (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-1946">FX_OPEN_FOR_READ_FAST (0x02)</span></span>

<span data-ttu-id="34ea1-1947">FX_OPEN_FOR_READ ve FX_OPEN_FOR_READ_FAST dosyaları açmak benzerdir:</span><span class="sxs-lookup"><span data-stu-id="34ea1-1947">Opening files with FX_OPEN_FOR_READ and FX_OPEN_FOR_READ_FAST is similar:</span></span>

- <span data-ttu-id="34ea1-1948">FX_OPEN_FOR_READ, dosyayı oluşturan kümelerin bağlı listesinin bozulmamış olduğunu ve FX_OPEN_FOR_READ_FAST Bu doğrulamayı gerçekleştirmediğinden daha hızlı hale gelmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1948">FX_OPEN_FOR_READ includes verification that the linked-list of clusters that comprise the file are intact, and FX_OPEN_FOR_READ_FAST does not perform this verification, which makes it faster.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-1949">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-1949">Return Values</span></span>

- <span data-ttu-id="34ea1-1950">**FX_SUCCESS** (0x00) başarılı dosya açıldı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1950">**FX_SUCCESS** (0x00) Successful file open.</span></span>
- <span data-ttu-id="34ea1-1951">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1951">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-1952">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1952">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="34ea1-1953">**FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1953">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="34ea1-1954">**FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve açma başarısız.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1954">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the open failed.</span></span>
- <span data-ttu-id="34ea1-1955">**FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık veya açma türü geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1955">**FX_ACCESS_ERROR** (0x06) Specified file is already open or open type is invalid.</span></span>
- <span data-ttu-id="34ea1-1956">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1956">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-1957">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1957">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="34ea1-1958">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1958">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-1959">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-1959">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-1960">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1960">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-1961">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1961">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="34ea1-1962">**FX_PTR_ERROR** (0x18) geçersiz medya veya dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1962">**FX_PTR_ERROR** (0x18) Invalid media or file pointer.</span></span>
- <span data-ttu-id="34ea1-1963">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1963">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-1964">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-1964">Allowed From</span></span>

<span data-ttu-id="34ea1-1965">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-1965">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-1966">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1966">Example</span></span>

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-1967">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1967">See Also</span></span>

- <span data-ttu-id="34ea1-1968">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1968">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-1969">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1969">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-1970">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1970">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-1971">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1971">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1972">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1972">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="34ea1-1973">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1973">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-1974">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-1974">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-1975">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1975">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-1976">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1976">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-1977">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1977">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-1978">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1978">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-1979">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1979">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-1980">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1980">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-1981">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1981">fx_file_read</span></span>
- <span data-ttu-id="34ea1-1982">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1982">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-1983">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1983">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-1984">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-1984">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-1985">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-1985">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-1986">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-1986">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-1987">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-1987">fx_file_write</span></span>
- <span data-ttu-id="34ea1-1988">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-1988">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-1989">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-1989">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-1990">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-1990">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-1991">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1991">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-1992">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-1992">fx_unicode_short_name_get</span></span>

## <a name="fx_file_read"></a><span data-ttu-id="34ea1-1993">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-1993">fx_file_read</span></span>

<span data-ttu-id="34ea1-1994">Dosyadan bayt okur</span><span class="sxs-lookup"><span data-stu-id="34ea1-1994">Reads bytes from file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-1995">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-1995">Prototype</span></span>

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a><span data-ttu-id="34ea1-1996">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-1996">Description</span></span>

<span data-ttu-id="34ea1-1997">Bu hizmet, dosyadaki baytları okur ve bunları sağlanan arabellekte depolar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1997">This service reads bytes from the file and stores them in the supplied buffer.</span></span> <span data-ttu-id="34ea1-1998">Okuma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1998">After the read is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span> <span data-ttu-id="34ea1-1999">İstekte daha az bayt kaldığında, yalnızca kalan baytlar arabellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-1999">If there are fewer bytes remaining in the request, only the bytes remaining are stored in the buffer.</span></span> <span data-ttu-id="34ea1-2000">Herhangi bir durumda, arabelleğe yerleştirilmiş baytların toplam sayısı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2000">In any case, the total number of bytes placed in the buffer is returned to the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2001">*Uygulama, sağlanan arabelleğin belirtilen sayıda istenen bayt depolayana kadar olduğundan emin olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2001">*The application must ensure that the buffer supplied is able to store the specified number of requested bytes.*</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2002">*Hedef arabellek uzun sözcük sınırında ise ve istenen boyut sizeof( ULONG ) ile bölünebilirse daha hızlı performans elde **edilir.***</span><span class="sxs-lookup"><span data-stu-id="34ea1-2002">*Faster performance is achieved if the destination buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2003">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2003">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2004">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2004">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-2005">**buffer_ptr:** Okuma için hedef arabelleğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2005">**buffer_ptr**: Pointer to the destination buffer for the read.</span></span>
- <span data-ttu-id="34ea1-2006">**request_size:** Okunan bayt sayısı üst sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2006">**request_size**: Maximum number of bytes to read.</span></span>
- <span data-ttu-id="34ea1-2007">**actual_size:** Sağlanan arabellekte okunan gerçek bayt sayısını tutmak için değişkenin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2007">**actual_size**: Pointer to the variable to hold the actual number of bytes read into the supplied buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2008">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2008">Return Values</span></span>

- <span data-ttu-id="34ea1-2009">**FX_SUCCESS** (0x00) Başarılı dosya okuma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2009">**FX_SUCCESS** (0x00) Successful file read.</span></span>
- <span data-ttu-id="34ea1-2010">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2010">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="34ea1-2011">**FX_FILE_CORRUPT** (0x08) Belirtilen dosya bozuk ve okuma başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2011">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the read failed.</span></span>
- <span data-ttu-id="34ea1-2012">**FX_END_OF_FILE** (0x09) Dosyanın sonuna ulaşıldı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2012">**FX_END_OF_FILE** (0x09) End of file has been reached.</span></span>
- <span data-ttu-id="34ea1-2013">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2013">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2014">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-2014">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-2015">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2015">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2016">**FX_PTR_ERROR** (0x18) Geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2016">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="34ea1-2017">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2017">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2018">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2018">Allowed From</span></span>

<span data-ttu-id="34ea1-2019">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2019">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2020">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2020">Example</span></span>

```c
FX_FILE                 my_file;
unsigned char           my_buffer[1024];
ULONG                   actual_bytes;
UINT                    status;

/* Read up to 1024 bytes into "my_buffer." */
status = fx_file_read(&my_file, my_buffer, 1024, &actual_bytes);

/* If status equals FX_SUCCESS, "my_buffer" contains the bytes
    read from the file. The total number of bytes read is in "actual_bytes." */
```
### <a name="see-also"></a><span data-ttu-id="34ea1-2021">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2021">See Also</span></span>

- <span data-ttu-id="34ea1-2022">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2022">fx_file_allocate,</span></span>
- <span data-ttu-id="34ea1-2023">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2023">fx_file_attributes_read,</span></span>
- <span data-ttu-id="34ea1-2024">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2024">fx_file_attributes_set,</span></span>
- <span data-ttu-id="34ea1-2025">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2025">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="34ea1-2026">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2026">fx_file_close,</span></span>
- <span data-ttu-id="34ea1-2027">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2027">fx_file_create,</span></span>
- <span data-ttu-id="34ea1-2028">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2028">fx_file_date_time_set,</span></span>
- <span data-ttu-id="34ea1-2029">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2029">fx_file_delete,</span></span>
- <span data-ttu-id="34ea1-2030">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2030">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="34ea1-2031">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2031">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="34ea1-2032">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2032">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="34ea1-2033">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2033">fx_file_extended_seek,</span></span>
- <span data-ttu-id="34ea1-2034">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2034">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="34ea1-2035">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2035">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="34ea1-2036">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2036">fx_file_open,</span></span>
- <span data-ttu-id="34ea1-2037">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2037">fx_file_relative_seek,</span></span>
- <span data-ttu-id="34ea1-2038">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2038">fx_file_rename,</span></span>
- <span data-ttu-id="34ea1-2039">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2039">fx_file_seek,</span></span>
- <span data-ttu-id="34ea1-2040">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2040">fx_file_truncate,</span></span>
- <span data-ttu-id="34ea1-2041">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2041">fx_file_truncate_release,</span></span>
- <span data-ttu-id="34ea1-2042">fx_file_write,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2042">fx_file_write,</span></span>
- <span data-ttu-id="34ea1-2043">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2043">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="34ea1-2044">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2044">fx_unicode_file_create,</span></span>
- <span data-ttu-id="34ea1-2045">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2045">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="34ea1-2046">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2046">fx_unicode_name_get,</span></span>
- <span data-ttu-id="34ea1-2047">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2047">fx_unicode_short_name_get</span></span>

## <a name="fx_file_relative_seek"></a><span data-ttu-id="34ea1-2048">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2048">fx_file_relative_seek</span></span>

<span data-ttu-id="34ea1-2049">Göreli bir byte uzaklığına konumlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2049">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2050">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2050">Prototype</span></span>

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="34ea1-2051">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2051">Description</span></span>

<span data-ttu-id="34ea1-2052">Bu hizmet, dahili dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2052">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="34ea1-2053">Sonraki herhangi bir dosya okuma veya yazma isteği, dosyada bu konumda başlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2053">Any subsequent file read or write request will begin at this location in the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-2054">*Arama işlemi dosyanın sonunu aramaya çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın sonuna konum sağlar. Buna karşılık, arama işlemi dosyanın başına konumlandırmaya çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başına konum sağlar.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2054">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

<span data-ttu-id="34ea1-2055">Uygulama, 4 GB'ın ötesinde bir uzaklık değeriyle arama yapmak için *fx_file_extended_relative_seek.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2055">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_relative_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2056">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2056">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2057">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2057">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-2058">**byte_offset:** Dosyada istenen göreli bayt uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2058">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="34ea1-2059">**seek_from:** Göreli aramanın nerede gerçekleştirecekleri yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2059">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="34ea1-2060">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-2060">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="34ea1-2061">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2061">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="34ea1-2062">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2062">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="34ea1-2063">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2063">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="34ea1-2064">FX_SEEK_BACK (0x03)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2064">FX_SEEK_BACK (0x03)</span></span>

<span data-ttu-id="34ea1-2065">Bir FX_SEEK_BEGIN belirtilirse, arama işlemi dosyanın başından itibaren gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2065">If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="34ea1-2066">Bir FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2066">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="34ea1-2067">Bu FX_SEEK_FORWARD, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2067">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="34ea1-2068">Bu FX_SEEK_BACK, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2068">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2069">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2069">Return Values</span></span>

- <span data-ttu-id="34ea1-2070">**FX_SUCCESS** (0x00) Başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2070">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="34ea1-2071">**FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2071">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-2072">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2072">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2073">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2074">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2075">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2075">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-2076">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2076">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-2077">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2077">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2078">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2078">Allowed From</span></span>

<span data-ttu-id="34ea1-2079">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2079">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2080">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2080">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-2081">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2081">See Also</span></span>

- <span data-ttu-id="34ea1-2082">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2082">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-2083">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2083">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-2084">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2084">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-2085">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2085">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2086">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2086">fx_file_close</span></span>
- <span data-ttu-id="34ea1-2087">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2087">fx_file_create</span></span>
- <span data-ttu-id="34ea1-2088">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2088">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-2089">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-2089">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-2090">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2090">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-2091">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2091">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2092">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2092">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-2093">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2093">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-2094">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2094">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-2095">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2095">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-2096">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2096">fx_file_open</span></span>
- <span data-ttu-id="34ea1-2097">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2097">fx_file_read</span></span>
- <span data-ttu-id="34ea1-2098">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2098">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-2099">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2099">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-2100">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2100">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-2101">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2101">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-2102">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2102">fx_file_write</span></span>
- <span data-ttu-id="34ea1-2103">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2103">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-2104">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2104">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-2105">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2105">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-2106">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2106">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-2107">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2107">fx_unicode_short_name_get</span></span>

## <a name="fx_file_rename"></a><span data-ttu-id="34ea1-2108">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2108">fx_file_rename</span></span>

<span data-ttu-id="34ea1-2109">Dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="34ea1-2109">Renames  file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2110">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2110">Prototype</span></span>

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-2111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2111">Description</span></span>

<span data-ttu-id="34ea1-2112">Bu hizmet, tarafından belirtilen dosyanın adını *old_file_name.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2112">This service changes the name of the file specified by *old_file_name*.</span></span> <span data-ttu-id="34ea1-2113">Yeniden adı, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2113">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="34ea1-2114">Yeni dosya adı içinde bir yol belirtilirse, yeniden adlandırılan dosya belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2114">If a path is specified in the new file name, the renamed file is effectively moved to the specified path.</span></span> <span data-ttu-id="34ea1-2115">Yol belirtilmezse, yeniden adlandırılan dosya geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2115">If no path is specified, the renamed file is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2116">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2116">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2117">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2117">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="34ea1-2118">**old_file_name:** Yeniden adlandıracak dosyanın adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="34ea1-2118">**old_file_name**: Pointer to the name of the file to rename (directory path is optional).</span></span>
- <span data-ttu-id="34ea1-2119">**new_file_name:** Yeni dosya adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2119">**new_file_name**: Pointer to the new file name.</span></span> <span data-ttu-id="34ea1-2120">Dizin yoluna izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2120">The directory path is not allowed.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2121">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2121">Return Values</span></span>

- <span data-ttu-id="34ea1-2122">**FX_SUCCESS** (0x00) Başarılı dosya yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2122">**FX_SUCCESS** (0x00) Successful file rename.</span></span>
- <span data-ttu-id="34ea1-2123">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2123">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2124">**FX_NOT_FOUND** (0x04) Belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2124">**FX_NOT_FOUND** (0x04)    Specified file was not found.</span></span>
- <span data-ttu-id="34ea1-2125">**FX_NOT_A_FILE** (0x05) Belirtilen dosya bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2125">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="34ea1-2126">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya zaten açık.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2126">**FX_ACCESS_ERROR** (0x06) Specified file is already open.</span></span>
- <span data-ttu-id="34ea1-2127">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2127">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2128">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2128">**FX_WRITE_PROTECT** (0x23)    Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-2129">**FX_INVALID_NAME** (0x0C) Belirtilen yeni dosya adı geçerli bir dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2129">**FX_INVALID_NAME** (0x0C) Specified new file name is not a valid file name.</span></span>
- <span data-ttu-id="34ea1-2130">**FX_INVALID_PATH** (0x0D) Yolu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2130">**FX_INVALID_PATH** (0x0D)    Path is invalid.</span></span>
- <span data-ttu-id="34ea1-2131">**FX_ALREADY_CREATED** (0x0B) Yeni dosya adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2131">**FX_ALREADY_CREATED** (0x0B) The new file name is used.</span></span>
- <span data-ttu-id="34ea1-2132">**FX_MEDIA_INVALID** (0x02) Medya geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2132">**FX_MEDIA_INVALID** (0x02)    Media is invalid.</span></span>
- <span data-ttu-id="34ea1-2133">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2133">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2134">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2134">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2135">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2135">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-2136">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-2136">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-2137">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2137">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="34ea1-2138">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2138">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-2139">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2139">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2140">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2140">Allowed From</span></span>

<span data-ttu-id="34ea1-2141">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2142">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2142">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-2143">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2143">See Also</span></span>

- <span data-ttu-id="34ea1-2144">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2144">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-2145">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2145">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-2146">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2146">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-2147">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2147">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2148">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2148">fx_file_close</span></span>
- <span data-ttu-id="34ea1-2149">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2149">fx_file_create</span></span>
- <span data-ttu-id="34ea1-2150">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2150">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-2151">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-2151">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-2152">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2152">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-2153">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2153">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2154">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2154">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-2155">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2155">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-2156">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2156">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-2157">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2157">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-2158">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2158">fx_file_open</span></span>
- <span data-ttu-id="34ea1-2159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2159">fx_file_read</span></span>
- <span data-ttu-id="34ea1-2160">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2160">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-2161">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2161">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-2162">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2162">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-2163">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2163">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-2164">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2164">fx_file_write</span></span>
- <span data-ttu-id="34ea1-2165">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2165">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-2166">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2166">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-2167">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2167">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-2168">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2168">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-2169">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2169">fx_unicode_short_name_get</span></span>

## <a name="fx_file_seek"></a><span data-ttu-id="34ea1-2170">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2170">fx_file_seek</span></span>

<span data-ttu-id="34ea1-2171">Byte uzaklığına konumlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2171">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2172">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2172">Prototype</span></span>

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a><span data-ttu-id="34ea1-2173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2173">Description</span></span>

<span data-ttu-id="34ea1-2174">Bu hizmet, dahili dosya okuma/yazma işaretçisini belirtilen byte uzaklığına konumlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2174">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="34ea1-2175">Sonraki herhangi bir dosya okuma veya yazma isteği, dosyada bu konumda başlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2175">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="34ea1-2176">Uygulama, 4 GB'ın ötesinde bir uzaklık değeriyle arama yapmak için *fx_file_extended_seek.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2176">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2177">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2177">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2178">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2178">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-2179">**byte_offset:** Dosyada istenen bayt uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2179">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="34ea1-2180">Sıfır değeri dosyanın başına okuma/yazma işaretçisini, dosyanın boyutundan büyük bir değer ise dosyanın sonuna okuma/yazma işaretçisini konumlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2180">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2181">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2181">Return Values</span></span>

- <span data-ttu-id="34ea1-2182">**FX_SUCCESS** (0x00) Başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2182">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="34ea1-2183">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2183">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="34ea1-2184">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2184">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2185">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2185">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2186">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2186">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2187">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-2187">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-2188">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2188">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-2189">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2190">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2190">Allowed From</span></span>

<span data-ttu-id="34ea1-2191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2192">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2192">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-2193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2193">See Also</span></span>

- <span data-ttu-id="34ea1-2194">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2194">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-2195">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2195">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-2196">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2196">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-2197">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2197">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2198">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2198">fx_file_close</span></span>
- <span data-ttu-id="34ea1-2199">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2199">fx_file_create</span></span>
- <span data-ttu-id="34ea1-2200">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2200">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-2201">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-2201">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-2202">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2202">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-2203">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2203">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2204">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2204">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-2205">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2205">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-2206">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2206">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-2207">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2207">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-2208">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2208">fx_file_open</span></span>
- <span data-ttu-id="34ea1-2209">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2209">fx_file_read</span></span>
- <span data-ttu-id="34ea1-2210">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2210">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-2211">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2211">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-2212">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2212">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-2213">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2213">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-2214">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2214">fx_file_write</span></span>
- <span data-ttu-id="34ea1-2215">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2215">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-2216">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2216">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-2217">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2217">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-2218">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2218">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-2219">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2219">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate"></a><span data-ttu-id="34ea1-2220">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2220">fx_file_truncate</span></span>

<span data-ttu-id="34ea1-2221">Dosyanın kesilmesi</span><span class="sxs-lookup"><span data-stu-id="34ea1-2221">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2222">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2222">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="34ea1-2223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2223">Description</span></span>

<span data-ttu-id="34ea1-2224">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar kısaltır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2224">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="34ea1-2225">Sağlanan boyut gerçek dosya boyutundan büyükse bu hizmet herhangi bir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2225">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="34ea1-2226">Dosyayla ilişkili medya kümelerinin hiçbiri yayımlenmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2226">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2227">*Aynı anda okuma için açık olan dosyaları kesme konusunda dikkatli olun. Ayrıca okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2227">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="34ea1-2228">Uygulama, 4 GB'ın ötesinde çalıştırmak için hizmet *fx_file_extended_truncate.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2228">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2229">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2229">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2230">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2230">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-2231">**size:** Yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2231">**size**: New file size.</span></span> <span data-ttu-id="34ea1-2232">Bu yeni dosya boyutunu geçen baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2232">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2233">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2233">Return Values</span></span>

- <span data-ttu-id="34ea1-2234">**FX_SUCCESS** (0x00) Başarılı dosya kesme.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2234">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="34ea1-2235">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2235">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="34ea1-2236">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2236">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-2237">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2237">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2238">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2238">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-2239">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2239">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2240">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2240">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2241">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2241">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-2242">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="34ea1-2242">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="34ea1-2243">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2243">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-2244">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2244">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2245">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2245">Allowed From</span></span>

<span data-ttu-id="34ea1-2246">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2247">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2247">Example</span></span>

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-2248">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2248">See Also</span></span>

- <span data-ttu-id="34ea1-2249">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2249">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-2250">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2250">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-2251">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2251">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-2252">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2252">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2253">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2253">fx_file_close</span></span>
- <span data-ttu-id="34ea1-2254">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2254">fx_file_create</span></span>
- <span data-ttu-id="34ea1-2255">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2255">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-2256">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-2256">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-2257">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2257">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-2258">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2258">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2259">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2259">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-2260">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2260">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-2261">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2261">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-2262">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2262">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-2263">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2263">fx_file_open</span></span>
- <span data-ttu-id="34ea1-2264">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2264">fx_file_read</span></span>
- <span data-ttu-id="34ea1-2265">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2265">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-2266">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2266">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-2267">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2267">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-2268">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2268">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-2269">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2269">fx_file_write</span></span>
- <span data-ttu-id="34ea1-2270">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2270">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-2271">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2271">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-2272">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2272">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-2273">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2273">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-2274">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2274">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate_release"></a><span data-ttu-id="34ea1-2275">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2275">fx_file_truncate_release</span></span>

<span data-ttu-id="34ea1-2276">Dosya ve yayın kümelerini keser</span><span class="sxs-lookup"><span data-stu-id="34ea1-2276">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2277">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2277">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="34ea1-2278">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2278">Description</span></span>

<span data-ttu-id="34ea1-2279">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar kısaltır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2279">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="34ea1-2280">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet herhangi bir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2280">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="34ea1-2281">Bu ***hizmet fx_file_truncate*** kullanılmayan kümeleri serbest bırakmaz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2281">Unlike the ***fx_file_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2282">*Aynı anda okuma için açık olan dosyaları kesme konusunda dikkatli olun. Ayrıca okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2282">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="34ea1-2283">Uygulama, 4 GB'ın ötesinde çalıştırmak için hizmet *fx_file_extended_truncate_release.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2283">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate_release*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2284">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2284">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2285">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2285">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="34ea1-2286">**size:** Yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2286">**size**: New file size.</span></span> <span data-ttu-id="34ea1-2287">Bu yeni dosya boyutunu geçen baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2287">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2288">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2288">Return Values</span></span>

- <span data-ttu-id="34ea1-2289">**FX_SUCCESS** (0x00) Başarılı dosya kesme.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2289">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="34ea1-2290">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2290">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-2291">**FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2291">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="34ea1-2292">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2292">**FX_IO_ERROR** (0x90)    Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2293">**FX_WRITE_PROTECT** (0x23) Temel medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2293">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="34ea1-2294">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2294">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2295">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2295">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2296">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2296">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-2297">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2297">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-2298">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2298">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation.</span></span>
- <span data-ttu-id="34ea1-2299">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2299">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="34ea1-2300">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2300">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2301">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2301">Allowed From</span></span>

<span data-ttu-id="34ea1-2302">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2303">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2303">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a><span data-ttu-id="34ea1-2304">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2304">See Also</span></span>

- <span data-ttu-id="34ea1-2305">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2305">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-2306">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2306">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-2307">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2307">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-2308">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2308">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2309">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2309">fx_file_close</span></span>
- <span data-ttu-id="34ea1-2310">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2310">fx_file_create</span></span>
- <span data-ttu-id="34ea1-2311">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2311">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-2312">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-2312">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-2313">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2313">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-2314">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2314">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2315">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2315">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-2316">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2316">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-2317">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2317">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-2318">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2318">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-2319">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2319">fx_file_open</span></span>
- <span data-ttu-id="34ea1-2320">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2320">fx_file_read</span></span>
- <span data-ttu-id="34ea1-2321">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2321">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-2322">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2322">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-2323">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2323">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-2324">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2324">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-2325">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2325">fx_file_write</span></span>
- <span data-ttu-id="34ea1-2326">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2326">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-2327">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2327">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-2328">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2328">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-2329">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2329">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-2330">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2330">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write"></a><span data-ttu-id="34ea1-2331">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2331">fx_file_write</span></span>

<span data-ttu-id="34ea1-2332">Dosyaya bayt yazar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2332">Writes bytes to file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2333">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2333">Prototype</span></span>

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="34ea1-2334">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2334">Description</span></span>

<span data-ttu-id="34ea1-2335">Bu hizmet, dosyanın geçerli konumundan başlayarak belirtilen arabellekten baytlar yazar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2335">This service writes bytes from the specified buffer starting at the file's current position.</span></span> <span data-ttu-id="34ea1-2336">Yazma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyada bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2336">After the write is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2337">*Kaynak arabelleği uzun sözcük sınırında ise ve istenen boyut sizeof( ULONG ) ile bölünebilirse daha hızlı performans elde **edilir.***</span><span class="sxs-lookup"><span data-stu-id="34ea1-2337">*Faster performance is achieved if the source buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2338">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2338">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2339">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2339">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-2340">**buffer_ptr:** Yazma için kaynak arabelleğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2340">**buffer_ptr**: Pointer to the source buffer for the write.</span></span>
- <span data-ttu-id="34ea1-2341">**boyut:** Yazacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2341">**size**: Number of bytes to write.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2342">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2342">Return Values</span></span>

- <span data-ttu-id="34ea1-2343">**FX_SUCCESS** (0x00) Başarılı dosya yazma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2343">**FX_SUCCESS** (0x00) Successful file write.</span></span>
- <span data-ttu-id="34ea1-2344">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2344">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="34ea1-2345">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2345">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="34ea1-2346">**FX_NO_MORE_SPACE** (0x0A) Bu yazma işlemini gerçekleştirmek için medyada yer yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2346">**FX_NO_MORE_SPACE** (0x0A) There is no more room available in the media to perform this write.</span></span>
- <span data-ttu-id="34ea1-2347">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2347">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2348">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2348">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-2349">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2349">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2350">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2350">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2351">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2351">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="34ea1-2352">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2352">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="34ea1-2353">**FX_PTR_ERROR** (0x18) Geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2353">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="34ea1-2354">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2354">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2355">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2355">Allowed From</span></span>

<span data-ttu-id="34ea1-2356">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2356">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2357">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2357">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-2358">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2358">See Also</span></span>

- <span data-ttu-id="34ea1-2359">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2359">fx_file_allocate,</span></span>
- <span data-ttu-id="34ea1-2360">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2360">fx_file_attributes_read,</span></span>
- <span data-ttu-id="34ea1-2361">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2361">fx_file_attributes_set,</span></span>
- <span data-ttu-id="34ea1-2362">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2362">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="34ea1-2363">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2363">fx_file_close,</span></span>
- <span data-ttu-id="34ea1-2364">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2364">fx_file_create,</span></span>
- <span data-ttu-id="34ea1-2365">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2365">fx_file_date_time_set,</span></span>
- <span data-ttu-id="34ea1-2366">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2366">fx_file_delete,</span></span>
- <span data-ttu-id="34ea1-2367">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2367">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="34ea1-2368">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2368">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="34ea1-2369">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2369">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="34ea1-2370">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2370">fx_file_extended_seek,</span></span>
- <span data-ttu-id="34ea1-2371">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2371">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="34ea1-2372">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2372">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="34ea1-2373">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2373">fx_file_open,</span></span>
- <span data-ttu-id="34ea1-2374">fx_file_read,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2374">fx_file_read,</span></span>
- <span data-ttu-id="34ea1-2375">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2375">fx_file_relative_seek,</span></span>
- <span data-ttu-id="34ea1-2376">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2376">fx_file_rename,</span></span>
- <span data-ttu-id="34ea1-2377">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2377">fx_file_seek,</span></span>
- <span data-ttu-id="34ea1-2378">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2378">fx_file_truncate,</span></span>
- <span data-ttu-id="34ea1-2379">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2379">fx_file_truncate_release,</span></span>
- <span data-ttu-id="34ea1-2380">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2380">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="34ea1-2381">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2381">fx_unicode_file_create,</span></span>
- <span data-ttu-id="34ea1-2382">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2382">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="34ea1-2383">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="34ea1-2383">fx_unicode_name_get,</span></span>
- <span data-ttu-id="34ea1-2384">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2384">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write_notify_set"></a><span data-ttu-id="34ea1-2385">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2385">fx_file_write_notify_set</span></span>

<span data-ttu-id="34ea1-2386">Dosya yazma notify işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2386">Sets the file write notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2387">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2387">Prototype</span></span>

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a><span data-ttu-id="34ea1-2388">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2388">Description</span></span>

<span data-ttu-id="34ea1-2389">Bu hizmet, başarılı bir dosya yazma işlemi sonrasında çağrılan geri çağırma işlevini yüklür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2389">This service installs callback function that is invoked after a successful file write operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2390">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2390">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2391">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2391">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="34ea1-2392">**file_write_notify:** Dosya yazma geri çağırma işlevi yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2392">**file_write_notify**: File write callback function to be installed.</span></span> <span data-ttu-id="34ea1-2393">Geri çağırma işlevini NULL olarak ayarlamak geri çağırma işlevini devre dışı bırakıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2393">Set the callback function to NULL disables the callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2394">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2394">Return Values</span></span>

- <span data-ttu-id="34ea1-2395">**FX_SUCCESS** (0x00) Geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2395">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="34ea1-2396">**FX_PTR_ERROR** (0x18) file_ptr NULL olur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2396">**FX_PTR_ERROR** (0x18) file_ptr is NULL.</span></span>
- <span data-ttu-id="34ea1-2397">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2397">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2398">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2398">Allowed From</span></span>

<span data-ttu-id="34ea1-2399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2400">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2400">Example</span></span>

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2401">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2401">See Also</span></span>

- <span data-ttu-id="34ea1-2402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2402">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-2403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2403">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-2404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2404">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-2405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2406">fx_file_close</span></span>
- <span data-ttu-id="34ea1-2407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2407">fx_file_create</span></span>
- <span data-ttu-id="34ea1-2408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2408">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-2409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-2409">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-2410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-2411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-2412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-2413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2413">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-2414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-2415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-2416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2416">fx_file_open</span></span>
- <span data-ttu-id="34ea1-2417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2417">fx_file_read</span></span>
- <span data-ttu-id="34ea1-2418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2418">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-2419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2419">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-2420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2420">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-2421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2421">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-2422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-2422">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-2423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2423">fx_file_write</span></span>
- <span data-ttu-id="34ea1-2424">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-2424">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-2425">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-2425">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-2426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2426">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-2427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2427">fx_unicode_short_name_get</span></span>

## <a name="fx_media_abort"></a><span data-ttu-id="34ea1-2428">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2428">fx_media_abort</span></span>

<span data-ttu-id="34ea1-2429">Medya etkinliklerini iptal eder</span><span class="sxs-lookup"><span data-stu-id="34ea1-2429">Aborts media activities</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2430">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2430">Prototype</span></span>

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-2431">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2431">Description</span></span>

<span data-ttu-id="34ea1-2432">Bu hizmet, tüm açık dosyaları kapatma, ilişkili sürücüye bir iptal isteği gönderme ve medyayı durdurulmuş duruma yerleştirme dahil olmak üzere medyayla ilişkili tüm geçerli etkinlikleri iptal eder.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2432">This service aborts all current activities associated with the media, including closing all open files, sending an abort request to the associated driver, and placing the media in an aborted state.</span></span> <span data-ttu-id="34ea1-2433">Bu hizmet genellikle g/ç hataları algılandığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2433">This service is typically called when I/O errors are detected.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2434">*Bir iptal işlemi gerçekleştirildikten sonra yeniden kullanmak için medyanın yeniden açılması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2434">*The media must be re-opened to use it again after an abort operation is performed.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2435">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2435">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2436">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2436">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2437">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2437">Return Values</span></span>

- <span data-ttu-id="34ea1-2438">**FX_SUCCESS** (0x00) başarılı medya iptali.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2438">**FX_SUCCESS** (0x00) Successful media abort.</span></span>
- <span data-ttu-id="34ea1-2439">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2439">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2440">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2440">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-2441">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2441">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2442">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2442">Allowed From</span></span>

<span data-ttu-id="34ea1-2443">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2444">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2444">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2445">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2445">See Also</span></span>

- <span data-ttu-id="34ea1-2446">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2446">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2447">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2447">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2448">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2448">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2449">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2449">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2450">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2450">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2451">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2451">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2452">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2452">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2453">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2453">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2454">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2454">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2455">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2455">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2456">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2456">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2457">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2457">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2458">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2458">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2459">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2459">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2460">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2460">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2461">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2461">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2462">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2462">fx_system_initialize</span></span>

## <a name="fx_media_cache_invalidate"></a><span data-ttu-id="34ea1-2463">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2463">fx_media_cache_invalidate</span></span>

<span data-ttu-id="34ea1-2464">Mantıksal kesim önbelleğini geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2464">Invalidates logical sector cache</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2465">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2465">Prototype</span></span>

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="34ea1-2466">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2466">Description</span></span>

<span data-ttu-id="34ea1-2467">Bu hizmet önbellekteki tüm kirli kesimleri temizler ve sonra mantıksal kesim önbelleğinin tamamını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2467">This service flushes all dirty sectors in the cache and then invalidates the entire logical sector cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2468">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2468">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2469">**media_ptr**: medya denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="34ea1-2469">**media_ptr**: Pointer to media control block</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2470">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2470">Return Values</span></span>

- <span data-ttu-id="34ea1-2471">**FX_SUCCESS** (0x00) başarılı medya önbelleği geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2471">**FX_SUCCESS** (0x00) Successful media cache invalidate.</span></span>
- <span data-ttu-id="34ea1-2472">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2472">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2473">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2473">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2474">**FX_PTR_ERROR** (0x18) geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2474">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="34ea1-2475">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2475">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2476">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2476">Allowed From</span></span>

<span data-ttu-id="34ea1-2477">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2478">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2478">Example</span></span>

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2479">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2479">See Also</span></span>

- <span data-ttu-id="34ea1-2480">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2480">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2481">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2481">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2482">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2482">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2483">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2483">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2484">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2484">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2485">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2485">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2486">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2486">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2487">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2487">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2488">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2488">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2489">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2489">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2490">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2490">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2491">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2491">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2492">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2492">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2493">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2493">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2494">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2494">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2495">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2495">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2496">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2496">fx_system_initialize</span></span>

## <a name="fx_media_check"></a><span data-ttu-id="34ea1-2497">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2497">fx_media_check</span></span>

<span data-ttu-id="34ea1-2498">Medyayı hatalara karşı denetler</span><span class="sxs-lookup"><span data-stu-id="34ea1-2498">Checks media for errors</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2499">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2499">Prototype</span></span>

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-2500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2500">Description</span></span>

<span data-ttu-id="34ea1-2501">Bu hizmet, dosya/dizin çapraz bağlantı, geçersiz FAT zincirleri ve kayıp kümeler gibi temel yapısal hatalar için belirtilen medyayı denetler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2501">This service checks the specified media for basic structural errors, including file/directory cross-linking, invalid FAT chains, and lost clusters.</span></span> <span data-ttu-id="34ea1-2502">Bu hizmet ayrıca algılanan hataları düzeltme olanağı da sağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2502">This service also provides the capability to correct detected errors.</span></span>

<span data-ttu-id="34ea1-2503">Fx_media_check hizmeti, medyada dizinlerin ve dosyaların derinlik ilk analizi için karalama belleği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2503">The fx_media_check service requires scratch memory for its depth-first analysis of directories and files in the media.</span></span> <span data-ttu-id="34ea1-2504">Özellikle, medya denetimi hizmetine sağlanan karalama belleği birkaç dizin girişini, alt dizinlere girmeden önce geçerli dizin giriş konumunu "yığacak" bir veri yapısı ve son olarak mantıksal FAT bit eşlemesini tutacak kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2504">Specifically, the scratch memory supplied to the media check service must be large enough to hold several directory entries, a data structure to "stack" the current directory entry position before entering into subdirectories, and finally the logical FAT bit map.</span></span> <span data-ttu-id="34ea1-2505">Karalama belleği en az 512-1024 bayt ve mantıksal FAT bit eşlemesi için bellek olmalıdır. Bu, medyada kümeler olduğu kadar bit gerektirir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2505">The scratch memory should be at least 512-1024 bytes plus memory for the logical FAT bit map, which requires as many bits as there are clusters in the media.</span></span> <span data-ttu-id="34ea1-2506">Örneğin, 8000 kümeye sahip bir cihazın temsili için 1000 bayt gerekir ve bu nedenle 2048 bayt sırasına göre toplam karalama alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2506">For example, a device with 8000 clusters would require 1000 bytes to represent and thus require a total scratch area on the order of 2048 bytes.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2507">*Bu hizmet yalnızca herhangi bir dosya sistemi etkinliği fx_media_open hemen çağrılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2507">*This service should only be called immediately after fx_media_open and without any other file system activity.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2508">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2508">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2509">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2509">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-2510">**scratch_memory_ptr:** Karalama belleğinin başlangıcına işaret.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2510">**scratch_memory_ptr**: Pointer to the start of scratch memory.</span></span>
- <span data-ttu-id="34ea1-2511">**scratch_memory_size:** Karalama belleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2511">**scratch_memory_size**: Size of scratch memory in bytes.</span></span>
- <span data-ttu-id="34ea1-2512">**error_correction_option:** Hata düzeltme seçeneği bitleri, bit ayarlanırken hata düzeltmesi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2512">**error_correction_option**: Error correction option bits, when the bit is set, error correction is performed.</span></span> <span data-ttu-id="34ea1-2513">Hata düzeltme seçeneği bitleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-2513">The error correction option bits are defined as follows:</span></span>
  - <span data-ttu-id="34ea1-2514">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2514">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="34ea1-2515">FX_DIRECTORY_ERROR (0x02)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2515">FX_DIRECTORY_ERROR (0x02)</span></span>
  - <span data-ttu-id="34ea1-2516">FX_LOST_CLUSTER_ERROR (0x04) Basitçe OR ile gerekli hata düzeltme seçeneklerini birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2516">FX_LOST_CLUSTER_ERROR (0x04) Simply OR together the required error correction options.</span></span> <span data-ttu-id="34ea1-2517">Hata düzeltmesi gerekmiyorsa 0 değeri sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2517">If no error correction is required, a value of 0 should be supplied.</span></span>
- <span data-ttu-id="34ea1-2518">**errors_detected_ptr:** Aşağıda tanımlandığı gibi hata algılama bitleri için hedef:</span><span class="sxs-lookup"><span data-stu-id="34ea1-2518">**errors_detected_ptr**: Destination for error detection bits, as defined below:</span></span>
  - <span data-ttu-id="34ea1-2519">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2519">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="34ea1-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span></span>
  - <span data-ttu-id="34ea1-2521">FX_FILE_SIZE_ERROR (0x08)</span><span class="sxs-lookup"><span data-stu-id="34ea1-2521">FX_FILE_SIZE_ERROR (0x08)</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2522">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2522">Return Values</span></span>

- <span data-ttu-id="34ea1-2523">**FX_SUCCESS** (0x00) Başarılı medya denetimi, ayrıntılar için algılanan hataları görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2523">**FX_SUCCESS** (0x00) Successful media check, view the errors detected destination for details.</span></span>
- <span data-ttu-id="34ea1-2524">**FX_ACCESS_ERROR** (0x06) Açık dosyalarda denetim gerçekleştiremiyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2524">**FX_ACCESS_ERROR** (0x06) Unable to perform check with open files.</span></span>
- <span data-ttu-id="34ea1-2525">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2525">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2526">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2526">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2527">**FX_NO_MORE_SPACE** (0x0A) Medyada daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2527">**FX_NO_MORE_SPACE** (0x0A) No more space on the media.</span></span>
- <span data-ttu-id="34ea1-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) Sağlanan karalama belleği yeterince büyük değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) Supplied scratch memory is not large enough.</span></span>
- <span data-ttu-id="34ea1-2529">**FX_ERROR_NOT_FIXED** (0x93) FAT32 kök dizininin düzeltilenemleri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2529">**FX_ERROR_NOT_FIXED** (0x93) Corruption of FAT32 root directory that could not be fixed.</span></span>
- <span data-ttu-id="34ea1-2530">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2531">**FX_SECTOR_INVALID** (0x89) Kesimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2531">**FX_SECTOR_INVALID** (0x89) Sector is invalid.</span></span>
- <span data-ttu-id="34ea1-2532">**FX_PTR_ERROR** (0x18) Geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2532">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="34ea1-2533">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="34ea1-2534">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2534">Allowed From</span></span>

<span data-ttu-id="34ea1-2535">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2536">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2536">Example</span></span>

```c
FX_MEDIA         my_media;
ULONG             detected_errors;
UCHAR             sratch_memory[4096];

/* Check the media and correct all errors. */

status = fx_media_check(&my_media, sratch_memory, 4096,
                        FX_FAT_CHAIN_ERROR |
                        FX_DIRECTORY_ERROR |
                        FX_LOST_CLUSTER_ERROR, &detected_errors);

/* If status is FX_SUCCESS and detected_errors is 0,
    the media was successfully checked and found to be error free. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2537">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2537">See Also</span></span>

- <span data-ttu-id="34ea1-2538">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2538">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2539">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2539">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2540">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2540">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2541">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2541">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2542">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2542">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2543">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2543">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2544">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2544">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2545">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2545">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2546">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2546">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2547">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2547">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2548">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2548">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2549">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2549">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2550">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2550">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2551">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2551">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2552">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2552">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2553">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2553">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2554">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2554">fx_system_initialize</span></span>

## <a name="fx_media_close"></a><span data-ttu-id="34ea1-2555">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2555">fx_media_close</span></span>

<span data-ttu-id="34ea1-2556">Medyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="34ea1-2556">Closes media</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2557">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2557">Prototype</span></span>

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-2558">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2558">Description</span></span>

<span data-ttu-id="34ea1-2559">Bu hizmet, belirtilen medyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2559">This service closes the specified media.</span></span> <span data-ttu-id="34ea1-2560">Medyayı kapatma işlemi sırasında, tüm açık dosyalar kapatılır ve kalan arabellekler fiziksel medyaya boşaltılmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2560">In the process of closing the media, all open files are closed and any remaining buffers are flushed to the physical media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2561">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2561">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2562">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2562">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2563">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2563">Return Values</span></span>

- <span data-ttu-id="34ea1-2564">**FX_SUCCESS** (0x00) Başarılı medya kapatma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2564">**FX_SUCCESS** (0x00) Successful media close.</span></span>
- <span data-ttu-id="34ea1-2565">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2565">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2566">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2566">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2567">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2567">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-2568">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2568">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2569">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2569">Allowed From</span></span>

<span data-ttu-id="34ea1-2570">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2571">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2571">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2572">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2572">See Also</span></span>

- <span data-ttu-id="34ea1-2573">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2573">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2574">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2574">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2575">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2575">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2576">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2576">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2577">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2577">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2578">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2578">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2579">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2579">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2580">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2580">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2581">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2581">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2582">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2582">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2583">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2583">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2584">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2584">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2585">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2585">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2586">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2586">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2587">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2587">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2588">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2588">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2589">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2589">fx_system_initialize</span></span>

## <a name="fx_media_close_notify_set"></a><span data-ttu-id="34ea1-2590">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2590">fx_media_close_notify_set</span></span>

<span data-ttu-id="34ea1-2591">Medya kapatma notify işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2591">Sets the media close notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2592">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2592">Prototype</span></span>

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a><span data-ttu-id="34ea1-2593">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2593">Description</span></span>

<span data-ttu-id="34ea1-2594">Bu hizmet, bir medya başarıyla kapatıldıktan sonra çağrılan bir notify callback işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2594">This service sets a notify callback function which will be invoked after a media is successfully closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2595">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2595">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2596">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2596">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-2597">**media_close_notify:** Medya kapatma bildirimi geri çağırma işlevinin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2597">**media_close_notify**: Media close notify callback function to be installed.</span></span> <span data-ttu-id="34ea1-2598">Geri çağırma işlevi olarak NULL değerinin geçişini medya kapatma geri çağırmasını devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2598">Passing NULL as the callback function disables the media close callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2599">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2599">Return Values</span></span>

- <span data-ttu-id="34ea1-2600">**FX_SUCCESS** (0x00) Geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2600">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="34ea1-2601">**FX_PTR_ERROR** (0x18) media_ptr NULL olur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2601">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="34ea1-2602">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2602">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2603">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2603">Allowed From</span></span>

<span data-ttu-id="34ea1-2604">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2604">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2605">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2605">Example</span></span>

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a><span data-ttu-id="34ea1-2606">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2606">See Also</span></span>

- <span data-ttu-id="34ea1-2607">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2607">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2608">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2608">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2609">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2609">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2610">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2610">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2611">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2611">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2612">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2612">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2613">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2613">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2614">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2614">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2615">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2615">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2616">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2616">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2617">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2617">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2618">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2618">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2619">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2619">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2620">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2620">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2621">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2621">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2622">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2622">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2623">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2623">fx_system_initialize</span></span>

## <a name="fx_media_exfat_format"></a><span data-ttu-id="34ea1-2624">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2624">fx_media_exFAT_format</span></span>

<span data-ttu-id="34ea1-2625">Medyayı biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="34ea1-2625">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2626">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2626">Prototype</span></span>

```c
UINT fx_media_exFAT_format(
    FX_MEDIA *media_ptr,
    VOID (*driver)(FX_MEDIA *media),
    VOID *driver_info_ptr, 
    UCHAR *memory_ptr,
    UINT memory_size, 
    CHAR *volume_name,
    UINT number_of_fats,
    ULONG64 hidden_sectors, 
    ULONG64 total_sectors,
    UINT bytes_per_sector, 
    UINT sectors_per_cluster,
    UINT volume_serial_number, 
    UINT boundary_unit);
```
### <a name="description"></a><span data-ttu-id="34ea1-2627">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2627">Description</span></span>

<span data-ttu-id="34ea1-2628">Bu hizmet sağlanan medyayı sağlanan parametrelere göre exFAT uyumlu bir şekilde biçimler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2628">This service formats the supplied media in an exFAT compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="34ea1-2629">Medya açılmadan önce bu hizmetin çağrılsı gerekir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2629">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2630">*Zaten biçimlendirilmiş bir medyayı biçimlendirmek, medyanın tüm dosyalarını ve dizinlerini etkili bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2630">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-2631">*ExFAT birim boyutu bölümün boyutuyla (MBR veya GPT düzeni varsa) veya bölüm düzeni yoksa (MBR veya GPT yoksa) cihazın boyutuyla eşleşmesi gerekir. Kullanılabilir kesimlerden Windows toplam kesim değerleriyle biçimlendirildiklerinde exFAT Disk'in yeniden tanınmamasıyla ilgili bir sınırlama vardır*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2631">*The exFAT volume size should match the size of the partition (if there is an MBR or GPT layout), or the size of the whole device if there is no partition layout (no MBR or GPT). There is a limitation on Windows that exFAT Disk will not be recoginzed if formatted with some values of total sectors that are less than available sectors*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2632">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2632">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2633">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2633">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="34ea1-2634">Bu yalnızca sürücünün çalışması için gereken bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2634">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="34ea1-2635">**driver:** Bu medya için I/O sürücüsünün işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2635">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="34ea1-2636">Bu genellikle sonraki çağrıya sağlanan sürücü fx_media_open olur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2636">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="34ea1-2637">**driver_info_ptr:** I/Ç sürücüsünün kullanabiliyor olduğu isteğe bağlı bilgilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2637">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="34ea1-2638">**memory_ptr:** Medya için çalışan belleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2638">**memory_ptr**: Pointer to the working memory for the media.</span></span> <span data-ttu-id="34ea1-2639">memory_size Çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2639">memory_size Specifies the size of the working media memory.</span></span> <span data-ttu-id="34ea1-2640">Boyutun en azından medyanın kesim boyutu kadar büyük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2640">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="34ea1-2641">**volume_name:** En fazla 11 karakter uzunluğunda olan birim adı dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2641">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="34ea1-2642">**number_of_fats:** Medyada SSS sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2642">**number_of_fats**: Number of FATs on the media.</span></span> <span data-ttu-id="34ea1-2643">Geçerli uygulama medyada bir FAT'i destekler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2643">Current implementation supports one FAT on the media.</span></span>
- <span data-ttu-id="34ea1-2644">**hidden_sectors:** Bu medyanın önyükleme kesimi öncesinde gizlenen kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2644">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="34ea1-2645">Bu durum, birden çok bölüm olduğunda normaldir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2645">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="34ea1-2646">**total_sectors:** Medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2646">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="34ea1-2647">**bytes_per_sector:** Genellikle 512 olan kesim başına bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2647">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="34ea1-2648">FileX için bunun 32'nin katları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2648">FileX requires this to be a multiple of 32.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="34ea1-2649">*Belirtim başvurusuyla, kesim başına bayt sayısı yalnızca şu değerleri alır: 512, 1024, 2048 veya 4096.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2649">*With reference to the specification the bytes per sector may take on only the following values: 512, 1024, 2048 or 4096.*</span></span>

- <span data-ttu-id="34ea1-2650">**sectors_per_cluster:** Her kümede kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2650">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="34ea1-2651">Küme, FAT dosya sistemi içinde en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2651">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="34ea1-2652">**volumne_serial_number:** Bu birim için kullanılacak seri numarası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2652">**volumne_serial_number**: Serial number to be used for this volume.</span></span>
- <span data-ttu-id="34ea1-2653">**boundary_unit:** Kesim sayısı olarak fiziksel veri alanı hizalama boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2653">**boundary_unit**: Physical data area alignment size, in number of sectors.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2654">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2654">Return Values</span></span>

- <span data-ttu-id="34ea1-2655">**FX_SUCCESS** (0x00) Başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2655">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="34ea1-2656">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2656">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2657">**FX_PTR_ERROR** (0x18) Geçersiz medya, sürücü veya bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2657">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="34ea1-2658">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2658">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2659">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2659">Allowed From</span></span>

<span data-ttu-id="34ea1-2660">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2660">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2661">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2661">Example</span></span>

```c
FX_MEDIA             sd_card;
UCHAR                 media_memory[512];

/* Format a 64GB SD card with exFAT file system. The media has
    been properly partitioned, with the partition starts from sector 32768.
    For 64GB, there are total of 120913920 sectors, each sector 512 bytes. */

status = fx_media_exFAT_format(&sd_card, _fx_sd_driver,
                                driver_information, media_memory,
                                sizeof(media_memory),
                                "exFAT_DISK" /* Volume Name */,
                                1 /* Number of FATs */,
                                32768 /* Hidden sectors */,
                                120913920 /* Total sectors */,
                                512 /* Sector size */,
                                256 /* Sectors per cluster */,
                                12345 /* Volume ID */,
                                8192 /* Boundary unit */);

/* If status is FX_SUCCESS, the media was successfully formatted. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2662">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2662">See Also</span></span>

- <span data-ttu-id="34ea1-2663">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2663">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2664">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2664">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2665">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2665">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2666">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2666">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2667">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2667">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2668">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2668">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2669">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2669">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2670">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2670">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2671">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2671">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2672">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2672">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2673">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2673">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2674">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2674">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2675">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2675">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2676">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2676">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2677">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2677">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2678">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2678">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2679">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2679">fx_system_initialize</span></span>

## <a name="fx_media_extended_space_available"></a><span data-ttu-id="34ea1-2680">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2680">fx_media_extended_space_available</span></span>

<span data-ttu-id="34ea1-2681">Kullanılabilir medya alanı döndürür</span><span class="sxs-lookup"><span data-stu-id="34ea1-2681">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2682">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2682">Prototype</span></span>

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-2683">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2683">Description</span></span>

<span data-ttu-id="34ea1-2684">Bu hizmet, medyada kullanılabilir bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2684">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="34ea1-2685">Bu hizmet exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2685">This service is designed for exFAT.</span></span> <span data-ttu-id="34ea1-2686">Available_bytes *parametresinin işaretçisi,* çağıranın 4 GB aralığının ötesindeki medyayla çalışmasına olanak sağlayan 64 bit tamsayı değerini alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2686">The pointer to *available_bytes* parameter takes a 64-bit integer value, which allows the caller to work with media beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2687">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2687">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2688">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2688">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="34ea1-2689">**available_bytes_ptr:** Medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2689">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2690">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2690">Return Values</span></span>

- <span data-ttu-id="34ea1-2691">**FX_SUCCESS** (0x00) Medyada kullanılabilir alan başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2691">**FX_SUCCESS** (0x00) Successfully retrieved space available on the media.</span></span>
- <span data-ttu-id="34ea1-2692">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2692">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2693">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi NULL.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2693">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="34ea1-2694">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2694">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2695">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2695">Allowed From</span></span>

<span data-ttu-id="34ea1-2696">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2696">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2697">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2697">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2698">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2698">See Also</span></span>

- <span data-ttu-id="34ea1-2699">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2699">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2700">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2700">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2701">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2701">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2702">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2702">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2703">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2703">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2704">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2704">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2705">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2705">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2706">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2706">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2707">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2707">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2708">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2708">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2709">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2709">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2710">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2710">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2711">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2711">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2712">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2712">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2713">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2713">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2714">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2714">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2715">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2715">fx_system_initialize</span></span>

## <a name="fx_media_flush"></a><span data-ttu-id="34ea1-2716">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2716">fx_media_flush</span></span>

<span data-ttu-id="34ea1-2717">Fiziksel medyada verileri boşaltır</span><span class="sxs-lookup"><span data-stu-id="34ea1-2717">Flushes data to physical media</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2718">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2718">Prototype</span></span>

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-2719">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2719">Description</span></span>

<span data-ttu-id="34ea1-2720">Bu hizmet, herhangi bir değiştirilen dosyanın tüm önbelleğe alınan kesimlerini ve dizin girdilerini fiziksel medyada boşaltır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2720">This service flushes all cached sectors and directory entries of any modified files to the physical media.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2721">*Bu yordam, hedef üzerinde ani bir güç kaybı olması durumunda dosya bozulması ve/veya veri kaybı riskini azaltmak için uygulama tarafından düzenli aralıklarla çağrılabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2721">*This routine may be called periodically by the application to reduce the risk of file corruption and/or data loss in the event of a sudden loss of power on the target.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2722">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2722">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2723">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2723">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2724">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2724">Return Values</span></span>

- <span data-ttu-id="34ea1-2725">**FX_SUCCESS** (0x00) başarılı medya Temizleme.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2725">**FX_SUCCESS** (0x00) Successful media flush.</span></span>
- <span data-ttu-id="34ea1-2726">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2726">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2727">**FX_FILE_CORRUPT**    (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2727">**FX_FILE_CORRUPT**    (0x08) File is corrupted.</span></span>
- <span data-ttu-id="34ea1-2728">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2728">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2729">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2729">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2730">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2730">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-2731">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2731">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-2732">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2732">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2733">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2733">Allowed From</span></span>

<span data-ttu-id="34ea1-2734">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2734">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2735">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2735">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2736">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2736">See Also</span></span>

- <span data-ttu-id="34ea1-2737">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2737">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2738">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2738">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2739">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2739">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2740">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2740">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2741">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2741">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2742">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2742">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2743">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2743">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2744">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2744">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2745">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2745">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2746">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2746">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2747">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2747">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2748">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2748">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2749">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2749">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2750">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2750">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2751">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2751">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2752">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2752">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2753">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2753">fx_system_initialize</span></span>

## <a name="fx_media_format"></a><span data-ttu-id="34ea1-2754">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2754">fx_media_format</span></span>

<span data-ttu-id="34ea1-2755">Medyayı biçimlendirir</span><span class="sxs-lookup"><span data-stu-id="34ea1-2755">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2756">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2756">Prototype</span></span>

```c
UINT fx_media_format(
    FX_MEDIA *media_ptr,
    VOID (*driver)(FX_MEDIA *media),
    VOID *driver_info_ptr,
    UCHAR *memory_ptr, 
    UINT memory_size,
    CHAR *volume_name, 
    UINT number_of_fats,
    UINT directory_entries, 
    UINT hidden_sectors,
    ULONG total_sectors, 
    UINT bytes_per_sector,
    UINT sectors_per_cluster,
    UINT heads,
    UINT sectors_per_track);
```
### <a name="description"></a><span data-ttu-id="34ea1-2757">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2757">Description</span></span>

<span data-ttu-id="34ea1-2758">Bu hizmet verilen medyayı sağlanan parametrelere göre FAT 12/16/32 ile uyumlu bir şekilde biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2758">This service formats the supplied media in a FAT 12/16/32 compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="34ea1-2759">Medyayı açmadan önce bu hizmetin çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2759">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2760">*Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2760">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2761">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2761">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2762">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2762">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="34ea1-2763">Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2763">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="34ea1-2764">**sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2764">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="34ea1-2765">Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2765">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="34ea1-2766">**driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2766">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="34ea1-2767">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2767">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="34ea1-2768">**memory_size**: çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2768">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="34ea1-2769">Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2769">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="34ea1-2770">**Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2770">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="34ea1-2771">**number_of_fats**: medyadaki Fats sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2771">**number_of_fats**: Number of FATs in the media.</span></span> <span data-ttu-id="34ea1-2772">Birincil FAT için en düşük değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2772">The minimal value is 1 for the primary FAT.</span></span> <span data-ttu-id="34ea1-2773">1 ' den büyük değerler, çalışma zamanında sürdürülmekte olan ek FAT kopyalarla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2773">Values greater than 1 result in additional FAT copies being maintained at run-time.</span></span>
- <span data-ttu-id="34ea1-2774">**directory_entries**: kök dizindeki Dizin girişi sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2774">**directory_entries**: Number of directory entries in the root directory.</span></span>
- <span data-ttu-id="34ea1-2775">**hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2775">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="34ea1-2776">Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2776">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="34ea1-2777">**total_sectors**: medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2777">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="34ea1-2778">**bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2778">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="34ea1-2779">FileX, bunun 32 katı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2779">FileX requires this to be a multiple of 32.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="34ea1-2780">*Belirtime başvuru ile kesim başına bayt yalnızca şu değerleri alabilir: 512, 1024, 2048 veya 4096.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2780">*With reference to the specification the bytes per sector may take on only the following values: 512, 1024, 2048 or 4096.*</span></span>

- <span data-ttu-id="34ea1-2781">**sectors_per_cluster**: her kümedeki sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2781">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="34ea1-2782">Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2782">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="34ea1-2783">**Heads**: fiziksel kafa sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2783">**heads**: Number of physical heads.</span></span>
- <span data-ttu-id="34ea1-2784">**sectors_per_track**: iz başına kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2784">**sectors_per_track**: Number of sectors per track.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2785">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2785">Return Values</span></span>

- <span data-ttu-id="34ea1-2786">**FX_SUCCESS** (0x00) başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2786">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="34ea1-2787">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2787">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2788">**FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2788">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="34ea1-2789">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2789">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2790">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2790">Allowed From</span></span>

<span data-ttu-id="34ea1-2791">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2791">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2792">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2792">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             media_memory[512];
UCHAR             ram_disk_memory[32768];

/* Format a RAM disk with 32768 bytes and 512 bytes per sector. */

status = fx_media_format(&ram_disk, _fx_ram_driver,
                         ram_disk_memory, media_memory,
                         sizeof(media_memory),
                         "MY_RAM_DISK" /* Volume Name */,
                         1 /* Number of FATs */,
                         32 /* Directory Entries */,
                         0 /* Hidden sectors */,
                         64 /* Total sectors */,
                         512 /* Sector size */,
                         1 /* Sectors per cluster */,
                         1 /* Heads */,
                         1 /* Sectors per track */);

/* If status is FX_SUCCESS, the media was successfully formatted
    and can now be opened with the following call: */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2793">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2793">See Also</span></span>

- <span data-ttu-id="34ea1-2794">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2794">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2795">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2795">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2796">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2796">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2797">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2797">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2798">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2798">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2799">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2799">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2800">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2800">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2801">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2801">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2802">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2802">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2803">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2803">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2804">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2804">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2805">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2805">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2806">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2806">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2807">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2807">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2808">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2808">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2809">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2809">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2810">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2810">fx_system_initialize</span></span>

## <a name="fx_media_open"></a><span data-ttu-id="34ea1-2811">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2811">fx_media_open</span></span>

<span data-ttu-id="34ea1-2812">Dosya erişimi için medyayı açar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2812">Opens media for file access</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2813">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2813">Prototype</span></span>

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a><span data-ttu-id="34ea1-2814">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2814">Description</span></span>

<span data-ttu-id="34ea1-2815">Bu hizmet, sağlanan I/O sürücüsünü kullanarak dosya erişimi için bir medya açar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2815">This service opens a media for file access using the supplied I/O driver.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-2816">*Bu hizmete sağlanan bellek iç mantıksal kesim önbelleğini uygulamak için kullanılır, bu nedenle bellek ne kadar fazla bellek sağlanırsa O kadar fazla fiziksel I/O azalır. FileX için en az bir mantıksal kesim (medya kesimi başına bayt) önbelleği gerekir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2816">*The memory supplied to this service is used to implement an internal logical sector cache, hence, the more memory supplied the more physical I/O is reduced. FileX requires a cache of at least one logical sector (bytes per sector of the media).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2817">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2817">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2818">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2818">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-2819">**media_name:** Medyanın adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2819">**media_name**: Pointer to media's name.</span></span>
- <span data-ttu-id="34ea1-2820">**media_driver:** Bu medya için I/O sürücüsünün işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2820">**media_driver**: Pointer to I/O driver for this media.</span></span> <span data-ttu-id="34ea1-2821">I/O sürücüsünün Bölüm 5'te tanımlanan FileX sürücü gereksinimlerine uyması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2821">The I/O driver must conform to FileX driver requirements defined in Chapter 5.</span></span>
- <span data-ttu-id="34ea1-2822">**driver_info_ptr:** Sağlanan I/Ç sürücüsünün kullanabiliyor olduğu isteğe bağlı bilgilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2822">**driver_info_ptr**: Pointer to optional information that the supplied I/O driver may utilize.</span></span>
- <span data-ttu-id="34ea1-2823">**memory_ptr:** Medya için çalışan belleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2823">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="34ea1-2824">**memory_size:** Çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2824">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="34ea1-2825">Boyut, medyanın kesim boyutu (genellikle 512 bayt) kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2825">The size must be as large as the media's sector size (typically 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2826">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2826">Return Values</span></span>

- <span data-ttu-id="34ea1-2827">**FX_SUCCESS** (0x00) Başarılı medya açma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2827">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="34ea1-2828">**FX_BOOT_ERROR** (0x01) Medyanın önyükleme kesimi okuma hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2828">**FX_BOOT_ERROR** (0x01) Error reading the media's boot sector.</span></span>
- <span data-ttu-id="34ea1-2829">**FX_MEDIA_INVALID** (0x02) Belirtilen medyanın önyükleme kesimi bozuk veya geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2829">**FX_MEDIA_INVALID** (0x02) Specified media's boot sector is corrupt or invalid.</span></span> <span data-ttu-id="34ea1-2830">Ayrıca, bu dönüş kodu mantıksal kesim önbellek boyutunun veya FAT giriş boyutunun 2'nin gücü olmadığını belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2830">In addition, this return code is used to indicate that either the logical sector cache size or the FAT entry size is not a power of 2.</span></span>
- <span data-ttu-id="34ea1-2831">**FX_FAT_READ_ERROR** FAT 0x03 okuma hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2831">**FX_FAT_READ_ERROR** (0x03) Error reading the media FAT.</span></span>
- <span data-ttu-id="34ea1-2832">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2832">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2833">**FX_PTR_ERROR** (0x18) Bir veya daha fazla işaretçi NULL olur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2833">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="34ea1-2834">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2834">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2835">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2835">Allowed From</span></span>

<span data-ttu-id="34ea1-2836">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2836">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2837">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2837">Example</span></span>

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2838">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2838">See Also</span></span>

- <span data-ttu-id="34ea1-2839">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2839">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2840">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2840">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2841">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2841">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2842">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2842">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2843">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2843">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2844">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2844">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2845">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2845">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2846">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2846">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2847">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2847">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2848">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2848">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2849">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2849">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2850">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2850">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2851">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2851">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2852">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2852">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2853">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2853">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2854">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2854">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2855">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2855">fx_system_initialize</span></span>

## <a name="fx_media_open_notify_set"></a><span data-ttu-id="34ea1-2856">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2856">fx_media_open_notify_set</span></span>

<span data-ttu-id="34ea1-2857">Medya açık notify işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-2857">Sets the media open notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2858">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2858">Prototype</span></span>

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a><span data-ttu-id="34ea1-2859">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2859">Description</span></span>

<span data-ttu-id="34ea1-2860">Bu hizmet, bir medya başarıyla açıldıktan sonra çağrılan bir notify callback işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2860">This service sets a notify callback function which will be invoked after a media is successfully opened.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2861">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2861">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2862">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2862">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-2863">**media_open_notify:** Medya aç notify callback işlevi yüklenmek için.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2863">**media_open_notify**: Media open notify callback function to be installed.</span></span> <span data-ttu-id="34ea1-2864">Geri çağırma işlevi olarak NULL değerinin geçirmesi, medya açık geri çağırmayı devre dışı bırakmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2864">Passing NULL as the callback function disables the media open callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2865">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2865">Return Values</span></span>


- <span data-ttu-id="34ea1-2866">**FX_SUCCESS** (0x00) Geri çağırma işlevi başarılı bir şekilde yüklendi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2866">**FX_SUCCESS** (0x00) Successfuly installed the callback function.</span></span>
- <span data-ttu-id="34ea1-2867">**FX_PTR_ERROR** (0x18) media_ptr NULL olur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2867">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="34ea1-2868">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2868">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2869">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2869">Allowed From</span></span>

<span data-ttu-id="34ea1-2870">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2871">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2871">Example</span></span>

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2872">See Also</span></span>

- <span data-ttu-id="34ea1-2873">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2873">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2874">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2874">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2875">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2875">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2876">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2876">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2877">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2877">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2878">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2878">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2879">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2879">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2880">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2880">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2881">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2881">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2882">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2882">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2883">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2883">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2884">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2884">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2885">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2885">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2886">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2886">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2887">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2887">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2888">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2888">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2889">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2889">fx_system_initialize</span></span>

## <a name="fx_media_read"></a><span data-ttu-id="34ea1-2890">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2890">fx_media_read</span></span>

<span data-ttu-id="34ea1-2891">Medyadan mantıksal kesim okur</span><span class="sxs-lookup"><span data-stu-id="34ea1-2891">Reads logical sector from media</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2892">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2892">Prototype</span></span>

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-2893">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2893">Description</span></span>

<span data-ttu-id="34ea1-2894">Bu hizmet, medyadan bir mantıksal kesim okur ve sağlanan arabelleğe yer sağlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2894">This service reads a logical sector from the media and places it into the supplied buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2895">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2895">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2896">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2896">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="34ea1-2897">**logical_sector:** Okunacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2897">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="34ea1-2898">**buffer_ptr:** Mantıksal kesim okuması için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2898">**buffer_ptr**: Pointer to the destination for the logical sector read.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2899">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2899">Return Values</span></span>

- <span data-ttu-id="34ea1-2900">**FX_SUCCESS** (0x00) Başarılı medya okuma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2900">**FX_SUCCESS** (0x00) Successful media read.</span></span>
- <span data-ttu-id="34ea1-2901">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2901">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2902">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2902">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2903">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2903">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-2904">**FX_PTR_ERROR** (0x18) Geçersiz medya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2904">**FX_PTR_ERROR** (0x18) Invalid media or buffer pointer.</span></span>
- <span data-ttu-id="34ea1-2905">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2905">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2906">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2906">Allowed From</span></span>

<span data-ttu-id="34ea1-2907">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2907">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2908">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2908">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-2909">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2909">See Also</span></span>

- <span data-ttu-id="34ea1-2910">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2910">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2911">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2911">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2912">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2912">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2913">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2913">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2914">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2914">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2915">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2915">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2916">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2916">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2917">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2917">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2918">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2918">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2919">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2919">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2920">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2920">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2921">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2921">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2922">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2922">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-2923">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2923">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2924">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2924">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2925">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2925">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2926">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2926">fx_system_initialize</span></span>

## <a name="fx_media_space_available"></a><span data-ttu-id="34ea1-2927">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2927">fx_media_space_available</span></span>

<span data-ttu-id="34ea1-2928">Kullanılabilir medya alanı döndürür</span><span class="sxs-lookup"><span data-stu-id="34ea1-2928">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2929">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2929">Prototype</span></span>

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a><span data-ttu-id="34ea1-2930">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2930">Description</span></span>

<span data-ttu-id="34ea1-2931">Bu hizmet, medyada kullanılabilir bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2931">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="34ea1-2932">4 GB'den büyük medya ile çalışmak için, uygulama tarafından *fx_media_extended_space_available.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-2932">To work with the media larger than 4GB, application shall use the service *fx_media_extended_space_available*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2933">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2933">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2934">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2934">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="34ea1-2935">**available_bytes_ptr:** Medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2935">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2936">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2936">Return Values</span></span>

- <span data-ttu-id="34ea1-2937">**FX_SUCCESS** (0x00) Medyada kullanılabilir alan başarıyla döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2937">**FX_SUCCESS** (0x00) Successfully returned available space on media.</span></span>
- <span data-ttu-id="34ea1-2938">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2938">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2939">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi NULL.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2939">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="34ea1-2940">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2940">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2941">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2941">Allowed From</span></span>

<span data-ttu-id="34ea1-2942">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2942">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2943">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2943">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2944">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2944">See Also</span></span>

- <span data-ttu-id="34ea1-2945">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2945">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2946">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2946">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2947">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2947">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2948">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2948">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2949">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2949">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2950">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2950">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2951">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2951">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2952">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2952">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2953">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2953">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2954">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2954">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2955">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2955">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2956">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2956">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2957">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2957">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2958">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2958">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-2959">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2959">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-2960">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-2960">fx_media_write</span></span>
- <span data-ttu-id="34ea1-2961">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-2961">fx_system_initialize</span></span>

## <a name="fx_media_volume_get"></a><span data-ttu-id="34ea1-2962">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-2962">fx_media_volume_get</span></span>

<span data-ttu-id="34ea1-2963">Medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-2963">Gets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-2964">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-2964">Prototype</span></span>

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="34ea1-2965">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-2965">Description</span></span>

<span data-ttu-id="34ea1-2966">Bu hizmet, önceden açılmış olan medyanın birim adını almaktadır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2966">This service retrieves the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-2967">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2967">Input Parameters</span></span>

- <span data-ttu-id="34ea1-2968">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2968">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-2969">**volume_name:** Birim adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2969">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="34ea1-2970">Hedefin en az 12 karakter uzunluğunda olacak kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2970">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="34ea1-2971">**volume_source:** Önyükleme kesimi veya kök dizinden adın nereden alınacaklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2971">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="34ea1-2972">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-2972">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="34ea1-2973">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="34ea1-2973">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="34ea1-2974">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="34ea1-2974">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-2975">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-2975">Return Values</span></span>

- <span data-ttu-id="34ea1-2976">**FX_SUCCESS** (0x00) Başarılı medya birimi get.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2976">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="34ea1-2977">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2977">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-2978">**FX_NOT_FOUND** (0x04) Birimi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2978">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="34ea1-2979">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2979">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-2980">**FX_PTR_ERROR** (0x18) Geçersiz medya veya birim hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2980">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="34ea1-2981">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2981">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-2982">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-2982">Allowed From</span></span>

<span data-ttu-id="34ea1-2983">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-2983">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-2984">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-2984">Example</span></span>

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a><span data-ttu-id="34ea1-2985">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-2985">See Also</span></span>

- <span data-ttu-id="34ea1-2986">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-2986">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-2987">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-2987">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-2988">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-2988">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-2989">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-2989">fx_media_check</span></span>
- <span data-ttu-id="34ea1-2990">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-2990">fx_media_close</span></span>
- <span data-ttu-id="34ea1-2991">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2991">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-2992">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2992">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-2993">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2993">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-2994">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-2994">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-2995">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-2995">fx_media_format</span></span>
- <span data-ttu-id="34ea1-2996">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-2996">fx_media_open</span></span>
- <span data-ttu-id="34ea1-2997">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-2997">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-2998">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-2998">fx_media_read</span></span>
- <span data-ttu-id="34ea1-2999">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-2999">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-3000">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3000">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-3001">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3001">fx_media_write</span></span>
- <span data-ttu-id="34ea1-3002">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3002">fx_system_initialize</span></span>

## <a name="fx_media_volume_get_extended"></a><span data-ttu-id="34ea1-3003">fx_media_volume_get_extended</span><span class="sxs-lookup"><span data-stu-id="34ea1-3003">fx_media_volume_get_extended</span></span>

<span data-ttu-id="34ea1-3004">Daha önce açılmış medyanın medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3004">Gets media volume name of previously opened media</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3005">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3005">Prototype</span></span>

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="34ea1-3006">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3006">Description</span></span>

<span data-ttu-id="34ea1-3007">Bu hizmet, daha önce açılmış medyanın birim adını alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3007">This service retrieves the volume name of the previously opened media.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3008">Bu hizmet, çağıran _ *Volume_Name*\* arabelleğinin boyutunda geçtiği sürece \***fx_media_volume_get ()** _ ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3008">This service is identical to ***fx_media_volume_get()** _ except the caller passes in the size of the _ *volume_name** buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3009">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3009">Input Parameters</span></span>


- <span data-ttu-id="34ea1-3010">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3010">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3011">**Volume_Name**: birim adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3011">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="34ea1-3012">Hedefin en az 12 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3012">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="34ea1-3013">**volume_name_buffer_length**: Volume_Name arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3013">**volume_name_buffer_length**: Size of volume_name buffer.</span></span>
- <span data-ttu-id="34ea1-3014">**volume_source**: önyükleme kesiminden veya kök dizinden adın nereden alındığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3014">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="34ea1-3015">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="34ea1-3015">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="34ea1-3016">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="34ea1-3016">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="34ea1-3017">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="34ea1-3017">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3018">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3018">Return Values</span></span>

- <span data-ttu-id="34ea1-3019">**FX_SUCCESS** (0x00) başarılı medya birimi al.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3019">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="34ea1-3020">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3020">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3021">**FX_NOT_FOUND** (0x04) birim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3021">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="34ea1-3022">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3022">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3023">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3023">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="34ea1-3024">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3024">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3025">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3025">Allowed From</span></span>

<span data-ttu-id="34ea1-3026">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3026">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3027">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3027">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3028">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3028">See Also</span></span>

- <span data-ttu-id="34ea1-3029">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-3029">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-3030">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-3030">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-3031">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3031">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-3032">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-3032">fx_media_check</span></span>
- <span data-ttu-id="34ea1-3033">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3033">fx_media_close</span></span>
- <span data-ttu-id="34ea1-3034">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3034">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-3035">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-3035">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-3036">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-3036">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-3037">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-3037">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-3038">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-3038">fx_media_format</span></span>
- <span data-ttu-id="34ea1-3039">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3039">fx_media_open</span></span>
- <span data-ttu-id="34ea1-3040">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3040">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-3041">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3041">fx_media_read</span></span>
- <span data-ttu-id="34ea1-3042">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-3042">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-3043">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3043">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-3044">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3044">fx_media_write</span></span>
- <span data-ttu-id="34ea1-3045">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3045">fx_system_initialize</span></span>

## <a name="fx_media_volume_set"></a><span data-ttu-id="34ea1-3046">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3046">fx_media_volume_set</span></span>

<span data-ttu-id="34ea1-3047">Medya birimi adını ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-3047">Sets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3048">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3048">Prototype</span></span>

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-3049">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3049">Description</span></span>

<span data-ttu-id="34ea1-3050">Bu hizmet, daha önce açılmış medyanın birim adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3050">This service sets the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3051">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3051">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3052">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3052">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3053">**Volume_Name**: birim adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3053">**volume_name**: Pointer to the volume name.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3054">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3054">Return Values</span></span>

- <span data-ttu-id="34ea1-3055">**FX_SUCCESS** (0x00) başarılı medya birimi kümesi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3055">**FX_SUCCESS** (0x00) Successful media volume set.</span></span>
- <span data-ttu-id="34ea1-3056">**FX_INVALID_NAME** (0x0C) Volume_name geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3056">**FX_INVALID_NAME** (0x0C) Volume_name is invalid.</span></span>
- <span data-ttu-id="34ea1-3057">**FX_MEDIA_INVALID** (0x02) birim adı ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3057">**FX_MEDIA_INVALID** (0x02) Unable to set volume name.</span></span>
- <span data-ttu-id="34ea1-3058">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3058">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3059">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3059">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3060">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3060">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-3061">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3061">**FX_PTR_ERROR** (0x18) Invalid media or volume name pointer.</span></span>
- <span data-ttu-id="34ea1-3062">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3062">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3063">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3063">Allowed From</span></span>

<span data-ttu-id="34ea1-3064">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3064">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3065">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3065">Example</span></span>

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3066">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3066">See Also</span></span>

- <span data-ttu-id="34ea1-3067">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-3067">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-3068">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-3068">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-3069">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3069">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-3070">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-3070">fx_media_check</span></span>
- <span data-ttu-id="34ea1-3071">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3071">fx_media_close</span></span>
- <span data-ttu-id="34ea1-3072">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3072">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-3073">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-3073">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-3074">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-3074">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-3075">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-3075">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-3076">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-3076">fx_media_format</span></span>
- <span data-ttu-id="34ea1-3077">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3077">fx_media_open</span></span>
- <span data-ttu-id="34ea1-3078">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3078">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-3079">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3079">fx_media_read</span></span>
- <span data-ttu-id="34ea1-3080">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-3080">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-3081">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3081">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-3082">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3082">fx_media_write</span></span>
- <span data-ttu-id="34ea1-3083">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3083">fx_system_initialize</span></span>

## <a name="fx_media_write"></a><span data-ttu-id="34ea1-3084">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3084">fx_media_write</span></span>

<span data-ttu-id="34ea1-3085">Mantıksal kesimi yazar</span><span class="sxs-lookup"><span data-stu-id="34ea1-3085">Writes logical sector</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3086">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3086">Prototype</span></span>

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="34ea1-3087">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3087">Description</span></span>

<span data-ttu-id="34ea1-3088">Bu hizmet verilen arabelleği belirtilen mantıksal kesime yazar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3088">This service writes the supplied buffer to the specified logical sector.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3089">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3089">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3090">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3090">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="34ea1-3091">**logical_sector**: yazılacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3091">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="34ea1-3092">**buffer_ptr**: mantıksal kesim yazma için kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3092">**buffer_ptr**: Pointer to the source for the logical sector write.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3093">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3093">Return Values</span></span>

- <span data-ttu-id="34ea1-3094">**FX_SUCCESS** (0x00) başarılı medya yazma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3094">**FX_SUCCESS** (0x00) Successful media write.</span></span>
- <span data-ttu-id="34ea1-3095">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3095">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3096">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3096">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-3097">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3097">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3098">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3098">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-3099">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3099">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="34ea1-3100">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3100">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3101">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3101">Allowed From</span></span>

<span data-ttu-id="34ea1-3102">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3102">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3103">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3103">Example</span></span>

```c
FX_MEDIA             my_media;
UCHAR                 my_buffer[128];
UINT                 status;

/* Write logical sector 22 from "my_buffer" assuming
    the physical media has a sector size of 128. */

status = fx_media_write(&my_media, 22, my_buffer);

/* If status equals FX_SUCCESS, the contents of logical
    sector 22 are now the same as "my_buffer." */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3104">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3104">See Also</span></span>

- <span data-ttu-id="34ea1-3105">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="34ea1-3105">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="34ea1-3106">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="34ea1-3106">fx_media_abort</span></span>
- <span data-ttu-id="34ea1-3107">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3107">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="34ea1-3108">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="34ea1-3108">fx_media_check</span></span>
- <span data-ttu-id="34ea1-3109">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3109">fx_media_close</span></span>
- <span data-ttu-id="34ea1-3110">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3110">fx_media_close_notify_set</span></span>
- <span data-ttu-id="34ea1-3111">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-3111">fx_media_exFAT_format</span></span>
- <span data-ttu-id="34ea1-3112">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-3112">fx_media_extended_space_available</span></span>
- <span data-ttu-id="34ea1-3113">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="34ea1-3113">fx_media_flush</span></span>
- <span data-ttu-id="34ea1-3114">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="34ea1-3114">fx_media_format</span></span>
- <span data-ttu-id="34ea1-3115">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3115">fx_media_open</span></span>
- <span data-ttu-id="34ea1-3116">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3116">fx_media_open_notify_set</span></span>
- <span data-ttu-id="34ea1-3117">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3117">fx_media_read</span></span>
- <span data-ttu-id="34ea1-3118">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="34ea1-3118">fx_media_space_available</span></span>
- <span data-ttu-id="34ea1-3119">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3119">fx_media_volume_get</span></span>
- <span data-ttu-id="34ea1-3120">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3120">fx_media_volume_set</span></span>
- <span data-ttu-id="34ea1-3121">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3121">fx_system_initialize</span></span>

## <a name="fx_system_date_get"></a><span data-ttu-id="34ea1-3122">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3122">fx_system_date_get</span></span>

<span data-ttu-id="34ea1-3123">Dosya sistemi tarihini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3123">Gets file system date</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3124">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3124">Prototype</span></span>

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a><span data-ttu-id="34ea1-3125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3125">Description</span></span>

<span data-ttu-id="34ea1-3126">Bu hizmet geçerli sistem tarihini döndürür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3126">This service returns the current system date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3127">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3127">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3128">**year:** Yıl için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3128">**year**: Pointer to destination for year.</span></span>
- <span data-ttu-id="34ea1-3129">**month:** Ay için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3129">**month**: Pointer to destination for month.</span></span>
- <span data-ttu-id="34ea1-3130">**day:** Gün için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3130">**day**: Pointer to destination for day.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3131">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3131">Return Values</span></span>

- <span data-ttu-id="34ea1-3132">**FX_SUCCESS** (0x00) Başarılı tarih alma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3132">**FX_SUCCESS** (0x00) Successful date retrieval.</span></span>
- <span data-ttu-id="34ea1-3133">**FX_PTR_ERROR** (0x18) Bir veya daha fazla giriş parametresi NULL olur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3133">**FX_PTR_ERROR** (0x18) One or more of the input parameters are NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3134">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3134">Allowed From</span></span>

<span data-ttu-id="34ea1-3135">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3135">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3136">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3136">Example</span></span>

```c
UINT            status;
UINT            year;
UINT            month;
UINT            day;
/* Retrieve the current system date. */

status = fx_system_date_get(&year, &month, &day);

/* If status equals FX_SUCCESS, the year, month,
    and day parameters now have meaningful information. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3137">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3137">See Also</span></span>

- <span data-ttu-id="34ea1-3138">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3138">fx_system_date_set</span></span>
- <span data-ttu-id="34ea1-3139">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3139">fx_system_initialize</span></span>
- <span data-ttu-id="34ea1-3140">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3140">fx_system_time_get</span></span>
- <span data-ttu-id="34ea1-3141">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3141">fx_system_time_set</span></span>

## <a name="fx_system_date_set"></a><span data-ttu-id="34ea1-3142">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3142">fx_system_date_set</span></span>

<span data-ttu-id="34ea1-3143">Sistem tarihini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-3143">Sets system date</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3144">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3144">Prototype</span></span>

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a><span data-ttu-id="34ea1-3145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3145">Description</span></span>

<span data-ttu-id="34ea1-3146">Bu hizmet, sistem tarihini belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3146">This service sets the system date as specified.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-3147">*İlk sistem tarihini ayarlamak için **bu fx_system_initialize** kısa süre sonra çağrılacaktır. Varsayılan olarak, sistem tarihi son genel FileX sürümüne göredir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3147">*This service should be called shortly after **fx_system_initialize** to set the initial system date. By default, the system date is that of the last generic FileX release.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3148">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3148">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3149">**year:** Yeni yıl.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3149">**year**: New year.</span></span> <span data-ttu-id="34ea1-3150">Geçerli aralık 1980 ile 2107 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3150">The valid range is from 1980 through the year 2107.</span></span>
- <span data-ttu-id="34ea1-3151">**month:** Yeni ay.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3151">**month**: New month.</span></span> <span data-ttu-id="34ea1-3152">Geçerli aralık 1 ile 12 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3152">The valid range is from 1 through 12.</span></span>
- <span data-ttu-id="34ea1-3153">**gün:** Yeni gün.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3153">**day**: New day.</span></span> <span data-ttu-id="34ea1-3154">Ay ve artık yıl koşullarına bağlı olarak geçerli aralık 1 ile 31 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3154">The valid range is from 1 through 31, depending on month and leap year conditions.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3155">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3155">Return Values</span></span>

- <span data-ttu-id="34ea1-3156">**FX_SUCCESS** (0x00) Başarılı tarih ayarı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3156">**FX_SUCCESS** (0x00) Successful date setting.</span></span>
- <span data-ttu-id="34ea1-3157">**FX_INVALID_YEAR** (0x12) Geçersiz yıl belirtildi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3157">**FX_INVALID_YEAR** (0x12) Invalid year specified.</span></span>
- <span data-ttu-id="34ea1-3158">**FX_INVALID_MONTH** (0x13) Geçersiz ay belirtildi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3158">**FX_INVALID_MONTH** (0x13) Invalid month specified.</span></span>
- <span data-ttu-id="34ea1-3159">**FX_INVALID_DAY** (0x14) Geçersiz gün belirtildi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3159">**FX_INVALID_DAY** (0x14) Invalid day specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3160">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3160">Allowed From</span></span>

<span data-ttu-id="34ea1-3161">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3161">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3162">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3162">Example</span></span>

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3163">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3163">See Also</span></span>

- <span data-ttu-id="34ea1-3164">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3164">fx_system_date_get</span></span>
- <span data-ttu-id="34ea1-3165">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3165">fx_system_initialize</span></span>
- <span data-ttu-id="34ea1-3166">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3166">fx_system_time_get</span></span>
- <span data-ttu-id="34ea1-3167">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3167">fx_system_time_set</span></span>

## <a name="fx_system_initialize"></a><span data-ttu-id="34ea1-3168">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3168">fx_system_initialize</span></span>

<span data-ttu-id="34ea1-3169">Sistemin tamamını başlatıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-3169">Initializes entire system</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3170">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3170">Prototype</span></span>

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a><span data-ttu-id="34ea1-3171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3171">Description</span></span>

<span data-ttu-id="34ea1-3172">Bu hizmet tüm önemli FileX veri yapılarını başlatıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3172">This service initializes all the major FileX data structures.</span></span> <span data-ttu-id="34ea1-3173">Başka bir FileX ***hizmeti tx_application_define*** veya bir başlatma iş parçacığından çağrılmalı ve çağrılmalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3173">It should be called either in ***tx_application_define*** or possibly from an initialization thread and must be called prior to using any other FileX service.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-3174">*Bu çağrı tarafından başlatıldıktan sonra, doğru bir sistem tarihi ve saatiyle başlamak için ***uygulamanın fx_system_date_set** _ ve _ *fx_system_time_set** çağrısında olması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3174">*Once initialized by this call, the application should call ***fx_system_date_set** _ and _ *fx_system_time_set** to start with an accurate system date and time.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3175">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3175">Input Parameters</span></span>

<span data-ttu-id="34ea1-3176">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3176">None</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3177">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3177">Return Values</span></span>

<span data-ttu-id="34ea1-3178">Yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3178">None.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3179">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3179">Allowed From</span></span>

<span data-ttu-id="34ea1-3180">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3180">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3181">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3181">Example</span></span>

```c
void tx_application_define(VOID *free_memory)
{
    UINT status;
    /* Initialize the FileX system. */
    fx_system_initialize();
    /* Set the file system date. */
    fx_system_date_set(my_year, my_month, my_day);

    /* Set the file system time. */
    fx_system_time_set(my_hour, my_minute, my_second);

    /* Now perform all other initialization and possibly FileX media
        open calls if the corresponding driver does not block on the boot sector read. */

    ...

}
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3182">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3182">See Also</span></span>

- <span data-ttu-id="34ea1-3183">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3183">fx_system_date_get</span></span>
- <span data-ttu-id="34ea1-3184">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3184">fx_system_date_set</span></span>
- <span data-ttu-id="34ea1-3185">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3185">fx_system_time_get</span></span>
- <span data-ttu-id="34ea1-3186">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3186">fx_system_time_set</span></span>

## <a name="fx_system_time_get"></a><span data-ttu-id="34ea1-3187">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3187">fx_system_time_get</span></span>

<span data-ttu-id="34ea1-3188">Geçerli sistem saatlerini alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3188">Gets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3189">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3189">Prototype</span></span>

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="34ea1-3190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3190">Description</span></span>

<span data-ttu-id="34ea1-3191">Bu hizmet geçerli sistem saatlerini almaktadır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3191">This service retrieves the current system time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3192">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3192">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3193">**hour:** Hedefe saat işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3193">**hour**: Pointer to destination for hour.</span></span>
- <span data-ttu-id="34ea1-3194">**minute:** Dakika için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3194">**minute**: Pointer to destination for minute.</span></span>
- <span data-ttu-id="34ea1-3195">**second:** saniye için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3195">**second**: Pointer to destination for second.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3196">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3196">Return Values</span></span>

- <span data-ttu-id="34ea1-3197">**FX_SUCCESS** (0x00) Başarılı sistem zamanı alma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3197">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="34ea1-3198">**FX_PTR_ERROR** (0x18) Bir veya daha fazla giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="34ea1-3198">**FX_PTR_ERROR** (0x18) One or more of the input parameters</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3199">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3199">Allowed From</span></span>

<span data-ttu-id="34ea1-3200">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3200">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3201">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3201">Example</span></span>

```c
UINT             status;
UINT             hour;
UINT             minute;
UINT             second;

/* Retrieve the current system time. */

status = fx_system_time_get(&hour, &minute, &second);

/* If status equals FX_SUCCESS, the current system time
    is in the hour, minute, and second variables. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3202">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3202">See Also</span></span>

- <span data-ttu-id="34ea1-3203">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3203">fx_system_date_get</span></span>
- <span data-ttu-id="34ea1-3204">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3204">fx_system_date_set</span></span>
- <span data-ttu-id="34ea1-3205">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3205">fx_system_initialize</span></span>
- <span data-ttu-id="34ea1-3206">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3206">fx_system_time_set</span></span>

## <a name="fx_system_time_set"></a><span data-ttu-id="34ea1-3207">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3207">fx_system_time_set</span></span>

<span data-ttu-id="34ea1-3208">Geçerli sistem saatlerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="34ea1-3208">Sets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3209">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3209">Prototype</span></span>

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a><span data-ttu-id="34ea1-3210">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3210">Description</span></span>

<span data-ttu-id="34ea1-3211">Bu hizmet, geçerli sistem saatlerini giriş parametreleri tarafından belirtilen saat olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3211">This service sets the current system time to that specified by the input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-3212">*Bu hizmet, ilk sistem fx_system_initialize **kısa** bir süre sonra çağrılacaktır. Varsayılan olarak sistem saati 0:0:0'dır.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3212">*This service should be called shortly after **fx_system_initialize** to set the initial system time. By default, the system time is 0:0:0.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3213">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3213">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3214">**hour:** Yeni saat (0-23).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3214">**hour**: New hour (0-23).</span></span>
- <span data-ttu-id="34ea1-3215">**minute:** Yeni dakika (0-59).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3215">**minute**: New minute (0-59).</span></span>
- <span data-ttu-id="34ea1-3216">**second:** Yeni saniye (0-59).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3216">**second**: New second (0-59).</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3217">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3217">Return Values</span></span>

- <span data-ttu-id="34ea1-3218">**FX_SUCCESS** (0x00) Başarılı sistem zamanı alma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3218">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="34ea1-3219">**FX_INVALID_HOUR**    (0x15) Yeni saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3219">**FX_INVALID_HOUR**    (0x15) New hour is invalid.</span></span>
- <span data-ttu-id="34ea1-3220">**FX_INVALID_MINUTE** (0x16) Yeni dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3220">**FX_INVALID_MINUTE** (0x16) New minute is invalid.</span></span>
- <span data-ttu-id="34ea1-3221">**FX_INVALID_SECOND** (0x17) Yeni saniye geçersiz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3221">**FX_INVALID_SECOND** (0x17) New second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3222">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3222">Allowed From</span></span>

<span data-ttu-id="34ea1-3223">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3223">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3224">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3224">Example</span></span>

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3225">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3225">See Also</span></span>

- <span data-ttu-id="34ea1-3226">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3226">fx_system_date_get</span></span>
- <span data-ttu-id="34ea1-3227">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3227">fx_system_date_set</span></span>
- <span data-ttu-id="34ea1-3228">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="34ea1-3228">fx_system_initialize</span></span>
- <span data-ttu-id="34ea1-3229">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3229">fx_system_time_get</span></span>

## <a name="fx_unicode_directory_create"></a><span data-ttu-id="34ea1-3230">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3230">fx_unicode_directory_create</span></span>

<span data-ttu-id="34ea1-3231">Unicode dizini oluşturur</span><span class="sxs-lookup"><span data-stu-id="34ea1-3231">Creates a Unicode directory</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3232">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3232">Prototype</span></span>

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-3233">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3233">Description</span></span>

<span data-ttu-id="34ea1-3234">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir alt dizin oluşturur; Unicode kaynak adı parametresinde yol bilgilerine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3234">This service creates a Unicode-named subdirectory in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="34ea1-3235">Başarılı olursa, yeni oluşturulan Unicode alt dizininin kısa adı (8.3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3235">If successful, the short name (8.3 format) of the newly created Unicode subdirectory is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-3236">*Unicode alt dizininde (varsayılan yol, silme vb.) yapılan tüm işlemler, standart FileX dizin hizmetlerine döndürülen kısa ad (8.3 biçimi) ekilerek gerçekleştir gerekir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3236">*All operations on the Unicode subdirectory (making it the default path, deleting, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX directory services.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3237">*Bu hizmet exFAT medyası üzerinde desteklenmiyor.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3237">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3238">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3238">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3239">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3239">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3240">**source_unicode_name:** Yeni alt dizin için Unicode adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3240">**source_unicode_name**: Pointer to the Unicode name for the new subdirectory.</span></span>
- <span data-ttu-id="34ea1-3241">**source_unicode_length:** Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3241">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="34ea1-3242">**short_name:** Yeni Unicode alt dizini için kısa ad (8.3 biçimi) için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3242">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode subdirectory.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3243">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3243">Return Values</span></span>

- <span data-ttu-id="34ea1-3244">**FX_SUCCESS** (0x00) Başarılı Unicode dizini oluşturma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3244">**FX_SUCCESS** (0x00) Successful Unicode directory create.</span></span>
- <span data-ttu-id="34ea1-3245">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3245">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3246">**FX_ALREADY_CREATED** (0x0B) Belirtilen dizin zaten var.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3246">**FX_ALREADY_CREATED** (0x0B) Specified directory already exists.</span></span>
- <span data-ttu-id="34ea1-3247">**FX_NO_MORE_SPACE** (0x0A) Yeni dizin girişi için medyada artık kullanılabilir küme yok.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3247">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new directory entry.</span></span>
- <span data-ttu-id="34ea1-3248">**FX_NOT_IMPLEMENTED** (0x22) Hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3248">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="34ea1-3249">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3249">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-3250">**FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3250">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="34ea1-3251">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3251">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="34ea1-3252">**FX_IO_ERROR (0x90)** Sürücü I/O hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3252">**FX_IO_ERROR    (0x90)** Driver I/O error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3253">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3253">Allowed From</span></span>

<span data-ttu-id="34ea1-3254">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3254">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3255">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3255">Example</span></span>

```c
FX_MEDIA             ram_disk;
UCHAR                 my_short_name[13];
UCHAR                 my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                         0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                         0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                         0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                         0x63,0x00, 0x00,0x00};

/* Create a Unicode subdirectory with the name contained in "my_unicode_name". */

length = fx_unicode_directory_create(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the Unicode subdirectory is created and "my_short_name"
    contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3256">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3256">See Also</span></span>

- <span data-ttu-id="34ea1-3257">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3257">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-3258">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3258">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-3259">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3259">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-3260">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3260">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-3261">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3261">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-3262">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3262">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-3263">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3263">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-3264">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3264">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-3265">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3265">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-3266">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-3266">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-3267">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3267">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-3268">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-3268">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-3269">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3269">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-3270">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3270">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-3271">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-3271">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-3272">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3272">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-3273">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3273">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-3274">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3274">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-3275">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3275">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-3276">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3276">fx_unicode_directory_rename</span></span>

## <a name="fx_unicode_directory_rename"></a><span data-ttu-id="34ea1-3277">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3277">fx_unicode_directory_rename</span></span>

<span data-ttu-id="34ea1-3278">Unicode dizesini kullanarak dizini yeniden adlandırıyor</span><span class="sxs-lookup"><span data-stu-id="34ea1-3278">Renames directory using Unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3279">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3279">Prototype</span></span>

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-3280">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3280">Description</span></span>

<span data-ttu-id="34ea1-3281">Bu hizmet, Unicode adlı alt dizini geçerli çalışma dizininde belirtilen yeni Unicode adıyla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3281">This service changes a Unicode-named subdirectory to specified new Unicode name in current working directory.</span></span> <span data-ttu-id="34ea1-3282">Unicode ad parametrelerinin yol bilgilerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3282">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3283">*Bu hizmet exFAT medyası üzerinde desteklenmiyor.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3283">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3284">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3284">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3285">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3285">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3286">**old_unicode_name:** Geçerli dosyanın Unicode adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3286">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="34ea1-3287">**old_unicode_name_length:** Geçerli Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3287">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="34ea1-3288">**new_unicode_name:** Yeni Unicode dosya adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3288">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="34ea1-3289">**old_unicode_name_length:** Yeni Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3289">**old_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="34ea1-3290">**new_short_name:** Yeniden adlandırılan Unicode dosyası için kısa ad (8.3 biçimi) için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3290">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span> <span data-ttu-id="34ea1-3291">Dizini Unicode ile Yeniden Adlandırma</span><span class="sxs-lookup"><span data-stu-id="34ea1-3291">Rename Directory with Unicode</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3292">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3292">Return Values</span></span>

- <span data-ttu-id="34ea1-3293">**FX_SUCCESS** (0x00) Başarılı medya açma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3293">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="34ea1-3294">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3294">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3295">**FX_ALREADY_CREATED** (0x0B) Belirtilen dizin adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3295">**FX_ALREADY_CREATED** (0x0B) Specified directory name already exists.</span></span>
- <span data-ttu-id="34ea1-3296">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3296">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3297">**FX_PTR_ERROR** (0x18) Bir veya daha fazla işaretçi NULL olur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3297">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="34ea1-3298">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3298">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="34ea1-3299">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3299">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3300">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3300">Allowed From</span></span>

<span data-ttu-id="34ea1-3301">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3302">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3302">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
UCHAR                 my_short_name[13];
UCHAR                 my_old_unicode_name[] = {'a', '\0', 'b', '\0', 'c', '\0', '\0', '\0'};
UCHAR                 my_new_unicode_name[] = {'d', '\0', 'e', '\0', 'f', '\0', '\0', '\0'};

/* Change the Unicode-named file "abc" to "def". */

status = fx_unicode_directory_rename(&my_media, my_old_unicode_name,
    3, my_new_unicode_name, 3, my_short_name);

/* If status equals FX_SUCCESS, the directory was changed to "def" and
    "my_short_name" contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3303">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3303">See Also</span></span>

- <span data-ttu-id="34ea1-3304">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3304">fx_directory_attributes_read</span></span>
- <span data-ttu-id="34ea1-3305">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3305">fx_directory_attributes_set</span></span>
- <span data-ttu-id="34ea1-3306">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3306">fx_directory_create</span></span>
- <span data-ttu-id="34ea1-3307">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3307">fx_directory_default_get</span></span>
- <span data-ttu-id="34ea1-3308">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3308">fx_directory_default_set</span></span>
- <span data-ttu-id="34ea1-3309">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3309">fx_directory_delete</span></span>
- <span data-ttu-id="34ea1-3310">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3310">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="34ea1-3311">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3311">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="34ea1-3312">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3312">fx_directory_information_get</span></span>
- <span data-ttu-id="34ea1-3313">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="34ea1-3313">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="34ea1-3314">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3314">fx_directory_local_path_get</span></span>
- <span data-ttu-id="34ea1-3315">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="34ea1-3315">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="34ea1-3316">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3316">fx_directory_local_path_set</span></span>
- <span data-ttu-id="34ea1-3317">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3317">fx_directory_long_name_get</span></span>
- <span data-ttu-id="34ea1-3318">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="34ea1-3318">fx_directory_name_test</span></span>
- <span data-ttu-id="34ea1-3319">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3319">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="34ea1-3320">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="34ea1-3320">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="34ea1-3321">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3321">fx_directory_rename</span></span>
- <span data-ttu-id="34ea1-3322">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3322">fx_directory_short_name_get</span></span>
- <span data-ttu-id="34ea1-3323">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3323">fx_unicode_directory_create</span></span>

## <a name="fx_unicode_file_create"></a><span data-ttu-id="34ea1-3324">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3324">fx_unicode_file_create</span></span>

<span data-ttu-id="34ea1-3325">Unicode dosyası oluşturur</span><span class="sxs-lookup"><span data-stu-id="34ea1-3325">Creates a Unicode file</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3326">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3326">Prototype</span></span>

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-3327">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3327">Description</span></span>

<span data-ttu-id="34ea1-3328">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya oluşturur; Unicode kaynak adı parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3328">This service creates a Unicode-named file in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="34ea1-3329">Başarılı olursa, yeni oluşturulan Unicode dosyanın kısa adı (8,3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3329">If successful, the short name (8.3 format) of the newly created Unicode file is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="34ea1-3330">*Unicode dosyasındaki (açma, yazma, okuma, kapatma, vb.) tüm işlemler, standart FileX dosya hizmetlerine döndürülen kısa ad (8,3 biçimi) sağlanarak yapılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3330">*All operations on the Unicode file (opening, writing, reading, closing, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX file services.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3331">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3331">Input Parameters</span></span>


- <span data-ttu-id="34ea1-3332">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3332">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3333">**source_unicode_name**: yeni dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3333">**source_unicode_name**: Pointer to the Unicode name for the new file.</span></span>
- <span data-ttu-id="34ea1-3334">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3334">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="34ea1-3335">**short_name**: yeni Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3335">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3336">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3336">Return Values</span></span>

- <span data-ttu-id="34ea1-3337">**FX_SUCCESS** (0x00) başarılı dosya oluştur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3337">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="34ea1-3338">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3338">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3339">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya zaten var.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3339">**FX_ALREADY_CREATED** (0x0B) Specified file already exists.</span></span>
- <span data-ttu-id="34ea1-3340">Yeni dosya girişi için medyada daha fazla küme yok **FX_NO_MORE_SPACE** (0x0A).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3340">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new file entry.</span></span>
- <span data-ttu-id="34ea1-3341">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3341">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="34ea1-3342">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3342">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3343">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3343">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="34ea1-3344">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3344">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="34ea1-3345">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3345">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3346">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3346">Allowed From</span></span>

<span data-ttu-id="34ea1-3347">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3347">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3348">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3348">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             my_short_name[13];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Create a Unicode file with the name contained in "my_unicode_name". */

length = fx_unicode_file_create(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the Unicode file is created and "my_short_name"
    contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3349">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3349">See Also</span></span>

- <span data-ttu-id="34ea1-3350">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3350">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3351">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3351">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3352">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3352">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3353">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3353">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3354">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3354">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3355">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3355">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3356">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3356">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3357">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3357">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3358">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3358">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3359">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3359">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3360">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3360">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3361">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3361">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3362">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3362">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3363">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3363">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3364">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3364">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3365">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3365">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3366">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3366">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3367">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3367">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3368">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3368">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3369">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3369">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3370">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3370">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3371">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3371">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3372">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3372">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3373">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3373">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-3374">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3374">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-3375">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3375">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_file_rename"></a><span data-ttu-id="34ea1-3376">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3376">fx_unicode_file_rename</span></span>

<span data-ttu-id="34ea1-3377">Unicode dizesini kullanarak bir dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3377">Renames a file using unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3378">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3378">Prototype</span></span>

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a><span data-ttu-id="34ea1-3379">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3379">Description</span></span>

<span data-ttu-id="34ea1-3380">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya adını belirtilen yeni Unicode adı olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3380">This service changes a Unicode-named file name to specified new Unicode name in current default directory.</span></span> <span data-ttu-id="34ea1-3381">Unicode ad parametreleri yol bilgilerine sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3381">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3382">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3382">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3383">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3383">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3384">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3384">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3385">**old_unicode_name**: geçerli dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3385">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="34ea1-3386">**old_unicode_name_length**: geçerli Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3386">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="34ea1-3387">**new_unicode_name**: yeni Unicode dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3387">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="34ea1-3388">**new_unicode_name_length**: yeni Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3388">**new_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="34ea1-3389">**new_short_name**: yeniden adlandırılan Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3389">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3390">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3390">Return Values</span></span>


- <span data-ttu-id="34ea1-3391">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3391">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="34ea1-3392">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3392">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3393">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3393">**FX_ALREADY_CREATED** (0x0B) Specified file name already exists.</span></span>
- <span data-ttu-id="34ea1-3394">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3394">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3395">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3395">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="34ea1-3396">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3396">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="34ea1-3397">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3397">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3398">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3398">Allowed From</span></span>

<span data-ttu-id="34ea1-3399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3400">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3400">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
UCHAR                 my_short_name[13];
UCHAR                 my_old_unicode_name[] = {'a', '\0', 'b', '\0', 'c', '\0', '\0', '\0'};
UCHAR                 my_new_unicode_name[] = {'d', '\0', 'e', '\0', 'f', '\0', '\0', '\0'};

/* Change the Unicode-named file "abc" to "def". */

status = fx_unicode_file_rename(&my_media, my_old_unicode_name,
    3, my_new_unicode_name, 3, my_short_name);

/* If status equals FX_SUCCESS, the file name was changed to "def" and
    "my_short_name" contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3401">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3401">See Also</span></span>

- <span data-ttu-id="34ea1-3402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3402">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3403">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3404">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3406">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3407">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3408">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3409">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3413">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3416">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3417">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3418">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3419">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3420">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3421">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3422">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3423">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3424">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3424">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3425">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3425">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-3426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3426">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-3427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3427">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get"></a><span data-ttu-id="34ea1-3428">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3428">fx_unicode_length_get</span></span>

<span data-ttu-id="34ea1-3429">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3429">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3430">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3430">Prototype</span></span>

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a><span data-ttu-id="34ea1-3431">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3431">Description</span></span>

<span data-ttu-id="34ea1-3432">Bu hizmet, sağlanan Unicode adının uzunluğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3432">This service determines the length of the supplied Unicode name.</span></span> <span data-ttu-id="34ea1-3433">Unicode bir karakter iki bayt ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3433">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="34ea1-3434">Unicode adı, iki baytlık bir Unicode karakter olan ve iki boş bayt (0 değeri 0 değeri) tarafından sonlandırılan bir serisidir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3434">A Unicode name is a series of two byte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3435">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3435">Input Parameters</span></span>

<span data-ttu-id="34ea1-3436">**unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3436">**unicode_name**: Pointer to Unicode name.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3437">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3437">Return Values</span></span>

<span data-ttu-id="34ea1-3438">**uzunluk**: Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3438">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3439">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3439">Allowed From</span></span>

<span data-ttu-id="34ea1-3440">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3440">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3441">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3441">Example</span></span>

```c
UCHAR     my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                           0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                           0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                           0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                           0x63,0x00, 0x00,0x00};

UINT     length;

/* Get the length of "my_unicode_name". */

length = fx_unicode_length_get(my_unicode_name);

/* A value of 17 will be returned for the length of the "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3442">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3442">See Also</span></span>

- <span data-ttu-id="34ea1-3443">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3443">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3444">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3444">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3445">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3445">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3446">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3446">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3447">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3447">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3448">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3448">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3449">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3449">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3450">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3450">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3451">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3451">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3452">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3452">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3453">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3453">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3454">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3454">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3455">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3455">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3456">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3456">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3457">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3457">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3458">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3458">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3459">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3459">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3460">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3460">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3461">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3461">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3462">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3462">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3463">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3463">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3464">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3464">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3465">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3465">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3466">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3466">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-3467">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3467">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-3468">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3468">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-3469">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3469">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get_extended"></a><span data-ttu-id="34ea1-3470">fx_unicode_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="34ea1-3470">fx_unicode_length_get_extended</span></span>

<span data-ttu-id="34ea1-3471">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3471">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3472">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3472">Prototype</span></span>

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a><span data-ttu-id="34ea1-3473">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3473">Description</span></span>

<span data-ttu-id="34ea1-3474">Bu hizmet, sağlanan Unicode adının uzunluğunu alır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3474">This service gets the length of the supplied Unicode name.</span></span> <span data-ttu-id="34ea1-3475">Unicode bir karakter iki bayt ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3475">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="34ea1-3476">Unicode adı, iki boş bayt (iki bayt 0 değeri) tarafından sonlandırılan bir dizi TWA Unicode karakter dizisidir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3476">A Unicode name is a series of twobyte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3477">*Bu hizmet, iki NULL karakter de dahil olmak üzere, çağıran **unicode_name** arabelleğinin boyutuna geçtiğinde, **fx_unicode_length_get ()** ile aynıdır.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3477">*This service is identical to **fx_unicode_length_get()** except the caller passes in the size of the **unicode_name** buffer, including the two NULL characters.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3478">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3478">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3479">**unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3479">**unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="34ea1-3480">**BUFFER_LENGTH**: Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3480">**buffer_length**: Size of Unicode name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3481">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3481">Return Values</span></span>

<span data-ttu-id="34ea1-3482">**uzunluk**: Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3482">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3483">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3483">Allowed From</span></span>

<span data-ttu-id="34ea1-3484">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3484">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3485">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3485">Example</span></span>

```c
UCHAR         my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                 0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                 0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                 0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                 0x63,0x00, 0x00,0x00};

UINT         length;

/* Get the length of "my_unicode_name". */

length = fx_unicode_length_get_extended(my_unicode_name, sizeof(my_unicode_name));

/* A value of 17 will be returned for the length of the "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3486">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3486">See Also</span></span>

- <span data-ttu-id="34ea1-3487">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3487">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3488">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3488">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3489">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3489">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3490">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3490">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3491">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3491">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3492">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3492">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3493">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3493">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3494">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3494">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3495">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3495">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3496">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3496">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3497">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3497">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3498">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3498">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3499">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3499">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3500">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3500">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3501">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3501">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3502">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3502">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3503">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3503">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3504">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3504">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3505">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3505">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3506">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3506">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3507">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3507">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3508">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3508">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3509">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3509">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3510">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3510">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-3511">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3511">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-3512">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3512">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-3513">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3513">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get"></a><span data-ttu-id="34ea1-3514">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3514">fx_unicode_name_get</span></span>

<span data-ttu-id="34ea1-3515">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3515">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3516">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3516">Prototype</span></span>

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a><span data-ttu-id="34ea1-3517">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3517">Description</span></span>

<span data-ttu-id="34ea1-3518">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3518">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="34ea1-3519">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3519">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3520">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3520">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3521">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3521">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3522">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3522">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3523">**short_name** Kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3523">**short_name** Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="34ea1-3524">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3524">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="34ea1-3525">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3525">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3526">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3526">Return Values</span></span>

- <span data-ttu-id="34ea1-3527">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3527">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="34ea1-3528">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3528">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="34ea1-3529">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-3529">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-3530">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3531">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3531">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3532">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3532">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="34ea1-3533">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3533">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-3534">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3534">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="34ea1-3535">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3535">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3536">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3536">Allowed From</span></span>

<span data-ttu-id="34ea1-3537">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3537">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3538">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3538">Example</span></span>

```c
FX_MEDIA             ram_disk;
UCHAR                 my_unicode_name[256*2];
ULONG                 unicode_name_length;

/* Get the Unicode name associated with the short name "ABC0~111.TXT".
    Note that the Unicode destination must have 2 times the
    number of maximum characters in the name. */

length = fx_unicode_name_get(&ram_disk, "ABC0~111.TXT", my_unicode_name, unicode_name_length);

/* If successful, the Unicode name is returned in "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3539">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3539">See Also</span></span>

- <span data-ttu-id="34ea1-3540">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3540">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3541">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3541">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3542">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3542">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3543">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3543">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3544">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3544">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3545">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3545">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3546">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3546">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3547">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3547">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3548">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3548">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3549">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3549">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3550">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3550">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3551">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3551">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3552">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3552">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3553">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3553">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3554">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3554">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3555">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3555">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3556">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3556">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3557">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3557">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3558">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3558">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3559">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3559">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3560">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3560">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3561">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3561">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3562">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3562">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3563">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3563">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-3564">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3564">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-3565">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3565">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get_extended"></a><span data-ttu-id="34ea1-3566">fx_unicode_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="34ea1-3566">fx_unicode_name_get_extended</span></span>

<span data-ttu-id="34ea1-3567">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3567">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3568">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3568">Prototype</span></span>

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a><span data-ttu-id="34ea1-3569">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3569">Description</span></span>

<span data-ttu-id="34ea1-3570">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3570">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="34ea1-3571">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3571">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3572">\* Bu hizmet,_çağıran, hedef Unicode arabelleğinin bir giriş bağımsız değişkeni olarak boyutunu sağladığı sürece \* fx_unicode_name_get aynıdır. Bu, hizmetin hedef Unicode arabelleğinin üzerine yazmayacağı garantisi sağlamasına izin verir_</span><span class="sxs-lookup"><span data-stu-id="34ea1-3572">\*This service is identical to \***fx_unicode_name_get**_, except the caller supplies the size of the destination Unicode buffer as an input argument. This allows the service to guarantee that it will not overwrite the destination Unicode buffer_</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3573">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3573">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3574">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3574">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3575">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3575">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3576">**short_name**: kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="34ea1-3576">**short_name**: Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="34ea1-3577">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3577">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="34ea1-3578">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3578">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>
- <span data-ttu-id="34ea1-3579">**unicode_name_buffer_length**: Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3579">**unicode_name_buffer_length**: Size of the Unicode name buffer.</span></span> <span data-ttu-id="34ea1-3580">Note: bir NULL Sonlandırıcı gereklidir ve bu da ek bir bayt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3580">Note: A NULL terminator is required, which makes an extra byte.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3581">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3581">Return Values</span></span>

- <span data-ttu-id="34ea1-3582">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3582">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="34ea1-3583">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3583">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="34ea1-3584">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-3584">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-3585">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3585">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3586">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3586">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3587">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3587">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="34ea1-3588">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3588">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-3589">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3589">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="34ea1-3590">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3590">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3591">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3591">Allowed From</span></span>

<span data-ttu-id="34ea1-3592">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3592">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3593">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3593">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             my_unicode_name[256*2];
ULONG             unicode_name_length;

/* Get the Unicode name associated with the short name "ABC0~111.TXT".
    Note that the Unicode destination must have 2 times the number of maximum characters in the name. */

length = fx_unicode_name_get_extended(&ram_disk, "ABC0~111.TXT",
    my_unicode_name,&unicode_name_length, sizeof(ny_unicode_name));

/* If successful, the Unicode name is returned in "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3594">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3594">See Also</span></span>

- <span data-ttu-id="34ea1-3595">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3595">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3596">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3596">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3597">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3597">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3598">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3598">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3599">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3599">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3600">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3600">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3601">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3601">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3602">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3602">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3603">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3603">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3604">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3604">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3605">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3605">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3606">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3606">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3607">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3607">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3608">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3608">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3609">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3609">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3610">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3610">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3611">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3611">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3612">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3612">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3613">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3613">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3614">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3614">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3615">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3615">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3616">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3616">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3617">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3617">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3618">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3618">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-3619">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3619">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-3620">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3620">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_short_name_get"></a><span data-ttu-id="34ea1-3621">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3621">fx_unicode_short_name_get</span></span>

<span data-ttu-id="34ea1-3622">Unicode addan kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3622">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3623">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3623">Prototype</span></span>

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

<span data-ttu-id="34ea1-3624">Bu hizmet, geçerli varsayılan dizinde Unicode-name ile ilişkili kısa adı (8.3 biçimi) verir; Unicode ad parametresinde yol bilgilerine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3624">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="34ea1-3625">Başarılı olursa, Unicode adıyla ilişkili kısa ad hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3625">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3626">*Bu hizmet hem dosyalar hem de alt dizinler için kısa adlar almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3626">*This service can be used to get short names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3627">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3627">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3628">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3628">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3629">**source_unicode_name:** Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3629">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="34ea1-3630">**source_unicode_length:** Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3630">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="34ea1-3631">**destination_short_name:** Kısa ad (8.3 biçimi) için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3631">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="34ea1-3632">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3632">This must be at least 13 bytes in size.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3633">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3633">Return Values</span></span>

- <span data-ttu-id="34ea1-3634">**FX_SUCCESS** (0x00) Başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3634">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="34ea1-3635">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3635">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="34ea1-3636">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-3636">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="34ea1-3637">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3637">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3638">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3638">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3639">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3639">**FX_NOT_FOUND** (0x04)    Unicode name was not found.</span></span>
- <span data-ttu-id="34ea1-3640">**FX_NOT_IMPLEMENTED** (0x22) Hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3640">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="34ea1-3641">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3641">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-3642">**FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3642">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="34ea1-3643">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3643">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3644">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3644">Allowed From</span></span>

<span data-ttu-id="34ea1-3645">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3645">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3646">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3646">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             my_short_name[13];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Get the short name associated with the Unicode name contained in the array "my_unicode_name". */

length = fx_unicode_short_name_get(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the short name is returned in "my_short_name". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3647">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3647">See Also</span></span>

- <span data-ttu-id="34ea1-3648">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3648">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3649">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3649">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3650">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3650">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3651">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3651">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3652">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3652">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3653">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3653">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3654">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3654">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3655">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3655">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3656">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3656">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3657">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3657">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3658">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3658">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3659">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3659">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3660">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3660">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3661">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3661">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3662">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3662">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3663">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3663">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3664">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3664">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3665">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3665">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3666">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3666">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3667">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3667">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3668">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3668">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3669">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3669">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3670">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3670">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3671">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3671">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-3672">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3672">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-3673">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3673">fx_unicode_name_get</span></span>

## <a name="fx_unicode_short_name_get_extended"></a><span data-ttu-id="34ea1-3674">fx_unicode_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="34ea1-3674">fx_unicode_short_name_get_extended</span></span>

<span data-ttu-id="34ea1-3675">Unicode addan kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="34ea1-3675">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="34ea1-3676">Prototype</span><span class="sxs-lookup"><span data-stu-id="34ea1-3676">Prototype</span></span>

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="34ea1-3677">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34ea1-3677">Description</span></span>

<span data-ttu-id="34ea1-3678">Bu hizmet, geçerli varsayılan dizinde Unicode-name ile ilişkili kısa adı (8.3 biçimi) verir; Unicode ad parametresinde yol bilgilerine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3678">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="34ea1-3679">Başarılı olursa, Unicode adıyla ilişkili kısa ad hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3679">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34ea1-3680">*Bu hizmet **fx_unicode_short_name_get() ile** aynıdır, ancak çağıranın hedef arabelleğin boyutunu giriş bağımsız değişkeni olarak sağlar. Bu, hizmetin kısa adın hedef arabelleği aşmasını garantilemektedir.*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3680">*This service is identical to **fx_unicode_short_name_get()**, except the caller supplies the size of the destination buffer as an input argument. This allows the service to guarantee the short name does not exceed the destination buffer.*</span></span>

<span data-ttu-id="34ea1-3681">*Bu hizmet hem dosyalar hem de alt dizinler için kısa adlar almak için kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="34ea1-3681">*This service can be used to get short names for both files and subdirectories*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="34ea1-3682">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3682">Input Parameters</span></span>

- <span data-ttu-id="34ea1-3683">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3683">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="34ea1-3684">**source_unicode_name:** Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3684">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="34ea1-3685">**source_unicode_length:** Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3685">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="34ea1-3686">**destination_short_name:** Kısa ad (8.3 biçimi) için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3686">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="34ea1-3687">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3687">This must be at least 13 bytes in size.</span></span>
- <span data-ttu-id="34ea1-3688">**short_name_buffer_length:** Hedef arabelleğin boyutu.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3688">**short_name_buffer_length**: Size of the destination buffer.</span></span> <span data-ttu-id="34ea1-3689">Arabellek boyutu en az 14 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3689">The buffer size must be at least 14 bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="34ea1-3690">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="34ea1-3690">Return Values</span></span>

- <span data-ttu-id="34ea1-3691">**FX_SUCCESS** (0x00) Başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3691">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="34ea1-3692">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3692">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="34ea1-3693">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="34ea1-3693">**FX_FILE_CORRUPT** (0x08)    File is corrupted</span></span>
- <span data-ttu-id="34ea1-3694">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3694">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="34ea1-3695">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3695">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="34ea1-3696">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3696">**FX_NOT_FOUND** (0x04) Unicode name was not found.</span></span>
- <span data-ttu-id="34ea1-3697">**FX_NOT_IMPLEMENTED** (0x22) Hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3697">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="34ea1-3698">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3698">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="34ea1-3699">**FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3699">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="34ea1-3700">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3700">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="34ea1-3701">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="34ea1-3701">Allowed From</span></span>

<span data-ttu-id="34ea1-3702">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="34ea1-3702">Threads</span></span>

### <a name="example"></a><span data-ttu-id="34ea1-3703">Örnek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3703">Example</span></span>

```c
#define         SHORT_NAME_BUFFER_SIZE 13
FX_MEDIA         ram_disk;
UCHAR             my_short_name[SHORT_NAME_BUFFER_SIZE];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Get the short name associated with the Unicode name contained in the array "my_unicode_name". */

length = fx_unicode_short_name_get_extended(&ram_disk,
    my_unicode_name, 17, my_short_name,SHORT_NAME_BUFFER_SIZE);

/* If successful, the short name is returned in "my_short_name". */
```

### <a name="see-also"></a><span data-ttu-id="34ea1-3704">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="34ea1-3704">See Also</span></span>

- <span data-ttu-id="34ea1-3705">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3705">fx_file_allocate</span></span>
- <span data-ttu-id="34ea1-3706">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3706">fx_file_attributes_read</span></span>
- <span data-ttu-id="34ea1-3707">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3707">fx_file_attributes_set</span></span>
- <span data-ttu-id="34ea1-3708">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3708">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3709">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="34ea1-3709">fx_file_close</span></span>
- <span data-ttu-id="34ea1-3710">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3710">fx_file_create</span></span>
- <span data-ttu-id="34ea1-3711">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3711">fx_file_date_time_set</span></span>
- <span data-ttu-id="34ea1-3712">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="34ea1-3712">fx_file_delete</span></span>
- <span data-ttu-id="34ea1-3713">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3713">fx_file_extended_allocate</span></span>
- <span data-ttu-id="34ea1-3714">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3714">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="34ea1-3715">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3715">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="34ea1-3716">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3716">fx_file_extended_seek</span></span>
- <span data-ttu-id="34ea1-3717">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3717">fx_file_extended_truncate</span></span>
- <span data-ttu-id="34ea1-3718">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3718">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="34ea1-3719">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="34ea1-3719">fx_file_open</span></span>
- <span data-ttu-id="34ea1-3720">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="34ea1-3720">fx_file_read</span></span>
- <span data-ttu-id="34ea1-3721">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3721">fx_file_relative_seek</span></span>
- <span data-ttu-id="34ea1-3722">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3722">fx_file_rename</span></span>
- <span data-ttu-id="34ea1-3723">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="34ea1-3723">fx_file_seek</span></span>
- <span data-ttu-id="34ea1-3724">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="34ea1-3724">fx_file_truncate</span></span>
- <span data-ttu-id="34ea1-3725">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="34ea1-3725">fx_file_truncate_release</span></span>
- <span data-ttu-id="34ea1-3726">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="34ea1-3726">fx_file_write</span></span>
- <span data-ttu-id="34ea1-3727">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="34ea1-3727">fx_file_write_notify_set</span></span>
- <span data-ttu-id="34ea1-3728">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="34ea1-3728">fx_unicode_file_create</span></span>
- <span data-ttu-id="34ea1-3729">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="34ea1-3729">fx_unicode_file_rename</span></span>
- <span data-ttu-id="34ea1-3730">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3730">fx_unicode_name_get</span></span>
- <span data-ttu-id="34ea1-3731">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="34ea1-3731">fx_unicode_short_name_get</span></span>
