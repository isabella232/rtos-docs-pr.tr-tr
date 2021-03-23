---
title: Azure RTOS LevelX nve desteği
description: NVE Flash belleği, genellikle dosya sistemlerinin tipik bir örneği olan büyük veri depolama için LevelX içinde kullanılır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3286e4ea7f16b28ff55fc95a87a1e0c313ec4240
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826267"
---
# <a name="chapter-3---azure-rtos-levelx-nand-support"></a>Bölüm 3-Azure RTOS LevelX nve desteği

NVE Flash belleği genellikle dosya sistemlerinin tipik bir örneği olan büyük veri depolama için kullanılır. NVE belleği *bloklardan* oluşur. Her nve bloğunun içinde bir dizi *sayfa*. NAND blokları silinebilir, yani nve bloğu içindeki tüm sayfalar silinir (tümüne ayarlanır). Her nve blok sayfasında, Azure RTOS LevelX tarafından muhasebe, bozuk blok yönetimi ve hata algılama için kullanılan bir dizi *yedek bayt* bulunur. NVE blok sayfaları çeşitli boyutlarda kullanılabilir. En yaygın sayfa boyutları şunlardır: 

| **Sayfa boyutu** | **Yedek baytlar** |
| ------------- | --------------- |
| 256           | 8               |
| 512           | 16              |
| 2048          | 64              |

NVE belleği, doğrudan erişim bulunmadığından veya bellekten farklıdır; Örneğin, nve bellek, doğrudan işlemciden veya bellekten bellek gibi okunamaz. NVE belleği yalnızca, sınırlı sayıda silme işleminden sonra yazılabilir. Bu, bu değerden ve yazma isteğinin küme bitlerini temizleme işlemini sağlayan sınırsız sayıda kez yazılabilen bellekten farklıdır. Son olarak, her sayfayla ilişkili yedek baytlar nve Flash için benzersizdir. Tipik yedek bayt yapılandırması aşağıdaki tabloda gösterildiği gibidir.

| **Yedek baytlar** | **Bayt numaraları** | **Yapılandırma**     |
| ------------------------- | -------------- | --------------------- |
| 8                         | Bayt 0-2:     | ECC bayt sayısı             |
|                           | Bayt 3, 4, 6, 7: | LevelX kesim eşleme |
|                           | Bayt 5:        | Hatalı blok bayrağı        |
| 16                        | Bayt 0-3, 6-7: | ECC bayt sayısı             |
|                           | Bayt 8-11:    | LevelX kesim eşleme |
|                           | Bayt 12-15:   | Kullanılmıyor                |
|                           | Bayt 5:        | Hatalı blok bayrağı        |
| 64                        | Bayt 0:        | Hatalı blok bayrağı        |
|                           | Bayt 2-5:     | LevelX kesim eşleme |
|                           | Bayt 6-39:    | Kullanılmıyor                |
|                           | Bayt 40-63:   | ECC bayt sayısı             |

LevelX, fiziksel nve sayfasıyla eşleştirilmiş mantıksal sektörün izlenmesini sağlamak için her bir nve sayfanın yedek baytından oluşan 4 ' ü kullanır. Bu 4 bayt, bir LevelX özel biçimiyle 32 bitlik işaretsiz bir tamsayı uygulamak için kullanılır. 32 bitlik alanın (bit 31) üst biti, mantıksal kesim-sayfa eşlemesinin geçerli olduğunu göstermek için kullanılır. Bu bit 0 ise, bu sayfadaki bilgiler artık geçerli değildir. Sonraki bit — bit 30 — bu sayfanın kullanılmıyor olma sürecinde olduğunu ve yeni bir sektör yazıldığını belirtmek için kullanılır. Eşleme girişi yazma işleminin tamamlandığını göstermek için bit 29 kullanılır. Bit 29 0 ise, eşleme girişi yazma tamamlanmıştır. Bit 29 ayarlanmışsa, eşleme girişi yazma süreciydi. BITS 30 ve 29, yeni bir Flash sayfası güncelleştirilirken olası bir güç kaybından kurtarmak için kullanılır. Son olarak, daha düşük 29 bit (28-0) sayfanın mantıksal sektör numarasını içerir.

**LevelX eşleme girişi**

| Bit (lar) | Anlamı |
| ------ | ------- |
| 31     | Geçerli bayrak. Set ve mantıksal kesim her ikisi de, eşlemenin geçerli olduğunu belirtir |
| 30     | Kullanım dışı bayrağı. Bu eşleme açık olmadığında veya artık kullanılmıyor olma sürecinde. |
| 29     | Bu bit 0 olduğunda eşleme girişi yazma işlemi tamamlanır |
| 0-28   | Bu fiziksel sayfayla eşlenen mantıksal kesim (hepsi değil). |

LevelX, blok silme sayısı için her nve bloğunun ilk sayfasından ve blok dolduğunda eşlenen sayfaların listesine de yararlanır. LevelX içindeki bir nve bloğunun ilk sayfasının biçimi aşağıda gösterilmiştir:

| LevelX blok sayfası 0 biçimi |
|:--------------------------:|
| [Blok silme sayısı]        |
| [Sayfa 1 kesim eşleme]    |
| ...                        |
| [Sayfa "n" kesim eşleme]  |
| [0xF0F0F0F0]               |

> [!NOTE]
> Sayfa eşleme bilgileri yalnızca blok dolduğunda yazılır, yani bloktaki tüm sayfalar üzerine yazılır. Bu, çalışma zamanında Ücretsiz sayfalar ve mantıksal kesim eşlemesi için daha hızlı arama yapmanızı sağlar.

## <a name="nand-bad-block-support"></a>NVE hatalı blok desteği

NVE belleğin bozuk blokları veya belleği da daha yüksektir. Bu çoğu büyük bir deyişle, nve üreticileri kötü bloklara izin vererek ve yazılımın bu tür hatalı bloklar üzerinde çalışmasını gerektirerek verimi artırabilir. LevelX yalnızca hatalı bloklar etrafında eşleme yaparak nve hatalı blok yönetimini işler.

LevelX, yeni ECC kodlarını hesaplamak için kullanılacak temel LevelX sürücüsü için 256 baytlık bir hata düzeltme kodları (ECC) için API 'Ler sağlar veya sayfanın her 256-Byte bölümünde sayfa okuma sırasında 1 bit hata düzeltmesi gerçekleştirir.

## <a name="nand-driver-requirements"></a>NVE sürücü gereksinimleri

LevelX, temel alınan Flash bölümü ve donanım uygulamasına özel bir temel nve Flash sürücüsü gerektirir. Sürücü, API ***lx_nand_flash_open*** aracılığıyla başlatma sırasında levelx olarak belirtilir. LevelX sürücüsünün prototipi aşağıdaki gibidir.

```c
INT nand_driver_initialize(LX_NAND_FLASH *instance);
```

*Örnek* parametresi, LEVELX NAND denetim bloğunu belirtir. Sürücü başlatma işlevi, ilişkili LevelX örneği için diğer tüm sürücü düzeyi Hizmetleri ayarlamaktan sorumludur. Her bir LevelX NAND örneği için gereken hizmetler aşağıdaki listede gösterilmektedir.

- Sayfayı oku
- Yazma sayfası
- Blok silme
- Blok silinme doğrulaması
- Sayfa silindi doğrula
- Engelleme durumu Al
- Blok durumu kümesi
- Ek baytları engelle al
- Fazla bayt kümesini engelle
- Sistem hata Işleyicisi

## <a name="driver-initialization"></a>Sürücü başlatma

Bu hizmetler, sürücünün başlatma işlevindeki **LX_NAND_FLASH** örneğindeki işlev işaretçileri ayarlanarak kurulumlardır. Sürücü başlatma işlevi aynı zamanda toplam blok sayısını, blok başına sayfa sayısını, sayfa başına baytları ve bir sayfadan oluşan belleği okumak için yeterince büyük bir RAM alanını belirtir. Sürücü başlatma işlevi büyük olasılıkla **LX_SUCCESS** döndürmeden önce ek cihaz ve/veya uygulamaya özgü başlatma görevlerini de gerçekleştiriyor.

## <a name="driver-read-page"></a>Sürücü okuma sayfası

LevelX nve sürücü "okuma sayfası" hizmeti, nve Flash 'ın belirli bir bloğundaki belirli bir sayfayı okumaktan sorumludur. Mantığın tüm hata denetlemesi ve düzeltilmesi, sürücü hizmetinin sorumluluğundadır. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "okuma sayfası" hizmetinin prototipi aşağıda verilmiştir.

```c
INT nand_driver_read_page(
    ULONG block,
    ULONG page,
    ULONG *destination, 
    ULONG words);
```

Burada *blok* ve *sayfa* hangi sayfanın okunacağını ve *hedef* ve *sözcükleri* belirler sayfa içeriğinin nereye yerleştirileceğini ve kaç 32 bitlik kelime okunacağını belirtir.

## <a name="driver-write-page"></a>Sürücü yazma sayfası

LevelX nve sürücü "yazma sayfası" hizmeti, belirli bir sayfanın belirtilen nve Flash bloğuna yazmasından sorumludur. Tüm hata denetimi ve ECC hesaplama, sürücü hizmetinin sorumluluğundadır. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "yazma sayfası" hizmetinin prototipi aşağıda gösterilmiştir.

```c
INT nand_driver_write_page(
    ULONG block, 
    ULONG page,
    ULONG *source, 
    ULONG words);
```

Burada *blok* ve *sayfa* hangi sayfanın yazılacağını ve *kaynak* ve *sözcükleri* belirler, yazma kaynağını ve kaç 32 bitlik sözcük yazılacağını belirtir.

> [!NOTE]
> LevelX, genellikle sayfanın geri okunmasını ve yazma işleminin başarılı olduğundan emin olmak için yazma arabelleğini karşılaştırarak, Flash sayfasına yazarken alt düzey hata algılaması için sürücüyü kullanır.

## <a name="driver-block-erase"></a>Sürücü bloğunu silme

LevelX nve sürücü "blok silme" hizmeti, nve Flash 'un belirtilen bloğunu silmekten sorumludur. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "blok silme" hizmetinin prototipi aşağıdaki gibidir.

```c
INT nand_driver_block_erase(ULONG block,  
    ULONG erase_count);
```

Burada *blok* hangi bloğun silinecek bloğunu belirler. *Erase_count* parametresi, tanılama amacıyla sağlanır. Örneğin, sürücü, silme sayısı belirli bir eşiği aştığında, uygulama yazılımının başka bir bölümüne uyarı vermek isteyebilir.

> [!NOTE]
> LevelX, blok silinince alt düzey hata algılaması için sürücüyü kullanır. Bu, genellikle bloktaki tüm sayfaların tümünün olduğundan emin olmayı içerir.

## <a name="driver-block-erased-verify"></a>Sürücü bloğunu silinen doğrulama

LevelX nve sürücü "blok silinenler" hizmeti, nve Flash 'un belirtilen bloğunun silindiğini doğrulamaktan sorumludur. Silinirse, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Blok silinmeyen, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "blok silinenler" hizmetinin prototipi:

```c
INT nand_driver_block_erased_verify(ULONG block);
```

Burada *blok* , hangi bloğun silindiğini doğrulayabildiğini belirtir.

> [!NOTE]
> LevelX, tüm sayfaları ve her bir sayfanın (yedek ve veri baytları dahil olmak üzere) silindiklerinden emin olmak için sürücüyü temel alır.

## <a name="driver-page-erased-verify"></a>Sürücü sayfası silinme doğrulaması

LevelX nve Driver "sayfa silinenler" hizmeti, belirtilen nve Flash bloğunun belirtilen sayfasının silinmesinden emin olmak için sorumludur. Silinirse, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Sayfa silinmeyen, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "sayfa silinverify" hizmetinin prototipi:

```c
INT nand_driver_page_erased_verify(
    ULONG block,  
    ULONG page);
```
Burada *blok* , hangi bloğun ve *sayfanın* silineceğini doğrulamak için sayfayı belirtir.

> [!NOTE]
> LevelX belirtilen sayfanın tüm baytlarını (yedek ve veri baytları dahil olmak üzere) inceleyerek, silindiklerinden emin olmak için sürücüyü kullanır (tümünü içerir).

## <a name="driver-block-status-get"></a>Sürücü engelleme durumu Al

LevelX nve sürücü "blok durumu alma" hizmeti, nve Flash 'ın belirtilen bloğunun hatalı blok bayrağını almaktan sorumludur. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Bu başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "blok durumu Al" hizmetinin prototipi aşağıda verilmiştir: aşağıda gösterilmektedir.

```c
INT nand_driver_block_status_get(
    ULONG block,  
    UCHAR *bad_block_byte);
```

Burada *blok* , hangi bloğun ve *bad_block_byte* hatalı blok bayrağıyla ilgili hedefi belirtir.

## <a name="driver-block-status-set"></a>Sürücü bloğu durum kümesi

LevelX nve sürücü "blok durum kümesi" hizmeti, nve Flash 'ın belirtilen bloğunun hatalı blok bayrağını ayarlamaktan sorumludur. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Bu başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "blok durum kümesi" hizmetinin prototipi şunlardır:

```c
INT nand_driver_block_status_set(
    ULONG block,
    UCHAR bad_block_byte);
```

Burada *blok* , hangi bloğun ve *bad_block_byte* hatalı blok bayrağının değerini belirtir.

## <a name="driver-block-extra-bytes-get"></a>Sürücü bloğu ek baytları al

LevelX nve sürücüsü "fazladan bayt alma" işlemi, nve Flash 'un belirli bir bloğunun belirli bir sayfasıyla ilişkili ek baytları almaktan sorumludur. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Bu başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "ekstra bayt al" hizmeti 'nin prototipi:

```c
INT nand_driver_block_extra_bytes_get(
    ULONG block,  
    ULONG page, 
    UCHAR *destination, 
    UINT size);
```

Burada *blok* hangi engellemeyi belirtir, *sayfa* belirli bir sayfayı belirtir ve *hedef* , ek baytlar için hedefi belirtir. Parametre *boyutu* kaç tane fazladan bayt alınacağını belirtir.

## <a name="driver-block-extra-bytes-set"></a>Sürücü bloğu ek bayt kümesi

LevelX nve sürücü "ekstra bayt kümesini engelle" hizmeti, nve Flash 'un belirli bir bloğunun belirli bir sayfasında fazladan baytlar ayarlamaktan sorumludur. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Bu başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve Driver "ekstra bayt kümesini engelle" hizmetinin prototipi şunlardır:

```c
INT nand_driver_block_extra_bytes_set(
    ULONG block,  
    ULONG page, 
    UCHAR *source, 
    UINT size);
```

Burada *blok* hangi engellemeyi belirtir, *sayfa* belirli bir sayfayı belirtir ve *kaynak* , fazladan baytların kaynağını belirtir. Parametre *boyutu* , kaç tane fazladan bayt ayarlanacağını belirtir.

## <a name="driver-system-error"></a>Sürücü sistemi hatası

Levelx nve sürücü "sistem hatası işleyicisi" hizmeti, LevelX tarafından algılanan sistem hatalarının işlenmesini ayarlamaktan sorumludur. Bu yordamın işleme uygulamaya bağımlıdır. Başarılı olursa, LevelX nve sürücüsü **LX_SUCCESS** döndürür. Bu başarılı olmazsa, LevelX nve sürücüsü **LX_ERROR** döndürür. LevelX nve sürücü "sistem hatası" hizmetinin prototipi:

```c
INT nand_driver_system_error(
    UINT error_code,  
    ULONG block, 
    ULONG page);
```

Burada *blok* hangi bloğun ve *sayfanın* *error_code* tarafından temsil edilen hatayı belirten sayfayı belirtir.

## <a name="nand-simulated-driver"></a>NVE sanal sürücü

LevelX, bir nve Flash bölümü işleminin benzetimini yapmak için yalnızca RAM kullanan bir benzetimli nve Flash sürücüsü sağlar. Varsayılan olarak, nve sanal sürücü, blok başına 16 sayfa ve sayfa başına 2048 bayt içeren 8 nve Flash blokları sağlar.

Benzetimli nve Flash sürücü başlatma işlevi, ***lx_nand_flash_simulator_initialize** _ ve _ *_lx_nand_flash_simulator. c_* * içinde tanımlanmıştır. Bu sürücü Ayrıca belirli nve Flash sürücülerini yazmak için iyi bir şablon sağlar.

## <a name="nand-filex-integration"></a>NVE FileX tümleştirmesi

Daha önce belirtildiği gibi, LevelX işlem için FileX 'i kullanmaz. Tüm LevelX API 'Leri, ham verileri, LevelX tarafından sunulan mantıksal sektörlerde depolamak/almak için doğrudan uygulama yazılımı tarafından çağrılabilir. Ancak, LevelX de Fılex 'i destekler.

***Fx_nand_flash_simulated_driver. c*** dosyası, nve flash simülasyonu ile kullanılmak üzere bir örnek FileX sürücüsü içerir. Bu sürücünün ilgi çekici bir yönü, genellikle FileX tarafından, 2048 baytlık sayfalar kullanılarak LevelX benzeticisinde tek mantıksal kesim okuma/yazma istekleri olarak kullanılan 512 baytlık mantıksal kesimleri birleştirmesidir. Bu, nve flash belleğin daha verimli bir şekilde kullanılmasına neden olur. LevelX için nve Flash FileX sürücüsü, özel FileX sürücüleri yazmak için iyi bir başlangıç noktası sağlar.  
  
> [!NOTE]
> FileX nve Flash biçimi, nve Flash tarafından sağlanan kesimlerin bir tam blok boyutu olmalıdır. Bu, aşınma düzeyi işleme sırasında en iyi performansı sağlamaya yardımcı olur. LevelX aşmalar seviyelendirme algoritmasındaki yazma performansını artırmaya yönelik ek teknikler şunlardır.

1. Tüm yazmamaların tam olarak bir veya daha fazla küme olduğundan emin olun ve tam küme sınırları üzerinde başlatın.
1. API 'lerin FileX ***fx_file_allocate*** sınıfı aracılığıyla büyük dosya yazma işlemleri gerçekleştirmeden önce kümeleri önceden ayırın.
1. FileX sürücüsünün yayın sektörü bilgilerini alacak şekilde etkinleştirildiğinden emin olun ve sürücü sürüm sektörlerine yapılan istekler ***lx_nor_flash_sector_release*** çağırarak sürücüde işlenir.
1. Olabildiğince çok nve blok açmak için ***lx_nand_flash_defragment*** düzenli olarak kullanımı ve bu sayede yazma performansını artırma.
1. Daha hızlı performans sağlamak için ***lx_nand_flash_extended_cache_enable*** API 'sini, ÇEŞITLI nve kaynak blok kaynakları IÇIN bir RAM önbelleği sağlamak üzere kullanın.
