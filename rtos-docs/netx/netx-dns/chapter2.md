---
title: Bölüm 2-Azure RTOS NetX DNS Istemcisini yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX DNS Istemcisinin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 054b7366eb9a28bc0dc2fb8c4b2479c12532499b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826753"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-dns-client"></a>Bölüm 2-Azure RTOS NetX DNS Istemcisini yükleme ve kullanma

Bu bölümde, Azure RTOS NetX DNS Istemcisinin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX DNS Istemcisi adresinde bulunabilir <https://github.com/azure-rtos/netx> . Paket aşağıdaki dosyaları içerir:

- **nx_dns. h**: NETX DNS istemcisi için üst bilgi dosyası
- **nx_dns. c**: NETX DNS istemcisi Için c kaynak dosyası
- **nx_dns.pdf**: NETX DNS istemcisinin PDF açıklaması

## <a name="dns-client-installation"></a>DNS Istemcisi yüklemesi

NetX DNS Istemcisini kullanmak için *nx_dns. c* ve *nx_dns. h* kaynak kodu dosyalarını NETX 'in yüklü olduğu dizine kopyalayın. Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_dns. h* ve *nx_dns. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-the-dns-client"></a>DNS Istemcisini kullanma

NetX DNS Istemcisini kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_dns.* h içermelidir. *Nx_dns. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen DNS işlev çağrılarını yapabilir. Uygulamanın yapı işlemine *nx_dns. c* eklemesi de gerekir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX DNS kullanmak için gereklidir.

>[!NOTE]
> DNS, NetX UDP hizmetlerini kullandığından, DNS kullanılmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerekir.

## <a name="small-example-system-for-dns-client"></a>DNS Istemcisi için küçük örnek sistem 

Bu bölümde sağlanan örnek DNS uygulama programında, *nx_dns. h* , 6. satırda bulunur. DNS istemcisi uygulamasının DNS Istemcisi için paket havuzu oluşturmasına izin veren NX_DNS_CLIENT_USER_CREATE_PACKET_POOL, 21-23 satırlarında bildirilmiştir. Bu paket havuzu, DNS iletileri göndermek için paket ayırmak üzere kullanılır. NX_DNS_CLIENT_USER_CREATE_PACKET_POOL tanımlanmışsa, 71-91 satırlarında bir paket havuzu oluşturulur. Bu seçenek etkinleştirilmemişse, DNS Istemcisi, paket yükünün ve havuz boyutunun, *nx_dns. h* içinde yapılandırma parametreleri tarafından ayarlanan ve bu bölümün başka bir yerinde açıklandığı şekilde kendi paket havuzunu oluşturur.

İç NetX işlemleri için kullanılan Istemci IP örneği için 93-105 satırlarında başka bir paket havuzu oluşturulur. Daha sonra, 107-119 satırındaki *nx_ip_create* ÇAĞRıSı kullanılarak IP örneği oluşturulur. IP görevinin ve DNS Istemcisinin aynı paket havuzunu paylaşması mümkündür, ancak DNS Istemcisi genellikle IP görevi tarafından gönderilen denetim paketlerinden daha büyük iletiler gönderdiğinden, ayrı paket havuzlarının kullanılması belleğin daha verimli bir şekilde kullanılmasını sağlar.

ARP ve UDP (IPv4 ağları tarafından kullanılır) sırasıyla 122 ve 134 satırlarında etkindir.

>[!NOTE]
> Bu demo, 37 satırında belirtilen ve *nx_ip_create* çağrısında kullanılan ' RAM ' sürücüsünü kullanır. Bu RAM sürücüsü NetX kaynak kodu ile dağıtılır. DNS Istemcisini gerçekten çalıştırmak için, uygulamanın DNS sunucusundan paket iletmek ve almak için gerçek fiziksel ağ sürücüsü sağlaması gerekir.

*Thread_client_entry* istemci iş parçacığı girişi işlevi *tx_application_define* işlevinin altında tanımlanmıştır. İlk olarak, IP görevi iş parçacığının ağ sürücüsü tarafından başlatılmasına izin vermek için sisteme denetimi yeniden denetler.

Daha sonra, 176-187. satırlarda DNS Istemcisini oluşturur, önbelleği 189-200 ' de başlatır ve daha önce oluşturulan paket havuzunu satırlarda 202-217 DNS Istemci örneğine ayarlar. Ardından 220-229 satırlarına bir IPv4 DNS sunucusu ekler.

Örnek programın geri kalanı DNS sorguları yapmak için DNS Istemci hizmetlerini kullanır. Ana bilgisayar IP adresi aramaları 240 ve 262 satırlarında gerçekleştirilir. Bu iki hizmet arasındaki fark, *nx_dns_host_by_name_get* ve *nx_dns_ipv4_address_by_name_get*, eskı olarak yalnızca bir IP adresı kaydettiğinden, DNS sunucusu yanıt verdi.

Ters aramalar (IP adresinden ana bilgisayar adı) 354 (*nx_dns_host_by_address_get*) satırlarında gerçekleştirilir.

DNS aramaları, CNAME ve TXT için iki diğer hizmet, giriş etki alanı adı için CNAME ve TXT 'yi bulmaya yönelik sırasıyla 375 ve 420 satırlarında gösterilmiştir. NetX DNS Istemcisi diğer kayıt türleri için benzer hizmetler olarak, örneğin NS, MX, SRV ve SOA. NetX DNS Istemcisinde bulunan tüm kayıt türü aramalarının ayrıntılı açıklamaları için bkz. Bölüm 3.

*Nx_dns_delete* hizmeti kullanılarak, 594. satırdaki DNS istemcisi silindiğinde, DNS istemcisi kendi paket havuzunu oluşturmadığı takdirde DNS istemcisi için paket havuzu silinmez. Aksi takdirde, bu uygulama için daha fazla kullanım yoksa, paket havuzunu silmek uygulamaya çalışır.

```c
/* This is a small demo of DNS Client for the high-performance NetX TCP/IP stack.*/
#include "tx_api.h"
#include "nx_api.h"
#include "nx_udp.h"
#include "nx_dns.h"

#define     DEMO_STACK_SIZE         4096
#define     NX_PACKET_PAYLOAD       1536
#define     NX_PACKET_POOL_SIZE     30 * NX_PACKET_PAYLOAD
#define     LOCAL_CACHE_SIZE        2048

/* Define the ThreadX and NetX object control blocks... */

NX_DNS             client_dns;
TX_THREAD          client_thread;
NX_IP              client_ip;
NX_PACKET_POOL     main_pool;

#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL
    NX_PACKET_POOL client_pool;
#endif

UCHAR       local_cache[LOCAL_CACHE_SIZE];
UINT        error_counter = 0;
#define     CLIENT_ADDRESS IP_ADDRESS(192,168,0,11)
#define     DNS_SERVER_ADDRESS IP_ADDRESS(192,168,0,1)

/* Define thread prototypes. */
void        thread_client_entry(ULONG thread_input);

/***** Substitute your ethernet driver entry function here *********/
extern     VOID _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Define main entry point. */
int main()
{
/* Enter the ThreadX kernel. */
    tx_kernel_enter();
}
/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{
    CHAR     *pointer;
    UINT     status;
    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;
    /* Create the main thread. */
    tx_thread_create(&client_thread, "Client thread", 
                     thread_client_entry, 0, pointer, 
                     DEMO_STACK_SIZE, 4, 4, TX_NO_TIME_SLICE, 
                     TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL

    /*Create the packet pool for the DNS Client to send packets. If the DNS Client is configured for letting the host application create the DNS packet pool, 
        (see NX_DNS_CLIENT_USER_CREATE_PACKET_POOL option), see 77 nx_dns_create() for guidelines on packet payload size and pool size. 
        packet traffic for NetX processes.
    */

    status = nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                   NX_DNS_PACKET_PAYLOAD, pointer, 
                                   NX_DNS_PACKET_POOL_SIZE);

    pointer = pointer + NX_DNS_PACKET_POOL_SIZE;
    /* Check for pool creation error. */
    if (status)
    {
        error_counter++;
        return;
    }

#endif
/* Create the packet pool which the IP task will use to send packets. Also available to the host 94 application to send packet. */

    status = nx_packet_pool_create(&main_pool, "Main Packet Pool", 
                                   NX_PACKET_PAYLOAD, pointer, 
                                   NX_PACKET_POOL_SIZE);
    pointer = pointer + NX_PACKET_POOL_SIZE;

/* Check for pool creation error. */
    if (status)
    {
        error_counter++;
        return;
    }

/* Create an IP instance for the DNS Client. */
    status = nx_ip_create(&client_ip, "DNS Client IP Instance", 
                          CLIENT_ADDRESS, 0xFFFFFF00UL, 
                          &main_pool, _nx_ram_network_driver, 
                          pointer, 2048, 1);
    pointer = pointer + 2048;

/* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }
/* Enable ARP and supply ARP cache memory for the DNS Client IP. */
    status = nx_arp_enable(&client_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

/* Check for ARP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }
/* Enable UDP traffic because DNS is a UDP based protocol. */

    status = nx_udp_enable(&client_ip);
/* Check for UDP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

}

#define BUFFER_SIZE 200
#define RECORD_COUNT 10

/* Define the Client thread. */
void thread_client_entry(ULONG thread_input)
{
    UCHAR         record_buffer[200];
    UINT          record_count;
    UINT          status;
    ULONG         host_ip_address;
    UINT          i;
    ULONG         *ipv4_address_ptr[RECORD_COUNT];

#ifdef NX_DNS_ENABLE_EXTENDED_RR_TYPES
    NX_DNS_NS_ENTRY    *nx_dns_ns_entry_ptr[RECORD_COUNT];
    NX_DNS_MX_ENTRY    *nx_dns_mx_entry_ptr[RECORD_COUNT];
    NX_DNS_SRV_ENTRY    *nx_dns_srv_entry_ptr[RECORD_COUNT];
    NX_DNS_SOA_ENTRY    *nx_dns_soa_entry_ptr;
    ULONG                host_address;
    USHORT               host_port;
#endif

    /* Give NetX IP task a chance to get initialized . */
    tx_thread_sleep(100);
    /* Create a DNS instance for the Client. Note this function will create the DNS Client packet pool for creating DNS message packets intended for querying its DNS server. */
    status = nx_dns_create(&client_dns, &client_ip, (UCHAR *)"DNS Client");

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

    /* Yes, use the packet pool created above which has appropriate payload size for DNS messages. */
    status = nx_dns_packet_pool_set(&client_dns, &client_pool);
    /* Check for set DNS packet pool error. */
        
    if (status)
    {
        error_counter++;
        return;
    }
#endif /* NX_DNS_CLIENT_USER_CREATE_PACKET_POOL */

    /* Add an IPv4 server address to the Client list. */
    status = nx_dns_server_add(&client_dns, DNS_SERVER_ADDRESS);
    /* Check for DNS add server error. */
    if (status)
    {
        error_counter++;
        return;
    }
/********************************************************************************/
/* Type A */
/* Send A type DNS Query to its DNS server and get the IPv4 address. */
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
        printf("------------------------------------------------------> n");
        printf("Test A: \n");
        printf("IP address: %lu.%lu.%lu.%lu\n",
        host_ip_address >> 24,
        host_ip_address >> 16 & 0xFF,
        host_ip_address >> 8 & 0xFF,
        host_ip_address & 0xFF);
    }
    /* Look up IPv4 addresses to record multiple IPv4 addresses in record_buffer and return the IPv4 address count. */
    status = nx_dns_ipv4_address_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, &record_count, 400);
    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
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
/* Type A + CNAME response */
/* Send A type DNS Query to its DNS server and get the IPv4 address. */
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
        printf("------------------------------------------------------> n");
        printf("Test A + CNAME response: \n");
        printf("IP address: %lu.%lu.%lu.%lu\n",
        host_ip_address >> 24,
        host_ip_address >> 16 & 0xFF,
        host_ip_address >> 8 & 0xFF,
        host_ip_address & 0xFF);
    }

    /* Look up IPv4 addresses to record multiple IPv4 addresses in record_buffer and return the IPv4 address count. */
    status = nx_dns_ipv4_address_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, 
                                             &record_count, 400);
    
    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
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
/* Type PTR */
/* Send PTR type DNS Query to its DNS server and get the host name. */
/********************************************************************************/

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
        printf("------------------------------------------------------> n");
        printf("Test PTR: %s\n", record_buffer);
    }

#ifdef NX_DNS_ENABLE_EXTENDED_RR_TYPES
/********************************************************************************/
/* Type CNAME */
/* Send CNAME type DNS Query to its DNS server and get the canonical name . */
/********************************************************************************/

    /* Send CNAME type to record the canonical name of host in record_buffer. */

    status = nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com", 
                              &record_buffer[0], BUFFER_SIZE, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test CNAME: %s\n", record_buffer);
    }
/********************************************************************************/
/* Type TXT */
/* Send TXT type DNS Query to its DNS server and get descriptive text. */
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
        printf("------------------------------------------------------> n");
        printf("Test TXT: %s\n", record_buffer);
    }

/********************************************************************************/
/* Type NS */
/* Send NS type DNS Query to its DNS server and get the domain name server. */
/********************************************************************************/

    /* Send NS type to record multiple name servers in record_buffer and return the name server count. If the DNS response includes the IPv4 addresses of name server, record it similarly in record_buffer. */

    status = nx_dns_domain_name_server_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                           &record_buffer[0], BUFFER_SIZE, 
                                           &record_count, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test NS: ");
        printf("record_count = %d \n", record_count);
    }
    /* Get the name server. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)(record_buffer + i * sizeof(NX_DNS_NS_ENTRY));
        printf("record %d: IP address: %d.%d.%d.%d\n", i,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 24,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 16 & 0xFF,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 8 & 0xFF,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address & 0xFF);
        
        if(nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr)
            printf("hostname = %s\n", nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr);
        else
            printf("hostname is not set\n");
    }

/********************************************************************************/
/* Type MX */
/* Send MX type DNS Query to its DNS server and get the domain mail exchange. */
/********************************************************************************/

    /* Send MX DNS query type to record multiple mail exchanges in record_buffer and return the mail exchange count. If the DNS response includes the IPv4 addresses of mail exchange, record it similarly in record_buffer. */

    status = nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, &record_count, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
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
/* Type SRV */
/* Send SRV type DNS Query to its DNS server and get the location of services. */
/********************************************************************************/

    /* Send SRV DNS query type to record the location of services in record_buffer and return count. If the DNS response includes the IPv4 addresses of service name, record it similarly in record_buffer. */

    status = nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                       &record_buffer[0], BUFFER_SIZE, &record_count, 400);
    
    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
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
    status = nx_dns_info_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                     &host_address, &host_port, 200);
    /* Check for DNS add server error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test SRV: ");
        printf("IP address: %d.%d.%d.%d\n",
                host_address >> 24,
                host_address >> 16 & 0xFF,
                host_address >> 8 & 0xFF,
                host_address & 0xFF);
        printf("port number = %d\n", host_port);
    }
    
/********************************************************************************/
/* Type SOA */
/* Send SOA type DNS Query to its DNS server and get zone of start of authority.*/
/********************************************************************************/

    /* Send SOA DNS query type to record the zone of start of authority in record_buffer. */

    status = nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    
    /* Get the loc*/
    nx_dns_soa_entry_ptr = (NX_DNS_SOA_ENTRY *) record_buffer;
    printf("------------------------------------------------------> n");
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

NetX için DNS oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Bu seçenekler *nx_dns. h* içinde yeniden tanımlanabilir. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:  

- **NX_DNS_TYPE_OF_SERVICE**: DNS UDP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmeti için NX_IP_NORMAL olarak tanımlanmıştır.

- **NX_DNS_TIME_TO_LIVE**: bir paketin, atılmadan önce geçebilmesi için en fazla yönlendirici sayısını belirtir. Varsayılan değer 0x80 ' dır

- **NX_DNS_FRAGMENT_OPTION**: yuva özelliğini giden paketlerin parçalanması için izin vermek veya engellemek üzere ayarlar. Varsayılan değer NX_DONT_FRAGMENT.

- **NX_DNS_QUEUE_DEPTH**: yuva alma kuyruğunda depolanacak en fazla paket sayısını ayarlar. Varsayılan değer 5 ' tir.

- **NX_DNS_MAX_SERVERS**: istemci sunucusu listesindeki en fazla DNS sunucusu sayısını belirtir.

- **NX_DNS_MESSAGE_MAX**: DNS sorguları göndermek için en yüksek DNS iletisi boyutu. Varsayılan değer 512 ' dir ve ayrıca, RFC 1035 bölümünde belirtilen en büyük boyut 2.3.4.

- **NX_DNS_PACKET_PAYLOAD_UNALIGNED**: tanımlanmamışsa, Ethernet, IP (veya IPv6) ve UDP üst bilgilerinin yanı sıra NX_DNS_MESSAGE_MAX tarafından belirtilen en büyük DNS ileti boyutunu içeren istemci paketi yükünün boyutu. Tanımlanmış olmasına bakılmaksızın, paket yükü 4 bayt hizalı ve NX_DNS_PACKET_PAYLOAD depolanır.

- **NX_DNS_PACKET_POOL_SIZE**: NX_DNS_CLIENT_USER_CREATE_PACKET_POOL tanımlanmamışsa DNS sorguları göndermek için istemci paket havuzunun boyutu. Varsayılan değer, NX_DNS_PACKET_PAYLOAD tarafından tanımlanan yük boyutu 16 paketi için yeterince büyük ve 4 bayt hizalı.

- **NX_DNS_MAX_RETRIES**: DNS istemcisinin, başka bir sunucuyu denemeden veya DNS sorgusunu iptal etmeden önce geçerli DNS sunucusunu sorgulayabilmesi için gereken en fazla sayı.

- **NX_DNS_MAX_RETRANS_TIMEOUT**: DNS sorgusunda belırlı bir DNS sunucusuna en fazla yeniden iletim zaman aşımı. Varsayılan değer 64 saniyedir (64 * NX_IP_PERIODIC_RATE).

- **NX_DNS_IP_GATEWAY_AND_DNS_SERVER**: tanımlanmışsa ve istemci IPv4 ağ geçidi adresi sıfır değilse DNS Istemcisi, IPv4 ağ geçidini ISTEMCININ birincil DNS sunucusu olarak ayarlar. Varsayılan değer devre dışıdır.

- **NX_DNS_PACKET_ALLOCATE_TIMEOUT**: Bu, BIR paketin DNS istemci paket havuzundan ayrılmasına yönelik zaman aşımı seçeneğini ayarlar. Varsayılan değer 1 saniyedir (1 * NX_IP_PERIODIC_RATE).

- **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL**: Bu, DNS istemcisinin, uygulamanın DNS istemci paket havuzunu oluşturmasına ve ayarlamaya izin verir. Varsayılan olarak, bu seçenek devre dışıdır ve DNS Istemcisi *nx_dns_create* içinde kendi paket havuzunu oluşturur.

- **NX_DNS_CLIENT_CLEAR_QUEUE**: Bu, yeni bir sorgu göndermeden önce, DNS ISTEMCISININ eski DNS iletilerini alma sırasından temizlamasına olanak sağlar. Bu paketlerin önceki DNS sorgularından kaldırılması, DNS Istemci yuva kuyruğunun geçerli paketlerin taşmasını ve bırakılmasını engeller.

- **NX_DNS_ENABLE_EXTENDED_RR_TYPES**: Bu, DNS istemcisinin IÇINDEKI ek DNS kayıt türlerini sorgulamasını sağlar (ör. CNAME, NS, MX, SOA, SRV ve txt).

- **NX_DNS_CACHE_ENABLE**: Bu, DNS istemcisinin yanıt kayıtlarını DNS önbelleğine depolamasına olanak sağlar.
