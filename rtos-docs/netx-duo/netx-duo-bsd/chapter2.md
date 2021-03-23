---
title: Bölüm 2-Azure RTOS NetX Duo BSD yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX Duo BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 582661bc66c51341fc098de9ff7b6fa2a7d746de
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826153"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-bsd"></a>Bölüm 2-Azure RTOS NetX Duo BSD yüklemesi ve kullanımı

Bu bölümde, Azure RTOS NetX Duo BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX Duo BSD, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nxd_bsd. h**: NETX Duo BSD için üst bilgi dosyası
- **nxd_bsd. c**: NETX Duo BSD Için c kaynak dosyası
- **nxd_bsd.pdf**: NETX Duo BSD Kullanıcı Kılavuzu

Tanıtım dosyaları:

- **bsd_demo_udp. c**
- **bsd_demo_tcp. c**
- **bsd_demo_raw. c**

## <a name="netx-duo-bsd-installation"></a>NetX Duo BSD yüklemesi

NetX Duo BSD 'yi kullanmak için, daha önce bahsedilen dağıtımın tamamının NetX Duo 'un yüklü olduğu dizine kopyalanması gerekir. Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_bsd. h* ve *nxd_bsd. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="building-the-threadx-and-netx-duo-components-of-a-bsd-application"></a>Bir BSD uygulamasının ThreadX ve NetX Duo bileşenlerini oluşturma

### <a name="threadx"></a>ThreadX

ThreadX Kitaplığı `bsd_errno` iş parçacığı yerel depolama alanında tanımlanmalıdır. Aşağıdaki yordamı öneririz:

1. *Tx_port. h*'de TX_THREAD_EXTENSION makrolarından birini aşağıdaki şekilde ayarlayın:
   - `#define TX_THREAD_EXTENSION_3     int bsd_errno`

1. ThreadX kitaplığını yeniden derleyin.

> [!NOTE]
> TX_THREAD_EXTENSION_3 zaten kullanılıyorsa, Kullanıcı diğer TX_THREAD_EXTENSION makrolarından birini kullanücretsizdir.

### <a name="netx-duo"></a>NetX Duo

NetX Duo BSD hizmetlerini kullanmadan önce, NetX Duo kitaplığı tanımlı NX_ENABLE_EXTENDED_NOTIFY_SUPPORT oluşturulmalıdır. Varsayılan olarak tanımlı değildir. BSD RAW yuvaları kullanılacaksa, NetX Duo kitaplığı tanımlı NX_ENABLE_IP_RAW_PACKET_FILTER oluşturulmalıdır.

## <a name="using-netx-duo-bsd"></a>NetX Duo BSD kullanma

NetX Duo BSD uygulaması projesi, bu kılavuzda daha sonra belirtilen BSD hizmetlerini kullanabilmek için *tx_api. h* ve *nx_api. h* bilgilerini *nxd_bsd* içermelidir. Uygulama, yapı işlemine *nxd_bsd. c* de içermelidir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX Duo BSD 'yi kullanmak için gereklidir.

NetX Duo BSD hizmetlerini kullanmak için, uygulamanın bir IP örneği oluşturması, ' den paket ayırabilmesi için BSD katmanı için bir paket havuzu oluşturması, iç BSD iş parçacığı yığını için bellek alanı ayırması ve iç BSD iş parçacığının önceliğini belirtmesi gerekir. BSD katmanı, *bsd_initialize* çağırarak ve parametrelerine geçerek başlatılır. Bu belgede daha sonra "küçük örneklerde" gösterilmiştir, ancak prototip aşağıda gösterilmiştir:

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                    *CHAR *bsd_thread_stack_area,
                    *ULONG bsd_thread_stack_size,
                    *UINT bsd_thread_priority*);
```

Default_ip, BSD katmanının üzerinde çalıştığı IP örneğidir. Default_pool, BSD Hizmetleri tarafından paketleri ayırmak için kullanılır. Sonraki iki parametre: bsd_thread_stack_area, bsd_thread_stack_size iç BSD iş parçacığı tarafından kullanılan yığın alanını ve bsd_thread_priority son parametresini tanımlar, iş parçacığının önceliğini belirler.

## <a name="netx-duo-bsd-raw-socket-support"></a>NetX Duo BSD Ham yuva desteği

NetX Duo BSD, ham yuvaları da destekler. NetX Duo BSD içindeki ham yuvaları kullanmak için, NetX Duo kitaplığı tanımlı NX_ENABLE_IP_RAW_PACKET_FILTER ile derlenmelidir. Varsayılan olarak tanımlı değildir. Uygulama daha sonra nx_ip_raw_packet_enable çağırarak önceden oluşturulmuş bir IP örneği için ham yuva işlemeyi etkinleştirmelidir *.*

NetX Duo BSD içinde Ham yuva oluşturmak için, uygulama yuva oluşturma hizmeti *yuvasını* kullanır ve protokol ailesini, yuva türünü ve protokolünü belirtir:

```c
sock_1 = socket(INT protocolFamily, INT socket_type, INT protocol)
```

protocolFamily, IP örneğinde IPv6 'nın etkin olduğu varsayılarak IPv4 yuvaları için AF_INET veya IPv6 yuvaları için AF_INET6. Socket_type SOCK_RAW olarak ayarlanmalıdır. protokol uygulamaya özeldir.

Ham paketleri göndermek ve almak ve ham bir yuvayı kapatmak için, uygulama genellikle UDP için aynı BSD hizmetlerini kullanır örn. *SendTo, recvfrom, select* ve *soc_close*. Ham yuvalar, BSD hizmetlerini *kabul* veya *dinlemeyi* desteklemez.

- Varsayılan olarak, alınan IPv4 ham verileri IPv4 üst bilgisini içerir.  Buna karşılık, alınan IPv6 ham verileri IPv6 üst bilgisini içermez.

- Varsayılan olarak, ham IPv6 veya IPv4 paketleri gönderilirken, BSD sarmalayıcı katmanı, verileri göndermeden önce IPv6 veya IPv4 üstbilgisini ekler.

NetX Duo BSD IP_RAW_RX_NO_HEADER, IP_HDRINCL ve IP_RAW_IPV6_HDRINCL dahil ek ham yuva seçeneklerini destekler.

IP_RAW_RX_NO_HEADER ayarlandıysa IPv4 üst bilgisi kaldırılır, böylece alınan veriler IPv4 üst bilgisini içermez ve bildirilen ileti uzunluğu IPv4 üst bilgisini içermez.  IPv6 yuvaları için, varsayılan olarak ham yuva alma, IP_RAW_RX_NO_HEADER seçenek kümesine sahip olacak şekilde IPv6 üst bilgisini içermez. Uygulama, IP_RAW_RX_NO_HEADER seçeneğini temizlemek için *setsockopt* hizmetini kullanabilir, IP_RAW_RX_NO_HEADER seçeneği silinirse, alınan IPv6 RAW verileri IPv6 üst bilgisini içerir ve bildirilen Ileti uzunluğu IPv6 üstbilgisini içerir.

Bu seçeneğin IPv4 veya IPv6 iletilen verileri üzerinde hiçbir etkisi yoktur.

IP_HDRINCL ayarlandıysa, uygulama veri gönderirken IPv4 üst bilgisini içerir.  Bu seçeneğin IPv6 iletimi üzerinde hiçbir etkisi yoktur ve varsayılan olarak tanımlanmamıştır. IP_RAW_IPV6_HDRINCL ayarlandıysa, uygulama veri gönderirken IPv6 üst bilgisini içerir.  Bu seçeneğin IPv4 iletimi üzerinde hiçbir etkisi yoktur ve varsayılan olarak tanımlanmamıştır.

IP_HDRINCL ve IP_RAW_IPV6_HDRINCL IPv4 veya IPv6 alımı üzerinde hiçbir etkiye sahip değildir.

> [!NOTE]
> BSD 4,3 yuva belirtimi, çekirdeğin ham paketi her bir yuva alma arabelleğine kopyalamasını gerektiğini belirtir. Ancak NetX Duo BSD 'de, aynı protokolü paylaşan birden çok yuva oluşturulduysa, davranış tanımsızdır.

## <a name="netx-duo-bsd-raw-packet-support"></a>NetX Duo BSD ham paket desteği

PPPoE için ham paket desteğini etkinleştirmek üzere NetX Duo BSD sarmalayıcısı NX_BSD_RAW_PPPOE_SUPPORT etkinleştirilmiş olarak derlenmelidir.

Aşağıdaki komut, PPPoE ham paketlerini işlemek için bir BSD yuvası oluşturur:

```c
Sockfd = socket(AF_PACKET, SOCK_RAW, protocol);
```

Geçerli BSD uygulamasının AF_PACKET Family 'de yalnızca iki protokol türü desteklenir

- `ETHERTYPE_PPPOE_DISC`: PPPoE bulma paketleri. MAC veri çerçevesinde, bulma paketleri 0x8863 Ethernet çerçeve türüne sahiptir.

- `ETHERTYPE_PPPOE_SESS`: PPP oturum paketleri. MAC veri çerçevesinde, oturum paketleri 0x8864 Ethernet çerçeve türüne sahiptir.

Yapı, `sockaddr_ll` PPPoE çerçevelerini gönderirken veya alırken parametreleri belirtmek için kullanılır.

`struct sockaddr_ll` şöyle bildirilmiştir:

```c
struct sockaddr_ll
{
    USHORT  sll_family;     /* Must be AF_PACKET */
    USHORT  sll_protocol;   /* LL frame type */
    INT     sll_ifindex;    /* Interface Index. */
    USHORT  sll_hatype;     /* Header type */
    UCHAR   sll_pkttype;    /* Packet type */
    UCHAR   sll_halen;      /* Length of address */
    UCHAR   sll_addr[8];    /* Physical layer address */
};
```

> [!NOTE]
> Yapıdaki her alan veya tarafından kullanılmaz `sendto()` `recvfrom()` . `sockaddr_ll`PPPoE paketlerinin gönderilmesi ve alınması için aşağıdaki açıklamaya bakın.

AF_PACKET ailesinde oluşturulan yuva, belirtilen Protokolden bağımsız olarak, PPPoE bulma paketleri veya PPP oturum paketleri göndermek için kullanılabilir. Bir PPPoE paketi iletilirken, uygulama, MAC üstbilgileri (hedef MAC adresi, kaynak MAC adresi ve çerçeve türü) dahil, düzgün şekilde biçimlendirilen PPPoE çerçevesini içeren arabelleği hazırlanmalıdır. Arabelleğin boyutu 14 baytlık Ethernet üstbilgisini içerir.

`sockaddr_ll`Yapısı, `sll_ifindex` Bu paketi göndermek için kullanılacak fiziksel arabirimi belirtmek için kullanılır. Yapıdaki alanların geri kalanı kullanılmaz. Kullanılmayan alanlara ayarlanan değerler BSD iç işlemi tarafından yok sayılır.

Aşağıdaki kod bloğunda bir PPPoE paketinin nasıl iletilmesi gösterilmektedir:

```c
struct sockaddr_ll peer_addr;

/* Transmit a PPPoE frame using the primary network interface. */
peer_addr.sll_ifindex = 0;
n = sendto(sockfd, frame, frame_size, 0, (struct
        sockaddr*)&peer_addr, sizeof(peer_addr));
```

Dönüş değeri, aktarılan bayt sayısını gösterir. PPPoE paketleri ileti tabanlı olduğundan, başarılı bir iletimde, gönderilen bayt sayısı, 14 baytlık Ethernet üst bilgisi dahil olmak üzere paketin boyutuyla eşleşir.

PPPoE paketleri kullanılarak alınabilir `recvfrom()` . Alma arabelleğinin Ethernet MTU boyutu iletisine yetecek kadar büyük olması gerekir. Alınan PPPoE paketi 14 baytlık Ethernet üst bilgisini içerir. PPPoE paketleri alındığında, PPPoE bulma paketleri yalnızca protokol ile oluşturulan yuva tarafından alınabilir `ETHERTYPE_PPPOE_DISC` . Benzer şekilde, PPP oturum paketleri yalnızca protokolle oluşturulan yuva tarafından alınabilir `ETHERTYPE_PPPOE_SESS` . Aynı protokol türü için birden çok yuva oluşturulduysa, gelen PPPoE paketleri ilk oluşturulan yuvaya iletilir. Protokol için oluşturulan ilk yuva kapalıysa, bu paketlerin alınması için oluşturma sırasındaki sonraki yuva kullanılır.

Bir PPPoE paketi alındıktan sonra, yapı içindeki aşağıdaki alanlar `sockaddr_ll` geçerlidir:
- **sll_family**: BSD iç tarafından AF_PACKET olacak şekilde ayarlayın
- **sll_ifindex**: paketin alındığı arabirimi gösterir
- **sll_protocol**: alınan paket türüne ayarlı: `ETHERTYPE_PPPOE_DISC` veya `ETHERTYPE_PPPOE_SESS`

## <a name="eliminating-internal-bsd-thread"></a>Iç BSD Iş parçacığını ortadan kaldırma

Varsayılan olarak, BSD bazı işlemlerini gerçekleştirmek için bir iç iş parçacığını kullanır. Sıkı bellek kısıtlamalarına sahip sistemlerde, BSD, iç BSD iş parçacığını ortadan kaldıran ve bunun yerine aynı işlemi gerçekleştirmek için bir iç süreölçer kullanan NX_BSD_TIMEOUT_PROCESS_IN_TIMER tanımlanmış ile oluşturulabilir. Bu, iç BSD iş parçacığı denetim bloğu ve yığını için gereken belleği ortadan kaldırır. Ancak, genel Zamanlayıcı işlemesi önemli ölçüde artar ve BSD işlemi gerekenden daha yüksek bir önceliğe göre de çalıştırılabilir.

BSD yuvalarını ThreadX Zamanlayıcı bağlamında çalışacak şekilde yapılandırmak için, *nxd_bsd. h* içinde NX_BSD_TIMEOUT_PROCESS_IN_TIMER tanımlayın. BSD katmanı Zamanlayıcı bağlamındaki BSD görevlerini yürütmek üzere yapılandırılmışsa, *bsd_initialize* çağrısında aşağıdaki üç parametre yok SAYıLıR ve null olarak ayarlanmalıdır:

- **bsd_thread_stack_area**
- **bsd_thread_stack_size**
- **bsd_thread_priority**

## <a name="netx-duo-bsd-with-dns-support"></a>DNS desteğiyle NetX Duo BSD

NX_BSD_ENABLE_DNS tanımlanmışsa NetX Duo BSD, ana bilgisayar adı veya ana bilgisayar IP bilgilerini almak için DNS sorguları gönderebilir. Bu özellik, *nx_dns_create* hizmeti kullanılarak bir NETX DNS istemcisinin daha önce oluşturulmasını gerektirir. Bir veya daha fazla bilinen DNS sunucusu IP adresi, IPv4 sunucusu adreslerini eklemek için *nx_dns_server_add* hizmeti kullanılarak veya IPv4 veya IPv6 sunucu adreslerini eklemek için *NXD_DNS_SERVER_ADD* hizmeti kullanılarak DNS örneğine kaydedilmelidir.

DNS hizmetleri ve bellek ayırma, *GetAddrInfo* ve *GetNameInfo* Hizmetleri tarafından kullanılır:

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
        const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
        char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

BSD uygulaması, bir ana bilgisayar adı ile *GetAddrInfo* çağırdığında NETX BSD, IP adresini almak için aşağıdaki hizmetlerden herhangi birini çağırır:

- **nx_dns_ipv4_address_by_name_get**
- **nxd_dns_ipv6_address_by_name_get**
- **nx_dns_cname_get**

*Nx_dns_ipv4_address_by_name_get* ve *nxd_dns_ipv6_address_by_name_get* için netx BSD sırasıyla ipv4_addr_buffer ve ipv6_addr_buffer bellek alanını kullanır. Bu arabelleklerin boyutu, sırasıyla (NX_BSD_IPV4_ADDR_PER_HOST * 4) ve (NX_BSD_IPV6_ADDR_PER_HOST * 16) tarafından tanımlanır.

NETX BSD, *GetAddrInfo*'dan adres bilgilerini döndürmek için, bellek alanı başka bir yapılandırılabilir seçenekler kümesi, NX_BSD_IPV4_ADDR_MAX_NUM ve NX_BSD_IPV6_ADDR_MAX_NUM tarafından tanımlanmış olan Nx_bsd_addrinfo_pool_memory threadx blok bellek tablosunu kullanır.

Yukarıdaki yapılandırma seçenekleri hakkında daha fazla bilgi için bkz. **genel yapılandırma seçenekleri** .

Ayrıca, NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa ve konak girişi kurallı bir ad ise NetX Duo BSD, daha önce oluşturulmuş bir blok havuzundan belleği dinamik olarak ayırır _nx_bsd_cname_block_pool

> [!NOTE]
> *GetAddrInfo* çağrıldıktan sonra, *freeaddrinfo* hizmeti kullanılarak, kaynak bağımsız değişkeni tarafından işaret edilen belleğin blok tabloya geri bırakılması için BSD uygulaması sorumludur.

## <a name="netx-duo-bsd-limitations"></a>NetX Duo BSD sınırlamaları

NetX Duo BSD, performans ve mimari sorunlarından dolayı tüm BSD 4,3 yuva özelliklerini desteklemez:

*Gönderme, alma, SendTo* ve *RECVFROM* çağrılarında Int bayrakları desteklenmez.

## <a name="general-configuration-options"></a>Genel yapılandırma seçenekleri

*Nxd_bsd. h* içindeki kullanıcı yapılandırılabilir seçenekleri, uygulamanın, belirli uygulama gereksinimleri Için NETX Duo BSD yuvaları üzerinde ince ayar yapmasına izin verir.

Derleme zamanında ayarlanan yapılandırılabilir seçeneklerin listesi aşağıda verilmiştir:

- **NX_BSD_TCP_WINDOW**: TCP yuvası oluşturma çağrılarında kullanılır. 64K, 100Mb Ethernet için tipik bir pencere boyutudur. Varsayılan değer 65535 ' dir.

- **NX_BSD_SOCKFD_START**: Bu, BSD yuvası dosya tanımlayıcısı başlangıç değerinin mantıksal dizinidir. Varsayılan olarak, bu seçenek 32 ' dir.

- **NX_BSD_MAX_SOCKETS**: BSD katmanında kullanılabilir olan en fazla toplam yuva sayısını belirtir ve 32 katı olmalıdır. Değer, varsayılan olarak 32 ' dir.

- **NX_BSD_SOCKET_QUEUE_MAX**: alma yuvası sırasında depolanan en fazla UDP paketi sayısını belirtir. Değer, varsayılan olarak 5 ' tir.

- **NX_BSD_MAX_LISTEN_BACKLOG**: Bu, BSD TCP yuvaları için dinleme kuyruğunun boyutunu (' Backlog ') belirtir. Varsayılan değer 5 ' tir.

- **NX_MICROSECOND_PER_CPU_TICK**: Zamanlayıcı Zamanlayıcı numarası başına mikrosaniye sayısını belirtir.

- **NX_BSD_TIMEOUT**: BSD Için gereken NETX Duo iç çağrılarındaki süreölçer işaretleri cinsinden zaman aşımını belirtir. Varsayılan değer (20 * NX_IP_PERIODIC_RATE) değeridir.

- **NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: NETX Duo bağlantı kesme çağrısının süreölçer işaretleri cinsinden zaman aşımını belirtir. Varsayılan değer 1’dir.

- **NX_BSD_PRINT_ERRORS**: ayarlanırsa, bir BSD işlevinin hata durumu dönüşü bir satır numarası ve hata türü döndürür, örneğin hatanın gerçekleştiği NX_SOC_ERROR. Bu, uygulama geliştiricisinin hata ayıklama çıkışını tanımlamasını gerektirir. Varsayılan ayar devre dışıdır ve *nxd_bsd. h* içinde herhangi bir hata ayıklama çıkışı belirtilmez.

- **NX_BSD_TIMER_RATE**: BSD düzenli zamanlayıcı görevinin çalışması için gereken Aralık. Varsayılan değer 1 saniyedir (1 * NX_IP_PERIODIC_RATE).

- **NX_BSD_TIMEOUT_PROCESS_IN_TIMER**: ayarlanırsa, bu seçenek BSD zaman aşımı işleminin sistem Zamanlayıcı bağlamında yürütülmesine izin verir. Varsayılan davranış devre dışıdır. Bu özellik, Bölüm 2 "NetX Duo BSD yüklemesi ve kullanımı" bölümünde daha ayrıntılı olarak açıklanmıştır.

- **NX_BSD_RAW_PPPOE_SUPPORT**: PPPoE ham paket desteğini etkinleştirin. Varsayılan olarak bu seçenek etkin değildir.

- **NX_BSD_ENABLE_DNS**: etkinleştirilirse NETX Duo BSD bir ana bilgisayar adı veya ana bilgisayar IP adresi IÇIN bir DNS sorgusu gönderir. Daha önce oluşturulup başlatılmış bir DNS Istemci örneği gerektirir. Varsayılan olarak etkin değildir.

- **NX_BSD_SOCKET_RAW_PROTOCOL_TABLE_SIZE**: Ham yuva tablosunun boyutunu tanımlar. Değer ikinin üssü olmalıdır. NetX BSD, ham paketlerin gönderilmesi ve alınması için NX_BSD_SOCKETS türünde bir yuva dizisi oluşturur. NX_ENABLE_IP_RAW_PACKET_FILTER etkinleştirilmelidir. Varsayılan olarak 32 ' dir.

- **NX_BSD_IPV4_ADDR_MAX_NUM**: *GetAddrInfo* tarafından döndürülen en fazla IPv4 adresi sayısı. NX_BSD_IPV6_ADDR_MAX_NUM ile birlikte, bu, *GetAddrInfo* içinde bilgi depolamaya yönelik olarak bellek ayırmak Için NETX BSD bloğu havuzunun boyutunu nx_bsd_addrinfo_block_pool tanımlar. Varsayılan değer 5 ' tir.

- **NX_BSD_IPV6_ADDR_MAX_NUM**: *GetAddrInfo* tarafından döndürülen en fazla IPv6 adresi sayısı. NX_BSD_IPV4_ADDR_MAX_NUM ile birlikte, bu, *GetAddrInfo* içinde bilgi depolamaya yönelik olarak bellek ayırmak Için NETX BSD bloğu havuzunun boyutunu nx_bsd_addrinfo_block_pool tanımlar.

- **NX_BSD_IPV4_ADDR_PER_HOST**: DNS sorgusu başına depolanan en yüksek IPv4 adreslerini tanımlar. Varsayılan değer 5 ' tir.

- **NX_BSD_IPV6_ADDR_PER_HOST**: DNS sorgusu başına depolanan en yüksek IPv6 adreslerini tanımlar. Varsayılan değer 2 ' dir.

## <a name="bsd-socket-options"></a>BSD yuvası seçenekleri

Aşağıdaki NetX Duo BSD yuva seçeneklerinin listesi, *setsockopt* hizmeti kullanılarak her yuva temelinde çalışma zamanında etkinleştirilebilir (veya devre dışı bırakılabilir):

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, 
                const void *option_value, INT option_length);
```

Option_level için iki farklı ayar vardır.

Çalışma zamanı yuva seçeneklerinin ilk türü yuva düzeyi seçenekleri için SOL_SOCKET. Yuva düzeyi seçeneğini etkinleştirmek için, *sol_socket olarak ayarlanan* option_level ve option_name belirli bir seçeneğe ayarla ' yı çağırın. örneğin, so_broadcast *.* Bir seçenek ayarı almak için, option_level tekrar SOL_SOCKET olarak ayarlanan option_name için *getsockopt* çağırın.

Çalışma zamanı yuva düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.

- **So_broadcast**: ayarlandıysa, NETX yuvalarından yayın paketlerinin gönderilmesini ve alınmasına izin vermez. Bu, NetX Duo için varsayılan davranıştır. Tüm yuvalarda bu yetenek vardır.

- **SO_ERROR**: *getsockopt* hizmeti kullanılarak belirtilen yuvanın önceki yuva işleminde yuva durumunu elde etmek için kullanılır. Tüm yuvalarda bu yetenek vardır.

- **SO_KEEPALIVE**: AYARLANıRSA, TCP canlı tut özelliğini sunar. Bu, NetX Duo kitaplığının *nx_user. h* içinde tanımlanan NX_TCP_ENABLE_KEEPALIVE oluşturulması gerekir. Bu özellik varsayılan olarak devre dışıdır.

- **SO_RCVTIMEO**: Bu, NETX Duo BSD yuvalarda paketlerin alınması için saniye cinsinden bekleme seçeneğini ayarlar. Varsayılan değer NX_WAIT_FOREVER (0xFFFFFFFF) veya engelleyici olmayan bir etkin ise, NX_NO_WAIT (0x0).

- **SO_RCVBUF**: Bu, TCP yuvasının pencere boyutunu ayarlar. NX_BSD_TCP_WINDOW varsayılan değeri, BSD TCP yuvaları için 64K olarak ayarlanmıştır. 65535 üzerinden boyutu ayarlamak için NetX Duo kitaplığının NX_TCP_ENABLE_WINDOW_SCALING tanımlanması gerekir.

- **SO_REUSEADDR**: ayarlandıysa, bu, birden çok yuvaların bir bağlantı noktasıyla eşleştirilmesini sağlar. Genel kullanım, TCP sunucu soketi içindir. Bu, NetX Duo yuvaları varsayılan davranışıdır.

Çalışma zamanı yuva seçeneklerinin ikinci türü, IP seçenek düzeyidir. Bir IP düzeyi seçeneğini etkinleştirmek için, *setsockopt* ' i çağırın option_level IP_PROTO olarak ayarlayın ve option_name IP_MULTICAST_TTL seçeneğine ayarlayın *.* Bir seçenek ayarı almak için, option_level tekrar IP_PROTO olarak ayarlanan option_name için *getsockopt* çağırın.

Çalışma zamanı IP düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.

- **IP_MULTICAST_TTL**: Bu, UDP yuvaları için yaşam süresini ayarlar. Yuva oluşturulduğunda varsayılan değer NX_IP_TIME_TO_LIVE (0x80). Bu değer, bu yuva seçeneği ile *setsockopt* çağırarak geçersiz kılınabilir.

- **IP_RAW_IPV6_HDRINCL**: Bu seçenek ayarlandıysa, çağıran uygulama, BSD tarafından oluşturulan ham IPv6 yuvaları üzerinde aktarılan verilere bir IPv6 üst bilgisi ve isteğe bağlı olarak uygulama üstbilgileri eklememelidir. Bu seçeneği kullanmak için, IP görevinde Ham yuva işlemenin etkinleştirilmesi gerekir.

- **IP_ADD_MEMBERSHIP**: ayarlanırsa, belirtilen IGMP grubuna katılması için bu seçenekler BSD yuvasını (yalnızca UDP yuvaları için geçerlidir) sağlar.

- **IP_DROP_MEMBERSHIP**: ayarlanırsa, bu seçenekler belirtilen IGMP grubunu BıRAKMAK için BSD yuvasını (yalnızca UDP yuvaları için geçerlidir) sağlar.

- **IP_HDRINCL**: Bu seçenek ayarlandıysa, ÇAĞıRAN uygulamanın IP üst bilgisini ve isteğe bağlı olarak uygulama üst bilgilerini BSD içinde oluşturulan ham IPv4 yuvaları üzerinde aktarılan verilere ekleme gerekir. Bu seçeneği kullanmak için, IP görevinde Ham yuva işlemenin etkinleştirilmesi gerekir.

- **IP_RAW_RX_NO_HEADER**: silinirse, ıPV6 üstbilgisi BSD içinde oluşturulan ham IPv6 yuvaları için alınan verilere dahildir. IPv6 üstbilgileri, BSD RAW IPv6 Yuvaları ' nda varsayılan olarak kaldırılır ve paket uzunluğu IPv6 üst bilgisini içermez.

Ayarlanırsa, IPv4 üstbilgisi, IPv4 türündeki BSD RAW yuvalarda alınan verilerden kaldırılır. IPv4 üstbilgileri, BSD ham IPv4 Yuvaları ' nda varsayılan olarak dahil edilir ve paket uzunluğu IPv4 üst bilgisini içerir.

Bu seçeneğin IPv4 veya IPv6 iletim verisi üzerinde hiçbir etkisi yoktur.

## <a name="small-ipv4-example"></a>Küçük IPv4 örneği

IPv4 ağları için NetX Duo BSD hizmetlerinin nasıl kullanılacağına ilişkin bir örnek aşağıda açıklanmıştır. Bu örnekte, *nxd_bsd. h* içerme dosyası, 8. satırda getirilir. Ardından, IP örneği *bsd_ip* ve paket havuzu *bsd_pool* , 20 ve 21. satırda genel değişkenler olarak oluşturulur. Bu tanıtımda *, _nx_ram_network_driver* bir RAM (sanal) ağ sürücüsü kullanılmıştır. İstemci ve sunucu, bu örnekteki tek IP örneğinde aynı IP adresini paylaşır.

İstemci ve sunucu iş parçacıkları 62 ve 68 satırlarında oluşturulur. Paketleri iletmek için BSD paket havuzu, 78 satırı üzerinde oluşturulur ve 87. satırdaki IP örneği oluşturulurken kullanılır. IP iş parçacığı görevinin *nx_ip_create* çağrısında öncelik 1 verildiğini unutmayın. Bu iş parçacığı, programda en iyi NetX performansı için tanımlanan en yüksek öncelik görevi olmalıdır.

IP örneği, sırasıyla 88 ve 110 satırlarında ARP ve TCP hizmetleri için etkinleştirilir. BSD Hizmetleri 'nin kullanılabilmesi için son gereksinim, BSD için gereken tüm veri yapılarını ve NetX ve ThreadX kaynaklarını ayarlamak üzere 120 satırındaki *bsd_initialize* çağırmalıdır.

Sunucu iş parçacığı girişi işlevi daha sonra tanımlanır. BSD TCP yuvası 149. satırda oluşturulur. Sunucu IP adresi ve bağlantı noktası 160-163 satırları üzerinde ayarlanır. Ana bilgisayarın IP adresine ve bağlantı noktasına uygulanan *hton* ve ağ bayt *sıralaması makrolarının kullanımını aklınızda yazın.* Bu, birden çok baytlık verilerin ağ bayt düzeninde BSD hizmetlerine gönderildiği BSD yuvası belirtimiyle uyumludur.

Ardından, ana sunucu yuvası 166. satırdaki *BIND* hizmeti kullanılarak bağlantı noktasına bağlıdır. Bu, 180. satırdaki *dinleme* HIZMETINI kullanan TCP bağlantı istekleri için dinleme yuvadır. Buradan sunucu iş parçacığı işlevinden *thread_server_entry*, satır 202 ' de *Select* çağrısını kullanarak alma olaylarını denetlemek için döngüler. Alma olayı, okuma için hazırlanma listesi karşılaştırılmasıyla belirlenen bir bağlantı isteği ise, 213 satırı *kabul eder* . Bağlantı isteğini işlemek ve 223 satırındaki bir Istemciye bağlı TCP sunucusu yuvaları ana listesine eklemek için bir alt sunucu yuvası atanır. Yeni bağlantı isteği yoksa, sunucu iş parçacığı daha sonra 236 satırından başlayan for döngüsünde alma olayları için şu anda bağlı olan tüm yuvaları denetler. Alma olayı beklenirken, veri alınana (bağlantı diğer tarafa kapalı) *ve yuva* 277 satırındaki *soc_close* hizmeti kullanılarak kapatıldıktan kadar bu yuvaya *gönderme* ve alma işlemi çağrılır.

Sunucu iş parçacığı kurulduktan sonra, *Thread_client_entry* istemci iş parçacığı girişi işlevi, 326 numaralı satırda bir yuva oluşturur ve 337. satırdaki *Connect* çağrısını kullanarak TCP sunucu yuvasına bağlanır. Ardından, sırasıyla *gönderme* ve *alma hizmetlerini kullanarak paket gönderme ve alma* döngüleri olur. Daha fazla veri alınmadığında, *soc_close* hizmeti kullanılarak 398 satırındaki yuvayı kapatır. Bağlantı kesildikten sonra, istemci iş parçacığı girişi işlevi yeni bir TCP yuvası oluşturur ve while döngüsü 321. satırda başladığında başka bir bağlantı isteği yapar.

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection, sending,
and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQR
    STUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */

ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */

VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */
int     main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{
CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool", 128,
                                pointer, 16384);

    pointer = pointer + 16384;
    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                    0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                    pointer, 2048, 1);
                    pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable ARP \n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize (&bsd_ip, &bsd_pool,pointer, 2048, 2);
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT       status, sock, sock_tcp_server;
ULONG     actual_status;
INT       Clientlen;
INT       i;
UINT      is_set = NX_FALSE;
struct    sockaddr_in serverAddr;
struct    sockaddr_in ClientAddr;

    tx_thread_sleep(100);

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
        &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("Error on Server socket %d create \n", sock_tcp_server);
        return;
    }

    printf("Server socket %d created\n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    serverAddr.sin_port = htons(SERVER_PORT);

    /* Bind this server socket */
    status = bind (sock_tcp_server, (struct sockaddr *) &serverAddr,
                sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error on Server Socket %d Bind \n", sock_tcp_server);
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen (sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error on Server Socket %d Listen\n", sock_tcp_server);
        return;
    }
    else
        printf("Server socket %d listen complete\n", sock_tcp_server);

    /* All set to accept client connections */

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ((status == 0xFFFFFFFF) || (status == 0))
        {

            printf("Error with select. Status 0x%x\n", status);

            continue;
        }

        /* Check for a connection request. */
        is_set = FD_ISSET(sock_tcp_server, &read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,(struct sockaddr*)&ClientAddr,
                        &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i , &master_list)) &&
                (FD_ISSET(i , &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server received no data from Client on
                            socket %d)\n", i);
                        break;
                    }
                    else if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server receiving data from Client on
                            socket %d\n", i);
                        break;
                    }
                    if(status == SERVER_RCV_BUFFER_SIZE) status--;
                    Server_Rcv_Buffer[status] = 0;
                    printf("Server socket %d received %d bytes: %s\n ",
                            i, (ULONG)status, Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                        Client\n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                        Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != NX_SOC_ERROR)
                {
                    printf("Server socket %d closed \n", i);
                }
                else
                {
                    printf("Error on closing Server socket %d \n", i);
                }
            }
        }

    /* Loop back to check any next client connection */
    }
}

CHAR     Client_Rcv_Buffer[100];

VOID     thread_client_entry(ULONG thread_input)
{

INT        status;
INT        sock_tcp_client, length;
struct     sockaddr_in echoServAddr;
struct     sockaddr_in localAddr; /

    /* Let the server side get set up. */
    tx_thread_sleep(200);

    /* Set local port for displaying IP address and port. */
    memset(&localAddr, 0, sizeof(localAddr));
    localAddr.sin_family = AF_INET;
    localAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    localAddr.sin_port = htons(CLIENT_PORT);

    /* Set server port and IP address which we need to connect. */
    memset(&echoServAddr, 0, sizeof(echoServAddr));
    echoServAddr.sin_family = AF_INET;
    echoServAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    echoServAddr.sin_port = htons(SERVER_PORT);

    /* Now make client connections with the server. */
    while (1)
    {

        printf("\n");

        /* Create BSD TCP Socket */
        sock_tcp_client = socket( AF_INET, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n", sock_tcp_client);
            return;
        }

        printf("Client socket %d created\n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr,
                        sizeof(echoServAddr));

        /* Check for error. */
        if (status != OK)
        {
            printf("Error on Client socket %d connect\n", sock_tcp_client);
                    soc_close(sock_tcp_client);
            return;
        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr,
                            &length);

        printf("Client port = %lu , Client = 0x%x,",
            htonl(localAddr.sin_port), htonl(localAddr.sin_addr.s_addr));

        length = sizeof(struct sockaddr_in);

        status = getpeername( sock_tcp_client, (struct sockaddr *)
                            &echoServAddr, &length);

        printf("Remote port = %lu, Remote IP = 0x%x \n",
                htonl(echoServAddr.sin_port),
                htonl(echoServAddr.sin_addr.s_addr));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
            sock_tcp_client);

            status = send(sock_tcp_client, "Hello", (sizeof("Hello")), 0);

            if (status == ERROR)
            {
                printf("Error: Client Socket (%d) send \n", sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,100,0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    380 printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Nothing received by Client on socket %d\n",
                            sock_tcp_client);
                }

                break;
            }
            else
            {
                printf("Client socket %d received %d bytes: %s\n",
                        sock_tcp_client,
                        status, Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = soc_close(sock_tcp_client);

        if (status != ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```

## <a name="small-ipv6-example-system"></a>Küçük IPv6 örnek sistemi

IPv6 ağları için NetX Duo BSD hizmetlerinin nasıl kullanılacağına ilişkin bir örnek aşağıdaki programda açıklanmıştır. Bu örnek, daha önce birkaç önemli farklılık ile açıklanan IPv4 tanıtım programına çok benzer.

İstemci ve sunucu iş parçacıkları, BSD paket havuzu, IP örneği ve BSD başlatması, IPv4 BSD yuvaları için yaptığı gibi olur.

Sunucu iş parçacığı girişi işlevinde *thread_server_entry*, *sockaddr_in6* ve 145-148 numaralı satırlarda *NXD_ADDRESS* veri türlerini kullanarak birkaç IPv6 değişkeni tanımlar. NXD_ADDRESS veri türü aslında hem IPv4 hem de IPv6 adres türlerini saklayabilir.

Daha sonra, sunucu iş parçacığı IP örneğindeki IPv6 ve ICMPv6 'Yı 161 ve 169 numaralı satırda sırasıyla *nxd_ipv6_enable* ve *nxd_icmpv6_enable* hizmetini kullanarak sunar. Sonra, bağlantı yerel ve genel IP adresleri IP örneğiyle kaydedilir. Bu, 180 ve 195 satırlarında *nxd_ipv6_address_set* hizmeti kullanılarak yapılır. Daha sonra, yinelenen adres algılama protokolünü tamamlaması için IP iş parçacığı görevinin yeterince uzun sürmesine izin verebilir ve bu adresleri 201 numaralı satırdaki *tx_thread_sleep* çağrısında geçerli adresler olarak kaydeder.

Sonra TCP sunucusu yuvası, 204 satırındaki AF_INET6 yuva türü giriş bağımsız değişkeniyle oluşturulur. Yuva IPv6 adresi ve bağlantı noktası, 216-221 satırlarında, verileri de BSD yuva Hizmetleri için ağ bayt sırasına koymak üzere *htonl* ve *hton* makroları kullanımını belirterek ayarlar. Buradan, sunucu iş parçacığı girişi işlevi, IPv4 örneği ile neredeyse aynıdır.

İstemci iş parçacığı girişi işlevi *thread_client_entry*, bir sonraki adımda tanımlanmıştır. Bu örnekteki TCP istemcisi TCP sunucusuyla aynı IP örneğini ve IPv6 adresini paylaştığından, IP örneğinde IPv6 veya ICMPv6 hizmetlerini etkinleştirmek zorunda kalmaz. Ayrıca, IPv6 adresi zaten IP örneğiyle birlikte kaydedilir. Bunun yerine, istemci iş parçacığı girişi işlevi yalnızca sunucunun ayarlaması için 368 satırını bekler. Sunucu adresi ve bağlantı noktası ayarlanır, ana bilgisayar 387-392 satırlarında ağ baytı sıralaması makrolarıyla birlikte kullanılır ve ardından Istemci, 412. satırdaki TCP sunucusuyla bağlantı kurabilirsiniz. 378-383. satırlardaki yerel IP adresi veri türlerinin yalnızca 425 ve 434 sırasıyla *GetSockName* ve *GetPeerName* hizmetlerini göstermek için kullanıldığını unutmayın. Veriler ağdan geldiği için, 378-383 satırlarında kullanılan bayt sırası makrolarını barındırmak için ağ.

İstemci iş parçacığı girişi işlevi, bir TCP yuvası oluşturduğu bir döngü girer, bir TCP bağlantısı yapar ve IPv4 örneği ile aynı şekilde daha fazla veri alınana kadar, TCP sunucusuyla veri gönderir ve alır. Ardından, 483. satırdaki yuvayı kapatır, kısa bir süre duraklayıp başka bir TCP yuvası oluşturur ve bir TCP sunucu bağlantısı ister.

IPv4 örneğinde önemli bir *farklılık, AF_INET6* giriş bağımsız değişkenini kullanarak bir IPv6 yuvası belirtmektir. Diğer önemli fark, TCP Istemci *bağlantı* çağrısının bir *sockaddr_in6* veri türü ve bir length bağımsız değişkenini *sockaddr_in6* veri türü boyutuna ayarlamış olması gerektiğidir.

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection,
disconnection, sending, and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */
ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */
VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

int     main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void tx_application_define(void *first_unused_memory)
{
CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool",
    128, pointer, 16384);

    pointer = pointer + 16384;

    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                        0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                        pointer, 2048, 1);
                        pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in enable ARP on BSD IP instance\n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 2);

    /* Check BSD initialize status. */
    if (status)
    {
        error_counter++;
        printf("Error in BSD initialize \n");
    }

    pointer = pointer + 2048;
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT             status, sock, sock_tcp_server;
ULONG           actual_status;
INT             Clientlen;
INT             i;
UINT            is_set = NX_FALSE;
NXD_ADDRESS     ip_address;
struct          sockaddr_in6 serverAddr;
struct          sockaddr_in6 ClientAddr;
UINT            iface_index, address_index;

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
            &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable IPv6 */
    status = nxd_ipv6_enable(&bsd_ip);
    if((status != NX_SUCCESS) && (status != NX_ALREADY_ENABLED))
    {
        printf("Error with IPv6 enable 0x%x\n", status);
        return;
    }

    /* Enable ICMPv6 */
    status = nxd_icmp_enable(&bsd_ip);

    if(status)
    {
        printf("Error with ECMPv6 enable 0x%x\n", status);
        return;
    }

    /* Set the primary interface for our DNS IPv6 addresses. */
    iface_index = 0;

    /* This assumes we are using the primary network interface (index 0). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, NX_NULL, 10,
                                &address_index);

    if (status)
        return;

    /* Set ip_0 interface address. */
    ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    ip_address.nxd_ip_address.v6[0] = htonl(0x20010db8);
    ip_address.nxd_ip_address.v6[1] = htonl(0x0000f101);
    ip_address.nxd_ip_address.v6[2] = 0;
    ip_address.nxd_ip_address.v6[3] = htonl(0x101);

    /* Set the host global IP address. We are assuming a 64
    bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, &ip_address, 64,
                                &address_index);

    if (status)
        return;

    /* Wait for IPv6 stack to finish DAD process. */
    tx_thread_sleep(400);

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET6, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("\nError: BSD TCP Server socket create \n");
        return;
    }

    printf("\nBSD TCP Server socket created %lu \n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    serverAddr.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    serverAddr.sin6_addr._S6_un._S6_u32[2] = 0x0;
    serverAddr.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    serverAddr.sin6_port = htons(SERVER_PORT);
    serverAddr.sin6_family = AF_INET6;

    /* Bind this server socket */
    status = bind(sock_tcp_server, (struct sockaddr *) &serverAddr,
                    sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error: Server Socket Bind \n");
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen(sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error: Server Socket Listen\n");
        return;
    }
    else
        printf("Server Listen complete\n");

    /* All set to accept client connections */
    printf("Now accepting client connections\n");

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ( (status == 0xFFFFFFFF) || (status == 0) )
        {
            printf("Error with select? Status 0x%x. Try again\n", status);

            continue;
        }

        /* Detected a connection request. */
        is_set = FD_ISSET(sock_tcp_server,&read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,
            (struct sockaddr*)&ClientAddr,
            &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {
                printf("New connection %d\n", sock);

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i, &master_list)) &&
                (FD_ISSET(i, &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server socket %d received no data from
                                Client)\n", i);

                        break;
                    }
                    else if (status == 0xFFFFFFFF)
                    {
                        printf("Error on Server socket %d receiving data from
                                Client\n", i);

                        break;
                    }

                    printf("Server socket %d received from Client %lu bytes:
                            %s\n ", i, (ULONG)status,
                            Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                                Client \n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                                Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != ERROR)
                {
                    printf("Server socket %d closing\n", i);
                }
                else
                {

                    printf("Error on Server socket %d closing\n", i);
                }
            }
        }

        /* Loop back to check any next client connection */
    }
}

#define     CLIENT_BUFFER_SIZE 100
CHAR        Client_Rcv_Buffer[CLIENT_BUFFER_SIZE];

VOID        thread_client_entry(ULONG thread_input)
{

INT         status;
INT         sock_tcp_client, length;
struct      sockaddr_in6 echoServAddr6;
struct      sockaddr_in6 localAddr6; address */

    /* Wait for the server side to get set up, including the DAD process. */
    tx_thread_sleep(500);

    /* ICMPv6 and IPv6 should already be enabled on the IP instance
    by the server thread entry function. */

    /* Further the IPv6 address is already established with the IP instance.
    so no need to wait for DAD completion. */

    /* Set local port and IP address (used only for getsockname call). */
    memset(&localAddr6, 0, sizeof(localAddr6));
    localAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    localAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    localAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    localAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    localAddr6.sin6_port = htons(CLIENT_PORT);
    localAddr6.sin6_family = AF_INET6;

    /* Set Server port and IP address to connect to the TCP server. */
    memset(&echoServAddr6, 0, sizeof(echoServAddr6));
    echoServAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    echoServAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    echoServAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    echoServAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    echoServAddr6.sin6_port = htons(SERVER_PORT);
    echoServAddr6.sin6_family = AF_INET6;

    /* Now make client connections with the server. */
    while (1)
    {
        printf("\n");

        /* Create BSD TCP Socket */

        sock_tcp_client = socket(AF_INET6, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n");
            return;
        }

        printf("Client socket %d created \n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr6,
                sizeof(echoServAddr6));

        /* Check for error. */
        if (status != NX_SOC_OK)
        {
            printf("Error on Client socket %d connect\n");
            soc_close(sock_tcp_client);
            return;

        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr6,
        &length);

        printf("Client port = %lu , Client = 0x%x 0x%x 0x%x 0x%x,",
                ntohs(localAddr6.sin6_port),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[3]));

        length = sizeof(struct sockaddr_in6);

        status = getpeername(sock_tcp_client, (struct sockaddr *)
                            &echoServAddr6, &length);

        printf("Remote port = %lu, Remote IP = 0x%x 0x%x 0x%x 0x%x \n",
                ntohs(echoServAddr6.sin6_port),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[3]));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
                sock_tcp_client);

            status = send(sock_tcp_client, "Hello", sizeof("Hello"), 0);

            if (status == NX_SOC_ERROR)
            {
                printf("Error on Client Socket (%d) send \n",
                        sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message: Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,
                        CLIENT_BUFFER_SIZE, 0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Client received no data on socket %d\n",
                            sock_tcp_client);
                }

            break;
            }
            else
            {
                printf("Client socket %d received %d bytes and this message:
                        %s\n", sock_tcp_client, status,
                        Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = oc_close(sock_tcp_client);

        if (status != NX_SOC_ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```
