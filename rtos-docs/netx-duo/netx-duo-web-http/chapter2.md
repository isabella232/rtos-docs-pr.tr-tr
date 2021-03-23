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
# <a name="chapter-2---installation-and-use-of-http-and-https"></a><span data-ttu-id="a7f4d-103">Bölüm 2-HTTP ve HTTPS yükleme ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="a7f4d-103">Chapter 2 - Installation and use of HTTP and HTTPS</span></span>

<span data-ttu-id="a7f4d-104">Bu bölümde, NetX Web HTTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-104">This chapter contains a description of various issues related to installation, setup, and usage of the NetX Web HTTP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="a7f4d-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="a7f4d-105">Product Distribution</span></span>

<span data-ttu-id="a7f4d-106">NetX için HTTP, adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="a7f4d-106">HTTP for NetX is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="a7f4d-107">Bu paket, aşağıdaki gibi üç kaynak dosyası, iki içerme dosyası ve bu belgeyi içeren bir dosya içerir:</span><span class="sxs-lookup"><span data-stu-id="a7f4d-107">The package includes three source files, two include files, and a file that contains this document, as follows:</span></span>

- <span data-ttu-id="a7f4d-108">**nx_web_http_common. h** NetX Web HTTP için ortak üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-108">**nx_web_http_common.h** Common header file for NetX Web HTTP</span></span>
- <span data-ttu-id="a7f4d-109">**nx_web_http_client. h** NetX Web için HTTP Istemcisi üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-109">**nx_web_http_client.h** Header file for HTTP Client for NetX Web</span></span>
- <span data-ttu-id="a7f4d-110">**nx_web_http_server. h** NetX Web için HTTP sunucusu üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-110">**nx_web_http_server.h** Header file for HTTP Server for NetX Web</span></span>
- <span data-ttu-id="a7f4d-111">**nx_web_http_client. c** NetX Web için HTTP Istemcisi için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-111">**nx_web_http_client.c** C Source file for HTTP Client for NetX Web</span></span>
- <span data-ttu-id="a7f4d-112">**nx_web_http_server. c** NetX Web için HTTP sunucusu için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-112">**nx_web_http_server.c** C Source file for HTTP Server for NetX Web</span></span>
- <span data-ttu-id="a7f4d-113">**nx_tcpserver. c** Birden çok TCP yuvası için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-113">**nx_tcpserver.c** C Source file for multiple TCP sockets</span></span>
- <span data-ttu-id="a7f4d-114">**nx_tcpserver. h** HTTPS sunucu sembolleri tanımlamak için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-114">**nx_tcpserver.h** Header file for defining HTTPS Server symbols</span></span>
- <span data-ttu-id="a7f4d-115">**nx_md5. c** MD5 Özet algoritmaları</span><span class="sxs-lookup"><span data-stu-id="a7f4d-115">**nx_md5.c** MD5 digest algorithms</span></span>
- <span data-ttu-id="a7f4d-116">**filex_stub. h** FileX yoksa saplama dosyası</span><span class="sxs-lookup"><span data-stu-id="a7f4d-116">**filex_stub.h** Stub file if FileX is not present</span></span>
- <span data-ttu-id="a7f4d-117">**nx_web_http.pdf** NetX Web için HTTP açıklaması</span><span class="sxs-lookup"><span data-stu-id="a7f4d-117">**nx_web_http.pdf** Description of HTTP for NetX Web</span></span>
- <span data-ttu-id="a7f4d-118">**demo_netx_web_http. c** NetX Web HTTP tanıtımı</span><span class="sxs-lookup"><span data-stu-id="a7f4d-118">**demo_netx_web_http.c** NetX Web HTTP demonstration</span></span>

## <a name="http-installation"></a><span data-ttu-id="a7f4d-119">HTTP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="a7f4d-119">HTTP Installation</span></span>

<span data-ttu-id="a7f4d-120">NetX Web HTTP 'yi kullanmak için, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-120">In order to use NetX Web HTTP, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="a7f4d-121">Örneğin, NetX Duo "*\threadx\arm7\green*" dizinine yüklenmişse, *NETX Web http istemci uygulamaları için* *nx_web_http_client. h* ve Nx_web_http_client. c ve *netx Web http sunucusu uygulamaları için nx_web_http_server. h, nx_web_http_server. c, nx_tcpserver. c ve nx_tcpserver. h. Hem istemci hem de sunucu uygulamaları için nx_web_http_common. h de bu dizinde olmalıdır.* Özet kimlik doğrulaması kullanılıyorsa, nx_md5. c de bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-121">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nx_web_http_client.h* and *nx_web_http_client.c for NetX Web HTTP Client applications, and nx_web_http_server.h*, *nx_web_http_server.c, nx_tcpserver.c and nx_tcpserver.h for NetX Web HTTP Server applications. For both client and server applications, nx_web_http_common.h must be in this directory as well. nx_md5.c* should also be copied into this directory if digest authentication is being used.</span></span> <span data-ttu-id="a7f4d-122">Tanıtım ' RAM sürücüsü ' uygulaması için HTTP Istemcisi ve sunucu dosyaları aynı dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-122">For the demo ‘ram driver’ application HTTP Client and Server files should be copied into the same directory.</span></span>

<span data-ttu-id="a7f4d-123">TLS kullanılıyorsa, TLS kaynak dosyalarını içeren ayrı bir NetX güvenli dizininiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-123">If using TLS, you should have a separate NetX Secure directory containing the TLS source files.</span></span>

## <a name="using-http"></a><span data-ttu-id="a7f4d-124">HTTP kullanma</span><span class="sxs-lookup"><span data-stu-id="a7f4d-124">Using HTTP</span></span>

<span data-ttu-id="a7f4d-125">NetX Web HTTP kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-125">Using NetX Web HTTP is easy.</span></span> <span data-ttu-id="a7f4d-126">Temel olarak, uygulama kodu *nx_web_http_client.* h ve/veya *nx_web_http_server.* h içermelidir *tx_api. h, fx_api. h* ve *nx_api. h* (*nx_web_http_common. h* otomatik olarak eklenir).</span><span class="sxs-lookup"><span data-stu-id="a7f4d-126">Basically, the application code must include *nx_web_http_client.h* and/or *nx_web_http_server.h* after it includes *tx_api.h, fx_api.h,* and *nx_api.h* (*nx_web_http_common.h* is automatically included).</span></span> <span data-ttu-id="a7f4d-127">Bu üst bilgiler, uygulamanın sırasıyla ThreadX, FileX ve NetX Duo kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-127">Those headers enable the application to use ThreadX, FileX, and NetX Duo, respectively.</span></span> <span data-ttu-id="a7f4d-128">HTTPS desteği için, *nx_secure_tls. h* dosyası, TLS desteğini getirmek üzere eklendikten sonra üst bilgiler eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-128">For HTTPS support, the headers must be included after the *nx_secure_tls.h* file is included to bring in TLS support.</span></span>

<span data-ttu-id="a7f4d-129">HTTP üstbilgi dosyaları eklendikten sonra, uygulama kodu daha sonra bu kılavuzda belirtilen HTTP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-129">Once the HTTP header files are included, the application code is then able to make the HTTP function calls specified later in this guide.</span></span> <span data-ttu-id="a7f4d-130">Uygulama Ayrıca, http (s *) istemcileri için nx_web_http_client. c* *NX_TCPSERVER ve (http (s) sunucuları için, nx_web_http_server.* c ' ye ve derleme sürecinde *nx_md5. c (Özet kimlik doğrulaması için)* ile bağlantı etmelidir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-130">The application must also link with *nx_web_http_client.c for HTTP(S) clients*, *nx_web_http_server.c and nx_tcpserver.c for HTTP(S) servers*, and *nx_md5.c (for digest authentication)* in the build process.</span></span> <span data-ttu-id="a7f4d-131">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-131">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="a7f4d-132">Bu, NetX Web HTTP 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-132">This is all that is required to use NetX Web HTTP.</span></span>

> [!NOTE]
> <span data-ttu-id="a7f4d-133">Yapı işleminde NX_WEB_HTTP_DIGEST_ENABLE belirtilmemişse, *MD5. c* dosyasının uygulamaya eklenmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-133">If NX_WEB_HTTP_DIGEST_ENABLE is not specified in the build process, the *md5.c* file does not need to be added to the application.</span></span> <span data-ttu-id="a7f4d-134">Benzer şekilde, HTTP Istemci özellikleri gerekmiyorsa, *nx_web_http_client. c* dosyası atlanabilir ve hiçbir http sunucusu özelliği gerekmiyorsa, *nx_web_http_server. c* atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-134">Similarly, if no HTTP Client capabilities are required, the *nx_web_http_client.c* file may be omitted and if no HTTP Server capabilities are required, *nx_web_http_server.c* may be omitted.</span></span>
>
> <span data-ttu-id="a7f4d-135">HTTPS 'yi etkinleştirmek için NX_WEB_HTTPS_ENABLE tanımlanmamışsa (yalnızca düz metin HTTP kullanmak yerine), NetX güvenli TLS 'nin derlemede olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-135">Unless NX_WEB_HTTPS_ENABLE is defined in order to enable HTTPS (instead of using only plaintext HTTP) then NetX Secure TLS does not need to be in the build.</span></span>
>
> <span data-ttu-id="a7f4d-136">HTTP, NetX TCP hizmetlerini kullandığından, HTTP kullanmadan önce *nx_tcp_enable ()* çağrısıyla TCP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-136">Since HTTP utilizes NetX TCP services, TCP must be enabled with the *nx_tcp_enable()* call prior to using HTTP.</span></span>
>
> <span data-ttu-id="a7f4d-137">HTTPS 'yi NetX güvenli TLS ile kullanırken, HTTPS yordamları çağrılmadan önce TLS *nx_secure_tls_initialize ()* ile başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-137">When using HTTPS with NetX Secure TLS, TLS must be initialized with *nx_secure_tls_initialize()* prior to calling HTTPS routines.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="a7f4d-138">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="a7f4d-138">Small Example System</span></span>

<span data-ttu-id="a7f4d-139">NetX Web HTTP 'nin nasıl kullanılacağına ilişkin bir örnek aşağıda şekil 1,1 ' de açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-139">An example of how to use NetX Web HTTP is described in Figure 1.1 below.</span></span>

> [!CAUTION]
> <span data-ttu-id="a7f4d-140">Bu yalnızca tanıtım amaçlıdır ve olduğu gibi derlenmesi ve çalıştırılması garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-140">This is provided for demonstration purposes only and is not guaranteed to compile and run as is.</span></span>
>
> <span data-ttu-id="a7f4d-141">Lütfen yerel Express Logic ortamında düzgün şekilde oluşturulacak tanıtım kaynak kodu dosyaları için NetX Duo HTTPS sürüm kodu dağıtımına bakın.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-141">Please refer to the NetX Duo HTTPS release code distribution for  demo source code file(s) that will properly build in the native Express Logic environment.</span></span>  <span data-ttu-id="a7f4d-142">Ayrıca, bu tanıtımlar, yeni kullanıcılara HTTPS ve/veya NetX Duo HTTPS uygulaması tanıtılmak üzere bilinçli olarak çok basit bir şekilde tutulduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-142">Also be aware that these demos are intentionally kept very simple as they are intended to introduce HTTPS and/or NetX Duo HTTPS application to new users.</span></span>

<span data-ttu-id="a7f4d-143">Bu örnekte, HTTP içerme dosyası *nx_web_http_client. h ve nx_web_http_server. h* ' de getirilir (*netx_web_http_common. h* otomatik olarak dahildir).</span><span class="sxs-lookup"><span data-stu-id="a7f4d-143">In this example, the HTTP include file *nx_web_http_client.h and nx_web_http_server.h are* brought in (*netx_web_http_common.h* is included automatically).</span></span> <span data-ttu-id="a7f4d-144">Ardından, HTTP sunucusu "*tx_application_define*" içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-144">Next, the HTTP Server is created in “*tx_application_define*”.</span></span> <span data-ttu-id="a7f4d-145">HTTP sunucu denetimi bloğunun "*sunucu*" daha önce genel bir değişken olarak tanımlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-145">Note that the HTTP Server control block “*Server*” was defined as a global variable previously.</span></span> <span data-ttu-id="a7f4d-146">Başarılı oluşturulduktan sonra, HTTPS sunucusu başlatılır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-146">After successful creation, the HTTPS Server is started.</span></span> <span data-ttu-id="a7f4d-147">HTTPS Istemcisi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-147">The HTTPS Client is then created.</span></span> <span data-ttu-id="a7f4d-148">Dosyayı yazar ve dosyayı geri okur.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-148">It writes the file and reads the file back.</span></span>

> [!NOTE]
> <span data-ttu-id="a7f4d-149">NX_WEB_HTTPS_ENABLE bu sistemde tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-149">NX_WEB_HTTPS_ENABLE is defined on this system.</span></span>

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

<span data-ttu-id="a7f4d-150">**Şekil 1,1 NetX ve NetX güvenli TLS ile HTTPS kullanımı örneği**</span><span class="sxs-lookup"><span data-stu-id="a7f4d-150">**Figure 1.1 Example of HTTPS use with NetX and NetX Secure TLS**</span></span>

## <a name="configuration-options"></a><span data-ttu-id="a7f4d-151">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="a7f4d-151">Configuration Options</span></span>

<span data-ttu-id="a7f4d-152">NetX için HTTP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-152">There are several configuration options for building HTTP for NetX.</span></span> <span data-ttu-id="a7f4d-153">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-153">Following is a list of all options, where each is described in detail.</span></span> <span data-ttu-id="a7f4d-154">Varsayılan değerler listelenir, ancak *nx_web_http_client. h ve nx_web_http_server. h*'a dahil etmeden önce yeniden tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="a7f4d-154">The default values are listed but can be redefined prior to inclusion of *nx_web_http_client.h and nx_web_http_server.h*:</span></span>

- <span data-ttu-id="a7f4d-155">**NX_DISABLE_ERROR_CHECKING** Tanımlı, bu seçenek temel HTTP hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-155">**NX_DISABLE_ERROR_CHECKING** Defined, this option removes the basic HTTP error checking.</span></span> <span data-ttu-id="a7f4d-156">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-156">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="a7f4d-157">**NX_WEB_HTTP_DIGEST_ENABLE** Tanımlanmışsa, MD5 özetini kullanarak kimlik doğrulaması HTTPS sunucusunda etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-157">**NX_WEB_HTTP_DIGEST_ENABLE** If defined, authentication using the MD5 digest is enabled on the HTTPS Server.</span></span> <span data-ttu-id="a7f4d-158">Varsayılan olarak tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-158">By default it is not defined.</span></span>
- <span data-ttu-id="a7f4d-159">**NX_WEB_HTTP_SERVER_PRIORITY** HTTPS sunucusu iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-159">**NX_WEB_HTTP_SERVER_PRIORITY** The priority of the HTTPS Server thread.</span></span> <span data-ttu-id="a7f4d-160">Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-160">By default, this value is defined as 16 to specify priority 16.</span></span>
- <span data-ttu-id="a7f4d-161">**NX_WEB_HTTP_NO_FILEX** Tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-161">**NX_WEB_HTTP_NO_FILEX** Defined, this option provides a stub for FileX dependencies.</span></span> <span data-ttu-id="a7f4d-162">Bu seçenek tanımlanmışsa HTTPS Istemcisi herhangi bir değişiklik yapılmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-162">The HTTPS Client will function without any change if this option is defined.</span></span> <span data-ttu-id="a7f4d-163">HTTPS sunucusunun değiştirilmesi gerekir veya Kullanıcı düzgün bir şekilde çalışması için bir çok sayıda FileX hizmeti oluşturmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-163">The HTTPS Server will need to either be modified or the user will have to create a handful of FileX services in order to function properly.</span></span>
- <span data-ttu-id="a7f4d-164">**NX_WEB_HTTP_TYPE_OF_SERVICE** HTTPS TCP istekleri için gereken hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-164">**NX_WEB_HTTP_TYPE_OF_SERVICE** Type of service required for the HTTPS TCP requests.</span></span> <span data-ttu-id="a7f4d-165">Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-165">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="a7f4d-166">**NX_WEB_HTTP_SERVER_THREAD_TIME_SLICE** Aynı önceliğe sahip iş parçacıklarını oluşturmadan önce, sunucu iş parçacığının çalışmasına izin verilen süreölçer onay işareti sayısı.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-166">**NX_WEB_HTTP_SERVER_THREAD_TIME_SLICE** The number of timer ticks the Server thread is allowed to run before yielding to threads of the same priority.</span></span> <span data-ttu-id="a7f4d-167">Varsayılan değer 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-167">The default value is 2.</span></span> <span data-ttu-id="a7f4d-168">Bu seçeneğin kullanım dışı olduğunu aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-168">Note this option is deprecated.</span></span>
- <span data-ttu-id="a7f4d-169">**NX_WEB_HTTP_FRAGMENT_OPTION** HTTP TCP istekleri için parça etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-169">**NX_WEB_HTTP_FRAGMENT_OPTION** Fragment enable for HTTP TCP requests.</span></span> <span data-ttu-id="a7f4d-170">Varsayılan olarak, bu değer HTTP TCP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-170">By default, this value is NX_DONT_FRAGMENT to disable HTTP TCP fragmenting.</span></span>
- <span data-ttu-id="a7f4d-171">**NX_WEB_HTTP_SERVER_WINDOW_SIZE** Sunucu yuvası pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-171">**NX_WEB_HTTP_SERVER_WINDOW_SIZE** Server socket window size.</span></span> <span data-ttu-id="a7f4d-172">Varsayılan olarak, bu değer 2048 bayttır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-172">By default, this value is 2048 bytes.</span></span>
- <span data-ttu-id="a7f4d-173">**NX_WEB_HTTP_TIME_TO_LIVE** Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-173">**NX_WEB_HTTP_TIME_TO_LIVE** Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="a7f4d-174">Varsayılan değer 0x80 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-174">The default value is set to 0x80.</span></span>
- <span data-ttu-id="a7f4d-175">**NX_WEB_HTTP_SERVER_TIMEOUT** İç hizmetlerin askıya alınacağı ThreadX ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-175">**NX_WEB_HTTP_SERVER_TIMEOUT** Specifies the number of ThreadX ticks that internal services will suspend for.</span></span> <span data-ttu-id="a7f4d-176">Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-176">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="a7f4d-177">**NX_WEB_HTTP_SERVER_TIMEOUT_ACCEPT** İç *nx_tcp_server_socket_accept ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-177">**NX_WEB_HTTP_SERVER_TIMEOUT_ACCEPT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_server_socket_accept()* calls.</span></span> <span data-ttu-id="a7f4d-178">Varsayılan değer (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-178">The default value is set to (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="a7f4d-179">**NX_WEB_HTTP_SERVER_TIMEOUT_DISCONNECT** İç *nx_tcp_socket_disconnect ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-179">**NX_WEB_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_disconnect()* calls.</span></span> <span data-ttu-id="a7f4d-180">Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-180">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="a7f4d-181">**NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE** İç *nx_tcp_socket_receive ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-181">**NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_receive()* calls.</span></span> <span data-ttu-id="a7f4d-182">Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-182">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="a7f4d-183">**NX_WEB_HTTP_SERVER_TIMEOUT_SEND** İç *nx_tcp_socket_send ()* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-183">**NX_WEB_HTTP_SERVER_TIMEOUT_SEND** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_send()* calls.</span></span> <span data-ttu-id="a7f4d-184">Varsayılan değer 10 saniye (10 \* *NX_IP_PERIODIC_RATE*) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-184">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="a7f4d-185">**NX_WEB_HTTP_MAX_HEADER_FIELD** **, http üst bilgisi alanının en büyük boyutunu belirtir. Varsayılan değer 256 ' dir.**</span><span class="sxs-lookup"><span data-stu-id="a7f4d-185">**NX_WEB_HTTP_MAX_HEADER_FIELD** **Specifies the maximum size of the HTTP header field. The default value is 256.**</span></span>
- <span data-ttu-id="a7f4d-186">\* \* NX_WEB_HTTP_MULTIPART_ENABLE \* \* \* \* tanımlıysa, HTTPS sunucusunun çok parçalı HTTP isteklerini desteklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-186">\*\*NX_WEB_HTTP_MULTIPART_ENABLE \*\* \*\*If defined, enables HTTPS Server to support multipart HTTP requests.</span></span> **
- <span data-ttu-id="a7f4d-187">**NX_WEB_HTTP_SERVER_MAX_PENDING** HTTPS sunucusu için sıraya alınabilen bağlantı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-187">**NX_WEB_HTTP_SERVER_MAX_PENDING** Specifies the number of connections that can be queued for the HTTPS Server.</span></span> <span data-ttu-id="a7f4d-188">Varsayılan değer en fazla sunucu oturumu sayısı olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-188">The default value is set to twice the maximum number of server sessions.</span></span>
- <span data-ttu-id="a7f4d-189">**NX_WEB_HTTP_MAX_RESOURCE** İstemci tarafından sağlanan *kaynak adında* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-189">**NX_WEB_HTTP_MAX_RESOURCE** Specifies the number of bytes allowed in a client supplied *resource name*.</span></span> <span data-ttu-id="a7f4d-190">Varsayılan değer 40 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-190">The default value is set to 40.</span></span>
- <span data-ttu-id="a7f4d-191">**NX_WEB_HTTP_MAX_NAME** İstemci tarafından sağlanan *Kullanıcı adında* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-191">**NX_WEB_HTTP_MAX_NAME** Specifies the number of bytes allowed in a client supplied *username*.</span></span> <span data-ttu-id="a7f4d-192">Varsayılan değer 20 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-192">The default value is set to 20.</span></span>
- <span data-ttu-id="a7f4d-193">**NX_WEB_HTTP_MAX_PASSWORD** İstemci tarafından sağlanan *parolada* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-193">**NX_WEB_HTTP_MAX_PASSWORD** Specifies the number of bytes allowed in a client supplied *password*.</span></span> <span data-ttu-id="a7f4d-194">Varsayılan değer 20 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-194">The default value is set to 20.</span></span>
- <span data-ttu-id="a7f4d-195">**NX_WEB_HTTP_SERVER_SESSION_MAX** Bir HTTP veya HTTPS sunucusu için eş zamanlı oturumların sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-195">**NX_WEB_HTTP_SERVER_SESSION_MAX** Specifies the number of simultaneous sessions for an HTTP or HTTPS Server.</span></span> <span data-ttu-id="a7f4d-196">Her oturum için bir TCP yuvası ve TLS oturumu (HTTPS etkinse) ayrılır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-196">A TCP socket and a TLS session (if HTTPS is enabled) are allocated for each session.</span></span> <span data-ttu-id="a7f4d-197">Varsayılan değer 2 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-197">The default value is set to 2.</span></span>
- <span data-ttu-id="a7f4d-198">**NX_WEB_HTTPS_ENABLE** Tanımlandıysa, bu makro TLS ve HTTPS 'yi etkinleştirmesine izin vermez.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-198">**NX_WEB_HTTPS_ENABLE** If defined, this macro enables TLS and HTTPS.</span></span> <span data-ttu-id="a7f4d-199">Yalnızca düz metin HTTP isteniyorsa kaynakları boşaltmak için tanımsız bırakın.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-199">Leave undefined to free up resources if only plaintext HTTP is desired.</span></span> <span data-ttu-id="a7f4d-200">Varsayılan olarak, bu makro tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-200">By default, this macro is not defined.</span></span>
- <span data-ttu-id="a7f4d-201">**NX_WEB_HTTPS_KEEPALIVE_DISABLE** Bu makro tanımlanmışsa, HTTP canlı tutma özelliğini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-201">**NX_WEB_HTTPS_KEEPALIVE_DISABLE** If defined, this macro disables HTTP keep-alive feature.</span></span> <span data-ttu-id="a7f4d-202">Varsayılan olarak, bu makro tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-202">By default, this macro is not defined.</span></span>
- <span data-ttu-id="a7f4d-203">**NX_WEB_HTTP_SERVER_MIN_PACKET_SIZE** Sunucu oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-203">**NX_WEB_HTTP_SERVER_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at server creation.</span></span> <span data-ttu-id="a7f4d-204">En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-204">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="a7f4d-205">Varsayılan değer 600 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-205">The default value is set to 600.</span></span>
- <span data-ttu-id="a7f4d-206">**NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE** Istemci oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-206">**NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at Client creation.</span></span> <span data-ttu-id="a7f4d-207">En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-207">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="a7f4d-208">Varsayılan değer 600 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-208">The default value is set to 600.</span></span>
- <span data-ttu-id="a7f4d-209">**NX_WEB_HTTP_SERVER_RETRY_SECONDS** Sunucu yuvası yeniden aktarım zaman aşımını saniye cinsinden ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-209">**NX_WEB_HTTP_SERVER_RETRY_SECONDS** Set the Server socket retransmission timeout in seconds.</span></span> <span data-ttu-id="a7f4d-210">Varsayılan değer 2 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-210">The default value is set to 2.</span></span>
- <span data-ttu-id="a7f4d-211">**NX_WEB_HTTP_ SERVER_RETRY_MAX** Bu, sunucu yuvasıyla maksimum yeniden iletim sayısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-211">**NX_WEB_HTTP_ SERVER_RETRY_MAX** This sets the maximum number of retransmissions on Server socket.</span></span> <span data-ttu-id="a7f4d-212">Varsayılan değer 10 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-212">The default value is set to 10.</span></span>
- <span data-ttu-id="a7f4d-213">**NX_WEB_HTTP_ SERVER_RETRY_SHIFT** Bu değer, sonraki yeniden iletim zaman aşımını ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-213">**NX_WEB_HTTP_ SERVER_RETRY_SHIFT** This value is used to set the next retransmission timeout.</span></span> <span data-ttu-id="a7f4d-214">Geçerli zaman aşımı, bu nedenle, yuva zaman aşımı kaydırma değerine göre kaydırılan, o kadar yeniden iletim sayısı ile çarpılır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-214">The current timeout is multiplied by the number of retransmissions thus far, shifted by the value of the socket timeout shift.</span></span> <span data-ttu-id="a7f4d-215">Zaman aşımını katlama için varsayılan değer 1 ' e ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-215">The default value is set to 1 for doubling the timeout.</span></span>
- <span data-ttu-id="a7f4d-216">**NX_WEB_HTTP_SERVER_RETRY_TRANSMIT_QUEUE_DEPTH** Bu, sunucu yuvası yeniden iletim kuyruğunda sıraya alınabilen en fazla paket sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-216">**NX_WEB_HTTP_SERVER_RETRY_TRANSMIT_QUEUE_DEPTH** This specifies the maximum number of packets that can be enqueued on the Server socket retransmission queue.</span></span> <span data-ttu-id="a7f4d-217">Sıraya alınan paketlerin sayısı bu sayıya ulaşırsa, bir veya daha fazla sıraya alınmış paket yayınlanana kadar başka paket gönderilemez.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-217">If the number of packets enqueued reaches this number, no more packets can be sent until one or more enqueued packets are released.</span></span> <span data-ttu-id="a7f4d-218">Varsayılan değer 20 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7f4d-218">The default value is set to 20.</span></span>
