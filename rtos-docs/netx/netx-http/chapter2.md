---
title: Bölüm 2-NetX HTTP yüklemesi ve kullanımı
description: Bu bölümde, NetX HTTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: db621e38e9d2324ca3ce2398aee9f729b05886ee
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826716"
---
# <a name="chapter-2---installation-and-use-of-netx-http"></a>Bölüm 2-NetX HTTP yüklemesi ve kullanımı

Bu bölümde, NetX HTTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .

- **nx_http_client. h** NetX için HTTP Istemcisi üst bilgi dosyası
- **nx_http_server. h** NetX için HTTP sunucusu üst bilgi dosyası
- **nx_http_client. c** NetX için HTTP Istemcisi için C kaynak dosyası
- **nx_http_server. c** NetX için HTTP sunucusu için C kaynak dosyası
- **nx_md5. c** MD5 Özet algoritmaları
- **filex_stub. h** FileX yoksa saplama dosyası
- **nx_http.pdf** NetX için HTTP açıklaması
- **demo_netx_http. c** NetX HTTP tanıtımı

## <a name="http-installation"></a>HTTP yüklemesi

NetX için HTTP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır. Örneğin, NetX, "*\threadx\arm7\green*" dizinine yüklenirse, NETX http istemci uygulamaları için *nx_http_client. h* ve *Nx_http_client. c* ve netx http sunucu uygulamaları için *nx_http_server. h* ve *nx_http_server. c* . *nx_md5. c* bu dizine kopyalanmalıdır. Tanıtım ' RAM sürücüsü ' uygulaması NetX HTTP Istemcisi ve sunucu dosyaları aynı dizine kopyalanmalıdır.

## <a name="using-http"></a>HTTP kullanma

NetX için HTTP kullanmak kolaydır. Temel olarak, uygulama kodu, sırasıyla ThreadX, FileX ve NetX kullanmak için *tx_api. h, fx_api. h* ve *nx_api. h* dahil *nx_http_client. h* ve/veya *nx_http_server. h* içermelidir. HTTP üstbilgi dosyaları eklendikten sonra, uygulama kodu daha sonra bu kılavuzda belirtilen HTTP işlev çağrılarını yapabilir. Uygulama, yapı işlemine *nx_http_client. c*, *nx_http_server. c* ve *MD5. c* ' yi de içermelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX HTTP 'yi kullanmak için gereklidir.

>[!NOTE] 
> Yapı işleminde NX_HTTP_DIGEST_ENABLE belirtilmemişse, *MD5. c* dosyasının uygulamaya eklenmesi gerekmez. Benzer şekilde, HTTP Istemci özellikleri gerekmiyorsa *nx_http_client. c* dosyası atlanabilir.

>[!NOTE] 
> HTTP, NetX TCP hizmetlerinden yararlandığından, HTTP kullanılmadan önce *nx_tcp_enable* çağrısıyla TCP 'nin etkinleştirilmesi gerekir.

## <a name="small-example-system"></a>Küçük örnek sistem

Aşağıda görüntülenen Şekil 1,1 ' de NetX HTTP kullanmanın ne kadar kolay olduğunu gösteren bir örnek. Bu örnekte, *nx_http_client. h ve nx_http_server. h* http içerme dosyası 8. satırda getirilir. Ardından, HTTP sunucusu 131 satırındaki "*tx_application_define*" içinde oluşturulur.

>[!NOTE] 
> HTTP sunucu denetim bloğu "*sunucu*" daha önce 25. satırda genel değişken olarak tanımlandı.

Başarılı bir şekilde oluşturulduktan sonra, 136. satırda bir HTTP sunucusu başlatılır. Satır 149 ' de HTTP Istemcisi oluşturulur. Son olarak, Istemci dosyayı 157. satıra yazar ve dosyayı 195. satırda geri okur.

```c
/* This is a small demo of HTTP on the high-performance NetX TCP/IP stack.
This demo relies on ThreadX, NetX, and FileX to show a simple HTML
transfer from the client and then back from the server. */

#include "tx_api.h"
#include "fx_api.h"
#include "nx_api.h"
#include "nx_http_client.h"
#include "nx_http_server.h"
#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_0;
TX_THREAD         thread_1;
NX_PACKET_POOL    pool_0;
NX_PACKET_POOL    pool_1;
NX_IP             ip_0;
NX_IP             ip_1;
FX_MEDIA          ram_disk;

/* Define HTTP objects. */

NX_HTTP_SERVER    my_server;
NX_HTTP_CLIENT    my_client;

/* Define the counters used in the demo application... */

ULONG             error_counter;

/* Define the RAM disk memory. */

UCHAR             ram_disk_memory[32000];

/* Define function prototypes. */

void     thread_0_entry(ULONG thread_input);
VOID     _fx_ram_driver(FX_MEDIA *media_ptr) ;
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
UINT     authentication_check(NX_HTTP_SERVER *server_ptr, UINT request_type,
                              CHAR *resource, CHAR **name, CHAR **password, 
                              CHAR **realm);

/* Define the application's authentication check. This is called by
the HTTP server whenever a new request is received. */
UINT authentication_check(NX_HTTP_SERVER *server_ptr, UINT request_type,
                         CHAR *resource, CHAR **name, CHAR **password, 
                         CHAR **realm);
{

    /* Just use a simple name, password, and realm for all
    requests and resources. */
    *name = "name";
    *password = "password";
    *realm = "NetX HTTP demo";

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
                    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create packet pool. */
    nx_packet_pool_create(&pool_0, "NetX Packet Pool 0",
                         600, pointer, 8192);
                         pointer = pointer + 8192;

    /* Create an IP instance. */
    nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(1, 2, 3, 4),
                0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                pointer, 4096, 1);
                pointer = pointer + 4096;

    /* Create another packet pool. */
    nx_packet_pool_create(&pool_1, "NetX Packet Pool 1", 600, pointer, 8192);
                         pointer = pointer + 8192;

    /* Create another IP instance. */
    nx_ip_create(&ip_1, "NetX IP Instance 1", IP_ADDRESS(1, 2, 3, 5),
                0xFFFFFF00UL, &pool_1, _nx_ram_network_driver,
                pointer, 4096, 1);
                pointer = pointer + 4096;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    nx_arp_enable(&ip_0, (void *) pointer, 1024);
                 pointer = pointer + 1024;

    /* Enable ARP and supply ARP cache memory for IP Instance 1. */
    nx_arp_enable(&ip_1, (void *) pointer, 1024);
                 pointer = pointer + 1024;

    /* Enable TCP processing for both IP instances. */
    nx_tcp_enable(&ip_0);
    nx_tcp_enable(&ip_1);

    /* Open the RAM disk. */
                 _fx_ram_driver, ram_disk_memory, pointer, 4096) ;
                 pointer += 4096;

    /* Create the NetX HTTP Server. */
    nx_http_server_create(&my_server, "My HTTP Server", &ip_1, &ram_disk,
                         pointer, 4096, &pool_1, authentication_check, NX_NULL);
                         pointer = pointer + 4096;

    /* Start the HTTP Server. */
    nx_http_server_start(&my_server);
}

/* Define the test thread. */
void     thread_0_entry(ULONG thread_input)
{

NX_PACKET     *my_packet;
UINT          status;

    /* Create an HTTP client instance. */
    status = nx_http_client_create(&my_client, "My Client", &ip_0,
                                  &pool_0, 600);

    /* Check status. */
    if (status)
        error_counter++;

    /* Prepare to send the simple 103-byte HTML file to the Server. */
    status = nx_http_client_put_start(&my_client, IP_ADDRESS(1,2,3,5),
                                      "/test.htm", "name", "password", 103, 50);
    /* Check status. */
    if (status)
        error_counter++;

    /* Allocate a packet. */
    status = nx_packet_allocate(&pool_0, &my_packet, NX_TCP_PACKET,
                               NX_WAIT_FOREVER);
    /* Check status. */
    if (status != NX_SUCCESS)
        return;

    /* Build a simple 103-byte HTML page. */
    nx_packet_data_append(my_packet, "<HTML>\r\n", 8,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet,
                         "<HEAD><TITLE>NetX HTTP Test</TITLE></HEAD>\r\n", 44,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<BODY>\r\n", 8,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<H1>NetX Test Page</H1>\r\n", 25,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</BODY>\r\n", 9,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</HTML>\r\n", 9,
                         &pool_0, NX_WAIT_FOREVER);

    /* Complete the PUT by writing the total length. */
    status = **nx_http_client_put_packet**(&my_client, my_packet, 50);

    /* Check status. */
    if (status)
        error_counter++;

    /* Now GET the file back! */
    status = nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5),
                                     "/test.htm", NX_NULL, 0, "name", 
                                     "password", 50);

    /* Check status. */
    if (status)
        error_counter++;

    /* Get a packet. */
    status = nx_http_client_get_packet(&my_client, &my_packet, 20);

    /* Check for an error. */
    if ((status) || (my_packet -> nx_packet_length != 103))
        error_counter++;

    /* Check to see if we have a packet. */
    if (status == NX_SUCCESS)
    {

        /* Yes, release it! */
        nx_packet_release(my_packet);
    }

    /* Flush the media. */
     fx_media_flush(&ram_disk);
 }
```

Şekil 1,1 NetX ile HTTP kullanımı örneği

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX için HTTP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir. Varsayılan değerler listelenir, ancak *nx_http_client. h ve nx_http_server. h*'ye dahil etmeden önce yeniden tanımlanabilir:

- **NX_DISABLE_ERROR_CHECKING** Tanımlı, bu seçenek temel HTTP hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.
- **NX_HTTP_SERVER_PRIORITY** HTTP sunucusu iş parçacığının önceliği. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.
- **NX_HTTP_NO_FILEX** Tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar. Bu seçenek tanımlandıysa, HTTP Istemcisi herhangi bir değişiklik yapılmadan çalışır. HTTP sunucusunun değiştirilmesi veya kullanıcının düzgün çalışması için bir çok sayıda FileX hizmeti oluşturması gerekir.
- **NX_HTTP_TYPE_OF_SERVICE** HTTP TCP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.
- **NX_HTTP_SERVER_THREAD_TIME_SLICE** Aynı önceliğe sahip iş parçacıklarını oluşturmadan önce, sunucu iş parçacığının çalışmasına izin verilen süreölçer onay işareti sayısı. Varsayılan değer 2 ' dir.
- **NX_HTTP_FRAGMENT_OPTION** HTTP TCP istekleri için parça etkinleştirme. Varsayılan olarak, bu değer HTTP TCP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT.
- **NX_HTTP_SERVER_WINDOW_SIZE** Sunucu yuvası pencere boyutu. Varsayılan olarak, bu değer 2048 bayttır.
- **NX_HTTP_TIME_TO_LIVE** Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır.
- **NX_HTTP_SERVER_TIMEOUT** İç hizmetlerin askıya alınacağı ThreadX ticks sayısını belirtir. Varsayılan değer 10 saniyeye ayarlanır (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_SERVER_TIMEOUT_ACCEPT** İç *nx_tcp_server_socket_accept* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer (10 * NX_IP_PERIODIC_RATE) olarak ayarlanır.
- **NX_HTTP_SERVER_TIMEOUT_DISCONNECT** İç *nx_tcp_socket_disconnect* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 10 saniyeye ayarlanır (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_SERVER_TIMEOUT_RECEIVE** İç *nx_tcp_socket_receive* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 10 saniyeye ayarlanır (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_SERVER_TIMEOUT_SEND** İç *nx_tcp_socket_send* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 10 saniyeye ayarlanır (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_MAX_HEADER_FIELD** HTTP üst bilgisi alanının en büyük boyutunu belirtir. Varsayılan değer 256 ' dir.
- **NX_HTTP_MULTIPART_ENABLE** Tanımlandıysa, HTTP sunucusunun çok parçalı HTTP isteklerini desteklemesini sağlar.
- **NX_HTTP_SERVER_MAX_PENDING** HTTP sunucusu için sıraya alınabilen bağlantı sayısını belirtir. Varsayılan değer 5 ' e ayarlanır.
- **NX_HTTP_MAX_RESOURCE** İstemci tarafından sağlanan *kaynak adında* izin verilen bayt sayısını belirtir. Varsayılan değer 40 olarak ayarlanır.
- **NX_HTTP_MAX_NAME** İstemci tarafından sağlanan *Kullanıcı adında* izin verilen bayt sayısını belirtir. Varsayılan değer 20 olarak ayarlanır.
- **NX_HTTP_MAX_PASSWORD** İstemci tarafından sağlanan *parolada* izin verilen bayt sayısını belirtir. Varsayılan değer 20 olarak ayarlanır.
- **NX_HTTP_SERVER_MIN_PACKET_SIZE** Sunucu oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir. En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir. Varsayılan değer 600 olarak ayarlanır.
- **NX_HTTP_CLIENT_MIN_PACKET_SIZE** Istemci oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir. En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir. Varsayılan değer 300 olarak ayarlanır.
- **NX_HTTP_SERVER_RETRY_SECONDS** *sunucu yuvası yeniden aktarım zaman aşımını saniye cinsinden ayarlayın. Varsayılan değer* 2 olarak ayarlanır.
- **NX_HTTP_SERVER_RETRY_MAX** Bu, sunucu yuvasıyla maksimum yeniden iletim sayısını ayarlar. Varsayılan değer 10 olarak ayarlanır.
- **NX_HTTP_SERVER_RETRY_SHIFT** Bu değer, sonraki yeniden iletim zaman aşımını ayarlamak için kullanılır. Geçerli zaman aşımı, bu nedenle, yuva zaman aşımı kaydırma değerine göre kaydırılan, o kadar yeniden iletim sayısı ile çarpılır. Zaman aşımını katlama için varsayılan değer 1 ' e ayarlanır.
- **NX_HTTP_ SERVER_TRANSMIT_QUEUE_DEPTH** Bu, sunucu yuvası yeniden iletim kuyruğunda sıraya alınabilen en fazla paket sayısını belirtir. Sıraya alınan paketlerin sayısı bu sayıya ulaşırsa, bir veya daha fazla sıraya alınmış paket yayınlanana kadar başka paket gönderilemez. Varsayılan değer 20 olarak ayarlanır.