---
title: Bölüm 2-Azure RTOS NetX Duo SNTP Istemcisini yükleme ve kullanma
description: Bu bölüm, NetX Duo SNTP Istemcisinin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cd917e7e70ce21dbff6c8081c2ff115c0acad8a8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825750"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-sntp-client"></a><span data-ttu-id="e8e38-103">Bölüm 2-Azure RTOS NetX Duo SNTP Istemcisini yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="e8e38-103">Chapter 2 - Installation and Use of Azure RTOS NetX Duo SNTP Client</span></span>

<span data-ttu-id="e8e38-104">Bu bölümde, Azure RTOS NetX Duo SNTP Istemcisinin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo SNTP Client.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="e8e38-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="e8e38-105">Product Distribution</span></span>

<span data-ttu-id="e8e38-106">NetX Duo için SNTP, adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="e8e38-106">SNTP for NetX Duo is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="e8e38-107">Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="e8e38-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="e8e38-108">**nxd_sntp_client. c** SNTP Istemci C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="e8e38-108">**nxd_sntp_client.c** SNTP Client C source file</span></span>  
- <span data-ttu-id="e8e38-109">**nxd_sntp_client. h** SNTP Istemci üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="e8e38-109">**nxd_sntp_client.h** SNTP Client Header file</span></span>  
- <span data-ttu-id="e8e38-110">**demo_netxduo_sntp_client. c** Demo SNTP Istemci uygulaması</span><span class="sxs-lookup"><span data-stu-id="e8e38-110">**demo_netxduo_sntp_client.c** Demonstration SNTP Client application</span></span>  
- <span data-ttu-id="e8e38-111">**nxd_sntp_client.pdf** NetX Duo SNTP Istemci Kullanıcı Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="e8e38-111">**nxd_sntp_client.pdf** NetX Duo SNTP Client User Guide</span></span>  

## <a name="netx-duo-sntp-client-installation"></a><span data-ttu-id="e8e38-112">NetX Duo SNTP Istemci yüklemesi</span><span class="sxs-lookup"><span data-stu-id="e8e38-112">NetX Duo SNTP Client Installation</span></span>

<span data-ttu-id="e8e38-113">NetX Duo için SNTP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-113">In order to use SNTP for NetX Duo, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="e8e38-114">Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, NETX Duo SNTP istemci dosyaları *nxd_sntp_client. c* ve *nxd_sntp_client. h* (*nx_sntp_client. c* ve *nx_sntp_client. h* ) bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-114">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the NetX Duo SNTP Client files *nxd_sntp_client.c* and *nxd_sntp_client.h* (*nx_sntp_client.c* and *nx_sntp_client.h* in NetX) should be copied into this directory.</span></span>

## <a name="using-netx-duo-sntp-client"></a><span data-ttu-id="e8e38-115">NetX Duo SNTP Istemcisini kullanma</span><span class="sxs-lookup"><span data-stu-id="e8e38-115">Using NetX Duo SNTP Client</span></span>

<span data-ttu-id="e8e38-116">NetX Duo SNTP Istemcisini kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-116">Using NetX Duo SNTP Client is easy.</span></span> <span data-ttu-id="e8e38-117">Temel olarak, uygulama kodu, sırasıyla ThreadX ve NetX Duo kullanmak için *tx_api. h, fx_api. h* ve *nx_api. h* dahil *nxd_sntp_client.* h içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-117">Basically, the application code must include *nxd_sntp_client.h* after it includes *tx_api.h, fx_api.h,* and *nx_api.h*, in order to use ThreadX and NetX Duo, respectively.</span></span> <span data-ttu-id="e8e38-118">*Nxd_sntp_client. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen SNTP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-118">Once *nxd_sntp_client.h* is included, the application code is then able to make the SNTP function calls specified later in this guide.</span></span> <span data-ttu-id="e8e38-119">Uygulama, yapı işlemine *nxd_sntp_client. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-119">The application must also include *nxd_sntp_client.c* in the build process.</span></span> <span data-ttu-id="e8e38-120">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-120">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="e8e38-121">Bu, NetX Duo SNTP Istemcisini kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-121">This is all that is required to use NetX Duo SNTP Client.</span></span>

> [!NOTE]
> <span data-ttu-id="e8e38-122">NetX Duo SNTP Istemcisi NetX Duo UDP hizmetlerini kullandığından, SNTP hizmetlerini kullanmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-122">Since the NetX Duo SNTP Client utilizes NetX Duo UDP services, UDP must be enabled with the *nx_udp_enable* call prior to using SNTP services.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="e8e38-123">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="e8e38-123">Small Example System</span></span>

<span data-ttu-id="e8e38-124">NetX Duo SNTP kullanmanın bir örneği aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-124">An example of how to use NetX Duo SNTP is shown below.</span></span> <span data-ttu-id="e8e38-125">Bu **Örneğin, sisteminizde** olduğu gibi çalıştığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8e38-125">Note that this example is **not** guaranteed to work as is on your system.</span></span> <span data-ttu-id="e8e38-126">Belirli sistem ve donanımınız için ayarlamalar yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-126">You may need to make adjustments for your particular system and hardware.</span></span> <span data-ttu-id="e8e38-127">Örneğin, NetX RAM sürücüsünü gerçek sürücü işleviniz ile değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-127">For example you will have to replace the NetX ram driver with your actual driver function.</span></span> <span data-ttu-id="e8e38-128">Bu örnek, tam olarak tanıtım amaçlı amaçlıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-128">This example is intended strictly for demonstration purposes.</span></span>

<span data-ttu-id="e8e38-129">Bu örnekte, SNTP üstbilgi dosyası *nxd_sntp_client. h* dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-129">In this example, the SNTP header file *nxd_sntp_client.h* is included.</span></span> <span data-ttu-id="e8e38-130">SNTP Istemcisi "*tx_application_define*" içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e8e38-130">The SNTP Client is created in “*tx_application_define*”.</span></span> <span data-ttu-id="e8e38-131">SNTP Istemcisini oluştururken, ölüm ve artık ikinci işleyici işlevlerinin KISS 'nin isteğe bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8e38-131">Note that the kiss of death and leap second handler functions are optional when creating the SNTP Client.</span></span>

<span data-ttu-id="e8e38-132">Bu tanıtım, IPv6 veya IPv4 ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-132">This demo can be used with IPv6 or IPv4.</span></span> <span data-ttu-id="e8e38-133">SNTP Istemcisini IPv6 üzerinden çalıştırmak için USE_IPV6 tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e8e38-133">To run the SNTP Client over IPv6, define USE_IPV6.</span></span> <span data-ttu-id="e8e38-134">IPv6 'nın NetX Duo içinde de etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-134">IPv6 must be enabled in NetX Duo as well.</span></span> <span data-ttu-id="e8e38-135">SNTP Istemci Konağı, NetX Duo 'da IPv6 adres doğrulaması ve ICMPv6 ve IPv6 Hizmetleri için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-135">The SNTP Client host is set up for IPv6 address validation and ICMPv6 and IPv6 services in NetX Duo.</span></span> <span data-ttu-id="e8e38-136">NetX Duo 'daki IPv6 desteği hakkında daha ayrıntılı bilgi için bkz. NetX Duo Kullanıcı Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="e8e38-136">See the NetX Duo User Guide for more details on IPv6 support in NetX Duo.</span></span>

<span data-ttu-id="e8e38-137">Ardından, tek noktaya yayın veya yayın modu için SNTP Istemcisinin başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-137">Then the SNTP Client must be initialized for either unicast or broadcast mode.</span></span>

<span data-ttu-id="e8e38-138">SNTP Istemcisi başlangıçta sunucu saati güncelleştirmelerini kendi iç veri yapısına yazar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-138">SNTP Client initially writes Server time updates to its own internal data structure.</span></span> <span data-ttu-id="e8e38-139">Bu, cihaz yerel saati ile aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-139">This is not the same as the device local time.</span></span> <span data-ttu-id="e8e38-140">Cihaz yerel saati, SNTP Istemci iş parçacığını başlatmadan önce SNTP Istemcisinde temel bir zaman olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-140">The device local time can be set as a baseline time in the SNTP Client before starting the SNTP Client thread.</span></span> <span data-ttu-id="e8e38-141">Bu, SNTP Istemcisi yapılandırılmışsa (NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP NX_FALSE), ilk sunucu güncelleştirmesini NX_SNTP_CLIENT_MAX_ADJUSTMENT karşılaştırmak için (varsayılan değer 180 milisaniye) yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-141">This is useful if the SNTP Client is configured (NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP set to NX_FALSE) to compare the first Server update to the NX_SNTP_CLIENT_MAX_ADJUSTMENT (default value 180 milliseconds).</span></span> <span data-ttu-id="e8e38-142">Aksi takdirde, SNTP Istemcisi ilk yerel saati sunucudan ilk güncelleştirmeyi aldığında doğrudan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-142">Otherwise the SNTP Client will set the initial local time directly when it gets the first update from the Server.</span></span>

<span data-ttu-id="e8e38-143">Temel bir süre, *nx_sntp_client_set_local_time* HIZMETI kullanılarak SNTP istemcisine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-143">A baseline time is applied to the SNTP Client using the *nx_sntp_client_set_local_time* service.</span></span>

<span data-ttu-id="e8e38-144">SNTP Istemcisi, sırasıyla tek noktaya yayın ve yayın modu için başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-144">The SNTP Client is started on for unicast and broadcast mode respectively.</span></span> <span data-ttu-id="e8e38-145">Belirli bir Aralık (tek noktaya yayın yoklama aralığından biraz daha az) için uygulama, geçerli saatin saniye ve milisaniyesini artırdığımız "gerçek zaman saatinin" *nx_sntp_client_set_local_time* kullanarak SNTP istemci yerel saatini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-145">For a certain interval (slightly less than the unicast polling interval) the application updates the SNTP Client local time, using the *nx_sntp_client_set_local_time*, from the “real time clock” which we simulate by just incrementing the seconds and milliseconds of the current time.</span></span> <span data-ttu-id="e8e38-146">Her aralıktan sonra uygulama, SNTP sunucusundan güncelleştirmeleri düzenli olarak denetler.</span><span class="sxs-lookup"><span data-stu-id="e8e38-146">After each interval, the application then periodically checks for updates from the SNTP server.</span></span> <span data-ttu-id="e8e38-147">*Nx_sntp_client_receiving _updates* HIZMETI, SNTP istemcisinin Şu anda geçerli güncelleştirmeleri aldığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="e8e38-147">The *nx_sntp_client_receiving _updates* service verifies that the SNTP Client is currently receiving valid updates.</span></span> <span data-ttu-id="e8e38-148">Bu durumda, *nx_sntp_client_get_local_time_extended* hizmetini kullanarak en son güncelleştirme zamanı alınır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-148">If so, it will retrieve the latest update time using the *nx_sntp_client_get_local_time_extended* service.</span></span>

<span data-ttu-id="e8e38-149">SNTP istemcisi, *nx_sntp_client_stop* hizmeti kullanılarak herhangi bir zamanda durdurulabilir ve bu örnek, SNTP istemcisinin artık geçerli güncelleştirmeleri almadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-149">The SNTP Client can be stopped at any time using the *nx_sntp_client_stop* service if for example it detects the SNTP Client is no longer receiving valid updates..</span></span> <span data-ttu-id="e8e38-150">Istemciyi yeniden başlatmak için uygulama, tek noktaya yayın veya yayın başlatma hizmetini çağırmalıdır ve sonra tek noktaya yayın veya yayın çalıştırma Hizmetleri 'ni çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-150">To restart the Client, the application must call either the unicast or broadcast initialize service and then call either unicast or broadcast run services.</span></span> <span data-ttu-id="e8e38-151">SNTP Istemci iş parçacığı görevi durdurulduğunda, SNTP Istemcisi gerekirse SNTP sunucularını ve modlarını (tek noktaya yayın veya yayın) değiştirebilir, örneğin önceki SNTP sunucusu çalışmıyor gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="e8e38-151">While the SNTP Client thread task is stopped, the SNTP Client can switch SNTP servers and modes (unicast or broadcast) if needed e.g. the previous SNTP server appears to be down.</span></span>

```c
/* 
   This is a small demo of the NetX SNTP Client on the high-performance NetX
   TCP/IP stack. This demo relies on Thread, NetX and NetX SNTP Client API to
   execute the Simple Network Time Protocol in unicast and broadcast modes.  
 */

#include <stdio.h>
#include "nx_api.h"
#include "nx_ip.h"
#include "nxd_sntp_client.h"
                
/* Define SNTP packet size. */
#define NX_SNTP_CLIENT_PACKET_SIZE      (NX_UDP_PACKET + 100)

/* Define SNTP packet pool size. */
#define NX_SNTP_CLIENT_PACKET_POOL_SIZE      (4 * (NX_SNTP_CLIENT_PACKET_SIZE + 
                                                            sizeof(NX_PACKET)))

/* Define how often the demo checks for SNTP updates. */
#define DEMO_PERIODIC_CHECK_INTERVAL      (1 * NX_IP_PERIODIC_RATE) 

/* Define how often we check on SNTP server status. 
   We expect updates from the SNTP server about every hour using 
   the SNTP Client defaults. For testing
   make this (much) shorter. */
#define CHECK_SNTP_UPDATES_TIMEOUT       (180 * NX_IP_PERIODIC_RATE) 

/* Set up generic network driver for demo program. */
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Application defined services of the NetX SNTP Client. */

UINT leap_second_handler(NX_SNTP_CLIENT *client_ptr, 
                                UINT leap_indicator);
UINT kiss_of_death_handler(NX_SNTP_CLIENT *client_ptr, 
                                        UINT KOD_code);
VOID time_update_callback(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                       NX_SNTP_TIME *local_time);


/* Set up client thread and network resources. */

NX_PACKET_POOL      client_packet_pool;
NX_IP               client_ip;
TX_THREAD           demo_client_thread;
NX_SNTP_CLIENT      demo_sntp_client;
TX_EVENT_FLAGS_GROUP sntp_flags;

#define DEMO_SNTP_UPDATE_EVENT  1

/* Configure the SNTP Client to use IPv6. If not enabled, the 
   Client will use IPv4.  Note: IPv6 must be enabled in NetX Duo
   for the Client to communicate over IPv6.    */
#ifdef FEATURE_NX_IPV6
/* #define USE_IPV6 */
#endif /* FEATURE_NX_IPV6 */


/* Configure the SNTP Client to use unicast SNTP. */
#define USE_UNICAST


#define CLIENT_IP_ADDRESS       IP_ADDRESS(192,2,2,66)
#define SERVER_IP_ADDRESS       IP_ADDRESS(192,2,2,92)
#define SERVER_IP_ADDRESS_2     SERVER_IP_ADDRESS

/* Set up the SNTP network and address index; */
UINT     iface_index =0;
UINT     prefix = 64;   
UINT     address_index;

/* Set up client thread entry point. */
void    demo_client_thread_entry(ULONG info);

/* Define main entry point.  */
int main()
{
    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
    return 0;
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

UINT     status;
UCHAR    *free_memory_pointer;


    free_memory_pointer = (UCHAR *)first_unused_memory;

    /* Create client packet pool. */
    status =  nx_packet_pool_create(&client_packet_pool, 
                                "SNTP Client Packet Pool",
                                NX_SNTP_CLIENT_PACKET_SIZE, 
                                free_memory_pointer, 
                                NX_SNTP_CLIENT_PACKET_POOL_SIZE);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        return;
    }

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer =  free_memory_pointer + NX_SNTP_CLIENT_PACKET_POOL_SIZE;

    /* Create Client IP instances */
    status = nx_ip_create(&client_ip, "SNTP IP Instance", 
                                        CLIENT_IP_ADDRESS, 
                                        0xFFFFFF00UL, 
                                        &client_packet_pool, 
                                       _nx_ram_network_driver, 
                                       free_memory_pointer, 2048, 1);
    
    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }

    free_memory_pointer =  free_memory_pointer + 2048;

#ifndef NX_DISABLE_IPV4
    /* Enable ARP and supply ARP cache memory. */
    status =  nx_arp_enable(&client_ip, (void **) free_memory_pointer, 2048);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }
#endif /* NX_DISABLE_IPV4  */

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;
    
    /* Enable UDP for client. */
    status =  nx_udp_enable(&client_ip);
    
    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }

#ifndef NX_DISABLE_IPV4
    status = nx_icmp_enable(&client_ip);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        return;
    }
#endif /* NX_DISABLE_IPV4  */

    /* Create the client thread */
    status = tx_thread_create(&demo_client_thread, "SNTP Client Thread", 
                                                demo_client_thread_entry, 
                                              (ULONG)(&demo_sntp_client), 
                                                free_memory_pointer, 2048, 
                                                  4, 4, TX_NO_TIME_SLICE, 
                                                        TX_DONT_START);

    /* Check for errors */
    if (status != TX_SUCCESS)
    {

        return;
    }

    /* Create the event flags. */
    status = tx_event_flags_create(&sntp_flags, "SNTP event flags");

    /* Check for errors */
    if (status != TX_SUCCESS)
    {

        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* set the SNTP network interface to the primary interface. */
    iface_index = 0;

    /* Create the SNTP Client to run in broadcast mode.. */
status =  nx_sntp_client_create(&demo_sntp_client, &client_ip,
                           iface_index, &client_packet_pool,  
                               leap_second_handler, 
                               kiss_of_death_handler, 
                               NULL /* no random_number_generator callback */);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        /* Bail out!*/
        return;
    }

    tx_thread_resume(&demo_client_thread);

    return;
}

/* Define size of buffer to display client's local time. */
#define BUFSIZE 50

/* Define the client thread.  */
void    demo_client_thread_entry(ULONG info)
{

UINT   status;
UINT   spin;
UINT   server_status;
ULONG  base_seconds;
ULONG  base_fraction;
ULONG  seconds, milliseconds, microseconds, fraction;
UINT   wait = 0;
UINT   error_counter = 0;
ULONG  events = 0;
#ifdef USE_IPV6
NXD_ADDRESS sntp_server_address;
NXD_ADDRESS client_ip_address;
#endif

    NX_PARAMETER_NOT_USED(info);

    /* Give other threads (IP instance) initialize first. */
    tx_thread_sleep(NX_IP_PERIODIC_RATE); 

#ifdef USE_IPV6
    /* Set up IPv6 services. */
    status = nxd_ipv6_enable(&client_ip);

    status += nxd_icmp_enable(&client_ip);

    if (status  != NX_SUCCESS)
        return;

    client_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    client_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    client_ip_address.nxd_ip_address.v6[2] = 0x0;
    client_ip_address.nxd_ip_address.v6[3] = 0x101;
    client_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

    /* Set the IPv6 server address. */
    sntp_server_address.nxd_ip_address.v6[0] = 0x20010db8;  
    sntp_server_address.nxd_ip_address.v6[1] = 0x0000f101;
    sntp_server_address.nxd_ip_address.v6[2] = 0x0;
    sntp_server_address.nxd_ip_address.v6[3] = 0x00000106;
    sntp_server_address.nxd_ip_version = NX_IP_VERSION_V6;

    /* Establish the link local address for the host. The RAM driver creates
       a virtual MAC address. */
    status = nxd_ipv6_address_set(&client_ip, iface_index, NX_NULL, 10, NULL);

    /* Check for link local address set error.  */
    if (status != NX_SUCCESS) 
    {
        return;
    }

     /* Set the host global IP address. We are assuming a 64 
       bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&client_ip, iface_index, 
                                        &client_ip_address, 
                                    prefix, &address_index);

    /* Check for global address set error.  */
    if (status != NX_SUCCESS) 
    {
        return;
    }

    /* Wait while NetX Duo validates the global and link local addresses. */
    tx_thread_sleep(5 * NX_IP_PERIODIC_RATE);

#endif

    /* Setup time update callback function. */
    nx_sntp_client_set_time_update_notify(&demo_sntp_client, 
                                        time_update_callback);

    /* Set up client time updates depending on mode. */
#ifdef USE_UNICAST

    /* Initialize the Client for unicast mode to 
       poll the SNTP server once an hour. */
#ifdef USE_IPV6
/* Use the duo service to set up the Client and set the IPv6 SNTP server.
   Note: this can take either an IPv4 or IPv6 address. */
    status = nxd_sntp_client_initialize_unicast(&demo_sntp_client, 
                                            &sntp_server_address);
#else
    /* Use the IPv4 service to set up the Client and set the IPv4 SNTP server. */
    status = nx_sntp_client_initialize_unicast(&demo_sntp_client, 
                                                SERVER_IP_ADDRESS);
#endif  /* USE_IPV6 */


#else   /* Broadcast mode */

/* Initialize the Client for broadcast mode, no roundtrip calculation
   required and a broadcast SNTP service. */
#ifdef USE_IPV6
    /* Use the duo service to initialize the Client 
       and set IPv6 SNTP all hosts multicast address. 
       (Note: This can take either an IPv4 or IPv6 address.)*/
    status = nxd_sntp_client_initialize_broadcast(&demo_sntp_client, 
                                                &sntp_server_address, 
                                                            NX_NULL);
#else

    /* Use the IPv4 service to initialize the Client and set 
       IPv4 SNTP broadcast address. */
    status = nx_sntp_client_initialize_broadcast(&demo_sntp_client,  
                                                NX_NULL, 
                                                SERVER_IP_ADDRESS);
#endif  /* USE_IPV6 */
#endif  /* USE_UNICAST */

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Set the base time which is approximately the number of seconds since
       the turn of the last century. If this is not available in SNTP format,
       the nx_sntp_client_utility_add_msecs_to_ntp_time service can convert
       milliseconds to fraction.  For how to compute NTP seconds from real
   time, read the NetX SNTP User Guide. Otherwise set the base time to 
   zero and set NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP to NX_TRUE for
       the SNTP CLient to accept the first time update without applying a
       minimum or maximum adjustment parameters
      (NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT and
       NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT). */

    base_seconds =  0xd2c96b90;  /* Jan 24, 2012 UTC */
    base_fraction = 0xa132db1e;

    /* Apply to the SNTP Client local time.  */
status = nx_sntp_client_set_local_time(&demo_sntp_client, base_seconds,
                                base_fraction);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Run whichever service the client is configured for. */
#ifdef USE_UNICAST
    status = nx_sntp_client_run_unicast(&demo_sntp_client);
#else
    status = nx_sntp_client_run_broadcast(&demo_sntp_client);
#endif  /* USE_UNICAST */

    if (status != NX_SUCCESS)
    {
        return;
    }

    spin = NX_TRUE;

    /* Now check periodically for time changes. */
    while(spin)
    {
        /* Wait for a server update event. */
        tx_event_flags_get(&sntp_flags, DEMO_SNTP_UPDATE_EVENT, 
                                          TX_OR_CLEAR, &events, 
                                 DEMO_PERIODIC_CHECK_INTERVAL);

        if (events == DEMO_SNTP_UPDATE_EVENT)
        {

            /* Check for valid SNTP server status. */
            status = nx_sntp_client_receiving_updates(&demo_sntp_client,
                                               &server_status);

            if ((status != NX_SUCCESS) || (server_status == NX_FALSE))
            {

                /* We do not have a valid update. Skip processing any time
                   data. If this happens repeatedly, consider stopping the
                   SNTP Client thread, picking another SNTP server and
                   resuming the SNTP Client thread task (more details about
                   that in the comments at the end of this function).
                 
                   If SNTP Client configurable parameters are too restrictive,
                   such as Max Adjustment, that may also cause valid server
                   updates to be rejected. Configurable parameters, however,
                   cannot be changed at run time.
                 */
                 
                continue;
            }

            /* We have a valid update.  Get the SNTP Client time.  */
            status = nx_sntp_client_get_local_time_extended(&demo_sntp_client, 
                                                    &seconds, &fraction,  
                                                    NX_NULL, 0); 

            /* Convert fraction to microseconds. */
            nx_sntp_client_utility_fraction_to_usecs(fraction, &microseconds);

            milliseconds = ((microseconds + 500) / 1000);

            if (status != NX_SUCCESS)
            {
                printf("Internal error with getting local time 0x%x\n", 
                       status);
                error_counter++;
            }
            else
            {
                printf("\nSNTP updated\n");
                printf("Time: %lu.%03lu sec.\r\n", seconds, milliseconds);
            }

            /* Clear all events in our event flag. */
            events = 0;
        }
        else
        {

            /* No SNTP update event.             
               In the meantime, if we have an RTC we might want to check
               its notion of time. In this demo, we simulate the passage of 
               time on our 'RTC' really just the CPU counter, assuming that 
               seconds and milliseconds have previously been set to a base 
              (starting) time (as was the SNTP Client before running it) 
             */

            seconds += 1;
            milliseconds += 1;

            /* Update our timer. */
            wait += DEMO_PERIODIC_CHECK_INTERVAL;

            /* Check if it is time to display the local 'RTC' time. */
            if (wait >= CHECK_SNTP_UPDATES_TIMEOUT)
            {
                /* It is. Reset the timeout and print local time. */
                wait = 0;

                printf("Time: %lu.%03lu sec.\r\n", seconds, milliseconds);
            }           
        }
    }

/* We can stop the SNTP service if for example we think the SNTP server 
   has stopped sending updates.
     
       To restart the SNTP Client, simply call the
       nx_sntp_client_initialize_unicast or
       nx_sntp_client_initialize_broadcast using another SNTP server IP
       address as input, and resume the SNTP Client by calling
       nx_sntp_client_run_unicast or
       nx_sntp_client_run_braodcast. */
    status = nx_sntp_client_stop(&demo_sntp_client);

    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    /* When done with the SNTP Client, we delete it */
    status = nx_sntp_client_delete(&demo_sntp_client);

    return;
}


/* This application defined handler for handling an 
   impending leap second is not required by 
   the SNTP Client. The default handler below only logs the
   event for every time stamp received with the 
   leap indicator set.  */

UINT leap_second_handler(NX_SNTP_CLIENT *client_ptr, 
                                UINT leap_indicator)
{
    NX_PARAMETER_NOT_USED(client_ptr);
    NX_PARAMETER_NOT_USED(leap_indicator);

    /* Handle the leap second handler... */

    return NX_SUCCESS;
}

/* This application defined handler for handling 
   a Kiss of Death packet is not required by the SNTP Client. 
   A KOD handler should determine if the Client task should continue vs. 
   abort sending/receiving time data from its current time server, 
   and if aborting if it should remove
   the server from its active server list. 

   Note that the KOD list of codes is subject to change. The list
   below is current at the time of this software release. */

UINT kiss_of_death_handler(NX_SNTP_CLIENT *client_ptr, UINT KOD_code)
{

UINT    remove_server_from_list = NX_FALSE;
UINT    status = NX_SUCCESS;

    NX_PARAMETER_NOT_USED(client_ptr);

    /* Handle kiss of death by code group. */
    switch (KOD_code)
    {

        case NX_SNTP_KOD_RATE:
        case NX_SNTP_KOD_NOT_INIT:
        case NX_SNTP_KOD_STEP:

            /* Find another server while this one 
               is temporarily out of service.  */
            status =  NX_SNTP_KOD_SERVER_NOT_AVAILABLE;

        break;

        case NX_SNTP_KOD_AUTH_FAIL:
        case NX_SNTP_KOD_NO_KEY:
        case NX_SNTP_KOD_CRYP_FAIL:

            /* These indicate the server will not 
               service client with time updates
               without successful authentication. */


            remove_server_from_list =  NX_TRUE;

        break;


        default:

            /* All other codes. Remove server 
               before resuming time updates. */

            remove_server_from_list =  NX_TRUE;
        break;
    }

    /* Removing the server from the active server list? */
    if (remove_server_from_list)
    {

        /* Let the caller know it has to bail on 
           this server before resuming service. */
        status = NX_SNTP_KOD_REMOVE_SERVER;
    }

    return status;
}


/* This application defined handler for notifying SNTP time update event.  */

VOID time_update_callback(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                       NX_SNTP_TIME *local_time)
{
    tx_event_flags_set(&sntp_flags, DEMO_SNTP_UPDATE_EVENT, TX_OR);
}

```

<span data-ttu-id="e8e38-152">Şekil 1 NetX Duo ile SNTP Istemcisini kullanma örneği</span><span class="sxs-lookup"><span data-stu-id="e8e38-152">Figure 1 Example of using SNTP Client with NetX Duo</span></span>

## <a name="configuration-options"></a><span data-ttu-id="e8e38-153">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="e8e38-153">Configuration Options</span></span>

<span data-ttu-id="e8e38-154">NetX Duo SNTP Istemcisini tanımlamaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-154">There are several configuration options for defining the NetX Duo SNTP Client.</span></span> <span data-ttu-id="e8e38-155">Aşağıdaki listede her biri ayrıntılı açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="e8e38-155">The following list describes each in detail:</span></span>  
  

<span data-ttu-id="e8e38-156">**NX_SNTP_CLIENT_THREAD_STACK_SIZE**</span><span class="sxs-lookup"><span data-stu-id="e8e38-156">**NX_SNTP_CLIENT_THREAD_STACK_SIZE**</span></span>  
<span data-ttu-id="e8e38-157">Bu seçenek, Istemci iş parçacığı yığınının boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-157">This option sets the size of the Client thread stack.</span></span> <span data-ttu-id="e8e38-158">Varsayılan NetX Duo SNTP Istemci boyutu 2048 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-158">The default NetX Duo SNTP Client size is 2048.</span></span>

<span data-ttu-id="e8e38-159">**NX_SNTP_CLIENT_THREAD_TIME_SLICE**</span><span class="sxs-lookup"><span data-stu-id="e8e38-159">**NX_SNTP_CLIENT_THREAD_TIME_SLICE**</span></span>  
<span data-ttu-id="e8e38-160">Bu seçenek, Scheduler 'ın Istemci iş parçacığı yürütmeye izin verdiği zaman dilimini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-160">This option sets the time slice of the scheduler allows for Client thread execution.</span></span> <span data-ttu-id="e8e38-161">Varsayılan NetX Duo SNTP Istemci boyutu TX_NO_TIME_SLICE.</span><span class="sxs-lookup"><span data-stu-id="e8e38-161">The default NetX Duo SNTP Client size is TX_NO_TIME_SLICE.</span></span>

<span data-ttu-id="e8e38-162">**NX_SNTP_CLIENT_ THREAD_PRIORITY**</span><span class="sxs-lookup"><span data-stu-id="e8e38-162">**NX_SNTP_CLIENT_ THREAD_PRIORITY**</span></span>  
<span data-ttu-id="e8e38-163">Bu seçenek Istemci iş parçacığı önceliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-163">This option sets the Client thread priority.</span></span> <span data-ttu-id="e8e38-164">NetX Duo SNTP Istemci varsayılan değeri 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-164">The NetX Duo SNTP Client default value is 2.</span></span>

<span data-ttu-id="e8e38-165">**NX_SNTP_CLIENT_PREEMPTION_THRESHOLD**</span><span class="sxs-lookup"><span data-stu-id="e8e38-165">**NX_SNTP_CLIENT_PREEMPTION_THRESHOLD**</span></span>  
<span data-ttu-id="e8e38-166">Bu seçenek, Istemci iş parçacığının önalım izin verdiği öncelik düzeyini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-166">This option sets the sets the level of priority at which the Client thread allows preemption.</span></span> <span data-ttu-id="e8e38-167">Varsayılan NetX Duo SNTP Istemci değeri olarak ayarlanır `NX_SNTP_CLIENT_ THREAD_PRIORITY` .</span><span class="sxs-lookup"><span data-stu-id="e8e38-167">The default NetX Duo SNTP Client value is set to `NX_SNTP_CLIENT_ THREAD_PRIORITY`.</span></span>

<span data-ttu-id="e8e38-168">**NX_SNTP_CLIENT_UDP_SOCKET_NAME**</span><span class="sxs-lookup"><span data-stu-id="e8e38-168">**NX_SNTP_CLIENT_UDP_SOCKET_NAME**</span></span>  
<span data-ttu-id="e8e38-169">Bu seçenek, UDP yuva adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-169">This option sets the UDP socket name.</span></span> <span data-ttu-id="e8e38-170">NetX Duo SNTP Istemci UDP yuva adı varsayılan değer "SNTP Istemci soketi" dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-170">The NetX Duo SNTP Client UDP socket name default is “SNTP Client socket.”</span></span>

<span data-ttu-id="e8e38-171">**NX_SNTP_CLIENT_UDP_PORT**</span><span class="sxs-lookup"><span data-stu-id="e8e38-171">**NX_SNTP_CLIENT_UDP_PORT**</span></span>  
<span data-ttu-id="e8e38-172">Bu, Istemci yuvasının bağlandığı bağlantı noktasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-172">This sets the port which the Client socket is bound to.</span></span> <span data-ttu-id="e8e38-173">Varsayılan NetX Duo SNTP Istemci bağlantı noktası 123 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-173">The default NetX Duo SNTP Client port is 123.</span></span>

<span data-ttu-id="e8e38-174">**NX_SNTP_SERVER_UDP_PORT**</span><span class="sxs-lookup"><span data-stu-id="e8e38-174">**NX_SNTP_SERVER_UDP_PORT**</span></span>  
<span data-ttu-id="e8e38-175">Bu bağlantı noktası, Istemcinin SNTP sunucusuna SNTP iletileri gönderdiği bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-175">This is port which the Client sends SNTP messages to the SNTP Server on.</span></span> <span data-ttu-id="e8e38-176">Varsayılan NetX SNTP sunucu bağlantı noktası 123 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-176">The default NetX SNTP Server port is 123.</span></span>

<span data-ttu-id="e8e38-177">**NX_SNTP_CLIENT_TIME_TO_LIVE**</span><span class="sxs-lookup"><span data-stu-id="e8e38-177">**NX_SNTP_CLIENT_TIME_TO_LIVE**</span></span>  
<span data-ttu-id="e8e38-178">Bir Istemci paketinin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-178">Specifies the number of routers a Client packet can pass before it is discarded.</span></span> <span data-ttu-id="e8e38-179">Varsayılan NetX Duo SNTP Istemcisi, 0x80 olarak ayarlanır *.*</span><span class="sxs-lookup"><span data-stu-id="e8e38-179">The default NetX Duo SNTP Client is set to 0x80 *.*</span></span>

<span data-ttu-id="e8e38-180">**NX_SNTP_CLIENT_MAX_QUEUE_DEPTH**</span><span class="sxs-lookup"><span data-stu-id="e8e38-180">**NX_SNTP_CLIENT_MAX_QUEUE_DEPTH**</span></span>  
<span data-ttu-id="e8e38-181">NetX Duo SNTP Istemci yuvasında sıraya alınabilen en fazla UDP paketi sayısı (veri birimi).</span><span class="sxs-lookup"><span data-stu-id="e8e38-181">Maximum number of UDP packets (datagrams) that can be queued in the NetX Duo SNTP Client socket.</span></span> <span data-ttu-id="e8e38-182">Alınan ek paketler, en eski paketlerin yayımlandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-182">Additional packets received mean the oldest packets are released.</span></span> <span data-ttu-id="e8e38-183">Varsayılan NetX Duo SNTP Istemcisi 5 olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-183">The default NetX Duo SNTP Client is set to 5.</span></span>

<span data-ttu-id="e8e38-184">**NX_SNTP_CLIENT_PACKET_TIMEOUT**</span><span class="sxs-lookup"><span data-stu-id="e8e38-184">**NX_SNTP_CLIENT_PACKET_TIMEOUT**</span></span>  
<span data-ttu-id="e8e38-185">NetX Duo paket ayırması için zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="e8e38-185">Time out for NetX Duo packet allocation.</span></span> <span data-ttu-id="e8e38-186">Varsayılan NetX Duo SNTP Istemci paketi zaman aşımı değeri 1 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-186">The default NetX Duo SNTP Client packet timeout is 1 second.</span></span>

<span data-ttu-id="e8e38-187">**NX_SNTP_CLIENT_NTP_VERSION**</span><span class="sxs-lookup"><span data-stu-id="e8e38-187">**NX_SNTP_CLIENT_NTP_VERSION**</span></span>  
<span data-ttu-id="e8e38-188">Istemci tarafından kullanılan SNTP sürümü NetX Duo SNTP Istemci API 'SI sürüm 4 ' ü temel alır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-188">SNTP version used by the Client The NetX Duo SNTP Client API was based on Version 4.</span></span> <span data-ttu-id="e8e38-189">Varsayılan değer 3 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-189">The default value is 3.</span></span>

<span data-ttu-id="e8e38-190">**NX_SNTP_CLIENT_MIN_NTP_VERSION**</span><span class="sxs-lookup"><span data-stu-id="e8e38-190">**NX_SNTP_CLIENT_MIN_NTP_VERSION**</span></span>  
<span data-ttu-id="e8e38-191">En eski SNTP sürümü Istemci ile çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-191">Oldest SNTP version the Client will be able to work with.</span></span> <span data-ttu-id="e8e38-192">NetX Duo SNTP Istemcisi varsayılan sürüm 3 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-192">The NetX Duo SNTP Client default is Version 3.</span></span>

<span data-ttu-id="e8e38-193">**NX_SNTP_CLIENT_MIN_SERVER_STRATUM**</span><span class="sxs-lookup"><span data-stu-id="e8e38-193">**NX_SNTP_CLIENT_MIN_SERVER_STRATUM**</span></span>  
<span data-ttu-id="e8e38-194">İstemcinin kabul edeceği en düşük düzey (en yüksek sayısal katman düzeyi) SNTP sunucu katman.</span><span class="sxs-lookup"><span data-stu-id="e8e38-194">The lowest level (highest numeric stratum level) SNTP Server stratum the Client will accept.</span></span> <span data-ttu-id="e8e38-195">NetX Duo SNTP Istemci varsayılanı 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-195">The NetX Duo SNTP Client default is 2.</span></span>

<span data-ttu-id="e8e38-196">**NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT**</span><span class="sxs-lookup"><span data-stu-id="e8e38-196">**NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT**</span></span>  
<span data-ttu-id="e8e38-197">Istemcinin yerel saat saatinde yapması için milisaniye olarak en kısa süre ayarlaması.</span><span class="sxs-lookup"><span data-stu-id="e8e38-197">The minimum time adjustment in milliseconds the Client will make to its local clock time.</span></span> <span data-ttu-id="e8e38-198">Bu, aşağıdaki zaman ayarlamaları yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-198">Time adjustments below this will be ignored.</span></span> <span data-ttu-id="e8e38-199">NetX Duo SNTP Istemci varsayılanı 10 ' dur.</span><span class="sxs-lookup"><span data-stu-id="e8e38-199">The NetX Duo SNTP Client default is 10.</span></span>

<span data-ttu-id="e8e38-200">**NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT**</span><span class="sxs-lookup"><span data-stu-id="e8e38-200">**NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT**</span></span>  
<span data-ttu-id="e8e38-201">Istemcinin yerel saat saatinde yapması için milisaniye olarak en uzun süre ayarlaması.</span><span class="sxs-lookup"><span data-stu-id="e8e38-201">The maximum time adjustment in milliseconds the Client will make to its local clock time.</span></span> <span data-ttu-id="e8e38-202">Bu tutarın üzerindeki zaman ayarlamaları için, yerel saat ayarlaması en uzun süre ayarlamasıyla sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-202">For time adjustments above this amount, the local clock adjustment is limited to the maximum time adjustment.</span></span> <span data-ttu-id="e8e38-203">NetX Duo SNTP Istemci varsayılanı 180000 (3 dakika).</span><span class="sxs-lookup"><span data-stu-id="e8e38-203">The NetX Duo SNTP Client default is 180000 (3 minutes).</span></span>

<span data-ttu-id="e8e38-204">**NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP**</span><span class="sxs-lookup"><span data-stu-id="e8e38-204">**NX_SNTP_CLIENT_IGNORE_MAX_ADJUST_STARTUP**</span></span>  
<span data-ttu-id="e8e38-205">Bu, Istemci zaman sunucusundan ilk güncelleştirmeyi aldığında en uzun süre ayarlamasının alınmaz olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-205">This enables the maximum time adjustment to be waived when the Client receives the first update from its time server.</span></span> <span data-ttu-id="e8e38-206">Bundan sonra, en uzun süre ayarlaması zorlanır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-206">Thereafter, the maximum time adjustment is enforced.</span></span> <span data-ttu-id="e8e38-207">Amaç, Istemciyi sunucu saatiyle en kısa sürede eşitlenmiş duruma getirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-207">The intention is to get the Client in synch with the server clock as soon as possible.</span></span> <span data-ttu-id="e8e38-208">NetX Duo SNTP Istemci varsayılanı NX_TRUE.</span><span class="sxs-lookup"><span data-stu-id="e8e38-208">The NetX Duo SNTP Client default is NX_TRUE.</span></span>

<span data-ttu-id="e8e38-209">**NX_SNTP_CLIENT_MAX_TIME_LAPSE**</span><span class="sxs-lookup"><span data-stu-id="e8e38-209">**NX_SNTP_CLIENT_MAX_TIME_LAPSE**</span></span>  
<span data-ttu-id="e8e38-210">SNTP Istemcisi tarafından alınan geçerli bir zaman güncelleştirmesi olmadan en fazla izin verilen süre (saniye) aşıldı.</span><span class="sxs-lookup"><span data-stu-id="e8e38-210">Maximum allowable amount of time (seconds) elapsed without a valid time update received by the SNTP Client.</span></span> <span data-ttu-id="e8e38-211">SNTP Istemcisi işlem sırasında devam eder, ancak SNTP sunucu durumu NX_FALSE olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-211">The SNTP Client will continue in operation but the SNTP Server status is set to NX_FALSE.</span></span> <span data-ttu-id="e8e38-212">Varsayılan değer 7200 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-212">The default value is 7200.</span></span>


<span data-ttu-id="e8e38-213">**NX_SNTP_UPDATE_TIMEOUT_INTERVAL**</span><span class="sxs-lookup"><span data-stu-id="e8e38-213">**NX_SNTP_UPDATE_TIMEOUT_INTERVAL**</span></span>  
<span data-ttu-id="e8e38-214">SNTP Istemci süreölçerinin, son geçerli güncelleştirmeden bu yana kalan SNTP Istemci zamanını güncelleştirdiği zaman aralığı (saniye) ve tek noktaya yayın Istemcisi, sonraki SNTP güncelleştirme isteğini göndermeden önce kalan yoklama aralığı süresini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-214">The interval (seconds) at which the SNTP Client timer updates the SNTP Client time remaining since the last valid update received, and the unicast Client updates the poll interval time remaining before sending the next SNTP update request.</span></span> <span data-ttu-id="e8e38-215">Varsayılan değer 1’dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-215">The default value is 1.</span></span>

<span data-ttu-id="e8e38-216">**NX_SNTP_CLIENT_UNICAST_POLL_INTERVAL**</span><span class="sxs-lookup"><span data-stu-id="e8e38-216">**NX_SNTP_CLIENT_UNICAST_POLL_INTERVAL**</span></span>  
<span data-ttu-id="e8e38-217">Istemcinin SNTP sunucusuna bir tek noktaya yayın isteği gönderdiği başlangıç yoklama aralığı (saniye).</span><span class="sxs-lookup"><span data-stu-id="e8e38-217">The starting poll interval (seconds) on which the Client sends a unicast request to its SNTP server.</span></span> <span data-ttu-id="e8e38-218">NetX Duo SNTP Istemci varsayılanı 3600 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-218">The NetX Duo SNTP Client default is 3600.</span></span>

<span data-ttu-id="e8e38-219">**NX_SNTP_CLIENT_EXP_BACKOFF_RATE**</span><span class="sxs-lookup"><span data-stu-id="e8e38-219">**NX_SNTP_CLIENT_EXP_BACKOFF_RATE**</span></span>  
<span data-ttu-id="e8e38-220">Geçerli Istemci tek noktaya yayın yoklama aralığının arttığı faktör.</span><span class="sxs-lookup"><span data-stu-id="e8e38-220">The factor by which the current Client unicast poll interval is increased.</span></span> <span data-ttu-id="e8e38-221">Istemci, bir sunucu saati güncelleştirmesi alamadığında veya sunucudan geçici olarak kullanılamayan (henüz eşitlenmemiş), zaman güncelleştirme hizmeti için geçerli yoklama aralığını arttıracaktır. bu hız, NX_SNTP_CLIENT_MAX_TIME_LAPSE aşmaz.</span><span class="sxs-lookup"><span data-stu-id="e8e38-221">When the Client fails to receive a server time update, or receiving indications from the server that it is temporarily unavailable (e.g. not synchronized yet) for time update service, it will increase the current poll interval by this rate up to but not exceeding NX_SNTP_CLIENT_MAX_TIME_LAPSE.</span></span> <span data-ttu-id="e8e38-222">Varsayılan değer 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-222">The default is 2.</span></span>

<span data-ttu-id="e8e38-223">**NX_SNTP_CLIENT_RTT_REQUIRED**</span><span class="sxs-lookup"><span data-stu-id="e8e38-223">**NX_SNTP_CLIENT_RTT_REQUIRED**</span></span>  
<span data-ttu-id="e8e38-224">Etkinleştirilirse Bu seçenek, SNTP Istemcisinin, yerel saate sunucu güncelleştirmelerini uygularken SNTP iletilerinin gidiş dönüş süresini hesaplamasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-224">This option if enabled requires that the SNTP Client calculate round trip time of SNTP messages when applying Server updates to the local clock.</span></span> <span data-ttu-id="e8e38-225">Varsayılan değer NX_FALSE (devre dışı).</span><span class="sxs-lookup"><span data-stu-id="e8e38-225">The default value is NX_FALSE (disabled).</span></span>

<span data-ttu-id="e8e38-226">**NX_SNTP_CLIENT_MAX_ROOT_DISPERSION**</span><span class="sxs-lookup"><span data-stu-id="e8e38-226">**NX_SNTP_CLIENT_MAX_ROOT_DISPERSION**</span></span>  
<span data-ttu-id="e8e38-227">Sunucu saati hassasiyetmesinin bir ölçüsü olan en fazla sunucu saati dağılımı (mikrosaniye), Istemci kabul eder.</span><span class="sxs-lookup"><span data-stu-id="e8e38-227">The maximum server clock dispersion (microseconds), which is a measure of server clock precision, the Client will accept.</span></span> <span data-ttu-id="e8e38-228">Bu gereksinimi devre dışı bırakmak için, en yüksek kök dağılımı için 0x0 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e8e38-228">To disable this requirement, set the maximum root dispersion to 0x0.</span></span> <span data-ttu-id="e8e38-229">NetX Duo SNTP Istemci varsayılanı 50000 olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-229">The NetX Duo SNTP Client default is set to 50000.</span></span>

<span data-ttu-id="e8e38-230">**NX_SNTP_CLIENT_INVALID_UPDATE_LIMIT**</span><span class="sxs-lookup"><span data-stu-id="e8e38-230">**NX_SNTP_CLIENT_INVALID_UPDATE_LIMIT**</span></span>  
<span data-ttu-id="e8e38-231">Istemci sunucudan yayın veya tek noktaya yayın modunda alınan ardışık geçersiz güncelleştirme sayısı sınırı.</span><span class="sxs-lookup"><span data-stu-id="e8e38-231">The limit on the number of consecutive invalid updates received from the Client server in either broadcast or unicast mode.</span></span> <span data-ttu-id="e8e38-232">Bu sınıra ulaşıldığında, Istemci geçerli SNTP sunucu durumunu geçersiz (NX_FALSE) olarak ayarlar, ancak sunucudan güncelleştirmeleri almaya çalışmaya devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-232">When this limit is reached, the Client sets the current SNTP Server status to invalid (NX_FALSE) although it will continue to try to receive updates from the Server.</span></span> <span data-ttu-id="e8e38-233">NetX Duo SNTP Istemci varsayılanı 3 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-233">The NetX Duo SNTP Client default is 3.</span></span>

<span data-ttu-id="e8e38-234">**NX_SNTP_CLIENT_RANDOMIZE_ON_STARTUP**</span><span class="sxs-lookup"><span data-stu-id="e8e38-234">**NX_SNTP_CLIENT_RANDOMIZE_ON_STARTUP**</span></span>  
<span data-ttu-id="e8e38-235">Bu, tek noktaya yayın modundaki SNTP Istemcisinin, rastgele bir bekleme aralığından sonra geçerli SNTP sunucusuyla ilk SNTP isteğini göndermesini gerekip gerekmediğini belirler.</span><span class="sxs-lookup"><span data-stu-id="e8e38-235">This determines if the SNTP Client in unicast mode should send its first SNTP request with the current SNTP server after a random wait interval.</span></span> <span data-ttu-id="e8e38-236">SNTP sunucusunda trafik tıkanıklığını sınırlamak için önemli sayıda SNTP Istemcisinin aynı anda başlatılmakta olduğu durumlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-236">It is used in cases where significant numbers of SNTP Clients are starting up simultaneously to limit traffic congestion on the SNTP Server.</span></span> <span data-ttu-id="e8e38-237">Varsayılan değer NX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="e8e38-237">The default value is NX_FALSE.</span></span>

<span data-ttu-id="e8e38-238">**NX_SNTP_CLIENT_SLEEP_INTERVAL**</span><span class="sxs-lookup"><span data-stu-id="e8e38-238">**NX_SNTP_CLIENT_SLEEP_INTERVAL**</span></span>  
<span data-ttu-id="e8e38-239">SNTP Istemci görevinin uyku moduna geçme zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="e8e38-239">The time interval during which the SNTP Client task sleeps.</span></span> <span data-ttu-id="e8e38-240">Bu, uygulama API çağrılarının SNTP Istemcisi tarafından yürütülmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8e38-240">This allows the application API calls to be executed by the SNTP Client.</span></span> <span data-ttu-id="e8e38-241">Varsayılan değer 1 Zamanlayıcı çentik ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-241">The default value is 1 timer tick.</span></span>

<span data-ttu-id="e8e38-242">**NX_SNTP_CURRENT_YEAR**</span><span class="sxs-lookup"><span data-stu-id="e8e38-242">**NX_SNTP_CURRENT_YEAR**</span></span>  
<span data-ttu-id="e8e38-243">Tarihi yıl/ay/tarih biçiminde göstermek için bu değeri geçerli yıldan eşit veya daha küçük olarak ayarlayın (değerlendirilmekte olan NTP süresi ile aynı yıl olması gerekir).</span><span class="sxs-lookup"><span data-stu-id="e8e38-243">To display date in year/month/date format, set this value to equal or less than current year (need not be same year as in NTP time being evaluated).</span></span> <span data-ttu-id="e8e38-244">Varsayılan değer 2015 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8e38-244">The default value is 2015.</span></span>

<span data-ttu-id="e8e38-245">**NTP_SECONDS_AT_01011999**</span><span class="sxs-lookup"><span data-stu-id="e8e38-245">**NTP_SECONDS_AT_01011999**</span></span>  
<span data-ttu-id="e8e38-246">Bu, ana NTP saatindeki ilk NTP dönemi için saniye cinsinden sayıdır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-246">This is the number of seconds into the first NTP Epoch on the master NTP clock.</span></span> <span data-ttu-id="e8e38-247">0xBA368E80 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e8e38-247">It is defined as 0xBA368E80.</span></span> <span data-ttu-id="e8e38-248">NTP saniyelik görüntülemeyi tarih ve saate devre dışı bırakmak için sıfır olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e8e38-248">To disable display of NTP seconds into date and time, set to zero.</span></span>
