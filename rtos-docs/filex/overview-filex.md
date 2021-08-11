---
title: FileX Azure RTOS anlama
description: Azure RTOS FileX, Azure RTOS ThreadX ile tamamen tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen yüksek performanslı, dosya ayırma tablosu (FAT) ile uyumlu bir dosya sistemidir. Azure RTOS ThreadX'te olduğu gibi Azure RTOS FileX de küçük bir ayak izine ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu nedenle dosya yönetimi işlemleri gerektiren günümüzün derinden eklenmiş uygulamaları için idealdir. FileX, LevelX aracılığıyla RAM, AZURE RTOS USBX, SD CARD ve NAND/NOR flash bellekler gibi çoğu fiziksel Azure RTOS destekler.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 399586eca18ef9345b94cc577bdacbf3c3a591bcd22b474b4e3d4ca4eefb4432
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782871"
---
# <a name="overview-of-azure-rtos-filex"></a>Azure RTOS FileX'e genel bakış

Azure RTOS DosyaX ekli dosya sistemi, Azure RTOS, gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanmış Microsoft FAT dosya biçimleri için gelişmiş, endüstriyel sınıf çözümüdür. Azure RTOS FileX; FAT12, FAT16, FAT32 ve exFAT dahil olmak üzere Microsoft'un tüm dosya biçimlerini destekler. FileX [ayrıca, LevelX](https://docs.microsoft.com/azure/rtos/levelx/)adlı bir eklenti ürünü aracılığıyla isteğe bağlı hataya dayanıklılık ve FLASH Azure RTOS sunar. Bunların hepsi küçük bir ayak izi, hızlı yürütme ve üstün kullanım kolaylığı ile birlikte, Azure RTOS FileX'i en zorlu tümleşik IoT uygulamaları için ideal seçenek yapın.

## <a name="api-protocols"></a>API protokolleri

### <a name="media-services"></a>Media Services

- FAT 12/16/32 ve exFAT desteği
- En az 6 KB FLASH, 2,5 KB RAM
- Tam medya erişim hizmetleri
- Sınırsız sayıda medya örneği
- Basit okuma/yazma mantıksal kesim sürücü arabirimi
- Birden çok bölüm desteği
- Mantıksal kesim önbelleği
- FAT giriş önbelleği
- İsteğe bağlı hataya dayanıklılık desteği
- Ertelenmiş İkincil FAT güncelleştirmesi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
- Şunları içeren sezgisel medya erişim API'leri:
  - fx_media_open
  - fx_media_close
  - fx_media_format
  - fx_media_space_available

### <a name="directory-services"></a>Dizin Hizmetleri

- En fazla 256 byte yolu
- Desteklenen uzun ve 8.3 dizin adları
- Dizin oluşturma & silme
- Dizin gezintisi ve çapraz geçiş
- Dizin öznitelikleri yönetimi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
- Şunları içeren sezgisel dizin erişimi API'leri:
  - fx_directory_create
  - fx_directory_delete
  - fx_directory_attributes_set
  - fx_directory_attributes_read
  - fx_directory_first_entry_find
  - fx_directory_next_entry_find

### <a name="file-services"></a>Dosya Hizmetleri

- En az 3,3 KB FLASH
- Sınırsız açık dosya
- Salt okunur dosyalar birden çok kez açılabilir
- Desteklenen uzun ve 8.3 dizin adları
- Bitişik dosya desteği
- Hızlı arama mantığı
- Kümelerin önceden ayırması
- Dosya oluşturma, silme ve yeniden adlandırma
- Dosya okuma, yazma ve görme
- Dosya öznitelikleri yönetimi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme
- Sezgisel dosya erişim API'leri, şunları içerir:
  - fx_file_create
  - fx_file_delete
  - fx_file_attributes_set
  - fx_file_attributes_read
  - fx_file_read
  - fx_file_seek
  - fx_file_write

## <a name="advanced-technology"></a>Gelişmiş teknoloji

Azure RTOS FileX, aşağıdakiler de dahil olmak üzere gelişmiş bir teknolojidir.

- FAT 12/16/32 ve exFAT desteği
- Birden çok bölüm desteği
- Otomatik ölçeklendirme
- Endian nötr
- Uzun dosya adı ve 8.3 desteği
- İsteğe bağlı hataya dayanıklılık desteği
- Mantıksal kesim önbelleği
- FAT giriş önbelleği
- Kümelerin önceden ayırması
- Bitişik dosya desteği
- İsteğe bağlı performans ölçümleri
- Azure RTOS TraceX sistem analizi desteği

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a>NOR/NAND Wear Leveling (Azure RTOS LevelX)

Azure RTOS LevelX, Microsoft'un NOR/NAND FLASH yıpranma düzeyi yıpranma ürünüdür. Azure RTOS LevelX, FileX ile birlikte veya uygulama için tek başına, doğrudan okuma/yazma FLASH kesim kitaplığı olarak kullanılabilir.
