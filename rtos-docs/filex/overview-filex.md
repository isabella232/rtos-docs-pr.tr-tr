---
title: Azure RTOS FileX 'i anlama
description: Azure RTOS FileX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen yüksek performanslı, dosya ayırma tablosu (FAT) ile uyumlu bir dosya sistemidir. Azure RTOS ThreadX gibi Azure RTOS FileX, küçük bir ayak izi ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da dosya yönetimi işlemleri gerektiren, günümüzün derin eklenmiş uygulamalar için idealdir. FileX, RAM, Azure RTOS USBX, SD kartı ve nve/veya Flash anıları dahil olmak üzere çoğu fiziksel medyayı Azure RTOS LevelX aracılığıyla destekler.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0a54f160c96fb3e90c2295ae72020c121d367a12
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171377"
---
# <a name="overview-of-azure-rtos-filex"></a>Azure RTOS FileX 'e genel bakış

Azure RTOS FileX Embedded dosya sistemi, özel olarak gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft FAT dosya biçimleri için Azure RTOS 'ın gelişmiş, endüstriyel sınıf çözümüdür. Azure RTOS FileX, FAT12, FAT16, FAT32 ve exFAT gibi Microsoft 'un dosya biçimlerini destekler. FileX, [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/)adlı bir eklenti ürünü aracılığıyla isteğe bağlı hata TOLERANSı ve Flash giyme seviyelendirme de sunar. Tüm bu, küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla birlikte Azure RTOS dosya x ' i en zorlu ekli IoT uygulamalarına yönelik ideal bir seçenek haline getirir.

## <a name="api-protocols"></a>API protokolleri

### <a name="media-services"></a>Media Services

- FAT 12/16/32 ve exFAT desteği
- Minimum 6KB FLASH, 2,5 KB RAM
- Medya erişim Hizmetleri 'ni doldurun
- Sınırsız sayıda medya örneği
- Basit okuma/yazma mantıksal sektör sürücü arabirimi
- Birden çok bölüm desteği
- Mantıksal kesim önbelleği
- FAT giriş önbelleği
- İsteğe bağlı hata toleransı desteği
- Ertelenmiş Ikincil FAT güncelleştirmesi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
- Aşağıdakiler dahil, sezgisel medya erişim API 'Leri:
  - fx_media_open
  - fx_media_close
  - fx_media_format
  - fx_media_space_available

### <a name="directory-services"></a>Dizin Hizmetleri

- En fazla 256 bayt yolu
- Uzun ve 8,3 dizin adları destekleniyor
- Dizin oluşturma & silme
- Dizin gezintisi ve geçişi
- Dizin öznitelikleri yönetimi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
- Aşağıdakiler dahil, sezgisel dizin erişimi API 'Leri:
  - fx_directory_create
  - fx_directory_delete
  - fx_directory_attributes_set
  - fx_directory_attributes_read
  - fx_directory_first_entry_find
  - fx_directory_next_entry_find

### <a name="file-services"></a>Dosya Hizmetleri

- Minimum 3.3 KB FLASH
- Sınırsız açık dosya
- Salt okuma dosyaları birden çok kez açılabilir
- Uzun ve 8,3 dizin adları destekleniyor
- Ardışık dosya desteği
- Hızlı arama mantığı
- Kümelerin ön ayırması
- Dosya oluşturma, silme ve yeniden adlandırma
- Dosya okuma, yazma ve görme
- Dosya öznitelikleri yönetimi
- Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme
- Aşağıdakiler dahil, sezgisel dosya erişim API 'Leri:
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
- Uzun dosya adı ve 8,3 desteği
- İsteğe bağlı hata toleransı desteği
- Mantıksal kesim önbelleği
- FAT giriş önbelleği
- Kümelerin ön ayırması
- Ardışık dosya desteği
- İsteğe bağlı performans ölçümleri
- Azure RTOS TraceX sistem analizi desteği

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a>VEYA/nve aşınma dengeleme (Azure RTOS LevelX)

Azure RTOS LevelX, Microsoft 'un veya/nve FLASH giyme Dengeleme ürünüdür. Azure RTOS LevelX, FileX ile birlikte veya uygulama için tek başına, doğrudan okuma/yazma FLASH sektör kitaplığı olarak kullanılabilir.
