---
title: Bölüm 5-Azure RTOS LevelX veya desteği
description: Flash belleği, genellikle 512 bayta eşit olarak bölünebilen bloklardan oluşur. Azure RTOS LevelX, her bir veya Flash bloğunu 512 baytlık mantıksal sektörlere böler.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3a0c73c2b45c32bf3f1ef56de684fa83c334b59e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826260"
---
# <a name="chapter-5---azure-rtos-levelx-nor-support"></a>Bölüm 5-Azure RTOS LevelX veya desteği

Flash belleği, genellikle 512 bayta eşit olarak bölünebilen *bloklardan* oluşur. Flash *Page* 'de veya Flash bellekte bir kavram yoktur. Ayrıca, veya Flash bellekte *yedek* bayt yoktur, bu nedenle Azure RTOS levelx 'in tüm yönetim BILGILERI için veya flash belleğini kullanması gerekir. Doğrudan okuma erişimi, veya Flash bellekte mümkündür. Yazma erişimi genellikle özel bir işlem dizisi gerektirir. VEYA Flash belleği birden çok kez yazılabilir, bu da bitleri temizlenemekte olabilir. VEYA Flash belleğindeki bitler, silme bloğu işlemi aracılığıyla yalnızca bir kez ayarlanabilir.

LevelX her bir veya Flash bloğunu 512 baytlık mantıksal *kesimlere* böler. Ayrıca, LevelX, yönetim bilgilerini depolamak için her bir veya Flash bloğunun ilk "n" sektörlerini kullanır. LevelX veya Flash bellek yönetimi bilgilerinin biçimi:

**LevelX veya Block biçimi**

| Bayt kayması  | İçindekiler                     |
| ------------ | ---------------------------- |
| 0            | [Blok silme sayısı]          |
| 4            | [En az eşlenmiş kesim]      |
| 8            | [Eşlenen en fazla kesim]      |
| 12           | [Serbest sektör bit eşlemesi]        |
| m            | [Sektör 0 eşleme girişi]     |
|              | …                            |
| a + 4 * (n-1)    | [Kesim "n" eşleme girişi]   |
|              | …                            |
| s            | [Kesim 0 Içeriği]          |
|              | …                            |
| s + 512 * (n-1) | [Kesim "n" Içerik]         |

32 bitlik *blok silme sayısı* , bloğun kaç kez silinme sayısını içerir. LevelX 'in ana amacı, herhangi bir bloğun erken bir şekilde erişmesini önlemeye yardımcı olmak için tüm blokların silme sayısını görece şekilde kapatmaktır. 32 bitlik *en az eşlenmiş kesim* ve *en fazla eşlenen sektör* alanları yalnızca bloktaki tüm mantıksal kesimlerin eşlendiği ve üzerine yazıldığı durumlarda yazılır. Bu alanlar, kesim okuma işleminin iyileştirilmesi için faydalıdır. *Serbest sektör bit eşleme* girişi, her küme bitinin bloktaki eşlenmemiş kesime karşılık geldiği bir bit haritadır. Bu alan, serbest sektör aramasını daha verimli hale getirmek için kullanılır. Bu, bloktaki her 32 kesim için bir sözcük gerektiren değişken uzunluklu bir alandır. *Kesim eşleme giriş* dizisi, bloktaki her bir kesime ait eşleme bilgilerini içerir. Her giriş aşağıdaki biçimdedir:

**Kesim eşleme girişi**

| Bit (lar) | Anlamı  |
| ------ | -------- |
| 31     | Geçerli bayrak. Küme ve mantıksal kesim hiçbir zaman eşleme, eşlemenin geçerli olduğunu belirtir |
| 30     | Kullanım dışı bayrağı. Bu eşleme açık olmadığında veya artık kullanılmıyor olma sürecinde. |
| 29     | Bu bit 0 olduğunda eşleme girişi yazma işlemi tamamlanır |
| 0-28   | Bu fiziksel kesime eşlenmiş mantıksal kesim (hepsi değil). |

32 bitlik alanın (bit 31) üst biti, mantıksal kesim eşlemesinin geçerli olduğunu göstermek için kullanılır. Bu bit 0 ise, bu girişteki bilgiler (ve buna karşılık gelen sektör içeriği) artık geçerli değildir. Sonraki bit bit 30-bu sektörün kullanılmıyor olma sürecinde olduğunu ve yeni bir kesimin yazılmakta olduğunu göstermek için kullanılır. Eşleme girişi yazma işleminin tamamlandığını göstermek için bit 29 kullanılır. Bit 29 0 ise, eşleme girişi yazma tamamlanmıştır. Bit 29 ayarlanmışsa, eşleme girişi yazma süreciydi. BITS 30 ve 29, yeni bir sektör eşlemesini güncelleştirirken olası bir güç kaybından kurtarmak için kullanılır. Son olarak, alt 29-bit (28-0), sektör için mantıksal kesim numarasını içerir. Bir sektör eşlenmişse, tüm bitler ayarlanır, yani, 0xFFFFFFFF değerine sahip olur.

## <a name="nor-driver-requirements"></a>VEYA sürücü gereksinimleri

LevelX, temel Flash bölümü ve donanım uygulamasına özel bir temel veya Flash sürücü gerektirir. Sürücü, API ***lx_nor_flash_open*** aracılığıyla başlatma sırasında levelx olarak belirtilir. LevelX sürücüsünün prototipi:

```c
INT nor_driver_initialize(LX_NOR_FLASH *instance);
```

"*Örnek*" parametresi, levelx veya denetim bloğunu belirtir. Sürücü başlatma işlevi, ilişkili LevelX örneği için diğer tüm sürücü düzeyi Hizmetleri ayarlamaktan sorumludur. Her bir LevelX veya örnek için gereken hizmetler şunlardır:

- Kesimi oku
- Yazma kesimi
- Blok silme
- Blok silinme doğrulaması
- Sistem hata Işleyicisi

## <a name="driver-initialization"></a>Sürücü başlatma

Bu hizmetler, sürücünün başlatma işlevindeki **LX_NOR_FLASH** örneğindeki işlev işaretçileri ayarlanarak kurulumlardır. Sürücü başlatma işlevi de şu şekilde sorumludur:

1. Flaşın temel adresini belirtme.
1. Toplam blok sayısını ve blok başına sözcük sayısını belirtme.
1. Bir Flash kesimini okumak için bir RAM arabelleği (512 bayt) ve ULONG erişimi için hizalanır.

Sürücü başlatma işlevi büyük olasılıkla **LX_SUCCESS** döndürmeden önce ek cihaz ve/veya uygulamaya özgü başlatma görevlerini de gerçekleştiriyor.

## <a name="driver-read-sector"></a>Sürücü okuma kesimi

LevelX ve sürücü "Read sektör" hizmeti, veya Flash 'un belirli bir bloğundaki belirli bir kesimi okumaktan sorumludur. Mantığın tüm hata denetlemesi ve düzeltilmesi, sürücü hizmetinin sorumluluğundadır. Başarılı olursa, LevelX ve sürücü **LX_SUCCESS** döndürür. Başarılı olmazsa, LevelX ve sürücü *LX_ERROR* döndürür. LevelX ve sürücü "Read sektör" hizmetinin prototipi şunlardır:

```c
INT nor_driver_read_sector(
    ULONG *flash_address,
    ULONG *destination, 
    ULONG words);
```

Burada "*flash_address*", bir veya Flash bellek bloğu ve "*hedef*" ve "*sözcük*" içindeki mantıksal bir kesimin adresini belirtir, kesim içeriğinin nereye yerleştirileceğini ve kaç 32 bit kelime okuyabileceğiniz belirtilir.

## <a name="driver-write-sector"></a>Sürücü yazma kesimi

LevelX ve sürücü "yazma kesimi" hizmeti, belirli bir sektörün bir veya Flash bloğuna yazılmasından sorumludur. Tüm hata denetimi, sürücü hizmetinin sorumluluğundadır. Başarılı olursa, LevelX ve sürücü **LX_SUCCESS** döndürür. Başarılı olmazsa, LevelX ve sürücü **LX_ERROR** döndürür. LevelX ve sürücü "yazma kesimi" hizmeti prototipi şunlardır:

```c
INT nor_driver_write_sector(
    ULONG *flash_address,
    ULONG *source, 
    ULONG words);
```

Burada "*flash_address*", bir veya Flash bellek bloğunda ve "*kaynak*" ve "*kelimeler*", yazma kaynağını ve kaç 32 bitlik sözcüğün yazılacağını belirten bir mantıksal kesim adresini belirtir.

> [!NOTE]
> LevelX, yazma kesiminin başarılı olduğunu doğrulamak için sürücüyü kullanır. Bu, genellikle programlanmış değeri okunarak, istenen değerin yazılmasına izin verildiğinden yapılır.

## <a name="driver-block-erase"></a>Sürücü bloğunu silme

LevelX ve sürücü "blok silme" hizmeti, belirtilen veya Flash bloğunu silmekten sorumludur. Başarılı olursa, LevelX ve sürücü **LX_SUCCESS** döndürür. Başarılı olmazsa, LevelX ve sürücü **LX_ERROR** döndürür. LevelX ve sürücü "blok silme" hizmetinin prototipi:

```c
INT nor_driver_block_erase(ULONG block,  
    ULONG erase_count);
```

Burada "*Block*" ne olduğunu veya silmeyi engellemeyi belirler. "*Erase_count*" parametresi, tanılama amacıyla sağlanır. Örneğin, sürücü, silme sayısı belirli bir eşiği aştığında, uygulama yazılımının başka bir bölümüne uyarı vermek isteyebilir.

> [!NOTE]
> LevelX, silindiklerinden emin olmak için bloğun tüm baytlarını incelemek üzere sürücüyü kullanır (tümünü içerir).

## <a name="driver-block-erased-verify"></a>Sürücü bloğunu silinen doğrulama

LevelX veya sürücünün "blok silinmi Verify" hizmeti, belirtilen veya Flash bloğunun silineceğini doğrulamadan sorumludur. Silinirse, LevelX ve sürücü **LX_SUCCESS** döndürür. Blok silinmeyen, LevelX ve sürücü **LX_ERROR** döndürür. LevelX ve sürücü "blok silinenler" hizmetinin prototipi:

```c
INT nor_driver_block_erased_verify(ULONG block);
```

Burada "*Engelle*", hangi bloğun silindiğini doğrulayabildiğini belirtir.

> [!NOTE]
> LevelX, silindiklerinden emin olmak için belirtilen tüm baytları incelemek için sürücüyü kullanır (tümünü içerir).

## <a name="driver-system-error"></a>Sürücü sistemi hatası

Levelx ve sürücü "sistem hatası işleyicisi" hizmeti, LevelX tarafından algılanan sistem hatalarının işlenmesini ayarlamaktan sorumludur. Bu yordamın işleme uygulamaya bağımlıdır. Başarılı olursa, LevelX ve sürücü **LX_SUCCESS** döndürür. Başarılı olmazsa, LevelX ve sürücü **LX_ERROR** döndürür. LevelX ve sürücü "sistem hatası" hizmetinin prototipi:

```c
INT nor_driver_system_error(UINT error_code);
```

Burada "*error_code*" oluşan hatayı temsil eder.

## <a name="nor-simulated-driver"></a>VEYA sanal sürücü

LevelX, veya Flash bölümü işleminin benzetimini yapmak için yalnızca RAM kullanan bir benzetimli veya Flash sürücü sağlar. Varsayılan olarak, veya sanal sürücü blok başına 16 512 baytlık sektörle 8 veya Flash blokları sağlar.

Benzetimli veya Flash sürücü başlatma işlevi, ***lx_nor_flash_simulator_initialize** _ ve _ *_lx_nor_flash_simulator. c_* * içinde tanımlanmıştır. Bu sürücü Ayrıca, belirli veya Flash sürücüleri yazmak için iyi bir şablon sağlar.

## <a name="nor-filex-integration"></a>VEYA FileX tümleştirmesi

Daha önce belirtildiği gibi, LevelX işlem için FileX 'i kullanmaz. Tüm LevelX API 'Leri, ham verileri, LevelX tarafından sunulan mantıksal sektörlerde depolamak/almak için doğrudan uygulama yazılımı tarafından çağrılabilir. Ancak, LevelX de Fılex 'i destekler.

***Fx_nor_flash_simulated_driver. c*** dosyası, veya flash simülasyonu ile kullanılmak üzere bir örnek FileX sürücüsü içerir. LevelX için Flash FileX sürücüsü, özel FileX sürücüleri yazmak için iyi bir başlangıç noktası sağlar.

> [!NOTE]
> FileX veya Flash biçimi, veya Flash tarafından sağlanan kesimlerin bir tam blok boyutu olmalıdır. Bu, aşınma düzeyi işleme sırasında en iyi performansı sağlamaya yardımcı olur. LevelX aşmalar seviyelendirme algoritmasındaki yazma performansını artırmaya yönelik ek teknikler şunlardır:
> 1. Tüm yazmamaların tam olarak bir veya daha fazla küme olduğundan emin olun ve tam küme sınırları üzerinde başlatın.
> 2. API 'lerin FileX ***fx_file_allocate*** sınıfı aracılığıyla büyük dosya yazma işlemleri gerçekleştirmeden önce kümeleri önceden ayırın.
> 3.  ***Lx_nor_flash_defragment*** düzenli olarak kullanımı mümkün olduğunca çok sayıda ve blok ve bu sayede yazma performansını geliştirir.
> 4. FileX sürücüsünün yayın sektörü bilgilerini alacak şekilde etkinleştirildiğinden emin olun ve sürücü sürüm sektörlerine yapılan istekler ***lx_nor_flash_sector_release*** çağırarak sürücüde işlenir.
