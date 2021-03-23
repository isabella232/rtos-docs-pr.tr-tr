---
title: Bölüm 4-Azure RTOS FileX hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS FileX hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c9e91244856b322d53f85bdd572bd317a055776a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826543"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a><span data-ttu-id="8b105-103">Bölüm 4-Azure RTOS FileX hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="8b105-103">Chapter 4- Description of Azure RTOS FileX services</span></span>

<span data-ttu-id="8b105-104">Bu bölüm, tüm Azure RTOS FileX hizmetlerinin alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="8b105-104">This chapter contains a description of all Azure RTOS FileX services in alphabetic order.</span></span> <span data-ttu-id="8b105-105">Hizmet adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-105">Service names are designed so all similar services are grouped together.</span></span>

## <a name="fx_directory_attributes_read"></a><span data-ttu-id="8b105-106">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-106">fx_directory_attributes_read</span></span>

<span data-ttu-id="8b105-107">Dizin özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="8b105-107">Reads directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-108">Prototype</span></span>

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a><span data-ttu-id="8b105-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-109">Description</span></span>

<span data-ttu-id="8b105-110">Bu hizmet, dizinin özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="8b105-110">This service reads the directory's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-111">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-111">Input Parameters</span></span>

- <span data-ttu-id="8b105-112">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-112">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-113">**directory_name**: istenen dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-113">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="8b105-114">**öznitelikler** _Ptr: dizin özniteliklerinin yerleştirileceği hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-114">**attributes** _ptr: Pointer to the destination for the directory's attributes to be placed.</span></span> <span data-ttu-id="8b105-115">Dizin öznitelikleri, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8b105-115">The directory attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8b105-116">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-116">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8b105-117">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-117">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8b105-118">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8b105-118">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8b105-119">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="8b105-119">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="8b105-120">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="8b105-120">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="8b105-121">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8b105-121">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-122">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-122">Return Values</span></span>

- <span data-ttu-id="8b105-123">**FX_SUCCESS** (0x00) başarılı dizin öznitelikleri okundu</span><span class="sxs-lookup"><span data-stu-id="8b105-123">**FX_SUCCESS** (0x00) Successful directory attributes read</span></span>
- <span data-ttu-id="8b105-124">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-124">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-125">**FX _NOT bulunan** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b105-125">**FX _NOT FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8b105-126">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8b105-126">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="8b105-127">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-127">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-128">**FX_FILE_CORRUPT** 0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-128">**FX_FILE_CORRUPT** 0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-129">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-129">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-130">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-130">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-131">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-131">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-132">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8b105-132">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8b105-133">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-133">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8b105-134">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-134">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-135">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-135">Allowed From</span></span>

<span data-ttu-id="8b105-136">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-136">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-137">Example</span></span>

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a><span data-ttu-id="8b105-138">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-138">See Also</span></span>

- <span data-ttu-id="8b105-139">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-139">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-140">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-140">fx_directory_create</span></span>
- <span data-ttu-id="8b105-141">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-141">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-142">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-142">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-143">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-143">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-144">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-144">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-145">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-145">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-146">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-146">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-147">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-147">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-148">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-148">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-149">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-149">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-150">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-150">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-151">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-151">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-152">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-152">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-153">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-153">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-154">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-154">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-155">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-155">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-156">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-156">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-157">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-157">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-158">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-158">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_attributes_set"></a><span data-ttu-id="8b105-159">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-159">fx_directory_attributes_set</span></span>

<span data-ttu-id="8b105-160">Dizin özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-160">Sets directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-161">Prototype</span></span>

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a><span data-ttu-id="8b105-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-162">Description</span></span>

<span data-ttu-id="8b105-163">Bu hizmet, dizinin özniteliklerini çağıran tarafından belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-163">This service sets the directory's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-164">*Bu uygulamanın yalnızca bu hizmetle dizin özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlamaya yönelik her türlü girişim bir hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="8b105-164">*This application is only allowed to modify a subset of the directory's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-165">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-165">Input Parameters</span></span>

- <span data-ttu-id="8b105-166">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-166">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-167">**directory_name**: istenen dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-167">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="8b105-168">**öznitelikler**: bu dizine yönelik yeni öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="8b105-168">**attributes**: The new attributes to this directory.</span></span> <span data-ttu-id="8b105-169">Geçerli dizin öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8b105-169">The valid directory attributes are defined as follows:</span></span>
  - <span data-ttu-id="8b105-170">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-170">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8b105-171">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-171">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8b105-172">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8b105-172">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8b105-173">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8b105-173">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-174">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-174">Return Values</span></span>

- <span data-ttu-id="8b105-175">**FX_SUCCESS** (0x00) başarılı Dizin öznitelik kümesi</span><span class="sxs-lookup"><span data-stu-id="8b105-175">**FX_SUCCESS** (0x00) Successful directory attribute set</span></span>
- <span data-ttu-id="8b105-176">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-176">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-177">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b105-177">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8b105-178">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8b105-178">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="8b105-179">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-179">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-180">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="8b105-180">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="8b105-181">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-181">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-182">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-182">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-183">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-183">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-184">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-184">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-185">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8b105-185">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8b105-186">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="8b105-186">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8b105-187">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-187">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8b105-188">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="8b105-188">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="8b105-189">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-190">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-190">Allowed From</span></span>

<span data-ttu-id="8b105-191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-192">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-192">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-193">See Also</span></span>

- <span data-ttu-id="8b105-194">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-194">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-195">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-195">fx_directory_create</span></span>
- <span data-ttu-id="8b105-196">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-196">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-197">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-197">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-198">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-198">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-199">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-199">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-200">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-200">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-201">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-201">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-202">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-202">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-203">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-203">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-204">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-204">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-205">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-205">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-206">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-206">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-207">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-207">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-208">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-208">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-209">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-209">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-210">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-210">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-211">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-211">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-212">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-212">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-213">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-213">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_create"></a><span data-ttu-id="8b105-214">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-214">fx_directory_create</span></span>

<span data-ttu-id="8b105-215">Alt dizin oluşturur</span><span class="sxs-lookup"><span data-stu-id="8b105-215">Creates subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-216">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-216">Prototype</span></span>

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a><span data-ttu-id="8b105-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-217">Description</span></span>

<span data-ttu-id="8b105-218">Bu hizmet, geçerli varsayılan dizinde veya dizin adında sağlanan yolda bir alt dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b105-218">This service creates a subdirectory in the current default directory or in the path supplied in the directory name.</span></span> <span data-ttu-id="8b105-219">Kök dizinden farklı olarak, alt dizinlerin tutabilecekleri dosya sayısı için bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="8b105-219">Unlike the root directory, subdirectories do not have a limit on the number of files they can hold.</span></span> <span data-ttu-id="8b105-220">Kök dizin yalnızca önyükleme kaydı tarafından belirlenen girdi sayısını tutabilirler.</span><span class="sxs-lookup"><span data-stu-id="8b105-220">The root directory can only hold the number of entries determined by the boot record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-221">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-221">Input Parameters</span></span>

- <span data-ttu-id="8b105-222">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-222">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-223">**directory_name**: Oluşturulacak dizinin adına yönelik işaretçi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-223">**directory_name**: Pointer to the name of the directory to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-224">Return Values</span></span>

- <span data-ttu-id="8b105-225">**FX_SUCCESS** (0x00) başarılı dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8b105-225">**FX_SUCCESS** (0x00) Successful directory create.</span></span>
- <span data-ttu-id="8b105-226">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-226">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-227">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b105-227">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8b105-228">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8b105-228">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="8b105-229">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-229">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-230">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-230">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-231">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-231">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-232">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-232">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-233">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-233">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-234">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8b105-234">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8b105-235">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="8b105-235">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8b105-236">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-236">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8b105-237">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="8b105-237">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="8b105-238">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-238">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-239">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-239">Allowed From</span></span>

<span data-ttu-id="8b105-240">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-240">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-241">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-242">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-242">See Also</span></span>

- <span data-ttu-id="8b105-243">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-243">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-244">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-244">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-245">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-245">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-246">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-246">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-247">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-247">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-248">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-248">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-249">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-249">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-250">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-250">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-251">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-251">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-252">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-252">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-253">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-253">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-254">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-254">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-255">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-255">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-256">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-256">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-257">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-257">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-258">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-258">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-259">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-259">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-260">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-260">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-261">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-261">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-262">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-262">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_get"></a><span data-ttu-id="8b105-263">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-263">fx_directory_default_get</span></span>

<span data-ttu-id="8b105-264">Son varsayılan dizini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-264">Gets last default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-265">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-265">Prototype</span></span>

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="8b105-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-266">Description</span></span>

<span data-ttu-id="8b105-267">Bu hizmet, ***fx_directory_default_set*** tarafından en son ayarlanan yola yönelik işaretçiyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b105-267">This service returns the pointer to the path last set by ***fx_directory_default_set***.</span></span> <span data-ttu-id="8b105-268">Varsayılan dizin ayarlanmamışsa veya geçerli varsayılan dizin kök dizin ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-268">If the default directory has not been set or if the current default directory is the root directory, a value of FX_NULL is returned.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-269">*İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="8b105-269">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-270">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-270">Input Parameters</span></span>

- <span data-ttu-id="8b105-271">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-271">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-272">**return_path_name**: son varsayılan dizin dizesinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-272">**return_path_name**: Pointer to the destination for the last default directory string.</span></span> <span data-ttu-id="8b105-273">Varsayılan dizinin geçerli ayarı kök ise FX_NULL değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-273">A value of FX_NULL is returned if the current setting of the default directory is the root.</span></span> <span data-ttu-id="8b105-274">Medya açıldığında, kök varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="8b105-274">When the media is opened, root is the default.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-275">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-275">Return Values</span></span>

- <span data-ttu-id="8b105-276">**FX_SUCCESS** (0x00) başarılı varsayılan dizin Al</span><span class="sxs-lookup"><span data-stu-id="8b105-276">**FX_SUCCESS** (0x00) Successful default directory get</span></span>
- <span data-ttu-id="8b105-277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-278">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-278">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="8b105-279">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-279">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-280">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-280">Allowed From</span></span>

<span data-ttu-id="8b105-281">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-282">Example</span></span>

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a><span data-ttu-id="8b105-283">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-283">See Also</span></span>

- <span data-ttu-id="8b105-284">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-284">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-285">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-285">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-286">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-286">fx_directory_create</span></span>
- <span data-ttu-id="8b105-287">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-287">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-288">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-288">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-289">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-289">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-290">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-290">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-291">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-291">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-292">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-292">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-293">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-293">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-294">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-294">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-295">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-295">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-296">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-296">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-297">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-297">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-298">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-298">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-299">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-299">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-300">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-300">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-301">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-301">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-302">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-302">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-303">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-303">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_set"></a><span data-ttu-id="8b105-304">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-304">fx_directory_default_set</span></span>

<span data-ttu-id="8b105-305">Varsayılan dizini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-305">Sets default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-306">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-306">Prototype</span></span>

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="8b105-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-307">Description</span></span>

<span data-ttu-id="8b105-308">Bu hizmet, medyanın varsayılan dizinini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-308">This service sets the default directory of the media.</span></span> <span data-ttu-id="8b105-309">FX_NULL değeri sağlanırsa, varsayılan dizin medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-309">If a value of FX_NULL is supplied, the default directory is set to the media's root directory.</span></span> <span data-ttu-id="8b105-310">Açıkça bir yol belirtmeyen tüm sonraki dosya işlemleri bu dizine varsayılan olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-310">All subsequent file operations that do not explicitly specify a path will default to this directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-311">*İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="8b105-311">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-312">*Uygulama tarafından sağlanan adlar için, FileX, \\ dizinler, alt dizinler ve dosya adlarına ayrı ters eğik çizgi () ve eğik çizgi (/) karakterlerini destekler. Ancak, FileX yalnızca uygulamaya döndürülen yollarda ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-312">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-313">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-313">Input Parameters</span></span>

- <span data-ttu-id="8b105-314">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-314">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-315">**new_path_name**: yeni varsayılan dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-315">**new_path_name**: Pointer to new default directory name.</span></span> <span data-ttu-id="8b105-316">Bir FX_NULL değeri sağlanırsa, medyanın varsayılan dizini medyanın kök dizinine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-316">If a value of FX_NULL is supplied, the default directory of the media is set to the media's root directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-317">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-317">Return Values</span></span>

- <span data-ttu-id="8b105-318">**FX_SUCCESS** (0x00) başarılı varsayılan dizin kümesi</span><span class="sxs-lookup"><span data-stu-id="8b105-318">**FX_SUCCESS** (0x00)  Successful default directory set</span></span>
- <span data-ttu-id="8b105-319">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-319">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-320">**FX_INVALID_PATH** (0x0D) yeni dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b105-320">**FX_INVALID_PATH** (0x0D) New directory could not be found</span></span>
- <span data-ttu-id="8b105-321">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-321">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-322">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-322">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-323">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-323">Allowed From</span></span>

<span data-ttu-id="8b105-324">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-324">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-325">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-325">Example</span></span>

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-326">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-326">See Also</span></span>

- <span data-ttu-id="8b105-327">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-327">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-328">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-328">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-329">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-329">fx_directory_create</span></span>
- <span data-ttu-id="8b105-330">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-330">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-331">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-331">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-332">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-332">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-333">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-333">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-334">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-334">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-335">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-335">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-336">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-336">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-337">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-337">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-338">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-338">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-339">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-339">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-340">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-340">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-341">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-341">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-342">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-342">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-343">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-343">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-344">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-344">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-345">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-345">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-346">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-346">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_delete"></a><span data-ttu-id="8b105-347">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-347">fx_directory_delete</span></span>

<span data-ttu-id="8b105-348">Alt dizini siler</span><span class="sxs-lookup"><span data-stu-id="8b105-348">Deletes subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-349">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-349">Prototype</span></span>

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="8b105-350">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-350">Description</span></span>

<span data-ttu-id="8b105-351">Bu hizmet belirtilen dizini siler.</span><span class="sxs-lookup"><span data-stu-id="8b105-351">This service deletes the specified directory.</span></span> <span data-ttu-id="8b105-352">Silmek için dizinin boş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b105-352">Note that the directory must be empty to delete it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-353">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-353">Input Parameters</span></span>

- <span data-ttu-id="8b105-354">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-354">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-355">**directory_name**: silinecek dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-355">**directory_name**: Pointer to name of directory to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-356">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-356">Return Values</span></span>

- <span data-ttu-id="8b105-357">**FX_SUCCESS** (0x00) başarılı dizin silme</span><span class="sxs-lookup"><span data-stu-id="8b105-357">**FX_SUCCESS** (0x00) Successful directory delete</span></span>
- <span data-ttu-id="8b105-358">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-358">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-359">**FX_NOT_FOUND** (0x04) belirtilen dizin bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b105-359">**FX_NOT_FOUND** (0x04) Specified directory was not found</span></span>
- <span data-ttu-id="8b105-360">**FX_DIR_NOT_EMPTY** (0x10) belirtilen dizin boş değil</span><span class="sxs-lookup"><span data-stu-id="8b105-360">**FX_DIR_NOT_EMPTY** (0x10) Specified directory is not empty</span></span>
- <span data-ttu-id="8b105-361">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-361">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-362">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="8b105-362">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="8b105-363">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-363">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-364">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-364">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-365">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-365">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-366">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-366">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-367">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8b105-367">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8b105-368">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="8b105-368">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8b105-369">**FX_NOT_DIRECTORY** (0x0E) dizin girişi değil</span><span class="sxs-lookup"><span data-stu-id="8b105-369">**FX_NOT_DIRECTORY** (0x0E) Not a directory entry</span></span>
- <span data-ttu-id="8b105-370">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-370">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="8b105-371">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-371">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-372">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-372">Allowed From</span></span>

<span data-ttu-id="8b105-373">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-373">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-374">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-374">Example</span></span>
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-375">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-375">See Also</span></span>

- <span data-ttu-id="8b105-376">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-376">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-377">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-377">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-378">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-378">fx_directory_create</span></span>
- <span data-ttu-id="8b105-379">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-379">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-380">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-380">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-381">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-381">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-382">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-382">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-383">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-383">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-384">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-384">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-385">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-385">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-386">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-386">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-387">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-387">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-388">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-388">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-389">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-389">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-390">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-390">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-391">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-391">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-392">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-392">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-393">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-393">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-394">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-394">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-395">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-395">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_entry_find"></a><span data-ttu-id="8b105-396">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-396">fx_directory_first_entry_find</span></span>

<span data-ttu-id="8b105-397">İlk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-397">Gets first directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-398">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-398">Prototype</span></span>

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="8b105-399">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-399">Description</span></span>

<span data-ttu-id="8b105-400">Bu hizmet, varsayılan dizindeki ilk giriş adını alır ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8b105-400">This service retrieves the first entry name in the default directory and copies it to the specified destination.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-401">*Belirtilen hedef, FX_MAX_LONG_NAME_LEN tarafından tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır **.***</span><span class="sxs-lookup"><span data-stu-id="8b105-401">*The specified destination must be large enough to hold the maximum sized FileX name, as defined by **FX_MAX_LONG_NAME_LEN.***</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-402">*Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-402">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-403">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-403">Input Parameters</span></span>

- <span data-ttu-id="8b105-404">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-404">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-405">**return_entry_name**: varsayılan dizindeki ilk giriş adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-405">**return_entry_name**: Pointer to destination for the first entry name in the default directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-406">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-406">Return Values</span></span>

- <span data-ttu-id="8b105-407">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="8b105-407">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="8b105-408">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-408">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-409">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="8b105-409">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8b105-410">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-410">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-411">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-411">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-412">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-412">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-413">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-413">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-414">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-414">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer</span></span>
- <span data-ttu-id="8b105-415">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="8b105-415">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-416">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-416">Allowed From</span></span>

<span data-ttu-id="8b105-417">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-417">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-418">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-418">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-419">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-419">See Also</span></span>

- <span data-ttu-id="8b105-420">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-420">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-421">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-421">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-422">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-422">fx_directory_create</span></span>
- <span data-ttu-id="8b105-423">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-423">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-424">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-424">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-425">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-425">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-426">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-426">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-427">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-427">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-428">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-428">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-429">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-429">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-430">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-430">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-431">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-431">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-432">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-432">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-433">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-433">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-434">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-434">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-435">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-435">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-436">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-436">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-437">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-437">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-438">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-438">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-439">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-439">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="8b105-440">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-440">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="8b105-441">Tüm bilgileri içeren ilk dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-441">Gets first directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-442">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-442">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="8b105-443">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-443">Input Parameters</span></span>

- <span data-ttu-id="8b105-444">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-444">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-445">**directory_name**: bir dizin girişi adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-445">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="8b105-446">En az FX_MAX_LONG_NAME_LEN kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-446">Must be at least as big as FX_MAX_LONG_NAME_LEN.</span></span>
- <span data-ttu-id="8b105-447">**öznitelikler**: null olmayan, girişin özniteliklerinin yerleştirileceği hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-447">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.</span></span> <span data-ttu-id="8b105-448">Öznitelikler, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8b105-448">The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8b105-449">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-449">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="8b105-450">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-450">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="8b105-451">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="8b105-451">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="8b105-452">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="8b105-452">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="8b105-453">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="8b105-453">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="8b105-454">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="8b105-454">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="8b105-455">**Boyut**: null olmayan, girdinin bayt cinsinden boyutu için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-455">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="8b105-456">**yıl**: null olmayan, girişin değiştirilme yılından hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-456">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="8b105-457">**ay**: null olmayan, girişin değiştirilme ayı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-457">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="8b105-458">**gün**: null olmayan, girişin değiştirilme günü için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-458">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="8b105-459">**saat**: null olmayan, girişin değiştirilme saati için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-459">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="8b105-460">**dakika**: null olmayan, girişin değiştirilme dakikası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-460">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="8b105-461">**ikinci**: null olmayan, girişin değiştirilme saniyesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-461">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-462">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-462">Return Values</span></span>

- <span data-ttu-id="8b105-463">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="8b105-463">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="8b105-464">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-464">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-465">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok</span><span class="sxs-lookup"><span data-stu-id="8b105-465">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="8b105-466">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-466">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-467">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı</span><span class="sxs-lookup"><span data-stu-id="8b105-467">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="8b105-468">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-468">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-469">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-469">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-470">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-470">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-471">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-471">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-472">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8b105-472">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8b105-473">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-473">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="8b105-474">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-474">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-475">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-475">Allowed From</span></span>

<span data-ttu-id="8b105-476">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-476">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-477">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-477">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-478">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-478">See Also</span></span>

- <span data-ttu-id="8b105-479">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-479">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-480">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-480">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-481">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-481">fx_directory_create</span></span>
- <span data-ttu-id="8b105-482">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-482">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-483">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-483">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-484">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-484">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-485">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-485">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-486">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-486">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-487">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-487">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-488">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-488">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-489">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-489">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-490">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-490">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-491">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-491">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-492">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-492">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-493">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-493">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-494">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-494">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-495">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-495">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-496">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-496">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-497">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-497">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-498">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-498">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_information_get"></a><span data-ttu-id="8b105-499">fx_directory_information_get:</span><span class="sxs-lookup"><span data-stu-id="8b105-499">fx_directory_information_get:</span></span>

<span data-ttu-id="8b105-500">Dizin girişi bilgilerini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-500">Gets directory entry information</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-501">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-501">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="8b105-502">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-502">Input Parameters</span></span>

- <span data-ttu-id="8b105-503">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-503">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-504">**directory_name**: Dizin girişinin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-504">**directory_name**: Pointer to name of the directory entry.</span></span>
- <span data-ttu-id="8b105-505">**öznitelikler**: özniteliklerin hedefe yönelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-505">**attributes**: Pointer to the destination for the attributes.</span></span>
- <span data-ttu-id="8b105-506">**Boyut**: boyut için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-506">**size**: Pointer to the destination for the size.</span></span>
- <span data-ttu-id="8b105-507">**Year**: yıl için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-507">**year**: Pointer to the destination for the year.</span></span>
- <span data-ttu-id="8b105-508">**Month**: ayın hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-508">**month**: Pointer to the destination for the month.</span></span>
- <span data-ttu-id="8b105-509">**Day**: günün hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-509">**day**: Pointer to the destination for the day.</span></span>
- <span data-ttu-id="8b105-510">**saat**: saat için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-510">**hour**: Pointer to the destination for the hour.</span></span>
- <span data-ttu-id="8b105-511">**Minute**: dakika için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-511">**minute**: Pointer to the destination for the minute.</span></span>
- <span data-ttu-id="8b105-512">**ikinci**: ikincisi için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-512">**second**: Pointer to the destination for the second.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-513">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-513">Return Values</span></span>

- <span data-ttu-id="8b105-514">**FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma</span><span class="sxs-lookup"><span data-stu-id="8b105-514">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="8b105-515">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-515">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-516">**FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b105-516">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="8b105-517">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-517">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-518">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8b105-518">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8b105-519">**FX_FILE _CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-519">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-520">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-520">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-521">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-521">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-522">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-522">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-523">**FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-523">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="8b105-524">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-524">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-525">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-525">Allowed From</span></span>

<span data-ttu-id="8b105-526">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-526">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-527">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-527">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-528">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-528">See Also</span></span>

- <span data-ttu-id="8b105-529">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-529">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-530">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-530">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-531">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-531">fx_directory_create</span></span>
- <span data-ttu-id="8b105-532">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-532">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-533">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-533">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-534">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-534">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-535">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-535">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-536">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-536">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-537">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-537">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-538">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-538">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-539">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-539">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-540">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-540">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-541">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-541">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-542">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-542">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-543">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-543">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-544">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-544">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-545">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-545">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-546">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-546">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-547">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-547">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-548">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-548">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_clear"></a><span data-ttu-id="8b105-549">fx_directory_local_path_clear:</span><span class="sxs-lookup"><span data-stu-id="8b105-549">fx_directory_local_path_clear:</span></span>

<span data-ttu-id="8b105-550">Varsayılan yerel yolu temizler</span><span class="sxs-lookup"><span data-stu-id="8b105-550">Clears default local path</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-551">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-551">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="8b105-552">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-552">Description</span></span>

<span data-ttu-id="8b105-553">Bu hizmet, çağıran iş parçacığı için ayarlanan önceki yerel yolu temizler.</span><span class="sxs-lookup"><span data-stu-id="8b105-553">This service clears the previous local path set up for the calling thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-554">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-554">Input Parameters</span></span>

- <span data-ttu-id="8b105-555">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-555">**media_ptr**: Pointer to a previously opened media.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-556">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-556">Return Values</span></span>

- <span data-ttu-id="8b105-557">**FX_SUCCESS** (0x00) başarılı yerel yol temizleme.</span><span class="sxs-lookup"><span data-stu-id="8b105-557">**FX_SUCCESS** (0x00) Successful local path clear.</span></span>
- <span data-ttu-id="8b105-558">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-558">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="8b105-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlandı</span><span class="sxs-lookup"><span data-stu-id="8b105-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined</span></span>
- <span data-ttu-id="8b105-560">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-560">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-561">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-561">Allowed From</span></span>

<span data-ttu-id="8b105-562">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-562">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-563">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-563">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-564">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-564">See Also</span></span>

- <span data-ttu-id="8b105-565">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-565">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-566">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-566">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-567">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-567">fx_directory_create</span></span>
- <span data-ttu-id="8b105-568">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-568">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-569">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-569">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-570">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-570">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-571">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-571">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-572">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-572">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-573">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-573">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-574">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-574">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-575">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-575">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-576">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-576">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-577">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-577">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-578">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-578">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-579">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-579">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-580">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-580">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-581">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-581">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-582">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-582">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-583">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-583">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-584">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-584">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_get"></a><span data-ttu-id="8b105-585">fx_directory_local_path_get:</span><span class="sxs-lookup"><span data-stu-id="8b105-585">fx_directory_local_path_get:</span></span>

<span data-ttu-id="8b105-586">Geçerli yerel yol dizesini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-586">Gets the current local path string</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-587">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-587">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="8b105-588">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-588">Description</span></span>

<span data-ttu-id="8b105-589">Bu hizmet, belirtilen medyanın yerel yol işaretçisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b105-589">This service returns the local path pointer of the specified media.</span></span> <span data-ttu-id="8b105-590">Yerel bir yol ayarlanmamışsa, çağırana bir NULL döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-590">If there is no local path set, a NULL is returned to the caller.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-591">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-591">Input Parameters</span></span>

- <span data-ttu-id="8b105-592">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-592">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-593">**return_path_name**: yerel yol dizesinin depolanacağı hedef dize işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-593">**return_path_name**: Pointer to the destination string pointer for the local path string to be stored.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-594">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-594">Return Values</span></span>

- <span data-ttu-id="8b105-595">**FX_SUCCESS** (0x00) başarılı yerel yol al.</span><span class="sxs-lookup"><span data-stu-id="8b105-595">**FX_SUCCESS** (0x00) Successful local path get.</span></span>
- <span data-ttu-id="8b105-596">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-596">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="8b105-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="8b105-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="8b105-598">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-598">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>


### <a name="allowed-from"></a><span data-ttu-id="8b105-599">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-599">Allowed From</span></span>

<span data-ttu-id="8b105-600">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-600">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-601">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-601">Example</span></span>

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-602">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-602">See Also</span></span>

- <span data-ttu-id="8b105-603">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-603">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-604">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-604">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-605">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-605">fx_directory_create</span></span>
- <span data-ttu-id="8b105-606">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-606">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-607">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-607">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-608">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-608">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-609">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-609">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-610">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-610">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-611">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-611">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-612">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-612">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-613">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-613">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-614">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-614">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-615">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-615">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-616">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-616">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-617">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-617">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-618">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-618">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-619">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-619">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-620">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-620">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-621">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-621">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-622">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-622">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_restore"></a><span data-ttu-id="8b105-623">fx_directory_local_path_restore:</span><span class="sxs-lookup"><span data-stu-id="8b105-623">fx_directory_local_path_restore:</span></span>

<span data-ttu-id="8b105-624">Önceki yerel yolu geri yükler</span><span class="sxs-lookup"><span data-stu-id="8b105-624">Restores previous local path</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-625">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-625">Prototype</span></span>

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a><span data-ttu-id="8b105-626">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-626">Description</span></span>

<span data-ttu-id="8b105-627">Bu hizmet daha önce ayarlanmış bir yerel yolu geri yükler.</span><span class="sxs-lookup"><span data-stu-id="8b105-627">This service restores a previously set local path.</span></span> <span data-ttu-id="8b105-628">Bu yerel yolda yapılan dizin arama konumu da geri yüklenir, bu da bu yordamı uygulama tarafından özyinelemeli Dizin traversals ' de yararlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-628">The directory search position made on this local path is also restored, which makes this routine useful in recursive directory traversals by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-629">*Her yerel yol, varsayılan olarak 256 karakter olan **FX_MAXIMUM_PATH** boyutunda bir yerel yol dizesi içerir. Bu iç yol dizesi FileX tarafından kullanılmaz ve yalnızca uygulamanın kullanımı için sağlanır. **FX_LOCAL_PATH** yerel bir değişken olarak bildiriecekse, kullanıcıların bu yapının boyutuyla büyüyen yığına dikkat etmesi gerekir. Kullanıcılar **FX_MAXIMUM_PATH** boyutunu azaltmak ve FileX kitaplık kaynağını yeniden derlemek için hoş geldiniz.*</span><span class="sxs-lookup"><span data-stu-id="8b105-629">*Each local path contains a local path string of **FX_MAXIMUM_PATH** in size, which by default is 256 characters. This internal path string is not used by FileX and is provided only for the application's use. If **FX_LOCAL_PATH** is going to be declared as a local variable, users should beware of the stack growing by the size of this structure. Users are welcome to reduce the size of **FX_MAXIMUM_PATH** and rebuild the FileX library source.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-630">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-630">Input Parameters</span></span>

- <span data-ttu-id="8b105-631">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-631">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-632">**local_path_ptr**: daha önce ayarlanan yerel yola yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-632">**local_path_ptr**: Pointer to the previously set local path.</span></span> <span data-ttu-id="8b105-633">Bu işaretçinin gerçekten daha önce kullanılmış ve bozulmadan yerel yola işaret ettiğinden emin olmak çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8b105-633">It's very important to ensure that this pointer does indeed point to a previously used and still intact local path.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-634">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-634">Return Values</span></span>

- <span data-ttu-id="8b105-635">**FX_SUCCESS** (0x00) başarılı yerel yol geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="8b105-635">**FX_SUCCESS** (0x00) Successful local path restore.</span></span>
- <span data-ttu-id="8b105-636">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open.</span></span>
- <span data-ttu-id="8b105-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="8b105-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined.</span></span>
- <span data-ttu-id="8b105-638">**FX_PTR_ERROR** (0x18) geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-638">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-639">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-639">Allowed From</span></span>

<span data-ttu-id="8b105-640">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-640">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-641">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-641">Example</span></span>

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-642">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-642">See Also</span></span>

- <span data-ttu-id="8b105-643">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-643">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-644">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-644">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-645">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-645">fx_directory_create</span></span>
- <span data-ttu-id="8b105-646">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-646">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-647">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-647">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-648">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-648">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-649">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-649">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-650">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-650">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-651">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-651">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-652">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-652">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-653">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-653">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-654">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-654">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-655">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-655">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-656">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-656">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-657">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-657">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-658">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-658">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-659">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-659">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-660">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-660">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-661">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-661">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-662">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-662">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_set"></a><span data-ttu-id="8b105-663">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-663">fx_directory_local_path_set</span></span>

<span data-ttu-id="8b105-664">İş parçacığına özgü bir yerel yol ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-664">Sets up a thread-specific local path</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-665">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-665">Prototype</span></span>

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="8b105-666">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-666">Description</span></span>

<span data-ttu-id="8b105-667">Bu hizmet, \***new_path_string** _ tarafından belirtilen bir iş parçacığına özgü yol ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-667">This service sets up a thread-specific path as specified by the \***new_path_string** _.</span></span> <span data-ttu-id="8b105-668">Bu yordamın başarıyla tamamlanmasından sonra, _ *_local_path_ptr_*\* içinde depolanan yerel yol bilgileri, bu iş parçacığı tarafından yapılan tüm dosya ve dizin işlemleri için genel medya yolundan öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="8b105-668">After successful completion of this routine, the local path information stored in _ *_local_path_ptr_*\* will take precedence over the global media path for all file and directory operations made by this thread.</span></span> <span data-ttu-id="8b105-669">Bu, sistemdeki diğer iş parçacıklarını etkilemez</span><span class="sxs-lookup"><span data-stu-id="8b105-669">This will have no impact on any other thread in the system</span></span> 
> [!IMPORTANT]
> <span data-ttu-id="8b105-670">*Yerel yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="8b105-670">*The default size of the local path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-671">*Uygulama tarafından sağlanan adlar için, FileX, \\ dizinler, alt dizinler ve dosya adlarına ayrı ters eğik çizgi () ve eğik çizgi (/) karakterlerini destekler. Ancak, FileX yalnızca uygulamaya döndürülen yollarda ters eğik çizgi karakterini kullanır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-671">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-672">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-672">Input Parameters</span></span>

- <span data-ttu-id="8b105-673">**media_ptr**: daha önce açılmış medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-673">**media_ptr**: Pointer to the previously opened media.</span></span>
- <span data-ttu-id="8b105-674">**local_path_ptr**: iş parçacığına özgü yerel yol bilgilerini tutmak için hedef.</span><span class="sxs-lookup"><span data-stu-id="8b105-674">**local_path_ptr**: Destination for holding the thread-specific local path information.</span></span> <span data-ttu-id="8b105-675">Bu yapının adresi gelecekte yerel yol geri yükleme işlevine sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-675">The address of this structure may be supplied to the local path restore function in the future.</span></span>
- <span data-ttu-id="8b105-676">**new_path_name**: kurulumun yerel yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b105-676">**new_path_name**: Specifies the local path to setup.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-677">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-677">Return Values</span></span>

- <span data-ttu-id="8b105-678">**FX_SUCCESS** (0x00) başarılı varsayılan dizin kümesi.</span><span class="sxs-lookup"><span data-stu-id="8b105-678">**FX_SUCCESS** (0x00) Successful default directory set.</span></span>
- <span data-ttu-id="8b105-679">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-679">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-680">**FX_NOT_IMPLEMENTED** (0x22) \* \* FX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="8b105-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="8b105-681">**FX_INVALID_PATH** (0x0D) yeni dizin bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-681">**FX_INVALID_PATH** (0x0D) New directory could not be found.</span></span>
- <span data-ttu-id="8b105-682">**FX_NOT_IMPLEMENTED** (0x22)-\* \* FX_NO_LOCAL_PATH tanımlı.</span><span class="sxs-lookup"><span data-stu-id="8b105-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH is defined.</span></span>
- <span data-ttu-id="8b105-683">**FX_PTR_ERROR** (0x18) geçersiz medya veya yerel yol işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-683">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-684">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-684">Allowed From</span></span>

<span data-ttu-id="8b105-685">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-685">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-686">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-686">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-687">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-687">See Also</span></span>

- <span data-ttu-id="8b105-688">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-688">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-689">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-689">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-690">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-690">fx_directory_create</span></span>
- <span data-ttu-id="8b105-691">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-691">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-692">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-692">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-693">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-693">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-694">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-694">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-695">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-695">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-696">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-696">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-697">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-697">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-698">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-698">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-699">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-699">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-700">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-700">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-701">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-701">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-702">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-702">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-703">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-703">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-704">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-704">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-705">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-705">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-706">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-706">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-707">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-707">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get"></a><span data-ttu-id="8b105-708">fx_directory_long_name_get:</span><span class="sxs-lookup"><span data-stu-id="8b105-708">fx_directory_long_name_get:</span></span>

<span data-ttu-id="8b105-709">Kısa adından uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="8b105-709">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-710">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-710">Prototype</span></span>

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a><span data-ttu-id="8b105-711">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-711">Description</span></span>

<span data-ttu-id="8b105-712">Bu hizmet, sağlanan kısa (8,3 biçim) adıyla ilişkili uzun adı (varsa) alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-712">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="8b105-713">Kısa ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-713">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-714">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-714">Input Parameters</span></span>

- <span data-ttu-id="8b105-715">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-715">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-716">**short_name**: kaynak kısa adı işaretçisi (8,3 biçim).</span><span class="sxs-lookup"><span data-stu-id="8b105-716">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="8b105-717">**long_name**: uzun ad için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-717">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="8b105-718">Uzun bir ad yoksa, kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-718">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="8b105-719">Uzun ad hedefinin FX_MAX_LONG_NAME_LEN karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b105-719">Note that the destination for the long name must be large enough to hold FX_MAX_LONG_NAME_LEN characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-720">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-720">Return Values</span></span>

- <span data-ttu-id="8b105-721">**FX_SUCCESS** (0x00) başarılı uzun ad al</span><span class="sxs-lookup"><span data-stu-id="8b105-721">**FX_SUCCESS** (0x00) Successful long name get</span></span>
- <span data-ttu-id="8b105-722">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b105-722">**FX_NOT_FOUND** (0x04) Short name was not found</span></span>
- <span data-ttu-id="8b105-723">**FX_IO_ERROR** (0x90) sürücü g/ç hatası</span><span class="sxs-lookup"><span data-stu-id="8b105-723">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="8b105-724">**FX_MEDIA_INVALID** (0x02) geçersiz medya</span><span class="sxs-lookup"><span data-stu-id="8b105-724">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="8b105-725">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-725">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-726">**FX_SECTOR_INVALID** (0x89) geçersiz kesim</span><span class="sxs-lookup"><span data-stu-id="8b105-726">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="8b105-727">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-727">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="8b105-728">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-728">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-729">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-729">**FX_PTR_ERROR** (0x18) Invalid media or name pointer</span></span>
- <span data-ttu-id="8b105-730">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil</span><span class="sxs-lookup"><span data-stu-id="8b105-730">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-731">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-731">Allowed From</span></span>

<span data-ttu-id="8b105-732">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-733">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-733">Example</span></span>

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-734">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-734">See Also</span></span>

- <span data-ttu-id="8b105-735">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-735">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-736">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-736">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-737">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-737">fx_directory_create</span></span>
- <span data-ttu-id="8b105-738">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-738">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-739">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-739">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-740">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-740">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-741">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-741">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-742">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-742">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-743">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-743">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-744">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-744">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-745">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-745">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-746">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-746">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-747">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-747">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-748">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-748">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-749">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-749">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-750">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-750">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-751">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-751">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-752">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-752">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-753">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-753">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-754">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-754">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get_extended"></a><span data-ttu-id="8b105-755">fx_directory_long_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8b105-755">fx_directory_long_name_get_extended</span></span>

<span data-ttu-id="8b105-756">Kısa adından uzun ad alır</span><span class="sxs-lookup"><span data-stu-id="8b105-756">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-757">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-757">Prototype</span></span>

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="8b105-758">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-758">Description</span></span>

<span data-ttu-id="8b105-759">Bu hizmet, sağlanan kısa (8,3 biçim) adıyla ilişkili uzun adı (varsa) alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-759">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="8b105-760">Kısa ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-760">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-761">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-761">Input Parameters</span></span>

- <span data-ttu-id="8b105-762">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-762">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-763">**short_name**: kaynak kısa adı işaretçisi (8,3 biçim).</span><span class="sxs-lookup"><span data-stu-id="8b105-763">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="8b105-764">**long_name**: uzun ad için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-764">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="8b105-765">Uzun bir ad yoksa, kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-765">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="8b105-766">Note: uzun ad hedefi **FX_MAX_LONG_NAME_LEN** karakter tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-766">Note: Destination for the long name must be large enough to hold **FX_MAX_LONG_NAME_LEN** characters.</span></span>
- <span data-ttu-id="8b105-767">**long_file_name_buffer_length**: uzun ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-767">**long_file_name_buffer_length**: Length of the long name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-768">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-768">Return Values</span></span>

- <span data-ttu-id="8b105-769">**FX_SUCCESS** (0x00) başarılı uzun ad al.</span><span class="sxs-lookup"><span data-stu-id="8b105-769">**FX_SUCCESS** (0x00) Successful long name get.</span></span>
- <span data-ttu-id="8b105-770">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-770">**FX_NOT_FOUND** (0x04) Short name was not found.</span></span>
- <span data-ttu-id="8b105-771">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-771">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-772">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-772">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-773">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-773">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-774">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-774">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-775">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-775">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-776">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-776">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8b105-777">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-777">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8b105-778">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-778">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-779">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-779">Allowed From</span></span>

<span data-ttu-id="8b105-780">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-780">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-781">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-781">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name), sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-782">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-782">See Also</span></span>

- <span data-ttu-id="8b105-783">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-783">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-784">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-784">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-785">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-785">fx_directory_create</span></span>
- <span data-ttu-id="8b105-786">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-786">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-787">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-787">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-788">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-788">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-789">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-789">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-790">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-790">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-791">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-791">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-792">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-792">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-793">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-793">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-794">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-794">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-795">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-795">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-796">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-796">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-797">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-797">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-798">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-798">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-799">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-799">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-800">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-800">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-801">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-801">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-802">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-802">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_name_test"></a><span data-ttu-id="8b105-803">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-803">fx_directory_name_test</span></span>

<span data-ttu-id="8b105-804">Dizin için testler</span><span class="sxs-lookup"><span data-stu-id="8b105-804">Tests for directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-805">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-805">Prototype</span></span>

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="8b105-806">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-806">Description</span></span>

<span data-ttu-id="8b105-807">Bu hizmet, belirtilen adın bir dizin olup olmadığını sınar.</span><span class="sxs-lookup"><span data-stu-id="8b105-807">This service tests whether or not the supplied name is a directory.</span></span> <span data-ttu-id="8b105-808">Öyleyse, bir FX_SUCCESS döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-808">If so, a FX_SUCCESS is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-809">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-809">Input Parameters</span></span>

- <span data-ttu-id="8b105-810">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-810">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-811">**directory_name**: Dizin girişinin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-811">**directory_name**: Pointer to name of the directory entry.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-812">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-812">Return Values</span></span>

- <span data-ttu-id="8b105-813">**FX_SUCCESS** (0x00) sağlanan ad bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="8b105-813">**FX_SUCCESS** (0x00) Supplied name is a directory.</span></span>
- <span data-ttu-id="8b105-814">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil</span><span class="sxs-lookup"><span data-stu-id="8b105-814">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="8b105-815">**FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-815">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="8b105-816">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil</span><span class="sxs-lookup"><span data-stu-id="8b105-816">**FX_NOT_DIRECTORY** (0x0E)  Entry is not a directory</span></span>
- <span data-ttu-id="8b105-817">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-817">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-818">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-818">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-819">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-819">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-820">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-820">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-821">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-821">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-822">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-822">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8b105-823">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-823">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8b105-824">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-824">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-825">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-825">Allowed From</span></span>

<span data-ttu-id="8b105-826">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-826">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-827">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-827">Example</span></span>

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-828">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-828">See Also</span></span>

- <span data-ttu-id="8b105-829">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-829">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-830">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-830">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-831">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-831">fx_directory_create</span></span>
- <span data-ttu-id="8b105-832">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-832">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-833">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-833">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-834">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-834">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-835">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-835">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-836">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-836">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-837">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-837">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-838">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-838">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-839">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-839">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-840">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-840">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-841">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-841">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-842">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-842">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-843">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-843">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-844">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-844">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-845">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-845">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-846">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-846">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-847">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-847">fx_unicode_directory_create</span></span>

## <a name="fx_directory_next_entry_find"></a><span data-ttu-id="8b105-848">fx_directory_next_entry_find:</span><span class="sxs-lookup"><span data-stu-id="8b105-848">fx_directory_next_entry_find:</span></span>

<span data-ttu-id="8b105-849">Sonraki dizin girişini seçer</span><span class="sxs-lookup"><span data-stu-id="8b105-849">Picks up next directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-850">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-850">Prototype</span></span>

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="8b105-851">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-851">Description</span></span>

<span data-ttu-id="8b105-852">Bu hizmet, geçerli varsayılan dizindeki bir sonraki giriş adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b105-852">This service returns the next entry name in the current default directory.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-853">*Yerel olmayan bir yol kullanılıyorsa, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek için de önemlidir (bir ThreadX semaforu veya iş parçacığı öncelik düzeyiyle). Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-853">*If using a non-local path, it is also important to prevent (with a ThreadX semaphore or thread priority level) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-854">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-854">Input Parameters</span></span>

- <span data-ttu-id="8b105-855">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-855">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-856">**return_entry_name**: varsayılan dizindeki bir sonraki giriş adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-856">**return_entry_name**: Pointer to destination for the next entry name in the default directory.</span></span> <span data-ttu-id="8b105-857">Bu işaretçinin işaret ettiği arabellek, **_FX_MAX_LONG_NAME_LEN_** tarafından tanımlanan en büyük FileX adı boyutunu tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-857">The buffer this pointer points to must be large enough to hold the maximum size of FileX name, defined by **_FX_MAX_LONG_NAME_LEN_**.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-858">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-858">Return Values</span></span>

- <span data-ttu-id="8b105-859">**FX_SUCCESS** (0x00) başarılı bir sonraki giriş bul</span><span class="sxs-lookup"><span data-stu-id="8b105-859">**FX_SUCCESS** (0x00) Successful next entry find</span></span>
- <span data-ttu-id="8b105-860">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-860">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-861">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-861">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="8b105-862">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-862">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-863">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-863">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-864">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-864">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-865">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-865">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-866">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-866">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-867">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-867">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-868">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-868">**FX_CALLER_ERROR** (0x20)     Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-869">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-869">Allowed From</span></span>

<span data-ttu-id="8b105-870">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-871">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-871">Example</span></span>

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a><span data-ttu-id="8b105-872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-872">See Also</span></span>

- <span data-ttu-id="8b105-873">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-873">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-874">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-874">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-875">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-875">fx_directory_create</span></span>
- <span data-ttu-id="8b105-876">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-876">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-877">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-877">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-878">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-878">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-879">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-879">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-880">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-880">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-881">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-881">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-882">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-882">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-883">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-883">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-884">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-884">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-885">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-885">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-886">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-886">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-887">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-887">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-888">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-888">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-889">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-889">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-890">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-890">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-891">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-891">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-892">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-892">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="8b105-893">fx_directory_next_full_entry_find:</span><span class="sxs-lookup"><span data-stu-id="8b105-893">fx_directory_next_full_entry_find:</span></span>

<span data-ttu-id="8b105-894">Tam bilgi içeren bir sonraki dizin girişini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-894">Gets next directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-895">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-895">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="8b105-896">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-896">Description</span></span>

<span data-ttu-id="8b105-897">Bu hizmet, varsayılan dizindeki bir sonraki giriş adını alır ve belirtilen hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8b105-897">This service retrieves the next entry name in the default directory and copies it to the specified destination.</span></span> <span data-ttu-id="8b105-898">Ayrıca, ek giriş parametreleriyle belirtilen girdi hakkında tam bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b105-898">It also returns full information about the entry as specified by the additional input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-899">\* Belirtilen hedef, \* \* \* FX_MAX_LONG_NAME_LEN \* \* \* \* ile tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır</span><span class="sxs-lookup"><span data-stu-id="8b105-899">\*The specified destination must be large enough to hold the maximum sized FileX name, as defined by \*\*\*FX_MAX_LONG_NAME_LEN\*\*\*\*</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-900">*Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-900">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-901">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-901">Input Parameters</span></span>

- <span data-ttu-id="8b105-902">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-902">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-903">**directory_name**: bir dizin girişi adı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-903">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="8b105-904">En az **FX_MAX_LONG_NAME_LEN** kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-904">Must be at least as big as **FX_MAX_LONG_NAME_LEN**.</span></span>
- <span data-ttu-id="8b105-905">**öznitelikler**: null olmayan, girişin özniteliklerinin yerleştirileceği hedefe yönelik işaretçi. Öznitelikler, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8b105-905">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8b105-906">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-906">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="8b105-907">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-907">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="8b105-908">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="8b105-908">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="8b105-909">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="8b105-909">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="8b105-910">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="8b105-910">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="8b105-911">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="8b105-911">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="8b105-912">**Boyut**: null olmayan, girdinin bayt cinsinden boyutu için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-912">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="8b105-913">**ay**: null olmayan, girişin değiştirilme ayı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-913">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="8b105-914">**yıl**: null olmayan, girişin değiştirilme yılından hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-914">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="8b105-915">**gün**: null olmayan, girişin değiştirilme günü için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-915">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="8b105-916">**saat**: null olmayan, girişin değiştirilme saati için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-916">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="8b105-917">**dakika**: null olmayan, girişin değiştirilme dakikası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-917">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="8b105-918">**ikinci**: null olmayan, girişin değiştirilme saniyesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-918">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-919">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-919">Return Values</span></span>

- <span data-ttu-id="8b105-920">**FX_SUCCESS** (0x00) başarılı Dizin sonraki giriş bul.</span><span class="sxs-lookup"><span data-stu-id="8b105-920">**FX_SUCCESS** (0x00) Successful directory next entry find.</span></span>
- <span data-ttu-id="8b105-921">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-921">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-922">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-922">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="8b105-923">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-923">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-924">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-924">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-925">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-925">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-926">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-926">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-927">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-927">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8b105-928">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-928">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-929">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya tüm GIRIŞ parametreleri null.</span><span class="sxs-lookup"><span data-stu-id="8b105-929">**FX_PTR_ERROR** (0x18) Invalid media pointer or all input parameters are NULL.</span></span>
- <span data-ttu-id="8b105-930">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-930">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-931">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-931">Allowed From</span></span>

<span data-ttu-id="8b105-932">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-932">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-933">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-933">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-934">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-934">See Also</span></span>

- <span data-ttu-id="8b105-935">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-935">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-936">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-936">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-937">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-937">fx_directory_create</span></span>
- <span data-ttu-id="8b105-938">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-938">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-939">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-939">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-940">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-940">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-941">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-941">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-942">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-942">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-943">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-943">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-944">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-944">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-945">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-945">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-946">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-946">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-947">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-947">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-948">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-948">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-949">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-949">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-950">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-950">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-951">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-951">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-952">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-952">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-953">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-953">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-954">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-954">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_rename"></a><span data-ttu-id="8b105-955">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-955">fx_directory_rename</span></span>

<span data-ttu-id="8b105-956">Dizini yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="8b105-956">Renames directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-957">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-957">Prototype</span></span>

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a><span data-ttu-id="8b105-958">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-958">Description</span></span>

<span data-ttu-id="8b105-959">Bu hizmet dizin adını belirtilen yeni dizin adıyla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-959">This service changes the directory name to the specified new directory name.</span></span> <span data-ttu-id="8b105-960">Yeniden adlandırma işlemi, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-960">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="8b105-961">Yeni Dizin adında bir yol belirtilmişse, yeniden adlandırılan dizin, belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="8b105-961">If a path is specified in the new directory name, the renamed directory is effectively moved to the specified path.</span></span> <span data-ttu-id="8b105-962">Yol belirtilmemişse, yeniden adlandırılan dizin geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-962">If no path is specified, the renamed directory is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-963">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-963">Input Parameters</span></span>

- <span data-ttu-id="8b105-964">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-964">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-965">**old_directory_name**: geçerli dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-965">**old_directory_name**: Pointer to current directory name.</span></span>
- <span data-ttu-id="8b105-966">**new_directory_name**: yeni dizin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-966">**new_directory_name**: Pointer to new directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-967">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-967">Return Values</span></span>

- <span data-ttu-id="8b105-968">**FX_SUCCESS** (0x00) başarılı dizin yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="8b105-968">**FX_SUCCESS** (0x00) Successful directory rename.</span></span>
- <span data-ttu-id="8b105-969">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-969">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-970">**FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-970">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="8b105-971">**FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-971">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory.</span></span>
- <span data-ttu-id="8b105-972">**FX_INVALID_NAME** (0x0C) yeni dizin adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-972">**FX_INVALID_NAME** (0x0C) New directory name is invalid.</span></span>
- <span data-ttu-id="8b105-973">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-973">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-974">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-974">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-975">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-975">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-976">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-976">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-977">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-977">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-978">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-978">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8b105-979">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-979">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-980">**FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-980">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="8b105-981">**FX_INVALID_PATH** (0x0D) dizin adıyla belirtilen yol geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-981">**FX_INVALID_PATH** (0x0D) Invalid path supplied with directory name.</span></span>
- <span data-ttu-id="8b105-982">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin zaten oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8b105-982">**FX_ALREADY_CREATED** (0x0B) Specified directory was already created.</span></span>
- <span data-ttu-id="8b105-983">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-983">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-984">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-984">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-985">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-985">Allowed From</span></span>

<span data-ttu-id="8b105-986">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-986">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-987">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-987">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a><span data-ttu-id="8b105-988">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-988">See Also</span></span>

- <span data-ttu-id="8b105-989">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-989">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-990">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-990">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-991">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-991">fx_directory_create</span></span>
- <span data-ttu-id="8b105-992">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-992">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-993">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-993">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-994">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-994">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-995">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-995">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-996">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-996">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-997">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-997">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-998">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-998">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-999">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-999">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-1000">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-1000">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-1001">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1001">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-1002">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1002">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-1003">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-1003">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-1004">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1004">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-1005">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1005">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-1006">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1006">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-1007">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1007">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-1008">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1008">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get"></a><span data-ttu-id="8b105-1009">fx_directory_short_name_get:</span><span class="sxs-lookup"><span data-stu-id="8b105-1009">fx_directory_short_name_get:</span></span>

<span data-ttu-id="8b105-1010">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="8b105-1010">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1011">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1011">Prototype</span></span>

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="8b105-1012">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1012">Description</span></span>

<span data-ttu-id="8b105-1013">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1013">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="8b105-1014">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1014">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1015">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1015">Input Parameters</span></span>

- <span data-ttu-id="8b105-1016">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1016">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-1017">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1017">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="8b105-1018">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="8b105-1018">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="8b105-1019">Kısa ad hedefinin 14 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b105-1019">Note that the destination for the short name must be large enough to hold 14 characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1020">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1020">Return Values</span></span>

- <span data-ttu-id="8b105-1021">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="8b105-1021">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="8b105-1022">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1022">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="8b105-1023">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1023">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1024">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1024">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1025">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1025">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1026">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1026">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1027">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1027">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1028">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1028">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1029">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1029">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-1030">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1030">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8b105-1031">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1031">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1032">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1032">Allowed From</span></span>

<span data-ttu-id="8b105-1033">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1033">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1034">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1034">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1035">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1035">See Also</span></span>

- <span data-ttu-id="8b105-1036">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1036">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-1037">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1037">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-1038">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1038">fx_directory_create</span></span>
- <span data-ttu-id="8b105-1039">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1039">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-1040">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1040">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-1041">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1041">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-1042">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1042">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-1043">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1043">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-1044">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1044">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-1045">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-1045">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-1046">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1046">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-1047">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-1047">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-1048">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1048">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-1049">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1049">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-1050">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-1050">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-1051">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1051">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-1052">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1052">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-1053">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1053">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-1054">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1054">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-1055">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1055">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get_extended"></a><span data-ttu-id="8b105-1056">fx_directory_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8b105-1056">fx_directory_short_name_get_extended</span></span>

<span data-ttu-id="8b105-1057">Uzun bir ada kısa ad alır</span><span class="sxs-lookup"><span data-stu-id="8b105-1057">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1058">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1058">Prototype</span></span>

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a><span data-ttu-id="8b105-1059">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1059">Description</span></span>

<span data-ttu-id="8b105-1060">Bu hizmet, sağlanan uzun adla ilişkili kısa (8,3 biçim) adı alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1060">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="8b105-1061">Uzun ad, bir dosya adı ya da dizin adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1061">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1062">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1062">Input Parameters</span></span>

- <span data-ttu-id="8b105-1063">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1063">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-1064">**long_name**: kaynak Long Name işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1064">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="8b105-1065">**short_name**: hedef kısa adı işaretçisi (8,3 biçimi).</span><span class="sxs-lookup"><span data-stu-id="8b105-1065">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="8b105-1066">Note: kısa ad hedefi 14 karakter tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1066">Note: Destination for the short name must be large enough to hold 14 characters.</span></span>
- <span data-ttu-id="8b105-1067">**short_file_name_length**: kısa ad arabelleğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-1067">**short_file_name_length**: Length of short name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1068">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1068">Return Values</span></span>

- <span data-ttu-id="8b105-1069">**FX_SUCCESS** (0x00) başarılı kısa ad al.</span><span class="sxs-lookup"><span data-stu-id="8b105-1069">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="8b105-1070">**FX_NOT_FOUND** (0x04) uzun ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1070">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="8b105-1071">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1071">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1072">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1072">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1073">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1074">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1075">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1075">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1076">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1076">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1077">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1077">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-1078">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1078">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8b105-1079">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1079">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1080">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1080">Allowed From</span></span>

<span data-ttu-id="8b105-1081">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1081">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1082">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1082">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1083">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1083">See Also</span></span>

- <span data-ttu-id="8b105-1084">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1084">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-1085">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1085">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-1086">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1086">fx_directory_create</span></span>
- <span data-ttu-id="8b105-1087">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1087">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-1088">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1088">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-1089">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1089">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-1090">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1090">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-1091">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1091">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-1092">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1092">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-1093">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-1093">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-1094">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1094">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-1095">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-1095">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-1096">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1096">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-1097">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1097">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-1098">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-1098">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-1099">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1099">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-1100">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-1100">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-1101">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1101">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-1102">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1102">fx_unicode_directory_create</span></span>
- <span data-ttu-id="8b105-1103">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1103">fx_unicode_directory_rename</span></span>

## <a name="fx_fault_tolerant_enable"></a><span data-ttu-id="8b105-1104">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-1104">fx_fault_tolerant_enable</span></span>

<span data-ttu-id="8b105-1105">Hataya dayanıklı hizmeti sunar</span><span class="sxs-lookup"><span data-stu-id="8b105-1105">Enables the fault tolerant service</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1106">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1106">Prototype</span></span>

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a><span data-ttu-id="8b105-1107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1107">Description</span></span>

<span data-ttu-id="8b105-1108">Bu hizmet, hataya dayanıklı modüle izin vermez.</span><span class="sxs-lookup"><span data-stu-id="8b105-1108">This service enables the fault tolerant module.</span></span> <span data-ttu-id="8b105-1109">Başlamadan sonra, hataya dayanıklı modül dosya sisteminin FileX hataya dayanıklı koruma altında olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1109">Upon starting, the fault tolerant module detects whether or not the file system is under FileX fault tolerant protection.</span></span> <span data-ttu-id="8b105-1110">Aksi takdirde, hizmet, dosya sistemi işlemlerinde günlükleri depolamak için dosya sisteminde kullanılabilir kesimleri bulur.</span><span class="sxs-lookup"><span data-stu-id="8b105-1110">If it is not, the service finds available sectors on the file system to store logs on file system transactions.</span></span> <span data-ttu-id="8b105-1111">Dosya sistemi, FileX hataya dayanıklı koruma altındaysa, bütünlüğünü sürdürmek için günlükleri dosya sistemine uygular.</span><span class="sxs-lookup"><span data-stu-id="8b105-1111">If the file system is under FileX fault tolerant protection, it applies the logs to the file system to maintain its integrity.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1112">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1112">Input Parameters</span></span>

- <span data-ttu-id="8b105-1113">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1113">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-1114">**memory_ptr**: hataya dayanıklı modül tarafından karalama belleği olarak kullanılan bir bellek bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1114">**memory_ptr**: Pointer to a block of memory used by the fault tolerant module as scratch memory.</span></span>
- <span data-ttu-id="8b105-1115">**memory_size**: karalama belleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-1115">**memory_size**: The size of the scratch memory.</span></span> <span data-ttu-id="8b105-1116">Hata toleranslı 'nin düzgün çalışması için, karalama belleği boyutu en az 3072 bayt olur ve sektör boyutunun katı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1116">In order for fault tolerant to work properly, the scratch memory size shall be at least 3072 bytes,- and must be multiple of sector size.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1117">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1117">Return Values</span></span>

- <span data-ttu-id="8b105-1118">**FX_SUCCESS** (0x00) hata dayanıklılığını başarıyla etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1118">**FX_SUCCESS** (0x00) Successfully enabled fault tolerant.</span></span>
- <span data-ttu-id="8b105-1119">**FX_NOT_ENOUGH_MEMORY** (0x91) bellek boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="8b105-1119">**FX_NOT_ENOUGH_MEMORY** (0x91)    memory size too small.</span></span>
- <span data-ttu-id="8b105-1120">**FX_BOOT_ERROR** (0x01) önyükleme kesimi hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1120">**FX_BOOT_ERROR** (0x01) Boot sector error.</span></span>
- <span data-ttu-id="8b105-1121">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1121">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1122">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1122">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="8b105-1123">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1123">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8b105-1124">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="8b105-1124">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="8b105-1125">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1125">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1126">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1126">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-1127">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1127">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1128">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1128">Allowed From</span></span>

<span data-ttu-id="8b105-1129">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1129">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1130">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1130">Example</span></span>

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a><span data-ttu-id="8b105-1131">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1131">See Also</span></span>

- <span data-ttu-id="8b105-1132">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-1132">fx_system_initialize</span></span>
- <span data-ttu-id="8b105-1133">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-1133">fx_media_abort</span></span>
- <span data-ttu-id="8b105-1134">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-1134">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-1135">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-1135">fx_media_check</span></span>
- <span data-ttu-id="8b105-1136">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1136">fx_media_close</span></span>
- <span data-ttu-id="8b105-1137">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1137">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-1138">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-1138">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-1139">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-1139">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-1140">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-1140">fx_media_flush</span></span>
- <span data-ttu-id="8b105-1141">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-1141">fx_media_format</span></span>
- <span data-ttu-id="8b105-1142">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1142">fx_media_open</span></span>
- <span data-ttu-id="8b105-1143">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1143">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-1144">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1144">fx_media_read</span></span>
- <span data-ttu-id="8b105-1145">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-1145">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-1146">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1146">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-1147">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1147">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-1148">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1148">fx_media_write</span></span>

## <a name="fx_file_allocate"></a><span data-ttu-id="8b105-1149">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1149">fx_file_allocate</span></span>

<span data-ttu-id="8b105-1150">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="8b105-1150">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1151">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1151">Prototype</span></span>

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="8b105-1152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1152">Description</span></span>

<span data-ttu-id="8b105-1153">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1153">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8b105-1154">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8b105-1154">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8b105-1155">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1155">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="8b105-1156">4 GB 'den daha fazla alan ayırmak için, uygulama Service *fx_file_extended_allocate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1156">To allocate space beyond 4GB, application shall use the service *fx_file_extended_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1157">Input Parameters</span></span>

- <span data-ttu-id="8b105-1158">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1158">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-1159">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1159">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1160">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1160">Return Values</span></span>

- <span data-ttu-id="8b105-1161">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="8b105-1161">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="8b105-1162">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1162">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-1163">**FX_FAT_READ_ERROR** (0x03), FAT girişini okuyamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1163">**FX_FAT_READ_ERROR** (0x03) Failed to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1164">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1164">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1165">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1165">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-1166">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1166">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="8b105-1167">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1167">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8b105-1168">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="8b105-1168">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="8b105-1169">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1169">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1170">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1170">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1171">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1171">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-1172">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1172">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1173">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1173">Allowed From</span></span>

<span data-ttu-id="8b105-1174">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1175">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1175">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1176">See Also</span></span>

- <span data-ttu-id="8b105-1177">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1177">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1178">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1178">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1179">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1179">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1180">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1180">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="8b105-1181">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1181">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1182">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1182">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1183">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1183">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1184">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1184">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1185">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1185">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1186">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1186">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1187">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1187">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1188">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1188">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1189">fx_file_open fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1189">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="8b105-1190">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1190">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1191">fx_file_rename fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1191">fx_file_rename- fx_file_seek</span></span>
- <span data-ttu-id="8b105-1192">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1192">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1193">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1193">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1194">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1194">fx_file_write</span></span>
- <span data-ttu-id="8b105-1195">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1195">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1196">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1196">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1197">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1197">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1198">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1198">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1199">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1199">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_read"></a><span data-ttu-id="8b105-1200">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1200">fx_file_attributes_read</span></span>

<span data-ttu-id="8b105-1201">Dosya özniteliklerini okur</span><span class="sxs-lookup"><span data-stu-id="8b105-1201">Reads file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1202">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1202">Prototype</span></span>

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-1203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1203">Description</span></span>

<span data-ttu-id="8b105-1204">Bu hizmet, dosyanın özniteliklerini belirtilen medyadan okur.</span><span class="sxs-lookup"><span data-stu-id="8b105-1204">This service reads the file's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1205">Input Parameters</span></span>

- <span data-ttu-id="8b105-1206">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1206">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-1207">**file_name**: istenen dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-1207">**file_name**: Pointer to the name of the requested file (directory path is optional).</span></span>
- <span data-ttu-id="8b105-1208">**attributes_ptr**: dosyaya yerleştirilecek özniteliklerin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1208">**attributes_ptr**: Pointer to the destination for the file's attributes to be placed.</span></span> <span data-ttu-id="8b105-1209">Dosya öznitelikleri, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:</span><span class="sxs-lookup"><span data-stu-id="8b105-1209">The file attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="8b105-1210">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-1210">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8b105-1211">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-1211">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8b105-1212">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8b105-1212">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8b105-1213">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="8b105-1213">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="8b105-1214">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="8b105-1214">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="8b105-1215">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8b105-1215">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1216">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1216">Return Values</span></span>

- <span data-ttu-id="8b105-1217">**FX_SUCCESS** (0x00) başarılı özniteliği okundu.</span><span class="sxs-lookup"><span data-stu-id="8b105-1217">**FX_SUCCESS** (0x00) Successful attribute read.</span></span>
- <span data-ttu-id="8b105-1218">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1218">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-1219">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1219">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="8b105-1220">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="8b105-1220">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="8b105-1221">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1221">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1222">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1222">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1223">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1223">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1224">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1224">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1225">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1225">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1226">**FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1226">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="8b105-1227">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1227">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1228">Allowed From</span></span>

<span data-ttu-id="8b105-1229">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1230">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1230">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a><span data-ttu-id="8b105-1231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1231">See Also</span></span>

- <span data-ttu-id="8b105-1232">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1232">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1233">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1233">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1234">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1234">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1235">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1235">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="8b105-1236">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1236">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1237">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1237">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1238">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1238">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1239">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1239">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1240">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1240">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1241">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1241">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1242">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1242">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1243">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1243">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1244">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1244">fx_file_open</span></span>
- <span data-ttu-id="8b105-1245">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1245">fx_file_read</span></span>
- <span data-ttu-id="8b105-1246">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1246">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1247">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1247">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1248">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1248">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1249">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1249">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1250">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1250">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1251">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1251">fx_file_write</span></span>
- <span data-ttu-id="8b105-1252">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1252">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1253">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1253">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1254">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1254">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1255">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1255">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1256">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1256">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_set"></a><span data-ttu-id="8b105-1257">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1257">fx_file_attributes_set</span></span>

<span data-ttu-id="8b105-1258">Dosya özniteliklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-1258">Sets file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1259">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1259">Prototype</span></span>

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a><span data-ttu-id="8b105-1260">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1260">Description</span></span>

<span data-ttu-id="8b105-1261">Bu hizmet, dosyanın özniteliklerini çağıran tarafından belirtilen olanlarla ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1261">This service sets the file's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-1262">*Uygulamanın yalnızca bu hizmetle birlikte dosyanın özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlamaya yönelik her türlü girişim bir hataya neden olur.*</span><span class="sxs-lookup"><span data-stu-id="8b105-1262">*The application is only allowed to modify a subset of the file's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1263">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1263">Input Parameters</span></span>

- <span data-ttu-id="8b105-1264">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1264">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-1265">**file_name**: istenen dosyanın adı işaretçisi \* \* (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-1265">**file_name**: Pointer to the name of the requested file\*\* (directory path is optional).</span></span>
- <span data-ttu-id="8b105-1266">**öznitelikler**: dosyanın yeni öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="8b105-1266">**attributes**: The new attributes for the file.</span></span> <span data-ttu-id="8b105-1267">Geçerli dosya öznitelikleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8b105-1267">The valid file attributes are defined as follows:</span></span>
  - <span data-ttu-id="8b105-1268">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-1268">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="8b105-1269">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-1269">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="8b105-1270">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="8b105-1270">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="8b105-1271">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="8b105-1271">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1272">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1272">Return Values</span></span>

- <span data-ttu-id="8b105-1273">**FX_SUCCESS** (0x00) başarılı öznitelik kümesi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1273">**FX_SUCCESS** (0x00) Successful attribute set.</span></span>
- <span data-ttu-id="8b105-1274">**FX_ACCESS_ERROR** (0x06) dosyası açık ve öznitelikleri ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1274">**FX_ACCESS_ERROR** (0x06) File is open and cannot have its attributes set.</span></span>
- <span data-ttu-id="8b105-1275">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1275">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1276">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1276">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1277">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-1278">**FX_NO_MORE_ENTRIES** (0x0F) FAT tablosunda veya exFAT Cluster eşlemesinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1278">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in the FAT table or exFAT cluster map.</span></span>
- <span data-ttu-id="8b105-1279">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1279">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8b105-1280">**FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1280">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="8b105-1281">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="8b105-1281">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="8b105-1282">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz</span><span class="sxs-lookup"><span data-stu-id="8b105-1282">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="8b105-1283">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1283">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1284">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1284">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1285">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1285">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-1286">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1286">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-1287">**FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1287">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="8b105-1288">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1288">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1289">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1289">Allowed From</span></span>

<span data-ttu-id="8b105-1290">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1290">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1291">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1291">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a><span data-ttu-id="8b105-1292">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1292">See Also</span></span>

- <span data-ttu-id="8b105-1293">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1293">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1294">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1294">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1295">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1295">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1296">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1296">fx_file_close</span></span>
- <span data-ttu-id="8b105-1297">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1297">fx_file_create</span></span>
- <span data-ttu-id="8b105-1298">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1298">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1299">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1299">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1300">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1300">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1301">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1301">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1302">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1302">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1303">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1303">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1304">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1304">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1305">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1305">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1306">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1306">fx_file_open</span></span>
- <span data-ttu-id="8b105-1307">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1307">fx_file_read</span></span>
- <span data-ttu-id="8b105-1308">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1308">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1309">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1309">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1310">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1310">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1311">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1311">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1312">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1312">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1313">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1313">fx_file_write</span></span>
- <span data-ttu-id="8b105-1314">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1314">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1315">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1315">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1316">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1316">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1317">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1317">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1318">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1318">fx_unicode_short_name_get</span></span>

## <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="8b105-1319">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1319">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="8b105-1320">Bir dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="8b105-1320">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1321">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1321">Prototype</span></span>

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="8b105-1322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1322">Description</span></span>

<span data-ttu-id="8b105-1323">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1323">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8b105-1324">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8b105-1324">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8b105-1325">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1325">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="8b105-1326">Medyada yeterli sayıda ardışık küme yoksa, bu hizmet birbirini izleyen en büyük küme bloğunu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1326">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="8b105-1327">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-1327">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="8b105-1328">4 GB 'den daha fazla alan ayırmak için, uygulama Service *fx_file_extended_best_effort_allocate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1328">To allocate space beyond 4GB, application shall use the service *fx_file_extended_best_effort_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1329">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1329">Input Parameters</span></span>

- <span data-ttu-id="8b105-1330">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1330">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-1331">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1331">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1332">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1332">Return Values</span></span>

- <span data-ttu-id="8b105-1333">**FX_SUCCESS** (0x00) başarılı en iyi çaba dosya ayırması.</span><span class="sxs-lookup"><span data-stu-id="8b105-1333">**FX_SUCCESS** (0x00) Successful best-effort file allocation.</span></span>
- <span data-ttu-id="8b105-1334">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1334">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-1335">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1335">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-1336">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1336">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8b105-1337">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1337">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1338">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1338">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1339">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1339">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1340">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1340">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1341">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1341">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1342">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1342">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1343">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi veya hedef.</span><span class="sxs-lookup"><span data-stu-id="8b105-1343">**FX_PTR_ERROR** (0x18) Invalid file pointer or destination.</span></span>
- <span data-ttu-id="8b105-1344">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1344">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1345">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1345">Allowed From</span></span>

<span data-ttu-id="8b105-1346">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1346">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1347">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1347">Example</span></span>

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a><span data-ttu-id="8b105-1348">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1348">See Also</span></span>

- <span data-ttu-id="8b105-1349">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1349">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1350">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1350">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1351">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1351">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1352">fx_file_close</span></span>
- <span data-ttu-id="8b105-1353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1353">fx_file_create</span></span>
- <span data-ttu-id="8b105-1354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1354">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1355">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1359">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1362">fx_file_open</span></span>
- <span data-ttu-id="8b105-1363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1363">fx_file_read</span></span>
- <span data-ttu-id="8b105-1364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1364">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1365">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1366">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1367">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1368">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1369">fx_file_write</span></span>
- <span data-ttu-id="8b105-1370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1371">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1371">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1372">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1372">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1373">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1373">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1374">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1374">fx_unicode_short_name_get</span></span>

## <a name="fx_file_close"></a><span data-ttu-id="8b105-1375">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1375">fx_file_close</span></span>

<span data-ttu-id="8b105-1376">Dosyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="8b105-1376">Closes file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1377">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1377">Prototype</span></span>

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-1378">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1378">Description</span></span>

<span data-ttu-id="8b105-1379">Bu hizmet, belirtilen dosyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1379">This service closes the specified file.</span></span> <span data-ttu-id="8b105-1380">Dosya yazmak için açıksa ve değiştirilmişse, bu hizmet Dizin girişini yeni boyut ve geçerli sistem saati ve tarihi ile güncelleştirerek dosya değiştirme işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1380">If the file was open for writing and if it was modified, this service completes the file modification process by updating its directory entry with the new size and the current system time and date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1381">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1381">Input Parameters</span></span>

- <span data-ttu-id="8b105-1382">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1382">**file_ptr**: Pointer to a previously opened file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1383">Return Values</span></span>

- <span data-ttu-id="8b105-1384">**FX_SUCCESS** (0x00) başarılı dosya kapatma.</span><span class="sxs-lookup"><span data-stu-id="8b105-1384">**FX_SUCCESS** (0x00) Successful file close.</span></span>
- <span data-ttu-id="8b105-1385">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1385">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8b105-1386">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1386">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1387">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1387">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1388">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1388">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1389">**FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1389">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="8b105-1390">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1390">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1391">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1391">Allowed From</span></span>

<span data-ttu-id="8b105-1392">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1392">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1393">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1393">Example</span></span>

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1394">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1394">See Also</span></span>

- <span data-ttu-id="8b105-1395">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1395">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1396">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1396">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1397">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1397">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1398">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1398">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1399">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1399">fx_file_create</span></span>
- <span data-ttu-id="8b105-1400">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1400">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1401">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1401">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1402">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1402">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1403">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1403">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1404">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1404">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1405">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1405">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1406">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1406">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1407">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1407">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1408">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1408">fx_file_open</span></span>
- <span data-ttu-id="8b105-1409">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1409">fx_file_read</span></span>
- <span data-ttu-id="8b105-1410">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1410">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1411">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1411">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1412">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1412">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1413">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1413">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1414">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1414">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1415">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1415">fx_file_write</span></span>
- <span data-ttu-id="8b105-1416">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1416">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1417">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1417">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1418">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1418">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1419">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1419">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1420">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1420">fx_unicode_short_name_get</span></span>

## <a name="fx_file_create"></a><span data-ttu-id="8b105-1421">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1421">fx_file_create</span></span>

<span data-ttu-id="8b105-1422">Dosya oluşturur</span><span class="sxs-lookup"><span data-stu-id="8b105-1422">Creates file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1423">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1423">Prototype</span></span>

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="8b105-1424">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1424">Description</span></span>

<span data-ttu-id="8b105-1425">Bu hizmet, belirtilen dosyayı varsayılan dizinde veya dosya adıyla sağlanan dizin yolunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b105-1425">This service creates the specified file in the default directory or in the directory path supplied with the file name.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-1426">*Bu hizmet, sıfır uzunluğunda bir dosya oluşturur, yani hiçbir küme ayrılmamış. Ayırma işlemi, sonraki dosya yazmaları üzerinde otomatik olarak gerçekleşir veya fx_file_allocate hizmeti veya 4 GB 'den daha fazla alan fx_file_extended_allocate daha önce yapılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-1426">*This service creates a file of zero length, i.e., no clusters allocated. Allocation will automatically take place on subsequent file writes or can be done in advance with the fx_file_allocate service or fx_file_extended_allocate for space beyond 4GB) service.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1427">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1427">Input Parameters</span></span>

- <span data-ttu-id="8b105-1428">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1428">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-1429">**file_name**: oluşturulacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-1429">**file_name**: Pointer to the name of the file to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1430">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1430">Return Values</span></span>

- <span data-ttu-id="8b105-1431">**FX_SUCCESS** (0x00) başarılı dosya oluştur.</span><span class="sxs-lookup"><span data-stu-id="8b105-1431">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="8b105-1432">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1432">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-1433">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya zaten oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8b105-1433">**FX_ALREADY_CREATED** (0x0B) Specified file was already created.</span></span>
- <span data-ttu-id="8b105-1434">**FX_NO_MORE_SPACE** (0x0A) kök dizinde başka girdi yok veya kullanılabilir daha fazla küme yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1434">**FX_NO_MORE_SPACE** (0x0A)    Either there are no more entries in the root directory or there are no more clusters available.</span></span>
- <span data-ttu-id="8b105-1435">**FX_INVALID_PATH** (0x0D) dosya adı ile geçersiz yol sağlandı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1435">**FX_INVALID_PATH** (0x0D) Invalid path supplied with file name.</span></span>
- <span data-ttu-id="8b105-1436">**FX_INVALID_NAME** (0x0C) dosya adı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1436">**FX_INVALID_NAME** (0x0C) File name is invalid.</span></span>
- <span data-ttu-id="8b105-1437">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1437">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1438">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1438">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1439">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1439">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1440">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1440">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1441">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1441">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1442">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1442">**FX_MEDIA_INVALID** (0x02)Invalid media.</span></span>
- <span data-ttu-id="8b105-1443">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1443">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1444">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1444">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8b105-1445">**FX_PTR_ERROR** (0x18) geçersiz medya veya dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1445">**FX_PTR_ERROR** (0x18) Invalid media or file name pointer.</span></span>
- <span data-ttu-id="8b105-1446">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1446">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1447">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1447">Allowed From</span></span>

<span data-ttu-id="8b105-1448">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1448">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1449">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1449">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1450">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1450">See Also</span></span>
- <span data-ttu-id="8b105-1451">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1451">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1452">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1452">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1453">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1453">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1454">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1454">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1455">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1455">fx_file_close</span></span>
- <span data-ttu-id="8b105-1456">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1456">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1457">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1457">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1458">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1458">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1459">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1459">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1460">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1460">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1461">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1461">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1462">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1462">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1463">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1463">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1464">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1464">fx_file_open</span></span>
- <span data-ttu-id="8b105-1465">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1465">fx_file_read</span></span>
- <span data-ttu-id="8b105-1466">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1466">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1467">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1467">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1468">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1468">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1469">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1469">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1470">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1470">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1471">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1471">fx_file_write</span></span>
- <span data-ttu-id="8b105-1472">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1472">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1473">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1473">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1474">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1474">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1475">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1475">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1476">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1476">fx_unicode_short_name_get</span></span>

## <a name="fx_file_date_time_set"></a><span data-ttu-id="8b105-1477">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1477">fx_file_date_time_set</span></span>

### <a name="sets-file-date-and-time"></a><span data-ttu-id="8b105-1478">Dosya tarih ve saatini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-1478">Sets file date and time</span></span>

<span data-ttu-id="8b105-1479">Dosya tarih ve saati ayarlanıyor</span><span class="sxs-lookup"><span data-stu-id="8b105-1479">Setting File Date and Time</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1480">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1480">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="8b105-1481">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1481">Description</span></span>

<span data-ttu-id="8b105-1482">Bu hizmet, belirtilen dosyanın tarih ve saatini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1482">This service sets the date and time of the specified file.</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a><span data-ttu-id="8b105-1483">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1483">Input Parameters</span></span>

- <span data-ttu-id="8b105-1484">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1484">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-1485">**file_name**: dosyanın adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1485">**file_name**: Pointer to name of the file.</span></span>
- <span data-ttu-id="8b105-1486">**yıl**: yılın değeri (1980-2107 dahil).</span><span class="sxs-lookup"><span data-stu-id="8b105-1486">**year**: Value of year (1980-2107 inclusive).</span></span>
- <span data-ttu-id="8b105-1487">**Month**: ayın değeri (1-12 dahil).</span><span class="sxs-lookup"><span data-stu-id="8b105-1487">**month**: Value of month (1-12 inclusive).</span></span>
- <span data-ttu-id="8b105-1488">**gün**: günün değeri (1-31 dahil).</span><span class="sxs-lookup"><span data-stu-id="8b105-1488">**day**: Value of day (1-31 inclusive).</span></span>
- <span data-ttu-id="8b105-1489">**saat**: Saat değeri (0-23 dahil).</span><span class="sxs-lookup"><span data-stu-id="8b105-1489">**hour**: Value of hour (0-23 inclusive).</span></span>
- <span data-ttu-id="8b105-1490">**Minute**: dakikalık değeri (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="8b105-1490">**minute**: Value of minute (0-59 inclusive).</span></span>
- <span data-ttu-id="8b105-1491">**ikinci**: ikinci değer (0-59 dahil).</span><span class="sxs-lookup"><span data-stu-id="8b105-1491">**second**: Value of second (0-59 inclusive).</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1492">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1492">Return Values</span></span>

- <span data-ttu-id="8b105-1493">**FX_SUCCESS** (0x00) başarılı tarih/saat kümesi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1493">**FX_SUCCESS** (0x00) Successful date/time set.</span></span>
- <span data-ttu-id="8b105-1494">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1494">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-1495">**FX_NOT_FOUND** (0x04) dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1495">**FX_NOT_FOUND** (0x04)    File was not found.</span></span>
- <span data-ttu-id="8b105-1496">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1496">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="8b105-1497">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1497">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1498">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1498">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1499">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1499">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1500">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1500">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="8b105-1501">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1501">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1502">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1502">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1503">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1503">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="8b105-1504">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1504">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="8b105-1505">**FX_INVALID_YEAR** (0x12) yıl geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1505">**FX_INVALID_YEAR** (0x12) Year is invalid.</span></span>
- <span data-ttu-id="8b105-1506">**FX_INVALID_MONTH** (0x13) ay geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1506">**FX_INVALID_MONTH** (0x13) Month is invalid.</span></span>
- <span data-ttu-id="8b105-1507">**FX_INVALID_DAY** (0x14) gün geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1507">**FX_INVALID_DAY** (0x14) Day is invalid.</span></span>
- <span data-ttu-id="8b105-1508">**FX_INVALID_HOUR** (0x15) saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1508">**FX_INVALID_HOUR** (0x15)    Hour is invalid.</span></span>
- <span data-ttu-id="8b105-1509">**FX_INVALID_MINUTE** (0x16) dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1509">**FX_INVALID_MINUTE** (0x16) Minute is invalid.</span></span>
- <span data-ttu-id="8b105-1510">**FX_INVALID_SECOND** (0x17) saniye geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1510">**FX_INVALID_SECOND** (0x17) Second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1511">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1511">Allowed From</span></span>

<span data-ttu-id="8b105-1512">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1512">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1513">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1513">Example</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a><span data-ttu-id="8b105-1514">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1514">See Also</span></span>

- <span data-ttu-id="8b105-1515">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1515">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1516">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1516">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1517">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1517">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1518">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1518">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1519">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1519">fx_file_close</span></span>
- <span data-ttu-id="8b105-1520">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1520">fx_file_create</span></span>
- <span data-ttu-id="8b105-1521">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1521">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1522">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1522">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1523">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1523">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1524">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1524">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1525">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1525">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1526">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1526">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1527">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1527">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1528">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1528">fx_file_open</span></span>
- <span data-ttu-id="8b105-1529">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1529">fx_file_read</span></span>
- <span data-ttu-id="8b105-1530">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1530">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1531">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1531">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1532">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1532">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1533">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1533">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1534">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1534">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1535">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1535">fx_file_write</span></span>
- <span data-ttu-id="8b105-1536">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1536">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1537">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1537">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1538">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1538">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1539">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1539">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1540">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1540">fx_unicode_short_name_get</span></span>

## <a name="fx_file_delete"></a><span data-ttu-id="8b105-1541">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1541">fx_file_delete</span></span>

### <a name="deletes-file"></a><span data-ttu-id="8b105-1542">Dosyayı siler</span><span class="sxs-lookup"><span data-stu-id="8b105-1542">Deletes file</span></span>

<span data-ttu-id="8b105-1543">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="8b105-1543">File Deletion</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1544">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1544">Prototype</span></span>

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="8b105-1545">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1545">Description</span></span>

<span data-ttu-id="8b105-1546">Bu hizmet, belirtilen dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="8b105-1546">This service deletes the specified file.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="8b105-1547">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1547">Input Parameters</span></span>

- <span data-ttu-id="8b105-1548">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1548">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-1549">**file_name**: Silinecek dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-1549">**file_name**: Pointer to the name of the file to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1550">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1550">Return Values</span></span>

- <span data-ttu-id="8b105-1551">**FX_SUCCESS** (0x00) başarılı dosya silme.</span><span class="sxs-lookup"><span data-stu-id="8b105-1551">**FX_SUCCESS** (0x00) Successful file delete.</span></span>
- <span data-ttu-id="8b105-1552">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1552">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-1553">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1553">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="8b105-1554">**FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1554">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="8b105-1555">**FX_ACCESS_ERROR** (0x06) belirtilen dosya şu anda açık.</span><span class="sxs-lookup"><span data-stu-id="8b105-1555">**FX_ACCESS_ERROR** (0x06) Specified file is currently open.</span></span>
- <span data-ttu-id="8b105-1556">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1556">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1557">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1557">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1558">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1558">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1559">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1559">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1560">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1560">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1561">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1561">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1562">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1562">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1563">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1563">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-1564">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1564">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-1565">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1565">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1566">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1566">Allowed From</span></span>

<span data-ttu-id="8b105-1567">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1568">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1568">Example</span></span>

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1569">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1569">See Also</span></span>

- <span data-ttu-id="8b105-1570">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1570">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1571">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1571">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1572">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1572">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1573">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1573">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1574">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1574">fx_file_close</span></span>
- <span data-ttu-id="8b105-1575">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1575">fx_file_create</span></span>
- <span data-ttu-id="8b105-1576">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1576">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1577">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1577">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1578">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1578">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1579">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1579">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1580">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1580">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1581">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1581">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1582">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1582">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1583">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1583">fx_file_open</span></span>
- <span data-ttu-id="8b105-1584">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1584">fx_file_read</span></span>
- <span data-ttu-id="8b105-1585">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1585">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1586">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1586">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1587">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1587">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1588">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1588">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1589">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1589">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1590">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1590">fx_file_write</span></span>
- <span data-ttu-id="8b105-1591">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1591">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1592">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1592">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1593">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1593">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1594">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1594">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1595">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1595">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_allocate"></a><span data-ttu-id="8b105-1596">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1596">fx_file_extended_allocate</span></span>

<span data-ttu-id="8b105-1597">Bir dosya için alan ayırır</span><span class="sxs-lookup"><span data-stu-id="8b105-1597">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1598">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1598">Prototype</span></span>

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="8b105-1599">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1599">Description</span></span>

<span data-ttu-id="8b105-1600">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1600">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8b105-1601">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8b105-1601">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8b105-1602">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1602">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="8b105-1603">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1603">This service is designed for exFAT.</span></span> <span data-ttu-id="8b105-1604">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1604">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1605">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1605">Input Parameters</span></span>

- <span data-ttu-id="8b105-1606">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1606">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-1607">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1607">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1608">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1608">Return Values</span></span>

- <span data-ttu-id="8b105-1609">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="8b105-1609">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="8b105-1610">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1610">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-1611">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1611">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-1612">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1612">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8b105-1613">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1613">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1614">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1614">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1615">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1615">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1616">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1616">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1617">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1617">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1618">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1618">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1619">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1619">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-1620">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1620">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1621">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1621">Allowed From</span></span>

<span data-ttu-id="8b105-1622">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1622">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1623">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1623">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1624">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1624">See Also</span></span>

- <span data-ttu-id="8b105-1625">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1625">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1626">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1626">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1627">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1627">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1628">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1628">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1629">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1629">fx_file_close</span></span>
- <span data-ttu-id="8b105-1630">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1630">fx_file_create</span></span>
- <span data-ttu-id="8b105-1631">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1631">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1632">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1632">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1633">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1633">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1634">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1634">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1635">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1635">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1636">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1636">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1637">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1637">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1638">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1638">fx_file_open</span></span>
- <span data-ttu-id="8b105-1639">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1639">fx_file_read</span></span>
- <span data-ttu-id="8b105-1640">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1640">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1641">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1641">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1642">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1642">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1643">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1643">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1644">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1644">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1645">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1645">fx_file_write</span></span>
- <span data-ttu-id="8b105-1646">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1646">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1647">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1647">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1648">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1648">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1649">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1649">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1650">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1650">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_best_effort_allocate"></a><span data-ttu-id="8b105-1651">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1651">fx_file_extended_best_effort_allocate</span></span>

<span data-ttu-id="8b105-1652">Bir dosya için alan ayırmak için en iyi çaba</span><span class="sxs-lookup"><span data-stu-id="8b105-1652">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1653">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1653">Prototype</span></span>

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="8b105-1654">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1654">Description</span></span>

<span data-ttu-id="8b105-1655">Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1655">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="8b105-1656">FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="8b105-1656">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="8b105-1657">Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1657">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="8b105-1658">Medyada yeterli sayıda ardışık küme yoksa, bu hizmet birbirini izleyen en büyük küme bloğunu dosyaya bağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1658">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="8b105-1659">Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-1659">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="8b105-1660">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1660">This service is designed for exFAT.</span></span> <span data-ttu-id="8b105-1661">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 Aralık dışında boşluk önceden ayırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1661">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1662">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1662">Input Parameters</span></span>

- <span data-ttu-id="8b105-1663">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1663">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-1664">**Boyut**: dosya için ayrılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1664">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1665">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1665">Return Values</span></span>

- <span data-ttu-id="8b105-1666">**FX_SUCCESS** (0x00) başarılı dosya ayırma.</span><span class="sxs-lookup"><span data-stu-id="8b105-1666">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="8b105-1667">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1667">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-1668">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1668">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-1669">Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1669">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="8b105-1670">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1670">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1671">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1671">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1672">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1672">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1673">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1673">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1674">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1674">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1675">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1675">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1676">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1676">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-1677">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1677">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1678">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1678">Allowed From</span></span>

<span data-ttu-id="8b105-1679">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1679">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1680">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1680">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-1681">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1681">See Also</span></span>

- <span data-ttu-id="8b105-1682">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1682">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1683">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1683">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1684">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1684">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1685">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1685">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1686">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1686">fx_file_close</span></span>
- <span data-ttu-id="8b105-1687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1687">fx_file_create</span></span>
- <span data-ttu-id="8b105-1688">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1688">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1689">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1689">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1690">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1690">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1691">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1691">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1692">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1692">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1693">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1693">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1694">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1694">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1695">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1695">fx_file_open</span></span>
- <span data-ttu-id="8b105-1696">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1696">fx_file_read</span></span>
- <span data-ttu-id="8b105-1697">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1697">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1698">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1698">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1699">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1699">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1700">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1700">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1701">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1701">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1702">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1702">fx_file_write</span></span>
- <span data-ttu-id="8b105-1703">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1703">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1704">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1704">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1705">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1705">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1706">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1706">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1707">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1707">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_relative_seek"></a><span data-ttu-id="8b105-1708">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1708">fx_file_extended_relative_seek</span></span>

<span data-ttu-id="8b105-1709">Göreli bayt uzaklığına pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="8b105-1709">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1710">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1710">Prototype</span></span>

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="8b105-1711">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1711">Description</span></span>

<span data-ttu-id="8b105-1712">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1712">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="8b105-1713">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1713">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="8b105-1714">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1714">This service is designed for exFAT.</span></span> <span data-ttu-id="8b105-1715">*Byte_offset* parametresi, çağıranın 4 Aralık dışında okuma/yazma işaretçisini yeniden konumlandırmasına olanak tanıyan bir bit-bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1715">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-1716">*Arama işlemi dosyanın sonundan sonra arama yapmayı denerse, dosyanın okuma/yazma işaretçisi dosyanın sonuna yerleştirilir. Buna karşılık, arama işlemi dosyanın başlangıcını aşan konuma çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başlangıcına yerleştirilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-1716">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1717">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1717">Input Parameters</span></span>

- <span data-ttu-id="8b105-1718">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1718">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-1719">**byte_offset**: dosyada istenen göreli bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="8b105-1719">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="8b105-1720">**seek_from**: göreli arama yapılacak yönün yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="8b105-1720">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="8b105-1721">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8b105-1721">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="8b105-1722">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="8b105-1722">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="8b105-1723">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-1723">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="8b105-1724">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-1724">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="8b105-1725">FX_SEEK_BACK (0x03) FX_SEEK_BEGIN belirtilmişse, arama işlemi dosyanın başından yapılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1725">FX_SEEK_BACK (0x03) If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="8b105-1726">FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1726">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="8b105-1727">FX_SEEK_FORWARD belirtilirse, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1727">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="8b105-1728">FX_SEEK_BACK belirtilirse, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1728">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1729">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1729">Return Values</span></span>

- <span data-ttu-id="8b105-1730">**FX_SUCCESS** (0x00) başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="8b105-1730">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="8b105-1731">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1731">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-1732">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1732">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1733">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1733">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1734">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1734">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1735">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1735">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1736">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1736">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-1737">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1737">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1738">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1738">Allowed From</span></span>

<span data-ttu-id="8b105-1739">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1740">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1740">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1741">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1741">See Also</span></span>

- <span data-ttu-id="8b105-1742">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1742">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1743">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1743">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1744">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1744">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1745">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1745">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1746">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1746">fx_file_close</span></span>
- <span data-ttu-id="8b105-1747">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1747">fx_file_create</span></span>
- <span data-ttu-id="8b105-1748">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1748">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1749">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1749">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1750">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1750">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1751">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1751">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1752">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1752">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1753">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1753">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1754">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1754">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1755">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1755">fx_file_open</span></span>
- <span data-ttu-id="8b105-1756">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1756">fx_file_read</span></span>
- <span data-ttu-id="8b105-1757">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1757">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1758">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1758">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1759">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1759">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1760">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1760">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1761">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1761">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1762">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1762">fx_file_write</span></span>
- <span data-ttu-id="8b105-1763">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1763">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1764">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1764">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1765">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1765">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1766">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1766">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1767">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1767">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_seek"></a><span data-ttu-id="8b105-1768">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1768">fx_file_extended_seek</span></span>

<span data-ttu-id="8b105-1769">Bayt uzaklığa pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="8b105-1769">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1770">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1770">Prototype</span></span>

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a><span data-ttu-id="8b105-1771">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1771">Description</span></span>

<span data-ttu-id="8b105-1772">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen bayt uzaklığa konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1772">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="8b105-1773">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1773">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="8b105-1774">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1774">This service is designed for exFAT.</span></span> <span data-ttu-id="8b105-1775">*Byte_offset* parametresi, çağıranın 4 Aralık dışında okuma/yazma işaretçisini yeniden konumlandırmasına olanak tanıyan bir bit-bit tamsayı değeri alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1775">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1776">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1776">Input Parameters</span></span>

- <span data-ttu-id="8b105-1777">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1777">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-1778">**byte_offset**: dosyada istenen bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="8b105-1778">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="8b105-1779">Sıfır değeri, dosyanın başındaki okuma/yazma işaretçisini konumlandırır, ancak dosyanın boyutundan büyük bir değer, dosyanın sonundaki okuma/yazma işaretçisini konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1779">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1780">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1780">Return Values</span></span>

- <span data-ttu-id="8b105-1781">**FX_SUCCESS** (0x00) başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="8b105-1781">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="8b105-1782">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1782">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8b105-1783">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1783">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1784">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1784">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1785">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1785">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1786">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1786">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1787">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1787">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-1788">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1788">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1789">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1789">Allowed From</span></span>

<span data-ttu-id="8b105-1790">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1790">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1791">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1791">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1792">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1792">See Also</span></span>

- <span data-ttu-id="8b105-1793">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1793">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1794">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1794">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1795">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1795">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1796">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1796">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1797">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1797">fx_file_close</span></span>
- <span data-ttu-id="8b105-1798">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1798">fx_file_create</span></span>
- <span data-ttu-id="8b105-1799">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1799">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1800">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1800">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1801">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1801">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1802">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1802">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1803">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1803">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1804">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1804">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1805">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1805">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1806">fx_file_open fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1806">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="8b105-1807">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1807">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1808">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1808">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1809">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1809">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1810">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1810">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1811">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1811">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1812">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1812">fx_file_write</span></span>
- <span data-ttu-id="8b105-1813">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1813">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1814">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1814">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1815">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1815">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1816">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1816">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1817">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1817">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate"></a><span data-ttu-id="8b105-1818">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1818">fx_file_extended_truncate</span></span>

<span data-ttu-id="8b105-1819">Dosya keser</span><span class="sxs-lookup"><span data-stu-id="8b105-1819">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1820">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1820">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="8b105-1821">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1821">Description</span></span>

<span data-ttu-id="8b105-1822">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="8b105-1822">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8b105-1823">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1823">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="8b105-1824">Dosyayla ilişkili medya kümelerinin hiçbiri serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1824">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-1825">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-1825">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8b105-1826">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1826">This service is designed for exFAT.</span></span> <span data-ttu-id="8b105-1827">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır, bu da arayanın 4'lik aralığın ötesinde çalışmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1827">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1828">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1828">Input Parameters</span></span>

- <span data-ttu-id="8b105-1829">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1829">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-1830">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-1830">**size**: New file size.</span></span> <span data-ttu-id="8b105-1831">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1831">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1832">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1832">Return Values</span></span>

- <span data-ttu-id="8b105-1833">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="8b105-1833">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8b105-1834">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1834">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8b105-1835">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1835">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-1836">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1836">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1837">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1837">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1838">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1838">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1839">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1839">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1840">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1840">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1841">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1841">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8b105-1842">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1842">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-1843">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1843">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1844">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1844">Allowed From</span></span>

<span data-ttu-id="8b105-1845">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1845">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1846">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1846">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1847">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1847">See Also</span></span>

- <span data-ttu-id="8b105-1848">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1848">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1849">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1849">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1850">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1850">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1851">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1851">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1852">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1852">fx_file_close</span></span>
- <span data-ttu-id="8b105-1853">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1853">fx_file_create</span></span>
- <span data-ttu-id="8b105-1854">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1854">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1855">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1855">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1856">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1856">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1857">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1857">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1858">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1858">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1859">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1859">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1860">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1860">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1861">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1861">fx_file_open</span></span>
- <span data-ttu-id="8b105-1862">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1862">fx_file_read</span></span>
- <span data-ttu-id="8b105-1863">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1863">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1864">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1864">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1865">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1865">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1866">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1866">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1867">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1867">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1868">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1868">fx_file_write</span></span>
- <span data-ttu-id="8b105-1869">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1869">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1870">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1870">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1871">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1871">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1872">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1872">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1873">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1873">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate_release"></a><span data-ttu-id="8b105-1874">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1874">fx_file_extended_truncate_release</span></span>

<span data-ttu-id="8b105-1875">Dosya ve yayınlar kümesi keser</span><span class="sxs-lookup"><span data-stu-id="8b105-1875">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1876">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1876">Prototype</span></span>

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a><span data-ttu-id="8b105-1877">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1877">Description</span></span>

<span data-ttu-id="8b105-1878">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="8b105-1878">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8b105-1879">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1879">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="8b105-1880">***Fx_file_extended_truncate*** hizmetinden farklı olarak, bu hizmet kullanılmayan kümeleri serbest bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1880">Unlike the ***fx_file_extended_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-1881">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-1881">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8b105-1882">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1882">This service is designed for exFAT.</span></span> <span data-ttu-id="8b105-1883">*Boyut* parametresi 64 bitlik bir tamsayı değeri alır, bu da arayanın 4'lik aralığın ötesinde çalışmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1883">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1884">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1884">Input Parameters</span></span>

- <span data-ttu-id="8b105-1885">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1885">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-1886">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-1886">**size**: New file size.</span></span> <span data-ttu-id="8b105-1887">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1887">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1888">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1888">Return Values</span></span>

- <span data-ttu-id="8b105-1889">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="8b105-1889">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8b105-1890">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1890">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-1891">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1891">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-1892">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1892">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1893">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-1893">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-1894">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1894">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1895">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-1895">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-1896">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1896">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1897">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1897">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1898">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1898">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-1899">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1899">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-1900">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1900">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1901">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1901">Allowed From</span></span>

<span data-ttu-id="8b105-1902">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1902">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1903">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1903">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1904">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1904">See Also</span></span>

- <span data-ttu-id="8b105-1905">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1905">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1906">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1906">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1907">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1907">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1908">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1908">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1909">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-1909">fx_file_close</span></span>
- <span data-ttu-id="8b105-1910">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1910">fx_file_create</span></span>
- <span data-ttu-id="8b105-1911">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1911">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1912">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1912">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1913">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1913">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1914">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1914">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1915">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1915">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1916">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1916">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1917">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1917">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1918">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1918">fx_file_open</span></span>
- <span data-ttu-id="8b105-1919">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1919">fx_file_read</span></span>
- <span data-ttu-id="8b105-1920">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1920">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1921">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1921">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1922">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1922">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1923">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1923">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1924">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1924">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1925">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1925">fx_file_write</span></span>
- <span data-ttu-id="8b105-1926">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1926">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1927">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1927">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1928">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1928">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1929">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1929">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1930">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1930">fx_unicode_short_name_get</span></span>

## <a name="fx_file_open"></a><span data-ttu-id="8b105-1931">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-1931">fx_file_open</span></span>

<span data-ttu-id="8b105-1932">Dosyayı açar</span><span class="sxs-lookup"><span data-stu-id="8b105-1932">Opens file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1933">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1933">Prototype</span></span>

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a><span data-ttu-id="8b105-1934">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1934">Description</span></span>

<span data-ttu-id="8b105-1935">Bu hizmet, belirtilen dosyayı okuma ya da yazma için açar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1935">This service opens the specified file for either reading or writing.</span></span> <span data-ttu-id="8b105-1936">Bir dosya birden çok kez okumak için açılabilir, ancak bir dosya yalnızca yazıcı dosyayı kapatana kadar bir kez yazmak üzere açılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1936">A file may be opened for reading multiple times, while a file can only be opened for writing once until the writer closes the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-1937">*Dosya okuma ve yazma için eşzamanlı olarak açıksa dikkatli olunmalıdır. Bir dosya okuma için eşzamanlı olarak açıldığında gerçekleştirilen dosya yazma işlemi, okuyucu kapanmadığı ve dosyayı okumak üzere yeniden açtığından, okuyucu tarafından görülemeyebilir. Benzer şekilde, dosya Truncate Services kullanılırken dosya yazıcısı dikkatli olmalıdır. Bir dosya yazıcı tarafından kesilmişse, aynı dosyanın okuyucuları geçersiz veri döndürebilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-1937">*Care must be taken if a file is concurrently open for reading and writing. File writing performed when a file is simultaneously opened for reading may not be seen by the reader, unless the reader closes and reopens the file for reading. Similarly, the file writer should be careful when using file truncate services. If a file is truncated by the writer, readers of the same file could return invalid data.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-1938">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1938">Input Parameters</span></span>

- <span data-ttu-id="8b105-1939">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1939">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-1940">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1940">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-1941">**file_name**: açılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-1941">**file_name**: Pointer to the name of the file to open (directory path is optional).</span></span>
- <span data-ttu-id="8b105-1942">**open_type**: dosya açma türü.</span><span class="sxs-lookup"><span data-stu-id="8b105-1942">**open_type**: Type of file open.</span></span> <span data-ttu-id="8b105-1943">Geçerli açık tür seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8b105-1943">Valid open type options are:</span></span>
  - <span data-ttu-id="8b105-1944">FX_OPEN_FOR_READ (0x00)</span><span class="sxs-lookup"><span data-stu-id="8b105-1944">FX_OPEN_FOR_READ (0x00)</span></span>
  - <span data-ttu-id="8b105-1945">FX_OPEN_FOR_WRITE (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-1945">FX_OPEN_FOR_WRITE (0x01)</span></span>
  - <span data-ttu-id="8b105-1946">FX_OPEN_FOR_READ_FAST (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-1946">FX_OPEN_FOR_READ_FAST (0x02)</span></span>

<span data-ttu-id="8b105-1947">FX_OPEN_FOR_READ ve FX_OPEN_FOR_READ_FAST dosyaları açmak benzerdir:</span><span class="sxs-lookup"><span data-stu-id="8b105-1947">Opening files with FX_OPEN_FOR_READ and FX_OPEN_FOR_READ_FAST is similar:</span></span>

- <span data-ttu-id="8b105-1948">FX_OPEN_FOR_READ, dosyayı oluşturan kümelerin bağlı listesinin bozulmamış olduğunu ve FX_OPEN_FOR_READ_FAST Bu doğrulamayı gerçekleştirmediğinden daha hızlı hale gelmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1948">FX_OPEN_FOR_READ includes verification that the linked-list of clusters that comprise the file are intact, and FX_OPEN_FOR_READ_FAST does not perform this verification, which makes it faster.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-1949">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-1949">Return Values</span></span>

- <span data-ttu-id="8b105-1950">**FX_SUCCESS** (0x00) başarılı dosya açıldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1950">**FX_SUCCESS** (0x00) Successful file open.</span></span>
- <span data-ttu-id="8b105-1951">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1951">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-1952">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1952">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="8b105-1953">**FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.</span><span class="sxs-lookup"><span data-stu-id="8b105-1953">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="8b105-1954">**FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve açma başarısız.</span><span class="sxs-lookup"><span data-stu-id="8b105-1954">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the open failed.</span></span>
- <span data-ttu-id="8b105-1955">**FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık veya açma türü geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1955">**FX_ACCESS_ERROR** (0x06) Specified file is already open or open type is invalid.</span></span>
- <span data-ttu-id="8b105-1956">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-1956">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-1957">**FX_MEDIA_INVALID** (0x02) ortam geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1957">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="8b105-1958">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-1958">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-1959">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-1959">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-1960">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-1960">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-1961">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-1961">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8b105-1962">**FX_PTR_ERROR** (0x18) geçersiz medya veya dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-1962">**FX_PTR_ERROR** (0x18) Invalid media or file pointer.</span></span>
- <span data-ttu-id="8b105-1963">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-1963">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-1964">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-1964">Allowed From</span></span>

<span data-ttu-id="8b105-1965">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-1965">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-1966">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-1966">Example</span></span>

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-1967">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-1967">See Also</span></span>

- <span data-ttu-id="8b105-1968">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1968">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-1969">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1969">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-1970">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1970">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-1971">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1971">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1972">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1972">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="8b105-1973">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1973">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-1974">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-1974">fx_file_delete</span></span>
- <span data-ttu-id="8b105-1975">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1975">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-1976">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-1976">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-1977">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1977">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-1978">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1978">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-1979">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1979">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-1980">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1980">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-1981">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1981">fx_file_read</span></span>
- <span data-ttu-id="8b105-1982">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1982">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-1983">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1983">fx_file_rename</span></span>
- <span data-ttu-id="8b105-1984">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-1984">fx_file_seek</span></span>
- <span data-ttu-id="8b105-1985">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-1985">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-1986">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-1986">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-1987">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-1987">fx_file_write</span></span>
- <span data-ttu-id="8b105-1988">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-1988">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-1989">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-1989">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-1990">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-1990">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-1991">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1991">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-1992">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-1992">fx_unicode_short_name_get</span></span>

## <a name="fx_file_read"></a><span data-ttu-id="8b105-1993">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-1993">fx_file_read</span></span>

<span data-ttu-id="8b105-1994">Dosyadan bayt okur</span><span class="sxs-lookup"><span data-stu-id="8b105-1994">Reads bytes from file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-1995">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-1995">Prototype</span></span>

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a><span data-ttu-id="8b105-1996">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-1996">Description</span></span>

<span data-ttu-id="8b105-1997">Bu hizmet, dosyadaki baytları okur ve bunları sağlanan arabellekte depolar.</span><span class="sxs-lookup"><span data-stu-id="8b105-1997">This service reads bytes from the file and stores them in the supplied buffer.</span></span> <span data-ttu-id="8b105-1998">Okuma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1998">After the read is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span> <span data-ttu-id="8b105-1999">İstekte daha az bayt kaldığında, yalnızca kalan baytlar arabellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-1999">If there are fewer bytes remaining in the request, only the bytes remaining are stored in the buffer.</span></span> <span data-ttu-id="8b105-2000">Herhangi bir durumda, arabelleğe yerleştirilmiş baytların toplam sayısı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-2000">In any case, the total number of bytes placed in the buffer is returned to the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2001">*Uygulama, sağlanan arabelleğin belirtilen sayıda istenen baytı depolayabilmesini sağlamalıdır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2001">*The application must ensure that the buffer supplied is able to store the specified number of requested bytes.*</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2002">*Hedef arabellek uzun bir sözcüklük sınırındayken ve istenen boyut sizeof (**ulong**) tarafından eşit olarak bölünediyse daha hızlı performans elde edilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2002">*Faster performance is achieved if the destination buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2003">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2003">Input Parameters</span></span>

- <span data-ttu-id="8b105-2004">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2004">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-2005">**buffer_ptr**: okuma için hedef arabelleğe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2005">**buffer_ptr**: Pointer to the destination buffer for the read.</span></span>
- <span data-ttu-id="8b105-2006">**request_size**: okunacak en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2006">**request_size**: Maximum number of bytes to read.</span></span>
- <span data-ttu-id="8b105-2007">**actual_size**: sağlanan arabelleğe okunan gerçek bayt sayısını tutacak değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2007">**actual_size**: Pointer to the variable to hold the actual number of bytes read into the supplied buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2008">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2008">Return Values</span></span>

- <span data-ttu-id="8b105-2009">**FX_SUCCESS** (0x00) başarılı dosya okundu.</span><span class="sxs-lookup"><span data-stu-id="8b105-2009">**FX_SUCCESS** (0x00) Successful file read.</span></span>
- <span data-ttu-id="8b105-2010">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2010">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8b105-2011">**FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve okuma başarısız.</span><span class="sxs-lookup"><span data-stu-id="8b105-2011">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the read failed.</span></span>
- <span data-ttu-id="8b105-2012">**FX_END_OF_FILE** (0x09) dosya sonuna ulaşıldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2012">**FX_END_OF_FILE** (0x09) End of file has been reached.</span></span>
- <span data-ttu-id="8b105-2013">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2013">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2014">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-2014">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-2015">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2015">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2016">**FX_PTR_ERROR** (0x18) geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2016">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="8b105-2017">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2017">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2018">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2018">Allowed From</span></span>

<span data-ttu-id="8b105-2019">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2019">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2020">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2020">Example</span></span>

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
### <a name="see-also"></a><span data-ttu-id="8b105-2021">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2021">See Also</span></span>

- <span data-ttu-id="8b105-2022">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2022">fx_file_allocate,</span></span>
- <span data-ttu-id="8b105-2023">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="8b105-2023">fx_file_attributes_read,</span></span>
- <span data-ttu-id="8b105-2024">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="8b105-2024">fx_file_attributes_set,</span></span>
- <span data-ttu-id="8b105-2025">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2025">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="8b105-2026">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="8b105-2026">fx_file_close,</span></span>
- <span data-ttu-id="8b105-2027">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="8b105-2027">fx_file_create,</span></span>
- <span data-ttu-id="8b105-2028">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="8b105-2028">fx_file_date_time_set,</span></span>
- <span data-ttu-id="8b105-2029">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="8b105-2029">fx_file_delete,</span></span>
- <span data-ttu-id="8b105-2030">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2030">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="8b105-2031">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2031">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="8b105-2032">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2032">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="8b105-2033">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2033">fx_file_extended_seek,</span></span>
- <span data-ttu-id="8b105-2034">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2034">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="8b105-2035">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8b105-2035">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="8b105-2036">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="8b105-2036">fx_file_open,</span></span>
- <span data-ttu-id="8b105-2037">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2037">fx_file_relative_seek,</span></span>
- <span data-ttu-id="8b105-2038">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8b105-2038">fx_file_rename,</span></span>
- <span data-ttu-id="8b105-2039">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2039">fx_file_seek,</span></span>
- <span data-ttu-id="8b105-2040">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2040">fx_file_truncate,</span></span>
- <span data-ttu-id="8b105-2041">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8b105-2041">fx_file_truncate_release,</span></span>
- <span data-ttu-id="8b105-2042">fx_file_write,</span><span class="sxs-lookup"><span data-stu-id="8b105-2042">fx_file_write,</span></span>
- <span data-ttu-id="8b105-2043">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="8b105-2043">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="8b105-2044">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="8b105-2044">fx_unicode_file_create,</span></span>
- <span data-ttu-id="8b105-2045">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8b105-2045">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="8b105-2046">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="8b105-2046">fx_unicode_name_get,</span></span>
- <span data-ttu-id="8b105-2047">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2047">fx_unicode_short_name_get</span></span>

## <a name="fx_file_relative_seek"></a><span data-ttu-id="8b105-2048">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2048">fx_file_relative_seek</span></span>

<span data-ttu-id="8b105-2049">Göreli bayt uzaklığına pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="8b105-2049">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2050">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2050">Prototype</span></span>

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="8b105-2051">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2051">Description</span></span>

<span data-ttu-id="8b105-2052">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2052">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="8b105-2053">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2053">Any subsequent file read or write request will begin at this location in the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-2054">*Arama işlemi dosyanın sonundan sonra arama yapmayı denerse, dosyanın okuma/yazma işaretçisi dosyanın sonuna yerleştirilir. Buna karşılık, arama işlemi dosyanın başlangıcını aşan konuma çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başlangıcına yerleştirilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2054">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

<span data-ttu-id="8b105-2055">4 GB 'ın ötesinde bir fark değeri ile arama yapmak için, uygulama Service *fx_file_extended_relative_seek* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2055">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_relative_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2056">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2056">Input Parameters</span></span>

- <span data-ttu-id="8b105-2057">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2057">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-2058">**byte_offset**: dosyada istenen göreli bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="8b105-2058">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="8b105-2059">**seek_from**: göreli arama yapılacak yönün yönü ve konumu.</span><span class="sxs-lookup"><span data-stu-id="8b105-2059">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="8b105-2060">Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8b105-2060">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="8b105-2061">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="8b105-2061">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="8b105-2062">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-2062">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="8b105-2063">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-2063">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="8b105-2064">FX_SEEK_BACK (0x03)</span><span class="sxs-lookup"><span data-stu-id="8b105-2064">FX_SEEK_BACK (0x03)</span></span>

<span data-ttu-id="8b105-2065">FX_SEEK_BEGIN belirtilirse, arama işlemi dosyanın başından yapılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2065">If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="8b105-2066">FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2066">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="8b105-2067">FX_SEEK_FORWARD belirtilirse, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2067">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="8b105-2068">FX_SEEK_BACK belirtilirse, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2068">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2069">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2069">Return Values</span></span>

- <span data-ttu-id="8b105-2070">**FX_SUCCESS** (0x00) başarılı dosya göreli arama.</span><span class="sxs-lookup"><span data-stu-id="8b105-2070">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="8b105-2071">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2071">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-2072">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2072">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2073">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2074">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2075">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2075">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-2076">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2076">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-2077">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2077">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2078">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2078">Allowed From</span></span>

<span data-ttu-id="8b105-2079">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2079">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2080">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2080">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-2081">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2081">See Also</span></span>

- <span data-ttu-id="8b105-2082">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2082">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-2083">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2083">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-2084">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2084">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-2085">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2085">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2086">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2086">fx_file_close</span></span>
- <span data-ttu-id="8b105-2087">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2087">fx_file_create</span></span>
- <span data-ttu-id="8b105-2088">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2088">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-2089">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-2089">fx_file_delete</span></span>
- <span data-ttu-id="8b105-2090">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2090">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-2091">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2091">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2092">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2092">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-2093">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2093">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-2094">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2094">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-2095">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2095">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-2096">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2096">fx_file_open</span></span>
- <span data-ttu-id="8b105-2097">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2097">fx_file_read</span></span>
- <span data-ttu-id="8b105-2098">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2098">fx_file_rename</span></span>
- <span data-ttu-id="8b105-2099">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2099">fx_file_seek</span></span>
- <span data-ttu-id="8b105-2100">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2100">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-2101">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2101">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-2102">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2102">fx_file_write</span></span>
- <span data-ttu-id="8b105-2103">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2103">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-2104">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2104">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-2105">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2105">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-2106">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2106">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-2107">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2107">fx_unicode_short_name_get</span></span>

## <a name="fx_file_rename"></a><span data-ttu-id="8b105-2108">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2108">fx_file_rename</span></span>

<span data-ttu-id="8b105-2109">Dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="8b105-2109">Renames  file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2110">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2110">Prototype</span></span>

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a><span data-ttu-id="8b105-2111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2111">Description</span></span>

<span data-ttu-id="8b105-2112">Bu hizmet *old_file_name* tarafından belirtilen dosyanın adını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2112">This service changes the name of the file specified by *old_file_name*.</span></span> <span data-ttu-id="8b105-2113">Yeniden adlandırma işlemi, belirtilen yola veya varsayılan yola göre de yapılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2113">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="8b105-2114">Yeni dosya adında bir yol belirtilmişse, yeniden adlandırılan dosya belirtilen yola etkili bir şekilde taşınır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2114">If a path is specified in the new file name, the renamed file is effectively moved to the specified path.</span></span> <span data-ttu-id="8b105-2115">Hiçbir yol belirtilmemişse, yeniden adlandırılan dosya geçerli varsayılan yola yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2115">If no path is specified, the renamed file is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2116">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2116">Input Parameters</span></span>

- <span data-ttu-id="8b105-2117">**media_ptr**: bir medya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2117">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="8b105-2118">**old_file_name**: yeniden adlandırılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="8b105-2118">**old_file_name**: Pointer to the name of the file to rename (directory path is optional).</span></span>
- <span data-ttu-id="8b105-2119">**new_file_name**: yeni dosya adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2119">**new_file_name**: Pointer to the new file name.</span></span> <span data-ttu-id="8b105-2120">Dizin yoluna izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-2120">The directory path is not allowed.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2121">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2121">Return Values</span></span>

- <span data-ttu-id="8b105-2122">**FX_SUCCESS** (0x00) başarılı dosya yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="8b105-2122">**FX_SUCCESS** (0x00) Successful file rename.</span></span>
- <span data-ttu-id="8b105-2123">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2123">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2124">**FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2124">**FX_NOT_FOUND** (0x04)    Specified file was not found.</span></span>
- <span data-ttu-id="8b105-2125">**FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.</span><span class="sxs-lookup"><span data-stu-id="8b105-2125">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="8b105-2126">**FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık.</span><span class="sxs-lookup"><span data-stu-id="8b105-2126">**FX_ACCESS_ERROR** (0x06) Specified file is already open.</span></span>
- <span data-ttu-id="8b105-2127">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2127">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2128">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2128">**FX_WRITE_PROTECT** (0x23)    Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-2129">**FX_INVALID_NAME** (0x0C) belirtilen yeni dosya adı geçerli bir dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2129">**FX_INVALID_NAME** (0x0C) Specified new file name is not a valid file name.</span></span>
- <span data-ttu-id="8b105-2130">**FX_INVALID_PATH** (0x0D) yolu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2130">**FX_INVALID_PATH** (0x0D)    Path is invalid.</span></span>
- <span data-ttu-id="8b105-2131">**FX_ALREADY_CREATED** (0x0B) yeni dosya adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2131">**FX_ALREADY_CREATED** (0x0B) The new file name is used.</span></span>
- <span data-ttu-id="8b105-2132">**FX_MEDIA_INVALID** (0x02) medyası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2132">**FX_MEDIA_INVALID** (0x02)    Media is invalid.</span></span>
- <span data-ttu-id="8b105-2133">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2133">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2134">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2134">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2135">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2135">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-2136">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-2136">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-2137">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-2137">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8b105-2138">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2138">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-2139">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2139">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2140">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2140">Allowed From</span></span>

<span data-ttu-id="8b105-2141">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2142">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2142">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-2143">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2143">See Also</span></span>

- <span data-ttu-id="8b105-2144">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2144">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-2145">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2145">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-2146">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2146">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-2147">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2147">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2148">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2148">fx_file_close</span></span>
- <span data-ttu-id="8b105-2149">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2149">fx_file_create</span></span>
- <span data-ttu-id="8b105-2150">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2150">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-2151">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-2151">fx_file_delete</span></span>
- <span data-ttu-id="8b105-2152">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2152">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-2153">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2153">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2154">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2154">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-2155">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2155">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-2156">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2156">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-2157">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2157">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-2158">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2158">fx_file_open</span></span>
- <span data-ttu-id="8b105-2159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2159">fx_file_read</span></span>
- <span data-ttu-id="8b105-2160">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2160">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-2161">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2161">fx_file_seek</span></span>
- <span data-ttu-id="8b105-2162">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2162">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-2163">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2163">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-2164">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2164">fx_file_write</span></span>
- <span data-ttu-id="8b105-2165">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2165">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-2166">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2166">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-2167">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2167">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-2168">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2168">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-2169">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2169">fx_unicode_short_name_get</span></span>

## <a name="fx_file_seek"></a><span data-ttu-id="8b105-2170">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2170">fx_file_seek</span></span>

<span data-ttu-id="8b105-2171">Bayt uzaklığa pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="8b105-2171">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2172">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2172">Prototype</span></span>

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a><span data-ttu-id="8b105-2173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2173">Description</span></span>

<span data-ttu-id="8b105-2174">Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen bayt uzaklığa konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2174">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="8b105-2175">Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2175">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="8b105-2176">4 GB 'ın ötesinde bir fark değeri ile arama yapmak için, uygulama Service *fx_file_extended_seek* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2176">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2177">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2177">Input Parameters</span></span>

- <span data-ttu-id="8b105-2178">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2178">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-2179">**byte_offset**: dosyada istenen bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="8b105-2179">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="8b105-2180">Sıfır değeri, dosyanın başındaki okuma/yazma işaretçisini konumlandırır, ancak dosyanın boyutundan büyük bir değer, dosyanın sonundaki okuma/yazma işaretçisini konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2180">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2181">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2181">Return Values</span></span>

- <span data-ttu-id="8b105-2182">**FX_SUCCESS** (0x00) başarılı dosya arama.</span><span class="sxs-lookup"><span data-stu-id="8b105-2182">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="8b105-2183">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2183">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8b105-2184">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2184">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2185">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2185">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2186">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2186">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2187">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-2187">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-2188">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2188">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-2189">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2190">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2190">Allowed From</span></span>

<span data-ttu-id="8b105-2191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2192">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2192">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-2193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2193">See Also</span></span>

- <span data-ttu-id="8b105-2194">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2194">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-2195">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2195">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-2196">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2196">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-2197">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2197">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2198">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2198">fx_file_close</span></span>
- <span data-ttu-id="8b105-2199">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2199">fx_file_create</span></span>
- <span data-ttu-id="8b105-2200">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2200">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-2201">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-2201">fx_file_delete</span></span>
- <span data-ttu-id="8b105-2202">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2202">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-2203">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2203">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2204">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2204">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-2205">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2205">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-2206">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2206">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-2207">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2207">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-2208">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2208">fx_file_open</span></span>
- <span data-ttu-id="8b105-2209">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2209">fx_file_read</span></span>
- <span data-ttu-id="8b105-2210">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2210">fx_file_rename</span></span>
- <span data-ttu-id="8b105-2211">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2211">fx_file_seek</span></span>
- <span data-ttu-id="8b105-2212">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2212">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-2213">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2213">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-2214">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2214">fx_file_write</span></span>
- <span data-ttu-id="8b105-2215">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2215">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-2216">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2216">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-2217">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2217">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-2218">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2218">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-2219">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2219">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate"></a><span data-ttu-id="8b105-2220">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2220">fx_file_truncate</span></span>

<span data-ttu-id="8b105-2221">Dosya keser</span><span class="sxs-lookup"><span data-stu-id="8b105-2221">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2222">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2222">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="8b105-2223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2223">Description</span></span>

<span data-ttu-id="8b105-2224">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="8b105-2224">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8b105-2225">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2225">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="8b105-2226">Dosyayla ilişkili medya kümelerinin hiçbiri serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2226">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2227">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2227">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8b105-2228">4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2228">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2229">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2229">Input Parameters</span></span>

- <span data-ttu-id="8b105-2230">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2230">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-2231">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-2231">**size**: New file size.</span></span> <span data-ttu-id="8b105-2232">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2232">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2233">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2233">Return Values</span></span>

- <span data-ttu-id="8b105-2234">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="8b105-2234">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8b105-2235">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2235">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8b105-2236">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2236">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-2237">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2237">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2238">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2238">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-2239">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2239">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2240">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2240">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2241">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2241">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-2242">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok</span><span class="sxs-lookup"><span data-stu-id="8b105-2242">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="8b105-2243">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2243">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-2244">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2244">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2245">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2245">Allowed From</span></span>

<span data-ttu-id="8b105-2246">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2247">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2247">Example</span></span>

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-2248">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2248">See Also</span></span>

- <span data-ttu-id="8b105-2249">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2249">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-2250">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2250">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-2251">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2251">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-2252">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2252">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2253">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2253">fx_file_close</span></span>
- <span data-ttu-id="8b105-2254">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2254">fx_file_create</span></span>
- <span data-ttu-id="8b105-2255">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2255">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-2256">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-2256">fx_file_delete</span></span>
- <span data-ttu-id="8b105-2257">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2257">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-2258">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2258">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2259">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2259">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-2260">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2260">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-2261">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2261">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-2262">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2262">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-2263">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2263">fx_file_open</span></span>
- <span data-ttu-id="8b105-2264">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2264">fx_file_read</span></span>
- <span data-ttu-id="8b105-2265">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2265">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-2266">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2266">fx_file_rename</span></span>
- <span data-ttu-id="8b105-2267">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2267">fx_file_seek</span></span>
- <span data-ttu-id="8b105-2268">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2268">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-2269">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2269">fx_file_write</span></span>
- <span data-ttu-id="8b105-2270">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2270">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-2271">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2271">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-2272">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2272">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-2273">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2273">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-2274">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2274">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate_release"></a><span data-ttu-id="8b105-2275">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2275">fx_file_truncate_release</span></span>

<span data-ttu-id="8b105-2276">Dosya ve yayınlar kümesi keser</span><span class="sxs-lookup"><span data-stu-id="8b105-2276">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2277">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2277">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="8b105-2278">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2278">Description</span></span>

<span data-ttu-id="8b105-2279">Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser.</span><span class="sxs-lookup"><span data-stu-id="8b105-2279">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="8b105-2280">Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2280">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="8b105-2281">***Fx_file_truncate*** hizmetinden farklı olarak, bu hizmet kullanılmayan kümeleri serbest bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2281">Unlike the ***fx_file_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2282">*Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2282">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="8b105-2283">4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate_release* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2283">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate_release*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2284">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2284">Input Parameters</span></span>

- <span data-ttu-id="8b105-2285">**file_ptr**: daha önce açılmış bir dosyanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2285">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="8b105-2286">**Boyut**: yeni dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-2286">**size**: New file size.</span></span> <span data-ttu-id="8b105-2287">Bu yeni dosya boyutunu aşan baytlar atılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2287">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2288">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2288">Return Values</span></span>

- <span data-ttu-id="8b105-2289">**FX_SUCCESS** (0x00) başarılı dosya kesilme.</span><span class="sxs-lookup"><span data-stu-id="8b105-2289">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="8b105-2290">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2290">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-2291">**FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2291">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="8b105-2292">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2292">**FX_IO_ERROR** (0x90)    Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2293">**FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2293">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="8b105-2294">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2294">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="8b105-2295">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2295">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2296">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-2296">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-2297">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2297">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-2298">**FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2298">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation.</span></span>
- <span data-ttu-id="8b105-2299">**FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2299">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="8b105-2300">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2300">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2301">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2301">Allowed From</span></span>

<span data-ttu-id="8b105-2302">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2303">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2303">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a><span data-ttu-id="8b105-2304">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2304">See Also</span></span>

- <span data-ttu-id="8b105-2305">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2305">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-2306">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2306">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-2307">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2307">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-2308">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2308">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2309">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2309">fx_file_close</span></span>
- <span data-ttu-id="8b105-2310">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2310">fx_file_create</span></span>
- <span data-ttu-id="8b105-2311">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2311">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-2312">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-2312">fx_file_delete</span></span>
- <span data-ttu-id="8b105-2313">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2313">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-2314">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2314">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2315">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2315">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-2316">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2316">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-2317">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2317">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-2318">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2318">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-2319">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2319">fx_file_open</span></span>
- <span data-ttu-id="8b105-2320">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2320">fx_file_read</span></span>
- <span data-ttu-id="8b105-2321">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2321">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-2322">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2322">fx_file_rename</span></span>
- <span data-ttu-id="8b105-2323">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2323">fx_file_seek</span></span>
- <span data-ttu-id="8b105-2324">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2324">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-2325">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2325">fx_file_write</span></span>
- <span data-ttu-id="8b105-2326">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2326">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-2327">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2327">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-2328">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2328">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-2329">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2329">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-2330">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2330">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write"></a><span data-ttu-id="8b105-2331">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2331">fx_file_write</span></span>

<span data-ttu-id="8b105-2332">Baytları dosyaya yazar</span><span class="sxs-lookup"><span data-stu-id="8b105-2332">Writes bytes to file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2333">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2333">Prototype</span></span>

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="8b105-2334">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2334">Description</span></span>

<span data-ttu-id="8b105-2335">Bu hizmet, dosyanın geçerli konumundan başlayarak belirtilen arabellekteki baytları yazar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2335">This service writes bytes from the specified buffer starting at the file's current position.</span></span> <span data-ttu-id="8b105-2336">Yazma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2336">After the write is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2337">*Kaynak arabelleğinin uzun bir sözcüklük sınırında olması ve istenen boyutun sizeof (**ulong**) tarafından eşit olarak bölünemesinin ardından daha hızlı performans elde edilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2337">*Faster performance is achieved if the source buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2338">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2338">Input Parameters</span></span>

- <span data-ttu-id="8b105-2339">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2339">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-2340">**buffer_ptr**: yazma için kaynak arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2340">**buffer_ptr**: Pointer to the source buffer for the write.</span></span>
- <span data-ttu-id="8b105-2341">**Boyut**: yazılacak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2341">**size**: Number of bytes to write.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2342">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2342">Return Values</span></span>

- <span data-ttu-id="8b105-2343">**FX_SUCCESS** (0x00) başarılı dosya yazma.</span><span class="sxs-lookup"><span data-stu-id="8b105-2343">**FX_SUCCESS** (0x00) Successful file write.</span></span>
- <span data-ttu-id="8b105-2344">**FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2344">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="8b105-2345">**FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2345">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="8b105-2346">**FX_NO_MORE_SPACE** (0x0A) medyada bu yazma işlemini gerçekleştirmek için kullanılabilecek daha fazla yer yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2346">**FX_NO_MORE_SPACE** (0x0A) There is no more room available in the media to perform this write.</span></span>
- <span data-ttu-id="8b105-2347">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2347">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2348">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2348">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-2349">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2349">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2350">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2350">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2351">**FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-2351">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="8b105-2352">**FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2352">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="8b105-2353">**FX_PTR_ERROR** (0x18) geçersiz dosya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2353">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="8b105-2354">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2354">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2355">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2355">Allowed From</span></span>

<span data-ttu-id="8b105-2356">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2356">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2357">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2357">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-2358">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2358">See Also</span></span>

- <span data-ttu-id="8b105-2359">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2359">fx_file_allocate,</span></span>
- <span data-ttu-id="8b105-2360">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="8b105-2360">fx_file_attributes_read,</span></span>
- <span data-ttu-id="8b105-2361">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="8b105-2361">fx_file_attributes_set,</span></span>
- <span data-ttu-id="8b105-2362">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2362">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="8b105-2363">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="8b105-2363">fx_file_close,</span></span>
- <span data-ttu-id="8b105-2364">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="8b105-2364">fx_file_create,</span></span>
- <span data-ttu-id="8b105-2365">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="8b105-2365">fx_file_date_time_set,</span></span>
- <span data-ttu-id="8b105-2366">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="8b105-2366">fx_file_delete,</span></span>
- <span data-ttu-id="8b105-2367">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2367">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="8b105-2368">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2368">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="8b105-2369">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2369">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="8b105-2370">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2370">fx_file_extended_seek,</span></span>
- <span data-ttu-id="8b105-2371">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2371">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="8b105-2372">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8b105-2372">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="8b105-2373">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="8b105-2373">fx_file_open,</span></span>
- <span data-ttu-id="8b105-2374">fx_file_read,</span><span class="sxs-lookup"><span data-stu-id="8b105-2374">fx_file_read,</span></span>
- <span data-ttu-id="8b105-2375">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2375">fx_file_relative_seek,</span></span>
- <span data-ttu-id="8b105-2376">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8b105-2376">fx_file_rename,</span></span>
- <span data-ttu-id="8b105-2377">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="8b105-2377">fx_file_seek,</span></span>
- <span data-ttu-id="8b105-2378">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="8b105-2378">fx_file_truncate,</span></span>
- <span data-ttu-id="8b105-2379">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="8b105-2379">fx_file_truncate_release,</span></span>
- <span data-ttu-id="8b105-2380">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="8b105-2380">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="8b105-2381">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="8b105-2381">fx_unicode_file_create,</span></span>
- <span data-ttu-id="8b105-2382">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="8b105-2382">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="8b105-2383">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="8b105-2383">fx_unicode_name_get,</span></span>
- <span data-ttu-id="8b105-2384">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2384">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write_notify_set"></a><span data-ttu-id="8b105-2385">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2385">fx_file_write_notify_set</span></span>

<span data-ttu-id="8b105-2386">Dosya yazma bildirim işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-2386">Sets the file write notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2387">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2387">Prototype</span></span>

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a><span data-ttu-id="8b105-2388">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2388">Description</span></span>

<span data-ttu-id="8b105-2389">Bu hizmet, başarılı bir dosya yazma işleminden sonra çağrılan geri çağırma işlevini yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-2389">This service installs callback function that is invoked after a successful file write operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2390">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2390">Input Parameters</span></span>

- <span data-ttu-id="8b105-2391">**file_ptr**: dosya denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2391">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="8b105-2392">**file_write_notify**: yüklenecek dosya yazma geri arama işlevi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2392">**file_write_notify**: File write callback function to be installed.</span></span> <span data-ttu-id="8b105-2393">Callback işlevini NULL olarak ayarlayın geri çağırma işlevini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2393">Set the callback function to NULL disables the callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2394">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2394">Return Values</span></span>

- <span data-ttu-id="8b105-2395">**FX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2395">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="8b105-2396">**FX_PTR_ERROR** (0x18) file_ptr null.</span><span class="sxs-lookup"><span data-stu-id="8b105-2396">**FX_PTR_ERROR** (0x18) file_ptr is NULL.</span></span>
- <span data-ttu-id="8b105-2397">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2397">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2398">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2398">Allowed From</span></span>

<span data-ttu-id="8b105-2399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2400">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2400">Example</span></span>

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a><span data-ttu-id="8b105-2401">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2401">See Also</span></span>

- <span data-ttu-id="8b105-2402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2402">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-2403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2403">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-2404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2404">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-2405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2406">fx_file_close</span></span>
- <span data-ttu-id="8b105-2407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2407">fx_file_create</span></span>
- <span data-ttu-id="8b105-2408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2408">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-2409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-2409">fx_file_delete</span></span>
- <span data-ttu-id="8b105-2410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-2411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-2411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-2412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-2413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2413">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-2414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-2415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-2416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2416">fx_file_open</span></span>
- <span data-ttu-id="8b105-2417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2417">fx_file_read</span></span>
- <span data-ttu-id="8b105-2418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2418">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-2419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2419">fx_file_rename</span></span>
- <span data-ttu-id="8b105-2420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-2420">fx_file_seek</span></span>
- <span data-ttu-id="8b105-2421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-2421">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-2422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-2422">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-2423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2423">fx_file_write</span></span>
- <span data-ttu-id="8b105-2424">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-2424">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-2425">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-2425">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-2426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2426">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-2427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2427">fx_unicode_short_name_get</span></span>

## <a name="fx_media_abort"></a><span data-ttu-id="8b105-2428">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2428">fx_media_abort</span></span>

<span data-ttu-id="8b105-2429">Medya etkinliklerini iptal eder</span><span class="sxs-lookup"><span data-stu-id="8b105-2429">Aborts media activities</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2430">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2430">Prototype</span></span>

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-2431">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2431">Description</span></span>

<span data-ttu-id="8b105-2432">Bu hizmet, tüm açık dosyaları kapatma, ilişkili sürücüye bir iptal isteği gönderme ve medyayı durdurulmuş duruma yerleştirme dahil olmak üzere medyayla ilişkili tüm geçerli etkinlikleri iptal eder.</span><span class="sxs-lookup"><span data-stu-id="8b105-2432">This service aborts all current activities associated with the media, including closing all open files, sending an abort request to the associated driver, and placing the media in an aborted state.</span></span> <span data-ttu-id="8b105-2433">Bu hizmet genellikle g/ç hataları algılandığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2433">This service is typically called when I/O errors are detected.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2434">*Bir iptal işlemi gerçekleştirildikten sonra yeniden kullanmak için medyanın yeniden açılması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2434">*The media must be re-opened to use it again after an abort operation is performed.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2435">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2435">Input Parameters</span></span>

- <span data-ttu-id="8b105-2436">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2436">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2437">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2437">Return Values</span></span>

- <span data-ttu-id="8b105-2438">**FX_SUCCESS** (0x00) başarılı medya iptali.</span><span class="sxs-lookup"><span data-stu-id="8b105-2438">**FX_SUCCESS** (0x00) Successful media abort.</span></span>
- <span data-ttu-id="8b105-2439">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2439">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2440">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2440">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-2441">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2441">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2442">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2442">Allowed From</span></span>

<span data-ttu-id="8b105-2443">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2444">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2444">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2445">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2445">See Also</span></span>

- <span data-ttu-id="8b105-2446">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2446">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2447">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2447">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2448">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2448">fx_media_check</span></span>
- <span data-ttu-id="8b105-2449">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2449">fx_media_close</span></span>
- <span data-ttu-id="8b105-2450">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2450">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2451">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2451">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2452">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2452">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2453">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2453">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2454">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2454">fx_media_format</span></span>
- <span data-ttu-id="8b105-2455">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2455">fx_media_open</span></span>
- <span data-ttu-id="8b105-2456">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2456">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2457">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2457">fx_media_read</span></span>
- <span data-ttu-id="8b105-2458">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2458">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2459">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2459">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2460">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2460">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2461">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2461">fx_media_write</span></span>
- <span data-ttu-id="8b105-2462">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2462">fx_system_initialize</span></span>

## <a name="fx_media_cache_invalidate"></a><span data-ttu-id="8b105-2463">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2463">fx_media_cache_invalidate</span></span>

<span data-ttu-id="8b105-2464">Mantıksal kesim önbelleğini geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="8b105-2464">Invalidates logical sector cache</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2465">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2465">Prototype</span></span>

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="8b105-2466">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2466">Description</span></span>

<span data-ttu-id="8b105-2467">Bu hizmet önbellekteki tüm kirli kesimleri temizler ve sonra mantıksal kesim önbelleğinin tamamını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2467">This service flushes all dirty sectors in the cache and then invalidates the entire logical sector cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2468">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2468">Input Parameters</span></span>

- <span data-ttu-id="8b105-2469">**media_ptr**: medya denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="8b105-2469">**media_ptr**: Pointer to media control block</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2470">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2470">Return Values</span></span>

- <span data-ttu-id="8b105-2471">**FX_SUCCESS** (0x00) başarılı medya önbelleği geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2471">**FX_SUCCESS** (0x00) Successful media cache invalidate.</span></span>
- <span data-ttu-id="8b105-2472">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2472">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2473">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2473">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2474">**FX_PTR_ERROR** (0x18) geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2474">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="8b105-2475">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2475">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2476">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2476">Allowed From</span></span>

<span data-ttu-id="8b105-2477">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2478">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2478">Example</span></span>

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2479">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2479">See Also</span></span>

- <span data-ttu-id="8b105-2480">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2480">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2481">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2481">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2482">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2482">fx_media_check</span></span>
- <span data-ttu-id="8b105-2483">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2483">fx_media_close</span></span>
- <span data-ttu-id="8b105-2484">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2484">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2485">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2485">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2486">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2486">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2487">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2487">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2488">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2488">fx_media_format</span></span>
- <span data-ttu-id="8b105-2489">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2489">fx_media_open</span></span>
- <span data-ttu-id="8b105-2490">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2490">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2491">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2491">fx_media_read</span></span>
- <span data-ttu-id="8b105-2492">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2492">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2493">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2493">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2494">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2494">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2495">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2495">fx_media_write</span></span>
- <span data-ttu-id="8b105-2496">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2496">fx_system_initialize</span></span>

## <a name="fx_media_check"></a><span data-ttu-id="8b105-2497">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2497">fx_media_check</span></span>

<span data-ttu-id="8b105-2498">Medyayı hatalara karşı denetler</span><span class="sxs-lookup"><span data-stu-id="8b105-2498">Checks media for errors</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2499">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2499">Prototype</span></span>

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-2500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2500">Description</span></span>

<span data-ttu-id="8b105-2501">Bu hizmet, dosya/dizin çapraz bağlantı, geçersiz FAT zincirleri ve kayıp kümeler dahil olmak üzere temel yapısal hatalar için belirtilen medyayı denetler.</span><span class="sxs-lookup"><span data-stu-id="8b105-2501">This service checks the specified media for basic structural errors, including file/directory cross-linking, invalid FAT chains, and lost clusters.</span></span> <span data-ttu-id="8b105-2502">Bu hizmet, algılanan hataları düzeltme yeteneği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2502">This service also provides the capability to correct detected errors.</span></span>

<span data-ttu-id="8b105-2503">Fx_media_check hizmeti, ortamdaki dizinlerin ve dosyaların derinlemesine ilk analizi için karalama belleği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2503">The fx_media_check service requires scratch memory for its depth-first analysis of directories and files in the media.</span></span> <span data-ttu-id="8b105-2504">Özellikle, medya denetimi hizmeti için sağlanan karalama belleği, birkaç dizin girişi tutabilecek kadar büyük olmalıdır, alt dizinlere girmeden önce geçerli dizin girişi konumunu "Stack" e bir veri yapısı ve son olarak mantıksal FAT bit eşlem.</span><span class="sxs-lookup"><span data-stu-id="8b105-2504">Specifically, the scratch memory supplied to the media check service must be large enough to hold several directory entries, a data structure to "stack" the current directory entry position before entering into subdirectories, and finally the logical FAT bit map.</span></span> <span data-ttu-id="8b105-2505">Boş bellek, medyada kümeler olduğundan çok sayıda bit olması gereken mantıksal FAT bit eşlem için en az 512-1024 bayt artı bellek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2505">The scratch memory should be at least 512-1024 bytes plus memory for the logical FAT bit map, which requires as many bits as there are clusters in the media.</span></span> <span data-ttu-id="8b105-2506">Örneğin, 8000 kümesi olan bir cihaz için 1000 bayt ve bu nedenle 2048 bayt düzeninde toplam bir karalama alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2506">For example, a device with 8000 clusters would require 1000 bytes to represent and thus require a total scratch area on the order of 2048 bytes.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2507">*Bu hizmet yalnızca fx_media_open ve diğer herhangi bir dosya sistemi etkinliği olmadan hemen çağrılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2507">*This service should only be called immediately after fx_media_open and without any other file system activity.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2508">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2508">Input Parameters</span></span>

- <span data-ttu-id="8b105-2509">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2509">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-2510">**scratch_memory_ptr**: karalama belleğinin başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2510">**scratch_memory_ptr**: Pointer to the start of scratch memory.</span></span>
- <span data-ttu-id="8b105-2511">**scratch_memory_size**: boş belleğin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-2511">**scratch_memory_size**: Size of scratch memory in bytes.</span></span>
- <span data-ttu-id="8b105-2512">**error_correction_option**: hata düzeltme seçeneği bitleri, bit ayarlandığında hata düzeltme gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2512">**error_correction_option**: Error correction option bits, when the bit is set, error correction is performed.</span></span> <span data-ttu-id="8b105-2513">Hata düzeltme seçeneği bitleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8b105-2513">The error correction option bits are defined as follows:</span></span>
  - <span data-ttu-id="8b105-2514">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-2514">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="8b105-2515">FX_DIRECTORY_ERROR (0x02)</span><span class="sxs-lookup"><span data-stu-id="8b105-2515">FX_DIRECTORY_ERROR (0x02)</span></span>
  - <span data-ttu-id="8b105-2516">Gerekli hata düzeltme seçeneklerini yalnızca bir arada FX_LOST_CLUSTER_ERROR (0x04).</span><span class="sxs-lookup"><span data-stu-id="8b105-2516">FX_LOST_CLUSTER_ERROR (0x04) Simply OR together the required error correction options.</span></span> <span data-ttu-id="8b105-2517">Hata düzeltmesi gerekmiyorsa 0 değeri sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2517">If no error correction is required, a value of 0 should be supplied.</span></span>
- <span data-ttu-id="8b105-2518">**errors_detected_ptr**: aşağıda tanımlandığı şekilde hata algılama bitleri için hedef:</span><span class="sxs-lookup"><span data-stu-id="8b105-2518">**errors_detected_ptr**: Destination for error detection bits, as defined below:</span></span>
  - <span data-ttu-id="8b105-2519">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="8b105-2519">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="8b105-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span><span class="sxs-lookup"><span data-stu-id="8b105-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span></span>
  - <span data-ttu-id="8b105-2521">FX_FILE_SIZE_ERROR (0x08)</span><span class="sxs-lookup"><span data-stu-id="8b105-2521">FX_FILE_SIZE_ERROR (0x08)</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2522">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2522">Return Values</span></span>

- <span data-ttu-id="8b105-2523">**FX_SUCCESS** (0x00) başarılı medya denetimi, Ayrıntılar için algılanan hedef hatalarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8b105-2523">**FX_SUCCESS** (0x00) Successful media check, view the errors detected destination for details.</span></span>
- <span data-ttu-id="8b105-2524">**FX_ACCESS_ERROR** (0x06) açık dosyalarla denetim yapılamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-2524">**FX_ACCESS_ERROR** (0x06) Unable to perform check with open files.</span></span>
- <span data-ttu-id="8b105-2525">**FX_FILE_CORRUPT** (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2525">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2526">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2526">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2527">**FX_NO_MORE_SPACE** (0x0A) medyada daha fazla alan yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-2527">**FX_NO_MORE_SPACE** (0x0A) No more space on the media.</span></span>
- <span data-ttu-id="8b105-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) sağlanan karalama belleği yeterince büyük değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) Supplied scratch memory is not large enough.</span></span>
- <span data-ttu-id="8b105-2529">**FX_ERROR_NOT_FIXED** (0x93) DÜZELTILMEYEN FAT32 kök dizininin bozulması.</span><span class="sxs-lookup"><span data-stu-id="8b105-2529">**FX_ERROR_NOT_FIXED** (0x93) Corruption of FAT32 root directory that could not be fixed.</span></span>
- <span data-ttu-id="8b105-2530">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2531">**FX_SECTOR_INVALID** (0x89) kesimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2531">**FX_SECTOR_INVALID** (0x89) Sector is invalid.</span></span>
- <span data-ttu-id="8b105-2532">**FX_PTR_ERROR** (0x18) geçersiz medya veya karalama işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2532">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="8b105-2533">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="8b105-2534">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2534">Allowed From</span></span>

<span data-ttu-id="8b105-2535">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2536">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2536">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-2537">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2537">See Also</span></span>

- <span data-ttu-id="8b105-2538">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2538">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2539">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2539">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2540">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2540">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2541">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2541">fx_media_close</span></span>
- <span data-ttu-id="8b105-2542">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2542">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2543">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2543">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2544">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2544">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2545">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2545">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2546">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2546">fx_media_format</span></span>
- <span data-ttu-id="8b105-2547">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2547">fx_media_open</span></span>
- <span data-ttu-id="8b105-2548">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2548">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2549">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2549">fx_media_read</span></span>
- <span data-ttu-id="8b105-2550">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2550">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2551">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2551">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2552">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2552">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2553">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2553">fx_media_write</span></span>
- <span data-ttu-id="8b105-2554">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2554">fx_system_initialize</span></span>

## <a name="fx_media_close"></a><span data-ttu-id="8b105-2555">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2555">fx_media_close</span></span>

<span data-ttu-id="8b105-2556">Medyayı kapatır</span><span class="sxs-lookup"><span data-stu-id="8b105-2556">Closes media</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2557">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2557">Prototype</span></span>

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-2558">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2558">Description</span></span>

<span data-ttu-id="8b105-2559">Bu hizmet, belirtilen medyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2559">This service closes the specified media.</span></span> <span data-ttu-id="8b105-2560">Medyayı kapatma sürecinde, tüm açık dosyalar kapatılır ve kalan arabellekler fiziksel medyaya silinir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2560">In the process of closing the media, all open files are closed and any remaining buffers are flushed to the physical media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2561">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2561">Input Parameters</span></span>

- <span data-ttu-id="8b105-2562">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2562">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2563">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2563">Return Values</span></span>

- <span data-ttu-id="8b105-2564">**FX_SUCCESS** (0x00) başarılı medya kapatma.</span><span class="sxs-lookup"><span data-stu-id="8b105-2564">**FX_SUCCESS** (0x00) Successful media close.</span></span>
- <span data-ttu-id="8b105-2565">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2565">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2566">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2566">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2567">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2567">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-2568">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2568">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2569">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2569">Allowed From</span></span>

<span data-ttu-id="8b105-2570">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2571">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2571">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2572">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2572">See Also</span></span>

- <span data-ttu-id="8b105-2573">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2573">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2574">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2574">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2575">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2575">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2576">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2576">fx_media_check</span></span>
- <span data-ttu-id="8b105-2577">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2577">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2578">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2578">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2579">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2579">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2580">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2580">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2581">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2581">fx_media_format</span></span>
- <span data-ttu-id="8b105-2582">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2582">fx_media_open</span></span>
- <span data-ttu-id="8b105-2583">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2583">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2584">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2584">fx_media_read</span></span>
- <span data-ttu-id="8b105-2585">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2585">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2586">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2586">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2587">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2587">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2588">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2588">fx_media_write</span></span>
- <span data-ttu-id="8b105-2589">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2589">fx_system_initialize</span></span>

## <a name="fx_media_close_notify_set"></a><span data-ttu-id="8b105-2590">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2590">fx_media_close_notify_set</span></span>

<span data-ttu-id="8b105-2591">Medya kapatma bildirimi işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-2591">Sets the media close notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2592">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2592">Prototype</span></span>

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a><span data-ttu-id="8b105-2593">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2593">Description</span></span>

<span data-ttu-id="8b105-2594">Bu hizmet, bir medya başarıyla kapatıldıktan sonra çağrılacak bir bildirim geri arama işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2594">This service sets a notify callback function which will be invoked after a media is successfully closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2595">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2595">Input Parameters</span></span>

- <span data-ttu-id="8b105-2596">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2596">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-2597">**media_close_notify**: medya kapatma geri arama işlevi yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="8b105-2597">**media_close_notify**: Media close notify callback function to be installed.</span></span> <span data-ttu-id="8b105-2598">Geri çağırma işlevi olarak NULL geçirme, medya kapatma geri aramasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2598">Passing NULL as the callback function disables the media close callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2599">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2599">Return Values</span></span>

- <span data-ttu-id="8b105-2600">**FX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2600">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="8b105-2601">**FX_PTR_ERROR** (0x18) media_ptr null.</span><span class="sxs-lookup"><span data-stu-id="8b105-2601">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="8b105-2602">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2602">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2603">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2603">Allowed From</span></span>

<span data-ttu-id="8b105-2604">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2604">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2605">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2605">Example</span></span>

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a><span data-ttu-id="8b105-2606">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2606">See Also</span></span>

- <span data-ttu-id="8b105-2607">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2607">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2608">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2608">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2609">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2609">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2610">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2610">fx_media_check</span></span>
- <span data-ttu-id="8b105-2611">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2611">fx_media_close</span></span>
- <span data-ttu-id="8b105-2612">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2612">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2613">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2613">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2614">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2614">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2615">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2615">fx_media_format</span></span>
- <span data-ttu-id="8b105-2616">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2616">fx_media_open</span></span>
- <span data-ttu-id="8b105-2617">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2617">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2618">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2618">fx_media_read</span></span>
- <span data-ttu-id="8b105-2619">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2619">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2620">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2620">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2621">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2621">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2622">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2622">fx_media_write</span></span>
- <span data-ttu-id="8b105-2623">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2623">fx_system_initialize</span></span>

## <a name="fx_media_exfat_format"></a><span data-ttu-id="8b105-2624">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2624">fx_media_exFAT_format</span></span>

<span data-ttu-id="8b105-2625">Medyayı biçimlendirir</span><span class="sxs-lookup"><span data-stu-id="8b105-2625">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2626">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2626">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="8b105-2627">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2627">Description</span></span>

<span data-ttu-id="8b105-2628">Bu hizmet verilen medyayı sağlanan parametrelere göre exFAT ile uyumlu bir şekilde biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2628">This service formats the supplied media in an exFAT compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="8b105-2629">Medyayı açmadan önce bu hizmetin çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2629">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2630">*Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2630">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2631">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2631">Input Parameters</span></span>

- <span data-ttu-id="8b105-2632">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2632">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="8b105-2633">Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2633">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="8b105-2634">**sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2634">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="8b105-2635">Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2635">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="8b105-2636">**driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2636">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="8b105-2637">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2637">**memory_ptr**: Pointer to the working memory for the media.</span></span> <span data-ttu-id="8b105-2638">memory_size, çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2638">memory_size Specifies the size of the working media memory.</span></span> <span data-ttu-id="8b105-2639">Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2639">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="8b105-2640">**Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2640">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="8b105-2641">**number_of_fats**: medyadaki Fats sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2641">**number_of_fats**: Number of FATs on the media.</span></span> <span data-ttu-id="8b105-2642">Geçerli uygulama, medyada bir FAT 'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="8b105-2642">Current implementation supports one FAT on the media.</span></span>
- <span data-ttu-id="8b105-2643">**hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2643">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="8b105-2644">Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2644">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="8b105-2645">**total_sectors**: medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2645">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="8b105-2646">**bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2646">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="8b105-2647">FileX, bunun 32 katı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2647">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="8b105-2648">**sectors_per_cluster**: her kümedeki sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2648">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="8b105-2649">Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2649">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="8b105-2650">**volumne_serial_number**: Bu birim için kullanılacak seri numarası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2650">**volumne_serial_number**: Serial number to be used for this volume.</span></span>
- <span data-ttu-id="8b105-2651">**boundary_unit**: fiziksel veri alanı hizalama boyutu, kesim sayısı olarak.</span><span class="sxs-lookup"><span data-stu-id="8b105-2651">**boundary_unit**: Physical data area alignment size, in number of sectors.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2652">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2652">Return Values</span></span>

- <span data-ttu-id="8b105-2653">**FX_SUCCESS** (0x00) başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2653">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="8b105-2654">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2654">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2655">**FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2655">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="8b105-2656">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2656">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2657">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2657">Allowed From</span></span>

<span data-ttu-id="8b105-2658">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2658">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2659">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2659">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-2660">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2660">See Also</span></span>

- <span data-ttu-id="8b105-2661">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2661">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2662">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2662">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2663">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2663">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2664">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2664">fx_media_check</span></span>
- <span data-ttu-id="8b105-2665">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2665">fx_media_close</span></span>
- <span data-ttu-id="8b105-2666">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2666">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2667">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2667">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2668">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2668">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2669">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2669">fx_media_format</span></span>
- <span data-ttu-id="8b105-2670">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2670">fx_media_open</span></span>
- <span data-ttu-id="8b105-2671">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2671">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2672">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2672">fx_media_read</span></span>
- <span data-ttu-id="8b105-2673">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2673">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2674">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2674">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2675">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2675">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2676">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2676">fx_media_write</span></span>
- <span data-ttu-id="8b105-2677">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2677">fx_system_initialize</span></span>

## <a name="fx_media_extended_space_available"></a><span data-ttu-id="8b105-2678">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2678">fx_media_extended_space_available</span></span>

<span data-ttu-id="8b105-2679">Kullanılabilir medya alanını döndürür</span><span class="sxs-lookup"><span data-stu-id="8b105-2679">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2680">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2680">Prototype</span></span>

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-2681">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2681">Description</span></span>

<span data-ttu-id="8b105-2682">Bu hizmet, medyada kullanılabilir olan bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b105-2682">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="8b105-2683">Bu hizmet, exFAT için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2683">This service is designed for exFAT.</span></span> <span data-ttu-id="8b105-2684">*Available_bytes* parametresi işaretçisi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 ' ün üzerinde medya ile çalışmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2684">The pointer to *available_bytes* parameter takes a 64-bit integer value, which allows the caller to work with media beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2685">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2685">Input Parameters</span></span>

- <span data-ttu-id="8b105-2686">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2686">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8b105-2687">**available_bytes_ptr**: medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2687">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2688">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2688">Return Values</span></span>

- <span data-ttu-id="8b105-2689">**FX_SUCCESS** (0x00) medyada bulunan alanı başarıyla aldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2689">**FX_SUCCESS** (0x00) Successfully retrieved space available on the media.</span></span>
- <span data-ttu-id="8b105-2690">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2690">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2691">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi null.</span><span class="sxs-lookup"><span data-stu-id="8b105-2691">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="8b105-2692">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2692">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2693">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2693">Allowed From</span></span>

<span data-ttu-id="8b105-2694">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2694">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2695">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2695">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2696">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2696">See Also</span></span>

- <span data-ttu-id="8b105-2697">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2697">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2698">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2698">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2699">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2699">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2700">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2700">fx_media_check</span></span>
- <span data-ttu-id="8b105-2701">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2701">fx_media_close</span></span>
- <span data-ttu-id="8b105-2702">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2702">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2703">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2703">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2704">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2704">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2705">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2705">fx_media_format</span></span>
- <span data-ttu-id="8b105-2706">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2706">fx_media_open</span></span>
- <span data-ttu-id="8b105-2707">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2707">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2708">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2708">fx_media_read</span></span>
- <span data-ttu-id="8b105-2709">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2709">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2710">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2710">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2711">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2711">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2712">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2712">fx_media_write</span></span>
- <span data-ttu-id="8b105-2713">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2713">fx_system_initialize</span></span>

## <a name="fx_media_flush"></a><span data-ttu-id="8b105-2714">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2714">fx_media_flush</span></span>

<span data-ttu-id="8b105-2715">Fiziksel medyada verileri boşaltır</span><span class="sxs-lookup"><span data-stu-id="8b105-2715">Flushes data to physical media</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2716">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2716">Prototype</span></span>

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-2717">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2717">Description</span></span>

<span data-ttu-id="8b105-2718">Bu hizmet, herhangi bir değiştirilen dosyanın tüm önbelleğe alınan kesimlerini ve dizin girdilerini fiziksel medyada boşaltır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2718">This service flushes all cached sectors and directory entries of any modified files to the physical media.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2719">*Bu yordam, hedef üzerinde ani bir güç kaybı olması durumunda dosya bozulması ve/veya veri kaybı riskini azaltmak için uygulama tarafından düzenli aralıklarla çağrılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2719">*This routine may be called periodically by the application to reduce the risk of file corruption and/or data loss in the event of a sudden loss of power on the target.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2720">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2720">Input Parameters</span></span>

- <span data-ttu-id="8b105-2721">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2721">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2722">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2722">Return Values</span></span>

- <span data-ttu-id="8b105-2723">**FX_SUCCESS** (0x00) başarılı medya Temizleme.</span><span class="sxs-lookup"><span data-stu-id="8b105-2723">**FX_SUCCESS** (0x00) Successful media flush.</span></span>
- <span data-ttu-id="8b105-2724">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2724">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2725">**FX_FILE_CORRUPT**    (0x08) dosyası bozuk.</span><span class="sxs-lookup"><span data-stu-id="8b105-2725">**FX_FILE_CORRUPT**    (0x08) File is corrupted.</span></span>
- <span data-ttu-id="8b105-2726">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2726">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2727">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2727">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2728">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2728">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-2729">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2729">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-2730">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2730">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2731">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2731">Allowed From</span></span>

<span data-ttu-id="8b105-2732">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2733">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2733">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2734">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2734">See Also</span></span>

- <span data-ttu-id="8b105-2735">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2735">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2736">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2736">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2737">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2737">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2738">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2738">fx_media_check</span></span>
- <span data-ttu-id="8b105-2739">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2739">fx_media_close</span></span>
- <span data-ttu-id="8b105-2740">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2740">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2741">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2741">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2742">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2742">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2743">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2743">fx_media_format</span></span>
- <span data-ttu-id="8b105-2744">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2744">fx_media_open</span></span>
- <span data-ttu-id="8b105-2745">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2745">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2746">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2746">fx_media_read</span></span>
- <span data-ttu-id="8b105-2747">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2747">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2748">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2748">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2749">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2749">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2750">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2750">fx_media_write</span></span>
- <span data-ttu-id="8b105-2751">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2751">fx_system_initialize</span></span>

## <a name="fx_media_format"></a><span data-ttu-id="8b105-2752">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2752">fx_media_format</span></span>

<span data-ttu-id="8b105-2753">Medyayı biçimlendirir</span><span class="sxs-lookup"><span data-stu-id="8b105-2753">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2754">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2754">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="8b105-2755">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2755">Description</span></span>

<span data-ttu-id="8b105-2756">Bu hizmet verilen medyayı sağlanan parametrelere göre FAT 12/16/32 ile uyumlu bir şekilde biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2756">This service formats the supplied media in a FAT 12/16/32 compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="8b105-2757">Medyayı açmadan önce bu hizmetin çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2757">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2758">*Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2758">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2759">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2759">Input Parameters</span></span>

- <span data-ttu-id="8b105-2760">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2760">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="8b105-2761">Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2761">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="8b105-2762">**sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2762">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="8b105-2763">Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2763">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="8b105-2764">**driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2764">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="8b105-2765">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2765">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="8b105-2766">**memory_size**: çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2766">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="8b105-2767">Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2767">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="8b105-2768">**Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2768">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="8b105-2769">**number_of_fats**: medyadaki Fats sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2769">**number_of_fats**: Number of FATs in the media.</span></span> <span data-ttu-id="8b105-2770">Birincil FAT için en düşük değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2770">The minimal value is 1 for the primary FAT.</span></span> <span data-ttu-id="8b105-2771">1 ' den büyük değerler, çalışma zamanında sürdürülmekte olan ek FAT kopyalarla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2771">Values greater than 1 result in additional FAT copies being maintained at run-time.</span></span>
- <span data-ttu-id="8b105-2772">**directory_entries**: kök dizindeki Dizin girişi sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2772">**directory_entries**: Number of directory entries in the root directory.</span></span>
- <span data-ttu-id="8b105-2773">**hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2773">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="8b105-2774">Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2774">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="8b105-2775">**total_sectors**: medyadaki toplam kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2775">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="8b105-2776">**bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2776">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="8b105-2777">FileX, bunun 32 katı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2777">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="8b105-2778">**sectors_per_cluster**: her kümedeki sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2778">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="8b105-2779">Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2779">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="8b105-2780">**Heads**: fiziksel kafa sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2780">**heads**: Number of physical heads.</span></span>
- <span data-ttu-id="8b105-2781">**sectors_per_track**: iz başına kesim sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2781">**sectors_per_track**: Number of sectors per track.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2782">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2782">Return Values</span></span>

- <span data-ttu-id="8b105-2783">**FX_SUCCESS** (0x00) başarılı medya biçimi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2783">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="8b105-2784">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2784">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2785">**FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2785">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="8b105-2786">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2786">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2787">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2787">Allowed From</span></span>

<span data-ttu-id="8b105-2788">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2788">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2789">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2789">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-2790">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2790">See Also</span></span>

- <span data-ttu-id="8b105-2791">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2791">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2792">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2792">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2793">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2793">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2794">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2794">fx_media_check</span></span>
- <span data-ttu-id="8b105-2795">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2795">fx_media_close</span></span>
- <span data-ttu-id="8b105-2796">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2796">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2797">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2797">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2798">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2798">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2799">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2799">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2800">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2800">fx_media_open</span></span>
- <span data-ttu-id="8b105-2801">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2801">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2802">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2802">fx_media_read</span></span>
- <span data-ttu-id="8b105-2803">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2803">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2804">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2804">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2805">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2805">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2806">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2806">fx_media_write</span></span>
- <span data-ttu-id="8b105-2807">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2807">fx_system_initialize</span></span>

## <a name="fx_media_open"></a><span data-ttu-id="8b105-2808">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2808">fx_media_open</span></span>

<span data-ttu-id="8b105-2809">Dosya erişimi için medyayı açar</span><span class="sxs-lookup"><span data-stu-id="8b105-2809">Opens media for file access</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2810">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2810">Prototype</span></span>

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a><span data-ttu-id="8b105-2811">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2811">Description</span></span>

<span data-ttu-id="8b105-2812">Bu hizmet, sağlanan g/ç sürücüsünü kullanarak dosya erişimi için bir medya açar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2812">This service opens a media for file access using the supplied I/O driver.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-2813">*Bu hizmete sağlanan bellek, bir iç mantıksal kesim önbelleğinin uygulanması için kullanılır, bu nedenle, daha fazla fiziksel g/ç daha fazla bellek azaltılır. FileX, en az bir mantıksal kesim (medyanın kesim başına bayt) için bir önbellek gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-2813">*The memory supplied to this service is used to implement an internal logical sector cache, hence, the more memory supplied the more physical I/O is reduced. FileX requires a cache of at least one logical sector (bytes per sector of the media).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2814">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2814">Input Parameters</span></span>

- <span data-ttu-id="8b105-2815">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2815">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-2816">**media_name**: medya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2816">**media_name**: Pointer to media's name.</span></span>
- <span data-ttu-id="8b105-2817">**media_driver**: Bu ortam için g/ç sürücüsü işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2817">**media_driver**: Pointer to I/O driver for this media.</span></span> <span data-ttu-id="8b105-2818">G/ç sürücüsü, Bölüm 5 ' te tanımlanan FileX sürücü gereksinimleriyle uyumlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2818">The I/O driver must conform to FileX driver requirements defined in Chapter 5.</span></span>
- <span data-ttu-id="8b105-2819">**driver_info_ptr**: sağlanan g/ç sürücüsünün yararlanabilecek isteğe bağlı bilgiler için işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2819">**driver_info_ptr**: Pointer to optional information that the supplied I/O driver may utilize.</span></span>
- <span data-ttu-id="8b105-2820">**memory_ptr**: medya için çalışma belleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2820">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="8b105-2821">**memory_size**: çalışma medyası belleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2821">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="8b105-2822">Boyut, medyanın kesim boyutu (genellikle 512 bayt) kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2822">The size must be as large as the media's sector size (typically 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2823">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2823">Return Values</span></span>

- <span data-ttu-id="8b105-2824">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2824">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="8b105-2825">Medyanın önyükleme kesimini okurken hata **FX_BOOT_ERROR** (0x01).</span><span class="sxs-lookup"><span data-stu-id="8b105-2825">**FX_BOOT_ERROR** (0x01) Error reading the media's boot sector.</span></span>
- <span data-ttu-id="8b105-2826">**FX_MEDIA_INVALID** (0x02) belirtilen medyanın önyükleme kesimi bozuk veya geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2826">**FX_MEDIA_INVALID** (0x02) Specified media's boot sector is corrupt or invalid.</span></span> <span data-ttu-id="8b105-2827">Ayrıca, bu dönüş kodu, mantıksal kesim önbelleğinin boyutunun veya FAT giriş boyutunun 2 ' nin üssü olduğunu göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2827">In addition, this return code is used to indicate that either the logical sector cache size or the FAT entry size is not a power of 2.</span></span>
- <span data-ttu-id="8b105-2828">**FX_FAT_READ_ERROR** (0x03) FAT medyayı okunurken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8b105-2828">**FX_FAT_READ_ERROR** (0x03) Error reading the media FAT.</span></span>
- <span data-ttu-id="8b105-2829">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2829">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2830">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="8b105-2830">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="8b105-2831">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2831">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2832">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2832">Allowed From</span></span>

<span data-ttu-id="8b105-2833">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2833">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2834">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2834">Example</span></span>

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2835">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2835">See Also</span></span>

- <span data-ttu-id="8b105-2836">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2836">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2837">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2837">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2838">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2838">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2839">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2839">fx_media_check</span></span>
- <span data-ttu-id="8b105-2840">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2840">fx_media_close</span></span>
- <span data-ttu-id="8b105-2841">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2841">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2842">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2842">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2843">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2843">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2844">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2844">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2845">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2845">fx_media_format</span></span>
- <span data-ttu-id="8b105-2846">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2846">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2847">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2847">fx_media_read</span></span>
- <span data-ttu-id="8b105-2848">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2848">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2849">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2849">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2850">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2850">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2851">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2851">fx_media_write</span></span>
- <span data-ttu-id="8b105-2852">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2852">fx_system_initialize</span></span>

## <a name="fx_media_open_notify_set"></a><span data-ttu-id="8b105-2853">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2853">fx_media_open_notify_set</span></span>

<span data-ttu-id="8b105-2854">Medya açma bildirim işlevini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-2854">Sets the media open notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2855">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2855">Prototype</span></span>

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a><span data-ttu-id="8b105-2856">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2856">Description</span></span>

<span data-ttu-id="8b105-2857">Bu hizmet, bir medya başarıyla açıldıktan sonra çağrılacak bir bildirim geri arama işlevi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2857">This service sets a notify callback function which will be invoked after a media is successfully opened.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2858">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2858">Input Parameters</span></span>

- <span data-ttu-id="8b105-2859">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2859">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-2860">**media_open_notify**: medya açmak için geri arama bildirme işlevini açın.</span><span class="sxs-lookup"><span data-stu-id="8b105-2860">**media_open_notify**: Media open notify callback function to be installed.</span></span> <span data-ttu-id="8b105-2861">Geri çağırma işlevi olarak NULL geçirme, medya açma geri aramasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2861">Passing NULL as the callback function disables the media open callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2862">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2862">Return Values</span></span>


- <span data-ttu-id="8b105-2863">**FX_SUCCESS** (0x00) geri çağırma işlevini başarıyla yükledi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2863">**FX_SUCCESS** (0x00) Successfuly installed the callback function.</span></span>
- <span data-ttu-id="8b105-2864">**FX_PTR_ERROR** (0x18) media_ptr null.</span><span class="sxs-lookup"><span data-stu-id="8b105-2864">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="8b105-2865">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2865">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2866">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2866">Allowed From</span></span>

<span data-ttu-id="8b105-2867">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2867">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2868">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2868">Example</span></span>

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a><span data-ttu-id="8b105-2869">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2869">See Also</span></span>

- <span data-ttu-id="8b105-2870">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2870">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2871">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2871">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2872">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2872">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2873">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2873">fx_media_check</span></span>
- <span data-ttu-id="8b105-2874">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2874">fx_media_close</span></span>
- <span data-ttu-id="8b105-2875">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2875">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2876">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2876">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2877">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2877">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2878">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2878">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2879">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2879">fx_media_format</span></span>
- <span data-ttu-id="8b105-2880">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2880">fx_media_open</span></span>
- <span data-ttu-id="8b105-2881">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2881">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2882">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2882">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2883">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2883">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2884">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2884">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2885">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2885">fx_media_write</span></span>
- <span data-ttu-id="8b105-2886">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2886">fx_system_initialize</span></span>

## <a name="fx_media_read"></a><span data-ttu-id="8b105-2887">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2887">fx_media_read</span></span>

<span data-ttu-id="8b105-2888">Medyadan mantıksal kesim okur</span><span class="sxs-lookup"><span data-stu-id="8b105-2888">Reads logical sector from media</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2889">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2889">Prototype</span></span>

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-2890">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2890">Description</span></span>

<span data-ttu-id="8b105-2891">Bu hizmet, medyadan bir mantıksal kesim okur ve sağlanan arabelleğe koyar.</span><span class="sxs-lookup"><span data-stu-id="8b105-2891">This service reads a logical sector from the media and places it into the supplied buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2892">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2892">Input Parameters</span></span>

- <span data-ttu-id="8b105-2893">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2893">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8b105-2894">**logical_sector**: okunacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2894">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="8b105-2895">**buffer_ptr**: mantıksal kesime okunan hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2895">**buffer_ptr**: Pointer to the destination for the logical sector read.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2896">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2896">Return Values</span></span>

- <span data-ttu-id="8b105-2897">**FX_SUCCESS** (0x00) başarılı medya okuma.</span><span class="sxs-lookup"><span data-stu-id="8b105-2897">**FX_SUCCESS** (0x00) Successful media read.</span></span>
- <span data-ttu-id="8b105-2898">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2898">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2899">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2899">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2900">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-2900">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-2901">**FX_PTR_ERROR** (0x18) geçersiz medya veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2901">**FX_PTR_ERROR** (0x18) Invalid media or buffer pointer.</span></span>
- <span data-ttu-id="8b105-2902">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2902">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2903">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2903">Allowed From</span></span>

<span data-ttu-id="8b105-2904">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2904">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2905">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2905">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a><span data-ttu-id="8b105-2906">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2906">See Also</span></span>

- <span data-ttu-id="8b105-2907">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2907">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2908">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2908">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2909">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2909">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2910">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2910">fx_media_check</span></span>
- <span data-ttu-id="8b105-2911">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2911">fx_media_close</span></span>
- <span data-ttu-id="8b105-2912">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2912">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2913">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2913">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2914">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2914">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2915">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2915">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2916">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2916">fx_media_format</span></span>
- <span data-ttu-id="8b105-2917">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2917">fx_media_open</span></span>
- <span data-ttu-id="8b105-2918">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2918">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2919">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2919">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2920">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2920">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2921">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2921">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2922">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2922">fx_media_write</span></span>
- <span data-ttu-id="8b105-2923">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2923">fx_system_initialize</span></span>

## <a name="fx_media_space_available"></a><span data-ttu-id="8b105-2924">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2924">fx_media_space_available</span></span>

<span data-ttu-id="8b105-2925">Kullanılabilir medya alanını döndürür</span><span class="sxs-lookup"><span data-stu-id="8b105-2925">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2926">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2926">Prototype</span></span>

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a><span data-ttu-id="8b105-2927">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2927">Description</span></span>

<span data-ttu-id="8b105-2928">Bu hizmet, medyada kullanılabilir olan bayt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b105-2928">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="8b105-2929">4 GB 'den büyük medyayla çalışmak için, uygulama Service *fx_media_extended_space_available* kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2929">To work with the media larger than 4GB, application shall use the service *fx_media_extended_space_available*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2930">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2930">Input Parameters</span></span>

- <span data-ttu-id="8b105-2931">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2931">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8b105-2932">**available_bytes_ptr**: medyada kalan kullanılabilir bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2932">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2933">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2933">Return Values</span></span>

- <span data-ttu-id="8b105-2934">**FX_SUCCESS** (0x00) medyada kullanılabilir alanı başarıyla döndürdü.</span><span class="sxs-lookup"><span data-stu-id="8b105-2934">**FX_SUCCESS** (0x00) Successfully returned available space on media.</span></span>
- <span data-ttu-id="8b105-2935">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2935">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2936">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi null.</span><span class="sxs-lookup"><span data-stu-id="8b105-2936">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="8b105-2937">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2937">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2938">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2938">Allowed From</span></span>

<span data-ttu-id="8b105-2939">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2939">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2940">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2940">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2941">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2941">See Also</span></span>

- <span data-ttu-id="8b105-2942">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2942">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2943">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2943">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2944">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2944">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2945">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2945">fx_media_check</span></span>
- <span data-ttu-id="8b105-2946">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2946">fx_media_close</span></span>
- <span data-ttu-id="8b105-2947">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2947">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2948">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2948">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2949">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2949">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2950">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2950">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2951">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2951">fx_media_format</span></span>
- <span data-ttu-id="8b105-2952">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2952">fx_media_open</span></span>
- <span data-ttu-id="8b105-2953">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2953">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2954">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2954">fx_media_read</span></span>
- <span data-ttu-id="8b105-2955">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2955">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-2956">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2956">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2957">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2957">fx_media_write</span></span>
- <span data-ttu-id="8b105-2958">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2958">fx_system_initialize</span></span>

## <a name="fx_media_volume_get"></a><span data-ttu-id="8b105-2959">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-2959">fx_media_volume_get</span></span>

<span data-ttu-id="8b105-2960">Medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="8b105-2960">Gets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-2961">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-2961">Prototype</span></span>

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="8b105-2962">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-2962">Description</span></span>

<span data-ttu-id="8b105-2963">Bu hizmet, daha önce açılmış medyanın birim adını alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-2963">This service retrieves the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-2964">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2964">Input Parameters</span></span>

- <span data-ttu-id="8b105-2965">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2965">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-2966">**Volume_Name**: birim adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2966">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="8b105-2967">Hedefin en az 12 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b105-2967">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="8b105-2968">**volume_source**: önyükleme kesiminden veya kök dizinden adın nereden alındığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b105-2968">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="8b105-2969">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8b105-2969">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="8b105-2970">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8b105-2970">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="8b105-2971">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8b105-2971">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-2972">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-2972">Return Values</span></span>

- <span data-ttu-id="8b105-2973">**FX_SUCCESS** (0x00) başarılı medya birimi al.</span><span class="sxs-lookup"><span data-stu-id="8b105-2973">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="8b105-2974">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2974">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-2975">**FX_NOT_FOUND** (0x04) birim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-2975">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="8b105-2976">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-2976">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-2977">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-2977">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="8b105-2978">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-2978">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-2979">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-2979">Allowed From</span></span>

<span data-ttu-id="8b105-2980">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-2980">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-2981">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-2981">Example</span></span>

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a><span data-ttu-id="8b105-2982">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-2982">See Also</span></span>

- <span data-ttu-id="8b105-2983">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-2983">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-2984">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-2984">fx_media_abort</span></span>
- <span data-ttu-id="8b105-2985">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-2985">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-2986">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-2986">fx_media_check</span></span>
- <span data-ttu-id="8b105-2987">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-2987">fx_media_close</span></span>
- <span data-ttu-id="8b105-2988">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2988">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-2989">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2989">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-2990">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2990">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-2991">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-2991">fx_media_flush</span></span>
- <span data-ttu-id="8b105-2992">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-2992">fx_media_format</span></span>
- <span data-ttu-id="8b105-2993">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-2993">fx_media_open</span></span>
- <span data-ttu-id="8b105-2994">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2994">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-2995">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-2995">fx_media_read</span></span>
- <span data-ttu-id="8b105-2996">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-2996">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-2997">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-2997">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-2998">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-2998">fx_media_write</span></span>
- <span data-ttu-id="8b105-2999">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-2999">fx_system_initialize</span></span>

## <a name="fx_media_volume_get_extended"></a><span data-ttu-id="8b105-3000">fx_media_volume_get_extended</span><span class="sxs-lookup"><span data-stu-id="8b105-3000">fx_media_volume_get_extended</span></span>

<span data-ttu-id="8b105-3001">Daha önce açılmış medyanın medya birimi adını alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3001">Gets media volume name of previously opened media</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3002">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3002">Prototype</span></span>

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="8b105-3003">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3003">Description</span></span>

<span data-ttu-id="8b105-3004">Bu hizmet, daha önce açılmış medyanın birim adını alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3004">This service retrieves the volume name of the previously opened media.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3005">Bu hizmet, çağıran _ *Volume_Name*\* arabelleğinin boyutunda geçtiği sürece \***fx_media_volume_get ()** _ ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3005">This service is identical to ***fx_media_volume_get()** _ except the caller passes in the size of the _ *volume_name** buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3006">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3006">Input Parameters</span></span>


- <span data-ttu-id="8b105-3007">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3007">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3008">**Volume_Name**: birim adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3008">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="8b105-3009">Hedefin en az 12 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b105-3009">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="8b105-3010">**volume_name_buffer_length**: Volume_Name arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3010">**volume_name_buffer_length**: Size of volume_name buffer.</span></span>
- <span data-ttu-id="8b105-3011">**volume_source**: önyükleme kesiminden veya kök dizinden adın nereden alındığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3011">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="8b105-3012">Bu parametre için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8b105-3012">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="8b105-3013">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8b105-3013">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="8b105-3014">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="8b105-3014">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3015">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3015">Return Values</span></span>

- <span data-ttu-id="8b105-3016">**FX_SUCCESS** (0x00) başarılı medya birimi al.</span><span class="sxs-lookup"><span data-stu-id="8b105-3016">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="8b105-3017">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3017">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3018">**FX_NOT_FOUND** (0x04) birim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3018">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="8b105-3019">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3019">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3020">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3020">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="8b105-3021">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3021">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3022">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3022">Allowed From</span></span>

<span data-ttu-id="8b105-3023">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3023">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3024">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3024">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-3025">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3025">See Also</span></span>

- <span data-ttu-id="8b105-3026">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-3026">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-3027">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-3027">fx_media_abort</span></span>
- <span data-ttu-id="8b105-3028">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-3028">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-3029">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-3029">fx_media_check</span></span>
- <span data-ttu-id="8b105-3030">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3030">fx_media_close</span></span>
- <span data-ttu-id="8b105-3031">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3031">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-3032">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-3032">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-3033">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-3033">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-3034">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-3034">fx_media_flush</span></span>
- <span data-ttu-id="8b105-3035">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-3035">fx_media_format</span></span>
- <span data-ttu-id="8b105-3036">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3036">fx_media_open</span></span>
- <span data-ttu-id="8b105-3037">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3037">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-3038">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3038">fx_media_read</span></span>
- <span data-ttu-id="8b105-3039">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-3039">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-3040">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3040">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-3041">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3041">fx_media_write</span></span>
- <span data-ttu-id="8b105-3042">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3042">fx_system_initialize</span></span>

## <a name="fx_media_volume_set"></a><span data-ttu-id="8b105-3043">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3043">fx_media_volume_set</span></span>

<span data-ttu-id="8b105-3044">Medya birimi adını ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-3044">Sets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3045">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3045">Prototype</span></span>

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a><span data-ttu-id="8b105-3046">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3046">Description</span></span>

<span data-ttu-id="8b105-3047">Bu hizmet, daha önce açılmış medyanın birim adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-3047">This service sets the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3048">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3048">Input Parameters</span></span>

- <span data-ttu-id="8b105-3049">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3049">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3050">**Volume_Name**: birim adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3050">**volume_name**: Pointer to the volume name.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3051">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3051">Return Values</span></span>

- <span data-ttu-id="8b105-3052">**FX_SUCCESS** (0x00) başarılı medya birimi kümesi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3052">**FX_SUCCESS** (0x00) Successful media volume set.</span></span>
- <span data-ttu-id="8b105-3053">**FX_INVALID_NAME** (0x0C) Volume_name geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3053">**FX_INVALID_NAME** (0x0C) Volume_name is invalid.</span></span>
- <span data-ttu-id="8b105-3054">**FX_MEDIA_INVALID** (0x02) birim adı ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-3054">**FX_MEDIA_INVALID** (0x02) Unable to set volume name.</span></span>
- <span data-ttu-id="8b105-3055">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3055">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3056">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3056">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3057">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3057">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-3058">**FX_PTR_ERROR** (0x18) geçersiz medya veya birim adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3058">**FX_PTR_ERROR** (0x18) Invalid media or volume name pointer.</span></span>
- <span data-ttu-id="8b105-3059">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3059">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3060">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3060">Allowed From</span></span>

<span data-ttu-id="8b105-3061">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3061">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3062">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3062">Example</span></span>

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-3063">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3063">See Also</span></span>

- <span data-ttu-id="8b105-3064">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-3064">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-3065">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-3065">fx_media_abort</span></span>
- <span data-ttu-id="8b105-3066">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-3066">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-3067">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-3067">fx_media_check</span></span>
- <span data-ttu-id="8b105-3068">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3068">fx_media_close</span></span>
- <span data-ttu-id="8b105-3069">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3069">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-3070">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-3070">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-3071">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-3071">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-3072">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-3072">fx_media_flush</span></span>
- <span data-ttu-id="8b105-3073">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-3073">fx_media_format</span></span>
- <span data-ttu-id="8b105-3074">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3074">fx_media_open</span></span>
- <span data-ttu-id="8b105-3075">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3075">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-3076">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3076">fx_media_read</span></span>
- <span data-ttu-id="8b105-3077">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-3077">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-3078">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3078">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-3079">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3079">fx_media_write</span></span>
- <span data-ttu-id="8b105-3080">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3080">fx_system_initialize</span></span>

## <a name="fx_media_write"></a><span data-ttu-id="8b105-3081">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3081">fx_media_write</span></span>

<span data-ttu-id="8b105-3082">Mantıksal kesimi yazar</span><span class="sxs-lookup"><span data-stu-id="8b105-3082">Writes logical sector</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3083">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3083">Prototype</span></span>

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="8b105-3084">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3084">Description</span></span>

<span data-ttu-id="8b105-3085">Bu hizmet verilen arabelleği belirtilen mantıksal kesime yazar.</span><span class="sxs-lookup"><span data-stu-id="8b105-3085">This service writes the supplied buffer to the specified logical sector.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3086">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3086">Input Parameters</span></span>

- <span data-ttu-id="8b105-3087">**media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3087">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="8b105-3088">**logical_sector**: yazılacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-3088">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="8b105-3089">**buffer_ptr**: mantıksal kesim yazma için kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3089">**buffer_ptr**: Pointer to the source for the logical sector write.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3090">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3090">Return Values</span></span>

- <span data-ttu-id="8b105-3091">**FX_SUCCESS** (0x00) başarılı medya yazma.</span><span class="sxs-lookup"><span data-stu-id="8b105-3091">**FX_SUCCESS** (0x00) Successful media write.</span></span>
- <span data-ttu-id="8b105-3092">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3092">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3093">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-3093">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-3094">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3094">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3095">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3095">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-3096">**FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3096">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="8b105-3097">**FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3097">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3098">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3098">Allowed From</span></span>

<span data-ttu-id="8b105-3099">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3099">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3100">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3100">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3101">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3101">See Also</span></span>

- <span data-ttu-id="8b105-3102">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="8b105-3102">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="8b105-3103">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="8b105-3103">fx_media_abort</span></span>
- <span data-ttu-id="8b105-3104">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="8b105-3104">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="8b105-3105">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="8b105-3105">fx_media_check</span></span>
- <span data-ttu-id="8b105-3106">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3106">fx_media_close</span></span>
- <span data-ttu-id="8b105-3107">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3107">fx_media_close_notify_set</span></span>
- <span data-ttu-id="8b105-3108">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="8b105-3108">fx_media_exFAT_format</span></span>
- <span data-ttu-id="8b105-3109">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-3109">fx_media_extended_space_available</span></span>
- <span data-ttu-id="8b105-3110">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="8b105-3110">fx_media_flush</span></span>
- <span data-ttu-id="8b105-3111">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="8b105-3111">fx_media_format</span></span>
- <span data-ttu-id="8b105-3112">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3112">fx_media_open</span></span>
- <span data-ttu-id="8b105-3113">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3113">fx_media_open_notify_set</span></span>
- <span data-ttu-id="8b105-3114">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3114">fx_media_read</span></span>
- <span data-ttu-id="8b105-3115">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="8b105-3115">fx_media_space_available</span></span>
- <span data-ttu-id="8b105-3116">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3116">fx_media_volume_get</span></span>
- <span data-ttu-id="8b105-3117">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3117">fx_media_volume_set</span></span>
- <span data-ttu-id="8b105-3118">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3118">fx_system_initialize</span></span>

## <a name="fx_system_date_get"></a><span data-ttu-id="8b105-3119">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3119">fx_system_date_get</span></span>

<span data-ttu-id="8b105-3120">Dosya sistemi tarihini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3120">Gets file system date</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3121">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3121">Prototype</span></span>

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a><span data-ttu-id="8b105-3122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3122">Description</span></span>

<span data-ttu-id="8b105-3123">Bu hizmet, geçerli sistem tarihini döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b105-3123">This service returns the current system date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3124">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3124">Input Parameters</span></span>

- <span data-ttu-id="8b105-3125">**yıl**: yıl için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3125">**year**: Pointer to destination for year.</span></span>
- <span data-ttu-id="8b105-3126">**Month**: ay için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3126">**month**: Pointer to destination for month.</span></span>
- <span data-ttu-id="8b105-3127">**gün**: günün hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3127">**day**: Pointer to destination for day.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3128">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3128">Return Values</span></span>

- <span data-ttu-id="8b105-3129">**FX_SUCCESS** (0x00) başarılı Tarih alımı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3129">**FX_SUCCESS** (0x00) Successful date retrieval.</span></span>
- <span data-ttu-id="8b105-3130">**FX_PTR_ERROR** (0x18) bir veya daha fazla GIRIŞ parametresi null.</span><span class="sxs-lookup"><span data-stu-id="8b105-3130">**FX_PTR_ERROR** (0x18) One or more of the input parameters are NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3131">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3131">Allowed From</span></span>

<span data-ttu-id="8b105-3132">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3132">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3133">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3133">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3134">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3134">See Also</span></span>

- <span data-ttu-id="8b105-3135">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3135">fx_system_date_set</span></span>
- <span data-ttu-id="8b105-3136">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3136">fx_system_initialize</span></span>
- <span data-ttu-id="8b105-3137">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3137">fx_system_time_get</span></span>
- <span data-ttu-id="8b105-3138">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3138">fx_system_time_set</span></span>

## <a name="fx_system_date_set"></a><span data-ttu-id="8b105-3139">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3139">fx_system_date_set</span></span>

<span data-ttu-id="8b105-3140">Sistem tarihini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-3140">Sets system date</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3141">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3141">Prototype</span></span>

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a><span data-ttu-id="8b105-3142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3142">Description</span></span>

<span data-ttu-id="8b105-3143">Bu hizmet, sistem tarihini belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-3143">This service sets the system date as specified.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-3144">*İlk sistem tarihini ayarlamak için bu hizmet **fx_system_initialize** kısa süre sonra çağrılmalıdır. Varsayılan olarak, sistem tarihi en son genel FileX sürümüdür.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3144">*This service should be called shortly after **fx_system_initialize** to set the initial system date. By default, the system date is that of the last generic FileX release.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3145">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3145">Input Parameters</span></span>

- <span data-ttu-id="8b105-3146">**yıl**: yeni yıl.</span><span class="sxs-lookup"><span data-stu-id="8b105-3146">**year**: New year.</span></span> <span data-ttu-id="8b105-3147">Geçerli Aralık 1980 yılında 2107 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3147">The valid range is from 1980 through the year 2107.</span></span>
- <span data-ttu-id="8b105-3148">**ay**: yeni ay.</span><span class="sxs-lookup"><span data-stu-id="8b105-3148">**month**: New month.</span></span> <span data-ttu-id="8b105-3149">Geçerli Aralık 1 ile 12 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3149">The valid range is from 1 through 12.</span></span>
- <span data-ttu-id="8b105-3150">**gün**: yeni gün.</span><span class="sxs-lookup"><span data-stu-id="8b105-3150">**day**: New day.</span></span> <span data-ttu-id="8b105-3151">Geçerli Aralık, aya ve artık yıl koşullarına bağlı olarak 1 ila 31 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3151">The valid range is from 1 through 31, depending on month and leap year conditions.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3152">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3152">Return Values</span></span>

- <span data-ttu-id="8b105-3153">**FX_SUCCESS** (0x00) başarılı tarih ayarı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3153">**FX_SUCCESS** (0x00) Successful date setting.</span></span>
- <span data-ttu-id="8b105-3154">**FX_INVALID_YEAR** (0x12) geçersiz yıl belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3154">**FX_INVALID_YEAR** (0x12) Invalid year specified.</span></span>
- <span data-ttu-id="8b105-3155">**FX_INVALID_MONTH** (0x13) geçersiz ay belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3155">**FX_INVALID_MONTH** (0x13) Invalid month specified.</span></span>
- <span data-ttu-id="8b105-3156">**FX_INVALID_DAY** (0x14) geçersiz gün belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3156">**FX_INVALID_DAY** (0x14) Invalid day specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3157">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3157">Allowed From</span></span>

<span data-ttu-id="8b105-3158">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3158">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3159">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3159">Example</span></span>

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-3160">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3160">See Also</span></span>

- <span data-ttu-id="8b105-3161">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3161">fx_system_date_get</span></span>
- <span data-ttu-id="8b105-3162">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3162">fx_system_initialize</span></span>
- <span data-ttu-id="8b105-3163">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3163">fx_system_time_get</span></span>
- <span data-ttu-id="8b105-3164">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3164">fx_system_time_set</span></span>

## <a name="fx_system_initialize"></a><span data-ttu-id="8b105-3165">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3165">fx_system_initialize</span></span>

<span data-ttu-id="8b105-3166">Tüm sistemi başlatır</span><span class="sxs-lookup"><span data-stu-id="8b105-3166">Initializes entire system</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3167">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3167">Prototype</span></span>

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a><span data-ttu-id="8b105-3168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3168">Description</span></span>

<span data-ttu-id="8b105-3169">Bu hizmet, tüm önemli dosya x veri yapılarını başlatır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3169">This service initializes all the major FileX data structures.</span></span> <span data-ttu-id="8b105-3170">***Tx_application_define*** veya belki de bir başlatma iş parçacığından çağrılmalıdır ve başka bir FileX hizmeti kullanılmadan önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3170">It should be called either in ***tx_application_define*** or possibly from an initialization thread and must be called prior to using any other FileX service.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-3171">\* Bu çağrı tarafından başlatıldıktan sonra uygulama, *doğru bir sistem tarih ve saati ile başlamak için **fx_system_date_set** _ ve _ *fx_system_time_set** çağırmalıdır.\*</span><span class="sxs-lookup"><span data-stu-id="8b105-3171">*Once initialized by this call, the application should call ***fx_system_date_set** _ and _ *fx_system_time_set** to start with an accurate system date and time.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3172">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3172">Input Parameters</span></span>

<span data-ttu-id="8b105-3173">Yok</span><span class="sxs-lookup"><span data-stu-id="8b105-3173">None</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3174">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3174">Return Values</span></span>

<span data-ttu-id="8b105-3175">Yok.</span><span class="sxs-lookup"><span data-stu-id="8b105-3175">None.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3176">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3176">Allowed From</span></span>

<span data-ttu-id="8b105-3177">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3177">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3178">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3178">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3179">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3179">See Also</span></span>

- <span data-ttu-id="8b105-3180">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3180">fx_system_date_get</span></span>
- <span data-ttu-id="8b105-3181">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3181">fx_system_date_set</span></span>
- <span data-ttu-id="8b105-3182">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3182">fx_system_time_get</span></span>
- <span data-ttu-id="8b105-3183">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3183">fx_system_time_set</span></span>

## <a name="fx_system_time_get"></a><span data-ttu-id="8b105-3184">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3184">fx_system_time_get</span></span>

<span data-ttu-id="8b105-3185">Geçerli sistem saatini alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3185">Gets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3186">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3186">Prototype</span></span>

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="8b105-3187">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3187">Description</span></span>

<span data-ttu-id="8b105-3188">Bu hizmet geçerli sistem saatini alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3188">This service retrieves the current system time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3189">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3189">Input Parameters</span></span>

- <span data-ttu-id="8b105-3190">**saat**: saat için hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3190">**hour**: Pointer to destination for hour.</span></span>
- <span data-ttu-id="8b105-3191">**Minute**: dakikalık hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3191">**minute**: Pointer to destination for minute.</span></span>
- <span data-ttu-id="8b105-3192">**ikinci**: saniye için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3192">**second**: Pointer to destination for second.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3193">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3193">Return Values</span></span>

- <span data-ttu-id="8b105-3194">**FX_SUCCESS** (0x00) sistem saati alımı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3194">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="8b105-3195">**FX_PTR_ERROR** (0x18) bir veya daha fazla giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="8b105-3195">**FX_PTR_ERROR** (0x18) One or more of the input parameters</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3196">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3196">Allowed From</span></span>

<span data-ttu-id="8b105-3197">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3197">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3198">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3198">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3199">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3199">See Also</span></span>

- <span data-ttu-id="8b105-3200">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3200">fx_system_date_get</span></span>
- <span data-ttu-id="8b105-3201">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3201">fx_system_date_set</span></span>
- <span data-ttu-id="8b105-3202">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3202">fx_system_initialize</span></span>
- <span data-ttu-id="8b105-3203">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3203">fx_system_time_set</span></span>

## <a name="fx_system_time_set"></a><span data-ttu-id="8b105-3204">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3204">fx_system_time_set</span></span>

<span data-ttu-id="8b105-3205">Geçerli sistem saatini ayarlar</span><span class="sxs-lookup"><span data-stu-id="8b105-3205">Sets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3206">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3206">Prototype</span></span>

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a><span data-ttu-id="8b105-3207">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3207">Description</span></span>

<span data-ttu-id="8b105-3208">Bu hizmet, geçerli sistem saatini giriş parametreleri tarafından belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b105-3208">This service sets the current system time to that specified by the input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-3209">*Bu hizmet, ilk sistem saatini ayarlamak için **fx_system_initialize** kısa süre sonra çağrılmalıdır. Varsayılan olarak, sistem saati 0:0:0 ' dir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3209">*This service should be called shortly after **fx_system_initialize** to set the initial system time. By default, the system time is 0:0:0.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3210">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3210">Input Parameters</span></span>

- <span data-ttu-id="8b105-3211">**saat**: yeni saat (0-23).</span><span class="sxs-lookup"><span data-stu-id="8b105-3211">**hour**: New hour (0-23).</span></span>
- <span data-ttu-id="8b105-3212">**dakika**: yeni dakika (0-59).</span><span class="sxs-lookup"><span data-stu-id="8b105-3212">**minute**: New minute (0-59).</span></span>
- <span data-ttu-id="8b105-3213">**ikinci**: Yeni saniye (0-59).</span><span class="sxs-lookup"><span data-stu-id="8b105-3213">**second**: New second (0-59).</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3214">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3214">Return Values</span></span>

- <span data-ttu-id="8b105-3215">**FX_SUCCESS** (0x00) sistem saati alımı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3215">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="8b105-3216">**FX_INVALID_HOUR**    (0x15) yeni saat geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3216">**FX_INVALID_HOUR**    (0x15) New hour is invalid.</span></span>
- <span data-ttu-id="8b105-3217">**FX_INVALID_MINUTE** (0x16) yeni dakika geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3217">**FX_INVALID_MINUTE** (0x16) New minute is invalid.</span></span>
- <span data-ttu-id="8b105-3218">**FX_INVALID_SECOND** (0x17) yeni ikinci değer geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3218">**FX_INVALID_SECOND** (0x17) New second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3219">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3219">Allowed From</span></span>

<span data-ttu-id="8b105-3220">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3220">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3221">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3221">Example</span></span>

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a><span data-ttu-id="8b105-3222">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3222">See Also</span></span>

- <span data-ttu-id="8b105-3223">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3223">fx_system_date_get</span></span>
- <span data-ttu-id="8b105-3224">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3224">fx_system_date_set</span></span>
- <span data-ttu-id="8b105-3225">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="8b105-3225">fx_system_initialize</span></span>
- <span data-ttu-id="8b105-3226">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3226">fx_system_time_get</span></span>

## <a name="fx_unicode_directory_create"></a><span data-ttu-id="8b105-3227">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3227">fx_unicode_directory_create</span></span>

<span data-ttu-id="8b105-3228">Unicode dizin oluşturur</span><span class="sxs-lookup"><span data-stu-id="8b105-3228">Creates a Unicode directory</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3229">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3229">Prototype</span></span>

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a><span data-ttu-id="8b105-3230">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3230">Description</span></span>

<span data-ttu-id="8b105-3231">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir alt dizin oluşturur; Unicode kaynak adı parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8b105-3231">This service creates a Unicode-named subdirectory in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="8b105-3232">Başarılı olursa, yeni oluşturulan Unicode alt dizininin kısa adı (8,3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-3232">If successful, the short name (8.3 format) of the newly created Unicode subdirectory is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-3233">*Unicode alt dizinindeki tüm işlemler (varsayılan yol, silme, vb.), standart FileX dizin hizmetlerine döndürülen kısa ad (8,3 biçimi) sağlanarak yapılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3233">*All operations on the Unicode subdirectory (making it the default path, deleting, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX directory services.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3234">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3234">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3235">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3235">Input Parameters</span></span>

- <span data-ttu-id="8b105-3236">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3236">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3237">**source_unicode_name**: yeni alt dizin için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3237">**source_unicode_name**: Pointer to the Unicode name for the new subdirectory.</span></span>
- <span data-ttu-id="8b105-3238">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3238">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8b105-3239">**short_name**: yeni Unicode alt dizini için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3239">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode subdirectory.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3240">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3240">Return Values</span></span>

- <span data-ttu-id="8b105-3241">**FX_SUCCESS** (0x00) başarılı Unicode dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8b105-3241">**FX_SUCCESS** (0x00) Successful Unicode directory create.</span></span>
- <span data-ttu-id="8b105-3242">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3242">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3243">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin zaten var.</span><span class="sxs-lookup"><span data-stu-id="8b105-3243">**FX_ALREADY_CREATED** (0x0B) Specified directory already exists.</span></span>
- <span data-ttu-id="8b105-3244">Yeni Dizin girişi için medyada daha fazla küme yok **FX_NO_MORE_SPACE** (0x0A).</span><span class="sxs-lookup"><span data-stu-id="8b105-3244">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new directory entry.</span></span>
- <span data-ttu-id="8b105-3245">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3245">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8b105-3246">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3246">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-3247">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8b105-3247">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8b105-3248">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3248">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="8b105-3249">**FX_IO_ERROR (0x90)** Sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3249">**FX_IO_ERROR    (0x90)** Driver I/O error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3250">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3250">Allowed From</span></span>

<span data-ttu-id="8b105-3251">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3251">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3252">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3252">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3253">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3253">See Also</span></span>

- <span data-ttu-id="8b105-3254">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3254">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-3255">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3255">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-3256">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3256">fx_directory_create</span></span>
- <span data-ttu-id="8b105-3257">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3257">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-3258">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3258">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-3259">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3259">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-3260">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3260">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-3261">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3261">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-3262">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3262">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-3263">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-3263">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-3264">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3264">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-3265">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-3265">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-3266">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3266">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-3267">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3267">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-3268">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-3268">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-3269">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3269">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-3270">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3270">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-3271">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3271">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-3272">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3272">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-3273">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3273">fx_unicode_directory_rename</span></span>

## <a name="fx_unicode_directory_rename"></a><span data-ttu-id="8b105-3274">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3274">fx_unicode_directory_rename</span></span>

<span data-ttu-id="8b105-3275">Unicode dizesini kullanarak dizini yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="8b105-3275">Renames directory using Unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3276">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3276">Prototype</span></span>

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a><span data-ttu-id="8b105-3277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3277">Description</span></span>

<span data-ttu-id="8b105-3278">Bu hizmet, Unicode adlı bir alt dizini geçerli çalışma dizininde belirtilen yeni Unicode adına değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3278">This service changes a Unicode-named subdirectory to specified new Unicode name in current working directory.</span></span> <span data-ttu-id="8b105-3279">Unicode ad parametreleri yol bilgilerine sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3279">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3280">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3280">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3281">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3281">Input Parameters</span></span>

- <span data-ttu-id="8b105-3282">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3282">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3283">**old_unicode_name**: geçerli dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3283">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="8b105-3284">**old_unicode_name_length**: geçerli Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3284">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="8b105-3285">**new_unicode_name**: yeni Unicode dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3285">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="8b105-3286">**old_unicode_name_length**: yeni Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3286">**old_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="8b105-3287">**new_short_name**: yeniden adlandırılan Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3287">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span> <span data-ttu-id="8b105-3288">Dizini Unicode ile yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="8b105-3288">Rename Directory with Unicode</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3289">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3289">Return Values</span></span>

- <span data-ttu-id="8b105-3290">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3290">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="8b105-3291">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3291">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3292">**FX_ALREADY_CREATED** (0x0B) belirtilen dizin adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="8b105-3292">**FX_ALREADY_CREATED** (0x0B) Specified directory name already exists.</span></span>
- <span data-ttu-id="8b105-3293">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3293">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3294">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="8b105-3294">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="8b105-3295">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3295">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="8b105-3296">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3296">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3297">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3297">Allowed From</span></span>

<span data-ttu-id="8b105-3298">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3298">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3299">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3299">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3300">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3300">See Also</span></span>

- <span data-ttu-id="8b105-3301">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3301">fx_directory_attributes_read</span></span>
- <span data-ttu-id="8b105-3302">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3302">fx_directory_attributes_set</span></span>
- <span data-ttu-id="8b105-3303">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3303">fx_directory_create</span></span>
- <span data-ttu-id="8b105-3304">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3304">fx_directory_default_get</span></span>
- <span data-ttu-id="8b105-3305">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3305">fx_directory_default_set</span></span>
- <span data-ttu-id="8b105-3306">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3306">fx_directory_delete</span></span>
- <span data-ttu-id="8b105-3307">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3307">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="8b105-3308">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3308">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="8b105-3309">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3309">fx_directory_information_get</span></span>
- <span data-ttu-id="8b105-3310">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="8b105-3310">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="8b105-3311">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3311">fx_directory_local_path_get</span></span>
- <span data-ttu-id="8b105-3312">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="8b105-3312">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="8b105-3313">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3313">fx_directory_local_path_set</span></span>
- <span data-ttu-id="8b105-3314">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3314">fx_directory_long_name_get</span></span>
- <span data-ttu-id="8b105-3315">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="8b105-3315">fx_directory_name_test</span></span>
- <span data-ttu-id="8b105-3316">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3316">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="8b105-3317">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="8b105-3317">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="8b105-3318">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3318">fx_directory_rename</span></span>
- <span data-ttu-id="8b105-3319">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3319">fx_directory_short_name_get</span></span>
- <span data-ttu-id="8b105-3320">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3320">fx_unicode_directory_create</span></span>

## <a name="fx_unicode_file_create"></a><span data-ttu-id="8b105-3321">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3321">fx_unicode_file_create</span></span>

<span data-ttu-id="8b105-3322">Unicode dosyası oluşturur</span><span class="sxs-lookup"><span data-stu-id="8b105-3322">Creates a Unicode file</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3323">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3323">Prototype</span></span>

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="8b105-3324">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3324">Description</span></span>

<span data-ttu-id="8b105-3325">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya oluşturur; Unicode kaynak adı parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8b105-3325">This service creates a Unicode-named file in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="8b105-3326">Başarılı olursa, yeni oluşturulan Unicode dosyanın kısa adı (8,3 biçimi) hizmet tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-3326">If successful, the short name (8.3 format) of the newly created Unicode file is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="8b105-3327">*Unicode dosyasındaki (açma, yazma, okuma, kapatma, vb.) tüm işlemler, standart FileX dosya hizmetlerine döndürülen kısa ad (8,3 biçimi) sağlanarak yapılmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3327">*All operations on the Unicode file (opening, writing, reading, closing, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX file services.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3328">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3328">Input Parameters</span></span>


- <span data-ttu-id="8b105-3329">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3329">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3330">**source_unicode_name**: yeni dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3330">**source_unicode_name**: Pointer to the Unicode name for the new file.</span></span>
- <span data-ttu-id="8b105-3331">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3331">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8b105-3332">**short_name**: yeni Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3332">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3333">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3333">Return Values</span></span>

- <span data-ttu-id="8b105-3334">**FX_SUCCESS** (0x00) başarılı dosya oluştur.</span><span class="sxs-lookup"><span data-stu-id="8b105-3334">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="8b105-3335">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3335">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3336">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya zaten var.</span><span class="sxs-lookup"><span data-stu-id="8b105-3336">**FX_ALREADY_CREATED** (0x0B) Specified file already exists.</span></span>
- <span data-ttu-id="8b105-3337">Yeni dosya girişi için medyada daha fazla küme yok **FX_NO_MORE_SPACE** (0x0A).</span><span class="sxs-lookup"><span data-stu-id="8b105-3337">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new file entry.</span></span>
- <span data-ttu-id="8b105-3338">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3338">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8b105-3339">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3339">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3340">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3340">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="8b105-3341">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8b105-3341">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8b105-3342">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3342">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3343">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3343">Allowed From</span></span>

<span data-ttu-id="8b105-3344">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3344">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3345">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3345">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3346">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3346">See Also</span></span>

- <span data-ttu-id="8b105-3347">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3347">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3348">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3348">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3349">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3349">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3350">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3350">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3351">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3351">fx_file_close</span></span>
- <span data-ttu-id="8b105-3352">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3352">fx_file_create</span></span>
- <span data-ttu-id="8b105-3353">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3353">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3354">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3354">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3355">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3355">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3356">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3356">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3357">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3357">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3358">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3358">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3359">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3359">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3360">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3360">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3361">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3361">fx_file_open</span></span>
- <span data-ttu-id="8b105-3362">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3362">fx_file_read</span></span>
- <span data-ttu-id="8b105-3363">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3363">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3364">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3364">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3365">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3365">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3366">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3366">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3367">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3367">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3368">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3368">fx_file_write</span></span>
- <span data-ttu-id="8b105-3369">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3369">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3370">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3370">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-3371">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3371">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-3372">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3372">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_file_rename"></a><span data-ttu-id="8b105-3373">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3373">fx_unicode_file_rename</span></span>

<span data-ttu-id="8b105-3374">Unicode dizesini kullanarak bir dosyayı yeniden adlandırır</span><span class="sxs-lookup"><span data-stu-id="8b105-3374">Renames a file using unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3375">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3375">Prototype</span></span>

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a><span data-ttu-id="8b105-3376">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3376">Description</span></span>

<span data-ttu-id="8b105-3377">Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya adını belirtilen yeni Unicode adı olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3377">This service changes a Unicode-named file name to specified new Unicode name in current default directory.</span></span> <span data-ttu-id="8b105-3378">Unicode ad parametreleri yol bilgilerine sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3378">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3379">*Bu hizmet, exFAT ortamında desteklenmez.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3379">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3380">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3380">Input Parameters</span></span>

- <span data-ttu-id="8b105-3381">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3381">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3382">**old_unicode_name**: geçerli dosya için Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3382">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="8b105-3383">**old_unicode_name_length**: geçerli Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3383">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="8b105-3384">**new_unicode_name**: yeni Unicode dosya adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3384">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="8b105-3385">**new_unicode_name_length**: yeni Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3385">**new_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="8b105-3386">**new_short_name**: yeniden adlandırılan Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3386">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3387">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3387">Return Values</span></span>


- <span data-ttu-id="8b105-3388">**FX_SUCCESS** (0x00) başarılı medya açıldı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3388">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="8b105-3389">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3389">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3390">**FX_ALREADY_CREATED** (0x0B) belirtilen dosya adı zaten var.</span><span class="sxs-lookup"><span data-stu-id="8b105-3390">**FX_ALREADY_CREATED** (0x0B) Specified file name already exists.</span></span>
- <span data-ttu-id="8b105-3391">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3391">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3392">**FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.</span><span class="sxs-lookup"><span data-stu-id="8b105-3392">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="8b105-3393">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3393">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="8b105-3394">**FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3394">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3395">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3395">Allowed From</span></span>

<span data-ttu-id="8b105-3396">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3396">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3397">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3397">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3398">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3398">See Also</span></span>

- <span data-ttu-id="8b105-3399">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3399">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3400">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3400">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3401">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3401">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3402">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3402">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3403">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3403">fx_file_close</span></span>
- <span data-ttu-id="8b105-3404">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3404">fx_file_create</span></span>
- <span data-ttu-id="8b105-3405">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3405">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3406">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3406">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3407">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3407">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3408">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3408">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3409">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3409">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3410">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3410">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3411">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3411">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3412">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3412">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3413">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3413">fx_file_open</span></span>
- <span data-ttu-id="8b105-3414">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3414">fx_file_read</span></span>
- <span data-ttu-id="8b105-3415">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3415">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3416">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3416">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3417">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3417">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3418">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3418">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3419">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3419">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3420">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3420">fx_file_write</span></span>
- <span data-ttu-id="8b105-3421">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3421">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3422">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3422">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-3423">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3423">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-3424">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3424">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get"></a><span data-ttu-id="8b105-3425">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3425">fx_unicode_length_get</span></span>

<span data-ttu-id="8b105-3426">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3426">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3427">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3427">Prototype</span></span>

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a><span data-ttu-id="8b105-3428">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3428">Description</span></span>

<span data-ttu-id="8b105-3429">Bu hizmet, sağlanan Unicode adının uzunluğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="8b105-3429">This service determines the length of the supplied Unicode name.</span></span> <span data-ttu-id="8b105-3430">Unicode bir karakter iki bayt ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3430">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="8b105-3431">Unicode adı, iki baytlık bir Unicode karakter olan ve iki boş bayt (0 değeri 0 değeri) tarafından sonlandırılan bir serisidir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3431">A Unicode name is a series of two byte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3432">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3432">Input Parameters</span></span>

<span data-ttu-id="8b105-3433">**unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3433">**unicode_name**: Pointer to Unicode name.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3434">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3434">Return Values</span></span>

<span data-ttu-id="8b105-3435">**uzunluk**: Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="8b105-3435">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3436">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3436">Allowed From</span></span>

<span data-ttu-id="8b105-3437">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3437">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3438">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3438">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3439">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3439">See Also</span></span>

- <span data-ttu-id="8b105-3440">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3440">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3441">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3441">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3442">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3442">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3443">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3443">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3444">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3444">fx_file_close</span></span>
- <span data-ttu-id="8b105-3445">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3445">fx_file_create</span></span>
- <span data-ttu-id="8b105-3446">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3446">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3447">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3447">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3448">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3448">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3449">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3449">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3450">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3450">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3451">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3451">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3452">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3452">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3453">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3453">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3454">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3454">fx_file_open</span></span>
- <span data-ttu-id="8b105-3455">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3455">fx_file_read</span></span>
- <span data-ttu-id="8b105-3456">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3456">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3457">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3457">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3458">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3458">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3459">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3459">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3460">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3460">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3461">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3461">fx_file_write</span></span>
- <span data-ttu-id="8b105-3462">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3462">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3463">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3463">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-3464">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3464">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-3465">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3465">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-3466">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3466">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get_extended"></a><span data-ttu-id="8b105-3467">fx_unicode_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="8b105-3467">fx_unicode_length_get_extended</span></span>

<span data-ttu-id="8b105-3468">Unicode adının uzunluğunu alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3468">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3469">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3469">Prototype</span></span>

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a><span data-ttu-id="8b105-3470">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3470">Description</span></span>

<span data-ttu-id="8b105-3471">Bu hizmet, sağlanan Unicode adının uzunluğunu alır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3471">This service gets the length of the supplied Unicode name.</span></span> <span data-ttu-id="8b105-3472">Unicode bir karakter iki bayt ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3472">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="8b105-3473">Unicode adı, iki boş bayt (iki bayt 0 değeri) tarafından sonlandırılan bir dizi TWA Unicode karakter dizisidir.</span><span class="sxs-lookup"><span data-stu-id="8b105-3473">A Unicode name is a series of twobyte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3474">*Bu hizmet, iki NULL karakter de dahil olmak üzere, çağıran **unicode_name** arabelleğinin boyutuna geçtiğinde, **fx_unicode_length_get ()** ile aynıdır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3474">*This service is identical to **fx_unicode_length_get()** except the caller passes in the size of the **unicode_name** buffer, including the two NULL characters.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3475">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3475">Input Parameters</span></span>

- <span data-ttu-id="8b105-3476">**unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3476">**unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="8b105-3477">**BUFFER_LENGTH**: Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3477">**buffer_length**: Size of Unicode name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3478">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3478">Return Values</span></span>

<span data-ttu-id="8b105-3479">**uzunluk**: Unicode adının uzunluğu (adda Unicode karakter sayısı).</span><span class="sxs-lookup"><span data-stu-id="8b105-3479">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3480">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3480">Allowed From</span></span>

<span data-ttu-id="8b105-3481">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3481">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3482">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3482">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3483">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3483">See Also</span></span>

- <span data-ttu-id="8b105-3484">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3484">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3485">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3485">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3486">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3486">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3487">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3487">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3488">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3488">fx_file_close</span></span>
- <span data-ttu-id="8b105-3489">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3489">fx_file_create</span></span>
- <span data-ttu-id="8b105-3490">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3490">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3491">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3491">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3492">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3492">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3493">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3493">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3494">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3494">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3495">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3495">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3496">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3496">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3497">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3497">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3498">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3498">fx_file_open</span></span>
- <span data-ttu-id="8b105-3499">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3499">fx_file_read</span></span>
- <span data-ttu-id="8b105-3500">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3500">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3501">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3501">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3502">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3502">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3503">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3503">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3504">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3504">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3505">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3505">fx_file_write</span></span>
- <span data-ttu-id="8b105-3506">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3506">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3507">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3507">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-3508">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3508">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-3509">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3509">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-3510">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3510">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get"></a><span data-ttu-id="8b105-3511">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3511">fx_unicode_name_get</span></span>

<span data-ttu-id="8b105-3512">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3512">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3513">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3513">Prototype</span></span>

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a><span data-ttu-id="8b105-3514">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3514">Description</span></span>

<span data-ttu-id="8b105-3515">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8b105-3515">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="8b105-3516">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-3516">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3517">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3517">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3518">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3518">Input Parameters</span></span>

- <span data-ttu-id="8b105-3519">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3519">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3520">**short_name** Kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="8b105-3520">**short_name** Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="8b105-3521">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3521">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="8b105-3522">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3522">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3523">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3523">Return Values</span></span>

- <span data-ttu-id="8b105-3524">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="8b105-3524">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="8b105-3525">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-3525">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8b105-3526">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-3526">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-3527">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3527">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3528">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3528">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3529">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="8b105-3529">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="8b105-3530">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-3530">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-3531">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8b105-3531">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8b105-3532">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3532">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3533">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3533">Allowed From</span></span>

<span data-ttu-id="8b105-3534">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3534">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3535">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3535">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3536">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3536">See Also</span></span>

- <span data-ttu-id="8b105-3537">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3537">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3538">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3538">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3539">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3539">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3540">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3540">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3541">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3541">fx_file_close</span></span>
- <span data-ttu-id="8b105-3542">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3542">fx_file_create</span></span>
- <span data-ttu-id="8b105-3543">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3543">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3544">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3544">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3545">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3545">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3546">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3546">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3547">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3547">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3548">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3548">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3549">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3549">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3550">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3550">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3551">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3551">fx_file_open</span></span>
- <span data-ttu-id="8b105-3552">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3552">fx_file_read</span></span>
- <span data-ttu-id="8b105-3553">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3553">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3554">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3554">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3555">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3555">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3556">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3556">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3557">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3557">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3558">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3558">fx_file_write</span></span>
- <span data-ttu-id="8b105-3559">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3559">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3560">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3560">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-3561">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3561">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-3562">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3562">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get_extended"></a><span data-ttu-id="8b105-3563">fx_unicode_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8b105-3563">fx_unicode_name_get_extended</span></span>

<span data-ttu-id="8b105-3564">Kısa adından Unicode adı alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3564">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3565">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3565">Prototype</span></span>

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a><span data-ttu-id="8b105-3566">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3566">Description</span></span>

<span data-ttu-id="8b105-3567">Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8b105-3567">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="8b105-3568">Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-3568">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3569">\* Bu hizmet,_çağıran, hedef Unicode arabelleğinin bir giriş bağımsız değişkeni olarak boyutunu sağladığı sürece \* fx_unicode_name_get aynıdır. Bu, hizmetin hedef Unicode arabelleğinin üzerine yazmayacağı garantisi sağlamasına izin verir_</span><span class="sxs-lookup"><span data-stu-id="8b105-3569">\*This service is identical to \***fx_unicode_name_get**_, except the caller supplies the size of the destination Unicode buffer as an input argument. This allows the service to guarantee that it will not overwrite the destination Unicode buffer_</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3570">*Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3570">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3571">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3571">Input Parameters</span></span>

- <span data-ttu-id="8b105-3572">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3572">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3573">**short_name**: kısa ad işaretçisi (8,3 biçiminde).</span><span class="sxs-lookup"><span data-stu-id="8b105-3573">**short_name**: Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="8b105-3574">**destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3574">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="8b105-3575">**destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3575">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>
- <span data-ttu-id="8b105-3576">**unicode_name_buffer_length**: Unicode ad arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3576">**unicode_name_buffer_length**: Size of the Unicode name buffer.</span></span> <span data-ttu-id="8b105-3577">Note: bir NULL Sonlandırıcı gereklidir ve bu da ek bir bayt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b105-3577">Note: A NULL terminator is required, which makes an extra byte.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3578">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3578">Return Values</span></span>

- <span data-ttu-id="8b105-3579">**FX_SUCCESS** (0x00) başarılı Unicode adı alma.</span><span class="sxs-lookup"><span data-stu-id="8b105-3579">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="8b105-3580">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-3580">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8b105-3581">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-3581">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-3582">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3582">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3583">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3583">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3584">**FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="8b105-3584">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="8b105-3585">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-3585">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-3586">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8b105-3586">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8b105-3587">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3587">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3588">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3588">Allowed From</span></span>

<span data-ttu-id="8b105-3589">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3589">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3590">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3590">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3591">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3591">See Also</span></span>

- <span data-ttu-id="8b105-3592">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3592">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3593">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3593">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3594">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3594">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3595">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3595">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3596">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3596">fx_file_close</span></span>
- <span data-ttu-id="8b105-3597">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3597">fx_file_create</span></span>
- <span data-ttu-id="8b105-3598">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3598">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3599">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3599">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3600">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3600">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3601">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3601">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3602">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3602">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3603">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3603">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3604">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3604">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3605">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3605">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3606">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3606">fx_file_open</span></span>
- <span data-ttu-id="8b105-3607">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3607">fx_file_read</span></span>
- <span data-ttu-id="8b105-3608">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3608">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3609">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3609">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3610">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3610">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3611">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3611">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3612">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3612">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3613">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3613">fx_file_write</span></span>
- <span data-ttu-id="8b105-3614">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3614">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3615">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3615">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-3616">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3616">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-3617">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3617">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_short_name_get"></a><span data-ttu-id="8b105-3618">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3618">fx_unicode_short_name_get</span></span>

<span data-ttu-id="8b105-3619">Unicode adından kısa adı alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3619">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3620">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3620">Prototype</span></span>

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

<span data-ttu-id="8b105-3621">Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8b105-3621">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="8b105-3622">Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-3622">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3623">*Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3623">*This service can be used to get short names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3624">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3624">Input Parameters</span></span>

- <span data-ttu-id="8b105-3625">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3625">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3626">**source_unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3626">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="8b105-3627">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3627">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8b105-3628">**destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3628">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="8b105-3629">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3629">This must be at least 13 bytes in size.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3630">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3630">Return Values</span></span>

- <span data-ttu-id="8b105-3631">**FX_SUCCESS** (0x00) başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="8b105-3631">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="8b105-3632">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-3632">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8b105-3633">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-3633">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="8b105-3634">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3634">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3635">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3635">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3636">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3636">**FX_NOT_FOUND** (0x04)    Unicode name was not found.</span></span>
- <span data-ttu-id="8b105-3637">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3637">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8b105-3638">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-3638">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-3639">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8b105-3639">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8b105-3640">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3640">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3641">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3641">Allowed From</span></span>

<span data-ttu-id="8b105-3642">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3642">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3643">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3643">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3644">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3644">See Also</span></span>

- <span data-ttu-id="8b105-3645">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3645">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3646">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3646">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3647">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3647">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3648">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3648">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3649">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3649">fx_file_close</span></span>
- <span data-ttu-id="8b105-3650">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3650">fx_file_create</span></span>
- <span data-ttu-id="8b105-3651">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3651">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3652">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3652">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3653">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3653">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3654">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3654">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3655">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3655">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3656">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3656">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3657">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3657">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3658">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3658">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3659">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3659">fx_file_open</span></span>
- <span data-ttu-id="8b105-3660">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3660">fx_file_read</span></span>
- <span data-ttu-id="8b105-3661">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3661">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3662">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3662">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3663">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3663">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3664">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3664">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3665">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3665">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3666">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3666">fx_file_write</span></span>
- <span data-ttu-id="8b105-3667">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3667">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3668">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3668">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-3669">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3669">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-3670">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3670">fx_unicode_name_get</span></span>

## <a name="fx_unicode_short_name_get_extended"></a><span data-ttu-id="8b105-3671">fx_unicode_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="8b105-3671">fx_unicode_short_name_get_extended</span></span>

<span data-ttu-id="8b105-3672">Unicode adından kısa adı alır</span><span class="sxs-lookup"><span data-stu-id="8b105-3672">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="8b105-3673">Prototype</span><span class="sxs-lookup"><span data-stu-id="8b105-3673">Prototype</span></span>

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="8b105-3674">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b105-3674">Description</span></span>

<span data-ttu-id="8b105-3675">Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="8b105-3675">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="8b105-3676">Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b105-3676">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b105-3677">*Çağıran, hedef arabelleğin bir giriş bağımsız değişkeni olarak boyutunu sağladığı, bu hizmet **fx_unicode_short_name_get ()** ile aynıdır. Bu, hizmetin kısa adı hedef arabelleği aşmadığını garanti etmesine olanak tanır.*</span><span class="sxs-lookup"><span data-stu-id="8b105-3677">*This service is identical to **fx_unicode_short_name_get()**, except the caller supplies the size of the destination buffer as an input argument. This allows the service to guarantee the short name does not exceed the destination buffer.*</span></span>

<span data-ttu-id="8b105-3678">*Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="8b105-3678">*This service can be used to get short names for both files and subdirectories*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8b105-3679">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3679">Input Parameters</span></span>

- <span data-ttu-id="8b105-3680">**media_ptr**: medya denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3680">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="8b105-3681">**source_unicode_name**: Unicode adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3681">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="8b105-3682">**source_unicode_length**: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3682">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="8b105-3683">**destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8b105-3683">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="8b105-3684">Bu, en az 13 bayt boyutunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3684">This must be at least 13 bytes in size.</span></span>
- <span data-ttu-id="8b105-3685">**short_name_buffer_length**: hedef arabelleğin boyutu.</span><span class="sxs-lookup"><span data-stu-id="8b105-3685">**short_name_buffer_length**: Size of the destination buffer.</span></span> <span data-ttu-id="8b105-3686">Arabellek boyutu en az 14 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b105-3686">The buffer size must be at least 14 bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="8b105-3687">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="8b105-3687">Return Values</span></span>

- <span data-ttu-id="8b105-3688">**FX_SUCCESS** (0x00) başarılı kısa ad alma.</span><span class="sxs-lookup"><span data-stu-id="8b105-3688">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="8b105-3689">**FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="8b105-3689">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="8b105-3690">**FX_FILE_CORRUPT** (0x08) dosyası bozuk</span><span class="sxs-lookup"><span data-stu-id="8b105-3690">**FX_FILE_CORRUPT** (0x08)    File is corrupted</span></span>
- <span data-ttu-id="8b105-3691">**FX_IO_ERROR** (0x90) sürücü g/ç hatası.</span><span class="sxs-lookup"><span data-stu-id="8b105-3691">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="8b105-3692">**FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3692">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="8b105-3693">**FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3693">**FX_NOT_FOUND** (0x04) Unicode name was not found.</span></span>
- <span data-ttu-id="8b105-3694">**FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="8b105-3694">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="8b105-3695">**FX_SECTOR_INVALID** (0x89) geçersiz kesim.</span><span class="sxs-lookup"><span data-stu-id="8b105-3695">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="8b105-3696">**FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.</span><span class="sxs-lookup"><span data-stu-id="8b105-3696">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="8b105-3697">**FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="8b105-3697">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8b105-3698">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8b105-3698">Allowed From</span></span>

<span data-ttu-id="8b105-3699">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8b105-3699">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8b105-3700">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b105-3700">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="8b105-3701">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b105-3701">See Also</span></span>

- <span data-ttu-id="8b105-3702">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3702">fx_file_allocate</span></span>
- <span data-ttu-id="8b105-3703">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3703">fx_file_attributes_read</span></span>
- <span data-ttu-id="8b105-3704">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3704">fx_file_attributes_set</span></span>
- <span data-ttu-id="8b105-3705">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3705">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3706">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="8b105-3706">fx_file_close</span></span>
- <span data-ttu-id="8b105-3707">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3707">fx_file_create</span></span>
- <span data-ttu-id="8b105-3708">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3708">fx_file_date_time_set</span></span>
- <span data-ttu-id="8b105-3709">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="8b105-3709">fx_file_delete</span></span>
- <span data-ttu-id="8b105-3710">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3710">fx_file_extended_allocate</span></span>
- <span data-ttu-id="8b105-3711">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="8b105-3711">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="8b105-3712">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3712">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="8b105-3713">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3713">fx_file_extended_seek</span></span>
- <span data-ttu-id="8b105-3714">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3714">fx_file_extended_truncate</span></span>
- <span data-ttu-id="8b105-3715">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3715">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="8b105-3716">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="8b105-3716">fx_file_open</span></span>
- <span data-ttu-id="8b105-3717">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="8b105-3717">fx_file_read</span></span>
- <span data-ttu-id="8b105-3718">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3718">fx_file_relative_seek</span></span>
- <span data-ttu-id="8b105-3719">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3719">fx_file_rename</span></span>
- <span data-ttu-id="8b105-3720">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="8b105-3720">fx_file_seek</span></span>
- <span data-ttu-id="8b105-3721">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="8b105-3721">fx_file_truncate</span></span>
- <span data-ttu-id="8b105-3722">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="8b105-3722">fx_file_truncate_release</span></span>
- <span data-ttu-id="8b105-3723">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="8b105-3723">fx_file_write</span></span>
- <span data-ttu-id="8b105-3724">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="8b105-3724">fx_file_write_notify_set</span></span>
- <span data-ttu-id="8b105-3725">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="8b105-3725">fx_unicode_file_create</span></span>
- <span data-ttu-id="8b105-3726">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="8b105-3726">fx_unicode_file_rename</span></span>
- <span data-ttu-id="8b105-3727">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3727">fx_unicode_name_get</span></span>
- <span data-ttu-id="8b105-3728">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="8b105-3728">fx_unicode_short_name_get</span></span>
