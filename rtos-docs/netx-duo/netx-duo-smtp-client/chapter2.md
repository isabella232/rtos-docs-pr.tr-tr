---
title: Bölüm 2-NetX Duo SMTP istemcisinin yüklenmesi ve kullanımı
description: Bu bölümde, NetX Duo SMTP Istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 86f324935ba32aab010b81f825be0a6564983a2e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825786"
---
# <a name="chapter-2---installation-and-use-of-netx-duo-smtp-client"></a><span data-ttu-id="d11e4-103">Bölüm 2-NetX Duo SMTP istemcisinin yüklenmesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="d11e4-103">Chapter 2 - Installation and use of NetX Duo SMTP client</span></span>

<span data-ttu-id="d11e4-104">Bu bölümde, NetX Duo SMTP Istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-104">This chapter contains a description of various issues related to installation, setup, and usage of the NetX Duo SMTP Client component.</span></span>

## <a name="netx-duo-smtp-client-installation"></a><span data-ttu-id="d11e4-105">NetX Duo SMTP Istemcisi yüklemesi</span><span class="sxs-lookup"><span data-stu-id="d11e4-105">NetX Duo SMTP Client Installation</span></span>

<span data-ttu-id="d11e4-106">NetX Duo SMTP Istemcisi adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="d11e4-106">The NetX Duo SMTP Client is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="d11e4-107">Paket aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="d11e4-107">The package includes the following files:</span></span>

- <span data-ttu-id="d11e4-108">**nxd_smtp_client. c** NetX Duo SMTP Istemcisi API 'SI için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="d11e4-108">**nxd_smtp_client.c** C Source file for NetX Duo SMTP Client API</span></span>
- <span data-ttu-id="d11e4-109">**nxd_smtp_client. h** NetX Duo SMTP Istemcisi API 'SI için C üstbilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="d11e4-109">**nxd_smtp_client.h** C Header file for NetX Duo SMTP Client API</span></span>
- <span data-ttu-id="d11e4-110">**demo_netxduo_smtp_client. c** NetX Duo SMTP Istemcisi tanıtımı</span><span class="sxs-lookup"><span data-stu-id="d11e4-110">**demo_netxduo_smtp_client.c** Demo for NetX Duo SMTP Client</span></span>
- <span data-ttu-id="d11e4-111">**İçinnxd_smtp_client.pdf Kullanıcı Kılavuzu** NetX Duo SMTP Istemcisi API 'SI</span><span class="sxs-lookup"><span data-stu-id="d11e4-111">**nxd_smtp_client.pdf User Guide for** NetX Duo SMTP Client API</span></span>

<span data-ttu-id="d11e4-112">NetX Duo SMTP Istemcisi API 'sini kullanmak için, daha önce bahsedilen tüm dağıtım, NetX Duo yüklendiği dizine kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-112">To use the NetX Duo SMTP Client API, the entire distribution mentioned previously may be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="d11e4-113">Örneğin, "c:*\MyProject*" dizininde NETX Duo yüklüyse, *nxd_smtp_client. h ve nxd_smtp_client. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-113">For example, if NetX Duo is installed in the directory “c:*\myproject*” then the *nxd_smtp_client.h, and nxd_smtp_client.c* files should be copied into this directory.</span></span>

## <a name="using-netx-duo-smtp-client"></a><span data-ttu-id="d11e4-114">NetX Duo SMTP Istemcisini kullanma</span><span class="sxs-lookup"><span data-stu-id="d11e4-114">Using NetX Duo SMTP Client</span></span>

<span data-ttu-id="d11e4-115">NetX Duo SMTP Istemci uygulamasını oluşturmak için öncelikle ThreadX ve NetX Duo kitaplıklarını oluşturmalı ve bunları Build projesine dahil etmelidir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-115">To create the NetX Duo SMTP Client application, it must first build the ThreadX and NetX Duo libraries and include them in the build project.</span></span> <span data-ttu-id="d11e4-116">Uygulamanın, uygulama kaynak kodunda TX *_api. h* ve *nx_api. h*'yi içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-116">The application must then include tx *_api.h* and *nx_api.h in its application source code*.</span></span> <span data-ttu-id="d11e4-117">Bu, ThreadX ve NetX Duo hizmetlerini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-117">This will enable ThreadX and NetX Duo services.</span></span> <span data-ttu-id="d11e4-118">Ayrıca, *SMTP istemci hizmetlerini kullanmak için* *tx_api. h* ve nx_api. h sonrasında *nxd_smtp_client. c* ve *nxd_smtp_client. h* içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-118">It must also include *nxd_smtp_client.c* and *nxd_smtp_client.h* after *tx_api.h* and *nx_api.h to use SMTP Client services.*</span></span>

<span data-ttu-id="d11e4-119">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne kodu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-119">These files must be compiled in the same manner as other application files and the object code must be linked along with the files of the application.</span></span> <span data-ttu-id="d11e4-120">Bu, bir NetX Duo SMTP Istemci uygulaması oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-120">This is all that is required to create a NetX Duo SMTP Client application.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="d11e4-121">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="d11e4-121">Small Example System</span></span>

<span data-ttu-id="d11e4-122">NetX Duo SMTP Istemcisini kullanmanın bir örneği aşağıda gösterilen Şekil 1 ' de açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-122">An example of using the NetX Duo SMTP Client is described in Figure 1 that appears below.</span></span> <span data-ttu-id="d11e4-123">IP örneği için paket havuzu, 68 satırındaki nx_packet_pool_create hizmeti kullanılarak oluşturulur ve çok küçük bir paket yüküne sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-123">The packet pool for the IP instance is created using the nx_packet_pool_create service, on line 68 and has a very small packet payload.</span></span> <span data-ttu-id="d11e4-124">Bunun nedeni, IP örneğinin yalnızca fazla yük gerektirmeyen denetim paketlerini göndermesi içindir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-124">This is because the IP instance only sends control packets which don’t require much payload.</span></span> <span data-ttu-id="d11e4-125">84. satırda oluşturulan SMTP Istemcisi paket havuzu ve SMTP Istemci iletilerini sunucuya ve ileti verilerine iletmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-125">The SMTP Client packet pool created on line 84 and is used for transmitting SMTP Client messages to the server and message data.</span></span> <span data-ttu-id="d11e4-126">Paket yükü çok daha büyük.</span><span class="sxs-lookup"><span data-stu-id="d11e4-126">Its packet payload is much larger.</span></span> <span data-ttu-id="d11e4-127">IP örneği, aynı paket havuzunu kullanan 118. satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d11e4-127">The IP instance is created in line 118 using the same packet pool.</span></span> <span data-ttu-id="d11e4-128">SMTP protokolü için gereken TCP, 130. satırdaki IP örneğinde etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-128">TCP, required for the SMTP protocol, is enabled on the IP instance in line 130.</span></span>

<span data-ttu-id="d11e4-129">Uygulama iş parçacığında, SMTP Istemcisi *nxd_smtp_client_create* hizmeti kullanılarak oluşturulur, satır 170.</span><span class="sxs-lookup"><span data-stu-id="d11e4-129">In the application thread, the SMTP Client is created using the *nxd_smtp_client_create* service, in line 170.</span></span> <span data-ttu-id="d11e4-130">*Nxd_smtp_client_create* hizmeti IPv4 ve IPv6 SMTP sunucusu bağlantılarını destekler, ancak bu örnek IPv4 ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-130">The *nxd_smtp_client_create* service supports both IPv4 and IPv6 SMTP server connections although this example is limited to IPv4.</span></span> <span data-ttu-id="d11e4-131">Ardından posta iletisi, *nx_smtp_mail_send* hizmeti kullanılarak 184. satırda ıletım Için SMTP istemcisine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-131">Then the mail message is submitted to the SMTP Client for transmission on line 184 using the *nx_smtp_mail_send* service.</span></span> <span data-ttu-id="d11e4-132">Posta içeriği üst bilgisine sahip konu satırının ileti gövdesinden ayrı olarak oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d11e4-132">Note that the subject line with the mail content header is created separately from the message body.</span></span> <span data-ttu-id="d11e4-133">Ayrıca, e-posta isteği yalnızca, sözdizimsel olarak doğru olarak kabul edilen tek bir alıcı posta adresini kabul ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d11e4-133">Also note that the send mail request accepts only one recipient mail address which is assumed to be syntactically correct.</span></span>

<span data-ttu-id="d11e4-134">Ardından, uygulama SMTP Istemcisini 200. satırda sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-134">Then the application terminates the SMTP Client on line 200.</span></span> <span data-ttu-id="d11e4-135">*Nx_smtp_client_delete* hizmeti yuva bağlantısının kapalı olduğunu ve bağlantı noktasının ilişkisiz olduğunu denetler.</span><span class="sxs-lookup"><span data-stu-id="d11e4-135">The *nx_smtp_client_delete* service checks that the socket connection is closed and the port is unbound.</span></span> <span data-ttu-id="d11e4-136">Bu, daha önce kullanımda değilse, paket havuzunu silmek için SMTP Istemci uygulamasına kadar olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d11e4-136">Note that it is up to the SMTP Client application to delete the packet pool if it no longer has use for it.</span></span>

```c
/*
   demo_netxduo_smtp_client.c

   This is a small demo of the NetX Duo SMTP Client on the high-performance NetX
   Duo TCP/IP stack.  This demo relies on Thread, NetX Duo and SMTP Client API to
   perform simple SMTP mail transfers in an SMTP client application to an SMTP mail
   server.   */

#include "nx_api.h"
#include "nx_ip.h"
#include "nxd_smtp_client.h"


/* Define the host user name and mail box parameters */
#define USERNAME               "myusername"
#define PASSWORD               "mypassword"
#define FROM_ADDRESS           "my@mycompany.com"
#define RECIPIENT_ADDRESS      "your@yourcompany.com"
#define LOCAL_DOMAIN           "mycompany.com"

#define SUBJECT_LINE           "NetX Duo SMTP Client Demo"
#define MAIL_BODY              "NetX Duo SMTP client is an SMTP client \r\n" \
                               “implementation for embedded devices to send  \r\n" \
                               "email to SMTP servers. This feature is \r\n" \
                               "intended to allow a device to send simple \r\n " \
                               "status reports using the most universal \r\n " \
                               “Internet application, email.\r\n"

/* See the NetX Duo SMTP Client User Guide for how to set the authentication type.
   The most common authentication type is PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE 3


#define CLIENT_IP_ADDRESS  IP_ADDRESS(1,2,3,5)
#define SERVER_IP_ADDRESS  IP_ADDRESS(1,2,3,4)
#define SERVER_PORT        25


/* Define the NetX Duo and ThreadX structures for the SMTP client appliciation. */
NX_PACKET_POOL                  ip_packet_pool;
NX_PACKET_POOL                  client_packet_pool;
NX_IP                           client_ip;
TX_THREAD                       demo_client_thread;
static NX_SMTP_CLIENT           demo_client;


void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
void    demo_client_thread_entry(ULONG info);

/* Define main entry point.  */
int main()
{
    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

    UINT    status;
    CHAR    *free_memory_pointer;


    /* Setup the pointer to unallocated memory.  */
    free_memory_pointer =  (CHAR *) first_unused_memory;

    /* Create IP default packet pool. */
    status =  nx_packet_pool_create(&ip_packet_pool, "Default IP Packet Pool",
                                    128, free_memory_pointer, 2048);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* Create SMTP Client packet pool. This is only for transmitting packets to the
       server. It need not be a separate packet pool than the IP default packet pool
       but for more efficient resource use, we use two different packet pools
       because the CLient SMTP messages generally require more payload than IP
       control packets.

       Packet payload depends on the SMTP Client application requirements.  Size of
       packet payload must include IP and TCP headers. For IPv6 connections, IP and
       TCP header data is 60 bytes. For IPv4 IP and TCP header data is 40 bytes (not
       including TCP options). */
    status |=  nx_packet_pool_create(&client_packet_pool, "SMTP Client Packet Pool",
                                     800, free_memory_pointer, (10*800));

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + (10*800);

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the client thread */
    status = tx_thread_create(&demo_client_thread, "client_thread",
                              demo_client_thread_entry, 0, free_memory_pointer,
                              2048, 16, 16,
                              TX_NO_TIME_SLICE, TX_DONT_START);

    if (status != NX_SUCCESS)
    {

        printf("Error creating Client thread. Status 0x%x\r\n", status);
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer =  free_memory_pointer + 4096;


    /* Create Client IP instance. Remember to replace the generic driver
       with a real ethernet driver to actually run this demo! */

    status = nx_ip_create(&client_ip, "SMTP Client IP Instance", CLIENT_IP_ADDRESS,
                          0xFFFFFF00UL, &ip_packet_pool, _nx_ram_network_driver,
                          free_memory_pointer, 2048, 1);


    free_memory_pointer =  free_memory_pointer + 2048;

    /* Enable ARP and supply ARP cache memory. */
    status =  nx_arp_enable(&client_ip, (void **) free_memory_pointer, 1040);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 1040;

    /* Enable TCP for client. */
    status =  nx_tcp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable ICMP for client. */
    status =  nx_icmp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Start the client thread. */
    tx_thread_resume(&demo_client_thread);

    return;
}


/* Define the smtp application thread task.   */
void    demo_client_thread_entry(ULONG info)
{

    UINT        status;
    UINT        error_counter = 0;
    NXD_ADDRESS server_ip_address;


    tx_thread_sleep(100);

    /* Set up the server IP address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;

    /* The demo client username and password is the authentication
       data used when the server attempts to authentication the client. */

    status =  nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
                                     USERNAME,
                                     PASSWORD,
                                     FROM_ADDRESS,
                                     LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
                                     &server_ip_address, SERVER_PORT);

    if (status != NX_SUCCESS)
    {
        printf("Error creating the client. Status: 0x%x.\n\r", status);
        return;
    }

    /* Create a mail instance with the above text message and recipient info. */
    status =  nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
                                TP_MAIL_PRIORITY_NORMAL,
                                SUBJECT_LINE, MAIL_BODY, sizeof(MAIL_BODY) - 1);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        /* Mail item was not sent. Note that we need not delete the client. The
           error status may be a failed authentication check or a broken connection.
           We can simply call nx_smtp_mail_send again.  */
        error_counter++;
    }

    /* Release resources used by client. Note that the transmit packet
       pool must be deleted by the application if it no longer has use for it.*/
    status = nx_smtp_client_delete(&demo_client);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    return;
}
```

<span data-ttu-id="d11e4-137">**Şekil 1. NetX Duo ile SMTP Istemcisi kullanımı örneği**</span><span class="sxs-lookup"><span data-stu-id="d11e4-137">**Figure 1. Example of SMTP Client use with NetX Duo**</span></span>

## <a name="client-configuration-options"></a><span data-ttu-id="d11e4-138">İstemci yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="d11e4-138">Client Configuration Options</span></span>

<span data-ttu-id="d11e4-139">NetX Duo SMTP Istemcisi API 'SI ile birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-139">There are several configuration options with the NetX Duo SMTP Client API.</span></span> <span data-ttu-id="d11e4-140">Aşağıda, ayrıntılı olarak açıklanan tüm seçeneklerin bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d11e4-140">Following is a list of all options described in detail:</span></span>

- <span data-ttu-id="d11e4-141">**NX_SMTP_CLIENT_TCP_WINDOW_SIZE** Bu seçenek, Istemci TCP alma penceresinin boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-141">**NX_SMTP_CLIENT_TCP_WINDOW_SIZE** This option sets the size of the Client TCP receive window.</span></span> <span data-ttu-id="d11e4-142">Bu, temel alınan Ethernet donanımının MTU boyutunun altına ayarlanmalıdır ve IP ve TCP üstbilgileri için odaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-142">This should be set to below the MTU size of the underlying Ethernet hardware and allow room for IP and TCP headers.</span></span> <span data-ttu-id="d11e4-143">Varsayılan NetX Duo SMTP Istemcisi TCP pencere boyutu 1460 ' dir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-143">The default NetX Duo SMTP Client TCP window size is 1460.</span></span>
- <span data-ttu-id="d11e4-144">**NX_SMTP_CLIENT_PACKET_TIMEOUT** Bu seçenek, NetX paket ayırması sırasında zaman aşımını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-144">**NX_SMTP_CLIENT_PACKET_TIMEOUT** This option sets the timeout on NetX packet allocation.</span></span> <span data-ttu-id="d11e4-145">Varsayılan NetX Duo SMTP Istemcisi paket zaman aşımı 2 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-145">The default NetX Duo SMTP Client packet timeout is 2 seconds.</span></span>
- <span data-ttu-id="d11e4-146">**NX_SMTP_CLIENT_CONNECTION_TIMEOUT** Bu seçenek Istemci TCP yuvası bağlantı zaman aşımını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-146">**NX_SMTP_CLIENT_CONNECTION_TIMEOUT** This option sets the Client TCP socket connect timeout.</span></span> <span data-ttu-id="d11e4-147">Varsayılan NetX Duo SMTP Istemcisi bağlantı zaman aşımı 10 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-147">The default NetX Duo SMTP Client connect timeout is 10 seconds.</span></span>
- <span data-ttu-id="d11e4-148">**NX_SMTP_CLIENT_DISCONNECT_TIMEOUT** Bu seçenek, Istemci TCP yuvası bağlantı kesme zaman aşımını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-148">**NX_SMTP_CLIENT_DISCONNECT_TIMEOUT** This option sets the Client TCP socket disconnect timeout.</span></span> <span data-ttu-id="d11e4-149">Varsayılan NetX Duo SMTP Istemcisi bağlantı kesme zaman aşımı 5 saniyedir \*.</span><span class="sxs-lookup"><span data-stu-id="d11e4-149">The default NetX Duo SMTP Client disconnect timeout is 5 seconds\*.</span></span> <span data-ttu-id="d11e4-150">SMTP Istemcisi bozuk bağlantı gibi bir iç hatayla karşılaşırsa, bağlantıyı sıfır bekleme zaman aşımıyla sonlandırabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d11e4-150">Note that if the SMTP Client encounters an internal error such as a broken connection it may terminate the connection with a zero wait timeout.</span></span>
- <span data-ttu-id="d11e4-151">**NX_SMTP_GREETING_TIMEOUT** Bu seçenek, Istemcinin, karşılamasına yönelik sunucu yanıtı alması için zaman aşımını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-151">**NX_SMTP_GREETING_TIMEOUT** This option sets the timeout for the Client to receive the Server reply to its greeting.</span></span> <span data-ttu-id="d11e4-152">Varsayılan NetX Duo SMTP Istemci değeri 10 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-152">The default NetX Duo SMTP Client value is 10 seconds.</span></span>
- <span data-ttu-id="d11e4-153">**NX_SMTP_ENVELOPE_TIMEOUT** Bu seçenek, Istemci için sunucu yanıtı almak üzere Istemcinin zaman aşımını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-153">**NX_SMTP_ENVELOPE_TIMEOUT** This option sets the timeout for the Client to receive the Server reply to a Client command.</span></span> <span data-ttu-id="d11e4-154">Varsayılan NetX Duo SMTP Istemci değeri 10 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-154">The default NetX Duo SMTP Client value is 10 seconds.</span></span>
- <span data-ttu-id="d11e4-155">**NX_SMTP_MESSAGE_TIMEOUT** Bu seçenek, e-posta iletisi verilerini almak üzere Istemcinin sunucu yanıtı alması için zaman aşımını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-155">**NX_SMTP_MESSAGE_TIMEOUT** This option sets the timeout for the Client to receive the Server reply to receiving the mail message data.</span></span> <span data-ttu-id="d11e4-156">Varsayılan NetX Duo SMTP Istemcisi değeri 30 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-156">The default NetX Duo SMTP Client value is 30 seconds.</span></span>
- <span data-ttu-id="d11e4-157">**NX_SMTP_CLIENT_SEND_TIMEOUT** Bu seçenek, SMTP kimlik doğrulaması sırasında sunucu ile Kullanıcı parolasını depolamak için arabellek bekleme seçeneğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-157">**NX_SMTP_CLIENT_SEND_TIMEOUT** This option defines the wait option of the buffer to store the user password during SMTP authentication with the Server.</span></span> <span data-ttu-id="d11e4-158">Varsayılan değer 20 bayttır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-158">The default value is 20 bytes.</span></span>
- <span data-ttu-id="d11e4-159">**NX_SMTP_SERVER_CHALLENGE_MAX_STRING** Bu seçenek, SMTP kimlik doğrulaması sırasında sunucu sınamasını ayıklama için arabellek boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-159">**NX_SMTP_SERVER_CHALLENGE_MAX_STRING** This option defines the size of the buffer for extracting the Server challenge during SMTP authentication.</span></span> <span data-ttu-id="d11e4-160">Varsayılan değer 200 bayttır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-160">The default value is 200 bytes.</span></span> <span data-ttu-id="d11e4-161">OTURUM açma ve düz kimlik doğrulama için, SMTP Istemcisi muhtemelen daha küçük bir arabellek kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d11e4-161">For LOGIN and PLAIN authentication, the SMTP Client can probably use a smaller buffer.</span></span>
- <span data-ttu-id="d11e4-162">**NX_SMTP_CLIENT_MAX_PASSWORD** Bu seçenek, SMTP kimlik doğrulaması sırasında sunucu ile Kullanıcı parolasını depolamak için arabelleğin boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-162">**NX_SMTP_CLIENT_MAX_PASSWORD** This option defines the size of the buffer to store the user password during SMTP authentication with the Server.</span></span> <span data-ttu-id="d11e4-163">Varsayılan değer 20 bayttır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-163">The default value is 20 bytes.</span></span> 
- <span data-ttu-id="d11e4-164">**NX_SMTP_CLIENT_MAX_USERNAME** Bu seçenek, sunucu ile SMTP kimlik doğrulaması sırasında konak Kullanıcı adını depolamak için arabelleğin boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d11e4-164">**NX_SMTP_CLIENT_MAX_USERNAME** This option defines the size of the buffer to store the host username during SMTP authentication with the Server.</span></span> <span data-ttu-id="d11e4-165">Varsayılan değer 40 bayttır.</span><span class="sxs-lookup"><span data-stu-id="d11e4-165">The default value is 40 bytes.</span></span> 
