---
title: Bölüm 2-Azure RTOS FileX yükleme ve kullanımı
description: Bu bölümde, aşağıdakiler de dahil olmak üzere Azure RTOS FileX 'e giriş ve yükleme koşulları, yordamları ve kullanımı açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6703b10d8e0895984bb92d74d5dff809dca1a7f8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825510"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-filex"></a>Bölüm 2-Azure RTOS FileX yükleme ve kullanımı

Bu bölümde, Azure RTOS FileX 'e giriş ve yükleme koşulları, yordamları ve kullanımı hakkında bir açıklama yer almaktadır. 

## <a name="host-considerations"></a>Ana bilgisayar konuları

### <a name="computer-type"></a>Bilgisayar türü

Katıştırılmış Geliştirme genellikle Windows veya Linux (UNIX) ana bilgisayar bilgisayarlarında gerçekleştirilir. Uygulama derlendikten, bağlandıktan ve konakta bulunuyorsa, yürütme için hedef donanıma indirilir.

### <a name="download-interfaces"></a>Arabirimleri indir

Genellikle hedef indirme işlemi geliştirme aracının hata ayıklayıcı içinden yapılır. İndirmeden sonra, hata ayıklayıcı, hedef yürütme denetimi (go, dur, kesme noktası vb.) ve bellek ve işlemci kayıtlarına erişimi sağlamaktan sorumludur.

### <a name="debugging-tools"></a>Hata ayıklama araçları

Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar. OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.

### <a name="required-hard-disk-space"></a>Gerekli sabit disk alanı

FileX için kaynak kodu ASCII biçiminde dağıtılır ve konak bilgisayarın sabit diskinde yaklaşık 500 Kbayt alan gerektirir

## <a name="target-considerations"></a>Hedef konuları

Dosya x, hedefte 6 Kbayt ve 30 Kbayt Read-Only bellek (ROM) arasında olmalıdır. FileX genel veri yapıları için hedefin rastgele erişim belleğinin (RAM) başka bir 100 baytı gerekir. Her açılan medya Ayrıca, bir kesime yönelik verilerin depolanması için RAM 'e ek olarak denetim bloğunda 1,5 Kbayt RAM gerektirir (genellikle 512 bayt).

Tarih/saat damgalaması için düzgün çalışması için, FileX, ThreadX Zamanlayıcı tesislerini kullanır. Bu, FileX başlatma sırasında FileX 'e özgü bir Zamanlayıcı oluşturularak uygulanır. FileX, Ayrıca birden çok iş parçacığı koruması ve g/ç askıya alma için ThreadX semaforları kullanır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS FileX, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/filex/> .

Depodaki birçok önemli dosyanın listesi aşağıda verilmiştir:

- ***fx_api. h*** : Bu C üstbilgi dosyası tüm sistem eş, veri yapılarını ve hizmet prototiplerini içerir.
- ***fx_port. h*** : Bu C üstbilgi dosyası, tüm geliştirme aracına özgü veri tanımlarını ve yapılarını içerir.
- ***demo_filex. c*** : Bu c dosyası küçük bir demo uygulaması içerir.
- ***FX. a (veya FX. lib)*** : Bu, FileX C kitaplığının ikili sürümüdür. Standart paketiyle dağıtılır.

> [!IMPORTANT]
> *Tüm dosya adları küçük bir durumdur. Bu adlandırma kuralı, komutların Linux (UNIX) geliştirme platformlarına dönüştürülmesini kolaylaştırır.*

## <a name="filex-installation"></a>FileX yüklemesi

Dosya x, GitHub deposu yerel makinenize kopyalanarak yüklenir. Bilgisayarınızda FileX deposunun bir kopyasını oluşturmak için tipik sözdizimi aşağıda verilmiştir:

```c
    git clone https://github.com/azure-rtos/filex
```

Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında FileX kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.

> [!IMPORTANT]
> Uygulama yazılımının FileX kitaplık dosyasına erişmesi gerekir (genellikle * genellikle ***FX. a** _ veya _*_FX. lib_*_) C içerme dosyaları **fx_api. h** ve **fx_port. h** _and. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaları uygulama geliştirme alanına kopyalayarak gerçekleştirilir.

## <a name="using-filex"></a>FileX kullanma

FileX kullanmak kolaydır. Temel olarak, uygulama kodu derleme sırasında ***fx_api. h** _ ve FileX çalışma zamanı kitaplığı _*_FX. a_*_ (veya _*_FX. lib_*_) ile bağlantı içermelidir. Tabii ki, _*_tx_api. h_*_ ve _*_TX. a_*_ (veya _*_TX. lib_*_) _, * olan threadx dosyaları da gereklidir.

> [!IMPORTANT]
> Bağımsız modda FileX kullanılırken (**FX_STANDALONE_ENABLE** tanımlanmalıdır), threadx dosyaları/kitaplıkları gerekli değildir.

Zaten ThreadX kullandığınızı varsayarsak, bir FileX uygulaması oluşturmak için dört adım gereklidir:

1. FileX Hizmetleri veya veri yapıları kullanan tüm uygulama dosyalarına ***fx_api. h*** dosyasını dahil edin.
1. _ *_Tx_application_define_** işlevinden veya bir uygulama iş parçacığından ***Fx_system_initialize** _ çağırarak FileX sistemini başlatın.

    > [!IMPORTANT]
    > Bağımsız modda FileX kullanırken, ***fx_system_initialize*** doğrudan uygulama kodundan çağrılmalıdır.

1. FileX medyasını ayarlamak için ***fx_media_open*** bir veya daha fazla çağrı ekleyin. Bu çağrı, bir uygulama iş parçacığı bağlamından yapılmalıdır.

    > [!IMPORTANT]
    > ***Fx_media_open** çağrısının, verileri bir sektör için depolamak IÇIN yeterli RAM gerektirdiğini unutmayın.*

1. Uygulama kaynağını derleyin ve FileX ve ThreadX çalışma zamanı kitaplıkları, ***FX. a** _ (veya _*_FX. lib_*_) ve _*_TX. a_*_ (veya _ *_TX. lib_* *) ile bağlantı yapın. Elde edilen görüntü hedefe indirilebilir ve yürütülür!

## <a name="troubleshooting"></a>Sorun giderme

Her FileX bağlantı noktası, bir tanıtım uygulamasıyla birlikte dağıtılır. Her zaman, hedef donanımda veya belirli bir demo ortamında, ilk olarak tanıtım sisteminin çalışmasını sağlamak iyi bir fikirdir.

Tanıtım sistemi çalışmazsa, sorunu daraltmak için aşağıdaki şeyleri deneyin:

1. Tanıtım 'in ne kadarının çalıştığını belirleme.
1. Yığın boyutlarını artırın (gerçek uygulama kodunda tanıtım için olduğundan daha önemlidir).
1. 32Kbayt varsayılan RAM disk boyutu için yeterli RAM olduğundan emin olun. Temel sistem çok daha az RAM üzerinde çalışır; Ancak, RAM diskinin daha fazlası kullanıldığında, yeterli bellek yoksa, sorunlar ortaya çıkabilir.
1. Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın. Bu tür bilgiler, Microsoft Destek mühendislerinin yararlı olduğunu kanıtlamaları gerekir. Sorun giderme adımlarından toplanan bilgileri göndermek için "Müşteri Destek Merkezi" bölümünde özetlenen yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

Dosya x kitaplığı ve FileX kullanarak uygulama derlenirken birkaç yapılandırma seçeneği vardır. Aşağıdaki seçenekler uygulama kaynağında, komut satırında veya ***fx_user. h*** içerme dosyası içinde tanımlanabilir.

> [!IMPORTANT]
> ***Fx_user. h** içinde tanımlanan seçenekler yalnızca uygulama ve Threadx kitaplığı, tek başına modda (FX_STANDALONE_ENABLE * tanımlanması gerekir) **FileX kullanılırken _FX_INCLUDE_USER_DEFINE_FILE_* _ Defined._** ile derlenip*, threadx dosyaları/kitaplıkları gerekli değildir.

Aşağıdaki listede her yapılandırma seçeneği ayrıntılı olarak açıklanmaktadır:

|Tanımlayın|Anlamı|
|----------    |-----------|
|FX_MAX_LAST_NAME_LEN        |Bu değer, tam yol adı içeren en büyük dosya adı uzunluğunu tanımlar. Varsayılan olarak, bu değer 256 ' dir.|
|FX_DONT_UPDATE_OPEN_FILES    |Tanımlı, FileX zaten açık olan dosyaları güncelleştirmiyor.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Tanımlı, dosya arama önbelleği iyileştirmesi devre dışı bırakıldı.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Tanımlı, dosya arama önbelleği iyileştirmesi devre dışı bırakıldı.|
|FX_DISABLE_DIRECT_DATA_READ_CACHE_FILL |Tanımlı, önbelleğin doğrudan okuma sektör güncelleştirmesi devre dışı bırakıldı.|
|FX_MEDIA_STATISTICS_DISABLE |Tanımlı, medya istatistiklerinin toplanması devre dışı bırakıldı.|
|FX_SINGLE_OPEN_LEGACY |Aynı dosya için tanımlı, eski tek açık mantık etkindir.|
|FX_RENAME_PATH_INHERIT    |Tanımlanan, yeniden adlandırma yol bilgilerini devralır.|
|FX_DISABLE_ERROR_CHECKING    |Temel FileX hata denetimi API 'sini kaldırır ve gelişmiş performans ile sonuçlanır (%30 ' a kadar) ve daha küçük kod boyutu.|
|FX_MAX_LONG_NAME_LEN    |FileX için maksimum dosya adı boyutunu belirtir. Varsayılan değer 256 ' dir, ancak bu, komut satırı tanımlamaile geçersiz kılınabilir. Geçerli değerler 13 ile 256 arasında değişir.|
|FX_MAX_SECTOR_CACHE|FileX tarafından Önbelleğe alınabilecek mantıksal kesimlerin maksimum sayısını belirtir. Önbelleğe alınabilecek gerçek kesimlerin sayısı, bu sabit değerden daha azdır ve fx_media_open sağlanan bellek miktarına kaç kesim uyadırabilirler. Varsayılan değer 256 ' dir. Tüm değerler 2 ' nin üssü olmalıdır.|
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
