---
title: Bölüm 2-Azure RTOS NetX Duo Telnet yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX Duo Telnet bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d5b24690db6ccbc582387dd9dba5b0471e6f278d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825726"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-telnet"></a><span data-ttu-id="55a3a-103">Bölüm 2-Azure RTOS NetX Duo Telnet yüklemesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="55a3a-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo Telnet</span></span>

<span data-ttu-id="55a3a-104">Bu bölümde, Azure RTOS NetX Duo Telnet bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo Telnet component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="55a3a-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="55a3a-105">Product Distribution</span></span>

<span data-ttu-id="55a3a-106">Azure RTOS NetX Duo Telnet paketini adresinden bulabilirsiniz <https://github.com/azure-rtos/netxduo> .</span><span class="sxs-lookup"><span data-stu-id="55a3a-106">The Azure RTOS NetX Duo Telnet package is available at <https://github.com/azure-rtos/netxduo>.</span></span> <span data-ttu-id="55a3a-107">Paket aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="55a3a-107">The package includes the following files:</span></span>

- <span data-ttu-id="55a3a-108">**nxd_telnet_client. h**: NETX Duo Için Telnet istemcisi üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="55a3a-108">**nxd_telnet_client.h**: Header file for Telnet Client for NetX Duo</span></span>
- <span data-ttu-id="55a3a-109">**nxd_telnet_client. c**: NETX Duo Için Telnet istemcisi Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="55a3a-109">**nxd_telnet_client.c**: C Source file for Telnet Client for NetX Duo</span></span>
- <span data-ttu-id="55a3a-110">**nxd_telnet_server. h**: NETX Duo Için Telnet sunucusu üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="55a3a-110">**nxd_telnet_server.h**: Header file for Telnet Server for NetX Duo</span></span>
- <span data-ttu-id="55a3a-111">**nxd_telnet_server. c**: NETX Duo Için Telnet sunucusu Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="55a3a-111">**nxd_telnet_server.c**: C Source file for Telnet Server for NetX Duo</span></span>
- <span data-ttu-id="55a3a-112">**nxd_telnet.pdf**: NETX Duo için Telnet 'in PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="55a3a-112">**nxd_telnet.pdf**: PDF description of Telnet for NetX Duo</span></span>
- <span data-ttu-id="55a3a-113">**demo_netxduo_telnet. c**: NETX Duo Telnet tanıtımı</span><span class="sxs-lookup"><span data-stu-id="55a3a-113">**demo_netxduo_telnet.c**: NetX Duo Telnet demonstration</span></span>

## <a name="telnet-installation"></a><span data-ttu-id="55a3a-114">Telnet yüklemesi</span><span class="sxs-lookup"><span data-stu-id="55a3a-114">Telnet Installation</span></span>

<span data-ttu-id="55a3a-115">NetX Duo için Telnet kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-115">In order to use Telnet for NetX Duo, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="55a3a-116">Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_telnet_client. h*, *nxd_telnet_client. c*, *nxd_telnet_server. c ve nxd_telnet_server. h* dosyalarının bu dizine kopyalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-116">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nxd_telnet_client.h*, *nxd_telnet_client.c*, *nxd_telnet_server.c and nxd_telnet_server.h* files should be copied into this directory.</span></span>

## <a name="using-telnet"></a><span data-ttu-id="55a3a-117">Telnet kullanma</span><span class="sxs-lookup"><span data-stu-id="55a3a-117">Using Telnet</span></span>

<span data-ttu-id="55a3a-118">NetX Duo için Telnet kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-118">Using Telnet for NetX Duo is easy.</span></span> <span data-ttu-id="55a3a-119">Temel olarak, uygulama kodu için nxd_telnet_server. h ve, ThreadX ve NetX Duo kullanmak için *tx_api. h* ve *nx_api. h* dahil olmak üzere, telnet istemci uygulamalarına yönelik *.* h ve *nxd_telnet_client.* h içermelidir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-119">Basically, the application code must include *nxd_telnet_server.h* for Telnet Server applications and *nxd_telnet_client.h* for Telnet Client applications after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX Duo.</span></span> <span data-ttu-id="55a3a-120">*Üstbilgi* eklendikten sonra, uygulama kodu bu kılavuzda daha sonra belirtilen Telnet işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-120">Once *the header* is included, the application code is then able to make the Telnet function calls specified later in this guide.</span></span> <span data-ttu-id="55a3a-121">Uygulama ayrıca yapı işlemine *nxd_telnet_client. c* ve *nxd_telnet_server. c* içermelidir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-121">The application must also include *nxd_telnet_client.c* and *nxd_telnet_server.c* in the build process.</span></span> <span data-ttu-id="55a3a-122">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-122">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="55a3a-123">Bu, NetX Duo Telnet 'i kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-123">This is all that is required to use NetX Duo Telnet.</span></span>

<span data-ttu-id="55a3a-124">Hiçbir Telnet Istemci özelliği gerekmiyorsa, *nxd_telnet_client. c* dosyası atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-124">If no Telnet Client capabilities are required, the *nxd_telnet_client.c* file may be omitted.</span></span>

<span data-ttu-id="55a3a-125">Telnet 'in NetX Duo TCP hizmetlerini kullandığından, Telnet kullanılmadan önce *nx_tcp_enable* çağrısıyla TCP 'nin etkinleştirilmesi gerektiğini de unutmayın.</span><span class="sxs-lookup"><span data-stu-id="55a3a-125">Note also that because Telnet utilizes NetX Duo TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using Telnet.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="55a3a-126">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="55a3a-126">Small Example System</span></span>

<span data-ttu-id="55a3a-127">NetX Duo Telnet 'in nasıl kullanılacağına ilişkin bir örnek aşağıda şekil 1,1 ' de gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-127">An example of how to use NetX Duo Telnet is shown in Figure 1.1 below.</span></span> <span data-ttu-id="55a3a-128">Bu örnekte, Telnet içerme dosyaları, 7. ve 8. *satırda getirilir.*</span><span class="sxs-lookup"><span data-stu-id="55a3a-128">In this example, the Telnet include files *are* brought in at line 7 and 8.</span></span> <span data-ttu-id="55a3a-129">Ardından, Telnet sunucusu 146 satırındaki "*tx_application_define*" içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="55a3a-129">Next, the Telnet Server is created in “*tx_application_define*” at line 146.</span></span> <span data-ttu-id="55a3a-130">Telnet sunucusunun ve Istemci denetim bloklarının daha önce satır 23-24 ' de genel değişkenler olarak tanımlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="55a3a-130">Note that the Telnet Server and Client control blocks are defined as global variables at line 23-24 previously.</span></span>

<span data-ttu-id="55a3a-131">Telnet sunucusu veya Istemcisinin başlatılması için önce, IP adreslerini NetX Duo ile doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-131">Before the Telnet Server or Client can be started they must validate their IP address with NetX Duo.</span></span> <span data-ttu-id="55a3a-132">IPv4 bağlantıları için bu, yalnızca NetX sürücüsünün 166. satırda sistemi başlatmasını sağlamak için kısa bir süre bekledikten sonra gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-132">For IPv4 connections this is accomplished by simply waiting briefly to let the NetX driver initialize the system on line 166.</span></span> <span data-ttu-id="55a3a-133">IPv6 bağlantıları için, bu, 171-172. satırlarda yaptığı IPv6 ve ICMPv6 'nın etkinleştirilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-133">For IPv6 connections, this requires enabling IPv6 and ICMPv6 which it does in lines 171-172.</span></span> <span data-ttu-id="55a3a-134">Istemci, birincil arabirimdeki genel ve bağlantı yerel IPv6 adreslerini, 181-186 satırları üzerinde ayarlar ve NetX Duo doğrulamasının arka planda tamamlanmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="55a3a-134">The Client sets its global and link local IPv6 addresses on the primary interface on lines 181-186 and waits for NetX Duo validation to complete in the background.</span></span> <span data-ttu-id="55a3a-135">Sunucu, birincil arabirimindeki genel ve bağlantı yerel adreslerini 192 – 198 satırlarında de ayarlar.</span><span class="sxs-lookup"><span data-stu-id="55a3a-135">The Server also sets its global and link local addresses on its primary interface in lines 192 – 198.</span></span> <span data-ttu-id="55a3a-136">*Nxd_ipv6_global_address_set* ve *nxd_ipv6_linklocal_address_set* iki hizmetin *nxd_ipv6_address_set hizmeti* ile değiştirildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="55a3a-136">Note that the two services, *nxd_ipv6_global_address_set* and *nxd_ipv6_linklocal_address_set* are replaced with *nxd_ipv6_address_set service*.</span></span> <span data-ttu-id="55a3a-137">Eski iki hizmet, eski NetX Duo uygulamaları için hala kullanılabilir ancak sonunda kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-137">The former two services are still available for legacy NetX Duo applications but are eventually deprecated.</span></span> <span data-ttu-id="55a3a-138">Geliştiricilerin bunun yerine *nxd_ipv6_address_set* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-138">Developers are encouraged to use *nxd_ipv6_address_set* instead.</span></span>

<span data-ttu-id="55a3a-139">NetX Duo ile başarılı IP adresi doğrulamasından sonra, Telnet sunucusu, *nxd_telnet_server_start* hizmeti kullanılarak 215. satırda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-139">After successful IP address validation with NetX Duo, the Telnet Server is started at line 215 using the *nxd_telnet_server_start* service.</span></span> <span data-ttu-id="55a3a-140">226. satırda Telnet Istemcisi *nx_telnet_client_create* hizmeti kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="55a3a-140">At line 226 the Telnet Client is created using the *nx_telnet_client_create* service.</span></span> <span data-ttu-id="55a3a-141">Ardından, sırasıyla *nxd_telnet_client_connect* ve *Nx_telnet_client_connect* hizmetlerini kullanarak IPv4 uygulamaları ve ıpv6 uygulamaları için satır 238 242 ' de Telnet sunucusuyla bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="55a3a-141">It then connects with the Telnet Server on line 242 for IPv4 applications and line 238 for IPv6 applications using the *nxd_telnet_client_connect* and *nx_telnet_client_connect* services respectively.</span></span> <span data-ttu-id="55a3a-142">Sunucuyla başarılı bir şekilde doğrulama ve bağlantı kurulduktan sonra, bağlantısını kesmeden önce birkaç değişim yapar.</span><span class="sxs-lookup"><span data-stu-id="55a3a-142">After successful validation and connection with the server, it makes a few exchanges before disconnecting.</span></span>

```c
/* This is a small demo of TELNET on the high-performance NetX Duo TCP/IP stack.  
       This demo relies on ThreadX and NetX Duo to show a simple TELNET connection,
       send, server echo, and then disconnection from the TELNET server.  */
    
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nxd_telnet_client.h"
#include  "nxd_telnet_server.h"
#define     DEMO_STACK_SIZE         4096    
   
/* Define the ThreadX and NetX object control blocks...  */
TX_THREAD               test_thread;
NX_PACKET_POOL          pool_server;
NX_PACKET_POOL          pool_client;
NX_IP                   ip_server;
NX_IP                   ip_client;
   
/* Define TELNET objects.  */

NX_TELNET_SERVER        my_server;
NX_TELNET_CLIENT        my_client;


#ifdef FEATURE_NX_IPV6

/* Define NetX Duo IP address for the NetX Duo Telnet Server and Client. */

NXD_ADDRESS     server_ip_address;
NXD_ADDRESS     client_ip_address;

#endif

#define         SERVER_ADDRESS          IP_ADDRESS(1,2,3,4)
#define         CLIENT_ADDRESS          IP_ADDRESS(1,2,3,5)

/* Define the counters used in the demo application...  */
ULONG                   error_counter;

/* Define timeout in ticks for connecting and sending/receiving data. */

#define                 TELNET_TIMEOUT  200

/* Define function prototypes.  */

void    thread_test_entry(ULONG thread_input);
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);


/* Define the application's TELNET Server callback routines.  */

void    telnet_new_connection(NX_TELNET_SERVER *server_ptr, UINT 
                              logical_connection); 
void    telnet_receive_data(NX_TELNET_SERVER *server_ptr, UINT logical_connection, 
                            NX_PACKET *packet_ptr);
void    telnet_connection_end(NX_TELNET_SERVER *server_ptr, UINT 
                              logical_connection);

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
CHAR    *pointer;
UINT    iface_index, address_index;
    
    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;
    
    /* Create the main thread.  */
    tx_thread_create(&test_thread, "test thread", thread_test_entry, 0,  
                     pointer, DEMO_STACK_SIZE, 
                     2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;
    
    /* Initialize the NetX system.  */
    nx_system_initialize();
    
    /* Create packet pool.  */
    nx_packet_pool_create(&pool_server, "Server NetX Packet Pool", 600, pointer, 8192);
    pointer = pointer + 8192;
    
    /* Create an IP instance.  */
    nx_ip_create(&ip_server, "Server NetX IP Instance", SERVER_ADDRESS, 
                 0xFFFFFF00UL, &pool_server, _nx_ram_network_driver,
                 pointer, 4096, 1);
    
    pointer =  pointer + 4096;
    
    /* Create another packet pool. */
    nx_packet_pool_create(&pool_client, "Client NetX Packet Pool", 600, 
                          pointer, 8192);
    pointer = pointer + 8192;
    
    /* Create another IP instance.  */
    nx_ip_create(&ip_client, "Client NetX IP Instance", CLIENT_ADDRESS, 
                 0xFFFFFF00UL, &pool_client, _nx_ram_network_driver, 
                 pointer, 4096, 1);
    
    pointer = pointer + 4096;
    
    /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
    nx_arp_enable(&ip_server, (void *) pointer, 1024);
    pointer = pointer + 1024;
    
    /* Enable ARP and supply ARP cache memory for IP Instance 1.  */
    nx_arp_enable(&ip_client, (void *) pointer, 1024);
    pointer = pointer + 1024;
    
    /* Enable TCP processing for both IP instances.  */
    nx_tcp_enable(&ip_server);
    nx_tcp_enable(&ip_client);

#ifdef FEATURE_NX_IPV6

    /* Next set the NetX Duo Telnet Server and Client addresses. */
    server_ip_address.nxd_ip_address.v6[3] = 0x105;
    server_ip_address.nxd_ip_address.v6[2] = 0x0;
    server_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db1;
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

    client_ip_address.nxd_ip_address.v6[3] = 0x101;
    client_ip_address.nxd_ip_address.v6[2] = 0x0;
    client_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    client_ip_address.nxd_ip_address.v6[0] = 0x20010db1;
    client_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

#endif

    /* Create the NetX Duo TELNET Server.  */
    status =  nx_telnet_server_create(&my_server, "Telnet Server", &ip_server, 
                                      pointer, 2048, telnet_new_connection, telnet_receive_data, 
                                      telnet_connection_end);
    
    /* Check for errors.  */
    if (status)
        error_counter++;
    
    return;
}

/* Define the test thread.  */
void    thread_test_entry(ULONG thread_input)
{

NX_PACKET   *my_packet;
UINT        status;
    
    /* Allow other threads (e.g. IP thread task) to run first. */
    tx_thread_sleep(100);
    
    #ifdef FEATURE_NX_IPV6
    /* Here's where we make the Telnet Client IPv6 enabled. */
    nxd_ipv6_enable(&ip_client);
    nxd_icmp_enable(&ip_client);     
    
    /* Wait till the IP task thread initializes the system. */
    tx_thread_sleep(100);
        
    /* Set up the Client addresses on the Client IP for the primary interface. */
    if_index = 0;
    
    status = nxd_ipv6_address_set(&ip_ client, iface_index, NX_NULL, 10, 
                                  &address_index);
    status = nxd_ipv6_address_set(&ip_ client, iface_index, & client _ip_address, 
                                   64, &address_index);
        
    /* Allow NetX Duo time to validate addresses. */
    tx_thread_sleep(400);
    
    /* Set up the Server addresses on the Client IP. */
    iface_index = 0;
    status = nxd_ipv6_address_set (&ip_server, iface_index, NX_NULL, 10, 
                                   &address_index);
    
    status = nxd_ ipv6_address _set(&ip_server, iface_index, & server _ip_address, 
                                     64, &address_index);
        
    /* Allow NetX Duo time to validate addresses. */     
    tx_thread_sleep(400);
    
    #endif
    
    /* Start the TELNET Server.  */
    status =  nx_telnet_server_start(&my_server);
    
    /* Check for errors.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Create a TELENT client instance.  */
    status =  nx_telnet_client_create(&my_client, "My TELNET Client", 
                                      &ip_client, 600);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    #ifdef FEATURE_NX_IPV6
    
        /* Connect the TELNET client to the TELNET Server at port 23.  */
        status =  nxd_telnet_client_connect(&my_client, &server_ip_address, 23, 
                                             TELNET_TIMEOUT);
    
    #else
        /* Connect the TELNET client to the TELNET Server at port 23.  */
        status =  nx_telnet_client_connect(&my_client, SERVER_ADDRESS, 23,
                                            TELNET_TIMEOUT);
    #endif
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Allocate a packet.  */
    status =  nx_packet_allocate(&pool_client, &my_packet, NX_TCP_PACKET, 
                                  NX_WAIT_FOREVER);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Build a simple 1-byte message.  */
    nx_packet_data_append(my_packet, "a", 1, &pool_client, NX_WAIT_FOREVER);
    
    /* Send the packet to the TELNET Server.  */
    status =  nx_telnet_client_packet_send(&my_client, my_packet, TELNET_TIMEOUT);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Pickup the Server header.  */
    status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 
                                               TELNET_TIMEOUT);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* At this point the packet should contain the Server's banner
        message sent by the Server callback function below.  Just
        release it for this demo.  */
    nx_packet_release(my_packet);
    
    /* Pickup the Server echo of the character.  */
    status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 
                                               TELNET_TIMEOUT);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* At this point the packet should contain the character 'a' that
        we sent earlier.  Just release the packet for now.  */
    nx_packet_release(my_packet);
    
    /* Now disconnect form the TELNET Server.  */
    status =  nx_telnet_client_disconnect(&my_client, TELNET_TIMEOUT);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Delete the TELNET Client.  */
    status =  nx_telnet_client_delete(&my_client);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
}

/* This routine is called by the NetX Telnet Server whenever a new Telnet client 
    connection is established.  */
void  telnet_new_connection(NX_TELNET_SERVER *server_ptr, UINT logical_connection)
{

UINT        status;
NX_PACKET   *packet_ptr;

    /* Allocate a packet for client greeting. */
    status =  nx_packet_allocate(&pool_server, &packet_ptr, NX_TCP_PACKET, 
                                  NX_NO_WAIT);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Build a banner message and a prompt.  */
    nx_packet_data_append(packet_ptr,"**** Welcome to NetX TELNET Server ****\r\n\r\n\r\n", 45,                            
                         &pool_server, NX_NO_WAIT);

    nx_packet_data_append(packet_ptr, "NETX> ", 6, &pool_server, NX_NO_WAIT);
    
    /* Send the packet to the client.  */
    status =  nx_telnet_server_packet_send(server_ptr, logical_connection, 
                                           packet_ptr, TELNET_TIMEOUT);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        nx_packet_release(packet_ptr);
    }
    return;
}

/* This routine is called by the NetX Telnet Server whenever data is present on a 
    Telnet client connection.  */          
void  telnet_receive_data(NX_TELNET_SERVER *server_ptr, UINT logical_connection,
                          NX_PACKET *packet_ptr)
{

UINT    status;
UCHAR   alpha;

    /* This demo echoes the character back; on <cr,lf> sends a new prompt back to 
        the client.  A real system would likely buffer the character(s) received in a 
        buffer associated with the supplied logical connection and process it.  */

    /* Just throw away carriage returns.  */
    if ((packet_ptr -> nx_packet_prepend_ptr[0] == '\r') && (packet_ptr -> nx_packet_length == 1))
    {
        printf("telnet server received just a CRLF\n");

        nx_packet_release(packet_ptr);
        return;
    }

    /* Setup new line on line feed.  */
    if ((packet_ptr -> nx_packet_prepend_ptr[0] == '\n') || (packet_ptr -> nx_packet_prepend_ptr[1] == '\n'))
    {
        /* Clean up the packet.  */
        packet_ptr -> nx_packet_length =  0;
        packet_ptr -> nx_packet_prepend_ptr =  packet_ptr -> nx_packet_data_start + NX_TCP_PACKET;
        packet_ptr -> nx_packet_append_ptr =   packet_ptr -> nx_packet_data_start + NX_TCP_PACKET;

        /* Build the next prompt.  */
        nx_packet_data_append(packet_ptr, "\r\nNETX> ", 8, &pool_server, 
                              NX_NO_WAIT);

        /* Send the packet to the client.  */
        status =  nx_telnet_server_packet_send(server_ptr, logical_connection, 
                                               packet_ptr, TELNET_TIMEOUT);

        if (status != NX_SUCCESS)
        {
            error_counter++;
            nx_packet_release(packet_ptr);
        }
        return;
    }

    /* Pickup first character (usually only one from client).  */
    alpha =  packet_ptr -> nx_packet_prepend_ptr[0];

    /* Echo character.  */
    status =  nx_telnet_server_packet_send(server_ptr, logical_connection, 
                                           packet_ptr, TELNET_TIMEOUT);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        nx_packet_release(packet_ptr);
    }

    /* Check for a disconnection.  */
    if (alpha == 'q')
    {
        /* Initiate server disconnection.  */
        nx_telnet_server_disconnect(server_ptr, logical_connection);
    }
}


/* This routine is called by the NetX Telnet Server when the client disconnects.  */
void  telnet_connection_end(NX_TELNET_SERVER *server_ptr, UINT logical_connection)
{
    /* Cleanup any application specific connection or buffer information.  */
    return;
}
```

## <a name="configuration-options"></a><span data-ttu-id="55a3a-143">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="55a3a-143">Configuration Options</span></span>

<span data-ttu-id="55a3a-144">NetX Duo için Telnet oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-144">There are several configuration options for building Telnet for NetX Duo.</span></span> <span data-ttu-id="55a3a-145">Bu #defines, *nxd_telnet_server. h*. ve *nxd_telnet_client. h* 'a dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-145">These #defines can be set by the application prior to inclusion of *nxd_telnet_server.h*.and *nxd_telnet_client.h.*</span></span>

<span data-ttu-id="55a3a-146">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="55a3a-146">Following is a list of all options, where each is described in detail:</span></span>  
  
- <span data-ttu-id="55a3a-147">**NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel Telnet hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-147">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic Telnet error checking.</span></span> <span data-ttu-id="55a3a-148">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-148">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="55a3a-149">**NX_TELNET_MAX_CLIENTS**: sunucu iş parçacığı tarafından desteklenen en fazla Telnet istemcisi sayısı.</span><span class="sxs-lookup"><span data-stu-id="55a3a-149">**NX_TELNET_MAX_CLIENTS**: The maximum number of Telnet Clients supported by the Server thread.</span></span> <span data-ttu-id="55a3a-150">Varsayılan olarak, bu değer, aynı anda en fazla 4 istemci belirtmek için 4 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-150">By default, this value is defined as 4 to specify a maximum of 4 clients at a time.</span></span>
- <span data-ttu-id="55a3a-151">**NX_TELNET_SERVER_PRIORITY**: Telnet sunucusu iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="55a3a-151">**NX_TELNET_SERVER_PRIORITY**: The priority of the Telnet Server thread.</span></span> <span data-ttu-id="55a3a-152">Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-152">By default, this value is defined as 16 to specify priority 16.</span></span>
- <span data-ttu-id="55a3a-153">**NX_TELNET_TOS**: Telnet TCP istekleri için gereken hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="55a3a-153">**NX_TELNET_TOS**: Type of service required for the Telnet TCP requests.</span></span> <span data-ttu-id="55a3a-154">Varsayılan olarak, bu değer NX_IP_NORMAL belirtmek için olarak tanımlanır</span><span class="sxs-lookup"><span data-stu-id="55a3a-154">By default, this value is defined as NX_IP_NORMAL to indicate</span></span>  
<span data-ttu-id="55a3a-155">normal IP paket hizmeti.</span><span class="sxs-lookup"><span data-stu-id="55a3a-155">normal IP packet service.</span></span>
- <span data-ttu-id="55a3a-156">**NX_TELNET_FRAGMENT_OPTION**: Telnet TCP istekleri için parça etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-156">**NX_TELNET_FRAGMENT_OPTION**: Fragment enable for Telnet TCP requests.</span></span> <span data-ttu-id="55a3a-157">Varsayılan olarak, bu değer Telnet TCP fragmenting ' ı devre dışı bırakmak için NX_DONT_FRAGMENT.</span><span class="sxs-lookup"><span data-stu-id="55a3a-157">By default, this value is NX_DONT_FRAGMENT to disable Telnet TCP fragmenting.</span></span>
- <span data-ttu-id="55a3a-158">**NX_TELNET_SERVER_WINDOW_SIZE**: sunucu yuvası pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="55a3a-158">**NX_TELNET_SERVER_WINDOW_SIZE**: Server socket window size.</span></span> <span data-ttu-id="55a3a-159">Varsayılan olarak, bu değer 2048 bayttır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-159">By default, this value is 2048 bytes.</span></span>
- <span data-ttu-id="55a3a-160">**NX_TELNET_TIME_TO_LIVE**: Bu paketin atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-160">**NX_TELNET_TIME_TO_LIVE**: Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="55a3a-161">Varsayılan değer 0x80 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-161">The default value is set to 0x80.</span></span>
- <span data-ttu-id="55a3a-162">**NX_TELNET_SERVER_TIMEOUT**: iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-162">**NX_TELNET_SERVER_TIMEOUT**: Specifies the number of ThreadX ticks that internal services will suspend for.</span></span> <span data-ttu-id="55a3a-163">Varsayılan değer 10 saniyeye ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-163">The default value is set to 10 seconds.</span></span>
- <span data-ttu-id="55a3a-164">**NX_TELNET_ACTIVITY_TIMEOUT**: sunucu istemci bağlantısının bağlantısını kesmeden önce herhangi bir etkinlik olmadan geçebilecek saniye sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-164">**NX_TELNET_ACTIVITY_TIMEOUT**: Specifies the number of seconds that can elapse without any activity before the Server disconnects the Client connection.</span></span> <span data-ttu-id="55a3a-165">Varsayılan değer 600 saniyeye ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-165">The default value is set to 600 seconds.</span></span>
- <span data-ttu-id="55a3a-166">**NX_TELNET_TIMEOUT_PERIOD**: istemci etkinlik zaman aşımları için denetim arasındaki saniye sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-166">**NX_TELNET_TIMEOUT_PERIOD**: Specifies the number of seconds between checking for Client activity timeouts.</span></span> <span data-ttu-id="55a3a-167">Varsayılan değer 60 saniyeye ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-167">The default value is set to 60 seconds.</span></span>
- <span data-ttu-id="55a3a-168">**NX_TELNET_SERVER_OPTION_DISABLE**: tanımlı, Telnet seçeneği anlaşması devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="55a3a-168">**NX_TELNET_SERVER_OPTION_DISABLE**: Defined, Telnet option negotiation is disabled.</span></span> <span data-ttu-id="55a3a-169">Varsayılan olarak bu seçenek tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-169">By default this option is not defined.</span></span>
- <span data-ttu-id="55a3a-170">**NX_TELNET_SERVER_USER_CREATE_PACKET_POOL**: tanımlanmışsa, Telnet sunucusu paket havuzunun dışarıdan oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-170">**NX_TELNET_SERVER_USER_CREATE_PACKET_POOL**: If defined, the Telnet Server packet pool must be created externally.</span></span> <span data-ttu-id="55a3a-171">Bu yalnızca NX_TELNET_SERVER_OPTION_DISABLE tanımlıysa anlamlıdır.</span><span class="sxs-lookup"><span data-stu-id="55a3a-171">This is only meaningful if NX_TELNET_SERVER_OPTION_DISABLE is not defined.</span></span> <span data-ttu-id="55a3a-172">Varsayılan olarak, bu seçenek tanımlı değildir ve Telnet sunucusu iş parçacığı kendi paket havuzunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="55a3a-172">By default this option is not defined and the Telnet Server thread creates its own packet pool.</span></span>
- <span data-ttu-id="55a3a-173">**NX_TELNET_SERVER_PACKET_PAYLOAD**: seçenek anlaşması Için Telnet sunucusu tarafından oluşturulan paket yükünün boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="55a3a-173">**NX_TELNET_SERVER_PACKET_PAYLOAD**: Defines the size of the packet payload created by the Telnet Server for option negotiation.</span></span> <span data-ttu-id="55a3a-174">Telnet sunucusunun yalnızca NX_TELNET_SERVER _OPTION_DISABLE tanımlanmamışsa Bu paket havuzunu oluşturduğunu unutmayın (Telnet seçenekleri etkinleştirilir).</span><span class="sxs-lookup"><span data-stu-id="55a3a-174">Note that the Telnet Server only creates this packet pool if NX_TELNET_SERVER _OPTION_DISABLE is not defined (Telnet options are enabled).</span></span> <span data-ttu-id="55a3a-175">Bu seçeneğin varsayılan değeri 300 ' dir.</span><span class="sxs-lookup"><span data-stu-id="55a3a-175">The default value of this option is 300.</span></span>
- <span data-ttu-id="55a3a-176">**NX_TELNET_SERVER_PACKET_POOL_SIZE**: Telnet anlaşmaları Için kullanılan Telnet sunucusu paket havuzunun boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="55a3a-176">**NX_TELNET_SERVER_PACKET_POOL_SIZE**: Defines the size of the Telnet Server packet pool used for Telnet negotiations.</span></span> <span data-ttu-id="55a3a-177">Telnet sunucusunun yalnızca NX_TELNET_SERVER _OPTION_DISABLE tanımlanmamışsa Bu paket havuzunu oluşturduğunu unutmayın (Telnet seçenekleri etkinleştirilir).</span><span class="sxs-lookup"><span data-stu-id="55a3a-177">Note that the Telnet Server only creates this packet pool if NX_TELNET_SERVER _OPTION_DISABLE is not defined (Telnet options are enabled).</span></span> <span data-ttu-id="55a3a-178">Bu seçeneğin varsayılan değeri 2048 ' dir ( \~ 5-6 paketleri).</span><span class="sxs-lookup"><span data-stu-id="55a3a-178">The default value of this option is 2048 (\~5-6 packets).</span></span>
