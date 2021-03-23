---
title: Bölüm 2-HTTP ve HTTPS yükleme ve kullanımı
description: Bu bölümde, NetX Web HTTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/24/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 99e649781588b56e72b509c2aa077c38423379d1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825703"
---
# <a name="chapter-2---installation-and-use-of-http-and-https"></a>Bölüm 2-HTTP ve HTTPS yükleme ve kullanımı

Bu bölümde, NetX Web HTTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX için HTTP, adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Bu paket, aşağıdaki gibi üç kaynak dosyası, iki içerme dosyası ve bu belgeyi içeren bir dosya içerir:

- **nx_web_http_common. h** NetX Web HTTP için ortak üst bilgi dosyası
- **nx_web_http_client. h** NetX Web için HTTP Istemcisi üst bilgi dosyası
- **nx_web_http_server. h** NetX Web için HTTP sunucusu üst bilgi dosyası
- **nx_web_http_client. c** NetX Web için HTTP Istemcisi için C kaynak dosyası
- **nx_web_http_server. c** NetX Web için HTTP sunucusu için C kaynak dosyası
- **nx_tcpserver. c** Birden çok TCP yuvası için C kaynak dosyası
- **nx_tcpserver. h** HTTPS sunucu sembolleri tanımlamak için üst bilgi dosyası
- **nx_md5. c** MD5 Özet algoritmaları
- **filex_stub. h** FileX yoksa saplama dosyası
- **nx_web_http.pdf** NetX Web için HTTP açıklaması
- **demo_netx_web_http. c** NetX Web HTTP tanıtımı

## <a name="http-installation"></a>HTTP yüklemesi

NetX Web HTTP 'yi kullanmak için, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır. Örneğin, NetX Duo "*\threadx\arm7\green*" dizinine yüklenmişse, *NETX Web http istemci uygulamaları için* *nx_web_http_client. h* ve Nx_web_http_client. c ve *netx Web http sunucusu uygulamaları için nx_web_http_server. h, nx_web_http_server. c, nx_tcpserver. c ve nx_tcpserver. h. Hem istemci hem de sunucu uygulamaları için nx_web_http_common. h de bu dizinde olmalıdır.* Özet kimlik doğrulaması kullanılıyorsa, nx_md5. c de bu dizine kopyalanmalıdır. Tanıtım ' RAM sürücüsü ' uygulaması için HTTP Istemcisi ve sunucu dosyaları aynı dizine kopyalanmalıdır.

TLS kullanılıyorsa, TLS kaynak dosyalarını içeren ayrı bir NetX güvenli dizininiz olmalıdır.

## <a name="using-http"></a>HTTP kullanma

NetX Web HTTP kullanmak kolaydır. Temel olarak, uygulama kodu *nx_web_http_client.* h ve/veya *nx_web_http_server.* h içermelidir *tx_api. h, fx_api. h* ve *nx_api. h* (*nx_web_http_common. h* otomatik olarak eklenir). Bu üst bilgiler, uygulamanın sırasıyla ThreadX, FileX ve NetX Duo kullanmasını sağlar. HTTPS desteği için, *nx_secure_tls. h* dosyası, TLS desteğini getirmek üzere eklendikten sonra üst bilgiler eklenmelidir.

HTTP üstbilgi dosyaları eklendikten sonra, uygulama kodu daha sonra bu kılavuzda belirtilen HTTP işlev çağrılarını yapabilir. Uygulama Ayrıca, http (s *) istemcileri için nx_web_http_client. c* *NX_TCPSERVER ve (http (s) sunucuları için, nx_web_http_server.* c ' ye ve derleme sürecinde *nx_md5. c (Özet kimlik doğrulaması için)* ile bağlantı etmelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX Web HTTP 'yi kullanmak için gereklidir.

> [!NOTE]
> Yapı işleminde NX_WEB_HTTP_DIGEST_ENABLE belirtilmemişse, *MD5. c* dosyasının uygulamaya eklenmesi gerekmez. Benzer şekilde, HTTP Istemci özellikleri gerekmiyorsa, *nx_web_http_client. c* dosyası atlanabilir ve hiçbir http sunucusu özelliği gerekmiyorsa, *nx_web_http_server. c* atlanabilir.
>
> HTTPS 'yi etkinleştirmek için NX_WEB_HTTPS_ENABLE tanımlanmamışsa (yalnızca düz metin HTTP kullanmak yerine), NetX güvenli TLS 'nin derlemede olması gerekmez.
>
> HTTP, NetX TCP hizmetlerini kullandığından, HTTP kullanmadan önce *nx_tcp_enable ()* çağrısıyla TCP 'nin etkinleştirilmesi gerekir.
>
> HTTPS 'yi NetX güvenli TLS ile kullanırken, HTTPS yordamları çağrılmadan önce TLS *nx_secure_tls_initialize ()* ile başlatılmalıdır.

## <a name="small-example-system"></a>Küçük örnek sistem

NetX Web HTTP 'nin nasıl kullanılacağına ilişkin bir örnek aşağıda şekil 1,1 ' de açıklanmıştır.

> [!CAUTION]
> Bu yalnızca tanıtım amaçlıdır ve olduğu gibi derlenmesi ve çalıştırılması garanti edilmez.
>
> Lütfen yerel Express Logic ortamında düzgün şekilde oluşturulacak tanıtım kaynak kodu dosyaları için NetX Duo HTTPS sürüm kodu dağıtımına bakın.  Ayrıca, bu tanıtımlar, yeni kullanıcılara HTTPS ve/veya NetX Duo HTTPS uygulaması tanıtılmak üzere bilinçli olarak çok basit bir şekilde tutulduğuna dikkat edin.

Bu örnekte, HTTP içerme dosyası *nx_web_http_client. h ve nx_web_http_server. h* ' de getirilir (*netx_web_http_common. h* otomatik olarak dahildir). Ardından, HTTP sunucusu "*tx_application_define*" içinde oluşturulur. HTTP sunucu denetimi bloğunun "*sunucu*" daha önce genel bir değişken olarak tanımlandığını unutmayın. Başarılı oluşturulduktan sonra, HTTPS sunucusu başlatılır. HTTPS Istemcisi oluşturulur. Dosyayı yazar ve dosyayı geri okur.

> [!NOTE]
> NX_WEB_HTTPS_ENABLE bu sistemde tanımlandı.

```c
/* This is a small demo of HTTPS on the high-performance NetX Duo TCP/IP stack.
   This demo relies on ThreadX, NetX Duo, and FileX to show an HTML
   transfer from the client and then back from the server.  */

#include  "tx_api.h"
#include  "fx_api.h"
#include  "nx_api.h"
#include  “nx_crypto.h”
#include  “nx_secure_tls_api.h”
#include  “nx_secure_x509.h”
#include  "nx_web_http_client.h"
#include  "nx_web_http_server.h"
#define    DEMO_STACK_SIZE         4096


/* Define the ThreadX and NetX object control blocks...  */

TX_THREAD               thread_0;
TX_THREAD               thread_1;
NX_PACKET_POOL          pool_0;
NX_PACKET_POOL          pool_1;
NX_IP                   ip_0;
NX_IP                   ip_1;
FX_MEDIA                ram_disk;

/* Define HTTP objects.  */

NX_WEB_HTTP_SERVER      my_server;
NX_WEB_HTTP_CLIENT      my_client;

/* Define the counters used in the demo application...  */

ULONG                   error_counter;


/* Define the RAM disk memory.  */

UCHAR                   ram_disk_memory[32000];

/* Include cryptographic routines for TLS. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Define TLS data for HTTPS. */
CHAR crypto_metadata[8928 * NX_WEB_HTTP_SESSION_MAX];
UCHAR tls_packet_buffer[16500];

/* NX_WEB_HTTP_SERVER_SESSION_MAX defaults to 2 in nx_web_http_server.h */
UCHAR server_tls_packet_buffer[16500 * NX_WEB_HTTP_SERVER_SESSION_MAX];

/* Define certificate containers. The server certificate is used to identify the NetX
   Web HTTPS server and the trusted certificate is used by the client to verify the
   server’s identity certificate.  */
NX_SECURE_X509_CERT server_certificate;
NX_SECURE_X509_CERT trusted_certificate;

/* Remote certificates need both an NX_SECURE_X509_CERT container and an associated
   buffer. The number of certificates depends on the remote host, but usually at least
   two certificates will be sent – the identity certificate for the host and the
   certificate that issued the identity certificate. */
NX_SECURE_X509_CERT remote_certificate, remote_issuer;

UCHAR remote_cert_buffer[2000];
UCHAR remote_issuer_buffer[2000];

/* Certificate information for server and client (see NetX Secure TLS reference on X.509
    certificates for more information). Arrays are populated with binary versions Of
    certificates and keys and the corresponding “len” variables are assigned the lengths
    of that data. Trusted certificates do not need a private key. */
const UCHAR server_cert_der[] = { … };
const UINT  server_cert_derlen = … ;
const UCHAR server_cert_key_der[] = { … };
const UINT  server_cert_key_derlen = … ;

const UCHAR trusted_cert_der[] = { … };
const UINT  trusted_cert_derlen = … ;


/* Define function prototypes.  */

void    thread_0_entry(ULONG thread_input);
VOID    _fx_ram_driver(FX_MEDIA *media_ptr) ;
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
UINT    authentication_check(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
             CHAR *resource, CHAR **name, CHAR **password, CHAR **realm);
UINT tls_setup_callback(NX_WEB_HTTP_CLIENT *client_ptr,
   NX_SECURE_TLS_SESSION *tls_session);

/* Define the application's authentication check.  This is called by
   the HTTP server whenever a new request is received.  */
UINT  authentication_check(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
            CHAR *resource, CHAR **name, CHAR **password, CHAR **realm)
{
    /* Just use a simple name, password, and realm for all
       requests and resources.  */
    *name =     "name";
    *password = "password";
    *realm =    "NetX Web HTTP demo";

    /* Request basic authentication.  */
    return(NX_WEB_HTTP_BASIC_AUTHENTICATE);
}

/* Define the TLS setup callback for HTTPS Client. This function is invoked when the
   HTTPS client is started – all TLS per-session initialization should go in here. */
UINT tls_setup_callback(NX_WEB_HTTP_CLIENT *client_ptr,
  NX_SECURE_TLS_SESSION *tls_session)
{
    UINT status;

    /* Initialize and create TLS session. */
    nx_secure_tls_session_create(tls_session, &nx_crypto_tls_ciphers,
        crypto_metadata, sizeof(crypto_metadata));

    /* Allocate space for packet reassembly. */
    nx_secure_tls_session_packet_buffer_set(tls_session, tls_packet_buffer,
        sizeof(tls_packet_buffer));


    /* Add a CA Certificate to our trusted store for verifying incoming server
        certificates. */
    nx_secure_x509_certificate_initialize(&trusted_certificate, trusted_cert_der,
        trusted_cert_der_len, NX_NULL, 0, NULL, 0,
        NX_SECURE_X509_KEY_TYPE_NONE);
    nx_secure_tls_trusted_certificate_add(tls_session, &trusted_certificate);

    /* Need to allocate space for the certificate coming in from the remote host. */
    nx_secure_tls_remote_certificate_allocate(tls_session, &remote_certificate,
        remote_cert_buffer, sizeof(remote_cert_buffer));
    nx_secure_tls_remote_certificate_allocate(tls_session,
        &remote_issuer, remote_issuer_buffer,
        sizeof(remote_issuer_buffer));

    return(NX_SUCCESS);
 }

/* Define main entry point.  */

 int main()
 {
     /* Enter the ThreadX kernel.  */
     tx_kernel_enter();
 }

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

    CHAR    *pointer;

    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;

    /* Create the main thread.  */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
        pointer, DEMO_STACK_SIZE,
        2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* Create packet pool.  */
    nx_packet_pool_create(&pool_0, "NetX Packet Pool 0",
        600, pointer, 8192);
    pointer = pointer + 8192;

    /* Create an IP instance.  */
    nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(1, 2, 3, 4),
        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
        pointer, 4096, 1);
    pointer =  pointer + 4096;

    /* Create another packet pool. */
    nx_packet_pool_create(&pool_1, "NetX Packet Pool 1", 600, pointer, 8192);
    pointer = pointer + 8192;

    /* Create another IP instance.  */
    nx_ip_create(&ip_1, "NetX IP Instance 1", IP_ADDRESS(1, 2, 3, 5),
        0xFFFFFF00UL, &pool_1, _nx_ram_network_driver,
        pointer, 4096, 1);
    pointer = pointer + 4096;

    /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
    nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable ARP and supply ARP cache memory for IP Instance 1.  */
    nx_arp_enable(&ip_1, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable TCP processing for both IP instances.  */
    nx_tcp_enable(&ip_0);
    nx_tcp_enable(&ip_1);

    /* Open the RAM disk.  */
    fx_media_open(&ram_disk, "RAM DISK",
        _fx_ram_driver, ram_disk_memory, pointer, 4096);
    pointer += 4096;

    /* Create the NetX Web HTTP Server.  */
    nx_web_http_server_create(&my_server, "My HTTP Server", &ip_1,
        NX_WEB_HTTPS_SERVER_PORT, &ram_disk,
        pointer, 4096, &pool_1, authentication_check, NX_NULL);
    pointer = pointer + 4096;

    /* The TLS server needs an identity certificate which is imported as a binary DER-
        encoded X.509 certificate and its associated private key (e.g. DER-encoded PKCS#1
        RSA private key). */
    nx_secure_x509_certificate_initialize(&server_certificate, server_cert_der,
        server_cert_der_len, NX_NULL, 0,
        server_cert_key_der, server_cert_key_der_len,
        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Setup TLS session data for the TCP server.
        This enables TLS and HTTPS for the server.  */
    nx_web_http_server_secure_configure(&my_server, &nx_crypto_tls_ciphers,
        crypto_metadata, sizeof(crypto_metadata), server_tls_packet_buffer,
        sizeof(server_tls_packet_buffer), &server_certificate, NX_NULL, 0,
        NX_NULL, 0, NX_NULL, 0);

    /* Start the HTTP Server.  */
    nx_web_http_server_start(&my_server);
}

/* Define the test thread.  */
void    thread_0_entry(ULONG thread_input)
{
    NX_PACKET   *my_packet;
    UINT        status;

    /* Create an HTTP client instance.  */
    status = nx_web_http_client_create(&my_client, "My Client", &ip_0, &pool_0, 600);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Prepare to send the simple 103-byte HTML file to the Server over HTTPS.  */
    status = nx_web_http_client_put_secure_start(&my_client, IP_ADDRESS(1,2,3,5),
        NX_WEB_HTTPS_SERVER_PORT, "/test.htm", "name", "password", 103, tls_setup_callback, 50);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Allocate a packet.  */
     tatus = nx_web_http_client_request_packet_allocate(&pool_0, &my_packet,
        NX_TCP_PACKET, NX_WAIT_FOREVER);

    /* Check status.  */
    if (status != NX_SUCCESS)
        return;

    /* Build a simple 103-byte HTML page.  */
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

    /* Complete the PUT by writing the total length.  */
    status =  nx_web_http_client_put_packet(&my_client, my_packet, 50);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Now GET the file back!  */
    status =  nx_web_http_client_get_secure_start(&my_client, IP_ADDRESS(1,2,3,5),
        NX_WEB_HTTPS_SERVER_PORT, "/test.htm",
        "name", "password", tls_setup_callback, 50);
 
    /* Check status.  */
    if (status)
        error_counter++;

    /* Get a packet.  */
    status =  nx_web_http_client_response_body_get(&my_client, &my_packet, 20);

    /* Check for an error.  */
    if ((status) || (my_packet -> nx_packet_length != 103))
        error_counter++;

    /* Check to see if we have a packet.  */
    if (status == NX_SUCCESS)
    {

        /* Yes, release it!  */
        nx_packet_release(my_packet);
    }

    /* Make sure TLS shuts down properly. */
    nx_web_http_client_delete(&my_client);

    /* Flush the media.  */
    fx_media_flush(&ram_disk);
}
```

**Şekil 1,1 NetX ve NetX güvenli TLS ile HTTPS kullanımı örneği**

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX için HTTP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir. Varsayılan değerler listelenir, ancak *nx_web_http_client. h ve nx_web_http_server. h*'a dahil etmeden önce yeniden tanımlanabilir:

- **NX_DISABLE_ERROR_CHECKING** Tanımlı, bu seçenek temel HTTP hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.
- **NX_WEB_HTTP_DIGEST_ENABLE** Tanımlanmışsa, MD5 özetini kullanarak kimlik doğrulaması HTTPS sunucusunda etkinleştirilir. Varsayılan olarak tanımlı değildir.
- **NX_WEB_HTTP_SERVER_PRIORITY** HTTPS sunucusu iş parçacığının önceliği. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.
- **NX_WEB_HTTP_NO_FILEX** Tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar. Bu seçenek tanımlanmışsa HTTPS Istemcisi herhangi bir değişiklik yapılmadan çalışır. HTTPS sunucusunun değiştirilmesi gerekir veya Kullanıcı düzgün bir şekilde çalışması için bir çok sayıda FileX hizmeti oluşturmanız gerekecektir.
- **NX_WEB_HTTP_TYPE_OF_SERVICE** HTTPS TCP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.
- **NX_WEB_HTTP_SERVER_THREAD_TIME_SLICE** Aynı önceliğe sahip iş parçacıklarını oluşturmadan önce, sunucu iş parçacığının çalışmasına izin verilen süreölçer onay işareti sayısı. Varsayılan değer 2 ' dir. Bu seçeneğin kullanım dışı olduğunu aklınızda edin.
- **NX_WEB_HTTP_FRAGMENT_OPTION** HTTP TCP istekleri için parça etkinleştirme. Varsayılan olarak, bu değer HTTP TCP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT.
- **NX_WEB_HTTP_SERVER_WINDOW_SIZE** Sunucu yuvası pencere boyutu. Varsayılan olarak, bu değer 2048 bayttır.
- **NX_WEB_HTTP_TIME_TO_LIVE** Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır.
- **NX_WEB_HTTP_SERVER_TIMEOUT** İç hizmetlerin askıya alınacağı ThreadX ticks sayısını belirtir. Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.
- **NX_WEB_HTTP_SERVER_TIMEOUT_ACCEPT** İç *nx_tcp_server_socket_accept ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.
- **NX_WEB_HTTP_SERVER_TIMEOUT_DISCONNECT** İç *nx_tcp_socket_disconnect ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.
- **NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE** İç *nx_tcp_socket_receive ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.
- **NX_WEB_HTTP_SERVER_TIMEOUT_SEND** İç *nx_tcp_socket_send ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.
- **NX_WEB_HTTP_MAX_HEADER_FIELD** **, http üst bilgisi alanının en büyük boyutunu belirtir. Varsayılan değer 256 ' dir.**
- * * NX_WEB_HTTP_MULTIPART_ENABLE * * * * tanımlıysa, HTTPS sunucusunun çok parçalı HTTP isteklerini desteklemesini sağlar. **
- **NX_WEB_HTTP_SERVER_MAX_PENDING** HTTPS sunucusu için sıraya alınabilen bağlantı sayısını belirtir. Varsayılan değer en fazla sunucu oturumu sayısı olarak ayarlanır.
- **NX_WEB_HTTP_MAX_RESOURCE** İstemci tarafından sağlanan *kaynak adında* izin verilen bayt sayısını belirtir. Varsayılan değer 40 olarak ayarlanır.
- **NX_WEB_HTTP_MAX_NAME** İstemci tarafından sağlanan *Kullanıcı adında* izin verilen bayt sayısını belirtir. Varsayılan değer 20 olarak ayarlanır.
- **NX_WEB_HTTP_MAX_PASSWORD** İstemci tarafından sağlanan *parolada* izin verilen bayt sayısını belirtir. Varsayılan değer 20 olarak ayarlanır.
- **NX_WEB_HTTP_SERVER_SESSION_MAX** Bir HTTP veya HTTPS sunucusu için eş zamanlı oturumların sayısını belirtir. Her oturum için bir TCP yuvası ve TLS oturumu (HTTPS etkinse) ayrılır. Varsayılan değer 2 olarak ayarlanır.
- **NX_WEB_HTTPS_ENABLE** Tanımlandıysa, bu makro TLS ve HTTPS 'yi etkinleştirmesine izin vermez. Yalnızca düz metin HTTP isteniyorsa kaynakları boşaltmak için tanımsız bırakın. Varsayılan olarak, bu makro tanımlı değildir.
- **NX_WEB_HTTPS_KEEPALIVE_DISABLE** Bu makro tanımlanmışsa, HTTP canlı tutma özelliğini devre dışı bırakır. Varsayılan olarak, bu makro tanımlı değildir.
- **NX_WEB_HTTP_SERVER_MIN_PACKET_SIZE** Sunucu oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir. En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir. Varsayılan değer 600 olarak ayarlanır.
- **NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE** Istemci oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir. En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir. Varsayılan değer 600 olarak ayarlanır.
- **NX_WEB_HTTP_SERVER_RETRY_SECONDS** Sunucu yuvası yeniden aktarım zaman aşımını saniye cinsinden ayarlayın. Varsayılan değer 2 olarak ayarlanır.
- **NX_WEB_HTTP_ SERVER_RETRY_MAX** Bu, sunucu yuvasıyla maksimum yeniden iletim sayısını ayarlar. Varsayılan değer 10 olarak ayarlanır.
- **NX_WEB_HTTP_ SERVER_RETRY_SHIFT** Bu değer, sonraki yeniden iletim zaman aşımını ayarlamak için kullanılır. Geçerli zaman aşımı, bu nedenle, yuva zaman aşımı kaydırma değerine göre kaydırılan, o kadar yeniden iletim sayısı ile çarpılır. Zaman aşımını katlama için varsayılan değer 1 ' e ayarlanır.
- **NX_WEB_HTTP_SERVER_RETRY_TRANSMIT_QUEUE_DEPTH** Bu, sunucu yuvası yeniden iletim kuyruğunda sıraya alınabilen en fazla paket sayısını belirtir. Sıraya alınan paketlerin sayısı bu sayıya ulaşırsa, bir veya daha fazla sıraya alınmış paket yayınlanana kadar başka paket gönderilemez. Varsayılan değer 20 olarak ayarlanır.
