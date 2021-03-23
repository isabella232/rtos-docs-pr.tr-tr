---
title: Bölüm 2-Azure RTOS NetX güvenli DTLS yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX güvenli DTLS bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3533471edf17ec6e812027ef0af672a00773f968
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825691"
---
# <a name="chapter-2-installation-and-use-of-azure-rtos-netx-secure-dtls"></a><span data-ttu-id="4b6f6-103">Bölüm 2: Azure RTOS NetX güvenli DTLS yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="4b6f6-103">Chapter 2: Installation and use of Azure RTOS NetX Secure DTLS</span></span>

<span data-ttu-id="4b6f6-104">Bu bölümde, Azure RTOS NetX güvenli DTLS bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Secure DTLS component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="4b6f6-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="4b6f6-105">Product Distribution</span></span>

<span data-ttu-id="4b6f6-106">NetX güvenli, adresinde bulunabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="4b6f6-106">NetX Secure is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="4b6f6-107">Paket, kaynak dosyaları, içerme dosyaları ve bu belgeyi içeren bir PDF dosyasını aşağıdaki gibi içerir:</span><span class="sxs-lookup"><span data-stu-id="4b6f6-107">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="4b6f6-108">**nx_secure_dtls_api. h** NetX güvenli DTLS için ortak API üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="4b6f6-108">**nx_secure_dtls_api.h** Public API header file for NetX Secure DTLS</span></span>
- <span data-ttu-id="4b6f6-109">**nx_secure_dtls_user. h** Kullanıcı NetX güvenli DTLS için üst bilgi dosyasını tanımlıyor</span><span class="sxs-lookup"><span data-stu-id="4b6f6-109">**nx_secure_dtls_user.h** User defines header file for NetX Secure DTLS</span></span>
- <span data-ttu-id="4b6f6-110">**nx_secure_ bağlantı noktası. h** NetX güvenli için platforma özgü tanımlar</span><span class="sxs-lookup"><span data-stu-id="4b6f6-110">**nx_secure_ port.h** Platform-specific definitions for NetX Secure</span></span>
- <span data-ttu-id="4b6f6-111">**nx_secure_dtls. h** NetX güvenli DTLS için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="4b6f6-111">**nx_secure_dtls.h** Header file for NetX Secure DTLS</span></span>
- <span data-ttu-id="4b6f6-112">**nx_secure_tls. h** NetX güvenli TLS için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="4b6f6-112">**nx_secure_tls.h** Header file for NetX Secure TLS</span></span>
- <span data-ttu-id="4b6f6-113">NetX güvenli DTLS için **nx_secure_dtls \* . c/h** c/h kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="4b6f6-113">**nx_secure_dtls\*.c/h** C/H Source files for NetX Secure DTLS</span></span>
- <span data-ttu-id="4b6f6-114">NetX güvenli TLS için **nx_secure_tls \* . c/h** c/h kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="4b6f6-114">**nx_secure_tls\*.c/h** C/H Source files for NetX Secure TLS</span></span>
- <span data-ttu-id="4b6f6-115">NetX güvenli şifreleme için **nx_crypto \* . c/h** c/h kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="4b6f6-115">**nx_crypto\*.c/h** C/H Source files for NetX Secure Cryptography</span></span>
- <span data-ttu-id="4b6f6-116">X. 509.440 dijital sertifikaları için **\* . c/h** c/h kaynak dosyalarını nx_secure_x509.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-116">**nx_secure_x509\*.c/h** C/H Source files for X.509 digital certificates.</span></span>
- <span data-ttu-id="4b6f6-117">**demo_netx_secure_dtls. c** NetX güvenli DTLS tanıtımı için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="4b6f6-117">**demo_netx_secure_dtls.c** C Source file for NetX Secure DTLS Demo</span></span>
- <span data-ttu-id="4b6f6-118">**NetX_Secure_DTLS_User_Guide.pdf** NetX güvenli ürününün PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="4b6f6-118">**NetX_Secure_DTLS_User_Guide.pdf** PDF description of NetX Secure product</span></span>

> [!NOTE]
> <span data-ttu-id="4b6f6-119">Nx_crypto \* dosyaları, NetX güvenli üst dizininin bir alt dizinindeki farklı donanım platformları için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-119">The nx_crypto\* files are provided for different hardware platforms in a subdirectory of the NetX Secure parent directory.</span></span>

## <a name="netx-secure-dtls-installation"></a><span data-ttu-id="4b6f6-120">NetX güvenli DTLS yüklemesi</span><span class="sxs-lookup"><span data-stu-id="4b6f6-120">NetX Secure DTLS Installation</span></span>

<span data-ttu-id="4b6f6-121">NetX güvenli DTLS 'yi kullanmak için, daha önce bahsedilen dağıtımın tamamı, NetX 'in yüklü olduğu aynı dizin düzeyine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-121">In order to use NetX Secure DTLS, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="4b6f6-122">Örneğin, "*\threadx\arm7\netx*" dizininde NETX yüklüyse *nx_secure \* . \** dizinlerin "*\threadx\arm7\netxsecure*" dizinine kopyalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-122">For example, if NetX is installed in the directory “*\threadx\arm7\NetX*” then the *nx_secure\*.\** directories should be copied into “*\threadx\arm7\NetXSecure*”.</span></span>

## <a name="using-netx-secure-dlts"></a><span data-ttu-id="4b6f6-123">NetX güvenli DLCı 'leri kullanma</span><span class="sxs-lookup"><span data-stu-id="4b6f6-123">Using NetX Secure DLTS</span></span>

<span data-ttu-id="4b6f6-124">NetX güvenli DTLS kullanımı basittir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-124">Using NetX Secure DTLS is straightforward.</span></span> <span data-ttu-id="4b6f6-125">Uygulama kodu, *tx_api. h* ve *nx_api. h* (sırasıyla Threadx ve NETX için olan) öğesini ekledikten sonra *nx_secure_dtls_api. h* içermelidir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-125">The application code must include *nx_secure_dtls_api.h* after it includes *tx_api.h* and *nx_api.h* (which are for ThreadX and NetX, respectively).</span></span> <span data-ttu-id="4b6f6-126">*Nx_secure_dtls_api. h* dahil olduğunda, uygulama kodu daha sonra bu kılavuzda belirtilen NETX GÜVENLI DTLS işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-126">Once *nx_secure_dtls_api.h* is included, the application code is then able to make the NetX Secure DTLS function calls specified later in this guide.</span></span> <span data-ttu-id="4b6f6-127">Uygulamanın Ayrıca, *nx_secure \* . \** dosyaları netxsecure kitaplığına ve platforma özgü *nx_crypto \* . \** dosyaları, daha sonra son uygulama ikilisinde bağlantılı bir netxşifre kitaplığı içine aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-127">The application must also import the *nx_secure\*.\** files into a NetXSecure library, and the platform-specific *nx_crypto\*.\** files into a NetXCrypto library which are then linked into the final application binary.</span></span>

## <a name="small-example-system-dtls-client"></a><span data-ttu-id="4b6f6-128">Küçük örnek sistem (DTLS Istemcisi)</span><span class="sxs-lookup"><span data-stu-id="4b6f6-128">Small Example System (DTLS Client)</span></span>

<span data-ttu-id="4b6f6-129">NetX güvenli DTLS kullanmanın ne kadar kolay olduğunu gösteren bir örnek, aşağıda görüntülenen Şekil 1,1 ' de açıklanmış ve OpenSSL (ya da benzer) DTLS sunucusuyla çalışmak üzere tasarlanan basit bir DTLS Istemcisini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-129">An example of how easy it is to use NetX Secure DTLS is described in Figure 1.1, which appears below and demonstrates a simple DTLS Client, designed to work with an OpenSSL (or similar) DTLS server.</span></span> <span data-ttu-id="4b6f6-130">DTLS istemci programı yapısının bir NetX güvenli TLS Istemcisine çok benzediğini unutmayın (bkz. NetX güvenli TLS belgeleri).</span><span class="sxs-lookup"><span data-stu-id="4b6f6-130">Note that the DTLS client program structure is very similar to a NetX Secure TLS Client (see NetX Secure TLS documentation).</span></span> <span data-ttu-id="4b6f6-131">Bunun nedeni, DTLS protokolünün temel olarak UDP gibi güvenilir olmayan aktarım ağ protokolleri üzerinde kullanılması için bir TLS sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-131">This is because the DTLS protocol is essentially a version of TLS for use over unreliable transport network protocols such as UDP.</span></span>

```C
#include "tx_api.h"
#include "nx_api.h"
#include "nx_secure_dtls_api.h"

/* Define the size of our application stack. */
#define     DEMO_STACK_SIZE             4096

/* Define the remote server IP address using NetX IP_ADDRESS macro. */
#define     REMOTE_SERVER_IP_ADDRESS      IP_ADDRESS(192, 168, 1, 1)

/* Define the remote server port. */
#define     REMOTE_SERVER_PORT           4443

/* Define the size of the buffer used for incoming certificates. The
   Buffer will contain both the raw certificate data and an instance
   of the NX_SECURE_X509_CERT structure used for X.509 parsing. */
#define     REMOTE_CERT_BUFFER_SIZE     (sizeof(NX_SECURE_X509_CERT) + 2000)

/* Define the number of certificates we expect to receive from the server
   so we can allocate enough space for them. */
#define     REMOTE_CERT_NUMBER          2

/* Define the ThreadX and NetX object control blocks...  */

NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;
NX_UDP_SOCKET udp_socket;
NX_SECURE_DTLS_SESSION dtls_session;
NX_SECURE_X509_CERTIFICATE dtls_certificate;

/* Define space for remote certificate storage. The size of the
buffer is determined by the expected number of certificates times
the expected size of each certificate.   */
UCHAR remote_certificate_buffer[REMOTE_CERT_BUFFER_SIZE * REMOTE_CERT_NUMBER];

/* Define some data to send to the DTLS server. */
UCHAR request_data[] = { … };

/* Define the IP thread's stack area.  */
ULONG ip_thread_stack[3 * 1024 / sizeof(ULONG)];

/* Define packet pool for the demonstration.  */
#define NX_PACKET_POOL_SIZE ((1536 + sizeof(NX_PACKET)) * 32)

ULONG packet_pool_area[NX_PACKET_POOL_SIZE/sizeof(ULONG) + 64 / sizeof(ULONG)];

/* Define the ARP cache area.  */
ULONG arp_space_area[512 / sizeof(ULONG)];

/* Define the DTLS Client thread.  */
ULONG             dtls_client_thread_stack[6 * 1024 / sizeof(ULONG)];
TX_THREAD         dtls_client_thread;
void              client_thread_entry(ULONG thread_input);

/* Define the DTLS packet reassembly buffer. */
UCHAR dtls_packet_buffer[4000];

/* Define the metadata area for TLS cryptography. The actual size needed can be
   Ascertained by calling nx_secure_tls_metadata_size_calculate.
*/
UCHAR dtls_crypto_metadata[14000];

/* Pointer to the TLS/DTLS ciphersuite table that is included in the platform-
specific cryptography subdirectory. The table maps the cryptographic routines for
the platform to function pointers usable by the DTLS library.
*/
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Binary data for the DTLS Client X.509 trusted root CA certificate: ASN.1 DER-
   encoded. A trusted certificate must be provided for TLS/DTLS Client applications
   (unless an alternate authentication mechanism is used, such as PSK) or DTLS will
treat all certificates as untrusted and the handshake will fail.
*/
const UCHAR trusted_ca_data[] = { … }; /* DER-encoded binary certificate. */
const UINT trusted_ca_length[] = 0x574;

/* Define the application – initialize drivers and UDP setup.  */
void    tx_application_define(void *first_unused_memory)
{
    UINT  status;

    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* Create a packet pool. Check status for errors. */
    status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1536,
   (ULONG*)(((int)packet_pool_area + 64) & ~63) ,
   NX_PACKET_POOL_SIZE);

    /* Create an IP instance for the specific target. Check status for errors. */
    status = nx_ip_create(&ip_0, …);

    /* Enable ARP and supply ARP cache memory for IP Instance 0. Check status for
         errors. */
    status =  nx_arp_enable(&ip_0, (void *)arp_space_area, sizeof(arp_space_area));

    /* Enable UDP traffic. Check status for errors. */
    status =  nx_udp_enable(&ip_0);

    status =  nx_ip_fragment_enable(&ip_0);

    /* Initialize the NetX Secure TLS/DTLS system.  */
   nx_secure_tls_initialize();

    /* Create the client thread to start handling incoming requests. */
    tx_thread_create(&dtls_client_thread, "DTLS Client thread", client_thread_entry,
        0, dtls_client_thread_stack, sizeof(dtls_client_thread_stack),
        16, 16, 4, TX_AUTO_START);
}

     /* Thread to handle the DTLS Client instance. */
void client_thread_entry(ULONG thread_input)
{
    UINT       status;
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UCHAR receive_buffer[100];
    ULONG bytes;
    ULONG server_ipv4_address;

     /* We are not using the thread input parameter so suppress compiler warning. */
    NX_PARAMETER_NOT_USED(thread_input);

    /* Ensure the IP instance has been initialized.  */
    status =  nx_ip_status_check(&ip_0, NX_IP_INITIALIZE_DONE, &actual_status,
        NX_IP_PERIODIC_RATE);

    /* Check status for errors... */

    /* Create a UDP socket to use for our DTLS session.  */
    status =  nx_udp_socket_create(&ip_0, &udp_socket, "DTLS Client Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY, NX_IP_TIME_TO_LIVE, 8192);

    /* Check status for errors... */

    /* Create a DTLS session for our socket. This sets up the DTLS session object for
            later use with encryption, packet buffer space for decryption, and buffer
    space for incoming server X.509 certificates. */
    status =  nx_secure_dtls_session_create(&dtls_session,
        &nx_crypto_tls_ciphers,
        tls_crypto_metadata,
        sizeof(tls_crypto_metadata),
        dtls_packet_buffer,
        sizeof(dtls_packet_buffer),
        REMOTE_CERT_NUMBER,
        remote_certificate_buffer,
        sizeof(remote_certificate_buffer) );

    /* Initialize an X.509 certificate with our CA root certificate data. */
    nx_secure_x509_certificate_initialize(&certificate, trusted_ca_data,
        trusted_ca_length, NX_NULL, 0, NX_NULL, 0,
        NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the initialized certificate as a trusted root certificate. */
    nx_secure_dtls_session_trusted_certificate_add(&dtls_session, &certificate);

    /* Setup this thread to open a connection on the UDP socket to a remote server.
       The IP address can be used directly or it can be obtained via DNS or other
       means.  */
   server_ipv4_address = REMOTE_SERVER_IP_ADDRESS;

   /* Check for errors…  */

    /* Start the DTLS Session using the given UDP socket, remote server IP Address,
        and remote server port. */
    status = nx_secure_dtls_client_session_start(&dtls_session, &udp_socket,
        &ip_address, REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

        /* Allocate a DTLS packet to send some encrypted data to the server. */
        status = nx_secure_dtls_packet_allocate(&dtls_session, &pool_0, &send_packet,
     NX_TLS_PACKET, NX_WAIT_FOREVER);

        /* Check for errors…  */

         /* Populate the packet with some data. */
        nx_packet_data_append(send_packet, request_data, sizeof(request_data), &pool_0,
            NX_WAIT_FOREVER);

         /* Send the request over the DTLS Session, encrypting it before sending. */
    status = nx_secure_dtls_session_send(&dtls_session, send_packet, NX_WAIT_FOREVER);

        /* Check for errors…  */
        if (status)
        {
              /* Release the packet since we could not send it.  */
              nx_packet_release(send_packet);
        }

     /* Receive the response from the server. */
    status = nx_secure_dtls_session_receive(&dtls_session, &receive_packet,
       NX_WAIT_FOREVER);

    /* Extract the data we received from the remote server. */
    status = nx_packet_data_extract_offset(receive_packet, 0, receive_buffer, 100,
        &bytes);
    /* Display the response data. */
    receive_buffer[bytes] = 0;
    printf("Received data: %s\n", receive_buffer)
     /* End the DTLS session now that we have received our response. */
    status = nx_secure_dtls_session_end(&tls_session, NX_WAIT_FOREVER)

     /* Check for errors to make sure the session ended cleanly. */
     /* Clean up the UDP socket. */
    status =  nx_udp_socket_delete(&udp_socket)

    /* Check for errors... */

}
```

<span data-ttu-id="4b6f6-132">**Şekil 1,1 NetX ile NetX güvenli kullanımı örneği**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-132">**Figure 1.1 Example of NetX Secure use with NetX**</span></span>

## <a name="small-example-system-dtls-server"></a><span data-ttu-id="4b6f6-133">Küçük örnek sistem (DTLS sunucusu)</span><span class="sxs-lookup"><span data-stu-id="4b6f6-133">Small Example System (DTLS Server)</span></span>

<span data-ttu-id="4b6f6-134">Aşağıda görüntülenen ve basit bir DTLS sunucusunu gösteren şekil 1,2 ' de NetX güvenli kullanmanın ne kadar kolay olduğunu gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-134">An example of how easy it is to use NetX Secure is described in Figure 1.2, which appears below and demonstrates a simple DTLS Server.</span></span> <span data-ttu-id="4b6f6-135">DTLS sunucusunun tek bir UDP bağlantı noktasında (DTLS sunucu örneğinde depolanır) birden çok gelen istemci isteğini yönetmesi gerektiğinden, DTLS sunucusu işlevinin DTLS Istemcisi ve TLS Istemcisi/sunucusundan oldukça farklı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-135">Note that the DTLS Server functionality is quite different from DTLS Client and TLS Client/Server since the DTLS Server needs to manage multiple incoming client requests on a single UDP port (stored in the DTLS Server instance).</span></span>

```C
#include "tx_api.h"
#include "nx_api.h"
#include "nx_secure_dtls_api.h"

#define     DEMO_STACK_SIZE         4096

/* Define the ThreadX and NetX object control blocks.
   NOTE: These must be initialized for the target platform. See the
   NetX documentation for details. */

NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;

/* Define the IP thread's stack area.  */
ULONG ip_thread_stack[3 * 1024 / sizeof(ULONG)];

/* Define packet pool for the demonstration.  */
#define NX_PACKET_POOL_SIZE ((1536 + sizeof(NX_PACKET)) * 32)

ULONG packet_pool_area[NX_PACKET_POOL_SIZE/sizeof(ULONG) + 64 / sizeof(ULONG)];

/* Define the ARP cache area.  */
ULONG arp_space_area[512 / sizeof(ULONG)];


/* Define the DTLS Server thread.  */
ULONG             dtls_server_thread_stack[6 * 1024 / sizeof(ULONG)];
TX_THREAD         dtls_server_thread;
void              server_thread_entry(ULONG thread_input);

/* Define the DTLS packet reassembly buffer. */
UCHAR packet_buffer[4000];

/* Define the metadata area for TLS/DTLS cryptography. The actual size needed can be
   Ascertained by calling nx_secure_tls_metadata_size_calculate.
*/
UCHAR crypto_metadata_buffer[4000];

/* Pointer to the TLS ciphersuite table that is included in the platform-specific
   cryptography subdirectory. The table maps the cryptographic routines for the
   platform to function pointers usable by the TLS library. The TLS structure is also
   used for DTLS. See the NetX Secure TLS User Guide for more information.
*/
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Define our server certificate structure. */
NX_SECURE_X509_CERTIFICATE certificate;

/* DER-encoded certificate data for the server identity X.509 certificate. */
UCHAR device_cert_der[] = { … };
UCHAR device_cert_der_length[] = { … };
UCHAR device_cert_key_der[] = { … };
UCHAR device_cert_key_der_length[] = { … };

/* Define the number of sessions we want to allocate to our DTLS Server. */
#define DTLS_SERVER_SESSIONS (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION) * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive. NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Define the application – initialize drivers and UDP setup.  */
void    tx_application_define(void *first_unused_memory)
{
    UINT  status;

    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* Create a packet pool. Check status for errors. */
    status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1536,
   (ULONG*)(((int)packet_pool_area + 64) & ~63) ,
   NX_PACKET_POOL_SIZE);

    /* Create an IP instance for the specific target. Check status for errors. */
    status = nx_ip_create(&ip_0, …);

    /* Enable ARP and supply ARP cache memory for IP Instance 0. Check status for
         errors. */
    status =  nx_arp_enable(&ip_0, (void *)arp_space_area, sizeof(arp_space_area));

    /* Enable UDP traffic. Check status for errors. */
    status =  nx_udp_enable(&ip_0);

    status =  nx_ip_fragment_enable(&ip_0);

    /* Initialize the NetX Secure TLS/DTLS system.  */
    nx_secure_tls_initialize();

     /* Create the server thread to start handling incoming requests. */
    tx_thread_create(&dtls_server_thread, "DTLS Server thread", server_thread_entry,
       0, dtls_server_thread_stack, sizeof(dtls_server_thread_stack),
       16, 16, 4, TX_AUTO_START);
}


/* Primary application thread for handling DTLS server operations. */
void server_thread_entry(ULONG thread_input)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UCHAR receive_buffer[100];
    ULONG bytes;
    UINT status;

    NX_PARAMETER_NOT_USED(thread_input);

    /* Ensure the IP instance has been initialized.  */
    status =  nx_ip_status_check(&ip_0, NX_IP_INITIALIZE_DONE, &actual_status,
        NX_IP_PERIODIC_RATE);

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance, LOCAL_SERVER_PORT,
        NX_IP_PERIODIC_RATE, dtls_server_session_buffer,
        sizeof(dtls_server_session_buffer),
        &tls_crypto_table, crypto_metadata_buffer,
        sizeof(crypto_metadata_buffer), packet_buffer,
        sizeof(packet_buffer),
        dtls_server_connect_notify,
        dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                        device_cert_der_len, NX_NULL, 0,
                        device_cert_key_der, device_cert_key_der_len,
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server, &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            status = nx_secure_dtls_session_receive(receive_dtls_session, &receive_packet,
            NX_IP_PERIODIC_RATE);


            /* Process received data… */
            status = nx_packet_data_extract_offset(receive_packet, 0, receive_buffer, 100,
                 &bytes);
            /* Display the Client request data. */
           receive_buffer[bytes] = 0;
           printf("Received data: %s\n", receive_buffer);


            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                &send_packet, NX_IP_PERIODIC_RATE);


           /* Populate the packet with our response data. */
           nx_packet_data_append(send_packet, response_data, response_data_length,
                &pool_0, NX_WAIT_FOREVER);

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done, stop the server instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}
```

<span data-ttu-id="4b6f6-136">**Şekil 1,2 NetX güvenli DTLS Server örneği**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-136">**Figure 1.2 Example of NetX Secure DTLS Server**</span></span>

## <a name="configuration-options"></a><span data-ttu-id="4b6f6-137">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="4b6f6-137">Configuration Options</span></span>

<span data-ttu-id="4b6f6-138">NetX güvenli oluşturmak için birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-138">There are several configuration options for building NetX Secure.</span></span>
<span data-ttu-id="4b6f6-139">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4b6f6-139">Following is a list of all options, where each is described in detail:</span></span>

| <span data-ttu-id="4b6f6-140">Tanımlayın</span><span class="sxs-lookup"><span data-stu-id="4b6f6-140">Define</span></span>                                                 | <span data-ttu-id="4b6f6-141">Anlamı</span><span class="sxs-lookup"><span data-stu-id="4b6f6-141">Meaning</span></span>                                                                                                                                                                                                                |
|--------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4b6f6-142">**NX_SECURE_ENABLE_DTLS**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-142">**NX_SECURE_ENABLE_DTLS**</span></span>                           | <span data-ttu-id="4b6f6-143">NetX güvenli içinde DTLS mantığını etkinleştirmek için bu makronun tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-143">This macro must be defined to enable DTLS logic in NetX Secure.</span></span>                                                                                                                                                       |
| <span data-ttu-id="4b6f6-144">**NX_SECURE_DISABLE_ERROR_CHECKING**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-144">**NX_SECURE_DISABLE_ERROR_CHECKING**</span></span>               | <span data-ttu-id="4b6f6-145">Tanımlı, bu seçenek temel NetX güvenli hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-145">Defined, this option removes the basic NetX Secure error checking.</span></span> <span data-ttu-id="4b6f6-146">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-146">It is typically used after the application has been debugged.</span></span>                                                                                     |
| <span data-ttu-id="4b6f6-147">**NX_SECURE_TLS_CLIENT_DISABLED**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-147">**NX_SECURE_TLS_CLIENT_DISABLED**</span></span>                  | <span data-ttu-id="4b6f6-148">Tanımlı, bu seçenek, Istemci moduyla ilgili tüm TLS/DTLS yığın kodunu kaldırır, kod ve veri kullanımını azaltır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-148">Defined, this option removes all TLS/DTLS stack code related to Client mode, reducing code and data usage.</span></span>                                                                                                            |
| <span data-ttu-id="4b6f6-149">**NX_SECURE_TLS_SERVER_DISABLED**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-149">**NX_SECURE_TLS_SERVER_DISABLED**</span></span>                  | <span data-ttu-id="4b6f6-150">Tanımlı, bu seçenek, sunucu moduyla ilgili tüm TLS/DTLS yığın kodunu kaldırır, kod ve veri kullanımını azaltır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-150">Defined, this option removes all TLS/DTLS stack code related to Server mode, reducing code and data usage.</span></span>                                                                                                            |
| <span data-ttu-id="4b6f6-151">**NX_SECURE_ENABLE_PSK_CIPHERSUITES**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-151">**NX_SECURE_ENABLE_PSK_CIPHERSUITES**</span></span>              | <span data-ttu-id="4b6f6-152">Tanımlı, bu seçenek önceden paylaşılan anahtar (PSK) işlevselliği sunar.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-152">Defined, this option enables Pre-Shared Key (PSK) functionality.</span></span> <span data-ttu-id="4b6f6-153">Dijital sertifikaları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-153">It does not disable digital certificates.</span></span>                                                                                                        |
| <span data-ttu-id="4b6f6-154">**NX_SECURE_X509_STRICT_NAME_COMPARE**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-154">**NX_SECURE_X509_STRICT_NAME_COMPARE**</span></span>            | <span data-ttu-id="4b6f6-155">Bu seçenek, sertifika arama ve doğrulama için X. 509.440 sertifikaları için katı ayırt edici ad karşılaştırmayı mümkün bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-155">Defined, this option enables strict distinguished name comparison for X.509 certificates for certificate searching and verification.</span></span> <span data-ttu-id="4b6f6-156">Varsayılan değer yalnızca ortak ad alanlarını ayırt edici adlara göre karşılaştırmaktır.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-156">The default is to only compare the Common Name fields the Distinguished Names.</span></span> |
| <span data-ttu-id="4b6f6-157">**NX_SECURE_X509_USE_EXTENDED_DISTINGUISHED_NAMES**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-157">**NX_SECURE_X509_USE_EXTENDED_DISTINGUISHED_NAMES**</span></span>     | <span data-ttu-id="4b6f6-158">Bu seçenek, X. 509.440 sertifikaları için ek bellek kullanımı masrafındaki isteğe bağlı X. 509.952 ayırt edici ad alanlarını mümkün bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-158">Defined, this option enables the optional X.509 Distinguished Name fields, at the expense of extra memory use for X.509 certificates.</span></span>                                                                               |
| <span data-ttu-id="4b6f6-159">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**</span><span class="sxs-lookup"><span data-stu-id="4b6f6-159">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**</span></span>                | <span data-ttu-id="4b6f6-160">Tanımlı, bu seçenek bit cinsinden beklenen maksimum RSA mod sayısını verir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-160">Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="4b6f6-161">Varsayılan değer 4096 bit mod için 4096 ' dir \- .</span><span class="sxs-lookup"><span data-stu-id="4b6f6-161">The default value is 4096 for a 4096\-bit modulus.</span></span> <span data-ttu-id="4b6f6-162">Diğer değerler 3072, 2048 veya 1024 (önerilmez) olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b6f6-162">Other values can be 3072, 2048, or 1024 (not recommended).</span></span>                               |
