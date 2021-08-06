---
title: Bölüm 2-Azure RTOS NetX Duo yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX Duo yüksek performanslı ağ yığınının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ac41672959c0873d90bdafe0d6b959efdddf8ecc
ms.sourcegitcommit: 62cfdf02628530807f4d9c390d6ab623e2973fee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/05/2021
ms.locfileid: "115178230"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo"></a>Bölüm 2-Azure RTOS NetX Duo yüklemesi ve kullanımı

Bu bölümde, aşağıdakiler de dahil olmak üzere yüksek performanslı ağ yığınının Azure RTOS NetX Duo 'i yükleme, kurulum ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır: 

## <a name="host-considerations"></a>Ana bilgisayar konuları

katıştırılmış geliştirme genellikle Windows veya Linux (unıx) ana bilgisayar bilgisayarlarında gerçekleştirilir. Uygulama derlendikten, bağlanır ve çalıştırılabilir dosya konakta üretildikten sonra, yürütme için hedef donanıma indirilir.

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

netx Duo, GitHub deposu yerel makinenize kopyalanarak yüklenir. Bilgisayarınızda NetX Duo deposunun bir kopyasını oluşturmak için tipik sözdizimi aşağıda verilmiştir:

```c
    git clone https://github.com/azure-rtos/netxduo
```

alternatif olarak, GitHub ana sayfasındaki indir düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında NetX Duo kitaplığını oluşturmaya yönelik yönergeleri de bulacaksınız.

> [!IMPORTANT]
> *Uygulama yazılımının NetX Duo kitaplık dosyasına (genellikle **NX. a** veya **NX. lib**) ve C içerme dosyalarına **nx_api. h ve nx_port. h** erişimi olması gerekir. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaları uygulama geliştirme alanına kopyalayarak gerçekleştirilir.*

## <a name="using-netx-duo"></a>NetX Duo kullanma

NetX Duo kullanmak kolaydır. Temel olarak, uygulama kodu derleme sırasında ***nx_api. h** _ Içermeli ve NETX Duo Kitaplığı _*_NX. a_*_ (veya _ *_NX. lib_*) * ile bağlantı içermelidir.

NetX Duo uygulaması oluşturmak için gereken dört kolay adım aşağıda verilmiştir:

| Adım  | Description  |
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
|NX_ENABLE_SOURCE_ADDRESS_CHECK| Tanımlı, gelen paketin kaynak adresinin denetlenir. Varsayılan olarak bu seçenek devre dışıdır.|
| NX_IPSEC_ENABLE  | Tanımlı, NetX Duo kitaplığının IPsec işlemlerini desteklemesini sağlar. Bu özellik, isteğe bağlı NetX Duo IPsec modülünü gerektirir. Bu özellik varsayılan olarak etkin değildir.            |
| NX_LITTLE_ENDIAN | Tanımlı, protokol üst bilgilerini düzgün bir biçimde little endian için gerekli bayt değiştirme işlemini big endian gerçekleştirir. Varsayılan değerin genellikle ***nx_port.h olarak ayar olduğunu unutmayın.***|
|NX_MAX_PHYSICAL_INTERFACES | Cihazdaki toplam fiziksel ağ arabirimi sayısını belirtir. Varsayılan değer 1'tir ve ***nx_api.h ;*** bir cihazın en az bir fiziksel arabirimi olması gerekir. Bunun geri döngü arabirimini dahil olmadığını unutmayın.|
| NX_NAT_ENABLE | NetX Duo, NAT işlemiyle hazırlandı. Varsayılan olarak bu seçenek tanımlanmamıştır.|
| NX_PHYSICAL_HEADER  | Boyutu çerçevenin fiziksel üst bilgisi bayt cinsinden belirtir. Varsayılan değer 16'dır (32 bit sınıra hizalanmış tipik bir 14 bit Ethernet çerçevesine göre) ve ***nx_api.h** _ içinde tanımlanır. Uygulama,*__nx_user.h .*_* gibi _*_nx_api.h_*_ dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz |
| NX_PHYSICAL_TRAILER | Fiziksel paket fragmanlarının bayt cinsinden boyutunu belirtir ve genellikle Ethernet CRC'leri gibi şeyler için depolama alanı ayrılana kadar kullanılır. Varsayılan değer 4'tir ve ***nx_api.h içinde tanımlanır.***|

### <a name="arp-configuration-options"></a>ARP Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_ARP_DEFEND_BY_REPLY | Tanımlı, NetX Duo'ya bir ARP yanıtı göndererek IP adresini savunmasını sağlar.|
|NX_ARP_DEFEND_INTERVAL| ARP modülünün çakışmada bir adresi gösteren gelen ARP iletisine yanıt olarak bir sonraki savunma paketini saniyeler içinde gönderme aralığını tanımlar.|
|NX_ARP_DISABLE_AUTO_ARP_ENTRY|  * NX_DISABLE_ARP_AUTO_ENTRY _ **olarak yeniden** adlandırıldı. Hala desteklense de, yeni tasarımların __*_ veya **NX_DISABLE_ARP_AUTO_ENTRY teşvik edilmiştir.|
|NX_ARP_EXPIRATION_RATE| ARP girişlerinin geçerli kalma saniye sayısını belirtir. Varsayılan sıfır değeri ARP girişlerinin süre sonu veya eskimesi özelliğini devre dışı bırakarak ***nx_api.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_ARP_MAC_CHANGE_NOTIFICATION_ENABLE | ***** NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION _. Hala desteklense de, yeni tasarımların __*_ veya **NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION teşvik edilmiştir.|
|NX_ARP_MAX_QUEUE_DEPTH | Bir ARP yanıtı beklerken kuyruğa alın en fazla paket sayısını belirtir. Varsayılan değer 4'tir ve ***nx_api.h içinde tanımlanır.***|
|NX_ARP_MAXIMUM_RETRIES | ARP yanıtı olmadan yapılan en fazla ARP yeniden deneme sayısını belirtir. Varsayılan değer 18'tir ve ***nx_api.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_ARP_UPDATE_RATE | ARP yeniden denemeleri arasındaki saniye sayısını belirtir. Varsayılan değer 10'dır ve 10 saniyeyi temsil eder ve ***nx_api.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_DISABLE_ARP_AUTO_ENTRY | Tanımlı, ARP önbelleğine ARP istek bilgilerini girmeyi devre dışı bırakıyor.|
|NX_DISABLE_ARP_INFO | Tanımlı, ARP bilgi toplamayı devre dışı bırakıyor.|
|NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION| Tanımlı, MAC adresinin güncelleştirilmiş olduğunu algılamak için ARP'nin bir geri çağırma notify işlevi çağırana izin verir.|

### <a name="icmp-configuration-options"></a>ICMP Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_ICMP_INFO| Tanımlı, ICMP bilgi toplamayı devre dışı bırakıyor.|
|NX_DISABLE_ICMP_RX_CHECKSUM| Tanımlı, alınan ICMP paketlerde hem ICMPv4 hem de ICMPv6 sağlamam hesaplamasını devre dışı bırakmıştır. Bu seçenek, ağ arabirimi sürücüsü ICMPv4 ve ICMPv6 sağlamalarını doğrulayana ve uygulama IP parçalanma özelliğini veya IPsec özelliğini kullanmazsa yararlıdır. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_DISABLE_ICMP_TX_CHECKSUM | Tanımlanan, iletilen ICMP paketlerde hem ICMPv4 hem de ICMPv6 sağlamam hesaplamasını devre dışı bıraktır. Bu seçenek, ağ arabirimi sürücüsünün ICMPv4 ve ICMPv6 sağlama toplamlarını hesaplayama,
ve uygulama IP parçalanma özelliğini veya IPsec özelliğini kullanmaz. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_DISABLE_ICMPV4_ERROR_MESSAGE | NetX Duo, hatalı biçimlendirilmiş IPv4 üst bilgisi gibi hata koşullarına yanıt olarak ICMPv4 Hata İletileri göndermez. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_DISABLE_ICMPV4_RX_CHECKSUM | Tanımlı, alınan ICMP paketlerde ICMPv4 sağlama sayısı hesaplamasını devre dışı bırakmıştır. Bu seçenek, bir ***NX_DISABLE_ICMP_RX_CHECKSUM*** otomatik olarak tanımlanır. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_DISABLE_ICMPv4_RX_CHECKSUM | ***** NX_DISABLE_ICMPV4_RX_CHECKSUM _. Hala desteklense de, yeni tasarımların __*_ veya **NX_DISABLE_ICMPV4_RX_CHECKSUM teşvik edilmiştir.|
|NX_DISABLE_ICMPV4_TX_CHECKSUM | Tanımlanan, iletilen ICMP paketlerde ICMPv4 sağlama sayısı hesaplamasını devre dışı bıraktır. Bu seçenek, bir ***NX_DISABLE_ICMP_TX_CHECKSUM*** otomatik olarak tanımlanır. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_DISABLE_ICMPv4_TX_CHECKSUM | ***** NX_DISABLE_ICMPV4_TX_CHECKSUM _.</br>Hala desteklense de, yeni tasarımların __*_ veya **NX_DISABLE_ICMPV4_TX_CHECKSUM teşvik edilmiştir.|
|NX_ENABLE_ICMP_ADDRESS_CHECK | Tanımlı, ICMP paketinin hedef adresi denetlenir. Varsayılan olarak devre dışı seçeneği kullanılır. IP yayını veya IP çok noktaya yayın adresine yönelik icMP Yankı İsteği sessizce atılır.|

### <a name="igmp-configuration-options"></a>IGMP Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_IGMP_INFO | Tanımlandı, IGMP bilgi toplamayı devre dışı bırakıyor.|
|NX_DISABLE_IGMPV2 | Tanımlı, IGMPv2 desteğini devre dışı bırakarak ve NetX Duo yalnızca IGMPv1'i destekler. Varsayılan olarak bu seçenek ayarlanmamıştır ve ***nx_api.h içinde tanımlanır.***|
|NX_MAX_MULTICAST_GROUPS | Birleştirilene en fazla çok noktaya yayın grubu sayısını belirtir. Varsayılan değer 7'dir ve ***nx_api.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|

### <a name="ip-configuration-options"></a>IP Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_FRAGMENTATION | Tanımlanan, hem IPv4 hem de IPv6 parçalanması ve yeniden değerlendirme mantığını devre dışı bırakma.|
| NX_DISABLE_IPV4     | Tanımlandı, IPv4 işlevselliğini devre dışı bırakıyor. Bu seçenek yalnızca IPv6'yı suupport etmek için NetX Duo oluşturmak için kullanılabilir. Varsayılan olarak bu seçenek tanımlanmamıştır. |
| NX_DISABLE_IP_INFO | Tanımlandı, IP bilgileri toplamayı devre dışı bırakıyor.|
|NX_DISABLE_IP_RX_CHECKSUM | Tanımlı, alınan IPv4 paketlerde sağlama sağlamama mantığını devre dışı bırakmıştır. Bu, ağ cihazı IPv4 sağlamalarını doğrulayaya sahipse ve uygulama IP parçalanması veya IPsec kullanmayı beklemezse yararlıdır.|
|NX_DISABLE_IP_TX_CHECKSUM | Tanımlı, gönderilen IPv4 paketlerde sağlama sağlamama mantığını devre dışı bıraktır. Bu, temel alınan ağ aygıtının IPv4 üst bilgi sağlamasını oluşturabilen ve uygulamanın IP parçalanması veya IPsec kullanmayı beklemeyebilecek durumlarda yararlıdır.|
|NX_DISABLE_LOOPBACK_INTERFACE | Tanımlı, geri döngü arabirimi için NetX Duo desteğini devre dışı bırakıyor.|
|NX_DISABLE_RX_SIZE_CHECKING | Tanımlı, alınan paketlerde boyut denetlemesini devre dışı bırakmıştır.|
|NX_ENABLE_IP_RAW_PACKET_FILTER | Tanımlı, IP ham paketi alma filtresi işlevini sağlar. Alınan ham IP paketleri türü üzerinde daha fazla denetim gerektiren uygulamalar bu özelliği kullanabilir. IP ham paket filtresi özelliği, BSD uyumluluk katmanında ham yuva işlemi de destekler. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_ENABLE_IP_STATIC_ROUTING | Tanımlı, hedef adresin belirli bir sonraki atlama adresine atandığı IPv4 statik yönlendirmeyi sağlar. Varsayılan olarak IPv4 statik yönlendirme devre dışıdır.|
|NX_FRAGMENT_IMMEDIATE_ASSEMBLY | Tanımlı, IPv4 ve IPv6 yeniden değerlendirme mantığının bir IP parçası aldıktan hemen sonra yürütülse izin verir. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_IP_MAX_REASSEMBLY_TIME | IPv4 parçasını ve IPv6 parçasını yeniden bir kez yeniden değerlendirmeye izin verilen en uzun zamanı kontrol eden simge. Burada tanımlanan değerin ** hem ***** NX_IPV4_MAX_REASSEMBLY_TIME _ hem de _*_NX_IPV6_MAX_REASSEMBLY_TIME_ not.|
|NX_IP_PERIODIC_RATE | Tanımlandı, bir saniye içinde ThreadX zamanlayıcı tık sayısını belirtir. Varsayılan değer, varsayılan olarak 100 (10ms **süreölçeri)** olarak ayarlanmış olan * TX_TIMER_TICKS_PER_SECOND _ threadX simgesinden türetildi. NetX Duo modüllerinin geri kalanı _ veya değerinden zamanlama bilgileri türetirken uygulamalar bu değeri değiştirirken *_dikkatli NX_IP_PERIODIC_RATE._**|
|NX_IP_RAW_MAX_QUEUE_DEPTH | Ham IP paketlerinin sayısını kontrol eden sembol ham paket alma kuyruğunda kuyruğa alınabilirsiniz. Varsayılan olarak değer 20'ye ayarlanır.| 
|NX_IP_ROUTING_TABLE_SIZE | Tanımlı, IPv4 statik yönlendirme tablosunda, belirli bir hedef adres için giden arabirimin ve sonraki atlama adreslerinin listesi olan en fazla girdi sayısını ayarlar. Varsayılan değer 8'tir ve ***nx_api.h içinde tanımlanır.** _ Bu simge yalnızca *___* NX_ENABLE_IP_STATIC_ROUTING * tanımlandığı zaman kullanılır.|
|NX_IPV4_MAX_REASSEMBLY_TIME | IPv4 parçasını yeniden değerlendirmeye izin verilen en uzun zamanı kontrol eden sembol. Içinde tanımlanan değerin bu NX_IP_MAX_REASSEMBLY_TIME üzerine yazarak yaz olduğunu unutmayın.|

### <a name="packet-configuration-options"></a>Paket Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_PACKET_CHAIN | Tanımlandı, paket zinciri mantığını devre dışı bırakıyor. Varsayılan olarak bu tanımlanmamıştır.|
|NX_DISABLE_PACKET_INFO | Tanımlandı, paket havuzu bilgilerini toplamayı devre dışı bırakıyor.|
|NX_ENABLE_LOW_WATERMARK | Tanımlı, NetX Duo paket havuzu alt filigran özelliğini sağlar. Uygulama, düşük filigran değeri ayarlar. TCP paketlerini alırken, paket havuzuna düşük filigran ulaşılırsa NetX Duo paketi serbest bırakarak sessizce atar ve paket havuzunun açık kalmasını önler. Bu özellik varsayılan olarak etkin değildir.|
|NX_ENABLE_PACKET_DEBUG_INFO | Tanımlı, paket hata ayıklama bilgilerini günlüğe kaydeder.|
|NX_PACKET_ALIGNMENT | Tanımlı, paket yükü alanı başlangıç adresi için hizalama gereksinimini bayt cinsinden belirtir. Bu seçenek * NX_PACKET_HEADER_PAD _ **ve** _* NX_PACKET_HEADER_PAD_SIZE ** kullanım _dışıdır._ Varsayılan olarak bu seçenek 4 olarak tanımlanır ve yük alanı 4 baytı başlangıç adresi hizalanır.|
|NX_PACKET_HEADER_PAD | Tanımlı, denetim bloğuna doğru doldurmayı NX_PACKET sağlar. ULONG sözcüklerinin sayısı * NX_PACKET_HEADER_PAD_SIZE **_.** Bu seçeneğin _* veya **tarafından _NX_PACKET_ALIGNMENT_ unutmayın.|
|NX_PACKET_HEADER_PAD_SIZE | Paket yükü alanına istenen hizalamada başlamasını NX_PACKET için, NX_PACKET ULONG sözcüklerinin sayısını ayarlar. Bu özellik, arabellek tanımlayıcıları doğrudan yük alanına işaret NX_PACKET ve ağ arabirimi alma mantığı veya önbellek işlem mantığı belirli hizalama gereksinimlerini karşılamak için arabellek başlangıç adresini bekliyorsa yararlıdır. Bu değer yalnızca ***** NX_PACKET_HEADER_PAD _ tanımlandığı zaman geçerli olur. Bu seçeneğin **.__*_ tarafından NX_PACKET_ALIGNMENT.|

### <a name="rarp-configuration-options"></a>RARP Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_RARP_INFO | Tanımlandı, RARP bilgi toplamayı devre dışı bırakıyor.|

### <a name="tcp-configuration-options"></a>TCP Yapılandırma Seçenekleri

| Seçenek | Açıklama |
|---|---|
|NX_DISABLE_RESET_DISCONNECT | Tanımlanan, sağlanan zaman aşımı değeri bağlantı kesiliyor olarak belirtilirken sıfırlama işlemini devre dışı ***NX_NO_WAIT.***|
|NX_DISABLE_TCP_INFO | Tanımlandı, TCP bilgi toplamayı devre dışı bırakıyor.|
|NX_DISABLE_TCP_RX_CHECKSUM | Tanımlı, alınan TCP paketlerindeki sağlama sayısı mantığını devre dışı bırakmıştır. Bu yalnızca bağlantı katmanında güvenilir sağlama grubu veya CRC işlemesi olan ya da arabirim sürücüsünün donanımda TCP sağlama sağlamasını doğrulaya sahip olduğu ve uygulamanın IPsec kullanmamış olduğu durumlarda yararlıdır.|
|NX_DISABLE_TCP_TX_CHECKSUM | Tanımlı, TCP paketleri göndermek için sağlama sayısı mantığını devre dışı bıraktır. Bu yalnızca, alıcı ağ düğümünün TCP sağlama kümesi mantığının devre dışı bırakılmıştır veya temel ağ sürücüsünün TCP sağlamalarını oluşturabilen ve uygulamanın IPsec kullanmamış olduğu durumlarda yararlıdır.|
|NX_ENABLE_TCP_KEEPALIVE | Tanımlı, isteğe bağlı TCP keepalive zamanlayıcıyı sağlar. Varsayılan ayarlar etkin değildir.|
|NX_ENABLE_TCP_MSS_CHECK | Tanımlı, TCP bağlantısını kabulmeden önce en düşük eş MSS'nin doğrulanmasına olanak sağlar. Bu özelliği kullanmak ***için,*** NX_ENABLE_TCP_MSS_MINIMUM tanımlanmalıdır. Varsayılan olarak, bu seçenek etkin değildir.|
|NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY| Tanımlı, uygulamanın TCP iletme kuyruğu derinliği artık en yüksek değerde olmadığı zaman çağrılan bir geri çağırma işlevi yüklemesini sağlar. Bu geri çağırma, TCP yuvasının daha fazla veri aktarmaya hazır olduğunu gösteren bir göstergedir. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_TCP_WINDOW_SCALING | TCP uygulamaları için pencere ölçeklendirme seçeneğini sağlar. Tanımlanmışsa, TCP bağlantı aşamasında pencere ölçeklendirme seçeneği belirlenebilir ve uygulama 64.000'den büyük bir pencere boyutu belirtebilir. Varsayılan ayar etkin değildir (tanımlanmamış).|
|NX_MAX_LISTEN_REQUESTS | En fazla sunucu dinleme isteği sayısını belirtir. Varsayılan değer 10'dır ve ***nx_api.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_ACK_EVERY_N_PACKETS | ACK göndermeden önce alacak TCP paketlerinin sayısını belirtir. ***** NX_TCP_IMMEDIATE_ACK _ etkinse ancak _ *_NX_TCP_ACK_EVERY_N_PACKETS_** etkinse, geriye dönük uyumluluk için bu değer otomatik olarak 1 olarak ayarlanır.|
|NX_TCP_ACK_TIMER_RATE | Tcp gecikmeli ACK işlemesi için zamanlayıcı NX_IP_PERIODIC_RATE sistem işaretlerinin (NX_IP_PERIODIC_RATE) nasıl bölündüklerini belirtir. Varsayılan değer 5'tir ve 200 m'yi temsil eder ve ***nx_tcp.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_ENABLE_KEEPALIVE | ***** NX_ENABLE_TCP_KEEPALIVE _. Hala desteklense de, yeni tasarımların __*_ veya **NX_ENABLE_TCP_KEEPALIVE teşvik edilmiştir.|
|NX_TCP_ENABLE_MSS_CHECK | ***** NX_ENABLE_TCP_MSS_CHECK _. Hala desteklense de, yeni tasarımların _ veya *_NX_ENABLE_TCP_MSS_CHECK._**|
|NX_TCP_ENABLE_WINDOW_SCALING | ***** NX_ENABLE_TCP_WINDOW_SCALING _. Hala desteklense de, yeni tasarımların __*_ veya **NX_ENABLE_TCP_WINDOW_SCALING teşvik edilmiştir.|
|NX_TCP_FAST_TIMER_RATE | NetX Duo iç tık sayısının (NX_IP_PERIODIC_RATE) hızlı TCP zamanlayıcı oranını hesaplamak için nasıl bölündüklerini belirtir. Hızlı TCP zamanlayıcısı, gecikmeli ACK zamanlayıcısı da dahil olmak üzere çeşitli TCP süreölçerlerini kullanmak için kullanılır. Varsayılan değer 10'dır ve ThreadX zamanlayıcının 10ms'de çalıştırılı olduğunu varsayarak 100 m'yi temsil eder. Bu değer ***nx_tcp.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_IMMEDIATE_ACK| Tanımlı, isteğe bağlı TCP anında ACK yanıt işlemeyi sağlar. Bu simgeyi tanımlamak, 1  ***NX_TCP_ACK_EVERY_N_PACKETS*** tanımlamaya eşdeğerdir.|
|NX_TCP_KEEPALIVE_INITIAL | Keepalive süreölçeri etkinleştirmeden önce, etkin değil olarak saniye sayısını belirtir. Varsayılan değer 2 saati temsil eden ve * nx_tcp.h _ içinde tanımlanan **7200'tir.** Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_KEEPALIVE_RETRIES | Bağlantının bozuk olduğu kabul edildiklerine kadar kaç tane sürekli yeniden denemeye izin verilmiyorsa bunu belirtir. Varsayılan değer 10'dır ve 10 yeniden denemeyi temsil eder ve ***nx_tcp.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_KEEPALIVE_RETRY | Bağlantının diğer tarafının yanıt vermey olduğunu varsayarak, sürekli zamanlayıcının yeniden denemeleri arasındaki saniye sayısını belirtir. Varsayılan değer, yeniden denemeler arasında 75 saniyeyi temsil eden ve ***nx_tcp.h _ içinde tanımlanan 75'tir.** Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_MAX_OUT_OF_ORDER_PACKETS | En fazla sırasız TCP paketi sayısını tanımlayan sembol, TCP yuvası alma kuyruğunda tutulmalıdır. Bu sembol, TCP alma yuvasında kuyruğa alınan paket sayısını sınırlamak için kullanılabilir ve paket havuzunun aç bırakılamaması önlenebilir. Varsayılan olarak bu simge tanımlanmamıştır, bu nedenle TCP yuvasında kuyruğa alınan sipariş dışında paket sayısına bir sınır yoktur.|
|NX_TCP_MAXIMUM_RETRIES | Bağlantının bozuk olduğu kabul olmadan önce kaç tane veri iletme yeniden denemesine izin ver verilmiyorsa bunu belirtir. Varsayılan değer 10'dır ve 10 yeniden denemeyi temsil eder ve ***nx_tcp.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_MAXIMUM_RX_QUEUE | TCP yuvaları için en yüksek alma kuyruğu tanımlayan sembol. Bu özellik, tarafından ***NX_ENABLE_LOW_WATERMARK.***|
|NX_TCP_MAXIMUM_TX_QUEUE | TCP gönderme istekleri askıya alınmadan veya reddedmeden önce TCP aktarım kuyruğu en yüksek derinliğini belirtir. Varsayılan değer 20'dir, yani herhangi bir zamanda aktarım kuyruğunda en fazla 20 paket olabilir. Paketlerin, bağlantının diğer tarafından paket verilerinden bir veya hepsini kapsayan bir ACK alınana kadar aktarım kuyruğunda kalacağına dikkat edin. Bu sabit ***nx_tcp.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_MSS_MINIMUM | NetX Duo TCP modülünün kabulladığı en düşük MSS değerini tanımlayan sembol. Bu özellik, tarafından ***NX_ENABLE_TCP_MSS_CHECK.***|
|NX_TCP_QUEUE_DEPTH_UPDATE_NOTIFY_ENABLE | ***** NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY _. Hala desteklense de, yeni tasarımların __*_ veya **NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY teşvik edilmiştir.|
|NX_TCP_RETRY_SHIFT | Yeniden denemeler arasında yeniden iletim zaman aşımı döneminin nasıl değişiklik gösterir. Bu değer 0 ise, ilk yeniden iletim zaman aşımı sonraki yeniden iletim zaman aşımı ile aynıdır. Bu değer 1 ise, her bir birbirinin tekrarı iki kat uzun olur. Bu değer 2 ise, izleyen her yeniden iletim zaman aşımı dört kat uzun olur. Varsayılan değer 0'dır ve ***nx_tcp.h _ içinde** tanımlanır. Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|
|NX_TCP_TRANSMIT_TIMER_RATE | TCP iletme yeniden deneme işleminin zamanlayıcı oranını **hesaplamak için sistem işaretlerinin**(* NX_IP_PERIODIC_RATE _) nasıl bölündüklerini belirtir. Varsayılan değer 1'tir ve 1 saniyeyi temsil eder ve _*_nx_tcp.h içinde tanımlanır._*_ Uygulama, _ *_nx_api.h_** dahil olmadan önce değeri tanımlayarak varsayılan değeri geçersiz kabilirsiniz.|

### <a name="udp-configuration-options"></a>UDP Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_UDP_INFO | Tanımlandı, UDP bilgi toplamayı devre dışı bırakıyor.|
|NX_DISABLE_UDP_RX_CHECKSUM | Tanımlı, gelen UDP paketlerde UDP sağlama sayısı hesaplamasını devre dışı bıraktır. Bu, ağ arabirimi sürücüsü donanımda UDP üst bilgi sağlamasını doğrulayana ve uygulama IPsec veya IP parçalanma mantığını etkinleştirmezse yararlıdır.|
|NX_DISABLE_UDP_TX_CHECKSUM | Tanımlı, giden UDP paketlerde UDP sağlama süresi hesaplamasını devre dışı bıraktır. Bu, ağ arabirimi sürücüsünün VERILERI iletmeden önce UDP üst bilgi sağlama toplamlarını hesaplanması ve değeri IP başına eklemesi ve uygulamanın IPsec veya IP parçalanma mantığını etkinleştirmesi durumuyla ilgili faydalıdır.|

### <a name="ipv6-options"></a>IPv6 Seçenekleri  

| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_IPV6 | NetX Duo kitaplığı 7.000.000'i kullanarak IPv6 işlevselliğini devre dışı bırakarak. IPv6'ya ihtiyaç olmayan uygulamalar için bu, IPv6'yı desteklemek için gereken kodu ve ek depolama alanını çekmeyi önler.|
|NX_DISABLE_IPV6_PATH_MTU_DISCOVERY | Tanımlı, NetX Duo konak hedef tablosunda bir hedefe giden yolda en yüksek MTU'nun belirlenmesi için kullanılan MTU bulma yolunu devre dışı bıraktır. Bu, NetX Duo ana bilgisayarının parçalanma gerektirmeyen olası en büyük paketi göndermesini sağlar. Varsayılan olarak, bu seçenek tanımlanır (MTU yolu devre dışıdır).|
|NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY | Tanımlı, IPv6 adresi değiştiriken bir geri çağırma işlevinin çağrılmasını sağlar. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_IPV6_MULTICAST | Tanımlı, IPv6 çok noktaya yayın birleştirme/bırakma işlevini sağlar. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_IPV6_PATH_MTU_DISCOVERY | Tanımlı, IPv6 yolu MTU bulma özelliğini sağlar. Varsayılan olarak bu seçenek etkin değildir.|
|NX_IPV6_ADDRESS_CHANGE_NOTIFY_ENABLE | ***** NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY _. Hala desteklense de, yeni tasarımların __*_ veya **NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY teşvik edilmiştir.|
|NX_IPV6_DEFAULT_ROUTER_TABLE_SIZE | IPv6 yönlendirme tablosunda girdi sayısını belirtir. Varsayılan yönlendirici için en azından onS girişi gereklidir. ***nx_api.h içinde tanımlanır,*** varsayılan değer 8'tir.|
|NX_IPV6_DESTINATION_TABLE_SIZE | IPv6 hedef tablosunda girdi sayısını belirtir. Bu, IPv6 adresleri için sonraki atlama adresleriyle ilgili bilgileri depolar. ***nx_api.h içinde tanımlanır,*** varsayılan değer 8'tir.|
|NX_IPV6_MAX_REASSEMBLY_TIME | IPv6 parçasını yeniden değerlendirmeye izin verilen en uzun zamanı kontrol eden simge.|
|NX_IPV6_MULTICAST_ENABLE | ***** NX_ENABLE_IPV6_MULTICAST _. Hala desteklense de, yeni tasarımların __*_ veya **NX_ENABLE_IPV6_MULTICAST teşvik edilmiştir.|
|NX_IPV6_PREFIX_LIST_TABLE_SIZE | Ön ek tablosu boyutunu belirtir. Ön ek bilgileri yönlendirici tanıtımlarından elde edilir ve IPv6 adres yapılandırmasının bir parçasıtır. ***nx_api.h içinde tanımlanır,*** varsayılan değer 8'tir.|
|NX_IPV6_STATELESS_AUTOCONFIG_CONTROL | Tanımlı, NetX Duo'ya durum bilgileri olmayan adres otomatik yapılandırma özelliğini devre dışı bırakmasını sağlar. Varsayılan olarak bu seçenek etkin değildir.|
|NX_MAX_IPV6_ADDRESSES | IPv6 adres havuzu girişlerinin sayısını belirtir. Arabirim yapılandırması sırasında NetX Duo, havuzdan IPv6 girişlerini kullanır. Her arabirimin en az bir bağlantı yerel adresine ve iki genel adrese sahip olmasına izin vermek için varsayılan olarak (NX_MAX_PHYSICAL_INTERFACES \* 3) kullanılır. Tüm arabirimlerin IPv6 adres havuzunu paylaştığını unutmayın.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Hedef tablodaki belirli bir hedef için MTU yolunu sıfırlamak için zamanlayıcı tıklarında bekleme aralığını belirtir. Bu ***NX_DISABLE_IPV6_PATH_MTU_DISCOVERY*** tanımlanmışsa, bu sembolün tanımlanmasının hiçbir etkisi olmaz.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Hedef tablo girdisi için yol MTU değerini sıfırlamak için bekleme aralığını (saniye olarak) belirten simge. Yalnızca NX_ENABLE_IPV6_PATH_MTU_DISCOVERY ***geçerlidir.*** Varsayılan olarak bu değer 600 (saniye) olarak ayarlanır.|

### <a name="neighbor-cache-configuration-options"></a>Komşu Önbelleği Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DELAY_FIRST_PROBE_TIME | ESKI durumdaki bir önbellek girdisi için ilk istek gönderilmeden önceki gecikmeyi saniyeler içinde belirtir. ***nx_nd_cache.h içinde*** tanımlanır, varsayılan değer 5'tir.|
|NX_DISABLE_IPV6_DAD | Tanımlı, bu seçenek IPv6 adres ataması sırasında Yinelenen Adres Algılama'yı (ELE) devre dışı bırakıyor. Adresler el ile yapılandırmayla veya Durum Bilgisiz Adres Otomatik Yapılandırması aracılığıyla ayarlanır.|
|NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES | Tanımlanan bu seçenek NetX Duo'ya zaman aşımı süresi dolmadan önce eski önbellek tablosu girdilerini kaldırarak tablo dolu olduğunda yeni girişlere yer sağlamasını önleyecektir. Statik ve yönlendirici girişleri hiçbir zaman temiz değildir.|
|NX_IPV6_DAD_TRANSMITS | NetX Duo bir arabirim adresini geçerli olarak işaretlemeden önce gönderilecek Komşu Solicitation iletilerinin sayısını belirtir. ***NX_DISABLE_IPV6_DAD** _ tanımlanmışsa (DEVRE DıŞı), bu seçeneğin ayarlandığı herhangi bir etki olmaz. Alternatif olarak, sıfır (0) değeri, DAİrE'i kapatmaz ancak NETX Duo'da YERİNE IŞLEVINI bırakır. _*_nx_api.h_** içinde tanımlanan varsayılan değer 3'tir.|
|NX_IPV6_DISABLE_PURGE_UNUSED_CACHE_ENTRIES | ***** NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES _. Hala desteklense de, yeni tasarımların __*_ veya **NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES teşvik edilmiştir.|
|NX_IPV6_NEIGHBOR_CACHE_SIZE | IPv6 Komşu Önbelleği tablosunda girdi sayısını belirtir. ***nx_nd_cache.h içinde*** tanımlanır, varsayılan değer 16'dır.|
|NX_MAX_MULTICAST_SOLICIT | IPv6 adresi ile MAC adresi arasında eşleme gerektiğinde, NetX Duo'nın IPv6 Komşu Bulma protokolünün bir parçası olarak ilettiği Komşu Solicitation iletilerinin sayısını belirtir. ***nx_nd_cache.h içinde tanımlanır,*** varsayılan değer 3'tir.|
|NX_MAX_UNICAST_SOLICIT | NetX Duo'nun belirli bir komşunun ulaşabilirsiniz olup olmadığını belirlemek için ilettiği Komşu Solicitation iletilerinin sayısını belirtir. ***nx_nd_cache.h içinde tanımlanır,*** varsayılan değer 3'tir.|
|NX_ND_MAX_QUEUE_DEPTH | ND önbelleğinin çözümlensin diye kuyruğa alınan en fazla paket sayısını tanımlayan simge. Varsayılan olarak bu simge 4'e ayarlanır.|
|NX_REACHABLE_TIME | Önbellek girişinin, önbellek hedef IPv6 adreslerinden paket alınmadan REACHABLE durumda varolarak saniyeler içinde zaman zamanlarını belirtir. ***nx_nd_cache.h içinde tanımlanan*** varsayılan değer 30'dır.|
|NX_RETRANS_TIMER  | NetX Duo tarafından gönderilen istek paketleri arasındaki gecikme süresini milisaniye cinsinden belirtir. ***nx_nd_cache.h içinde*** tanımlanır, varsayılan değer 1000'tir.|
| NXDUO_DISABLE_DAD | ***** NX_DISABLE_IPV6_DAD _. Hala desteklense de, yeni tasarımların __*_ veya **NX_DISABLE_IPV6_DAD teşvik edilmiştir.|
|NXDUO_DUP_ADDR_DETECT_TRANSMITS | ***** NX_IPV6_DAD_TRANSMITS _. Hala desteklense de, yeni tasarımların __*_ veya **NX_IPV6_DAD_TRANSMITS teşvik edilmiştir.|

### <a name="miscellaneous-icmpv6-configuration-options"></a>Çeşitli ICMPv6 Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
|NX_DISABLE_ICMPV6_ERROR_MESSAGE | Tanımlandı, başka bir konaktan alınan bir sorun paketine (örneğin, yanlış biçimlendirilmiş üst bilgi veya paket üst bilgisi türü kullanım dışı bırakıldı) yanıt olarak NetX Duo'ya ICMPv6 hata iletisi göndermesini devre dışı bırakmıştır.|
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