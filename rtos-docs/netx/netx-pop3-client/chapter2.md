---
title: Bölüm 2-Azure RTOS NetX POP3 Istemcisinin yüklenmesi ve kullanımı
description: NetX POP3 Istemcisi bir kaynak dosyası, bir üst bilgi dosyası ve bir demo dosyası içerir. MD5 Özet Hizmetleri için iki ek dosya vardır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 24de396c69d458866f9423fd995bcb8d905f29c8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826663"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-pop3-client"></a><span data-ttu-id="e72fc-104">Bölüm 2-Azure RTOS NetX POP3 Istemcisinin yüklenmesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="e72fc-104">Chapter 2 - Installation and use of Azure RTOS NetX POP3 Client</span></span>

<span data-ttu-id="e72fc-105">NetX POP3 Istemcisi bir kaynak dosyası, bir üst bilgi dosyası ve bir demo dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-105">NetX POP3 Client includes one source file, one header file, and a demo file.</span></span> <span data-ttu-id="e72fc-106">MD5 Özet Hizmetleri için iki ek dosya vardır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-106">There are two additional files for MD5 digest services.</span></span> <span data-ttu-id="e72fc-107">Ayrıca bir Kullanıcı Kılavuzu PDF dosyası (Bu belge) vardır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-107">There is also a User Guide PDF file (this document).</span></span>

- <span data-ttu-id="e72fc-108">**nx_pop3_client. c**: NETX POP3 istemcisi API 'si Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="e72fc-108">**nx_pop3_client.c**: C Source file for NetX POP3 Client API</span></span>
- <span data-ttu-id="e72fc-109">**nx_pop3_client. h**: NETX POP3 istemcisi API 'si Için C üstbilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="e72fc-109">**nx_pop3_client.h**: C Header file for NetX POP3 Client API</span></span>
- <span data-ttu-id="e72fc-110">**demo_netxduo_pop3_client. c**: POP3 istemcisi oluşturma ve oturum başlatma için demo dosyası</span><span class="sxs-lookup"><span data-stu-id="e72fc-110">**demo_netxduo_pop3_client.c**: Demo file for POP3 Client creation and session initiation</span></span>
- <span data-ttu-id="e72fc-111">**nx_md5. c**: MD5 Özet hizmetlerini tanımlayan c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="e72fc-111">**nx_md5.c**: C Source file defining MD5 digest services</span></span>
- <span data-ttu-id="e72fc-112">**nx_md5. h**: MD5 Özet hizmetlerini tanımlayan C üstbilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="e72fc-112">**nx_md5.h**: C Header file defining MD5 digest services</span></span>
- <span data-ttu-id="e72fc-113">**nx_pop3_client.pdf**: NETX POP3 Istemcisi Kullanıcı Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="e72fc-113">**nx_pop3_client.pdf**: NetX POP3 Client User Guide</span></span>

<span data-ttu-id="e72fc-114">NetX POP3 Istemcisini kullanmak için, daha önce bahsedilen tüm dağıtım, NetX 'in yüklendiği dizine kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-114">To use NetX POP3 Client, the entire distribution mentioned previously can be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="e72fc-115">Örneğin, "*\threadx\mcf5272\green*" dizininde NETX yüklüyse, *nx_md5. h*, *nx_md5. c,* *nx_pop3_client. h ve nx_pop3_client. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-115">For example, if NetX is installed in the directory "*\threadx\mcf5272\green*" then the *nx_md5.h*, *nx_md5.c,* *nx_pop3_client.h, and nx_pop3_client.c* files should be copied into this directory.</span></span>

## <a name="using-netx-pop3-client"></a><span data-ttu-id="e72fc-116">NetX POP3 Istemcisi kullanma</span><span class="sxs-lookup"><span data-stu-id="e72fc-116">Using NetX POP3 Client</span></span>

<span data-ttu-id="e72fc-117">NetX POP3 Istemci hizmetini kullanmak için, uygulamanın yapı projesine *nx_pop3_client. c* eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-117">To use the NetX POP3 Client service, the application must add *nx_pop3_client.c* to its build project.</span></span> <span data-ttu-id="e72fc-118">Uygulama kodu, ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* sonrasında *nx_md5. h, nx_pop3. h ve nx_pop3_client.* h içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-118">The application code must include *nx_md5.h, nx_pop3.h and nx_pop3_client.h* after *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span>

<span data-ttu-id="e72fc-119">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne kodu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-119">These files must be compiled in the same manner as other application files and the object code must be linked along with the files of the application.</span></span> <span data-ttu-id="e72fc-120">Bu, NetX POP3 Istemcisini kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-120">This is all that is required to use the NetX POP3 Client.</span></span>

## <a name="small-example-of-the-netx-pop3-client"></a><span data-ttu-id="e72fc-121">NetX POP3 Istemcisinin küçük örneği</span><span class="sxs-lookup"><span data-stu-id="e72fc-121">Small Example of the NetX POP3 Client</span></span>

<span data-ttu-id="e72fc-122">NetX POP3 Istemci hizmetlerinin nasıl kullanılacağına ilişkin bir örnek şekil 1 ' de aşağıda gösterilen şekilde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-122">An example of how to use NetX POP3 Client services is described in Figure 1 that appears below.</span></span> <span data-ttu-id="e72fc-123">Bu demo, 37 ve 38 satırlarında posta indirme ve oturum tamamlama bildirimi için iki geri çağırma yapar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-123">This demo sets up the two callbacks for notification of mail download and session completion on lines 37 and 38.</span></span> <span data-ttu-id="e72fc-124">POP3 Istemcisi paket havuzu 76. satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e72fc-124">The POP3 Client packet pool is created on line 76.</span></span> <span data-ttu-id="e72fc-125">IP iş parçacığı görevi 88. satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e72fc-125">The IP thread task is created on line 88.</span></span> <span data-ttu-id="e72fc-126">Bu paket havuzunun POP3 Istemci paket havuzu için de kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e72fc-126">Note that this packet pool is also used for the POP3 Client packet pool.</span></span> <span data-ttu-id="e72fc-127">TCP, satır 107 ' deki IP görevinde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-127">TCP is enabled on the IP task in line 107.</span></span>

<span data-ttu-id="e72fc-128">POP3 Istemcisi, uygulama iş parçacığı girişi *demo_thread_entry* işlevi içindeki 133 numaralı satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e72fc-128">The POP3 Client is created on line 133 inside the application thread entry function, *demo_thread_entry*.</span></span> <span data-ttu-id="e72fc-129">Bunun nedeni, *nx_pop3_client_create* hizmetinin POP3 sunucusuyla TCP bağlantısı kurmaya da çalışır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-129">This is because the *nx_pop3_client_create* service also attempts to make a TCP connection with the POP3 server.</span></span> <span data-ttu-id="e72fc-130">Başarılı olursa, uygulama POP3 sunucusunu, *nx_pop3_client_mail_items_get* hizmeti kullanılarak 149 numaralı satırdaki maildrop öğesinde bulunan öğe sayısı için sorgular.</span><span class="sxs-lookup"><span data-stu-id="e72fc-130">If successful, the application queries the POP3 server for the number of items in its maildrop on line 149 using the *nx_pop3_client_mail_items_get* service.</span></span>

<span data-ttu-id="e72fc-131">Bir veya daha fazla öğe varsa, uygulama posta iletisini indirmek üzere her bir posta öğesinin while döngüsü boyunca yinelenir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-131">If there are one or more items, the application iterates through the while loop for each mail item to download the mail message.</span></span> <span data-ttu-id="e72fc-132">RETR isteği *nx_pop3_client_mail_item_get* çağrısında satır 149 ' de yapılır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-132">The RETR request is made on line 149 in the *nx_pop3_client_mail_item_get* call.</span></span> <span data-ttu-id="e72fc-133">Başarılı olursa, uygulama, 196. satırda alınan son paketi algıladığı için 177. satırdaki *nx_pop3_client_mail_item_message_get* hizmetini kullanarak paketleri indirir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-133">If successful, the application downloads packets using the *nx_pop3_client_mail_item_message_get* service on line 177 till it detects the last packet in the message has been received on line 196.</span></span> <span data-ttu-id="e72fc-134">Son olarak, uygulama posta öğesini siler, bu, *nx_pop3_client_mail_item_delete* çağrısında 199 satırında başarılı bir indirmenin gerçekleştiğini kabul ediyor.</span><span class="sxs-lookup"><span data-stu-id="e72fc-134">Lastly, the application deletes the mail item, assuming a successful download has occurred on line 199 in *the nx_pop3_client_mail_item_delete* call.</span></span> <span data-ttu-id="e72fc-135">RFC 1939, POP3 Istemcilerinin, Istemcinin maildrop ile posta biriktirmesini engellemek üzere indirilen posta öğelerini silmesini ister.</span><span class="sxs-lookup"><span data-stu-id="e72fc-135">The RFC 1939 recommends that POP3 Clients instruct the Server to delete downloaded mail items to prevent mail accumulating in the Client's maildrop.</span></span> <span data-ttu-id="e72fc-136">Sunucu yine de bunu otomatik olarak yapamayabilir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-136">The Server may automatically do so anyway.</span></span>

<span data-ttu-id="e72fc-137">Tüm posta öğeleri indirildikten veya bir POP3 Istemci hizmeti çağrısı başarısız olursa, uygulama döngüden çıkar ve *nx_pop3_client_delete* hizmeti kullanılarak 217. satırdaki POP3 istemcisini siler.</span><span class="sxs-lookup"><span data-stu-id="e72fc-137">Once all the mail items are downloaded, or if a POP3 Client service call fails, the application exits of the loop and deletes the POP3 Client on line 217 using the *nx_pop3_client_delete* service.</span></span>

```c
/*
    demo_netxduo_pop3.c

    This is a small demo of POP3 Client on the NetX TCP/IP stack.
    This demo relies on Thread, NetX and POP3 Client API to conduct
    a POP3 mail session.
*/

#include "tx_api.h"
#include "nx_api.h"
#include "nx_pop3_client.h"

#define DEMO_STACK_SIZE        4096
#define CLIENT_ADDRESS         IP_ADDRESS(192,2,2,61)
#define SERVER_ADDRESS         IP_ADDRESS(192,2,2,89)
#define SERVER_PORT            110

/* Replace the 'ram' driver with your own Ethernet driver. */
void _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Set up the POP3 Client. */

TX_THREAD          demo_client_thread;
NX_POP3_CLIENT     demo_client;
NX_PACKET_POOL     client_packet_pool;
NX_IP              client_ip;

#define PAYLOAD_SIZE 500

/* Set up Client thread entry point. */
void     demo_thread_entry(ULONG info);

/* Shared secret is the same as password. */

#define LOCALHOST              "recipient@domain.com"
#define LOCALHOST_PASSWORD     "testpwd"

/* Define main entry point. */
int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{

UINT      status;
UCHAR     *free_memory_pointer;

    /* Setup the working pointer. */
    free_memory_pointer = first_unused_memory;

    /* Create a client thread. */
    tx_thread_create(&demo_client_thread, "Client", demo_thread_entry, 0,
                    free_memory_pointer, DEMO_STACK_SIZE, 1, 1,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    free_memory_pointer = free_memory_pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* The demo client username and password is the authentication
    data used when the server attempts to authentication the client. */

    /* Create Client packet pool. */
    status = nx_packet_pool_create(&client_packet_pool,"POP3 Client Packet Pool",
                        PAYLOAD_SIZE, free_memory_pointer, (PAYLOAD_SIZE * 10));
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + (PAYLOAD_SIZE * 10);

    /* Create IP instance for demo Client */
    status = nx_ip_create(&client_ip, "POP3 Client IP Instance",
                            CLIENT_ADDRESS, 0xFFFFFF00UL, &client_packet_pool,
                            _nx_ram_network_driver, free_memory_pointer,
                            2048, 1);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* Enable ARP and supply ARP cache memory. */
    nx_arp_enable(&client_ip, (void **) free_memory_pointer, 1024);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 1024;

    /* Enable TCP and ICMP for Client IP. */
    nx_tcp_enable(&client_ip);
    nx_icmp_enable(&client_ip);

    return;
}

/* Define the application thread entry function. */

void demo_thread_entry(ULONG info)
{

UINT          status;
UINT          mail_item, number_mail_items;
UINT          bytes_downloaded = 0;
UINT          final_packet = NX_FALSE;
ULONG         total_size, mail_item_size, bytes_retrieved;
NX_PACKET     *packet_ptr;

    /* Let the IP instance get initialized with driver parameters. */
    tx_thread_sleep(40);

    /* Create a NetX POP3 Client instance with no byte or block memory pools.
    Note that it uses its password for its APOP shared secret. */
    status = nx_pop3_client_create(&demo_client,
                        NX_TRUE,
                        &client_ip, &client_packet_pool, SERVER_ADDRESS,
                        SERVER_PORT, LOCALHOST, LOCALHOST_PASSWORD);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        status = nx_pop3_client_delete(&demo_client);

        /* Abort. */
        return;
    }

    /* Find out how many items are in our mailbox. */
    status = nx_pop3_client_mail_items_get(&demo_client, &number_mail_items, &total_size);

    printf("Got %d mail items, total size%d \n", number_mail_items, total_size);

    /* If nothing in the mailbox, disconnect. */
    if (number_mail_items == 0)
    {
        nx_pop3_client_delete(&demo_client);

        return;
    }

    /* Download all mail items. */
    mail_item = 1;

    while (mail_item <= number_mail_items)
    {

        /* This submits a RETR request and gets the mail message size. */
        status = nx_pop3_client_mail_item_get(&demo_client, mail_item, &mail_item_size);

        /* Loop to get all mail message packets until the mail item is completely downloaded. */

        while((final_packet == NX_FALSE) && (status == NX_SUCCESS))
        {
            status = nx_pop3_client_mail_item_message_get(&demo_client, &packet_ptr,
                                                        &bytes_retrieved,
                                                        &final_packet);

            if (status != NX_SUCCESS)
            {
                break;
            }

            if (bytes_retrieved != 0)
            {

            printf("Received %d bytes of data for item %d: %s\n",
                    packet_ptr -> nx_packet_length,
                    mail_item, packet_ptr -> nx_packet_prepend_ptr);
            }

            nx_packet_release(packet_ptr);

            /* Determine if this is the last data packet. */
            if (final_packet)
            {
                /* It is. Let the server know it can delete this mail item. */
                status = nx_pop3_client_mail_item_delete(&demo_client, mail_item);
            }

            /* Keep track of how much mail message data is left. */
            bytes_downloaded += bytes_retrieved;
        }

        /* Get the next mail item. */
        mail_item++;

        tx_thread_sleep(100);
    }

    /* Disconnect from the POP3 server. */
    status = nx_pop3_client_quit(&demo_client);

    /* Delete the POP3 Client. This will not delete the Client packet pool. */
    status = nx_pop3_client_delete(&demo_client);

}
```

<span data-ttu-id="e72fc-138">Şekil 1.</span><span class="sxs-lookup"><span data-stu-id="e72fc-138">Figure 1.</span></span> <span data-ttu-id="e72fc-139">NetX POP3 Istemci uygulaması örneği</span><span class="sxs-lookup"><span data-stu-id="e72fc-139">Example of a NetX POP3 Client application</span></span>

## <a name="pop3-client-configuration-options"></a><span data-ttu-id="e72fc-140">POP3 Istemcisi yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="e72fc-140">POP3 Client Configuration Options</span></span>

<span data-ttu-id="e72fc-141">NetX POP3 Istemcisi ile birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-141">There are several configuration options with the NetX POP3 Client.</span></span> <span data-ttu-id="e72fc-142">Aşağıda, ayrıntılı olarak açıklanan tüm seçeneklerin bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e72fc-142">Following is a list of all options described in detail:</span></span>

- <span data-ttu-id="e72fc-143">**NX_POP3_CLIENT_PACKET_TIMEOUT**: Bu, POP3 istemcisinin bir paket ayırması için saniye cinsinden bekleme seçeneğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-143">**NX_POP3_CLIENT_PACKET_TIMEOUT**: This defines the wait option in seconds for the POP3 Client to allocate a packet.</span></span> <span data-ttu-id="e72fc-144">Varsayılan değer 1 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-144">The default value is 1 second.</span></span>

- <span data-ttu-id="e72fc-145">**NX_POP3_CLIENT_CONNECTION_TIMEOUT**: Bu, POP3 Istemcisinin POP3 sunucusuyla bağlantı kurmak için saniye cinsinden bekleme seçeneğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-145">**NX_POP3_CLIENT_CONNECTION_TIMEOUT**: This defines the wait option in seconds for the POP3 Client to connect with the POP3 Server.</span></span> <span data-ttu-id="e72fc-146">Varsayılan değer 30 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-146">The default value is 30 seconds.</span></span>

- <span data-ttu-id="e72fc-147">**NX_POP3_CLIENT_DISCONNECT_TIMEOUT**: Bu, POP3 Istemcisinin POP3 sunucusu bağlantısını kesmek için saniye cinsinden bekleme seçeneğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-147">**NX_POP3_CLIENT_DISCONNECT_TIMEOUT**: This defines the wait option in seconds for the POP3 Client to disconnect from the POP3 Server.</span></span> <span data-ttu-id="e72fc-148">Varsayılan değer 2 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-148">The default value is 2 seconds.</span></span>

- <span data-ttu-id="e72fc-149">**NX_POP3_TCP_SOCKET_SEND_WAIT**: Bu seçenek, *nx_tcp_socket_send* hizmeti çağrılarında bekle seçeneğini saniye cinsinden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-149">**NX_POP3_TCP_SOCKET_SEND_WAIT**: This option sets the wait option in seconds in *nx_tcp_socket_send* service calls.</span></span> <span data-ttu-id="e72fc-150">Varsayılan değer 2 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-150">The default value is 2 seconds.</span></span>

- <span data-ttu-id="e72fc-151">**NX_POP3_SERVER_REPLY_TIMEOUT**: Bu seçenek, istemci isteğine yanıt vermesi için *nx_tcp_socket_receive* hizmet çağrılarında bekle seçeneğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-151">**NX_POP3_SERVER_REPLY_TIMEOUT**: This option sets the wait option in *nx_tcp_socket_receive* service calls for the Server reply to a Client request.</span></span> <span data-ttu-id="e72fc-152">Varsayılan değer 10 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-152">The default value is 10 seconds.</span></span>

- <span data-ttu-id="e72fc-153">**NX_POP3_CLIENT_TCP_WINDOW_SIZE**: Bu seçenek, istemci TCP alma penceresinin boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-153">**NX_POP3_CLIENT_TCP_WINDOW_SIZE**: This option sets the size of the Client TCP receive window.</span></span> <span data-ttu-id="e72fc-154">Bu, IP örneği MTU boyutu eksi IP ve TCP üst bilgisi olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-154">This should be set to the IP instance MTU size minus the IP and TCP header.</span></span> <span data-ttu-id="e72fc-155">Varsayılan değer 1460 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e72fc-155">The default value is 1460.</span></span>

- <span data-ttu-id="e72fc-156">**NX_POP3_MAX_USERNAME**: Bu seçenek, POP3 istemci Kullanıcı adı arabelleğinin boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-156">**NX_POP3_MAX_USERNAME**: This option sets the size of the buffer of the POP3 Client user name.</span></span> <span data-ttu-id="e72fc-157">Varsayılan değer 40 bayttır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-157">The default value is 40 bytes.</span></span>

- <span data-ttu-id="e72fc-158">**NX_POP3_MAX_PASSWORD**: Bu seçenek, POP3 istemci parolasının arabellek boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e72fc-158">**NX_POP3_MAX_PASSWORD**: This option sets the size of the buffer of the POP3 Client password.</span></span> <span data-ttu-id="e72fc-159">Varsayılan değer 20 bayttır.</span><span class="sxs-lookup"><span data-stu-id="e72fc-159">The default value is 20 bytes.</span></span>