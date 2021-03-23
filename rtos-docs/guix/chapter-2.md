---
title: Bölüm 2-Gux yükleme ve kullanımı
description: Bu bölümde, HighPerformance Kullanıcı arabirimi ürününün Gux ' i yükleme, kurulum ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6527227062fc667b3f527a798d6621914c374c5c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826392"
---
# <a name="chapter-2---installation-and-use-of-guix"></a>Bölüm 2-Gux yükleme ve kullanımı

Bu bölümde, HighPerformance Kullanıcı arabirimi ürününün Gux ' i yükleme, kurulum ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.  

## <a name="host-considerations"></a>Ana bilgisayar konuları

Katıştırılmış Geliştirme genellikle Windows veya Linux (UNIX) ana bilgisayar bilgisayarlarında gerçekleştirilir. Uygulama derlendikten, bağlanır ve çalıştırılabilir dosya konakta üretildikten sonra, yürütme için hedef donanıma indirilir.

Genellikle hedef indirme işlemi geliştirme aracının hata ayıklayıcı içinden yapılır. İndirmeden sonra, hata ayıklayıcı, hedef yürütme denetimi (go, dur, kesme noktası vb.) ve bellek ve işlemci kayıtlarına erişimi sağlamaktan sorumludur.

Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar. OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.

Konakta kullanılan kaynaklar için, GUXI kaynak kodu ASCII biçiminde dağıtılır ve konak bilgisayarın sabit diskinde yaklaşık 30 MB alan gerektirir.

## <a name="target-considerations"></a>Hedef konuları

GUX, hedefte 5 Kbayt ve 80 Kbayt Read-Only bellek (ROM) arasında olmalıdır. GUX iş parçacığı yığını ve diğer genel veri yapıları için hedefin rastgele erişim belleği (RAM) için bir adet 5-10Kbayt gereklidir.

Ayrıca, GUıDX, bir ThreadX süreölçeri ve bir ThreadX mutex nesnesi kullanılmasını gerektirir. Bu tesisler, Gux içinde düzenli işleme ihtiyaçları ve iş parçacığı koruması için kullanılır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS Gux, konumundaki ortak kaynak kodu depomızdan elde edilebilir <https://github.com/azure-rtos/guix/> .

Aşağıda, çoğu ürün dağıtımlarıyla ortak olan önemli dosyaların bir listesi verilmiştir:

| Kısaltın&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Açıklama   |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| gx_api. h        | Bu C üstbilgi dosyası tüm sistem eş, veri yapılarını ve hizmet prototiplerini içerir. |
| gx_port. h       | Bu C üstbilgi dosyası, hedefe özgü ve geliştirme aracına özgü veri tanımlarını ve yapılarını içerir.                                                                                                                                         |
| GX. a (veya GX. lib) | Bu, GUıDX C kitaplığının ikili sürümüdür. Bu, normal olarak, sunulan Gux kitaplık kaynak dosyalarını derleyip arşivleyerek oluşturulur, ancak bu kitaplık, donanım hedefi ve lisans türüne bağlı olarak önceden oluşturulmuş biçimde sağlanmış olabilir. |
|

> [!IMPORTANT]
> *Tüm dosyalar küçük harfli olduğundan, komutların Linux (UNIX) geliştirme platformlarına dönüştürülmesini kolaylaştırır.*

## <a name="guix-installation"></a>GUX yüklemesi

GUIX, GitHub deposu yerel makinenize kopyalanarak yüklenir. Aşağıda, bilgisayarınızda Gux deposunun bir kopyasını oluşturmak için tipik sözdizimi verilmiştir:

```c
    git clone https://github.com/azure-rtos/guix
```

Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında Gux kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.

>[!NOTE]  
> *Uygulama yazılımının, genellikle **GX. a** (veya **GX. lib**) olarak adlandırılan Gux kitaplık dosyasına erişmesi gerekir ve C içerme dosyaları **gx_api. h** ve **gx_port. h**. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaları uygulama geliştirme alanına kopyalayarak gerçekleştirilir.*

## <a name="using-guix"></a>GUX kullanma

GUX kullanmak kolaydır. Temel olarak, uygulama kodu derleme sırasında ***gx_api. h** _ ve Gux Kitaplığı _*_GX. a_*_ (veya _ *_GX. lib_*) * ile bağlantı içermelidir.

Bir Gux uygulaması oluşturmak için gereken dört kolay adım vardır:

| Adımlar   | Açıklama    |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| &nbsp;1. Adım: | ***Gx_api. h*** dosyasını Gux hizmetlerini veya veri yapılarını kullanan tüm uygulama dosyalarına ekleyin.                                                               |
| &nbsp;2. Adım: | _ *_Tx_application_define_** işlevinden veya bir uygulama iş parçacığından ***gx_system_initialize** _ çağırarak Gux sistemini başlatın.                       |
| Adım &nbsp; 3: | Bir görüntü örneği oluşturun, ekran için bir tuval oluşturun ve kök pencereyi ve gereken diğer pencereleri veya pencere öğelerini oluşturun.                                 |
| &nbsp;4. Adım: | GUX çalışma zamanı kitaplığı ***GX. a** _ (veya _ *_GX. lib_* *) ile uygulama kaynağını derleyin ve bağlayın. Elde edilen görüntü hedefe indirilebilir ve yürütülür! |

## <a name="troubleshooting"></a>Sorun giderme

Her bir Gux bağlantı noktası, belirli bir görüntüleme donanımında yürütülen bir tanıtım uygulamasıyla birlikte dağıtılır. Aynı temel tanıtım, Gux 'in tüm sürümleriyle birlikte dağıtılır. Öncelikle tanıtım sisteminin çalıştırılması her zaman iyi bir fikirdir.

Tanıtım sistemi düzgün çalışmıyorsa, sorunu daraltmak için aşağıdaki işlemleri gerçekleştirin:

1. Tanıtım 'in ne kadarının çalıştığını belirleme.

2. Bir derleme zamanı sabiti **GX_THREAD_STACK_SIZE** ve Gux kitaplığını yeniden DERLEYEREK Gux iş parçacığının yığın boyutunu artırın

3. GUX kitaplığını yapılandırma seçeneği bölümünde listelenen uygun hata ayıklama seçenekleriyle yeniden derleyin.

4. Tüm API çağrılarından dönüş durumunu inceleyin.

5. ***_Gx_system_error_process*** işlevde bir kesme noktası ayarlayarak iç sistem hatası olup olmadığını belirleme. Hata kodu ve çağıranın, yanlış gitmeye yönelik ipuçları vermesi gerekir.

6. Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın. Bu tür bilgiler, Microsoft Destek mühendislerinin yararlı olduğunu kanıtlamaları gerekir.

Sorun giderme adımlarından toplanan bilgileri göndermek için "sizin bizim için gerekenler" başlıklı bölümde açıklanan yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

GUX kitaplığı ve Gux kullanarak uygulama oluşturulurken birkaç yapılandırma seçeneği vardır. Bu seçenekler, uygulama gereksinimlerinize en iyi şekilde uyum sağlamak için kitaplık boyutunu ve özellik kümesini ayarlamak için kullanılır. Örneğin, uygulamanızın Gux API hizmetlerinden yalnızca bir iş parçacığı varsa, kritik kod bölümlerinin birden çok iş parçacığı tarafından önceden çıkarılması ile ilişkili ek yükü ortadan kaldırmak için **GX_DISABLE_MULTITHREAD_SUPPORT** yapılandırma bayrağı tanımlanmalıdır. Çeşitli yapılandırma bayrakları uygulama kaynağında, komut satırında veya **_gx_user. h_** içerme dosyası içinde tanımlanabilir.

GUX kitaplık yapılandırma bayrakları her değiştirildiğinde, yapılandırma değişikliklerinin etkili olabilmesi için hem Gux kitaplığını hem de uygulama modüllerinizi yeniden oluşturmanız gerekir.

Yapılandırma bayraklarının tüm listesi Ek H: GUIX Build-Time yapılandırma bayraklarıyla belgelenmiştir.

## <a name="guix-version-id"></a>GUX sürüm KIMLIĞI

Geçerli Gux sürümü çalışma zamanı sırasında hem Kullanıcı hem de uygulama yazılımı için kullanılabilir. Programcı, "**gx_port. h** _ dosyasının INCEAĞıNDAN Gux sürümünü alabilir. Ayrıca, bu dosya Ayrıca karşılık gelen bağlantı noktası uygulama yazılımının bir sürüm geçmişini içerir _ *_gx_port. h_* * içindeki genel dizeyi _ *_ _gx_version_id_* _ ' i inceleyerek, guıdx sürümünü alabilir.

Uygulama yazılımı ayrıca, ***gx_api. h** içinde tanımlanan sabitlerden gelen sürüm bilgilerini de alabilir. * Bu sabitler, geçerli ürün sürümünü ada ve ürünün birincil ve ikincil sürümüne göre belirler.

```C
#define __PRODUCT_GUIX__

#define __GUIX_MAJOR_VERSION__

#define __GUIX_MINOR_VERSION__
```
