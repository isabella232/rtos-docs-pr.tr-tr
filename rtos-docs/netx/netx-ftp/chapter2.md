---
title: Bölüm 2-Azure RTOS NetX FTP yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX FTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 812422566b9761baac5f9c2477dba1f0fcc0a778
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826723"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-ftp"></a>Bölüm 2-Azure RTOS NetX FTP yüklemesi ve kullanımı

Bu bölümde, Azure RTOS NetX FTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/]) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nx_ftp. h**: NETX için FTP için üst bilgi dosyası
- **nx_ftp_client. c**: NETX Için FTP istemcisi Için c kaynak dosyası
- **nx_ftp_server. c**: NETX Için FTP sunucusu Için c kaynak dosyası
- **filex_stub. h**: FileX yoksa saplama dosyası
- **nx_ftp.pdf**: NETX için FTP 'nin PDF açıklaması
- **demo_netx_ftp. c**: FTP demo sistemi

## <a name="ftp-installation"></a>FTP yüklemesi

NetX için FTP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_ftp. h*, *nx_ftp_client. c* ve *nx_ftp_server. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-ftp"></a>FTP kullanma

NetX için FTP kullanmak kolaydır. Temel olarak, uygulama kodu, sırasıyla ThreadX, FileX ve NetX kullanmak için, *tx_api. h, fx_api. h* ve *nx_api. h* dahil *nx_ftp.* h 'yi içermelidir. *Nx_ftp. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen FTP işlev çağrılarını yapabilir. Uygulama ayrıca yapı işlemine *nx_ftp_client. c* ve *nx_ftp_server. c* içermelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX FTP 'yi kullanmak için gereklidir.

> [!NOTE]
> FTP, NetX TCP hizmetlerinden yararlandığından, FTP kullanılmadan önce *nx_tcp_enable* çağrısıyla TCP 'nin etkinleştirilmesi gerekir.

## <a name="small-example-system"></a>Küçük örnek sistem

Aşağıdaki gibi, Şekil 1,1 ' de NetX FTP kullanmanın ne kadar kolay olduğunu gösteren bir örnek.

> [!NOTE]
> Bu, tek bir ağ arabirimine sahip bir konak cihazına yöneliktir.

Bu örnekte, *nx_ftp_client. h* ve *NX_FTP_SERVER. h* FTP içerme dosyası 10. ve 11. satırda getirilir. Sonra, FTP sunucusu 134 satırındaki "*tx_application_define*" içinde oluşturulur. FTP sunucu denetimi bloğunun "*sunucu*" daha önce satır 31 ' de genel değişken olarak tanımlandığını unutmayın. Başarılı bir şekilde oluşturulduktan sonra, 363. satırda bir FTP sunucusu başlatılır. Satır 183 ' de FTP Istemcisi oluşturulur. Son olarak, Istemci dosyayı 229. satıra yazar ve dosyayı 318. satırda geri okur.

```c
/* This is a small demo of NetX FTP on the high-performance NetX TCP/IP stack. This demo
relies on ThreadX, NetX, and FileX to show a simple file transfer from the client
and then back to the server. */

#include     "tx_api.h"
#include     "fx_api.h"
#include     "nx_api.h"
#include     "nx_ftp_client.h"
#include     "nx_ftp_server.h"

#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX, NetX, and FileX object control blocks... */

TX_THREAD          server_thread;
TX_THREAD          client_thread;
NX_PACKET_POOL     server_pool;
NX_IP              server_ip;
NX_PACKET_POOL     client_pool;
NX_IP              client_ip;
FX_MEDIA           ram_disk;

/* Define the NetX FTP object control blocks. */

NX_FTP_CLIENT     ftp_client;
NX_FTP_SERVER     ftp_server;

/* Define the counters used in the demo application... */

ULONG     error_counter = 0;

/* Define the memory area for the FileX RAM disk. */

UCHAR     ram_disk_memory[32000];
UCHAR     ram_disk_sector_cache[512];

#define FTP_SERVER_ADDRESS IP_ADDRESS(1,2,3,4)
#define FTP_CLIENT_ADDRESS IP_ADDRESS(1,2,3,5)

extern UINT _fx_media_format(FX_MEDIA *media_ptr, VOID (*driver)(FX_MEDIA *media),
                    VOID *driver_info_ptr, UCHAR *memory_ptr, UINT memory_size,
                    CHAR *volume_name, UINT number_of_fats, UINT directory_entries,
                    UINT hidden_sectors, ULONG total_sectors, UINT bytes_per_sector,
                    UINT sectors_per_cluster, UINT heads, UINT sectors_per_track);

/* Define the FileX and NetX driver entry functions. */
VOID     _fx_ram_driver(FX_MEDIA *media_ptr);

/* Replace the 'ram' driver with your own Ethernet driver. */
VOID     _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

void     client_thread_entry(ULONG thread_input);
void     thread_server_entry(ULONG thread_input);

/* Define server login/logout functions. These are stubs for functions that would
validate a client login request. */

UINT     server_login(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                ULONG client_ip_address, UINT client_port, CHAR *name,
                CHAR *password, CHAR *extra_info);

UINT     server_logout(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                    ULONG client_ip_address, UINT client_port, CHAR *name,
                    CHAR *password, CHAR *extra_info);

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
    return(0);
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{

UINT      status;
UCHAR     *pointer;

    /* Setup the working pointer. */
    pointer = (UCHAR *) first_unused_memory;

    /* Create a helper thread for the server. */
    tx_thread_create(&server_thread, "FTP Server thread", thread_server_entry,
                    0, pointer, DEMO_STACK_SIZE,
                    4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize NetX. */
    nx_system_initialize();

    /* Create the packet pool for the FTP Server. */
    status = nx_packet_pool_create(&server_pool, "NetX Server Packet Pool",
                                    256, pointer, 8192);
    pointer = pointer + 8192;

    /* Check for errors. */
    if (status)
        error_counter++;

    /* Create the IP instance for the FTP Server. */
    status = nx_ip_create(&server_ip, "NetX Server IP Instance",
                        FTP_SERVER_ADDRESS, 0xFFFFFF00UL, &server_pool,
                        _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Enable ARP and supply ARP cache memory for server IP instance. */
    nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable TCP. */
    nx_tcp_enable(&server_ip);

    /* Create the FTP server. */
    status = nx_ftp_server_create(&ftp_server, "FTP Server Instance",
                    &server_ip, &ram_disk, pointer, DEMO_STACK_SIZE,
                    &server_pool, server_login, server_logout);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Now set up the FTP Client. */

    /* Create the main FTP client thread. */
    status = tx_thread_create(&client_thread, "FTP Client thread ",
                            client_thread_entry, 0,
                            pointer, DEMO_STACK_SIZE,
                            6, 6, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Create a packet pool for the FTP client. */
    status = nx_packet_pool_create(&client_pool, "NetX Client Packet Pool",
                                    256, pointer, 8192);
    pointer = pointer + 8192;

    /* Create an IP instance for the FTP client. */
    status = nx_ip_create(&client_ip, "NetX Client IP Instance", FTP_CLIENT_ADDRESS,
            0xFFFFFF00UL, &client_pool, _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Enable ARP and supply ARP cache memory for the FTP Client IP. */
    nx_arp_enable(&client_ip, (void *) pointer, 1024);

    pointer = pointer + 1024;

    /* Enable TCP for client IP instance. */
    nx_tcp_enable(&client_ip);

    return;
}

/* Define the FTP client thread. */
void     client_thread_entry(ULONG thread_input)
{

NX_PACKET     *my_packet;
UINT          status;

    /* Format the RAM disk - the memory for the RAM disk was defined above. */
    status = _fx_media_format(&ram_disk,
            _fx_ram_driver, /* Driver entry */
            ram_disk_memory, /* RAM disk memory pointer */
            ram_disk_sector_cache, /* Media buffer pointer */
            sizeof(ram_disk_sector_cache), /* Media buffer size */
            "MY_RAM_DISK", /* Volume Name */
            1, /* Number of FATs */
            32, /* Directory Entries */
            0, /* Hidden sectors */
            256, /* Total sectors */
            128, /* Sector size */
            1, /* Sectors per cluster */
            1, /* Heads */
            1); /* Sectors per track */

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Open the RAM disk. */
    status = fx_media_open(&ram_disk, "RAM DISK", _fx_ram_driver, ram_disk_memory,
                            ram_disk_sector_cache, sizeof(ram_disk_sector_cache));

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

     /* Let the IP threads and driver initialize the system. */
    tx_thread_sleep(100);

    /* Create an FTP client. */
    status = nx_ftp_client_create(&ftp_client, "FTP Client", &client_ip, 2000, &client_pool);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    printf("Created the FTP Client\n");

    /* Now connect with the NetX FTP (IPv4) server. */
    status = nx_ftp_client_connect(&ftp_client, FTP_SERVER_ADDRESS,
                                    "name", "password", 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    printf("Connected to the FTP Server\n");

    /* Open a FTP file for writing. */
    status = nx_ftp_client_file_open(&ftp_client, "test.txt", NX_FTP_OPEN_FOR_WRITE, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    printf("Opened the FTP client test.txt file\n");

    /* Allocate a FTP packet. */
    status = nx_packet_allocate(&client_pool, &my_packet, NX_TCP_PACKET, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Write ABCs into the packet payload! */
    memcpy(my_packet -> nx_packet_prepend_ptr, "ABCDEFGHIJKLMNOPQRSTUVWXYZ ", 28);

    /* Adjust the write pointer. */
    my_packet -> nx_packet_length = 28;
    my_packet -> nx_packet_append_ptr = my_packet -> nx_packet_prepend_ptr + 28;

    /* Write the packet to the file test.txt. */
    status = nx_ftp_client_file_write(&ftp_client, my_packet, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
        printf("Wrote to the FTP client test.txt file\n");

    /* Close the file. */
    status = nx_ftp_client_file_close(&ftp_client, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;
    else
        printf("Closed the FTP client test.txt file\n");

    /* Now open the same file for reading. */
    status = nx_ftp_client_file_open(&ftp_client, "test.txt", NX_FTP_OPEN_FOR_READ, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;

    else
        printf("Reopened the FTP client test.txt file\n");

    /* Read the file. */
    status = nx_ftp_client_file_read(&ftp_client, &my_packet, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;
    else
    {
        printf("Reread the FTP client test.txt file\n");
        nx_packet_release(my_packet);
    }

    /* Close this file. */
    status = nx_ftp_client_file_close(&ftp_client, 100);

    if (status != NX_SUCCESS)
        error_counter++;

    /* Disconnect from the server. */
    status = nx_ftp_client_disconnect(&ftp_client, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;

    /* Delete the FTP client. */
    status = nx_ftp_client_delete(&ftp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;
}

/* Define the helper FTP server thread. */
void     thread_server_entry(ULONG thread_input)
{

UINT     status;

    /* Wait till the IP thread and driver have initialized the system. */
    tx_thread_sleep(100);

    /* OK to start the FTP Server. */
    status = nx_ftp_server_start(&ftp_server);

    if (status != NX_SUCCESS)
        error_counter++;

    printf("Server started!\n");

    /* FTP server ready to take requests! */

    /* Let the IP threads execute. */
    tx_thread_relinquish();

    return;
}

UINT     server_login(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                ULONG client_ip_address, UINT client_port,
                CHAR *name, CHAR *password, CHAR *extra_info)
{

    printf("Logged in!\n");
    /* Always return success. */
    return(NX_SUCCESS);
}

UINT     server_logout(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                    ULONG client_ip_address, UINT client_port,
                    CHAR *name, CHAR *password, CHAR *extra_info)
{
    printf("Logged out!\n");

    /* Always return success. */
    return(NX_SUCCESS);
}
```

Şekil 1,1 NetX ile FTP Istemcisi ve sunucu örneği (tek ağ arabirimi ana bilgisayarı)

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX için FTP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:  

- **NX_FTP_SERVER_PRIORITY**: FTP sunucusu iş parçacığının önceliği. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.

- **NX_FTP_MAX_CLIENTS**: sunucunun tek seferde işleyebileceği en fazla istemci sayısı. Varsayılan olarak, bu değer 4 Istemciyi aynı anda desteklemek için 4 ' ü destekler.

- **NX_FTP_SERVER_MIN_PACKET_PAYLOAD**: TCP, IP ve ağ çerçevesi ÜSTBILGILERI ve http verileri dahil olmak üzere, bayt cinsinden sunucu paket havuzu yükünün en küçük boyutu. Varsayılan değer, 256 (dosya adı dosya boyutu için en fazla dosya adı) + dosya bilgileri için 12 bayt ve NX_PHYSICAL_TRAILER.

- **NX_FTP_NO_FILEX**: tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar. Bu seçenek tanımlanmışsa FTP Istemcisi herhangi bir değişiklik yapılmadan çalışır. FTP sunucusunun, düzgün çalışması için bir veya daha fazla FileX hizmeti oluşturması gerekir.

- **NX_FTP_CONTROL_TOS**: FTP TCP denetim istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır. Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.

- **NX_FTP_DATA_TOS**: FTP TCP veri istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır. Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.

- **NX_FTP_FRAGMENT_OPTION**: FTP TCP istekleri için parça etkinleştirilir. Varsayılan olarak, bu değer FTP TCP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT. Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.

- **NX_FTP_CONTROL_WINDOW_SIZE**: denetim yuvası pencere boyutu. Varsayılan olarak, bu değer 400 bayttır. Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.

- **NX_FTP_DATA_WINDOW_SIZE**: veri yuvası pencere boyutu. Varsayılan olarak, bu değer 2048 bayttır. Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.

- **NX_FTP_TIME_TO_LIVE**: Bu paketin atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.

- **NX_FTP_SERVER_TIMEOUT**: iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir. Varsayılan değer 100 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.

- **NX_FTP_USERNAME_SIZE**: istemcinin sağladığı *Kullanıcı adında* izin verilen bayt sayısını belirtir. Varsayılan değer 20 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.

- **NX_FTP_PASSWORD_SIZE**: istemci tarafından sağlanan *parolada* izin verilen bayt sayısını belirtir. Varsayılan değer 20 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.

- **NX_FTP_ACTIVITY_TIMEOUT**: bir etkinlik olmadığında istemci bağlantısının korunacağı saniye sayısını belirtir. Varsayılan değer 240 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.

- **NX_FTP_TIMEOUT_PERIOD**: Istemci için sunucu denetimi eylemsizlik arasındaki saniye sayısını belirtir. Varsayılan değer 60 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.
