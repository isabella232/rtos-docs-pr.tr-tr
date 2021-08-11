---
title: Bölüm 2 - NetX Duo Azure RTOS yükleme ve Noktadan Noktaya Protokolü (PPP)
description: Bu bölümde NetX Duo Noktadan Noktaya Protokolü (PPP) bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 141197daa87b40ebe2ea34ff096a0b01b260e9296a33e3b678f11400d5d46ab6
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797169"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-point-to-point-protocol-ppp"></a>Bölüm 2 - NetX Duo Azure RTOS yükleme ve Noktadan Noktaya Protokolü (PPP)

Bu bölümde NetX Duo Noktadan Noktaya Protokolü (PPP) bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.

## <a name="product-distribution"></a>Ürün Dağıtımı

Azure RTOS NetX Duo Noktadan Noktaya Protokolü (PPP) paketine şu bağlantıdan <https://github.com/azure-rtos/netxduo> bakabilirsiniz: . Paket aşağıdaki dosyaları içerir:

- **nx_ppp.h:** NetX için PPP üst bilgi dosyası
- **nx_ppp.c:** NetX için PPP için C Kaynak dosyası
- **nx_ppp.pdf:** NetX için PPP'nin PDF açıklaması
- **demo_netx_ppp.c**: NetX PPP gösterimi

## <a name="ppp-installation"></a>PPP Yüklemesi

NetX için PPP kullanmak üzere, daha önce bahsedilen dağıtımın tamamı NetX'in yüklü olduğu dizine kopyalanır. Örneğin,*"\threadx\arm7\green"* dizininde NetX yüklüyse, *nx_ppp.h* ve *nx_ppp.c* dosyalarının bu dizine kopyalanmış olması gerekir.

## <a name="using-ppp"></a>PPP kullanma

NetX için PPP kullanmak kolaydır. Temel olarak, ThreadX ve NetX'i sırasıyla kullanmak için uygulama kodu *tx_api.h* ve nx_api.h 'yi içeren *nx_ppp.h'yi* içermeli.  *nx_ppp.h* ekli olduktan sonra, uygulama kodu bu kılavuzun devamlarında belirtilen PPP işlev çağrılarını da mümkün hale gelecektir. Uygulamanın derleme sürecine *nx_ppp.c'yi* de içermesi gerekir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmiş olmalı ve nesne formu uygulamanın dosyalarıyla birlikte bağlanacak. NetX PPP'yi kullanmak için gerekenler bunlardır.

## <a name="using-modems"></a>Modemleri Kullanma

İnternet bağlantısı için modem gerekli ise NetX PPP ürününü kullanmak için dikkat edilmesi gereken bazı özel noktalar vardır. Temel olarak, modem kullanmak iletişim kaybı için ek başlatma mantığı ve mantık sağlar. Ayrıca, ek modem mantığının çoğu NetX PPP bağlamı dışında yapılır. NetX PPP'yi modem ile kullanmanın temel akışı şöyledir:

1. Modem Başlatma

1. İnternet Hizmet Sağlayıcısı'nın (ISS) arama

1. Bağlantı'nın beklemesi

1. UserID İstemi'nin beklemesi

1. NetX PPP'yi başlatma [PPP işlemde]

1. İletişim Kaybı

1. NetX PPP'yi durdurma (veya nx_ppp_restart)

### <a name="initialize-modem"></a>Modem Başlatma

Uygulamanın alt düzey seri çıkış yordamı kullanılarak, modem bir dizi ASCII karakter komutuyla başlatılır (daha fazla ayrıntı için modemin belgelerine bakın).

### <a name="dial-internet-service-provider"></a>İnternet Hizmet Sağlayıcısını Çevirme

Uygulamanın alt düzey seri çıkış yordamını kullanarak modemin ISS'yi çevirmesi ist. Örneğin, bir ISS'yi 123-4567 numarasına kadar çevirmede kullanılan bir ASCII dizesi tipiktir:

"ATDT123456\r"

### <a name="wait-for-connection"></a>Bağlantı'nın beklemesi

Bu noktada, uygulama modemden bir bağlantının kurul olduğuna dair göstergeyi almak için bekler. Bu, uygulamanın alt düzey seri giriş yordamından karakterlere bakarak başarılı olur. Modemler genellikle bir bağlantı kurularak bir ASCII "CONNECT" dizesi döndürür.

### <a name="wait-for-user-id-prompt"></a>Kullanıcı Kimliği İstemi'nin beklemesi

Bağlantı kurulduktan sonra uygulamanın iss'den ilk oturum açma isteğini beklemesi gerekir. Bu genellikle "Login?" gibi bir ASCII dizesi biçimi alır.

### <a name="start-netx-ppp"></a>NetX PPP'yi başlatma

Bu noktada NetX PPP başlat olabilir. Bu, nx_ppp_create hizmeti *çağrılarak* ve ardından nx_ip_create  başarılı olur. PAP'yi etkinleştirmek ve PPP IP adreslerinin kurulumunu yapmak için ek hizmetler de gerekebilir. Daha fazla bilgi için lütfen bu kılavuzun aşağıdaki bölümlerini gözden geçirebilirsiniz.

### <a name="loss-of-communication"></a>İletişim Kaybı

PPP başlatıldıktan sonra PPP olmayan tüm bilgiler, uygulamanın nx_ppp_create hizmetine belirtilen "geçersiz paket *işleme" yordamına* geçiriliyor. Modemler genellikle ISS ile iletişimin kaybedilip "TAŞıYıCı YOK" gibi bir ASCII dizesi gönderir. Uygulama bu tür bilgilerle PPP olmayan bir paket aldığında, NetX PPP örneğini durdurmaya veya ppp durum makinesini nx_ppp_restart *API'si aracılığıyla yeniden başlatması* gerekir.

### <a name="stop-netx-ppp"></a>NetX PPP'yi durdurma

NetX PPP'yi durdurmak oldukça kolaydır. Temel olarak, oluşturulan tüm yuvaların sınırsız olması ve silinmesi gerekir. Ardından, ip örneğini nx_ip_delete *silin.* IP örneği silindikten sonra, *PPP nx_ppp_delete* durdurma işlemini tamamlamak için nx_ppp_delete hizmeti çağrılması gerekir. Bu noktada, uygulama artık ISS ile iletişimi yeniden kurma girişiminde olabilir.

## <a name="small-example-system"></a>Küçük Örnek Sistem

Aşağıda gösterilen Şekil 1.1'de NetX PPP kullanmanın ne kadar kolay olduğunu gösteren bir örnek açıklanmıştır. Bu örnekte PPP include *nx_ppp.h* dosyası 3. satıra getiri. Ardından PPP, 56.*satırda "tx_application_define"* içinde oluşturulur. PPP denetim bloğu "*my_ppp*" daha önce 9. satırda genel değişken olarak tanımlanmıştır. 

>[!NOTE]
>PPP, IP örneği oluşturulmadan önce oluşturulacak. PPP ve IP'nin başarıyla oluşturulmasının ardından , "*my_thread*" iş parçacığı PPP bağlantısının 98. satırda canlanır. 104. satırda hem PPP hem de NetX tamamen çalışır durumdadır.

Bu örnekte göster almayan bir öğe, uygulamanın seri bayt alma ISR'dir. "my_ppp " *ile nx_ppp_byte_receive* çağrısı *my_ppp* giriş parametreleri olarak alınan bayta çağrılacak.

```c
0001 #include   "tx_api.h"
0002 #include   "nx_api.h"
0003 #include   "nx_ppp.h"
0004
#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_PPP                  my_ppp;

/* Define function prototypes. */

void    my_thread_entry(ULONG thread_input);
void    my_serial_driver_byte_output(UCHAR byte);
void    my_invalid_packet_handler(NX_PACKET *packet_ptr);
 
/* Define main entry point. */
intmain()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
 }


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;

/* Setup the working pointer. */
pointer =  (CHAR *) first_unused_memory;

/* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                  pointer, DEMO_STACK_SIZE, 
                  2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                    1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error. */
    if (status)
        error_counter++;

    /* Create a PPP instance. */
    status = nx_ppp_create(&my_ppp, “My PPP”, &my_ip, pointer, 1024, 2, 
                           &my_pool, my_invalid_packet_handler, my_serial_driver_byte_output);
    pointer =  pointer + 1024;
    /* Check for PPP creation pool. */
    if (status)
        error_counter++;

    /* Create an IP instance with the PPP driver. */
    status = nx_ip_create(&my_ip,"My NetX IP Instance", 
                           IP_ADDRESS(216,2,3,1), 0xFFFFFF00, &my_pool, 
                           nx_ppp_driver, pointer, DEMO_STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors. */
    if (status)
        error_counter++;

    /* Enable ICMP for my IP Instance. */
    status =  nx_icmp_enable(&my_ip);

    /* Check for ICMP enable errors. */
    if (status)
        error_counter++;

    /* Enable UDP. */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
}

/* Define my thread. */
void    my_thread_entry(ULONG thread_input)
{

UINT        status;
ULONG       ip_status;
NX_PACKET   *my_packet;

/* Wait for the PPP link in my_ip to become enabled. */
    status =  nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,&ip_status,3000);

    /* Check for IP status error. */
    if (status) 
        return;

    /* Link is fully up and operational. All NetX activities 
    are now available. */

}
```
## <a name="configuration-options"></a>Yapılandırma Seçenekleri

NetX için PPP'yi inşa için çeşitli yapılandırma seçenekleri vardır. Aşağıdaki listede her biri ayrıntılı olarak açıklanmaktadır:

- **NX_DISABLE_ERROR_CHECKING:** Tanımlandı, bu seçenek temel PPP hata denetimlerini kaldırır. Genellikle uygulama hata ayıklandıktan sonra kullanılır.
- **NX_PPP_PPPOE_ENABLE:** Tanımlandı ise PPP paketi Ethernet üzerinden iletilmesini sağlar
- **NX_PPP_BASE_TIMEOUT:** PPP iş parçacığı görevinin PPP olaylarını kontrol etmek için uyandır olduğu dönem oranını (zamanlayıcı değer tıklarında) tanımlar. Varsayılan değer 1*NX_IP_PERIODIC_RATE (100 tık) değeridir.
- **NX_PPP_DISABLE_INFO:** Tanımlanmışsa, iç PPP bilgi toplama devre dışı bırakılır.
- **NX_PPP_DEBUG_LOG_ENABLE:** Tanımlandı ise iç PPP hata ayıklama günlüğü etkinleştirilir.
- **NX_PPP_DEBUG_LOG_PRINT_ENABLE:** Tanımlandı ise *stdio'ya* iç PPP hata ayıklama günlüğü *printf* etkinleştirilir. Bu yalnızca hata ayıklama günlüğü de etkinleştirildiğinde geçerlidir.
- **NX_PPP_DEBUG_LOG_SIZE:** Hata ayıklama günlüğünün boyutu (hata ayıklama günlüğünde girdi sayısı). Son girişe ulaşılan hata ayıklama yakalaması ilk girdiye sarmalanır ve daha önce yakalanan verilerin üzerine yazarak. Varsayılan değer 50'dir.
- **NX_PPP_DEBUG_FRAME_SIZE:** Alınan paket yükünden yakalanan ve çıkışta hata ayıklamak için kaydedilen maksimum veri miktarı. Varsayılan değer 50'dir.
- **NX_PPP_DISABLE_CHAP:** Tanımlanırsa, MD5 özet mantığı da dahil olmak üzere iç PPP CHAP mantığı kaldırılır.
- **NX_PPP_DISABLE_PAP:** Tanımlanırsa iç PPP PAP mantığı kaldırılır.
- **NX_PPP_DNS_OPTION_DISABLE:** Tanımlanmışsa, IPCP yanıtta birincil DNS Sunucusu Seçeneği devre dışı bırakılır. Varsayılan olarak bu seçenek tanımlanmamıştır.
- **NX_PPP_DNS_ADDRESS_MAX_RETRIES:** PPP ana bilgisayarının IPCP durumdaki eşten kaç kez DNS Sunucusu adresi isteği gönderileceğini belirtir. Bu, tanımlandığı NX_PPP_DNS_OPTION_DISABLE etkisi yoktur. Varsayılan değer 2'dir.
- **NX_PPP_HASHED_VALUE_SIZE:** CHAP kimlik doğrulamasında kullanılan "karma değer" dizelerinin boyutunu belirtir. Varsayılan değer 16 bayt olarak ayarlanır, ancak nx_ppp.h eklenmeden *önce yeniden tanımlandır.*
- **NX_PPP_MAX_LCP_PROTOCOL_RETRIES:** Başka bir LCP yapılandırma isteği iletisi göndermeden önce PPP'nin zaman atladığı maksimum yeniden deneme sayısını tanımlar. Bu numaraya ulaşıldıkça PPP el sıkışması durdurulacak ve bağlantı durumu durdurulacak. Varsayılan değer 20'dir.
- **NX_PPP_MAX_PAP_PROTOCOL_RETRIES**: Bu, başka bir PAP kimlik doğrulama isteği iletisi göndermeden önce PPP zaman aşımına uğrarsa en fazla yeniden deneme sayısını tanımlar. Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır. Varsayılan değer 20 ' dir.
- **NX_PPP_MAX_CHAP_PROTOCOL_RETRIES**: Bu, başka bir CHAP sınama iletisi göndermeden önce PPP zaman aşımına uğrarsa en fazla yeniden deneme sayısını tanımlar. Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır. Varsayılan değer 20 ' dir.
- **NX_PPP_MAX_IPCP_PROTOCOL_RETRIES**: Bu, PPP zaman aşımına uğrarsa başka bir IPCP yapılandırma isteği iletisini gönderdikten en fazla yeniden deneme sayısını tanımlar. Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır. Varsayılan değer 20 ' dir.
- **NX_PPP_MRU**: PPP Için en fazla alma BIRIMI (MRU) sayısını belirtir. Varsayılan olarak, bu değer 1.500 bayttır (minimum değer). Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.
- **NX_PPP_MINIMUM_MRU**: bir LCP yapılandırma isteği iletisinde alınan en küçük MRU değeri belirtir. Varsayılan olarak, bu değer 1.500 bayttır (minimum değer). Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.
- **NX_PPP_NAME_SIZE**: kimlik doğrulamasında kullanılan "ad" dizelerinin boyutunu belirtir. Varsayılan değer 32bytes olarak ayarlanır, ancak * nx_ppp. h 'ye dahil etmeden önce yeniden tanımlanabilir.
- **NX_PPP_PASSWORD_SIZE**: kimlik doğrulamasında kullanılan "parola" dizelerinin boyutunu belirtir. Varsayılan değer 32bytes olarak ayarlanır, ancak *nx_ppp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.
- **NX_PPP_PROTOCOL_TIMEOUT**: Bu, PPP GÖREVININ bir PPP protokol isteği iletisine yanıt alması için bekleme seçeneğini (saniye cinsinden) tanımlar. Varsayılan değer 4 saniyedir.
- **NX_PPP_RECEIVE_TIMEOUTS**: Bu, PPP iş parçacığı GÖREVININ bir PPP ileti akışında bir sonraki karakteri almak için bekleyen kaç kez zaman aşımı olduğunu tanımlar. Bundan sonra PPP paketi yayınlar ve sonraki PPP iletisini almayı beklemeye başlar. Varsayılan değer 4'tür.
- **NX_PPP_SERIAL_BUFFER_SIZE**: alma karakteri seri arabelleğinin boyutunu belirtir. Varsayılan olarak, bu değer 3.000 bayttır. Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.
- **NX_PPP_TIMEOUT**: Bu, verileri iletmek için paket AYıRMAYA ve IP katmanına gönderilmek üzere paketlere PPP seri verileri arabelleğe almak için bekleme seçeneğini (süreölçer işaretleri) tanımlar. Varsayılan değer 4 * NX_IP_PERIODIC_RATE (400 Ticks).
- **NX_PPP_THREAD_TIME_SLICE**: PPP iş parçacıkları için zaman dilimi seçeneği. Varsayılan olarak, bu değer TX_NO_TIME_SLICE. Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.
- **NX_PPP_VALUE_SIZE**: CHAP kimlik doğrulamasında kullanılan "değer" dizelerinin boyutunu belirtir. Varsayılan değer 32bytes olarak ayarlanır, ancak nx_ppp. h 'ye dahil etmeden önce yeniden tanımlanabilir.