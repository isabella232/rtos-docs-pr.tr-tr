---
title: Bölüm 7-Azure RTOS FileX izleme olayları
description: Bu bölümde, Azure RTOS FileX olaylarının açıklaması yer almaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 8668f0867e205afdeab112dfedd257998a5f5b7ff256f27298072dde3e9019b0
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116803299"
---
# <a name="chapter-7---azure-rtos-filex-trace-events"></a>Bölüm 7-Azure RTOS FileX izleme olayları

Bu bölümde, Azure RTOS FileX olaylarının açıklaması yer almaktadır. 

## <a name="list-of-events-and-icons"></a>Olay ve simgelerin listesi

**Aşağıda, TraceX tarafından görünen FileX olaylarının bir listesi verilmiştir.**

Aşağıda her bir olay açıklanmaktadır:

| **Simge**                         | **Anlamı**                               |
| -------------------------------- | ----------------------------------------- |
| ![İç mantıksal kesim önbelleğinde Isabetsizlik simgesi](./media/user-guide/fx-events/image1.png)    | İç mantıksal kesim önbelleği Isabetsizlik |
| ![İç dizin önbelleği Isabetsizlik simgesi](./media/user-guide/fx-events/image2.png)    | İç dizin önbelleğinde Isabetsizlik |
| ![İç medya Temizleme simgesi](./media/user-guide/fx-events/image3.png)    | İç medya Temizleme |
| ![İç dizin girişi okuma simgesi](./media/user-guide/fx-events/image4.png)    | İç dizin girişi okundu |
| ![İç dizin girişi yazma simgesi](./media/user-guide/fx-events/image5.png)    | İç dizin girişi yazma |
| ![İç g/ç sürücüsü okuma simgesi](./media/user-guide/fx-events/image6.png)    | İç g/ç sürücüsü okuma |
| ![İç g/ç sürücüsü yazma simgesi](./media/user-guide/fx-events/image7.png)    | İç g/ç sürücüsü yazma |
| ![İç g/ç sürücüsü Temizleme simgesi](./media/user-guide/fx-events/image8.png)    | İç g/ç sürücüsü Temizleme |
| ![İç g/ç sürücüsü Iptali simgesi](./media/user-guide/fx-events/image9.png)    | İç g/ç sürücüsü Iptali |
| ![İç g/ç sürücüsü başlatma simgesi](./media/user-guide/fx-events/image10.png)    | İç g/ç sürücüsü başlatma |
| ![İç g/ç sürücüsü önyüklemesi okuma simgesi](./media/user-guide/fx-events/image11.png)    | İç g/ç sürücüsü önyüklemesi okuma |
| ![İç g/ç sürücüsü sürüm kesimleri simgesi](./media/user-guide/fx-events/image12.png)    | İç g/ç sürücüsü sürüm kesimleri |
| ![İç g/ç sürücüsü önyükleme yazma simgesi](./media/user-guide/fx-events/image13.png)    | İç g/ç sürücüsü önyükleme yazma |
| ![İç g/ç sürücü sürücüsü başlatması kaldır simgesi](./media/user-guide/fx-events/image14.png)    | İç g/ç sürücü sürücüsü başlatması kaldır |
| ![Dizin özniteliklerini oku simgesi](./media/user-guide/fx-events/image15.png)    | **Dizin öznitelikleri okuma** (*fx_directory_attributes_read*) |
| ![Dizin öznitelikleri kümesi simgesi](./media/user-guide/fx-events/image16.png)    | **Dizin öznitelikleri kümesi** (*fx_directory_attributes_set*) |
| ![Dizin oluşturma simgesi](./media/user-guide/fx-events/image17.png)    | **Dizin oluşturma** (*fx_directory_create*) |
| ![Dizin varsayılanı al simgesi](./media/user-guide/fx-events/image18.png)    | **Dizin varsayılanı al** (*fx_directory_default_get*) |
| ![Dizin varsayılan kümesi simgesi](./media/user-guide/fx-events/image19.png)    | **Dizin varsayılan kümesi** (*fx_directory_default_set*) |
| ![Dizin silme simgesi](./media/user-guide/fx-events/image20.png)    | **Dizin silme** (*fx_directory_delete*) |
| ![Dizin Ilk girişi bul simgesi](./media/user-guide/fx-events/image21.png)    | **Dizin Ilk giriş bulma** (*fx_directory_first_entry_find*) |
| ![Dizinin Ilk tam giriş bul simgesi](./media/user-guide/fx-events/image22.png)    | **Dizinin Ilk tam girişi bul** (*fx_directory_first_full_entry_find*) |
| ![Dizin bilgileri al simgesi](./media/user-guide/fx-events/image23.png)    | **Dizin bilgileri al** (*fx_directory_information_get*) |
| ![Dizin yerel yolu temizle simgesi](./media/user-guide/fx-events/image24.png)    | **Dizin yerel yolu temizle** (*fx_directory_local_path_clear*) |
| ![Dizin yerel yolu al simgesi](./media/user-guide/fx-events/image25.png)    | **Dizin yerel yolu al** (*fx_directory_local_path_get*) |
| ![Dizin yerel yolu geri yükleme simgesi](./media/user-guide/fx-events/image26.png)    | **Dizin yerel yolunu geri yükleme** (*fx_directory_local_path_restore*) |
| ![Dizin yerel yolu kümesi simgesi](./media/user-guide/fx-events/image27.png)    | **Dizin yerel yol kümesi** (*fx_directory_local_path_set*) |
| ![Dizin uzun adı Al simgesi](./media/user-guide/fx-events/image28.png)    | **Dizin uzun adı Al** (*fx_directory_long_name_get*) |
| ![Dizin adı test simgesi](./media/user-guide/fx-events/image29.png)    | **Dizin adı testi** (*fx_directory_name_test*) |
| ![Dizin sonraki giriş bul simgesi](./media/user-guide/fx-events/image30.png)    | **Dizin sonraki giriş bul** (*fx_directory_next_entry_find*) |
| ![Dizin bir sonraki tam giriş bul simgesi](./media/user-guide/fx-events/image31.png)    | **Dizin bir sonraki tam girdi bul** (*fx_directory_next_full_entry_find*) |
| ![Dizin yeniden adlandırma simgesi](./media/user-guide/fx-events/image32.png)    | **Dizin yeniden adlandırma** (*fx_directory_rename*) |
| ![Dizin kısa adı Al simgesi](./media/user-guide/fx-events/image33.png)    | **Dizin kısa adı Get** (*fx_directory_short_name_get*) |
| ![Dosya ayırma simgesi](./media/user-guide/fx-events/image34.png)    | **Dosya ayırma** (*fx_file_allocate*) |
| ![Dosya öznitelikleri okuma simgesi](./media/user-guide/fx-events/image35.png)    | **Dosya öznitelikleri okuma** (*fx_file_attributes_read*) |
| ![Dosya öznitelikleri kümesi simgesi](./media/user-guide/fx-events/image36.png)    | **Dosya öznitelikleri kümesi** (*fx_file_attributes_set*) |
| ![Dosya En Iyi çaba ayırma simgesi](./media/user-guide/fx-events/image37.png)    | **Dosya En Iyi efor tahsisi** (*fx_file_best_effort_allocate*) |
| ![Dosya Kapat simgesi](./media/user-guide/fx-events/image38.png)    | **Dosya Kapat** (*fx_file_close*) |
| ![Dosya oluşturma simgesi](./media/user-guide/fx-events/image39.png)    | **Dosya oluşturma** (*fx_file_create*) |
| ![Dosya tarih saat kümesi simgesi](./media/user-guide/fx-events/image40.png)    | **Dosya tarih saat kümesi** (*fx_file_date_time_set*) |
| ![Dosya silme simgesi](./media/user-guide/fx-events/image41.png)    | **Dosya silme** (*fx_file_delete*) |
| ![Dosya aç simgesi](./media/user-guide/fx-events/image42.png)    | **Dosya açık** (*fx_file_open*) |
| ![Dosya okuma simgesi](./media/user-guide/fx-events/image43.png)    | **Dosya okuma** (*fx_file_read*) |
| ![Dosya göreli arama simgesi](./media/user-guide/fx-events/image44.png)    | **Dosya göreli arama** (*fx_file_relative_seek*) |
| ![Dosya yeniden adlandırma simgesi](./media/user-guide/fx-events/image45.png)    | **Dosya yeniden adlandırma** (*fx_file_rename*) |
| ![Dosya arama simgesi](./media/user-guide/fx-events/image46.png)    | **Dosya Arama** (*fx_file_seek*) |
| ![Dosya Kesme simgesi](./media/user-guide/fx-events/image47.png)    | **Dosya Kesilmesi** (*fx_file_truncate*) |
| ![Dosya Kesme Yayın simgesi](./media/user-guide/fx-events/image48.png)    | **Dosya Kesme Sürümü** (*fx_file_truncate_release*) |
| ![Dosya Yazma simgesi](./media/user-guide/fx-events/image49.png)    | **Dosya Yazma** (*fx_file_write*) |
| ![Medya Durdurma simgesi](./media/user-guide/fx-events/image50.png)    | **Medya Durdurma** (*fx_media_abort*) |
| ![Medya Önbelleği Geçersiz Kılın simgesi](./media/user-guide/fx-events/image51.png)    | **Medya Önbelleği Geçersiz Kılındı** (*fx_media_cache_invalidate*) |
| ![Medya Denetimi simgesi](./media/user-guide/fx-events/image52.png)    | **Medya Denetimi** (*fx_media_check*) |
| ![*MedyaYı Kapat simgesi](./media/user-guide/fx-events/image53.png)    | **Medya Kapatma** (*fx_media_close*) |
| ![Medya Boşaltma simgesi](./media/user-guide/fx-events/image54.png)    | **Medya Boşaltma** (*fx_media_flush*) |
| ![Medya Biçimi simgesi](./media/user-guide/fx-events/image55.png)    | **Medya Biçimi** (*fx_media_format*) |
| ![Medya Aç simgesi](./media/user-guide/fx-events/image56.png)    | **Media Open** (*fx_media_open*) |
| ![Medya Okuma simgesi](./media/user-guide/fx-events/image57.png)    | **Medya Okuma** (*fx_media_read*) |
| ![Medya Alanı Kullanılabilir simgesi](./media/user-guide/fx-events/image58.png)    | **Kullanılabilir Medya Alanı** (*fx_media_space_available*) |
| ![Medya Birimi Al simgesi](./media/user-guide/fx-events/image59.png)    | **Medya Birimi Al** (*fx_media_volume_get*) |
| ![Medya Birim Kümesi simgesi](./media/user-guide/fx-events/image60.png)    | **Medya Birim Kümesi** (*fx_media_volume_set*) |
| ![Medya Yazma simgesi](./media/user-guide/fx-events/image61.png)    | **Medya Yazma** (*fx_media_write*) |
| ![Sistem Tarihi Al simgesi](./media/user-guide/fx-events/image62.png)    | **Sistem Tarih Al** (*fx_system_date_get*) |
| ![Sistem Tarih Kümesi simgesi](./media/user-guide/fx-events/image63.png)    | **Sistem Tarih Kümesi** (*fx_system_date_set*) |
| ![Sistem Başlatma simgesi](./media/user-guide/fx-events/image64.png)    | **Sistem Başlatma** (*fx_system_initialize*) |
| ![Sistem Saati Al simgesi](./media/user-guide/fx-events/image65.png)    | **Sistem Zamanı Al** (*fx_system_time_get*) |
| ![Sistem Zaman Kümesi simgesi](./media/user-guide/fx-events/image66.png)    | **Sistem Zaman Kümesi** (*fx_system_time_set*) |
| ![Unicode Dizini Oluştur simgesi](./media/user-guide/fx-events/image67.png)    | **Unicode Dizin Oluşturma** (*fx_unicode_directory_create*) |
| ![Unicode Dizini Yeniden Adlandırma simgesi](./media/user-guide/fx-events/image68.png)    | **Unicode Dizin Yeniden Adlandırma** (*fx_unicode_directory_rename*) |
| ![Unicode Dosya Oluştur simgesi](./media/user-guide/fx-events/image69.png)    | **Unicode Dosya Oluşturma** (*fx_unicode_file_create*) |
| ![Unicode Dosya Yeniden Adlandırma simgesi](./media/user-guide/fx-events/image70.png)    | **Unicode Dosya Yeniden Adlandırma** (*fx_unicode_file_rename*) |
| ![Unicode Lenght Get simgesi](./media/user-guide/fx-events/image71.png)    | **Unicode Lenght Get** (*fx_unicode_length_get*) |
| ![Unicode Adı Al simgesi](./media/user-guide/fx-events/image72.png)    | **Unicode Ad Get** (*fx_unicode_name_get*) |
| ![Unicode Kısa Adı Al simgesi](./media/user-guide/fx-events/image73.png)    | **Unicode Kısa Adı Al** (*fx_unicode_short_name_get*) |

## <a name="event-descriptions"></a>Olay Açıklamaları

Aşağıda her bir olay açık bir şekilde açık almaktadır.

### <a name="internal-logical-sector-cache-miss"></a>İç Mantıksal Kesim Önbellek Isabeti 

#### <a name="internal-logical-sector-cache-miss"></a>İç mantıksal kesim önbelleği isabet isabetli değil

**Simge** ![ İç mantıksal kesim önbelleği isabet isabeti simgesi](./media/user-guide/fx-events/image1.png)

**Açıklama**

Bu olay, iç FileX mantıksal kesim önbelleği isabeti temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Kesim.
- Bilgi Alanı 3: Toplam kaçırma sayısı.
- Bilgi Alanı 4: Önbellek boyutu.

### <a name="internal-directory-cache-miss"></a>İç Dizin Önbelleği Isabeti

#### <a name="internal-directory-cache-miss"></a>İç dizin önbelleği isabet isabeti

**Simge** ![ İç dizin önbelleği isabet yok simgesi](./media/user-guide/fx-events/image2.png)

**Açıklama** 

Bu olay bir iç FileX dizin önbelleği isabeti temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Toplam kaçırma sayısı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="internal-media-flush"></a>İç Medya Boşaltma 

#### <a name="internal-media-flush"></a>İç medya boşaltma

**Simge** ![ İç medya boşaltma simgesi](./media/user-guide/fx-events/image3.png)

**Açıklama**

Bu olay bir iç FileX medya boşaltmasını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Kirli kesimlerin sayısı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.


### <a name="internal-directory-entry-read"></a>İç Dizin Girişi Okuma 

#### <a name="internal-directory-entry-read"></a>İç dizin girişi okuma

**Simge** ![ İç dizin girişi okuma simgesi](./media/user-guide/fx-events/image4.png)

**Açıklama**

Bu olay bir iç FileX dizin girişi okuma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="internal-directory-entry-write"></a>İç Dizin Girişi Yazma

#### <a name="internal-directory-entry-write"></a>İç dizin girişi yazma

**Simge** ![ İç dizin girişi yazma simgesi](./media/user-guide/fx-events/image5.png)

**Açıklama**

Bu olay bir iç FileX Dizin girişi yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-read"></a>İç g/ç sürücüsü okuma 

#### <a name="internal-io-driver-read"></a>İç g/ç sürücüsü okuma 

**Simge** ![ İç g/ç sürücüsü okuma simgesi](./media/user-guide/fx-events/image6.png)

**Açıklama** 

Bu olay iç bir FileX g/ç sürücüsü okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: sektör.
- Bilgi alanı 3: sektör sayısı.
- Bilgi alanı 4: arabellek işaretçisi.

### <a name="internal-io-driver-write"></a>İç g/ç sürücüsü yazma 

#### <a name="internal-io-driver-write"></a>İç g/ç sürücüsü yazma 

**Simge** ![ İç g/ç sürücüsü yazma simgesi](./media/user-guide/fx-events/image7.png)

**Açıklama** 

Bu olay bir iç FileX g/ç sürücüsü yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: sektör.
- Bilgi alanı 3: sektör sayısı.
- Bilgi alanı 4: arabellek işaretçisi.

### <a name="internal-io-driver-flush"></a>İç g/ç sürücüsü Temizleme 

#### <a name="internal-io-driver-flush"></a>İç g/ç sürücüsü Temizleme 

**Simge** ![ İç g/ç sürücüsü Temizleme simgesi](./media/user-guide/fx-events/image8.png)

**Açıklama** 

Bu olay bir iç FileX g/ç Sürücü temizleme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-abort"></a>İç g/ç sürücüsü Iptali 

#### <a name="internal-io-dirver-abort"></a>İç g/ç dirver iptali

**Simge** ![ İç g/ç sürücüsü iptali simgesi](./media/user-guide/fx-events/image9.png)

**Açıklama**

Bu olay bir iç FileX g/ç sürücüsü iptali olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-initialize"></a>İç g/ç sürücüsü başlatma 

#### <a name="internal-io-driver-initialize"></a>İç g/ç sürücüsü başlatma 

**Simge** ![ İç g/ç sürücüsü başlatma simgesi](./media/user-guide/fx-events/image10.png)

**Açıklama** 

Bu olay bir iç FileX g/ç sürücüsü başlatma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-boot-sector-read"></a>İç g/ç sürücüsü önyükleme kesimi okuma 

#### <a name="internal-io-driver-boot-sector-read"></a>İç g/ç sürücüsü önyükleme kesimi okuma 

**Simge** ![ İç g/ç sürücüsü önyükleme kesimini okuma simgesi](./media/user-guide/fx-events/image11.png)

**Açıklama** 

Bu olay bir iç FileX g/ç sürücüsü önyükleme kesimi okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: arabellek işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-release-sectors"></a>İç g/ç sürücüsü sürüm kesimleri 

#### <a name="internal-io-driver-release-sectors"></a>İç g/ç sürücüsü sürüm kesimleri 

**Simge** ![ İç g/ç sürücüsü sürüm kesimleri simgesi](./media/user-guide/fx-events/image12.png)

**Açıklama** 

Bu olay bir iç FileX g/ç sürücüsü sürüm kesimleri olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: sektör.
- Bilgi alanı 3: sektör sayısı.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-boot-sector-write"></a>İç g/ç sürücüsü önyükleme kesimi yazma

#### <a name="internal-io-driver-boot-sector-write"></a>İç g/ç sürücüsü önyükleme kesimi yazma 

**Simge** ![ İç g/ç sürücüsü önyükleme kesimi yazma simgesi](./media/user-guide/fx-events/image13.png)

**Açıklama** 

Bu olay bir iç FileX g/ç sürücüsü önyükleme kesimi yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: arabellek işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-un-initialize"></a>İç g/ç sürücüsü başlatması geri al 

#### <a name="internal-io-driver-un-initialize"></a>İç g/ç sürücüsü başlatması geri al 

**Simge** ![ İç g/ç sürücüsü başlatması kaldır simgesi](./media/user-guide/fx-events/image14.png)

**Açıklama** 

Bu olay iç bir FileX g/ç sürücüsü başlatma kaldırma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.
</blockquote></td>

### <a name="directory-attributes-read"></a>Okunan dizin öznitelikleri 

#### <a name="fx_directory_attributes_read"></a>fx_directory_attributes_read 

**Simge** ![ Dizin özniteliklerini oku simgesi](./media/user-guide/fx-events/image15.png)

**Açıklama** 

Bu olay, bir dizin öznitelikleri okuma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dizin adının işaretçisi.
- Bilgi Alanı 3: Öznitelikler bit eşlemesi:

  | Öznitelik                         | Değer        |
  |---------------------------------- | --------|
  |  Salt Okunur                        | (0x01)  |
  |  Gizli                           | (0x02)  |
  |  Sistem                           | (0x04)  |
  |  Birim                           | (0x08)  |
  |  Dizin                        | (0x10)  |
  |  Arşiv                          | (0x20)  |
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-attributes-set"></a>Dizin Öznitelikleri Kümesi 

#### <a name="fx_directory_attributes_set"></a>fx_directory_attributes_set 

**Simge** ![ Öznitelik kümesi simgesi](./media/user-guide/fx-events/image16.png)

**Açıklama** 

Bu olay dizin öznitelik kümesi olayı dizinini temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dizin adının işaretçisi.
- Bilgi Alanı 3: Öznitelikler bit eşlemesi:

  |  Öznitelik                        | Değer        |
  |---------------------------------- | --------|
  |  Salt Okunur                        | (0x01)  |
  |  Gizli                           | (0x02)  |
  |  Sistem                           | (0x04)  |
  |  Arşiv                          | (0x20)  |
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-create"></a>Dizin Oluşturma 

#### <a name="fx_directory_create"></a>fx_directory_create

**Simge** ![ Dizin oluşturma simgesi](./media/user-guide/fx-events/image17.png)

**Açıklama** 

Bu olay bir dizin oluşturma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dizin adının işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-default-get"></a>Dizin Varsayılanı Al 

#### <a name="fx_directory_default_get"></a>fx_directory_default_get 

**Simge** ![ Dizin varsayılanı get simgesi](./media/user-guide/fx-events/image18.png)

**Açıklama** 

Bu olay bir dizin varsayılan kümesi olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dönüş yolu adı işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-default-set"></a>Dizin Varsayılan Kümesi 

#### <a name="fx_directory_default_set"></a>fx_directory_default_set 

**Simge** ![ Dizin varsayılan kümesi simgesi](./media/user-guide/fx-events/image19.png)

**Açıklama** 

Bu olay bir dizin varsayılan kümesi olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Yeni varsayılan yol adının işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-delete"></a>Dizin Silme 

#### <a name="fx_directory_delete"></a>fx_directory_delete

**Simge** ![ Dizin silme simgesi](./media/user-guide/fx-events/image20.png)

**Açıklama** 

Bu olay bir dizin silme olayıdır.

**Bilgi Alanları**
- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dizin adının işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-first-entry-find"></a>Dizin İlk Giriş Bul 

#### <a name="fx_directory_first_entry_find"></a>fx_directory_first_entry_find

**Simge** ![ Dizin ilk girdisi bul simgesi](./media/user-guide/fx-events/image21.png)

**Açıklama** 

Bu olay bir dizin ilk girdi bulma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dizin adının işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-first-full-entry-find"></a>Dizin İlk Tam Giriş Bul 

#### <a name="fx_directory_first_full_entry_find"></a>fx_directory_first_full_entry_find

**Simge** ![ Dizin ilk tam giriş bul simgesi](./media/user-guide/fx-events/image22.png)

**Açıklama** 

Bu olay, dizin ilk tam giriş bulma olayıdır.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dizin adının işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-information-get"></a>Dizin bilgileri al 

#### <a name="fx_directory_information_get"></a>fx_directory_information_get

**Simge** ![ Dizin bilgileri al simgesi](./media/user-guide/fx-events/image23.png)

**Açıklama** 

Bu olay bir dizin bilgileri al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: Dizin adı Işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-local-path-clear"></a>Dizin yerel yolu temizle 

#### <a name="fx_directory_local_path_clear"></a>fx_directory_local_path_clear

**Simge** ![ Dizin yerel yolu temizle simgesi](./media/user-guide/fx-events/image24.png)

**Açıklama** 

Bu olay, Dizin yerel yolu temizle olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-local-path-get"></a>Dizin yerel yolu al 

#### <a name="fx_directory_local_path_get"></a>fx_directory_local_path_get

**Simge** ![ Dizin yerel yolu al simgesi](./media/user-guide/fx-events/image25.png)

**Açıklama** 

Bu olay bir dizin yerel yolu al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: dönüş yolu adı Işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-local-path-restore"></a>Dizin yerel yolunu geri yükleme 

#### <a name="fx_directory_local_path_restore"></a>fx_directory_local_path_restore

**Simge** ![ Dizin yerel yolu geri yükleme simgesi](./media/user-guide/fx-events/image26.png)

**Açıklama** 

Bu olay, Dizin yerel yolu geri yükleme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: yerel yol yapısına yönelik Işaretçi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-local-path-set"></a>Dizin yerel yol kümesi 

#### <a name="fx_directory_local_path_set"></a>fx_directory_local_path_set

**Simge** ![ Dizin yerel yolu kümesi simgesi](./media/user-guide/fx-events/image27.png)

**Açıklama** 

Bu olay bir dizin yerel yol kümesi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: yerel yol yapısına yönelik Işaretçi.
- Bilgi alanı 3: yeni yol adı Işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-long-name-get"></a>Dizin uzun adı Al 

#### <a name="fx_directory_long_name_get"></a>fx_directory_long_name_get

**Simge** ![ Dizin uzun adı Al simgesi](./media/user-guide/fx-events/image28.png)

**Açıklama** 

Bu olay bir dizin uzun adı Al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kısa dosya adı Işaretçisi.
- Bilgi alanı 3: uzun dosya adı Işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-name-test"></a>Dizin adı sınaması 

#### <a name="fx_directory_name_test"></a>fx_directory_name_test

**Simge** ![ Dizin adı test simgesi](./media/user-guide/fx-events/image29.png)

**Açıklama** 

Bu olay bir dizin adı sınama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: Dizin adı Işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-next-entry-find"></a>Dizin sonraki giriş bul 

#### <a name="fx_directory_next_entry_find"></a>fx_directory_next_entry_find

**Simge** ![ Dizin sonraki giriş bul simgesi](./media/user-guide/fx-events/image30.png)

**Açıklama** 

Bu olay bir dizin sonraki girişi bul olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: Dizin adı Işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-next-full-entry-find"></a>Dizin bir sonraki tam girdi bul 

#### <a name="fx_directory_next_full_entry_find"></a>fx_directory_next_full_entry_find

**Simge** ![ Dizin bir sonraki tam giriş bul simgesi](./media/user-guide/fx-events/image31.png)

**Açıklama**

Bu olay, bir dizinin bir sonraki tam giriş bul olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: Dizin adı Işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="directory-rename"></a>Dizin yeniden adlandırma 

#### <a name="fx_directory_rename-event"></a>fx_directory_rename olayı

**Simge** ![ Dizin yeniden adlandırma simgesi](./media/user-guide/fx-events/image32.png)

**Açıklama**

Bu olay bir dizin yeniden adlandırma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: eski dizin adı Işaretçisi.
- Bilgi alanı 3: yeni dizin adı Işaretçisi.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="directory-short-name-get"></a>Dizin Kısa Adı Al 

#### <a name="fx_directory_short_name_get"></a>fx_directory_short_name_get

**Simge** ![ Dizin kısa adı al simgesi](./media/user-guide/fx-events/image33.png)

**Açıklama**

Bu olay bir dizin kısa adı get olayı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Uzun dosya adının işaretçisi.
- Bilgi Alanı 3: Kısa dosya adının işaretçisi.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="file-allocate"></a>Dosya Ayırma 

#### <a name="fx_file_allocate"></a>fx_file_allocate

**Simge** ![ Dosya ayırma simgesi](./media/user-guide/fx-events/image34.png)

**Açıklama**

Bu olay bir dosya ayırma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Dosyanın işaretçisi.
- Bilgi Alanı 2: İstenen boyut.
- Bilgi Alanı 3: Geçerli boyut.
- Bilgi Alanı 4: Yeni boyut.

### <a name="file-attributes-read"></a>Okunan Dosya Öznitelikleri 

#### <a name="fx_file_attributes_read"></a>fx_file_attributes_read

**Simge** ![ Dosya öznitelikleri okuma simgesi](./media/user-guide/fx-events/image35.png)

**Açıklama**

Bu olay, bir dosya özniteliklerini okuma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi. 
- Bilgi Alanı 2: Öznitelikler bit eşlemesi:

  |  Attribut                         | Değer        |
  |---------------------------------- | --------|
  |  Salt Okunur                        | (0x01)  |
  |  Gizli                           | (0x02)  |
  |  Sistem                           | (0x04)  |
  |  Birim                           | (0x08)  |
  |  Dizin                        | (0x10)  |
  |  Arşiv                          | (0x20)  |
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="file-attributes-set"></a>Dosya Öznitelikleri Kümesi 

#### <a name="fx_file_attributes_set"></a>fx_file_attributes_set

**Simge** ![ Dosya öznitelikleri kümesi simgesi](./media/user-guide/fx-events/image36.png)

**Açıklama** 

Bu olay, bir dosya öznitelikleri kümesi olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dosya adının işaretçisi. 
- Bilgi Alanı 3: Öznitelikler bit eşlemesi:

  | Öznitelik                         | Değer        |
  |---------------------------------- | --------|
  |  Salt Okunur                        | (0x01)  |
  |  Gizli                           | (0x02)  |
  |  Sistem                           | (0x04)  |
  |  Arşiv                          | (0x20)  |
- Bilgi Alanı 4: Kullanılmadı.

### <a name="file-best-effort-allocate"></a>Dosya Ayırma için En İyi Çaba 

#### <a name="fx_file_best_effort_allocate"></a>fx_file_best_effort_allocate

**Simge** ![ Dosya en iyi çabayı ayırma simgesi](./media/user-guide/fx-events/image37.png)

**Açıklama** 

Bu olay, olayı ayırmak için en iyi çabayı gösteren bir dosyayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Dosyanın işaretçisi.
- Bilgi Alanı 2: İstenen boyut.
- Bilgi Alanı 3: Ayrılan gerçek boyut.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="file-close"></a>Dosya Kapatma 

#### <a name="fx_file_close"></a>fx_file_close

**Simge** ![ Dosya kapatma simgesi](./media/user-guide/fx-events/image38.png)

**Açıklama** 

Bu olay bir dosya kapatma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Dosyanın işaretçisi.
- Bilgi Alanı 2: Dosya boyutu.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="file-create"></a>Dosya Oluşturma

#### <a name="fx_file_create"></a>fx_file_create

**Simge** ![ Dosya oluşturma simgesi](./media/user-guide/fx-events/image39.png)

**Açıklama**

Bu olay bir dosya oluşturma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Dosya adının işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="file-date-time-set"></a>Dosya Tarih Saat Kümesi 

#### <a name="fx_file_date_time_set"></a>fx_file_date_time_set

**Simge** ![ Dosya tarihi saat kümesi simgesi](./media/user-guide/fx-events/image40.png)

**Açıklama**

Bu olay bir dosya tarihi/saat kümesi olayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: dosya adı Işaretçisi.
- Bilgi alanı 3: yıl.
- Bilgi alanı 4: ay.

### <a name="file-delete"></a>Dosya silme 

#### <a name="fx_file_delete"></a>fx_file_delete

**Simge** ![ Dosya silme simgesi](./media/user-guide/fx-events/image41.png)

**Açıklama**

Bu olay bir dosya silme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: dosya adı Işaretçisi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="file-open"></a>Dosya açık 

#### <a name="fx_file_open"></a>fx_file_open

**Simge** ![ Dosya aç simgesi](./media/user-guide/fx-events/image42.png)

**Açıklama**

Bu olay bir dosya açma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: dosya denetim bloğu Işaretçisi.
- Bilgi alanı 3: dosya adı Işaretçisi.
- Bilgi alanı 4: açık tür:

  |  Açık tür                        | Değer        |
  |---------------------------------- | --------|
  |  Okuma için aç                    | -  |
  |  Yazma için aç                   | 0x01  |
  |  Okuma için hızlı aç               | 0x02 şeklindedir  |

### <a name="file-read"></a>Dosya okuma 

#### <a name="fx_file_read"></a>fx_file_read

**Simge** ![ Dosya okuma simgesi](./media/user-guide/fx-events/image43.png)

**Açıklama**

Bu olay bir dosya okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: dosya Işaretçisi.
- Bilgi alanı 2: arabellek işaretçisi.
- Bilgi alanı 3: Istek boyutu.
- Bilgi alanı 4: gerçek boyut okuma.

### <a name="file-relative-seek"></a>Dosya göreli arama 

#### <a name="fx_file_relative_seek"></a>fx_file_relative_seek

**Simge** ![ Dosya göreli arama simgesi](./media/user-guide/fx-events/image44.png)

**Açıklama**

Bu olay bir dosya göreli arama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: dosya Işaretçisi.
- Bilgi alanı 2: bayt kayması.
- Bilgi alanı 3: şuradan ara:

  | Olay                             | Değer        |
  |---------------------------------- | --------|
  |  Başlangıçtan itibaren                   | -  |
  |  Uçtan uca                         | 0x01  | 
  |  İleri                          | 0x02 şeklindedir  |
  |  Geri                         | (0x03)  |
- Bilgi alanı 4: önceki fark.

### <a name="file-rename"></a>Dosya yeniden adlandırma 

#### <a name="fx_file_rename"></a>fx_file_rename

**Simge** ![ Dosya yeniden adlandırma simgesi](./media/user-guide/fx-events/image45.png)

**Açıklama**

Bu olay bir dosya yeniden adlandırma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: eski dosya adı Işaretçisi.
- Bilgi alanı 3: yeni dosya adı Işaretçisi.
- Bilgi alanı 4: kullanılmıyor.

### <a name="file-seek"></a>Dosya ara 

#### <a name="fx_file_seek"></a>fx_file_seek

**Simge** ![ Dosya arama simgesi](./media/user-guide/fx-events/image46.png)

**Açıklama**

Bu olay bir dosya arama olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: dosya Işaretçisi.
- Bilgi alanı 2: bayt kayması.
- Bilgi alanı 3: önceki fark.
- Bilgi alanı 4: kullanılmıyor.

### <a name="file-truncate"></a>Dosya kesme 

#### <a name="fx_file_truncate"></a>fx_file_truncate

**Simge** ![ Dosya kesme simgesi](./media/user-guide/fx-events/image47.png)

**Açıklama**

Bu olay bir dosya Truncate olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: dosya Işaretçisi.
- Bilgi alanı 2: Istenen boyut.
- Bilgi alanı 3: önceki boyut.
- Bilgi alanı 4: yeni boyut.

### <a name="file-truncate-release"></a>Dosya kesme sürümü 

#### <a name="fx_file_truncate_release"></a>fx_file_truncate_release 

**Simge** ![ Dosya kesme sürümü simgesi](./media/user-guide/fx-events/image48.png)

**Açıklama**

Bu olay bir dosya Truncate Release olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: dosya Işaretçisi.
- Bilgi alanı 2: Istenen boyut.
- Bilgi alanı 3: önceki boyut.
- Bilgi alanı 4: yeni boyut.

### <a name="file-write"></a>Dosya yazma 

#### <a name="fx_file_write"></a>fx_file_write 

**Simge** ![ Dosya yazma simgesi](./media/user-guide/fx-events/image49.png)

**Açıklama**

Bu olay bir dosya yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: dosya Işaretçisi.
- Bilgi alanı 2: arabellek işaretçisi.
- Bilgi alanı 3: Istek boyutu.
- Bilgi alanı 4: gerçek boyut yazıldı.

### <a name="media-abort"></a>Medya Iptali 

#### <a name="fx_media_abort"></a>fx_media_abort 

**Simge** ![ Medya iptali simgesi](./media/user-guide/fx-events/image50.png)

**Açıklama**

Bu olay bir medya iptali olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="media-cache-invalidate"></a>Medya önbelleği geçersiz kıl

#### <a name="fx_media_cache_invalidate"></a>fx_media_cache_invalidate

**Simge** ![ Medya önbelleği geçersiz kıl simgesi](./media/user-guide/fx-events/image51.png)

**Açıklama**

Bu olay, bir medya önbelleği geçersiz kılan olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="media-check"></a>Medya denetimi 

#### <a name="fx_media_check"></a>fx_media_check

**Simge** ![ Medya onay simgesi](./media/user-guide/fx-events/image52.png)

**Açıklama**

Bu olay bir medya denetimi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: karalama bellek işaretçisi.
- Bilgi alanı 3: boş bellek boyutu.
- Bilgi alanı 4: hatalar bit eşlem:

  | Hata türü                        | Değer        |
  |---------------------------------- | --------|
  |  FAT zinciri hatası                  | 0x01  |
  |  Dizin hatası                  | 0x02 şeklindedir  |
  |  Kayıp küme hatası               | (0x04)  |
  |  Dosya boyutu hatası                  | (0x08)  |

### <a name="media-close"></a>Medya kapatma 

#### <a name="fx_media_close"></a>fx_media_close

**Simge** ![ Medya kapatma simgesi](./media/user-guide/fx-events/image53.png)

**Açıklama**

Bu olay bir medya kapatma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="media-flush"></a>Medya Temizleme 

#### <a name="fx_media_flush"></a>fx_media_flush

**Simge** ![ Medya Temizleme simgesi](./media/user-guide/fx-events/image54.png)

**Açıklama**

Bu olay bir medya Temizleme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="media-format"></a>Medya biçimi 

#### <a name="fx_media_format"></a>fx_media_format

**Simge** ![ Medya biçimi simgesi](./media/user-guide/fx-events/image55.png)

**Açıklama**

Bu olay bir medya biçimi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kök girişlerinin sayısı.
- Bilgi alanı 3: kesimler.
- Bilgi alanı 4: küme başına kesimler.

### <a name="media-open"></a>Medya açık 

#### <a name="fx_media_open"></a>fx_media_open

**Simge** ![ Medya açma simgesi](./media/user-guide/fx-events/image56.png)

**Açıklama**

Bu olay medya açık olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: medya sürücüsü girişi Işaretçisi.
- Bilgi alanı 3: bellek işaretçisi.
- Bilgi alanı 4: bellek boyutu.

### <a name="media-read-media-read"></a>Medya okuma medya okuma 

#### <a name="fx_media_read"></a>fx_media_read

**Simge** ![ Medya okuma simgesi](./media/user-guide/fx-events/image57.png)

**Açıklama**

Bu olay bir medya okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi Alanı 2: Mantıksal kesim.
- Bilgi Alanı 3: Arabellek işaretçisi.
- Bilgi Alanı 4: Okunan bayt.

### <a name="media-space-available"></a>Kullanılabilir Medya Alanı 

#### <a name="fx_media_space_available"></a>fx_media_space_available

**Simge** ![ Medya alanı kullanılabilir simgesi](./media/user-guide/fx-events/image58.png)

**Açıklama**

Bu olay, kullanılabilir medya alanı olaylarını temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Kullanılabilir bayt işaretçisi.
- Bilgi Alanı 3: Ücretsiz küme sayısı.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="media-volume-get"></a>Medya Birimi Al 

#### <a name="fx_media_volume_get"></a>fx_media_volume_get

**Simge** ![ Medya birimi al simgesi](./media/user-guide/fx-events/image59.png)

**Açıklama**

Bu olay bir medya birimi get olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Birim adının işaretçisi.
- Bilgi Alanı 3: Birim kaynağı.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="media-volume-set"></a>Medya Birim Kümesi 

#### <a name="fx_media_volume_set"></a>fx_media_volume_set

**Simge** ![ Medya birimi kümesi simgesi](./media/user-guide/fx-events/image60.png)

**Açıklama**

Bu olay bir medya birim kümesi olayı temsil eder.

**Bilgi Alanları** 
- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Birim adının işaretçisi.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="media-write"></a>Medya Yazma 

#### <a name="fx_media_write"></a>fx_media_write

**Simge** ![ Medya yazma simgesi](./media/user-guide/fx-events/image61.png)

**Açıklama**

Bu olay bir medya yazma olayıdır.

**Bilgi Alanları**

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi Alanı 2: Mantıksal kesim.
- Bilgi Alanı 3: Arabellek işaretçisi.
- Bilgi Alanı 4: Yazılan bayt sayısı.

### <a name="system-date-get"></a>Sistem Tarihi Al 

#### <a name="fx_system_date_get"></a>fx_system_date_get 

**Simge** ![ Sistem tarihi al simgesi](./media/user-guide/fx-events/image62.png)

**Açıklama**

Bu olay bir sistem tarihi get olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Yıl.
- Bilgi Alanı 2: Ay.
- Bilgi Alanı 3: Gün.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="system-date-set"></a>Sistem Tarih Kümesi 

#### <a name="fx_system_date_set"></a>fx_system_date_set 

**Simge** ![ Sistem tarih kümesi simgesi](./media/user-guide/fx-events/image63.png)

**Açıklama**

Bu olay bir sistem tarih kümesi olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Yıl.
- Bilgi Alanı 2: Ay.
- Bilgi Alanı 3: Gün.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="system-initialize"></a>Sistem Başlatma 

#### <a name="fx_system_initialize"></a>fx_system_initialize 

**Simge** ![ Sistem başlatma simgesi](./media/user-guide/fx-events/image64.png)

**Açıklama**

Bu olay bir sistem başlatma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Kullanılmaz.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="system-time-get"></a>Sistem Zamanı Al 

#### <a name="fx_system_time_get"></a>fx_system_time_get 

**Simge** ![ Sistem saati al simgesi](./media/user-guide/fx-events/image65.png)

**Açıklama**

Bu olay bir sistem zamanı get olayı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Saat.
- Bilgi Alanı 2: Dakika.
- Bilgi Alanı 3: saniye.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="system-time-set"></a>Sistem Zaman Kümesi 

#### <a name="fx_system_time_set"></a>fx_system_time_set 

**Simge** ![ Sistem zaman kümesi simgesi](./media/user-guide/fx-events/image66.png)

**Açıklama**

Bu olay bir sistem zaman kümesi olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Saat.
- Bilgi Alanı 2: Dakika.
- Bilgi Alanı 3: saniye.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="unicode-directory-create"></a>Unicode Dizin Oluşturma 

#### <a name="fx_unicode_directory_create"></a>fx_unicode_directory_create 

**Simge** ![ Unicode dizini oluşturma simgesi](./media/user-guide/fx-events/image67.png)

**Açıklama**

Bu olay bir Unicode dizin oluşturma olayı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Medyanın işaretçisi.
- Bilgi alanı 2: Unicode adı Işaretçisi.
- Bilgi alanı 3: Unicode adının boyutu.
- Bilgi alanı 4: kısa ad Işaretçisi.

### <a name="unicode-directory-rename"></a>Unicode dizin yeniden adlandırma 

#### <a name="fx_unicode_directory_rename"></a>fx_unicode_directory_rename

**Simge** ![ Unicode dizin yeniden adlandırma simgesi](./media/user-guide/fx-events/image68.png)

**Açıklama**

Bu olay bir Unicode dizin yeniden adlandırma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: Unicode adı Işaretçisi.
- Bilgi alanı 3: Unicode adının boyutu.
- Bilgi alanı 4: kısa ad Işaretçisi.

### <a name="unicode-file-create"></a>Unicode dosya oluşturma 

#### <a name="fx_unicode_file_create"></a>fx_unicode_file_create

**Simge** ![ Unicode dosya oluştur simgesi](./media/user-guide/fx-events/image69.png)

**Açıklama**

Bu olay bir Unicode dosya oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: Unicode adı Işaretçisi.
- Bilgi alanı 3: Unicode adının boyutu.
- Bilgi alanı 4: kısa ad Işaretçisi.

### <a name="unicode-file-rename"></a>Unicode dosya yeniden adlandırma 

#### <a name="fx_unicode_file_rename"></a>fx_unicode_file_rename

**Simge** ![ Unicode dosya yeniden adlandırma simgesi](./media/user-guide/fx-events/image70.png)

**Açıklama**

Bu olay bir Unicode dosya yeniden adlandırma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: Unicode adı Işaretçisi.
- Bilgi alanı 3: Unicode adının boyutu.
- Bilgi alanı 4: kısa ad Işaretçisi.

### <a name="unicode-length-get"></a>Unicode uzunluğu al 

#### <a name="fx_unicode_length_get"></a>fx_unicode_length_get

**Simge** ![ Unicode uzunluğu al simgesi](./media/user-guide/fx-events/image71.png)

**Açıklama**

Bu olay bir Unicode uzunluğu Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: Unicode adı Işaretçisi.
- Bilgi alanı 2: Uzunluk.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="unicode-name-get"></a>Unicode ad al 

#### <a name="fx_unicode_name_get"></a>fx_unicode_name_get

**Simge** ![ Unicode ad Al simgesi](./media/user-guide/fx-events/image72.png)

**Açıklama**

Bu olay bir Unicode ad Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kaynak kısa adı.
- Bilgi alanı 3: hedef Unicode adı işaretçisi.
- Bilgi alanı 4: hedef Unicode adı uzunluğu.

### <a name="unicode-short-name-get"></a>Unicode kısa ad al 

#### <a name="fx_unicode_short_name_get"></a>fx_unicode_short_name_get

**Simge** ![ Unicode kısa ad Al simgesi](./media/user-guide/fx-events/image73.png)

**Açıklama**

Bu olay Unicode kısa ad Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: medyaya yönelik Işaretçi.
- Bilgi alanı 2: kaynak Unicode adı Işaretçisi.
- Bilgi alanı 3: Unicode adının uzunluğu.
- Bilgi alanı 4: kısa ad Işaretçisi.