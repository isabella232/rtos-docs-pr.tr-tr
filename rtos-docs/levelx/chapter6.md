---
title: Bölüm 6 - Azure RTOS LevelX NOR API'leri
description: Uygulama Azure RTOS LevelX VEYA API'leri kullanılabilir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2e109f5916a9e903aa3341f2855ade085e9d9a22b80ec7cb2e0c310e43ff3eac
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790250"
---
# <a name="chapter-6---azure-rtos-levelx-nor-apis"></a>Bölüm 6 - Azure RTOS LevelX NOR API'leri

Uygulama Azure RTOS için kullanılabilir olan levelX NOR API işlevleri aşağıdaki gibidir.

- ***lx_nor_flash_close** _: _Close NOR flash örneği*
- ***lx_nor_flash_defragment** _: _Defragment NOR flash örneği*
- ***lx_nor_flash_extended_cache_enable** _: genişletilmiş NOR _Enable/devre dışı bırakma*
- ***lx_nor_flash_initialize** _: _Initialize NOR flash desteği*
- ***lx_nor_flash_open** _: _Open NOR flash örneği*
- ***lx_nor_flash_partial_defragment** _: _Partial VEYA flash örneğinin birleştiricisi*
- ***lx_nor_flash_sector_read** _: _Read NOR flash sektör*
- ***lx_nor_flash_sector_release** _: _Release NOR flash sektör*
- ***lx_nor_flash_sector_write** _: _Write NOR flash sektör*

## <a name="lx_nor_flash_close"></a>lx_nor_flash_close

NOR flash örneğini kapatma

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_close(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a>Description

Bu hizmet, önceden açılmış OLAN NOR flash örneğini kapatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- *nor_flash:* NOR flash örnek işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS:**(0x00) Başarılı istek.
- **LX_ERROR:**(0x01) Flash örneği kapatılıyor hatası.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Close NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_close(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_defragment"></a>lx_nor_flash_defragment

Birleştirme NOR flash örneği

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_defragment(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a>Description

Bu hizmet, daha önce açılan NOR flash örneğini birleştirmektedir. Birleştirme işlemi, serbest kesim ve blok sayısını en üst düzeye çıkartır.

### <a name="input-parameters"></a>Giriş Parametreleri

- *nor_flash:* NOR flash örnek işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS:**(0x00) Başarılı istek.
- **LX_ERROR:**(0x01) Flash örneği birleştirme hatası.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Defragment NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_defragment(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_extended_cache_enable"></a>lx_nor_flash_extended_cache_enable

Genişletilmiş NOR önbelleğini etkinleştirme/devre dışı bırakma

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_extended_cache_enable(
    LX_NOR_FLASH *nor_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a>Description

Bu hizmet, uygulama tarafından sağlanan belleği kullanarak RAM'de bir NOR kesim önbellek katmanı kullanır. Sağlanan her 512 bayt bellek, önbelleğe alınacak bir NOR kesimine çevrilir. Önbelleğe alınan kesimler; silme sayısı, serbest kesim eşlemesi ve kesim eşleme bilgileri gibi blok denetimi bilgilerini içeren kesimlerdir. Veri kesimleri bu önbellekte depolanmaz.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nor_flash:** NOR flash örnek işaretçisi.  
- **memory:** ULONG erişimi için hizalanmış önbellek belleğinin başlangıç adresi. LX_NULL değeri önbelleği devre dışı bırakıyor.  
- **boyut:** Sağlanan belleğin bayt cinsinden boyutu (512 bayt'ın katları olmalıdır).

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS:**(0x00) Başarılı istek.
- **LX_ERROR:**(0x01) Bir NOR kesimi için yeterli bellek yok.
- **LX_DISABLED:**(0x09) VEYA genişletilmiş önbellek yapılandırma seçeneği tarafından devre dışı bırakılır.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Enable the NOR flash cache for the instance "my_nor_flash". */  
status = lx_nor_flash_extended_cache_enable(&my_nor_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_initialize"></a>lx_nor_flash_initialize

NOR flash desteği başlatma

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_initialize(void);
```

### <a name="description"></a>Description

Bu hizmet LevelX NOR flash desteğini başlatıyor. Başka bir LevelX VEYA API'den önce çağrılmalı.

### <a name="input-parameters"></a>Giriş Parametreleri

- **Hiçbiri**

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS:**(0x00) Başarılı istek.
- **LX_ERROR:**(0x01) NOR flash desteği başlatma hatası.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Initialize NOR flash support. */  
status = lx_nor_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_partial_defragment
- lx_nor_flash_open
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_open"></a>lx_nor_flash_open

Açık veya Flash örneği

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_open(
    LX_NOR_FLASH *nor_flash, 
    CHAR *name,  
    UINT (*nor_driver_initialize) (LX_NOR_FLASH *));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen veya Flash denetim bloğu ve sürücü başlatma işlevi ile bir veya Flash örneği açar. Sürücü başlatma işlevinin, bu veya Flash örneğiyle ilişkili veya donanımı okuma, yazma ve silme blokları için çeşitli işlev işaretçileri yüklememesinden sorumlu olduğunu unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- *nor_flash*: veya Flash örnek işaretçisi.
- *ad*: veya Flash örneğinin adı.
- *nor_driver_initialize*: Işlev işaretçisi veya Flash sürücü başlatma işlevi. VEYA Flash sürücü sorumlulukları hakkında daha fazla bilgi için lütfen bu kılavuzun Bölüm 5 ' e bakın.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) veya Flash örneği açılırken hata oluştu.
- **LX_NO_MEMORY**: (0x08) sürücü, None kesimini RAM 'e okumak için arabellek sağlamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Open NOR flash instance "my_nor_flash" with the driver "my_nor_driver_initialize". */  
status = lx_nor_flash_open(&my_nor_flash,"my NOR flash",  
    my_nor_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_partial_defragment"></a>lx_nor_flash_partial_defragment

VEYA Flash örneğinin kısmi birleştirmesi

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_partial_defragment(
    LX_NOR_FLASH *nor_flash, 
    UINT max_blocks);
```

### <a name="description"></a>Description

Bu hizmet, önceden açılmış veya Flash örneğini belirtilen en fazla blok sayısına kadar birleştirir. Birleştirme işlemi, boş kesimlerin ve blokların sayısını en üst düzeye çıkarır.

### <a name="input-parameters"></a>Giriş Parametreleri

- *nor_flash*: veya Flash örnek işaretçisi.
- *max_blocks*: en fazla blok sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) Flash örneği birleştirme hatası.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Defragment of one block in NOR flash instance* *"my_nor_flash". */  
status = lx_nor_flash_partial_defragment(&my_nor_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_sector_read"></a>lx_nor_flash_sector_read

Okuma veya Flash sektörü

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_sector_read(
    LX_NOR_FLASH *nor_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Description

Bu hizmet, mantıksal kesimi veya Flash örneğinden okur ve başarılı olursa sağlanan arabellekteki içeriği döndürür. Bu ve sektör boyutunun her zaman 512 bayt olduğunu unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- *nor_flash* VEYA Flash örnek işaretçisi.
- *logical_sector*: okunacak mantıksal kesim.
- *buffer*: mantıksal sektörün içerikleri için hedef işaretçisi. Arabelleğin 512 bayt olduğunu ve ULONG erişimi için hizalandığını unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) veya Flash kesimini okuma hatası.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Read logical sector 20 of the NOR flash instance "my_nor_flash" and place contents in "buffer". */ 
status = lx_nor_flash_sector_read(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contents of logical sector 20. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_release
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_sector_release"></a>lx_nor_flash_sector_release

Yayın veya Flash sektörü

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_sector_release(
    LX_NOR_FLASH *nor_flash,
    ULONG logical_sector);
```

### <a name="description"></a>Description

Bu hizmet, veya Flash örneğindeki mantıksal kesim eşlemesini yayınlar. Kullanılmayan bir mantıksal kesimi serbest bırakmak, LevelX aşumu seviyelendirmenin daha verimli olmasını sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- *nor_flash*: veya Flash örnek işaretçisi.
- *logical_sector*: serbest bırakmak için mantıksal kesim.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) hata veya Flash kesim yazma.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Release logical sector 20 of the NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_sector_release(&my_nor_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_write

## <a name="lx_nor_flash_sector_write"></a>lx_nor_flash_sector_write

YAZMA NOR flash sektör

### <a name="prototype"></a>Prototype

```c
UINT lx_nor_flash_sector_write(
    LX_nor_FLASH *NOR_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Description

Bu hizmet, NOR flash örneğinde belirtilen mantıksal kesimi yazar.

### <a name="input-parameters"></a>Giriş Parametreleri

- *nor_flash:* NOR flash örnek işaretçisi.
- *logical_sector:* Yazacak mantıksal kesim.
- *buffer:* Mantıksal kesimin içeriklerinin işaretçisi. Arabelleğin ULONG erişimi için hizalanmış 512 bayt olduğu varsayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS:**(0x00) Başarılı istek.
- **LX_NO_SECTORS:**(0x02) Yazma işlemini gerçekleştirmek için artık ücretsiz kesim yok.
- **LX_ERROR:**(0x01) NOR flash kesimini serbest bırakma hatası.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Write logical sector 20 of the NOR flash instance "my_nor_flash" with the contents pointed to by "buffer". */ 
status = lx_nor_flash_sector_write(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nor_flash_close
- lx_nor_flash_defragment
- lx_nor_flash_extended_cache_enable
- lx_nor_flash_initialize
- lx_nor_flash_open
- lx_nor_flash_partial_defragment
- lx_nor_flash_sector_read
- lx_nor_flash_sector_release
