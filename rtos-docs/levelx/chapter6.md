---
title: Bölüm 6-Azure RTOS LevelX veya API 'Leri
description: Azure RTOS LevelX veya API 'si uygulama tarafından kullanılabilir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3ab7d3a7e431d7c8f49ef4f5cab9216dc77c8d33
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827052"
---
# <a name="chapter-6---azure-rtos-levelx-nor-apis"></a><span data-ttu-id="a7cd6-103">Bölüm 6-Azure RTOS LevelX veya API 'Leri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-103">Chapter 6 - Azure RTOS LevelX NOR APIs</span></span>

<span data-ttu-id="a7cd6-104">Uygulama için kullanılabilen Azure RTOS LevelX ve API işlevleri aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-104">The Azure RTOS LevelX NOR API functions available to the application are as follows.</span></span>

- <span data-ttu-id="a7cd6-105">\***lx_nor_flash_close** _: _Close veya Flash örneği \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-105">***lx_nor_flash_close** _: _Close NOR flash instance*</span></span>
- <span data-ttu-id="a7cd6-106">\***lx_nor_flash_defragment** _: _Defragment veya Flash örneği \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-106">***lx_nor_flash_defragment** _: _Defragment NOR flash instance*</span></span>
- <span data-ttu-id="a7cd6-107">\***lx_nor_flash_extended_cache_enable** _: _Enable/genişletilmiş ve önbelleği devre dışı bırak \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-107">***lx_nor_flash_extended_cache_enable** _: _Enable/disable extended NOR cache*</span></span>
- <span data-ttu-id="a7cd6-108">\***lx_nor_flash_initialize** _: _Initialize veya Flash desteği \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-108">***lx_nor_flash_initialize** _: _Initialize NOR flash support*</span></span>
- <span data-ttu-id="a7cd6-109">\***lx_nor_flash_open** _: _Open veya Flash örneği \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-109">***lx_nor_flash_open** _: _Open NOR flash instance*</span></span>
- <span data-ttu-id="a7cd6-110">\***lx_nor_flash_partial_defragment** _: _Partial veya Flash örneği birleştirme</span><span class="sxs-lookup"><span data-stu-id="a7cd6-110">***lx_nor_flash_partial_defragment** _: _Partial defragment of NOR flash instance*</span></span>
- <span data-ttu-id="a7cd6-111">\***lx_nor_flash_sector_read** _: _Read veya Flash sektörü \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-111">***lx_nor_flash_sector_read** _: _Read NOR flash sector*</span></span>
- <span data-ttu-id="a7cd6-112">\***lx_nor_flash_sector_release** _: _Release veya Flash sektörü \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-112">***lx_nor_flash_sector_release** _: _Release NOR flash sector*</span></span>
- <span data-ttu-id="a7cd6-113">\***lx_nor_flash_sector_write** _: _write veya Flash sektörü \*</span><span class="sxs-lookup"><span data-stu-id="a7cd6-113">***lx_nor_flash_sector_write** _: _Write NOR flash sector*</span></span>

## <a name="lx_nor_flash_close"></a><span data-ttu-id="a7cd6-114">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-114">lx_nor_flash_close</span></span>

<span data-ttu-id="a7cd6-115">Kapat veya Flash örneği</span><span class="sxs-lookup"><span data-stu-id="a7cd6-115">Close NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-116">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-116">Prototype</span></span>

```c
UINT lx_nor_flash_close(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a><span data-ttu-id="a7cd6-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-117">Description</span></span>

<span data-ttu-id="a7cd6-118">Bu hizmet, daha önce açılmış veya Flash örneğini kapatır.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-118">This service closes the previously opened NOR flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-119">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-119">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-120">*nor_flash*: veya Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-120">*nor_flash*: NOR flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-121">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-121">Return Values</span></span>

- <span data-ttu-id="a7cd6-122">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-122">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-123">**LX_ERROR**: (0x01) Flash örneği kapatılırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-123">**LX_ERROR**: (0x01) Error closing flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-124">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-124">Allowed From</span></span>

<span data-ttu-id="a7cd6-125">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-125">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-126">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-126">Example</span></span>

```c
/* Close NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_close(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-127">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-127">See Also</span></span>

- <span data-ttu-id="a7cd6-128">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-128">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-129">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-129">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-130">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-130">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-131">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-131">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-132">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-132">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-133">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-133">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-134">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-134">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="a7cd6-135">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-135">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_defragment"></a><span data-ttu-id="a7cd6-136">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-136">lx_nor_flash_defragment</span></span>

<span data-ttu-id="a7cd6-137">Birleştirme veya Flash örneği</span><span class="sxs-lookup"><span data-stu-id="a7cd6-137">Defragment NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-138">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-138">Prototype</span></span>

```c
UINT lx_nor_flash_defragment(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a><span data-ttu-id="a7cd6-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-139">Description</span></span>

<span data-ttu-id="a7cd6-140">Bu hizmet, daha önce açılan veya Flash örneğini birleştirir.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-140">This service defragments the previously opened NOR flash instance.</span></span> <span data-ttu-id="a7cd6-141">Birleştirme işlemi, boş kesimlerin ve blokların sayısını en üst düzeye çıkarır.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-141">The defragment process maximizes the number of free sectors and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-142">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-142">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-143">*nor_flash*: veya Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-143">*nor_flash*: NOR flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-144">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-144">Return Values</span></span>

- <span data-ttu-id="a7cd6-145">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-145">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-146">**LX_ERROR**: (0x01) Flash örneği birleştirme hatası.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-146">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-147">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-147">Allowed From</span></span>

<span data-ttu-id="a7cd6-148">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-148">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-149">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-149">Example</span></span>

```c
/* Defragment NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_defragment(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-150">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-150">See Also</span></span>

- <span data-ttu-id="a7cd6-151">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-151">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-152">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-152">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-153">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-153">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-154">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-154">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-155">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-155">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-156">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-156">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-157">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-157">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="a7cd6-158">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-158">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_extended_cache_enable"></a><span data-ttu-id="a7cd6-159">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-159">lx_nor_flash_extended_cache_enable</span></span>

<span data-ttu-id="a7cd6-160">Genişletilmiş ve önbelleği etkinleştir/devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="a7cd6-160">Enable/disable extended NOR cache</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-161">Prototype</span></span>

```c
UINT lx_nor_flash_extended_cache_enable(
    LX_NOR_FLASH *nor_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="a7cd6-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-162">Description</span></span>

<span data-ttu-id="a7cd6-163">Bu hizmet, uygulama tarafından sağlanan belleği kullanarak RAM 'de bir veya kesim önbelleği katmanı uygular.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-163">This service implements a NOR sector cache layer in RAM using the memory supplied by the application.</span></span> <span data-ttu-id="a7cd6-164">Sağlanan her 512 bayt belleği, Önbelleğe alınabilecek bir veya kesime dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-164">Each 512 bytes of memory supplied translates to one NOR sector that can be cached.</span></span> <span data-ttu-id="a7cd6-165">Önbelleğe alınan kesimler, blok denetim bilgilerini, örneğin, silme sayısını, serbest sektör eşlemesini ve sektör eşleme bilgilerini içeren olanlardır.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-165">The sectors cached are those that contain the block control information, e.g., erase count, free sector map, and sector mapping information.</span></span> <span data-ttu-id="a7cd6-166">Veri kesimleri bu önbellekte depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-166">Data sectors are not stored in this cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-167">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-167">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-168">**nor_flash**: veya Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-168">**nor_flash**: NOR flash instance pointer.</span></span>  
- <span data-ttu-id="a7cd6-169">**bellek**:, ulong erişimi için hizalanmış önbellek belleği için başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-169">**memory**: Starting address for cache memory, aligned for ULONG access.</span></span> <span data-ttu-id="a7cd6-170">LX_NULL değeri önbelleği devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-170">A value of LX_NULL disables the cache.</span></span>  
- <span data-ttu-id="a7cd6-171">**Boyut**: sağlanan belleğin bayt cinsinden boyutu (512 baytın katlarından biri olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="a7cd6-171">**size**: The size in bytes of the memory supplied (should be multiple of 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-172">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-172">Return Values</span></span>

- <span data-ttu-id="a7cd6-173">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-173">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-174">**LX_ERROR**: (0x01) bir veya kesimi için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-174">**LX_ERROR**: (0x01) Not enough memory for one NOR sector.</span></span>
- <span data-ttu-id="a7cd6-175">**LX_DISABLED**: (0x09) veya genişletilmiş önbellek yapılandırma seçeneği tarafından devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-175">**LX_DISABLED**: (0x09) NOR extended cache disabled by configuration option.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-176">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-176">Allowed From</span></span>

<span data-ttu-id="a7cd6-177">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-177">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-178">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-178">Example</span></span>

```c
/* Enable the NOR flash cache for the instance "my_nor_flash". */  
status = lx_nor_flash_extended_cache_enable(&my_nor_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-179">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-179">See Also</span></span>

- <span data-ttu-id="a7cd6-180">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-180">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-181">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-181">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-182">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-182">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-183">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-183">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-184">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-184">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-185">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-185">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-186">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-186">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="a7cd6-187">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-187">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_initialize"></a><span data-ttu-id="a7cd6-188">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-188">lx_nor_flash_initialize</span></span>

<span data-ttu-id="a7cd6-189">Başlatma veya Flash desteği</span><span class="sxs-lookup"><span data-stu-id="a7cd6-189">Initialize NOR flash support</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-190">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-190">Prototype</span></span>

```c
UINT lx_nor_flash_initialize(void);
```

### <a name="description"></a><span data-ttu-id="a7cd6-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-191">Description</span></span>

<span data-ttu-id="a7cd6-192">Bu hizmet, LevelX veya Flash desteğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-192">This service initializes LevelX NOR flash support.</span></span> <span data-ttu-id="a7cd6-193">Diğer bir LevelX ve API 'lerden önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-193">It must be called before any other LevelX NOR APIs.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-194">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-194">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-195">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="a7cd6-195">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-196">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-196">Return Values</span></span>

- <span data-ttu-id="a7cd6-197">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-197">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-198">**LX_ERROR**: (0x01) hata veya Flash desteği başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-198">**LX_ERROR**: (0x01) Error initializing NOR flash support.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-199">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-199">Allowed From</span></span>

<span data-ttu-id="a7cd6-200">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-200">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-201">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-201">Example</span></span>

```c
/* Initialize NOR flash support. */  
status = lx_nor_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-202">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-202">See Also</span></span>

- <span data-ttu-id="a7cd6-203">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-203">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-204">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-204">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-205">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-205">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-206">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-206">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-207">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-207">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-208">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-208">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-209">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-209">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="a7cd6-210">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-210">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_open"></a><span data-ttu-id="a7cd6-211">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-211">lx_nor_flash_open</span></span>

<span data-ttu-id="a7cd6-212">Açık veya Flash örneği</span><span class="sxs-lookup"><span data-stu-id="a7cd6-212">Open NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-213">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-213">Prototype</span></span>

```c
UINT lx_nor_flash_open(
    LX_NOR_FLASH *nor_flash, 
    CHAR *name,  
    UINT (*nor_driver_initialize) (LX_NOR_FLASH *));
```

### <a name="description"></a><span data-ttu-id="a7cd6-214">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-214">Description</span></span>

<span data-ttu-id="a7cd6-215">Bu hizmet, belirtilen veya Flash denetim bloğu ve sürücü başlatma işlevi ile bir veya Flash örneği açar.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-215">This service opens a NOR flash instance with the specified NOR flash control block and driver initialization function.</span></span> <span data-ttu-id="a7cd6-216">Sürücü başlatma işlevinin, bu veya Flash örneğiyle ilişkili veya donanımı okuma, yazma ve silme blokları için çeşitli işlev işaretçileri yüklememesinden sorumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-216">Note that the driver initialization function is responsible for installing various function pointers for reading, writing, and erasing blocks of the NOR hardware associated with this NOR flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-217">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-217">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-218">*nor_flash*: veya Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-218">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="a7cd6-219">*ad*: veya Flash örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-219">*name*: Name of NOR flash instance.</span></span>
- <span data-ttu-id="a7cd6-220">*nor_driver_initialize*: Işlev işaretçisi veya Flash sürücü başlatma işlevi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-220">*nor_driver_initialize*: Function pointer to NOR flash driver Initialization function.</span></span> <span data-ttu-id="a7cd6-221">VEYA Flash sürücü sorumlulukları hakkında daha fazla bilgi için lütfen bu kılavuzun Bölüm 5 ' e bakın.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-221">Please refer to Chapter 5 of this guide for more details on NOR flash driver responsibilities.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-222">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-222">Return Values</span></span>

- <span data-ttu-id="a7cd6-223">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-223">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-224">**LX_ERROR**: (0x01) veya Flash örneği açılırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-224">**LX_ERROR**: (0x01) Error opening NOR flash instance.</span></span>
- <span data-ttu-id="a7cd6-225">**LX_NO_MEMORY**: (0x08) sürücü, None kesimini RAM 'e okumak için arabellek sağlamadı.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-225">**LX_NO_MEMORY**:  (0x08) Driver did not provide buffer for reading none sector into RAM.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-226">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-226">Allowed From</span></span>

<span data-ttu-id="a7cd6-227">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-227">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-228">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-228">Example</span></span>

```c
/* Open NOR flash instance "my_nor_flash" with the driver "my_nor_driver_initialize". */  
status = lx_nor_flash_open(&my_nor_flash,"my NOR flash",  
    my_nor_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-229">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-229">See Also</span></span>

- <span data-ttu-id="a7cd6-230">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-230">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-231">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-231">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-232">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-232">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-233">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-233">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-234">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-234">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-235">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-235">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-236">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-236">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="a7cd6-237">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-237">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_partial_defragment"></a><span data-ttu-id="a7cd6-238">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-238">lx_nor_flash_partial_defragment</span></span>

<span data-ttu-id="a7cd6-239">VEYA Flash örneğinin kısmi birleştirmesi</span><span class="sxs-lookup"><span data-stu-id="a7cd6-239">Partial defragment of NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-240">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-240">Prototype</span></span>

```c
UINT lx_nor_flash_partial_defragment(
    LX_NOR_FLASH *nor_flash, 
    UINT max_blocks);
```

### <a name="description"></a><span data-ttu-id="a7cd6-241">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-241">Description</span></span>

<span data-ttu-id="a7cd6-242">Bu hizmet, önceden açılmış veya Flash örneğini belirtilen en fazla blok sayısına kadar birleştirir.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-242">This service defragments the previously opened NOR flash instance up to the maximum number of blocks specified.</span></span> <span data-ttu-id="a7cd6-243">Birleştirme işlemi, boş kesimlerin ve blokların sayısını en üst düzeye çıkarır.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-243">The defragment process maximizes the number of free sectors and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-244">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-244">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-245">*nor_flash*: veya Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-245">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="a7cd6-246">*max_blocks*: en fazla blok sayısı.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-246">*max_blocks*: Maximum number of blocks.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-247">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-247">Return Values</span></span>

- <span data-ttu-id="a7cd6-248">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-248">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-249">**LX_ERROR**: (0x01) Flash örneği birleştirme hatası.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-249">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-250">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-250">Allowed From</span></span>

<span data-ttu-id="a7cd6-251">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-251">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-252">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-252">Example</span></span>

```c
/* Defragment of one block in NOR flash instance* *"my_nor_flash". */  
status = lx_nor_flash_partial_defragment(&my_nor_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-253">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-253">See Also</span></span>

- <span data-ttu-id="a7cd6-254">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-254">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-255">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-255">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-256">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-256">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-257">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-257">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-258">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-258">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-259">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-259">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-260">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-260">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="a7cd6-261">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-261">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_sector_read"></a><span data-ttu-id="a7cd6-262">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-262">lx_nor_flash_sector_read</span></span>

<span data-ttu-id="a7cd6-263">Okuma veya Flash sektörü</span><span class="sxs-lookup"><span data-stu-id="a7cd6-263">Read NOR flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-264">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-264">Prototype</span></span>

```c
UINT lx_nor_flash_sector_read(
    LX_NOR_FLASH *nor_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="a7cd6-265">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-265">Description</span></span>

<span data-ttu-id="a7cd6-266">Bu hizmet, mantıksal kesimi veya Flash örneğinden okur ve başarılı olursa sağlanan arabellekteki içeriği döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-266">This service reads the logical sector from the NOR flash instance and if successful returns the contents in the supplied buffer.</span></span> <span data-ttu-id="a7cd6-267">Bu ve sektör boyutunun her zaman 512 bayt olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-267">Note that NOR sector size is always 512 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-268">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-268">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-269">*nor_flash* VEYA Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-269">*nor_flash* NOR flash instance pointer.</span></span>
- <span data-ttu-id="a7cd6-270">*logical_sector*: okunacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-270">*logical_sector*: Logical sector to read.</span></span>
- <span data-ttu-id="a7cd6-271">*buffer*: mantıksal sektörün içerikleri için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-271">*buffer*: Pointer to destination for contents of the logical sector.</span></span> <span data-ttu-id="a7cd6-272">Arabelleğin 512 bayt olduğunu ve ULONG erişimi için hizalandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-272">Note that the buffer is assumed to be 512 bytes and aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-273">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-273">Return Values</span></span>

- <span data-ttu-id="a7cd6-274">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-274">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-275">**LX_ERROR**: (0x01) veya Flash kesimini okuma hatası.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-275">**LX_ERROR**: (0x01) Error reading NOR flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-276">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-276">Allowed From</span></span>

<span data-ttu-id="a7cd6-277">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-278">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-278">Example</span></span>

```c
/* Read logical sector 20 of the NOR flash instance "my_nor_flash" and place contents in "buffer". */ 
status = lx_nor_flash_sector_read(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contents of logical sector 20. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-279">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-279">See Also</span></span>

- <span data-ttu-id="a7cd6-280">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-280">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-281">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-281">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-282">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-282">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-283">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-283">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-284">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-284">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-285">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-285">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-286">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-286">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="a7cd6-287">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-287">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_sector_release"></a><span data-ttu-id="a7cd6-288">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-288">lx_nor_flash_sector_release</span></span>

<span data-ttu-id="a7cd6-289">Yayın veya Flash sektörü</span><span class="sxs-lookup"><span data-stu-id="a7cd6-289">Release NOR flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-290">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-290">Prototype</span></span>

```c
UINT lx_nor_flash_sector_release(
    LX_NOR_FLASH *nor_flash,
    ULONG logical_sector);
```

### <a name="description"></a><span data-ttu-id="a7cd6-291">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-291">Description</span></span>

<span data-ttu-id="a7cd6-292">Bu hizmet, veya Flash örneğindeki mantıksal kesim eşlemesini yayınlar.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-292">This service releases the logical sector mapping in the NOR flash instance.</span></span> <span data-ttu-id="a7cd6-293">Kullanılmayan bir mantıksal kesimi serbest bırakmak, LevelX aşumu seviyelendirmenin daha verimli olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-293">Releasing a logical sector when not used makes the LevelX wear leveling more efficient.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-294">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-294">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-295">*nor_flash*: veya Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-295">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="a7cd6-296">*logical_sector*: serbest bırakmak için mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-296">*logical_sector*: Logical sector to release.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-297">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-297">Return Values</span></span>

- <span data-ttu-id="a7cd6-298">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-298">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-299">**LX_ERROR**: (0x01) hata veya Flash kesim yazma.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-299">**LX_ERROR**: (0x01) Error NOR flash sector write.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-300">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-300">Allowed From</span></span>

<span data-ttu-id="a7cd6-301">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-302">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-302">Example</span></span>

```c
/* Release logical sector 20 of the NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_sector_release(&my_nor_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-303">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-303">See Also</span></span>

- <span data-ttu-id="a7cd6-304">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-304">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-305">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-305">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-306">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-306">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-307">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-307">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-308">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-308">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-309">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-309">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-310">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-310">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-311">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-311">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_sector_write"></a><span data-ttu-id="a7cd6-312">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="a7cd6-312">lx_nor_flash_sector_write</span></span>

<span data-ttu-id="a7cd6-313">Yazma veya Flash sektörü</span><span class="sxs-lookup"><span data-stu-id="a7cd6-313">Write NOR flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="a7cd6-314">Prototype</span><span class="sxs-lookup"><span data-stu-id="a7cd6-314">Prototype</span></span>

```c
UINT lx_nor_flash_sector_write(
    LX_nor_FLASH *NOR_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="a7cd6-315">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7cd6-315">Description</span></span>

<span data-ttu-id="a7cd6-316">Bu hizmet, veya Flash örneğinde belirtilen mantıksal kesimi yazar.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-316">This service writes the specified logical sector in the NOR flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7cd6-317">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-317">Input Parameters</span></span>

- <span data-ttu-id="a7cd6-318">*nor_flash*: veya Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-318">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="a7cd6-319">*logical_sector*: yazılacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-319">*logical_sector*: Logical sector to write.</span></span>
- <span data-ttu-id="a7cd6-320">*buffer*: mantıksal sektörün içeriğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-320">*buffer*: Pointer to the contents of the logical sector.</span></span> <span data-ttu-id="a7cd6-321">Arabelleğin, ULONG erişimi için 512 bayt hizalı kabul edilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-321">Note that the buffer is assumed to be 512 bytes aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7cd6-322">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="a7cd6-322">Return Values</span></span>

- <span data-ttu-id="a7cd6-323">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-323">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="a7cd6-324">**LX_NO_SECTORS**: (0x02) yazma işlemini gerçekleştirmek için kullanılabilir daha fazla boş sektör yok.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-324">**LX_NO_SECTORS**: (0x02) No more free sectors are available to perform the write.</span></span>
- <span data-ttu-id="a7cd6-325">**LX_ERROR**: (0x01) veya Flash kesimini serbest bırakma hatası.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-325">**LX_ERROR**: (0x01) Error releasing NOR flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7cd6-326">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="a7cd6-326">Allowed From</span></span>

<span data-ttu-id="a7cd6-327">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="a7cd6-327">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7cd6-328">Örnek</span><span class="sxs-lookup"><span data-stu-id="a7cd6-328">Example</span></span>

```c
/* Write logical sector 20 of the NOR flash instance "my_nor_flash" with the contents pointed to by "buffer". */ 
status = lx_nor_flash_sector_write(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a><span data-ttu-id="a7cd6-329">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a7cd6-329">See Also</span></span>

- <span data-ttu-id="a7cd6-330">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="a7cd6-330">lx_nor_flash_close</span></span>
- <span data-ttu-id="a7cd6-331">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-331">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="a7cd6-332">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="a7cd6-332">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="a7cd6-333">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="a7cd6-333">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="a7cd6-334">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="a7cd6-334">lx_nor_flash_open</span></span>
- <span data-ttu-id="a7cd6-335">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="a7cd6-335">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="a7cd6-336">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="a7cd6-336">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="a7cd6-337">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="a7cd6-337">lx_nor_flash_sector_release</span></span>
