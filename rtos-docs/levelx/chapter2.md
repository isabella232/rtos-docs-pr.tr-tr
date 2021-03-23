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
# <a name="chapter-2---installation-and-use-of-azure-rtos-levelx"></a>Bölüm 2-Azure RTOS LevelX yükleme ve kullanımı

Azure RTOS LevelX yükleme ve kullanımı, bu bölümün aşağıdaki bölümlerinde basittir ve açıklanmaktadır.

## <a name="distribution"></a>Dağıtım

LevelX, her bir işlevin kendi ayrı C dosyasında bulunduğu ANSI C 'de dağıtılır. LevelX dağıtımındaki dosyalar aşağıdaki gibidir.
- lx_api. h
- lx_nand_flash_256byte_ecc_check. c
- lx_nand_flash_256byte_ecc_compute. c
- lx_nand_flash_block_full_update. c
- lx_nand_flash_block_reclaim. c
- lx_nand_flash_close. c
- lx_nand_flash_defragment. c  
- lx_nand_flash_extended_cache_enable. c
- lx_nand_flash_initialize. c
- lx_nand_flash_logical_sector_find. c
- lx_nand_flash_next_block_to_erase_find. c
- lx_nand_flash_open. c
- lx_nand_flash_page_ecc_check. c
- lx_nand_flash_page_ecc_compute. c  
- lx_nand_flash_partial_defragment. c
- lx_nand_flash_physical_page_allocate. c
- lx_nand_flash_sector_mapping_cache_invalidate. c
- lx_nand_flash_sector_read. c
- lx_nand_flash_sector_release. c
- lx_nand_flash_sector_write. c
- lx_nand_flash_system_error. c
- lx_nor_flash_block_reclaim. c
- lx_nor_flash_close. c
- lx_nor_flash_defragment. c  
- lx_nor_flash_extended_cache_enable. c
- lx_nor_flash_initialize. c
- lx_nor_flash_logical_sector_find. c
- lx_nor_flash_next_block_to_erase_find. c
- lx_nor_flash_open. c
- lx_nor_flash_partial_defragment. c
- lx_nor_flash_physical_sector_allocate. c
- lx_nor_flash_sector_mapping_cache_invalidate. c
- lx_nor_flash_sector_read. c
- lx_nor_flash_sector_release. c
- lx_nor_flash_sector_write. c
- lx_nor_flash_system_error. c

Ayrıca, hem LevelX NAND hem de örnekleri için Benzetici ve FileX sürücü örnekleri de vardır.

- demo_filex_nand_flash. c  
- fx_nand_flash_simulated_driver. c
- lx_nand_flash_simulator. c
- demo_filex_nor_flash. c  
- fx_nor_flash_simulated_driver. c
- lx_nor_flash_simulator. c

Kuşkusuz, yalnızca nve Flash gerekliyse, yalnızca LevelX nve Flash dosyaları (***lx_nand_ \* . c***) gereklidir. Benzer şekilde, yalnızca veya Flash gerekliyse yalnızca veya Flash dosyaları (* *_lx_nor_ \_ . c * * *) gereklidir.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

LevelX, aşağıda açıklanan koşullu tanımlar yoluyla derleme zamanında yapılandırılabilir. Seçeneğini kullanmak için, her bir LevelX kaynağının derlemesine istenen tanımla eklemek yeterlidir.

- **LX_DIRECT_READ**: tanımlı, bu seçenek veya belleği doğrudan kabul eden veya okuyan Flash sürücü okuma yordamını atlar, böylece önemli bir performans artışı elde edilir.
- **LX_FREE_SECTOR_DATA_VERIFY**: tanımlı, bu, levelx veya örnek açık MANTıĞıNıN ücretsiz veya sektörlerin tümünün tarafından doğrulanmasına neden olur.
- **LX_NAND_SECTOR_MAPPING_CACHE_SIZE**: Bu değer varsayılan olarak 16 ' dır ve mantıksal kesim eşleme önbelleği boyutunu tanımlar. Büyük değerler performansı iyileştirir, ancak maliyet belleği. En küçük boyut 8 ' dir ve tüm değerler 2 ' nin üssü olmalıdır.
- **LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: tanımlı, önbellek isabetsizlik olmaması gibi bir doğrudan eşleme önbelleği oluşturur. Ayrıca LX_NAND_SECTOR_MAPPING_CACHE_SIZE, Flash cihazınızdaki toplam sayfa sayısını tam olarak temsil eder.
- **LX_NOR_DISABLE_EXTENDED_CACHE**: tanımlı, genişletilmiş ne de önbellek devre dışı bırakıldı.
- **LX_NOR_EXTENDED_CACHE_SIZE**: Bu değer varsayılan olarak 8 ' dir ve bir veya örneğinde Önbelleğe alınabilecek en fazla 8 kesimi temsil eder.
- **LX_NOR_SECTOR_MAPPING_CACHE_SIZE**: Bu değer varsayılan olarak 16 ' dır ve mantıksal kesim eşleme önbelleği boyutunu tanımlar. Büyük değerler performansı iyileştirir, ancak maliyet belleği. En küçük boyut 8 ' dir ve tüm değerler 2 ' nin üssü olmalıdır.
- **LX_THREAD_SAFE_ENABLE**: TANıMLı, API 'nin tamamında bir threadx mutex nesnesi kullanarak levelx iş parçacığı güvenli hale getirir.

## <a name="using-levelx"></a>LevelX kullanma

LevelX 'i kendisi veya FileX ile birlikte kullanmak için, LevelX API 'sine başvuran koda ***lx_api. h** _ dosyasını dahil edin. Ayrıca, LevelX nesne kodunun bağlantı sırasında kullanılabilir olduğundan emin olun. LevelX kullanma örnekleri için lütfen _*_demo_filex_nand_flash. c_*_ ve _ *_demo_filex_nor_flash. c_** dosyalarını inceleyin.
