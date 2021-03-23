---
title: Bölüm 2-Azure RTOS LevelX yükleme ve kullanımı
description: LevelX 'in yüklenmesi ve kullanılması, bu bölümün aşağıdaki bölümlerinde anlaşılır ve açıklanacaktır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 575776875452cfc718401556a6440d787cb18893
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827065"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-levelx"></a><span data-ttu-id="7a7f9-103">Bölüm 2-Azure RTOS LevelX yükleme ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="7a7f9-103">Chapter 2 - Installation and use of Azure RTOS LevelX</span></span>

<span data-ttu-id="7a7f9-104">Azure RTOS LevelX yükleme ve kullanımı, bu bölümün aşağıdaki bölümlerinde basittir ve açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-104">Installation and use of Azure RTOS LevelX is straightforward and described in the following sections of this chapter.</span></span>

## <a name="distribution"></a><span data-ttu-id="7a7f9-105">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="7a7f9-105">Distribution</span></span>

<span data-ttu-id="7a7f9-106">LevelX, her bir işlevin kendi ayrı C dosyasında bulunduğu ANSI C 'de dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-106">LevelX is distributed in ANSI C where each function is contained in its own separate C file.</span></span> <span data-ttu-id="7a7f9-107">LevelX dağıtımındaki dosyalar aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-107">The files in the LevelX distribution are as follows.</span></span>
- <span data-ttu-id="7a7f9-108">lx_api. h</span><span class="sxs-lookup"><span data-stu-id="7a7f9-108">lx_api.h</span></span>
- <span data-ttu-id="7a7f9-109">lx_nand_flash_256byte_ecc_check. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-109">lx_nand_flash_256byte_ecc_check.c</span></span>
- <span data-ttu-id="7a7f9-110">lx_nand_flash_256byte_ecc_compute. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-110">lx_nand_flash_256byte_ecc_compute.c</span></span>
- <span data-ttu-id="7a7f9-111">lx_nand_flash_block_full_update. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-111">lx_nand_flash_block_full_update.c</span></span>
- <span data-ttu-id="7a7f9-112">lx_nand_flash_block_reclaim. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-112">lx_nand_flash_block_reclaim.c</span></span>
- <span data-ttu-id="7a7f9-113">lx_nand_flash_close. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-113">lx_nand_flash_close.c</span></span>
- <span data-ttu-id="7a7f9-114">lx_nand_flash_defragment. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-114">lx_nand_flash_defragment.c</span></span>  
- <span data-ttu-id="7a7f9-115">lx_nand_flash_extended_cache_enable. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-115">lx_nand_flash_extended_cache_enable.c</span></span>
- <span data-ttu-id="7a7f9-116">lx_nand_flash_initialize. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-116">lx_nand_flash_initialize.c</span></span>
- <span data-ttu-id="7a7f9-117">lx_nand_flash_logical_sector_find. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-117">lx_nand_flash_logical_sector_find.c</span></span>
- <span data-ttu-id="7a7f9-118">lx_nand_flash_next_block_to_erase_find. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-118">lx_nand_flash_next_block_to_erase_find.c</span></span>
- <span data-ttu-id="7a7f9-119">lx_nand_flash_open. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-119">lx_nand_flash_open.c</span></span>
- <span data-ttu-id="7a7f9-120">lx_nand_flash_page_ecc_check. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-120">lx_nand_flash_page_ecc_check.c</span></span>
- <span data-ttu-id="7a7f9-121">lx_nand_flash_page_ecc_compute. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-121">lx_nand_flash_page_ecc_compute.c</span></span>  
- <span data-ttu-id="7a7f9-122">lx_nand_flash_partial_defragment. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-122">lx_nand_flash_partial_defragment.c</span></span>
- <span data-ttu-id="7a7f9-123">lx_nand_flash_physical_page_allocate. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-123">lx_nand_flash_physical_page_allocate.c</span></span>
- <span data-ttu-id="7a7f9-124">lx_nand_flash_sector_mapping_cache_invalidate. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-124">lx_nand_flash_sector_mapping_cache_invalidate.c</span></span>
- <span data-ttu-id="7a7f9-125">lx_nand_flash_sector_read. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-125">lx_nand_flash_sector_read.c</span></span>
- <span data-ttu-id="7a7f9-126">lx_nand_flash_sector_release. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-126">lx_nand_flash_sector_release.c</span></span>
- <span data-ttu-id="7a7f9-127">lx_nand_flash_sector_write. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-127">lx_nand_flash_sector_write.c</span></span>
- <span data-ttu-id="7a7f9-128">lx_nand_flash_system_error. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-128">lx_nand_flash_system_error.c</span></span>
- <span data-ttu-id="7a7f9-129">lx_nor_flash_block_reclaim. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-129">lx_nor_flash_block_reclaim.c</span></span>
- <span data-ttu-id="7a7f9-130">lx_nor_flash_close. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-130">lx_nor_flash_close.c</span></span>
- <span data-ttu-id="7a7f9-131">lx_nor_flash_defragment. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-131">lx_nor_flash_defragment.c</span></span>  
- <span data-ttu-id="7a7f9-132">lx_nor_flash_extended_cache_enable. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-132">lx_nor_flash_extended_cache_enable.c</span></span>
- <span data-ttu-id="7a7f9-133">lx_nor_flash_initialize. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-133">lx_nor_flash_initialize.c</span></span>
- <span data-ttu-id="7a7f9-134">lx_nor_flash_logical_sector_find. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-134">lx_nor_flash_logical_sector_find.c</span></span>
- <span data-ttu-id="7a7f9-135">lx_nor_flash_next_block_to_erase_find. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-135">lx_nor_flash_next_block_to_erase_find.c</span></span>
- <span data-ttu-id="7a7f9-136">lx_nor_flash_open. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-136">lx_nor_flash_open.c</span></span>
- <span data-ttu-id="7a7f9-137">lx_nor_flash_partial_defragment. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-137">lx_nor_flash_partial_defragment.c</span></span>
- <span data-ttu-id="7a7f9-138">lx_nor_flash_physical_sector_allocate. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-138">lx_nor_flash_physical_sector_allocate.c</span></span>
- <span data-ttu-id="7a7f9-139">lx_nor_flash_sector_mapping_cache_invalidate. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-139">lx_nor_flash_sector_mapping_cache_invalidate.c</span></span>
- <span data-ttu-id="7a7f9-140">lx_nor_flash_sector_read. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-140">lx_nor_flash_sector_read.c</span></span>
- <span data-ttu-id="7a7f9-141">lx_nor_flash_sector_release. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-141">lx_nor_flash_sector_release.c</span></span>
- <span data-ttu-id="7a7f9-142">lx_nor_flash_sector_write. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-142">lx_nor_flash_sector_write.c</span></span>
- <span data-ttu-id="7a7f9-143">lx_nor_flash_system_error. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-143">lx_nor_flash_system_error.c</span></span>

<span data-ttu-id="7a7f9-144">Ayrıca, hem LevelX NAND hem de örnekleri için Benzetici ve FileX sürücü örnekleri de vardır.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-144">There are also simulator and FileX driver samples for both LevelX NAND and NOR instances, as follows.</span></span>

- <span data-ttu-id="7a7f9-145">demo_filex_nand_flash. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-145">demo_filex_nand_flash.c</span></span>  
- <span data-ttu-id="7a7f9-146">fx_nand_flash_simulated_driver. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-146">fx_nand_flash_simulated_driver.c</span></span>
- <span data-ttu-id="7a7f9-147">lx_nand_flash_simulator. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-147">lx_nand_flash_simulator.c</span></span>
- <span data-ttu-id="7a7f9-148">demo_filex_nor_flash. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-148">demo_filex_nor_flash.c</span></span>  
- <span data-ttu-id="7a7f9-149">fx_nor_flash_simulated_driver. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-149">fx_nor_flash_simulated_driver.c</span></span>
- <span data-ttu-id="7a7f9-150">lx_nor_flash_simulator. c</span><span class="sxs-lookup"><span data-stu-id="7a7f9-150">lx_nor_flash_simulator.c</span></span>

<span data-ttu-id="7a7f9-151">Kuşkusuz, yalnızca nve Flash gerekliyse, yalnızca LevelX nve Flash dosyaları (***lx_nand_ \* . c***) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-151">Of course, if only NAND flash is required, only the LevelX NAND flash files (***lx_nand_\*.c***) are needed.</span></span> <span data-ttu-id="7a7f9-152">Benzer şekilde, yalnızca veya Flash gerekliyse yalnızca veya Flash dosyaları (\* \*_lx_nor_ \_ . c \* \* \*) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-152">Similarly, if only NOR flash is required, only the NOR flash files (\*\*_lx_nor_\_.c\*\*\*) are needed.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="7a7f9-153">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7a7f9-153">Configuration Options</span></span>

<span data-ttu-id="7a7f9-154">LevelX, aşağıda açıklanan koşullu tanımlar yoluyla derleme zamanında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-154">LevelX can be configured at compile time via the conditional defines described below.</span></span> <span data-ttu-id="7a7f9-155">Seçeneğini kullanmak için, her bir LevelX kaynağının derlemesine istenen tanımla eklemek yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-155">Simply add the desired define to the compilation of each LevelX source to use the option.</span></span>

- <span data-ttu-id="7a7f9-156">**LX_DIRECT_READ**: tanımlı, bu seçenek veya belleği doğrudan kabul eden veya okuyan Flash sürücü okuma yordamını atlar, böylece önemli bir performans artışı elde edilir.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-156">**LX_DIRECT_READ**:  Defined, this option bypasses the NOR flash driver read routine in favor or reading the NOR memory directly, resulting in a significant performance increase.</span></span>
- <span data-ttu-id="7a7f9-157">**LX_FREE_SECTOR_DATA_VERIFY**: tanımlı, bu, levelx veya örnek açık MANTıĞıNıN ücretsiz veya sektörlerin tümünün tarafından doğrulanmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-157">**LX_FREE_SECTOR_DATA_VERIFY**: Defined, this causes the LevelX NOR instance open logic to verify free NOR sectors are all ones.</span></span>
- <span data-ttu-id="7a7f9-158">**LX_NAND_SECTOR_MAPPING_CACHE_SIZE**: Bu değer varsayılan olarak 16 ' dır ve mantıksal kesim eşleme önbelleği boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-158">**LX_NAND_SECTOR_MAPPING_CACHE_SIZE**:  By default this value is 16 and defines the logical sector mapping cache size.</span></span> <span data-ttu-id="7a7f9-159">Büyük değerler performansı iyileştirir, ancak maliyet belleği.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-159">Large values improve performance, but cost memory.</span></span> <span data-ttu-id="7a7f9-160">En küçük boyut 8 ' dir ve tüm değerler 2 ' nin üssü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-160">The minimum size is 8 and all values must be a power of 2.</span></span>
- <span data-ttu-id="7a7f9-161">**LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: tanımlı, önbellek isabetsizlik olmaması gibi bir doğrudan eşleme önbelleği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-161">**LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: Defined, this creates a direct mapping cache, such that there are no cache misses.</span></span> <span data-ttu-id="7a7f9-162">Ayrıca LX_NAND_SECTOR_MAPPING_CACHE_SIZE, Flash cihazınızdaki toplam sayfa sayısını tam olarak temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-162">It also requires that LX_NAND_SECTOR_MAPPING_CACHE_SIZE represents the exact number of total pages in your flash device.</span></span>
- <span data-ttu-id="7a7f9-163">**LX_NOR_DISABLE_EXTENDED_CACHE**: tanımlı, genişletilmiş ne de önbellek devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-163">**LX_NOR_DISABLE_EXTENDED_CACHE**: Defined, this disabled the extended NOR cache.</span></span>
- <span data-ttu-id="7a7f9-164">**LX_NOR_EXTENDED_CACHE_SIZE**: Bu değer varsayılan olarak 8 ' dir ve bir veya örneğinde Önbelleğe alınabilecek en fazla 8 kesimi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-164">**LX_NOR_EXTENDED_CACHE_SIZE**: By default this value is 8, which represents a maximum of 8 sectors that can be cached in a NOR instance.</span></span>
- <span data-ttu-id="7a7f9-165">**LX_NOR_SECTOR_MAPPING_CACHE_SIZE**: Bu değer varsayılan olarak 16 ' dır ve mantıksal kesim eşleme önbelleği boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-165">**LX_NOR_SECTOR_MAPPING_CACHE_SIZE**: By default this value is 16 and defines the logical sector mapping cache size.</span></span> <span data-ttu-id="7a7f9-166">Büyük değerler performansı iyileştirir, ancak maliyet belleği.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-166">Large values improve performance, but cost memory.</span></span> <span data-ttu-id="7a7f9-167">En küçük boyut 8 ' dir ve tüm değerler 2 ' nin üssü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-167">The minimum size is 8 and all values must be a power of 2.</span></span>
- <span data-ttu-id="7a7f9-168">**LX_THREAD_SAFE_ENABLE**: TANıMLı, API 'nin tamamında bir threadx mutex nesnesi kullanarak levelx iş parçacığı güvenli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-168">**LX_THREAD_SAFE_ENABLE**: Defined, this makes LevelX thread-safe by using a ThreadX mutex object throughout the API.</span></span>

## <a name="using-levelx"></a><span data-ttu-id="7a7f9-169">LevelX kullanma</span><span class="sxs-lookup"><span data-stu-id="7a7f9-169">Using LevelX</span></span>

<span data-ttu-id="7a7f9-170">LevelX 'i kendisi veya FileX ile birlikte kullanmak için, LevelX API 'sine başvuran koda \***lx_api. h** _ dosyasını dahil edin.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-170">To use LevelX, either by itself or with FileX, include the file \***lx_api.h** _ in the code that references the LevelX API.</span></span> <span data-ttu-id="7a7f9-171">Ayrıca, LevelX nesne kodunun bağlantı sırasında kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-171">Also ensure that the LevelX object code is available at link time.</span></span> <span data-ttu-id="7a7f9-172">LevelX kullanma örnekleri için lütfen _*_demo_filex_nand_flash. c_*_ ve _ *_demo_filex_nor_flash. c_*\* dosyalarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="7a7f9-172">Please examine the files _*_demo_filex_nand_flash.c_*_ and _ *_demo_filex_nor_flash.c_*\* for examples of how to use LevelX.</span></span>
