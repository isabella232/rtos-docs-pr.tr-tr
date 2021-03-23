---
title: Bölüm 4-Azure RTOS LevelX nve API 'Leri
description: Azure RTOS LevelX nve uygulama için kullanılabilir API 'Ler.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 73bb94768396b4b8461791a164a102d1f8ef159f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827064"
---
# <a name="chapter-4---azure-rtos-levelx-nand-apis"></a><span data-ttu-id="bf04b-103">Bölüm 4-Azure RTOS LevelX nve API 'Leri</span><span class="sxs-lookup"><span data-stu-id="bf04b-103">Chapter 4 - Azure RTOS LevelX NAND APIs</span></span>

<span data-ttu-id="bf04b-104">Uygulamanın kullanabildiği Azure RTOS LevelX nve API 'Leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bf04b-104">The Azure RTOS LevelX NAND APIs available to the application are:</span></span>

- <span data-ttu-id="bf04b-105">\***lx_nand_flash_close** _: _CLOSE nve Flash örneği \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-105">***lx_nand_flash_close** _: _Close NAND flash instance*</span></span>
- <span data-ttu-id="bf04b-106">\***lx_nand_flash_defragment** _: _Defragment nve Flash örneği \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-106">***lx_nand_flash_defragment** _: _Defragment NAND flash instance*</span></span>
- <span data-ttu-id="bf04b-107">\***lx_nand_flash_extended_cache_enable** _: _Enable/GENIŞLETILMIŞ nve önbelleğini devre dışı bırak \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-107">***lx_nand_flash_extended_cache_enable** _: _Enable/disable extended NAND cache*</span></span>
- <span data-ttu-id="bf04b-108">\***lx_nand_flash_initialize** _: _Initialize nve Flash desteği \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-108">***lx_nand_flash_initialize** _: _Initialize NAND flash support*</span></span>
- <span data-ttu-id="bf04b-109">\***lx_nand_flash_open** _: _OPEN nve Flash örneği \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-109">***lx_nand_flash_open** _: _Open NAND flash instance*</span></span>
- <span data-ttu-id="bf04b-110">\***lx_nand_flash_page_ecc_check** _: düzeltme ile ECC hataları için _Check sayfası</span><span class="sxs-lookup"><span data-stu-id="bf04b-110">***lx_nand_flash_page_ecc_check** _: _Check page for ECC errors with correction*</span></span>
- <span data-ttu-id="bf04b-111">\***lx_nand_flash_page_ecc_compute** _: sayfa \* IÇIN _Computes ECC</span><span class="sxs-lookup"><span data-stu-id="bf04b-111">***lx_nand_flash_page_ecc_compute** _: _Computes ECC for page*</span></span>
- <span data-ttu-id="bf04b-112">\***lx_nand_flash_partial_defragment** _: nve flash örneğinin _Partial birleştirme \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-112">***lx_nand_flash_partial_defragment** _: _Partial defragment of NAND flash instance*</span></span>
- <span data-ttu-id="bf04b-113">\***lx_nand_flash_sector_read** _: _read nve Flash sektörü \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-113">***lx_nand_flash_sector_read** _: _Read NAND flash sector*</span></span>
- <span data-ttu-id="bf04b-114">\***lx_nand_flash_sector_release** _: _Release nve Flash sektörü \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-114">***lx_nand_flash_sector_release** _: _Release NAND flash sector*</span></span>
- <span data-ttu-id="bf04b-115">\***lx_nand_flash_sector_write** _: _WRITE nve Flash sektörü \*</span><span class="sxs-lookup"><span data-stu-id="bf04b-115">***lx_nand_flash_sector_write** _: _Write NAND flash sector*</span></span>

## <a name="lx_nand_flash_close"></a><span data-ttu-id="bf04b-116">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-116">lx_nand_flash_close</span></span>

<span data-ttu-id="bf04b-117">NVE Flash örneğini kapat</span><span class="sxs-lookup"><span data-stu-id="bf04b-117">Close NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-118">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-118">Prototype</span></span>

```c
UINT lx_nand_flash_close(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a><span data-ttu-id="bf04b-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-119">Description</span></span>

<span data-ttu-id="bf04b-120">Bu hizmet, daha önce açılmış nve Flash örneğini kapatır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-120">This service closes the previously opened NAND flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-121">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-121">Input Parameters</span></span>

- <span data-ttu-id="bf04b-122">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-122">**nand_flash**: NAND flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-123">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-123">Return Values</span></span>

- <span data-ttu-id="bf04b-124">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-124">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-125">**LX_ERROR**: (0x01) Flash örneği kapatılırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="bf04b-125">**LX_ERROR**: (0x01) Error closing flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-126">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-126">Allowed From</span></span>

<span data-ttu-id="bf04b-127">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-127">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-128">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-128">Example</span></span>

```c
/* Close NAND flash instance "my_nand_flash". */
status = lx_nand_flash_close(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-129">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-129">See Also</span></span>

- <span data-ttu-id="bf04b-130">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-130">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-131">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-131">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-132">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-132">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-133">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-133">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-134">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-134">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-135">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-135">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-136">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-136">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-137">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-137">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-138">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-138">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-139">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-139">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_defragment"></a><span data-ttu-id="bf04b-140">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-140">lx_nand_flash_defragment</span></span>

<span data-ttu-id="bf04b-141">NVE Flash örneğini birleştirin</span><span class="sxs-lookup"><span data-stu-id="bf04b-141">Defragment NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-142">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-142">Prototype</span></span>

```c
UINT lx_nand_flash_defragment(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a><span data-ttu-id="bf04b-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-143">Description</span></span>

<span data-ttu-id="bf04b-144">Bu hizmet, daha önce açılan nve Flash örneğini birleştirir.</span><span class="sxs-lookup"><span data-stu-id="bf04b-144">This service defragments the previously opened NAND flash instance.</span></span> <span data-ttu-id="bf04b-145">Birleştirme işlemi, serbest sayfa ve blok sayısını en üst düzeye çıkarır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-145">The defragment process maximizes the number of free pages and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-146">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-146">Input Parameters</span></span>

- <span data-ttu-id="bf04b-147">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-147">**nand_flash**: NAND flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-148">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-148">Return Values</span></span>

- <span data-ttu-id="bf04b-149">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-149">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-150">**LX_ERROR**: (0x01) Flash örneği birleştirme hatası.</span><span class="sxs-lookup"><span data-stu-id="bf04b-150">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-151">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-151">Allowed From</span></span>

<span data-ttu-id="bf04b-152">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-152">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-153">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-153">Example</span></span>

```c
/* Defragment NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_defragment(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-154">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-154">See Also</span></span>

- <span data-ttu-id="bf04b-155">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-155">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-156">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-156">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-157">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-157">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-158">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-158">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-159">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-159">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-160">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-160">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-161">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-161">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-162">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-162">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-163">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-163">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-164">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-164">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_extended_cache_enable"></a><span data-ttu-id="bf04b-165">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-165">lx_nand_flash_extended_cache_enable</span></span>

<span data-ttu-id="bf04b-166">Genişletilmiş nve önbelleği etkinleştir/devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="bf04b-166">Enable/disable extended NAND cache</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-167">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-167">Prototype</span></span>

```c
UINT lx_nand_flash_extended_cache_enable(
    LX_NAND_FLASH
    *nand_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="bf04b-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-168">Description</span></span>

<span data-ttu-id="bf04b-169">Bu hizmet, uygulama tarafından sağlanan belleği kullanarak RAM 'de bir önbellek katmanı uygular.</span><span class="sxs-lookup"><span data-stu-id="bf04b-169">This service implements a cache layer in RAM using the memory supplied by the application.</span></span> <span data-ttu-id="bf04b-170">Tam önbellek işlemi için gereken toplam bellek miktarı şu şekilde hesaplanabilir:</span><span class="sxs-lookup"><span data-stu-id="bf04b-170">The total amount of memory required for full cache operation can be calculated as follows:</span></span>

```c
size (in_bytes) = number_of_blocks (rounded up to be divisible by 4) +  
    ((number_of_blocks * pages_per_block) * 4)  +  
    ((number_of_blocks * (pages_per_block + 1)) * 4)
```

<span data-ttu-id="bf04b-171">Sağlanan bellek tam nve önbelleğe uyum sağlayacak kadar büyük değilse, bu yordam sağlanan belleğe göre nve Flash önbelleğinin büyük bir kısmını mümkün olduğunca etkinleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="bf04b-171">If the supplied memory is not large enough to accommodate the full NAND cache, this routine will enable as much of the NAND flash cache as possible based on the memory supplied.</span></span>

<span data-ttu-id="bf04b-172">Belirtilen bellek adresi NULL ise nve önbelleği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-172">The NAND cache is disabled if the memory address specified is NULL.</span></span> <span data-ttu-id="bf04b-173">Bu nedenle, nve önbelleği geçici bir biçimde kullanılıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="bf04b-173">Hence, the NAND cache maybe be used in a temporary fashion.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-174">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-174">Input Parameters</span></span>

- <span data-ttu-id="bf04b-175">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-175">**nand_flash**: NAND flash instance pointer.</span></span>  
- <span data-ttu-id="bf04b-176">**bellek**: ulong erişimi için hizalanmış önbellek belleği için başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-176">**memory**: Starting address for cache memory aligned for ULONG access.</span></span> <span data-ttu-id="bf04b-177">LX_NULL değeri önbelleği devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-177">A value of LX_NULL disables the cache.</span></span>  
- <span data-ttu-id="bf04b-178">**Boyut**: sağlanan belleğin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="bf04b-178">**size**: The size in bytes of the memory supplied.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-179">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-179">Return Values</span></span>

- <span data-ttu-id="bf04b-180">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-180">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-181">**LX_ERROR**: (0x01) nve önbelleğinin bir öğesi için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="bf04b-181">**LX_ERROR**: (0x01) Not enough memory for one element of the NAND cache.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-182">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-182">Allowed From</span></span>

<span data-ttu-id="bf04b-183">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-183">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-184">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-184">Example</span></span>

```c
/* Enable the NAND flash cache for the instance "my_nand_flash". */
status = lx_nand_flash_extended_cache_enable(&my_nand_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-185">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-185">See Also</span></span>

- <span data-ttu-id="bf04b-186">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-186">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-187">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-187">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-188">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-188">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-189">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-189">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-190">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-190">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-191">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-191">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-192">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-192">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-193">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-193">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-194">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-194">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-195">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-195">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_initialize"></a><span data-ttu-id="bf04b-196">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-196">lx_nand_flash_initialize</span></span>

<span data-ttu-id="bf04b-197">NVE Flash desteğini başlatma</span><span class="sxs-lookup"><span data-stu-id="bf04b-197">Initialize NAND flash support</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-198">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-198">Prototype</span></span>

```c
UINT lx_nand_flash_initialize(void);
```

### <a name="description"></a><span data-ttu-id="bf04b-199">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-199">Description</span></span>

<span data-ttu-id="bf04b-200">Bu hizmet, LevelX nve Flash desteğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-200">This service initializes LevelX NAND flash support.</span></span> <span data-ttu-id="bf04b-201">Diğer bir LevelX nve API 'lerden önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-201">It must be called before any other LevelX NAND APIs.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-202">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-202">Input Parameters</span></span>

- <span data-ttu-id="bf04b-203">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="bf04b-203">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-204">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-204">Return Values</span></span>

- <span data-ttu-id="bf04b-205">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-205">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-206">**LX_ERROR**: (0x01) nve Flash desteği başlatılırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="bf04b-206">**LX_ERROR**: (0x01) Error initializing NAND flash support.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-207">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-207">Allowed From</span></span>

<span data-ttu-id="bf04b-208">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-208">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-209">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-209">Example</span></span>

```c
/* Initialize NAND flash support. */
status = lx_nand_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-210">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-210">See Also</span></span>

- <span data-ttu-id="bf04b-211">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-211">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-212">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-212">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-213">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-213">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-214">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-214">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-215">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-215">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-216">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-216">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-217">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-217">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-218">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-218">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-219">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-219">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-220">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-220">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_open"></a><span data-ttu-id="bf04b-221">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-221">lx_nand_flash_open</span></span>

<span data-ttu-id="bf04b-222">NVE Flash örneğini aç</span><span class="sxs-lookup"><span data-stu-id="bf04b-222">Open NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-223">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-223">Prototype</span></span>

```c
UINT lx_nand_flash_open(
    LX_NAND_FLASH *nand_flash, 
    CHAR *name,  
    UINT (*nand_driver_initialize) (LX_NAND_FLASH *));
```

### <a name="description"></a><span data-ttu-id="bf04b-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-224">Description</span></span>

<span data-ttu-id="bf04b-225">Bu hizmet, belirtilen nve Flash denetim bloğu ve sürücü başlatma işlevi ile bir nve Flash örneği açar.</span><span class="sxs-lookup"><span data-stu-id="bf04b-225">This service opens a NAND flash instance with the specified NAND flash control block and driver initialization function.</span></span> <span data-ttu-id="bf04b-226">Sürücü başlatma işlevinin, bu nve Flash örneğiyle ilişkili nve donanımının blok/sayfalarını okuma, yazma ve silme işlemleri için çeşitli işlev işaretçileri yüklememesinden sorumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bf04b-226">Note that the driver initialization function is responsible for installing various function pointers for reading, writing, and erasing blocks/pages of the NAND hardware associated with this NAND flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-227">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-227">Input Parameters</span></span>

- <span data-ttu-id="bf04b-228">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-228">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="bf04b-229">**ad**: nve Flash örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="bf04b-229">**name**: Name of NAND flash instance.</span></span>
- <span data-ttu-id="bf04b-230">**nand_driver_initialize**: nve Flash sürücü başlatma işlevine işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-230">**nand_driver_initialize**: Function pointer to NAND flash driver initialization function.</span></span> <span data-ttu-id="bf04b-231">NVE Flash sürücü sorumlulukları hakkında daha fazla bilgi için lütfen bu kılavuzun Bölüm 3 ' e başvurun.</span><span class="sxs-lookup"><span data-stu-id="bf04b-231">Please refer to Chapter 3 of this guide for more details on NAND flash driver responsibilities.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-232">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-232">Return Values</span></span>

- <span data-ttu-id="bf04b-233">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-233">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-234">**LX_ERROR**: (0x01) nve Flash örneği açılırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="bf04b-234">**LX_ERROR**: (0x01) Error opening NAND flash instance.</span></span>
- <span data-ttu-id="bf04b-235">**LX_NO_MEMORY**: (0x08) sürücü, BIR sayfayı RAM 'e okumak için arabellek sağlamadı.</span><span class="sxs-lookup"><span data-stu-id="bf04b-235">**LX_NO_MEMORY**: (0x08) Driver did not provide buffer for reading one page into RAM.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-236">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-236">Allowed From</span></span>

<span data-ttu-id="bf04b-237">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-237">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-238">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-238">Example</span></span>

```c
/* Open NAND flash instance "my_nand_flash" with the driver "my_nand_driver_initialize". */ 
status = lx_nand_flash_open(&my_nand_flash,"my nand flash",  
    my_nand_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-239">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-239">See Also</span></span>

- <span data-ttu-id="bf04b-240">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-240">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-241">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-241">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-242">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-242">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-243">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-243">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-244">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-244">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-245">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-245">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-246">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-246">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-247">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-247">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-248">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-248">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-249">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-249">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_page_ecc_check"></a><span data-ttu-id="bf04b-250">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-250">lx_nand_flash_page_ecc_check</span></span>

<span data-ttu-id="bf04b-251">Düzeltme ile ECC hataları için sayfayı denetle</span><span class="sxs-lookup"><span data-stu-id="bf04b-251">Check page for ECC errors with correction</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-252">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-252">Prototype</span></span>

```c
UINT lx_nand_flash_page_ecc_check(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a><span data-ttu-id="bf04b-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-253">Description</span></span>

<span data-ttu-id="bf04b-254">Bu hizmet sağlanan ECC ile sağlanan nve sayfa arabelleğinin bütünlüğünü doğrular.</span><span class="sxs-lookup"><span data-stu-id="bf04b-254">This service verifies the integrity of the supplied NAND page buffer with the supplied ECC.</span></span> <span data-ttu-id="bf04b-255">Sayfa boyutu (nve Flash örneği İşaretçisinde tanımlanmıştır), 256 baytlık bir katı kabul edilir ve sağlanan ECC kodu, sayfanın her 256-Byte bölümünde 1 bit hatası düzeltiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="bf04b-255">Page size (defined in the NAND flash instance pointer) is assumed to be a multiple of 256-bytes and the ECC code supplied is capable of correcting a 1 bit error in each 256-byte portion of the page.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-256">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-256">Input Parameters</span></span>

- <span data-ttu-id="bf04b-257">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-257">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="bf04b-258">**page_buffer**: nve Flash sayfa arabelleğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-258">**page_buffer**: Pointer to NAND flash page buffer.</span></span>
- <span data-ttu-id="bf04b-259">**ecc_buffer**: nve Flash SAYFASıNA yönelik ECC işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-259">**ecc_buffer**: Pointer to ECC for NAND flash page.</span></span> <span data-ttu-id="bf04b-260">Sayfanın 256 baytlık bölümü başına 3 ECC bayt olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bf04b-260">Note that there are 3 ECC bytes per 256-byte portion of the page.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-261">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-261">Return Values</span></span>

- <span data-ttu-id="bf04b-262">**LX_SUCCESS**: (0x00) nve sayfasında hata yok.</span><span class="sxs-lookup"><span data-stu-id="bf04b-262">**LX_SUCCESS**: (0x00) NAND page has no errors.</span></span>
- <span data-ttu-id="bf04b-263">**LX_NAND_ERROR_CORRECTED**: (0x06) nve sayfasında 1 bitlik bir hata düzeltildi — düzeltmeler sayfa arabelleğinde.</span><span class="sxs-lookup"><span data-stu-id="bf04b-263">**LX_NAND_ERROR_CORRECTED**: (0x06) One or more 1-bit errors were corrected in the NAND page—correction(s) are in the page buffer.</span></span>
- <span data-ttu-id="bf04b-264">**LX_NAND_ERROR_NOT_CORRECTED**: (0x07) nve sayfasında düzeltmeniz için çok fazla hata var.</span><span class="sxs-lookup"><span data-stu-id="bf04b-264">**LX_NAND_ERROR_NOT_CORRECTED**: (0x07) Too many errors to correct on the NAND page.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-265">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-265">Allowed From</span></span>

<span data-ttu-id="bf04b-266">LevelX sürücüsü</span><span class="sxs-lookup"><span data-stu-id="bf04b-266">LevelX Driver</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-267">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-267">Example</span></span>

```c
/* Check the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash" . */
status = lx_nand_flash_page_ecc_check(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the page is valid. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-268">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-268">See Also</span></span>

- <span data-ttu-id="bf04b-269">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-269">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-270">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-270">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-271">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-271">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-272">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-272">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-273">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-273">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-274">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-274">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-275">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-275">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-276">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-276">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-277">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-277">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-278">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-278">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_page_ecc_compute"></a><span data-ttu-id="bf04b-279">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-279">lx_nand_flash_page_ecc_compute</span></span>

<span data-ttu-id="bf04b-280">Sayfa için işlem ECC</span><span class="sxs-lookup"><span data-stu-id="bf04b-280">Compute ECC for page</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-281">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-281">Prototype</span></span>

```c
UINT lx_nand_flash_page_ecc_compute(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a><span data-ttu-id="bf04b-282">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-282">Description</span></span>

<span data-ttu-id="bf04b-283">Bu hizmet, sağlanan nve sayfa arabelleğinin ECC 'sini hesaplar ve sağlanan ECC arabelleğindeki ECC 'yi döndürür.</span><span class="sxs-lookup"><span data-stu-id="bf04b-283">This service computes the ECC of the supplied NAND page buffer and returns the ECC in the supplied ECC buffer.</span></span> <span data-ttu-id="bf04b-284">Sayfa boyutu, 256 baytlık bir (nve Flash örnek İşaretçisinde tanımlanan) bir katı kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="bf04b-284">Page size is assume to be a multiple of 256-bytes (defined in the NAND flash instance pointer).</span></span> <span data-ttu-id="bf04b-285">ECC kodu, sayfanın daha sonra okunışında bütünlüğünü doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-285">The ECC code is used to verify the integrity of the page when it is read at a later time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-286">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-286">Input Parameters</span></span>

- <span data-ttu-id="bf04b-287">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-287">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="bf04b-288">**page_buffer**: nve Flash sayfa arabelleğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-288">**page_buffer**: Pointer to NAND flash page buffer.</span></span>
- <span data-ttu-id="bf04b-289">**ecc_buffer**: nve Flash sayfasının ECC 'si için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-289">**ecc_buffer**: Pointer to destination for ECC of the NAND flash page.</span></span> <span data-ttu-id="bf04b-290">Sayfanın 256 baytlık bölümü başına 3 bayt ECC depolaması olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bf04b-290">Note that must be 3 bytes of ECC storage per 256-byte portion of the page.</span></span> <span data-ttu-id="bf04b-291">Örneğin, 2048 baytlık bir sayfa ECC için 24 bayt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bf04b-291">For example, a 2048 byte page would require 24 bytes for the ECC.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-292">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-292">Return Values</span></span>

- <span data-ttu-id="bf04b-293">**LX_SUCCESS**: (0x00) ECC başarıyla hesaplandı.</span><span class="sxs-lookup"><span data-stu-id="bf04b-293">**LX_SUCCESS**: (0x00) ECC successfully calculated.</span></span>
- <span data-ttu-id="bf04b-294">**LX_ERROR**: (0x01) ECC hesaplama hatası.</span><span class="sxs-lookup"><span data-stu-id="bf04b-294">**LX_ERROR**: (0x01) Error calculating ECC.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-295">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-295">Allowed From</span></span>

<span data-ttu-id="bf04b-296">LevelX sürücüsü</span><span class="sxs-lookup"><span data-stu-id="bf04b-296">LevelX Driver</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-297">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-297">Example</span></span>

```c
/* Compute ECC for the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_page_ecc_compute(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the ECC was calculated and Can be found in the memory pointed to by "ecc_pointer." */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-298">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-298">See Also</span></span>

- <span data-ttu-id="bf04b-299">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-299">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-300">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-300">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-301">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-301">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-302">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-302">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-303">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-303">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-304">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-304">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-305">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-305">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-306">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-306">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-307">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-307">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-308">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-308">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_partial_defragment"></a><span data-ttu-id="bf04b-309">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-309">lx_nand_flash_partial_defragment</span></span>

<span data-ttu-id="bf04b-310">NVE Flash örneğinin kısmi birleştirmesi</span><span class="sxs-lookup"><span data-stu-id="bf04b-310">Partial defragment of NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-311">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-311">Prototype</span></span>

```c
UINT lx_nand_flash_partial_defragment(
    LX_NAND_FLASH *nand_flash,  
    UINT max_blocks);
```

### <a name="description"></a><span data-ttu-id="bf04b-312">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-312">Description</span></span>

<span data-ttu-id="bf04b-313">Bu hizmet, önceden açılan nve Flash örneğini belirtilen en fazla blok sayısına kadar birleştirir.</span><span class="sxs-lookup"><span data-stu-id="bf04b-313">This service defragments the previously opened NAND flash instance up to the maximum number of blocks specified.</span></span> <span data-ttu-id="bf04b-314">Birleştirme işlemi, serbest sayfa ve blok sayısını en üst düzeye çıkarır.</span><span class="sxs-lookup"><span data-stu-id="bf04b-314">The defragment process maximizes the number of free pages and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-315">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-315">Input Parameters</span></span>

- <span data-ttu-id="bf04b-316">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-316">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="bf04b-317">**max_blocks**: en fazla blok sayısı.</span><span class="sxs-lookup"><span data-stu-id="bf04b-317">**max_blocks**: Maximum number of blocks.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-318">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-318">Return Values</span></span>

- <span data-ttu-id="bf04b-319">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-319">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-320">**LX_ERROR**: (0x01) Flash örneği birleştirme hatası.</span><span class="sxs-lookup"><span data-stu-id="bf04b-320">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-321">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-321">Allowed From</span></span>

<span data-ttu-id="bf04b-322">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-322">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-323">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-323">Example</span></span>

```c
/* Defragment 1 block of NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_partial_defragment(&my_nand_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-324">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-324">See Also</span></span>

- <span data-ttu-id="bf04b-325">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-325">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-326">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-326">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-327">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-327">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-328">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-328">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-329">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-329">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-330">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-330">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-331">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-331">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-332">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-332">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-333">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-333">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-334">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-334">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_sector_read"></a><span data-ttu-id="bf04b-335">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-335">lx_nand_flash_sector_read</span></span>

<span data-ttu-id="bf04b-336">NVE Flash kesimini oku</span><span class="sxs-lookup"><span data-stu-id="bf04b-336">Read NAND flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-337">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-337">Prototype</span></span>

```c
UINT lx_nand_flash_sector_read(
    LX_NAND_FLASH *nand_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="bf04b-338">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-338">Description</span></span>

<span data-ttu-id="bf04b-339">Bu hizmet, nve Flash örneğinden mantıksal kesimi okur ve başarılı olursa, sağlanan arabellekteki içerik döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bf04b-339">This service reads the logical sector from the NAND flash instance and if successful returns the contents in the supplied buffer.</span></span> <span data-ttu-id="bf04b-340">NVE sektör boyutunun her zaman temeldeki nve donanımın sayfa boyutu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bf04b-340">Note that NAND sector size is always the page size of the underlying NAND hardware.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-341">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-341">Input Parameters</span></span>

- <span data-ttu-id="bf04b-342">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-342">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="bf04b-343">**logical_sector**: okunacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="bf04b-343">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="bf04b-344">**buffer**: mantıksal sektörün içerikleri için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-344">**buffer**: Pointer to destination for contents of the logical sector.</span></span> <span data-ttu-id="bf04b-345">Arabelleğin nve Flash sayfa boyutunun boyutu olduğunu ve ULONG erişimi için hizalandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bf04b-345">Note that the buffer is assumed to be the size of the NAND flash page size and aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-346">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-346">Return Values</span></span>

- <span data-ttu-id="bf04b-347">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-347">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-348">**LX_ERROR**: (0x01) nve Flash sektörü okunurken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="bf04b-348">**LX_ERROR**: (0x01) Error reading NAND flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-349">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-349">Allowed From</span></span>

<span data-ttu-id="bf04b-350">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-350">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-351">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-351">Example</span></span>

```c
/* Read logical sector 20 of the NAND flash instance "my_nand_flash" and place contents in "buffer". */
status = lx_nand_flash_sector_read(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contentsnof logical sector 20. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-352">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-352">See Also</span></span>

- <span data-ttu-id="bf04b-353">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-353">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-354">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-354">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-355">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-355">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-356">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-356">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-357">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-357">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-358">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-358">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-359">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-359">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-360">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-360">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-361">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-361">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="bf04b-362">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-362">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_sector_release"></a><span data-ttu-id="bf04b-363">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-363">lx_nand_flash_sector_release</span></span>

<span data-ttu-id="bf04b-364">Yayın nve Flash sektörü</span><span class="sxs-lookup"><span data-stu-id="bf04b-364">Release NAND flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-365">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-365">Prototype</span></span>

```c
UINT lx_nand_flash_sector_release(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector);
```

### <a name="description"></a><span data-ttu-id="bf04b-366">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-366">Description</span></span>

<span data-ttu-id="bf04b-367">Bu hizmet, nve Flash örneğindeki mantıksal kesim eşlemesini yayınlar.</span><span class="sxs-lookup"><span data-stu-id="bf04b-367">This service releases the logical sector mapping in the NAND flash instance.</span></span> <span data-ttu-id="bf04b-368">Kullanılmayan bir mantıksal kesimi serbest bırakmak, LevelX aşumu seviyelendirmenin daha verimli olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf04b-368">Releasing a logical sector when not used makes the LevelX wear leveling more efficient.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-369">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-369">Input Parameters</span></span>

- <span data-ttu-id="bf04b-370">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-370">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="bf04b-371">**logical_sector**: serbest bırakmak için mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="bf04b-371">**logical_sector**: Logical sector to release.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-372">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-372">Return Values</span></span>

- <span data-ttu-id="bf04b-373">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-373">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-374">**LX_ERROR**: (0x01) hata nve Flash sektör yazma.</span><span class="sxs-lookup"><span data-stu-id="bf04b-374">**LX_ERROR**: (0x01) Error NAND flash sector write.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-375">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-375">Allowed From</span></span>

<span data-ttu-id="bf04b-376">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-376">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-377">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-377">Example</span></span>

```c
/* Release logical sector 20 of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_sector_release(&my_nand_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-378">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-378">See Also</span></span>

- <span data-ttu-id="bf04b-379">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-379">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-380">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-380">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-381">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-381">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-382">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-382">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-383">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-383">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-384">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-384">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-385">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-385">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-386">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-386">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-387">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-387">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-388">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-388">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_sector_write"></a><span data-ttu-id="bf04b-389">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="bf04b-389">lx_nand_flash_sector_write</span></span>

<span data-ttu-id="bf04b-390">NVE Flash kesimini yaz</span><span class="sxs-lookup"><span data-stu-id="bf04b-390">Write NAND flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="bf04b-391">Prototype</span><span class="sxs-lookup"><span data-stu-id="bf04b-391">Prototype</span></span>

```c
UINT lx_nand_flash_sector_write(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="bf04b-392">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf04b-392">Description</span></span>

<span data-ttu-id="bf04b-393">Bu hizmet, nve Flash örneğinde belirtilen mantıksal kesimi yazar.</span><span class="sxs-lookup"><span data-stu-id="bf04b-393">This service writes the specified logical sector in the NAND flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bf04b-394">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-394">Input Parameters</span></span>

- <span data-ttu-id="bf04b-395">**nand_flash**: nve Flash örnek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-395">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="bf04b-396">**logical_sector**: yazılacak mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="bf04b-396">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="bf04b-397">**buffer**: mantıksal sektörün içeriğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="bf04b-397">**buffer**: Pointer to the contents of the logical sector.</span></span> <span data-ttu-id="bf04b-398">Arabelleğin nve Flash sayfa boyutunun boyutu olduğunu ve ULONG erişimi için hizalandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bf04b-398">Note that the buffer is assumed to be the size of the NAND flash page size and aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="bf04b-399">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bf04b-399">Return Values</span></span>

- <span data-ttu-id="bf04b-400">**LX_SUCCESS**: (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bf04b-400">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="bf04b-401">**LX_NO_SECTORS**: (0x02) yazma işlemini gerçekleştirmek için kullanılabilir daha fazla boş sektör yok.</span><span class="sxs-lookup"><span data-stu-id="bf04b-401">**LX_NO_SECTORS**: (0x02) No more free sectors are available to perform the write.</span></span>
- <span data-ttu-id="bf04b-402">**LX_ERROR**: (0x01) nve Flash kesimini serbest bırakma hatası.</span><span class="sxs-lookup"><span data-stu-id="bf04b-402">**LX_ERROR**: (0x01) Error releasing NAND flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bf04b-403">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bf04b-403">Allowed From</span></span>

<span data-ttu-id="bf04b-404">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bf04b-404">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bf04b-405">Örnek</span><span class="sxs-lookup"><span data-stu-id="bf04b-405">Example</span></span>

```c
/* Write logical sector 20 of the NAND flash instance "my_nand_flash" with the contents pointed to by "buffer". */  
status = lx_nand_flash_sector_write(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a><span data-ttu-id="bf04b-406">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf04b-406">See Also</span></span>

- <span data-ttu-id="bf04b-407">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="bf04b-407">lx_nand_flash_close</span></span>
- <span data-ttu-id="bf04b-408">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-408">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="bf04b-409">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="bf04b-409">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="bf04b-410">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="bf04b-410">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="bf04b-411">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="bf04b-411">lx_nand_flash_open</span></span>
- <span data-ttu-id="bf04b-412">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="bf04b-412">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="bf04b-413">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="bf04b-413">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="bf04b-414">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="bf04b-414">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="bf04b-415">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="bf04b-415">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="bf04b-416">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="bf04b-416">lx_nand_flash_sector_release</span></span>
