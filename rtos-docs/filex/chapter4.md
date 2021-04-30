---
title: Bölüm 4-Azure RTOS FileX hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS FileX hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f70b8890be6b12f917ac1724a29559afab33b88d
ms.sourcegitcommit: 0520b2afb6b7f8ae1ea48581e160459fc9292ca7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/30/2021
ms.locfileid: "108297505"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a><span data-ttu-id="a8f47-103">Bölüm 4-Azure RTOS FileX hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="a8f47-103">Chapter 4- Description of Azure RTOS FileX services</span></span>

<span data-ttu-id="a8f47-104">Bu bölüm, tüm Azure RTOS FileX hizmetlerinin alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-104">This chapter contains a description of all Azure RTOS FileX services in alphabetic order.</span></span> <span data-ttu-id="a8f47-105">Hizmet adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-105">Service names are designed so all similar services are grouped together.</span></span>

## <a name="fx_directory_attributes_read"></a><span data-ttu-id="a8f47-106">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-106">fx_directory_attributes_read</span></span>

<span data-ttu-id="a8f47-107">Dizin özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="a8f47-107">Reads directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-108">Prototype</span></span>

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a><span data-ttu-id="a8f47-109">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-109">Description</span></span>

<span data-ttu-id="a8f47-110">Bu hizmet, dizinin özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-110">This service reads the directory's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-111">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-111">Input Parameters</span></span>

- <span data-ttu-id="a8f47-112">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-112">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-113">**directory_name**: istenen dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-113">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="a8f47-114">**öznitelikler** _Ptr: dizin özniteliklerinin yerleştirileceği hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-114">**attributes** _ptr: Pointer to the destination for the directory's attributes to be placed.</span></span> <span data-ttu-id="a8f47-115">Dizin öznitelikleri, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="a8f47-115">The directory attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="a8f47-116">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-116">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="a8f47-117">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-117">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="a8f47-118">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="a8f47-118">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="a8f47-119">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="a8f47-119">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="a8f47-120">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="a8f47-120">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="a8f47-121">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="a8f47-121">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-122">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-122">Return Values</span></span>

- <span data-ttu-id="a8f47-123">**FX_SUCCESS** (0x00) başarılı dizin öznitelikleri okundu</span><span class="sxs-lookup"><span data-stu-id="a8f47-123">**FX_SUCCESS** (0x00) Successful directory attributes read</span></span>
- <span data-ttu-id="a8f47-124">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-124">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-125">**FX _NOT bulunan** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a8f47-125">**FX _NOT FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="a8f47-126">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-126">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="a8f47-127">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-127">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-128">**FX_FILE_CORRUPT** 0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-128">**FX_FILE_CORRUPT** 0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-129">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-129">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-130">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-130">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-131">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-131">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-132">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="a8f47-132">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="a8f47-133">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-133">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="a8f47-134">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-134">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-135">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-135">Allowed From</span></span>

<span data-ttu-id="a8f47-136">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-136">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-137">Example</span></span>

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-138">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-138">See Also</span></span>

- <span data-ttu-id="a8f47-139">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-139">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-140">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-140">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-141">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-141">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-142">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-142">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-143">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-143">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-144">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-144">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-145">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-145">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-146">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-146">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-147">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-147">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-148">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-148">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-149">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-149">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-150">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-150">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-151">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-151">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-152">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-152">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-153">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-153">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-154">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-154">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-155">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-155">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-156">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-156">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-157">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-157">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-158">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-158">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_attributes_set"></a><span data-ttu-id="a8f47-159">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-159">fx_directory_attributes_set</span></span>

<span data-ttu-id="a8f47-160">Dizin özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-160">Sets directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-161">Prototype</span></span>

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a><span data-ttu-id="a8f47-162">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-162">Description</span></span>

<span data-ttu-id="a8f47-163">Bu hizmet, dizinin özniteliklerini çağıran tarafından belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-163">This service sets the directory's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-164">*Bu uygulamanın yalnızca bu hizmetle dizin özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlamaya yönelik her türlü girişim bir hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-164">*This application is only allowed to modify a subset of the directory's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-165">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-165">Input Parameters</span></span>

- <span data-ttu-id="a8f47-166">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-166">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-167">**directory_name**: istenen dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-167">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="a8f47-168">**öznitelikler**: bu dizine yönelik yeni öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-168">**attributes**: The new attributes to this directory.</span></span> <span data-ttu-id="a8f47-169">Geçerli dizin öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-169">The valid directory attributes are defined as follows:</span></span>
  - <span data-ttu-id="a8f47-170">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-170">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="a8f47-171">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-171">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="a8f47-172">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="a8f47-172">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="a8f47-173">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="a8f47-173">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-174">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-174">Return Values</span></span>

- <span data-ttu-id="a8f47-175">**FX_SUCCESS** (0x00) başarılı Dizin öznitelik kümesi</span><span class="sxs-lookup"><span data-stu-id="a8f47-175">**FX_SUCCESS** (0x00) Successful directory attribute set</span></span>
- <span data-ttu-id="a8f47-176">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-176">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-177">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a8f47-177">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="a8f47-178">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-178">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="a8f47-179">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-179">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-180">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="a8f47-180">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="a8f47-181">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-181">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-182">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-182">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-183">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-183">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-184">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-184">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-185">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="a8f47-185">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="a8f47-186">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-186">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="a8f47-187">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-187">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="a8f47-188">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-188">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="a8f47-189">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-190">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-190">Allowed From</span></span>

<span data-ttu-id="a8f47-191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-192">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-192">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-193">See Also</span></span>

- <span data-ttu-id="a8f47-194">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-194">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-195">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-195">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-196">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-196">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-197">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-197">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-198">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-198">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-199">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-199">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-200">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-200">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-201">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-201">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-202">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-202">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-203">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-203">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-204">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-204">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-205">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-205">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-206">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-206">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-207">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-207">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-208">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-208">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-209">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-209">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-210">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-210">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-211">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-211">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-212">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-212">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-213">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-213">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_create"></a><span data-ttu-id="a8f47-214">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-214">fx_directory_create</span></span>

<span data-ttu-id="a8f47-215">Alt dizin oluşturur</span><span class="sxs-lookup"><span data-stu-id="a8f47-215">Creates subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-216">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-216">Prototype</span></span>

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-217">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-217">Description</span></span>

<span data-ttu-id="a8f47-218">Bu hizmet, geçerli varsayılan dizinde veya dizin adında sağlanan yolda bir alt dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-218">This service creates a subdirectory in the current default directory or in the path supplied in the directory name.</span></span> <span data-ttu-id="a8f47-219">Kök dizinden farklı olarak, alt dizinlerin tutabilecekleri dosya sayısı için bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-219">Unlike the root directory, subdirectories do not have a limit on the number of files they can hold.</span></span> <span data-ttu-id="a8f47-220">Kök dizin yalnızca önyükleme kaydı tarafından belirlenen girdi sayısını tutabilirler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-220">The root directory can only hold the number of entries determined by the boot record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-221">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-221">Input Parameters</span></span>

- <span data-ttu-id="a8f47-222">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-222">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-223">**directory_name**: Oluşturulacak dizinin adına yönelik işaretçi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-223">**directory_name**: Pointer to the name of the directory to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-224">Return Values</span></span>

- <span data-ttu-id="a8f47-225">**FX_SUCCESS** (0x00) başarılı dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-225">**FX_SUCCESS** (0x00) Successful directory create.</span></span>
- <span data-ttu-id="a8f47-226">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-226">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-227">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a8f47-227">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="a8f47-228">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-228">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="a8f47-229">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-229">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-230">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-230">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-231">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-231">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-232">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-232">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-233">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-233">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-234">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="a8f47-234">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="a8f47-235">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-235">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="a8f47-236">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-236">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="a8f47-237">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-237">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="a8f47-238">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-238">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-239">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-239">Allowed From</span></span>

<span data-ttu-id="a8f47-240">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-240">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-241">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-242">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-242">See Also</span></span>

- <span data-ttu-id="a8f47-243">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-243">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-244">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-244">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-245">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-245">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-246">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-246">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-247">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-247">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-248">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-248">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-249">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-249">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-250">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-250">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-251">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-251">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-252">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-252">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-253">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-253">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-254">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-254">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-255">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-255">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-256">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-256">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-257">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-257">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-258">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-258">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-259">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-259">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-260">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-260">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-261">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-261">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-262">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-262">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_get"></a><span data-ttu-id="a8f47-263">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-263">fx_directory_default_get</span></span>

<span data-ttu-id="a8f47-264">Son varsayılan dizini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-264">Gets last default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-265">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-265">Prototype</span></span>

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-266">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-266">Description</span></span>

<span data-ttu-id="a8f47-267">Bu hizmet, ***fx_directory_default_set*** tarafından en son ayarlanan yola yönelik işaretçiyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-267">This service returns the pointer to the path last set by ***fx_directory_default_set***.</span></span> <span data-ttu-id="a8f47-268">Varsayılan dizin ayarlanmamışsa veya geçerli varsayılan dizin kök dizin ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-268">If the default directory has not been set or if the current default directory is the root directory, a value of FX_NULL is returned.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-269">*İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-269">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-270">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-270">Input Parameters</span></span>

- <span data-ttu-id="a8f47-271">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-271">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-272">**return_path_name**: son varsayılan dizin dizesinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-272">**return_path_name**: Pointer to the destination for the last default directory string.</span></span> <span data-ttu-id="a8f47-273">Varsayılan dizinin geçerli ayarı kök ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-273">A value of FX_NULL is returned if the current setting of the default directory is the root.</span></span> <span data-ttu-id="a8f47-274">Medya açıldığında, kök varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-274">When the media is opened, root is the default.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-275">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-275">Return Values</span></span>

- <span data-ttu-id="a8f47-276">**FX_SUCCESS** (0x00) başarılı varsayılan dizin Al</span><span class="sxs-lookup"><span data-stu-id="a8f47-276">**FX_SUCCESS** (0x00) Successful default directory get</span></span>
- <span data-ttu-id="a8f47-277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-278">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-278">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="a8f47-279">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-279">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-280">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-280">Allowed From</span></span>

<span data-ttu-id="a8f47-281">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-282">Example</span></span>

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a><span data-ttu-id="a8f47-283">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-283">See Also</span></span>

- <span data-ttu-id="a8f47-284">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-284">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-285">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-285">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-286">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-286">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-287">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-287">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-288">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-288">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-289">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-289">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-290">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-290">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-291">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-291">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-292">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-292">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-293">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-293">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-294">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-294">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-295">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-295">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-296">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-296">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-297">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-297">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-298">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-298">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-299">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-299">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-300">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-300">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-301">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-301">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-302">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-302">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-303">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-303">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_set"></a><span data-ttu-id="a8f47-304">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-304">fx_directory_default_set</span></span>

<span data-ttu-id="a8f47-305">Varsayılan dizini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-305">Sets default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-306">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-306">Prototype</span></span>

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-307">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-307">Description</span></span>

<span data-ttu-id="a8f47-308">Bu hizmet, medyanın varsayılan dizinini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-308">This service sets the default directory of the media.</span></span> <span data-ttu-id="a8f47-309">FX_NULL değeri sağlanırsa, varsayılan dizin medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-309">If a value of FX_NULL is supplied, the default directory is set to the media's root directory.</span></span> <span data-ttu-id="a8f47-310">Açıkça bir yol belirtmeyen tüm sonraki dosya işlemleri bu dizine varsayılan olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-310">All subsequent file operations that do not explicitly specify a path will default to this directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-311">*İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-311">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-312">*Uygulama tarafından sağlanan adlar için, FileX, \\ dizinler, alt dizinler ve dosya adlarına ayrı ters eğik çizgi () ve eğik çizgi (/) karakterlerini destekler. Ancak, FileX yalnızca uygulamaya döndürülen yollarda ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-312">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-313">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-313">Input Parameters</span></span>

- <span data-ttu-id="a8f47-314">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-314">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-315">**new_path_name**: yeni varsayılan dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-315">**new_path_name**: Pointer to new default directory name.</span></span> <span data-ttu-id="a8f47-316">Bir FX_NULL değeri sağlanırsa, medyanın varsayılan dizini medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-316">If a value of FX_NULL is supplied, the default directory of the media is set to the media's root directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-317">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-317">Return Values</span></span>

- <span data-ttu-id="a8f47-318">**FX_SUCCESS** (0x00) başarılı varsayılan dizin kümesi</span><span class="sxs-lookup"><span data-stu-id="a8f47-318">**FX_SUCCESS** (0x00)  Successful default directory set</span></span>
- <span data-ttu-id="a8f47-319">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-319">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-320">**FX_INVALID_PATH** (0x0D) yeni dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a8f47-320">**FX_INVALID_PATH** (0x0D) New directory could not be found</span></span>
- <span data-ttu-id="a8f47-321">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-321">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-322">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-322">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-323">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-323">Allowed From</span></span>

<span data-ttu-id="a8f47-324">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-324">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-325">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-325">Example</span></span>

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-326">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-326">See Also</span></span>

- <span data-ttu-id="a8f47-327">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-327">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-328">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-328">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-329">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-329">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-330">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-330">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-331">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-331">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-332">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-332">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-333">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-333">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-334">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-334">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-335">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-335">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-336">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-336">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-337">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-337">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-338">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-338">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-339">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-339">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-340">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-340">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-341">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-341">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-342">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-342">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-343">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-343">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-344">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-344">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-345">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-345">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-346">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-346">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_delete"></a><span data-ttu-id="a8f47-347">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-347">fx_directory_delete</span></span>

<span data-ttu-id="a8f47-348">Alt dizini siler</span><span class="sxs-lookup"><span data-stu-id="a8f47-348">Deletes subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-349">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-349">Prototype</span></span>

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-350">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-350">Description</span></span>

<span data-ttu-id="a8f47-351">Bu hizmet belirtilen dizini siler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-351">This service deletes the specified directory.</span></span> <span data-ttu-id="a8f47-352">Silmek için dizinin boş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a8f47-352">Note that the directory must be empty to delete it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-353">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-353">Input Parameters</span></span>

- <span data-ttu-id="a8f47-354">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-354">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-355">**directory_name**: silinecek dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-355">**directory_name**: Pointer to name of directory to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-356">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-356">Return Values</span></span>

- <span data-ttu-id="a8f47-357">**FX_SUCCESS** (0x00) başarılı dizin silme</span><span class="sxs-lookup"><span data-stu-id="a8f47-357">**FX_SUCCESS** (0x00) Successful directory delete</span></span>
- <span data-ttu-id="a8f47-358">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-358">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-359">**FX_NOT_FOUND** (0x04) belirtilen dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a8f47-359">**FX_NOT_FOUND** (0x04) Specified directory was not found</span></span>
- <span data-ttu-id="a8f47-360">**FX_DIR_NOT_EMPTY** (0x10) belirtilen dizin boş değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-360">**FX_DIR_NOT_EMPTY** (0x10) Specified directory is not empty</span></span>
- <span data-ttu-id="a8f47-361">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-361">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-362">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="a8f47-362">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="a8f47-363">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-363">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-364">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-364">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-365">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-365">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-366">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-366">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-367">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="a8f47-367">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="a8f47-368">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-368">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="a8f47-369">**FX_NOT_DIRECTORY** (0x0E) dizin girişi değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-369">**FX_NOT_DIRECTORY** (0x0E) Not a directory entry</span></span>
- <span data-ttu-id="a8f47-370">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-370">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="a8f47-371">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-371">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-372">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-372">Allowed From</span></span>

<span data-ttu-id="a8f47-373">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-373">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-374">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-374">Example</span></span>
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-375">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-375">See Also</span></span>

- <span data-ttu-id="a8f47-376">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-376">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-377">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-377">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-378">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-378">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-379">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-379">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-380">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-380">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-381">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-381">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-382">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-382">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-383">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-383">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-384">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-384">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-385">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-385">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-386">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-386">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-387">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-387">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-388">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-388">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-389">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-389">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-390">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-390">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-391">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-391">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-392">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-392">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-393">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-393">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-394">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-394">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-395">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-395">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_entry_find"></a><span data-ttu-id="a8f47-396">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-396">fx_directory_first_entry_find</span></span>

<span data-ttu-id="a8f47-397">İlk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-397">Gets first directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-398">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-398">Prototype</span></span>

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-399">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-399">Description</span></span>

<span data-ttu-id="a8f47-400">Bu hizmet, varsayılan dizindeki ilk giriş adını alır ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-400">This service retrieves the first entry name in the default directory and copies it to the specified destination.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-401">*Belirtilen hedef, FX_MAX_LONG_NAME_LEN tarafından tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır **.***</span><span class="sxs-lookup"><span data-stu-id="a8f47-401">*The specified destination must be large enough to hold the maximum sized FileX name, as defined by **FX_MAX_LONG_NAME_LEN.***</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-402">*Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-402">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-403">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-403">Input Parameters</span></span>

- <span data-ttu-id="a8f47-404">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-404">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-405">**return_entry_name**: varsayılan dizindeki ilk giriş adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-405">**return_entry_name**: Pointer to destination for the first entry name in the default directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-406">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-406">Return Values</span></span>

- <span data-ttu-id="a8f47-407">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="a8f47-407">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="a8f47-408">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-408">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-409">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-409">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="a8f47-410">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-410">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-411">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-411">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-412">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-412">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-413">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-413">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-414">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-414">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer</span></span>
- <span data-ttu-id="a8f47-415">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-415">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-416">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-416">Allowed From</span></span>

<span data-ttu-id="a8f47-417">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-417">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-418">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-418">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-419">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-419">See Also</span></span>

- <span data-ttu-id="a8f47-420">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-420">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-421">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-421">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-422">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-422">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-423">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-423">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-424">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-424">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-425">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-425">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-426">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-426">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-427">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-427">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-428">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-428">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-429">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-429">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-430">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-430">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-431">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-431">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-432">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-432">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-433">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-433">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-434">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-434">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-435">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-435">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-436">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-436">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-437">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-437">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-438">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-438">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-439">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-439">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="a8f47-440">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-440">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="a8f47-441">Tüm bilgileri içeren ilk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-441">Gets first directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-442">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-442">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="a8f47-443">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-443">Input Parameters</span></span>

- <span data-ttu-id="a8f47-444">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-444">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-445">**directory_name**: bir dizin girişi adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-445">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="a8f47-446">En az FX_MAX_LONG_NAME_LEN kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-446">Must be at least as big as FX_MAX_LONG_NAME_LEN.</span></span>
- <span data-ttu-id="a8f47-447">**öznitelikler**: null olmayan, girişin özniteliklerinin yerleştirileceği hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-447">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.</span></span> <span data-ttu-id="a8f47-448">Öznitelikler, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="a8f47-448">The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="a8f47-449">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-449">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="a8f47-450">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-450">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="a8f47-451">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="a8f47-451">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="a8f47-452">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="a8f47-452">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="a8f47-453">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="a8f47-453">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="a8f47-454">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="a8f47-454">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="a8f47-455">**Boyut**: null olmayan, girdinin bayt cinsinden boyutu için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-455">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="a8f47-456">**yıl**: null olmayan, girişin değiştirilme yılından hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-456">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="a8f47-457">**ay**: null olmayan, girişin değiştirilme ayı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-457">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="a8f47-458">**gün**: null olmayan, girişin değiştirilme günü için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-458">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="a8f47-459">**saat**: null olmayan, girişin değiştirilme saati için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-459">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="a8f47-460">**dakika**: null olmayan, girişin değiştirilme dakikası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-460">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="a8f47-461">**ikinci**: null olmayan, girişin değiştirilme saniyesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-461">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-462">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-462">Return Values</span></span>

- <span data-ttu-id="a8f47-463">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="a8f47-463">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="a8f47-464">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-464">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-465">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-465">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="a8f47-466">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-466">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-467">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="a8f47-467">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="a8f47-468">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-468">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-469">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-469">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-470">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-470">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-471">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-471">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-472">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="a8f47-472">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="a8f47-473">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-473">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="a8f47-474">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-474">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-475">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-475">Allowed From</span></span>

<span data-ttu-id="a8f47-476">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-476">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-477">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-477">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-478">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-478">See Also</span></span>

- <span data-ttu-id="a8f47-479">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-479">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-480">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-480">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-481">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-481">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-482">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-482">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-483">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-483">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-484">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-484">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-485">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-485">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-486">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-486">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-487">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-487">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-488">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-488">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-489">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-489">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-490">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-490">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-491">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-491">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-492">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-492">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-493">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-493">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-494">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-494">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-495">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-495">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-496">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-496">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-497">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-497">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-498">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-498">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_information_get"></a><span data-ttu-id="a8f47-499">fx_directory_information_get:</span><span class="sxs-lookup"><span data-stu-id="a8f47-499">fx_directory_information_get:</span></span>

<span data-ttu-id="a8f47-500">Dizin girişi bilgilerini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-500">Gets directory entry information</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-501">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-501">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="a8f47-502">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-502">Input Parameters</span></span>

- <span data-ttu-id="a8f47-503">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-503">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-504">**directory_name**: Dizin girişinin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-504">**directory_name**: Pointer to name of the directory entry.</span></span>
- <span data-ttu-id="a8f47-505">**öznitelikler**: özniteliklerin hedefe yönelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-505">**attributes**: Pointer to the destination for the attributes.</span></span>
- <span data-ttu-id="a8f47-506">**Boyut**: boyut için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-506">**size**: Pointer to the destination for the size.</span></span>
- <span data-ttu-id="a8f47-507">**Year**: yıl için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-507">**year**: Pointer to the destination for the year.</span></span>
- <span data-ttu-id="a8f47-508">**Month**: ayın hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-508">**month**: Pointer to the destination for the month.</span></span>
- <span data-ttu-id="a8f47-509">**Day**: günün hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-509">**day**: Pointer to the destination for the day.</span></span>
- <span data-ttu-id="a8f47-510">**saat**: saat için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-510">**hour**: Pointer to the destination for the hour.</span></span>
- <span data-ttu-id="a8f47-511">**Minute**: dakika için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-511">**minute**: Pointer to the destination for the minute.</span></span>
- <span data-ttu-id="a8f47-512">**ikinci**: ikincisi için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-512">**second**: Pointer to the destination for the second.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-513">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-513">Return Values</span></span>

- <span data-ttu-id="a8f47-514">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="a8f47-514">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="a8f47-515">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-515">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-516">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a8f47-516">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="a8f47-517">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-517">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-518">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="a8f47-518">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="a8f47-519">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-519">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-520">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-520">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-521">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-521">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-522">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-522">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-523">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-523">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="a8f47-524">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-524">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-525">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-525">Allowed From</span></span>

<span data-ttu-id="a8f47-526">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-526">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-527">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-527">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-528">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-528">See Also</span></span>

- <span data-ttu-id="a8f47-529">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-529">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-530">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-530">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-531">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-531">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-532">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-532">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-533">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-533">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-534">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-534">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-535">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-535">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-536">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-536">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-537">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-537">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-538">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-538">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-539">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-539">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-540">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-540">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-541">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-541">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-542">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-542">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-543">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-543">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-544">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-544">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-545">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-545">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-546">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-546">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-547">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-547">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-548">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-548">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_clear"></a><span data-ttu-id="a8f47-549">fx_directory_local_path_clear:</span><span class="sxs-lookup"><span data-stu-id="a8f47-549">fx_directory_local_path_clear:</span></span>

<span data-ttu-id="a8f47-550">Varsayılan yerel yolu temizler</span><span class="sxs-lookup"><span data-stu-id="a8f47-550">Clears default local path</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-551">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-551">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="a8f47-552">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-552">Description</span></span>

<span data-ttu-id="a8f47-553">Bu hizmet, çağıran iş parçacığı için ayarlanan önceki yerel yolu temizler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-553">This service clears the previous local path set up for the calling thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-554">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-554">Input Parameters</span></span>

- <span data-ttu-id="a8f47-555">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-555">**media_ptr**: Pointer to a previously opened media.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-556">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-556">Return Values</span></span>

- <span data-ttu-id="a8f47-557">**FX_SUCCESS** (0x00) başarılı yerel yol temizleme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-557">**FX_SUCCESS** (0x00) Successful local path clear.</span></span>
- <span data-ttu-id="a8f47-558">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-558">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="a8f47-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlandı</span><span class="sxs-lookup"><span data-stu-id="a8f47-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined</span></span>
- <span data-ttu-id="a8f47-560">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-560">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-561">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-561">Allowed From</span></span>

<span data-ttu-id="a8f47-562">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-562">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-563">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-563">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-564">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-564">See Also</span></span>

- <span data-ttu-id="a8f47-565">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-565">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-566">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-566">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-567">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-567">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-568">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-568">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-569">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-569">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-570">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-570">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-571">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-571">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-572">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-572">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-573">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-573">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-574">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-574">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-575">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-575">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-576">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-576">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-577">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-577">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-578">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-578">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-579">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-579">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-580">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-580">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-581">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-581">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-582">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-582">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-583">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-583">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-584">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-584">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_get"></a><span data-ttu-id="a8f47-585">fx_directory_local_path_get:</span><span class="sxs-lookup"><span data-stu-id="a8f47-585">fx_directory_local_path_get:</span></span>

<span data-ttu-id="a8f47-586">Geçerli yerel yol dizesini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-586">Gets the current local path string</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-587">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-587">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-588">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-588">Description</span></span>

<span data-ttu-id="a8f47-589">Bu hizmet, belirtilen medyanın yerel yol işaretçisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-589">This service returns the local path pointer of the specified media.</span></span> <span data-ttu-id="a8f47-590">Yerel bir yol ayarlanmamışsa, çağırana bir NULL döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-590">If there is no local path set, a NULL is returned to the caller.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-591">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-591">Input Parameters</span></span>

- <span data-ttu-id="a8f47-592">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-592">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-593">**return_path_name**: yerel yol dizesinin depolanacağı hedef dize işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-593">**return_path_name**: Pointer to the destination string pointer for the local path string to be stored.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-594">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-594">Return Values</span></span>

- <span data-ttu-id="a8f47-595">**FX_SUCCESS** (0x00) başarılı yerel yol al.</span><span class="sxs-lookup"><span data-stu-id="a8f47-595">**FX_SUCCESS** (0x00) Successful local path get.</span></span>
- <span data-ttu-id="a8f47-596">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-596">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="a8f47-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="a8f47-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="a8f47-598">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-598">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>


### <a name="allowed-from"></a><span data-ttu-id="a8f47-599">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-599">Allowed From</span></span>

<span data-ttu-id="a8f47-600">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-600">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-601">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-601">Example</span></span>

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-602">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-602">See Also</span></span>

- <span data-ttu-id="a8f47-603">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-603">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-604">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-604">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-605">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-605">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-606">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-606">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-607">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-607">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-608">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-608">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-609">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-609">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-610">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-610">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-611">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-611">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-612">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-612">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-613">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-613">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-614">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-614">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-615">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-615">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-616">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-616">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-617">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-617">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-618">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-618">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-619">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-619">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-620">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-620">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-621">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-621">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-622">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-622">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_restore"></a><span data-ttu-id="a8f47-623">fx_directory_local_path_restore:</span><span class="sxs-lookup"><span data-stu-id="a8f47-623">fx_directory_local_path_restore:</span></span>

<span data-ttu-id="a8f47-624">Önceki yerel yolu geri yükler</span><span class="sxs-lookup"><span data-stu-id="a8f47-624">Restores previous local path</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-625">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-625">Prototype</span></span>

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a><span data-ttu-id="a8f47-626">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-626">Description</span></span>

<span data-ttu-id="a8f47-627">Bu hizmet daha önce ayarlanmış bir yerel yolu geri yükler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-627">This service restores a previously set local path.</span></span> <span data-ttu-id="a8f47-628">Bu yerel yolda yapılan dizin arama konumu da geri yüklenir, bu da bu yordamı uygulama tarafından özyinelemeli Dizin traversals ' de yararlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-628">The directory search position made on this local path is also restored, which makes this routine useful in recursive directory traversals by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-629">*Her yerel yol, varsayılan olarak 256 karakter olan **FX_MAXIMUM_PATH** boyutunda bir yerel yol dizesi içerir. Bu iç yol dizesi FileX tarafından kullanılmaz ve yalnızca uygulamanın kullanımı için sağlanır. **FX_LOCAL_PATH** yerel bir değişken olarak bildiriecekse, kullanıcıların bu yapının boyutuyla büyüyen yığına dikkat etmesi gerekir. Kullanıcılar **FX_MAXIMUM_PATH** boyutunu azaltmak ve FileX kitaplık kaynağını yeniden derlemek için hoş geldiniz.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-629">*Each local path contains a local path string of **FX_MAXIMUM_PATH** in size, which by default is 256 characters. This internal path string is not used by FileX and is provided only for the application's use. If **FX_LOCAL_PATH** is going to be declared as a local variable, users should beware of the stack growing by the size of this structure. Users are welcome to reduce the size of **FX_MAXIMUM_PATH** and rebuild the FileX library source.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-630">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-630">Input Parameters</span></span>

- <span data-ttu-id="a8f47-631">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-631">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-632">**local_path_ptr**: daha önce ayarlanan yerel yola yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-632">**local_path_ptr**: Pointer to the previously set local path.</span></span> <span data-ttu-id="a8f47-633">Bu işaretçinin gerçekten daha önce kullanılmış ve bozulmadan yerel yola işaret ettiğinden emin olmak çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-633">It's very important to ensure that this pointer does indeed point to a previously used and still intact local path.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-634">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-634">Return Values</span></span>

- <span data-ttu-id="a8f47-635">**FX_SUCCESS** (0x00) başarılı yerel yol geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-635">**FX_SUCCESS** (0x00) Successful local path restore.</span></span>
- <span data-ttu-id="a8f47-636">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open.</span></span>
- <span data-ttu-id="a8f47-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined.</span></span>
- <span data-ttu-id="a8f47-638">**FX_PTR_ERROR** (0x18) geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-638">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-639">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-639">Allowed From</span></span>

<span data-ttu-id="a8f47-640">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-640">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-641">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-641">Example</span></span>

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-642">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-642">See Also</span></span>

- <span data-ttu-id="a8f47-643">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-643">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-644">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-644">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-645">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-645">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-646">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-646">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-647">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-647">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-648">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-648">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-649">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-649">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-650">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-650">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-651">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-651">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-652">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-652">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-653">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-653">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-654">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-654">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-655">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-655">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-656">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-656">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-657">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-657">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-658">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-658">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-659">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-659">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-660">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-660">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-661">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-661">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-662">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-662">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_set"></a><span data-ttu-id="a8f47-663">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-663">fx_directory_local_path_set</span></span>

<span data-ttu-id="a8f47-664">İş parçacığına özgü bir yerel yol ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-664">Sets up a thread-specific local path</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-665">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-665">Prototype</span></span>

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-666">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-666">Description</span></span>

<span data-ttu-id="a8f47-667">Bu hizmet, \***new_path_string** _ tarafından belirtilen bir iş parçacığına özgü yol ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-667">This service sets up a thread-specific path as specified by the \***new_path_string** _.</span></span> <span data-ttu-id="a8f47-668">Bu yordamın başarıyla tamamlanmasından sonra, _ *_local_path_ptr_*\* içinde depolanan yerel yol bilgileri, bu iş parçacığı tarafından yapılan tüm dosya ve dizin işlemleri için genel medya yolundan öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-668">After successful completion of this routine, the local path information stored in _ *_local_path_ptr_*\* will take precedence over the global media path for all file and directory operations made by this thread.</span></span> <span data-ttu-id="a8f47-669">Bu, sistemdeki diğer iş parçacıklarını etkilemez</span><span class="sxs-lookup"><span data-stu-id="a8f47-669">This will have no impact on any other thread in the system</span></span> 
> [!IMPORTANT]
> <span data-ttu-id="a8f47-670">*Yerel yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-670">*The default size of the local path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-671">*Uygulama tarafından sağlanan adlar için, FileX, \\ dizinler, alt dizinler ve dosya adlarına ayrı ters eğik çizgi () ve eğik çizgi (/) karakterlerini destekler. Ancak, FileX yalnızca uygulamaya döndürülen yollarda ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-671">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-672">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-672">Input Parameters</span></span>

- <span data-ttu-id="a8f47-673">**media_ptr**: daha önce açılmış medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-673">**media_ptr**: Pointer to the previously opened media.</span></span>
- <span data-ttu-id="a8f47-674">**local_path_ptr**: iş parçacığına özgü yerel yol bilgilerini tutmak için hedef.</span><span class="sxs-lookup"><span data-stu-id="a8f47-674">**local_path_ptr**: Destination for holding the thread-specific local path information.</span></span> <span data-ttu-id="a8f47-675">Bu yapının adresi gelecekte yerel yol geri yükleme işlevine sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-675">The address of this structure may be supplied to the local path restore function in the future.</span></span>
- <span data-ttu-id="a8f47-676">**new_path_name**: kurulumun yerel yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-676">**new_path_name**: Specifies the local path to setup.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-677">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-677">Return Values</span></span>

- <span data-ttu-id="a8f47-678">**FX_SUCCESS** (0x00) başarılı varsayılan dizin kümesi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-678">**FX_SUCCESS** (0x00) Successful default directory set.</span></span>
- <span data-ttu-id="a8f47-679">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-679">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-680">**FX_NOT_IMPLEMENTED** (0x22) \* \* FX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="a8f47-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="a8f47-681">**FX_INVALID_PATH** (0x0D) yeni dizin bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-681">**FX_INVALID_PATH** (0x0D) New directory could not be found.</span></span>
- <span data-ttu-id="a8f47-682">**FX_NOT_IMPLEMENTED** (0x22)-\* \* FX_NO_LOCAL_PATH tanımlı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH is defined.</span></span>
- <span data-ttu-id="a8f47-683">**FX_PTR_ERROR** (0x18) geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-683">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-684">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-684">Allowed From</span></span>

<span data-ttu-id="a8f47-685">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-685">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-686">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-686">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-687">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-687">See Also</span></span>

- <span data-ttu-id="a8f47-688">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-688">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-689">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-689">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-690">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-690">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-691">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-691">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-692">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-692">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-693">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-693">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-694">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-694">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-695">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-695">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-696">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-696">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-697">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-697">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-698">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-698">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-699">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-699">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-700">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-700">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-701">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-701">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-702">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-702">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-703">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-703">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-704">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-704">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-705">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-705">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-706">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-706">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-707">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-707">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get"></a><span data-ttu-id="a8f47-708">fx_directory_long_name_get:</span><span class="sxs-lookup"><span data-stu-id="a8f47-708">fx_directory_long_name_get:</span></span>

<span data-ttu-id="a8f47-709">Kısa adından uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-709">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-710">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-710">Prototype</span></span>

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-711">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-711">Description</span></span>

<span data-ttu-id="a8f47-712">Bu hizmet, sağlanan kısa (8,3 biçim) adıyla ilişkili uzun adı (varsa) alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-712">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="a8f47-713">Kısa ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-713">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-714">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-714">Input Parameters</span></span>

- <span data-ttu-id="a8f47-715">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-715">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-716">**short_name**: kaynak kısa adı işaretçisi (8,3 biçim).</span><span class="sxs-lookup"><span data-stu-id="a8f47-716">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="a8f47-717">**long_name**: uzun ad için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-717">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="a8f47-718">Uzun bir ad yoksa, kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-718">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="a8f47-719">Uzun ad hedefinin FX_MAX_LONG_NAME_LEN karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a8f47-719">Note that the destination for the long name must be large enough to hold FX_MAX_LONG_NAME_LEN characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-720">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-720">Return Values</span></span>

- <span data-ttu-id="a8f47-721">**FX_SUCCESS** (0x00) başarılı uzun ad al</span><span class="sxs-lookup"><span data-stu-id="a8f47-721">**FX_SUCCESS** (0x00) Successful long name get</span></span>
- <span data-ttu-id="a8f47-722">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a8f47-722">**FX_NOT_FOUND** (0x04) Short name was not found</span></span>
- <span data-ttu-id="a8f47-723">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="a8f47-723">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="a8f47-724">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="a8f47-724">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="a8f47-725">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-725">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-726">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="a8f47-726">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="a8f47-727">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-727">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="a8f47-728">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-728">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-729">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-729">**FX_PTR_ERROR** (0x18) Invalid media or name pointer</span></span>
- <span data-ttu-id="a8f47-730">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-730">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-731">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-731">Allowed From</span></span>

<span data-ttu-id="a8f47-732">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-733">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-733">Example</span></span>

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-734">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-734">See Also</span></span>

- <span data-ttu-id="a8f47-735">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-735">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-736">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-736">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-737">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-737">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-738">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-738">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-739">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-739">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-740">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-740">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-741">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-741">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-742">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-742">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-743">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-743">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-744">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-744">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-745">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-745">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-746">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-746">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-747">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-747">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-748">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-748">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-749">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-749">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-750">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-750">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-751">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-751">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-752">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-752">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-753">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-753">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-754">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-754">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get_extended"></a><span data-ttu-id="a8f47-755">fx_directory_long_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="a8f47-755">fx_directory_long_name_get_extended</span></span>

<span data-ttu-id="a8f47-756">Kısa adından uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-756">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-757">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-757">Prototype</span></span>

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="a8f47-758">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-758">Description</span></span>

<span data-ttu-id="a8f47-759">Bu hizmet, sağlanan kısa (8,3 biçim) adıyla ilişkili uzun adı (varsa) alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-759">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="a8f47-760">Kısa ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-760">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-761">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-761">Input Parameters</span></span>

- <span data-ttu-id="a8f47-762">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-762">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-763">**short_name**: kaynak kısa adı işaretçisi (8,3 biçim).</span><span class="sxs-lookup"><span data-stu-id="a8f47-763">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="a8f47-764">**long_name**: uzun ad için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-764">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="a8f47-765">Uzun bir ad yoksa, kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-765">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="a8f47-766">Note: uzun ad hedefi **FX_MAX_LONG_NAME_LEN** karakter tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-766">Note: Destination for the long name must be large enough to hold **FX_MAX_LONG_NAME_LEN** characters.</span></span>
- <span data-ttu-id="a8f47-767">**long_file_name_buffer_length**: uzun ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-767">**long_file_name_buffer_length**: Length of the long name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-768">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-768">Return Values</span></span>

- <span data-ttu-id="a8f47-769">**FX_SUCCESS** (0x00) başarılı uzun ad al.</span><span class="sxs-lookup"><span data-stu-id="a8f47-769">**FX_SUCCESS** (0x00) Successful long name get.</span></span>
- <span data-ttu-id="a8f47-770">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-770">**FX_NOT_FOUND** (0x04) Short name was not found.</span></span>
- <span data-ttu-id="a8f47-771">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-771">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-772">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-772">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-773">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-773">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-774">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-774">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-775">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-775">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-776">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-776">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="a8f47-777">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-777">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="a8f47-778">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-778">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-779">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-779">Allowed From</span></span>

<span data-ttu-id="a8f47-780">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-780">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-781">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-781">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name), sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-782">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-782">See Also</span></span>

- <span data-ttu-id="a8f47-783">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-783">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-784">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-784">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-785">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-785">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-786">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-786">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-787">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-787">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-788">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-788">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-789">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-789">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-790">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-790">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-791">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-791">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-792">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-792">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-793">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-793">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-794">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-794">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-795">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-795">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-796">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-796">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-797">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-797">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-798">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-798">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-799">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-799">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-800">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-800">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-801">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-801">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-802">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-802">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_name_test"></a><span data-ttu-id="a8f47-803">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-803">fx_directory_name_test</span></span>

<span data-ttu-id="a8f47-804">Dizin için testler</span><span class="sxs-lookup"><span data-stu-id="a8f47-804">Tests for directory</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-805">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-805">Prototype</span></span>

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-806">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-806">Description</span></span>

<span data-ttu-id="a8f47-807">Bu hizmet, belirtilen adın bir dizin olup olmadığını sınar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-807">This service tests whether or not the supplied name is a directory.</span></span> <span data-ttu-id="a8f47-808">Öyleyse, bir FX_SUCCESS döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-808">If so, a FX_SUCCESS is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-809">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-809">Input Parameters</span></span>

- <span data-ttu-id="a8f47-810">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-810">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-811">**directory_name**: Dizin girişinin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-811">**directory_name**: Pointer to name of the directory entry.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-812">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-812">Return Values</span></span>

- <span data-ttu-id="a8f47-813">**FX_SUCCESS** (0x00) sağlanan ad bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-813">**FX_SUCCESS** (0x00) Supplied name is a directory.</span></span>
- <span data-ttu-id="a8f47-814">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-814">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="a8f47-815">**FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-815">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="a8f47-816">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="a8f47-816">**FX_NOT_DIRECTORY** (0x0E)  Entry is not a directory</span></span>
- <span data-ttu-id="a8f47-817">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-817">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-818">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-818">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-819">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-819">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-820">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-820">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-821">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-821">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-822">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-822">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="a8f47-823">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-823">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="a8f47-824">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-824">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-825">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-825">Allowed From</span></span>

<span data-ttu-id="a8f47-826">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-826">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-827">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-827">Example</span></span>

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-828">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-828">See Also</span></span>

- <span data-ttu-id="a8f47-829">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-829">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-830">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-830">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-831">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-831">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-832">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-832">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-833">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-833">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-834">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-834">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-835">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-835">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-836">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-836">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-837">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-837">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-838">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-838">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-839">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-839">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-840">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-840">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-841">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-841">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-842">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-842">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-843">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-843">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-844">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-844">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-845">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-845">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-846">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-846">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-847">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-847">fx_unicode_directory_create</span></span>

## <a name="fx_directory_next_entry_find"></a><span data-ttu-id="a8f47-848">fx_directory_next_entry_find:</span><span class="sxs-lookup"><span data-stu-id="a8f47-848">fx_directory_next_entry_find:</span></span>

<span data-ttu-id="a8f47-849">Sonraki dizin girişini seçer</span><span class="sxs-lookup"><span data-stu-id="a8f47-849">Picks up next directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-850">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-850">Prototype</span></span>

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-851">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-851">Description</span></span>

<span data-ttu-id="a8f47-852">Bu hizmet, geçerli varsayılan dizindeki bir sonraki giriş adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-852">This service returns the next entry name in the current default directory.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-853">*Yerel olmayan bir yol kullanılıyorsa, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek için de önemlidir (bir ThreadX semaforu veya iş parçacığı öncelik düzeyiyle). Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-853">*If using a non-local path, it is also important to prevent (with a ThreadX semaphore or thread priority level) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-854">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-854">Input Parameters</span></span>

- <span data-ttu-id="a8f47-855">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-855">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-856">**return_entry_name**: varsayılan dizindeki bir sonraki giriş adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-856">**return_entry_name**: Pointer to destination for the next entry name in the default directory.</span></span> <span data-ttu-id="a8f47-857">Bu işaretçinin işaret ettiği arabellek, **_FX_MAX_LONG_NAME_LEN_** tarafından tanımlanan en büyük FileX adı boyutunu tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-857">The buffer this pointer points to must be large enough to hold the maximum size of FileX name, defined by **_FX_MAX_LONG_NAME_LEN_**.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-858">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-858">Return Values</span></span>

- <span data-ttu-id="a8f47-859">**FX_SUCCESS** (0x00) başarılı bir sonraki giriş bul</span><span class="sxs-lookup"><span data-stu-id="a8f47-859">**FX_SUCCESS** (0x00) Successful next entry find</span></span>
- <span data-ttu-id="a8f47-860">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-860">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-861">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-861">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="a8f47-862">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-862">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-863">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-863">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-864">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-864">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-865">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-865">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-866">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-866">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-867">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-867">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-868">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-868">**FX_CALLER_ERROR** (0x20)     Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-869">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-869">Allowed From</span></span>

<span data-ttu-id="a8f47-870">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-871">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-871">Example</span></span>

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-872">See Also</span></span>

- <span data-ttu-id="a8f47-873">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-873">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-874">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-874">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-875">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-875">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-876">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-876">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-877">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-877">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-878">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-878">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-879">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-879">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-880">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-880">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-881">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-881">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-882">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-882">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-883">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-883">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-884">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-884">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-885">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-885">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-886">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-886">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-887">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-887">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-888">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-888">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-889">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-889">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-890">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-890">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-891">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-891">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-892">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-892">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="a8f47-893">fx_directory_next_full_entry_find:</span><span class="sxs-lookup"><span data-stu-id="a8f47-893">fx_directory_next_full_entry_find:</span></span>

<span data-ttu-id="a8f47-894">Tam bilgi içeren bir sonraki dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-894">Gets next directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-895">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-895">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="a8f47-896">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-896">Description</span></span>

<span data-ttu-id="a8f47-897">Bu hizmet, varsayılan dizindeki bir sonraki giriş adını alır ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-897">This service retrieves the next entry name in the default directory and copies it to the specified destination.</span></span> <span data-ttu-id="a8f47-898">Ayrıca, ek giriş parametreleriyle belirtilen girdi hakkında tam bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-898">It also returns full information about the entry as specified by the additional input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-899">\* Belirtilen hedef, \* \* \* FX_MAX_LONG_NAME_LEN \* \* \* \* ile tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır</span><span class="sxs-lookup"><span data-stu-id="a8f47-899">\*The specified destination must be large enough to hold the maximum sized FileX name, as defined by \*\*\*FX_MAX_LONG_NAME_LEN\*\*\*\*</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-900">*Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-900">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-901">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-901">Input Parameters</span></span>

- <span data-ttu-id="a8f47-902">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-902">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-903">**directory_name**: bir dizin girişi adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-903">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="a8f47-904">En az **FX_MAX_LONG_NAME_LEN** kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-904">Must be at least as big as **FX_MAX_LONG_NAME_LEN**.</span></span>
- <span data-ttu-id="a8f47-905">**öznitelikler**: null olmayan, girişin özniteliklerinin yerleştirileceği hedefe yönelik işaretçi. Öznitelikler, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="a8f47-905">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="a8f47-906">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-906">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="a8f47-907">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-907">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="a8f47-908">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="a8f47-908">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="a8f47-909">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="a8f47-909">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="a8f47-910">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="a8f47-910">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="a8f47-911">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="a8f47-911">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="a8f47-912">**Boyut**: null olmayan, girdinin bayt cinsinden boyutu için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-912">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="a8f47-913">**ay**: null olmayan, girişin değiştirilme ayı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-913">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="a8f47-914">**yıl**: null olmayan, girişin değiştirilme yılından hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-914">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="a8f47-915">**gün**: null olmayan, girişin değiştirilme günü için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-915">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="a8f47-916">**saat**: null olmayan, girişin değiştirilme saati için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-916">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="a8f47-917">**dakika**: null olmayan, girişin değiştirilme dakikası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-917">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="a8f47-918">**ikinci**: null olmayan, girişin değiştirilme saniyesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-918">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-919">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-919">Return Values</span></span>

- <span data-ttu-id="a8f47-920">**FX_SUCCESS** (0x00) başarılı Dizin sonraki giriş bul.</span><span class="sxs-lookup"><span data-stu-id="a8f47-920">**FX_SUCCESS** (0x00) Successful directory next entry find.</span></span>
- <span data-ttu-id="a8f47-921">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-921">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-922">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-922">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="a8f47-923">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-923">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-924">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-924">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-925">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-925">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-926">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-926">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-927">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-927">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="a8f47-928">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-928">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-929">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya tüm GIRIŞ parametreleri null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-929">**FX_PTR_ERROR** (0x18) Invalid media pointer or all input parameters are NULL.</span></span>
- <span data-ttu-id="a8f47-930">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-930">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-931">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-931">Allowed From</span></span>

<span data-ttu-id="a8f47-932">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-932">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-933">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-933">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-934">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-934">See Also</span></span>

- <span data-ttu-id="a8f47-935">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-935">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-936">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-936">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-937">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-937">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-938">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-938">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-939">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-939">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-940">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-940">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-941">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-941">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-942">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-942">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-943">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-943">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-944">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-944">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-945">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-945">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-946">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-946">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-947">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-947">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-948">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-948">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-949">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-949">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-950">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-950">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-951">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-951">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-952">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-952">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-953">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-953">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-954">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-954">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_rename"></a><span data-ttu-id="a8f47-955">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-955">fx_directory_rename</span></span>

<span data-ttu-id="a8f47-956">Dizini yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="a8f47-956">Renames directory</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-957">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-957">Prototype</span></span>

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-958">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-958">Description</span></span>

<span data-ttu-id="a8f47-959">Bu hizmet dizin adını belirtilen yeni dizin adıyla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-959">This service changes the directory name to the specified new directory name.</span></span> <span data-ttu-id="a8f47-960">Yeniden adlandırma işlemi, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-960">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="a8f47-961">Yeni Dizin adında bir yol belirtilmişse, yeniden adlandırılan dizin, belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-961">If a path is specified in the new directory name, the renamed directory is effectively moved to the specified path.</span></span> <span data-ttu-id="a8f47-962">Yol belirtilmemişse, yeniden adlandırılan dizin geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-962">If no path is specified, the renamed directory is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-963">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-963">Input Parameters</span></span>

- <span data-ttu-id="a8f47-964">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-964">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-965">**old_directory_name**: geçerli dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-965">**old_directory_name**: Pointer to current directory name.</span></span>
- <span data-ttu-id="a8f47-966">**new_directory_name**: yeni dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-966">**new_directory_name**: Pointer to new directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-967">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-967">Return Values</span></span>

- <span data-ttu-id="a8f47-968">**FX_SUCCESS** (0x00) başarılı dizin yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-968">**FX_SUCCESS** (0x00) Successful directory rename.</span></span>
- <span data-ttu-id="a8f47-969">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-969">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-970">**FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-970">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="a8f47-971">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-971">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory.</span></span>
- <span data-ttu-id="a8f47-972">**FX_INVALID_NAME** (0x0C) yeni dizin adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-972">**FX_INVALID_NAME** (0x0C) New directory name is invalid.</span></span>
- <span data-ttu-id="a8f47-973">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-973">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-974">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-974">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-975">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-975">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-976">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-976">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-977">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-977">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-978">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-978">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="a8f47-979">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-979">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-980">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-980">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="a8f47-981">**FX_INVALID_PATH** (0x0D) dizin adıyla belirtilen yol geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-981">**FX_INVALID_PATH** (0x0D) Invalid path supplied with directory name.</span></span>
- <span data-ttu-id="a8f47-982">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin zaten oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-982">**FX_ALREADY_CREATED** (0x0B) Specified directory was already created.</span></span>
- <span data-ttu-id="a8f47-983">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-983">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-984">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-984">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-985">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-985">Allowed From</span></span>

<span data-ttu-id="a8f47-986">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-986">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-987">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-987">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-988">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-988">See Also</span></span>

- <span data-ttu-id="a8f47-989">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-989">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-990">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-990">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-991">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-991">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-992">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-992">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-993">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-993">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-994">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-994">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-995">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-995">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-996">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-996">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-997">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-997">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-998">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-998">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-999">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-999">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-1000">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-1000">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-1001">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1001">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-1002">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1002">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-1003">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-1003">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-1004">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1004">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-1005">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1005">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-1006">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1006">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-1007">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1007">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-1008">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1008">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get"></a><span data-ttu-id="a8f47-1009">fx_directory_short_name_get:</span><span class="sxs-lookup"><span data-stu-id="a8f47-1009">fx_directory_short_name_get:</span></span>

<span data-ttu-id="a8f47-1010">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-1010">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1011">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1011">Prototype</span></span>

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-1012">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1012">Description</span></span>

<span data-ttu-id="a8f47-1013">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1013">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="a8f47-1014">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1014">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1015">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1015">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1016">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1016">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-1017">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1017">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="a8f47-1018">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1018">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="a8f47-1019">Kısa ad hedefinin 14 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1019">Note that the destination for the short name must be large enough to hold 14 characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1020">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1020">Return Values</span></span>

- <span data-ttu-id="a8f47-1021">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1021">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="a8f47-1022">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1022">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="a8f47-1023">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1023">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1024">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1024">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1025">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1025">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1026">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1026">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1027">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1027">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1028">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1028">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1029">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1029">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-1030">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1030">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="a8f47-1031">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1031">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1032">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1032">Allowed From</span></span>

<span data-ttu-id="a8f47-1033">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1033">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1034">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1034">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1035">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1035">See Also</span></span>

- <span data-ttu-id="a8f47-1036">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1036">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-1037">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1037">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-1038">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1038">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-1039">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1039">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-1040">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1040">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-1041">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1041">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-1042">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1042">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-1043">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1043">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-1044">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1044">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-1045">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-1045">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-1046">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1046">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-1047">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-1047">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-1048">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1048">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-1049">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1049">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-1050">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-1050">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-1051">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1051">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-1052">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1052">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-1053">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1053">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-1054">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1054">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-1055">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1055">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get_extended"></a><span data-ttu-id="a8f47-1056">fx_directory_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="a8f47-1056">fx_directory_short_name_get_extended</span></span>

<span data-ttu-id="a8f47-1057">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-1057">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1058">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1058">Prototype</span></span>

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a><span data-ttu-id="a8f47-1059">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1059">Description</span></span>

<span data-ttu-id="a8f47-1060">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1060">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="a8f47-1061">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1061">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1062">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1062">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1063">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1063">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-1064">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1064">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="a8f47-1065">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1065">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="a8f47-1066">Note: kısa ad hedefi 14 karakter tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1066">Note: Destination for the short name must be large enough to hold 14 characters.</span></span>
- <span data-ttu-id="a8f47-1067">**short_file_name_length**: kısa ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1067">**short_file_name_length**: Length of short name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1068">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1068">Return Values</span></span>

- <span data-ttu-id="a8f47-1069">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1069">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="a8f47-1070">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1070">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="a8f47-1071">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1071">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1072">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1072">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1073">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1074">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1075">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1075">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1076">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1076">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1077">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1077">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-1078">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1078">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="a8f47-1079">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1079">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1080">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1080">Allowed From</span></span>

<span data-ttu-id="a8f47-1081">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1081">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1082">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1082">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1083">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1083">See Also</span></span>

- <span data-ttu-id="a8f47-1084">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1084">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-1085">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1085">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-1086">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1086">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-1087">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1087">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-1088">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1088">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-1089">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1089">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-1090">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1090">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-1091">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1091">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-1092">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1092">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-1093">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-1093">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-1094">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1094">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-1095">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-1095">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-1096">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1096">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-1097">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1097">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-1098">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-1098">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-1099">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1099">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-1100">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-1100">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-1101">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1101">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-1102">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1102">fx_unicode_directory_create</span></span>
- <span data-ttu-id="a8f47-1103">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1103">fx_unicode_directory_rename</span></span>

## <a name="fx_fault_tolerant_enable"></a><span data-ttu-id="a8f47-1104">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-1104">fx_fault_tolerant_enable</span></span>

<span data-ttu-id="a8f47-1105">Hataya dayanıklı hizmeti sunar</span><span class="sxs-lookup"><span data-stu-id="a8f47-1105">Enables the fault tolerant service</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1106">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1106">Prototype</span></span>

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a><span data-ttu-id="a8f47-1107">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1107">Description</span></span>

<span data-ttu-id="a8f47-1108">Bu hizmet, hataya dayanıklı modüle izin vermez.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1108">This service enables the fault tolerant module.</span></span> <span data-ttu-id="a8f47-1109">Başlamadan sonra, hataya dayanıklı modül dosya sisteminin FileX hataya dayanıklı koruma altında olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1109">Upon starting, the fault tolerant module detects whether or not the file system is under FileX fault tolerant protection.</span></span> <span data-ttu-id="a8f47-1110">Aksi takdirde, hizmet, dosya sistemi işlemlerinde günlükleri depolamak için dosya sisteminde kullanılabilir kesimleri bulur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1110">If it is not, the service finds available sectors on the file system to store logs on file system transactions.</span></span> <span data-ttu-id="a8f47-1111">Dosya sistemi, FileX hataya dayanıklı koruma altındaysa, bütünlüğünü sürdürmek için günlükleri dosya sistemine uygular.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1111">If the file system is under FileX fault tolerant protection, it applies the logs to the file system to maintain its integrity.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1112">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1112">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1113">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1113">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-1114">**memory_ptr**: hataya dayanıklı modül tarafından karalama belleği olarak kullanılan bir bellek bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1114">**memory_ptr**: Pointer to a block of memory used by the fault tolerant module as scratch memory.</span></span>
- <span data-ttu-id="a8f47-1115">**memory_size**: karalama belleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1115">**memory_size**: The size of the scratch memory.</span></span> <span data-ttu-id="a8f47-1116">Hata toleranslı 'nin düzgün çalışması için, karalama belleği boyutu en az 3072 bayt olur ve sektör boyutunun katı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1116">In order for fault tolerant to work properly, the scratch memory size shall be at least 3072 bytes,- and must be multiple of sector size.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1117">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1117">Return Values</span></span>

- <span data-ttu-id="a8f47-1118">**FX_SUCCESS** (0x00) hata dayanıklılığını başarıyla etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1118">**FX_SUCCESS** (0x00) Successfully enabled fault tolerant.</span></span>
- <span data-ttu-id="a8f47-1119">**FX_NOT_ENOUGH_MEMORY** (0x91) bellek boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1119">**FX_NOT_ENOUGH_MEMORY** (0x91)    memory size too small.</span></span>
- <span data-ttu-id="a8f47-1120">**FX_BOOT_ERROR** (0x01) önyükleme kesimi hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1120">**FX_BOOT_ERROR** (0x01) Boot sector error.</span></span>
- <span data-ttu-id="a8f47-1121">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1121">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1122">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1122">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="a8f47-1123">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1123">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="a8f47-1124">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="a8f47-1124">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="a8f47-1125">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1125">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1126">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1126">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-1127">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1127">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1128">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1128">Allowed From</span></span>

<span data-ttu-id="a8f47-1129">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1129">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1130">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1130">Example</span></span>

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a><span data-ttu-id="a8f47-1131">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1131">See Also</span></span>

- <span data-ttu-id="a8f47-1132">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-1132">fx_system_initialize</span></span>
- <span data-ttu-id="a8f47-1133">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-1133">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-1134">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1134">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-1135">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-1135">fx_media_check</span></span>
- <span data-ttu-id="a8f47-1136">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1136">fx_media_close</span></span>
- <span data-ttu-id="a8f47-1137">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1137">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-1138">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-1138">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-1139">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-1139">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-1140">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-1140">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-1141">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-1141">fx_media_format</span></span>
- <span data-ttu-id="a8f47-1142">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1142">fx_media_open</span></span>
- <span data-ttu-id="a8f47-1143">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1143">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-1144">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1144">fx_media_read</span></span>
- <span data-ttu-id="a8f47-1145">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-1145">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-1146">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1146">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-1147">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1147">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-1148">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1148">fx_media_write</span></span>

## <a name="fx_file_allocate"></a><span data-ttu-id="a8f47-1149">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1149">fx_file_allocate</span></span>

<span data-ttu-id="a8f47-1150">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="a8f47-1150">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1151">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1151">Prototype</span></span>

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="a8f47-1152">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1152">Description</span></span>

<span data-ttu-id="a8f47-1153">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1153">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="a8f47-1154">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1154">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="a8f47-1155">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1155">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="a8f47-1156">4 GB 'den daha fazla alan ayırmak için, uygulama Service *fx_file_extended_allocate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1156">To allocate space beyond 4GB, application shall use the service *fx_file_extended_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1157">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1158">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1158">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-1159">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1159">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1160">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1160">Return Values</span></span>

- <span data-ttu-id="a8f47-1161">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1161">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="a8f47-1162">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1162">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-1163">**FX_FAT_READ_ERROR** (0x03), FAT girişini okuyamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1163">**FX_FAT_READ_ERROR** (0x03) Failed to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1164">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1164">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1165">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1165">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-1166">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1166">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="a8f47-1167">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1167">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="a8f47-1168">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="a8f47-1168">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="a8f47-1169">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1169">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1170">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1170">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1171">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1171">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-1172">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1172">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1173">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1173">Allowed From</span></span>

<span data-ttu-id="a8f47-1174">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1175">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1175">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1176">See Also</span></span>

- <span data-ttu-id="a8f47-1177">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1177">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1178">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1178">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1179">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1179">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1180">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1180">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="a8f47-1181">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1181">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1182">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1182">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1183">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1183">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1184">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1184">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1185">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1185">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1186">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1186">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1187">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1187">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1188">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1188">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1189">fx_file_open fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1189">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="a8f47-1190">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1190">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1191">fx_file_rename fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1191">fx_file_rename- fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1192">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1192">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1193">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1193">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1194">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1194">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1195">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1195">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1196">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1196">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1197">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1197">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1198">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1198">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1199">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1199">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_read"></a><span data-ttu-id="a8f47-1200">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1200">fx_file_attributes_read</span></span>

<span data-ttu-id="a8f47-1201">Dosya özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="a8f47-1201">Reads file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1202">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1202">Prototype</span></span>

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-1203">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1203">Description</span></span>

<span data-ttu-id="a8f47-1204">Bu hizmet, dosyanın özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1204">This service reads the file's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1205">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1206">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1206">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-1207">**file_name**: istenen dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1207">**file_name**: Pointer to the name of the requested file (directory path is optional).</span></span>
- <span data-ttu-id="a8f47-1208">**attributes_ptr**: dosyaya yerleştirilecek özniteliklerin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1208">**attributes_ptr**: Pointer to the destination for the file's attributes to be placed.</span></span> <span data-ttu-id="a8f47-1209">Dosya öznitelikleri, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="a8f47-1209">The file attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="a8f47-1210">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1210">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="a8f47-1211">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1211">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="a8f47-1212">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1212">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="a8f47-1213">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1213">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="a8f47-1214">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1214">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="a8f47-1215">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1215">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1216">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1216">Return Values</span></span>

- <span data-ttu-id="a8f47-1217">**FX_SUCCESS** (0x00) başarılı özniteliği okundu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1217">**FX_SUCCESS** (0x00) Successful attribute read.</span></span>
- <span data-ttu-id="a8f47-1218">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1218">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-1219">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1219">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="a8f47-1220">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1220">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="a8f47-1221">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1221">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1222">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1222">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1223">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1223">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1224">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1224">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1225">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1225">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1226">**FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1226">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="a8f47-1227">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1227">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1228">Allowed From</span></span>

<span data-ttu-id="a8f47-1229">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1230">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1230">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-1231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1231">See Also</span></span>

- <span data-ttu-id="a8f47-1232">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1232">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1233">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1233">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1234">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1234">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1235">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1235">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="a8f47-1236">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1236">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1237">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1237">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1238">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1238">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1239">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1239">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1240">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1240">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1241">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1241">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1242">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1242">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1243">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1243">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1244">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1244">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1245">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1245">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1246">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1246">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1247">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1247">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1248">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1248">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1249">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1249">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1250">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1250">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1251">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1251">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1252">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1252">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1253">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1253">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1254">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1254">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1255">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1255">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1256">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1256">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_set"></a><span data-ttu-id="a8f47-1257">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1257">fx_file_attributes_set</span></span>

<span data-ttu-id="a8f47-1258">Dosya özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-1258">Sets file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1259">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1259">Prototype</span></span>

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a><span data-ttu-id="a8f47-1260">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1260">Description</span></span>

<span data-ttu-id="a8f47-1261">Bu hizmet, dosyanın özniteliklerini çağıran tarafından belirtilen olanlarla ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1261">This service sets the file's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-1262">*Uygulamanın yalnızca bu hizmetle birlikte dosyanın özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlamaya yönelik her türlü girişim bir hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-1262">*The application is only allowed to modify a subset of the file's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1263">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1263">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1264">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1264">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-1265">**file_name**: istenen dosyanın adı işaretçisi \* \* (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1265">**file_name**: Pointer to the name of the requested file\*\* (directory path is optional).</span></span>
- <span data-ttu-id="a8f47-1266">**öznitelikler**: dosyanın yeni öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1266">**attributes**: The new attributes for the file.</span></span> <span data-ttu-id="a8f47-1267">Geçerli dosya öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-1267">The valid file attributes are defined as follows:</span></span>
  - <span data-ttu-id="a8f47-1268">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1268">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="a8f47-1269">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1269">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="a8f47-1270">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1270">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="a8f47-1271">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1271">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1272">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1272">Return Values</span></span>

- <span data-ttu-id="a8f47-1273">**FX_SUCCESS** (0x00) başarılı öznitelik kümesi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1273">**FX_SUCCESS** (0x00) Successful attribute set.</span></span>
- <span data-ttu-id="a8f47-1274">**FX_ACCESS_ERROR** (0x06) dosyası açık ve öznitelikleri ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1274">**FX_ACCESS_ERROR** (0x06) File is open and cannot have its attributes set.</span></span>
- <span data-ttu-id="a8f47-1275">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1275">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1276">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1276">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-1278">**FX_NO_MORE_ENTRIES** (0x0F) FAT tablosunda veya exFAT Cluster eşlemesinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1278">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in the FAT table or exFAT cluster map.</span></span>
- <span data-ttu-id="a8f47-1279">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1279">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="a8f47-1280">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1280">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="a8f47-1281">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1281">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="a8f47-1282">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="a8f47-1282">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="a8f47-1283">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1283">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1284">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1284">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1285">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1285">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-1286">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1286">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-1287">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1287">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="a8f47-1288">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1288">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1289">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1289">Allowed From</span></span>

<span data-ttu-id="a8f47-1290">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1290">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1291">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1291">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-1292">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1292">See Also</span></span>

- <span data-ttu-id="a8f47-1293">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1293">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1294">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1294">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1295">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1295">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1296">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1296">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1297">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1297">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1298">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1298">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1299">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1299">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1300">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1300">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1301">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1301">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1302">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1302">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1303">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1303">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1304">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1304">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1305">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1305">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1306">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1306">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1307">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1307">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1308">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1308">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1309">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1309">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1310">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1310">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1311">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1311">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1312">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1312">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1313">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1313">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1314">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1314">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1315">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1315">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1316">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1316">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1317">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1317">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1318">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1318">fx_unicode_short_name_get</span></span>

## <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="a8f47-1319">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1319">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="a8f47-1320">Bir dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="a8f47-1320">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1321">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1321">Prototype</span></span>

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="a8f47-1322">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1322">Description</span></span>

<span data-ttu-id="a8f47-1323">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1323">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="a8f47-1324">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1324">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="a8f47-1325">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1325">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="a8f47-1326">Medyada yeterli sayıda ardışık küme yoksa, bu hizmet birbirini izleyen en büyük küme bloğunu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1326">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="a8f47-1327">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1327">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="a8f47-1328">4 GB 'den daha fazla alan ayırmak için, uygulama Service *fx_file_extended_best_effort_allocate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1328">To allocate space beyond 4GB, application shall use the service *fx_file_extended_best_effort_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1329">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1329">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1330">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1330">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-1331">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1331">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1332">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1332">Return Values</span></span>

- <span data-ttu-id="a8f47-1333">**FX_SUCCESS** (0x00) başarılı en iyi çaba dosya ayırması.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1333">**FX_SUCCESS** (0x00) Successful best-effort file allocation.</span></span>
- <span data-ttu-id="a8f47-1334">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1334">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-1335">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1335">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-1336">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1336">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="a8f47-1337">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1337">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1338">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1338">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1339">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1339">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1340">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1340">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1341">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1341">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1342">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1342">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1343">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi veya hedef.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1343">**FX_PTR_ERROR** (0x18) Invalid file pointer or destination.</span></span>
- <span data-ttu-id="a8f47-1344">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1344">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1345">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1345">Allowed From</span></span>

<span data-ttu-id="a8f47-1346">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1346">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1347">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1347">Example</span></span>

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-1348">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1348">See Also</span></span>

- <span data-ttu-id="a8f47-1349">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1349">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1350">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1350">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1351">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1351">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1352">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1353">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1354">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1355">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1359">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1362">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1363">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1364">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1365">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1366">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1367">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1368">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1369">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1371">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1371">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1372">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1372">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1373">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1373">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1374">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1374">fx_unicode_short_name_get</span></span>

## <a name="fx_file_close"></a><span data-ttu-id="a8f47-1375">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1375">fx_file_close</span></span>

<span data-ttu-id="a8f47-1376">Dosyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="a8f47-1376">Closes file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1377">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1377">Prototype</span></span>

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-1378">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1378">Description</span></span>

<span data-ttu-id="a8f47-1379">Bu hizmet, belirtilen dosyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1379">This service closes the specified file.</span></span> <span data-ttu-id="a8f47-1380">Dosya yazmak için açıksa ve değiştirilmişse, bu hizmet Dizin girişini yeni boyut ve geçerli sistem saati ve tarihi ile güncelleştirerek dosya değiştirme işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1380">If the file was open for writing and if it was modified, this service completes the file modification process by updating its directory entry with the new size and the current system time and date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1381">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1381">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1382">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1382">**file_ptr**: Pointer to a previously opened file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1383">Return Values</span></span>

- <span data-ttu-id="a8f47-1384">**FX_SUCCESS** (0x00) başarılı dosya kapatma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1384">**FX_SUCCESS** (0x00) Successful file close.</span></span>
- <span data-ttu-id="a8f47-1385">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1385">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="a8f47-1386">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1386">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1387">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1387">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1388">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1388">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1389">**FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1389">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="a8f47-1390">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1390">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1391">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1391">Allowed From</span></span>

<span data-ttu-id="a8f47-1392">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1392">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1393">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1393">Example</span></span>

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1394">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1394">See Also</span></span>

- <span data-ttu-id="a8f47-1395">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1395">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1396">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1396">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1397">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1397">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1398">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1398">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1399">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1399">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1400">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1400">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1401">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1401">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1402">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1402">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1403">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1403">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1404">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1404">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1405">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1405">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1406">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1406">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1407">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1407">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1408">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1408">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1409">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1409">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1410">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1410">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1411">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1411">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1412">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1412">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1413">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1413">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1414">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1414">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1415">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1415">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1416">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1416">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1417">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1417">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1418">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1418">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1419">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1419">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1420">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1420">fx_unicode_short_name_get</span></span>

## <a name="fx_file_create"></a><span data-ttu-id="a8f47-1421">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1421">fx_file_create</span></span>

<span data-ttu-id="a8f47-1422">Dosya oluşturur</span><span class="sxs-lookup"><span data-stu-id="a8f47-1422">Creates file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1423">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1423">Prototype</span></span>

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-1424">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1424">Description</span></span>

<span data-ttu-id="a8f47-1425">Bu hizmet, belirtilen dosyayı varsayılan dizinde veya dosya adıyla sağlanan dizin yolunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1425">This service creates the specified file in the default directory or in the directory path supplied with the file name.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-1426">*Bu hizmet, sıfır uzunluğunda bir dosya oluşturur, yani hiçbir küme ayrılmamış. Ayırma işlemi, sonraki dosya yazmaları üzerinde otomatik olarak gerçekleşir veya fx_file_allocate hizmeti veya 4 GB 'den daha fazla alan fx_file_extended_allocate daha önce yapılabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-1426">*This service creates a file of zero length, i.e., no clusters allocated. Allocation will automatically take place on subsequent file writes or can be done in advance with the fx_file_allocate service or fx_file_extended_allocate for space beyond 4GB) service.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1427">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1427">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1428">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1428">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-1429">**file_name**: oluşturulacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1429">**file_name**: Pointer to the name of the file to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1430">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1430">Return Values</span></span>

- <span data-ttu-id="a8f47-1431">**FX_SUCCESS** (0x00) başarılı dosya oluştur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1431">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="a8f47-1432">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1432">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-1433">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya zaten oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1433">**FX_ALREADY_CREATED** (0x0B) Specified file was already created.</span></span>
- <span data-ttu-id="a8f47-1434">**FX_NO_MORE_SPACE** (0x0A) kök dizinde başka girdi yok veya kullanılabilir daha fazla küme yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1434">**FX_NO_MORE_SPACE** (0x0A)    Either there are no more entries in the root directory or there are no more clusters available.</span></span>
- <span data-ttu-id="a8f47-1435">**FX_INVALID_PATH** (0x0D) dosya adı ile geçersiz yol sağlandı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1435">**FX_INVALID_PATH** (0x0D) Invalid path supplied with file name.</span></span>
- <span data-ttu-id="a8f47-1436">**FX_INVALID_NAME** (0x0C) dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1436">**FX_INVALID_NAME** (0x0C) File name is invalid.</span></span>
- <span data-ttu-id="a8f47-1437">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1437">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1438">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1438">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1439">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1439">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1440">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1440">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1441">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1441">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1442">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1442">**FX_MEDIA_INVALID** (0x02)Invalid media.</span></span>
- <span data-ttu-id="a8f47-1443">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1443">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1444">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1444">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="a8f47-1445">**FX_PTR_ERROR** (0x18) geçersiz medya veya dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1445">**FX_PTR_ERROR** (0x18) Invalid media or file name pointer.</span></span>
- <span data-ttu-id="a8f47-1446">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1446">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1447">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1447">Allowed From</span></span>

<span data-ttu-id="a8f47-1448">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1448">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1449">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1449">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1450">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1450">See Also</span></span>
- <span data-ttu-id="a8f47-1451">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1451">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1452">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1452">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1453">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1453">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1454">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1454">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1455">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1455">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1456">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1456">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1457">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1457">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1458">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1458">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1459">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1459">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1460">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1460">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1461">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1461">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1462">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1462">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1463">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1463">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1464">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1464">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1465">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1465">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1466">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1466">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1467">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1467">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1468">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1468">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1469">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1469">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1470">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1470">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1471">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1471">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1472">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1472">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1473">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1473">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1474">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1474">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1475">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1475">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1476">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1476">fx_unicode_short_name_get</span></span>

## <a name="fx_file_date_time_set"></a><span data-ttu-id="a8f47-1477">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1477">fx_file_date_time_set</span></span>

### <a name="sets-file-date-and-time"></a><span data-ttu-id="a8f47-1478">Dosya tarih ve saatini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-1478">Sets file date and time</span></span>

<span data-ttu-id="a8f47-1479">Dosya tarih ve saati ayarlanıyor</span><span class="sxs-lookup"><span data-stu-id="a8f47-1479">Setting File Date and Time</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1480">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1480">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="a8f47-1481">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1481">Description</span></span>

<span data-ttu-id="a8f47-1482">Bu hizmet, belirtilen dosyanın tarih ve saatini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1482">This service sets the date and time of the specified file.</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1483">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1483">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1484">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1484">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-1485">**file_name**: dosyanın adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1485">**file_name**: Pointer to name of the file.</span></span>
- <span data-ttu-id="a8f47-1486">**yıl**: yılın değeri (1980-2107 dahil).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1486">**year**: Value of year (1980-2107 inclusive).</span></span>
- <span data-ttu-id="a8f47-1487">**Month**: ayın değeri (1-12 dahil).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1487">**month**: Value of month (1-12 inclusive).</span></span>
- <span data-ttu-id="a8f47-1488">**gün**: günün değeri (1-31 dahil).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1488">**day**: Value of day (1-31 inclusive).</span></span>
- <span data-ttu-id="a8f47-1489">**saat**: Saat değeri (0-23 dahil).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1489">**hour**: Value of hour (0-23 inclusive).</span></span>
- <span data-ttu-id="a8f47-1490">**Minute**: dakikalık değeri (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1490">**minute**: Value of minute (0-59 inclusive).</span></span>
- <span data-ttu-id="a8f47-1491">**ikinci**: ikinci değer (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1491">**second**: Value of second (0-59 inclusive).</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1492">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1492">Return Values</span></span>

- <span data-ttu-id="a8f47-1493">**FX_SUCCESS** (0x00) başarılı tarih/saat kümesi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1493">**FX_SUCCESS** (0x00) Successful date/time set.</span></span>
- <span data-ttu-id="a8f47-1494">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1494">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-1495">**FX_NOT_FOUND** (0x04) dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1495">**FX_NOT_FOUND** (0x04)    File was not found.</span></span>
- <span data-ttu-id="a8f47-1496">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1496">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1497">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1497">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1498">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1498">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1499">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1499">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1500">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1500">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="a8f47-1501">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1501">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1502">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1502">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1503">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1503">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="a8f47-1504">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1504">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="a8f47-1505">**FX_INVALID_YEAR** (0x12) yıl geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1505">**FX_INVALID_YEAR** (0x12) Year is invalid.</span></span>
- <span data-ttu-id="a8f47-1506">**FX_INVALID_MONTH** (0x13) ay geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1506">**FX_INVALID_MONTH** (0x13) Month is invalid.</span></span>
- <span data-ttu-id="a8f47-1507">**FX_INVALID_DAY** (0x14) gün geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1507">**FX_INVALID_DAY** (0x14) Day is invalid.</span></span>
- <span data-ttu-id="a8f47-1508">**FX_INVALID_HOUR** (0x15) saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1508">**FX_INVALID_HOUR** (0x15)    Hour is invalid.</span></span>
- <span data-ttu-id="a8f47-1509">**FX_INVALID_MINUTE** (0x16) dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1509">**FX_INVALID_MINUTE** (0x16) Minute is invalid.</span></span>
- <span data-ttu-id="a8f47-1510">**FX_INVALID_SECOND** (0x17) saniye geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1510">**FX_INVALID_SECOND** (0x17) Second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1511">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1511">Allowed From</span></span>

<span data-ttu-id="a8f47-1512">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1512">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1513">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1513">Example</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1514">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1514">See Also</span></span>

- <span data-ttu-id="a8f47-1515">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1515">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1516">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1516">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1517">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1517">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1518">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1518">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1519">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1519">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1520">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1520">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1521">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1521">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1522">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1522">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1523">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1523">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1524">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1524">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1525">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1525">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1526">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1526">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1527">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1527">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1528">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1528">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1529">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1529">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1530">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1530">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1531">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1531">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1532">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1532">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1533">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1533">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1534">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1534">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1535">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1535">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1536">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1536">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1537">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1537">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1538">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1538">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1539">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1539">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1540">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1540">fx_unicode_short_name_get</span></span>

## <a name="fx_file_delete"></a><span data-ttu-id="a8f47-1541">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1541">fx_file_delete</span></span>

### <a name="deletes-file"></a><span data-ttu-id="a8f47-1542">Dosyayı siler</span><span class="sxs-lookup"><span data-stu-id="a8f47-1542">Deletes file</span></span>

<span data-ttu-id="a8f47-1543">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="a8f47-1543">File Deletion</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1544">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1544">Prototype</span></span>

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-1545">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1545">Description</span></span>

<span data-ttu-id="a8f47-1546">Bu hizmet, belirtilen dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1546">This service deletes the specified file.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="a8f47-1547">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1547">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1548">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1548">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-1549">**file_name**: Silinecek dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1549">**file_name**: Pointer to the name of the file to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1550">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1550">Return Values</span></span>

- <span data-ttu-id="a8f47-1551">**FX_SUCCESS** (0x00) başarılı dosya silme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1551">**FX_SUCCESS** (0x00) Successful file delete.</span></span>
- <span data-ttu-id="a8f47-1552">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1552">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-1553">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1553">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="a8f47-1554">**FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1554">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="a8f47-1555">**FX_ACCESS_ERROR** (0x06) belirtilen dosya şu anda açık.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1555">**FX_ACCESS_ERROR** (0x06) Specified file is currently open.</span></span>
- <span data-ttu-id="a8f47-1556">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1556">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1557">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1557">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1558">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1558">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1559">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1559">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1560">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1560">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1561">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1561">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1562">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1562">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1563">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1563">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-1564">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1564">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-1565">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1565">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1566">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1566">Allowed From</span></span>

<span data-ttu-id="a8f47-1567">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1568">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1568">Example</span></span>

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1569">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1569">See Also</span></span>

- <span data-ttu-id="a8f47-1570">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1570">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1571">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1571">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1572">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1572">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1573">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1573">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1574">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1574">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1575">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1575">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1576">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1576">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1577">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1577">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1578">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1578">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1579">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1579">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1580">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1580">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1581">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1581">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1582">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1582">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1583">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1583">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1584">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1584">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1585">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1585">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1586">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1586">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1587">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1587">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1588">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1588">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1589">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1589">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1590">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1590">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1591">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1591">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1592">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1592">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1593">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1593">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1594">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1594">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1595">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1595">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_allocate"></a><span data-ttu-id="a8f47-1596">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1596">fx_file_extended_allocate</span></span>

<span data-ttu-id="a8f47-1597">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="a8f47-1597">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1598">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1598">Prototype</span></span>

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="a8f47-1599">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1599">Description</span></span>

<span data-ttu-id="a8f47-1600">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1600">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="a8f47-1601">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1601">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="a8f47-1602">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1602">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="a8f47-1603">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1603">This service is designed for exFAT.</span></span> <span data-ttu-id="a8f47-1604">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1604">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1605">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1605">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1606">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1606">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-1607">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1607">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1608">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1608">Return Values</span></span>

- <span data-ttu-id="a8f47-1609">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1609">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="a8f47-1610">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1610">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-1611">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1611">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-1612">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1612">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="a8f47-1613">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1613">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1614">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1614">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1615">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1615">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1616">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1616">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1617">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1617">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1618">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1618">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1619">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1619">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-1620">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1620">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1621">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1621">Allowed From</span></span>

<span data-ttu-id="a8f47-1622">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1622">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1623">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1623">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1624">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1624">See Also</span></span>

- <span data-ttu-id="a8f47-1625">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1625">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1626">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1626">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1627">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1627">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1628">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1628">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1629">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1629">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1630">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1630">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1631">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1631">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1632">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1632">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1633">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1633">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1634">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1634">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1635">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1635">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1636">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1636">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1637">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1637">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1638">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1638">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1639">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1639">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1640">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1640">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1641">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1641">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1642">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1642">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1643">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1643">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1644">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1644">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1645">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1645">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1646">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1646">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1647">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1647">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1648">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1648">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1649">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1649">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1650">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1650">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_best_effort_allocate"></a><span data-ttu-id="a8f47-1651">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1651">fx_file_extended_best_effort_allocate</span></span>

<span data-ttu-id="a8f47-1652">Bir dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="a8f47-1652">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1653">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1653">Prototype</span></span>

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="a8f47-1654">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1654">Description</span></span>

<span data-ttu-id="a8f47-1655">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1655">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="a8f47-1656">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1656">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="a8f47-1657">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1657">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="a8f47-1658">Medyada yeterli sayıda ardışık küme yoksa, bu hizmet birbirini izleyen en büyük küme bloğunu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1658">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="a8f47-1659">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1659">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="a8f47-1660">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1660">This service is designed for exFAT.</span></span> <span data-ttu-id="a8f47-1661">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1661">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1662">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1662">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1663">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1663">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-1664">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1664">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1665">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1665">Return Values</span></span>

- <span data-ttu-id="a8f47-1666">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1666">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="a8f47-1667">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1667">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-1668">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1668">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-1669">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1669">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="a8f47-1670">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1670">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1671">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1671">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1672">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1672">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1673">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1673">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1674">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1674">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1675">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1675">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1676">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1676">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-1677">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1677">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1678">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1678">Allowed From</span></span>

<span data-ttu-id="a8f47-1679">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1679">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1680">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1680">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-1681">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1681">See Also</span></span>

- <span data-ttu-id="a8f47-1682">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1682">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1683">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1683">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1684">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1684">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1685">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1685">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1686">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1686">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1687">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1688">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1688">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1689">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1689">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1690">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1690">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1691">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1691">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1692">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1692">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1693">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1693">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1694">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1694">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1695">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1695">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1696">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1696">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1697">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1697">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1698">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1698">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1699">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1699">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1700">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1700">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1701">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1701">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1702">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1702">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1703">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1703">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1704">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1704">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1705">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1705">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1706">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1706">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1707">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1707">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_relative_seek"></a><span data-ttu-id="a8f47-1708">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1708">fx_file_extended_relative_seek</span></span>

<span data-ttu-id="a8f47-1709">Göreli bayt uzaklığına pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-1709">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1710">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1710">Prototype</span></span>

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="a8f47-1711">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1711">Description</span></span>

<span data-ttu-id="a8f47-1712">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1712">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="a8f47-1713">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1713">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="a8f47-1714">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1714">This service is designed for exFAT.</span></span> <span data-ttu-id="a8f47-1715">*Byte_offset* parametresi, çağıranın 4 Aralık dışında okuma/yazma işaretçisini yeniden konumlandırmasına olanak tanıyan bir bit-bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1715">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-1716">*Arama işlemi dosyanın sonundan sonra arama yapmayı denerse, dosyanın okuma/yazma işaretçisi dosyanın sonuna yerleştirilir. Buna karşılık, arama işlemi dosyanın başlangıcını aşan konuma çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başlangıcına yerleştirilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-1716">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1717">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1717">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1718">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1718">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-1719">**byte_offset**: dosyada istenen göreli bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1719">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="a8f47-1720">**seek_from**: göreli arama yapılacak yönün yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1720">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="a8f47-1721">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-1721">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="a8f47-1722">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1722">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="a8f47-1723">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1723">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="a8f47-1724">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1724">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="a8f47-1725">FX_SEEK_BACK (0x03) FX_SEEK_BEGIN belirtilmişse, arama işlemi dosyanın başından yapılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1725">FX_SEEK_BACK (0x03) If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="a8f47-1726">FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1726">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="a8f47-1727">FX_SEEK_FORWARD belirtilirse, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1727">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="a8f47-1728">FX_SEEK_BACK belirtilirse, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1728">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1729">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1729">Return Values</span></span>

- <span data-ttu-id="a8f47-1730">**FX_SUCCESS** (0x00) başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1730">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="a8f47-1731">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1731">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-1732">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1732">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1733">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1733">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1734">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1734">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1735">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1735">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1736">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1736">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-1737">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1737">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1738">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1738">Allowed From</span></span>

<span data-ttu-id="a8f47-1739">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1740">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1740">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1741">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1741">See Also</span></span>

- <span data-ttu-id="a8f47-1742">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1742">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1743">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1743">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1744">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1744">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1745">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1745">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1746">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1746">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1747">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1747">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1748">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1748">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1749">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1749">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1750">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1750">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1751">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1751">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1752">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1752">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1753">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1753">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1754">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1754">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1755">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1755">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1756">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1756">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1757">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1757">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1758">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1758">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1759">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1759">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1760">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1760">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1761">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1761">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1762">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1762">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1763">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1763">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1764">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1764">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1765">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1765">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1766">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1766">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1767">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1767">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_seek"></a><span data-ttu-id="a8f47-1768">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1768">fx_file_extended_seek</span></span>

<span data-ttu-id="a8f47-1769">Bayt uzaklığa pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-1769">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1770">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1770">Prototype</span></span>

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a><span data-ttu-id="a8f47-1771">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1771">Description</span></span>

<span data-ttu-id="a8f47-1772">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen bayt uzaklığa konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1772">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="a8f47-1773">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1773">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="a8f47-1774">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1774">This service is designed for exFAT.</span></span> <span data-ttu-id="a8f47-1775">*Byte_offset* parametresi, çağıranın 4 Aralık dışında okuma/yazma işaretçisini yeniden konumlandırmasına olanak tanıyan bir bit-bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1775">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1776">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1776">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1777">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1777">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-1778">**byte_offset**: dosyada istenen bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1778">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="a8f47-1779">Sıfır değeri, dosyanın başındaki okuma/yazma işaretçisini konumlandırır, ancak dosyanın boyutundan büyük bir değer, dosyanın sonundaki okuma/yazma işaretçisini konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1779">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1780">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1780">Return Values</span></span>

- <span data-ttu-id="a8f47-1781">**FX_SUCCESS** (0x00) başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1781">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="a8f47-1782">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1782">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="a8f47-1783">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1783">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1784">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1784">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1785">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1785">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1786">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1786">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1787">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1787">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-1788">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1788">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1789">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1789">Allowed From</span></span>

<span data-ttu-id="a8f47-1790">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1790">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1791">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1791">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1792">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1792">See Also</span></span>

- <span data-ttu-id="a8f47-1793">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1793">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1794">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1794">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1795">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1795">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1796">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1796">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1797">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1797">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1798">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1798">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1799">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1799">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1800">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1800">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1801">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1801">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1802">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1802">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1803">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1803">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1804">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1804">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1805">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1805">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1806">fx_file_open fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1806">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="a8f47-1807">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1807">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1808">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1808">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1809">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1809">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1810">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1810">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1811">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1811">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1812">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1812">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1813">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1813">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1814">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1814">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1815">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1815">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1816">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1816">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1817">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1817">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate"></a><span data-ttu-id="a8f47-1818">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1818">fx_file_extended_truncate</span></span>

<span data-ttu-id="a8f47-1819">Dosya keser</span><span class="sxs-lookup"><span data-stu-id="a8f47-1819">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1820">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1820">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="a8f47-1821">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1821">Description</span></span>

<span data-ttu-id="a8f47-1822">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1822">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="a8f47-1823">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1823">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="a8f47-1824">Dosyayla ilişkili medya kümelerinin hiçbiri serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1824">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-1825">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-1825">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="a8f47-1826">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1826">This service is designed for exFAT.</span></span> <span data-ttu-id="a8f47-1827">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır, bu da arayanın 4'lik aralığın ötesinde çalışmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1827">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1828">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1828">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1829">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1829">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-1830">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1830">**size**: New file size.</span></span> <span data-ttu-id="a8f47-1831">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1831">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1832">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1832">Return Values</span></span>

- <span data-ttu-id="a8f47-1833">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1833">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="a8f47-1834">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1834">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="a8f47-1835">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1835">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-1836">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1836">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1837">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1837">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1838">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1838">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1839">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1839">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1840">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1840">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1841">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1841">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="a8f47-1842">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1842">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-1843">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1843">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1844">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1844">Allowed From</span></span>

<span data-ttu-id="a8f47-1845">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1845">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1846">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1846">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1847">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1847">See Also</span></span>

- <span data-ttu-id="a8f47-1848">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1848">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1849">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1849">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1850">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1850">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1851">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1851">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1852">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1852">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1853">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1853">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1854">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1854">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1855">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1855">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1856">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1856">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1857">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1857">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1858">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1858">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1859">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1859">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1860">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1860">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1861">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1861">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1862">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1862">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1863">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1863">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1864">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1864">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1865">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1865">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1866">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1866">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1867">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1867">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1868">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1868">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1869">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1869">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1870">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1870">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1871">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1871">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1872">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1872">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1873">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1873">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate_release"></a><span data-ttu-id="a8f47-1874">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1874">fx_file_extended_truncate_release</span></span>

<span data-ttu-id="a8f47-1875">Dosya ve yayınlar kümesi keser</span><span class="sxs-lookup"><span data-stu-id="a8f47-1875">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1876">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1876">Prototype</span></span>

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a><span data-ttu-id="a8f47-1877">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1877">Description</span></span>

<span data-ttu-id="a8f47-1878">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1878">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="a8f47-1879">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1879">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="a8f47-1880">***Fx_file_extended_truncate*** hizmetinden farklı olarak, bu hizmet kullanılmayan kümeleri serbest bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1880">Unlike the ***fx_file_extended_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-1881">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-1881">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="a8f47-1882">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1882">This service is designed for exFAT.</span></span> <span data-ttu-id="a8f47-1883">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır, bu da arayanın 4'lik aralığın ötesinde çalışmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1883">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1884">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1884">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1885">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1885">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-1886">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1886">**size**: New file size.</span></span> <span data-ttu-id="a8f47-1887">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1887">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1888">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1888">Return Values</span></span>

- <span data-ttu-id="a8f47-1889">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1889">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="a8f47-1890">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1890">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-1891">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1891">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-1892">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1892">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1893">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1893">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-1894">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1894">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1895">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1895">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-1896">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1896">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1897">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1897">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1898">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1898">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-1899">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1899">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-1900">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1900">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1901">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1901">Allowed From</span></span>

<span data-ttu-id="a8f47-1902">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1902">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1903">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1903">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1904">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1904">See Also</span></span>

- <span data-ttu-id="a8f47-1905">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1905">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1906">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1906">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1907">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1907">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1908">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1908">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1909">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-1909">fx_file_close</span></span>
- <span data-ttu-id="a8f47-1910">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1910">fx_file_create</span></span>
- <span data-ttu-id="a8f47-1911">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1911">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1912">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1912">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1913">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1913">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1914">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1914">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1915">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1915">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1916">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1916">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1917">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1917">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1918">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1918">fx_file_open</span></span>
- <span data-ttu-id="a8f47-1919">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1919">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1920">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1920">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1921">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1921">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1922">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1922">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1923">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1923">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1924">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1924">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1925">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1925">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1926">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1926">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1927">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1927">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1928">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1928">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1929">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1929">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1930">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1930">fx_unicode_short_name_get</span></span>

## <a name="fx_file_open"></a><span data-ttu-id="a8f47-1931">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-1931">fx_file_open</span></span>

<span data-ttu-id="a8f47-1932">Dosyayı açar</span><span class="sxs-lookup"><span data-stu-id="a8f47-1932">Opens file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1933">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1933">Prototype</span></span>

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a><span data-ttu-id="a8f47-1934">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1934">Description</span></span>

<span data-ttu-id="a8f47-1935">Bu hizmet, belirtilen dosyayı okuma ya da yazma için açar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1935">This service opens the specified file for either reading or writing.</span></span> <span data-ttu-id="a8f47-1936">Bir dosya birden çok kez okumak için açılabilir, ancak bir dosya yalnızca yazıcı dosyayı kapatana kadar bir kez yazmak üzere açılabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1936">A file may be opened for reading multiple times, while a file can only be opened for writing once until the writer closes the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-1937">*Dosya okuma ve yazma için eşzamanlı olarak açıksa dikkatli olunmalıdır. Bir dosya okuma için eşzamanlı olarak açıldığında gerçekleştirilen dosya yazma işlemi, okuyucu kapanmadığı ve dosyayı okumak üzere yeniden açtığından, okuyucu tarafından görülemeyebilir. Benzer şekilde, dosya Truncate Services kullanılırken dosya yazıcısı dikkatli olmalıdır. Bir dosya yazıcı tarafından kesilmişse, aynı dosyanın okuyucuları geçersiz veri döndürebilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-1937">*Care must be taken if a file is concurrently open for reading and writing. File writing performed when a file is simultaneously opened for reading may not be seen by the reader, unless the reader closes and reopens the file for reading. Similarly, the file writer should be careful when using file truncate services. If a file is truncated by the writer, readers of the same file could return invalid data.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-1938">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1938">Input Parameters</span></span>

- <span data-ttu-id="a8f47-1939">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1939">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-1940">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1940">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-1941">**file_name**: açılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-1941">**file_name**: Pointer to the name of the file to open (directory path is optional).</span></span>
- <span data-ttu-id="a8f47-1942">**open_type**: dosya açma türü.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1942">**open_type**: Type of file open.</span></span> <span data-ttu-id="a8f47-1943">Geçerli açık tür seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-1943">Valid open type options are:</span></span>
  - <span data-ttu-id="a8f47-1944">FX_OPEN_FOR_READ (0x00)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1944">FX_OPEN_FOR_READ (0x00)</span></span>
  - <span data-ttu-id="a8f47-1945">FX_OPEN_FOR_WRITE (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1945">FX_OPEN_FOR_WRITE (0x01)</span></span>
  - <span data-ttu-id="a8f47-1946">FX_OPEN_FOR_READ_FAST (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-1946">FX_OPEN_FOR_READ_FAST (0x02)</span></span>

<span data-ttu-id="a8f47-1947">FX_OPEN_FOR_READ ve FX_OPEN_FOR_READ_FAST dosyaları açmak benzerdir:</span><span class="sxs-lookup"><span data-stu-id="a8f47-1947">Opening files with FX_OPEN_FOR_READ and FX_OPEN_FOR_READ_FAST is similar:</span></span>

- <span data-ttu-id="a8f47-1948">FX_OPEN_FOR_READ, dosyayı oluşturan kümelerin bağlı listesinin bozulmamış olduğunu ve FX_OPEN_FOR_READ_FAST Bu doğrulamayı gerçekleştirmediğinden daha hızlı hale gelmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1948">FX_OPEN_FOR_READ includes verification that the linked-list of clusters that comprise the file are intact, and FX_OPEN_FOR_READ_FAST does not perform this verification, which makes it faster.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-1949">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-1949">Return Values</span></span>

- <span data-ttu-id="a8f47-1950">**FX_SUCCESS** (0x00) başarılı dosya açıldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1950">**FX_SUCCESS** (0x00) Successful file open.</span></span>
- <span data-ttu-id="a8f47-1951">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1951">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-1952">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1952">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="a8f47-1953">**FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1953">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="a8f47-1954">**FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve açma başarısız.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1954">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the open failed.</span></span>
- <span data-ttu-id="a8f47-1955">**FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık veya açma türü geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1955">**FX_ACCESS_ERROR** (0x06) Specified file is already open or open type is invalid.</span></span>
- <span data-ttu-id="a8f47-1956">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1956">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-1957">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1957">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="a8f47-1958">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1958">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-1959">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-1959">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-1960">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1960">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-1961">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1961">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="a8f47-1962">**FX_PTR_ERROR** (0x18) geçersiz medya veya dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1962">**FX_PTR_ERROR** (0x18) Invalid media or file pointer.</span></span>
- <span data-ttu-id="a8f47-1963">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1963">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-1964">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-1964">Allowed From</span></span>

<span data-ttu-id="a8f47-1965">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-1965">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-1966">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1966">Example</span></span>

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-1967">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1967">See Also</span></span>

- <span data-ttu-id="a8f47-1968">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1968">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-1969">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1969">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-1970">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1970">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-1971">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1971">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1972">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1972">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="a8f47-1973">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1973">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-1974">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-1974">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-1975">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1975">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-1976">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1976">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-1977">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1977">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-1978">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1978">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-1979">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1979">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-1980">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1980">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-1981">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1981">fx_file_read</span></span>
- <span data-ttu-id="a8f47-1982">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1982">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-1983">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1983">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-1984">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-1984">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-1985">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-1985">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-1986">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-1986">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-1987">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-1987">fx_file_write</span></span>
- <span data-ttu-id="a8f47-1988">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-1988">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-1989">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-1989">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-1990">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-1990">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-1991">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1991">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-1992">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-1992">fx_unicode_short_name_get</span></span>

## <a name="fx_file_read"></a><span data-ttu-id="a8f47-1993">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-1993">fx_file_read</span></span>

<span data-ttu-id="a8f47-1994">Dosyadan bayt okur</span><span class="sxs-lookup"><span data-stu-id="a8f47-1994">Reads bytes from file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-1995">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-1995">Prototype</span></span>

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a><span data-ttu-id="a8f47-1996">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-1996">Description</span></span>

<span data-ttu-id="a8f47-1997">Bu hizmet, dosyadaki baytları okur ve bunları sağlanan arabellekte depolar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1997">This service reads bytes from the file and stores them in the supplied buffer.</span></span> <span data-ttu-id="a8f47-1998">Okuma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1998">After the read is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span> <span data-ttu-id="a8f47-1999">İstekte daha az bayt kaldığında, yalnızca kalan baytlar arabellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-1999">If there are fewer bytes remaining in the request, only the bytes remaining are stored in the buffer.</span></span> <span data-ttu-id="a8f47-2000">Herhangi bir durumda, arabelleğe yerleştirilmiş baytların toplam sayısı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2000">In any case, the total number of bytes placed in the buffer is returned to the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2001">*Uygulama, sağlanan arabelleğin belirtilen sayıda istenen baytı depolayabilmesini sağlamalıdır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2001">*The application must ensure that the buffer supplied is able to store the specified number of requested bytes.*</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2002">*Hedef arabellek uzun bir sözcüklük sınırındayken ve istenen boyut sizeof (**ulong**) tarafından eşit olarak bölünediyse daha hızlı performans elde edilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2002">*Faster performance is achieved if the destination buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2003">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2003">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2004">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2004">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-2005">**buffer_ptr**: okuma için hedef arabelleğe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2005">**buffer_ptr**: Pointer to the destination buffer for the read.</span></span>
- <span data-ttu-id="a8f47-2006">**request_size**: okunacak en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2006">**request_size**: Maximum number of bytes to read.</span></span>
- <span data-ttu-id="a8f47-2007">**actual_size**: sağlanan arabelleğe okunan gerçek bayt sayısını tutacak değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2007">**actual_size**: Pointer to the variable to hold the actual number of bytes read into the supplied buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2008">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2008">Return Values</span></span>

- <span data-ttu-id="a8f47-2009">**FX_SUCCESS** (0x00) başarılı dosya okundu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2009">**FX_SUCCESS** (0x00) Successful file read.</span></span>
- <span data-ttu-id="a8f47-2010">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2010">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="a8f47-2011">**FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve okuma başarısız.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2011">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the read failed.</span></span>
- <span data-ttu-id="a8f47-2012">**FX_END_OF_FILE** (0x09) dosya sonuna ulaşıldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2012">**FX_END_OF_FILE** (0x09) End of file has been reached.</span></span>
- <span data-ttu-id="a8f47-2013">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2013">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2014">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-2014">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-2015">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2015">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2016">**FX_PTR_ERROR** (0x18) geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2016">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="a8f47-2017">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2017">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2018">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2018">Allowed From</span></span>

<span data-ttu-id="a8f47-2019">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2019">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2020">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2020">Example</span></span>

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
### <a name="see-also"></a><span data-ttu-id="a8f47-2021">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2021">See Also</span></span>

- <span data-ttu-id="a8f47-2022">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2022">fx_file_allocate,</span></span>
- <span data-ttu-id="a8f47-2023">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2023">fx_file_attributes_read,</span></span>
- <span data-ttu-id="a8f47-2024">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2024">fx_file_attributes_set,</span></span>
- <span data-ttu-id="a8f47-2025">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2025">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="a8f47-2026">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2026">fx_file_close,</span></span>
- <span data-ttu-id="a8f47-2027">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2027">fx_file_create,</span></span>
- <span data-ttu-id="a8f47-2028">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2028">fx_file_date_time_set,</span></span>
- <span data-ttu-id="a8f47-2029">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2029">fx_file_delete,</span></span>
- <span data-ttu-id="a8f47-2030">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2030">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="a8f47-2031">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2031">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="a8f47-2032">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2032">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="a8f47-2033">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2033">fx_file_extended_seek,</span></span>
- <span data-ttu-id="a8f47-2034">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2034">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="a8f47-2035">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2035">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="a8f47-2036">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2036">fx_file_open,</span></span>
- <span data-ttu-id="a8f47-2037">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2037">fx_file_relative_seek,</span></span>
- <span data-ttu-id="a8f47-2038">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2038">fx_file_rename,</span></span>
- <span data-ttu-id="a8f47-2039">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2039">fx_file_seek,</span></span>
- <span data-ttu-id="a8f47-2040">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2040">fx_file_truncate,</span></span>
- <span data-ttu-id="a8f47-2041">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2041">fx_file_truncate_release,</span></span>
- <span data-ttu-id="a8f47-2042">fx_file_write,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2042">fx_file_write,</span></span>
- <span data-ttu-id="a8f47-2043">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2043">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="a8f47-2044">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2044">fx_unicode_file_create,</span></span>
- <span data-ttu-id="a8f47-2045">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2045">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="a8f47-2046">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2046">fx_unicode_name_get,</span></span>
- <span data-ttu-id="a8f47-2047">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2047">fx_unicode_short_name_get</span></span>

## <a name="fx_file_relative_seek"></a><span data-ttu-id="a8f47-2048">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2048">fx_file_relative_seek</span></span>

<span data-ttu-id="a8f47-2049">Göreli bayt uzaklığına pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2049">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2050">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2050">Prototype</span></span>

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="a8f47-2051">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2051">Description</span></span>

<span data-ttu-id="a8f47-2052">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2052">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="a8f47-2053">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2053">Any subsequent file read or write request will begin at this location in the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-2054">*Arama işlemi dosyanın sonundan sonra arama yapmayı denerse, dosyanın okuma/yazma işaretçisi dosyanın sonuna yerleştirilir. Buna karşılık, arama işlemi dosyanın başlangıcını aşan konuma çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başlangıcına yerleştirilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2054">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

<span data-ttu-id="a8f47-2055">4 GB 'ın ötesinde bir fark değeri ile arama yapmak için, uygulama Service *fx_file_extended_relative_seek* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2055">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_relative_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2056">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2056">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2057">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2057">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-2058">**byte_offset**: dosyada istenen göreli bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2058">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="a8f47-2059">**seek_from**: göreli arama yapılacak yönün yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2059">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="a8f47-2060">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-2060">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="a8f47-2061">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2061">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="a8f47-2062">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2062">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="a8f47-2063">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2063">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="a8f47-2064">FX_SEEK_BACK (0x03)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2064">FX_SEEK_BACK (0x03)</span></span>

<span data-ttu-id="a8f47-2065">FX_SEEK_BEGIN belirtilirse, arama işlemi dosyanın başından yapılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2065">If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="a8f47-2066">FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2066">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="a8f47-2067">FX_SEEK_FORWARD belirtilirse, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2067">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="a8f47-2068">FX_SEEK_BACK belirtilirse, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2068">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2069">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2069">Return Values</span></span>

- <span data-ttu-id="a8f47-2070">**FX_SUCCESS** (0x00) başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2070">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="a8f47-2071">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2071">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-2072">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2072">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2073">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2074">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2075">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2075">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-2076">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2076">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-2077">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2077">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2078">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2078">Allowed From</span></span>

<span data-ttu-id="a8f47-2079">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2079">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2080">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2080">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-2081">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2081">See Also</span></span>

- <span data-ttu-id="a8f47-2082">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2082">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-2083">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2083">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-2084">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2084">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-2085">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2085">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2086">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2086">fx_file_close</span></span>
- <span data-ttu-id="a8f47-2087">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2087">fx_file_create</span></span>
- <span data-ttu-id="a8f47-2088">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2088">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-2089">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-2089">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-2090">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2090">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-2091">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2091">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2092">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2092">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-2093">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2093">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-2094">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2094">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-2095">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2095">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-2096">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2096">fx_file_open</span></span>
- <span data-ttu-id="a8f47-2097">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2097">fx_file_read</span></span>
- <span data-ttu-id="a8f47-2098">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2098">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-2099">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2099">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-2100">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2100">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-2101">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2101">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-2102">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2102">fx_file_write</span></span>
- <span data-ttu-id="a8f47-2103">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2103">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-2104">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2104">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-2105">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2105">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-2106">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2106">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-2107">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2107">fx_unicode_short_name_get</span></span>

## <a name="fx_file_rename"></a><span data-ttu-id="a8f47-2108">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2108">fx_file_rename</span></span>

<span data-ttu-id="a8f47-2109">Dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="a8f47-2109">Renames  file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2110">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2110">Prototype</span></span>

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-2111">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2111">Description</span></span>

<span data-ttu-id="a8f47-2112">Bu hizmet *old_file_name* tarafından belirtilen dosyanın adını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2112">This service changes the name of the file specified by *old_file_name*.</span></span> <span data-ttu-id="a8f47-2113">Yeniden adlandırma işlemi, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2113">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="a8f47-2114">Yeni dosya adında bir yol belirtilmişse, yeniden adlandırılan dosya belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2114">If a path is specified in the new file name, the renamed file is effectively moved to the specified path.</span></span> <span data-ttu-id="a8f47-2115">Hiçbir yol belirtilmemişse, yeniden adlandırılan dosya geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2115">If no path is specified, the renamed file is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2116">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2116">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2117">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2117">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="a8f47-2118">**old_file_name**: yeniden adlandırılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="a8f47-2118">**old_file_name**: Pointer to the name of the file to rename (directory path is optional).</span></span>
- <span data-ttu-id="a8f47-2119">**new_file_name**: yeni dosya adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2119">**new_file_name**: Pointer to the new file name.</span></span> <span data-ttu-id="a8f47-2120">Dizin yoluna izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2120">The directory path is not allowed.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2121">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2121">Return Values</span></span>

- <span data-ttu-id="a8f47-2122">**FX_SUCCESS** (0x00) başarılı dosya yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2122">**FX_SUCCESS** (0x00) Successful file rename.</span></span>
- <span data-ttu-id="a8f47-2123">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2123">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2124">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2124">**FX_NOT_FOUND** (0x04)    Specified file was not found.</span></span>
- <span data-ttu-id="a8f47-2125">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2125">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="a8f47-2126">**FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2126">**FX_ACCESS_ERROR** (0x06) Specified file is already open.</span></span>
- <span data-ttu-id="a8f47-2127">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2127">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2128">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2128">**FX_WRITE_PROTECT** (0x23)    Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-2129">**FX_INVALID_NAME** (0x0C) belirtilen yeni dosya adı geçerli bir dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2129">**FX_INVALID_NAME** (0x0C) Specified new file name is not a valid file name.</span></span>
- <span data-ttu-id="a8f47-2130">**FX_INVALID_PATH** (0x0D) yolu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2130">**FX_INVALID_PATH** (0x0D)    Path is invalid.</span></span>
- <span data-ttu-id="a8f47-2131">**FX_ALREADY_CREATED** (0x0B) yeni dosya adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2131">**FX_ALREADY_CREATED** (0x0B) The new file name is used.</span></span>
- <span data-ttu-id="a8f47-2132">**FX_MEDIA_INVALID** (0x02) medyası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2132">**FX_MEDIA_INVALID** (0x02)    Media is invalid.</span></span>
- <span data-ttu-id="a8f47-2133">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2133">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2134">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2134">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2135">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2135">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-2136">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-2136">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-2137">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2137">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="a8f47-2138">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2138">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-2139">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2139">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2140">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2140">Allowed From</span></span>

<span data-ttu-id="a8f47-2141">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2142">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2142">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-2143">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2143">See Also</span></span>

- <span data-ttu-id="a8f47-2144">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2144">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-2145">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2145">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-2146">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2146">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-2147">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2147">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2148">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2148">fx_file_close</span></span>
- <span data-ttu-id="a8f47-2149">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2149">fx_file_create</span></span>
- <span data-ttu-id="a8f47-2150">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2150">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-2151">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-2151">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-2152">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2152">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-2153">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2153">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2154">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2154">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-2155">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2155">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-2156">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2156">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-2157">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2157">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-2158">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2158">fx_file_open</span></span>
- <span data-ttu-id="a8f47-2159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2159">fx_file_read</span></span>
- <span data-ttu-id="a8f47-2160">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2160">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-2161">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2161">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-2162">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2162">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-2163">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2163">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-2164">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2164">fx_file_write</span></span>
- <span data-ttu-id="a8f47-2165">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2165">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-2166">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2166">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-2167">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2167">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-2168">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2168">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-2169">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2169">fx_unicode_short_name_get</span></span>

## <a name="fx_file_seek"></a><span data-ttu-id="a8f47-2170">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2170">fx_file_seek</span></span>

<span data-ttu-id="a8f47-2171">Bayt uzaklığa pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2171">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2172">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2172">Prototype</span></span>

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a><span data-ttu-id="a8f47-2173">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2173">Description</span></span>

<span data-ttu-id="a8f47-2174">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen bayt uzaklığa konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2174">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="a8f47-2175">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2175">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="a8f47-2176">4 GB 'ın ötesinde bir fark değeri ile arama yapmak için, uygulama Service *fx_file_extended_seek* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2176">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2177">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2177">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2178">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2178">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-2179">**byte_offset**: dosyada istenen bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2179">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="a8f47-2180">Sıfır değeri, dosyanın başındaki okuma/yazma işaretçisini konumlandırır, ancak dosyanın boyutundan büyük bir değer, dosyanın sonundaki okuma/yazma işaretçisini konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2180">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2181">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2181">Return Values</span></span>

- <span data-ttu-id="a8f47-2182">**FX_SUCCESS** (0x00) başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2182">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="a8f47-2183">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2183">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="a8f47-2184">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2184">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2185">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2185">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2186">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2186">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2187">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-2187">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-2188">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2188">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-2189">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2190">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2190">Allowed From</span></span>

<span data-ttu-id="a8f47-2191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2192">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2192">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-2193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2193">See Also</span></span>

- <span data-ttu-id="a8f47-2194">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2194">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-2195">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2195">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-2196">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2196">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-2197">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2197">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2198">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2198">fx_file_close</span></span>
- <span data-ttu-id="a8f47-2199">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2199">fx_file_create</span></span>
- <span data-ttu-id="a8f47-2200">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2200">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-2201">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-2201">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-2202">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2202">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-2203">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2203">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2204">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2204">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-2205">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2205">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-2206">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2206">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-2207">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2207">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-2208">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2208">fx_file_open</span></span>
- <span data-ttu-id="a8f47-2209">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2209">fx_file_read</span></span>
- <span data-ttu-id="a8f47-2210">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2210">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-2211">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2211">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-2212">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2212">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-2213">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2213">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-2214">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2214">fx_file_write</span></span>
- <span data-ttu-id="a8f47-2215">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2215">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-2216">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2216">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-2217">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2217">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-2218">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2218">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-2219">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2219">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate"></a><span data-ttu-id="a8f47-2220">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2220">fx_file_truncate</span></span>

<span data-ttu-id="a8f47-2221">Dosya keser</span><span class="sxs-lookup"><span data-stu-id="a8f47-2221">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2222">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2222">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="a8f47-2223">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2223">Description</span></span>

<span data-ttu-id="a8f47-2224">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2224">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="a8f47-2225">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2225">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="a8f47-2226">Dosyayla ilişkili medya kümelerinin hiçbiri serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2226">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2227">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2227">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="a8f47-2228">4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2228">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2229">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2229">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2230">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2230">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-2231">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2231">**size**: New file size.</span></span> <span data-ttu-id="a8f47-2232">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2232">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2233">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2233">Return Values</span></span>

- <span data-ttu-id="a8f47-2234">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2234">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="a8f47-2235">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2235">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="a8f47-2236">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2236">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-2237">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2237">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2238">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2238">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-2239">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2239">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2240">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2240">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2241">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2241">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-2242">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-2242">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="a8f47-2243">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2243">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-2244">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2244">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2245">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2245">Allowed From</span></span>

<span data-ttu-id="a8f47-2246">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2247">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2247">Example</span></span>

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-2248">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2248">See Also</span></span>

- <span data-ttu-id="a8f47-2249">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2249">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-2250">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2250">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-2251">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2251">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-2252">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2252">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2253">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2253">fx_file_close</span></span>
- <span data-ttu-id="a8f47-2254">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2254">fx_file_create</span></span>
- <span data-ttu-id="a8f47-2255">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2255">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-2256">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-2256">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-2257">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2257">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-2258">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2258">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2259">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2259">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-2260">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2260">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-2261">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2261">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-2262">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2262">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-2263">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2263">fx_file_open</span></span>
- <span data-ttu-id="a8f47-2264">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2264">fx_file_read</span></span>
- <span data-ttu-id="a8f47-2265">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2265">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-2266">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2266">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-2267">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2267">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-2268">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2268">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-2269">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2269">fx_file_write</span></span>
- <span data-ttu-id="a8f47-2270">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2270">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-2271">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2271">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-2272">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2272">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-2273">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2273">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-2274">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2274">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate_release"></a><span data-ttu-id="a8f47-2275">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2275">fx_file_truncate_release</span></span>

<span data-ttu-id="a8f47-2276">Dosya ve yayınlar kümesi keser</span><span class="sxs-lookup"><span data-stu-id="a8f47-2276">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2277">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2277">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="a8f47-2278">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2278">Description</span></span>

<span data-ttu-id="a8f47-2279">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2279">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="a8f47-2280">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2280">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="a8f47-2281">***Fx_file_truncate*** hizmetinden farklı olarak, bu hizmet kullanılmayan kümeleri serbest bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2281">Unlike the ***fx_file_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2282">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2282">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="a8f47-2283">4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate_release* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2283">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate_release*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2284">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2284">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2285">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2285">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="a8f47-2286">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2286">**size**: New file size.</span></span> <span data-ttu-id="a8f47-2287">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2287">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2288">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2288">Return Values</span></span>

- <span data-ttu-id="a8f47-2289">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2289">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="a8f47-2290">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2290">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-2291">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2291">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="a8f47-2292">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2292">**FX_IO_ERROR** (0x90)    Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2293">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2293">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="a8f47-2294">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2294">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2295">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2295">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2296">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2296">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-2297">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2297">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-2298">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2298">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation.</span></span>
- <span data-ttu-id="a8f47-2299">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2299">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="a8f47-2300">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2300">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2301">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2301">Allowed From</span></span>

<span data-ttu-id="a8f47-2302">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2303">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2303">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a><span data-ttu-id="a8f47-2304">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2304">See Also</span></span>

- <span data-ttu-id="a8f47-2305">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2305">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-2306">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2306">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-2307">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2307">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-2308">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2308">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2309">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2309">fx_file_close</span></span>
- <span data-ttu-id="a8f47-2310">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2310">fx_file_create</span></span>
- <span data-ttu-id="a8f47-2311">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2311">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-2312">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-2312">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-2313">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2313">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-2314">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2314">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2315">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2315">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-2316">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2316">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-2317">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2317">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-2318">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2318">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-2319">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2319">fx_file_open</span></span>
- <span data-ttu-id="a8f47-2320">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2320">fx_file_read</span></span>
- <span data-ttu-id="a8f47-2321">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2321">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-2322">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2322">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-2323">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2323">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-2324">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2324">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-2325">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2325">fx_file_write</span></span>
- <span data-ttu-id="a8f47-2326">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2326">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-2327">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2327">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-2328">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2328">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-2329">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2329">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-2330">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2330">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write"></a><span data-ttu-id="a8f47-2331">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2331">fx_file_write</span></span>

<span data-ttu-id="a8f47-2332">Baytları dosyaya yazar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2332">Writes bytes to file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2333">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2333">Prototype</span></span>

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="a8f47-2334">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2334">Description</span></span>

<span data-ttu-id="a8f47-2335">Bu hizmet, dosyanın geçerli konumundan başlayarak belirtilen arabellekteki baytları yazar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2335">This service writes bytes from the specified buffer starting at the file's current position.</span></span> <span data-ttu-id="a8f47-2336">Yazma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2336">After the write is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2337">*Kaynak arabelleğinin uzun bir sözcüklük sınırında olması ve istenen boyutun sizeof (**ulong**) tarafından eşit olarak bölünemesinin ardından daha hızlı performans elde edilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2337">*Faster performance is achieved if the source buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2338">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2338">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2339">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2339">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-2340">**buffer_ptr**: yazma için kaynak arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2340">**buffer_ptr**: Pointer to the source buffer for the write.</span></span>
- <span data-ttu-id="a8f47-2341">**Boyut**: yazılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2341">**size**: Number of bytes to write.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2342">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2342">Return Values</span></span>

- <span data-ttu-id="a8f47-2343">**FX_SUCCESS** (0x00) başarılı dosya yazma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2343">**FX_SUCCESS** (0x00) Successful file write.</span></span>
- <span data-ttu-id="a8f47-2344">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2344">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="a8f47-2345">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2345">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="a8f47-2346">**FX_NO_MORE_SPACE** (0x0A) medyada bu yazma işlemini gerçekleştirmek için kullanılabilecek daha fazla yer yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2346">**FX_NO_MORE_SPACE** (0x0A) There is no more room available in the media to perform this write.</span></span>
- <span data-ttu-id="a8f47-2347">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2347">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2348">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2348">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-2349">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2349">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2350">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2350">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2351">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2351">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="a8f47-2352">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2352">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="a8f47-2353">**FX_PTR_ERROR** (0x18) geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2353">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="a8f47-2354">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2354">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2355">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2355">Allowed From</span></span>

<span data-ttu-id="a8f47-2356">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2356">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2357">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2357">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-2358">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2358">See Also</span></span>

- <span data-ttu-id="a8f47-2359">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2359">fx_file_allocate,</span></span>
- <span data-ttu-id="a8f47-2360">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2360">fx_file_attributes_read,</span></span>
- <span data-ttu-id="a8f47-2361">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2361">fx_file_attributes_set,</span></span>
- <span data-ttu-id="a8f47-2362">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2362">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="a8f47-2363">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2363">fx_file_close,</span></span>
- <span data-ttu-id="a8f47-2364">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2364">fx_file_create,</span></span>
- <span data-ttu-id="a8f47-2365">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2365">fx_file_date_time_set,</span></span>
- <span data-ttu-id="a8f47-2366">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2366">fx_file_delete,</span></span>
- <span data-ttu-id="a8f47-2367">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2367">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="a8f47-2368">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2368">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="a8f47-2369">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2369">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="a8f47-2370">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2370">fx_file_extended_seek,</span></span>
- <span data-ttu-id="a8f47-2371">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2371">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="a8f47-2372">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2372">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="a8f47-2373">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2373">fx_file_open,</span></span>
- <span data-ttu-id="a8f47-2374">fx_file_read,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2374">fx_file_read,</span></span>
- <span data-ttu-id="a8f47-2375">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2375">fx_file_relative_seek,</span></span>
- <span data-ttu-id="a8f47-2376">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2376">fx_file_rename,</span></span>
- <span data-ttu-id="a8f47-2377">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2377">fx_file_seek,</span></span>
- <span data-ttu-id="a8f47-2378">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2378">fx_file_truncate,</span></span>
- <span data-ttu-id="a8f47-2379">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2379">fx_file_truncate_release,</span></span>
- <span data-ttu-id="a8f47-2380">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2380">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="a8f47-2381">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2381">fx_unicode_file_create,</span></span>
- <span data-ttu-id="a8f47-2382">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2382">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="a8f47-2383">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="a8f47-2383">fx_unicode_name_get,</span></span>
- <span data-ttu-id="a8f47-2384">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2384">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write_notify_set"></a><span data-ttu-id="a8f47-2385">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2385">fx_file_write_notify_set</span></span>

<span data-ttu-id="a8f47-2386">Dosya yazma bildirim işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2386">Sets the file write notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2387">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2387">Prototype</span></span>

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a><span data-ttu-id="a8f47-2388">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2388">Description</span></span>

<span data-ttu-id="a8f47-2389">Bu hizmet, başarılı bir dosya yazma işleminden sonra çağrılan geri çağırma işlevini yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2389">This service installs callback function that is invoked after a successful file write operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2390">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2390">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2391">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2391">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="a8f47-2392">**file_write_notify**: yüklenecek dosya yazma geri arama işlevi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2392">**file_write_notify**: File write callback function to be installed.</span></span> <span data-ttu-id="a8f47-2393">Callback işlevini NULL olarak ayarlayın geri çağırma işlevini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2393">Set the callback function to NULL disables the callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2394">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2394">Return Values</span></span>

- <span data-ttu-id="a8f47-2395">**FX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2395">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="a8f47-2396">**FX_PTR_ERROR** (0x18) file_ptr null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2396">**FX_PTR_ERROR** (0x18) file_ptr is NULL.</span></span>
- <span data-ttu-id="a8f47-2397">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2397">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2398">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2398">Allowed From</span></span>

<span data-ttu-id="a8f47-2399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2400">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2400">Example</span></span>

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2401">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2401">See Also</span></span>

- <span data-ttu-id="a8f47-2402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2402">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-2403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2403">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-2404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2404">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-2405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2406">fx_file_close</span></span>
- <span data-ttu-id="a8f47-2407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2407">fx_file_create</span></span>
- <span data-ttu-id="a8f47-2408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2408">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-2409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-2409">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-2410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-2411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-2412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-2413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2413">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-2414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-2415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-2416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2416">fx_file_open</span></span>
- <span data-ttu-id="a8f47-2417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2417">fx_file_read</span></span>
- <span data-ttu-id="a8f47-2418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2418">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-2419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2419">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-2420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2420">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-2421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2421">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-2422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-2422">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-2423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2423">fx_file_write</span></span>
- <span data-ttu-id="a8f47-2424">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-2424">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-2425">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-2425">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-2426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2426">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-2427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2427">fx_unicode_short_name_get</span></span>

## <a name="fx_media_abort"></a><span data-ttu-id="a8f47-2428">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2428">fx_media_abort</span></span>

<span data-ttu-id="a8f47-2429">Medya etkinliklerini iptal eder</span><span class="sxs-lookup"><span data-stu-id="a8f47-2429">Aborts media activities</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2430">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2430">Prototype</span></span>

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-2431">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2431">Description</span></span>

<span data-ttu-id="a8f47-2432">Bu hizmet, tüm açık dosyaları kapatma, ilişkili sürücüye bir iptal isteği gönderme ve medyayı durdurulmuş duruma yerleştirme dahil olmak üzere medyayla ilişkili tüm geçerli etkinlikleri iptal eder.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2432">This service aborts all current activities associated with the media, including closing all open files, sending an abort request to the associated driver, and placing the media in an aborted state.</span></span> <span data-ttu-id="a8f47-2433">Bu hizmet genellikle g/ç hataları algılandığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2433">This service is typically called when I/O errors are detected.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2434">*Bir iptal işlemi gerçekleştirildikten sonra yeniden kullanmak için medyanın yeniden açılması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2434">*The media must be re-opened to use it again after an abort operation is performed.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2435">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2435">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2436">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2436">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2437">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2437">Return Values</span></span>

- <span data-ttu-id="a8f47-2438">**FX_SUCCESS** (0x00) başarılı medya iptali.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2438">**FX_SUCCESS** (0x00) Successful media abort.</span></span>
- <span data-ttu-id="a8f47-2439">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2439">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2440">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2440">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-2441">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2441">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2442">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2442">Allowed From</span></span>

<span data-ttu-id="a8f47-2443">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2444">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2444">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2445">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2445">See Also</span></span>

- <span data-ttu-id="a8f47-2446">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2446">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2447">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2447">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2448">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2448">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2449">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2449">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2450">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2450">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2451">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2451">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2452">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2452">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2453">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2453">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2454">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2454">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2455">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2455">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2456">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2456">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2457">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2457">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2458">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2458">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2459">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2459">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2460">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2460">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2461">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2461">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2462">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2462">fx_system_initialize</span></span>

## <a name="fx_media_cache_invalidate"></a><span data-ttu-id="a8f47-2463">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2463">fx_media_cache_invalidate</span></span>

<span data-ttu-id="a8f47-2464">Mantıksal kesim önbelleğini geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2464">Invalidates logical sector cache</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2465">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2465">Prototype</span></span>

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="a8f47-2466">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2466">Description</span></span>

<span data-ttu-id="a8f47-2467">Bu hizmet önbellekteki tüm kirli kesimleri temizler ve sonra mantıksal kesim önbelleğinin tamamını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2467">This service flushes all dirty sectors in the cache and then invalidates the entire logical sector cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2468">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2468">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2469">**media_ptr**: medya denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="a8f47-2469">**media_ptr**: Pointer to media control block</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2470">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2470">Return Values</span></span>

- <span data-ttu-id="a8f47-2471">**FX_SUCCESS** (0x00) başarılı medya önbelleği geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2471">**FX_SUCCESS** (0x00) Successful media cache invalidate.</span></span>
- <span data-ttu-id="a8f47-2472">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2472">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2473">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2473">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2474">**FX_PTR_ERROR** (0x18) geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2474">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="a8f47-2475">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2475">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2476">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2476">Allowed From</span></span>

<span data-ttu-id="a8f47-2477">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2478">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2478">Example</span></span>

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2479">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2479">See Also</span></span>

- <span data-ttu-id="a8f47-2480">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2480">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2481">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2481">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2482">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2482">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2483">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2483">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2484">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2484">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2485">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2485">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2486">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2486">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2487">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2487">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2488">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2488">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2489">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2489">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2490">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2490">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2491">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2491">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2492">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2492">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2493">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2493">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2494">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2494">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2495">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2495">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2496">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2496">fx_system_initialize</span></span>

## <a name="fx_media_check"></a><span data-ttu-id="a8f47-2497">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2497">fx_media_check</span></span>

<span data-ttu-id="a8f47-2498">Medyayı hatalara karşı denetler</span><span class="sxs-lookup"><span data-stu-id="a8f47-2498">Checks media for errors</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2499">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2499">Prototype</span></span>

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-2500">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2500">Description</span></span>

<span data-ttu-id="a8f47-2501">Bu hizmet, dosya/dizin çapraz bağlantı, geçersiz FAT zincirleri ve kayıp kümeler dahil olmak üzere temel yapısal hatalar için belirtilen medyayı denetler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2501">This service checks the specified media for basic structural errors, including file/directory cross-linking, invalid FAT chains, and lost clusters.</span></span> <span data-ttu-id="a8f47-2502">Bu hizmet, algılanan hataları düzeltme yeteneği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2502">This service also provides the capability to correct detected errors.</span></span>

<span data-ttu-id="a8f47-2503">Fx_media_check hizmeti, ortamdaki dizinlerin ve dosyaların derinlemesine ilk analizi için karalama belleği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2503">The fx_media_check service requires scratch memory for its depth-first analysis of directories and files in the media.</span></span> <span data-ttu-id="a8f47-2504">Özellikle, medya denetimi hizmeti için sağlanan karalama belleği, birkaç dizin girişi tutabilecek kadar büyük olmalıdır, alt dizinlere girmeden önce geçerli dizin girişi konumunu "Stack" e bir veri yapısı ve son olarak mantıksal FAT bit eşlem.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2504">Specifically, the scratch memory supplied to the media check service must be large enough to hold several directory entries, a data structure to "stack" the current directory entry position before entering into subdirectories, and finally the logical FAT bit map.</span></span> <span data-ttu-id="a8f47-2505">Boş bellek, medyada kümeler olduğundan çok sayıda bit olması gereken mantıksal FAT bit eşlem için en az 512-1024 bayt artı bellek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2505">The scratch memory should be at least 512-1024 bytes plus memory for the logical FAT bit map, which requires as many bits as there are clusters in the media.</span></span> <span data-ttu-id="a8f47-2506">Örneğin, 8000 kümesi olan bir cihaz için 1000 bayt ve bu nedenle 2048 bayt düzeninde toplam bir karalama alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2506">For example, a device with 8000 clusters would require 1000 bytes to represent and thus require a total scratch area on the order of 2048 bytes.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2507">*Bu hizmet yalnızca fx_media_open ve diğer herhangi bir dosya sistemi etkinliği olmadan hemen çağrılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2507">*This service should only be called immediately after fx_media_open and without any other file system activity.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2508">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2508">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2509">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2509">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-2510">**scratch_memory_ptr**: karalama belleğinin başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2510">**scratch_memory_ptr**: Pointer to the start of scratch memory.</span></span>
- <span data-ttu-id="a8f47-2511">**scratch_memory_size**: boş belleğin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2511">**scratch_memory_size**: Size of scratch memory in bytes.</span></span>
- <span data-ttu-id="a8f47-2512">**error_correction_option**: hata düzeltme seçeneği bitleri, bit ayarlandığında hata düzeltme gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2512">**error_correction_option**: Error correction option bits, when the bit is set, error correction is performed.</span></span> <span data-ttu-id="a8f47-2513">Hata düzeltme seçeneği bitleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-2513">The error correction option bits are defined as follows:</span></span>
  - <span data-ttu-id="a8f47-2514">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2514">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="a8f47-2515">FX_DIRECTORY_ERROR (0x02)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2515">FX_DIRECTORY_ERROR (0x02)</span></span>
  - <span data-ttu-id="a8f47-2516">Gerekli hata düzeltme seçeneklerini yalnızca bir arada FX_LOST_CLUSTER_ERROR (0x04).</span><span class="sxs-lookup"><span data-stu-id="a8f47-2516">FX_LOST_CLUSTER_ERROR (0x04) Simply OR together the required error correction options.</span></span> <span data-ttu-id="a8f47-2517">Hata düzeltmesi gerekmiyorsa 0 değeri sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2517">If no error correction is required, a value of 0 should be supplied.</span></span>
- <span data-ttu-id="a8f47-2518">**errors_detected_ptr**: aşağıda tanımlandığı şekilde hata algılama bitleri için hedef:</span><span class="sxs-lookup"><span data-stu-id="a8f47-2518">**errors_detected_ptr**: Destination for error detection bits, as defined below:</span></span>
  - <span data-ttu-id="a8f47-2519">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2519">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="a8f47-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span></span>
  - <span data-ttu-id="a8f47-2521">FX_FILE_SIZE_ERROR (0x08)</span><span class="sxs-lookup"><span data-stu-id="a8f47-2521">FX_FILE_SIZE_ERROR (0x08)</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2522">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2522">Return Values</span></span>

- <span data-ttu-id="a8f47-2523">**FX_SUCCESS** (0x00) başarılı medya denetimi, Ayrıntılar için algılanan hedef hatalarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2523">**FX_SUCCESS** (0x00) Successful media check, view the errors detected destination for details.</span></span>
- <span data-ttu-id="a8f47-2524">**FX_ACCESS_ERROR** (0x06) açık dosyalarla denetim yapılamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2524">**FX_ACCESS_ERROR** (0x06) Unable to perform check with open files.</span></span>
- <span data-ttu-id="a8f47-2525">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2525">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2526">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2526">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2527">**FX_NO_MORE_SPACE** (0x0A) medyada daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2527">**FX_NO_MORE_SPACE** (0x0A) No more space on the media.</span></span>
- <span data-ttu-id="a8f47-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) sağlanan karalama belleği yeterince büyük değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) Supplied scratch memory is not large enough.</span></span>
- <span data-ttu-id="a8f47-2529">**FX_ERROR_NOT_FIXED** (0x93) DÜZELTILMEYEN FAT32 kök dizininin bozulması.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2529">**FX_ERROR_NOT_FIXED** (0x93) Corruption of FAT32 root directory that could not be fixed.</span></span>
- <span data-ttu-id="a8f47-2530">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2531">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2531">**FX_SECTOR_INVALID** (0x89) Sector is invalid.</span></span>
- <span data-ttu-id="a8f47-2532">**FX_PTR_ERROR** (0x18) geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2532">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="a8f47-2533">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="a8f47-2534">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2534">Allowed From</span></span>

<span data-ttu-id="a8f47-2535">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2536">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2536">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-2537">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2537">See Also</span></span>

- <span data-ttu-id="a8f47-2538">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2538">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2539">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2539">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2540">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2540">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2541">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2541">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2542">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2542">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2543">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2543">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2544">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2544">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2545">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2545">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2546">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2546">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2547">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2547">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2548">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2548">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2549">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2549">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2550">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2550">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2551">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2551">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2552">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2552">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2553">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2553">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2554">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2554">fx_system_initialize</span></span>

## <a name="fx_media_close"></a><span data-ttu-id="a8f47-2555">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2555">fx_media_close</span></span>

<span data-ttu-id="a8f47-2556">Medyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="a8f47-2556">Closes media</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2557">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2557">Prototype</span></span>

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-2558">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2558">Description</span></span>

<span data-ttu-id="a8f47-2559">Bu hizmet, belirtilen medyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2559">This service closes the specified media.</span></span> <span data-ttu-id="a8f47-2560">Medyayı kapatma sürecinde, tüm açık dosyalar kapatılır ve kalan arabellekler fiziksel medyaya silinir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2560">In the process of closing the media, all open files are closed and any remaining buffers are flushed to the physical media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2561">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2561">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2562">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2562">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2563">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2563">Return Values</span></span>

- <span data-ttu-id="a8f47-2564">**FX_SUCCESS** (0x00) başarılı medya kapatma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2564">**FX_SUCCESS** (0x00) Successful media close.</span></span>
- <span data-ttu-id="a8f47-2565">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2565">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2566">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2566">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2567">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2567">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-2568">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2568">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2569">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2569">Allowed From</span></span>

<span data-ttu-id="a8f47-2570">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2571">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2571">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2572">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2572">See Also</span></span>

- <span data-ttu-id="a8f47-2573">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2573">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2574">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2574">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2575">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2575">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2576">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2576">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2577">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2577">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2578">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2578">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2579">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2579">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2580">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2580">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2581">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2581">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2582">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2582">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2583">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2583">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2584">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2584">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2585">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2585">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2586">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2586">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2587">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2587">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2588">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2588">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2589">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2589">fx_system_initialize</span></span>

## <a name="fx_media_close_notify_set"></a><span data-ttu-id="a8f47-2590">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2590">fx_media_close_notify_set</span></span>

<span data-ttu-id="a8f47-2591">Medya kapatma bildirimi işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2591">Sets the media close notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2592">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2592">Prototype</span></span>

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a><span data-ttu-id="a8f47-2593">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2593">Description</span></span>

<span data-ttu-id="a8f47-2594">Bu hizmet, bir medya başarıyla kapatıldıktan sonra çağrılacak bir bildirim geri arama işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2594">This service sets a notify callback function which will be invoked after a media is successfully closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2595">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2595">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2596">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2596">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-2597">**media_close_notify**: medya kapatma geri arama işlevi yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2597">**media_close_notify**: Media close notify callback function to be installed.</span></span> <span data-ttu-id="a8f47-2598">Geri çağırma işlevi olarak NULL geçirme, medya kapatma geri aramasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2598">Passing NULL as the callback function disables the media close callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2599">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2599">Return Values</span></span>

- <span data-ttu-id="a8f47-2600">**FX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2600">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="a8f47-2601">**FX_PTR_ERROR** (0x18) media_ptr null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2601">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="a8f47-2602">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2602">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2603">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2603">Allowed From</span></span>

<span data-ttu-id="a8f47-2604">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2604">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2605">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2605">Example</span></span>

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a><span data-ttu-id="a8f47-2606">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2606">See Also</span></span>

- <span data-ttu-id="a8f47-2607">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2607">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2608">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2608">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2609">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2609">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2610">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2610">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2611">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2611">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2612">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2612">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2613">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2613">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2614">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2614">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2615">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2615">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2616">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2616">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2617">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2617">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2618">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2618">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2619">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2619">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2620">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2620">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2621">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2621">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2622">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2622">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2623">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2623">fx_system_initialize</span></span>

## <a name="fx_media_exfat_format"></a><span data-ttu-id="a8f47-2624">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2624">fx_media_exFAT_format</span></span>

<span data-ttu-id="a8f47-2625">Medyayı biçimlendirir</span><span class="sxs-lookup"><span data-stu-id="a8f47-2625">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2626">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2626">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="a8f47-2627">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2627">Description</span></span>

<span data-ttu-id="a8f47-2628">Bu hizmet verilen medyayı sağlanan parametrelere göre exFAT ile uyumlu bir şekilde biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2628">This service formats the supplied media in an exFAT compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="a8f47-2629">Medyayı açmadan önce bu hizmetin çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2629">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2630">*Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2630">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-2631">*ExFAT birim boyutu bölümün boyutuyla (MBR veya GPT düzeni varsa) veya bölüm düzeni yoksa (MBR veya GPT) tüm cihazın boyutuna eşleşmelidir. Windows üzerinde, kullanılabilir sektörden daha az sayıda toplam sektörde biçimlendirildiyse exFAT diskinin bir kısıtlaması yoktur*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2631">*The exFAT volume size should match the size of the partition (if there is an MBR or GPT layout), or the size of the whole device if there is no partition layout (no MBR or GPT). There is a limitation on Windows that exFAT Disk will not be recoginzed if formatted with some values of total sectors that are less than available sectors*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2632">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2632">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2633">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2633">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="a8f47-2634">Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2634">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="a8f47-2635">**sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2635">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="a8f47-2636">Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2636">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="a8f47-2637">**driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2637">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="a8f47-2638">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2638">**memory_ptr**: Pointer to the working memory for the media.</span></span> <span data-ttu-id="a8f47-2639">memory_size, çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2639">memory_size Specifies the size of the working media memory.</span></span> <span data-ttu-id="a8f47-2640">Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2640">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="a8f47-2641">**Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2641">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="a8f47-2642">**number_of_fats**: medyadaki Fats sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2642">**number_of_fats**: Number of FATs on the media.</span></span> <span data-ttu-id="a8f47-2643">Geçerli uygulama, medyada bir FAT 'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2643">Current implementation supports one FAT on the media.</span></span>
- <span data-ttu-id="a8f47-2644">**hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2644">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="a8f47-2645">Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2645">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="a8f47-2646">**total_sectors**: medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2646">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="a8f47-2647">**bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2647">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="a8f47-2648">FileX, bunun 32 katı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2648">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="a8f47-2649">**sectors_per_cluster**: her kümedeki sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2649">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="a8f47-2650">Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2650">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="a8f47-2651">**volumne_serial_number**: Bu birim için kullanılacak seri numarası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2651">**volumne_serial_number**: Serial number to be used for this volume.</span></span>
- <span data-ttu-id="a8f47-2652">**boundary_unit**: fiziksel veri alanı hizalama boyutu, kesim sayısı olarak.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2652">**boundary_unit**: Physical data area alignment size, in number of sectors.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2653">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2653">Return Values</span></span>

- <span data-ttu-id="a8f47-2654">**FX_SUCCESS** (0x00) başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2654">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="a8f47-2655">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2655">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2656">**FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2656">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="a8f47-2657">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2657">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2658">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2658">Allowed From</span></span>

<span data-ttu-id="a8f47-2659">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2659">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2660">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2660">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-2661">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2661">See Also</span></span>

- <span data-ttu-id="a8f47-2662">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2662">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2663">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2663">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2664">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2664">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2665">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2665">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2666">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2666">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2667">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2667">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2668">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2668">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2669">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2669">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2670">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2670">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2671">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2671">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2672">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2672">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2673">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2673">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2674">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2674">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2675">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2675">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2676">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2676">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2677">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2677">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2678">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2678">fx_system_initialize</span></span>

## <a name="fx_media_extended_space_available"></a><span data-ttu-id="a8f47-2679">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2679">fx_media_extended_space_available</span></span>

<span data-ttu-id="a8f47-2680">Kullanılabilir medya alanını döndürür</span><span class="sxs-lookup"><span data-stu-id="a8f47-2680">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2681">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2681">Prototype</span></span>

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-2682">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2682">Description</span></span>

<span data-ttu-id="a8f47-2683">Bu hizmet, medyada kullanılabilir olan bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2683">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="a8f47-2684">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2684">This service is designed for exFAT.</span></span> <span data-ttu-id="a8f47-2685">*Available_bytes* parametresi işaretçisi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 ' ün üzerinde medya ile çalışmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2685">The pointer to *available_bytes* parameter takes a 64-bit integer value, which allows the caller to work with media beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2686">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2686">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2687">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2687">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="a8f47-2688">**available_bytes_ptr**: medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2688">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2689">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2689">Return Values</span></span>

- <span data-ttu-id="a8f47-2690">**FX_SUCCESS** (0x00) medyada bulunan alanı başarıyla aldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2690">**FX_SUCCESS** (0x00) Successfully retrieved space available on the media.</span></span>
- <span data-ttu-id="a8f47-2691">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2691">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2692">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2692">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="a8f47-2693">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2693">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2694">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2694">Allowed From</span></span>

<span data-ttu-id="a8f47-2695">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2695">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2696">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2696">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2697">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2697">See Also</span></span>

- <span data-ttu-id="a8f47-2698">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2698">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2699">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2699">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2700">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2700">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2701">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2701">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2702">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2702">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2703">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2703">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2704">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2704">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2705">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2705">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2706">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2706">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2707">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2707">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2708">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2708">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2709">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2709">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2710">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2710">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2711">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2711">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2712">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2712">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2713">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2713">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2714">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2714">fx_system_initialize</span></span>

## <a name="fx_media_flush"></a><span data-ttu-id="a8f47-2715">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2715">fx_media_flush</span></span>

<span data-ttu-id="a8f47-2716">Fiziksel medyada verileri boşaltır</span><span class="sxs-lookup"><span data-stu-id="a8f47-2716">Flushes data to physical media</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2717">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2717">Prototype</span></span>

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-2718">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2718">Description</span></span>

<span data-ttu-id="a8f47-2719">Bu hizmet, herhangi bir değiştirilen dosyanın tüm önbelleğe alınan kesimlerini ve dizin girdilerini fiziksel medyada boşaltır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2719">This service flushes all cached sectors and directory entries of any modified files to the physical media.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2720">*Bu yordam, hedef üzerinde ani bir güç kaybı olması durumunda dosya bozulması ve/veya veri kaybı riskini azaltmak için uygulama tarafından düzenli aralıklarla çağrılabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2720">*This routine may be called periodically by the application to reduce the risk of file corruption and/or data loss in the event of a sudden loss of power on the target.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2721">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2721">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2722">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2722">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2723">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2723">Return Values</span></span>

- <span data-ttu-id="a8f47-2724">**FX_SUCCESS** (0x00) başarılı medya Temizleme.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2724">**FX_SUCCESS** (0x00) Successful media flush.</span></span>
- <span data-ttu-id="a8f47-2725">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2725">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2726">**FX_FILE_CORRUPT**    (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2726">**FX_FILE_CORRUPT**    (0x08) File is corrupted.</span></span>
- <span data-ttu-id="a8f47-2727">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2727">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2728">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2728">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2729">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2729">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-2730">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2730">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-2731">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2731">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2732">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2732">Allowed From</span></span>

<span data-ttu-id="a8f47-2733">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2733">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2734">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2734">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2735">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2735">See Also</span></span>

- <span data-ttu-id="a8f47-2736">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2736">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2737">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2737">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2738">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2738">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2739">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2739">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2740">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2740">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2741">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2741">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2742">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2742">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2743">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2743">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2744">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2744">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2745">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2745">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2746">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2746">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2747">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2747">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2748">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2748">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2749">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2749">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2750">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2750">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2751">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2751">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2752">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2752">fx_system_initialize</span></span>

## <a name="fx_media_format"></a><span data-ttu-id="a8f47-2753">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2753">fx_media_format</span></span>

<span data-ttu-id="a8f47-2754">Medyayı biçimlendirir</span><span class="sxs-lookup"><span data-stu-id="a8f47-2754">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2755">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2755">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="a8f47-2756">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2756">Description</span></span>

<span data-ttu-id="a8f47-2757">Bu hizmet verilen medyayı sağlanan parametrelere göre FAT 12/16/32 ile uyumlu bir şekilde biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2757">This service formats the supplied media in a FAT 12/16/32 compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="a8f47-2758">Medyayı açmadan önce bu hizmetin çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2758">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2759">*Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2759">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2760">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2760">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2761">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2761">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="a8f47-2762">Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2762">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="a8f47-2763">**sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2763">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="a8f47-2764">Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2764">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="a8f47-2765">**driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2765">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="a8f47-2766">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2766">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="a8f47-2767">**memory_size**: çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2767">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="a8f47-2768">Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2768">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="a8f47-2769">**Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2769">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="a8f47-2770">**number_of_fats**: medyadaki Fats sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2770">**number_of_fats**: Number of FATs in the media.</span></span> <span data-ttu-id="a8f47-2771">Birincil FAT için en düşük değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2771">The minimal value is 1 for the primary FAT.</span></span> <span data-ttu-id="a8f47-2772">1 ' den büyük değerler, çalışma zamanında sürdürülmekte olan ek FAT kopyalarla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2772">Values greater than 1 result in additional FAT copies being maintained at run-time.</span></span>
- <span data-ttu-id="a8f47-2773">**directory_entries**: kök dizindeki Dizin girişi sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2773">**directory_entries**: Number of directory entries in the root directory.</span></span>
- <span data-ttu-id="a8f47-2774">**hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2774">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="a8f47-2775">Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2775">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="a8f47-2776">**total_sectors**: medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2776">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="a8f47-2777">**bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2777">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="a8f47-2778">FileX, bunun 32 katı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2778">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="a8f47-2779">**sectors_per_cluster**: her kümedeki sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2779">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="a8f47-2780">Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2780">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="a8f47-2781">**Heads**: fiziksel kafa sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2781">**heads**: Number of physical heads.</span></span>
- <span data-ttu-id="a8f47-2782">**sectors_per_track**: iz başına kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2782">**sectors_per_track**: Number of sectors per track.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2783">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2783">Return Values</span></span>

- <span data-ttu-id="a8f47-2784">**FX_SUCCESS** (0x00) başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2784">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="a8f47-2785">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2785">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2786">**FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2786">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="a8f47-2787">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2787">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2788">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2788">Allowed From</span></span>

<span data-ttu-id="a8f47-2789">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2789">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2790">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2790">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-2791">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2791">See Also</span></span>

- <span data-ttu-id="a8f47-2792">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2792">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2793">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2793">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2794">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2794">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2795">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2795">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2796">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2796">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2797">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2797">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2798">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2798">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2799">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2799">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2800">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2800">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2801">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2801">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2802">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2802">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2803">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2803">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2804">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2804">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2805">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2805">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2806">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2806">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2807">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2807">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2808">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2808">fx_system_initialize</span></span>

## <a name="fx_media_open"></a><span data-ttu-id="a8f47-2809">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2809">fx_media_open</span></span>

<span data-ttu-id="a8f47-2810">Dosya erişimi için medyayı açar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2810">Opens media for file access</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2811">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2811">Prototype</span></span>

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a><span data-ttu-id="a8f47-2812">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2812">Description</span></span>

<span data-ttu-id="a8f47-2813">Bu hizmet, sağlanan g/ç sürücüsünü kullanarak dosya erişimi için bir medya açar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2813">This service opens a media for file access using the supplied I/O driver.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-2814">*Bu hizmete sağlanan bellek, bir iç mantıksal kesim önbelleğinin uygulanması için kullanılır, bu nedenle, daha fazla fiziksel g/ç daha fazla bellek azaltılır. FileX, en az bir mantıksal kesim (medyanın kesim başına bayt) için bir önbellek gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-2814">*The memory supplied to this service is used to implement an internal logical sector cache, hence, the more memory supplied the more physical I/O is reduced. FileX requires a cache of at least one logical sector (bytes per sector of the media).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2815">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2815">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2816">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2816">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-2817">**media_name**: medya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2817">**media_name**: Pointer to media's name.</span></span>
- <span data-ttu-id="a8f47-2818">**media_driver**: Bu ortam için g/ç sürücüsü işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2818">**media_driver**: Pointer to I/O driver for this media.</span></span> <span data-ttu-id="a8f47-2819">G/ç sürücüsü, Bölüm 5 ' te tanımlanan FileX sürücü gereksinimleriyle uyumlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2819">The I/O driver must conform to FileX driver requirements defined in Chapter 5.</span></span>
- <span data-ttu-id="a8f47-2820">**driver_info_ptr**: sağlanan g/ç sürücüsünün yararlanabilecek isteğe bağlı bilgiler için işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2820">**driver_info_ptr**: Pointer to optional information that the supplied I/O driver may utilize.</span></span>
- <span data-ttu-id="a8f47-2821">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2821">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="a8f47-2822">**memory_size**: çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2822">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="a8f47-2823">Boyut, medyanın kesim boyutu (genellikle 512 bayt) kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2823">The size must be as large as the media's sector size (typically 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2824">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2824">Return Values</span></span>

- <span data-ttu-id="a8f47-2825">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2825">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="a8f47-2826">Medyanın önyükleme kesimini okurken hata **FX_BOOT_ERROR** (0x01).</span><span class="sxs-lookup"><span data-stu-id="a8f47-2826">**FX_BOOT_ERROR** (0x01) Error reading the media's boot sector.</span></span>
- <span data-ttu-id="a8f47-2827">**FX_MEDIA_INVALID** (0x02) belirtilen medyanın önyükleme kesimi bozuk veya geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2827">**FX_MEDIA_INVALID** (0x02) Specified media's boot sector is corrupt or invalid.</span></span> <span data-ttu-id="a8f47-2828">Ayrıca, bu dönüş kodu, mantıksal kesim önbelleğinin boyutunun veya FAT giriş boyutunun 2 ' nin üssü olduğunu göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2828">In addition, this return code is used to indicate that either the logical sector cache size or the FAT entry size is not a power of 2.</span></span>
- <span data-ttu-id="a8f47-2829">**FX_FAT_READ_ERROR** (0x03) FAT medyayı okunurken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2829">**FX_FAT_READ_ERROR** (0x03) Error reading the media FAT.</span></span>
- <span data-ttu-id="a8f47-2830">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2830">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2831">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2831">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="a8f47-2832">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2832">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2833">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2833">Allowed From</span></span>

<span data-ttu-id="a8f47-2834">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2834">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2835">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2835">Example</span></span>

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2836">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2836">See Also</span></span>

- <span data-ttu-id="a8f47-2837">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2837">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2838">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2838">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2839">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2839">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2840">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2840">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2841">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2841">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2842">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2842">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2843">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2843">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2844">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2844">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2845">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2845">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2846">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2846">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2847">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2847">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2848">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2848">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2849">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2849">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2850">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2850">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2851">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2851">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2852">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2852">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2853">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2853">fx_system_initialize</span></span>

## <a name="fx_media_open_notify_set"></a><span data-ttu-id="a8f47-2854">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2854">fx_media_open_notify_set</span></span>

<span data-ttu-id="a8f47-2855">Medya açma bildirim işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-2855">Sets the media open notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2856">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2856">Prototype</span></span>

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a><span data-ttu-id="a8f47-2857">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2857">Description</span></span>

<span data-ttu-id="a8f47-2858">Bu hizmet, bir medya başarıyla açıldıktan sonra çağrılacak bir bildirim geri arama işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2858">This service sets a notify callback function which will be invoked after a media is successfully opened.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2859">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2859">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2860">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2860">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-2861">**media_open_notify**: medya açmak için geri arama bildirme işlevini açın.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2861">**media_open_notify**: Media open notify callback function to be installed.</span></span> <span data-ttu-id="a8f47-2862">Geri çağırma işlevi olarak NULL geçirme, medya açma geri aramasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2862">Passing NULL as the callback function disables the media open callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2863">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2863">Return Values</span></span>


- <span data-ttu-id="a8f47-2864">**FX_SUCCESS** (0x00) geri çağırma işlevini başarıyla yükledi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2864">**FX_SUCCESS** (0x00) Successfuly installed the callback function.</span></span>
- <span data-ttu-id="a8f47-2865">**FX_PTR_ERROR** (0x18) media_ptr null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2865">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="a8f47-2866">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2866">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2867">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2867">Allowed From</span></span>

<span data-ttu-id="a8f47-2868">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2868">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2869">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2869">Example</span></span>

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2870">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2870">See Also</span></span>

- <span data-ttu-id="a8f47-2871">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2871">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2872">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2872">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2873">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2873">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2874">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2874">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2875">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2875">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2876">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2876">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2877">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2877">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2878">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2878">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2879">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2879">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2880">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2880">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2881">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2881">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2882">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2882">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2883">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2883">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2884">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2884">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2885">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2885">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2886">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2886">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2887">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2887">fx_system_initialize</span></span>

## <a name="fx_media_read"></a><span data-ttu-id="a8f47-2888">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2888">fx_media_read</span></span>

<span data-ttu-id="a8f47-2889">Medyadan mantıksal kesim okur</span><span class="sxs-lookup"><span data-stu-id="a8f47-2889">Reads logical sector from media</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2890">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2890">Prototype</span></span>

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-2891">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2891">Description</span></span>

<span data-ttu-id="a8f47-2892">Bu hizmet, medyadan bir mantıksal kesim okur ve sağlanan arabelleğe koyar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2892">This service reads a logical sector from the media and places it into the supplied buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2893">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2893">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2894">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2894">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="a8f47-2895">**logical_sector**: okunacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2895">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="a8f47-2896">**buffer_ptr**: mantıksal kesime okunan hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2896">**buffer_ptr**: Pointer to the destination for the logical sector read.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2897">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2897">Return Values</span></span>

- <span data-ttu-id="a8f47-2898">**FX_SUCCESS** (0x00) başarılı medya okuma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2898">**FX_SUCCESS** (0x00) Successful media read.</span></span>
- <span data-ttu-id="a8f47-2899">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2899">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2900">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2900">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2901">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2901">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-2902">**FX_PTR_ERROR** (0x18) geçersiz medya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2902">**FX_PTR_ERROR** (0x18) Invalid media or buffer pointer.</span></span>
- <span data-ttu-id="a8f47-2903">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2903">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2904">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2904">Allowed From</span></span>

<span data-ttu-id="a8f47-2905">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2905">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2906">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2906">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-2907">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2907">See Also</span></span>

- <span data-ttu-id="a8f47-2908">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2908">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2909">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2909">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2910">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2910">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2911">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2911">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2912">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2912">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2913">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2913">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2914">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2914">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2915">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2915">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2916">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2916">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2917">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2917">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2918">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2918">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2919">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2919">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2920">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2920">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2921">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2921">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2922">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2922">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2923">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2923">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2924">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2924">fx_system_initialize</span></span>

## <a name="fx_media_space_available"></a><span data-ttu-id="a8f47-2925">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2925">fx_media_space_available</span></span>

<span data-ttu-id="a8f47-2926">Kullanılabilir medya alanını döndürür</span><span class="sxs-lookup"><span data-stu-id="a8f47-2926">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2927">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2927">Prototype</span></span>

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a><span data-ttu-id="a8f47-2928">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2928">Description</span></span>

<span data-ttu-id="a8f47-2929">Bu hizmet, medyada kullanılabilir olan bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2929">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="a8f47-2930">4 GB 'den büyük medyayla çalışmak için, uygulama Service *fx_media_extended_space_available* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2930">To work with the media larger than 4GB, application shall use the service *fx_media_extended_space_available*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2931">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2931">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2932">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2932">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="a8f47-2933">**available_bytes_ptr**: medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2933">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2934">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2934">Return Values</span></span>

- <span data-ttu-id="a8f47-2935">**FX_SUCCESS** (0x00) medyada kullanılabilir alanı başarıyla döndürdü.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2935">**FX_SUCCESS** (0x00) Successfully returned available space on media.</span></span>
- <span data-ttu-id="a8f47-2936">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2936">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2937">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2937">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="a8f47-2938">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2938">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2939">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2939">Allowed From</span></span>

<span data-ttu-id="a8f47-2940">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2940">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2941">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2941">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2942">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2942">See Also</span></span>

- <span data-ttu-id="a8f47-2943">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2943">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2944">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2944">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2945">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2945">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2946">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2946">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2947">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2947">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2948">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2948">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2949">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2949">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2950">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2950">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2951">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2951">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2952">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2952">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2953">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2953">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2954">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2954">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2955">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2955">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2956">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2956">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-2957">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2957">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2958">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2958">fx_media_write</span></span>
- <span data-ttu-id="a8f47-2959">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-2959">fx_system_initialize</span></span>

## <a name="fx_media_volume_get"></a><span data-ttu-id="a8f47-2960">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-2960">fx_media_volume_get</span></span>

<span data-ttu-id="a8f47-2961">Medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-2961">Gets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-2962">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-2962">Prototype</span></span>

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="a8f47-2963">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-2963">Description</span></span>

<span data-ttu-id="a8f47-2964">Bu hizmet, daha önce açılmış medyanın birim adını alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2964">This service retrieves the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-2965">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2965">Input Parameters</span></span>

- <span data-ttu-id="a8f47-2966">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2966">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-2967">**Volume_Name**: birim adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2967">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="a8f47-2968">Hedefin en az 12 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2968">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="a8f47-2969">**volume_source**: önyükleme kesiminden veya kök dizinden adın nereden alındığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2969">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="a8f47-2970">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-2970">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="a8f47-2971">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="a8f47-2971">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="a8f47-2972">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="a8f47-2972">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-2973">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-2973">Return Values</span></span>

- <span data-ttu-id="a8f47-2974">**FX_SUCCESS** (0x00) başarılı medya birimi al.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2974">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="a8f47-2975">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2975">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-2976">**FX_NOT_FOUND** (0x04) birim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2976">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="a8f47-2977">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2977">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-2978">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2978">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="a8f47-2979">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2979">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-2980">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-2980">Allowed From</span></span>

<span data-ttu-id="a8f47-2981">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-2981">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-2982">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-2982">Example</span></span>

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a><span data-ttu-id="a8f47-2983">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-2983">See Also</span></span>

- <span data-ttu-id="a8f47-2984">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-2984">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-2985">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-2985">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-2986">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-2986">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-2987">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-2987">fx_media_check</span></span>
- <span data-ttu-id="a8f47-2988">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-2988">fx_media_close</span></span>
- <span data-ttu-id="a8f47-2989">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2989">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-2990">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2990">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-2991">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2991">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-2992">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-2992">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-2993">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-2993">fx_media_format</span></span>
- <span data-ttu-id="a8f47-2994">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-2994">fx_media_open</span></span>
- <span data-ttu-id="a8f47-2995">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2995">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-2996">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-2996">fx_media_read</span></span>
- <span data-ttu-id="a8f47-2997">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-2997">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-2998">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-2998">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-2999">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-2999">fx_media_write</span></span>
- <span data-ttu-id="a8f47-3000">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3000">fx_system_initialize</span></span>

## <a name="fx_media_volume_get_extended"></a><span data-ttu-id="a8f47-3001">fx_media_volume_get_extended</span><span class="sxs-lookup"><span data-stu-id="a8f47-3001">fx_media_volume_get_extended</span></span>

<span data-ttu-id="a8f47-3002">Daha önce açılmış medyanın medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3002">Gets media volume name of previously opened media</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3003">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3003">Prototype</span></span>

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="a8f47-3004">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3004">Description</span></span>

<span data-ttu-id="a8f47-3005">Bu hizmet, daha önce açılmış medyanın birim adını alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3005">This service retrieves the volume name of the previously opened media.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3006">Bu hizmet, çağıran _ *Volume_Name*\* arabelleğinin boyutunda geçtiği sürece \***fx_media_volume_get ()** _ ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3006">This service is identical to ***fx_media_volume_get()** _ except the caller passes in the size of the _ *volume_name** buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3007">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3007">Input Parameters</span></span>


- <span data-ttu-id="a8f47-3008">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3008">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3009">**Volume_Name**: birim adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3009">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="a8f47-3010">Hedefin en az 12 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3010">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="a8f47-3011">**volume_name_buffer_length**: Volume_Name arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3011">**volume_name_buffer_length**: Size of volume_name buffer.</span></span>
- <span data-ttu-id="a8f47-3012">**volume_source**: önyükleme kesiminden veya kök dizinden adın nereden alındığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3012">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="a8f47-3013">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a8f47-3013">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="a8f47-3014">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="a8f47-3014">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="a8f47-3015">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="a8f47-3015">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3016">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3016">Return Values</span></span>

- <span data-ttu-id="a8f47-3017">**FX_SUCCESS** (0x00) başarılı medya birimi al.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3017">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="a8f47-3018">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3018">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3019">**FX_NOT_FOUND** (0x04) birim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3019">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="a8f47-3020">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3020">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3021">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3021">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="a8f47-3022">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3022">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3023">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3023">Allowed From</span></span>

<span data-ttu-id="a8f47-3024">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3024">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3025">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3025">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-3026">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3026">See Also</span></span>

- <span data-ttu-id="a8f47-3027">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-3027">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-3028">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-3028">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-3029">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3029">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-3030">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-3030">fx_media_check</span></span>
- <span data-ttu-id="a8f47-3031">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3031">fx_media_close</span></span>
- <span data-ttu-id="a8f47-3032">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3032">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-3033">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-3033">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-3034">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-3034">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-3035">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-3035">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-3036">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-3036">fx_media_format</span></span>
- <span data-ttu-id="a8f47-3037">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3037">fx_media_open</span></span>
- <span data-ttu-id="a8f47-3038">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3038">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-3039">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3039">fx_media_read</span></span>
- <span data-ttu-id="a8f47-3040">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-3040">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-3041">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3041">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-3042">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3042">fx_media_write</span></span>
- <span data-ttu-id="a8f47-3043">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3043">fx_system_initialize</span></span>

## <a name="fx_media_volume_set"></a><span data-ttu-id="a8f47-3044">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3044">fx_media_volume_set</span></span>

<span data-ttu-id="a8f47-3045">Medya birimi adını ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-3045">Sets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3046">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3046">Prototype</span></span>

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-3047">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3047">Description</span></span>

<span data-ttu-id="a8f47-3048">Bu hizmet, daha önce açılmış medyanın birim adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3048">This service sets the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3049">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3049">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3050">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3050">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3051">**Volume_Name**: birim adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3051">**volume_name**: Pointer to the volume name.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3052">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3052">Return Values</span></span>

- <span data-ttu-id="a8f47-3053">**FX_SUCCESS** (0x00) başarılı medya birimi kümesi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3053">**FX_SUCCESS** (0x00) Successful media volume set.</span></span>
- <span data-ttu-id="a8f47-3054">**FX_INVALID_NAME** (0x0C) Volume_name geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3054">**FX_INVALID_NAME** (0x0C) Volume_name is invalid.</span></span>
- <span data-ttu-id="a8f47-3055">**FX_MEDIA_INVALID** (0x02) birim adı ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3055">**FX_MEDIA_INVALID** (0x02) Unable to set volume name.</span></span>
- <span data-ttu-id="a8f47-3056">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3056">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3057">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3057">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3058">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3058">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-3059">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3059">**FX_PTR_ERROR** (0x18) Invalid media or volume name pointer.</span></span>
- <span data-ttu-id="a8f47-3060">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3060">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3061">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3061">Allowed From</span></span>

<span data-ttu-id="a8f47-3062">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3062">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3063">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3063">Example</span></span>

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-3064">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3064">See Also</span></span>

- <span data-ttu-id="a8f47-3065">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-3065">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-3066">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-3066">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-3067">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3067">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-3068">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-3068">fx_media_check</span></span>
- <span data-ttu-id="a8f47-3069">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3069">fx_media_close</span></span>
- <span data-ttu-id="a8f47-3070">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3070">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-3071">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-3071">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-3072">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-3072">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-3073">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-3073">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-3074">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-3074">fx_media_format</span></span>
- <span data-ttu-id="a8f47-3075">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3075">fx_media_open</span></span>
- <span data-ttu-id="a8f47-3076">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3076">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-3077">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3077">fx_media_read</span></span>
- <span data-ttu-id="a8f47-3078">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-3078">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-3079">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3079">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-3080">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3080">fx_media_write</span></span>
- <span data-ttu-id="a8f47-3081">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3081">fx_system_initialize</span></span>

## <a name="fx_media_write"></a><span data-ttu-id="a8f47-3082">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3082">fx_media_write</span></span>

<span data-ttu-id="a8f47-3083">Mantıksal kesimi yazar</span><span class="sxs-lookup"><span data-stu-id="a8f47-3083">Writes logical sector</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3084">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3084">Prototype</span></span>

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="a8f47-3085">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3085">Description</span></span>

<span data-ttu-id="a8f47-3086">Bu hizmet verilen arabelleği belirtilen mantıksal kesime yazar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3086">This service writes the supplied buffer to the specified logical sector.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3087">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3087">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3088">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3088">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="a8f47-3089">**logical_sector**: yazılacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3089">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="a8f47-3090">**buffer_ptr**: mantıksal kesim yazma için kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3090">**buffer_ptr**: Pointer to the source for the logical sector write.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3091">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3091">Return Values</span></span>

- <span data-ttu-id="a8f47-3092">**FX_SUCCESS** (0x00) başarılı medya yazma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3092">**FX_SUCCESS** (0x00) Successful media write.</span></span>
- <span data-ttu-id="a8f47-3093">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3093">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3094">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3094">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-3095">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3095">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3096">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3096">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-3097">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3097">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="a8f47-3098">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3098">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3099">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3099">Allowed From</span></span>

<span data-ttu-id="a8f47-3100">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3100">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3101">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3101">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3102">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3102">See Also</span></span>

- <span data-ttu-id="a8f47-3103">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="a8f47-3103">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="a8f47-3104">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="a8f47-3104">fx_media_abort</span></span>
- <span data-ttu-id="a8f47-3105">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3105">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="a8f47-3106">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="a8f47-3106">fx_media_check</span></span>
- <span data-ttu-id="a8f47-3107">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3107">fx_media_close</span></span>
- <span data-ttu-id="a8f47-3108">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3108">fx_media_close_notify_set</span></span>
- <span data-ttu-id="a8f47-3109">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-3109">fx_media_exFAT_format</span></span>
- <span data-ttu-id="a8f47-3110">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-3110">fx_media_extended_space_available</span></span>
- <span data-ttu-id="a8f47-3111">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="a8f47-3111">fx_media_flush</span></span>
- <span data-ttu-id="a8f47-3112">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="a8f47-3112">fx_media_format</span></span>
- <span data-ttu-id="a8f47-3113">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3113">fx_media_open</span></span>
- <span data-ttu-id="a8f47-3114">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3114">fx_media_open_notify_set</span></span>
- <span data-ttu-id="a8f47-3115">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3115">fx_media_read</span></span>
- <span data-ttu-id="a8f47-3116">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="a8f47-3116">fx_media_space_available</span></span>
- <span data-ttu-id="a8f47-3117">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3117">fx_media_volume_get</span></span>
- <span data-ttu-id="a8f47-3118">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3118">fx_media_volume_set</span></span>
- <span data-ttu-id="a8f47-3119">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3119">fx_system_initialize</span></span>

## <a name="fx_system_date_get"></a><span data-ttu-id="a8f47-3120">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3120">fx_system_date_get</span></span>

<span data-ttu-id="a8f47-3121">Dosya sistemi tarihini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3121">Gets file system date</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3122">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3122">Prototype</span></span>

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a><span data-ttu-id="a8f47-3123">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3123">Description</span></span>

<span data-ttu-id="a8f47-3124">Bu hizmet, geçerli sistem tarihini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3124">This service returns the current system date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3125">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3125">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3126">**yıl**: yıl için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3126">**year**: Pointer to destination for year.</span></span>
- <span data-ttu-id="a8f47-3127">**Month**: ay için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3127">**month**: Pointer to destination for month.</span></span>
- <span data-ttu-id="a8f47-3128">**gün**: günün hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3128">**day**: Pointer to destination for day.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3129">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3129">Return Values</span></span>

- <span data-ttu-id="a8f47-3130">**FX_SUCCESS** (0x00) başarılı Tarih alımı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3130">**FX_SUCCESS** (0x00) Successful date retrieval.</span></span>
- <span data-ttu-id="a8f47-3131">**FX_PTR_ERROR** (0x18) bir veya daha fazla GIRIŞ parametresi null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3131">**FX_PTR_ERROR** (0x18) One or more of the input parameters are NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3132">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3132">Allowed From</span></span>

<span data-ttu-id="a8f47-3133">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3133">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3134">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3134">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3135">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3135">See Also</span></span>

- <span data-ttu-id="a8f47-3136">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3136">fx_system_date_set</span></span>
- <span data-ttu-id="a8f47-3137">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3137">fx_system_initialize</span></span>
- <span data-ttu-id="a8f47-3138">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3138">fx_system_time_get</span></span>
- <span data-ttu-id="a8f47-3139">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3139">fx_system_time_set</span></span>

## <a name="fx_system_date_set"></a><span data-ttu-id="a8f47-3140">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3140">fx_system_date_set</span></span>

<span data-ttu-id="a8f47-3141">Sistem tarihini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-3141">Sets system date</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3142">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3142">Prototype</span></span>

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a><span data-ttu-id="a8f47-3143">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3143">Description</span></span>

<span data-ttu-id="a8f47-3144">Bu hizmet, sistem tarihini belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3144">This service sets the system date as specified.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-3145">*İlk sistem tarihini ayarlamak için bu hizmet **fx_system_initialize** kısa süre sonra çağrılmalıdır. Varsayılan olarak, sistem tarihi en son genel FileX sürümüdür.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3145">*This service should be called shortly after **fx_system_initialize** to set the initial system date. By default, the system date is that of the last generic FileX release.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3146">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3146">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3147">**yıl**: yeni yıl.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3147">**year**: New year.</span></span> <span data-ttu-id="a8f47-3148">Geçerli Aralık 1980 yılında 2107 ' dir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3148">The valid range is from 1980 through the year 2107.</span></span>
- <span data-ttu-id="a8f47-3149">**ay**: yeni ay.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3149">**month**: New month.</span></span> <span data-ttu-id="a8f47-3150">Geçerli Aralık 1 ile 12 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3150">The valid range is from 1 through 12.</span></span>
- <span data-ttu-id="a8f47-3151">**gün**: yeni gün.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3151">**day**: New day.</span></span> <span data-ttu-id="a8f47-3152">Geçerli Aralık, aya ve artık yıl koşullarına bağlı olarak 1 ila 31 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3152">The valid range is from 1 through 31, depending on month and leap year conditions.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3153">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3153">Return Values</span></span>

- <span data-ttu-id="a8f47-3154">**FX_SUCCESS** (0x00) başarılı tarih ayarı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3154">**FX_SUCCESS** (0x00) Successful date setting.</span></span>
- <span data-ttu-id="a8f47-3155">**FX_INVALID_YEAR** (0x12) geçersiz yıl belirtildi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3155">**FX_INVALID_YEAR** (0x12) Invalid year specified.</span></span>
- <span data-ttu-id="a8f47-3156">**FX_INVALID_MONTH** (0x13) geçersiz ay belirtildi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3156">**FX_INVALID_MONTH** (0x13) Invalid month specified.</span></span>
- <span data-ttu-id="a8f47-3157">**FX_INVALID_DAY** (0x14) geçersiz gün belirtildi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3157">**FX_INVALID_DAY** (0x14) Invalid day specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3158">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3158">Allowed From</span></span>

<span data-ttu-id="a8f47-3159">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3159">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3160">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3160">Example</span></span>

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-3161">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3161">See Also</span></span>

- <span data-ttu-id="a8f47-3162">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3162">fx_system_date_get</span></span>
- <span data-ttu-id="a8f47-3163">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3163">fx_system_initialize</span></span>
- <span data-ttu-id="a8f47-3164">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3164">fx_system_time_get</span></span>
- <span data-ttu-id="a8f47-3165">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3165">fx_system_time_set</span></span>

## <a name="fx_system_initialize"></a><span data-ttu-id="a8f47-3166">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3166">fx_system_initialize</span></span>

<span data-ttu-id="a8f47-3167">Tüm sistemi başlatır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3167">Initializes entire system</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3168">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3168">Prototype</span></span>

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a><span data-ttu-id="a8f47-3169">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3169">Description</span></span>

<span data-ttu-id="a8f47-3170">Bu hizmet, tüm önemli dosya x veri yapılarını başlatır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3170">This service initializes all the major FileX data structures.</span></span> <span data-ttu-id="a8f47-3171">***Tx_application_define*** veya belki de bir başlatma iş parçacığından çağrılmalıdır ve başka bir FileX hizmeti kullanılmadan önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3171">It should be called either in ***tx_application_define*** or possibly from an initialization thread and must be called prior to using any other FileX service.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-3172">\* Bu çağrı tarafından başlatıldıktan sonra uygulama, *doğru bir sistem tarih ve saati ile başlamak için **fx_system_date_set** _ ve _ *fx_system_time_set** çağırmalıdır.\*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3172">*Once initialized by this call, the application should call ***fx_system_date_set** _ and _ *fx_system_time_set** to start with an accurate system date and time.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3173">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3173">Input Parameters</span></span>

<span data-ttu-id="a8f47-3174">Yok</span><span class="sxs-lookup"><span data-stu-id="a8f47-3174">None</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3175">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3175">Return Values</span></span>

<span data-ttu-id="a8f47-3176">Yok.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3176">None.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3177">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3177">Allowed From</span></span>

<span data-ttu-id="a8f47-3178">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3178">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3179">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3179">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3180">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3180">See Also</span></span>

- <span data-ttu-id="a8f47-3181">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3181">fx_system_date_get</span></span>
- <span data-ttu-id="a8f47-3182">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3182">fx_system_date_set</span></span>
- <span data-ttu-id="a8f47-3183">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3183">fx_system_time_get</span></span>
- <span data-ttu-id="a8f47-3184">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3184">fx_system_time_set</span></span>

## <a name="fx_system_time_get"></a><span data-ttu-id="a8f47-3185">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3185">fx_system_time_get</span></span>

<span data-ttu-id="a8f47-3186">Geçerli sistem saatini alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3186">Gets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3187">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3187">Prototype</span></span>

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="a8f47-3188">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3188">Description</span></span>

<span data-ttu-id="a8f47-3189">Bu hizmet geçerli sistem saatini alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3189">This service retrieves the current system time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3190">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3190">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3191">**saat**: saat için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3191">**hour**: Pointer to destination for hour.</span></span>
- <span data-ttu-id="a8f47-3192">**Minute**: dakikalık hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3192">**minute**: Pointer to destination for minute.</span></span>
- <span data-ttu-id="a8f47-3193">**ikinci**: saniye için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3193">**second**: Pointer to destination for second.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3194">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3194">Return Values</span></span>

- <span data-ttu-id="a8f47-3195">**FX_SUCCESS** (0x00) sistem saati alımı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3195">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="a8f47-3196">**FX_PTR_ERROR** (0x18) bir veya daha fazla giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="a8f47-3196">**FX_PTR_ERROR** (0x18) One or more of the input parameters</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3197">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3197">Allowed From</span></span>

<span data-ttu-id="a8f47-3198">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3198">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3199">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3199">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3200">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3200">See Also</span></span>

- <span data-ttu-id="a8f47-3201">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3201">fx_system_date_get</span></span>
- <span data-ttu-id="a8f47-3202">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3202">fx_system_date_set</span></span>
- <span data-ttu-id="a8f47-3203">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3203">fx_system_initialize</span></span>
- <span data-ttu-id="a8f47-3204">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3204">fx_system_time_set</span></span>

## <a name="fx_system_time_set"></a><span data-ttu-id="a8f47-3205">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3205">fx_system_time_set</span></span>

<span data-ttu-id="a8f47-3206">Geçerli sistem saatini ayarlar</span><span class="sxs-lookup"><span data-stu-id="a8f47-3206">Sets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3207">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3207">Prototype</span></span>

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a><span data-ttu-id="a8f47-3208">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3208">Description</span></span>

<span data-ttu-id="a8f47-3209">Bu hizmet, geçerli sistem saatini giriş parametreleri tarafından belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3209">This service sets the current system time to that specified by the input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-3210">*Bu hizmet, ilk sistem saatini ayarlamak için **fx_system_initialize** kısa süre sonra çağrılmalıdır. Varsayılan olarak, sistem saati 0:0:0 ' dir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3210">*This service should be called shortly after **fx_system_initialize** to set the initial system time. By default, the system time is 0:0:0.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3211">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3211">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3212">**saat**: yeni saat (0-23).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3212">**hour**: New hour (0-23).</span></span>
- <span data-ttu-id="a8f47-3213">**dakika**: yeni dakika (0-59).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3213">**minute**: New minute (0-59).</span></span>
- <span data-ttu-id="a8f47-3214">**ikinci**: Yeni saniye (0-59).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3214">**second**: New second (0-59).</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3215">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3215">Return Values</span></span>

- <span data-ttu-id="a8f47-3216">**FX_SUCCESS** (0x00) sistem saati alımı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3216">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="a8f47-3217">**FX_INVALID_HOUR**    (0x15) yeni saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3217">**FX_INVALID_HOUR**    (0x15) New hour is invalid.</span></span>
- <span data-ttu-id="a8f47-3218">**FX_INVALID_MINUTE** (0x16) yeni dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3218">**FX_INVALID_MINUTE** (0x16) New minute is invalid.</span></span>
- <span data-ttu-id="a8f47-3219">**FX_INVALID_SECOND** (0x17) yeni ikinci değer geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3219">**FX_INVALID_SECOND** (0x17) New second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3220">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3220">Allowed From</span></span>

<span data-ttu-id="a8f47-3221">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3221">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3222">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3222">Example</span></span>

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a><span data-ttu-id="a8f47-3223">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3223">See Also</span></span>

- <span data-ttu-id="a8f47-3224">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3224">fx_system_date_get</span></span>
- <span data-ttu-id="a8f47-3225">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3225">fx_system_date_set</span></span>
- <span data-ttu-id="a8f47-3226">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="a8f47-3226">fx_system_initialize</span></span>
- <span data-ttu-id="a8f47-3227">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3227">fx_system_time_get</span></span>

## <a name="fx_unicode_directory_create"></a><span data-ttu-id="a8f47-3228">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3228">fx_unicode_directory_create</span></span>

<span data-ttu-id="a8f47-3229">Unicode dizin oluşturur</span><span class="sxs-lookup"><span data-stu-id="a8f47-3229">Creates a Unicode directory</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3230">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3230">Prototype</span></span>

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-3231">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3231">Description</span></span>

<span data-ttu-id="a8f47-3232">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir alt dizin oluşturur; Unicode kaynak adı parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3232">This service creates a Unicode-named subdirectory in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="a8f47-3233">Başarılı olursa, yeni oluşturulan Unicode alt dizininin kısa adı (8,3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3233">If successful, the short name (8.3 format) of the newly created Unicode subdirectory is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-3234">*Unicode alt dizinindeki tüm işlemler (varsayılan yol, silme, vb.), standart FileX dizin hizmetlerine döndürülen kısa ad (8,3 biçimi) sağlanarak yapılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3234">*All operations on the Unicode subdirectory (making it the default path, deleting, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX directory services.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3235">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3235">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3236">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3236">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3237">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3237">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3238">**source_unicode_name**: yeni alt dizin için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3238">**source_unicode_name**: Pointer to the Unicode name for the new subdirectory.</span></span>
- <span data-ttu-id="a8f47-3239">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3239">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="a8f47-3240">**short_name**: yeni Unicode alt dizini için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3240">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode subdirectory.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3241">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3241">Return Values</span></span>

- <span data-ttu-id="a8f47-3242">**FX_SUCCESS** (0x00) başarılı Unicode dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3242">**FX_SUCCESS** (0x00) Successful Unicode directory create.</span></span>
- <span data-ttu-id="a8f47-3243">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3243">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3244">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin zaten var.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3244">**FX_ALREADY_CREATED** (0x0B) Specified directory already exists.</span></span>
- <span data-ttu-id="a8f47-3245">Yeni Dizin girişi için medyada daha fazla küme yok **FX_NO_MORE_SPACE** (0x0A).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3245">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new directory entry.</span></span>
- <span data-ttu-id="a8f47-3246">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3246">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="a8f47-3247">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3247">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-3248">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3248">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="a8f47-3249">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3249">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="a8f47-3250">**FX_IO_ERROR (0x90)** Sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3250">**FX_IO_ERROR    (0x90)** Driver I/O error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3251">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3251">Allowed From</span></span>

<span data-ttu-id="a8f47-3252">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3252">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3253">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3253">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3254">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3254">See Also</span></span>

- <span data-ttu-id="a8f47-3255">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3255">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-3256">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3256">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-3257">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3257">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-3258">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3258">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-3259">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3259">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-3260">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3260">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-3261">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3261">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-3262">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3262">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-3263">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3263">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-3264">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-3264">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-3265">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3265">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-3266">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-3266">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-3267">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3267">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-3268">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3268">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-3269">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-3269">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-3270">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3270">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-3271">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3271">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-3272">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3272">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-3273">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3273">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-3274">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3274">fx_unicode_directory_rename</span></span>

## <a name="fx_unicode_directory_rename"></a><span data-ttu-id="a8f47-3275">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3275">fx_unicode_directory_rename</span></span>

<span data-ttu-id="a8f47-3276">Unicode dizesini kullanarak dizini yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3276">Renames directory using Unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3277">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3277">Prototype</span></span>

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-3278">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3278">Description</span></span>

<span data-ttu-id="a8f47-3279">Bu hizmet, Unicode adlı bir alt dizini geçerli çalışma dizininde belirtilen yeni Unicode adına değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3279">This service changes a Unicode-named subdirectory to specified new Unicode name in current working directory.</span></span> <span data-ttu-id="a8f47-3280">Unicode ad parametreleri yol bilgilerine sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3280">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3281">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3281">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3282">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3282">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3283">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3283">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3284">**old_unicode_name**: geçerli dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3284">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="a8f47-3285">**old_unicode_name_length**: geçerli Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3285">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="a8f47-3286">**new_unicode_name**: yeni Unicode dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3286">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="a8f47-3287">**old_unicode_name_length**: yeni Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3287">**old_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="a8f47-3288">**new_short_name**: yeniden adlandırılan Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3288">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span> <span data-ttu-id="a8f47-3289">Dizini Unicode ile yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="a8f47-3289">Rename Directory with Unicode</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3290">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3290">Return Values</span></span>

- <span data-ttu-id="a8f47-3291">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3291">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="a8f47-3292">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3292">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3293">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3293">**FX_ALREADY_CREATED** (0x0B) Specified directory name already exists.</span></span>
- <span data-ttu-id="a8f47-3294">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3294">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3295">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3295">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="a8f47-3296">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3296">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="a8f47-3297">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3297">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3298">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3298">Allowed From</span></span>

<span data-ttu-id="a8f47-3299">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3299">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3300">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3300">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3301">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3301">See Also</span></span>

- <span data-ttu-id="a8f47-3302">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3302">fx_directory_attributes_read</span></span>
- <span data-ttu-id="a8f47-3303">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3303">fx_directory_attributes_set</span></span>
- <span data-ttu-id="a8f47-3304">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3304">fx_directory_create</span></span>
- <span data-ttu-id="a8f47-3305">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3305">fx_directory_default_get</span></span>
- <span data-ttu-id="a8f47-3306">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3306">fx_directory_default_set</span></span>
- <span data-ttu-id="a8f47-3307">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3307">fx_directory_delete</span></span>
- <span data-ttu-id="a8f47-3308">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3308">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="a8f47-3309">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3309">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="a8f47-3310">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3310">fx_directory_information_get</span></span>
- <span data-ttu-id="a8f47-3311">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="a8f47-3311">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="a8f47-3312">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3312">fx_directory_local_path_get</span></span>
- <span data-ttu-id="a8f47-3313">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="a8f47-3313">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="a8f47-3314">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3314">fx_directory_local_path_set</span></span>
- <span data-ttu-id="a8f47-3315">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3315">fx_directory_long_name_get</span></span>
- <span data-ttu-id="a8f47-3316">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="a8f47-3316">fx_directory_name_test</span></span>
- <span data-ttu-id="a8f47-3317">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3317">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="a8f47-3318">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="a8f47-3318">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="a8f47-3319">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3319">fx_directory_rename</span></span>
- <span data-ttu-id="a8f47-3320">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3320">fx_directory_short_name_get</span></span>
- <span data-ttu-id="a8f47-3321">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3321">fx_unicode_directory_create</span></span>

## <a name="fx_unicode_file_create"></a><span data-ttu-id="a8f47-3322">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3322">fx_unicode_file_create</span></span>

<span data-ttu-id="a8f47-3323">Unicode dosyası oluşturur</span><span class="sxs-lookup"><span data-stu-id="a8f47-3323">Creates a Unicode file</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3324">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3324">Prototype</span></span>

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-3325">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3325">Description</span></span>

<span data-ttu-id="a8f47-3326">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya oluşturur; Unicode kaynak adı parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3326">This service creates a Unicode-named file in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="a8f47-3327">Başarılı olursa, yeni oluşturulan Unicode dosyanın kısa adı (8,3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3327">If successful, the short name (8.3 format) of the newly created Unicode file is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="a8f47-3328">*Unicode dosyasındaki (açma, yazma, okuma, kapatma, vb.) tüm işlemler, standart FileX dosya hizmetlerine döndürülen kısa ad (8,3 biçimi) sağlanarak yapılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3328">*All operations on the Unicode file (opening, writing, reading, closing, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX file services.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3329">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3329">Input Parameters</span></span>


- <span data-ttu-id="a8f47-3330">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3330">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3331">**source_unicode_name**: yeni dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3331">**source_unicode_name**: Pointer to the Unicode name for the new file.</span></span>
- <span data-ttu-id="a8f47-3332">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3332">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="a8f47-3333">**short_name**: yeni Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3333">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3334">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3334">Return Values</span></span>

- <span data-ttu-id="a8f47-3335">**FX_SUCCESS** (0x00) başarılı dosya oluştur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3335">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="a8f47-3336">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3336">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3337">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya zaten var.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3337">**FX_ALREADY_CREATED** (0x0B) Specified file already exists.</span></span>
- <span data-ttu-id="a8f47-3338">Yeni dosya girişi için medyada daha fazla küme yok **FX_NO_MORE_SPACE** (0x0A).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3338">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new file entry.</span></span>
- <span data-ttu-id="a8f47-3339">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3339">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="a8f47-3340">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3340">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3341">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3341">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="a8f47-3342">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3342">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="a8f47-3343">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3343">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3344">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3344">Allowed From</span></span>

<span data-ttu-id="a8f47-3345">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3345">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3346">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3346">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3347">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3347">See Also</span></span>

- <span data-ttu-id="a8f47-3348">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3348">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3349">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3349">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3350">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3350">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3351">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3351">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3352">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3353">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3354">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3355">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3359">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3362">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3363">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3364">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3365">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3366">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3367">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3368">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3369">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3371">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3371">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-3372">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3372">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-3373">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3373">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_file_rename"></a><span data-ttu-id="a8f47-3374">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3374">fx_unicode_file_rename</span></span>

<span data-ttu-id="a8f47-3375">Unicode dizesini kullanarak bir dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3375">Renames a file using unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3376">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3376">Prototype</span></span>

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a><span data-ttu-id="a8f47-3377">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3377">Description</span></span>

<span data-ttu-id="a8f47-3378">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya adını belirtilen yeni Unicode adı olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3378">This service changes a Unicode-named file name to specified new Unicode name in current default directory.</span></span> <span data-ttu-id="a8f47-3379">Unicode ad parametreleri yol bilgilerine sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3379">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3380">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3380">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3381">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3381">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3382">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3382">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3383">**old_unicode_name**: geçerli dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3383">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="a8f47-3384">**old_unicode_name_length**: geçerli Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3384">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="a8f47-3385">**new_unicode_name**: yeni Unicode dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3385">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="a8f47-3386">**new_unicode_name_length**: yeni Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3386">**new_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="a8f47-3387">**new_short_name**: yeniden adlandırılan Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3387">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3388">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3388">Return Values</span></span>


- <span data-ttu-id="a8f47-3389">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3389">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="a8f47-3390">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3390">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3391">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3391">**FX_ALREADY_CREATED** (0x0B) Specified file name already exists.</span></span>
- <span data-ttu-id="a8f47-3392">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3392">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3393">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3393">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="a8f47-3394">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3394">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="a8f47-3395">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3395">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3396">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3396">Allowed From</span></span>

<span data-ttu-id="a8f47-3397">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3398">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3398">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3399">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3399">See Also</span></span>

- <span data-ttu-id="a8f47-3400">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3400">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3401">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3401">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3402">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3402">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3403">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3403">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3404">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3404">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3405">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3405">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3406">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3406">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3407">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3407">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3408">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3408">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3409">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3409">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3410">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3410">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3411">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3411">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3412">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3412">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3413">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3413">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3414">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3414">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3415">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3415">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3416">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3416">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3417">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3417">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3418">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3418">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3419">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3419">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3420">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3420">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3421">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3421">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3422">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3422">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3423">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3423">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-3424">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3424">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-3425">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3425">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get"></a><span data-ttu-id="a8f47-3426">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3426">fx_unicode_length_get</span></span>

<span data-ttu-id="a8f47-3427">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3427">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3428">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3428">Prototype</span></span>

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a><span data-ttu-id="a8f47-3429">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3429">Description</span></span>

<span data-ttu-id="a8f47-3430">Bu hizmet, sağlanan Unicode adının uzunluğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3430">This service determines the length of the supplied Unicode name.</span></span> <span data-ttu-id="a8f47-3431">Unicode bir karakter iki bayt ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3431">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="a8f47-3432">Unicode adı, iki baytlık bir Unicode karakter olan ve iki boş bayt (0 değeri 0 değeri) tarafından sonlandırılan bir serisidir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3432">A Unicode name is a series of two byte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3433">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3433">Input Parameters</span></span>

<span data-ttu-id="a8f47-3434">**unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3434">**unicode_name**: Pointer to Unicode name.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3435">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3435">Return Values</span></span>

<span data-ttu-id="a8f47-3436">**uzunluk**: Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3436">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3437">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3437">Allowed From</span></span>

<span data-ttu-id="a8f47-3438">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3438">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3439">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3439">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3440">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3440">See Also</span></span>

- <span data-ttu-id="a8f47-3441">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3441">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3442">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3442">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3443">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3443">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3444">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3444">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3445">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3445">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3446">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3446">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3447">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3447">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3448">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3448">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3449">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3449">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3450">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3450">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3451">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3451">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3452">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3452">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3453">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3453">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3454">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3454">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3455">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3455">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3456">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3456">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3457">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3457">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3458">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3458">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3459">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3459">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3460">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3460">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3461">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3461">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3462">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3462">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3463">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3463">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3464">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3464">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-3465">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3465">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-3466">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3466">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-3467">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3467">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get_extended"></a><span data-ttu-id="a8f47-3468">fx_unicode_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="a8f47-3468">fx_unicode_length_get_extended</span></span>

<span data-ttu-id="a8f47-3469">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3469">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3470">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3470">Prototype</span></span>

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a><span data-ttu-id="a8f47-3471">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3471">Description</span></span>

<span data-ttu-id="a8f47-3472">Bu hizmet, sağlanan Unicode adının uzunluğunu alır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3472">This service gets the length of the supplied Unicode name.</span></span> <span data-ttu-id="a8f47-3473">Unicode bir karakter iki bayt ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3473">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="a8f47-3474">Unicode adı, iki boş bayt (iki bayt 0 değeri) tarafından sonlandırılan bir dizi TWA Unicode karakter dizisidir.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3474">A Unicode name is a series of twobyte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3475">*Bu hizmet, iki NULL karakter de dahil olmak üzere, çağıran **unicode_name** arabelleğinin boyutuna geçtiğinde, **fx_unicode_length_get ()** ile aynıdır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3475">*This service is identical to **fx_unicode_length_get()** except the caller passes in the size of the **unicode_name** buffer, including the two NULL characters.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3476">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3476">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3477">**unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3477">**unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="a8f47-3478">**BUFFER_LENGTH**: Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3478">**buffer_length**: Size of Unicode name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3479">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3479">Return Values</span></span>

<span data-ttu-id="a8f47-3480">**uzunluk**: Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3480">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3481">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3481">Allowed From</span></span>

<span data-ttu-id="a8f47-3482">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3482">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3483">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3483">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3484">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3484">See Also</span></span>

- <span data-ttu-id="a8f47-3485">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3485">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3486">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3486">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3487">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3487">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3488">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3488">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3489">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3489">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3490">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3490">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3491">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3491">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3492">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3492">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3493">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3493">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3494">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3494">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3495">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3495">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3496">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3496">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3497">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3497">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3498">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3498">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3499">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3499">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3500">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3500">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3501">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3501">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3502">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3502">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3503">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3503">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3504">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3504">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3505">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3505">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3506">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3506">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3507">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3507">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3508">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3508">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-3509">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3509">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-3510">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3510">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-3511">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3511">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get"></a><span data-ttu-id="a8f47-3512">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3512">fx_unicode_name_get</span></span>

<span data-ttu-id="a8f47-3513">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3513">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3514">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3514">Prototype</span></span>

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a><span data-ttu-id="a8f47-3515">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3515">Description</span></span>

<span data-ttu-id="a8f47-3516">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3516">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="a8f47-3517">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3517">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3518">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3518">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3519">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3519">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3520">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3520">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3521">**short_name** Kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3521">**short_name** Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="a8f47-3522">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3522">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="a8f47-3523">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3523">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3524">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3524">Return Values</span></span>

- <span data-ttu-id="a8f47-3525">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3525">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="a8f47-3526">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3526">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="a8f47-3527">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-3527">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-3528">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3528">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3529">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3529">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3530">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3530">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="a8f47-3531">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3531">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-3532">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3532">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="a8f47-3533">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3534">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3534">Allowed From</span></span>

<span data-ttu-id="a8f47-3535">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3536">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3536">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3537">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3537">See Also</span></span>

- <span data-ttu-id="a8f47-3538">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3538">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3539">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3539">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3540">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3540">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3541">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3541">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3542">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3542">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3543">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3543">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3544">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3544">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3545">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3545">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3546">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3546">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3547">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3547">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3548">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3548">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3549">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3549">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3550">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3550">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3551">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3551">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3552">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3552">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3553">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3553">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3554">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3554">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3555">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3555">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3556">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3556">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3557">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3557">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3558">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3558">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3559">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3559">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3560">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3560">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3561">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3561">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-3562">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3562">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-3563">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3563">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get_extended"></a><span data-ttu-id="a8f47-3564">fx_unicode_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="a8f47-3564">fx_unicode_name_get_extended</span></span>

<span data-ttu-id="a8f47-3565">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3565">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3566">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3566">Prototype</span></span>

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a><span data-ttu-id="a8f47-3567">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3567">Description</span></span>

<span data-ttu-id="a8f47-3568">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3568">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="a8f47-3569">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3569">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3570">\* Bu hizmet,_çağıran, hedef Unicode arabelleğinin bir giriş bağımsız değişkeni olarak boyutunu sağladığı sürece \* fx_unicode_name_get aynıdır. Bu, hizmetin hedef Unicode arabelleğinin üzerine yazmayacağı garantisi sağlamasına izin verir_</span><span class="sxs-lookup"><span data-stu-id="a8f47-3570">\*This service is identical to \***fx_unicode_name_get**_, except the caller supplies the size of the destination Unicode buffer as an input argument. This allows the service to guarantee that it will not overwrite the destination Unicode buffer_</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3571">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3571">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3572">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3572">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3573">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3573">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3574">**short_name**: kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="a8f47-3574">**short_name**: Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="a8f47-3575">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3575">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="a8f47-3576">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3576">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>
- <span data-ttu-id="a8f47-3577">**unicode_name_buffer_length**: Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3577">**unicode_name_buffer_length**: Size of the Unicode name buffer.</span></span> <span data-ttu-id="a8f47-3578">Note: bir NULL Sonlandırıcı gereklidir ve bu da ek bir bayt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3578">Note: A NULL terminator is required, which makes an extra byte.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3579">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3579">Return Values</span></span>

- <span data-ttu-id="a8f47-3580">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3580">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="a8f47-3581">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3581">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="a8f47-3582">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-3582">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-3583">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3583">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3584">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3584">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3585">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3585">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="a8f47-3586">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3586">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-3587">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3587">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="a8f47-3588">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3588">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3589">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3589">Allowed From</span></span>

<span data-ttu-id="a8f47-3590">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3590">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3591">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3591">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3592">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3592">See Also</span></span>

- <span data-ttu-id="a8f47-3593">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3593">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3594">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3594">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3595">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3595">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3596">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3596">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3597">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3597">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3598">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3598">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3599">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3599">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3600">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3600">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3601">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3601">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3602">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3602">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3603">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3603">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3604">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3604">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3605">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3605">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3606">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3606">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3607">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3607">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3608">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3608">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3609">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3609">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3610">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3610">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3611">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3611">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3612">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3612">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3613">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3613">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3614">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3614">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3615">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3615">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3616">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3616">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-3617">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3617">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-3618">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3618">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_short_name_get"></a><span data-ttu-id="a8f47-3619">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3619">fx_unicode_short_name_get</span></span>

<span data-ttu-id="a8f47-3620">Unicode adından kısa adı alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3620">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3621">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3621">Prototype</span></span>

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

<span data-ttu-id="a8f47-3622">Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3622">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="a8f47-3623">Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3623">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3624">*Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3624">*This service can be used to get short names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3625">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3625">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3626">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3626">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3627">**source_unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3627">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="a8f47-3628">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3628">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="a8f47-3629">**destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3629">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="a8f47-3630">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3630">This must be at least 13 bytes in size.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3631">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3631">Return Values</span></span>

- <span data-ttu-id="a8f47-3632">**FX_SUCCESS** (0x00) başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3632">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="a8f47-3633">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3633">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="a8f47-3634">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-3634">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="a8f47-3635">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3635">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3636">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3637">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3637">**FX_NOT_FOUND** (0x04)    Unicode name was not found.</span></span>
- <span data-ttu-id="a8f47-3638">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3638">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="a8f47-3639">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3639">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-3640">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3640">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="a8f47-3641">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3641">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3642">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3642">Allowed From</span></span>

<span data-ttu-id="a8f47-3643">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3643">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3644">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3644">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3645">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3645">See Also</span></span>

- <span data-ttu-id="a8f47-3646">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3646">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3647">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3647">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3648">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3648">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3649">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3649">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3650">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3650">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3651">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3651">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3652">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3652">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3653">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3653">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3654">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3654">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3655">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3655">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3656">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3656">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3657">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3657">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3658">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3658">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3659">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3659">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3660">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3660">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3661">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3661">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3662">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3662">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3663">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3663">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3664">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3664">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3665">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3665">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3666">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3666">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3667">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3667">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3668">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3668">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3669">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3669">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-3670">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3670">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-3671">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3671">fx_unicode_name_get</span></span>

## <a name="fx_unicode_short_name_get_extended"></a><span data-ttu-id="a8f47-3672">fx_unicode_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="a8f47-3672">fx_unicode_short_name_get_extended</span></span>

<span data-ttu-id="a8f47-3673">Unicode adından kısa adı alır</span><span class="sxs-lookup"><span data-stu-id="a8f47-3673">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="a8f47-3674">Prototype</span><span class="sxs-lookup"><span data-stu-id="a8f47-3674">Prototype</span></span>

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="a8f47-3675">Description</span><span class="sxs-lookup"><span data-stu-id="a8f47-3675">Description</span></span>

<span data-ttu-id="a8f47-3676">Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3676">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="a8f47-3677">Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3677">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f47-3678">*Çağıran, hedef arabelleğin bir giriş bağımsız değişkeni olarak boyutunu sağladığı, bu hizmet **fx_unicode_short_name_get ()** ile aynıdır. Bu, hizmetin kısa adı hedef arabelleği aşmadığını garanti etmesine olanak tanır.*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3678">*This service is identical to **fx_unicode_short_name_get()**, except the caller supplies the size of the destination buffer as an input argument. This allows the service to guarantee the short name does not exceed the destination buffer.*</span></span>

<span data-ttu-id="a8f47-3679">*Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="a8f47-3679">*This service can be used to get short names for both files and subdirectories*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a8f47-3680">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3680">Input Parameters</span></span>

- <span data-ttu-id="a8f47-3681">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3681">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="a8f47-3682">**source_unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3682">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="a8f47-3683">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3683">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="a8f47-3684">**destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3684">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="a8f47-3685">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3685">This must be at least 13 bytes in size.</span></span>
- <span data-ttu-id="a8f47-3686">**short_name_buffer_length**: hedef arabelleğin boyutu.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3686">**short_name_buffer_length**: Size of the destination buffer.</span></span> <span data-ttu-id="a8f47-3687">Arabellek boyutu en az 14 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3687">The buffer size must be at least 14 bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="a8f47-3688">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a8f47-3688">Return Values</span></span>

- <span data-ttu-id="a8f47-3689">**FX_SUCCESS** (0x00) başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3689">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="a8f47-3690">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3690">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="a8f47-3691">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="a8f47-3691">**FX_FILE_CORRUPT** (0x08)    File is corrupted</span></span>
- <span data-ttu-id="a8f47-3692">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3692">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="a8f47-3693">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3693">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="a8f47-3694">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3694">**FX_NOT_FOUND** (0x04) Unicode name was not found.</span></span>
- <span data-ttu-id="a8f47-3695">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3695">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="a8f47-3696">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3696">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="a8f47-3697">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3697">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="a8f47-3698">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3698">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a8f47-3699">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a8f47-3699">Allowed From</span></span>

<span data-ttu-id="a8f47-3700">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a8f47-3700">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a8f47-3701">Örnek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3701">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="a8f47-3702">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a8f47-3702">See Also</span></span>

- <span data-ttu-id="a8f47-3703">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3703">fx_file_allocate</span></span>
- <span data-ttu-id="a8f47-3704">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3704">fx_file_attributes_read</span></span>
- <span data-ttu-id="a8f47-3705">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3705">fx_file_attributes_set</span></span>
- <span data-ttu-id="a8f47-3706">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3706">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3707">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="a8f47-3707">fx_file_close</span></span>
- <span data-ttu-id="a8f47-3708">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3708">fx_file_create</span></span>
- <span data-ttu-id="a8f47-3709">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3709">fx_file_date_time_set</span></span>
- <span data-ttu-id="a8f47-3710">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="a8f47-3710">fx_file_delete</span></span>
- <span data-ttu-id="a8f47-3711">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3711">fx_file_extended_allocate</span></span>
- <span data-ttu-id="a8f47-3712">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3712">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="a8f47-3713">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3713">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="a8f47-3714">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3714">fx_file_extended_seek</span></span>
- <span data-ttu-id="a8f47-3715">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3715">fx_file_extended_truncate</span></span>
- <span data-ttu-id="a8f47-3716">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3716">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="a8f47-3717">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="a8f47-3717">fx_file_open</span></span>
- <span data-ttu-id="a8f47-3718">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="a8f47-3718">fx_file_read</span></span>
- <span data-ttu-id="a8f47-3719">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3719">fx_file_relative_seek</span></span>
- <span data-ttu-id="a8f47-3720">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3720">fx_file_rename</span></span>
- <span data-ttu-id="a8f47-3721">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="a8f47-3721">fx_file_seek</span></span>
- <span data-ttu-id="a8f47-3722">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="a8f47-3722">fx_file_truncate</span></span>
- <span data-ttu-id="a8f47-3723">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="a8f47-3723">fx_file_truncate_release</span></span>
- <span data-ttu-id="a8f47-3724">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="a8f47-3724">fx_file_write</span></span>
- <span data-ttu-id="a8f47-3725">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="a8f47-3725">fx_file_write_notify_set</span></span>
- <span data-ttu-id="a8f47-3726">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="a8f47-3726">fx_unicode_file_create</span></span>
- <span data-ttu-id="a8f47-3727">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="a8f47-3727">fx_unicode_file_rename</span></span>
- <span data-ttu-id="a8f47-3728">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3728">fx_unicode_name_get</span></span>
- <span data-ttu-id="a8f47-3729">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="a8f47-3729">fx_unicode_short_name_get</span></span>
