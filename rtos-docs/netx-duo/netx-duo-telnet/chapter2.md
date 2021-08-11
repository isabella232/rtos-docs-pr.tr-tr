---
title: Bölüm 2-Azure RTOS NetX Duo Telnet yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX Duo Telnet bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4781f45dc37f8c48a9f491d6cb67299432f3ae6743d12d9d92134298474182a5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799362"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-telnet"></a>Bölüm 2-Azure RTOS NetX Duo Telnet yüklemesi ve kullanımı

Bu bölümde, Azure RTOS NetX Duo Telnet bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX Duo Telnet paketini adresinden bulabilirsiniz <https://github.com/azure-rtos/netxduo> . Paket aşağıdaki dosyaları içerir:

- **nxd_telnet_client. h**: NETX Duo Için Telnet istemcisi üst bilgi dosyası
- **nxd_telnet_client. c**: NETX Duo Için Telnet istemcisi Için c kaynak dosyası
- **nxd_telnet_server. h**: NETX Duo Için Telnet sunucusu üst bilgi dosyası
- **nxd_telnet_server. c**: NETX Duo Için Telnet sunucusu Için c kaynak dosyası
- **nxd_telnet.pdf**: NETX Duo için Telnet 'in PDF açıklaması
- **demo_netxduo_telnet. c**: NETX Duo Telnet tanıtımı

## <a name="telnet-installation"></a>Telnet yüklemesi

NetX Duo için Telnet kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_telnet_client. h*, *nxd_telnet_client. c*, *nxd_telnet_server. c ve nxd_telnet_server. h* dosyalarının bu dizine kopyalanması gerekir.

## <a name="using-telnet"></a>Telnet kullanma

NetX Duo için Telnet kullanmak kolaydır. Temel olarak, uygulama kodu için nxd_telnet_server. h ve, ThreadX ve NetX Duo kullanmak için *tx_api. h* ve *nx_api. h* dahil olmak üzere, telnet istemci uygulamalarına yönelik *.* h ve *nxd_telnet_client.* h içermelidir. *Üstbilgi* eklendikten sonra, uygulama kodu bu kılavuzda daha sonra belirtilen Telnet işlev çağrılarını yapabilir. Uygulama ayrıca yapı işlemine *nxd_telnet_client. c* ve *nxd_telnet_server. c* içermelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX Duo Telnet 'i kullanmak için gereklidir.

Hiçbir Telnet Istemci özelliği gerekmiyorsa, *nxd_telnet_client. c* dosyası atlanabilir.

Telnet 'in NetX Duo TCP hizmetlerini kullandığından, Telnet kullanılmadan önce *nx_tcp_enable* çağrısıyla TCP 'nin etkinleştirilmesi gerektiğini de unutmayın.

## <a name="small-example-system"></a>Küçük örnek sistem

NetX Duo Telnet 'in nasıl kullanılacağına ilişkin bir örnek aşağıda şekil 1,1 ' de gösterilmiştir. Bu örnekte, Telnet içerme dosyaları, 7. ve 8. *satırda getirilir.* Ardından, Telnet sunucusu 146 satırındaki "*tx_application_define*" içinde oluşturulur. Telnet sunucusunun ve Istemci denetim bloklarının daha önce satır 23-24 ' de genel değişkenler olarak tanımlandığını unutmayın.

Telnet sunucusu veya Istemcisinin başlatılması için önce, IP adreslerini NetX Duo ile doğrulaması gerekir. IPv4 bağlantıları için bu, yalnızca NetX sürücüsünün 166. satırda sistemi başlatmasını sağlamak için kısa bir süre bekledikten sonra gerçekleştirilir. IPv6 bağlantıları için, bu, 171-172. satırlarda yaptığı IPv6 ve ICMPv6 'nın etkinleştirilmesini gerektirir. Istemci, birincil arabirimdeki genel ve bağlantı yerel IPv6 adreslerini, 181-186 satırları üzerinde ayarlar ve NetX Duo doğrulamasının arka planda tamamlanmasını bekler. Sunucu, birincil arabirimindeki genel ve bağlantı yerel adreslerini 192 – 198 satırlarında de ayarlar. *Nxd_ipv6_global_address_set* ve *nxd_ipv6_linklocal_address_set* iki hizmetin *nxd_ipv6_address_set hizmeti* ile değiştirildiğini unutmayın. Eski iki hizmet, eski NetX Duo uygulamaları için hala kullanılabilir ancak sonunda kullanım dışıdır. Geliştiricilerin bunun yerine *nxd_ipv6_address_set* kullanması önerilir.

NetX Duo ile başarılı IP adresi doğrulamasından sonra, Telnet sunucusu, *nxd_telnet_server_start* hizmeti kullanılarak 215. satırda başlatılır. 226. satırda Telnet Istemcisi *nx_telnet_client_create* hizmeti kullanılarak oluşturulur. Ardından, sırasıyla *nxd_telnet_client_connect* ve *Nx_telnet_client_connect* hizmetlerini kullanarak IPv4 uygulamaları ve ıpv6 uygulamaları için satır 238 242 ' de Telnet sunucusuyla bağlantı kurar. Sunucuyla başarılı bir şekilde doğrulama ve bağlantı kurulduktan sonra, bağlantısını kesmeden önce birkaç değişim yapar.

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

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX Duo için Telnet oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Bu #defines, *nxd_telnet_server. h*. ve *nxd_telnet_client. h* 'a dahil etmeden önce uygulama tarafından ayarlanabilir.

Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:  
  
- **NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel Telnet hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.
- **NX_TELNET_MAX_CLIENTS**: sunucu iş parçacığı tarafından desteklenen en fazla Telnet istemcisi sayısı. Varsayılan olarak, bu değer, aynı anda en fazla 4 istemci belirtmek için 4 olarak tanımlanır.
- **NX_TELNET_SERVER_PRIORITY**: Telnet sunucusu iş parçacığının önceliği. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.
- **NX_TELNET_TOS**: Telnet TCP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer NX_IP_NORMAL belirtmek için olarak tanımlanır  
normal IP paket hizmeti.
- **NX_TELNET_FRAGMENT_OPTION**: Telnet TCP istekleri için parça etkinleştirilir. Varsayılan olarak, bu değer Telnet TCP fragmenting ' ı devre dışı bırakmak için NX_DONT_FRAGMENT.
- **NX_TELNET_SERVER_WINDOW_SIZE**: sunucu yuvası pencere boyutu. Varsayılan olarak, bu değer 2048 bayttır.
- **NX_TELNET_TIME_TO_LIVE**: Bu paketin atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır.
- **NX_TELNET_SERVER_TIMEOUT**: iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 10 saniyeye ayarlanır.
- **NX_TELNET_ACTIVITY_TIMEOUT**: sunucu istemci bağlantısının bağlantısını kesmeden önce herhangi bir etkinlik olmadan geçebilecek saniye sayısını belirtir. Varsayılan değer 600 saniyeye ayarlanır.
- **NX_TELNET_TIMEOUT_PERIOD**: istemci etkinlik zaman aşımları için denetim arasındaki saniye sayısını belirtir. Varsayılan değer 60 saniyeye ayarlanır.
- **NX_TELNET_SERVER_OPTION_DISABLE**: tanımlı, Telnet seçeneği anlaşması devre dışı bırakıldı. Varsayılan olarak bu seçenek tanımlı değildir.
- **NX_TELNET_SERVER_USER_CREATE_PACKET_POOL**: tanımlanmışsa, Telnet sunucusu paket havuzunun dışarıdan oluşturulması gerekir. Bu yalnızca NX_TELNET_SERVER_OPTION_DISABLE tanımlıysa anlamlıdır. Varsayılan olarak, bu seçenek tanımlı değildir ve Telnet sunucusu iş parçacığı kendi paket havuzunu oluşturur.
- **NX_TELNET_SERVER_PACKET_PAYLOAD**: seçenek anlaşması Için Telnet sunucusu tarafından oluşturulan paket yükünün boyutunu tanımlar. Telnet sunucusunun yalnızca NX_TELNET_SERVER _OPTION_DISABLE tanımlanmamışsa Bu paket havuzunu oluşturduğunu unutmayın (Telnet seçenekleri etkinleştirilir). Bu seçeneğin varsayılan değeri 300 ' dir.
- **NX_TELNET_SERVER_PACKET_POOL_SIZE**: Telnet anlaşmaları Için kullanılan Telnet sunucusu paket havuzunun boyutunu tanımlar. Telnet sunucusunun yalnızca NX_TELNET_SERVER _OPTION_DISABLE tanımlanmamışsa Bu paket havuzunu oluşturduğunu unutmayın (Telnet seçenekleri etkinleştirilir). Bu seçeneğin varsayılan değeri 2048 ' dir ( \~ 5-6 paketleri).
