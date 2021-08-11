---
title: Bölüm 2 - NetX Duo'Azure RTOS Yükleme ve Kullanma
description: Bu bölümde NetX Duo'da yüksek performanslı ağ yığınının yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli Azure RTOS açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 32a9efaac3c85d415316fba2e9536cc40939f1f6debcbe3e2fa588de613a694d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788839"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo"></a>Bölüm 2 - NetX Duo'Azure RTOS Yükleme ve Kullanma

Bu bölümde NetX Duo'da yüksek performanslı ağ yığınının yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların Azure RTOS açıklaması yer almaktadır. Bunlar: 

## <a name="host-considerations"></a>KonakLa ilgili Dikkat Edilmesi Gerekenler

Katıştırılmış geliştirme genellikle linux (Unix) Windows bilgisayarlarda gerçekleştirilir. Uygulama derledikten, bağlandıktan ve yürütülebilir dosya konakta üretildikten sonra, yürütülebilir dosya yürütülebilirlik için hedef donanıma indirilir.

Hedef indirme genellikle geliştirme aracının hata ayıklayıcısından yapılır. İndirmeden sonra, hata ayıklayıcısı hedef yürütme denetimi (go, durdurma, kesme noktası vb.) sağlamanın yanı sıra bellek ve işlemci kayıtlarına erişim sağlamakla sorumludur.

Çoğu geliştirme aracı hata ayıklayıcısı, JTAG (IEEE 1149.1) ve Arka Plan Hata Ayıklama Modu (BDM) gibi yonga üzerinde hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar ayrıca Öykünme (ICE) In-Circuit hedef donanımla iletişim kurar. Hem OCD hem de ICE bağlantıları, hedef yerleşik yazılıma en az izinsiz girişle sağlam çözümler sağlar.

Konakta kullanılan kaynaklar için olduğu gibi NetX Duo'nun kaynak kodu ASCII biçiminde teslim edilir ve konak bilgisayarın sabit diskte yaklaşık 1 Mbayt alan gerektirir.

## <a name="target-considerations"></a>HedefLe ilgili Dikkat Edilmesi Gerekenler

NetX Duo, hedefte 5 KBayt ile 45 KBayt Read-Only Bellek (ROM) gerektirir. NetX Duo iş parçacığı yığını ve diğer genel veri yapıları için hedefin Rastgele Erişim Belleği'nin (RAM) 1 ile 5KBayt arasında bir bölümü daha gereklidir.

Ayrıca NetX Duo, iki ThreadX zamanlayıcı nesnesinin ve bir ThreadX mutex nesnesinin kullanımını gerektirir. Bu tesisler NetX Duo protokol yığını içinde düzenli işlem ihtiyaçları ve iş parçacığı koruması için kullanılır.

## <a name="product-distribution"></a>Ürün Dağıtımı

Azure RTOS NetX Duo, genel kaynak kod depomuzdan <https://github.com/azure-rtos/netxduo/> edinebilirsiniz.

Aşağıda, depoda yer alan birkaç önemli dosyanın listesi ve ardından yer alan liste ve bir liste ve ardından yer alan bilgileri bulabilirsiniz:

**nx_api.h**  
Tüm sistem eşitlerini, veri yapılarını ve hizmet prototiplerini içeren C üst bilgi dosyası.

**nx_port.h** Tüm geliştirme aracı ve hedef veri tanımlarını ve yapılarını içeren C üst bilgi dosyası. 

**demo_netx.c** Küçük bir tanıtım uygulaması içeren C dosyası.

**nx.a (veya nx.lib)**  
Standart paketle dağıtılan NetX C kitaplığının ikili sürümü.

## <a name="netx-duo-installation"></a>NetX Duo Yüklemesi

NetX Duo, GitHub yerel makinenize kopyalandı. Aşağıda, bilgisayarınızda NetX Duo deposunun bir kopyasını oluşturmak için tipik bir söz dizimi ve söz dizimi ve ardından yer alan genel bir söz dizimi ve ardından gelir:

```c
    git clone https://github.com/azure-rtos/netxduo
```

Alternatif olarak, ana sayfada yer alan indirme düğmesini kullanarak deponun bir GitHub indirebilirsiniz.

Çevrimiçi deponun ön sayfasında NetX Duo kitaplığını oluşturma yönergelerini de bulabilirsiniz.

> [!IMPORTANT]
> *Uygulama yazılımının NetX Duo kitaplık dosyasına **(genellikle nx.a veya** **nx.lib)** erişmesi ve C'nin **nx_api.h ve nx_port.h dosyalarına erişmesi gerekir.** Bu, geliştirme araçları için uygun yolu ayarlayıp veya bu dosyaları uygulama geliştirme alanına kopyalayıp bunu gerçekleştirebilirsiniz.*

## <a name="using-netx-duo"></a>NetX Duo kullanma

NetX Duo'ları kullanmak oldukça kolaydır. Temel olarak, uygulama kodu derleme sırasında ***nx_api.h** _ öğesini içermeli ve NetX Duo kitaplığı _*_nx.a_*_ (veya _ *_nx.lib_*)* ile bağlantı oluşturmalı.

Bir NetX Duo uygulaması oluşturmak için gereken dört kolay adım aşağıda ve ve aşağıda ve listelemektedir:

| Adım  | Description  |
|---|---|
|&nbsp;1. Adım: |NetX Duo nx_api veri yapılarını kullanan tüm uygulama dosyalarına ***nx_api.h*** dosyasını dahil etmek.|
|&nbsp;2. Adım: |_ tx_application_define * işlevinden veya **bir uygulama iş parçacığından****_nx_system_initialize_* _ çağırarak NetX Duo sistemini başlatma.|
|&nbsp;3. Adım: |Gerekirse bir IP örneği oluşturun, Gerekirse Adres Çözümleme Protokolü'nx_system_initialize ***etkinleştirin.***|
|&nbsp;4. Adım: |Uygulama kaynağını ve bağlantısını NetX Duo çalışma zamanı kitaplığı ***nx.a** _ (veya _*_nx.lib **) ile derle._ Sonuçta elde edilen görüntü hedefe indirilir ve yürütülür!|

## <a name="troubleshooting"></a>Sorun giderme

Her NetX Duo bağlantı noktası, gerçek bir ağ üzerinde veya sanal ağ sürücüsü aracılığıyla yürütülen bir veya daha fazla gösterimle birlikte teslim edilir. Tanıtım sisteminin ilk olarak çalıştırılana kadar her zaman iyi bir fikirdir.

Tanıtım sistemi düzgün çalışmazsa, sorunu daraltmak için aşağıdaki işlemleri gerçekleştirin:

1. Gösterimin ne kadar çalıştırı olduğunu belirleme.
2. Yeni uygulama iş parçacıklarında yığın boyutlarını artırma.
3. NetX Duo kitaplığını yapılandırma seçeneği bölümünde listelenen uygun hata ayıklama seçenekleriyle yeniden derleme.
4. Paketlerin gönder NX_IP alınarak alın mı olduğunu görmek için NX_IP yapısını inceleme.
5. Varsayılan paket havuzunu incelenin ve kullanılabilir paket olup olamay olduğunu kontrol etmek için.
6. Ağ sürücüsünün IPv4 veya IPv6 bağlantısı gerektiren uygulamalar için 4 bayt sınırlarda üst bilgileriyle birlikte ARP ve IP paketleri temin olduğundan emin olun.
7. Sorunun kaybolur mu yoksa değişir mi olduğunu görmek için son yapılan değişiklikleri geçici olarak atlar. Bu tür bilgiler Microsoft destek mühendisleri için faydalı olacaktır.

Sorun giderme adımlarından toplanan bilgileri göndermek için 12. sayfada yer alan "What We Need From You" (Sizden NeLere Ihtiyacımız Var) sayfasında açıklanan yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma Seçenekleri

NetX Duo kitaplığını ve uygulamayı NetX Duo kullanarak oluşturmanın çeşitli yapılandırma seçenekleri vardır. Yapılandırma seçenekleri uygulama kaynağında, komut satırı üzerinde veya aksi belirtilmedikçe ***nx_user.h*** include dosyasında tanımlanabilir.

> [!NOTE]
> ***nx_user.h'de tanımlanan*** seçenekler yalnızca uygulama ve NetX Duo kitaplığı NX_INCLUDE_USER_DEFINE_FILE **uygulanır.***

Aşağıdaki bölümlerde NetX Duo'da kullanılabilen yapılandırma seçenekleri listelanmaktadır. Hem IPv4 hem de IPv6 için geçerli genel seçenekler önce listelenir ve ardından IPv6'ya özgü seçenekler listelenir.

### <a name="system-configuration-options"></a>Sistem Yapılandırma Seçenekleri

| Seçenek  | Açıklama  |
|---|---|
| NX_ASSERT_FAIL    | Onay başarısız olduğunda kullanmak üzere hata ayıklama deyimini tanımlayan sembol.                               |
| NX_DEBUG           | Tanımlı, RAM Ethernet ağ sürücüsünden kullanılabilen isteğe bağlı yazdırma hata ayıklama bilgilerini sağlar. |
| NX_DEBUG_PACKET   | Tanımlı, RAM Ethernet ağ sürücüsünde kullanılabilen isteğe bağlı hata ayıklama paketi dökümlerini sağlar.      |
| NX_DISABLE_ASSERT | Tanımlı, kaynak kodda ASSERT denetimlerini devre dışı bırakıyor. Varsayılan olarak bu seçenek tanımlanmamıştır.            |
|NX_DISABLE_ERROR_CHECKING | Tanımlanan, temel NetX Duo hata denetleme API'sini kaldırır ve performansı artırır. Hata denetimi devre dışı bırakarak etkilenmeen API dönüş kodları, API tanımında kalın yazı tipiyle listelenir. Bu tanım genellikle uygulama yeterince hata ayıklandıktan sonra kullanılır ve kullanımı performansı artırır ve kod boyutunu artırır.|
|NX_DRIVER_DEFERRED_PROCESSING | Tanımlı, ertelenen ağ sürücüsü paket işlemeyi sağlar. Bu, ağ sürücüsünün IP örneğine bir paket depolamasını ve NetX Duo iç IP yardımcı iş parçacığından çağrılan gerçek işleme yordamını edinerek sağlar.|
|NX_DUAL_PACKET_POOL_ENABLE | ***** NX_ENABLE_DUAL_PACKET_POOL _. Hala desteklense de, yeni tasarımların __*_ veya **NX_ENABLE_DUAL_PACKET_POOL teşvik edilmiştir.|
|NX_ENABLE_DUAL_PACKET_POOL | Tanımlı, yığının biri büyük yük boyutuna ve biri daha küçük yük boyutuna sahip olmak üzere iki paket havuzu kullanmalarına olanak sağlar. Varsayılan olarak bu seçenek etkin değildir.|
|NX_ENABLE_EXTENDED_NOTIFY_SUPPORT| Tanımlı, yığında daha fazla geri çağırma kancası sağlar. Bu geri çağırma işlevleri BSD sarmalayıcı katmanı tarafından kullanılır. Varsayılan olarak bu seçenek tanımlanmamıştır.|
|NX_ENABLE_INTERFACE_CAPABILITY| Tanımlı, arabirim cihazı sürücüsünün sağlama dışı yükleme gibi ek özellik bilgileri belirtmesine olanak sağlar. Varsayılan olarak bu seçenek tanımlanmamıştır.|
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