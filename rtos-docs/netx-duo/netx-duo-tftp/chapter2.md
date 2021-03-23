---
title: Bölüm 2-Azure RTOS NetX Duo TFTP yükleme ve kullanımı
description: Bu bölümde, Azure RTOS NetX Duo TFTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ffb0c433bf1a5665e07da3cc6c240f1d0d8c87d9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826998"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-tftp"></a>Bölüm 2-Azure RTOS NetX Duo TFTP yükleme ve kullanımı

Bu bölümde, Azure RTOS NetX Duo TFTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX Duo, konumundaki ortak kaynak kodu deposundan elde edilebilir https://github.com/azure-rtos/netxduo/ . Paket aşağıdaki dosyaları içerir:


- **nxd_tftp_client. h** NetX Duo TFTP Istemcisi için üst bilgi dosyası

- **nxd_tftp_client. c** NetX Duo TFTP Istemcisi için C kaynak dosyası

- **nxd_tftp_server. h** NetX Duo TFTP sunucusu için üst bilgi dosyası

- **nxd_tftp_server. c** NetX Duo TFTP sunucusu için C kaynak dosyası

- **filex_stub. h** FileX yoksa saplama dosyası

- **nxd_tftp.pdf** NetX Duo TFTP 'nin PDF açıklaması

- **demo_netxduo_tftp. c** NetX Duo TFTP tanıtımı

## <a name="tftp-installation"></a>TFTP yüklemesi

NetX Duo TFTP 'yi kullanmak için, daha önce bahsedilen tüm dağıtım, NetX Duo 'in yüklendiği dizine kopyalanabilir. Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_tftp_client. h*, *nxd_tftp_client. c*, *nxd_tftp_server. h* ve *nxd_tftp_server. c* dosyaları bu dizine kopyalanabilir.

## <a name="using-tftp"></a>TFTP kullanma

Bir TFTP uygulamasını çalıştırmak için, uygulama kodu, sırasıyla ThreadX, FileX ve NetX Duo kullanmak amacıyla *tx_api. h, fx_api. h* ve *nx_api. h* dahil olmak üzere *nxd_tftp_client.* h ve/veya nxd_tftp_server. h içermelidir. Uygulama Projesi Ayrıca yapı işlemine *nxd_tftp_client. c* ve/veya *nxd_tftp_server. c* içermelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX Duo TFTP kullanmak için gereklidir. *Üst bilgi dosyaları* eklendikten sonra, uygulama kodu TFTP hizmetlerini kullanabilir.

> [!NOTE]
> TFTP, NetX Duo UDP hizmetlerini kullandığından, TFTP kullanılmadan önce *nx_udp_enable* çağrısıyla UDP etkinleştirilmelidir.

## <a name="small-example-system"></a>Küçük örnek sistem

Aşağıda görüntülenen Şekil 1,1 ' de NetX Duo TFTP kullanmanın ne kadar kolay olduğunu gösteren bir örnek. Bu örnekte, TFTP içerme dosyası *nxd_tftp_client. h* ve *nxd_tftp_server. h* , 19. ve 20. satırda getirilir. Ardından, TFTP sunucusu 179 satırındaki "*tx_application_define*" içinde oluşturulur. 

> [!NOTE]
> TFTP sunucu denetim bloğu "*sunucu*" daha önce satır 45 ' de genel bir değişken olarak tanımlandı. Bu demo, 6. satırda TFTP iletişimi için IPv4 kullanmayı seçer. Başarılı bir şekilde oluşturulduktan sonra, 304. satırda TFTP sunucusu başlatılır. 411. satırda TFTP Istemcisi oluşturulur. Son olarak, Istemci dosyayı 450. satıra yazar ve dosyayı 485. satırda geri okur.

TFTP sunucusu iş parçacığı görevi durdurulur ve 324 numaralı satırda TFTP sunucusu silinir. Uygulama, tüm dosyaları kapatmak ve dosya ve dizin verilerini USB medyasına güncelleştirmek için fx_media_close (satır 331) öğesini çağırmalıdır.

> [!NOTE]
> Bu örnek, TFTP Istemci dosyası isteklerinin alınması ve indirilmesi için TFTP sunucu işlemesi için FileX kullanır. Ancak, NX_TFTP_NO_FILEX tanımlanmışsa, uygulama fx_api. h yerine file_stub. h içerebilir.
>
> Ayrıca, mevcut NetX TFTP istemci ve sunucu uygulamalarının NetX Duo TFTP ile çalışacağına de unutmayın. Ancak, uygulama geliştiricisinin NetX TFTP uygulamalarının NetX Duo 'e bağlantı noktası olması önerilir. Eşdeğer NetX TFTP hizmetleri şunlardır:

- *nxd_tftp_server_start*

- *nxd_tftp_server_stop*

- *nxd_tftp_client_file_read*

- *nxd_tftp_client_file_write*

- *nxd_tftp_client_file_open*

```C
/* This is a small demo of TFTP on the high-performance NetX TCP/IP stack. This demo
   relies on ThreadX and NetX Duo, to show a simple file transfer from the client
   and then back to the server. */



/* Indicate if using IPv6. */
#define USE_DUO

/* If the host application is using NetX Duo, determine which IP version to use.
   Make sure IPv6 in NetX Duo is enabled if planning to use TFTP over IPv6 */
#ifdef USE_DUO
#define     IP_TYPE     6
#endif /* USE_DUO        */

#include    "tx_api.h"
#include    "nx_api.h"
#include    "nxd_tftp_client.h"
#include    "nxd_tftp_server.h"
#ifndef     NX_TFTP_NO_FILEX
#include    "fx_api.h"
#endif


#define     DEMO_STACK_SIZE         4096

/* To use another file storage utility define this symbol:
#define NX_TFTP_NO_FILEX
*/

/* Define the ThreadX, NetX, and FileX object control blocks... */

TX_THREAD               server_thread;
TX_THREAD               client_thread;
NX_PACKET_POOL          server_pool;
NX_IP                   server_ip;
NX_PACKET_POOL          client_pool;
NX_IP                   client_ip;
FX_MEDIA                ram_disk;

/* Define the NetX TFTP object control blocks. */

NX_TFTP_CLIENT          client;
NX_TFTP_SERVER          server;

/* Define the application global variables */

#define                 CLIENT_ADDRESS  IP_ADDRESS(1, 2, 3, 5)
#define                 SERVER_ADDRESS  IP_ADDRESS(1, 2, 3, 4)

NXD_ADDRESS             server_ip_address;
NXD_ADDRESS             client_ip_address;

UINT                    error_counter = 0;

/* Define buffer used in the demo application. */
UCHAR                   buffer[255];
ULONG                   data_length;


/* Define the memory area for the FileX RAM disk. */
#ifndef NX_TFTP_NO_FILEX
UCHAR                   ram_disk_memory[32000];
UCHAR                   ram_disk_sector_cache[512];
#endif


/* Define function prototypes. */

VOID    _fx_ram_driver(FX_MEDIA *media_ptr);
VOID    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);
void    client_thread_entry(ULONG thread_input);
void    server_thread_entry(ULONG thread_input);


/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

UINT    status;
UCHAR   *pointer;


    /* Setup the working pointer. */
    pointer =  (UCHAR *) first_unused_memory;


    /* Create the main TFTP server thread. */
    status = tx_thread_create(&server_thread, "TFTP Server Thread", server_thread_entry, 0,
                              pointer, DEMO_STACK_SIZE,
                              4,4, TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer += DEMO_STACK_SIZE ;

    /* Check for errors. */
    if (status)
        error_counter++;


    /* Create the main TFTP client thread at a slightly lower priority. */
    status = tx_thread_create(&client_thread, "TFTP Client Thread", client_thread_entry, 0,
                              pointer, DEMO_STACK_SIZE,
                              5, 5, TX_NO_TIME_SLICE, TX_DONT_START);

    pointer += DEMO_STACK_SIZE ;

    /* Check for errors. */
    if (status)
        error_counter++;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Note: The data portion of a packet is exactly 512 bytes, but the packet payload size must
       be at least 580 bytes. The remaining bytes are used for the UDP, IP, and Ethernet
       headers and byte alignment requirements. */

    status =  nx_packet_pool_create(&server_pool, "TFTP Server Packet Pool", NX_TFTP_PACKET_SIZE, pointer, 8192);
    pointer = pointer + 8192;

    /* Check for errors. */
    if (status)
        error_counter++;

    /* Create the IP instance for the TFTP Server. */
    status = nx_ip_create(&server_ip, "NetX Server IP Instance", SERVER_ADDRESS, 0xFFFFFF00UL,
                                        &server_pool, _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Check for errors. */
    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status =  nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for errors. */
    if (status)
        error_counter++;

    /* Enable UDP. */
    status =  nx_udp_enable(&server_ip);

    /* Check for errors. */
    if (status)
        error_counter++;


    /* Create the TFTP server. */
#ifdef USE_DUO
#if (IP_TYPE == 6)
#ifdef FEATURE_NX_IPV6
    /* Specify the tftp server global address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db1;
    server_ip_address.nxd_ip_address.v6[1] = 0xf101;
    server_ip_address.nxd_ip_address.v6[2] = 0;
    server_ip_address.nxd_ip_address.v6[3] = 0x102;
#endif
#else
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_ADDRESS;

#endif

    status =  nxd_tftp_server_create(&server, "TFTP Server Instance", &server_ip, &ram_disk,
                                      pointer, DEMO_STACK_SIZE, &server_pool);
#else
    status =  nx_tftp_server_create(&server, "TFTP Server Instance", &server_ip, &ram_disk,
                                      pointer, DEMO_STACK_SIZE, &server_pool);
#endif

    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for errors for the server. */
    if (status)
        error_counter++;

    /* Create a packet pool for the TFTP client. */

    /* Note: The data portion of a packet is exactly 512 bytes, but the packet payload size must
       be at least 580 bytes. The remaining bytes are used for the UDP, IP, and Ethernet
       headers and byte alignment requirements. */

    status =  nx_packet_pool_create(&client_pool, "TFTP Client Packet Pool", NX_TFTP_PACKET_SIZE, pointer, 8192);
    pointer =  pointer + 8192;

    /* Create an IP instance for the TFTP client. */
    status = nx_ip_create(&client_ip, "TFTP Client IP Instance", CLIENT_ADDRESS, 0xFFFFFF00UL,
                                                &client_pool, _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Enable ARP and supply ARP cache memory for IP Instance 1. */
    status =  nx_arp_enable(&client_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable UDP for client IP instance. */
    status |=  nx_udp_enable(&client_ip);
    status |= nx_icmp_enable(&client_ip);

    tx_thread_resume(&client_thread);
}

void server_thread_entry(ULONG thread_input)
{

UINT        status, running;
#if (IP_TYPE == 6)
#ifdef FEATURE_NX_IPV6
UINT        address_index;
UINT        iface_index;
#endif
#endif


    /* Allow time for the network driver and NetX to get initialized. */
    tx_thread_sleep(100);

#ifndef  NX_TFTP_NO_FILEX

    /* Format the RAM disk - the memory for the RAM disk was defined above. */
    status = fx_media_format(&ram_disk,
                            _fx_ram_driver,                  /* Driver entry             */
                            ram_disk_memory,                 /* RAM disk memory pointer  */
                            ram_disk_sector_cache,           /* Media buffer pointer     */
                            sizeof(ram_disk_sector_cache),   /* Media buffer size        */
                            "MY_RAM_DISK",                   /* Volume Name              */
                            1,                               /* Number of FATs           */
                            32,                              /* Directory Entries        */
                            0,                               /* Hidden sectors           */
                            256,                            /* Total sectors            */
                            128,                             /* Sector size              */
                            1,                               /* Sectors per cluster      */
                            1,                               /* Heads                    */
                            1);                              /* Sectors per track        */

    /* Check for errors. */
    if (status != FX_SUCCESS)
    {
        return;
    }

    /* Open the RAM disk. */
    status = fx_media_open(&ram_disk, "RAM DISK", _fx_ram_driver, ram_disk_memory, ram_disk_sector_cache,
                               sizeof(ram_disk_sector_cache));

    /* Check for errors. */
    if (status != FX_SUCCESS)
    {
        return;
    }

#endif /*  NX_TFTP_NO_FILEX */

#if (IP_TYPE == 6)
#ifdef FEATURE_NX_IPV6

    /* Enable ICMPv6 services. */
    status |= nxd_icmp_enable(&server_ip);
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable IPv6 services for the server. */
    status = nxd_ipv6_enable(&server_ip);
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* This assumes the primary interface. See the NetX Duo
       User Guide for more information on address configuration. */
    iface_index = 0;
    status = nxd_ipv6_address_set(&server_ip, iface_index, NX_NULL, 10, &address_index);
    status += nxd_ipv6_address_set(&server_ip, iface_index, &server_ip_address, 64, &address_index);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Wait for DAD to validate the address. */
    tx_thread_sleep(500);
#endif

#endif /* IP_TYPE == 6 */

    /* Start the NetX TFTP server. */
#ifdef USE_DUO
    status =  nxd_tftp_server_start(&server);
#else
    status =  nx_tftp_server_start(&server);
#endif

    /* Check for errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Run for a while */
    running = NX_TRUE;
    while(running)
        tx_thread_sleep(200);


    /* Stop and delete the TFTP server. */
#ifdef USE_DUO
    nxd_tftp_server_delete(&server);
#else
    nx_tftp_server_delete(&server);
#endif

    /* Close all open files and ensure directory information is also written out to the media.
    This will also flush the file data to USB media*/
    status = fx_media_close(&ram_disk);

    if (status)
    {
        error_counter++;
    }

    return;

}


/* Define the TFTP client thread. */

void    client_thread_entry(ULONG thread_input)
{

NX_PACKET   *my_packet;
UINT        status;
UINT        all_done = NX_FALSE;
#if (IP_TYPE == 6)
#ifdef FEATURE_NX_IPV6
UINT        address_index;
UINT        iface_index;
#endif
#endif


    /* Allow time for the network driver and NetX to get initialized. */
    tx_thread_sleep(100);

#if (IP_TYPE == 6)
#ifdef FEATURE_NX_IPV6

    /* Enable ECMPv6 services for the client. */
    status = nxd_icmp_enable(&client_ip);
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable IPv6 services for the client. */
    status = nxd_ipv6_enable(&client_ip);
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Set the Client IPv6 address */
    client_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    client_ip_address.nxd_ip_address.v6[0] = 0x20010db1;
    client_ip_address.nxd_ip_address.v6[1] = 0xf101;
    client_ip_address.nxd_ip_address.v6[2] = 0;
    client_ip_address.nxd_ip_address.v6[3] = 0x101;

    /* This assumes the primary interface. See the NetX Duo
       User Guide for more information on address configuration. */
    iface_index = 0;
    status = nxd_ipv6_address_set(&client_ip, iface_index, NX_NULL, 10, &address_index);
    status += nxd_ipv6_address_set(&client_ip, iface_index, &client_ip_address, 64, &address_index);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Wait for the link local and global addresses to be validated. */
    tx_thread_sleep(500);
#endif
#endif /*(IP_TYPE == 6) */


    /* The TFTP services used below include the NetX equivalent service which will work with
       NetX Duo TFTP. However, it is recommended for developers to port their applications
       to the newer services that take the NXD_ADDRESS type and support both IPv4 and IPv6
       communication.
    */

    /* Create a TFTP client. */
#ifdef USE_DUO
    status =  nxd_tftp_client_create(&client, "TFTP Client", &client_ip, &client_pool, IP_TYPE);
#else
    status =  nx_tftp_client_create(&client, "TFTP Client", &client_ip, &client_pool);
#endif

    /* Check status. */
    if (status)
        return;

    /* Open a TFTP file for writing. */
#ifdef USE_DUO
    status =  nxd_tftp_client_file_open(&client, "test.txt", &server_ip_address, NX_TFTP_OPEN_FOR_WRITE, 100, IP_TYPE);
#else
    status =  nx_tftp_client_file_open(&client, "test.txt", SERVER_ADDRESS, NX_TFTP_OPEN_FOR_WRITE, 100);
#endif

    /* Check status. */
    if (status)
        return;

    /* Allocate a TFTP packet. */
#ifdef USE_DUO
    status =  nxd_tftp_client_packet_allocate(&client_pool, &my_packet, 100, IP_TYPE);
#else
    status =  nx_tftp_client_packet_allocate(&client_pool, &my_packet, 100);
#endif
    /* Check status. */
    if (status)
        error_counter++;

    /* Write ABCs into the packet payload!  */
    memcpy(my_packet -> nx_packet_prepend_ptr, "ABCDEFGHIJKLMNOPQRSTUVWXYZ  ", 28);

    /* Adjust the write pointer. */
    my_packet -> nx_packet_length =  28;
    my_packet -> nx_packet_append_ptr =  my_packet -> nx_packet_prepend_ptr + 28;

    /* Write this packet to the file via TFTP. */
#ifdef USE_DUO
    status =  nxd_tftp_client_file_write(&client, my_packet, 100, IP_TYPE);
#else
    status =  nx_tftp_client_file_write(&client, my_packet, 100);
#endif

    /* Check status. */
    if (status)
        error_counter++;

    /* Close this file. */
#ifdef USE_DUO
    status =  nxd_tftp_client_file_close(&client, IP_TYPE);
#else
    status =  nx_tftp_client_file_close(&client);
#endif

    /* Check status. */
    if (status)
        error_counter++;

    /* Open the same file for reading. */
#ifdef USE_DUO
    status =  nxd_tftp_client_file_open(&client, "test.txt", &server_ip_address, NX_TFTP_OPEN_FOR_READ, 100, IP_TYPE);
#else
    status =  nx_tftp_client_file_open(&client, "test.txt", SERVER_ADDRESS, NX_TFTP_OPEN_FOR_READ, 100);
#endif

    /* Check status. */
    if (status)
        error_counter++;
    do
    {

    /* Read the file back. */
#ifdef USE_DUO
        status =  nxd_tftp_client_file_read(&client, &my_packet, 100, IP_TYPE);
#else
        status =  nx_tftp_client_file_read(&client, &my_packet, 100);
#endif
        /* Check for retranmission/dropped packet error. Benign. Try again... */
        if (status == NX_TFTP_INVALID_BLOCK_NUMBER)
        {

            continue;
        }
        else if (status == NX_TFTP_END_OF_FILE)
        {

            /* All done. */
            all_done = NX_TRUE;
        }
        else if (status != NX_SUCCESS)
        {

            /* Internal error, invalid packet or error on read. */
            break;
        }


        /* Do something with the packet data and release when done. */
        nx_packet_data_retrieve(my_packet, buffer, &data_length);
        buffer[data_length] = 0;
        printf("Receive data: %s\n", buffer);

        printf("release packet in demo.\n");

        nx_packet_release(my_packet);

    } while (all_done == NX_FALSE);

    /* Close the file again. */
#ifdef USE_DUO
    status =  nxd_tftp_client_file_close(&client, IP_TYPE);
#else
    status =  nx_tftp_client_file_close(&client);
#endif

    /* Check status. */
    if (status)
        error_counter++;

    /* Delete the client. */
#ifdef USE_DUO
    status =  nxd_tftp_client_delete(&client);
#else
    status =  nx_tftp_client_delete(&client);
#endif

    /* Check status. */
    if (status)
        error_counter++;

    return;
}
```

Şekil 1,1 NetX Duo ile TFTP kullanımı örneği

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX Duo TFTP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıdaki listede her biri ayrıntılı olarak açıklanmaktadır. Aksi belirtilmediği takdirde, bu seçenekler *nxd_tftp_client. h* ve *nxd_tftp_server. h* içinde bulunur.


- **NX_DISABLE_ERROR_CHECKING** Tanımlı, bu seçenek temel TFTP hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.

- **NX_TFTP_SERVER_PRIORITY** TFTP sunucusu iş parçacığının önceliği. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.

- **NX_TFTP_SERVER_TIME_SLICE** Aynı önceliğe sahip diğer iş parçacıklarına ayrılmadan önce, TFTP sunucusunun çalışacağı zaman dilimi. Varsayılan değer 2 ' dir.

- **NX_TFTP_MAX_CLIENTS** Sunucunun tek seferde işleyebileceği en fazla istemci sayısı. Varsayılan olarak, bu değer 10 istemciyi aynı anda desteklemek için 10 ' dur.

- **NX_TFTP_ERROR_STRING_MAX** Hata dizesindeki en fazla karakter sayısı. Varsayılan olarak, bu değer 64 ' dir.

- **NX_TFTP_NO_FILEX** Tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar. Bu seçenek tanımlanmışsa TFTP Istemcisi herhangi bir değişiklik yapılmadan çalışır. Düzgün çalışması için TFTP sunucusunun değiştirilmesi veya kullanıcının el ile bir FileX hizmeti oluşturması gerekir.

- **NX_TFTP_TYPE_OF_SERVICE** TFTP UDP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.

- **NX_TFTP_FRAGMENT_OPTION** TFTP UDP istekleri için parça etkinleştirme. Varsayılan olarak, bu değer TFTP UDP fragmenting devre dışı bırakılacak NX_DONT_FRAGMENT.

- **NX_TFTP_TIME_TO_LIVE** Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır.

- **NX_TFTP_SOURCE_PORT** Bu seçenek, TFTP istemci uygulamasının TFTP Istemci UDP yuva bağlantı noktasını belirtmesini sağlar. NX_ANY_PORT varsayılan olarak ayarlanır.

- ***NX_TFTP_SERVER_RETRANSMIT_ENABLE*** En son etkinlikle (bir ACK veya veri paketi) her TFTP istemci oturumunu kontrol etmek için TFTP sunucusunun zamanlayıcısında izin sağlar. Oturum zaman aşımı süresi en fazla kaç kez sona erdiğinde bağlantının kaybedildiği varsayılır. Sunucu, Istemci isteğini temizler, açık dosyaları kapatır ve bağlantı isteğini sonraki Istemci için kullanılabilir hale getirir. Varsayılan ayar devre dışıdır.

- **NX_TFTP_SERVER_TIMEOUT_PERIOD** TFTP sunucusu süreölçer girişi işlevinin herhangi bir paket almak için Istemci bağlantılarını denetleyeceği zaman aralığını belirtir. Varsayılan değer 20 ' dir (süreölçer işaretleri).

- **NX_TFTP_SERVER_RETRANSMIT_TIMEOUT** Bu, Istemciden geçerli bir ACK veya veri paketi alma zaman aşımından. Varsayılan değer 200 ' dir (süreölçer işaretleri)*.*

- **NX_TFTP_SERVER_MAX_RETRIES** Istemci oturumu yeniden aktarım süresinin yenilenme sayısı üst sınırını belirtir. Bundan sonra, oturum sunucu tarafından kapalıdır.

- **NX_TFTP_MAX_CLIENT_RETRANSMITS** İstemcinin istemciye bir hata iletisi göndermeden ve oturumu kapatmadan, sunucudan yinelenen bir ACK veya veri paketi alma işleminin (düşerek) en fazla kaç kez olduğunu belirtir. NX_TFTP_SERVER_RETRANSMIT_ENABLE tanımlanmışsa hiçbir etkisi yoktur.
