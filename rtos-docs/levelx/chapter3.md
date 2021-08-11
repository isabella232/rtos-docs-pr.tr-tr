---
title: Azure RTOS LevelX nve desteği
description: NVE Flash belleği, genellikle dosya sistemlerinin tipik bir örneği olan büyük veri depolama için LevelX içinde kullanılır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 950a4f260d032ebe032aca79ac99cc8217915a3b21b230be9475d82b267da18c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790590"
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
- Blok Durumu Al
- Durum Kümesi Engelleme
- Ek Bayt Al'a Engelle
- Ek Bayt Kümelerini Engelle
- Sistem Hata İşleyicisi

## <a name="driver-initialization"></a>Sürücü Başlatma

Bu hizmetler, sürücünün başlatma işlevi  içindeki LX_NAND_FLASH işaretçileri ayar aracılığıyla ayarlar. Sürücü başlatma işlevi ayrıca toplam blok sayısını, blok başına sayfa sayısını, sayfa başına bayt sayısını ve bir sayfayı belleğe okumak için yeterince büyük bir RAM alanı belirtir. Sürücü başlatma işlevi, büyük olasılıkla yeniden başlatmadan önce ek cihaz ve/veya uygulamaya özgü başlatma **görevlerini LX_SUCCESS.**

## <a name="driver-read-page"></a>Sürücü Okuma Sayfası

LevelX NAND sürücüsü "sayfayı okuma" hizmeti, BELIRLI bir sayfayı, NAND flash'ın belirli bir bloğunda okumaktan sorumludur. Tüm hata denetleme ve düzeltme mantığı sürücü hizmetinin sorumluluğundadır. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "okuma sayfası" hizmetinin prototipi aşağıda verilmiştir.

```c
INT nand_driver_read_page(
    ULONG block,
    ULONG page,
    ULONG *destination, 
    ULONG words);
```

Burada *blok* ve *sayfa,* okunacak  sayfayı ve hedefle sözcükleri, sayfa içeriğinin nereye konacaklarını ve kaç tane 32 bit sözcüklerin okunacaklarını belirtir. 

## <a name="driver-write-page"></a>Sürücü Yazma Sayfası

LevelX NAND sürücüsü "yazma sayfası" hizmeti, belirli bir sayfayı BELIRTILEN NAND flash bloğuna yazmaktan sorumludur. Tüm hata denetimi ve ECC hesaplaması, sürücü hizmetinin sorumluluğundadır. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "yazma sayfası" hizmetinin prototipi aşağıda gösterilmiştir.

```c
INT nand_driver_write_page(
    ULONG block, 
    ULONG page,
    ULONG *source, 
    ULONG words);
```

Burada *blok* ve *sayfa,* yazacak  sayfayı ve kaynak sözcükleri, yazma kaynağını ve kaç tane 32 bit sözcük yazacaklarını belirtir. 

> [!NOTE]
> LevelX, flash sayfaya yazarken düşük düzeyli hata algılama için sürücüden kullanır. Bu, genellikle sayfayı geri okumayı ve yazmanın başarılı olduğundan emin olmak için yazma arabelleğiyle karşılaştırmayı içerir.

## <a name="driver-block-erase"></a>Sürücü Blok Silme

LevelX NAND sürücüsü "blok silme" hizmeti, BELIRTILEN NAND flash bloğu silinerek sorumludur. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "blok silme" hizmetinin prototipi aşağıdaki gibidir.

```c
INT nand_driver_block_erase(ULONG block,  
    ULONG erase_count);
```

Burada *blok,* silinecek bloğu tanımlar. Parametre *erase_count* tanılama amacıyla sağlanır. Örneğin, silme sayısı belirli bir eşiği aştı mı, sürücü uygulama yazılımının başka bir bölümünü uyarmak istiyor olabilir.

> [!NOTE]
> LevelX, blok silinebilirken düşük düzeyli hata algılama için sürücüye güvenmektedir. Bu durum genellikle bloğun tüm sayfalarının aynı olmasını sağlar.

## <a name="driver-block-erased-verify"></a>Sürücü Blok Silme Doğrulama

LevelX NAND sürücüsü "silinen doğrulamayı engelle" hizmeti, BELIRTILEN NAND flash bloğu silindi doğrulamakla sorumludur. Silinirse, LevelX NAND sürücüsü **LX_SUCCESS.** Blok silinmezse LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "silinen doğrulamayı engelle" hizmetinin prototipi şu şekildedir:

```c
INT nand_driver_block_erased_verify(ULONG block);
```

Where *block* silindi doğrulamak için hangi bloğu belirtir.

> [!NOTE]
> LevelX, silinecekleri (hepsini içerir) emin olmak için sürücünün tüm sayfaları ve her sayfanın tüm baytlarını (yedek ve veri bayt'ları dahil) incelemektedir.

## <a name="driver-page-erased-verify"></a>Sürücü Sayfası Silinen Doğrulama

LevelX NAND sürücüsü "sayfa silme doğrulama" hizmeti, BELIRTILEN NAND flash bloğunda belirtilen sayfanın silindi olduğunu doğrulamakla sorumludur. Silinirse, LevelX NAND sürücüsü **LX_SUCCESS.** Sayfa silinmezse LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "sayfa silme doğrulama" hizmetinin prototipi şu şekildedir:

```c
INT nand_driver_page_erased_verify(
    ULONG block,  
    ULONG page);
```
Burada *blok* hangi bloğu belirtir ve *sayfa* silindi doğrulamak için sayfayı belirtir.

> [!NOTE]
> LevelX, silinecekleri (hepsini içerir) emin olmak için belirtilen sayfanın tüm baytlarını (yedek ve veri baytları dahil) incelemek için sürücüye güvenmektedir.

## <a name="driver-block-status-get"></a>Sürücü Blok Durumu Al

LevelX NAND sürücüsü "blok durumu alma" hizmeti, BELIRTILEN NAND flash bloğun hatalı blok bayrağını almakla sorumludur. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Bu başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "block status get" hizmetinin prototipi aşağıda gösterilmiştir.

```c
INT nand_driver_block_status_get(
    ULONG block,  
    UCHAR *bad_block_byte);
```

Burada *blok,* hatalı bad_block_byte *için* hedefi belirtir.

## <a name="driver-block-status-set"></a>Sürücü Bloğu Durum Kümesi

LevelX NAND sürücüsü "blok durumu kümesi" hizmeti, BELIRTILEN NAND flash bloğu için hatalı blok bayrağını ayarlamakla sorumludur. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Bu başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "blok durum kümesi" hizmetinin prototipi şu şekildedir:

```c
INT nand_driver_block_status_set(
    ULONG block,
    UCHAR bad_block_byte);
```

Burada *blok,* hangi bloğun *bad_block_byte* hatalı blok bayrağının değerini belirtir.

## <a name="driver-block-extra-bytes-get"></a>Sürücü Bloğu Ek Bayt Al

LevelX NAND sürücüsü "fazladan bayt alma bloğu" hizmeti, BELIRLI bir NAND flash bloğundan belirli bir sayfayla ilişkili ek baytların alınmasından sorumludur. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Bu başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "fazladan bayt bloklarını al" hizmetinin prototipi şu şekildedir:

```c
INT nand_driver_block_extra_bytes_get(
    ULONG block,  
    ULONG page, 
    UCHAR *destination, 
    UINT size);
```

Burada *blok* hangi bloğu belirtir, *sayfa* belirli bir sayfayı belirtir *ve* hedef ek baytlar için hedefi belirtir. Parametre *boyutu,* kaç tane ek bayt alacazı belirtir.

## <a name="driver-block-extra-bytes-set"></a>Sürücü Bloğu Ek Bayt Kümesi

LevelX NAND sürücüsü "fazladan bayt kümesi bloğu" hizmeti, BELIRLI bir NAND flash bloğunda belirli bir sayfada fazladan bayt ayarlamakla sorumludur. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Bu başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsünün "fazladan bayt kümesi engelleme" hizmetinin prototipi şu şekildedir:

```c
INT nand_driver_block_extra_bytes_set(
    ULONG block,  
    ULONG page, 
    UCHAR *source, 
    UINT size);
```

Burada *blok* hangi bloğu belirtirse *sayfa* belirli bir sayfayı, *kaynak* ise ek baytların kaynağını belirtir. Parametre boyutu *ayar* için ek bayt sayısını belirtir.

## <a name="driver-system-error"></a>Sürücü Sistemi Hatası

LevelX TARAFıNDAN algılanan sistem hatalarını işlemeyi ayarlamadan LevelX NAND sürücüsü "sistem hata işleyicisi" hizmeti sorumludur. Bu yordamda işlem uygulamaya bağlıdır. Başarılı olursa, LevelX NAND sürücüsü **LX_SUCCESS.** Bu başarılı olmazsa, LevelX NAND sürücüsü **LX_ERROR.** LevelX NAND sürücüsü "sistem hatası" hizmetinin prototipi şu şekildedir:

```c
INT nand_driver_system_error(
    UINT error_code,  
    ULONG block, 
    ULONG page);
```

Burada *blok,* hangi bloğu belirtir ve *sayfa,* hatanın hangi sayfayla temsil error_code *belirtir.*

## <a name="nand-simulated-driver"></a>NAND Sanal Sürücüsü

LevelX, YALNıZCA BIR NAND flash parçasının işlem simülasyonunu yapmak için RAM kullanan benzetimi yapılan bir NAND flash sürücü sağlar. VARSAYıLAN olarak, NAND sanal sürücüsü blok başına 16 sayfa ve sayfa başına 2048 bayt ile 8 NAND flash blok sağlar.

Benzetimi yapılan NAND flash sürücü başlatma işlevi ***lx_nand_flash_simulator_initialize** _ olur ve _*_lx_nand_flash_simulator.c ** içinde_ tanımlanır. Bu sürücü ayrıca belirli NAND flash sürücüleri yazmak için iyi bir şablon sağlar.

## <a name="nand-filex-integration"></a>NAND FileX Tümleştirmesi

Daha önce belirtildiği gibi, LevelX işlem için FileX'i güvenmez. Ham verileri LevelX tarafından sağlanan mantıksal kesimlerde depolamak/almak için tüm LevelX API'leri doğrudan uygulama yazılımı tarafından çağrılebilir. Ancak LevelX, FileX'i de destekler.

***fx_nand_flash_simulated_driver.c*** dosyasında, NAND flash simülasyonu ile birlikte kullanmak üzere örnek bir FileX sürücüsü vardır. Bu sürücünün ilginç bir yönü, Genellikle FileX tarafından kullanılan 512 byte mantıksal kesimlerini 2048-byte sayfalarını kullanarak LevelX simülatörüne tek mantıksal kesimli okuma/yazma istekleri olarak birleştirmesidir. Bu, NAND flash belleğinin daha verimli bir şekilde kullanımıyla sonuç verir. LevelX için NAND flash FileX sürücüsü, özel FileX sürücüleri yazmak için iyi bir başlangıç noktası sağlar.  
  
> [!NOTE]
> FileX NAND flash biçimi, NAND flash'ın sağladığından daha az kesimlerin tam blok boyutu olmalıdır. Bu, yıpranma düzeyi işleme sırasında en iyi performansı sağlamaya yardımcı olur. LevelX yıpranma düzeyi artırma algoritmasında yazma performansını geliştirmeye yardımcı olacak ek teknikler şunlardır.

1. Tüm yazmaların boyutu tam olarak bir veya daha fazla küme olduğundan emin olun ve tam olarak küme sınırlarıyla başlamayı seçin.
1. Büyük dosya yazma işlemlerini FileX aracılığıyla gerçekleştirmeden önce kümeleri önceden ***fx_file_allocate*** API sınıfına ayırma.
1. FileX sürücüsünün yayın kesimi bilgilerini almak için etkinleştirildiğinden ve sürücüye yayın kesimleri için yapılan isteklerin sürücüde ***lx_nor_flash_sector_release.***
1. Mümkün olduğunca ***lx_nand_flash_defragment*** SAYıDA NAND bloğu serbest bırakarak yazma performansını artırmak için düzenli aralıklarla veri kullanımı.
1. Performansta ***lx_nand_flash_extended_cache_enable*** için çeşitli NAND blok kaynaklarının RAM önbelleğini sağlamak üzere lx_nand_flash_extended_cache_enable API'sini kullanın.
