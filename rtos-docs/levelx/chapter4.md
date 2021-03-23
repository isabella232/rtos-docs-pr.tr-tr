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
# <a name="chapter-4---azure-rtos-levelx-nand-apis"></a>Bölüm 4-Azure RTOS LevelX nve API 'Leri

Uygulamanın kullanabildiği Azure RTOS LevelX nve API 'Leri şunlardır:

- ***lx_nand_flash_close** _: _CLOSE nve Flash örneği *
- ***lx_nand_flash_defragment** _: _Defragment nve Flash örneği *
- ***lx_nand_flash_extended_cache_enable** _: _Enable/GENIŞLETILMIŞ nve önbelleğini devre dışı bırak *
- ***lx_nand_flash_initialize** _: _Initialize nve Flash desteği *
- ***lx_nand_flash_open** _: _OPEN nve Flash örneği *
- ***lx_nand_flash_page_ecc_check** _: düzeltme ile ECC hataları için _Check sayfası
- ***lx_nand_flash_page_ecc_compute** _: sayfa * IÇIN _Computes ECC
- ***lx_nand_flash_partial_defragment** _: nve flash örneğinin _Partial birleştirme *
- ***lx_nand_flash_sector_read** _: _read nve Flash sektörü *
- ***lx_nand_flash_sector_release** _: _Release nve Flash sektörü *
- ***lx_nand_flash_sector_write** _: _WRITE nve Flash sektörü *

## <a name="lx_nand_flash_close"></a>lx_nand_flash_close

NVE Flash örneğini kapat

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_close(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce açılmış nve Flash örneğini kapatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) Flash örneği kapatılırken hata oluştu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Close NAND flash instance "my_nand_flash". */
status = lx_nand_flash_close(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_defragment"></a>lx_nand_flash_defragment

NVE Flash örneğini birleştirin

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_defragment(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce açılan nve Flash örneğini birleştirir. Birleştirme işlemi, serbest sayfa ve blok sayısını en üst düzeye çıkarır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) Flash örneği birleştirme hatası.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Defragment NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_defragment(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_extended_cache_enable"></a>lx_nand_flash_extended_cache_enable

Genişletilmiş nve önbelleği etkinleştir/devre dışı bırak

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_extended_cache_enable(
    LX_NAND_FLASH
    *nand_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulama tarafından sağlanan belleği kullanarak RAM 'de bir önbellek katmanı uygular. Tam önbellek işlemi için gereken toplam bellek miktarı şu şekilde hesaplanabilir:

```c
size (in_bytes) = number_of_blocks (rounded up to be divisible by 4) +  
    ((number_of_blocks * pages_per_block) * 4)  +  
    ((number_of_blocks * (pages_per_block + 1)) * 4)
```

Sağlanan bellek tam nve önbelleğe uyum sağlayacak kadar büyük değilse, bu yordam sağlanan belleğe göre nve Flash önbelleğinin büyük bir kısmını mümkün olduğunca etkinleştirecektir.

Belirtilen bellek adresi NULL ise nve önbelleği devre dışıdır. Bu nedenle, nve önbelleği geçici bir biçimde kullanılıyor olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.  
- **bellek**: ulong erişimi için hizalanmış önbellek belleği için başlangıç adresi. LX_NULL değeri önbelleği devre dışı bırakır.  
- **Boyut**: sağlanan belleğin bayt cinsinden boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) nve önbelleğinin bir öğesi için yeterli bellek yok.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Enable the NAND flash cache for the instance "my_nand_flash". */
status = lx_nand_flash_extended_cache_enable(&my_nand_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_initialize"></a>lx_nand_flash_initialize

NVE Flash desteğini başlatma

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_initialize(void);
```

### <a name="description"></a>Açıklama

Bu hizmet, LevelX nve Flash desteğini başlatır. Diğer bir LevelX nve API 'lerden önce çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **Hiçbiri**

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) nve Flash desteği başlatılırken hata oluştu.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Initialize NAND flash support. */
status = lx_nand_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_open"></a>lx_nand_flash_open

NVE Flash örneğini aç

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_open(
    LX_NAND_FLASH *nand_flash, 
    CHAR *name,  
    UINT (*nand_driver_initialize) (LX_NAND_FLASH *));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen nve Flash denetim bloğu ve sürücü başlatma işlevi ile bir nve Flash örneği açar. Sürücü başlatma işlevinin, bu nve Flash örneğiyle ilişkili nve donanımının blok/sayfalarını okuma, yazma ve silme işlemleri için çeşitli işlev işaretçileri yüklememesinden sorumlu olduğunu unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.
- **ad**: nve Flash örneğinin adı.
- **nand_driver_initialize**: nve Flash sürücü başlatma işlevine işlev işaretçisi. NVE Flash sürücü sorumlulukları hakkında daha fazla bilgi için lütfen bu kılavuzun Bölüm 3 ' e başvurun.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) nve Flash örneği açılırken hata oluştu.
- **LX_NO_MEMORY**: (0x08) sürücü, BIR sayfayı RAM 'e okumak için arabellek sağlamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Open NAND flash instance "my_nand_flash" with the driver "my_nand_driver_initialize". */ 
status = lx_nand_flash_open(&my_nand_flash,"my nand flash",  
    my_nand_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_page_ecc_check"></a>lx_nand_flash_page_ecc_check

Düzeltme ile ECC hataları için sayfayı denetle

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_page_ecc_check(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a>Açıklama

Bu hizmet sağlanan ECC ile sağlanan nve sayfa arabelleğinin bütünlüğünü doğrular. Sayfa boyutu (nve Flash örneği İşaretçisinde tanımlanmıştır), 256 baytlık bir katı kabul edilir ve sağlanan ECC kodu, sayfanın her 256-Byte bölümünde 1 bit hatası düzeltiyor olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.
- **page_buffer**: nve Flash sayfa arabelleğinin işaretçisi.
- **ecc_buffer**: nve Flash SAYFASıNA yönelik ECC işaretçisi. Sayfanın 256 baytlık bölümü başına 3 ECC bayt olduğunu unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) nve sayfasında hata yok.
- **LX_NAND_ERROR_CORRECTED**: (0x06) nve sayfasında 1 bitlik bir hata düzeltildi — düzeltmeler sayfa arabelleğinde.
- **LX_NAND_ERROR_NOT_CORRECTED**: (0x07) nve sayfasında düzeltmeniz için çok fazla hata var.

### <a name="allowed-from"></a>İzin verilen

LevelX sürücüsü

### <a name="example"></a>Örnek

```c
/* Check the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash" . */
status = lx_nand_flash_page_ecc_check(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the page is valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_page_ecc_compute"></a>lx_nand_flash_page_ecc_compute

Sayfa için işlem ECC

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_page_ecc_compute(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan nve sayfa arabelleğinin ECC 'sini hesaplar ve sağlanan ECC arabelleğindeki ECC 'yi döndürür. Sayfa boyutu, 256 baytlık bir (nve Flash örnek İşaretçisinde tanımlanan) bir katı kabul edilir. ECC kodu, sayfanın daha sonra okunışında bütünlüğünü doğrulamak için kullanılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.
- **page_buffer**: nve Flash sayfa arabelleğinin işaretçisi.
- **ecc_buffer**: nve Flash sayfasının ECC 'si için hedef işaretçisi. Sayfanın 256 baytlık bölümü başına 3 bayt ECC depolaması olması gerektiğini unutmayın. Örneğin, 2048 baytlık bir sayfa ECC için 24 bayt gerektirir.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) ECC başarıyla hesaplandı.
- **LX_ERROR**: (0x01) ECC hesaplama hatası.

### <a name="allowed-from"></a>İzin verilen

LevelX sürücüsü

### <a name="example"></a>Örnek

```c
/* Compute ECC for the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_page_ecc_compute(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the ECC was calculated and Can be found in the memory pointed to by "ecc_pointer." */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_partial_defragment"></a>lx_nand_flash_partial_defragment

NVE Flash örneğinin kısmi birleştirmesi

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_partial_defragment(
    LX_NAND_FLASH *nand_flash,  
    UINT max_blocks);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden açılan nve Flash örneğini belirtilen en fazla blok sayısına kadar birleştirir. Birleştirme işlemi, serbest sayfa ve blok sayısını en üst düzeye çıkarır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.
- **max_blocks**: en fazla blok sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) Flash örneği birleştirme hatası.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Defragment 1 block of NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_partial_defragment(&my_nand_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_sector_read"></a>lx_nand_flash_sector_read

NVE Flash kesimini oku

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_sector_read(
    LX_NAND_FLASH *nand_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Açıklama

Bu hizmet, nve Flash örneğinden mantıksal kesimi okur ve başarılı olursa, sağlanan arabellekteki içerik döndürülür. NVE sektör boyutunun her zaman temeldeki nve donanımın sayfa boyutu olduğunu unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.
- **logical_sector**: okunacak mantıksal kesim.
- **buffer**: mantıksal sektörün içerikleri için hedef işaretçisi. Arabelleğin nve Flash sayfa boyutunun boyutu olduğunu ve ULONG erişimi için hizalandığını unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) nve Flash sektörü okunurken hata oluştu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Read logical sector 20 of the NAND flash instance "my_nand_flash" and place contents in "buffer". */
status = lx_nand_flash_sector_read(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contentsnof logical sector 20. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_release
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_sector_release"></a>lx_nand_flash_sector_release

Yayın nve Flash sektörü

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_sector_release(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector);
```

### <a name="description"></a>Açıklama

Bu hizmet, nve Flash örneğindeki mantıksal kesim eşlemesini yayınlar. Kullanılmayan bir mantıksal kesimi serbest bırakmak, LevelX aşumu seviyelendirmenin daha verimli olmasını sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.
- **logical_sector**: serbest bırakmak için mantıksal kesim.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_ERROR**: (0x01) hata nve Flash sektör yazma.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Release logical sector 20 of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_sector_release(&my_nand_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_write

## <a name="lx_nand_flash_sector_write"></a>lx_nand_flash_sector_write

NVE Flash kesimini yaz

### <a name="prototype"></a>Prototype

```c
UINT lx_nand_flash_sector_write(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a>Açıklama

Bu hizmet, nve Flash örneğinde belirtilen mantıksal kesimi yazar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nand_flash**: nve Flash örnek işaretçisi.
- **logical_sector**: yazılacak mantıksal kesim.
- **buffer**: mantıksal sektörün içeriğine yönelik işaretçi. Arabelleğin nve Flash sayfa boyutunun boyutu olduğunu ve ULONG erişimi için hizalandığını unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **LX_SUCCESS**: (0x00) başarılı istek.
- **LX_NO_SECTORS**: (0x02) yazma işlemini gerçekleştirmek için kullanılabilir daha fazla boş sektör yok.
- **LX_ERROR**: (0x01) nve Flash kesimini serbest bırakma hatası.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Write logical sector 20 of the NAND flash instance "my_nand_flash" with the contents pointed to by "buffer". */  
status = lx_nand_flash_sector_write(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- lx_nand_flash_close
- lx_nand_flash_defragment
- lx_nand_flash_extended_cache_enable
- lx_nand_flash_initialize
- lx_nand_flash_open
- lx_nand_flash_page_ecc_check
- lx_nand_flash_page_ecc_compute
- lx_nand_flash_partial_defragment
- lx_nand_flash_sector_read
- lx_nand_flash_sector_release
