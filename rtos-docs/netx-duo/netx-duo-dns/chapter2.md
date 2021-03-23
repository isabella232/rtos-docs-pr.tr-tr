---
title: Bölüm 2-Azure RTOS NetX Duo DNS Istemcisini yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX Duo DNS Istemcisinin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 75b85829f80462015d66e1623b880d5139349ce0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826999"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-dns-client"></a>Bölüm 2-Azure RTOS NetX Duo DNS Istemcisini yükleme ve kullanma

Bu bölümde, Azure RTOS NetX Duo DNS Istemcisinin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX Duo DNS Istemcisi adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nxd_dns. h** NetX Duo DNS Istemcisi için üst bilgi dosyası
- **nxd_dns. c** NetX Duo DNS Istemcisi için C kaynak dosyası
- **nxd_dns.pdf** NetX Duo DNS Istemcisinin PDF açıklaması

## <a name="dns-client-installation"></a>DNS Istemcisi yüklemesi

NetX Duo DNS Istemcisini kullanmak için, *nxd_dns. c* ve *nxd_dns. h* kaynak kodu dosyalarını NETX Duo 'un yüklü olduğu dizine kopyalayın. Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_dns. h* ve *nxd_dns. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-the-dns-client"></a>DNS Istemcisini kullanma

NetX Duo DNS Istemcisini kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX Duo kullanmak için *tx_api. h* ve *nx_api. h* dahil *nxd_dns.* h içermelidir. *Nxd_dns. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen DNS işlev çağrılarını yapabilir. Uygulamanın yapı işlemine *nxd_dns. c* eklemesi de gerekir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX Duo DNS 'i kullanmak için gereklidir.

> [!NOTE]
> DNS, NetX Duo UDP hizmetlerini kullandığından, DNS kullanılmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerekir.

## <a name="small-example-system-for-netx-duo-dns-client"></a>NetX Duo DNS Istemcisi için küçük örnek sistem 

NetX Duo DNS Istemcisi, mevcut NetX DNS uygulamalarıyla uyumludur. Eski hizmetlerin listesi ve NetX Duo eşdeğeri aşağıda gösterilmiştir:

| NetX DNS API hizmeti (yalnızca IPv4) | NetX Duo DNS API hizmeti (IPv4 ve IPv6 desteklenir) |
|----------------------------------|----------------------------------------------------|
| nx_dns_host_by_name_get          | nxd_dns_host_by_name_get                           |
| nx_dns_host_by_address_get       | nxd_dns_host_by_address_get                        |
| nx_dns_server_get                | nxd_dns_server_get                                 |
| nx_dns_server_add                | nxd_dns_server_add                                 |
| nx_dns_server_remove             | nxd_dns_server_remove                              |

Daha fazla ayrıntı için, Bölüm 3 ' teki NetX Duo DNS Istemcisi API hizmetlerinin açıklamasına bakın.

Bu bölümde sağlanan örnek DNS uygulama programında, *nxd_dns. h* , 6. satırda bulunur. DNS istemcisi uygulamasının DNS Istemcisi için paket havuzu oluşturmasına izin veren NX_DNS_CLIENT_USER_CREATE_PACKET_POOL, 24-26 satırlarında bildirilmiştir. Bu paket havuzu, DNS iletileri göndermek için paket ayırmak üzere kullanılır. NX_DNS_CLIENT_USER_CREATE_PACKET_POOL tanımlanmışsa, 78-98 satırlarında bir paket havuzu oluşturulur. Bu seçenek etkinleştirilmemişse, DNS Istemcisi, paket yükünün ve havuz boyutunun, *nxd_dns. h* içinde yapılandırma parametreleri tarafından ayarlanan ve bu bölümün başka bir yerinde açıklandığı şekilde kendi paket havuzunu oluşturur.

İç NetX Duo işlemleri için kullanılan Istemci IP örneği için 100-112 satırlarında başka bir paket havuzu oluşturulur. Daha sonra, 115 satırındaki *nx_ip_create* ÇAĞRıSı kullanılarak IP örneği oluşturulur. IP görevinin ve DNS Istemcisinin aynı paket havuzunu paylaşması mümkündür, ancak DNS Istemcisi genellikle IP görevi tarafından gönderilen denetim paketlerinden daha büyük iletiler gönderdiğinden, ayrı paket havuzlarının kullanılması belleğin daha verimli bir şekilde kullanılmasını sağlar.

ARP ve UDP (IPv4 ağları tarafından kullanılır) sırasıyla 129 ve 141 satırlarında etkindir.

>[!NOTE]
> Bu demo, 44 satırında belirtilen ve *nx_ip_create* çağrısında kullanılan ' RAM ' sürücüsünü kullanır. Bu RAM sürücüsü NetX Duo kaynak kodu ile dağıtılır. DNS Istemcisini gerçekten çalıştırmak için, uygulamanın DNS sunucusundan paket iletmek ve almak için gerçek fiziksel ağ sürücüsü sağlaması gerekir.

*Thread_client_entry* istemci iş parçacığı girişi işlevi *tx_application_define* işlevinin altında tanımlanmıştır. İlk olarak, IP görevi iş parçacığının ağ sürücüsü tarafından başlatılmasına izin vermek için sisteme denetimi yeniden denetler.

Daha sonra, satır 257 ' de DNS Istemcisini oluşturur, 267-278. satırdaki DNS önbelleğini başlatır ve daha önce oluşturulmuş olan paket havuzunu, satırlarda 281-295 olan DNS Istemci örneğine ayarlar. Ardından 297-341 satırlarına DNS sunucusu ekler.

Örnek programın geri kalanı DNS sorguları yapmak için DNS Istemci hizmetlerini kullanır. Ana bilgisayar IP adresi aramaları 193 ve 207 satırlarında gerçekleştirilir. Bu iki hizmet arasındaki fark *nxd_dns_host_by_name_get* ve *nx_dns_host_by_name_get*, daha önce adres verilerini bir NXD_ADDRESS veri türüne kaydettiğinden, ıkıncı, verileri bir ULONG veri türüne kaydettiğinden. İkincisi, IPv4 ağları ile sınırlıdır, ancak ilki IPv6 veya IPv4 ağlarla birlikte kullanılabilir. Bu yalnızca IP örneği IPv6 için etkinleştirildiğinde mümkündür. IPv6 ağı için IP örneğini etkinleştirme hakkında daha fazla bilgi için bkz. NetX Duo Kullanıcı Kılavuzu.

Ana bilgisayar IP adresi aramaları için başka bir hizmet, *nx_dns_ipv4_address_by_name_get* satır 464 ' de gösterilmiştir. Bu hizmet, DNS sunucusu yanıtında yalnızca ilk adresin değil, etki alanı adı için bulunan IPv4 adreslerinin tümünü (veya sağlanan arabelleğe sığar) döndüren *nx_dns_host_by_name_get* farklıdır.

Benzer şekilde, satır 380 ' de çağrılan *nxd_dns_ipv6_address_by_name_get* hizmeti, yalnızca ilki DEĞIL, DNS istemcisi tarafından bulunan tüm IPv6 adreslerini döndürür.

Ters aramalar (IP adresinden ana bilgisayar adı) 606 (*nx_dns_host_by_address_get*) satırları üzerinde ve 564 ve 588 (*nxd_dns_host_by_address_get*) üzerinde bir kez gerçekleştirilir. *nx_dns_host_by_address_get* yalnızca IPv4 ağlarında çalışır, ancak *Nxd_dns_host_by_address_get* IPv4 veya IPv6 AĞLARıNDA (örn. IP örneği IPv6 için, IPv4 ağları için de etkindir) çalışır.

DNS aramaları, CNAME ve TXT için iki diğer hizmet, giriş etki alanı adı için CNAME ve etki alanı adı verilerini bulacak şekilde sırasıyla 627 ve 649 satırlarında gösterilmiştir. NetX Duo DNS Istemcisi diğer kayıt türleri için benzer hizmetler (örneğin, MX, NS, SRV ve SOA) olarak. NetX Duo DNS Istemcisinde bulunan tüm kayıt türü aramalarının ayrıntılı açıklamaları için bkz. Bölüm 3.

*Nx_dns_delete* hizmeti kullanılarak, 846. satırdaki DNS istemcisi silindiğinde, DNS istemcisi kendi paket havuzunu oluşturmadığı takdirde DNS istemcisi için paket havuzu silinmez. Aksi takdirde, bu uygulama için daha fazla kullanım yoksa, paket havuzunu silmek uygulamaya çalışır.

```C
/* This is a small demo of DNS Client for the high-performance NetX TCP/IP stack. */

#include   "tx_api.h"
#include   "nx_api.h"
#include   "nx_udp.h"
#include   "nxd_dns.h"

#ifdef FEATURE_NX_IPV6
#include   "nx_ipv6.h"
#endif

#define     DEMO_STACK_SIZE         4096

#define     NX_PACKET_PAYLOAD       1536
#define     NX_PACKET_POOL_SIZE     30 * NX_PACKET_PAYLOAD
#define     LOCAL_CACHE_SIZE        2048

/* Define the ThreadX and NetX object control blocks... */

NX_DNS                  client_dns;
TX_THREAD               client_thread;
NX_IP                   client_ip;
NX_PACKET_POOL          main_pool;
#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL
NX_PACKET_POOL          client_pool;
#endif
UCHAR                   local_cache[LOCAL_CACHE_SIZE];

UINT                    error_counter = 0;

#ifdef FEATURE_NX_IPV6
/* If IPv6 is enabled in NetX Duo, allow DNS Client to try using IPv6 */
//#define USE_IPV6
#endif

#define CLIENT_ADDRESS      IP_ADDRESS(192,168,0,11)
#define DNS_SERVER_ADDRESS  IP_ADDRESS(192,168,0,1)

/* Define thread prototypes. */

void    thread_client_entry(ULONG thread_input);

/***** Substitute your ethernet driver entry function here *********/
extern  VOID _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Define main entry point. */

int main()
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

    /* Create the main thread. */
    tx_thread_create(&client_thread, "Client thread", thread_client_entry, 0,
            pointer, DEMO_STACK_SIZE, 4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL

    /* Create the packet pool for the DNS Client to send packets.

        If the DNS Client is configured for letting the host application create
        the DNS packet pool, (see NX_DNS_CLIENT_USER_CREATE_PACKET_POOL option), see
       nx_dns_create() for guidelines on packet payload size and pool size.
       packet traffic for NetX processes.
    */
    status =  nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", NX_DNS_PACKET_PAYLOAD, pointer, NX_DNS_PACKET_POOL_SIZE);

    pointer = pointer + NX_DNS_PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {

        error_counter++;
        return;
     }
#endif
     /* Create the packet pool which the IP task will use to send packets. Also available to the host
       application to send packet. */
    status =  nx_packet_pool_create(&main_pool, "Main Packet Pool", NX_PACKET_PAYLOAD, pointer, NX_PACKET_POOL_SIZE);

    pointer = pointer + NX_PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {

        error_counter++;
        return;
     }

    /* Create an IP instance for the DNS Client. */
    status = nx_ip_create(&client_ip, "DNS Client IP Instance", CLIENT_ADDRESS, 0xFFFFFF00UL,
                          &main_pool, _nx_ram_network_driver, pointer, 2048, 1);

    pointer =  pointer + 2048;

    /* Check for IP create errors. */
    if (status)
    {

        error_counter++;
        return;
     }

    /* Enable ARP and supply ARP cache memory for the DNS Client IP. */
    status =  nx_arp_enable(&client_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors. */
    if (status)
    {

        error_counter++;
        return;
     }

    /* Enable UDP traffic because DNS is a UDP based protocol. */
    status =  nx_udp_enable(&client_ip);

    /* Check for UDP enable errors. */
    if (status)
    {

        error_counter++;
        return;
     }
}

#define BUFFER_SIZE     200
#define RECORD_COUNT    10

/* Define the Client thread. */

void    thread_client_entry(ULONG thread_input)
{

UCHAR           record_buffer[200];
UINT            record_count;
UINT            status;
ULONG           host_ip_address;
#ifdef FEATURE_NX_IPV6
NXD_ADDRESS     host_ipduo_address;
NXD_ADDRESS     test_ipduo_server_address;
#ifdef USE_IPV6
NXD_ADDRESS     client_ipv6_address;
NXD_ADDRESS     dns_ipv6_server_address;
UINT            iface_index, address_index;
#endif
#endif
UINT            i;
ULONG           *ipv4_address_ptr[RECORD_COUNT];
NX_DNS_IPV6_ADDRESS
                *ipv6_address_ptr[RECORD_COUNT];
#ifdef NX_DNS_ENABLE_EXTENDED_RR_TYPES
NX_DNS_NS_ENTRY
                *nx_dns_ns_entry_ptr[RECORD_COUNT];
NX_DNS_MX_ENTRY
                *nx_dns_mx_entry_ptr[RECORD_COUNT];
NX_DNS_SRV_ENTRY
                *nx_dns_srv_entry_ptr[RECORD_COUNT];
NX_DNS_SOA_ENTRY
                *nx_dns_soa_entry_ptr;
ULONG           host_address;
USHORT          host_port;
#endif

    /* Give NetX IP task a chance to get initialized . */
    tx_thread_sleep(100);

#ifdef FEATURE_NX_IPV6
#ifdef USE_IPV6

    /* Make the DNS Client IPv6 enabled. */
    status = nxd_ipv6_enable(&client_ip);

    /* Check for enable errors. */
    if (status)
    {

        error_counter++;
        return;
     }
    status = nxd_icmp_enable(&client_ip);

    /* Check for enable errors. */
    if (status)
    {

        error_counter++;
        return;
    }

    client_ipv6_address.nxd_ip_address.v6[3] = 0x101;
    client_ipv6_address.nxd_ip_address.v6[2] = 0x0;
    client_ipv6_address.nxd_ip_address.v6[1] = 0x0000f101;
    client_ipv6_address.nxd_ip_address.v6[0] = 0x20010db8;
    client_ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;


     /* Set the link local address with the host MAC address. */
    iface_index = 0;

    /* This assumes we are using the primary network interface (index 0). */
    status = nxd_ipv6_address_set(&client_ip, iface_index, NX_NULL, 10, &address_index);

    /* Check for link local address set error. */
    if (status)
    {

        error_counter++;
        return;
     }

    /* Set the host global IP address. We are assuming a 64
       bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&client_ip, iface_index, &client_ipv6_address, 64, &address_index);

    /* Check for global address set error. */
    if (status)
    {

        error_counter++;
        return;
     }

    /* Wait while NetX Duo validates the link local and global address. */
    tx_thread_sleep(500);
#endif
#endif

    /* Create a DNS instance for the Client. Note this function will create
       the DNS Client packet pool for creating DNS message packets intended
       for querying its DNS server. */
    status =  nx_dns_create(&client_dns, &client_ip, (UCHAR *)"DNS Client");

    /* Check for DNS create error. */
    if (status)
    {

        error_counter++;
        return;
     }

#ifdef NX_DNS_CACHE_ENABLE
    /* Initialize the cache. */
    status = nx_dns_cache_initialize(&client_dns, local_cache, LOCAL_CACHE_SIZE);

    /* Check for DNS cache error. */
    if (status)
    {

        error_counter++;
        return;
     }
#endif

    /* Is the DNS client configured for the host application to create the pecket pool? */
#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL

    /* Yes, use the packet pool created above which has appropriate payload size
       for DNS messages. */
     status = nx_dns_packet_pool_set(&client_dns, &client_pool);

     /* Check for set DNS packet pool error. */
     if (status)
     {

         error_counter++;
         return;
      }

#endif /* NX_DNS_CLIENT_USER_CREATE_PACKET_POOL */

#ifdef FEATURE_NX_IPV6
#ifdef USE_IPV6

    /* Add an IPv6 DNS server to the DNS client. */
    dns_ipv6_server_address.nxd_ip_address.v6[3] = 0x106;
    dns_ipv6_server_address.nxd_ip_address.v6[2] = 0x0;
    dns_ipv6_server_address.nxd_ip_address.v6[1] = 0x0000f101;
    dns_ipv6_server_address.nxd_ip_address.v6[0] = 0x20010db8;
    dns_ipv6_server_address.nxd_ip_version = NX_IP_VERSION_V6;

    status = nxd_dns_server_add(&client_dns, &dns_ipv6_server_address);

    /* Check for DNS add server error. */
    if (status)
    {

        error_counter++;
        return;
     }
#else

    /* Add an IPv4 server address to the Client list. */
    status = nx_dns_server_add(&client_dns, DNS_SERVER_ADDRESS);

    /* Check for DNS add server error. */
    if (status)
    {

        error_counter++;
        return;
     }
#endif
#else

    /* Add an IPv4 server address to the Client list. */
    status = nx_dns_server_add(&client_dns, DNS_SERVER_ADDRESS);

    /* Check for DNS add server error. */
    if (status)
    {

        error_counter++;
        return;
     }
#endif


/********************************************************************************/
/*                                  Type AAAA                                   */
/*     Send AAAA type DNS Query to its DNS server and get the IPv6 address. */
/********************************************************************************/
#ifdef FEATURE_NX_IPV6

    /* Send a DNS Client name query. Indicate the Client expects an IPv6 address (containing an AAAA record). The DNS
       Client will send AAAA type query to its DNS server. */
    status = nxd_dns_host_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &host_ipduo_address, 400, NX_IP_VERSION_V6);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test AAAA: \n");

        printf("IP address: %x:%x:%x:%x:%x:%x:%x:%x\n",
            (UINT)host_ipduo_address.nxd_ip_address.v6[0]  >>16 & 0xFFFF,
            (UINT)host_ipduo_address.nxd_ip_address.v6[0]  & 0xFFFF,
            (UINT)host_ipduo_address.nxd_ip_address.v6[1]  >>16 & 0xFFFF,
            (UINT)host_ipduo_address.nxd_ip_address.v6[1]  & 0xFFFF,
            (UINT)host_ipduo_address.nxd_ip_address.v6[2]  >>16 & 0xFFFF,
            (UINT)host_ipduo_address.nxd_ip_address.v6[2]  & 0xFFFF,
            (UINT)host_ipduo_address.nxd_ip_address.v6[3]  >>16 & 0xFFFF,
            (UINT)host_ipduo_address.nxd_ip_address.v6[3]  & 0xFFFF);
    }

#endif

    /* Look up IPv6 addresses(AAAA TYPE) to record multiple IPv6 addresses in record_buffer and return the IPv6 address count. */
    status = nxd_dns_ipv6_address_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, &record_count, 400);

    /* Check for DNS add server error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test AAAA: ");
        printf("record_count = %d \n", record_count);
    }

    /* Get the IPv6 addresses of host. */
    for(i =0; i< record_count; i++)
    {
        ipv6_address_ptr[i] = (NX_DNS_IPV6_ADDRESS *)(record_buffer + i * sizeof(NX_DNS_IPV6_ADDRESS));

        printf("record %d: IP address: %x:%x:%x:%x:%x:%x:%x:%x\n", i,
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[0]  >>16 & 0xFFFF),
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[0]  & 0xFFFF),
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[1]  >>16 & 0xFFFF),
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[1]  & 0xFFFF),
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[2]  >>16 & 0xFFFF),
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[2]  & 0xFFFF),
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[3]  >>16 & 0xFFFF),
                (UINT)(ipv6_address_ptr[i] -> ipv6_address[3]  & 0xFFFF));
    }


/********************************************************************************/
/*                                  Type A                                      */
/*       Send A type DNS Query to its DNS server and get the IPv4 address. */
/********************************************************************************/
#ifdef FEATURE_NX_IPV6
    /* Send a DNS Client name query. Indicate the Client expects an IPv4 address (containing an A record). If the DNS client
       is using an IPv6 DNS server it will send this query over IPv6; otherwise it will be sent over IPv4. */
    status = nxd_dns_host_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &host_ipduo_address, 400, NX_IP_VERSION_V4);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {

        printf("------------------------------------------------------\n");
        printf("Test A: \n");
        printf("IP address: %lu.%lu.%lu.%lu\n",
              host_ipduo_address.nxd_ip_address.v4 >> 24,
              host_ipduo_address.nxd_ip_address.v4 >> 16 & 0xFF,
              host_ipduo_address.nxd_ip_address.v4 >> 8 & 0xFF,
              host_ipduo_address.nxd_ip_address.v4 & 0xFF);
    }

#endif

    /* Look up an IPv4 address over IPv4. */
    status = nx_dns_host_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &host_ip_address, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test A: \n");
        printf("IP address: %lu.%lu.%lu.%lu\n",
        host_ip_address >> 24,
        host_ip_address >> 16 & 0xFF,
        host_ip_address >> 8 & 0xFF,
        host_ip_address & 0xFF);
    }


    /* Look up IPv4 addresses to record multiple IPv4 addresses in record_buffer and return the IPv4 address count. */
    status = nx_dns_ipv4_address_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, &record_count, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test A: ");
        printf("record_count = %d \n", record_count);
    }

    /* Get the IPv4 addresses of host. */
    for(i =0; i< record_count; i++)
    {
        ipv4_address_ptr[i] = (ULONG *)(record_buffer + i * sizeof(ULONG));
        printf("record %d: IP address: %lu.%lu.%lu.%lu\n", i,
                *ipv4_address_ptr[i] >> 24,
                *ipv4_address_ptr[i] >> 16 & 0xFF,
                *ipv4_address_ptr[i] >> 8 & 0xFF,
                *ipv4_address_ptr[i] & 0xFF);
    }


/********************************************************************************/
/*                                  Type A + CNAME response                     */
/*       Send A type DNS Query to its DNS server and get the IPv4 address. */
/********************************************************************************/
    /* Look up an IPv4 address over IPv4. */
    status = nx_dns_host_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &host_ip_address, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test A + CNAME response: \n");
        printf("IP address: %lu.%lu.%lu.%lu\n",
        host_ip_address >> 24,
        host_ip_address >> 16 & 0xFF,
        host_ip_address >> 8 & 0xFF,
        host_ip_address & 0xFF);
    }


    /* Look up IPv4 addresses to record multiple IPv4 addresses in record_buffer and return the IPv4 address count. */
    status = nx_dns_ipv4_address_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, &record_count, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test Test A + CNAME response: ");
        printf("record_count = %d \n", record_count);
    }

    /* Get the IPv4 addresses of host. */
    for(i =0; i< record_count; i++)
    {
        ipv4_address_ptr[i] = (ULONG *)(record_buffer + i * sizeof(ULONG));
        printf("record %d: IP address: %lu.%lu.%lu.%lu\n", i,
                *ipv4_address_ptr[i] >> 24,
                *ipv4_address_ptr[i] >> 16 & 0xFF,
                *ipv4_address_ptr[i] >> 8 & 0xFF,
                *ipv4_address_ptr[i] & 0xFF);
    }


/********************************************************************************/
/*                                  Type PTR                                    */
/*       Send PTR type DNS Query to its DNS server and get the host name. */
/********************************************************************************/

#ifdef FEATURE_NX_IPV6

    /* Look up a host name from an IPv6 address (reverse lookup). */

    /* Create an IPv6 address for a reverse lookup. */
    test_ipduo_server_address.nxd_ip_version = NX_IP_VERSION_V6;
    test_ipduo_server_address.nxd_ip_address.v6[0] = 0x24046800;
    test_ipduo_server_address.nxd_ip_address.v6[1] = 0x40050c00;
    test_ipduo_server_address.nxd_ip_address.v6[2] = 0x00000000;
    test_ipduo_server_address.nxd_ip_address.v6[3] = 0x00000065;

    /* This will be sent over IPv6 to the DNS server who should return a PTR record if it can find the information. */
    status = nxd_dns_host_by_address_get(&client_dns, &test_ipduo_server_address, &record_buffer[0], BUFFER_SIZE, 450);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test PTR: %s\n", record_buffer);
    }
#endif

#ifdef FEATURE_NX_IPV6

    /* Create an IPv4 address for the reverse lookup. If the DNS client is IPv6 enabled, it will send this over
       IPv6 to the DNS server; otherwise it will send it over IPv4. In either case the respective server will
       return a PTR record if it has the information. */
    test_ipduo_server_address.nxd_ip_version = NX_IP_VERSION_V4;
    test_ipduo_server_address.nxd_ip_address.v4 = IP_ADDRESS(74, 125, 71, 106);

    status = nxd_dns_host_by_address_get(&client_dns, &test_ipduo_server_address, &record_buffer[0], BUFFER_SIZE, 450);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test PTR: %s\n", record_buffer);
    }
#endif

     /* Look up host name over IPv4. */
     host_ip_address = IP_ADDRESS(74, 125, 71, 106);
     status = nx_dns_host_by_address_get(&client_dns, host_ip_address, &record_buffer[0], BUFFER_SIZE, 450);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {
        printf("------------------------------------------------------\n");
        printf("Test PTR: %s\n", record_buffer);
    }

#ifdef NX_DNS_ENABLE_EXTENDED_RR_TYPES
/********************************************************************************/
/*                                  Type CNAME                                  */
/*   Send CNAME type DNS Query to its DNS server and get the canonical name . */
/********************************************************************************/

     /* Send CNAME type to record the canonical name of host in record_buffer. */
     status = nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, 400);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test CNAME: %s\n", record_buffer);
    }


/********************************************************************************/
/*                                  Type TXT                                    */
/*      Send TXT type DNS Query to its DNS server and get descriptive text. */
/********************************************************************************/

     /* Send TXT type to record the descriptive test of host in record_buffer. */
     status = nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, 400);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test TXT: %s\n", record_buffer);
    }


/********************************************************************************/
/*                                  Type NS                                     */
/*   Send NS type DNS Query to its DNS server and get the domain name server. */
/********************************************************************************/

     /* Send NS type to record multiple name servers in record_buffer and return the name server count.
        If the DNS response includes the IPv4 addresses of name server, record it similarly in record_buffer. */
     status = nx_dns_domain_name_server_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, &record_count, 400);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test NS: ");
        printf("record_count = %d \n", record_count);
    }

    /* Get the name server. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)(record_buffer + i * sizeof(NX_DNS_NS_ENTRY));

        printf("record %d: IP address: %d.%d.%d.%d\n", i,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address  >> 24,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 16 & 0xFF,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 8 & 0xFF,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address & 0xFF);
        if(nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr)
            printf("hostname = %s\n", nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr);
        else
            printf("hostname is not set\n");
    }

/********************************************************************************/
/*                                  Type MX                                     */
/*   Send MX type DNS Query to its DNS server and get the domain mail exchange. */
/********************************************************************************/

     /* Send MX DNS query type to record multiple mail exchanges in record_buffer and return the mail exchange count.
        If the DNS response includes the IPv4 addresses of mail exchange, record it similarly in record_buffer. */
     status = nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, &record_count, 400);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test MX: ");
        printf("record_count = %d \n", record_count);
    }

    /* Get the mail exchange. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_mx_entry_ptr[i] = (NX_DNS_MX_ENTRY *)(record_buffer + i * sizeof(NX_DNS_MX_ENTRY));

        printf("record %d: IP address: %d.%d.%d.%d\n", i,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 24,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 16 & 0xFF,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 8 & 0xFF,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address & 0xFF);
        printf("preference = %d \n ", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_preference);
        if(nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr)
            printf("hostname = %s\n", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr);
        else
            printf("hostname is not set\n");
    }

/********************************************************************************/
/*                                  Type SRV                                    */
/*  Send SRV type DNS Query to its DNS server and get the location of services. */
/********************************************************************************/

     /* Send SRV DNS query type to record the location of services in record_buffer and return count.
        If the DNS response includes the IPv4 addresses of service name, record it similarly in record_buffer. */
     status = nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, &record_count, 400);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test SRV: ");
        printf("record_count = %d \n", record_count);
    }

    /* Get the location of services. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)(record_buffer + i * sizeof(NX_DNS_SRV_ENTRY));

        printf("record %d: IP address: %d.%d.%d.%d\n", i,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 24,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 16 & 0xFF,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 8 & 0xFF,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address & 0xFF);
        printf("port number = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_port_number );
        printf("priority = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_priority );
        printf("weight = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_weight );
        if(nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr)
            printf("hostname = %s\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr);
        else
            printf("hostname is not set\n");
    }

    /* Get the service info, NetX old API.*/
    status = nx_dns_info_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &host_address, &host_port, 200);

    /* Check for DNS add server error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

    else
    {

        printf("------------------------------------------------------\n");
        printf("Test SRV: ");
        printf("IP address: %d.%d.%d.%d\n",
                host_address >> 24,
                host_address >> 16 & 0xFF,
                host_address >> 8 & 0xFF,
                host_address & 0xFF);
        printf("port number = %d\n", host_port);
    }

/********************************************************************************/
/*                                  Type SOA                                    */
/* Send SOA type DNS Query to its DNS server and get zone of start of authority.*/
/********************************************************************************/

     /* Send SOA DNS query type to record the zone of start of authority in record_buffer. */
     status = nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, 400);

     /* Check for DNS query error. */
     if (status != NX_SUCCESS)
     {
         error_counter++;
     }

     /* Get the loc*/
     nx_dns_soa_entry_ptr = (NX_DNS_SOA_ENTRY *) record_buffer;
     printf("------------------------------------------------------\n");
     printf("Test SOA: \n");
     printf("serial = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_serial );
     printf("refresh = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_refresh );
     printf("retry = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_retry );
     printf("expire = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_expire );
     printf("minmum = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_minmum );
     if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr)
         printf("host mname = %s\n", nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr);
     else
         printf("host mame is not set\n");
     if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr)
         printf("host rname = %s\n", nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr);
     else
         printf("host rname is not set\n");


#endif

    /* Shutting down...*/

    /* Terminate the DNS Client thread. */
    status = nx_dns_delete(&client_dns);

    return;
}
```
## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX için DNS oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Bu seçenekler *nxd_dns. h* içinde yeniden tanımlanabilir. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:  

- **NX_DNS_TYPE_OF_SERVICE** DNS UDP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmeti için NX_IP_NORMAL olarak tanımlanmıştır.

- **NX_DNS_TIME_TO_LIVE** Bir paketin, atılmadan önce geçebilmesi için en fazla yönlendirici sayısını belirtir. Varsayılan değer 0x80 ' dır.

- **NX_DNS_FRAGMENT_OPTION** Yuva özelliğini giden paketlerin parçalanması için izin vermek veya engellemek üzere ayarlar. Varsayılan değer NX_DONT_FRAGMENT.

- **NX_DNS_QUEUE_DEPTH** Yuva alma kuyruğunda depolanacak en fazla paket sayısını ayarlar. Varsayılan değer 5 ' tir.

- **NX_DNS_MAX_SERVERS** Istemci sunucusu listesindeki en fazla DNS sunucusu sayısını belirtir. Varsayılan değer 5 ' tir.

- **NX_DNS_MESSAGE_MAX** DNS sorguları göndermek için en yüksek DNS iletisi boyutu. Varsayılan değer 512 ' dir ve ayrıca, RFC 1035 bölümünde belirtilen en büyük boyut 2.3.4.

- **NX_DNS_PACKET_PAYLOAD_UNALIGNED** Tanımlı değilse, Ethernet, IP (veya IPv6) ve UDP üst bilgilerinin yanı sıra NX_DNS_MESSAGE_MAX tarafından belirtilen en büyük DNS ileti boyutunu içeren Istemci paketi yükünün boyutu. Tanımlanmış olmasına bakılmaksızın, paket yükü 4 bayt hizalı ve NX_DNS_PACKET_PAYLOAD depolanır.

- **NX_DNS_PACKET_POOL_SIZE** NX_DNS_CLIENT_USER_CREATE_PACKET_POOL tanımlanmamışsa DNS sorguları göndermek için Istemci paket havuzunun boyutu. Varsayılan değer, NX_DNS_PACKET_PAYLOAD tarafından tanımlanan yük boyutu 16 paketi için yeterince büyük ve 4 bayt hizalı.

- **NX_DNS_MAX_RETRIES** DNS Istemcisinin, başka bir sunucuyu denemeden veya DNS sorgusunu iptal etmeden önce geçerli DNS sunucusunu sorgulayabilmesi için gereken en fazla sayı. Varsayılan değer 3 ' dir.

- **NX_DNS_MAX_RETRANS_TIMEOUT** Belirli bir DNS sunucusuna bir DNS sorgusunda en fazla yeniden iletim zaman aşımı. Varsayılan değer 64 saniyedir (64 * NX_IP_PERIODIC_RATE).

- **NX_DNS_IP_GATEWAY_AND_DNS_SERVER** Tanımlandıysa ve Istemci IPv4 ağ geçidi adresi sıfır değilse DNS Istemcisi, IPv4 ağ geçidini Istemcinin birincil DNS sunucusu olarak ayarlar. Varsayılan değer devre dışıdır.

- **NX_DNS_PACKET_ALLOCATE_TIMEOUT** Bu, DNS istemci paket havuzundan bir paket ayırma zaman aşımı seçeneğini ayarlar. Varsayılan değer 1 saniyedir (1 * NX_IP_PERIODIC_RATE).

- **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** Bu, DNS Istemcisinin, uygulamanın DNS Istemci paket havuzunu oluşturmasına ve ayarlamaya izin verir. Varsayılan olarak, bu seçenek devre dışıdır ve DNS Istemcisi *nx_dns_create* içinde kendi paket havuzunu oluşturur.

- **NX_DNS_CLIENT_CLEAR_QUEUE** Bu, yeni bir sorgu göndermeden önce DNS Istemcisinin eski DNS iletilerini alma sırasından temizlemenizi sağlar. Bu paketlerin önceki DNS sorgularından kaldırılması, DNS Istemci yuva kuyruğunun geçerli paketlerin taşmasını ve bırakılmasını engeller.

- **NX_DNS_ENABLE_EXTENDED_RR_TYPES** Bu, DNS Istemcisinin içindeki ek DNS kayıt türlerini sorgulamasını sağlar (ör. CNAME, NS, MX, SOA, SRV ve TXT).

- **NX_DNS_CACHE_ENABLE** Bu, DNS Istemcisinin yanıt kayıtlarını DNS önbelleğine depolamasını sağlar.