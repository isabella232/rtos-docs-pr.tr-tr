---
title: Bölüm 2-Azure RTOS NetX Duo yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX Duo yüksek performanslı ağ yığınının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 457eca2144bb0cba7cae63aa007e9cb658bbcd96
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827029"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo"></a>Bölüm 2-Azure RTOS NetX Duo yüklemesi ve kullanımı

Bu bölümde, aşağıdakiler de dahil olmak üzere yüksek performanslı ağ yığınının Azure RTOS NetX Duo 'i yükleme, kurulum ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır: 

## <a name="host-considerations"></a>Ana bilgisayar konuları

Katıştırılmış Geliştirme genellikle Windows veya Linux (UNIX) ana bilgisayar bilgisayarlarında gerçekleştirilir. Uygulama derlendikten, bağlanır ve çalıştırılabilir dosya konakta üretildikten sonra, yürütme için hedef donanıma indirilir.

Genellikle hedef indirme işlemi geliştirme aracının hata ayıklayıcı içinden yapılır. İndirmeden sonra, hata ayıklayıcı, hedef yürütme denetimi (go, dur, kesme noktası vb.) ve bellek ve işlemci kayıtlarına erişimi sağlamaktan sorumludur.

Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar. OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.

Konakta kullanılan kaynaklar için, NetX Duo kaynak kodu ASCII biçiminde dağıtılır ve ana bilgisayarın sabit diskinde yaklaşık 1 MB boş alan gerektirir.

## <a name="target-considerations"></a>Hedef konuları

NetX Duo, hedefte 5 Kbayt ve 45 Kbayt Read-Only bellek (ROM) arasında olmalıdır. NetX Duo iş parçacığı yığını ve diğer genel veri yapıları için hedefin rastgele erişim belleği (RAM) için bir adet 1-5 KB gerekir.

Ayrıca NetX Duo, iki ThreadX Zamanlayıcı nesnesinin ve bir ThreadX mutex nesnesinin kullanılmasını gerektirir. Bu tesisler, NetX Duo protokol yığını içinde düzenli işleme ihtiyaçları ve iş parçacığı koruması için kullanılır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX Duo, konumundaki ortak kaynak kodu deposundan elde edilebilir <https://github.com/azure-rtos/netxduo/> .

Depodaki birçok önemli dosyanın listesi aşağıda verilmiştir:

**nx_api. h**  
Tüm sistem eşlerini, veri yapılarını ve hizmet prototiplerini içeren C üstbilgi dosyası.

**nx_port. h** Tüm geliştirme araçlarını ve targetspecific veri tanımlarını ve yapılarını içeren C üstbilgi dosyası. 

**demo_netx. c** Küçük bir demo uygulaması içeren C dosyası.

**NX. a (veya NX. lib)**  
Standart paketiyle dağıtılan NetX C kitaplığının ikili sürümü.

## <a name="netx-duo-installation"></a>NetX Duo yüklemesi

NetX Duo, GitHub deposu yerel makinenize kopyalanarak yüklenir. Bilgisayarınızda NetX Duo deposunun bir kopyasını oluşturmak için tipik sözdizimi aşağıda verilmiştir:

```c
    git clone https://github.com/azure-rtos/netxduo
```

Alternatif olarak, GitHub ana sayfasında İndir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında NetX Duo kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.

> [!IMPORTANT]
> *Uygulama yazılımının NetX Duo kitaplık dosyasına (genellikle **NX. a** veya **NX. lib**) ve C içerme dosyalarına **nx_api. h ve nx_port. h** erişimi olması gerekir. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaları uygulama geliştirme alanına kopyalayarak gerçekleştirilir.*

## <a name="using-netx-duo"></a>NetX Duo kullanma

NetX Duo kullanmak kolaydır. Temel olarak, uygulama kodu derleme sırasında ***nx_api. h** _ Içermeli ve NETX Duo Kitaplığı _*_NX. a_*_ (veya _ *_NX. lib_*) * ile bağlantı içermelidir.

NetX Duo uygulaması oluşturmak için gereken dört kolay adım aşağıda verilmiştir:

[!div class="mx-tdCol2BreakAll"]
| Adım  | Açıklama  |
|---|---|
|&nbsp;1. Adım: |NetX Duo Hizmetleri veya veri yapıları kullanan tüm uygulama dosyalarına ***nx_api. h*** dosyasını dahil edin.|
|&nbsp;2. Adım: |_ *_Tx_application_define_** işlevinden veya bir uygulama iş parçacığından ***Nx_system_initialize** _ çağırarak NETX Duo sistemini başlatın.|
|Adım &nbsp; 3: |Bir IP örneği oluşturun, gerekirse Adres Çözümleme Protokolü 'Nü (ARP) ve ***nx_system_initialize*** sonra tüm yuvaları etkinleştirin.|
|&nbsp;4. Adım: |Uygulama kaynağını derleyin ve NetX Duo çalışma zamanı kitaplığıyla bağlayın ***NX. a** _ (veya _ *_NX. lib_* *). Elde edilen görüntü hedefe indirilebilir ve yürütülür!|

## <a name="troubleshooting"></a>Sorun giderme

Her NetX Duo bağlantı noktası, gerçek bir ağ üzerinde veya sanal ağ sürücüsü aracılığıyla yürütülen bir veya daha fazla gösterimle birlikte dağıtılır. Öncelikle tanıtım sisteminin çalıştırılması her zaman iyi bir fikirdir.

Tanıtım sistemi düzgün çalışmıyorsa, sorunu daraltmak için aşağıdaki işlemleri gerçekleştirin:

1. Tanıtım 'in ne kadarının çalıştığını belirleme.
2. Yeni uygulama iş parçacıklarında yığın boyutlarını artırın.
3. NetX Duo kitaplığını yapılandırma seçeneği bölümünde listelenen uygun hata ayıklama seçenekleriyle yeniden derleyin.
4. Paketlerin gönderilip gönderilmediğini veya alındığını görmek için NX_IP yapısını inceleyin.
5. Kullanılabilir paketlerin olup olmadığını görmek için varsayılan paket havuzunu inceleyin.
6. Ağ sürücüsünün, IPv4 veya IPv6 bağlantısı gerektiren uygulamalar için 4 baytlık sınırlardaki üst bilgilerini içeren ARP ve IP paketleri sağladığı emin olun.
7. Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın. Bu tür bilgiler, Microsoft Destek mühendislerinin yararlı olduğunu kanıtlamaları gerekir.

Sorun giderme adımlarından toplanan bilgileri göndermek için sayfa 12 ' de "sizin bizim için gerekenler" bölümünde özetlenen yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NETX Duo kitaplığı ve NetX Duo kullanan uygulamayı oluştururken birkaç yapılandırma seçeneği vardır. Yapılandırma seçenekleri, aksi belirtilmedikçe, uygulama kaynağında, komut satırında veya ***nx_user. h*** içerme dosyası içinde tanımlanabilir.

> [!NOTE]
> ***Nx_user. h** içinde tanımlanan seçenekler, yalnızca uygulama ve NETX Duo kitaplığı, tanımlı NX_INCLUDE_USER_DEFINE_FILE ile derlenme durumunda uygulanır* . * 

Aşağıdaki bölümlerde NetX Duo 'da kullanılabilen yapılandırma seçenekleri listelenmektedir. Hem IPv4 hem de IPv6 için geçerli olan genel seçenekler önce, ardından IPv6 'ya özgü seçenekler tarafından listelenir.

### <a name="system-configuration-options"></a>Sistem yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
| NX_ASSERT_FAIL    | Bir onaylama başarısız olduğunda kullanılacak hata ayıklama ifadesini tanımlayan simge.                               |
| NX_DEBUG           | Tanımlı, RAM Ethernet ağ sürücüsünden kullanılabilen isteğe bağlı yazdırma hata ayıklama bilgilerini sunar. |
| NX_DEBUG_PACKET   | , İsteğe bağlı hata ayıklama paketi dökümünü RAM Ethernet ağ sürücüsünde kullanılabilir olarak sunar.      |
| NX_DISABLE_ASSERT | Tanımlı, kaynak koddaki onay denetimlerini devre dışı bırakır. Varsayılan olarak bu seçenek tanımlı değildir.            |
|NX_DISABLE_ERROR_CHECKING | Tanımlanmıştır, temel NetX Duo hata denetimi API 'sini kaldırır ve performansı geliştirir. Hata denetimini devre dışı bırakarak etkilenmeyen API dönüş kodları, API tanımında kalın yazı tipiyle listelenmiştir. Bu tanımlama genellikle uygulamanın yeterince hata ayıklaması yapıldıktan ve kullanımı performansı artırdığında ve kod boyutunu azalttığında kullanılır.|
|NX_DRIVER_DEFERRED_PROCESSING | Tanımlı, ertelenmiş ağ sürücüsü paket işleme etkinleştirilir. Bu, ağ sürücüsünün IP örneğine bir paket yerleştirmesini ve NetX Duo iç IP Yardımcısı iş parçacığından, gerçek işleme yordamının çağrılmasına izin verir.|
|NX_DUAL_PACKET_POOL_ENABLE | ***NX_ENABLE_DUAL_PACKET_POOL** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ENABLE_DUAL_PACKET_POOL_* * kullanması önerilir.|
|NX_ENABLE_DUAL_PACKET_POOL | Tanımlı, yığının büyük yük boyutu ve diğeri daha küçük yük boyutuyla iki paket havuzu kullanmasına izin verir. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_EXTENDED_NOTIFY_SUPPORT| Tanımlı, yığında daha fazla geri çağırma kancaları sunar. Bu geri çağırma işlevleri, BSD sarmalayıcı katmanı tarafından kullanılır. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_ENABLE_INTERFACE_CAPABILITY| Tanımlı, arabirim aygıt sürücüsünün sağlama toplamı yükleme gibi ek yetenek bilgileri belirtmesini sağlar. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_ENABLE_SOURCE_ADDRESS_CHECK| Tanımlı, gelen paketin kaynak adresinin denetlenmesini sağlar. Varsayılan olarak bu seçenek devre dışıdır.|
| NX_IPSEC_ENABLE  | Tanımlı, IPSec işlemlerini desteklemek için NetX Duo kitaplığını sağlar. Bu özellik isteğe bağlı NetX Duo IPSec modülünü gerektirir. Bu özellik varsayılan olarak etkin değildir.            |
| NX_LITTLE_ENDIAN | Tanımlı, protokol üstbilgilerinin doğru big endian biçimde olduğundan emin olmak için little endian ortamlarında gerekli bayt takas işlemini gerçekleştirir. Varsayılan değer genellikle ***nx_port. h***' de kurulumlardır.|
|NX_MAX_PHYSICAL_INTERFACES | Cihazdaki toplam fiziksel ağ arabirimi sayısını belirtir. Varsayılan değer 1 ' dir ve ***nx_api. h***; içinde tanımlanmıştır bir cihazın en az bir fiziksel arabirimi olmalıdır. Not geri döngü arabirimini içermez.|
| NX_NAT_ENABLE | Tanımlanan NetX Duo, NAT işlemi ile oluşturulmuştur. Varsayılan olarak bu seçenek tanımlı değildir.|
| NX_PHYSICAL_HEADER  | Çerçevenin fiziksel üstbilgisinin boyutunu bayt cinsinden belirtir. Varsayılan değer 16 ' dır (32 bitlik sınıra hizalanmış tipik bir 14 baytlık Ethernet çerçevesine göre) ve ***nx_api. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_user. h_*. * gibi _*_nx_api. h_*_ dahil etmeden önce değeri tanımlayarak varsayılanı geçersiz kılabilir. |
| NX_PHYSICAL_TRAILER | Fiziksel paket artbilgisi boyutunu bayt cinsinden belirtir ve genellikle, Ethernet CRCs gibi şeyler için depolama alanı ayırmak için kullanılır. Varsayılan değer 4 ' dir ve ***nx_api. h***' de tanımlanmıştır.|

### <a name="arp-configuration-options"></a>ARP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_ARP_DEFEND_BY_REPLY | Tanımlı, NetX Duo 'un IP adresini bir ARP yanıtı göndererek savunmasına olanak tanır.|
|NX_ARP_DEFEND_INTERVAL| , Saniye cinsinden, ARP modülünün bir gelen ARP iletisine yanıt olarak bir sonraki savunı paketini gönderdiği bir adresi, çakışmanın bir adres olduğunu belirten bir şekilde tanımlar.|
|NX_ARP_DISABLE_AUTO_ARP_ENTRY|  ***NX_DISABLE_ARP_AUTO_ENTRY** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ARP_AUTO_ENTRY_* * kullanması önerilir.|
|NX_ARP_EXPIRATION_RATE| ARP girişlerinin geçerli kaldığı saniye sayısını belirtir. Varsayılan sıfır değeri, ARP girdilerinin süre sonunu veya eskime süresini devre dışı bırakır ve ***nx_api. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_ARP_MAC_CHANGE_NOTIFICATION_ENABLE | ***NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION_* * kullanması önerilir.|
|NX_ARP_MAX_QUEUE_DEPTH | Bir ARP yanıtı beklenirken sıraya alınabilen en fazla paket sayısını belirtir. Varsayılan değer 4 ' dir ve ***nx_api. h***' de tanımlanmıştır.|
|NX_ARP_MAXIMUM_RETRIES | ARP yanıtı olmadan gerçekleştirilen en fazla ARP yeniden deneme sayısını belirtir. Varsayılan değer 18 ' dir ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_ARP_UPDATE_RATE | ARP yeniden denemeleri arasındaki saniye sayısını belirtir. Varsayılan değer 10 saniye temsil eden 10 ' dur ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_DISABLE_ARP_AUTO_ENTRY | Tanımlı, ARP istek bilgilerini ARP önbelleğinde girmeyi devre dışı bırakır.|
|NX_DISABLE_ARP_INFO | Tanımlı, ARP bilgi toplamayı devre dışı bırakır.|
|NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION| Tanımlı, ARP 'nin MAC adresini algılama üzerinde bir geri çağırma bildirim işlevi çağırmasına izin verir.|

### <a name="icmp-configuration-options"></a>ICMP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_ICMP_INFO| Tanımlı, ıCMP bilgi toplamayı devre dışı bırakır.|
|NX_DISABLE_ICMP_RX_CHECKSUM| Tanımlı, alınan ıCMP paketlerinde hem Icmpv4 hem de ICMPv6 sağlama toplamı hesaplamasını devre dışı bırakır. Bu seçenek, ağ arabirimi sürücüsü Icmpv4 ve ICMPv6 sağlama toplamını doğrulayabilip, uygulamanın IP parçalanma özelliğini veya IPSec özelliğini kullanmayan durumlarda faydalıdır. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_DISABLE_ICMP_TX_CHECKSUM | Tanımlı, iletilen ıCMP paketlerinde hem Icmpv4 hem de ICMPv6 sağlama toplamı hesaplamasını devre dışı bırakır. Bu seçenek, ağ arabirimi sürücüsünün Icmpv4 ve ICMPv6 sağlama toplamını hesaplarken faydalıdır.
ve uygulama, IP parçalama özelliğini veya IPSec özelliğini kullanmaz. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_DISABLE_ICMPV4_ERROR_MESSAGE | Tanımlanan NetX Duo, hatalı biçimli IPv4 üst bilgisi gibi hata koşullarına yanıt olarak Icmpv4 hata Iletileri göndermez. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_DISABLE_ICMPV4_RX_CHECKSUM | Tanımlı, alınan ıCMP paketlerinde Icmpv4 sağlama toplamı hesaplamasını devre dışı bırakır. ***NX_DISABLE_ICMP_RX_CHECKSUM*** tanımlanmışsa Bu seçenek otomatik olarak tanımlanır. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_DISABLE_ICMPv4_RX_CHECKSUM | ***NX_DISABLE_ICMPV4_RX_CHECKSUM** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ICMPV4_RX_CHECKSUM_* * kullanması önerilir.|
|NX_DISABLE_ICMPV4_TX_CHECKSUM | Tanımlı, iletilen ıCMP paketlerinde Icmpv4 sağlama toplamı hesaplamasını devre dışı bırakır. ***NX_DISABLE_ICMP_TX_CHECKSUM*** tanımlanmışsa Bu seçenek otomatik olarak tanımlanır. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_DISABLE_ICMPv4_TX_CHECKSUM | ***NX_DISABLE_ICMPV4_TX_CHECKSUM** _ olarak yeniden adlandırıldı.</br>Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ICMPV4_TX_CHECKSUM_* * kullanması önerilir.|
|NX_ENABLE_ICMP_ADDRESS_CHECK | Tanımlı, ıCMP paketinin hedef adresi denetlenir. Varsayılan olarak devre dışı seçeneği kullanılır. Bir IP yayınını veya IP çok noktaya yayın adresini hedefleyen bir ıCMP yankı Isteği sessizce atılır.|

### <a name="igmp-configuration-options"></a>IGMP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_IGMP_INFO | Tanımlı, ıGMP bilgi toplamayı devre dışı bırakır.|
|NX_DISABLE_IGMPV2 | Tanımlı, IGMPv2 desteğini devre dışı bırakır ve NetX Duo yalnızca IGMPv1 destekler. Varsayılan olarak bu seçenek ayarlı değildir ve ***nx_api. h***' de tanımlanmıştır.|
|NX_MAX_MULTICAST_GROUPS | Birleştirilebilecek en fazla çok noktaya yayın grubu sayısını belirtir. Varsayılan değer 7 ' dir ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|

### <a name="ip-configuration-options"></a>IP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_FRAGMENTATION | Tanımlı, hem IPv4 hem de IPv6 parçalanması ve yeniden birleştirme mantığını devre dışı bırakır.|
| NX_DISABLE_IPV4     | Tanımlı, IPv4 işlevini devre dışı bırakır. Bu seçenek, yalnızca suupport IPv6 'ya NetX Duo oluşturmak için kullanılabilir. Varsayılan olarak bu seçenek tanımlı değildir. |
| NX_DISABLE_IP_INFO | Tanımlı, IP bilgilerini toplamayı devre dışı bırakır.|
|NX_DISABLE_IP_RX_CHECKSUM | Tanımlı, alınan IPv4 paketlerinde sağlama toplamı mantığını devre dışı bırakır. Bu, ağ aygıtı IPv4 sağlama toplamını doğrulayabildiğinde ve uygulamanın IP parçalama veya IPSec kullanımını beklemediğinde yararlı olur.|
|NX_DISABLE_IP_TX_CHECKSUM | Tanımlı, gönderilen IPv4 paketlerindeki sağlama toplamı mantığını devre dışı bırakır. Bu, temel alınan ağ cihazının IPv4 üst bilgisi sağlama toplamı oluşturma yeteneğine sahip olduğu ve uygulamanın IP parçalama veya IPSec kullanımını beklemediği durumlarda faydalıdır.|
|NX_DISABLE_LOOPBACK_INTERFACE | Tanımlı, geri döngü arabirimi için NetX Duo desteğini devre dışı bırakır.|
|NX_DISABLE_RX_SIZE_CHECKING | Tanımlı, alınan paketlerin boyut denetimini devre dışı bırakır.|
|NX_ENABLE_IP_RAW_PACKET_FILTER | Tanımlı, IP ham paket alma filtresi işlevlerini sunar. Alınacak ham IP paketlerinin türü üzerinde daha fazla denetim gerektiren uygulamalar, bu özelliği kullanabilir. IP ham paket filtresi özelliği, BSD uyumluluk katmanındaki Ham yuva işlemini de destekler. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_ENABLE_IP_STATIC_ROUTING | Tanımlı, bir hedef adrese belirli bir sonraki atlama adresi atanabileceği IPv4 statik yönlendirmeye izin vermez. Varsayılan olarak IPv4 statik yönlendirmesi devre dışıdır.|
|NX_FRAGMENT_IMMEDIATE_ASSEMBLY | Tanımlı, IPv4 ve IPv6 yeniden birleştirme mantığının bir IP parçası aldıktan sonra hemen yürütülmesi için izin verir. Varsayılan olarak bu seçenek tanımlı değildir.|
|NX_IP_MAX_REASSEMBLY_TIME | IPv4 parçasını ve IPv6 parçasını yeniden birleştirmek için izin verilen en uzun süreyi denetleyen simge. Burada tanımlanan değer hem ***NX_IPV4_MAX_REASSEMBLY_TIME** _ hem de _ *_NX_IPV6_MAX_REASSEMBLY_TIME_* * üzerine yazar.|
|NX_IP_PERIODIC_RATE | Tanımlı, bir saniye içinde ThreadX süreölçer onay işareti sayısını belirtir. Varsayılan değer, ThreadX symbol ***TX_TIMER_TICKS_PER_SECOND** türetilir. Bu, varsayılan olarak 100 (10ms zamanlayıcı) olarak ayarlanmıştır. NetX Duo modüllerinin geri kalanı _ NX_IP_PERIODIC_RATE 'tan zamanlama bilgilerini türetecağından uygulamalar bu değeri değiştirirken dikkatli olacaktır *.**|
|NX_IP_RAW_MAX_QUEUE_DEPTH | Ham paket alma kuyruğunda, ham IP paketlerinin sayısını denetleyen simge kuyruğa alınabilir. Varsayılan olarak, değeri 20 olarak ayarlanır.| 
|NX_IP_ROUTING_TABLE_SIZE | Tanımlı, bir giden arabirimin listesi olan IPv4 statik yönlendirme tablosundaki en fazla giriş sayısını ve belirli bir hedef adres için sonraki atlama adreslerini ayarlar. Varsayılan değer 8 ' dir ve ***nx_api. h** ' de tanımlanmıştır. _ Bu sembol yalnızca _ *_NX_ENABLE_IP_STATIC_ROUTING_** tanımlanmışsa kullanılır.|
|NX_IPV4_MAX_REASSEMBLY_TIME | IPv4 parçasını yeniden ayırma için izin verilen en uzun süreyi denetleyen simge. Aklınızda NX_IP_MAX_REASSEMBLY_TIME tanımlanan değer bu değerin üzerine yazılır.|

### <a name="packet-configuration-options"></a>Paket yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_PACKET_CHAIN | Tanımlı, paket zinciri mantığını devre dışı bırakır. Bu, varsayılan olarak tanımlı değildir.|
|NX_DISABLE_PACKET_INFO | Tanımlı, paket havuzu bilgileri toplamayı devre dışı bırakır.|
|NX_ENABLE_LOW_WATERMARK | Tanımlı, NetX Duo paket havuzu düşük filigran özelliğini etkinleştiriyor. Uygulama, düşük filigran değeri ayarlar. TCP paketleri alındığında, paket havuzuna düşük filigrana ulaşıldığında NetX Duo bu paketi serbest bırakarak sessizce atar ve paket havuzunun devam etmesini önler. Bu özellik varsayılan olarak etkin değildir.|
|NX_ENABLE_PACKET_DEBUG_INFO | Tanımlı, paket hata ayıklama bilgilerini günlüğe kaydeder.|
|NX_PACKET_ALIGNMENT | Tanımlı, paket yük alanının başlangıç adresi için bayt cinsinden hizalama gereksinimini belirtir. Bu seçenek, ***NX_PACKET_HEADER_PAD** _ ve _ *_NX_PACKET_HEADER_PAD_SIZE_* * ' i kullanımdan kaldırır. Varsayılan olarak, bu seçenek 4 olacak şekilde tanımlanır ve yük alanının başlangıç adresini 4 bayt hizalı olarak yapar.|
|NX_PACKET_HEADER_PAD | Tanımlı, NX_PACKET denetim bloğunun sonuna doğru doldurma imkanı sunar. Panel için ULONG sözcüklerinin sayısı ***NX_PACKET_HEADER_PAD_SIZE** _ tarafından tanımlanır. Bu seçenek _ *_NX_PACKET_ALIGNMENT_* * tarafından amorti edilir.|
|NX_PACKET_HEADER_PAD_SIZE | NX_PACKET yapısına eklenecek ULONG sözcüklerinin sayısını ayarlar ve paket yükü alanının istenen hizalamadan başlatılmasına izin verir. Bu özellik, arabellek tanımlayıcıları alma işlemini doğrudan NX_PACKET yük alanına eklemek ve ağ arabirimi alma mantığı veya önbellek işlemi mantığı, arabellek başlangıç adresinin belirli hizalama gereksinimlerini karşılamasını bekler. Bu değer yalnızca ***NX_PACKET_HEADER_PAD** _ tanımlandığında geçerli olur. Bu seçenek _ *_NX_PACKET_ALIGNMENT_* * tarafından kullanım dışı bırakılmıştır.|

### <a name="rarp-configuration-options"></a>RARP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_RARP_INFO | Tanımlı, RARP bilgi toplamayı devre dışı bırakır.|

### <a name="tcp-configuration-options"></a>TCP yapılandırma seçenekleri

| Seçenek | Açıklama |
|---|---|
|NX_DISABLE_RESET_DISCONNECT | Tanımlanan zaman aşımı değeri ***NX_NO_WAIT*** olarak belirtildiğinde, bağlantı kesme sırasında sıfırlama işlemini devre dışı bırakır.|
|NX_DISABLE_TCP_INFO | Tanımlı, TCP bilgi toplamayı devre dışı bırakır.|
|NX_DISABLE_TCP_RX_CHECKSUM | Tanımlı, alınan TCP paketlerinde sağlama toplamı mantığını devre dışı bırakır. Bu yalnızca bağlantı katmanının güvenilir sağlama toplamı veya CRC işleme sahip olduğu durumlarda veya arabirim sürücüsünün donanımda TCP sağlama toplamını doğrulayabileceği ve uygulamanın IPSec kullanmadığı durumlarda faydalıdır.|
|NX_DISABLE_TCP_TX_CHECKSUM | Tanımlı, TCP paketleri göndermek için sağlama toplamı mantığını devre dışı bırakır. Bu yalnızca, alıcı ağ düğümünde TCP sağlama toplamı mantığını devre dışı bırakılan veya temel alınan ağ sürücüsünün TCP sağlama toplamını oluşturma yeteneğine sahip olduğu ve uygulamanın IPSec kullanmadığı durumlarda faydalıdır.|
|NX_ENABLE_TCP_KEEPALIVE | Tanımlı, isteğe bağlı TCP KeepAlive zamanlayıcısını sunar. Varsayılan ayarlar etkin değil.|
|NX_ENABLE_TCP_MSS_CHECK | Tanımlı, bir TCP bağlantısını kabul etmeden önce en düşük eş ağın doğrulanmasını mümkün. Bu özelliği kullanmak için sembol ***NX_ENABLE_TCP_MSS_MINIMUM*** tanımlanmalıdır. Varsayılan olarak, bu seçenek etkin değildir.|
|NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY| Tanımlı, uygulamanın TCP iletim sırası derinliği artık maksimum değer olmadığında çağrılan bir geri arama işlevini yüklemesine izin verir. Bu geri arama, TCP yuvasının daha fazla veri aktarmaya hazırlandığını belirten bir bildirim görevi görür. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_TCP_WINDOW_SCALING | TCP uygulamaları için pencere ölçeklendirme seçeneğini sunar. Tanımlı ise, TCP bağlantı aşamasında pencere ölçekleme seçeneği görüşülür ve uygulama 64 ' ten büyük bir pencere boyutu belirtebilir. Varsayılan ayar etkin değil (tanımlı değil).|
|NX_MAX_LISTEN_REQUESTS | Maksimum sunucu dinleme isteği sayısını belirtir. Varsayılan değer 10 ' dur ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_ACK_EVERY_N_PACKETS | ACK gönderilmeden önce alacak olan TCP paketlerinin sayısını belirtir. Not ***NX_TCP_IMMEDIATE_ACK** _ etkinse ancak _ *_NX_TCP_ACK_EVERY_N_PACKETS_** yoksa, bu değer geriye dönük uyumluluk için otomatik olarak 1 ' e ayarlanır.|
|NX_TCP_ACK_TIMER_RATE | TCP Gecikmeli onay işleme için süreölçer oranını hesaplamak üzere sistem işaretleri (NX_IP_PERIODIC_RATE) sayısının nasıl bölüneceğini belirtir. Varsayılan değer, 200ms 'yi temsil eden 5 ' tir ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_ENABLE_KEEPALIVE | ***NX_ENABLE_TCP_KEEPALIVE** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ENABLE_TCP_KEEPALIVE_* * kullanması önerilir.|
|NX_TCP_ENABLE_MSS_CHECK | ***NX_ENABLE_TCP_MSS_CHECK** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ NX_ENABLE_TCP_MSS_CHECK kullanması önerilir *_._**|
|NX_TCP_ENABLE_WINDOW_SCALING | ***NX_ENABLE_TCP_WINDOW_SCALING** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ENABLE_TCP_WINDOW_SCALING_* * kullanması önerilir.|
|NX_TCP_FAST_TIMER_RATE | NetX Duo iç onay işareti (NX_IP_PERIODIC_RATE) sayısının hızlı TCP Zamanlayıcı hızını hesaplamak için nasıl bölüneceğini belirtir. Hızlı TCP süreölçeri, Gecikmeli onay süreölçeri dahil olmak üzere çeşitli TCP zamanlayıcılarını sağlamak için kullanılır. Varsayılan değer 10 ' dur ve ThreadX zamanlayıcısının 10ms 'de çalıştığı varsayılarak 100 ms 'yi temsil eder. Bu değer ***nx_tcp. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_IMMEDIATE_ACK| Tanımlı, isteğe bağlı TCP anında BILDIRIM yanıtı işlemesini mümkün bir şekilde sunar. Bu sembolün tanımlanması  ***NX_TCP_ACK_EVERY_N_PACKETS*** 1 olarak tanımlanmasıyla eşdeğerdir.|
|NX_TCP_KEEPALIVE_INITIAL | KeepAlive süreölçeri etkinleşmeden önce geçen işlem yapılmayan saniye sayısını belirtir. Varsayılan değer, 2 saati temsil eden 7200 ' dir ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_KEEPALIVE_RETRIES | Bağlantının bozuk olması için kaç tane canlı tutma yeniden denemeye izin verileceğini belirtir. Varsayılan değer 10 yeniden denemeyi temsil eden 10 ' dur ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_KEEPALIVE_RETRY | Canlı tutma zamanlayıcısında bağlantının diğer tarafının yanıt vermediğini varsayarak geçen saniye sayısını belirtir. Varsayılan değer, yeniden denemeler arasındaki 75 saniyeyi temsil eden 75 ' dir ve ***nx_tcp. h** _ içinde tanımlanır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_MAX_OUT_OF_ORDER_PACKETS | TCP yuvası alma kuyruğunda en fazla sıralı TCP paketi sayısını tanımlayan simge. Bu simge, TCP alma yuvasında sıraya alınmış paketlerin sayısını sınırlandırmak için kullanılabilir ve paket havuzunun başlatılmasını önler. Varsayılan olarak, bu simge tanımlı değildir, bu nedenle TCP yuvasında sırada sıraya alınan paketlerin sayısı için bir sınır yoktur.|
|NX_TCP_MAXIMUM_RETRIES | Bağlantının bozuk olması için kaç veri aktarımı yeniden denenmesine izin verileceğini belirtir. Varsayılan değer 10 yeniden denemeyi temsil eden 10 ' dur ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_MAXIMUM_RX_QUEUE | TCP yuvaları için en fazla alma sırasını tanımlayan simge. Bu özellik ***NX_ENABLE_LOW_WATERMARK*** tarafından etkinleştirilir.|
|NX_TCP_MAXIMUM_TX_QUEUE | TCP gönderme istekleri askıya alınmadan veya reddedilmeden önce TCP iletme sırasının en yüksek derinliğini belirtir. Varsayılan değer 20 ' dir ve bu, en fazla 20 paketin belirli bir zamanda iletme kuyruğunda olabileceği anlamına gelir. Paket verilerinin bir kısmını veya tümünü içeren bir ACK bağlantının diğer tarafından alınana kadar, paket paketleri iletme sırasında kalır. Bu sabit, ***nx_tcp. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_MSS_MINIMUM | NetX Duo TCP modülünün kabul ettiği minimum en düşük, değeri tanımlayan simge. Bu özellik ***NX_ENABLE_TCP_MSS_CHECK*** tarafından etkinleştirilir.|
|NX_TCP_QUEUE_DEPTH_UPDATE_NOTIFY_ENABLE | ***NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY_* * kullanması önerilir.|
|NX_TCP_RETRY_SHIFT | Yeniden aktarım zaman aşımı süresinin yeniden denemeler arasındaki değişiklik şeklini belirtir. Bu değer 0 ise, ilk yeniden aktarım zaman aşımı sonraki yeniden aktarım zaman aşımları ile aynıdır. Bu değer 1 ise, art arda yapılan her yeniden aktarım uzun olur. Bu değer 2 ise, sonraki her yeniden aktarım zaman aşımı süresi dört kez olur. Varsayılan değer 0 ' dır ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|
|NX_TCP_TRANSMIT_TIMER_RATE | TCP iletme yeniden deneme işleminin Zamanlayıcı oranını hesaplamak için sistem işaretleri (***NX_IP_PERIODIC_RATE** _) sayısının nasıl bölüneceğini belirtir. Varsayılan değer 1 ' dir ve _*_nx_tcp. h_*_ içinde tanımlanır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.|

### <a name="udp-configuration-options"></a>UDP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_UDP_INFO | Tanımlı, UDP bilgi toplamayı devre dışı bırakır.|
|NX_DISABLE_UDP_RX_CHECKSUM | Tanımlı, gelen UDP paketlerindeki UDP sağlama toplamı hesaplamasını devre dışı bırakır. Bu, ağ arabirimi sürücüsü donanımdaki UDP üst bilgi sağlama toplamını doğrulayabiliyor ve uygulama IPSec veya IP parçalama mantığını etkinleştirmezse yararlı olur.|
|NX_DISABLE_UDP_TX_CHECKSUM | Tanımlı, giden UDP paketlerinde UDP sağlama toplamı hesaplamasını devre dışı bırakır. Bu, ağ arabirimi sürücüsü UDP üst bilgisi sağlama toplamını hesaplarken ve verileri iletmeden önce IP başlığına değer eklerken kullanışlıdır ve uygulama IPSec veya IP parçalama mantığını etkinleştirmez.|

### <a name="ipv6-options"></a>IPv6 seçenekleri  

| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_IPV6 | NetX Duo kitaplığı yapılandırıldığında IPv6 işlevselliğini devre dışı bırakır. IPv6 gerektirmeyen uygulamalarda, bu, kodun ve IPv6 'Yı desteklemek için gereken ek depolama alanının çekmesini önler.|
|NX_DISABLE_IPV6_PATH_MTU_DISCOVERY | Tanımlı, NetX Duo ana bilgisayar hedef tablosundaki bir hedefin yolundaki en büyük MTU değerini belirlemede kullanılan yol MTU bulmayı devre dışı bırakır. Bu, NetX Duo ana bilgisayarının parçalanma gerektirmeyen mümkün olan en büyük paketi göndermesini sağlar. Varsayılan olarak, bu seçenek tanımlanmıştır (yol MTU devre dışı).|
|NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY | Tanımlı, IPv6 adresi değiştirildiğinde bir geri çağırma işlevinin çağrılmasına izin verir. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_IPV6_MULTICAST | Tanımlı, IPv6 çok noktaya yayın JOIN/Leave işlevini etkinleştir. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_IPV6_PATH_MTU_DISCOVERY | Tanımlı, IPv6 yolu MTU Keşfi özelliğini sunar. Varsayılan olarak bu seçenek etkin değildir.|
|NX_IPV6_ADDRESS_CHANGE_NOTIFY_ENABLE | ***NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY_* * kullanması önerilir.|
|NX_IPV6_DEFAULT_ROUTER_TABLE_SIZE | IPv6 yönlendirme tablosundaki giriş sayısını belirtir. Varsayılan yönlendirici için en az onS girişi gerekir. ***Nx_api. h*** içinde tanımlanan varsayılan değer 8 ' dir.|
|NX_IPV6_DESTINATION_TABLE_SIZE | IPv6 hedef tablosundaki giriş sayısını belirtir. Bu, IPv6 adresleri için sonraki atlama adresleriyle ilgili bilgileri depolar. ***Nx_api. h*** içinde tanımlanan varsayılan değer 8 ' dir.|
|NX_IPV6_MAX_REASSEMBLY_TIME | IPv6 parçasını yeniden atamaları için izin verilen en uzun süreyi denetleyen simge.|
|NX_IPV6_MULTICAST_ENABLE | ***NX_ENABLE_IPV6_MULTICAST** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ENABLE_IPV6_MULTICAST_* * kullanması önerilir.|
|NX_IPV6_PREFIX_LIST_TABLE_SIZE | Önek tablosunun boyutunu belirtir. Ön ek bilgileri, yönlendirici tanıtımlarından alınır ve IPv6 adres yapılandırmasının bir parçasıdır. ***Nx_api. h*** içinde tanımlanan varsayılan değer 8 ' dir.|
|NX_IPV6_STATELESS_AUTOCONFIG_CONTROL | Tanımlı, NetX Duo durum bilgisiz adres otomatik yapılandırma özelliğini devre dışı bırakmasına izin verir Varsayılan olarak bu seçenek etkin değildir.|
|NX_MAX_IPV6_ADDRESSES | IPv6 adres havuzundaki giriş sayısını belirtir. Arabirim yapılandırması sırasında NetX Duo, havuzdan IPv6 girdileri kullanır. \*Her arabirimin en az bir bağlantı yerel adresine ve iki genel adrese sahip olmasını sağlamak için varsayılan olarak (NX_MAX_PHYSICAL_INTERFACES 3) kullanılır. Tüm arabirimlerin IPv6 adres havuzunu paylaştığından emin olmanız gerektiğini unutmayın.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Hedef tablodaki belirli bir hedefin yol MTU değerini sıfırlamak için süreölçer onay işaretleri içindeki bekleme aralığını belirtir. ***NX_DISABLE_IPV6_PATH_MTU_DISCOVERY*** tanımlanmışsa, bu sembolün tanımlanması etkisizdir.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Hedef tablo girişi için yol MTU değerini sıfırlama bekleme aralığını (saniye cinsinden) belirten simge. Yalnızca ***NX_ENABLE_IPV6_PATH_MTU_DISCOVERY*** tanımlanmışsa geçerlidir. Varsayılan olarak bu değer 600 (saniye) olarak ayarlanır.|

### <a name="neighbor-cache-configuration-options"></a>Komşu önbelleği yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DELAY_FIRST_PROBE_TIME | ESKI durumdaki bir önbellek girişi için ilk isteme gönderilmeden önce geçmesi gereken saniye cinsinden gecikme süresini belirtir. ***Nx_nd_cache. h*** içinde tanımlanan varsayılan değer 5 ' tir.|
|NX_DISABLE_IPV6_DAD | Tanımlı, bu seçenek IPv6 adres ataması sırasında yinelenen adres algılamayı (BABACıĞıM) devre dışı bırakır. Adresler el ile yapılandırma ya da durum bilgisiz adres otomatik yapılandırması aracılığıyla ayarlanır.|
|NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES | Tanımlı, bu seçenek, tablo dolduğunda yeni girişler için yer açmak için zaman aşımı süresi dolmadan NetX Duo 'un eski önbellek tablosu girdilerini kaldırmasını engeller. Statik ve yönlendirici girdileri hiçbir şekilde temizlenmez.|
|NX_IPV6_DAD_TRANSMITS | NetX Duo bir arabirim adresini geçerli olarak işaretlediğinde, gönderilecek komşu ISTEME iletilerinin sayısını belirtir. ***NX_DISABLE_IPV6_DAD** _ TANıMLANMıŞSA (DAD devre dışı), bu seçeneğin ayarlanması etkisizdir. Alternatif olarak, sıfır (0) değeri, BABACıĞıM ' ı kapatır, ancak NetX Duo içinde BABACıĞıM işlevini bırakır. _ *_Nx_api. h_* * içinde tanımlanmıştır, varsayılan değer 3 ' dir.|
|NX_IPV6_DISABLE_PURGE_UNUSED_CACHE_ENTRIES | ***NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES_* * kullanması önerilir.|
|NX_IPV6_NEIGHBOR_CACHE_SIZE | IPv6 komşu önbelleği tablosundaki giriş sayısını belirtir. ***Nx_nd_cache. h*** içinde tanımlanan varsayılan değer 16 ' dır.|
|NX_MAX_MULTICAST_SOLICIT | IPv6 adresi ile MAC adresi arasında eşleme yapıldığında, IPv6 komşu bulma protokolünün bir parçası olarak NetX Duo iletim iletilerinin sayısını belirtir. ***Nx_nd_cache. h*** içinde tanımlanan varsayılan değer 3 ' dir.|
|NX_MAX_UNICAST_SOLICIT | Belirli bir komşunuzun ulaşılabilirlik düzeyini tespit etmek için NetX Duo ilettiği komşu ISTEME iletilerinin sayısını belirtir. ***Nx_nd_cache. h*** içinde tanımlanan varsayılan değer 3 ' dir.|
|NX_ND_MAX_QUEUE_DEPTH | ND önbelleğinin çözülmesi için sıralanmış en fazla paket sayısını tanımlayan simge. Varsayılan olarak, bu simge 4 olarak ayarlanır.|
|NX_REACHABLE_TIME | Önbellek hedefi IPv6 adresinden hiçbir paket alınmadığında, ERIŞILEBILIR durumda bir önbellek girişinin mevcut olması için saniye cinsinden zaman aşımı süresini belirtir. ***Nx_nd_cache. h*** içinde tanımlanan varsayılan değer 30 ' dur.|
|NX_RETRANS_TIMER  | NetX Duo tarafından gönderilen isteme paketleri arasındaki gecikme süresini milisaniye olarak belirtir. ***Nx_nd_cache. h*** içinde tanımlanan varsayılan değer 1000 ' dir.|
| NXDUO_DISABLE_DAD | ***NX_DISABLE_IPV6_DAD** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_IPV6_DAD_* * kullanması önerilir.|
|NXDUO_DUP_ADDR_DETECT_TRANSMITS | ***NX_IPV6_DAD_TRANSMITS** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_IPV6_DAD_TRANSMITS_* * kullanması önerilir.|

### <a name="miscellaneous-icmpv6-configuration-options"></a>Çeşitli ICMPv6 yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_ICMPV6_ERROR_MESSAGE | Tanımlı, NetX Duo 'in bir sorun paketine yanıt olarak bir ICMPv6 hata iletisi göndermesini devre dışı bırakır (ör. yanlış biçimli üst bilgi veya paket üst bilgisi türü kullanım dışı) başka bir konaktan alındı.|
|NX_DISABLE_ICMPV6_REDIRECT_PROCESS | Tanımlı, ICMPv6 yeniden yönlendirme paketi işlemeyi devre dışı bırakır. NetX Duo varsayılan olarak iletileri yeniden yönlendirir ve hedef tabloyu sonraki atlama IP adresi bilgileriyle güncelleştirir.|
|NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS | Tanımlı, NetX Duo 'un IPv6 yönlendirici tanıtımı paketlerinde alınan bilgileri işlemesini devre dışı bırakır.|
|NX_DISABLE_ICMPV6_ROUTER_SOLICITATION | Tanımlı, NetX Duo 'un, yönlendiriciye düzenli aralıklarla IPv6 Yönlendirici isteme iletileri göndermesini devre dışı bırakır.|
|NX_DISABLE_ICMPV6_RX_CHECKSUM | Tanımlı, alınan ıCMP paketlerinde ICMPv6 sağlama toplamı hesaplamasını devre dışı bırakır.|
|NX_DISABLE_ICMPv6_RX_CHECKSUM | ***NX_DISABLE_ICMPV6_RX_CHECKSUM** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_CMPV6_RX_CHECKSUM_* * kullanması önerilir.|
|NX_DISABLE_ICMPV6_TX_CHECKSUM | Aktarılan ıCMP paketlerinde tanımlanan, devre dışı bırakan ve ICMPv6 sağlama toplamı hesaplaması.|
|NX_DISABLE_ICMPV6_TX_CHECKSUM | ***NX_DISABLE_ICMPV6_TX_CHECKSUM** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ICMPV6_TX_CHECKSUM_* * kullanması önerilir.|
|NX_ICMPV6_MAX_RTR_SOLICITATIONS | Bir konağın, yönlendirici yanıtı alınana kadar gönderdiği en fazla yönlendirici isteme sayısını tanımlayın. Yanıt alınmadığında, ana bilgisayar Hayır yönlendiricisi yok demektir. Varsayılan değer 3 ' dir.|
|NX_ICMPV6_RTR_SOLICITATION_DELAY | İlk yönlendirici bağlantısı için saniye cinsinden en fazla gecikme süresini belirtir.|
|NX_ICMPV6_RTR_SOLICITATION_INTERVAL | İki yönlendirici bağlantısı iletisi arasındaki aralığı belirtir. Varsayılan değer 4'tür.|
|NXDUO_DESTINATION_TABLE_SIZE | ***NX_IPV6_DESTINATION_TABLE_SIZE** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_IPV6_DESTINATION_TABLE_SIZE_* * kullanması önerilir.|
|NXDUO_DISABLE_ICMPV6_ERROR_MESSAGE | ***NX_DISABLE_ICMPV6_ERROR_MESSAGE** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ICMPV6_ERROR_MESSAGE_* * kullanması önerilir.|
|NXDUO_DISABLE_ICMPV6_REDIRECT_PROCESS | ***NX_DISABLE_ICMPV6_REDIRECT_PROCESS** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ICMPV6_REDIRECT_PROCESS_ kullanması önerilir**|  
|NXDUO_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS| ***NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS_* * kullanması önerilir.|
|NXDUO_DISABLE_ICMPV6_ROUTER_SOLICITATION | ***NX_DISABLE_ICMPV6_ROUTER_SOLICITATION** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_DISABLE_ICMPV6_ROUTER_SOLICITATION_* * kullanması önerilir.|
|NXDUO_ICMPV6_MAX_RTR_SOLICITATIONS | ***NX_ICMPV6_MAX_RTR_SOLICITATIONS** _ olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ICMPV6_MAX_RTR_SOLICITATIONS_* * kullanması önerilir.|
|NXDUO_ICMPV6_RTR_SOLICITATION_INTERVAL | ***NX_ICMPV6_RTR_SOLICITATION_INTERVAL** _ olarak yeniden adlandırıldı. Bu simgeye yıpranma uygulanıyor. Yine de desteklenmekle birlikte, yeni tasarımların _ *_NX_ICMPV6_RTR_SOLICITATION_INTERVAL_ kullanması önerilir**|

## <a name="netx-duo-version-id"></a>NetX Duo sürüm KIMLIĞI

NetX Duo 'un geçerli sürümü, çalışma zamanı sırasında hem Kullanıcı hem de uygulama yazılımı için kullanılabilir. NetX Duo sürümünü **nx_port. h** dosyasının inceağından elde edebilirsiniz. Ayrıca, bu dosya karşılık gelen bağlantı noktasının sürüm geçmişini de içerir. Uygulama yazılımı, _ *_nx_port. h_* * içindeki genel dize _* *_nx_version_id_*_ inceleyerek NETX Duo sürümünü alabilir.

Uygulama yazılımı ayrıca, ***nx_api. h***'de tanımlanan sabitlerin altında gösterilen sabitlerden sürüm bilgileri elde edebilir.

Bu sabitler, geçerli ürün sürümünü ada ve ürünün büyük ve küçük sürümüne göre belirler.

\#EL_PRODUCT_NETXDUO tanımlama  
\#NETXDUO_MAJOR_VERSION tanımlama  
\#NETXDUO_MINOR_VERSION tanımlama