---
title: Bölüm 2 - NetX Duo DNS Azure RTOS Yükleme ve Kullanma
description: Bu bölümde NetX Duo DNS İstemcisi'nin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d18e6444f13f069347719901b24234aebe04cdc5cd6230212e0781a50ed245d1
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792018"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-dns-client"></a>Bölüm 2 - NetX Duo DNS Azure RTOS Yükleme ve Kullanma

Bu bölümde NetX Duo DNS İstemcisi'nin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.

## <a name="product-distribution"></a>Ürün Dağıtımı

NetX Duo DNS İstemcisi sayfasından [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) kullanılabilir. Paket, aşağıdaki gibi iki kaynak dosya ve bu belgeyi içeren bir PDF dosyası içerir:

- **nxd_dns.h** NetX Duo DNS İstemcisi için üst bilgi dosyası
- **nxd_dns.c** NetX Duo DNS İstemcisi için C Kaynak dosyası
- **nxd_dns.pdf** NetX Duo DNS İstemcisi'nin PDF açıklaması

## <a name="dns-client-installation"></a>DNS İstemcisi Yüklemesi

NetX Duo DNS İstemcisi'ni kullanmak için *nxd_dns.c* ve *nxd_dns.h* kaynak kod dosyalarını NetX Duo'nın yüklü olduğu dizine kopyalayın. Örneğin,*"\threadx\arm7\green"* dizininde NetX Duo *yüklüyse, nxd_dns.h* ve *nxd_dns.c* dosyalarının bu dizine kopyalanmış olması gerekir.

## <a name="using-the-dns-client"></a>DNS İstemcisini Kullanma

NetX Duo DNS İstemcisini kullanmak kolaydır. Temel olarak, ThreadX ve NetX Duo'nxd_dns kullanmak için uygulama kodu *tx_api.h* ve *nx_api.h*'yi içeren *nxd_dns.h'yi* içermesi gerekir. Uygulama *nxd_dns.h* ekli olduktan sonra, uygulama kodu bu kılavuzun devamlarında belirtilen DNS işlev çağrılarını oluşturabilir. Uygulamanın derleme sürecine *nxd_dns.c* de eklemesi gerekir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmiş olmalı ve nesne formu uygulamanın dosyalarıyla birlikte bağlanacak. NetX Duo DNS'yi kullanmak için gerekenler bunlardır.

> [!NOTE]
> DNS NetX Duo UDP hizmetlerini kullanıyorsa, DNS'yi kullanmadan önce UDP *nx_udp_enable* çağrısıyla etkinleştirilmelidir.

## <a name="small-example-system-for-netx-duo-dns-client"></a>NetX Duo DNS İstemcisi için Küçük Örnek Sistem 

NetX Duo DNS İstemcisi, mevcut NetX DNS uygulamalarıyla uyumludur. Eski hizmetlerin ve NetX Duo eşdeğerlerinin listesi aşağıda gösterilmiştir:

| NetX DNS API hizmeti (yalnızca IPv4) | NetX Duo DNS API hizmeti (IPv4 ve IPv6 desteği) |
|----------------------------------|----------------------------------------------------|
| nx_dns_host_by_name_get          | nxd_dns_host_by_name_get                           |
| nx_dns_host_by_address_get       | nxd_dns_host_by_address_get                        |
| nx_dns_server_get                | nxd_dns_server_get                                 |
| nx_dns_server_add                | nxd_dns_server_add                                 |
| nx_dns_server_remove             | nxd_dns_server_remove                              |

Daha fazla ayrıntı için 3. Bölüm'de NetX Duo DNS İstemci API'si hizmetlerinin açıklamasına bakın.

Bu bölümde sağlanan örnek DNS uygulama programında *nxd_dns.h,* 6. satıra dahil edilir. NX_DNS_CLIENT_USER_CREATE_PACKET_POOL DNS İstemcisi uygulamasının DNS İstemcisi için paket havuzunu oluşturmasını sağlayan paket havuzu, 24-26. satırlarda bildirildi. Bu paket havuzu, DNS iletileri göndermek için paketlerin gönderilmesi için kullanılır. Bu NX_DNS_CLIENT_USER_CREATE_PACKET_POOL, 78-98. satırlarda bir paket havuzu oluşturulur. Bu seçenek etkinleştirilmezse, DNS İstemcisi *nxd_dns.h'de* yapılandırma parametreleri tarafından ayarlanmış ve bu bölümün başka bir yerinde açıklanan paket yüküne ve havuz boyutuna göre kendi paket havuzunu oluşturur.

dahili NetX Duo işlemleri için kullanılan İstemci IP örneği için 100-112. satırlarda başka bir paket havuzu oluşturulur. Ardından IP örneği, 115. *satırda* nx_ip_create çağrı kullanılarak oluşturulur. IP görevi ve DNS İstemcisi'nin aynı paket havuzunu paylaşması mümkündür, ancak DNS İstemcisi genellikle IP görevi tarafından gönderilen denetim paketlerinden daha büyük iletiler gönderdiğinden, ayrı paket havuzları kullanmak bellek kullanımını daha verimli hale getirir.

ARP ve UDP (IPv4 ağları tarafından kullanılır) sırasıyla 129 ve 141. satırlarda etkinleştirilir.

>[!NOTE]
> Bu tanıtımda, 44. satırda bildirilen 'ram' sürücüsü kullanılır ve bu sürücü *nx_ip_create* kullanılır. Bu ram sürücüsü NetX Duo kaynak koduyla dağıtılır. DNS İstemcisi'ni gerçekten çalıştırmak için uygulamanın, PAKETLERI DNS sunucusundan iletmek ve almak için gerçek bir fiziksel ağ sürücüsü sağlamak zorunda olması gerekir.

İstemci iş parçacığı giriş *thread_client_entry* işlevi, tx_application_define *tanımlanır.* BAŞLANGıÇTA IP görev iş parçacığının ağ sürücüsü tarafından başlatılmasına izin vermek için denetimi sisteme verir.

Ardından 257. satırda DNS İstemcisi oluşturur, 267- 278. satırlarda DNS önbelleğini başlatıyor ve daha önce oluşturulan paket havuzunu 281-295. satırlarda DNS İstemcisi örneğine ayarlar. Ardından 297-341 satırlarında DNS sunucusu ekler.

Örnek programın geri kalanı DNS sorguları yapmak için DNS İstemcisi hizmetlerini kullanır. Ana bilgisayar IP adresi aramaları 193 ve 207. satırlarda gerçekleştirilir. *nxd_dns_host_by_name_get* ve *nx_dns_host_by_name_get* gibi bu iki hizmet arasındaki fark, önceki hizmette adres verilerini bir NXD_ADDRESS veri türüne kaydederken ikinci hizmet de verileri ULONG veri türüne kaydeder. Daha fazla, IPv4 ağları ile sınırlıyken, önceki IPv6 veya IPv4 ağları ile kullanılabilir. Bu yalnızca IP örneği IPv6 için etkinleştirildiğinde mümkündür. IPv6 ağı için IP örneğini etkinleştirme hakkında daha fazla bilgi için bkz. NetX Duo Kullanıcı Kılavuzu.

Konak IP adresi aramaları için başka bir hizmet, 464. satırda *nx_dns_ipv4_address_by_name_get.* Bu hizmet, *nx_dns_host_by_name_get* yalnızca DNS Sunucusu yanıtını alan ilk adresi değil, etki alanı adı için bulunan IPv4 adreslerinin hepsini (veya sağlanan arabelleğe sığacak kadar çok) döndüren hizmetten farklıdır.

Benzer *şekilde, nxd_dns_ipv6_address_by_name_get* 380'de çağrılır ve DNS İstemcisi tarafından bulunan tüm IPv6 adreslerini döndürür.

Geriye doğru aramalar (IP adresinden ana bilgisayar adı) 606 (*nx_dns_host_by_address_get*) satırlarında ve tekrar 564 ve 588 *.* satırda ( nxd_dns_host_by_address_get). *nx_dns_host_by_address_get* IPv4 ağlarında, *nxd_dns_host_by_address_get* ise IPv4 veya IPv6 ağlarında (örneğin, IP örneği IPv6 ve IPv4 ağları için etkinleştirilir) çalışır.

Giriş etki alanı adı için CNAME ve etki alanı adı verilerini bulmak için sırasıyla 627 ve 649. satırlarda CNAME ve TXT adlı iki DNS araması daha gösterildi. MX, NS, SRV ve SOA gibi diğer kayıt türlerine benzer hizmetler olarak NetX Duo DNS İstemcisi. NetX Duo DNS İstemcisinde kullanılabilen tüm kayıt türü aramalarının ayrıntılı açıklamaları için 3. Bölüm'e bakın.

DNS İstemcisi 846. satırda, *nx_dns_delete* hizmeti kullanılarak silindiğinde, DNS İstemcisi kendi paket havuzunu oluşturmadıkça DNS İstemcisi için paket havuzu silinmez. Aksi takdirde, paket havuzunun başka bir kullanımı yoksa, uygulamanın paket havuzunu silmesi gerekir.

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
## <a name="configuration-options"></a>Yapılandırma Seçenekleri

NetX için DNS'yi oluşturabilirsiniz. Bu seçenekler *nxd_dns.h içinde yeniden tanımlandırabilirsiniz.* Aşağıdaki listede her biri ayrıntılı olarak açıklanmaktadır:  

- **NX_DNS_TYPE_OF_SERVICE** DNS UDP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP NX_IP_NORMAL için varsayılan olarak bir değer olarak tanımlanır.

- **NX_DNS_TIME_TO_LIVE** Bir paketin atmadan önce geçeceği en fazla yönlendirici sayısını belirtir. Varsayılan değer, 0x80.

- **NX_DNS_FRAGMENT_OPTION** Yuva özelliğini giden paketlerin parçalanmasına izin verecek veya izin vermayacak şekilde ayarlar. Varsayılan değer, NX_DONT_FRAGMENT.

- **NX_DNS_QUEUE_DEPTH** Yuva alma kuyruğunda depo için en fazla paket sayısını ayarlar. Varsayılan değer 5'tir.

- **NX_DNS_MAX_SERVERS** İstemci sunucusu listesinde en fazla DNS Sunucusu sayısını belirtir. Varsayılan değer 5'tir.

- **NX_DNS_MESSAGE_MAX** DNS sorguları göndermek için maksimum DNS ileti boyutu. Varsayılan değer, RFC 1035 Bölüm 2.3.4'te belirtilen en büyük boyut olan 512'dir.

- **NX_DNS_PACKET_PAYLOAD_UNALIGNED** Tanımlanmamışsa, Ethernet, IP (veya IPv6) ve UDP üst bilgilerini içeren İstemci paket yükünün boyutu ve ağ arabirimi tarafından belirtilen maksimum DNS ileti NX_DNS_MESSAGE_MAX. Tanımlansa da paket yükü, 4 bayt hizalanır ve paket yükü NX_DNS_PACKET_PAYLOAD.

- **NX_DNS_PACKET_POOL_SIZE** Dns sorguları göndermek için İstemci paket havuzunun boyutu NX_DNS_CLIENT_USER_CREATE_PACKET_POOL tanımlanmamıştır. Varsayılan değer, NX_DNS_PACKET_PAYLOAD tarafından tanımlanan 16 yük boyutu paketi için yeterince büyüktür ve 4 bayt hizalıdır.

- **NX_DNS_MAX_RETRIES** DNS İstemcisi'nin başka bir sunucuyu denmeden veya DNS sorgusunu durdurmadan önce geçerli DNS sunucusunu en fazla kaç kez sorgulayacak? Varsayılan değer 3'tir.

- **NX_DNS_MAX_RETRANS_TIMEOUT** Dns sorgusunda belirli bir DNS sunucusuna en fazla yeniden iletim zaman aşımı. Varsayılan değer 64 saniyedir (64 * NX_IP_PERIODIC_RATE).

- **NX_DNS_IP_GATEWAY_AND_DNS_SERVER** Tanımlı ve İstemci IPv4 ağ geçidi adresi sıfır olmayan bir adresse, DNS İstemcisi IPv4 ağ geçidini İstemcinin birincil DNS sunucusu olarak ayarlar. Varsayılan değer devre dışıdır.

- **NX_DNS_PACKET_ALLOCATE_TIMEOUT** Bu, BIR paketi DNS istemci paket havuzundan ayrım için zaman aşımı seçeneğini ayarlar. Varsayılan değer 1 saniyedir (1*NX_IP_PERIODIC_RATE).

- **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** Bu, DNS İstemcisi'nin uygulamanın DNS İstemcisi paket havuzunu oluşturmasına ve ayarlamasına olanak sağlar. Varsayılan olarak bu seçenek devre dışıdır ve DNS İstemcisi, içinde kendi paket havuzunu *nx_dns_create.*

- **NX_DNS_CLIENT_CLEAR_QUEUE** Bu, DNS İstemcisi'nin yeni bir sorgu göndermeden önce eski DNS iletilerini alma kuyruğunda temizlemesini sağlar. Bu paketleri önceki DNS sorgularından kaldırmak, DNS İstemcisi yuva kuyruğunda taşma ve geçerli paketlerin bırakmasını önler.

- **NX_DNS_ENABLE_EXTENDED_RR_TYPES** Bu, DNS İstemcisi'nin 'de (CNAME, NS, MX, SOA, SRV ve TXT gibi) ek DNS kayıt türleri üzerinde sorgulamasını sağlar.

- **NX_DNS_CACHE_ENABLE** Bu, DNS İstemcisi'nin yanıt kayıtlarını DNS önbelleğine depolamasını sağlar.