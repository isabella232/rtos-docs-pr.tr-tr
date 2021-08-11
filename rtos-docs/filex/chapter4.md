---
title: Bölüm 4- FileX Azure RTOS açıklaması
description: Bu bölümde, FileX hizmetleriyle Azure RTOS alfabetik olarak sıralanmış bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 87b278c9b8642976fdab098636c518a3960f73cb906b4f1b28136a9a597a7a78
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783841"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a>Bölüm 4- FileX Azure RTOS açıklaması

Bu bölümde, FileX hizmetleriyle Azure RTOS alfabetik olarak sıralanmış bir açıklama yer almaktadır. Hizmet adları, benzer hizmetlerin hepsi birlikte grup olacak şekilde tasarlanmıştır.

## <a name="fx_directory_attributes_read"></a>fx_directory_attributes_read

Dizin özniteliklerini okur

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a>Description

Bu hizmet, dizinin özniteliklerini belirtilen medyadan okur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **directory_name:** İstenen dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).
- **öznitelikler** _ptr: Dizinin özniteliklerinin yerleştirilecek hedefin işaretçisi. Dizin öznitelikleri, aşağıdaki olası ayarlarla bit eşlemesi biçiminde döndürülür:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_VOLUME (0x08)
  - FX_DIRECTORY (0x10)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dizin öznitelikleri okundu
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil
- **FX _NOT BULUNDU** (0x04) Belirtilen dizin medyada bulunamadı
- **FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değil
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası
- **FX_FILE_CORRUPT** 0x08) Dosya bozuk
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_attributes_set"></a>fx_directory_attributes_set

Dizin özniteliklerini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a>Description

Bu hizmet, dizinin özniteliklerini çağıran tarafından belirtilen özniteliklere ayarlar.

> [!WARNING]
> *Bu uygulamanın yalnızca bu hizmetle dizin özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlama girişimi hataya neden olur.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **directory_name:** İstenen dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).
- **attributes:** Bu dizine yeni öznitelikler. Geçerli dizin öznitelikleri aşağıdaki gibi tanımlanır:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dizin öznitelik kümesi
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil
- **FX_NOT_FOUND** (0x04) Belirtilen dizin medyada bulunamadı
- **FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değil
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalı
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya
- **FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi
- **FX_INVALID_ATTR** (0x19) Geçersiz öznitelikler seçildi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_create"></a>fx_directory_create

Alt dizin oluşturur

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizinde veya dizin adıyla sağlanan yolda bir alt dizin oluşturur. Kök dizinden farklı olarak, alt dizinlerin tutanın dosya sayısıyla ilgili bir sınırı yoktur. Kök dizin yalnızca önyükleme kaydı tarafından belirlenen girdi sayısını tutabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **directory_name:** Oluşturulacak dizinin adının işaretçisi (dizin yolu isteğe bağlıdır).

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dizin oluşturma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil
- **FX_NOT_FOUND** (0x04) Belirtilen dizin medyada bulunamadı
- **FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değil
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası
- **FX_FILE _CORRUPT** (0x08) Dosyası bozuk
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya
- **FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi
- **FX_INVALID_ATTR** (0x19) Geçersiz öznitelikler seçildi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_default_get"></a>fx_directory_default_get

Son varsayılan dizini alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a>Description

Bu hizmet, son ayar tarafından ayarlanmış yolun işaretçisini ***fx_directory_default_set.*** Varsayılan dizin ayarlanmazsa veya geçerli varsayılan dizin kök dizinse, varsayılan dizin FX_NULL döndürülür.

> [!IMPORTANT]
> *İç yol dizesinin varsayılan boyutu 256 karakterdir; fx_api.h **dosyasındaki** FX_MAXIMUM_PATH **değiştirerek** ve FileX kitaplığının tamamını yeniden oluşturarak değiştirilebilir. Karakter dizesi yolu uygulama için korunur ve FileX tarafından dahili olarak kullanılmaz.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **return_path_name:** Son varsayılan dizin dizesi için hedefin işaretçisi. Varsayılan dizinin geçerli FX_NULL kök ise varsayılan değer değeri döndürülür. Medya açıldığında kök varsayılan değerdir.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı varsayılan dizin get
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya hedef işaretçi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_default_set"></a>fx_directory_default_set

Varsayılan dizini ayarlar

### <a name="prototype"></a>Prototype

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a>Description

Bu hizmet, medyanın varsayılan dizinini ayarlar. FX_NULL değeri sağlanırsa, varsayılan dizin medyanın kök dizinine ayarlanır. Açıkça bir yol belirtmeyen tüm sonraki dosya işlemleri bu dizine varsayılan olarak uygulanır.

> [!IMPORTANT]
> *İç yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*

> [!IMPORTANT]
> *Uygulama tarafından sağlanan adlar için, FileX, \\ dizinler, alt dizinler ve dosya adlarına ayrı ters eğik çizgi () ve eğik çizgi (/) karakterlerini destekler. Ancak, FileX yalnızca uygulamaya döndürülen yollarda ters eğik çizgi karakterini kullanır.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **new_path_name**: yeni varsayılan dizin adı işaretçisi. Bir FX_NULL değeri sağlanırsa, medyanın varsayılan dizini medyanın kök dizinine ayarlanır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı varsayılan dizin kümesi
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil
- **FX_INVALID_PATH** (0x0D) yeni dizin bulunamadı
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_delete"></a>fx_directory_delete

Alt dizini siler

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a>Description

Bu hizmet belirtilen dizini siler. Silmek için dizinin boş olması gerektiğini unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **directory_name**: silinecek dizinin adı işaretçisi (Dizin yolu isteğe bağlıdır).

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dizin silme
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil
- **FX_NOT_FOUND** (0x04) belirtilen dizin bulunamadı
- **FX_DIR_NOT_EMPTY** (0x10) belirtilen dizin boş değil
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02) geçersiz medya
- **FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok
- **FX_NOT_DIRECTORY** (0x0E) dizin girişi değil
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_first_entry_find"></a>fx_directory_first_entry_find

İlk dizin girişini alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a>Description

Bu hizmet, varsayılan dizindeki ilk giriş adını alır ve belirtilen hedefe kopyalar.

> [!WARNING]
> *Belirtilen hedef, dosya adı tarafından tanımlandığı gibi en büyük boyutlu FileX adını tutacak kadar **büyük FX_MAX_LONG_NAME_LEN.***

> [!WARNING]
> *Yerel olmayan bir yol kullanıyorsanız, dizin geçişi sırasında diğer uygulama iş parçacıklarının bu dizini değiştirmesini önlemek (ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile) önemlidir. Aksi takdirde geçersiz sonuçlar elde edilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **return_entry_name:** Varsayılan dizinde ilk giriş adı için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı ilk dizin girişi bulma
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil
- **FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya hedef işaretçi
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değil

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_first_full_entry_find"></a>fx_directory_first_full_entry_find

Tam bilgilerle ilk dizin girişini alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **directory_name:** Dizin girişinin adı için hedefin işaretçisi. En az bu kadar büyük FX_MAX_LONG_NAME_LEN.
- **attributes:** Null olmayan bir değerse, girişin yerleştirilecek öznitelikleri için hedefin işaretçisi. Öznitelikler, aşağıdaki olası ayarlarla bit eşlemesi biçiminde döndürülür:
  - **FX_READ_ONLY** (0x01)
  - **FX_HIDDEN** (0x02)
  - **FX_SYSTEM** (0x04)
  - **FX_VOLUME** (0x08)
  - **FX_DIRECTORY** (0x10)
  - **FX_ARCHIVE** (0x20)
- **size:** Null olmayan bir değerse, girişin boyutu için hedefin bayt cinsinden işaretçisi.
- **year:** Null olmayan bir değerse, girişin değişiklik yılı için hedefin işaretçisi.
- **month:** Null olmayan bir değerse, girişin değişiklik ayı için hedefin işaretçisi.
- **day:** Null olmayan bir değerse, girişin değişiklik günü için hedefin işaretçisi.
- **hour:** Null olmayan bir değerse, girişin değişiklik saati için hedefin işaretçisi.
- **minute:** Null olmayan bir değerse, girişin değişiklik dakikası için hedefin işaretçisi.
- **second:** Null olmayan bir değerse, girişin ikinci değişikliği için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı ilk dizin girişi bulma
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil
- **FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalı
- **FX_FILE _CORRUPT** (0x08) Dosyası bozuk
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya hedef işaretçi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_information_get"></a>fx_directory_information_get:

Dizin giriş bilgilerini alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **directory_name**: Dizin girişinin adı işaretçisi.
- **öznitelikler**: özniteliklerin hedefe yönelik işaretçisi.
- **Boyut**: boyut için hedefin işaretçisi.
- **Year**: yıl için hedefe yönelik işaretçi.
- **Month**: ayın hedefi işaretçisi.
- **Day**: günün hedefi işaretçisi.
- **saat**: saat için hedefin işaretçisi.
- **Minute**: dakika için hedefin işaretçisi.
- **ikinci**: ikincisi için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı ilk dizin girişi bulma
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil
- **FX_NOT_FOUND** (0x04) belirtilen dizin medyada bulunamadı
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası
- **FX_MEDIA_INVALID** (0x02) geçersiz medya
- **FX_FILE _CORRUPT** (0x08) dosyası bozuk
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim
- **FX_PTR_ERROR** (0x18) geçersiz medya veya hedef işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_clear"></a>fx_directory_local_path_clear:

Varsayılan yerel yolu temizler

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a>Description

Bu hizmet, çağıran iş parçacığı için ayarlanan önceki yerel yolu temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı yerel yol temizleme.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil
- **FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlandı
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_get"></a>fx_directory_local_path_get:

Geçerli yerel yol dizesini alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen medyanın yerel yol işaretçisini döndürür. Yerel bir yol ayarlanmamışsa, çağırana bir NULL döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **return_path_name**: yerel yol dizesinin depolanacağı hedef dize işaretçisine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı yerel yol al.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil
- **FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi


### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_restore"></a>fx_directory_local_path_restore:

Önceki yerel yolu geri yükler

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a>Description

Bu hizmet daha önce ayarlanmış bir yerel yolu geri yükler. Bu yerel yolda yapılan dizin arama konumu da geri yüklenir, bu da bu yordamı uygulama tarafından özyinelemeli Dizin traversals ' de yararlı hale getirir.

> [!IMPORTANT]
> *Her yerel yol, varsayılan olarak 256 karakter olan **FX_MAXIMUM_PATH** boyutunda bir yerel yol dizesi içerir. Bu iç yol dizesi FileX tarafından kullanılmaz ve yalnızca uygulamanın kullanımı için sağlanır. **FX_LOCAL_PATH** yerel bir değişken olarak bildiriecekse, kullanıcıların bu yapının boyutuyla büyüyen yığına dikkat etmesi gerekir. Kullanıcılar **FX_MAXIMUM_PATH** boyutunu azaltmak ve FileX kitaplık kaynağını yeniden derlemek için hoş geldiniz.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **local_path_ptr**: daha önce ayarlanan yerel yola yönelik işaretçi. Bu işaretçinin gerçekten daha önce kullanılmış ve bozulmadan yerel yola işaret ettiğinden emin olmak çok önemlidir.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı yerel yol geri yükleme.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya Şu anda açık değil.
- **FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH tanımlandı.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya yerel yol işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_local_path_set"></a>fx_directory_local_path_set

İş parçacığına özgü bir yerel yol ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a>Description

Bu hizmet, ***new_path_string** _ tarafından belirtilen bir iş parçacığına özgü yol ayarlar. Bu yordamın başarıyla tamamlanmasından sonra, _ *_local_path_ptr_** içinde depolanan yerel yol bilgileri, bu iş parçacığı tarafından yapılan tüm dosya ve dizin işlemleri için genel medya yolundan öncelikli olur. Bu, sistemdeki diğer iş parçacıklarını etkilemez 
> [!IMPORTANT]
> *Yerel yol dizesinin varsayılan boyutu 256 karakterdir; Bu, **fx_api. h** içinde **FX_MAXIMUM_PATH** değiştirilerek ve tüm FileX kitaplığını yeniden inşa ederek değiştirilebilir. Uygulama için karakter dizesi yolu tutulur ve FileX tarafından dahili olarak kullanılmaz.*

> [!IMPORTANT]
> *Uygulama tarafından sağlanan adlar için, FileX, \\ dizinler, alt dizinler ve dosya adlarına ayrı ters eğik çizgi () ve eğik çizgi (/) karakterlerini destekler. Ancak, FileX yalnızca uygulamaya döndürülen yollarda ters eğik çizgi karakterini kullanır.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: daha önce açılmış medyaya yönelik işaretçi.
- **local_path_ptr**: iş parçacığına özgü yerel yol bilgilerini tutmak için hedef. Bu yapının adresi gelecekte yerel yol geri yükleme işlevine sağlanabilir.
- **new_path_name**: kurulumun yerel yolunu belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı varsayılan dizin kümesi.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_IMPLEMENTED** (0x22) * * FX_NO_LCOAL_PATH
- **FX_INVALID_PATH** (0x0D) yeni dizin bulunamadı.
- **FX_NOT_IMPLEMENTED** (0x22)-* * FX_NO_LOCAL_PATH tanımlı.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya yerel yol işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_long_name_get"></a>fx_directory_long_name_get:

Kısa addan uzun ad alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan kısa (8.3 biçim) adıyla ilişkili uzun adı (varsa) verir. Kısa ad bir dosya adı veya dizin adı olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **short_name:** Kaynak kısa adının işaretçisi (8.3 biçimi).
- **long_name:** Uzun ad için hedefin işaretçisi. Uzun ad yoksa kısa ad döndürülür. Uzun adın hedefinin, uzun karakterlerin tutulacak kadar büyük FX_MAX_LONG_NAME_LEN dikkat edin.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı uzun ad get
- **FX_NOT_FOUND** (0x04) Kısa ad bulunamadı
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçisi
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değil

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_long_name_get_extended"></a>fx_directory_long_name_get_extended

Kısa addan uzun ad alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan kısa (8.3 biçim) adıyla ilişkili uzun adı (varsa) verir. Kısa ad bir dosya adı veya dizin adı olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **short_name:** Kaynak kısa adının işaretçisi (8.3 biçimi).
- **long_name:** Uzun ad için hedefin işaretçisi. Uzun ad yoksa kısa ad döndürülür. Not: Uzun adın hedefi, uzun karakterlerin tutulacak **FX_MAX_LONG_NAME_LEN** olmalıdır.
- **long_file_name_buffer_length:** Uzun ad arabelleğinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı uzun ad get.
- **FX_NOT_FOUND** (0x04) Kısa ad bulunamadı.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name, sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_name_test"></a>fx_directory_name_test

Dizin için testler

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen adın bir dizin olup olmadığını sınar. Öyleyse, bir FX_SUCCESS döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.
- **directory_name**: Dizin girişinin adı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) sağlanan ad bir dizindir.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil
- **FX_NOT_FOUND** (0x04) dizin girişi bulunamadı.
- **FX_NOT_DIRECTORY** (0x0E) girişi bir dizin değil
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_MEDIA_INVALID** (0x02) ortam geçersiz.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create

## <a name="fx_directory_next_entry_find"></a>fx_directory_next_entry_find:

Sonraki dizin girişini seçer

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizindeki bir sonraki giriş adını döndürür.

> [!WARNING]
> *Yerel olmayan bir yol kullanılıyorsa, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek için de önemlidir (bir ThreadX semaforu veya iş parçacığı öncelik düzeyiyle). Aksi takdirde, geçersiz sonuçlar elde edilebilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **return_entry_name**: varsayılan dizindeki bir sonraki giriş adı için hedef işaretçisi. Bu işaretçinin işaret ettiği arabellek, **_FX_MAX_LONG_NAME_LEN_** tarafından tanımlanan en büyük FileX adı boyutunu tutabilecek kadar büyük olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı bir sonraki giriş bul
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NO_MORE_ENTRIES** (0x0F) bu dizinde daha fazla girdi yok.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_next_full_entry_find"></a>fx_directory_next_full_entry_find:

Tam bilgi içeren bir sonraki dizin girişini alır

### <a name="prototype"></a>Prototype

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

### <a name="description"></a>Description

Bu hizmet, varsayılan dizindeki bir sonraki giriş adını alır ve belirtilen hedefe kopyalar. Ayrıca, ek giriş parametreleriyle belirtilen girdi hakkında tam bilgileri döndürür.

> [!WARNING]
> * Belirtilen hedef, * * * FX_MAX_LONG_NAME_LEN * * * * ile tanımlanan en büyük boyutlu FileX adını tutabilecek kadar büyük olmalıdır

> [!WARNING]
> *Yerel olmayan bir yol kullanıyorsanız, bir dizin çapraz geçişi gerçekleşirken diğer uygulama iş parçacıklarının bu dizini değiştirmesini engellemek (bir ThreadX semaforu, mutex veya öncelik düzeyi değişikliği ile birlikte) için diğer uygulama iş parçacıklarından kaçınmak önemlidir. Aksi takdirde, geçersiz sonuçlar elde edilebilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **directory_name:** Dizin girişinin adı için hedefin işaretçisi. en az bir veya daha büyük **FX_MAX_LONG_NAME_LEN.**
- **attributes:** Null olmayan bir değerse, girişin yerleştirilecek öznitelikleri için hedefin işaretçisi. Öznitelikler, aşağıdaki olası ayarlarla bit eşlemesi biçiminde döndürülür:
  - **FX_READ_ONLY** (0x01)
  - **FX_HIDDEN** (0x02)
  - **FX_SYSTEM** (0x04)
  - **FX_VOLUME** (0x08)
  - **FX_DIRECTORY** (0x10)
  - **FX_ARCHIVE** (0x20)
- **size:** Null olmayan bir değerse, girişin boyutu için hedefin bayt cinsinden işaretçisi.
- **month:** Null olmayan bir değerse, girişin değişiklik ayı için hedefin işaretçisi.
- **year:** Null olmayan bir değerse, girişin değişiklik yılı için hedefin işaretçisi.
- **day:** Null olmayan bir değerse, girişin değişiklik günü için hedefin işaretçisi.
- **hour:** Null olmayan bir değerse, girişin değişiklik saati için hedefin işaretçisi.
- **minute:** Null olmayan bir değerse, girişin değişiklik dakikası için hedefin işaretçisi.
- **second:** Null olmayan bir değerse, girişin ikinci değişikliği için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dizin sonraki girdi bulma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya.
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi veya tüm giriş parametreleri NULL.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_rename"></a>fx_directory_rename

Dizini yeniden adlandırıyor

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a>Description

Bu hizmet, dizin adını belirtilen yeni dizin adıyla değiştirir. Yeniden adı, belirtilen yola veya varsayılan yola göre de yapılır. Yeni dizin adı içinde bir yol belirtilirse, yeniden adlandırılan dizin belirtilen yola etkili bir şekilde taşınır. Yol belirtilmezse, yeniden adlandırılan dizin geçerli varsayılan yola yerleştirilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **old_directory_name:** Geçerli dizin adının işaretçisi.
- **new_directory_name:** Yeni dizin adının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dizin yeniden adlandırması.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) Dizin girdisi bulunamadı.
- **FX_NOT_DIRECTORY** (0x0E) Girdisi bir dizin değildir.
- **FX_INVALID_NAME** (0x0C) Yeni dizin adı geçersiz.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya.
- **FX_NO_MORE_ENTRIES** (0x0F) Bu dizinde başka giriş yok.
- **FX_INVALID_PATH** (0x0D) Dizin adı ile sağlanan geçersiz yol.
- **FX_ALREADY_CREATED** (0x0B) Belirtilen dizin zaten oluşturulmuş.
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_short_name_get
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_short_name_get"></a>fx_directory_short_name_get:

Uzun bir addan kısa ad alır

### <a name="prototype"></a>Prototype

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan uzun adla ilişkili kısa (8.3 biçim) adı verir. Uzun ad bir dosya adı veya dizin adı olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **long_name:** Kaynak uzun adının işaretçisi.
- **short_name:** Hedef kısa adın işaretçisi (8.3 biçimi). Kısa adın hedefinin 14 karakter uzunluğunda olacak kadar büyük olması gerektiğini unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı kısa ad get.
- **FX_NOT_FOUND** (0x04) Uzun ad bulunamadı.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_directory_short_name_get_extended"></a>fx_directory_short_name_get_extended

Uzun bir addan kısa ad alır

### <a name="prototype"></a>Prototype

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan uzun adla ilişkili kısa (8.3 biçim) adı verir. Uzun ad bir dosya adı veya dizin adı olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **long_name:** Kaynak uzun adının işaretçisi.
- **short_name:** Hedef kısa adın işaretçisi (8.3 biçimi). Not: Kısa adın hedefi 14 karakter uzunluğunda olacak kadar büyük olmalıdır.
- **short_file_name_length:** Kısa ad arabelleğinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı kısa ad get.
- **FX_NOT_FOUND** (0x04) Uzun ad bulunamadı.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02) Geçersiz medya.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_unicode_directory_create
- fx_unicode_directory_rename

## <a name="fx_fault_tolerant_enable"></a>fx_fault_tolerant_enable

Hataya dayanıklı hizmeti sunar

### <a name="prototype"></a>Prototype

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a>Description

Bu hizmet, hataya dayanıklı modüle izin vermez. Başlamadan sonra, hataya dayanıklı modül dosya sisteminin FileX hataya dayanıklı koruma altında olup olmadığını algılar. Aksi takdirde, hizmet, dosya sistemi işlemlerinde günlükleri depolamak için dosya sisteminde kullanılabilir kesimleri bulur. Dosya sistemi, FileX hataya dayanıklı koruma altındaysa, bütünlüğünü sürdürmek için günlükleri dosya sistemine uygular.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **memory_ptr**: hataya dayanıklı modül tarafından karalama belleği olarak kullanılan bir bellek bloğuna yönelik işaretçi.
- **memory_size**: karalama belleğinin boyutu. Hata toleranslı 'nin düzgün çalışması için, karalama belleği boyutu en az 3072 bayt olur ve sektör boyutunun katı olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) hata dayanıklılığını başarıyla etkinleştirdi.
- **FX_NOT_ENOUGH_MEMORY** (0x91) bellek boyutu çok küçük.
- **FX_BOOT_ERROR** (0x01) önyükleme kesimi hatası.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.
- Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.
- **FX_SECTOR_INVALID** (0x89) kesimi geçersiz
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_system_initialize
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write

## <a name="fx_file_allocate"></a>fx_file_allocate

Bir dosya için alan ayırır

### <a name="prototype"></a>Prototype

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar. FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler. Sonuç daha sonra bir sonraki bütün kümeye yuvarlanır.

4 GB 'den daha fazla alan ayırmak için, uygulama Service *fx_file_extended_allocate* kullanacaktır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: daha önce açılmış bir dosyanın işaretçisi.
- **Boyut**: dosya için ayrılacak bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya ayırma.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.
- **FX_FAT_READ_ERROR** (0x03), FAT girişini okuyamadı.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla kullanılabilir boş küme yok.
- Bu dosyayla ilişkilendirilmiş **FX_NO_MORE_SPACE** (0X0a) medya yeterli kullanılabilir kümeye sahip değil.
- **FX_SECTOR_INVALID** (0x89) kesimi geçersiz
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open fx_file_read
- fx_file_relative_seek
- fx_file_rename fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_attributes_read"></a>fx_file_attributes_read

Dosya özniteliklerini okur

### <a name="prototype"></a>Prototype

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a>Description

Bu hizmet, dosyanın özniteliklerini belirtilen medyadan okur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **file_name**: istenen dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).
- **attributes_ptr**: dosyaya yerleştirilecek özniteliklerin hedefi işaretçisi. Dosya öznitelikleri, aşağıdaki olası ayarlarla bir bit eşleme biçiminde döndürülür:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_VOLUME (0x08)
  - FX_DIRECTORY (0x10)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı özniteliği okundu.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.
- **FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya öznitelik işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_attributes_set"></a>fx_file_attributes_set

Dosya özniteliklerini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a>Description

Bu hizmet, dosyanın özniteliklerini çağıran tarafından belirtilen olanlarla ayarlar.

> [!WARNING]
> *Uygulamanın yalnızca bu hizmetle birlikte dosyanın özniteliklerinin bir alt kümesini değiştirmesine izin verilir. Ek öznitelikler ayarlamaya yönelik her türlü girişim bir hataya neden olur.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **file_name**: istenen dosyanın adı işaretçisi * * (Dizin yolu isteğe bağlıdır).
- **öznitelikler**: dosyanın yeni öznitelikleri. Geçerli dosya öznitelikleri aşağıdaki gibi tanımlanır:
  - FX_READ_ONLY (0x01)
  - FX_HIDDEN (0x02)
  - FX_SYSTEM (0x04)
  - FX_ARCHIVE (0x20)

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı öznitelik kümesi.
- **FX_ACCESS_ERROR** (0x06) dosyası açık ve öznitelikleri ayarlanamaz.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NO_MORE_ENTRIES** (0x0F) FAT tablosunda veya exFAT Cluster eşlemesinde daha fazla girdi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.
- **FX_NOT_FOUND** (0x04) belirtilen dosya medyada bulunamadı.
- **FX_NOT_A_FILE** (0x05) belirtilen dosya bir dizin.
- **FX_SECTOR_INVALID** (0x89) kesimi geçersiz
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_MEDIA_INVALID** (0x02) ortam geçersiz.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.
- **FX_INVALID_ATTR** (0x19) geçersiz öznitelikler seçildi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_best_effort_allocate"></a>fx_file_best_effort_allocate

Dosya için alan ayırmak için en iyi çaba

### <a name="prototype"></a>Prototype

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a>Description

Bu hizmet, bir veya daha fazla bitişik kümeyi belirtilen dosyanın sonuna ayırır ve bağlar. FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler. Sonuç daha sonra bir sonraki kümenin tamam yanına yuvarlanmış olur. Medyada yeterli ardışık küme yoksa, bu hizmet ardışık kümeler için kullanılabilen en büyük bloğu dosyaya bağlar. Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.

Uygulama, 4 GB'ın üzerinde alan ayırmak için hizmet *fx_file_extended_best_effort_allocate.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.
- **boyut:** Dosya için ayrılarak ayrılan bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı en iyi çaba dosya ayırma.
- **FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.
- **FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.
- **FX_NO_MORE_SPACE** (0x0A) Bu dosyayla ilişkilendirilmiş medya yeterli kullanılabilir kümeye sahip değil.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi veya hedefi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_close"></a>fx_file_close

Dosyayı kapatır

### <a name="prototype"></a>Prototype

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a>Description

Bu hizmet belirtilen dosyayı kapatır. Dosya yazmaya açıksa ve değiştirilmişse, bu hizmet dizin girdisini yeni boyut ve geçerli sistem saati ve tarihi ile güncelleştirerek dosya değiştirme işlemini tamamlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya kapatma.
- **FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya öznitelik işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_create"></a>fx_file_create

Dosya oluşturur

### <a name="prototype"></a>Prototype

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen dosyayı varsayılan dizinde veya dosya adıyla sağlanan dizin yolunda oluşturur.

> [!WARNING]
> *Bu hizmet sıfır uzunluklu bir dosya oluşturur, başka bir ifadeyle ayrılmış küme yoktur. Ayırma, sonraki dosya yazmalarında otomatik olarak yapılır veya fx_file_allocate hizmetiyle veya 4 GB'ın fx_file_extended_allocate alan için önceden yapılabilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **file_name:** Oluşturulacak dosyanın adının işaretçisi (dizin yolu isteğe bağlıdır).

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya oluşturma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_ALREADY_CREATED** (0x0B) Belirtilen dosya zaten oluşturulmuş.
- **FX_NO_MORE_SPACE** (0x0A) Kök dizinde daha fazla giriş yok veya kullanılabilir başka küme yok.
- **FX_INVALID_PATH** (0x0D) Dosya adıyla sağlanan geçersiz yol.
- **FX_INVALID_NAME** (0x0C) Dosya adı geçersiz.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_MEDIA_INVALID** (0x02)Geçersiz medya.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Temel alınan medya yazma korumalıdır.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya dosya adı işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a>Ayrıca Bkz.
- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_date_time_set"></a>fx_file_date_time_set

### <a name="sets-file-date-and-time"></a>Dosya tarih ve saati ayarlar

Dosya Tarihi ve Saati Ayarlama

### <a name="prototype"></a>Prototype

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
### <a name="description"></a>Description

Bu hizmet, belirtilen dosyanın tarih ve saati ayarlar.

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **file_name:** Dosyanın adının işaretçisi.
- **year:** Yılın değeri (1980-2107 dahil).
- **month:** Ayın değeri (1-12 dahil).
- **day:** Günün değeri (1-31 dahil).
- **hour:** Saat değeri (0-23 dahil).
- **minute:** Dakika değeri (0-59 dahil).
- **second:** Saniyenin değeri (0-59 dahil).

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı tarih/saat kümesi.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) Dosyası bulunamadı.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.
- **FX_INVALID_YEAR** (0x12) yıl geçersiz.
- **FX_INVALID_MONTH** (0x13) ay geçersiz.
- **FX_INVALID_DAY** (0x14) gün geçersiz.
- **FX_INVALID_HOUR** (0x15) saat geçersiz.
- **FX_INVALID_MINUTE** (0x16) dakika geçersiz.
- **FX_INVALID_SECOND** (0x17) saniye geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_delete"></a>fx_file_delete

### <a name="deletes-file"></a>Dosyayı siler

Dosya silme

### <a name="prototype"></a>Prototype

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen dosyayı siler.


### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **file_name**: Silinecek dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya silme.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.
- **FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya şu anda açık.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_MEDIA_INVALID** (0x02) ortam geçersiz.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_allocate"></a>fx_file_extended_allocate

Bir dosya için alan ayırır

### <a name="prototype"></a>Prototype

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen dosyanın sonuna bir veya daha fazla bitişik kümeyi ayırır ve bağlar. FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler. Sonuç daha sonra bir sonraki kümenin tamam yanına yuvarlanmış olur.

Bu hizmet exFAT için tasarlanmıştır. Size *parametresi* 64 bit tamsayı değeri alır ve bu değer çağıranın 4 GB aralığının ötesinde önceden alan ayırması için olanak sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.
- **boyut:** Dosya için ayrılarak ayrılan bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya ayırma.
- **FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.
- **FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.
- **FX_NO_MORE_SPACE** (0x0A) Bu dosyayla ilişkilendirilmiş medya yeterli kullanılabilir kümeye sahip değil.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_best_effort_allocate"></a>fx_file_extended_best_effort_allocate

Dosya için alan ayırmak için en iyi çaba

### <a name="prototype"></a>Prototype

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a>Description

Bu hizmet, bir veya daha fazla bitişik kümeyi belirtilen dosyanın sonuna ayırır ve bağlar. FileX istenen boyutu küme başına bayt sayısına bölerek gereken küme sayısını belirler. Sonuç daha sonra bir sonraki kümenin tamam yanına yuvarlanmış olur. Medyada yeterli ardışık küme yoksa, bu hizmet ardışık kümeler için kullanılabilen en büyük bloğu dosyaya bağlar. Dosyaya gerçekten ayrılan alan miktarı çağırana döndürülür.

Bu hizmet exFAT için tasarlanmıştır. Size *parametresi* 64 bit tamsayı değeri alır ve bu değer çağıranın 4 GB aralığının ötesinde önceden alan ayırması için olanak sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.
- **boyut:** Dosya için ayrılarak ayrılan bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya ayırma.
- **FX_ACCESS_ERROR** (0x06) Belirtilen dosya yazmaya açık değil.
- **FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.
- **FX_NO_MORE_SPACE** (0x0A) Bu dosyayla ilişkilendirilmiş medya yeterli kullanılabilir kümeye sahip değil.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girişi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_relative_seek"></a>fx_file_extended_relative_seek

Göreli bir byte uzaklığına konumlar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a>Description

Bu hizmet, dahili dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlar. Sonraki herhangi bir dosya okuma veya yazma isteği, dosyada bu konumda başlar.

Bu hizmet exFAT için tasarlanmıştır. Byte_offset  parametresi, çağıranın okuma/yazma işaretçisini 4 GB aralığının ötesinde yeniden konumlandırması için 64 bit tamsayı değeri alır.

> [!IMPORTANT]
> *Arama işlemi dosyanın sonunu aramaya çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın sonuna konum sağlar. Buna karşılık, arama işlemi dosyanın başına konumlandırmaya çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başına konum sağlar.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr:** Daha önce açılmış bir dosyanın işaretçisi.
- **byte_offset:** Dosyada istenen göreli bayt uzaklığı.
- **seek_from:** Göreli aramanın nerede gerçekleştirecekleri yönü ve konumu. Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:
  - FX_SEEK_BEGIN (0x00)
  - FX_SEEK_END (0x01)
  - FX_SEEK_FORWARD (0x02)
  - FX_SEEK_BACK (0x03) FX_SEEK_BEGIN belirtilirse, arama işlemi dosyanın başından itibaren gerçekleştirilir. Bir FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir. Bu FX_SEEK_FORWARD, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir. Bu FX_SEEK_BACK, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya göreli arama.
- **FX_NOT_OPEN** (0x07) Belirtilen dosya şu anda açık değil.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_seek"></a>fx_file_extended_seek

Byte uzaklığına konumlar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a>Description

Bu hizmet, dahili dosya okuma/yazma işaretçisini belirtilen byte uzaklığına konumlar. Sonraki herhangi bir dosya okuma veya yazma isteği, dosyada bu konumda başlar.

Bu hizmet exFAT için tasarlanmıştır. Byte_offset  parametresi, çağıranın okuma/yazma işaretçisini 4 GB aralığının ötesinde yeniden konumlandırması için 64 bit tamsayı değeri alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr:** Dosya denetim bloğuna işaretçi.
- **byte_offset:** Dosyada istenen bayt uzaklığı. Sıfır değeri dosyanın başına okuma/yazma işaretçisini, dosyanın boyutundan büyük bir değer ise dosyanın sonuna okuma/yazma işaretçisini konumlar.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya arama.
- **FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_truncate"></a>fx_file_extended_truncate

Dosya keser

### <a name="prototype"></a>Prototype

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a>Description

Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser. Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz. Dosyayla ilişkili medya kümelerinin hiçbiri serbest bırakıldı.

> [!WARNING]
> *Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*

Bu hizmet, exFAT için tasarlanmıştır. *Boyut* parametresi 64 bitlik bir tamsayı değeri alır, bu da arayanın 4'lik aralığın ötesinde çalışmasına izin verir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: dosya denetim bloğuna yönelik işaretçi.
- **Boyut**: yeni dosya boyutu. Bu yeni dosya boyutunu aşan baytlar atılır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya kesilme.
- **FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.
- **FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_extended_truncate_release"></a>fx_file_extended_truncate_release

Dosya ve yayınlar kümesi keser

### <a name="prototype"></a>Prototype

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a>Description

Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser. Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz. ***Fx_file_extended_truncate*** hizmetinden farklı olarak, bu hizmet kullanılmayan kümeleri serbest bırakabilir.

> [!WARNING]
> *Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*

Bu hizmet, exFAT için tasarlanmıştır. *Boyut* parametresi 64 bitlik bir tamsayı değeri alır, bu da arayanın 4'lik aralığın ötesinde çalışmasına izin verir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: daha önce açılmış bir dosyanın işaretçisi.
- **Boyut**: yeni dosya boyutu. Bu yeni dosya boyutunu aşan baytlar atılır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya kesilme.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.
- **FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_open"></a>fx_file_open

Dosyayı açar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen dosyayı okuma ya da yazma için açar. Bir dosya birden çok kez okumak için açılabilir, ancak bir dosya yalnızca yazıcı dosyayı kapatana kadar bir kez yazmak üzere açılabilir.

> [!IMPORTANT]
> *Dosya okuma ve yazma için eşzamanlı olarak açıksa dikkatli olunmalıdır. Bir dosya okuma için eşzamanlı olarak açıldığında gerçekleştirilen dosya yazma işlemi, okuyucu kapanmadığı ve dosyayı okumak üzere yeniden açtığından, okuyucu tarafından görülemeyebilir. Benzer şekilde, dosya Truncate Services kullanılırken dosya yazıcısı dikkatli olmalıdır. Bir dosya yazıcı tarafından kesilmişse, aynı dosyanın okuyucuları geçersiz veri döndürebilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: bir medya denetim bloğuna yönelik işaretçi.
- **file_ptr**: dosya denetim bloğuna yönelik işaretçi.
- **file_name**: açılacak dosyanın adı işaretçisi (Dizin yolu isteğe bağlıdır).
- **open_type**: dosya açma türü. Geçerli açık tür seçenekleri şunlardır:
  - FX_OPEN_FOR_READ (0x00)
  - FX_OPEN_FOR_WRITE (0x01)
  - FX_OPEN_FOR_READ_FAST (0x02)

FX_OPEN_FOR_READ ve FX_OPEN_FOR_READ_FAST dosyaları açmak benzerdir:

- FX_OPEN_FOR_READ, dosyayı oluşturan kümelerin bağlı listesinin bozulmamış olduğunu ve FX_OPEN_FOR_READ_FAST Bu doğrulamayı gerçekleştirmediğinden daha hızlı hale gelmesini sağlar.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya açıldı.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) belirtilen dosya bulunamadı.
- **FX_NOT_A_FILE** (0x05) belirtilen dosya adı bir dizin veya birimdir.
- **FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve açma başarısız.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya zaten açık veya açma türü geçersiz.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_MEDIA_INVALID** (0x02) ortam geçersiz.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_read"></a>fx_file_read

Dosyadan bayt okur

### <a name="prototype"></a>Prototype

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a>Description

Bu hizmet, dosyadaki baytları okur ve bunları sağlanan arabellekte depolar. Okuma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır. İstekte daha az bayt kaldığında, yalnızca kalan baytlar arabellekte depolanır. Herhangi bir durumda, arabelleğe yerleştirilmiş baytların toplam sayısı çağırana döndürülür.

> [!WARNING]
> *Uygulama, sağlanan arabelleğin belirtilen sayıda istenen baytı depolayabilmesini sağlamalıdır.*

> [!WARNING]
> *Hedef arabellek uzun bir sözcüklük sınırındayken ve istenen boyut sizeof (**ulong**) tarafından eşit olarak bölünediyse daha hızlı performans elde edilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: dosya denetim bloğuna yönelik işaretçi.
- **buffer_ptr**: okuma için hedef arabelleğe yönelik işaretçi.
- **request_size**: okunacak en fazla bayt sayısı.
- **actual_size**: sağlanan arabelleğe okunan gerçek bayt sayısını tutacak değişkene yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya okundu.
- **FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.
- **FX_FILE_CORRUPT** (0x08) belirtilen dosya bozuk ve okuma başarısız.
- **FX_END_OF_FILE** (0x09) dosya sonuna ulaşıldı.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) geçersiz dosya veya arabellek işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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
### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate,
- fx_file_attributes_read,
- fx_file_attributes_set,
- fx_file_best_effort_allocate,
- fx_file_close,
- fx_file_create,
- fx_file_date_time_set,
- fx_file_delete,
- fx_file_extended_allocate,
- fx_file_extended_best_effort_allocate,
- fx_file_extended_relative_seek,
- fx_file_extended_seek,
- fx_file_extended_truncate,
- fx_file_extended_truncate_release,
- fx_file_open,
- fx_file_relative_seek,
- fx_file_rename,
- fx_file_seek,
- fx_file_truncate,
- fx_file_truncate_release,
- fx_file_write,
- fx_file_write_notify_set,
- fx_unicode_file_create,
- fx_unicode_file_rename,
- fx_unicode_name_get,
- fx_unicode_short_name_get

## <a name="fx_file_relative_seek"></a>fx_file_relative_seek

Göreli bayt uzaklığına pozisyonlar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a>Description

Bu hizmet, iç dosya okuma/yazma işaretçisini belirtilen göreli bayt uzaklığına konumlandırır. Sonraki dosya okuma veya yazma isteği, dosyadaki bu konumda başlayacaktır.

> [!IMPORTANT]
> *Arama işlemi dosyanın sonundan sonra arama yapmayı denerse, dosyanın okuma/yazma işaretçisi dosyanın sonuna yerleştirilir. Buna karşılık, arama işlemi dosyanın başlangıcını aşan konuma çalışırsa, dosyanın okuma/yazma işaretçisi dosyanın başlangıcına yerleştirilir.*

4 GB 'ın ötesinde bir fark değeri ile arama yapmak için, uygulama Service *fx_file_extended_relative_seek* kullanacaktır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: daha önce açılmış bir dosyanın işaretçisi.
- **byte_offset**: dosyada istenen göreli bayt kayması.
- **seek_from**: göreli arama yapılacak yönün yönü ve konumu. Geçerli arama seçenekleri aşağıdaki gibi tanımlanır:
  - FX_SEEK_BEGIN (0x00)
  - FX_SEEK_END (0x01)
  - FX_SEEK_FORWARD (0x02)
  - FX_SEEK_BACK (0x03)

FX_SEEK_BEGIN belirtilirse, arama işlemi dosyanın başından yapılır. FX_SEEK_END belirtilirse, arama işlemi dosyanın sonundan geriye doğru gerçekleştirilir. FX_SEEK_FORWARD belirtilirse, arama işlemi geçerli dosya konumundan ileri doğru gerçekleştirilir. FX_SEEK_BACK belirtilirse, arama işlemi geçerli dosya konumundan geriye doğru gerçekleştirilir.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya göreli arama.
- **FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_rename"></a>fx_file_rename

Dosyayı yeniden adlandırır

### <a name="prototype"></a>Prototype

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a>Description

Bu hizmet, tarafından belirtilen dosyanın adını *old_file_name.* Yeniden adı, belirtilen yola veya varsayılan yola göre de yapılır. Yeni dosya adı içinde bir yol belirtilirse, yeniden adlandırılan dosya belirtilen yola etkili bir şekilde taşınır. Yol belirtilmezse, yeniden adlandırılan dosya geçerli varsayılan yola yerleştirilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **old_file_name:** Yeniden adlandıracak dosyanın adının işaretçisi (dizin yolu isteğe bağlıdır).
- **new_file_name:** Yeni dosya adının işaretçisi. Dizin yoluna izin verilmez.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya yeniden adlandırma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) Belirtilen dosya bulunamadı.
- **FX_NOT_A_FILE** (0x05) Belirtilen dosya bir dizindir.
- **FX_ACCESS_ERROR** (0x06) Belirtilen dosya zaten açık.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_INVALID_NAME** (0x0C) Belirtilen yeni dosya adı geçerli bir dosya adı değil.
- **FX_INVALID_PATH** (0x0D) Yolu geçersiz.
- **FX_ALREADY_CREATED** (0x0B) Yeni dosya adı kullanılır.
- **FX_MEDIA_INVALID** (0x02) Medya geçersiz.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_NO_MORE_ENTRIES** (0x0F) Artık FAT girdisi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_seek"></a>fx_file_seek

Byte uzaklığına konumlar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a>Description

Bu hizmet, dahili dosya okuma/yazma işaretçisini belirtilen byte uzaklığına konumlar. Sonraki herhangi bir dosya okuma veya yazma isteği, dosyada bu konumda başlar.

Uygulama, 4 GB'ın ötesinde bir uzaklık değeriyle arama yapmak için *fx_file_extended_seek.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr:** Dosya denetim bloğuna işaretçi.
- **byte_offset:** Dosyada istenen bayt uzaklığı. Sıfır değeri dosyanın başına okuma/yazma işaretçisini, dosyanın boyutundan büyük bir değer ise dosyanın sonuna okuma/yazma işaretçisini konumlar.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı dosya arama.
- **FX_NOT_OPEN** (0x07) Belirtilen dosya açık değil.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamak için daha fazla alan yok
- **FX_PTR_ERROR** (0x18) Geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_truncate"></a>fx_file_truncate

Dosya keser

### <a name="prototype"></a>Prototype

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a>Description

Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser. Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz. Dosyayla ilişkili medya kümelerinin hiçbiri serbest bırakıldı.

> [!WARNING]
> *Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*

4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate* kullanacaktır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: dosya denetim bloğuna yönelik işaretçi.
- **Boyut**: yeni dosya boyutu. Bu yeni dosya boyutunu aşan baytlar atılır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya kesilme.
- **FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok
- **FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_truncate_release"></a>fx_file_truncate_release

Dosya ve yayınlar kümesi keser

### <a name="prototype"></a>Prototype

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a>Description

Bu hizmet, dosyanın boyutunu belirtilen boyuta kadar keser. Sağlanan boyut gerçek dosya boyutundan büyükse, bu hizmet hiçbir şey yapmaz. ***Fx_file_truncate*** hizmetinden farklı olarak, bu hizmet kullanılmayan kümeleri serbest bırakabilir.

> [!WARNING]
> *Okuma için aynı anda açık olabilecek bir uyarı kesiliyor dosyaları kullanın. Okuma için açılan bir dosyanın kesilmesi, geçersiz verilerin okunmasına neden olabilir.*

4 GB 'den daha fazla işlem yapmak için, uygulama Service *fx_file_extended_truncate_release* kullanacaktır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: daha önce açılmış bir dosyanın işaretçisi.
- **Boyut**: yeni dosya boyutu. Bu yeni dosya boyutunu aşan baytlar atılır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya kesilme.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.
- **FX_NOT_OPEN** (0x07) belirtilen dosya şu anda açık değil.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) temel alınan medya, yazma korumalı.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_NO_MORE_SPACE** (0x0A) işlemi tamamlamaya yönelik daha fazla alan yok.
- **FX_PTR_ERROR** (0x18) geçersiz dosya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_file_write"></a>fx_file_write

Baytları dosyaya yazar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a>Description

Bu hizmet, dosyanın geçerli konumundan başlayarak belirtilen arabellekteki baytları yazar. Yazma işlemi tamamlandıktan sonra dosyanın iç okuma işaretçisi, dosyadaki bir sonraki bayta işaret etmek üzere ayarlanır.

> [!WARNING]
> *Kaynak arabelleğinin uzun bir sözcüklük sınırında olması ve istenen boyutun sizeof (**ulong**) tarafından eşit olarak bölünemesinin ardından daha hızlı performans elde edilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: dosya denetim bloğuna yönelik işaretçi.
- **buffer_ptr**: yazma için kaynak arabelleği işaretçisi.
- **Boyut**: yazılacak bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya yazma.
- **FX_NOT_OPEN** (0x07) belirtilen dosya açık değil.
- **FX_ACCESS_ERROR** (0x06) belirtilen dosya yazma için açık değil.
- **FX_NO_MORE_SPACE** (0x0A) medyada bu yazma işlemini gerçekleştirmek için kullanılabilecek daha fazla yer yok.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_FAT_READ_ERROR** (0x03) FAT girdisi okunamıyor.
- **FX_NO_MORE_ENTRIES** (0x0F) daha fazla FAT girişi yok.
- **FX_PTR_ERROR** (0x18) geçersiz dosya veya arabellek işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate,
- fx_file_attributes_read,
- fx_file_attributes_set,
- fx_file_best_effort_allocate,
- fx_file_close,
- fx_file_create,
- fx_file_date_time_set,
- fx_file_delete,
- fx_file_extended_allocate,
- fx_file_extended_best_effort_allocate,
- fx_file_extended_relative_seek,
- fx_file_extended_seek,
- fx_file_extended_truncate,
- fx_file_extended_truncate_release,
- fx_file_open,
- fx_file_read,
- fx_file_relative_seek,
- fx_file_rename,
- fx_file_seek,
- fx_file_truncate,
- fx_file_truncate_release,
- fx_file_write_notify_set,
- fx_unicode_file_create,
- fx_unicode_file_rename,
- fx_unicode_name_get,
- fx_unicode_short_name_get

## <a name="fx_file_write_notify_set"></a>fx_file_write_notify_set

Dosya yazma bildirim işlevini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a>Description

Bu hizmet, başarılı bir dosya yazma işleminden sonra çağrılan geri çağırma işlevini yüklüyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **file_ptr**: dosya denetim bloğuna yönelik işaretçi.
- **file_write_notify**: yüklenecek dosya yazma geri arama işlevi. Callback işlevini NULL olarak ayarlayın geri çağırma işlevini devre dışı bırakır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.
- **FX_PTR_ERROR** (0x18) file_ptr null.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_media_abort"></a>fx_media_abort

Medya etkinliklerini iptal eder

### <a name="prototype"></a>Prototype

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a>Description

Bu hizmet, tüm açık dosyaları kapatma, ilişkili sürücüye bir iptal isteği gönderme ve medyayı durdurulmuş duruma yerleştirme dahil olmak üzere medyayla ilişkili tüm geçerli etkinlikleri iptal eder. Bu hizmet genellikle g/ç hataları algılandığında çağrılır.

> [!WARNING]
> *Bir iptal işlemi gerçekleştirildikten sonra yeniden kullanmak için medyanın yeniden açılması gerekir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı medya iptali.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_cache_invalidate"></a>fx_media_cache_invalidate

Mantıksal kesim önbelleğini geçersiz kılar

### <a name="prototype"></a>Prototype

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a>Description

Bu hizmet önbellekteki tüm kirli kesimleri temizler ve sonra mantıksal kesim önbelleğinin tamamını geçersiz kılar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı medya önbelleği geçersiz kılar.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya karalama işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_check"></a>fx_media_check

Medyayı hatalara karşı denetler

### <a name="prototype"></a>Prototype

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a>Description

Bu hizmet, dosya/dizin çapraz bağlantı, geçersiz FAT zincirleri ve kayıp kümeler gibi temel yapısal hatalar için belirtilen medyayı denetler. Bu hizmet ayrıca algılanan hataları düzeltme olanağı da sağlar.

Fx_media_check hizmeti, medyada dizinlerin ve dosyaların derinlik ilk analizi için karalama belleği gerektirir. Özellikle, medya denetimi hizmetine sağlanan karalama belleği birkaç dizin girişini, alt dizinlere girmeden önce geçerli dizin giriş konumunu "yığacak" bir veri yapısı ve son olarak mantıksal FAT bit eşlemesini tutacak kadar büyük olmalıdır. Karalama belleği en az 512-1024 bayt ve mantıksal FAT bit eşlemesi için bellek olmalıdır. Bu, medyada kümeler olduğu kadar bit gerektirir. Örneğin, 8000 kümeye sahip bir cihazın temsili için 1000 bayt gerekir ve bu nedenle 2048 bayt sırasına göre toplam karalama alanı gerekir.

> [!WARNING]
> *Bu hizmet yalnızca herhangi bir dosya sistemi etkinliği fx_media_open hemen çağrılmalıdır.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **scratch_memory_ptr:** Karalama belleğinin başlangıcına işaret.
- **scratch_memory_size:** Karalama belleğinin bayt cinsinden boyutu.
- **error_correction_option:** Hata düzeltme seçeneği bitleri, bit ayarlanırken hata düzeltmesi gerçekleştirilir. Hata düzeltme seçeneği bitleri aşağıdaki gibi tanımlanır:
  - FX_FAT_CHAIN_ERROR (0x01)
  - FX_DIRECTORY_ERROR (0x02)
  - FX_LOST_CLUSTER_ERROR (0x04) Yalnızca VEYA ile gerekli hata düzeltme seçeneklerini birlikte kullanın. Hata düzeltmesi gerekmiyorsa 0 değeri sağlanmalıdır.
- **errors_detected_ptr:** Aşağıda tanımlandığı gibi hata algılama bitleri için hedef:
  - FX_FAT_CHAIN_ERROR (0x01)
  - FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)
  - FX_FILE_SIZE_ERROR (0x08)

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya denetimi, ayrıntılar için algılanan hataları görüntüleme.
- **FX_ACCESS_ERROR** (0x06) Açık dosyalarda denetim gerçekleştiremiyor.
- **FX_FILE_CORRUPT** (0x08) Dosyası bozuk.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_NO_MORE_SPACE** (0x0A) Medyada daha fazla alan yok.
- **FX_NOT_ENOUGH_MEMORY** (0x91) Sağlanan karalama belleği yeterince büyük değil.
- **FX_ERROR_NOT_FIXED** (0x93) FAT32 kök dizininin düzeltilenemleri.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_SECTOR_INVALID** (0x89) Kesimi geçersiz.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya karalama işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.


### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_close"></a>fx_media_close

Medyayı kapatır

### <a name="prototype"></a>Prototype

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen medyayı kapatır. Medyayı kapatma işlemi sırasında, tüm açık dosyalar kapatılır ve kalan arabellekler fiziksel medyaya boşaltılmıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya kapatma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.
- **FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_close_notify_set"></a>fx_media_close_notify_set

Medya kapatma notify işlevini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a>Description

Bu hizmet, bir medya başarıyla kapatıldıktan sonra çağrılan bir notify callback işlevi ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **media_close_notify:** Medya kapatma bildirimi geri çağırma işlevinin yüklü olması. Geri çağırma işlevi olarak NULL değerinin geçirmesi medya kapatma geri çağrısını devre dışı bırakıyor.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Geri çağırma işlevi başarıyla yüklendi.
- **FX_PTR_ERROR** (0x18) media_ptr null.
- **FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_exfat_format"></a>fx_media_exFAT_format

Medyayı biçimlendirir

### <a name="prototype"></a>Prototype

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
### <a name="description"></a>Description

Bu hizmet verilen medyayı sağlanan parametrelere göre exFAT ile uyumlu bir şekilde biçimlendirir. Medyayı açmadan önce bu hizmetin çağrılması gerekir.

> [!WARNING]
> *Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*

> [!IMPORTANT]
> *ExFAT birim boyutu bölümün boyutuyla (MBR veya GPT düzeni varsa) veya bölüm düzeni yoksa (MBR veya GPT) tüm cihazın boyutuna eşleşmelidir. kullanılabilir sektörlerden daha az sayıda toplam sektörde biçimlendirildiyse, exFAT diskinin bir Windows sınırlama yoktur*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi. Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.
- **sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi. Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.
- **driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.
- **memory_ptr**: medya için çalışma belleğine yönelik işaretçi. memory_size, çalışma medyası belleğinin boyutunu belirtir. Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.
- **Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.
- **number_of_fats**: medyadaki Fats sayısı. Geçerli uygulama, medyada bir FAT 'ı destekler.
- **hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı. Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.
- **total_sectors**: medyadaki toplam kesim sayısı.
- **bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı. FileX, bunun 32 katı olmasını gerektirir.
> [!IMPORTANT]
> *Belirtime başvuru ile kesim başına bayt yalnızca şu değerleri alabilir: 512, 1024, 2048 veya 4096.*

- **sectors_per_cluster**: her kümedeki sektör sayısı. Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.
- **volumne_serial_number**: Bu birim için kullanılacak seri numarası.
- **boundary_unit**: fiziksel veri alanı hizalama boyutu, kesim sayısı olarak.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı medya biçimi.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.
- **FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_extended_space_available"></a>fx_media_extended_space_available

Kullanılabilir medya alanını döndürür

### <a name="prototype"></a>Prototype

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a>Description

Bu hizmet, medyada kullanılabilir olan bayt sayısını döndürür.

Bu hizmet, exFAT için tasarlanmıştır. *Available_bytes* parametresi işaretçisi 64 bitlik bir tamsayı değeri alır ve bu, çağıranın 4 ' ün üzerinde medya ile çalışmasına olanak tanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.
- **available_bytes_ptr**: medyada kalan kullanılabilir bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) medyada bulunan alanı başarıyla aldı.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi null.
- **FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_flush"></a>fx_media_flush

Fiziksel medyada verileri boşaltır

### <a name="prototype"></a>Prototype

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a>Description

Bu hizmet, herhangi bir değiştirilen dosyanın tüm önbelleğe alınan kesimlerini ve dizin girdilerini fiziksel medyada boşaltır.

> [!WARNING]
> *Bu yordam, hedef üzerinde ani bir güç kaybı olması durumunda dosya bozulması ve/veya veri kaybı riskini azaltmak için uygulama tarafından düzenli aralıklarla çağrılabilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı medya Temizleme.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_FILE_CORRUPT**    (0x08) dosyası bozuk.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi.
- **FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_format"></a>fx_media_format

Medyayı biçimlendirir

### <a name="prototype"></a>Prototype

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
### <a name="description"></a>Description

Bu hizmet verilen medyayı sağlanan parametrelere göre FAT 12/16/32 ile uyumlu bir şekilde biçimlendirir. Medyayı açmadan önce bu hizmetin çağrılması gerekir.

> [!WARNING]
> *Zaten biçimlendirilmiş bir medyanın biçimlendirilmesi, medyadaki tüm dosya ve dizinleri etkin bir şekilde siler.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi. Bu, yalnızca sürücünün çalışması için gerekli olan bazı temel bilgileri sağlamak için kullanılır.
- **sürücü**: Bu ortam için g/ç sürücüsüne yönelik işaretçi. Bu, genellikle sonraki fx_media_open çağrısına sağlanan sürücü olacaktır.
- **driver_info_ptr**: g/ç sürücüsünün yararlanmasına yönelik isteğe bağlı bilgiler işaretçisi.
- **memory_ptr**: medya için çalışma belleğine yönelik işaretçi.
- **memory_size**: çalışma medyası belleğinin boyutunu belirtir. Boyut en az medyanın kesim boyutu kadar büyük olmalıdır.
- **Volume_Name**: en fazla 11 karakter olan birim adı dizesi işaretçisi.
- **number_of_fats**: medyadaki Fats sayısı. Birincil FAT için en düşük değer 1 ' dir. 1 ' den büyük değerler, çalışma zamanında sürdürülmekte olan ek FAT kopyalarla sonuçlanır.
- **directory_entries**: kök dizindeki Dizin girişi sayısı.
- **hidden_sectors**: Bu medyanın önyükleme kesiminden önce gizlenen kesimlerin sayısı. Bu, birden çok bölüm mevcut olduğunda tipik bir davranıştır.
- **total_sectors**: medyadaki toplam kesim sayısı.
- **bytes_per_sector**: kesim başına genellikle 512 olan bayt sayısı. FileX, bunun 32 katı olmasını gerektirir.
> [!IMPORTANT]
> *Belirtime başvuru ile kesim başına bayt yalnızca şu değerleri alabilir: 512, 1024, 2048 veya 4096.*

- **sectors_per_cluster**: her kümedeki sektör sayısı. Küme, bir FAT dosya sistemindeki en düşük ayırma birimidir.
- **Heads**: fiziksel kafa sayısı.
- **sectors_per_track**: iz başına kesim sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı medya biçimi.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) medya, sürücü veya bellek işaretçisi geçersiz.
- **FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_open"></a>fx_media_open

Dosya erişimi için medya açar

### <a name="prototype"></a>Prototype

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan I/O sürücüsünü kullanarak dosya erişimi için bir medya açar.

> [!WARNING]
> *Bu hizmete sağlanan bellek iç mantıksal kesim önbelleğini uygulamak için kullanılır, bu nedenle bellek ne kadar fazla bellek sağlanırsa o kadar fazla fiziksel I/O azalır. FileX için en az bir mantıksal kesim (medya kesimi başına bayt) önbelleği gerekir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **media_name:** Medyanın adına işaretçi.
- **media_driver:** Bu medya için I/O sürücüsünün işaretçisi. I/O sürücüsünün Bölüm 5'te tanımlanan FileX sürücü gereksinimlerine uyması gerekir.
- **driver_info_ptr:** Sağlanan I/Ç sürücüsünün kullanabiliyor olduğu isteğe bağlı bilgilerin işaretçisi.
- **memory_ptr:** Medya için çalışan belleğin işaretçisi.
- **memory_size:** Çalışma medyası belleğinin boyutunu belirtir. Boyut, medyanın kesim boyutu (genellikle 512 bayt) kadar büyük olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya açma.
- **FX_BOOT_ERROR** (0x01) Medyanın önyükleme kesimi okundu.
- **FX_MEDIA_INVALID** (0x02) Belirtilen medyanın önyükleme kesimi bozuk veya geçersiz. Ayrıca, bu dönüş kodu mantıksal kesim önbellek boyutunun veya FAT giriş boyutunun 2'nin gücü olmadığını belirtmek için kullanılır.
- **FX_FAT_READ_ERROR** FAT 0x03 okuma hatası.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_PTR_ERROR** (0x18) Bir veya daha fazla işaretçi NULL olur.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_open_notify_set"></a>fx_media_open_notify_set

Medya açık notify işlevini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a>Description

Bu hizmet, bir medya başarıyla açıldıktan sonra çağrılan bir notify callback işlevi ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **media_open_notify:** Medya aç notify callback işlevi yüklenmek için. Geri çağırma işlevi olarak NULL değerinin geçirmesi, medya açık geri çağırmayı devre dışı bırakmanızı sağlar.

### <a name="return-values"></a>Dönüş Değerleri


- **FX_SUCCESS** (0x00) Geri çağırma işlevi başarılı bir şekilde yüklendi.
- **FX_PTR_ERROR** (0x18) media_ptr NULL olur.
- **FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_read"></a>fx_media_read

Medyadan mantıksal kesim okur

### <a name="prototype"></a>Prototype

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a>Description

Bu hizmet, medyadan bir mantıksal kesim okur ve sağlanan arabelleğe yer sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Önceden açılmış bir medyanın işaretçisi.
- **logical_sector:** Okunacak mantıksal kesim.
- **buffer_ptr:** Mantıksal kesim okuması için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya okuma.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya arabellek işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_space_available"></a>fx_media_space_available

Kullanılabilir medya alanını döndürür

### <a name="prototype"></a>Prototype

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a>Description

Bu hizmet, medyada kullanılabilir olan bayt sayısını döndürür.

4 GB 'den büyük medyayla çalışmak için, uygulama Service *fx_media_extended_space_available* kullanacaktır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: daha önce açılmış bir medyaya yönelik işaretçi.
- **available_bytes_ptr**: medyada kalan kullanılabilir bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) medyada kullanılabilir alanı başarıyla döndürdü.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_PTR_ERROR** (0x18) geçersiz medya işaretçisi veya kullanılabilir bayt işaretçisi null.
- **FX_CALLER_ERROR**    (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_volume_get
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_volume_get"></a>fx_media_volume_get

Medya birimi adını alır

### <a name="prototype"></a>Prototype

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a>Description

Bu hizmet, daha önce açılmış medyanın birim adını alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.
- **Volume_Name**: birim adı için hedef işaretçisi. Hedefin en az 12 karakter tutabilecek kadar büyük olması gerektiğini unutmayın.
- **volume_source**: önyükleme kesiminden veya kök dizinden adın nereden alındığını belirtir. Bu parametre için geçerli değerler şunlardır:
  - FX_BOOT_SECTOR
  - FX_DIRECTORY_SECTOR

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı medya birimi al.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) birim bulunamadı.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya birim hedefi işaretçisi.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_volume_get_extended"></a>fx_media_volume_get_extended

Önceden açılmış olan medyanın medya birimi adını alır

### <a name="prototype"></a>Prototype

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a>Description

Bu hizmet, önceden açılmış olan medyanın birim adını alır.

> [!IMPORTANT]
> Bu hizmet ***fx_media_volume_get() _** ile aynıdır, ancak çağıranın _ volume_name **arabelleğinin boyutunu* geçer.

### <a name="input-parameters"></a>Giriş Parametreleri


- **media_ptr:** Medya denetim bloğuna işaretçi.
- **volume_name:** Birim adı için hedefin işaretçisi. Hedefin en az 12 karakter uzunluğunda olacak kadar büyük olması gerektiğini unutmayın.
- **volume_name_buffer_length:** Arabelleğin volume_name boyutu.
- **volume_source:** Önyükleme kesimi veya kök dizinden adın nereden alınacaklarını belirtir. Bu parametre için geçerli değerler şunlardır:
  - FX_BOOT_SECTOR
  - FX_DIRECTORY_SECTOR

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya birimi get.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) Birimi bulunamadı.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya birim hedef işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_set
- fx_media_write
- fx_system_initialize

## <a name="fx_media_volume_set"></a>fx_media_volume_set

Medya birimi adını ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a>Description

Bu hizmet, önceden açılmış olan medyanın birim adını ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **volume_name:** Birim adının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya birimi kümesi.
- **FX_INVALID_NAME** (0x0C) Volume_name geçersiz.
- **FX_MEDIA_INVALID** (0x02) Birim adı ayarlanamıyor.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya birim adı işaretçisi.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_write
- fx_system_initialize

## <a name="fx_media_write"></a>fx_media_write

Yazma mantıksal kesimi

### <a name="prototype"></a>Prototype

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a>Description

Bu hizmet sağlanan arabelleği belirtilen mantıksal kesime yazar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Önceden açılmış bir medyanın işaretçisi.
- **logical_sector:** Yazacak mantıksal kesim.
- **buffer_ptr:** Mantıksal kesim yazma için kaynağın işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya yazma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_SECTOR_INVALID** (0x89) Geçersiz kesim.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_PTR_ERROR** (0x18) Geçersiz medya işaretçisi.
- **FX_CALLER_ERROR**    (0x20) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_fault_tolerant_enable
- fx_media_abort
- fx_media_cache_invalidate
- fx_media_check
- fx_media_close
- fx_media_close_notify_set
- fx_media_exFAT_format
- fx_media_extended_space_available
- fx_media_flush
- fx_media_format
- fx_media_open
- fx_media_open_notify_set
- fx_media_read
- fx_media_space_available
- fx_media_volume_get
- fx_media_volume_set
- fx_system_initialize

## <a name="fx_system_date_get"></a>fx_system_date_get

Dosya sistemi tarihini alır

### <a name="prototype"></a>Prototype

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a>Description

Bu hizmet geçerli sistem tarihini döndürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **year:** Yıl için hedefin işaretçisi.
- **month:** Ay için hedefin işaretçisi.
- **day:** Gün için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı tarih alma.
- **FX_PTR_ERROR** (0x18) Bir veya daha fazla giriş parametresi NULL olur.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_system_date_set
- fx_system_initialize
- fx_system_time_get
- fx_system_time_set

## <a name="fx_system_date_set"></a>fx_system_date_set

Sistem tarihini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a>Description

Bu hizmet, sistem tarihini belirtilen şekilde ayarlar.

> [!WARNING]
> *İlk sistem tarihini ayarlamak için bu **fx_system_initialize** kısa bir süre sonra çağrılacaktır. Varsayılan olarak, sistem tarihi son genel FileX sürümüne göredir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **year:** Yeni yıl. Geçerli aralık 1980 ile 2107 arasındadır.
- **month:** Yeni ay. Geçerli aralık 1 ile 12 arasındadır.
- **gün:** Yeni gün. Ay ve artık yıl koşullarına bağlı olarak geçerli aralık 1 ile 31 arasındadır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı tarih ayarı.
- **FX_INVALID_YEAR** (0x12) Geçersiz yıl belirtildi.
- **FX_INVALID_MONTH** (0x13) Geçersiz ay belirtildi.
- **FX_INVALID_DAY** (0x14) Geçersiz gün belirtildi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_system_date_get
- fx_system_initialize
- fx_system_time_get
- fx_system_time_set

## <a name="fx_system_initialize"></a>fx_system_initialize

Sistemin tamamını başlatıyor

### <a name="prototype"></a>Prototype

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a>Description

Bu hizmet tüm önemli FileX veri yapılarını başlatıyor. Başka bir FileX ***hizmeti tx_application_define*** veya bir başlatma iş parçacığından çağrılmalı ve çağrılmalı.

> [!WARNING]
> *Bu çağrı tarafından başlatıldıktan sonra, doğru bir sistem tarihi ve saatiyle başlamak için ***uygulamanın fx_system_date_set** _ ve _ *fx_system_time_set** çağrısında olması gerekir.*

### <a name="input-parameters"></a>Giriş Parametreleri

Hiçbiri

### <a name="return-values"></a>Dönüş Değerleri

Yok.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_system_date_get
- fx_system_date_set
- fx_system_time_get
- fx_system_time_set

## <a name="fx_system_time_get"></a>fx_system_time_get

Geçerli sistem saati alır

### <a name="prototype"></a>Prototype

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a>Description

Bu hizmet geçerli sistem saatlerini almaktadır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **hour:** Hedefin saat işaretçisi.
- **minute:** Dakika için hedefin işaretçisi.
- **second:** saniye için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı sistem zamanı alma.
- **FX_PTR_ERROR** (0x18) Bir veya daha fazla giriş parametresi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_system_date_get
- fx_system_date_set
- fx_system_initialize
- fx_system_time_set

## <a name="fx_system_time_set"></a>fx_system_time_set

Geçerli sistem saatlerini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a>Description

Bu hizmet, geçerli sistem saatlerini giriş parametreleri tarafından belirtilen saat olarak ayarlar.

> [!WARNING]
> *Bu hizmet, ilk sistem fx_system_initialize **kısa** bir süre sonra çağrılacaktır. Varsayılan olarak sistem saati 0:0:0'dır.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **hour:** Yeni saat (0-23).
- **minute:** Yeni dakika (0-59).
- **second:** Yeni saniye (0-59).

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı sistem zamanı alma.
- **FX_INVALID_HOUR**    (0x15) Yeni saat geçersiz.
- **FX_INVALID_MINUTE** (0x16) Yeni dakika geçersiz.
- **FX_INVALID_SECOND** (0x17) Yeni saniye geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- fx_system_date_get
- fx_system_date_set
- fx_system_initialize
- fx_system_time_get

## <a name="fx_unicode_directory_create"></a>fx_unicode_directory_create

Unicode dizini oluşturur

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir alt dizin oluşturur; Unicode kaynak adı parametresinde yol bilgilerine izin verilmez. Başarılı olursa, yeni oluşturulan Unicode alt dizininin kısa adı (8.3 biçimi) hizmet tarafından döndürülür.

> [!WARNING]
> *Unicode alt dizininde (varsayılan yol, silme vb.) yapılan tüm işlemler, standart FileX dizin hizmetlerine döndürülen kısa ad (8.3 biçimi) ekilerek gerçekleştir gerekir.*

> [!IMPORTANT]
> *Bu hizmet exFAT medyası üzerinde desteklenmiyor.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **source_unicode_name:** Yeni alt dizin için Unicode adının işaretçisi.
- **source_unicode_length:** Unicode adının uzunluğu.
- **short_name:** Yeni Unicode alt dizini için kısa ad (8.3 biçimi) için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı Unicode dizini oluşturma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_ALREADY_CREATED** (0x0B) Belirtilen dizin zaten var.
- **FX_NO_MORE_SPACE** (0x0A) Yeni dizin girişi için medyada artık kullanılabilir küme yok.
- **FX_NOT_IMPLEMENTED** (0x22) Hizmeti exFAT dosya sistemi için uygulanmadı.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.
- **FX_PTR_ERROR** (0x18) Geçersiz medya veya ad işaretçileri.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.
- **FX_IO_ERROR (0x90)** Sürücü I/O hatası.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_rename

## <a name="fx_unicode_directory_rename"></a>fx_unicode_directory_rename

Unicode dizesini kullanarak dizini yeniden adlandırıyor

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a>Description

Bu hizmet, Unicode adlı alt dizini geçerli çalışma dizininde belirtilen yeni Unicode adıyla değiştirir. Unicode ad parametrelerinin yol bilgilerine sahip olması gerekir.

> [!IMPORTANT]
> *Bu hizmet exFAT medyası üzerinde desteklenmiyor.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr:** Medya denetim bloğuna işaretçi.
- **old_unicode_name:** Geçerli dosyanın Unicode adının işaretçisi.
- **old_unicode_name_length:** Geçerli Unicode adının uzunluğu.
- **new_unicode_name:** Yeni Unicode dosya adının işaretçisi.
- **old_unicode_name_length:** Yeni Unicode adının uzunluğu.
- **new_short_name:** Yeniden adlandırılan Unicode dosyası için kısa ad (8.3 biçimi) için hedefin işaretçisi. Dizini Unicode ile Yeniden Adlandırma

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) Başarılı medya açma.
- **FX_MEDIA_NOT_OPEN** (0x11) Belirtilen medya açık değil.
- **FX_ALREADY_CREATED** (0x0B) Belirtilen dizin adı zaten var.
- **FX_IO_ERROR** (0x90) Sürücü Ç hatası.
- **FX_PTR_ERROR** (0x18) Bir veya daha fazla işaretçi NULL olur.
- **FX_CALLER_ERROR** (0x20) Çağıran bir iş parçacığı değildir.
- **FX_WRITE_PROTECT** (0x23) Belirtilen medya yazma korumalıdır.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_directory_attributes_read
- fx_directory_attributes_set
- fx_directory_create
- fx_directory_default_get
- fx_directory_default_set
- fx_directory_delete
- fx_directory_first_entry_find
- fx_directory_first_full_entry_find
- fx_directory_information_get
- fx_directory_local_path_clear
- fx_directory_local_path_get
- fx_directory_local_path_restore
- fx_directory_local_path_set
- fx_directory_long_name_get
- fx_directory_name_test
- fx_directory_next_entry_find
- fx_directory_next_full_entry_find
- fx_directory_rename
- fx_directory_short_name_get
- fx_unicode_directory_create

## <a name="fx_unicode_file_create"></a>fx_unicode_file_create

Unicode dosyası oluşturur

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya oluşturur; Unicode kaynak adı parametresinde hiçbir yol bilgisine izin verilmez. Başarılı olursa, yeni oluşturulan Unicode dosyanın kısa adı (8,3 biçimi) hizmet tarafından döndürülür.

> [!WARNING]
> *Unicode dosyasındaki (açma, yazma, okuma, kapatma, vb.) tüm işlemler, standart FileX dosya hizmetlerine döndürülen kısa ad (8,3 biçimi) sağlanarak yapılmalıdır.*

### <a name="input-parameters"></a>Giriş Parametreleri


- **media_ptr**: medya denetim bloğu işaretçisi.
- **source_unicode_name**: yeni dosya için Unicode adı işaretçisi.
- **source_unicode_length**: Unicode adının uzunluğu.
- **short_name**: yeni Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı dosya oluştur.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_ALREADY_CREATED** (0x0B) belirtilen dosya zaten var.
- Yeni dosya girişi için medyada daha fazla küme yok **FX_NO_MORE_SPACE** (0x0A).
- **FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_file_rename"></a>fx_unicode_file_rename

Unicode dizesini kullanarak bir dosyayı yeniden adlandırır

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizinde Unicode adlı bir dosya adını belirtilen yeni Unicode adı olarak değiştirir. Unicode ad parametreleri yol bilgilerine sahip olmamalıdır.

> [!IMPORTANT]
> *Bu hizmet, exFAT ortamında desteklenmez.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.
- **old_unicode_name**: geçerli dosya için Unicode adı işaretçisi.
- **old_unicode_name_length**: geçerli Unicode adı uzunluğu.
- **new_unicode_name**: yeni Unicode dosya adı işaretçisi.
- **new_unicode_name_length**: yeni Unicode adı uzunluğu.
- **new_short_name**: yeniden adlandırılan Unicode dosyası için kısa ad (8,3 biçimi) hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri


- **FX_SUCCESS** (0x00) başarılı medya açıldı.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_ALREADY_CREATED** (0x0B) belirtilen dosya adı zaten var.
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_PTR_ERROR** (0x18) bir veya daha fazla işaretçi null.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.
- **FX_WRITE_PROTECT** (0x23) belirtilen medya yazma korumalı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_length_get"></a>fx_unicode_length_get

Unicode adının uzunluğunu alır

### <a name="prototype"></a>Prototype

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan Unicode adının uzunluğunu belirler. Bir Unicode karakteri iki bayt ile temsil eder. Unicode adı, iki NULL bayt (0 değeri iki bayt) tarafından sonlandırılan iki baytlık Unicode karakter dizisidir.

### <a name="input-parameters"></a>Giriş Parametreleri

**unicode_name:** Unicode adı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

**length:** Unicode adının uzunluğu (adda Unicode karakter sayısı).

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_length_get_extended"></a>fx_unicode_length_get_extended

Unicode adının uzunluğunu alır

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan Unicode adının uzunluğunu alır. Bir Unicode karakteri iki bayt ile temsil eder. Unicode adı, iki NULL bayt (0 değeri iki bayt) tarafından sonlandırılan iki baytlık Unicode karakter dizisidir.

> [!IMPORTANT]
> *Bu hizmet **fx_unicode_length_get()** ile aynıdır ancak çağıranın iki NULL karakter dahil olmak **üzere unicode_name** arabelleğinin boyutunu geçerse.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **unicode_name:** Unicode adı işaretçisi.
- **buffer_length:** Unicode ad arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

**length:** Unicode adının uzunluğu (adda Unicode karakter sayısı).

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get

## <a name="fx_unicode_name_get"></a>fx_unicode_name_get

Kısa adından Unicode adı alır

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez. Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.

> [!IMPORTANT]
> *Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.
- **short_name** Kısa ad işaretçisi (8,3 biçiminde).
- **destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.
- **destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı Unicode adı alma.
- **FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_short_name_get

## <a name="fx_unicode_name_get_extended"></a>fx_unicode_name_get_extended

Kısa adından Unicode adı alır

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizin içinde sağlanan kısa ad (8,3 biçimi) ile ilişkili Unicode adını alır; kısa ad parametresinde hiçbir yol bilgisine izin verilmez. Başarılı olursa, hizmet tarafından kısa adla ilişkili Unicode adı döndürülür.

> [!IMPORTANT]
> * Bu hizmet,_çağıran, hedef Unicode arabelleğinin bir giriş bağımsız değişkeni olarak boyutunu sağladığı sürece * fx_unicode_name_get aynıdır. Bu, hizmetin hedef Unicode arabelleğinin üzerine yazmayacağı garantisi sağlamasına izin verir_

> [!IMPORTANT]
> *Bu hizmet, hem dosya hem de alt dizinlerin Unicode adlarını almak için kullanılabilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.
- **short_name**: kısa ad işaretçisi (8,3 biçiminde).
- **destination_unicode_name**: sağlanan kısa adla ilişkili Unicode adı için hedef işaretçisi.
- **destination_unicode_length**: döndürülen Unicode ad uzunluğu işaretçisi.
- **unicode_name_buffer_length**: Unicode ad arabelleğinin boyutu. Note: bir NULL Sonlandırıcı gereklidir ve bu da ek bir bayt oluşturur.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı Unicode adı alma.
- **FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) kısa ad bulunamadı veya Unicode hedef boyutu çok küçük.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_short_name_get

## <a name="fx_unicode_short_name_get"></a>fx_unicode_short_name_get

Unicode adından kısa adı alır

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez. Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.

> [!IMPORTANT]
> *Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.
- **source_unicode_name**: Unicode adına işaretçi.
- **source_unicode_length**: Unicode adının uzunluğu.
- **destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi. Bu, en az 13 bayt boyutunda olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı kısa ad alma.
- **FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.
- **FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get

## <a name="fx_unicode_short_name_get_extended"></a>fx_unicode_short_name_get_extended

Unicode adından kısa adı alır

### <a name="prototype"></a>Prototype

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a>Description

Bu hizmet, geçerli varsayılan dizin içindeki UNICODE adı ile ilişkili kısa adı (8,3 biçimi) alır; Unicode ad parametresinde hiçbir yol bilgisine izin verilmez. Başarılı olursa, hizmet tarafından Unicode adıyla ilişkili kısa ad döndürülür.

> [!IMPORTANT]
> *Çağıran, hedef arabelleğin bir giriş bağımsız değişkeni olarak boyutunu sağladığı, bu hizmet **fx_unicode_short_name_get ()** ile aynıdır. Bu, hizmetin kısa adı hedef arabelleği aşmadığını garanti etmesine olanak tanır.*

*Bu hizmet, hem dosya hem de alt dizinlerin kısa adlarını almak için kullanılabilir*

### <a name="input-parameters"></a>Giriş Parametreleri

- **media_ptr**: medya denetim bloğu işaretçisi.
- **source_unicode_name**: Unicode adına işaretçi.
- **source_unicode_length**: Unicode adının uzunluğu.
- **destination_short_name**: kısa ad (8,3 biçimi) için hedef işaretçisi. Bu, en az 13 bayt boyutunda olmalıdır.
- **short_name_buffer_length**: hedef arabelleğin boyutu. Arabellek boyutu en az 14 bayt olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **FX_SUCCESS** (0x00) başarılı kısa ad alma.
- **FX_FAT_READ_ERROR** (0x03) FAT tablosu okunamıyor.
- **FX_FILE_CORRUPT** (0x08) dosyası bozuk
- **FX_IO_ERROR** (0x90) sürücü g/ç hatası.
- **FX_MEDIA_NOT_OPEN** (0x11) belirtilen medya açık değil.
- **FX_NOT_FOUND** (0x04) Unicode adı bulunamadı.
- **FX_NOT_IMPLEMENTED** (0x22) hizmeti exFAT dosya sistemi için uygulanmadı.
- **FX_SECTOR_INVALID** (0x89) geçersiz kesim.
- **FX_PTR_ERROR** (0x18) geçersiz medya veya ad işaretçileri.
- **FX_CALLER_ERROR** (0x20) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

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

### <a name="see-also"></a>Ayrıca Bkz.

- fx_file_allocate
- fx_file_attributes_read
- fx_file_attributes_set
- fx_file_best_effort_allocate
- fx_file_close
- fx_file_create
- fx_file_date_time_set
- fx_file_delete
- fx_file_extended_allocate
- fx_file_extended_best_effort_allocate
- fx_file_extended_relative_seek
- fx_file_extended_seek
- fx_file_extended_truncate
- fx_file_extended_truncate_release
- fx_file_open
- fx_file_read
- fx_file_relative_seek
- fx_file_rename
- fx_file_seek
- fx_file_truncate
- fx_file_truncate_release
- fx_file_write
- fx_file_write_notify_set
- fx_unicode_file_create
- fx_unicode_file_rename
- fx_unicode_name_get
- fx_unicode_short_name_get
