---
title: Bölüm 4- FileX Azure RTOS açıklaması
description: Bu bölümde, FileX hizmetleriyle Azure RTOS alfabetik olarak sıralanmış bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 39b31c1abae8613eb54382162504aaadc07ceebf
ms.sourcegitcommit: 97f6724d6eee7b9c251a50c191911050c52b1c69
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025930"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a><span data-ttu-id="8ac81-103">Bölüm 4- FileX Azure RTOS açıklaması</span><span class="sxs-lookup"><span data-stu-id="8ac81-103">Chapter 4- Description of Azure RTOS FileX services</span></span>

<span data-ttu-id="8ac81-104">Bu bölümde, FileX hizmetleriyle Azure RTOS alfabetik olarak sıralanmış bir açıklama yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-104">This chapter contains a description of all Azure RTOS FileX services in alphabetic order.</span></span> <span data-ttu-id="8ac81-105">Hizmet adları, benzer hizmetlerin hepsi birlikte grup olacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-105">Service names are designed so all similar services are grouped together.</span></span>

## <a name="fx_directory_attributes_read"></a><span data-ttu-id="8ac81-106">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-106">fx_directory_attributes_read</span></span>

<span data-ttu-id="8ac81-107">Dizin özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="8ac81-107">Reads directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-108">Prototype</span></span>

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a><span data-ttu-id="8ac81-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-109">Description</span></span>

<span data-ttu-id="8ac81-110">Bu hizmet, dizinin özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-110">This service reads the directory's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-111">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-111">Input Parameters</span></span>

- <span data-ttu-id="8ac81-112">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-112">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-113">**directory_name:** İstenen dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-113">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="8ac81-114">**öznitelikler** _ptr: Dizinin özniteliklerinin yerleştirilecek hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-114">**attributes** _ptr: Pointer to the destination for the directory's attributes to be placed.</span></span> <span data-ttu-id="8ac81-115">Dizin öznitelikleri, aşağıdaki olası ayarlarla bit eşlemesi biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8ac81-115">The directory attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8ac81-116">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-116">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8ac81-117">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-117">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8ac81-118">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8ac81-118">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8ac81-119">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="8ac81-119">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="8ac81-120">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="8ac81-120">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="8ac81-121">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8ac81-121">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-122">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-122">Return Values</span></span>

- <span data-ttu-id="8ac81-123">**FX_SUCCESS** (0x00) Başarılı dizin öznitelikleri okundu</span><span class="sxs-lookup"><span data-stu-id="8ac81-123">**FX_SUCCESS** (0x00) Successful directory attributes read</span></span>
- <span data-ttu-id="8ac81-124">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-124">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-125">**FX _NOT BULUNDU** (0x04) Belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ac81-125">**FX _NOT FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8ac81-126">**FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-126">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="8ac81-127">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-127">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-128">**FX_FILE_CORRUPT** 0x08) Dosya bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-128">**FX_FILE_CORRUPT** 0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-129">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-129">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-130">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-130">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-131">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-131">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-132">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8ac81-132">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8ac81-133">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-133">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8ac81-134">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-134">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-135">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-135">Allowed From</span></span>

<span data-ttu-id="8ac81-136">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-136">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-137">Example</span></span>

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-138">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-138">See Also</span></span>

- <span data-ttu-id="8ac81-139">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-139">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-140">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-140">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-141">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-141">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-142">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-142">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-143">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-143">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-144">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-144">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-145">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-145">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-146">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-146">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-147">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-147">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-148">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-148">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-149">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-149">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-150">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-150">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-151">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-151">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-152">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-152">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-153">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-153">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-154">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-154">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-155">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-155">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-156">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-156">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-157">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-157">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-158">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-158">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_attributes_set"></a><span data-ttu-id="8ac81-159">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-159">fx_directory_attributes_set</span></span>

<span data-ttu-id="8ac81-160">Dizin özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-160">Sets directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-161">Prototype</span></span>

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a><span data-ttu-id="8ac81-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-162">Description</span></span>

<span data-ttu-id="8ac81-163">Bu hizmet, dizinin özniteliklerini çağıran tarafından belirtilen özniteliklere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-163">This service sets the directory's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-164">*Bu uygulamanın yalnızca bu hizmetle dizin özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlama girişimi hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-164">*This application is only allowed to modify a subset of the directory's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-165">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-165">Input Parameters</span></span>

- <span data-ttu-id="8ac81-166">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-166">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-167">**directory_name:** İstenen dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-167">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="8ac81-168">**attributes:** Bu dizine yeni öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-168">**attributes**: The new attributes to this directory.</span></span> <span data-ttu-id="8ac81-169">Geçerli dizin öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-169">The valid directory attributes are defined as follows:</span></span>
  - <span data-ttu-id="8ac81-170">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-170">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8ac81-171">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-171">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8ac81-172">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8ac81-172">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8ac81-173">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8ac81-173">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-174">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-174">Return Values</span></span>

- <span data-ttu-id="8ac81-175">**FX_SUCCESS** (0x00) Başarılı dizin öznitelik kümesi</span><span class="sxs-lookup"><span data-stu-id="8ac81-175">**FX_SUCCESS** (0x00) Successful directory attribute set</span></span>
- <span data-ttu-id="8ac81-176">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-176">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-177">**FX_NOT_FOUND** (0x04) Belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ac81-177">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8ac81-178">**FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-178">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="8ac81-179">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-179">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-180">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="8ac81-180">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="8ac81-181">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-181">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-182">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-182">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-183">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-183">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-184">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-184">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-185">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8ac81-185">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8ac81-186">**FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-186">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8ac81-187">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-187">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8ac81-188">**FX_INVALID_ATTR** (0x19) Geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-188">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="8ac81-189">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-190">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-190">Allowed From</span></span>

<span data-ttu-id="8ac81-191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-192">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-192">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-193">See Also</span></span>

- <span data-ttu-id="8ac81-194">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-194">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-195">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-195">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-196">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-196">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-197">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-197">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-198">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-198">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-199">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-199">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-200">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-200">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-201">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-201">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-202">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-202">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-203">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-203">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-204">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-204">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-205">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-205">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-206">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-206">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-207">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-207">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-208">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-208">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-209">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-209">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-210">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-210">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-211">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-211">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-212">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-212">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-213">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-213">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_create"></a><span data-ttu-id="8ac81-214">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-214">fx_directory_create</span></span>

<span data-ttu-id="8ac81-215">Alt dizin oluşturur</span><span class="sxs-lookup"><span data-stu-id="8ac81-215">Creates subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-216">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-216">Prototype</span></span>

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-217">Description</span></span>

<span data-ttu-id="8ac81-218">Bu hizmet, geçerli varsayılan dizinde veya dizin adında sağlanan yolda bir alt dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-218">This service creates a subdirectory in the current default directory or in the path supplied in the directory name.</span></span> <span data-ttu-id="8ac81-219">Kök dizinden farklı olarak, alt dizinlerin tutabilecekleri dosya sayısı için bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-219">Unlike the root directory, subdirectories do not have a limit on the number of files they can hold.</span></span> <span data-ttu-id="8ac81-220">Kök dizin yalnızca önyükleme kaydı tarafından belirlenen girdi sayısını tutabilirler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-220">The root directory can only hold the number of entries determined by the boot record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-221">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-221">Input Parameters</span></span>

- <span data-ttu-id="8ac81-222">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-222">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-223">**directory_name**: Oluşturulacak dizinin adına yönelik işaretçi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-223">**directory_name**: Pointer to the name of the directory to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-224">Return Values</span></span>

- <span data-ttu-id="8ac81-225">**FX_SUCCESS** (0x00) başarılı dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-225">**FX_SUCCESS** (0x00) Successful directory create.</span></span>
- <span data-ttu-id="8ac81-226">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-226">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-227">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ac81-227">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8ac81-228">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-228">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="8ac81-229">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-229">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-230">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-230">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-231">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-231">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-232">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-232">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-233">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-233">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-234">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8ac81-234">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8ac81-235">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-235">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8ac81-236">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-236">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8ac81-237">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-237">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="8ac81-238">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-238">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-239">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-239">Allowed From</span></span>

<span data-ttu-id="8ac81-240">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-240">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-241">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-242">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-242">See Also</span></span>

- <span data-ttu-id="8ac81-243">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-243">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-244">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-244">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-245">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-245">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-246">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-246">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-247">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-247">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-248">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-248">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-249">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-249">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-250">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-250">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-251">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-251">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-252">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-252">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-253">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-253">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-254">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-254">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-255">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-255">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-256">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-256">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-257">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-257">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-258">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-258">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-259">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-259">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-260">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-260">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-261">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-261">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-262">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-262">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_get"></a><span data-ttu-id="8ac81-263">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-263">fx_directory_default_get</span></span>

<span data-ttu-id="8ac81-264">Son varsayılan dizini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-264">Gets last default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-265">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-265">Prototype</span></span>

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-266">Description</span></span>

<span data-ttu-id="8ac81-267">Bu hizmet, ***fx_directory_default_set*** tarafından en son ayarlanan yola yönelik işaretçiyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-267">This service returns the pointer to the path last set by ***fx_directory_default_set***.</span></span> <span data-ttu-id="8ac81-268">Varsayılan dizin ayarlanmamışsa veya geçerli varsayılan dizin kök dizin ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-268">If the default directory has not been set or if the current default directory is the root directory, a value of FX_NULL is returned.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-269">*İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-269">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-270">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-270">Input Parameters</span></span>

- <span data-ttu-id="8ac81-271">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-271">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-272">**return_path_name**: son varsayılan dizin dizesinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-272">**return_path_name**: Pointer to the destination for the last default directory string.</span></span> <span data-ttu-id="8ac81-273">Varsayılan dizinin geçerli ayarı kök ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-273">A value of FX_NULL is returned if the current setting of the default directory is the root.</span></span> <span data-ttu-id="8ac81-274">Medya açıldığında, kök varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-274">When the media is opened, root is the default.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-275">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-275">Return Values</span></span>

- <span data-ttu-id="8ac81-276">**FX_SUCCESS** (0x00) başarılı varsayılan dizin Al</span><span class="sxs-lookup"><span data-stu-id="8ac81-276">**FX_SUCCESS** (0x00) Successful default directory get</span></span>
- <span data-ttu-id="8ac81-277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-278">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-278">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="8ac81-279">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-279">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-280">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-280">Allowed From</span></span>

<span data-ttu-id="8ac81-281">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-282">Example</span></span>

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a><span data-ttu-id="8ac81-283">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-283">See Also</span></span>

- <span data-ttu-id="8ac81-284">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-284">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-285">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-285">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-286">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-286">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-287">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-287">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-288">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-288">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-289">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-289">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-290">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-290">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-291">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-291">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-292">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-292">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-293">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-293">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-294">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-294">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-295">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-295">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-296">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-296">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-297">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-297">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-298">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-298">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-299">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-299">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-300">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-300">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-301">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-301">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-302">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-302">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-303">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-303">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_set"></a><span data-ttu-id="8ac81-304">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-304">fx_directory_default_set</span></span>

<span data-ttu-id="8ac81-305">Varsayılan dizini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-305">Sets default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-306">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-306">Prototype</span></span>

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-307">Description</span></span>

<span data-ttu-id="8ac81-308">Bu hizmet, medyanın varsayılan dizinini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-308">This service sets the default directory of the media.</span></span> <span data-ttu-id="8ac81-309">FX_NULL değeri sağlanırsa, varsayılan dizin medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-309">If a value of FX_NULL is supplied, the default directory is set to the media's root directory.</span></span> <span data-ttu-id="8ac81-310">Açıkça bir yol belirtmeen sonraki tüm dosya işlemleri varsayılan olarak bu dizine gelecektir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-310">All subsequent file operations that do not explicitly specify a path will default to this directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-311">*İç yol dizesinin varsayılan boyutu 256 karakterdir; fx_api.h **dosyasındaki** FX_MAXIMUM_PATH **değiştirerek** ve FileX kitaplığının tamamını yeniden oluşturarak değiştirilebilir. Karakter dizesi yolu uygulama için korunur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-311">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-312">*Uygulama tarafından sağlanan adlar için FileX hem ters eğik çizgi ( ) hem de eğik çizgi (/) karakterlerini ayrı dizinlere, alt dizinlere ve dosya \\ adlarına destekler. Ancak FileX, uygulamaya döndürülen yollarda yalnızca ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-312">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-313">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-313">Input Parameters</span></span>

- <span data-ttu-id="8ac81-314">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-314">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-315">**new_path_name:** Yeni varsayılan dizin adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-315">**new_path_name**: Pointer to new default directory name.</span></span> <span data-ttu-id="8ac81-316">Bir FX_NULL değeri sağlanırsa, medyanın varsayılan dizini medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-316">If a value of FX_NULL is supplied, the default directory of the media is set to the media's root directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-317">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-317">Return Values</span></span>

- <span data-ttu-id="8ac81-318">**FX_SUCCESS** (0x00) Başarılı varsayılan dizin kümesi</span><span class="sxs-lookup"><span data-stu-id="8ac81-318">**FX_SUCCESS** (0x00)  Successful default directory set</span></span>
- <span data-ttu-id="8ac81-319">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-319">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-320">**FX_INVALID_PATH** (0x0D) Yeni dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ac81-320">**FX_INVALID_PATH** (0x0D) New directory could not be found</span></span>
- <span data-ttu-id="8ac81-321">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-321">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-322">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-322">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-323">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-323">Allowed From</span></span>

<span data-ttu-id="8ac81-324">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-324">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-325">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-325">Example</span></span>

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-326">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-326">See Also</span></span>

- <span data-ttu-id="8ac81-327">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-327">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-328">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-328">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-329">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-329">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-330">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-330">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-331">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-331">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-332">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-332">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-333">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-333">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-334">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-334">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-335">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-335">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-336">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-336">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-337">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-337">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-338">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-338">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-339">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-339">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-340">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-340">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-341">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-341">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-342">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-342">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-343">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-343">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-344">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-344">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-345">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-345">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-346">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-346">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_delete"></a><span data-ttu-id="8ac81-347">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-347">fx_directory_delete</span></span>

<span data-ttu-id="8ac81-348">Alt dizini siler</span><span class="sxs-lookup"><span data-stu-id="8ac81-348">Deletes subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-349">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-349">Prototype</span></span>

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-350">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-350">Description</span></span>

<span data-ttu-id="8ac81-351">Bu hizmet belirtilen dizini siler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-351">This service deletes the specified directory.</span></span> <span data-ttu-id="8ac81-352">Dizini silmek için dizinin boş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ac81-352">Note that the directory must be empty to delete it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-353">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-353">Input Parameters</span></span>

- <span data-ttu-id="8ac81-354">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-354">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-355">**directory_name:** Silinecek dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-355">**directory_name**: Pointer to name of directory to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-356">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-356">Return Values</span></span>

- <span data-ttu-id="8ac81-357">**FX_SUCCESS** (0x00) Başarılı dizin silme</span><span class="sxs-lookup"><span data-stu-id="8ac81-357">**FX_SUCCESS** (0x00) Successful directory delete</span></span>
- <span data-ttu-id="8ac81-358">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-358">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-359">**FX_NOT_FOUND** (0x04) Belirtilen dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ac81-359">**FX_NOT_FOUND** (0x04) Specified directory was not found</span></span>
- <span data-ttu-id="8ac81-360">**FX_DIR_NOT_EMPTY** (0x10) Belirtilen dizin boş değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-360">**FX_DIR_NOT_EMPTY** (0x10) Specified directory is not empty</span></span>
- <span data-ttu-id="8ac81-361">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-361">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-362">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="8ac81-362">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="8ac81-363">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-363">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-364">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-364">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-365">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-365">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-366">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-366">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-367">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8ac81-367">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8ac81-368">**FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-368">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8ac81-369">**FX_NOT_DIRECTORY** (0x0E) Dizin girişi değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-369">**FX_NOT_DIRECTORY** (0x0E) Not a directory entry</span></span>
- <span data-ttu-id="8ac81-370">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-370">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8ac81-371">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-371">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-372">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-372">Allowed From</span></span>

<span data-ttu-id="8ac81-373">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-373">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-374">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-374">Example</span></span>
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-375">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-375">See Also</span></span>

- <span data-ttu-id="8ac81-376">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-376">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-377">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-377">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-378">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-378">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-379">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-379">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-380">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-380">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-381">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-381">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-382">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-382">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-383">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-383">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-384">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-384">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-385">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-385">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-386">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-386">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-387">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-387">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-388">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-388">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-389">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-389">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-390">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-390">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-391">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-391">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-392">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-392">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-393">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-393">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-394">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-394">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-395">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-395">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_entry_find"></a><span data-ttu-id="8ac81-396">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-396">fx_directory_first_entry_find</span></span>

<span data-ttu-id="8ac81-397">İlk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-397">Gets first directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-398">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-398">Prototype</span></span>

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-399">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-399">Description</span></span>

<span data-ttu-id="8ac81-400">Bu hizmet, varsayılan dizinde ilk giriş adını alan ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-400">This service retrieves the first entry name in the default directory and copies it to the specified destination.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-401">*Belirtilen hedef, dosya adı tarafından tanımlandığı gibi en büyük boyutlu FileX adını tutacak kadar **büyük FX_MAX_LONG_NAME_LEN.***</span><span class="sxs-lookup"><span data-stu-id="8ac81-401">*The specified destination must be large enough to hold the maximum sized FileX name, as defined by **FX_MAX_LONG_NAME_LEN.***</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-402">*Yerel olmayan bir yol kullanıyorsanız, dizin geçişi sırasında diğer uygulama iş parçacıklarının bu dizini değiştirmesini önlemek (ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile) önemlidir. Aksi takdirde geçersiz sonuçlar elde edilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-402">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-403">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-403">Input Parameters</span></span>

- <span data-ttu-id="8ac81-404">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-404">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-405">**return_entry_name:** Varsayılan dizinde ilk giriş adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-405">**return_entry_name**: Pointer to destination for the first entry name in the default directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-406">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-406">Return Values</span></span>

- <span data-ttu-id="8ac81-407">**FX_SUCCESS** (0x00) Başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="8ac81-407">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="8ac81-408">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-408">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-409">**FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-409">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8ac81-410">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-410">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-411">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-411">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-412">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-412">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-413">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-413">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-414">**FX_PTR_ERROR** (0x18) Geçersiz medya veya hedef işaretçi</span><span class="sxs-lookup"><span data-stu-id="8ac81-414">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer</span></span>
- <span data-ttu-id="8ac81-415">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-415">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-416">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-416">Allowed From</span></span>

<span data-ttu-id="8ac81-417">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-417">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-418">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-418">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-419">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-419">See Also</span></span>

- <span data-ttu-id="8ac81-420">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-420">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-421">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-421">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-422">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-422">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-423">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-423">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-424">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-424">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-425">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-425">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-426">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-426">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-427">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-427">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-428">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-428">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-429">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-429">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-430">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-430">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-431">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-431">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-432">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-432">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-433">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-433">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-434">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-434">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-435">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-435">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-436">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-436">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-437">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-437">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-438">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-438">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-439">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-439">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="8ac81-440">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-440">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="8ac81-441">Tam bilgilerle ilk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-441">Gets first directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-442">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-442">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="8ac81-443">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-443">Input Parameters</span></span>

- <span data-ttu-id="8ac81-444">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-444">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-445">**directory_name:** Dizin girişinin adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-445">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="8ac81-446">En az bu kadar büyük FX_MAX_LONG_NAME_LEN.</span><span class="sxs-lookup"><span data-stu-id="8ac81-446">Must be at least as big as FX_MAX_LONG_NAME_LEN.</span></span>
- <span data-ttu-id="8ac81-447">**attributes:** Null olmayan bir değerse, girişin yerleştirilecek öznitelikleri için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-447">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.</span></span> <span data-ttu-id="8ac81-448">Öznitelikler, aşağıdaki olası ayarlarla bit eşlemesi biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8ac81-448">The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8ac81-449">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-449">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="8ac81-450">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-450">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="8ac81-451">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="8ac81-451">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="8ac81-452">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="8ac81-452">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="8ac81-453">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="8ac81-453">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="8ac81-454">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="8ac81-454">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="8ac81-455">**size:** Null olmayan bir değerse, girişin boyutu için hedefin bayt cinsinden işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-455">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="8ac81-456">**year:** Null olmayan bir değerse, girişin değişiklik yılı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-456">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="8ac81-457">**month:** Null olmayan bir değerse, girişin değişiklik ayı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-457">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="8ac81-458">**day:** Null olmayan bir değerse, girişin değişiklik günü için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-458">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="8ac81-459">**hour:** Null olmayan bir değerse, girişin değişiklik saati için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-459">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="8ac81-460">**minute:** Null olmayan bir değerse, girişin değişiklik dakikası için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-460">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="8ac81-461">**second:** Null olmayan bir değerse, girişin ikinci değişikliği için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-461">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-462">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-462">Return Values</span></span>

- <span data-ttu-id="8ac81-463">**FX_SUCCESS** (0x00) Başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="8ac81-463">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="8ac81-464">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-464">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-465">**FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-465">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8ac81-466">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-466">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-467">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="8ac81-467">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="8ac81-468">**FX_FILE _CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-468">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-469">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-469">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-470">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-470">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-471">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-471">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-472">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8ac81-472">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8ac81-473">**FX_PTR_ERROR** (0x18) Geçersiz medya veya hedef işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-473">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="8ac81-474">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-474">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-475">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-475">Allowed From</span></span>

<span data-ttu-id="8ac81-476">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-476">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-477">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-477">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-478">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-478">See Also</span></span>

- <span data-ttu-id="8ac81-479">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-479">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-480">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-480">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-481">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-481">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-482">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-482">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-483">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-483">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-484">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-484">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-485">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-485">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-486">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-486">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-487">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-487">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-488">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-488">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-489">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-489">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-490">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-490">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-491">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-491">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-492">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-492">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-493">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-493">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-494">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-494">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-495">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-495">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-496">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-496">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-497">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-497">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-498">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-498">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_information_get"></a><span data-ttu-id="8ac81-499">fx_directory_information_get:</span><span class="sxs-lookup"><span data-stu-id="8ac81-499">fx_directory_information_get:</span></span>

<span data-ttu-id="8ac81-500">Dizin giriş bilgilerini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-500">Gets directory entry information</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-501">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-501">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="8ac81-502">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-502">Input Parameters</span></span>

- <span data-ttu-id="8ac81-503">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-503">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-504">**directory_name:** Dizin girişinin adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-504">**directory_name**: Pointer to name of the directory entry.</span></span>
- <span data-ttu-id="8ac81-505">**attributes:** Öznitelikler için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-505">**attributes**: Pointer to the destination for the attributes.</span></span>
- <span data-ttu-id="8ac81-506">**size:** Boyut için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-506">**size**: Pointer to the destination for the size.</span></span>
- <span data-ttu-id="8ac81-507">**year:** Yılın hedefine işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-507">**year**: Pointer to the destination for the year.</span></span>
- <span data-ttu-id="8ac81-508">**month:** Ay için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-508">**month**: Pointer to the destination for the month.</span></span>
- <span data-ttu-id="8ac81-509">**day:** Günün hedefine işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-509">**day**: Pointer to the destination for the day.</span></span>
- <span data-ttu-id="8ac81-510">**hour:** Bir saat için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-510">**hour**: Pointer to the destination for the hour.</span></span>
- <span data-ttu-id="8ac81-511">**minute:** Dakika için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-511">**minute**: Pointer to the destination for the minute.</span></span>
- <span data-ttu-id="8ac81-512">**second:** saniye için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-512">**second**: Pointer to the destination for the second.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-513">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-513">Return Values</span></span>

- <span data-ttu-id="8ac81-514">**FX_SUCCESS** (0x00) Başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="8ac81-514">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="8ac81-515">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-515">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-516">**FX_NOT_FOUND** (0x04) Belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ac81-516">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8ac81-517">**FX_IO_ERROR** (0x90) Sürücü Ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-517">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-518">**FX_MEDIA_INVALID** (0x02) Geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8ac81-518">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8ac81-519">**FX_FILE _CORRUPT** (0x08) Dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-519">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-520">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-520">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-521">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-521">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-522">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-522">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-523">**FX_PTR_ERROR** (0x18) Geçersiz medya veya hedef işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-523">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="8ac81-524">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-524">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-525">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-525">Allowed From</span></span>

<span data-ttu-id="8ac81-526">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-526">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-527">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-527">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-528">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-528">See Also</span></span>

- <span data-ttu-id="8ac81-529">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-529">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-530">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-530">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-531">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-531">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-532">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-532">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-533">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-533">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-534">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-534">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-535">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-535">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-536">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-536">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-537">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-537">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-538">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-538">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-539">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-539">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-540">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-540">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-541">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-541">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-542">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-542">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-543">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-543">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-544">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-544">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-545">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-545">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-546">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-546">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-547">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-547">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-548">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-548">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_clear"></a><span data-ttu-id="8ac81-549">fx_directory_local_path_clear:</span><span class="sxs-lookup"><span data-stu-id="8ac81-549">fx_directory_local_path_clear:</span></span>

<span data-ttu-id="8ac81-550">Varsayılan yerel yolu temizler</span><span class="sxs-lookup"><span data-stu-id="8ac81-550">Clears default local path</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-551">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-551">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="8ac81-552">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-552">Description</span></span>

<span data-ttu-id="8ac81-553">Bu hizmet, çağıran iş parçacığı için ayarlanmış önceki yerel yolu temizler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-553">This service clears the previous local path set up for the calling thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-554">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-554">Input Parameters</span></span>

- <span data-ttu-id="8ac81-555">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-555">**media_ptr**: Pointer to a previously opened media.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-556">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-556">Return Values</span></span>

- <span data-ttu-id="8ac81-557">**FX_SUCCESS** (0x00) Başarılı yerel yol temiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-557">**FX_SUCCESS** (0x00) Successful local path clear.</span></span>
- <span data-ttu-id="8ac81-558">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-558">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="8ac81-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlı</span><span class="sxs-lookup"><span data-stu-id="8ac81-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined</span></span>
- <span data-ttu-id="8ac81-560">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-560">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-561">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-561">Allowed From</span></span>

<span data-ttu-id="8ac81-562">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-562">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-563">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-563">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-564">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-564">See Also</span></span>

- <span data-ttu-id="8ac81-565">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-565">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-566">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-566">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-567">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-567">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-568">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-568">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-569">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-569">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-570">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-570">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-571">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-571">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-572">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-572">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-573">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-573">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-574">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-574">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-575">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-575">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-576">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-576">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-577">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-577">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-578">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-578">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-579">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-579">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-580">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-580">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-581">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-581">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-582">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-582">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-583">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-583">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-584">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-584">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_get"></a><span data-ttu-id="8ac81-585">fx_directory_local_path_get:</span><span class="sxs-lookup"><span data-stu-id="8ac81-585">fx_directory_local_path_get:</span></span>

<span data-ttu-id="8ac81-586">Geçerli yerel yol dizesini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-586">Gets the current local path string</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-587">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-587">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-588">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-588">Description</span></span>

<span data-ttu-id="8ac81-589">Bu hizmet, belirtilen medyanın yerel yol işaretçisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-589">This service returns the local path pointer of the specified media.</span></span> <span data-ttu-id="8ac81-590">Yerel yol kümesi yoksa, çağırana NULL döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-590">If there is no local path set, a NULL is returned to the caller.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-591">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-591">Input Parameters</span></span>

- <span data-ttu-id="8ac81-592">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-592">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-593">**return_path_name:** Depoilecek yerel yol dizesi için hedef dize işaretçisinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-593">**return_path_name**: Pointer to the destination string pointer for the local path string to be stored.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-594">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-594">Return Values</span></span>

- <span data-ttu-id="8ac81-595">**FX_SUCCESS** (0x00) Başarılı yerel yol get.</span><span class="sxs-lookup"><span data-stu-id="8ac81-595">**FX_SUCCESS** (0x00) Successful local path get.</span></span>
- <span data-ttu-id="8ac81-596">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-596">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="8ac81-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="8ac81-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="8ac81-598">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-598">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>


### <a name="allowed-from"></a><span data-ttu-id="8ac81-599">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-599">Allowed From</span></span>

<span data-ttu-id="8ac81-600">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-600">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-601">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-601">Example</span></span>

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-602">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-602">See Also</span></span>

- <span data-ttu-id="8ac81-603">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-603">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-604">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-604">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-605">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-605">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-606">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-606">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-607">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-607">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-608">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-608">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-609">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-609">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-610">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-610">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-611">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-611">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-612">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-612">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-613">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-613">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-614">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-614">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-615">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-615">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-616">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-616">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-617">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-617">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-618">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-618">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-619">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-619">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-620">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-620">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-621">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-621">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-622">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-622">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_restore"></a><span data-ttu-id="8ac81-623">fx_directory_local_path_restore:</span><span class="sxs-lookup"><span data-stu-id="8ac81-623">fx_directory_local_path_restore:</span></span>

<span data-ttu-id="8ac81-624">Önceki yerel yolu geri yükleme</span><span class="sxs-lookup"><span data-stu-id="8ac81-624">Restores previous local path</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-625">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-625">Prototype</span></span>

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a><span data-ttu-id="8ac81-626">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-626">Description</span></span>

<span data-ttu-id="8ac81-627">Bu hizmet daha önce ayarlanmış bir yerel yolu geri yüklemektedir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-627">This service restores a previously set local path.</span></span> <span data-ttu-id="8ac81-628">Bu yerel yolda yapılan dizin arama konumu da geri yüklenir ve bu da bu yordamı uygulama tarafından yapılan yinelemeli dizin geçişlerinde yararlı yapar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-628">The directory search position made on this local path is also restored, which makes this routine useful in recursive directory traversals by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-629">*Her yerel yol, varsayılan olarak 256 **FX_MAXIMUM_PATH** bir yerel yol dizesi içerir. Bu iç yol dizesi FileX tarafından kullanılmaz ve yalnızca uygulamanın kullanımı için sağlanır. Bu **FX_LOCAL_PATH** yerel değişken olarak bildirilemezse, kullanıcılar bu yapının boyutuna göre büyüyen yığından dikkatli olması gerekir. Kullanıcılar dosya boyutunu azaltmak ve FileX **FX_MAXIMUM_PATH** yeniden oluşturmasını sağlar.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-629">*Each local path contains a local path string of **FX_MAXIMUM_PATH** in size, which by default is 256 characters. This internal path string is not used by FileX and is provided only for the application's use. If **FX_LOCAL_PATH** is going to be declared as a local variable, users should beware of the stack growing by the size of this structure. Users are welcome to reduce the size of **FX_MAXIMUM_PATH** and rebuild the FileX library source.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-630">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-630">Input Parameters</span></span>

- <span data-ttu-id="8ac81-631">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-631">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-632">**local_path_ptr:** Önceden ayarlanmış yerel yolun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-632">**local_path_ptr**: Pointer to the previously set local path.</span></span> <span data-ttu-id="8ac81-633">Bu işaretçinin daha önce kullanılan ve hala bozulmamış bir yerel yola işaret etmelerinden emin olmak çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-633">It's very important to ensure that this pointer does indeed point to a previously used and still intact local path.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-634">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-634">Return Values</span></span>

- <span data-ttu-id="8ac81-635">**FX_SUCCESS** (0x00) Başarılı yerel yol geri yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-635">**FX_SUCCESS** (0x00) Successful local path restore.</span></span>
- <span data-ttu-id="8ac81-636">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open.</span></span>
- <span data-ttu-id="8ac81-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined.</span></span>
- <span data-ttu-id="8ac81-638">**FX_PTR_ERROR** (0x18) Geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-638">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-639">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-639">Allowed From</span></span>

<span data-ttu-id="8ac81-640">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-640">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-641">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-641">Example</span></span>

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-642">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-642">See Also</span></span>

- <span data-ttu-id="8ac81-643">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-643">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-644">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-644">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-645">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-645">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-646">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-646">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-647">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-647">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-648">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-648">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-649">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-649">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-650">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-650">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-651">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-651">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-652">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-652">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-653">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-653">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-654">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-654">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-655">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-655">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-656">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-656">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-657">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-657">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-658">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-658">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-659">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-659">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-660">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-660">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-661">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-661">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-662">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-662">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_set"></a><span data-ttu-id="8ac81-663">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-663">fx_directory_local_path_set</span></span>

<span data-ttu-id="8ac81-664">İş parçacığına özgü bir yerel yol ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-664">Sets up a thread-specific local path</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-665">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-665">Prototype</span></span>

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-666">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-666">Description</span></span>

<span data-ttu-id="8ac81-667">Bu hizmet , \* new_path_string _ tarafından belirtilen iş **parçacığına özgü bir yol** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-667">This service sets up a thread-specific path as specified by the \***new_path_string** _.</span></span> <span data-ttu-id="8ac81-668">Bu yordam başarıyla tamamlandıktan sonra, _ *_local_path_ptr_*\* içinde depolanan yerel yol bilgileri, bu iş parçacığı tarafından yapılan tüm dosya ve dizin işlemleri için genel medya yolundan önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-668">After successful completion of this routine, the local path information stored in _ *_local_path_ptr_*\* will take precedence over the global media path for all file and directory operations made by this thread.</span></span> <span data-ttu-id="8ac81-669">Bunun sistem üzerindeki diğer iş parçacığı üzerinde hiçbir etkisi olmaz</span><span class="sxs-lookup"><span data-stu-id="8ac81-669">This will have no impact on any other thread in the system</span></span> 
> [!IMPORTANT]
> <span data-ttu-id="8ac81-670">*Yerel yol dizesinin varsayılan boyutu 256 karakterdir; fx_api.h **dosyasındaki** FX_MAXIMUM_PATH **değiştirerek** ve FileX kitaplığının tamamını yeniden oluşturarak değiştirilebilir. Karakter dizesi yolu uygulama için korunur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-670">*The default size of the local path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-671">*Uygulama tarafından sağlanan adlar için FileX hem ters eğik çizgi ( ) hem de eğik çizgi (/) karakterlerini ayrı dizinlere, alt dizinlere ve dosya \\ adlarına destekler. Ancak FileX, uygulamaya döndürülen yollarda yalnızca ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-671">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-672">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-672">Input Parameters</span></span>

- <span data-ttu-id="8ac81-673">**media_ptr:** Önceden açılmış olan medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-673">**media_ptr**: Pointer to the previously opened media.</span></span>
- <span data-ttu-id="8ac81-674">**local_path_ptr:** İş parçacığına özgü yerel yol bilgilerini tutmak için hedef.</span><span class="sxs-lookup"><span data-stu-id="8ac81-674">**local_path_ptr**: Destination for holding the thread-specific local path information.</span></span> <span data-ttu-id="8ac81-675">Bu yapının adresi gelecekte yerel yol geri yükleme işlevine sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-675">The address of this structure may be supplied to the local path restore function in the future.</span></span>
- <span data-ttu-id="8ac81-676">**new_path_name:** Kurulumun yerel yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-676">**new_path_name**: Specifies the local path to setup.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-677">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-677">Return Values</span></span>

- <span data-ttu-id="8ac81-678">**FX_SUCCESS** (0x00) Başarılı varsayılan dizin kümesi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-678">**FX_SUCCESS** (0x00) Successful default directory set.</span></span>
- <span data-ttu-id="8ac81-679">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-679">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="8ac81-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="8ac81-681">**FX_INVALID_PATH** (0x0D) Yeni dizin bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-681">**FX_INVALID_PATH** (0x0D) New directory could not be found.</span></span>
- <span data-ttu-id="8ac81-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH is defined.</span></span>
- <span data-ttu-id="8ac81-683">**FX_PTR_ERROR** (0x18) Geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-683">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-684">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-684">Allowed From</span></span>

<span data-ttu-id="8ac81-685">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-685">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-686">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-686">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-687">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-687">See Also</span></span>

- <span data-ttu-id="8ac81-688">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-688">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-689">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-689">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-690">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-690">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-691">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-691">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-692">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-692">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-693">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-693">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-694">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-694">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-695">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-695">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-696">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-696">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-697">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-697">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-698">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-698">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-699">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-699">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-700">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-700">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-701">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-701">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-702">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-702">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-703">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-703">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-704">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-704">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-705">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-705">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-706">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-706">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-707">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-707">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get"></a><span data-ttu-id="8ac81-708">fx_directory_long_name_get:</span><span class="sxs-lookup"><span data-stu-id="8ac81-708">fx_directory_long_name_get:</span></span>

<span data-ttu-id="8ac81-709">Kısa adından uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-709">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-710">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-710">Prototype</span></span>

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-711">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-711">Description</span></span>

<span data-ttu-id="8ac81-712">Bu hizmet, sağlanan kısa (8,3 biçim) adıyla ilişkili uzun adı (varsa) alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-712">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="8ac81-713">Kısa ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-713">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-714">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-714">Input Parameters</span></span>

- <span data-ttu-id="8ac81-715">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-715">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-716">**short_name**: kaynak kısa adı işaretçisi (8,3 biçim).</span><span class="sxs-lookup"><span data-stu-id="8ac81-716">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="8ac81-717">**long_name**: uzun ad için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-717">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="8ac81-718">Uzun bir ad yoksa, kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-718">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="8ac81-719">Uzun ad hedefinin FX_MAX_LONG_NAME_LEN karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ac81-719">Note that the destination for the long name must be large enough to hold FX_MAX_LONG_NAME_LEN characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-720">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-720">Return Values</span></span>

- <span data-ttu-id="8ac81-721">**FX_SUCCESS** (0x00) başarılı uzun ad al</span><span class="sxs-lookup"><span data-stu-id="8ac81-721">**FX_SUCCESS** (0x00) Successful long name get</span></span>
- <span data-ttu-id="8ac81-722">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8ac81-722">**FX_NOT_FOUND** (0x04) Short name was not found</span></span>
- <span data-ttu-id="8ac81-723">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8ac81-723">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8ac81-724">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8ac81-724">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8ac81-725">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-725">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-726">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8ac81-726">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8ac81-727">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-727">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8ac81-728">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-728">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-729">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-729">**FX_PTR_ERROR** (0x18) Invalid media or name pointer</span></span>
- <span data-ttu-id="8ac81-730">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-730">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-731">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-731">Allowed From</span></span>

<span data-ttu-id="8ac81-732">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-733">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-733">Example</span></span>

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-734">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-734">See Also</span></span>

- <span data-ttu-id="8ac81-735">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-735">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-736">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-736">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-737">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-737">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-738">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-738">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-739">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-739">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-740">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-740">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-741">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-741">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-742">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-742">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-743">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-743">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-744">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-744">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-745">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-745">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-746">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-746">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-747">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-747">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-748">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-748">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-749">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-749">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-750">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-750">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-751">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-751">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-752">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-752">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-753">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-753">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-754">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-754">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get_extended"></a><span data-ttu-id="8ac81-755">fx_directory_long_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8ac81-755">fx_directory_long_name_get_extended</span></span>

<span data-ttu-id="8ac81-756">Kısa adından uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-756">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-757">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-757">Prototype</span></span>

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="8ac81-758">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-758">Description</span></span>

<span data-ttu-id="8ac81-759">Bu hizmet, sağlanan kısa (8,3 biçim) adıyla ilişkili uzun adı (varsa) alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-759">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="8ac81-760">Kısa ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-760">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-761">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-761">Input Parameters</span></span>

- <span data-ttu-id="8ac81-762">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-762">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-763">**short_name**: kaynak kısa adı işaretçisi (8,3 biçim).</span><span class="sxs-lookup"><span data-stu-id="8ac81-763">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="8ac81-764">**long_name**: uzun ad için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-764">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="8ac81-765">Uzun bir ad yoksa, kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-765">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="8ac81-766">Note: uzun ad hedefi **FX_MAX_LONG_NAME_LEN** karakter tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-766">Note: Destination for the long name must be large enough to hold **FX_MAX_LONG_NAME_LEN** characters.</span></span>
- <span data-ttu-id="8ac81-767">**long_file_name_buffer_length**: uzun ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-767">**long_file_name_buffer_length**: Length of the long name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-768">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-768">Return Values</span></span>

- <span data-ttu-id="8ac81-769">**FX_SUCCESS** (0x00) başarılı uzun ad al.</span><span class="sxs-lookup"><span data-stu-id="8ac81-769">**FX_SUCCESS** (0x00) Successful long name get.</span></span>
- <span data-ttu-id="8ac81-770">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-770">**FX_NOT_FOUND** (0x04) Short name was not found.</span></span>
- <span data-ttu-id="8ac81-771">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-771">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-772">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-772">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-773">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-773">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-774">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-774">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-775">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-775">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-776">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-776">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8ac81-777">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-777">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8ac81-778">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-778">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-779">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-779">Allowed From</span></span>

<span data-ttu-id="8ac81-780">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-780">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-781">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-781">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name), sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-782">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-782">See Also</span></span>

- <span data-ttu-id="8ac81-783">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-783">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-784">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-784">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-785">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-785">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-786">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-786">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-787">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-787">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-788">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-788">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-789">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-789">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-790">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-790">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-791">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-791">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-792">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-792">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-793">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-793">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-794">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-794">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-795">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-795">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-796">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-796">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-797">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-797">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-798">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-798">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-799">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-799">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-800">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-800">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-801">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-801">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-802">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-802">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_name_test"></a><span data-ttu-id="8ac81-803">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-803">fx_directory_name_test</span></span>

<span data-ttu-id="8ac81-804">Dizin için testler</span><span class="sxs-lookup"><span data-stu-id="8ac81-804">Tests for directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-805">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-805">Prototype</span></span>

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-806">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-806">Description</span></span>

<span data-ttu-id="8ac81-807">Bu hizmet, belirtilen adın bir dizin olup olmadığını sınar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-807">This service tests whether or not the supplied name is a directory.</span></span> <span data-ttu-id="8ac81-808">Öyleyse, bir FX_SUCCESS döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-808">If so, a FX_SUCCESS is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-809">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-809">Input Parameters</span></span>

- <span data-ttu-id="8ac81-810">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-810">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-811">**directory_name**: Dizin girişinin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-811">**directory_name**: Pointer to name of the directory entry.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-812">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-812">Return Values</span></span>

- <span data-ttu-id="8ac81-813">**FX_SUCCESS** (0x00) sağlanan ad bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-813">**FX_SUCCESS** (0x00) Supplied name is a directory.</span></span>
- <span data-ttu-id="8ac81-814">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-814">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8ac81-815">**FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-815">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="8ac81-816">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8ac81-816">**FX_NOT_DIRECTORY** (0x0E)  Entry is not a directory</span></span>
- <span data-ttu-id="8ac81-817">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-817">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-818">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-818">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-819">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-819">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-820">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-820">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-821">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-821">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-822">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-822">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8ac81-823">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-823">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8ac81-824">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-824">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-825">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-825">Allowed From</span></span>

<span data-ttu-id="8ac81-826">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-826">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-827">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-827">Example</span></span>

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-828">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-828">See Also</span></span>

- <span data-ttu-id="8ac81-829">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-829">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-830">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-830">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-831">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-831">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-832">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-832">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-833">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-833">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-834">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-834">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-835">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-835">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-836">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-836">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-837">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-837">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-838">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-838">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-839">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-839">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-840">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-840">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-841">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-841">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-842">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-842">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-843">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-843">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-844">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-844">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-845">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-845">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-846">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-846">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-847">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-847">fx_unicode_directory_create</span></span>

## <a name="fx_directory_next_entry_find"></a><span data-ttu-id="8ac81-848">fx_directory_next_entry_find:</span><span class="sxs-lookup"><span data-stu-id="8ac81-848">fx_directory_next_entry_find:</span></span>

<span data-ttu-id="8ac81-849">Sonraki dizin girişini seçer</span><span class="sxs-lookup"><span data-stu-id="8ac81-849">Picks up next directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-850">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-850">Prototype</span></span>

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-851">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-851">Description</span></span>

<span data-ttu-id="8ac81-852">Bu hizmet, geçerli varsayılan dizindeki bir sonraki giriş adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-852">This service returns the next entry name in the current default directory.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-853">*Yerel olmayan bir yol kullanılıyorsa, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek için de önemlidir (bir ThreadX semaforu veya iş parçacığı öncelik düzeyiyle). Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-853">*If using a non-local path, it is also important to prevent (with a ThreadX semaphore or thread priority level) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-854">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-854">Input Parameters</span></span>

- <span data-ttu-id="8ac81-855">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-855">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-856">**return_entry_name**: varsayılan dizindeki bir sonraki giriş adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-856">**return_entry_name**: Pointer to destination for the next entry name in the default directory.</span></span> <span data-ttu-id="8ac81-857">Bu işaretçinin işaret ettiği arabellek, **_FX_MAX_LONG_NAME_LEN_** tarafından tanımlanan en büyük FileX adı boyutunu tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-857">The buffer this pointer points to must be large enough to hold the maximum size of FileX name, defined by **_FX_MAX_LONG_NAME_LEN_**.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-858">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-858">Return Values</span></span>

- <span data-ttu-id="8ac81-859">**FX_SUCCESS** (0x00) başarılı bir sonraki giriş bul</span><span class="sxs-lookup"><span data-stu-id="8ac81-859">**FX_SUCCESS** (0x00) Successful next entry find</span></span>
- <span data-ttu-id="8ac81-860">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-860">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-861">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-861">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="8ac81-862">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-862">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-863">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-863">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-864">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-864">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-865">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-865">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-866">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-866">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-867">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-867">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-868">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-868">**FX_CALLER_ERROR** (0x20)     Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-869">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-869">Allowed From</span></span>

<span data-ttu-id="8ac81-870">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-871">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-871">Example</span></span>

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-872">See Also</span></span>

- <span data-ttu-id="8ac81-873">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-873">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-874">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-874">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-875">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-875">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-876">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-876">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-877">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-877">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-878">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-878">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-879">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-879">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-880">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-880">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-881">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-881">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-882">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-882">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-883">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-883">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-884">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-884">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-885">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-885">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-886">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-886">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-887">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-887">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-888">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-888">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-889">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-889">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-890">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-890">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-891">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-891">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-892">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-892">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="8ac81-893">fx_directory_next_full_entry_find:</span><span class="sxs-lookup"><span data-stu-id="8ac81-893">fx_directory_next_full_entry_find:</span></span>

<span data-ttu-id="8ac81-894">Tam bilgi içeren bir sonraki dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-894">Gets next directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-895">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-895">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="8ac81-896">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-896">Description</span></span>

<span data-ttu-id="8ac81-897">Bu hizmet, varsayılan dizindeki bir sonraki giriş adını alır ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-897">This service retrieves the next entry name in the default directory and copies it to the specified destination.</span></span> <span data-ttu-id="8ac81-898">Ayrıca, ek giriş parametreleriyle belirtilen girdi hakkında tam bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-898">It also returns full information about the entry as specified by the additional input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-899">\* Belirtilen hedef, \* \* \* FX_MAX_LONG_NAME_LEN \* \* \* \* ile tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır</span><span class="sxs-lookup"><span data-stu-id="8ac81-899">\*The specified destination must be large enough to hold the maximum sized FileX name, as defined by \*\*\*FX_MAX_LONG_NAME_LEN\*\*\*\*</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-900">*Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-900">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-901">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-901">Input Parameters</span></span>

- <span data-ttu-id="8ac81-902">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-902">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-903">**directory_name:** Dizin girişinin adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-903">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="8ac81-904">en az bir veya daha büyük **FX_MAX_LONG_NAME_LEN.**</span><span class="sxs-lookup"><span data-stu-id="8ac81-904">Must be at least as big as **FX_MAX_LONG_NAME_LEN**.</span></span>
- <span data-ttu-id="8ac81-905">**attributes:** Null olmayan bir değerse, girişin yerleştirilecek öznitelikleri için hedefin işaretçisi. Öznitelikler, aşağıdaki olası ayarlarla bit eşlemesi biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8ac81-905">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8ac81-906">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-906">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="8ac81-907">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-907">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="8ac81-908">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="8ac81-908">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="8ac81-909">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="8ac81-909">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="8ac81-910">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="8ac81-910">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="8ac81-911">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="8ac81-911">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="8ac81-912">**size:** Null olmayan bir değerse, girişin boyutu için hedefin bayt cinsinden işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-912">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="8ac81-913">**month:** Null olmayan bir değerse, girişin değişiklik ayı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-913">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="8ac81-914">**year:** Null olmayan bir değerse, girişin değişiklik yılı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-914">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="8ac81-915">**day:** Null olmayan bir değerse, girişin değişiklik günü için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-915">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="8ac81-916">**hour:** Null olmayan bir değerse, girişin değişiklik saati için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-916">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="8ac81-917">**minute:** Null olmayan bir değerse, girişin değişiklik dakikası için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-917">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="8ac81-918">**second:** Null olmayan bir değerse, girişin ikinci değişikliği için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-918">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-919">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-919">Return Values</span></span>

- <span data-ttu-id="8ac81-920">**FX_SUCCESS** (0x00) Başarılı dizin sonraki girdi bulma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-920">**FX_SUCCESS** (0x00) Successful directory next entry find.</span></span>
- <span data-ttu-id="8ac81-921">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-921">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-922">**FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-922">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="8ac81-923">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-923">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-924">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-924">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-925">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-925">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-926">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-926">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-927">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-927">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8ac81-928">**FX_MEDIA_INVALID** (0x02) Geçersiz medya.</span><span class="sxs-lookup"><span data-stu-id="8ac81-928">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-929">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi veya tüm giriş parametreleri NULL.</span><span class="sxs-lookup"><span data-stu-id="8ac81-929">**FX_PTR_ERROR** (0x18) Invalid media pointer or all input parameters are NULL.</span></span>
- <span data-ttu-id="8ac81-930">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-930">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-931">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-931">Allowed From</span></span>

<span data-ttu-id="8ac81-932">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-932">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-933">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-933">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-934">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-934">See Also</span></span>

- <span data-ttu-id="8ac81-935">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-935">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-936">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-936">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-937">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-937">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-938">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-938">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-939">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-939">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-940">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-940">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-941">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-941">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-942">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-942">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-943">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-943">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-944">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-944">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-945">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-945">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-946">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-946">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-947">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-947">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-948">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-948">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-949">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-949">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-950">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-950">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-951">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-951">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-952">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-952">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-953">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-953">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-954">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-954">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_rename"></a><span data-ttu-id="8ac81-955">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-955">fx_directory_rename</span></span>

<span data-ttu-id="8ac81-956">Dizini yeniden adlandırıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-956">Renames directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-957">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-957">Prototype</span></span>

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-958">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-958">Description</span></span>

<span data-ttu-id="8ac81-959">Bu hizmet, dizin adını belirtilen yeni dizin adıyla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-959">This service changes the directory name to the specified new directory name.</span></span> <span data-ttu-id="8ac81-960">Yeniden adı, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-960">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="8ac81-961">Yeni dizin adı içinde bir yol belirtilirse, yeniden adlandırılan dizin belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-961">If a path is specified in the new directory name, the renamed directory is effectively moved to the specified path.</span></span> <span data-ttu-id="8ac81-962">Yol belirtilmezse, yeniden adlandırılan dizin geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-962">If no path is specified, the renamed directory is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-963">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-963">Input Parameters</span></span>

- <span data-ttu-id="8ac81-964">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-964">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-965">**old_directory_name:** Geçerli dizin adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-965">**old_directory_name**: Pointer to current directory name.</span></span>
- <span data-ttu-id="8ac81-966">**new_directory_name:** Yeni dizin adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-966">**new_directory_name**: Pointer to new directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-967">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-967">Return Values</span></span>

- <span data-ttu-id="8ac81-968">**FX_SUCCESS** (0x00) Başarılı dizin yeniden adlandırması.</span><span class="sxs-lookup"><span data-stu-id="8ac81-968">**FX_SUCCESS** (0x00) Successful directory rename.</span></span>
- <span data-ttu-id="8ac81-969">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-969">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-970">**FX_NOT_FOUND** (0x04) Dizin girdisi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-970">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="8ac81-971">**FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-971">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory.</span></span>
- <span data-ttu-id="8ac81-972">**FX_INVALID_NAME** (0x0C) Yeni dizin adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-972">**FX_INVALID_NAME** (0x0C) New directory name is invalid.</span></span>
- <span data-ttu-id="8ac81-973">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-973">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-974">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-974">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-975">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-975">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-976">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-976">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-977">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-977">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-978">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-978">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8ac81-979">**FX_MEDIA_INVALID** (0x02) Geçersiz medya.</span><span class="sxs-lookup"><span data-stu-id="8ac81-979">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-980">**FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-980">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="8ac81-981">**FX_INVALID_PATH** (0x0D) Dizin adı ile sağlanan geçersiz yol.</span><span class="sxs-lookup"><span data-stu-id="8ac81-981">**FX_INVALID_PATH** (0x0D) Invalid path supplied with directory name.</span></span>
- <span data-ttu-id="8ac81-982">**FX_ALREADY_CREATED** (0x0B) Belirtilen dizin zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="8ac81-982">**FX_ALREADY_CREATED** (0x0B) Specified directory was already created.</span></span>
- <span data-ttu-id="8ac81-983">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-983">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-984">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-984">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-985">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-985">Allowed From</span></span>

<span data-ttu-id="8ac81-986">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-986">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-987">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-987">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-988">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-988">See Also</span></span>

- <span data-ttu-id="8ac81-989">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-989">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-990">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-990">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-991">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-991">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-992">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-992">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-993">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-993">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-994">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-994">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-995">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-995">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-996">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-996">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-997">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-997">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-998">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-998">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-999">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-999">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-1000">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-1000">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-1001">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1001">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-1002">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1002">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-1003">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-1003">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-1004">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1004">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-1005">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1005">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-1006">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1006">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-1007">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1007">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-1008">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1008">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get"></a><span data-ttu-id="8ac81-1009">fx_directory_short_name_get:</span><span class="sxs-lookup"><span data-stu-id="8ac81-1009">fx_directory_short_name_get:</span></span>

<span data-ttu-id="8ac81-1010">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-1010">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1011">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1011">Prototype</span></span>

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-1012">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1012">Description</span></span>

<span data-ttu-id="8ac81-1013">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1013">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="8ac81-1014">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1014">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1015">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1015">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1016">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1016">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-1017">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1017">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="8ac81-1018">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1018">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="8ac81-1019">Kısa ad hedefinin 14 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1019">Note that the destination for the short name must be large enough to hold 14 characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1020">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1020">Return Values</span></span>

- <span data-ttu-id="8ac81-1021">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1021">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="8ac81-1022">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1022">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="8ac81-1023">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1023">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1024">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1024">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1025">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1025">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1026">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1026">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1027">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1027">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1028">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1028">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1029">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1029">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-1030">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1030">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8ac81-1031">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1031">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1032">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1032">Allowed From</span></span>

<span data-ttu-id="8ac81-1033">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1033">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1034">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1034">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1035">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1035">See Also</span></span>

- <span data-ttu-id="8ac81-1036">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1036">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-1037">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1037">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-1038">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1038">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-1039">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1039">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-1040">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1040">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-1041">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1041">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-1042">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1042">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-1043">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1043">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-1044">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1044">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-1045">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-1045">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-1046">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1046">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-1047">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-1047">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-1048">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1048">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-1049">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1049">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-1050">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-1050">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-1051">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1051">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-1052">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1052">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-1053">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1053">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-1054">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1054">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-1055">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1055">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get_extended"></a><span data-ttu-id="8ac81-1056">fx_directory_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8ac81-1056">fx_directory_short_name_get_extended</span></span>

<span data-ttu-id="8ac81-1057">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-1057">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1058">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1058">Prototype</span></span>

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a><span data-ttu-id="8ac81-1059">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1059">Description</span></span>

<span data-ttu-id="8ac81-1060">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1060">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="8ac81-1061">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1061">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1062">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1062">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1063">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1063">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-1064">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1064">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="8ac81-1065">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1065">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="8ac81-1066">Note: kısa ad hedefi 14 karakter tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1066">Note: Destination for the short name must be large enough to hold 14 characters.</span></span>
- <span data-ttu-id="8ac81-1067">**short_file_name_length**: kısa ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1067">**short_file_name_length**: Length of short name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1068">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1068">Return Values</span></span>

- <span data-ttu-id="8ac81-1069">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1069">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="8ac81-1070">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1070">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="8ac81-1071">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1071">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1072">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1072">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1073">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1074">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1075">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1075">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1076">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1076">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1077">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1077">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-1078">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1078">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8ac81-1079">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1079">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1080">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1080">Allowed From</span></span>

<span data-ttu-id="8ac81-1081">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1081">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1082">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1082">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1083">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1083">See Also</span></span>

- <span data-ttu-id="8ac81-1084">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1084">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-1085">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1085">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-1086">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1086">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-1087">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1087">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-1088">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1088">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-1089">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1089">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-1090">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1090">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-1091">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1091">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-1092">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1092">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-1093">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-1093">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-1094">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1094">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-1095">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-1095">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-1096">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1096">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-1097">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1097">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-1098">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-1098">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-1099">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1099">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-1100">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-1100">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-1101">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1101">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-1102">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1102">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8ac81-1103">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1103">fx_unicode_directory_rename</span></span>

## <a name="fx_fault_tolerant_enable"></a><span data-ttu-id="8ac81-1104">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-1104">fx_fault_tolerant_enable</span></span>

<span data-ttu-id="8ac81-1105">Hataya karşı iyi hizmet sağlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-1105">Enables the fault tolerant service</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1106">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1106">Prototype</span></span>

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a><span data-ttu-id="8ac81-1107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1107">Description</span></span>

<span data-ttu-id="8ac81-1108">Bu hizmet hataya karşı iyi bir modül sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1108">This service enables the fault tolerant module.</span></span> <span data-ttu-id="8ac81-1109">Başlatmadan sonra hataya karşı koruma modülü, dosya sisteminin FileX hataya karşı koruma altında olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1109">Upon starting, the fault tolerant module detects whether or not the file system is under FileX fault tolerant protection.</span></span> <span data-ttu-id="8ac81-1110">Yoksa, hizmet dosya sistemi işlemlerinde günlükleri depolamak için dosya sistemi üzerinde kullanılabilir kesimleri bulur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1110">If it is not, the service finds available sectors on the file system to store logs on file system transactions.</span></span> <span data-ttu-id="8ac81-1111">Dosya sistemi FileX hataya karşı koruma altında ise, bütünlüğünü korumak için günlükleri dosya sistemine uygular.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1111">If the file system is under FileX fault tolerant protection, it applies the logs to the file system to maintain its integrity.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1112">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1112">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1113">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1113">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-1114">**memory_ptr:** Hataya dayanıklı modül tarafından karalama belleği olarak kullanılan bir bellek bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1114">**memory_ptr**: Pointer to a block of memory used by the fault tolerant module as scratch memory.</span></span>
- <span data-ttu-id="8ac81-1115">**memory_size:** Karalama belleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1115">**memory_size**: The size of the scratch memory.</span></span> <span data-ttu-id="8ac81-1116">Hataya dayanıklının düzgün çalışması için, karalama belleği boyutu en az 3072 bayt olmalı ve kesim boyutunun katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1116">In order for fault tolerant to work properly, the scratch memory size shall be at least 3072 bytes,- and must be multiple of sector size.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1117">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1117">Return Values</span></span>

- <span data-ttu-id="8ac81-1118">**FX_SUCCESS** (0x00) Hataya karşı iyi bir şekilde etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1118">**FX_SUCCESS** (0x00) Successfully enabled fault tolerant.</span></span>
- <span data-ttu-id="8ac81-1119">**FX_NOT_ENOUGH_MEMORY** (0x91) bellek boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1119">**FX_NOT_ENOUGH_MEMORY** (0x91)    memory size too small.</span></span>
- <span data-ttu-id="8ac81-1120">**FX_BOOT_ERROR** (0x01) Önyükleme kesimi hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1120">**FX_BOOT_ERROR** (0x01) Boot sector error.</span></span>
- <span data-ttu-id="8ac81-1121">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1121">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1122">**FX_NO_MORE_ENTRIES** (0x0F) Artık ücretsiz küme yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1122">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="8ac81-1123">**FX_NO_MORE_SPACE** (0x0A) Bu dosyayla ilişkilendirilmiş medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1123">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8ac81-1124">**FX_SECTOR_INVALID** (0x89) Kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="8ac81-1124">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="8ac81-1125">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1125">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1126">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1126">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-1127">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1127">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1128">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1128">Allowed From</span></span>

<span data-ttu-id="8ac81-1129">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1129">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1130">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1130">Example</span></span>

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a><span data-ttu-id="8ac81-1131">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1131">See Also</span></span>

- <span data-ttu-id="8ac81-1132">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-1132">fx_system_initialize</span></span>
- <span data-ttu-id="8ac81-1133">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-1133">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-1134">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1134">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-1135">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-1135">fx_media_check</span></span>
- <span data-ttu-id="8ac81-1136">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1136">fx_media_close</span></span>
- <span data-ttu-id="8ac81-1137">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1137">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-1138">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-1138">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-1139">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-1139">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-1140">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-1140">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-1141">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-1141">fx_media_format</span></span>
- <span data-ttu-id="8ac81-1142">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1142">fx_media_open</span></span>
- <span data-ttu-id="8ac81-1143">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1143">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-1144">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1144">fx_media_read</span></span>
- <span data-ttu-id="8ac81-1145">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-1145">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-1146">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1146">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-1147">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1147">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-1148">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1148">fx_media_write</span></span>

## <a name="fx_file_allocate"></a><span data-ttu-id="8ac81-1149">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1149">fx_file_allocate</span></span>

<span data-ttu-id="8ac81-1150">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="8ac81-1150">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1151">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1151">Prototype</span></span>

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="8ac81-1152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1152">Description</span></span>

<span data-ttu-id="8ac81-1153">Bu hizmet, bir veya daha fazla bitişik kümeyi belirtilen dosyanın sonuna ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1153">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8ac81-1154">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1154">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8ac81-1155">Sonuç daha sonra bir sonraki kümenin tamam yanına yuvarlanmış olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1155">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="8ac81-1156">Uygulama, 4 GB'ın üzerinde alan ayırmak için hizmet *fx_file_extended_allocate.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1156">To allocate space beyond 4GB, application shall use the service *fx_file_extended_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1157">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1158">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1158">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-1159">**boyut:** Dosya için ayrılarak ayrılan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1159">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1160">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1160">Return Values</span></span>

- <span data-ttu-id="8ac81-1161">**FX_SUCCESS** (0x00) Başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1161">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="8ac81-1162">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1162">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-1163">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1163">**FX_FAT_READ_ERROR** (0x03) Failed to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1164">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1164">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1165">**FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1165">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-1166">**FX_NO_MORE_ENTRIES** (0x0F) Artık ücretsiz küme yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1166">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="8ac81-1167">**FX_NO_MORE_SPACE** (0x0A) Bu dosyayla ilişkilendirilmiş medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1167">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8ac81-1168">**FX_SECTOR_INVALID** (0x89) Kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="8ac81-1168">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="8ac81-1169">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1169">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1170">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1170">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1171">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1171">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-1172">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1172">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1173">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1173">Allowed From</span></span>

<span data-ttu-id="8ac81-1174">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1175">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1175">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1176">See Also</span></span>

- <span data-ttu-id="8ac81-1177">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1177">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1178">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1178">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1179">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1179">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1180">fx_file_close- fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1180">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="8ac81-1181">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1181">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1182">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1182">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1183">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1183">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1184">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1184">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1185">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1185">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1186">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1186">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1187">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1187">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1188">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1188">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1189">fx_file_open- fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1189">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="8ac81-1190">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1190">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1191">fx_file_rename- fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1191">fx_file_rename- fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1192">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1192">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1193">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1193">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1194">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1194">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1195">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1195">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1196">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1196">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1197">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1197">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1198">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1198">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1199">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1199">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_read"></a><span data-ttu-id="8ac81-1200">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1200">fx_file_attributes_read</span></span>

<span data-ttu-id="8ac81-1201">Dosya özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="8ac81-1201">Reads file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1202">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1202">Prototype</span></span>

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-1203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1203">Description</span></span>

<span data-ttu-id="8ac81-1204">Bu hizmet, dosyanın özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1204">This service reads the file's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1205">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1206">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1206">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-1207">**file_name**: istenen dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1207">**file_name**: Pointer to the name of the requested file (directory path is optional).</span></span>
- <span data-ttu-id="8ac81-1208">**attributes_ptr**: dosyaya yerleştirilecek özniteliklerin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1208">**attributes_ptr**: Pointer to the destination for the file's attributes to be placed.</span></span> <span data-ttu-id="8ac81-1209">Dosya öznitelikleri, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8ac81-1209">The file attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8ac81-1210">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1210">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8ac81-1211">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1211">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8ac81-1212">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1212">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8ac81-1213">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1213">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="8ac81-1214">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1214">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="8ac81-1215">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1215">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1216">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1216">Return Values</span></span>

- <span data-ttu-id="8ac81-1217">**FX_SUCCESS** (0x00) başarılı özniteliği okundu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1217">**FX_SUCCESS** (0x00) Successful attribute read.</span></span>
- <span data-ttu-id="8ac81-1218">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1218">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-1219">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1219">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="8ac81-1220">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1220">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="8ac81-1221">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1221">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1222">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1222">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1223">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1223">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1224">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1224">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1225">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1225">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1226">**FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1226">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="8ac81-1227">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1227">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1228">Allowed From</span></span>

<span data-ttu-id="8ac81-1229">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1230">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1230">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-1231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1231">See Also</span></span>

- <span data-ttu-id="8ac81-1232">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1232">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1233">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1233">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1234">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1234">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1235">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1235">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="8ac81-1236">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1236">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1237">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1237">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1238">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1238">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1239">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1239">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1240">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1240">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1241">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1241">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1242">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1242">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1243">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1243">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1244">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1244">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1245">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1245">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1246">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1246">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1247">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1247">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1248">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1248">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1249">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1249">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1250">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1250">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1251">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1251">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1252">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1252">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1253">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1253">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1254">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1254">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1255">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1255">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1256">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1256">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_set"></a><span data-ttu-id="8ac81-1257">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1257">fx_file_attributes_set</span></span>

<span data-ttu-id="8ac81-1258">Dosya özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-1258">Sets file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1259">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1259">Prototype</span></span>

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a><span data-ttu-id="8ac81-1260">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1260">Description</span></span>

<span data-ttu-id="8ac81-1261">Bu hizmet, dosyanın özniteliklerini çağıran tarafından belirtilen olanlarla ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1261">This service sets the file's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-1262">*Uygulamanın yalnızca bu hizmetle birlikte dosyanın özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlamaya yönelik her türlü girişim bir hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1262">*The application is only allowed to modify a subset of the file's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1263">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1263">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1264">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1264">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-1265">**file_name**: istenen dosyanın adı işaretçisi \* \* (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1265">**file_name**: Pointer to the name of the requested file\*\* (directory path is optional).</span></span>
- <span data-ttu-id="8ac81-1266">**öznitelikler**: dosyanın yeni öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1266">**attributes**: The new attributes for the file.</span></span> <span data-ttu-id="8ac81-1267">Geçerli dosya öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-1267">The valid file attributes are defined as follows:</span></span>
  - <span data-ttu-id="8ac81-1268">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1268">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8ac81-1269">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1269">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8ac81-1270">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1270">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8ac81-1271">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1271">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1272">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1272">Return Values</span></span>

- <span data-ttu-id="8ac81-1273">**FX_SUCCESS** (0x00) başarılı öznitelik kümesi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1273">**FX_SUCCESS** (0x00) Successful attribute set.</span></span>
- <span data-ttu-id="8ac81-1274">**FX_ACCESS_ERROR** (0x06) dosyası açık ve öznitelikleri ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1274">**FX_ACCESS_ERROR** (0x06) File is open and cannot have its attributes set.</span></span>
- <span data-ttu-id="8ac81-1275">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1275">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1276">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1276">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-1278">**FX_NO_MORE_ENTRIES** (0x0F) FAT tablosunda veya exFAT Cluster eşlemesinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1278">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in the FAT table or exFAT cluster map.</span></span>
- <span data-ttu-id="8ac81-1279">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1279">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8ac81-1280">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1280">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="8ac81-1281">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1281">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="8ac81-1282">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="8ac81-1282">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="8ac81-1283">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1283">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1284">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1284">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1285">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1285">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-1286">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1286">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-1287">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1287">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="8ac81-1288">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1288">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1289">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1289">Allowed From</span></span>

<span data-ttu-id="8ac81-1290">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1290">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1291">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1291">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-1292">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1292">See Also</span></span>

- <span data-ttu-id="8ac81-1293">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1293">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1294">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1294">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1295">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1295">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1296">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1296">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1297">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1297">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1298">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1298">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1299">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1299">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1300">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1300">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1301">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1301">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1302">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1302">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1303">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1303">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1304">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1304">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1305">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1305">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1306">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1306">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1307">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1307">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1308">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1308">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1309">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1309">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1310">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1310">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1311">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1311">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1312">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1312">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1313">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1313">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1314">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1314">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1315">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1315">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1316">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1316">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1317">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1317">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1318">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1318">fx_unicode_short_name_get</span></span>

## <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="8ac81-1319">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1319">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="8ac81-1320">Dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="8ac81-1320">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1321">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1321">Prototype</span></span>

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="8ac81-1322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1322">Description</span></span>

<span data-ttu-id="8ac81-1323">Bu hizmet, bir veya daha fazla bitişik kümeyi belirtilen dosyanın sonuna ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1323">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8ac81-1324">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1324">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8ac81-1325">Sonuç daha sonra bir sonraki kümenin tamam yanına yuvarlanmış olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1325">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="8ac81-1326">Medyada yeterli ardışık küme yoksa, bu hizmet ardışık kümeler için kullanılabilen en büyük bloğu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1326">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="8ac81-1327">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1327">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="8ac81-1328">Uygulama, 4 GB'ın üzerinde alan ayırmak için hizmet *fx_file_extended_best_effort_allocate.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1328">To allocate space beyond 4GB, application shall use the service *fx_file_extended_best_effort_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1329">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1329">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1330">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1330">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-1331">**boyut:** Dosya için ayrılarak ayrılan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1331">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1332">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1332">Return Values</span></span>

- <span data-ttu-id="8ac81-1333">**FX_SUCCESS** (0x00) Başarılı en iyi çaba dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1333">**FX_SUCCESS** (0x00) Successful best-effort file allocation.</span></span>
- <span data-ttu-id="8ac81-1334">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1334">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-1335">**FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1335">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-1336">**FX_NO_MORE_SPACE** (0x0A) Bu dosyayla ilişkilendirilmiş medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1336">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8ac81-1337">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1337">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1338">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1338">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1339">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1339">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1340">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1340">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1341">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1341">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1342">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1342">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1343">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi veya hedefi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1343">**FX_PTR_ERROR** (0x18) Invalid file pointer or destination.</span></span>
- <span data-ttu-id="8ac81-1344">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1344">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1345">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1345">Allowed From</span></span>

<span data-ttu-id="8ac81-1346">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1346">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1347">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1347">Example</span></span>

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-1348">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1348">See Also</span></span>

- <span data-ttu-id="8ac81-1349">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1349">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1350">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1350">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1351">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1351">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1352">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1353">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1354">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1355">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1359">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1362">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1363">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1364">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1365">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1366">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1367">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1368">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1369">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1371">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1371">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1372">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1372">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1373">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1373">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1374">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1374">fx_unicode_short_name_get</span></span>

## <a name="fx_file_close"></a><span data-ttu-id="8ac81-1375">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1375">fx_file_close</span></span>

<span data-ttu-id="8ac81-1376">Dosyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="8ac81-1376">Closes file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1377">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1377">Prototype</span></span>

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-1378">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1378">Description</span></span>

<span data-ttu-id="8ac81-1379">Bu hizmet belirtilen dosyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1379">This service closes the specified file.</span></span> <span data-ttu-id="8ac81-1380">Dosya yazmaya açıksa ve değiştirilmişse, bu hizmet dizin girdisini yeni boyut ve geçerli sistem saati ve tarihi ile güncelleştirerek dosya değiştirme işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1380">If the file was open for writing and if it was modified, this service completes the file modification process by updating its directory entry with the new size and the current system time and date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1381">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1381">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1382">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1382">**file_ptr**: Pointer to a previously opened file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1383">Return Values</span></span>

- <span data-ttu-id="8ac81-1384">**FX_SUCCESS** (0x00) Başarılı dosya kapatma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1384">**FX_SUCCESS** (0x00) Successful file close.</span></span>
- <span data-ttu-id="8ac81-1385">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1385">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8ac81-1386">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1386">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1387">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1387">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1388">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1388">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1389">**FX_PTR_ERROR** (0x18) Geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1389">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="8ac81-1390">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1390">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1391">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1391">Allowed From</span></span>

<span data-ttu-id="8ac81-1392">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1392">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1393">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1393">Example</span></span>

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1394">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1394">See Also</span></span>

- <span data-ttu-id="8ac81-1395">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1395">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1396">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1396">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1397">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1397">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1398">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1398">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1399">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1399">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1400">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1400">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1401">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1401">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1402">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1402">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1403">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1403">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1404">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1404">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1405">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1405">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1406">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1406">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1407">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1407">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1408">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1408">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1409">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1409">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1410">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1410">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1411">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1411">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1412">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1412">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1413">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1413">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1414">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1414">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1415">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1415">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1416">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1416">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1417">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1417">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1418">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1418">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1419">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1419">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1420">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1420">fx_unicode_short_name_get</span></span>

## <a name="fx_file_create"></a><span data-ttu-id="8ac81-1421">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1421">fx_file_create</span></span>

<span data-ttu-id="8ac81-1422">Dosya oluşturur</span><span class="sxs-lookup"><span data-stu-id="8ac81-1422">Creates file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1423">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1423">Prototype</span></span>

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-1424">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1424">Description</span></span>

<span data-ttu-id="8ac81-1425">Bu hizmet, belirtilen dosyayı varsayılan dizinde veya dosya adıyla sağlanan dizin yolunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1425">This service creates the specified file in the default directory or in the directory path supplied with the file name.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-1426">*Bu hizmet sıfır uzunluklu bir dosya oluşturur, başka bir ifadeyle ayrılmış küme yoktur. Ayırma, sonraki dosya yazmalarında otomatik olarak yapılır veya fx_file_allocate hizmetiyle veya 4 GB'ın fx_file_extended_allocate alan için önceden yapılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1426">*This service creates a file of zero length, i.e., no clusters allocated. Allocation will automatically take place on subsequent file writes or can be done in advance with the fx_file_allocate service or fx_file_extended_allocate for space beyond 4GB) service.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1427">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1427">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1428">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1428">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-1429">**file_name:** Oluşturulacak dosyanın adının işaretçisi (dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1429">**file_name**: Pointer to the name of the file to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1430">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1430">Return Values</span></span>

- <span data-ttu-id="8ac81-1431">**FX_SUCCESS** (0x00) Başarılı dosya oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1431">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="8ac81-1432">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1432">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-1433">**FX_ALREADY_CREATED** (0x0B) Belirtilen dosya zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1433">**FX_ALREADY_CREATED** (0x0B) Specified file was already created.</span></span>
- <span data-ttu-id="8ac81-1434">**FX_NO_MORE_SPACE** (0x0A) Kök dizinde daha fazla giriş yok veya kullanılabilir başka küme yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1434">**FX_NO_MORE_SPACE** (0x0A)    Either there are no more entries in the root directory or there are no more clusters available.</span></span>
- <span data-ttu-id="8ac81-1435">**FX_INVALID_PATH** (0x0D) Dosya adıyla sağlanan geçersiz yol.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1435">**FX_INVALID_PATH** (0x0D) Invalid path supplied with file name.</span></span>
- <span data-ttu-id="8ac81-1436">**FX_INVALID_NAME** (0x0C) Dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1436">**FX_INVALID_NAME** (0x0C) File name is invalid.</span></span>
- <span data-ttu-id="8ac81-1437">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1437">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1438">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1438">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1439">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1439">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1440">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1440">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1441">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1441">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1442">**FX_MEDIA_INVALID** (0x02)Geçersiz medya.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1442">**FX_MEDIA_INVALID** (0x02)Invalid media.</span></span>
- <span data-ttu-id="8ac81-1443">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1443">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1444">**FX_WRITE_PROTECT** (0x23) Temel alınan medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1444">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8ac81-1445">**FX_PTR_ERROR** (0x18) Geçersiz medya veya dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1445">**FX_PTR_ERROR** (0x18) Invalid media or file name pointer.</span></span>
- <span data-ttu-id="8ac81-1446">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1446">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1447">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1447">Allowed From</span></span>

<span data-ttu-id="8ac81-1448">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1448">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1449">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1449">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1450">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1450">See Also</span></span>
- <span data-ttu-id="8ac81-1451">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1451">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1452">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1452">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1453">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1453">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1454">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1454">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1455">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1455">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1456">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1456">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1457">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1457">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1458">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1458">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1459">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1459">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1460">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1460">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1461">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1461">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1462">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1462">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1463">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1463">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1464">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1464">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1465">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1465">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1466">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1466">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1467">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1467">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1468">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1468">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1469">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1469">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1470">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1470">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1471">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1471">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1472">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1472">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1473">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1473">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1474">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1474">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1475">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1475">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1476">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1476">fx_unicode_short_name_get</span></span>

## <a name="fx_file_date_time_set"></a><span data-ttu-id="8ac81-1477">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1477">fx_file_date_time_set</span></span>

### <a name="sets-file-date-and-time"></a><span data-ttu-id="8ac81-1478">Dosya tarih ve saati ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-1478">Sets file date and time</span></span>

<span data-ttu-id="8ac81-1479">Dosya Tarihi ve Saati Ayarlama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1479">Setting File Date and Time</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1480">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1480">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="8ac81-1481">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1481">Description</span></span>

<span data-ttu-id="8ac81-1482">Bu hizmet, belirtilen dosyanın tarih ve saati ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1482">This service sets the date and time of the specified file.</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1483">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1483">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1484">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1484">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-1485">**file_name:** Dosyanın adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1485">**file_name**: Pointer to name of the file.</span></span>
- <span data-ttu-id="8ac81-1486">**year:** Yılın değeri (1980-2107 dahil).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1486">**year**: Value of year (1980-2107 inclusive).</span></span>
- <span data-ttu-id="8ac81-1487">**month:** Ayın değeri (1-12 dahil).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1487">**month**: Value of month (1-12 inclusive).</span></span>
- <span data-ttu-id="8ac81-1488">**day:** Günün değeri (1-31 dahil).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1488">**day**: Value of day (1-31 inclusive).</span></span>
- <span data-ttu-id="8ac81-1489">**hour:** Saat değeri (0-23 dahil).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1489">**hour**: Value of hour (0-23 inclusive).</span></span>
- <span data-ttu-id="8ac81-1490">**minute:** Dakika değeri (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1490">**minute**: Value of minute (0-59 inclusive).</span></span>
- <span data-ttu-id="8ac81-1491">**second:** Saniyenin değeri (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1491">**second**: Value of second (0-59 inclusive).</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1492">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1492">Return Values</span></span>

- <span data-ttu-id="8ac81-1493">**FX_SUCCESS** (0x00) Başarılı tarih/saat kümesi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1493">**FX_SUCCESS** (0x00) Successful date/time set.</span></span>
- <span data-ttu-id="8ac81-1494">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1494">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-1495">**FX_NOT_FOUND** (0x04) Dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1495">**FX_NOT_FOUND** (0x04)    File was not found.</span></span>
- <span data-ttu-id="8ac81-1496">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1496">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1497">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1497">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1498">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1498">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1499">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1499">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1500">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1500">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8ac81-1501">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1501">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1502">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1502">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1503">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1503">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8ac81-1504">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1504">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="8ac81-1505">**FX_INVALID_YEAR** (0x12) yıl geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1505">**FX_INVALID_YEAR** (0x12) Year is invalid.</span></span>
- <span data-ttu-id="8ac81-1506">**FX_INVALID_MONTH** (0x13) ay geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1506">**FX_INVALID_MONTH** (0x13) Month is invalid.</span></span>
- <span data-ttu-id="8ac81-1507">**FX_INVALID_DAY** (0x14) gün geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1507">**FX_INVALID_DAY** (0x14) Day is invalid.</span></span>
- <span data-ttu-id="8ac81-1508">**FX_INVALID_HOUR** (0x15) saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1508">**FX_INVALID_HOUR** (0x15)    Hour is invalid.</span></span>
- <span data-ttu-id="8ac81-1509">**FX_INVALID_MINUTE** (0x16) dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1509">**FX_INVALID_MINUTE** (0x16) Minute is invalid.</span></span>
- <span data-ttu-id="8ac81-1510">**FX_INVALID_SECOND** (0x17) saniye geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1510">**FX_INVALID_SECOND** (0x17) Second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1511">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1511">Allowed From</span></span>

<span data-ttu-id="8ac81-1512">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1512">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1513">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1513">Example</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1514">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1514">See Also</span></span>

- <span data-ttu-id="8ac81-1515">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1515">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1516">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1516">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1517">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1517">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1518">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1518">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1519">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1519">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1520">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1520">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1521">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1521">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1522">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1522">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1523">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1523">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1524">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1524">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1525">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1525">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1526">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1526">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1527">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1527">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1528">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1528">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1529">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1529">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1530">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1530">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1531">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1531">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1532">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1532">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1533">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1533">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1534">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1534">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1535">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1535">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1536">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1536">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1537">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1537">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1538">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1538">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1539">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1539">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1540">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1540">fx_unicode_short_name_get</span></span>

## <a name="fx_file_delete"></a><span data-ttu-id="8ac81-1541">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1541">fx_file_delete</span></span>

### <a name="deletes-file"></a><span data-ttu-id="8ac81-1542">Dosyayı siler</span><span class="sxs-lookup"><span data-stu-id="8ac81-1542">Deletes file</span></span>

<span data-ttu-id="8ac81-1543">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="8ac81-1543">File Deletion</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1544">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1544">Prototype</span></span>

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-1545">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1545">Description</span></span>

<span data-ttu-id="8ac81-1546">Bu hizmet, belirtilen dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1546">This service deletes the specified file.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="8ac81-1547">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1547">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1548">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1548">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-1549">**file_name**: Silinecek dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1549">**file_name**: Pointer to the name of the file to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1550">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1550">Return Values</span></span>

- <span data-ttu-id="8ac81-1551">**FX_SUCCESS** (0x00) başarılı dosya silme.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1551">**FX_SUCCESS** (0x00) Successful file delete.</span></span>
- <span data-ttu-id="8ac81-1552">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1552">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-1553">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1553">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="8ac81-1554">**FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1554">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="8ac81-1555">**FX_ACCESS_ERROR** (0x06) belirtilen dosya şu anda açık.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1555">**FX_ACCESS_ERROR** (0x06) Specified file is currently open.</span></span>
- <span data-ttu-id="8ac81-1556">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1556">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1557">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1557">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1558">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1558">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1559">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1559">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1560">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1560">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1561">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1561">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1562">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1562">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1563">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1563">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-1564">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1564">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-1565">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1565">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1566">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1566">Allowed From</span></span>

<span data-ttu-id="8ac81-1567">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1568">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1568">Example</span></span>

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1569">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1569">See Also</span></span>

- <span data-ttu-id="8ac81-1570">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1570">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1571">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1571">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1572">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1572">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1573">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1573">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1574">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1574">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1575">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1575">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1576">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1576">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1577">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1577">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1578">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1578">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1579">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1579">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1580">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1580">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1581">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1581">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1582">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1582">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1583">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1583">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1584">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1584">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1585">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1585">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1586">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1586">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1587">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1587">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1588">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1588">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1589">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1589">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1590">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1590">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1591">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1591">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1592">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1592">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1593">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1593">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1594">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1594">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1595">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1595">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_allocate"></a><span data-ttu-id="8ac81-1596">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1596">fx_file_extended_allocate</span></span>

<span data-ttu-id="8ac81-1597">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="8ac81-1597">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1598">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1598">Prototype</span></span>

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="8ac81-1599">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1599">Description</span></span>

<span data-ttu-id="8ac81-1600">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1600">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8ac81-1601">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1601">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8ac81-1602">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1602">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="8ac81-1603">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1603">This service is designed for exFAT.</span></span> <span data-ttu-id="8ac81-1604">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1604">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1605">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1605">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1606">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1606">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-1607">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1607">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1608">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1608">Return Values</span></span>

- <span data-ttu-id="8ac81-1609">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1609">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="8ac81-1610">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1610">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-1611">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1611">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-1612">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1612">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8ac81-1613">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1613">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1614">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1614">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1615">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1615">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1616">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1616">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1617">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1617">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1618">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1618">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1619">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1619">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-1620">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1620">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1621">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1621">Allowed From</span></span>

<span data-ttu-id="8ac81-1622">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1622">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1623">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1623">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1624">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1624">See Also</span></span>

- <span data-ttu-id="8ac81-1625">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1625">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1626">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1626">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1627">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1627">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1628">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1628">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1629">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1629">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1630">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1630">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1631">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1631">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1632">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1632">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1633">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1633">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1634">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1634">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1635">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1635">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1636">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1636">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1637">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1637">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1638">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1638">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1639">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1639">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1640">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1640">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1641">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1641">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1642">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1642">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1643">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1643">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1644">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1644">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1645">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1645">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1646">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1646">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1647">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1647">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1648">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1648">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1649">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1649">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1650">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1650">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_best_effort_allocate"></a><span data-ttu-id="8ac81-1651">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1651">fx_file_extended_best_effort_allocate</span></span>

<span data-ttu-id="8ac81-1652">Bir dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="8ac81-1652">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1653">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1653">Prototype</span></span>

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="8ac81-1654">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1654">Description</span></span>

<span data-ttu-id="8ac81-1655">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1655">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8ac81-1656">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1656">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8ac81-1657">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1657">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="8ac81-1658">Medyada yeterli sayıda ardışık küme yoksa, bu hizmet birbirini izleyen en büyük küme bloğunu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1658">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="8ac81-1659">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1659">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="8ac81-1660">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1660">This service is designed for exFAT.</span></span> <span data-ttu-id="8ac81-1661">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1661">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1662">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1662">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1663">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1663">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-1664">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1664">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1665">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1665">Return Values</span></span>

- <span data-ttu-id="8ac81-1666">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1666">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="8ac81-1667">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1667">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-1668">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1668">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-1669">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1669">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8ac81-1670">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1670">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1671">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1671">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1672">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1672">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1673">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1673">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1674">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1674">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1675">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1675">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1676">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1676">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-1677">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1677">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1678">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1678">Allowed From</span></span>

<span data-ttu-id="8ac81-1679">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1679">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1680">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1680">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-1681">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1681">See Also</span></span>

- <span data-ttu-id="8ac81-1682">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1682">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1683">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1683">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1684">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1684">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1685">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1685">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1686">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1686">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1687">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1688">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1688">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1689">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1689">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1690">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1690">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1691">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1691">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1692">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1692">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1693">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1693">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1694">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1694">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1695">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1695">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1696">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1696">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1697">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1697">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1698">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1698">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1699">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1699">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1700">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1700">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1701">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1701">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1702">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1702">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1703">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1703">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1704">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1704">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1705">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1705">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1706">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1706">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1707">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1707">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_relative_seek"></a><span data-ttu-id="8ac81-1708">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1708">fx_file_extended_relative_seek</span></span>

<span data-ttu-id="8ac81-1709">Göreli bir byte uzaklığına konumlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-1709">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1710">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1710">Prototype</span></span>

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="8ac81-1711">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1711">Description</span></span>

<span data-ttu-id="8ac81-1712">Bu hizmet, dahili dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1712">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="8ac81-1713">Sonraki herhangi bir dosya okuma veya yazma isteği, dosyada bu konumda başlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1713">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="8ac81-1714">Bu hizmet exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1714">This service is designed for exFAT.</span></span> <span data-ttu-id="8ac81-1715">Byte_offset  parametresi, çağıranın okuma/yazma işaretçisini 4 GB aralığının ötesinde yeniden konumlandırması için 64 bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1715">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-1716">*Arama işlemi dosyanın sonunu aramaya çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın sonuna konum sağlar. Buna karşılık, arama işlemi dosyanın başına konumlandırmaya çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başına konum sağlar.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1716">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1717">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1717">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1718">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1718">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-1719">**byte_offset:** Dosyada istenen göreli bayt uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1719">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="8ac81-1720">**seek_from:** Göreli aramanın nerede gerçekleştirecekleri yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1720">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="8ac81-1721">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-1721">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="8ac81-1722">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1722">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="8ac81-1723">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1723">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="8ac81-1724">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1724">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="8ac81-1725">FX_SEEK_BACK (0x03) FX_SEEK_BEGIN belirtilirse, arama işlemi dosyanın başından itibaren gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1725">FX_SEEK_BACK (0x03) If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="8ac81-1726">Bir FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1726">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="8ac81-1727">Bu FX_SEEK_FORWARD, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1727">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="8ac81-1728">Bu FX_SEEK_BACK, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1728">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1729">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1729">Return Values</span></span>

- <span data-ttu-id="8ac81-1730">**FX_SUCCESS** (0x00) Başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1730">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="8ac81-1731">**FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1731">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-1732">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1732">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1733">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1733">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1734">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1734">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1735">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1735">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1736">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1736">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-1737">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1737">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1738">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1738">Allowed From</span></span>

<span data-ttu-id="8ac81-1739">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1740">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1740">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1741">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1741">See Also</span></span>

- <span data-ttu-id="8ac81-1742">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1742">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1743">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1743">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1744">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1744">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1745">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1745">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1746">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1746">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1747">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1747">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1748">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1748">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1749">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1749">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1750">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1750">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1751">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1751">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1752">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1752">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1753">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1753">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1754">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1754">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1755">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1755">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1756">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1756">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1757">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1757">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1758">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1758">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1759">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1759">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1760">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1760">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1761">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1761">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1762">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1762">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1763">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1763">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1764">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1764">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1765">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1765">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1766">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1766">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1767">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1767">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_seek"></a><span data-ttu-id="8ac81-1768">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1768">fx_file_extended_seek</span></span>

<span data-ttu-id="8ac81-1769">Byte uzaklığına konumlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-1769">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1770">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1770">Prototype</span></span>

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a><span data-ttu-id="8ac81-1771">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1771">Description</span></span>

<span data-ttu-id="8ac81-1772">Bu hizmet, dahili dosya okuma/yazma işaretçisini belirtilen byte uzaklığına konumlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1772">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="8ac81-1773">Sonraki herhangi bir dosya okuma veya yazma isteği, dosyada bu konumda başlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1773">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="8ac81-1774">Bu hizmet exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1774">This service is designed for exFAT.</span></span> <span data-ttu-id="8ac81-1775">Byte_offset  parametresi, çağıranın okuma/yazma işaretçisini 4 GB aralığının ötesinde yeniden konumlandırması için 64 bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1775">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1776">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1776">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1777">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1777">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-1778">**byte_offset:** Dosyada istenen bayt uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1778">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="8ac81-1779">Sıfır değeri dosyanın başına okuma/yazma işaretçisini, dosyanın boyutundan büyük bir değer ise dosyanın sonuna okuma/yazma işaretçisini konumlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1779">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1780">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1780">Return Values</span></span>

- <span data-ttu-id="8ac81-1781">**FX_SUCCESS** (0x00) Başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1781">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="8ac81-1782">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1782">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8ac81-1783">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1783">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1784">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1784">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1785">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1785">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1786">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1786">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1787">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1787">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-1788">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1788">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1789">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1789">Allowed From</span></span>

<span data-ttu-id="8ac81-1790">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1790">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1791">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1791">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1792">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1792">See Also</span></span>

- <span data-ttu-id="8ac81-1793">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1793">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1794">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1794">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1795">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1795">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1796">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1796">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1797">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1797">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1798">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1798">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1799">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1799">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1800">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1800">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1801">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1801">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1802">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1802">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1803">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1803">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1804">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1804">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1805">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1805">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1806">fx_file_open- fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1806">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="8ac81-1807">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1807">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1808">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1808">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1809">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1809">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1810">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1810">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1811">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1811">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1812">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1812">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1813">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1813">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1814">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1814">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1815">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1815">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1816">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1816">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1817">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1817">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate"></a><span data-ttu-id="8ac81-1818">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1818">fx_file_extended_truncate</span></span>

<span data-ttu-id="8ac81-1819">Dosyanın kesilmesi</span><span class="sxs-lookup"><span data-stu-id="8ac81-1819">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1820">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1820">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="8ac81-1821">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1821">Description</span></span>

<span data-ttu-id="8ac81-1822">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar kısaltır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1822">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8ac81-1823">Sağlanan boyut gerçek dosya boyutundan büyükse bu hizmet herhangi bir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1823">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="8ac81-1824">Dosyayla ilişkili medya kümelerinin hiçbiri yayımlenmez.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1824">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-1825">*Aynı anda okuma için açık olan dosyaları kesme konusunda dikkatli olun. Ayrıca okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1825">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8ac81-1826">Bu hizmet exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1826">This service is designed for exFAT.</span></span> <span data-ttu-id="8ac81-1827">Size *parametresi,* çağıranın 4 GB'ın ötesinde çalışmasına olanak sağlayan 64 bit tamsayı değerini alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1827">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1828">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1828">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1829">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1829">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-1830">**size:** Yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1830">**size**: New file size.</span></span> <span data-ttu-id="8ac81-1831">Bu yeni dosya boyutunu geçen baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1831">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1832">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1832">Return Values</span></span>

- <span data-ttu-id="8ac81-1833">**FX_SUCCESS** (0x00) Başarılı dosya kesme.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1833">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8ac81-1834">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1834">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8ac81-1835">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1835">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-1836">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1836">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1837">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1837">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1838">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1838">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1839">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1839">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1840">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1840">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1841">**FX_WRITE_PROTECT** (0x23) Temel alınan medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1841">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8ac81-1842">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1842">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-1843">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1843">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1844">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1844">Allowed From</span></span>

<span data-ttu-id="8ac81-1845">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1845">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1846">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1846">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1847">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1847">See Also</span></span>

- <span data-ttu-id="8ac81-1848">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1848">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1849">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1849">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1850">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1850">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1851">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1851">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1852">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1852">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1853">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1853">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1854">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1854">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1855">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1855">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1856">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1856">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1857">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1857">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1858">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1858">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1859">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1859">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1860">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1860">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1861">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1861">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1862">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1862">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1863">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1863">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1864">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1864">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1865">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1865">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1866">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1866">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1867">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1867">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1868">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1868">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1869">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1869">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1870">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1870">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1871">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1871">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1872">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1872">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1873">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1873">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate_release"></a><span data-ttu-id="8ac81-1874">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1874">fx_file_extended_truncate_release</span></span>

<span data-ttu-id="8ac81-1875">Dosya ve yayın kümelerini keser</span><span class="sxs-lookup"><span data-stu-id="8ac81-1875">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1876">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1876">Prototype</span></span>

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a><span data-ttu-id="8ac81-1877">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1877">Description</span></span>

<span data-ttu-id="8ac81-1878">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar kısaltır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1878">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8ac81-1879">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet herhangi bir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1879">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="8ac81-1880">Bu ***hizmet fx_file_extended_truncate*** kullanılmayan kümeleri serbest bırakmaz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1880">Unlike the ***fx_file_extended_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-1881">*Aynı anda okuma için açık olan dosyaları kesme konusunda dikkatli olun. Ayrıca okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1881">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8ac81-1882">Bu hizmet exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1882">This service is designed for exFAT.</span></span> <span data-ttu-id="8ac81-1883">Size *parametresi,* çağıranın 4 GB'ın ötesinde çalışmasına olanak sağlayan 64 bit tamsayı değerini alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1883">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1884">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1884">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1885">**file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1885">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-1886">**size:** Yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1886">**size**: New file size.</span></span> <span data-ttu-id="8ac81-1887">Bu yeni dosya boyutunu geçen baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1887">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1888">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1888">Return Values</span></span>

- <span data-ttu-id="8ac81-1889">**FX_SUCCESS** (0x00) Başarılı dosya kesme.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1889">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8ac81-1890">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1890">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-1891">**FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1891">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-1892">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1892">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1893">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1893">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-1894">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1894">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1895">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1895">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-1896">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1896">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1897">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1897">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1898">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1898">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-1899">**FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1899">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-1900">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1900">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1901">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1901">Allowed From</span></span>

<span data-ttu-id="8ac81-1902">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1902">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1903">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1903">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1904">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1904">See Also</span></span>

- <span data-ttu-id="8ac81-1905">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1905">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1906">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1906">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1907">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1907">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1908">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1908">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1909">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-1909">fx_file_close</span></span>
- <span data-ttu-id="8ac81-1910">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1910">fx_file_create</span></span>
- <span data-ttu-id="8ac81-1911">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1911">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1912">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1912">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1913">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1913">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1914">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1914">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1915">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1915">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1916">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1916">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1917">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1917">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1918">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1918">fx_file_open</span></span>
- <span data-ttu-id="8ac81-1919">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1919">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1920">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1920">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1921">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1921">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1922">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1922">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1923">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1923">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1924">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1924">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1925">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1925">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1926">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1926">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1927">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1927">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1928">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1928">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1929">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1929">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1930">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1930">fx_unicode_short_name_get</span></span>

## <a name="fx_file_open"></a><span data-ttu-id="8ac81-1931">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-1931">fx_file_open</span></span>

<span data-ttu-id="8ac81-1932">Dosyayı açar</span><span class="sxs-lookup"><span data-stu-id="8ac81-1932">Opens file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1933">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1933">Prototype</span></span>

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a><span data-ttu-id="8ac81-1934">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1934">Description</span></span>

<span data-ttu-id="8ac81-1935">Bu hizmet, belirtilen dosyayı okuma ya da yazma için açar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1935">This service opens the specified file for either reading or writing.</span></span> <span data-ttu-id="8ac81-1936">Bir dosya birden çok kez okumak için açılabilir, ancak bir dosya yalnızca yazıcı dosyayı kapatana kadar bir kez yazmak üzere açılabilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1936">A file may be opened for reading multiple times, while a file can only be opened for writing once until the writer closes the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-1937">*Dosya okuma ve yazma için eşzamanlı olarak açıksa dikkatli olunmalıdır. Bir dosya okuma için eşzamanlı olarak açıldığında gerçekleştirilen dosya yazma işlemi, okuyucu kapanmadığı ve dosyayı okumak üzere yeniden açtığından, okuyucu tarafından görülemeyebilir. Benzer şekilde, dosya Truncate Services kullanılırken dosya yazıcısı dikkatli olmalıdır. Bir dosya yazıcı tarafından kesilmişse, aynı dosyanın okuyucuları geçersiz veri döndürebilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-1937">*Care must be taken if a file is concurrently open for reading and writing. File writing performed when a file is simultaneously opened for reading may not be seen by the reader, unless the reader closes and reopens the file for reading. Similarly, the file writer should be careful when using file truncate services. If a file is truncated by the writer, readers of the same file could return invalid data.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-1938">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1938">Input Parameters</span></span>

- <span data-ttu-id="8ac81-1939">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1939">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-1940">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1940">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-1941">**file_name**: açılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-1941">**file_name**: Pointer to the name of the file to open (directory path is optional).</span></span>
- <span data-ttu-id="8ac81-1942">**open_type**: dosya açma türü.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1942">**open_type**: Type of file open.</span></span> <span data-ttu-id="8ac81-1943">Geçerli açık tür seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-1943">Valid open type options are:</span></span>
  - <span data-ttu-id="8ac81-1944">FX_OPEN_FOR_READ (0x00)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1944">FX_OPEN_FOR_READ (0x00)</span></span>
  - <span data-ttu-id="8ac81-1945">FX_OPEN_FOR_WRITE (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1945">FX_OPEN_FOR_WRITE (0x01)</span></span>
  - <span data-ttu-id="8ac81-1946">FX_OPEN_FOR_READ_FAST (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-1946">FX_OPEN_FOR_READ_FAST (0x02)</span></span>

<span data-ttu-id="8ac81-1947">FX_OPEN_FOR_READ ve FX_OPEN_FOR_READ_FAST dosyaları açmak benzerdir:</span><span class="sxs-lookup"><span data-stu-id="8ac81-1947">Opening files with FX_OPEN_FOR_READ and FX_OPEN_FOR_READ_FAST is similar:</span></span>

- <span data-ttu-id="8ac81-1948">FX_OPEN_FOR_READ, dosyayı oluşturan kümelerin bağlı listesinin bozulmamış olduğunu ve FX_OPEN_FOR_READ_FAST Bu doğrulamayı gerçekleştirmediğinden daha hızlı hale gelmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1948">FX_OPEN_FOR_READ includes verification that the linked-list of clusters that comprise the file are intact, and FX_OPEN_FOR_READ_FAST does not perform this verification, which makes it faster.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-1949">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-1949">Return Values</span></span>

- <span data-ttu-id="8ac81-1950">**FX_SUCCESS** (0x00) başarılı dosya açıldı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1950">**FX_SUCCESS** (0x00) Successful file open.</span></span>
- <span data-ttu-id="8ac81-1951">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1951">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-1952">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1952">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="8ac81-1953">**FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1953">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="8ac81-1954">**FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve açma başarısız.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1954">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the open failed.</span></span>
- <span data-ttu-id="8ac81-1955">**FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık veya açma türü geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1955">**FX_ACCESS_ERROR** (0x06) Specified file is already open or open type is invalid.</span></span>
- <span data-ttu-id="8ac81-1956">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1956">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-1957">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1957">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8ac81-1958">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1958">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-1959">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-1959">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-1960">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1960">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-1961">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1961">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8ac81-1962">**FX_PTR_ERROR** (0x18) geçersiz medya veya dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1962">**FX_PTR_ERROR** (0x18) Invalid media or file pointer.</span></span>
- <span data-ttu-id="8ac81-1963">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1963">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-1964">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-1964">Allowed From</span></span>

<span data-ttu-id="8ac81-1965">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-1965">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-1966">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1966">Example</span></span>

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-1967">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1967">See Also</span></span>

- <span data-ttu-id="8ac81-1968">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1968">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-1969">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1969">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-1970">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1970">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-1971">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1971">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1972">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1972">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="8ac81-1973">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1973">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-1974">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-1974">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-1975">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1975">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-1976">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1976">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-1977">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1977">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-1978">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1978">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-1979">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1979">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-1980">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1980">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-1981">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1981">fx_file_read</span></span>
- <span data-ttu-id="8ac81-1982">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1982">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-1983">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1983">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-1984">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-1984">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-1985">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-1985">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-1986">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-1986">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-1987">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-1987">fx_file_write</span></span>
- <span data-ttu-id="8ac81-1988">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-1988">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-1989">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-1989">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-1990">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-1990">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-1991">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1991">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-1992">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-1992">fx_unicode_short_name_get</span></span>

## <a name="fx_file_read"></a><span data-ttu-id="8ac81-1993">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-1993">fx_file_read</span></span>

<span data-ttu-id="8ac81-1994">Dosyadan bayt okur</span><span class="sxs-lookup"><span data-stu-id="8ac81-1994">Reads bytes from file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-1995">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-1995">Prototype</span></span>

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a><span data-ttu-id="8ac81-1996">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-1996">Description</span></span>

<span data-ttu-id="8ac81-1997">Bu hizmet, dosyadaki baytları okur ve bunları sağlanan arabellekte depolar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1997">This service reads bytes from the file and stores them in the supplied buffer.</span></span> <span data-ttu-id="8ac81-1998">Okuma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1998">After the read is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span> <span data-ttu-id="8ac81-1999">İstekte daha az bayt kaldığında, yalnızca kalan baytlar arabellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-1999">If there are fewer bytes remaining in the request, only the bytes remaining are stored in the buffer.</span></span> <span data-ttu-id="8ac81-2000">Herhangi bir durumda, arabelleğe yerleştirilmiş baytların toplam sayısı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2000">In any case, the total number of bytes placed in the buffer is returned to the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2001">*Uygulama, sağlanan arabelleğin belirtilen sayıda istenen baytı depolayabilmesini sağlamalıdır.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2001">*The application must ensure that the buffer supplied is able to store the specified number of requested bytes.*</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2002">*Hedef arabellek uzun bir sözcüklük sınırındayken ve istenen boyut sizeof (**ulong**) tarafından eşit olarak bölünediyse daha hızlı performans elde edilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2002">*Faster performance is achieved if the destination buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2003">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2003">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2004">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2004">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-2005">**buffer_ptr**: okuma için hedef arabelleğe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2005">**buffer_ptr**: Pointer to the destination buffer for the read.</span></span>
- <span data-ttu-id="8ac81-2006">**request_size**: okunacak en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2006">**request_size**: Maximum number of bytes to read.</span></span>
- <span data-ttu-id="8ac81-2007">**actual_size**: sağlanan arabelleğe okunan gerçek bayt sayısını tutacak değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2007">**actual_size**: Pointer to the variable to hold the actual number of bytes read into the supplied buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2008">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2008">Return Values</span></span>

- <span data-ttu-id="8ac81-2009">**FX_SUCCESS** (0x00) başarılı dosya okundu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2009">**FX_SUCCESS** (0x00) Successful file read.</span></span>
- <span data-ttu-id="8ac81-2010">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2010">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8ac81-2011">**FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve okuma başarısız.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2011">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the read failed.</span></span>
- <span data-ttu-id="8ac81-2012">**FX_END_OF_FILE** (0x09) dosya sonuna ulaşıldı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2012">**FX_END_OF_FILE** (0x09) End of file has been reached.</span></span>
- <span data-ttu-id="8ac81-2013">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2013">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2014">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-2014">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-2015">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2015">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2016">**FX_PTR_ERROR** (0x18) geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2016">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="8ac81-2017">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2017">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2018">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2018">Allowed From</span></span>

<span data-ttu-id="8ac81-2019">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2019">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2020">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2020">Example</span></span>

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
### <a name="see-also"></a><span data-ttu-id="8ac81-2021">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2021">See Also</span></span>

- <span data-ttu-id="8ac81-2022">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2022">fx_file_allocate,</span></span>
- <span data-ttu-id="8ac81-2023">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2023">fx_file_attributes_read,</span></span>
- <span data-ttu-id="8ac81-2024">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2024">fx_file_attributes_set,</span></span>
- <span data-ttu-id="8ac81-2025">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2025">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="8ac81-2026">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2026">fx_file_close,</span></span>
- <span data-ttu-id="8ac81-2027">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2027">fx_file_create,</span></span>
- <span data-ttu-id="8ac81-2028">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2028">fx_file_date_time_set,</span></span>
- <span data-ttu-id="8ac81-2029">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2029">fx_file_delete,</span></span>
- <span data-ttu-id="8ac81-2030">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2030">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="8ac81-2031">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2031">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="8ac81-2032">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2032">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="8ac81-2033">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2033">fx_file_extended_seek,</span></span>
- <span data-ttu-id="8ac81-2034">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2034">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="8ac81-2035">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2035">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="8ac81-2036">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2036">fx_file_open,</span></span>
- <span data-ttu-id="8ac81-2037">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2037">fx_file_relative_seek,</span></span>
- <span data-ttu-id="8ac81-2038">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2038">fx_file_rename,</span></span>
- <span data-ttu-id="8ac81-2039">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2039">fx_file_seek,</span></span>
- <span data-ttu-id="8ac81-2040">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2040">fx_file_truncate,</span></span>
- <span data-ttu-id="8ac81-2041">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2041">fx_file_truncate_release,</span></span>
- <span data-ttu-id="8ac81-2042">fx_file_write,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2042">fx_file_write,</span></span>
- <span data-ttu-id="8ac81-2043">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2043">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="8ac81-2044">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2044">fx_unicode_file_create,</span></span>
- <span data-ttu-id="8ac81-2045">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2045">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="8ac81-2046">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2046">fx_unicode_name_get,</span></span>
- <span data-ttu-id="8ac81-2047">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2047">fx_unicode_short_name_get</span></span>

## <a name="fx_file_relative_seek"></a><span data-ttu-id="8ac81-2048">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2048">fx_file_relative_seek</span></span>

<span data-ttu-id="8ac81-2049">Göreli bayt uzaklığına pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-2049">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2050">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2050">Prototype</span></span>

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="8ac81-2051">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2051">Description</span></span>

<span data-ttu-id="8ac81-2052">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2052">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="8ac81-2053">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2053">Any subsequent file read or write request will begin at this location in the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-2054">*Arama işlemi dosyanın sonundan sonra arama yapmayı denerse, dosyanın okuma/yazma işaretçisi dosyanın sonuna yerleştirilir. Buna karşılık, arama işlemi dosyanın başlangıcını aşan konuma çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başlangıcına yerleştirilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2054">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

<span data-ttu-id="8ac81-2055">4 GB 'ın ötesinde bir fark değeri ile arama yapmak için, uygulama Service *fx_file_extended_relative_seek* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2055">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_relative_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2056">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2056">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2057">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2057">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-2058">**byte_offset**: dosyada istenen göreli bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2058">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="8ac81-2059">**seek_from**: göreli arama yapılacak yönün yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2059">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="8ac81-2060">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-2060">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="8ac81-2061">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2061">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="8ac81-2062">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2062">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="8ac81-2063">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2063">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="8ac81-2064">FX_SEEK_BACK (0x03)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2064">FX_SEEK_BACK (0x03)</span></span>

<span data-ttu-id="8ac81-2065">FX_SEEK_BEGIN belirtilirse, arama işlemi dosyanın başından yapılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2065">If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="8ac81-2066">FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2066">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="8ac81-2067">FX_SEEK_FORWARD belirtilirse, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2067">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="8ac81-2068">FX_SEEK_BACK belirtilirse, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2068">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2069">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2069">Return Values</span></span>

- <span data-ttu-id="8ac81-2070">**FX_SUCCESS** (0x00) başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2070">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="8ac81-2071">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2071">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-2072">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2072">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2073">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2074">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2075">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2075">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-2076">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2076">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-2077">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2077">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2078">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2078">Allowed From</span></span>

<span data-ttu-id="8ac81-2079">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2079">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2080">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2080">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-2081">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2081">See Also</span></span>

- <span data-ttu-id="8ac81-2082">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2082">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-2083">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2083">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-2084">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2084">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-2085">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2085">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2086">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2086">fx_file_close</span></span>
- <span data-ttu-id="8ac81-2087">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2087">fx_file_create</span></span>
- <span data-ttu-id="8ac81-2088">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2088">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-2089">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-2089">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-2090">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2090">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-2091">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2091">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2092">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2092">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-2093">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2093">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-2094">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2094">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-2095">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2095">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-2096">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2096">fx_file_open</span></span>
- <span data-ttu-id="8ac81-2097">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2097">fx_file_read</span></span>
- <span data-ttu-id="8ac81-2098">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2098">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-2099">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2099">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-2100">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2100">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-2101">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2101">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-2102">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2102">fx_file_write</span></span>
- <span data-ttu-id="8ac81-2103">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2103">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-2104">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2104">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-2105">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2105">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-2106">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2106">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-2107">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2107">fx_unicode_short_name_get</span></span>

## <a name="fx_file_rename"></a><span data-ttu-id="8ac81-2108">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2108">fx_file_rename</span></span>

<span data-ttu-id="8ac81-2109">Dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="8ac81-2109">Renames  file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2110">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2110">Prototype</span></span>

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-2111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2111">Description</span></span>

<span data-ttu-id="8ac81-2112">Bu hizmet *old_file_name* tarafından belirtilen dosyanın adını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2112">This service changes the name of the file specified by *old_file_name*.</span></span> <span data-ttu-id="8ac81-2113">Yeniden adlandırma işlemi, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2113">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="8ac81-2114">Yeni dosya adında bir yol belirtilmişse, yeniden adlandırılan dosya belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2114">If a path is specified in the new file name, the renamed file is effectively moved to the specified path.</span></span> <span data-ttu-id="8ac81-2115">Hiçbir yol belirtilmemişse, yeniden adlandırılan dosya geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2115">If no path is specified, the renamed file is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2116">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2116">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2117">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2117">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8ac81-2118">**old_file_name**: yeniden adlandırılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8ac81-2118">**old_file_name**: Pointer to the name of the file to rename (directory path is optional).</span></span>
- <span data-ttu-id="8ac81-2119">**new_file_name**: yeni dosya adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2119">**new_file_name**: Pointer to the new file name.</span></span> <span data-ttu-id="8ac81-2120">Dizin yoluna izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2120">The directory path is not allowed.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2121">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2121">Return Values</span></span>

- <span data-ttu-id="8ac81-2122">**FX_SUCCESS** (0x00) başarılı dosya yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2122">**FX_SUCCESS** (0x00) Successful file rename.</span></span>
- <span data-ttu-id="8ac81-2123">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2123">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2124">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2124">**FX_NOT_FOUND** (0x04)    Specified file was not found.</span></span>
- <span data-ttu-id="8ac81-2125">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2125">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="8ac81-2126">**FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2126">**FX_ACCESS_ERROR** (0x06) Specified file is already open.</span></span>
- <span data-ttu-id="8ac81-2127">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2127">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2128">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2128">**FX_WRITE_PROTECT** (0x23)    Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-2129">**FX_INVALID_NAME** (0x0C) belirtilen yeni dosya adı geçerli bir dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2129">**FX_INVALID_NAME** (0x0C) Specified new file name is not a valid file name.</span></span>
- <span data-ttu-id="8ac81-2130">**FX_INVALID_PATH** (0x0D) yolu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2130">**FX_INVALID_PATH** (0x0D)    Path is invalid.</span></span>
- <span data-ttu-id="8ac81-2131">**FX_ALREADY_CREATED** (0x0B) yeni dosya adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2131">**FX_ALREADY_CREATED** (0x0B) The new file name is used.</span></span>
- <span data-ttu-id="8ac81-2132">**FX_MEDIA_INVALID** (0x02) medyası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2132">**FX_MEDIA_INVALID** (0x02)    Media is invalid.</span></span>
- <span data-ttu-id="8ac81-2133">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2133">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2134">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2134">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2135">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2135">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-2136">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-2136">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-2137">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2137">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8ac81-2138">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2138">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-2139">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2139">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2140">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2140">Allowed From</span></span>

<span data-ttu-id="8ac81-2141">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2142">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2142">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-2143">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2143">See Also</span></span>

- <span data-ttu-id="8ac81-2144">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2144">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-2145">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2145">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-2146">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2146">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-2147">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2147">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2148">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2148">fx_file_close</span></span>
- <span data-ttu-id="8ac81-2149">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2149">fx_file_create</span></span>
- <span data-ttu-id="8ac81-2150">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2150">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-2151">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-2151">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-2152">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2152">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-2153">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2153">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2154">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2154">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-2155">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2155">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-2156">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2156">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-2157">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2157">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-2158">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2158">fx_file_open</span></span>
- <span data-ttu-id="8ac81-2159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2159">fx_file_read</span></span>
- <span data-ttu-id="8ac81-2160">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2160">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-2161">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2161">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-2162">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2162">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-2163">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2163">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-2164">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2164">fx_file_write</span></span>
- <span data-ttu-id="8ac81-2165">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2165">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-2166">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2166">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-2167">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2167">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-2168">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2168">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-2169">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2169">fx_unicode_short_name_get</span></span>

## <a name="fx_file_seek"></a><span data-ttu-id="8ac81-2170">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2170">fx_file_seek</span></span>

<span data-ttu-id="8ac81-2171">Bayt uzaklığa pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-2171">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2172">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2172">Prototype</span></span>

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a><span data-ttu-id="8ac81-2173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2173">Description</span></span>

<span data-ttu-id="8ac81-2174">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen bayt uzaklığa konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2174">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="8ac81-2175">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2175">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="8ac81-2176">4 GB 'ın ötesinde bir fark değeri ile arama yapmak için, uygulama Service *fx_file_extended_seek* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2176">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2177">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2177">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2178">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2178">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-2179">**byte_offset**: dosyada istenen bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2179">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="8ac81-2180">Sıfır değeri, dosyanın başındaki okuma/yazma işaretçisini konumlandırır, ancak dosyanın boyutundan büyük bir değer, dosyanın sonundaki okuma/yazma işaretçisini konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2180">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2181">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2181">Return Values</span></span>

- <span data-ttu-id="8ac81-2182">**FX_SUCCESS** (0x00) başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2182">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="8ac81-2183">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2183">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8ac81-2184">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2184">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2185">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2185">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2186">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2186">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2187">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-2187">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-2188">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2188">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-2189">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2190">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2190">Allowed From</span></span>

<span data-ttu-id="8ac81-2191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2192">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2192">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-2193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2193">See Also</span></span>

- <span data-ttu-id="8ac81-2194">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2194">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-2195">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2195">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-2196">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2196">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-2197">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2197">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2198">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2198">fx_file_close</span></span>
- <span data-ttu-id="8ac81-2199">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2199">fx_file_create</span></span>
- <span data-ttu-id="8ac81-2200">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2200">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-2201">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-2201">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-2202">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2202">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-2203">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2203">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2204">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2204">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-2205">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2205">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-2206">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2206">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-2207">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2207">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-2208">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2208">fx_file_open</span></span>
- <span data-ttu-id="8ac81-2209">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2209">fx_file_read</span></span>
- <span data-ttu-id="8ac81-2210">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2210">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-2211">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2211">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-2212">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2212">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-2213">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2213">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-2214">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2214">fx_file_write</span></span>
- <span data-ttu-id="8ac81-2215">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2215">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-2216">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2216">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-2217">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2217">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-2218">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2218">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-2219">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2219">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate"></a><span data-ttu-id="8ac81-2220">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2220">fx_file_truncate</span></span>

<span data-ttu-id="8ac81-2221">Dosya keser</span><span class="sxs-lookup"><span data-stu-id="8ac81-2221">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2222">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2222">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="8ac81-2223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2223">Description</span></span>

<span data-ttu-id="8ac81-2224">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2224">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8ac81-2225">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2225">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="8ac81-2226">Dosyayla ilişkili medya kümelerinin hiçbiri serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2226">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2227">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2227">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8ac81-2228">4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2228">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2229">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2229">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2230">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2230">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-2231">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2231">**size**: New file size.</span></span> <span data-ttu-id="8ac81-2232">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2232">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2233">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2233">Return Values</span></span>

- <span data-ttu-id="8ac81-2234">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2234">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8ac81-2235">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2235">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8ac81-2236">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2236">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-2237">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2237">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2238">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2238">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-2239">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2239">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2240">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2240">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2241">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2241">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-2242">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8ac81-2242">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8ac81-2243">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2243">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-2244">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2244">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2245">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2245">Allowed From</span></span>

<span data-ttu-id="8ac81-2246">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2247">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2247">Example</span></span>

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-2248">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2248">See Also</span></span>

- <span data-ttu-id="8ac81-2249">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2249">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-2250">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2250">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-2251">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2251">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-2252">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2252">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2253">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2253">fx_file_close</span></span>
- <span data-ttu-id="8ac81-2254">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2254">fx_file_create</span></span>
- <span data-ttu-id="8ac81-2255">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2255">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-2256">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-2256">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-2257">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2257">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-2258">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2258">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2259">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2259">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-2260">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2260">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-2261">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2261">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-2262">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2262">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-2263">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2263">fx_file_open</span></span>
- <span data-ttu-id="8ac81-2264">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2264">fx_file_read</span></span>
- <span data-ttu-id="8ac81-2265">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2265">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-2266">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2266">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-2267">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2267">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-2268">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2268">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-2269">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2269">fx_file_write</span></span>
- <span data-ttu-id="8ac81-2270">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2270">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-2271">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2271">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-2272">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2272">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-2273">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2273">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-2274">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2274">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate_release"></a><span data-ttu-id="8ac81-2275">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2275">fx_file_truncate_release</span></span>

<span data-ttu-id="8ac81-2276">Dosya ve yayınlar kümesi keser</span><span class="sxs-lookup"><span data-stu-id="8ac81-2276">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2277">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2277">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="8ac81-2278">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2278">Description</span></span>

<span data-ttu-id="8ac81-2279">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2279">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8ac81-2280">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2280">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="8ac81-2281">***Fx_file_truncate*** hizmetinden farklı olarak, bu hizmet kullanılmayan kümeleri serbest bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2281">Unlike the ***fx_file_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2282">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2282">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8ac81-2283">4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate_release* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2283">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate_release*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2284">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2284">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2285">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2285">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8ac81-2286">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2286">**size**: New file size.</span></span> <span data-ttu-id="8ac81-2287">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2287">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2288">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2288">Return Values</span></span>

- <span data-ttu-id="8ac81-2289">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2289">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8ac81-2290">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2290">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-2291">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2291">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8ac81-2292">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2292">**FX_IO_ERROR** (0x90)    Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2293">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2293">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8ac81-2294">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2294">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2295">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2295">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2296">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2296">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-2297">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2297">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-2298">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2298">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation.</span></span>
- <span data-ttu-id="8ac81-2299">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2299">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8ac81-2300">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2300">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2301">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2301">Allowed From</span></span>

<span data-ttu-id="8ac81-2302">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2303">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2303">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a><span data-ttu-id="8ac81-2304">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2304">See Also</span></span>

- <span data-ttu-id="8ac81-2305">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2305">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-2306">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2306">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-2307">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2307">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-2308">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2308">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2309">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2309">fx_file_close</span></span>
- <span data-ttu-id="8ac81-2310">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2310">fx_file_create</span></span>
- <span data-ttu-id="8ac81-2311">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2311">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-2312">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-2312">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-2313">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2313">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-2314">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2314">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2315">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2315">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-2316">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2316">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-2317">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2317">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-2318">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2318">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-2319">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2319">fx_file_open</span></span>
- <span data-ttu-id="8ac81-2320">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2320">fx_file_read</span></span>
- <span data-ttu-id="8ac81-2321">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2321">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-2322">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2322">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-2323">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2323">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-2324">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2324">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-2325">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2325">fx_file_write</span></span>
- <span data-ttu-id="8ac81-2326">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2326">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-2327">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2327">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-2328">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2328">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-2329">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2329">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-2330">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2330">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write"></a><span data-ttu-id="8ac81-2331">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2331">fx_file_write</span></span>

<span data-ttu-id="8ac81-2332">Dosyaya bayt yazar</span><span class="sxs-lookup"><span data-stu-id="8ac81-2332">Writes bytes to file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2333">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2333">Prototype</span></span>

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="8ac81-2334">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2334">Description</span></span>

<span data-ttu-id="8ac81-2335">Bu hizmet, dosyanın geçerli konumundan başlayarak belirtilen arabellekten baytlar yazar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2335">This service writes bytes from the specified buffer starting at the file's current position.</span></span> <span data-ttu-id="8ac81-2336">Yazma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyada bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2336">After the write is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2337">*Kaynak arabelleği uzun sözcük sınırında ise ve istenen boyut sizeof( ULONG ) ile bölünebilirse daha hızlı performans elde **edilir.***</span><span class="sxs-lookup"><span data-stu-id="8ac81-2337">*Faster performance is achieved if the source buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2338">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2338">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2339">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2339">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-2340">**buffer_ptr:** Yazma için kaynak arabelleğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2340">**buffer_ptr**: Pointer to the source buffer for the write.</span></span>
- <span data-ttu-id="8ac81-2341">**boyut:** Yazacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2341">**size**: Number of bytes to write.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2342">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2342">Return Values</span></span>

- <span data-ttu-id="8ac81-2343">**FX_SUCCESS** (0x00) Başarılı dosya yazma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2343">**FX_SUCCESS** (0x00) Successful file write.</span></span>
- <span data-ttu-id="8ac81-2344">**FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2344">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8ac81-2345">**FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2345">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8ac81-2346">**FX_NO_MORE_SPACE** (0x0A) Bu yazma işlemini gerçekleştirmek için medyada yer yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2346">**FX_NO_MORE_SPACE** (0x0A) There is no more room available in the media to perform this write.</span></span>
- <span data-ttu-id="8ac81-2347">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2347">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2348">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2348">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-2349">**FX_FILE_CORRUPT** (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2349">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2350">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2350">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2351">**FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2351">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8ac81-2352">**FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2352">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8ac81-2353">**FX_PTR_ERROR** (0x18) Geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2353">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="8ac81-2354">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2354">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2355">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2355">Allowed From</span></span>

<span data-ttu-id="8ac81-2356">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2356">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2357">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2357">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-2358">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2358">See Also</span></span>

- <span data-ttu-id="8ac81-2359">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2359">fx_file_allocate,</span></span>
- <span data-ttu-id="8ac81-2360">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2360">fx_file_attributes_read,</span></span>
- <span data-ttu-id="8ac81-2361">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2361">fx_file_attributes_set,</span></span>
- <span data-ttu-id="8ac81-2362">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2362">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="8ac81-2363">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2363">fx_file_close,</span></span>
- <span data-ttu-id="8ac81-2364">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2364">fx_file_create,</span></span>
- <span data-ttu-id="8ac81-2365">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2365">fx_file_date_time_set,</span></span>
- <span data-ttu-id="8ac81-2366">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2366">fx_file_delete,</span></span>
- <span data-ttu-id="8ac81-2367">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2367">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="8ac81-2368">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2368">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="8ac81-2369">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2369">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="8ac81-2370">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2370">fx_file_extended_seek,</span></span>
- <span data-ttu-id="8ac81-2371">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2371">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="8ac81-2372">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2372">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="8ac81-2373">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2373">fx_file_open,</span></span>
- <span data-ttu-id="8ac81-2374">fx_file_read,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2374">fx_file_read,</span></span>
- <span data-ttu-id="8ac81-2375">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2375">fx_file_relative_seek,</span></span>
- <span data-ttu-id="8ac81-2376">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2376">fx_file_rename,</span></span>
- <span data-ttu-id="8ac81-2377">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2377">fx_file_seek,</span></span>
- <span data-ttu-id="8ac81-2378">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2378">fx_file_truncate,</span></span>
- <span data-ttu-id="8ac81-2379">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2379">fx_file_truncate_release,</span></span>
- <span data-ttu-id="8ac81-2380">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2380">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="8ac81-2381">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2381">fx_unicode_file_create,</span></span>
- <span data-ttu-id="8ac81-2382">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2382">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="8ac81-2383">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="8ac81-2383">fx_unicode_name_get,</span></span>
- <span data-ttu-id="8ac81-2384">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2384">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write_notify_set"></a><span data-ttu-id="8ac81-2385">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2385">fx_file_write_notify_set</span></span>

<span data-ttu-id="8ac81-2386">Dosya yazma notify işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-2386">Sets the file write notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2387">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2387">Prototype</span></span>

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a><span data-ttu-id="8ac81-2388">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2388">Description</span></span>

<span data-ttu-id="8ac81-2389">Bu hizmet, başarılı bir dosya yazma işlemi sonrasında çağrılan geri çağırma işlevini yüklür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2389">This service installs callback function that is invoked after a successful file write operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2390">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2390">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2391">**file_ptr:** Dosya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2391">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8ac81-2392">**file_write_notify:** Dosya yazma geri çağırma işlevi yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2392">**file_write_notify**: File write callback function to be installed.</span></span> <span data-ttu-id="8ac81-2393">Geri çağırma işlevini NULL olarak ayarlamak geri çağırma işlevini devre dışı bırakıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2393">Set the callback function to NULL disables the callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2394">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2394">Return Values</span></span>

- <span data-ttu-id="8ac81-2395">**FX_SUCCESS** (0x00) Geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2395">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="8ac81-2396">**FX_PTR_ERROR** (0x18) file_ptr NULL olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2396">**FX_PTR_ERROR** (0x18) file_ptr is NULL.</span></span>
- <span data-ttu-id="8ac81-2397">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2397">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2398">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2398">Allowed From</span></span>

<span data-ttu-id="8ac81-2399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2400">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2400">Example</span></span>

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2401">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2401">See Also</span></span>

- <span data-ttu-id="8ac81-2402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2402">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-2403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2403">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-2404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2404">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-2405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2406">fx_file_close</span></span>
- <span data-ttu-id="8ac81-2407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2407">fx_file_create</span></span>
- <span data-ttu-id="8ac81-2408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2408">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-2409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-2409">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-2410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-2411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-2412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-2413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2413">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-2414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-2415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-2416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2416">fx_file_open</span></span>
- <span data-ttu-id="8ac81-2417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2417">fx_file_read</span></span>
- <span data-ttu-id="8ac81-2418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2418">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-2419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2419">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-2420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2420">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-2421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2421">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-2422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-2422">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-2423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2423">fx_file_write</span></span>
- <span data-ttu-id="8ac81-2424">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-2424">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-2425">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-2425">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-2426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2426">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-2427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2427">fx_unicode_short_name_get</span></span>

## <a name="fx_media_abort"></a><span data-ttu-id="8ac81-2428">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2428">fx_media_abort</span></span>

<span data-ttu-id="8ac81-2429">Medya etkinliklerini iptal eder</span><span class="sxs-lookup"><span data-stu-id="8ac81-2429">Aborts media activities</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2430">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2430">Prototype</span></span>

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-2431">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2431">Description</span></span>

<span data-ttu-id="8ac81-2432">Bu hizmet, tüm açık dosyaları kapatma, ilişkili sürücüye bir durdurma isteği gönderme ve medyayı durdurulma durumuna yerleştirme de dahil olmak üzere medyayla ilişkili tüm geçerli etkinlikleri iptal eder.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2432">This service aborts all current activities associated with the media, including closing all open files, sending an abort request to the associated driver, and placing the media in an aborted state.</span></span> <span data-ttu-id="8ac81-2433">Bu hizmet genellikle, I/O hataları algılandığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2433">This service is typically called when I/O errors are detected.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2434">*Bir durdurma işlemi gerçekleştirildikten sonra medyanın yeniden kullanmak için yeniden açılması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2434">*The media must be re-opened to use it again after an abort operation is performed.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2435">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2435">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2436">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2436">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2437">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2437">Return Values</span></span>

- <span data-ttu-id="8ac81-2438">**FX_SUCCESS** (0x00) Başarılı medya durdurma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2438">**FX_SUCCESS** (0x00) Successful media abort.</span></span>
- <span data-ttu-id="8ac81-2439">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2439">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2440">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2440">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-2441">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2441">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2442">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2442">Allowed From</span></span>

<span data-ttu-id="8ac81-2443">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2444">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2444">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2445">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2445">See Also</span></span>

- <span data-ttu-id="8ac81-2446">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2446">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2447">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2447">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2448">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2448">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2449">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2449">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2450">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2450">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2451">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2451">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2452">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2452">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2453">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2453">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2454">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2454">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2455">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2455">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2456">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2456">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2457">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2457">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2458">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2458">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2459">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2459">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2460">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2460">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2461">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2461">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2462">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2462">fx_system_initialize</span></span>

## <a name="fx_media_cache_invalidate"></a><span data-ttu-id="8ac81-2463">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2463">fx_media_cache_invalidate</span></span>

<span data-ttu-id="8ac81-2464">Mantıksal kesim önbelleğini geçersiz kılın</span><span class="sxs-lookup"><span data-stu-id="8ac81-2464">Invalidates logical sector cache</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2465">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2465">Prototype</span></span>

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="8ac81-2466">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2466">Description</span></span>

<span data-ttu-id="8ac81-2467">Bu hizmet önbellekte tüm kirli kesimleri boşaltıyor ve ardından mantıksal kesim önbelleğinin tamamını geçersiz kılacak.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2467">This service flushes all dirty sectors in the cache and then invalidates the entire logical sector cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2468">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2468">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2469">**media_ptr:** Medya denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8ac81-2469">**media_ptr**: Pointer to media control block</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2470">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2470">Return Values</span></span>

- <span data-ttu-id="8ac81-2471">**FX_SUCCESS** (0x00) Başarılı medya önbelleği geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2471">**FX_SUCCESS** (0x00) Successful media cache invalidate.</span></span>
- <span data-ttu-id="8ac81-2472">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2472">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2473">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2473">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2474">**FX_PTR_ERROR** (0x18) Geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2474">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="8ac81-2475">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2475">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2476">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2476">Allowed From</span></span>

<span data-ttu-id="8ac81-2477">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2478">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2478">Example</span></span>

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2479">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2479">See Also</span></span>

- <span data-ttu-id="8ac81-2480">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2480">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2481">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2481">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2482">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2482">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2483">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2483">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2484">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2484">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2485">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2485">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2486">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2486">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2487">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2487">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2488">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2488">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2489">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2489">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2490">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2490">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2491">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2491">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2492">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2492">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2493">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2493">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2494">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2494">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2495">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2495">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2496">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2496">fx_system_initialize</span></span>

## <a name="fx_media_check"></a><span data-ttu-id="8ac81-2497">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2497">fx_media_check</span></span>

<span data-ttu-id="8ac81-2498">Medyada hataları denetler</span><span class="sxs-lookup"><span data-stu-id="8ac81-2498">Checks media for errors</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2499">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2499">Prototype</span></span>

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-2500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2500">Description</span></span>

<span data-ttu-id="8ac81-2501">Bu hizmet, dosya/dizin çapraz bağlantı, geçersiz FAT zincirleri ve kayıp kümeler dahil olmak üzere temel yapısal hatalar için belirtilen medyayı denetler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2501">This service checks the specified media for basic structural errors, including file/directory cross-linking, invalid FAT chains, and lost clusters.</span></span> <span data-ttu-id="8ac81-2502">Bu hizmet, algılanan hataları düzeltme yeteneği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2502">This service also provides the capability to correct detected errors.</span></span>

<span data-ttu-id="8ac81-2503">Fx_media_check hizmeti, ortamdaki dizinlerin ve dosyaların derinlemesine ilk analizi için karalama belleği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2503">The fx_media_check service requires scratch memory for its depth-first analysis of directories and files in the media.</span></span> <span data-ttu-id="8ac81-2504">Özellikle, medya denetimi hizmeti için sağlanan karalama belleği, birkaç dizin girişi tutabilecek kadar büyük olmalıdır, alt dizinlere girmeden önce geçerli dizin girişi konumunu "Stack" e bir veri yapısı ve son olarak mantıksal FAT bit eşlem.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2504">Specifically, the scratch memory supplied to the media check service must be large enough to hold several directory entries, a data structure to "stack" the current directory entry position before entering into subdirectories, and finally the logical FAT bit map.</span></span> <span data-ttu-id="8ac81-2505">Boş bellek, medyada kümeler olduğundan çok sayıda bit olması gereken mantıksal FAT bit eşlem için en az 512-1024 bayt artı bellek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2505">The scratch memory should be at least 512-1024 bytes plus memory for the logical FAT bit map, which requires as many bits as there are clusters in the media.</span></span> <span data-ttu-id="8ac81-2506">Örneğin, 8000 kümesi olan bir cihaz için 1000 bayt ve bu nedenle 2048 bayt düzeninde toplam bir karalama alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2506">For example, a device with 8000 clusters would require 1000 bytes to represent and thus require a total scratch area on the order of 2048 bytes.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2507">*Bu hizmet yalnızca fx_media_open ve diğer herhangi bir dosya sistemi etkinliği olmadan hemen çağrılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2507">*This service should only be called immediately after fx_media_open and without any other file system activity.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2508">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2508">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2509">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2509">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-2510">**scratch_memory_ptr**: karalama belleğinin başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2510">**scratch_memory_ptr**: Pointer to the start of scratch memory.</span></span>
- <span data-ttu-id="8ac81-2511">**scratch_memory_size**: boş belleğin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2511">**scratch_memory_size**: Size of scratch memory in bytes.</span></span>
- <span data-ttu-id="8ac81-2512">**error_correction_option**: hata düzeltme seçeneği bitleri, bit ayarlandığında hata düzeltme gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2512">**error_correction_option**: Error correction option bits, when the bit is set, error correction is performed.</span></span> <span data-ttu-id="8ac81-2513">Hata düzeltme seçeneği bitleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-2513">The error correction option bits are defined as follows:</span></span>
  - <span data-ttu-id="8ac81-2514">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2514">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="8ac81-2515">FX_DIRECTORY_ERROR (0x02)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2515">FX_DIRECTORY_ERROR (0x02)</span></span>
  - <span data-ttu-id="8ac81-2516">Gerekli hata düzeltme seçeneklerini yalnızca bir arada FX_LOST_CLUSTER_ERROR (0x04).</span><span class="sxs-lookup"><span data-stu-id="8ac81-2516">FX_LOST_CLUSTER_ERROR (0x04) Simply OR together the required error correction options.</span></span> <span data-ttu-id="8ac81-2517">Hata düzeltmesi gerekmiyorsa 0 değeri sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2517">If no error correction is required, a value of 0 should be supplied.</span></span>
- <span data-ttu-id="8ac81-2518">**errors_detected_ptr**: aşağıda tanımlandığı şekilde hata algılama bitleri için hedef:</span><span class="sxs-lookup"><span data-stu-id="8ac81-2518">**errors_detected_ptr**: Destination for error detection bits, as defined below:</span></span>
  - <span data-ttu-id="8ac81-2519">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2519">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="8ac81-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span></span>
  - <span data-ttu-id="8ac81-2521">FX_FILE_SIZE_ERROR (0x08)</span><span class="sxs-lookup"><span data-stu-id="8ac81-2521">FX_FILE_SIZE_ERROR (0x08)</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2522">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2522">Return Values</span></span>

- <span data-ttu-id="8ac81-2523">**FX_SUCCESS** (0x00) başarılı medya denetimi, Ayrıntılar için algılanan hedef hatalarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2523">**FX_SUCCESS** (0x00) Successful media check, view the errors detected destination for details.</span></span>
- <span data-ttu-id="8ac81-2524">**FX_ACCESS_ERROR** (0x06) açık dosyalarla denetim yapılamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2524">**FX_ACCESS_ERROR** (0x06) Unable to perform check with open files.</span></span>
- <span data-ttu-id="8ac81-2525">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2525">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2526">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2526">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2527">**FX_NO_MORE_SPACE** (0x0A) medyada daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2527">**FX_NO_MORE_SPACE** (0x0A) No more space on the media.</span></span>
- <span data-ttu-id="8ac81-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) sağlanan karalama belleği yeterince büyük değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) Supplied scratch memory is not large enough.</span></span>
- <span data-ttu-id="8ac81-2529">**FX_ERROR_NOT_FIXED** (0x93) DÜZELTILMEYEN FAT32 kök dizininin bozulması.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2529">**FX_ERROR_NOT_FIXED** (0x93) Corruption of FAT32 root directory that could not be fixed.</span></span>
- <span data-ttu-id="8ac81-2530">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2531">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2531">**FX_SECTOR_INVALID** (0x89) Sector is invalid.</span></span>
- <span data-ttu-id="8ac81-2532">**FX_PTR_ERROR** (0x18) geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2532">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="8ac81-2533">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="8ac81-2534">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2534">Allowed From</span></span>

<span data-ttu-id="8ac81-2535">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2536">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2536">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-2537">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2537">See Also</span></span>

- <span data-ttu-id="8ac81-2538">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2538">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2539">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2539">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2540">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2540">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2541">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2541">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2542">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2542">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2543">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2543">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2544">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2544">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2545">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2545">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2546">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2546">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2547">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2547">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2548">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2548">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2549">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2549">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2550">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2550">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2551">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2551">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2552">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2552">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2553">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2553">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2554">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2554">fx_system_initialize</span></span>

## <a name="fx_media_close"></a><span data-ttu-id="8ac81-2555">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2555">fx_media_close</span></span>

<span data-ttu-id="8ac81-2556">Medyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="8ac81-2556">Closes media</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2557">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2557">Prototype</span></span>

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-2558">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2558">Description</span></span>

<span data-ttu-id="8ac81-2559">Bu hizmet, belirtilen medyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2559">This service closes the specified media.</span></span> <span data-ttu-id="8ac81-2560">Medyayı kapatma sürecinde, tüm açık dosyalar kapatılır ve kalan arabellekler fiziksel medyaya silinir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2560">In the process of closing the media, all open files are closed and any remaining buffers are flushed to the physical media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2561">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2561">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2562">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2562">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2563">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2563">Return Values</span></span>

- <span data-ttu-id="8ac81-2564">**FX_SUCCESS** (0x00) başarılı medya kapatma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2564">**FX_SUCCESS** (0x00) Successful media close.</span></span>
- <span data-ttu-id="8ac81-2565">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2565">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2566">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2566">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2567">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2567">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-2568">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2568">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2569">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2569">Allowed From</span></span>

<span data-ttu-id="8ac81-2570">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2571">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2571">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2572">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2572">See Also</span></span>

- <span data-ttu-id="8ac81-2573">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2573">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2574">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2574">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2575">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2575">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2576">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2576">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2577">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2577">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2578">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2578">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2579">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2579">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2580">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2580">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2581">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2581">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2582">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2582">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2583">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2583">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2584">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2584">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2585">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2585">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2586">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2586">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2587">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2587">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2588">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2588">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2589">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2589">fx_system_initialize</span></span>

## <a name="fx_media_close_notify_set"></a><span data-ttu-id="8ac81-2590">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2590">fx_media_close_notify_set</span></span>

<span data-ttu-id="8ac81-2591">Medya kapatma bildirimi işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-2591">Sets the media close notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2592">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2592">Prototype</span></span>

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a><span data-ttu-id="8ac81-2593">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2593">Description</span></span>

<span data-ttu-id="8ac81-2594">Bu hizmet, bir medya başarıyla kapatıldıktan sonra çağrılacak bir bildirim geri arama işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2594">This service sets a notify callback function which will be invoked after a media is successfully closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2595">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2595">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2596">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2596">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-2597">**media_close_notify**: medya kapatma geri arama işlevi yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2597">**media_close_notify**: Media close notify callback function to be installed.</span></span> <span data-ttu-id="8ac81-2598">Geri çağırma işlevi olarak NULL geçirme, medya kapatma geri aramasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2598">Passing NULL as the callback function disables the media close callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2599">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2599">Return Values</span></span>

- <span data-ttu-id="8ac81-2600">**FX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2600">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="8ac81-2601">**FX_PTR_ERROR** (0x18) media_ptr null.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2601">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="8ac81-2602">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2602">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2603">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2603">Allowed From</span></span>

<span data-ttu-id="8ac81-2604">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2604">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2605">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2605">Example</span></span>

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a><span data-ttu-id="8ac81-2606">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2606">See Also</span></span>

- <span data-ttu-id="8ac81-2607">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2607">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2608">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2608">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2609">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2609">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2610">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2610">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2611">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2611">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2612">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2612">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2613">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2613">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2614">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2614">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2615">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2615">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2616">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2616">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2617">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2617">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2618">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2618">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2619">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2619">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2620">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2620">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2621">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2621">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2622">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2622">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2623">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2623">fx_system_initialize</span></span>

## <a name="fx_media_exfat_format"></a><span data-ttu-id="8ac81-2624">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2624">fx_media_exFAT_format</span></span>

<span data-ttu-id="8ac81-2625">Medyayı biçimlendirir</span><span class="sxs-lookup"><span data-stu-id="8ac81-2625">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2626">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2626">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="8ac81-2627">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2627">Description</span></span>

<span data-ttu-id="8ac81-2628">Bu hizmet verilen medyayı sağlanan parametrelere göre exFAT ile uyumlu bir şekilde biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2628">This service formats the supplied media in an exFAT compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="8ac81-2629">Medyayı açmadan önce bu hizmetin çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2629">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2630">*Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2630">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-2631">*ExFAT birim boyutu bölümün boyutuyla (MBR veya GPT düzeni varsa) veya bölüm düzeni yoksa (MBR veya GPT) tüm cihazın boyutuna eşleşmelidir. kullanılabilir sektörlerden daha az sayıda toplam sektörde biçimlendirildiyse, exFAT diskinin bir Windows sınırlama yoktur*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2631">*The exFAT volume size should match the size of the partition (if there is an MBR or GPT layout), or the size of the whole device if there is no partition layout (no MBR or GPT). There is a limitation on Windows that exFAT Disk will not be recoginzed if formatted with some values of total sectors that are less than available sectors*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2632">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2632">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2633">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2633">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="8ac81-2634">Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2634">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="8ac81-2635">**sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2635">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="8ac81-2636">Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2636">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="8ac81-2637">**driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2637">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="8ac81-2638">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2638">**memory_ptr**: Pointer to the working memory for the media.</span></span> <span data-ttu-id="8ac81-2639">memory_size, çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2639">memory_size Specifies the size of the working media memory.</span></span> <span data-ttu-id="8ac81-2640">Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2640">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="8ac81-2641">**Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2641">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="8ac81-2642">**number_of_fats**: medyadaki Fats sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2642">**number_of_fats**: Number of FATs on the media.</span></span> <span data-ttu-id="8ac81-2643">Geçerli uygulama, medyada bir FAT 'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2643">Current implementation supports one FAT on the media.</span></span>
- <span data-ttu-id="8ac81-2644">**hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2644">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="8ac81-2645">Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2645">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="8ac81-2646">**total_sectors**: medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2646">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="8ac81-2647">**bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2647">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="8ac81-2648">FileX, bunun 32 katı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2648">FileX requires this to be a multiple of 32.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ac81-2649">*Belirtime başvuru ile kesim başına bayt yalnızca şu değerleri alabilir: 512, 1024, 2048 veya 4096.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2649">*With reference to the specification the bytes per sector may take on only the following values: 512, 1024, 2048 or 4096.*</span></span>

- <span data-ttu-id="8ac81-2650">**sectors_per_cluster**: her kümedeki sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2650">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="8ac81-2651">Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2651">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="8ac81-2652">**volumne_serial_number**: Bu birim için kullanılacak seri numarası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2652">**volumne_serial_number**: Serial number to be used for this volume.</span></span>
- <span data-ttu-id="8ac81-2653">**boundary_unit**: fiziksel veri alanı hizalama boyutu, kesim sayısı olarak.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2653">**boundary_unit**: Physical data area alignment size, in number of sectors.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2654">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2654">Return Values</span></span>

- <span data-ttu-id="8ac81-2655">**FX_SUCCESS** (0x00) başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2655">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="8ac81-2656">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2656">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2657">**FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2657">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="8ac81-2658">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2658">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2659">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2659">Allowed From</span></span>

<span data-ttu-id="8ac81-2660">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2660">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2661">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2661">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-2662">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2662">See Also</span></span>

- <span data-ttu-id="8ac81-2663">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2663">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2664">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2664">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2665">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2665">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2666">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2666">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2667">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2667">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2668">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2668">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2669">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2669">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2670">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2670">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2671">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2671">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2672">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2672">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2673">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2673">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2674">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2674">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2675">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2675">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2676">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2676">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2677">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2677">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2678">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2678">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2679">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2679">fx_system_initialize</span></span>

## <a name="fx_media_extended_space_available"></a><span data-ttu-id="8ac81-2680">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2680">fx_media_extended_space_available</span></span>

<span data-ttu-id="8ac81-2681">Kullanılabilir medya alanını döndürür</span><span class="sxs-lookup"><span data-stu-id="8ac81-2681">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2682">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2682">Prototype</span></span>

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-2683">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2683">Description</span></span>

<span data-ttu-id="8ac81-2684">Bu hizmet, medyada kullanılabilir olan bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2684">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="8ac81-2685">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2685">This service is designed for exFAT.</span></span> <span data-ttu-id="8ac81-2686">*Available_bytes* parametresi işaretçisi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 ' ün üzerinde medya ile çalışmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2686">The pointer to *available_bytes* parameter takes a 64-bit integer value, which allows the caller to work with media beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2687">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2687">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2688">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2688">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8ac81-2689">**available_bytes_ptr**: medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2689">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2690">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2690">Return Values</span></span>

- <span data-ttu-id="8ac81-2691">**FX_SUCCESS** (0x00) medyada bulunan alanı başarıyla aldı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2691">**FX_SUCCESS** (0x00) Successfully retrieved space available on the media.</span></span>
- <span data-ttu-id="8ac81-2692">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2692">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2693">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi null.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2693">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="8ac81-2694">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2694">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2695">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2695">Allowed From</span></span>

<span data-ttu-id="8ac81-2696">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2696">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2697">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2697">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2698">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2698">See Also</span></span>

- <span data-ttu-id="8ac81-2699">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2699">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2700">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2700">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2701">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2701">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2702">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2702">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2703">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2703">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2704">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2704">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2705">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2705">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2706">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2706">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2707">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2707">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2708">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2708">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2709">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2709">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2710">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2710">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2711">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2711">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2712">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2712">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2713">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2713">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2714">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2714">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2715">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2715">fx_system_initialize</span></span>

## <a name="fx_media_flush"></a><span data-ttu-id="8ac81-2716">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2716">fx_media_flush</span></span>

<span data-ttu-id="8ac81-2717">Verileri fiziksel medyaya boşaltıyor</span><span class="sxs-lookup"><span data-stu-id="8ac81-2717">Flushes data to physical media</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2718">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2718">Prototype</span></span>

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-2719">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2719">Description</span></span>

<span data-ttu-id="8ac81-2720">Bu hizmet, değiştirilen dosyaların tüm önbelleğe alınmış kesimlerini ve dizin girişlerini fiziksel medyaya boşaltıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2720">This service flushes all cached sectors and directory entries of any modified files to the physical media.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2721">*Hedefte ani güç kaybı yaşanması durumunda dosya bozulması ve/veya veri kaybı riskini azaltmak için bu yordam uygulama tarafından düzenli aralıklarla çağrılabiliyor.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2721">*This routine may be called periodically by the application to reduce the risk of file corruption and/or data loss in the event of a sudden loss of power on the target.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2722">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2722">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2723">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2723">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2724">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2724">Return Values</span></span>

- <span data-ttu-id="8ac81-2725">**FX_SUCCESS** (0x00) Başarılı medya boşaltma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2725">**FX_SUCCESS** (0x00) Successful media flush.</span></span>
- <span data-ttu-id="8ac81-2726">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2726">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2727">**FX_FILE_CORRUPT**    (0x08) Dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2727">**FX_FILE_CORRUPT**    (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8ac81-2728">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2728">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2729">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2729">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2730">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2730">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-2731">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2731">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-2732">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2732">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2733">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2733">Allowed From</span></span>

<span data-ttu-id="8ac81-2734">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2734">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2735">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2735">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2736">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2736">See Also</span></span>

- <span data-ttu-id="8ac81-2737">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2737">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2738">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2738">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2739">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2739">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2740">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2740">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2741">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2741">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2742">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2742">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2743">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2743">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2744">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2744">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2745">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2745">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2746">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2746">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2747">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2747">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2748">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2748">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2749">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2749">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2750">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2750">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2751">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2751">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2752">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2752">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2753">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2753">fx_system_initialize</span></span>

## <a name="fx_media_format"></a><span data-ttu-id="8ac81-2754">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2754">fx_media_format</span></span>

<span data-ttu-id="8ac81-2755">Medyayı biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="8ac81-2755">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2756">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2756">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="8ac81-2757">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2757">Description</span></span>

<span data-ttu-id="8ac81-2758">Bu hizmet sağlanan medyayı fat 12/16/32 uyumlu bir şekilde sağlanan parametrelere göre biçimler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2758">This service formats the supplied media in a FAT 12/16/32 compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="8ac81-2759">Medya açılmadan önce bu hizmetin çağrılsı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2759">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2760">*Zaten biçimlendirilmiş bir medyayı biçimlendirmek, medyanın tüm dosyalarını ve dizinlerini etkili bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2760">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2761">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2761">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2762">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2762">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="8ac81-2763">Bu yalnızca sürücünün çalışması için gereken bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2763">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="8ac81-2764">**driver:** Bu medya için I/O sürücüsünün işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2764">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="8ac81-2765">Bu genellikle sonraki çağrıya sağlanan sürücü fx_media_open olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2765">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="8ac81-2766">**driver_info_ptr:** I/Ç sürücüsünün kullanabiliyor olduğu isteğe bağlı bilgilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2766">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="8ac81-2767">**memory_ptr:** Medya için çalışan belleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2767">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="8ac81-2768">**memory_size:** Çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2768">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="8ac81-2769">Boyutun en azından medyanın kesim boyutu kadar büyük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2769">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="8ac81-2770">**volume_name:** En fazla 11 karakter uzunluğunda olan birim adı dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2770">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="8ac81-2771">**number_of_fats:** Medyada SSS sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2771">**number_of_fats**: Number of FATs in the media.</span></span> <span data-ttu-id="8ac81-2772">Birincil FAT için minimum değer 1'tir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2772">The minimal value is 1 for the primary FAT.</span></span> <span data-ttu-id="8ac81-2773">1'den büyük değerler çalışma zamanında ek FAT kopyaların korunmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2773">Values greater than 1 result in additional FAT copies being maintained at run-time.</span></span>
- <span data-ttu-id="8ac81-2774">**directory_entries:** Kök dizindeki dizin girdilerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2774">**directory_entries**: Number of directory entries in the root directory.</span></span>
- <span data-ttu-id="8ac81-2775">**hidden_sectors:** Bu medyanın önyükleme kesimi öncesinde gizlenen kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2775">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="8ac81-2776">Bu durum, birden çok bölüm olduğunda normaldir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2776">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="8ac81-2777">**total_sectors:** Medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2777">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="8ac81-2778">**bytes_per_sector:** Genellikle 512 olan kesim başına bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2778">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="8ac81-2779">FileX için bunun 32'nin katları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2779">FileX requires this to be a multiple of 32.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ac81-2780">*Belirtim başvurusuyla, kesim başına bayt sayısı yalnızca şu değerleri alır: 512, 1024, 2048 veya 4096.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2780">*With reference to the specification the bytes per sector may take on only the following values: 512, 1024, 2048 or 4096.*</span></span>

- <span data-ttu-id="8ac81-2781">**sectors_per_cluster:** Her kümede kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2781">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="8ac81-2782">Küme, FAT dosya sistemi içinde en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2782">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="8ac81-2783">**heads:** Fiziksel tura sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2783">**heads**: Number of physical heads.</span></span>
- <span data-ttu-id="8ac81-2784">**sectors_per_track:** Parça başına kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2784">**sectors_per_track**: Number of sectors per track.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2785">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2785">Return Values</span></span>

- <span data-ttu-id="8ac81-2786">**FX_SUCCESS** (0x00) Başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2786">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="8ac81-2787">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2787">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2788">**FX_PTR_ERROR** (0x18) Geçersiz medya, sürücü veya bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2788">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="8ac81-2789">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2789">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2790">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2790">Allowed From</span></span>

<span data-ttu-id="8ac81-2791">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2791">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2792">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2792">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-2793">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2793">See Also</span></span>

- <span data-ttu-id="8ac81-2794">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2794">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2795">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2795">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2796">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2796">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2797">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2797">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2798">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2798">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2799">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2799">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2800">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2800">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2801">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2801">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2802">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2802">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2803">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2803">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2804">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2804">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2805">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2805">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2806">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2806">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2807">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2807">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2808">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2808">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2809">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2809">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2810">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2810">fx_system_initialize</span></span>

## <a name="fx_media_open"></a><span data-ttu-id="8ac81-2811">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2811">fx_media_open</span></span>

<span data-ttu-id="8ac81-2812">Dosya erişimi için medya açar</span><span class="sxs-lookup"><span data-stu-id="8ac81-2812">Opens media for file access</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2813">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2813">Prototype</span></span>

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a><span data-ttu-id="8ac81-2814">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2814">Description</span></span>

<span data-ttu-id="8ac81-2815">Bu hizmet, sağlanan I/O sürücüsünü kullanarak dosya erişimi için bir medya açar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2815">This service opens a media for file access using the supplied I/O driver.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-2816">*Bu hizmete sağlanan bellek iç mantıksal kesim önbelleğini uygulamak için kullanılır, bu nedenle bellek ne kadar fazla bellek sağlanırsa o kadar fazla fiziksel I/O azalır. FileX için en az bir mantıksal kesim (medya kesimi başına bayt) önbelleği gerekir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2816">*The memory supplied to this service is used to implement an internal logical sector cache, hence, the more memory supplied the more physical I/O is reduced. FileX requires a cache of at least one logical sector (bytes per sector of the media).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2817">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2817">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2818">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2818">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-2819">**media_name:** Medyanın adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2819">**media_name**: Pointer to media's name.</span></span>
- <span data-ttu-id="8ac81-2820">**media_driver:** Bu medya için I/O sürücüsünün işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2820">**media_driver**: Pointer to I/O driver for this media.</span></span> <span data-ttu-id="8ac81-2821">I/O sürücüsünün Bölüm 5'te tanımlanan FileX sürücü gereksinimlerine uyması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2821">The I/O driver must conform to FileX driver requirements defined in Chapter 5.</span></span>
- <span data-ttu-id="8ac81-2822">**driver_info_ptr:** Sağlanan I/Ç sürücüsünün kullanabiliyor olduğu isteğe bağlı bilgilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2822">**driver_info_ptr**: Pointer to optional information that the supplied I/O driver may utilize.</span></span>
- <span data-ttu-id="8ac81-2823">**memory_ptr:** Medya için çalışan belleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2823">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="8ac81-2824">**memory_size:** Çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2824">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="8ac81-2825">Boyut, medyanın kesim boyutu (genellikle 512 bayt) kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2825">The size must be as large as the media's sector size (typically 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2826">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2826">Return Values</span></span>

- <span data-ttu-id="8ac81-2827">**FX_SUCCESS** (0x00) Başarılı medya açma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2827">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="8ac81-2828">**FX_BOOT_ERROR** (0x01) Medyanın önyükleme kesimi okundu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2828">**FX_BOOT_ERROR** (0x01) Error reading the media's boot sector.</span></span>
- <span data-ttu-id="8ac81-2829">**FX_MEDIA_INVALID** (0x02) Belirtilen medyanın önyükleme kesimi bozuk veya geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2829">**FX_MEDIA_INVALID** (0x02) Specified media's boot sector is corrupt or invalid.</span></span> <span data-ttu-id="8ac81-2830">Ayrıca, bu dönüş kodu mantıksal kesim önbellek boyutunun veya FAT giriş boyutunun 2'nin gücü olmadığını belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2830">In addition, this return code is used to indicate that either the logical sector cache size or the FAT entry size is not a power of 2.</span></span>
- <span data-ttu-id="8ac81-2831">**FX_FAT_READ_ERROR** FAT 0x03 okuma hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2831">**FX_FAT_READ_ERROR** (0x03) Error reading the media FAT.</span></span>
- <span data-ttu-id="8ac81-2832">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2832">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2833">**FX_PTR_ERROR** (0x18) Bir veya daha fazla işaretçi NULL olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2833">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="8ac81-2834">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2834">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2835">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2835">Allowed From</span></span>

<span data-ttu-id="8ac81-2836">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2836">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2837">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2837">Example</span></span>

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2838">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2838">See Also</span></span>

- <span data-ttu-id="8ac81-2839">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2839">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2840">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2840">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2841">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2841">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2842">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2842">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2843">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2843">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2844">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2844">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2845">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2845">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2846">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2846">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2847">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2847">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2848">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2848">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2849">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2849">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2850">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2850">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2851">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2851">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2852">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2852">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2853">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2853">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2854">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2854">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2855">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2855">fx_system_initialize</span></span>

## <a name="fx_media_open_notify_set"></a><span data-ttu-id="8ac81-2856">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2856">fx_media_open_notify_set</span></span>

<span data-ttu-id="8ac81-2857">Medya açık notify işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-2857">Sets the media open notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2858">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2858">Prototype</span></span>

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a><span data-ttu-id="8ac81-2859">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2859">Description</span></span>

<span data-ttu-id="8ac81-2860">Bu hizmet, bir medya başarıyla açıldıktan sonra çağrılan bir notify callback işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2860">This service sets a notify callback function which will be invoked after a media is successfully opened.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2861">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2861">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2862">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2862">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-2863">**media_open_notify:** Medya aç notify callback işlevi yüklenmek için.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2863">**media_open_notify**: Media open notify callback function to be installed.</span></span> <span data-ttu-id="8ac81-2864">Geri çağırma işlevi olarak NULL değerinin geçirmesi, medya açık geri çağırmayı devre dışı bırakmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2864">Passing NULL as the callback function disables the media open callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2865">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2865">Return Values</span></span>


- <span data-ttu-id="8ac81-2866">**FX_SUCCESS** (0x00) Geri çağırma işlevi başarılı bir şekilde yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2866">**FX_SUCCESS** (0x00) Successfuly installed the callback function.</span></span>
- <span data-ttu-id="8ac81-2867">**FX_PTR_ERROR** (0x18) media_ptr NULL olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2867">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="8ac81-2868">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2868">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2869">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2869">Allowed From</span></span>

<span data-ttu-id="8ac81-2870">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2871">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2871">Example</span></span>

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2872">See Also</span></span>

- <span data-ttu-id="8ac81-2873">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2873">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2874">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2874">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2875">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2875">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2876">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2876">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2877">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2877">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2878">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2878">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2879">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2879">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2880">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2880">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2881">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2881">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2882">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2882">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2883">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2883">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2884">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2884">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2885">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2885">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2886">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2886">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2887">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2887">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2888">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2888">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2889">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2889">fx_system_initialize</span></span>

## <a name="fx_media_read"></a><span data-ttu-id="8ac81-2890">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2890">fx_media_read</span></span>

<span data-ttu-id="8ac81-2891">Medyadan mantıksal kesim okur</span><span class="sxs-lookup"><span data-stu-id="8ac81-2891">Reads logical sector from media</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2892">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2892">Prototype</span></span>

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-2893">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2893">Description</span></span>

<span data-ttu-id="8ac81-2894">Bu hizmet, medyadan bir mantıksal kesim okur ve sağlanan arabelleğe yer sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2894">This service reads a logical sector from the media and places it into the supplied buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2895">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2895">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2896">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2896">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8ac81-2897">**logical_sector:** Okunacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2897">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="8ac81-2898">**buffer_ptr:** Mantıksal kesim okuması için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2898">**buffer_ptr**: Pointer to the destination for the logical sector read.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2899">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2899">Return Values</span></span>

- <span data-ttu-id="8ac81-2900">**FX_SUCCESS** (0x00) Başarılı medya okuma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2900">**FX_SUCCESS** (0x00) Successful media read.</span></span>
- <span data-ttu-id="8ac81-2901">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2901">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2902">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2902">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2903">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2903">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-2904">**FX_PTR_ERROR** (0x18) Geçersiz medya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2904">**FX_PTR_ERROR** (0x18) Invalid media or buffer pointer.</span></span>
- <span data-ttu-id="8ac81-2905">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2905">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2906">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2906">Allowed From</span></span>

<span data-ttu-id="8ac81-2907">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2907">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2908">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2908">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-2909">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2909">See Also</span></span>

- <span data-ttu-id="8ac81-2910">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2910">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2911">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2911">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2912">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2912">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2913">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2913">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2914">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2914">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2915">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2915">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2916">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2916">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2917">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2917">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2918">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2918">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2919">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2919">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2920">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2920">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2921">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2921">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2922">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2922">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-2923">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2923">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2924">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2924">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2925">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2925">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2926">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2926">fx_system_initialize</span></span>

## <a name="fx_media_space_available"></a><span data-ttu-id="8ac81-2927">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2927">fx_media_space_available</span></span>

<span data-ttu-id="8ac81-2928">Kullanılabilir medya alanı döndürür</span><span class="sxs-lookup"><span data-stu-id="8ac81-2928">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2929">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2929">Prototype</span></span>

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a><span data-ttu-id="8ac81-2930">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2930">Description</span></span>

<span data-ttu-id="8ac81-2931">Bu hizmet, medyada kullanılabilir bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2931">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="8ac81-2932">4 GB'den büyük medya ile çalışmak için, uygulama tarafından *fx_media_extended_space_available.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-2932">To work with the media larger than 4GB, application shall use the service *fx_media_extended_space_available*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2933">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2933">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2934">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2934">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8ac81-2935">**available_bytes_ptr:** Medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2935">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2936">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2936">Return Values</span></span>

- <span data-ttu-id="8ac81-2937">**FX_SUCCESS** (0x00) Medyada kullanılabilir alan başarıyla döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2937">**FX_SUCCESS** (0x00) Successfully returned available space on media.</span></span>
- <span data-ttu-id="8ac81-2938">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2938">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2939">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi NULL.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2939">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="8ac81-2940">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2940">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2941">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2941">Allowed From</span></span>

<span data-ttu-id="8ac81-2942">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2942">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2943">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2943">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2944">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2944">See Also</span></span>

- <span data-ttu-id="8ac81-2945">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2945">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2946">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2946">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2947">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2947">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2948">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2948">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2949">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2949">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2950">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2950">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2951">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2951">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2952">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2952">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2953">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2953">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2954">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2954">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2955">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2955">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2956">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2956">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2957">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2957">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2958">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2958">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-2959">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2959">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-2960">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-2960">fx_media_write</span></span>
- <span data-ttu-id="8ac81-2961">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-2961">fx_system_initialize</span></span>

## <a name="fx_media_volume_get"></a><span data-ttu-id="8ac81-2962">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-2962">fx_media_volume_get</span></span>

<span data-ttu-id="8ac81-2963">Medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-2963">Gets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-2964">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-2964">Prototype</span></span>

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="8ac81-2965">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-2965">Description</span></span>

<span data-ttu-id="8ac81-2966">Bu hizmet, önceden açılmış olan medyanın birim adını alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2966">This service retrieves the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-2967">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2967">Input Parameters</span></span>

- <span data-ttu-id="8ac81-2968">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2968">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-2969">**volume_name:** Birim adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2969">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="8ac81-2970">Hedefin en az 12 karakter uzunluğunda olacak kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2970">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="8ac81-2971">**volume_source:** Önyükleme kesimi veya kök dizinden adın nereden alınacaklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2971">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="8ac81-2972">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-2972">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="8ac81-2973">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8ac81-2973">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="8ac81-2974">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8ac81-2974">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-2975">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-2975">Return Values</span></span>

- <span data-ttu-id="8ac81-2976">**FX_SUCCESS** (0x00) Başarılı medya birimi get.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2976">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="8ac81-2977">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2977">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-2978">**FX_NOT_FOUND** (0x04) Birimi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2978">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="8ac81-2979">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2979">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-2980">**FX_PTR_ERROR** (0x18) Geçersiz medya veya birim hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2980">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="8ac81-2981">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2981">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-2982">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-2982">Allowed From</span></span>

<span data-ttu-id="8ac81-2983">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-2983">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-2984">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-2984">Example</span></span>

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a><span data-ttu-id="8ac81-2985">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-2985">See Also</span></span>

- <span data-ttu-id="8ac81-2986">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-2986">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-2987">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-2987">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-2988">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-2988">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-2989">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-2989">fx_media_check</span></span>
- <span data-ttu-id="8ac81-2990">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-2990">fx_media_close</span></span>
- <span data-ttu-id="8ac81-2991">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2991">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-2992">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2992">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-2993">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2993">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-2994">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-2994">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-2995">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-2995">fx_media_format</span></span>
- <span data-ttu-id="8ac81-2996">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-2996">fx_media_open</span></span>
- <span data-ttu-id="8ac81-2997">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-2997">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-2998">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-2998">fx_media_read</span></span>
- <span data-ttu-id="8ac81-2999">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-2999">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-3000">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3000">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-3001">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3001">fx_media_write</span></span>
- <span data-ttu-id="8ac81-3002">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3002">fx_system_initialize</span></span>

## <a name="fx_media_volume_get_extended"></a><span data-ttu-id="8ac81-3003">fx_media_volume_get_extended</span><span class="sxs-lookup"><span data-stu-id="8ac81-3003">fx_media_volume_get_extended</span></span>

<span data-ttu-id="8ac81-3004">Önceden açılmış olan medyanın medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3004">Gets media volume name of previously opened media</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3005">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3005">Prototype</span></span>

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="8ac81-3006">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3006">Description</span></span>

<span data-ttu-id="8ac81-3007">Bu hizmet, önceden açılmış olan medyanın birim adını alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3007">This service retrieves the volume name of the previously opened media.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3008">Bu hizmet \***fx_media_volume_get() _** ile aynıdır, ancak çağıranın _ volume_name \**arabelleğinin boyutunu* geçer.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3008">This service is identical to ***fx_media_volume_get()** _ except the caller passes in the size of the _ *volume_name** buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3009">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3009">Input Parameters</span></span>


- <span data-ttu-id="8ac81-3010">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3010">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3011">**volume_name:** Birim adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3011">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="8ac81-3012">Hedefin en az 12 karakter uzunluğunda olacak kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3012">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="8ac81-3013">**volume_name_buffer_length:** Arabelleğin volume_name boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3013">**volume_name_buffer_length**: Size of volume_name buffer.</span></span>
- <span data-ttu-id="8ac81-3014">**volume_source:** Önyükleme kesimi veya kök dizinden adın nereden alınacaklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3014">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="8ac81-3015">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8ac81-3015">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="8ac81-3016">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8ac81-3016">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="8ac81-3017">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8ac81-3017">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3018">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3018">Return Values</span></span>

- <span data-ttu-id="8ac81-3019">**FX_SUCCESS** (0x00) Başarılı medya birimi get.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3019">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="8ac81-3020">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3020">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3021">**FX_NOT_FOUND** (0x04) Birimi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3021">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="8ac81-3022">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3022">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3023">**FX_PTR_ERROR** (0x18) Geçersiz medya veya birim hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3023">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="8ac81-3024">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3024">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3025">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3025">Allowed From</span></span>

<span data-ttu-id="8ac81-3026">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3026">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3027">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3027">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-3028">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3028">See Also</span></span>

- <span data-ttu-id="8ac81-3029">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-3029">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-3030">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-3030">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-3031">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3031">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-3032">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-3032">fx_media_check</span></span>
- <span data-ttu-id="8ac81-3033">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3033">fx_media_close</span></span>
- <span data-ttu-id="8ac81-3034">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3034">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-3035">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-3035">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-3036">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-3036">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-3037">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-3037">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-3038">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-3038">fx_media_format</span></span>
- <span data-ttu-id="8ac81-3039">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3039">fx_media_open</span></span>
- <span data-ttu-id="8ac81-3040">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3040">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-3041">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3041">fx_media_read</span></span>
- <span data-ttu-id="8ac81-3042">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-3042">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-3043">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3043">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-3044">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3044">fx_media_write</span></span>
- <span data-ttu-id="8ac81-3045">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3045">fx_system_initialize</span></span>

## <a name="fx_media_volume_set"></a><span data-ttu-id="8ac81-3046">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3046">fx_media_volume_set</span></span>

<span data-ttu-id="8ac81-3047">Medya birimi adını ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-3047">Sets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3048">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3048">Prototype</span></span>

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-3049">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3049">Description</span></span>

<span data-ttu-id="8ac81-3050">Bu hizmet, önceden açılmış olan medyanın birim adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3050">This service sets the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3051">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3051">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3052">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3052">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3053">**volume_name:** Birim adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3053">**volume_name**: Pointer to the volume name.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3054">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3054">Return Values</span></span>

- <span data-ttu-id="8ac81-3055">**FX_SUCCESS** (0x00) Başarılı medya birimi kümesi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3055">**FX_SUCCESS** (0x00) Successful media volume set.</span></span>
- <span data-ttu-id="8ac81-3056">**FX_INVALID_NAME** (0x0C) Volume_name geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3056">**FX_INVALID_NAME** (0x0C) Volume_name is invalid.</span></span>
- <span data-ttu-id="8ac81-3057">**FX_MEDIA_INVALID** (0x02) Birim adı ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3057">**FX_MEDIA_INVALID** (0x02) Unable to set volume name.</span></span>
- <span data-ttu-id="8ac81-3058">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3058">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3059">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3059">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3060">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3060">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-3061">**FX_PTR_ERROR** (0x18) Geçersiz medya veya birim adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3061">**FX_PTR_ERROR** (0x18) Invalid media or volume name pointer.</span></span>
- <span data-ttu-id="8ac81-3062">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3062">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3063">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3063">Allowed From</span></span>

<span data-ttu-id="8ac81-3064">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3064">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3065">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3065">Example</span></span>

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-3066">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3066">See Also</span></span>

- <span data-ttu-id="8ac81-3067">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-3067">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-3068">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-3068">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-3069">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3069">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-3070">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-3070">fx_media_check</span></span>
- <span data-ttu-id="8ac81-3071">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3071">fx_media_close</span></span>
- <span data-ttu-id="8ac81-3072">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3072">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-3073">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-3073">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-3074">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-3074">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-3075">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-3075">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-3076">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-3076">fx_media_format</span></span>
- <span data-ttu-id="8ac81-3077">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3077">fx_media_open</span></span>
- <span data-ttu-id="8ac81-3078">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3078">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-3079">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3079">fx_media_read</span></span>
- <span data-ttu-id="8ac81-3080">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-3080">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-3081">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3081">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-3082">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3082">fx_media_write</span></span>
- <span data-ttu-id="8ac81-3083">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3083">fx_system_initialize</span></span>

## <a name="fx_media_write"></a><span data-ttu-id="8ac81-3084">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3084">fx_media_write</span></span>

<span data-ttu-id="8ac81-3085">Yazma mantıksal kesimi</span><span class="sxs-lookup"><span data-stu-id="8ac81-3085">Writes logical sector</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3086">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3086">Prototype</span></span>

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="8ac81-3087">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3087">Description</span></span>

<span data-ttu-id="8ac81-3088">Bu hizmet sağlanan arabelleği belirtilen mantıksal kesime yazar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3088">This service writes the supplied buffer to the specified logical sector.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3089">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3089">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3090">**media_ptr:** Önceden açılmış bir medyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3090">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8ac81-3091">**logical_sector:** Yazacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3091">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="8ac81-3092">**buffer_ptr:** Mantıksal kesim yazma için kaynağın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3092">**buffer_ptr**: Pointer to the source for the logical sector write.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3093">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3093">Return Values</span></span>

- <span data-ttu-id="8ac81-3094">**FX_SUCCESS** (0x00) Başarılı medya yazma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3094">**FX_SUCCESS** (0x00) Successful media write.</span></span>
- <span data-ttu-id="8ac81-3095">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3095">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3096">**FX_SECTOR_INVALID** (0x89) Geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3096">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-3097">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3097">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3098">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3098">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-3099">**FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3099">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8ac81-3100">**FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3100">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3101">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3101">Allowed From</span></span>

<span data-ttu-id="8ac81-3102">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3102">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3103">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3103">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3104">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3104">See Also</span></span>

- <span data-ttu-id="8ac81-3105">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8ac81-3105">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8ac81-3106">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8ac81-3106">fx_media_abort</span></span>
- <span data-ttu-id="8ac81-3107">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3107">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8ac81-3108">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8ac81-3108">fx_media_check</span></span>
- <span data-ttu-id="8ac81-3109">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3109">fx_media_close</span></span>
- <span data-ttu-id="8ac81-3110">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3110">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8ac81-3111">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-3111">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8ac81-3112">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-3112">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8ac81-3113">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8ac81-3113">fx_media_flush</span></span>
- <span data-ttu-id="8ac81-3114">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8ac81-3114">fx_media_format</span></span>
- <span data-ttu-id="8ac81-3115">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3115">fx_media_open</span></span>
- <span data-ttu-id="8ac81-3116">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3116">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8ac81-3117">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3117">fx_media_read</span></span>
- <span data-ttu-id="8ac81-3118">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8ac81-3118">fx_media_space_available</span></span>
- <span data-ttu-id="8ac81-3119">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3119">fx_media_volume_get</span></span>
- <span data-ttu-id="8ac81-3120">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3120">fx_media_volume_set</span></span>
- <span data-ttu-id="8ac81-3121">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3121">fx_system_initialize</span></span>

## <a name="fx_system_date_get"></a><span data-ttu-id="8ac81-3122">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3122">fx_system_date_get</span></span>

<span data-ttu-id="8ac81-3123">Dosya sistemi tarihini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3123">Gets file system date</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3124">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3124">Prototype</span></span>

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a><span data-ttu-id="8ac81-3125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3125">Description</span></span>

<span data-ttu-id="8ac81-3126">Bu hizmet, geçerli sistem tarihini döndürür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3126">This service returns the current system date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3127">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3127">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3128">**yıl**: yıl için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3128">**year**: Pointer to destination for year.</span></span>
- <span data-ttu-id="8ac81-3129">**Month**: ay için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3129">**month**: Pointer to destination for month.</span></span>
- <span data-ttu-id="8ac81-3130">**gün**: günün hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3130">**day**: Pointer to destination for day.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3131">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3131">Return Values</span></span>

- <span data-ttu-id="8ac81-3132">**FX_SUCCESS** (0x00) başarılı Tarih alımı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3132">**FX_SUCCESS** (0x00) Successful date retrieval.</span></span>
- <span data-ttu-id="8ac81-3133">**FX_PTR_ERROR** (0x18) bir veya daha fazla GIRIŞ parametresi null.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3133">**FX_PTR_ERROR** (0x18) One or more of the input parameters are NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3134">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3134">Allowed From</span></span>

<span data-ttu-id="8ac81-3135">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3135">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3136">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3136">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3137">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3137">See Also</span></span>

- <span data-ttu-id="8ac81-3138">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3138">fx_system_date_set</span></span>
- <span data-ttu-id="8ac81-3139">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3139">fx_system_initialize</span></span>
- <span data-ttu-id="8ac81-3140">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3140">fx_system_time_get</span></span>
- <span data-ttu-id="8ac81-3141">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3141">fx_system_time_set</span></span>

## <a name="fx_system_date_set"></a><span data-ttu-id="8ac81-3142">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3142">fx_system_date_set</span></span>

<span data-ttu-id="8ac81-3143">Sistem tarihini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-3143">Sets system date</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3144">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3144">Prototype</span></span>

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a><span data-ttu-id="8ac81-3145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3145">Description</span></span>

<span data-ttu-id="8ac81-3146">Bu hizmet, sistem tarihini belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3146">This service sets the system date as specified.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-3147">*İlk sistem tarihini ayarlamak için bu hizmet **fx_system_initialize** kısa süre sonra çağrılmalıdır. Varsayılan olarak, sistem tarihi en son genel FileX sürümüdür.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3147">*This service should be called shortly after **fx_system_initialize** to set the initial system date. By default, the system date is that of the last generic FileX release.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3148">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3148">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3149">**yıl**: yeni yıl.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3149">**year**: New year.</span></span> <span data-ttu-id="8ac81-3150">Geçerli Aralık 1980 yılında 2107 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3150">The valid range is from 1980 through the year 2107.</span></span>
- <span data-ttu-id="8ac81-3151">**ay**: yeni ay.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3151">**month**: New month.</span></span> <span data-ttu-id="8ac81-3152">Geçerli Aralık 1 ile 12 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3152">The valid range is from 1 through 12.</span></span>
- <span data-ttu-id="8ac81-3153">**gün**: yeni gün.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3153">**day**: New day.</span></span> <span data-ttu-id="8ac81-3154">Geçerli Aralık, aya ve artık yıl koşullarına bağlı olarak 1 ila 31 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3154">The valid range is from 1 through 31, depending on month and leap year conditions.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3155">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3155">Return Values</span></span>

- <span data-ttu-id="8ac81-3156">**FX_SUCCESS** (0x00) başarılı tarih ayarı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3156">**FX_SUCCESS** (0x00) Successful date setting.</span></span>
- <span data-ttu-id="8ac81-3157">**FX_INVALID_YEAR** (0x12) geçersiz yıl belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3157">**FX_INVALID_YEAR** (0x12) Invalid year specified.</span></span>
- <span data-ttu-id="8ac81-3158">**FX_INVALID_MONTH** (0x13) geçersiz ay belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3158">**FX_INVALID_MONTH** (0x13) Invalid month specified.</span></span>
- <span data-ttu-id="8ac81-3159">**FX_INVALID_DAY** (0x14) geçersiz gün belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3159">**FX_INVALID_DAY** (0x14) Invalid day specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3160">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3160">Allowed From</span></span>

<span data-ttu-id="8ac81-3161">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3161">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3162">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3162">Example</span></span>

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-3163">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3163">See Also</span></span>

- <span data-ttu-id="8ac81-3164">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3164">fx_system_date_get</span></span>
- <span data-ttu-id="8ac81-3165">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3165">fx_system_initialize</span></span>
- <span data-ttu-id="8ac81-3166">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3166">fx_system_time_get</span></span>
- <span data-ttu-id="8ac81-3167">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3167">fx_system_time_set</span></span>

## <a name="fx_system_initialize"></a><span data-ttu-id="8ac81-3168">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3168">fx_system_initialize</span></span>

<span data-ttu-id="8ac81-3169">Tüm sistemi başlatır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3169">Initializes entire system</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3170">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3170">Prototype</span></span>

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a><span data-ttu-id="8ac81-3171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3171">Description</span></span>

<span data-ttu-id="8ac81-3172">Bu hizmet, tüm önemli dosya x veri yapılarını başlatır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3172">This service initializes all the major FileX data structures.</span></span> <span data-ttu-id="8ac81-3173">***Tx_application_define*** veya belki de bir başlatma iş parçacığından çağrılmalıdır ve başka bir FileX hizmeti kullanılmadan önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3173">It should be called either in ***tx_application_define*** or possibly from an initialization thread and must be called prior to using any other FileX service.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-3174">\* Bu çağrı tarafından başlatıldıktan sonra uygulama, *doğru bir sistem tarih ve saati ile başlamak için **fx_system_date_set** _ ve _ *fx_system_time_set** çağırmalıdır.\*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3174">*Once initialized by this call, the application should call ***fx_system_date_set** _ and _ *fx_system_time_set** to start with an accurate system date and time.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3175">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3175">Input Parameters</span></span>

<span data-ttu-id="8ac81-3176">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3176">None</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3177">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3177">Return Values</span></span>

<span data-ttu-id="8ac81-3178">Yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3178">None.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3179">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3179">Allowed From</span></span>

<span data-ttu-id="8ac81-3180">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3180">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3181">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3181">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3182">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3182">See Also</span></span>

- <span data-ttu-id="8ac81-3183">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3183">fx_system_date_get</span></span>
- <span data-ttu-id="8ac81-3184">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3184">fx_system_date_set</span></span>
- <span data-ttu-id="8ac81-3185">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3185">fx_system_time_get</span></span>
- <span data-ttu-id="8ac81-3186">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3186">fx_system_time_set</span></span>

## <a name="fx_system_time_get"></a><span data-ttu-id="8ac81-3187">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3187">fx_system_time_get</span></span>

<span data-ttu-id="8ac81-3188">Geçerli sistem saatini alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3188">Gets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3189">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3189">Prototype</span></span>

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="8ac81-3190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3190">Description</span></span>

<span data-ttu-id="8ac81-3191">Bu hizmet geçerli sistem saatini alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3191">This service retrieves the current system time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3192">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3192">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3193">**saat**: saat için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3193">**hour**: Pointer to destination for hour.</span></span>
- <span data-ttu-id="8ac81-3194">**Minute**: dakikalık hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3194">**minute**: Pointer to destination for minute.</span></span>
- <span data-ttu-id="8ac81-3195">**ikinci**: saniye için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3195">**second**: Pointer to destination for second.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3196">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3196">Return Values</span></span>

- <span data-ttu-id="8ac81-3197">**FX_SUCCESS** (0x00) sistem saati alımı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3197">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="8ac81-3198">**FX_PTR_ERROR** (0x18) bir veya daha fazla giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="8ac81-3198">**FX_PTR_ERROR** (0x18) One or more of the input parameters</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3199">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3199">Allowed From</span></span>

<span data-ttu-id="8ac81-3200">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3200">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3201">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3201">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3202">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3202">See Also</span></span>

- <span data-ttu-id="8ac81-3203">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3203">fx_system_date_get</span></span>
- <span data-ttu-id="8ac81-3204">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3204">fx_system_date_set</span></span>
- <span data-ttu-id="8ac81-3205">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3205">fx_system_initialize</span></span>
- <span data-ttu-id="8ac81-3206">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3206">fx_system_time_set</span></span>

## <a name="fx_system_time_set"></a><span data-ttu-id="8ac81-3207">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3207">fx_system_time_set</span></span>

<span data-ttu-id="8ac81-3208">Geçerli sistem saatini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ac81-3208">Sets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3209">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3209">Prototype</span></span>

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a><span data-ttu-id="8ac81-3210">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3210">Description</span></span>

<span data-ttu-id="8ac81-3211">Bu hizmet, geçerli sistem saatini giriş parametreleri tarafından belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3211">This service sets the current system time to that specified by the input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-3212">*Bu hizmet, ilk sistem saatini ayarlamak için **fx_system_initialize** kısa süre sonra çağrılmalıdır. Varsayılan olarak, sistem saati 0:0:0 ' dir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3212">*This service should be called shortly after **fx_system_initialize** to set the initial system time. By default, the system time is 0:0:0.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3213">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3213">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3214">**saat**: yeni saat (0-23).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3214">**hour**: New hour (0-23).</span></span>
- <span data-ttu-id="8ac81-3215">**dakika**: yeni dakika (0-59).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3215">**minute**: New minute (0-59).</span></span>
- <span data-ttu-id="8ac81-3216">**ikinci**: Yeni saniye (0-59).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3216">**second**: New second (0-59).</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3217">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3217">Return Values</span></span>

- <span data-ttu-id="8ac81-3218">**FX_SUCCESS** (0x00) sistem saati alımı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3218">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="8ac81-3219">**FX_INVALID_HOUR**    (0x15) yeni saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3219">**FX_INVALID_HOUR**    (0x15) New hour is invalid.</span></span>
- <span data-ttu-id="8ac81-3220">**FX_INVALID_MINUTE** (0x16) yeni dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3220">**FX_INVALID_MINUTE** (0x16) New minute is invalid.</span></span>
- <span data-ttu-id="8ac81-3221">**FX_INVALID_SECOND** (0x17) yeni ikinci değer geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3221">**FX_INVALID_SECOND** (0x17) New second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3222">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3222">Allowed From</span></span>

<span data-ttu-id="8ac81-3223">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3223">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3224">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3224">Example</span></span>

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a><span data-ttu-id="8ac81-3225">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3225">See Also</span></span>

- <span data-ttu-id="8ac81-3226">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3226">fx_system_date_get</span></span>
- <span data-ttu-id="8ac81-3227">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3227">fx_system_date_set</span></span>
- <span data-ttu-id="8ac81-3228">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8ac81-3228">fx_system_initialize</span></span>
- <span data-ttu-id="8ac81-3229">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3229">fx_system_time_get</span></span>

## <a name="fx_unicode_directory_create"></a><span data-ttu-id="8ac81-3230">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3230">fx_unicode_directory_create</span></span>

<span data-ttu-id="8ac81-3231">Unicode dizin oluşturur</span><span class="sxs-lookup"><span data-stu-id="8ac81-3231">Creates a Unicode directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3232">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3232">Prototype</span></span>

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-3233">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3233">Description</span></span>

<span data-ttu-id="8ac81-3234">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir alt dizin oluşturur; Unicode kaynak adı parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3234">This service creates a Unicode-named subdirectory in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="8ac81-3235">Başarılı olursa, yeni oluşturulan Unicode alt dizininin kısa adı (8,3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3235">If successful, the short name (8.3 format) of the newly created Unicode subdirectory is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-3236">*Unicode alt dizinindeki tüm işlemler (varsayılan yol, silme, vb.), standart FileX dizin hizmetlerine döndürülen kısa ad (8,3 biçimi) sağlanarak yapılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3236">*All operations on the Unicode subdirectory (making it the default path, deleting, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX directory services.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3237">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3237">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3238">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3238">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3239">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3239">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3240">**source_unicode_name**: yeni alt dizin için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3240">**source_unicode_name**: Pointer to the Unicode name for the new subdirectory.</span></span>
- <span data-ttu-id="8ac81-3241">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3241">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8ac81-3242">**short_name**: yeni Unicode alt dizini için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3242">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode subdirectory.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3243">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3243">Return Values</span></span>

- <span data-ttu-id="8ac81-3244">**FX_SUCCESS** (0x00) başarılı Unicode dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3244">**FX_SUCCESS** (0x00) Successful Unicode directory create.</span></span>
- <span data-ttu-id="8ac81-3245">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3245">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3246">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin zaten var.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3246">**FX_ALREADY_CREATED** (0x0B) Specified directory already exists.</span></span>
- <span data-ttu-id="8ac81-3247">Yeni Dizin girişi için medyada daha fazla küme yok **FX_NO_MORE_SPACE** (0x0A).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3247">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new directory entry.</span></span>
- <span data-ttu-id="8ac81-3248">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3248">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8ac81-3249">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3249">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-3250">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3250">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8ac81-3251">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3251">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="8ac81-3252">**FX_IO_ERROR (0x90)** Sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3252">**FX_IO_ERROR    (0x90)** Driver I/O error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3253">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3253">Allowed From</span></span>

<span data-ttu-id="8ac81-3254">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3254">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3255">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3255">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3256">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3256">See Also</span></span>

- <span data-ttu-id="8ac81-3257">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3257">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-3258">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3258">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-3259">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3259">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-3260">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3260">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-3261">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3261">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-3262">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3262">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-3263">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3263">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-3264">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3264">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-3265">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3265">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-3266">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-3266">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-3267">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3267">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-3268">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-3268">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-3269">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3269">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-3270">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3270">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-3271">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-3271">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-3272">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3272">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-3273">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3273">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-3274">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3274">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-3275">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3275">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-3276">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3276">fx_unicode_directory_rename</span></span>

## <a name="fx_unicode_directory_rename"></a><span data-ttu-id="8ac81-3277">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3277">fx_unicode_directory_rename</span></span>

<span data-ttu-id="8ac81-3278">Unicode dizesini kullanarak dizini yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3278">Renames directory using Unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3279">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3279">Prototype</span></span>

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-3280">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3280">Description</span></span>

<span data-ttu-id="8ac81-3281">Bu hizmet, Unicode adlı bir alt dizini geçerli çalışma dizininde belirtilen yeni Unicode adına değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3281">This service changes a Unicode-named subdirectory to specified new Unicode name in current working directory.</span></span> <span data-ttu-id="8ac81-3282">Unicode ad parametreleri yol bilgilerine sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3282">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3283">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3283">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3284">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3284">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3285">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3285">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3286">**old_unicode_name**: geçerli dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3286">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="8ac81-3287">**old_unicode_name_length**: geçerli Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3287">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="8ac81-3288">**new_unicode_name**: yeni Unicode dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3288">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="8ac81-3289">**old_unicode_name_length**: yeni Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3289">**old_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="8ac81-3290">**new_short_name**: yeniden adlandırılan Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3290">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span> <span data-ttu-id="8ac81-3291">Dizini Unicode ile yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="8ac81-3291">Rename Directory with Unicode</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3292">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3292">Return Values</span></span>

- <span data-ttu-id="8ac81-3293">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3293">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="8ac81-3294">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3294">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3295">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3295">**FX_ALREADY_CREATED** (0x0B) Specified directory name already exists.</span></span>
- <span data-ttu-id="8ac81-3296">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3296">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3297">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3297">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="8ac81-3298">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3298">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="8ac81-3299">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3299">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3300">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3300">Allowed From</span></span>

<span data-ttu-id="8ac81-3301">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3302">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3302">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3303">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3303">See Also</span></span>

- <span data-ttu-id="8ac81-3304">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3304">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8ac81-3305">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3305">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8ac81-3306">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3306">fx_directory_create</span></span>
- <span data-ttu-id="8ac81-3307">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3307">fx_directory_default_get</span></span>
- <span data-ttu-id="8ac81-3308">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3308">fx_directory_default_set</span></span>
- <span data-ttu-id="8ac81-3309">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3309">fx_directory_delete</span></span>
- <span data-ttu-id="8ac81-3310">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3310">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8ac81-3311">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3311">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8ac81-3312">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3312">fx_directory_information_get</span></span>
- <span data-ttu-id="8ac81-3313">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8ac81-3313">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8ac81-3314">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3314">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8ac81-3315">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8ac81-3315">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8ac81-3316">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3316">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8ac81-3317">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3317">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8ac81-3318">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8ac81-3318">fx_directory_name_test</span></span>
- <span data-ttu-id="8ac81-3319">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3319">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8ac81-3320">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8ac81-3320">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8ac81-3321">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3321">fx_directory_rename</span></span>
- <span data-ttu-id="8ac81-3322">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3322">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8ac81-3323">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3323">fx_unicode_directory_create</span></span>

## <a name="fx_unicode_file_create"></a><span data-ttu-id="8ac81-3324">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3324">fx_unicode_file_create</span></span>

<span data-ttu-id="8ac81-3325">Unicode dosyası oluşturur</span><span class="sxs-lookup"><span data-stu-id="8ac81-3325">Creates a Unicode file</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3326">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3326">Prototype</span></span>

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-3327">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3327">Description</span></span>

<span data-ttu-id="8ac81-3328">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya oluşturur; Unicode kaynak adı parametresinde yol bilgilerine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3328">This service creates a Unicode-named file in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="8ac81-3329">Başarılı olursa, yeni oluşturulan Unicode dosyasının kısa adı (8.3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3329">If successful, the short name (8.3 format) of the newly created Unicode file is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="8ac81-3330">*Unicode dosyasındaki tüm işlemler (açma, yazma, okuma, kapatma, vb.) standart FileX dosya hizmetlerine döndürülen kısa adı (8.3 biçimi) sağlamakla yapılır.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3330">*All operations on the Unicode file (opening, writing, reading, closing, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX file services.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3331">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3331">Input Parameters</span></span>


- <span data-ttu-id="8ac81-3332">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3332">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3333">**source_unicode_name:** Yeni dosya için Unicode adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3333">**source_unicode_name**: Pointer to the Unicode name for the new file.</span></span>
- <span data-ttu-id="8ac81-3334">**source_unicode_length:** Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3334">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8ac81-3335">**short_name:** Yeni Unicode dosyası için kısa ad (8.3 biçimi) için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3335">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3336">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3336">Return Values</span></span>

- <span data-ttu-id="8ac81-3337">**FX_SUCCESS** (0x00) Başarılı dosya oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3337">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="8ac81-3338">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3338">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3339">**FX_ALREADY_CREATED** (0x0B) Belirtilen dosya zaten var.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3339">**FX_ALREADY_CREATED** (0x0B) Specified file already exists.</span></span>
- <span data-ttu-id="8ac81-3340">**FX_NO_MORE_SPACE** (0x0A) Yeni dosya girişi için medyada artık kullanılabilir küme yok.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3340">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new file entry.</span></span>
- <span data-ttu-id="8ac81-3341">**FX_NOT_IMPLEMENTED** (0x22) Hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3341">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8ac81-3342">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3342">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3343">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3343">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8ac81-3344">**FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3344">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8ac81-3345">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3345">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3346">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3346">Allowed From</span></span>

<span data-ttu-id="8ac81-3347">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3347">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3348">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3348">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3349">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3349">See Also</span></span>

- <span data-ttu-id="8ac81-3350">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3350">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3351">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3351">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3352">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3352">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3353">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3353">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3354">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3354">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3355">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3355">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3356">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3356">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3357">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3357">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3358">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3358">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3359">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3359">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3360">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3360">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3361">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3361">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3362">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3362">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3363">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3363">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3364">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3364">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3365">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3365">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3366">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3366">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3367">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3367">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3368">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3368">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3369">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3369">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3370">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3370">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3371">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3371">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3372">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3372">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3373">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3373">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-3374">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3374">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-3375">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3375">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_file_rename"></a><span data-ttu-id="8ac81-3376">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3376">fx_unicode_file_rename</span></span>

<span data-ttu-id="8ac81-3377">Unicode dizesini kullanarak dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3377">Renames a file using unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3378">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3378">Prototype</span></span>

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a><span data-ttu-id="8ac81-3379">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3379">Description</span></span>

<span data-ttu-id="8ac81-3380">Bu hizmet, Unicode adlı bir dosya adını geçerli varsayılan dizinde belirtilen yeni Unicode adıyla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3380">This service changes a Unicode-named file name to specified new Unicode name in current default directory.</span></span> <span data-ttu-id="8ac81-3381">Unicode ad parametrelerinin yol bilgilerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3381">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3382">*Bu hizmet exFAT medyası üzerinde desteklenmiyor.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3382">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3383">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3383">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3384">**media_ptr:** Medya denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3384">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3385">**old_unicode_name:** Geçerli dosyanın Unicode adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3385">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="8ac81-3386">**old_unicode_name_length:** Geçerli Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3386">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="8ac81-3387">**new_unicode_name:** Yeni Unicode dosya adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3387">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="8ac81-3388">**new_unicode_name_length:** Yeni Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3388">**new_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="8ac81-3389">**new_short_name:** Yeniden adlandırılan Unicode dosyası için kısa ad (8.3 biçimi) için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3389">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3390">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3390">Return Values</span></span>


- <span data-ttu-id="8ac81-3391">**FX_SUCCESS** (0x00) Başarılı medya açma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3391">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="8ac81-3392">**FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3392">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3393">**FX_ALREADY_CREATED** (0x0B) Belirtilen dosya adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3393">**FX_ALREADY_CREATED** (0x0B) Specified file name already exists.</span></span>
- <span data-ttu-id="8ac81-3394">**FX_IO_ERROR** (0x90) Sürücü Ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3394">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3395">**FX_PTR_ERROR** (0x18) Bir veya daha fazla işaretçi NULL olur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3395">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="8ac81-3396">**FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3396">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="8ac81-3397">**FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3397">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3398">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3398">Allowed From</span></span>

<span data-ttu-id="8ac81-3399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3400">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3400">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3401">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3401">See Also</span></span>

- <span data-ttu-id="8ac81-3402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3402">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3403">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3404">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3406">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3407">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3408">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3409">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3413">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3416">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3417">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3418">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3419">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3420">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3421">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3422">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3423">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3424">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3424">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3425">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3425">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-3426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3426">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-3427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3427">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get"></a><span data-ttu-id="8ac81-3428">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3428">fx_unicode_length_get</span></span>

<span data-ttu-id="8ac81-3429">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3429">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3430">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3430">Prototype</span></span>

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a><span data-ttu-id="8ac81-3431">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3431">Description</span></span>

<span data-ttu-id="8ac81-3432">Bu hizmet, sağlanan Unicode adının uzunluğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3432">This service determines the length of the supplied Unicode name.</span></span> <span data-ttu-id="8ac81-3433">Bir Unicode karakteri iki bayt ile temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3433">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="8ac81-3434">Unicode adı, iki NULL bayt (0 değeri iki bayt) tarafından sonlandırılan iki baytlık Unicode karakter dizisidir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3434">A Unicode name is a series of two byte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3435">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3435">Input Parameters</span></span>

<span data-ttu-id="8ac81-3436">**unicode_name:** Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3436">**unicode_name**: Pointer to Unicode name.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3437">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3437">Return Values</span></span>

<span data-ttu-id="8ac81-3438">**length:** Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3438">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3439">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3439">Allowed From</span></span>

<span data-ttu-id="8ac81-3440">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3440">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3441">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3441">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3442">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3442">See Also</span></span>

- <span data-ttu-id="8ac81-3443">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3443">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3444">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3444">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3445">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3445">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3446">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3446">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3447">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3447">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3448">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3448">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3449">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3449">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3450">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3450">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3451">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3451">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3452">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3452">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3453">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3453">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3454">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3454">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3455">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3455">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3456">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3456">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3457">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3457">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3458">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3458">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3459">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3459">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3460">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3460">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3461">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3461">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3462">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3462">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3463">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3463">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3464">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3464">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3465">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3465">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3466">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3466">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-3467">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3467">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-3468">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3468">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-3469">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3469">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get_extended"></a><span data-ttu-id="8ac81-3470">fx_unicode_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="8ac81-3470">fx_unicode_length_get_extended</span></span>

<span data-ttu-id="8ac81-3471">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3471">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3472">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3472">Prototype</span></span>

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a><span data-ttu-id="8ac81-3473">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3473">Description</span></span>

<span data-ttu-id="8ac81-3474">Bu hizmet, sağlanan Unicode adının uzunluğunu alır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3474">This service gets the length of the supplied Unicode name.</span></span> <span data-ttu-id="8ac81-3475">Bir Unicode karakteri iki bayt ile temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3475">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="8ac81-3476">Unicode adı, iki NULL bayt (0 değeri iki bayt) tarafından sonlandırılan iki baytlık Unicode karakter dizisidir.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3476">A Unicode name is a series of twobyte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3477">*Bu hizmet **fx_unicode_length_get()** ile aynıdır ancak çağıranın iki NULL karakter dahil olmak **üzere unicode_name** arabelleğinin boyutunu geçerse.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3477">*This service is identical to **fx_unicode_length_get()** except the caller passes in the size of the **unicode_name** buffer, including the two NULL characters.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3478">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3478">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3479">**unicode_name:** Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3479">**unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="8ac81-3480">**buffer_length:** Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3480">**buffer_length**: Size of Unicode name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3481">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3481">Return Values</span></span>

<span data-ttu-id="8ac81-3482">**length:** Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3482">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3483">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3483">Allowed From</span></span>

<span data-ttu-id="8ac81-3484">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3484">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3485">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3485">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3486">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3486">See Also</span></span>

- <span data-ttu-id="8ac81-3487">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3487">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3488">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3488">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3489">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3489">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3490">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3490">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3491">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3491">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3492">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3492">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3493">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3493">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3494">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3494">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3495">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3495">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3496">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3496">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3497">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3497">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3498">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3498">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3499">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3499">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3500">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3500">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3501">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3501">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3502">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3502">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3503">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3503">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3504">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3504">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3505">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3505">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3506">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3506">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3507">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3507">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3508">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3508">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3509">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3509">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3510">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3510">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-3511">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3511">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-3512">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3512">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-3513">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3513">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get"></a><span data-ttu-id="8ac81-3514">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3514">fx_unicode_name_get</span></span>

<span data-ttu-id="8ac81-3515">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3515">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3516">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3516">Prototype</span></span>

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a><span data-ttu-id="8ac81-3517">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3517">Description</span></span>

<span data-ttu-id="8ac81-3518">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3518">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="8ac81-3519">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3519">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3520">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3520">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3521">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3521">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3522">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3522">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3523">**short_name** Kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3523">**short_name** Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="8ac81-3524">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3524">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="8ac81-3525">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3525">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3526">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3526">Return Values</span></span>

- <span data-ttu-id="8ac81-3527">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3527">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="8ac81-3528">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3528">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8ac81-3529">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-3529">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-3530">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3531">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3531">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3532">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3532">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="8ac81-3533">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3533">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-3534">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3534">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8ac81-3535">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3535">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3536">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3536">Allowed From</span></span>

<span data-ttu-id="8ac81-3537">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3537">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3538">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3538">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3539">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3539">See Also</span></span>

- <span data-ttu-id="8ac81-3540">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3540">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3541">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3541">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3542">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3542">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3543">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3543">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3544">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3544">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3545">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3545">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3546">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3546">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3547">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3547">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3548">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3548">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3549">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3549">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3550">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3550">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3551">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3551">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3552">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3552">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3553">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3553">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3554">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3554">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3555">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3555">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3556">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3556">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3557">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3557">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3558">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3558">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3559">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3559">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3560">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3560">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3561">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3561">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3562">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3562">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3563">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3563">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-3564">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3564">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-3565">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3565">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get_extended"></a><span data-ttu-id="8ac81-3566">fx_unicode_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8ac81-3566">fx_unicode_name_get_extended</span></span>

<span data-ttu-id="8ac81-3567">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3567">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3568">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3568">Prototype</span></span>

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a><span data-ttu-id="8ac81-3569">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3569">Description</span></span>

<span data-ttu-id="8ac81-3570">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3570">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="8ac81-3571">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3571">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3572">\* Bu hizmet,_çağıran, hedef Unicode arabelleğinin bir giriş bağımsız değişkeni olarak boyutunu sağladığı sürece \* fx_unicode_name_get aynıdır. Bu, hizmetin hedef Unicode arabelleğinin üzerine yazmayacağı garantisi sağlamasına izin verir_</span><span class="sxs-lookup"><span data-stu-id="8ac81-3572">\*This service is identical to \***fx_unicode_name_get**_, except the caller supplies the size of the destination Unicode buffer as an input argument. This allows the service to guarantee that it will not overwrite the destination Unicode buffer_</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3573">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3573">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3574">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3574">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3575">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3575">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3576">**short_name**: kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="8ac81-3576">**short_name**: Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="8ac81-3577">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3577">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="8ac81-3578">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3578">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>
- <span data-ttu-id="8ac81-3579">**unicode_name_buffer_length**: Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3579">**unicode_name_buffer_length**: Size of the Unicode name buffer.</span></span> <span data-ttu-id="8ac81-3580">Note: bir NULL Sonlandırıcı gereklidir ve bu da ek bir bayt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3580">Note: A NULL terminator is required, which makes an extra byte.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3581">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3581">Return Values</span></span>

- <span data-ttu-id="8ac81-3582">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3582">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="8ac81-3583">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3583">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8ac81-3584">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-3584">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-3585">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3585">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3586">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3586">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3587">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3587">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="8ac81-3588">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3588">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-3589">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3589">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8ac81-3590">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3590">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3591">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3591">Allowed From</span></span>

<span data-ttu-id="8ac81-3592">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3592">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3593">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3593">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3594">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3594">See Also</span></span>

- <span data-ttu-id="8ac81-3595">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3595">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3596">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3596">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3597">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3597">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3598">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3598">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3599">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3599">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3600">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3600">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3601">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3601">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3602">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3602">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3603">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3603">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3604">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3604">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3605">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3605">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3606">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3606">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3607">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3607">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3608">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3608">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3609">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3609">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3610">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3610">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3611">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3611">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3612">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3612">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3613">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3613">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3614">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3614">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3615">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3615">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3616">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3616">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3617">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3617">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3618">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3618">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-3619">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3619">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-3620">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3620">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_short_name_get"></a><span data-ttu-id="8ac81-3621">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3621">fx_unicode_short_name_get</span></span>

<span data-ttu-id="8ac81-3622">Unicode adından kısa adı alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3622">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3623">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3623">Prototype</span></span>

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

<span data-ttu-id="8ac81-3624">Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3624">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="8ac81-3625">Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3625">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3626">*Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3626">*This service can be used to get short names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3627">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3627">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3628">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3628">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3629">**source_unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3629">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="8ac81-3630">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3630">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8ac81-3631">**destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3631">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="8ac81-3632">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3632">This must be at least 13 bytes in size.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3633">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3633">Return Values</span></span>

- <span data-ttu-id="8ac81-3634">**FX_SUCCESS** (0x00) başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3634">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="8ac81-3635">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3635">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8ac81-3636">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-3636">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8ac81-3637">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3637">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3638">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3638">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3639">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3639">**FX_NOT_FOUND** (0x04)    Unicode name was not found.</span></span>
- <span data-ttu-id="8ac81-3640">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3640">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8ac81-3641">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3641">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-3642">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3642">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8ac81-3643">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3643">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3644">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3644">Allowed From</span></span>

<span data-ttu-id="8ac81-3645">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3645">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3646">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3646">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3647">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3647">See Also</span></span>

- <span data-ttu-id="8ac81-3648">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3648">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3649">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3649">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3650">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3650">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3651">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3651">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3652">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3652">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3653">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3653">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3654">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3654">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3655">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3655">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3656">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3656">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3657">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3657">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3658">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3658">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3659">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3659">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3660">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3660">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3661">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3661">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3662">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3662">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3663">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3663">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3664">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3664">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3665">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3665">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3666">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3666">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3667">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3667">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3668">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3668">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3669">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3669">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3670">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3670">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3671">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3671">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-3672">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3672">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-3673">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3673">fx_unicode_name_get</span></span>

## <a name="fx_unicode_short_name_get_extended"></a><span data-ttu-id="8ac81-3674">fx_unicode_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8ac81-3674">fx_unicode_short_name_get_extended</span></span>

<span data-ttu-id="8ac81-3675">Unicode adından kısa adı alır</span><span class="sxs-lookup"><span data-stu-id="8ac81-3675">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8ac81-3676">Prototype</span><span class="sxs-lookup"><span data-stu-id="8ac81-3676">Prototype</span></span>

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="8ac81-3677">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ac81-3677">Description</span></span>

<span data-ttu-id="8ac81-3678">Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3678">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="8ac81-3679">Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3679">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ac81-3680">*Çağıran, hedef arabelleğin bir giriş bağımsız değişkeni olarak boyutunu sağladığı, bu hizmet **fx_unicode_short_name_get ()** ile aynıdır. Bu, hizmetin kısa adı hedef arabelleği aşmadığını garanti etmesine olanak tanır.*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3680">*This service is identical to **fx_unicode_short_name_get()**, except the caller supplies the size of the destination buffer as an input argument. This allows the service to guarantee the short name does not exceed the destination buffer.*</span></span>

<span data-ttu-id="8ac81-3681">*Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="8ac81-3681">*This service can be used to get short names for both files and subdirectories*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8ac81-3682">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3682">Input Parameters</span></span>

- <span data-ttu-id="8ac81-3683">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3683">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8ac81-3684">**source_unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3684">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="8ac81-3685">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3685">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8ac81-3686">**destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3686">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="8ac81-3687">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3687">This must be at least 13 bytes in size.</span></span>
- <span data-ttu-id="8ac81-3688">**short_name_buffer_length**: hedef arabelleğin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3688">**short_name_buffer_length**: Size of the destination buffer.</span></span> <span data-ttu-id="8ac81-3689">Arabellek boyutu en az 14 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3689">The buffer size must be at least 14 bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="8ac81-3690">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8ac81-3690">Return Values</span></span>

- <span data-ttu-id="8ac81-3691">**FX_SUCCESS** (0x00) başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3691">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="8ac81-3692">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3692">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8ac81-3693">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8ac81-3693">**FX_FILE_CORRUPT** (0x08)    File is corrupted</span></span>
- <span data-ttu-id="8ac81-3694">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3694">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8ac81-3695">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3695">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8ac81-3696">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3696">**FX_NOT_FOUND** (0x04) Unicode name was not found.</span></span>
- <span data-ttu-id="8ac81-3697">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3697">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8ac81-3698">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3698">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8ac81-3699">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3699">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8ac81-3700">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3700">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8ac81-3701">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8ac81-3701">Allowed From</span></span>

<span data-ttu-id="8ac81-3702">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8ac81-3702">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8ac81-3703">Örnek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3703">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8ac81-3704">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8ac81-3704">See Also</span></span>

- <span data-ttu-id="8ac81-3705">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3705">fx_file_allocate</span></span>
- <span data-ttu-id="8ac81-3706">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3706">fx_file_attributes_read</span></span>
- <span data-ttu-id="8ac81-3707">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3707">fx_file_attributes_set</span></span>
- <span data-ttu-id="8ac81-3708">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3708">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3709">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8ac81-3709">fx_file_close</span></span>
- <span data-ttu-id="8ac81-3710">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3710">fx_file_create</span></span>
- <span data-ttu-id="8ac81-3711">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3711">fx_file_date_time_set</span></span>
- <span data-ttu-id="8ac81-3712">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8ac81-3712">fx_file_delete</span></span>
- <span data-ttu-id="8ac81-3713">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3713">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8ac81-3714">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3714">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8ac81-3715">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3715">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8ac81-3716">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3716">fx_file_extended_seek</span></span>
- <span data-ttu-id="8ac81-3717">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3717">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8ac81-3718">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3718">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8ac81-3719">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8ac81-3719">fx_file_open</span></span>
- <span data-ttu-id="8ac81-3720">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8ac81-3720">fx_file_read</span></span>
- <span data-ttu-id="8ac81-3721">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3721">fx_file_relative_seek</span></span>
- <span data-ttu-id="8ac81-3722">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3722">fx_file_rename</span></span>
- <span data-ttu-id="8ac81-3723">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8ac81-3723">fx_file_seek</span></span>
- <span data-ttu-id="8ac81-3724">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8ac81-3724">fx_file_truncate</span></span>
- <span data-ttu-id="8ac81-3725">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8ac81-3725">fx_file_truncate_release</span></span>
- <span data-ttu-id="8ac81-3726">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8ac81-3726">fx_file_write</span></span>
- <span data-ttu-id="8ac81-3727">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8ac81-3727">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8ac81-3728">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8ac81-3728">fx_unicode_file_create</span></span>
- <span data-ttu-id="8ac81-3729">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8ac81-3729">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8ac81-3730">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3730">fx_unicode_name_get</span></span>
- <span data-ttu-id="8ac81-3731">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8ac81-3731">fx_unicode_short_name_get</span></span>
