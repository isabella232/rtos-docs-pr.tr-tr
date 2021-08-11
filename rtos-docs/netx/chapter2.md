---
title: Bölüm 2-Azure RTOS NetX yükleme ve kullanımı
description: Bu bölümde, Azure RTOS NetX yüksek performanslı ağ yığınının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 942250cf864fca3c35b97ae731549c070ac2f2f2ef3ef8897e5cbf1e705e7c6a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801827"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx"></a>Bölüm 2-Azure RTOS NetX yükleme ve kullanımı

Bu bölümde, Azure RTOS NetX yüksek performanslı ağ yığınının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="host-considerations"></a>Ana bilgisayar konuları

katıştırılmış geliştirme genellikle Windows veya Linux (unıx) ana bilgisayar bilgisayarlarında gerçekleştirilir. Uygulama derlendikten, bağlanır ve çalıştırılabilir dosya konakta üretildikten sonra, yürütme için hedef donanıma indirilir.

Genellikle hedef indirme işlemi geliştirme aracının hata ayıklayıcı içinden yapılır. İndirmeden sonra, hata ayıklayıcı, hedef yürütme denetimi (go, dur, kesme noktası vb.) ve bellek ve işlemci kayıtlarına erişimi sağlamaktan sorumludur.

Çoğu geliştirme aracı hata ayıklayıcıları, JTAG (IEEE 1149,1) ve arka plan hata ayıklama modu (BDM) gibi yonga hata ayıklama (OCD) bağlantıları aracılığıyla hedef donanımla iletişim kurar. Hata ayıklayıcılar Ayrıca In-Circuit öykünme (buz) bağlantıları aracılığıyla hedef donanımla iletişim kurar. OCD ve ıCE bağlantıları, hedef yerleşik yazılımda en az yetkisiz erişim sağlayan güçlü çözümler sağlar.

Konakta kullanılan kaynaklar için, NetX kaynak kodu ASCII biçiminde dağıtılır ve konak bilgisayarın sabit diskinde yaklaşık 1 MB alan gerektirir.

## <a name="target-considerations"></a>Hedef konuları

NetX, hedefte 5 Kbayt ve 45 Kbayt Read-Only bellek (ROM) arasında olmalıdır. NetX iş parçacığı yığını ve diğer genel veri yapıları için hedefin rastgele erişim belleği (RAM) için 1 ile 5 kilobayt arasında bir değer gereklidir.

Ayrıca NetX, iki ThreadX Zamanlayıcı nesnesinin ve bir ThreadX mutex nesnesinin kullanılmasını gerektirir. Bu tesisler, NetX protokol yığını içinde düzenli işleme ihtiyaçları ve iş parçacığı koruması için kullanılır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX, konumundaki ortak kaynak kodu deposundan elde edilebilir <https://github.com/azure-rtos/netx/> .

Depodaki birçok önemli dosyanın listesi aşağıda verilmiştir:

- ***nx_api. h***: tüm sistem eşlerini, veri yapılarını ve hizmet prototiplerini Içeren C üstbilgi dosyası.
- ***nx_port. h***: tüm geliştirme araçlarını ve hedefe özgü veri tanımlarını ve yapılarını Içeren C üstbilgi dosyası.  
- küçük bir demo uygulaması içeren ***demo_netx. c***: c dosyası.
- ***NX. a (veya NX. lib)** _: _standard * paketiyle dağıtılan NETX C kitaplığının ikili sürümü.             |

## <a name="netx-installation"></a>NetX yüklemesi

GitHub deposunu yerel makinenize kopyalayarak netx 'i yükleyebilirsiniz. Bilgisayarınızda NetX deposunun bir kopyasını oluşturmak için tipik sözdizimi aşağıda verilmiştir:

```c
    git clone https://github.com/azure-rtos/netx
```

alternatif olarak, GitHub ana sayfasındaki **indir** düğmesini kullanarak deponun bir kopyasını indirebilirsiniz.

Ayrıca, çevrimiçi deponun ön sayfasında NetX kitaplığını oluşturmaya yönelik yönergeler de bulacaksınız.

> [!IMPORTANT]
> Uygulama yazılımının NetX kitaplık dosyasına erişmesi gerekir (genellikle ***NX. a** _ veya _*_NX. lib_*_) ve C içerme dosyaları _ *_nx_api. h ve nx_port. h_* *. Bu, geliştirme araçları için uygun yol ayarlanarak veya bu dosyaları uygulama geliştirme alanına kopyalayarak gerçekleştirilir.

## <a name="using-netx"></a>NetX kullanma

NetX kullanmak için, uygulama kodu derleme sırasında ***nx_api. h** _ Içermeli ve NETX Kitaplığı _*_NX. a_*_ (veya _ *_NX. lib_*) * ile bağlantı içermelidir.

NetX uygulaması oluşturmak için gereken dört adım aşağıda verilmiştir:

1. NetX Hizmetleri veya veri yapıları kullanan tüm uygulama dosyalarına ***nx_api. h*** dosyasını dahil edin.
1. _ *_Tx_application_define_** işlevinden veya bir uygulama iş parçacığından ***Nx_system_initialize** _ çağırarak NETX sistemini başlatın.  
1. Bir IP örneği oluşturun, gerekirse Adres Çözümleme Protokolü 'Nü (ARP) ve ***nx_system_initialize*** sonra tüm yuvaları etkinleştirin.  
1. Uygulama kaynağını derleyin ve NetX çalışma zamanı kitaplığı ***NX. a** _ (veya _ *_NX. lib_* *) ile ilişkilendirin. Elde edilen görüntü hedefe indirilebilir ve yürütülür!

## <a name="troubleshooting"></a>Sorun giderme

Her NetX bağlantı noktası, gerçek bir ağ üzerinde veya sanal ağ sürücüsü aracılığıyla yürütülen bir veya daha fazla örnek ile birlikte dağıtılır. Öncelikle örnek sistemi çalıştırmak için her zaman iyi bir fikirdir.

Örnek sistem düzgün çalışmıyorsa, sorunu daraltmak için aşağıdaki işlemleri gerçekleştirin:

1. Örneğin ne kadarının çalıştığını saptayın.
2. Yeni uygulama iş parçacıklarında yığın boyutlarını artırın.
3. NetX kitaplığını yapılandırma seçeneği bölümünde listelenen uygun hata ayıklama seçenekleriyle yeniden derleyin.
4. Paketlerin gönderilip gönderilmediğini veya alındığını görmek için **NX_IP** yapısını inceleyin.
5. Kullanılabilir paketlerin olup olmadığını görmek için varsayılan paket havuzunu inceleyin.
6. Ağ sürücüsünün, IP bağlantısı gerektiren uygulamalar için 4 baytlık sınırlardaki üst bilgilerini içeren ARP ve IP paketleri sağladığı emin olun.
7. Sorunun kaybolup olmadığını veya değişiklik olduğunu görmek için son değişiklikleri geçici olarak atlayın. Bu tür bilgiler, destek mühendislerimiz için yararlı olmalıdır.

Sorun giderme adımlarından toplanan bilgileri göndermek için, [Müşteri Destek Merkezi](about-this-guide.md) konusunda özetlenen yordamları izleyin.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NETX kitaplığı ve NetX kullanan uygulamayı oluştururken birkaç yapılandırma seçeneği vardır. Yapılandırma seçenekleri, aksi belirtilmedikçe, uygulama kaynağında, komut satırında veya ***nx_user. h*** içerme dosyası içinde tanımlanabilir.

> [!IMPORTANT]
> ***Nx_user. h** _ ' de tanımlanan seçenekler, yalnızca uygulama ve NETX kitaplığı _ *NX_INCLUDE_USER_DEFINE_FILE** tanımlı ile derlenme uygulandığında uygulanır.

Aşağıdaki bölümlerde NetX 'de kullanılabilen yapılandırma seçenekleri listelenmektedir.

### <a name="system-configuration-options"></a>Sistem yapılandırma seçenekleri  

| Seçenek  | Açıklama  |
|---|---|
| X_DEBUG | Tanımlı, RAM Ethernet ağ sürücüsünden kullanılabilen isteğe bağlı yazdırma hata ayıklama bilgilerini sunar. |
| NX_DISABLE_ERROR_CHECKING | Tanımlanmıştır, temel NetX hata denetimi API 'sini kaldırır ve performansı geliştirir. Hata denetimini devre dışı bırakarak etkilenmeyen API dönüş kodları, API tanımında kalın yazı tipiyle listelenmiştir. Bu tanımlama genellikle uygulamanın hata ayıklaması yapıldıktan sonra ve kullanımı performansı artırdığında ve kod boyutunu azalttığında kullanılır. |
| NX_DRIVER_DEFERRED_PROCESSING | Tanımlı, ertelenmiş ağ sürücüsü paket işleme etkinleştirilir. Bu, ağ sürücüsünün IP örneğine bir paket yerleştirmesini ve NetX iç IP Yardımcısı iş parçacığından, gerçek işleme yordamının çağrılmasına izin verir. |
| NX_ENABLE_EXTENDED_NOTIFY_SUPPORT | Yığında daha fazla geri çağırma kancaları sunar. Bu geri çağırma işlevleri, BSD sarmalayıcı katmanı tarafından kullanılır. Varsayılan olarak bu seçenek tanımlı değildir. |
| NX_ENABLE_SOURCE_ADDRESS_CHECK | Tanımlı, gelen paketin kaynak adresinin denetlenmesini sağlar. Varsayılan olarak bu seçenek devre dışıdır. |
| NX_LITTLE_ENDIAN | Tanımlı, protokol üstbilgilerinin doğru big endian biçimde olduğundan emin olmak için little endian ortamlarında gerekli bayt takas işlemini gerçekleştirir. Varsayılan değer genellikle ***nx_port. h***' de kurulumlardır. |
| NX_MAX_PHYSICAL_INTERFACES | Cihazdaki toplam fiziksel ağ arabirimi sayısını belirtir. Varsayılan değer 1 ' dir ve ***nx_api. h***' de tanımlanmıştır. Bir cihazın en az bir fiziksel arabirimi olmalıdır. Not geri döngü arabirimini içermez. |
| NX_PHYSICAL_HEADER | Çerçevenin fiziksel üstbilgisinin boyutunu bayt cinsinden belirtir. Varsayılan değer 16 ' dır (32 bitlik sınıra hizalanmış tipik bir 14 baytlık Ethernet çerçevesine göre) ve ***nx_api. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_user. h_*. * gibi _*_nx_api. h_*_ dahil etmeden önce değeri tanımlayarak varsayılanı geçersiz kılabilir. |

### <a name="arp-configuration-options"></a>ARP yapılandırma seçenekleri  

| Seçenek  | Açıklama  |
|---|---|
| NX_ARP_DEFEND_BY_REPLY | Tanımlı, NetX 'in bir ARP yanıtı göndererek IP adresini savunmasına olanak tanır. |
| NX_ARP_DEFEND_INTERVAL | , Saniye cinsinden, ARP modülünün bir gelen ARP iletisine yanıt olarak bir sonraki savunı paketini gönderdiği bir adresi, çakışmanın bir adres olduğunu belirten bir şekilde tanımlar. |
| NX_ARP_DISABLE_AUTO_ARP_ENTRY | **NX_DISABLE_ARP_AUTO_ENTRY** olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların **NX_DISABLE_ARP_AUTO_ENTRY** kullanması önerilir.
| NX_ARP_EXPIRATION_RATE | ARP girişlerinin geçerli kaldığı saniye sayısını belirtir. Varsayılan sıfır değeri, ARP girdilerinin süre sonunu veya eskime süresini devre dışı bırakır ve ***nx_api. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir.
| NX_ARP_MAC_CHANGE_NOTIFICATION_ENABLE | **NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION** olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların **NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION** kullanması önerilir. |
| NX_ARP_MAX_QUEUE_DEPTH | Bir ARP yanıtı beklenirken sıraya alınabilen en fazla paket sayısını belirtir. Varsayılan değer 4 ' dir ve ***nx_api. h***' de tanımlanmıştır. |
| NX_ARP_MAXIMUM_RETRIES | ARP yanıtı olmadan gerçekleştirilen en fazla ARP yeniden deneme sayısını belirtir. Varsayılan değer 18 ' dir ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_* * dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_ARP_UPDATE_RATE | ARP yeniden denemeleri arasındaki saniye sayısını belirtir. Varsayılan değer 10 saniye temsil eden 10 ' dur ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_* * dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_DISABLE_ARP_AUTO_ENTRY | Tanımlı, ARP istek bilgilerini ARP önbelleğinde girmeyi devre dışı bırakır. |
| NX_DISABLE_ARP_INFO | Tanımlı, ARP bilgi toplamayı devre dışı bırakır. |
| NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION | Tanımlı, ARP 'nin MAC adresini algılama üzerinde bir geri çağırma bildirim işlevi çağırmasına izin verir. |

### <a name="icmp-configuration-options"></a>ICMP yapılandırma seçenekleri  

| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_ICMP_INFO | Tanımlı, ıCMP bilgi toplamayı devre dışı bırakır. |
| NX_DISABLE_ICMP_RX_CHECKSUM | Alınan ıCMP paketlerinde ıCMP sağlama toplamı hesaplamasını devre dışı bırakır. Bu seçenek, ağ arabirimi sürücüsü ıCMP sağlama toplamını doğrulayabilip, uygulamanın IP parçalama özelliğini kullanmasının ardından yararlı olur. Varsayılan olarak bu seçenek tanımlı değildir. |
| NX_DISABLE_ICMP_TX_CHECKSUM | İletilen ıCMP paketlerinde ıCMP sağlama toplamı hesaplamasını devre dışı bırakır. Bu seçenek, ağ arabirimi sürücüsünün ıCMP sağlama toplamını hesapladığı ve uygulamanın IP parçalama özelliğini kullanmayan durumlarda faydalıdır. Varsayılan olarak bu seçenek tanımlı değildir. |

### <a name="igmp-configuration-options"></a>IGMP yapılandırma seçenekleri  

| Seçenek  | Açıklama  |
|---|---| 
| NX_DISABLE_IGMP_INFO | Tanımlı, ıGMP bilgi toplamayı devre dışı bırakır. |
| NX_DISABLE_IGMPV2 | Tanımlı, IGMPv2 desteğini devre dışı bırakır ve NetX yalnızca IGMPv1 destekler. Varsayılan olarak bu seçenek ayarlı değildir ve ***nx_api. h***' de tanımlanmıştır. |
| NX_MAX_MULTICAST_GROUPS | Birleştirilebilecek en fazla çok noktaya yayın grubu sayısını belirtir. Varsayılan değer 7 ' dir ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |

### <a name="ip-configuration-options"></a>IP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_FRAGMENTATION | Tanımlı, IP parçalama ve yeniden birleştirme mantığını devre dışı bırakır. |
| NX_DISABLE_IP_INFO | Tanımlı, IP bilgilerini toplamayı devre dışı bırakır. |
| NX_DISABLE_IP_RX_CHECKSUM | Tanımlı, alınan IP paketlerindeki sağlama toplamı mantığını devre dışı bırakır. Bu, ağ aygıtı IP üstbilgisi sağlama toplamını doğrulayabilip, uygulamanın IP parçalanması kullanmasının ardından yararlı olur. |
| NX_DISABLE_IP_TX_CHECKSUM | Tanımlı, gönderilen IP paketlerindeki sağlama toplamı mantığını devre dışı bırakır. Bu, temel alınan ağ cihazının IP üst bilgisi sağlama toplamını oluşturma yeteneğine sahip olduğu ve uygulamanın IP parçalanması kullanmadığı durumlarda faydalıdır. |
| NX_DISABLE_LOOPBACK_INTERFACE | Tanımlı, geri döngü arabirimi için NetX desteğini devre dışı bırakır. |
| NX_DISABLE_RX_SIZE_CHECKING | Tanımlı, alınan paketlerin boyut denetimini devre dışı bırakır. |
| NX_ENABLE_IP_STATIC_ROUTING | Tanımlı, hedef adrese belirli bir sonraki atlama adresi atanabileceği IP statik yönlendirmeye izin vermez. Varsayılan olarak IP statik yönlendirme devre dışıdır. |
| NX_IP_PERIODIC_RATE | Tanımlı, bir saniye içinde ThreadX süreölçer onay işareti sayısını belirtir. Varsayılan değer, varsayılan olarak 100 (10 MS zamanlayıcı) olarak ayarlanan ThreadX symbol **TX_TIMER_TICKS_PER_SECOND** türetilir. NetX modüllerinin geri kalanı **NX_IP_PERIODIC_RATE *** ' dan zamanlama bilgilerini türetecağından uygulamalar bu değeri değiştirirken dikkatli olacaktır. |
| NX_IP_ROUTING_TABLE_SIZE | Tanımlı, bir giden arabirim ve sonraki atlama listesi olan IP statik yönlendirme tablosundaki en fazla girdi sayısını ayarlar
belirli bir hedef adresi için adresler. Varsayılan değer 8 ' dir ve ***nx_api. h** ' de tanımlanmıştır. _ Bu sembol yalnızca _ *NX_ENABLE_IP_STATIC_ROUTING** tanımlanmışsa kullanılır. |

### <a name="packet-configuration-options"></a>Paket yapılandırma seçenekleri  

| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_PACKET_INFO | Tanımlı, paket havuzu bilgileri toplamayı devre dışı bırakır. | 
| NX_PACKET_HEADER_PAD | Tanımlı, NX_PACKET denetim bloğunun sonuna doğru doldurma imkanı sunar. Panel için **ulong** sözcüklerinin sayısı **NX_PACKET_HEADER_PAD_SIZE** tarafından tanımlanır. |
| NX_PACKET_HEADER_PAD_SIZE | NX_PACKET yapısına eklenecek **ulong** sözcüklerinin sayısını ayarlar ve paket yük alanının istendiği zaman başlatılmasına izin verir
hizalar. Bu özellik, arabellek tanımlayıcıları alma işlemini doğrudan NX_PACKET yük alanına eklemek ve ağ arabirimi alma mantığı veya önbellek işlemi mantığı, arabellek başlangıç adresinin belirli hizalama gereksinimlerini karşılamasını bekler. Bu değer yalnızca **NX_PACKET_HEADER_PAD** tanımlandığında geçerli olur. |

### <a name="rarp-configuration-options"></a>RARP yapılandırma seçenekleri  

| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_RARP_INFO | Tanımlı, RARP bilgi toplamayı devre dışı bırakır. |

### <a name="tcp-configuration-options"></a>TCP yapılandırma seçenekleri

| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_RESET_DISCONNECT | Tanımlanan zaman aşımı değeri **NX_NO_WAIT** olarak belirtildiğinde, bağlantı kesme sırasında sıfırlama işlemini devre dışı bırakır. |
| NX_DISABLE_TCP_INFO | Tanımlı, TCP bilgi toplamayı devre dışı bırakır. |
| NX_DISABLE_TCP_RX_CHECKSUM | Tanımlı, alınan TCP paketlerinde sağlama toplamı mantığını devre dışı bırakır. Bu yalnızca bağlantı katmanının güvenilir sağlama toplamı veya CRC işleme sahip olduğu durumlarda faydalıdır veya arabirim sürücüsü donanımda TCP sağlama toplamını doğrulayabilecektir. |
| NX_DISABLE_TCP_TX_CHECKSUM | Tanımlı, TCP paketleri göndermek için sağlama toplamı mantığını devre dışı bırakır. Bu yalnızca, alan ağ düğümünde alınan TCP sağlama toplamı mantığının devre dışı bırakıldığı veya temeldeki ağ sürücüsünün TCP sağlama toplamını oluşturma yeteneğine sahip olduğu durumlarda faydalıdır. |
| NX_ENABLE_TCP_KEEPALIVE | Tanımlı, isteğe bağlı TCP KeepAlive zamanlayıcısını sunar. Varsayılan ayarlar etkin değil. |
| NX_ENABLE_TCP_MSS_CHECKING | Tanımlı, bir TCP bağlantısını kabul etmeden önce en düşük eş ağın doğrulanmasını mümkün. Bu özelliği kullanmak için sembol **NX_ENABLE_TCP_MSS_MINIMUM** tanımlanmalıdır. Varsayılan olarak, bu seçenek etkin değildir. |
NX_ENABLE_TCP_WINDOW_SCALING | TCP uygulamaları için pencere ölçeklendirme seçeneğini sunar. Tanımlandıysa, TCP bağlantı aşamasında pencere ölçekleme seçeneği görüşülür ve uygulama, 64K 'dan daha büyük bir pencere boyutu belirtebilir. Varsayılan ayar etkin değil (tanımlı değil). |
| NX_MAX_LISTEN_REQUESTS | Maksimum sunucu dinleme isteği sayısını belirtir. Varsayılan değer 10 ' dur ve ***nx_api. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_ACK_EVERY_N_PACKETS | ACK gönderilmeden önce alacak olan TCP paketlerinin sayısını belirtir. Not **NX_TCP_IMMEDIATE_ACK** etkinse ancak **NX_TCP_ACK_EVERY_N_PACKETS** değilse, bu değer geriye dönük uyumluluk için otomatik olarak 1 ' e ayarlanır. |
| NX_TCP_ACK_TIMER_RATE | TCP Gecikmeli onay işleme için süreölçer oranını hesaplamak üzere sistem işaretleri (NX_IP_PERIODIC_RATE) sayısının nasıl bölüneceğini belirtir. Varsayılan değer, 200ms 'yi temsil eden 5 ' tir ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_* * dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_ENABLE_KEEPALIVE | **NX_ENABLE_TCP_KEEPALIVE** olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların **NX_ENABLE_TCP_KEEPALIVE** kullanması önerilir. |
| NX_TCP_ENABLE_WINDOW_SCALING | **NX_ENABLE_TCP_WINDOW_SCALING** olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların **NX_ENABLE_TCP_WINDOW_SCALING** kullanması önerilir. |
| NX_TCP_FAST_TIMER_RATE | Hızlı TCP Zamanlayıcı oranını hesaplamak için NetX iç onay işareti (NX_IP_PERIODIC_RATE) sayısının nasıl bölüneceğini belirtir. Hızlı TCP süreölçeri, Gecikmeli onay süreölçeri dahil olmak üzere çeşitli TCP zamanlayıcılarını sağlamak için kullanılır. Varsayılan değer 10 ' dur ve ThreadX zamanlayıcısının 10ms 'de çalıştığı varsayılarak 100 ms 'yi temsil eder. Bu değer ***nx_tcp. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_api. h_* * dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_IMMEDIATE_ACK | Tanımlı, isteğe bağlı TCP anında BILDIRIM yanıtı işlemesini mümkün bir şekilde sunar. Bu sembolün tanımlanması **NX_TCP_ACK_EVERY_N_PACKETS** 1 olarak tanımlanmasıyla eşdeğerdir. |
| NX_TCP_KEEPALIVE_INITIAL | KeepAlive süreölçeri etkinleşmeden önce geçen işlem yapılmayan saniye sayısını belirtir. Varsayılan değer, 2 saati temsil eden 7200 ' dir ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_* * dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_KEEPALIVE_RETRIES | Bağlantının bozuk olması için kaç tane canlı tutma yeniden denemeye izin verileceğini belirtir. Varsayılan değer 10 yeniden denemeyi temsil eden 10 ' dur ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_KEEPALIVE_RETRY | Canlı tutma zamanlayıcısında bağlantının diğer tarafının yanıt vermediğini varsayarak geçen saniye sayısını belirtir. Varsayılan değer, yeniden denemeler arasındaki 75 saniyeyi temsil eden 75 ' dir ve ***nx_tcp. h** _ içinde tanımlanır. Uygulama, _ *_nx_api. h_** dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_MAX_OUT_OF_ORDER_PACKETS | TCP yuvası alma kuyruğunda tutulabileceğini en fazla sıralı TCP paketi sayısını tanımlayan simge. Bu simge, TCP alma yuvasında sıraya alınmış paketlerin sayısını sınırlandırmak için kullanılabilir ve paket havuzunun başlatılmasını önler. Varsayılan olarak, bu simge tanımlı değildir, bu nedenle TCP yuvasında sırada sıraya alınan paketlerin sayısı için bir sınır yoktur. |
| NX_TCP_MAXIMUM_RETRIES | Bağlantının bozuk olması için kaç veri aktarımı yeniden denenmesine izin verileceğini belirtir. Varsayılan değer 10 yeniden denemeyi temsil eden 10 ' dur ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_* * dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_MAXIMUM_TX_QUEUE | TCP gönderme istekleri askıya alınmadan veya reddedilmeden önce TCP iletme sırasının en yüksek derinliğini belirtir. Varsayılan değer 20 ' dir ve bu, en fazla 20 paketin belirli bir zamanda iletme kuyruğunda olabileceği anlamına gelir. Paket verilerinin bir kısmını veya tümünü içeren bir ACK bağlantının diğer tarafından alınana kadar, paket paketleri iletme sırasında kalır. Bu sabit, ***nx_tcp. h** _ içinde tanımlanmıştır. Uygulama, _ *_nx_api. h_* * öğesini eklemeden önce değeri tanımlayarak varsayılanı geçersiz kılabilir. |
| X_TCP_MSS_CHECKING_ENABLED | **NX_ENABLE_TCP_MSS_CHECKING** olarak yeniden adlandırıldı. Yine de desteklenmekle birlikte, yeni tasarımların **NX_ENABLE_TCP_MSS_CHECKING** kullanması önerilir. |
| NX_TCP_MSS_MINIMUM | NetX TCP modülünün kabul ettiği minimum en düşük, değeri tanımlayan simge. Bu özellik **NX_ENABLE_TCP_MSS_CHECK** tarafından etkinleştirildi |
| NX_TCP_RETRY_SHIFT | Yeniden aktarım zaman aşımı süresinin yeniden denemeler arasındaki değişiklik şeklini belirtir. Bu değer 0 ise, ilk yeniden aktarım zaman aşımı sonraki yeniden aktarım zaman aşımları ile aynıdır. Bu değer 1 ise, art arda yapılan her yeniden aktarım uzun olur. Bu değer 2 ise, sonraki her yeniden aktarım zaman aşımı süresi dört kez olur. Varsayılan değer 0 ' dır ve ***nx_tcp. h** _ ' de tanımlanmıştır. Uygulama, _ *_nx_api. h_* * dahil olmak üzere değeri tanımlayarak varsayılan değeri geçersiz kılabilir. |
| NX_TCP_TRANSMIT_TIMER_RATE| TCP iletme yeniden deneme işleminin Zamanlayıcı oranını hesaplamak için sistem işaretleri **NX_IP_PERIODIC_RATE**) sayısının nasıl bölüneceğini belirtir. Varsayılan değer 1 ' dir ve **_nx_tcp. h_ _ ' de tanımlanmıştır.*Uygulama, _ nx_api. h dosyasını eklemeden önce değeri tanımlayarak varsayılanı geçersiz kılabilir***. |

### <a name="udp-configuration-options"></a>UDP yapılandırma seçenekleri
| Seçenek  | Açıklama  |
|---|---|
| NX_DISABLE_UDP_INFO | Tanımlı, UDP bilgi toplamayı devre dışı bırakır. |
| NX_DISABLE_UDP_RX_CHECKSUM | Tanımlı, gelen UDP paketlerindeki UDP sağlama toplamı hesaplamasını devre dışı bırakır. Bu, ağ arabirimi sürücüsü donanımda UDP üst bilgi sağlama toplamını doğrulayabiliyor ve uygulama IP parçalama mantığını etkinleştirmezse yararlıdır. |
| NX_DISABLE_UDP_TX_CHECKSUM | Tanımlı, giden UDP paketlerinde UDP sağlama toplamı hesaplamasını devre dışı bırakır. Bu, ağ arabirimi sürücüsü UDP üst bilgisi sağlama toplamını hesaplarken ve verileri iletmeden önce IP başlığına değer eklerken yararlı olur ve uygulama IP parçalama mantığını etkinleştirmez. |

## <a name="netx-version-id"></a>NetX sürüm KIMLIĞI

Geçerli NetX sürümü, çalışma zamanı sırasında hem Kullanıcı hem de uygulama yazılımı için kullanılabilir. Programcı, **nx_port. h** dosyasından NETX sürümünü alabilir. Ayrıca, bu dosya ilgili bağlantı noktasının sürüm geçmişini içerir. Uygulama yazılımı, **_nx_port.h'de_** genel dize **_nx_version_id Inceler** ve NetX sürümünü elde nx_port.  

Uygulama yazılımı, sürüm bilgilerini aşağıda gösterilen ***nx_api.h .*** içinde tanımlanan sabitlerden de edinebilir

Bu sabitler, geçerli ürün sürümünü ad ve ana ve ikincil sürüme göre tanımladı.

```c
#define EL_PRODUCT_NETX

#define NETX_MAJOR_VERSION

#define NETX_MINOR_VERSION
```