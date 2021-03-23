---
title: Bölüm 2-Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) yükleme ve kullanımı
description: Bu bölümde, Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 40f09da31f5541208c3b2cc0eeb54850b3d71f7c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826656"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-point-to-point-protocol-ppp"></a>Bölüm 2-Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) yükleme ve kullanımı

Bu bölümde, Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) paketi adresinde bulunabilir <https://github.com/azure-rtos/netx> . Paket aşağıdaki dosyaları içerir:

- **nx_ppp. h**: NETX için PPP için üst bilgi dosyası
- **nx_ppp. c**: NETX için PPP Için c kaynak dosyası
- **nx_ppp.pdf**: NETX için PPP açıklaması
- **demo_netx_ppp. c**: NETX PPP tanıtımı

## <a name="ppp-installation"></a>PPP yüklemesi

NetX için PPP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX ' in yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_ppp. h* ve *nx_ppp. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-ppp"></a>PPP kullanma

NetX için PPP kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_ppp.* h içermelidir. *Nx_ppp. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen PPP işlev çağrılarını yapabilir. Uygulama, yapı işlemine *nx_ppp. c* de içermelidir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX PPP 'yi kullanmak için gereklidir.

## <a name="using-modems"></a>Modem kullanma

İnternet bağlantısı için bir modem gerekliyse, NetX PPP ürününü kullanabilmeniz için bazı özel noktalar gerekir. Temel olarak, bir modem kullanılması, iletişim kaybı için ek başlatma mantığı ve mantığını tanıtır. Ayrıca, ek modem mantığının çoğu NetX PPP bağlamı dışında gerçekleştirilir. NetX PPP 'yi modem ile kullanmanın temel akışı şuna benzer:

1. Modemi Başlat

1. Internet servis sağlayıcısı (ISS) ara

1. Bağlantıyı bekle

1. Kullanıcı kimliği Istemi bekle

1. NetX PPP 'yi Başlat [işlemde PPP]

1. Iletişim kaybı

1. NetX PPP 'yi durdurun (veya nx_ppp_restart aracılığıyla yeniden başlatın)

### <a name="initialize-modem"></a>Modemi Başlat

Uygulamanın alt düzey seri çıkış yordamını kullanarak, modem bir dizi ASCII karakter komutlarıyla başlatılır (daha fazla ayrıntı için Modemin belgelerine bakın).

### <a name="dial-internet-service-provider"></a>Internet hizmet sağlayıcısını ara

Uygulamanın alt düzey seri çıkış yordamını kullanarak, modemin ISS 'yi çevirebileceği için talimat verilir. Örneğin, aşağıdaki 123-4567 numaralı bir ISS 'yi aramak için kullanılan bir ASCII dizesinin tipik bir örneğidir:

"ATDT123456\r"

### <a name="wait-for-connection"></a>Bağlantıyı bekle

Bu noktada, uygulama bir bağlantının kurulduğu modemden bildirim almayı bekler. Bu, uygulamanın alt düzey seri giriş yordamından karakter arayarak yapılır. Genellikle, modemler bir bağlantı oluşturulduğunda "Bağlan" ASCII dizesini döndürür.

### <a name="wait-for-user-id-prompt"></a>Kullanıcı KIMLIĞI Istemi bekle

Bağlantı kurulduktan sonra, uygulamanın ISS 'den bir ilk oturum açma isteği beklemesi gerekir. Bu genellikle "oturum aç?" gibi bir ASCII dizesi biçimini alır.

### <a name="start-netx-ppp"></a>NetX PPP 'yi Başlat

Bu noktada NetX PPP başlatılabilir. Bu, *nx_ip_create* hizmeti tarafından izlenen *nx_ppp_create* hizmeti çağırarak gerçekleştirilir. PAP 'yi etkinleştirmek ve PPP IP adreslerini ayarlamak için ek hizmetler de gerekebilir. Daha fazla bilgi için lütfen bu kılavuzun aşağıdaki bölümlerini gözden geçirin.

### <a name="loss-of-communication"></a>Iletişim kaybı

PPP başlatıldıktan sonra, PPP olmayan herhangi bir bilgi, *nx_ppp_create* hizmetine belirtilen uygulamayı "geçersiz paket işleme" yordamına geçirilir. Genellikle modemler, ISS ile iletişim kesildiğinde "TAŞıYıCı yok" gibi bir ASCII dizesi gönderir. Uygulama bu tür bilgilerle PPP olmayan bir paket aldığında, NetX PPP örneğini durdurmanız veya *nx_ppp_restart* API 'SI aracılığıyla PPP durum makinesini yeniden başlatmanız gerekir.

### <a name="stop-netx-ppp"></a>NetX PPP 'yi durdur

NetX PPP 'nin durdurulması oldukça basittir. Temel olarak, oluşturulan tüm yuvalar ilişkisiz ve silinmiş olmalıdır. Sonra, *nx_ip_delete* HIZMETI aracılığıyla IP örneğini silin. IP örneği silindikten sonra, PPP 'yi durdurma işlemini tamamlaması için *nx_ppp_delete* hizmeti çağrılmalıdır. Bu noktada, uygulama artık ISS ile iletişimi yeniden kurmayı deneyebilir.

## <a name="small-example-system"></a>Küçük örnek sistem

NetX PPP kullanmanın ne kadar kolay olduğunu gösteren bir örnek, aşağıda görüntülenen Şekil 1,1 ' de açıklanmıştır. Bu örnekte, *nx_ppp. h* PPP içerme dosyası 3. satırda getirilir. Sonra, 56 satırındaki *"tx_application_define*" içinde PPP oluşturulur. "*My_ppp*" PPP denetim bloğu, daha önce satır 9 ' da genel bir değişken olarak tanımlandı. 

>[!NOTE]
>IP örneği oluşturulmadan önce PPP oluşturulmalıdır. PPP ve IP başarıyla oluşturulduktan sonra, "*my_thread*" Iş parçacığı ppp bağlantısının 98. satırda canlı olmasını bekler. 104. satırda, hem PPP hem de NetX tam olarak çalışır.

Bu örnekte görünmeyen bir öğe, uygulamanın seri bayt Alım ıSR ' dir. "*My_ppp*" ile *nx_ppp_byte_receive* ve giriş parametresi olarak alınan bayt çağrısı yapması gerekecektir.

```c
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nx_ppp.h"

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
## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX için PPP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:

- **NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel PPP hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.
- **NX_PPP_PPPOE_ENABLE**: TANıMLANMıŞSA, PPP Ethernet üzerinden paket aktarabilir
- **NX_PPP_BASE_TIMEOUT**: Bu, PPP iş parçacığı GÖREVININ, PPP olaylarını denetlemek için uyandırması gereken dönem oranını (süreölçer işaretleri cinsinden) tanımlar. Varsayılan değer 1 * NX_IP_PERIODIC_RATE (100 Ticks).
- **NX_PPP_DISABLE_INFO**: tanımlanmışsa, iç PPP bilgi toplama devre dışıdır.
- **NX_PPP_DEBUG_LOG_ENABLE**: tanımlanmışsa, iç PPP hata ayıklama günlüğü etkinleştirilir.
- **NX_PPP_DEBUG_LOG_PRINT_ENABLE**: tanımlanmışsa, *STDıO* iç PPP hata *ayıklama günlüğü etkinleştirilir* . Bu yalnızca hata ayıklama günlüğü de etkinse geçerlidir.
- **NX_PPP_DEBUG_LOG_SIZE**: hata ayıklama günlüğü boyutu (hata ayıklama günlüğündeki giriş sayısı). Son girdiye ulaşıldığında, hata ayıklama yakalaması ilk girişe kaydırılır ve daha önce yakalanan tüm verilerin üzerine yazar. Varsayılan değer 50 ' dir.
- **NX_PPP_DEBUG_FRAME_SIZE**: alınan bir paket yükünden yakalanan ve hata ayıklama çıkışına kaydedilen maksimum veri miktarı. Varsayılan değer 50 ' dir.
- **NX_PPP_DISABLE_CHAP**: TANıMLANMıŞSA, MD5 Özet mantığı dahil olmak üzere Iç PPP CHAP mantığı kaldırılır.
- **NX_PPP_DISABLE_PAP**: tanımlanmışsa, Iç PPP PAP mantığı kaldırılır.
- **NX_PPP_DNS_OPTION_DISABLE**: TANıMLANMıŞSA, DNS seçeneği IPCP yanıtında devre dışıdır.  Varsayılan olarak bu seçenek tanımlı değildir (DNS seçeneği ayarlanır).
- **NX_PPP_DNS_ADDRESS_MAX_RETRIES**: Bu, PPP ana bilgisayarının her bir DNS sunucusu adresini IPCP durumundaki eşten ne kadar zaman isteyeceğini belirtir. NX_PPP_DNS_OPTION_DISABLE tanımlanmışsa bu bir etkiye sahip değildir. Varsayılan değer 2 ' dir.
- **NX_PPP_HASHED_VALUE_SIZE**: CHAP kimlik doğrulamasında kullanılan "karma değer" dizelerinin boyutunu belirtir. Varsayılan değer 16 bayt olarak ayarlanır, ancak *nx_ppp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.
- **NX_PPP_MAX_LCP_PROTOCOL_RETRIES**: Bu, PPP zaman aşımına uğrarsa DIĞER bir LCP yapılandırma isteği iletisini gönderdikten en fazla yeniden deneme sayısını tanımlar. Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır. Varsayılan değer 20 ' dir.
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
