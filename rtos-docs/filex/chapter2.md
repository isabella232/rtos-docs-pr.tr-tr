---
title: Bölüm 2 - Azure RTOS FileX'i yükleme ve kullanma
description: Bu bölümde FileX Azure RTOS ve yükleme koşullarının, yordamlarının ve kullanımının açıklaması ve aşağıdakiler de dahil olmak üzere bir giriş yer almaktadır
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2f064fc65ef8445ea33590f23d5a040ed8b07c6c651ea4cf5c4aaef4b6c4fa7b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783858"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-filex"></a>Bölüm 2 - Azure RTOS FileX'i yükleme ve kullanma

Bu bölümde FileX'e Azure RTOS ve yükleme koşulları, yordamları ve kullanımına ilişkin bir açıklama yer almaktadır. 

## <a name="host-considerations"></a>KonakLa ilgili Dikkat Edilmesi Gerekenler

### <a name="computer-type"></a>Bilgisayar Türü

Katıştırılmış geliştirme genellikle linux (Unix) Windows bilgisayarlarda gerçekleştirilir. Uygulama derledikten, bağlandıktan ve konakta bulunduktan sonra, yürütme için hedef donanıma indirilir.

### <a name="download-interfaces"></a>Arabirimleri İndirme

Hedef indirme genellikle geliştirme aracının hata ayıklayıcısından yapılır. İndirmeden sonra, hata ayıklayıcısı hedef yürütme denetimi (go, durdurma, kesme noktası vb.) sağlamanın yanı sıra bellek ve işlemci kayıtlarına erişim sağlamakla sorumludur.

### <a name="debugging-tools"></a>Hata Ayıklama Araçları

Çoğu geliştirme aracı hata ayıklayıcısı, JTAG (IEEE 1149.1) ve Arka Plan Hata Ayıklama Modu (BDM) gibi yonga üzerinde hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar ayrıca Öykünme (ICE) In-Circuit hedef donanımla iletişim kurar. Hem OCD hem de ICE bağlantıları, hedef yerleşik yazılıma en az izinsiz girişle sağlam çözümler sağlar.

### <a name="required-hard-disk-space"></a>Gerekli Sabit Disk Alanı

FileX kaynak kodu ASCII biçiminde teslim edilir ve konak bilgisayarın sabit diskte yaklaşık 500 KBayt alan gerektirir

## <a name="target-considerations"></a>HedefLe ilgili Dikkat Edilmesi Gerekenler

FileX, hedefte 6 KBayt ile 30 KBayt Read-Only Bellek (ROM) gerektirir. FileX genel veri yapıları için hedefin Rastgele Erişim Belleği'nin (RAM) 100 bayt daha olması gerekir. Her açık medya, bir kesime (genellikle 512 bayt) veri depolamak için RAM'e ek olarak denetim bloğu için 1,5 KBayt RAM gerektirir.

Tarih/saat damgasının düzgün çalışması için FileX, ThreadX zamanlayıcı olanaklarını kullanır. Bu, FileX başlatma sırasında FileX'e özgü bir zamanlayıcı oluşturarak uygulanır. FileX ayrıca birden çok iş parçacığı koruması ve I/O'nun askıya alınması için ThreadX semaforlarını da kullanabilir.

## <a name="product-distribution"></a>Ürün Dağıtımı

Azure RTOS FileX, genel kaynak kod depomuzdan <https://github.com/azure-rtos/filex/> edinebilirsiniz.

Aşağıda, depoda yer alan birkaç önemli dosyanın listesi ve ardından yer alan liste ve bir liste ve ardından yer alan bilgileri bulabilirsiniz:

- ***fx_api.h:*** Bu C üst bilgi dosyası tüm sistem eşitlerini, veri yapılarını ve hizmet prototiplerini içerir.
- ***fx_port.h:*** Bu C üst bilgi dosyası, geliştirme aracına özgü tüm veri tanımlarını ve yapılarını içerir.
- ***demo_filex.c:*** Bu C dosyası küçük bir tanıtım uygulaması içerir.
- ***fx.a (veya fx.lib):*** Bu, FileX C kitaplığının ikili sürümüdür. Standart paketle dağıtılır.

> [!IMPORTANT]
> *Tüm dosya adları küçük harflidir. Bu adlandırma kuralı komutları Linux (Unix) geliştirme platformlarına dönüştürmeyi kolaylaştırır.*

## <a name="filex-installation"></a>FileX Yüklemesi

FileX, yerel makinenize GitHub kopya tarafından yüklenir. Aşağıda, bilgisayarınızda FileX deposunun bir kopyasını oluşturmak için tipik bir söz dizimi ve ardından yer alan söz dizimi ve daha sonra yer alan genel bir söz dizimi ve daha fazla bilgi ve daha fazla bilgi için bkz.

```c
    git clone https://github.com/azure-rtos/filex
```

Alternatif olarak, ana sayfada yer alan indirme düğmesini kullanarak deponun bir GitHub indirebilirsiniz.

FileX kitaplığını oluşturma yönergelerini çevrimiçi deponun ön sayfasında da bulabilirsiniz.

> [!IMPORTANT]
> Uygulama yazılımının, C dahil **fx_api.h** ve fx_port.h dosyaları için FileX kitaplık dosyasına (genellikle * genellikle ***fx.a** _ veya _*_fx.lib_*_ _and olarak bilinir) **erişmesi gerekir.** Bu, geliştirme araçları için uygun yolu ayarlayıp veya bu dosyaları uygulama geliştirme alanına kopyalayıp bunu gerçekleştirebilirsiniz.

## <a name="using-filex"></a>FileX Kullanma

FileX'i kullanmak kolaydır. Temel olarak, uygulama kodu derleme sırasında ***fx_api.h** _ öğesini ve fx.a (veya _*_fx.lib)_*_ FileX çalışma zamanı kitaplığıyla bağlantıyı içermeli. _**_ Elbette, _*_tx_api.h_*_ ve _*_tx.a_*_ (veya _*_tx.lib_*_)_,* gibi ThreadX dosyaları da gereklidir.

> [!IMPORTANT]
> Tek başına modda FileX kullanılırken (**FX_STANDALONE_ENABLE** gerekir), ThreadX dosyaları/kitaplıkları gerekli değildir.

ThreadX'i zaten kullanıyorsanız, Bir FileX uygulaması oluşturmak için gereken dört adım vardır:

1. ***fx_api.h dosyasını*** FileX hizmetlerini veya veri yapılarını kullanan tüm uygulama dosyalarına dahil etmek.
1. _ tx_application_define * işlevinden veya **bir uygulama iş parçacığından****_fx_system_initialize_* _ çağırarak FileX sistemini başlatma.

    > [!IMPORTANT]
    > Tek başına modda FileX kullanırken, ***fx_system_initialize*** doğrudan uygulama kodundan çağrılabilir.

1. FileX medyası ayarlamak ***için fx_media_open*** bir veya daha fazla çağrı ekleyin. Bu çağrı bir uygulama iş parçacığının bağlamından yapılmış olması gerekir.

    > [!IMPORTANT]
    > *Çağrının tek **fx_media_open** verileri depolamak için yeterli RAM gerektirdiğini unutmayın.*

1. Uygulama kaynağını derle ve FileX ve ThreadX çalışma zamanı kitaplıkları, ***fx.a** _ (veya _*_fx.lib_*_) ve _*_tx.a_*_ (veya _*_tx.lib_**) ile bağlantıyı derle. Sonuçta elde edilen görüntü hedefe indirilir ve yürütülür!

## <a name="troubleshooting"></a>Sorun giderme

Her FileX bağlantı noktası bir tanıtım uygulaması ile birlikte teslim edilir. Tanıtım sisteminin önce hedef donanımda veya belirli bir tanıtım ortamında çalıştırılana kadar her zaman iyi bir fikirdir.

Tanıtım sistemi çalışmıyorsa sorunu daraltmak için aşağıdaki adımları deneyin:

1. Gösterimin ne kadar çalıştırı olduğunu belirleme.
1. Yığın boyutlarını artırma (bu, gerçek uygulama kodunda gösterimden daha önemlidir).
1. 32KBayt varsayılan RAM disk boyutu için yeterli RAM olduğundan emin olmak. Temel sistem çok daha az RAM üzerinde çalışır; ancak, RAM diskin daha fazlası kullanılırken, yeterli bellek yoksa sorunlar ortaya çıkar.
1. Sorunun kaybolur mu yoksa değişir mi olduğunu görmek için son yapılan değişiklikleri geçici olarak atlar. Bu tür bilgiler Microsoft destek mühendisleri için faydalı olacaktır. Sorun giderme adımlarından toplanan bilgileri göndermek için "Müşteri Destek Merkezi"nde özetlenen yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma Seçenekleri

FileX kitaplığını ve uygulamayı FileX kullanarak oluşturmanın çeşitli yapılandırma seçenekleri vardır. Aşağıdaki seçenekler uygulama kaynağında, komut satırı veya ***fx_user.h include dosyasında*** tanımlanabilir.

> [!IMPORTANT]
> fx_user.h dosyasında tanımlanan seçenekler yalnızca uygulama ve ThreadX kitaplığı ***FX_INCLUDE_USER_DEFINE_FILE *_ _defined.__ DosyaX*** tek başına modunda kullanılırken ( FX_STANDALONE_ENABLE * tanımlanmalıdır) uygulanır, ThreadX dosyaları/kitaplıkları gerekli değildir.

Aşağıdaki listede her yapılandırma seçeneği ayrıntılı olarak açıklanmaktadır:

|Tanımlamak|Anlamı|
|----------    |-----------|
|FX_MAX_LAST_NAME_LEN        |Bu değer, tam yol adını içeren maksimum dosya adı uzunluğunu tanımlar. Varsayılan olarak bu değer 256'dır.|
|FX_DONT_UPDATE_OPEN_FILES    |FileX önceden açılmış dosyaları güncelleştirmez.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Tanımlı, dosya arama önbelleği iyileştirmesi devre dışı bırakıldı.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Tanımlı, dosya arama önbelleği iyileştirmesi devre dışı bırakıldı.|
|FX_DISABLE_DIRECT_DATA_READ_CACHE_FILL |Tanımlı, önbelleğin doğrudan okuma kesimi güncelleştirmesi devre dışı bırakılmıştır.|
|FX_MEDIA_STATISTICS_DISABLE |Tanımlı, medya istatistiklerinin toplanması devre dışı bırakılmıştır.|
|FX_SINGLE_OPEN_LEGACY |Tanımlı, aynı dosya için eski tek açık mantık etkinleştirilir.|
|FX_RENAME_PATH_INHERIT    |Tanımlanan, yeniden yapılanma yol bilgilerini devralıyor.|
|FX_DISABLE_ERROR_CHECKING    |Temel FileX hata denetleme API'sini kaldırır ve gelişmiş performans (%30'a kadar) ve daha küçük kod boyutuna neden olur.|
|FX_MAX_LONG_NAME_LEN    |FileX için en büyük dosya adı boyutunu belirtir. Varsayılan değer 256'dır, ancak bir komut satırı tanımlaması ile geçersiz kılınabilir. Yasal değerler 13 ile 256 arasında değişebilir.|
|FX_MAX_SECTOR_CACHE|FileX tarafından önbelleğe alınacak en fazla mantıksal kesim sayısını belirtir. Önbelleğe alınacak gerçek kesim sayısı bu sabitten daha azdır ve bu sabitte sağlanan bellek miktarına kaç kesim fx_media_open. Varsayılan değer 256'dır. Tüm değerlerin 2 gücü olması gerekir.|
|FX_FAT_MAP_SIZE    |FAT güncelleştirme haritasında temsil edilebilir kesimlerin sayısını belirtir. Varsayılan değer 256 ' dir, ancak bu, komut satırı tanımlamaile geçersiz kılınabilir. Daha büyük değerler, ikincil FAT sektörlerinin gereksiz güncelleştirmelerini azaltmaya yardımcı olur.|
|FX_MAX_FAT_CACHE    |İç FAT önbelleğindeki giriş sayısını belirtir. Varsayılan değer 16 ' dır, ancak bu, bir komut satırı tanımlamaile geçersiz kılınabilir. Tüm değerler 2 ' nin üssü olmalıdır.|
|FX_FAULT_TOLERANT    |Tanımlandığında, FileX tüm sistem kesimlerinin (önyükleme, FAT ve Dizin kesimleri) yazma isteklerini medya sürücüsüne hemen geçirir. Bu, performansı düşürür, ancak bozulmaları kayıp kümeleriyle sınırlandırmaya yardımcı olur. Bu özelliğin etkinleştirilmesi, tanımlama tarafından etkinleştirilen, FileX hata dayanıklı modülünü otomatik olarak etkinleştirmez.|
|FX_FAULT_TOLERANT_DATA    |Tanımlandığında, FileX tüm dosya verileri yazma isteklerini medya sürücüsüne hemen geçirir. Bu, performansı düşürür, ancak kayıp dosya verilerini sınırlamaya yardımcı olur. Bu özelliğin etkinleştirilmesi, ***FX_ENABLE_FAULT_TOLERANT*** tanımlayarak etkinleştirilen FileX hata toleranslı modülünü otomatik olarak etkinleştirmez.|
|FX_NO_LOCAL_PATH|Yerel yol mantığını FileX öğesinden kaldırır ve daha küçük kod boyutuna neden olur.|
|FX_NO_TIMER|Dosya x sistem saatini ve tarihini güncelleştirmek için ThreadX Zamanlayıcı kurulumunu ortadan kaldırır. Bunun yapılması, tüm dosya işlemlerine varsayılan saat ve tarihin yerleştirilmesine neden olur.|
|FX_UPDATE_RATE_IN_SECONDS    |FileX içindeki sistem saatinin ayarlandığı oranı belirtir. Varsayılan değer 10 ' dur, FileX sistem saatinin her 10 saniyede bir güncelleştirildiğini belirten.|
|FX_ENABLE_EXFAT| Tanımlandığında, FileX 'te exFAT dosya sistemini işleme mantığı etkinleştirilir. Varsayılan olarak bu simge tanımlı değildir.| 
|FX_UPDATE_RATE_IN_TICKS| Temel alınan ThreadX Zamanlayıcı sıklığının dışında, ***FX_UPDATE_RATE_IN_SECONDS*** (yukarıya bakın) ile aynı oranı belirtir. Varsayılan değer, 10 MS ThreadX Zamanlayıcı oranının ve 10 saniyelik bir aralığın kabul eden 1000 ' dir.|
|FX_SINGLE_THREAD|Dosya x kaynağından ThreadX koruma mantığını ortadan kaldırır. FileX yalnızca bir iş parçacığından kullanılıyorsa veya dosya x ThreadX olmadan kullanılıyorsa, bu kullanılır.|
|FX_DRIVER_USE_64BIT_LBA|Tanımlandığında, g/ç sürücüsünde 64 bitlik kesim adreslerini kullanır. Varsayılan olarak bu seçenek tanımlı değildir.|
|FX_ENABLE_FAULT_TOLERANT| Tanımlandığında, FileX hataya dayanıklı modülü etkinleştirilir. Hata dayanıklılığını etkinleştirmek, otomatik olarak ***FX_FAULT_TOLERANT** _ ve _ *_FX_FAULT_TOLERANT_DATA_* * sembolünü tanımlar. Varsayılan olarak bu seçenek tanımlı değildir.|
|FX_FAULT_TOLERANT_BOOT_INDEX|Hata toleranslı günlük kümesinin olduğu önyükleme kesimindeki bayt sapmasını tanımlar. Bu değer varsayılan olarak 116 ' dir. Bu alan 4 bayt sürer. 116 ile 119 arasındaki baytlar, FAT 12/16/32/exFAT belirtimine göre ayrılmış olarak işaretlendiğinden seçilir.|
|FX_FAULT_TOLERANT_MINIMAL_CLUSTER|Bu simge kullanım dışıdır. Artık FileX hata toleranslı tarafından kullanılmıyor.|
|FX_STANDALONE_ENABLE|Tanımlı, FileX 'in tek başına modda kullanılmasını sağlar (Azure RTOS olmadan). Varsayılan olarak bu simge tanımlı değildir.|

> [!IMPORTANT]
> **FX_STANDALONE_ENABLE** tanımlandığında, yerel yol mantığı ve threadx Zamanlayıcı kurulumu devre dışı bırakılır.

## <a name="filex-version-id"></a>FileX sürüm KIMLIĞI

Geçerli FileX sürümü, hem Kullanıcı hem de uygulama yazılımının çalışma zamanı sırasında kullanılabilir. Programcı, FileX sürümünü **fx_port. h** dosyasının inceağından elde edebilir. Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir. Uygulama yazılımı, **_ _fx_version_id_** Genel dizesini inceleyerek FileX sürümünü alabilir.
