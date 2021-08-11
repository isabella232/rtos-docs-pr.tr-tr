---
title: Bölüm 2 - Azure RTOS LevelX'i yükleme ve kullanma
description: LevelX'in yüklenmesi ve kullanımı basittir ve bu bölümün aşağıdaki bölümlerinde açıklanmıştır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cfd2d616896e1797114e55abcaf1a7559685282f29c2d0dee8274d2a26ea8f0e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790318"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-levelx"></a>Bölüm 2 - Azure RTOS LevelX'i yükleme ve kullanma

Azure RTOS LevelX'in yüklenmesi ve kullanımı basittir ve bu bölümün aşağıdaki bölümlerinde açıklanmıştır.

## <a name="distribution"></a>Dağıtım

LevelX, ANSI C'de dağıtılır ve burada her işlev kendi ayrı C dosyasında yer alır. LevelX dağıtımında dosyalar aşağıdaki gibidir.
- lx_api.h
- lx_nand_flash_256byte_ecc_check.c
- lx_nand_flash_256byte_ecc_compute.c
- lx_nand_flash_block_full_update.c
- lx_nand_flash_block_reclaim.c
- lx_nand_flash_close.c
- lx_nand_flash_defragment.c  
- lx_nand_flash_extended_cache_enable.c
- lx_nand_flash_initialize.c
- lx_nand_flash_logical_sector_find.c
- lx_nand_flash_next_block_to_erase_find.c
- lx_nand_flash_open.c
- lx_nand_flash_page_ecc_check.c
- lx_nand_flash_page_ecc_compute.c  
- lx_nand_flash_partial_defragment.c
- lx_nand_flash_physical_page_allocate.c
- lx_nand_flash_sector_mapping_cache_invalidate.c
- lx_nand_flash_sector_read.c
- lx_nand_flash_sector_release.c
- lx_nand_flash_sector_write.c
- lx_nand_flash_system_error.c
- lx_nor_flash_block_reclaim.c
- lx_nor_flash_close.c
- lx_nor_flash_defragment.c  
- lx_nor_flash_extended_cache_enable.c
- lx_nor_flash_initialize.c
- lx_nor_flash_logical_sector_find.c
- lx_nor_flash_next_block_to_erase_find.c
- lx_nor_flash_open.c
- lx_nor_flash_partial_defragment.c
- lx_nor_flash_physical_sector_allocate.c
- lx_nor_flash_sector_mapping_cache_invalidate.c
- lx_nor_flash_sector_read.c
- lx_nor_flash_sector_release.c
- lx_nor_flash_sector_write.c
- lx_nor_flash_system_error.c

Ayrıca, aşağıdaki gibi hem LevelX NAND hem de NOR örnekleri için simülatör ve FileX sürücü örnekleri de vardır.

- demo_filex_nand_flash.c  
- fx_nand_flash_simulated_driver.c
- lx_nand_flash_simulator.c
- demo_filex_nor_flash.c  
- fx_nor_flash_simulated_driver.c
- lx_nor_flash_simulator.c

Elbette yalnızca NAND flash gerekli ise yalnızca LevelX NAND flash dosyaları ***(lx_nand_ \* .c***) gerekir. Benzer şekilde, yalnızca NOR flash gerekli ise, yalnızca NOR flash dosyaları (**_veya_ \_ .c lx_nor) gereklidir.

## <a name="configuration-options"></a>Yapılandırma Seçenekleri

LevelX, derleme zamanında aşağıda açıklanan koşullu tanımlar aracılığıyla yalıtabilirsiniz. seçeneğini kullanmak için her LevelX kaynağının derlemesi için istenen tanımlamayı eklemeniz gerekir.

- **LX_DIRECT_READ:** Tanımlandığı gibi, bu seçenek NOR flash sürücü okuma yordamını atlayarak NOR belleğini doğrudan okuyarak önemli bir performans artışına neden olur.
- **LX_FREE_SECTOR_DATA_VERIFY:** Tanımlandığı gibi, bu durum LevelX NOR örneğinin açık mantığının ücretsiz NOR kesimlerinin hepsi olduğunu doğrulamaya neden olur.
- **LX_NAND_SECTOR_MAPPING_CACHE_SIZE:** Varsayılan olarak bu değer 16'dır ve mantıksal kesim eşleme önbellek boyutunu tanımlar. Büyük değerler performansı artırır, ancak maliyet belleğini artırır. En küçük boyut 8'tir ve tüm değerlerin 2 gücü olması gerekir.
- **LX_NAND_FLASH_DIRECT_MAPPING_CACHE:** Tanımlandığı gibi, önbellek isabet isabeti yok gibi bir doğrudan eşleme önbelleği oluşturur. Ayrıca, LX_NAND_SECTOR_MAPPING_CACHE_SIZE flash LX_NAND_SECTOR_MAPPING_CACHE_SIZE toplam sayfa sayısını temsil eder.
- **LX_NOR_DISABLE_EXTENDED_CACHE:** Tanımlı, genişletilmiş NOR önbelleği devre dışı bırakıldı.
- **LX_NOR_EXTENDED_CACHE_SIZE:** Varsayılan olarak bu değer, nor örneğinde önbelleğe alınacak en fazla 8 kesimi temsil eden 8'tir.
- **LX_NOR_SECTOR_MAPPING_CACHE_SIZE:** Varsayılan olarak bu değer 16'dır ve mantıksal kesim eşlemesi önbellek boyutunu tanımlar. Büyük değerler performansı artırır, ancak maliyet belleğini artırır. En küçük boyut 8'tir ve tüm değerlerin 2 gücü olması gerekir.
- **LX_THREAD_SAFE_ENABLE:** Tanımlanan bu, API genelinde ThreadX mutex nesnesi kullanarak LevelX iş parçacığını güvenli yapar.
- **LX_STANDALONE_ENABLE:** Tanımlı, LevelX'in tek başına modda (tek başına) Azure RTOS. Varsayılan olarak bu simge tanımlanmamıştır.

> [!IMPORTANT]
> Tek başına modda LevelX kullanılırken (**LX_STANDALONE_ENABLE** tanımlanmalıdır), ThreadX dosyaları/kitaplıkları gerekli değildir. LevelX iş parçacığı güvenli özelliği bu modda devre dışı bırakıldı.

## <a name="using-levelx"></a>LevelX kullanma

LevelX'i tek başına veya FileX ile kullanmak için LevelX API'sini referans alan koda ***lx_api.h** _ dosyasını dahil edin. Ayrıca LevelX nesne kodunun bağlantı zamanında kullanılabilir olduğundan emin olur. LevelX kullanma örnekleri _*_için lütfen demo_filex_nand_flash.c_*_ ve _ *_demo_filex_nor_flash.c_** dosyalarını inceler.
