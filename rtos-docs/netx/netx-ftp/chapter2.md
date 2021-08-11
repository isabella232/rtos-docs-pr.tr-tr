---
title: Bölüm 2 - NetX FTP Azure RTOS yükleme ve kullanma
description: Bu bölümde, NetX FTP bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9da2761ed9483a920ab6f735b8a3a6bd82936c867ece8047b622788d5fb99804
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799498"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-ftp"></a>Bölüm 2 - NetX FTP Azure RTOS yükleme ve kullanma

Bu bölümde, NetX FTP bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.

## <a name="product-distribution"></a>Ürün Dağıtımı

Azure RTOS NetX, genel kaynak kodu depomuzdan [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/]) edinebilirsiniz. Paket, aşağıdaki gibi iki kaynak dosya ve bu belgeyi içeren bir PDF dosyası içerir:

- **nx_ftp.h:** NetX için FTP üst bilgi dosyası
- **nx_ftp_client.c:** NetX için FTP İstemcisi kaynak dosyası
- **nx_ftp_server.c:** NetX için FTP Sunucusu kaynak dosyası
- **filex_stub.h:** FileX yoksa saplama dosyası
- **nx_ftp.pdf:** NetX için FTP'nin PDF açıklaması
- **demo_netx_ftp.c**: FTP tanıtım sistemi

## <a name="ftp-installation"></a>FTP Yüklemesi

NetX için FTP kullanmak üzere, daha önce bahsedilen dağıtımın tamamı NetX'in yüklü olduğu dizine kopyalanır. Örneğin, NetX "*\threadx\arm7\green"* dizininde *yüklüyse, nx_ftp.h*, *nx_ftp_client.c* ve *nx_ftp_server.c* dosyaları bu dizine kopyalanır.

## <a name="using-ftp"></a>FTP kullanma

NetX için FTP kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX, FileX ve NetX kullanmak için *tx_api.h, fx_api.h* ve *nx_api.h*'yi içeren *nx_ftp.h* dosyasını içermesi gerekir. Uygulama *nx_ftp.h* ekli olduktan sonra, uygulama kodu bu kılavuzun devamlarında belirtilen FTP işlev çağrılarını mümkün hale gelecektir. Uygulamanın derleme sürecinde *nx_ftp_client.c* ve *nx_ftp_server.c'yi* de içermesi gerekir. Bu dosyaların diğer uygulama dosyalarıyla aynı şekilde derlenmiş olması ve nesne formunun uygulamanın dosyalarıyla birlikte bağlantılı olması gerekir. NetX FTP kullanmak için gerekenlerin hepsi bu kadardır.

> [!NOTE]
> FTP, NetX TCP hizmetlerini kullanıyorsa, FTP'yi kullanmadan önce *TCP nx_tcp_enable* çağrısıyla etkinleştirilmelidir.

## <a name="small-example-system"></a>Küçük Örnek Sistem

Aşağıda görünen Şekil 1.1'de NetX FTP kullanmanın ne kadar kolay olduğuna bir örnek verilmiştir.

> [!NOTE]
> Bu, tek bir ağ arabirimine sahip bir konak cihaza göredir.

Bu örnekte FTP include *nx_ftp_client.h* ve *nx_ftp_server.h* dosyaları 10. ve 11. satıra getiri. Ardından, FTP Sunucusu 134.*satırda*" tx_application_define " içinde oluşturulur. " Sunucu " FTP Sunucusu denetim bloğu daha *önce* 31. satırda genel değişken olarak tanımlanmıştır. Oluşturma işlemi başarılı olduktan sonra 363. satırda bir FTP Sunucusu başlatılacaktır. 183. satırda FTP İstemcisi oluşturulur. Son olarak, İstemci 229. satırda dosyayı yazar ve 318. satırda dosyayı geri okur.

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

Şekil 1.1 NetX ile FTP İstemcisi ve Sunucusu Örneği (Tek ağ arabirimi ana bilgisayarı)

## <a name="configuration-options"></a>Yapılandırma Seçenekleri

NetX için FTP oluşturmanın çeşitli yapılandırma seçenekleri vardır. Aşağıdaki listede her biri ayrıntılı olarak açıklanmaktadır:  

- **NX_FTP_SERVER_PRIORITY:** FTP Sunucusu iş parçacığının önceliği. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.

- **NX_FTP_MAX_CLIENTS:** Sunucunun tek bir anda işleyene en fazla İstemci sayısı. Varsayılan olarak, bu değer aynı anda 4 İstemciyi desteklemek için 4'tir.

- **NX_FTP_SERVER_MIN_PACKET_PAYLOAD:** TCP, IP ve ağ çerçevesi üst bilgileri ile HTTP verileri de dahil olmak üzere bayt cinsinden Sunucu paket havuzu yükünün minimum boyutu. Varsayılan değer 256 'dır (DosyaX'ta dosya adı uzunluğu üst sayısı) + dosya bilgileri için 12 bayt ve NX_PHYSICAL_TRAILER.

- **NX_FTP_NO_FILEX:** Tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar. Bu seçenek tanımlanırsa FTP İstemcisi herhangi bir değişiklik yapmadan işlev gösterir. FTP Sunucusunun değiştirilecek olması gerekir veya kullanıcının düzgün çalışması için birkaç FileX hizmeti oluşturması gerekir.

- **NX_FTP_CONTROL_TOS:** FTP TCP denetim istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP NX_IP_NORMAL belirtmek için varsayılan olarak tanımlanmıştır. Bu tanım, nx_ftp.h eklenmeden önce *uygulama tarafından ayarlandırabilirsiniz.*

- **NX_FTP_DATA_TOS:** FTP TCP veri istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP NX_IP_NORMAL belirtmek için varsayılan olarak tanımlanmıştır. Bu tanım, nx_ftp.h eklenmeden önce *uygulama tarafından ayarlandırabilirsiniz.*

- **NX_FTP_FRAGMENT_OPTION:** FTP TCP istekleri için parça etkinleştirme. Varsayılan olarak, bu değer FTP TCP NX_DONT_FRAGMENT devre dışı bırakmak için kullanılır. Bu tanım, nx_ftp.h eklenmeden önce *uygulama tarafından ayarlandırabilirsiniz.*

- **NX_FTP_CONTROL_WINDOW_SIZE:** Denetim yuvası penceresi boyutu. Varsayılan olarak, bu değer 400 bayttır. Bu tanım, nx_ftp.h eklenmeden önce *uygulama tarafından ayarlandırabilirsiniz.*

- **NX_FTP_DATA_WINDOW_SIZE:** Veri yuvası penceresi boyutu. Varsayılan olarak bu değer 2048 bayttır. Bu tanım, nx_ftp.h eklenmeden önce *uygulama tarafından ayarlandırabilirsiniz.*

- **NX_FTP_TIME_TO_LIVE:** Bu paketin atmadan önce geçeceği yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır, ancak nx_ftp.h eklenmeden önce *yeniden tanımlandır.*

- **NX_FTP_SERVER_TIMEOUT:** İç hizmetlerin askıya alması gereken ThreadX saat işaretlerinin sayısını belirtir. Varsayılan değer 100 olarak ayarlanır, ancak nx_ftp.h eklenmeden *önce yeniden tanımlandır.*

- **NX_FTP_USERNAME_SIZE:** İstemci tarafından sağlanan kullanıcı adı içinde izin verilen bayt sayısını *belirtir.* Varsayılan değer 20 olarak ayarlanır, ancak nx_ftp.h eklenmeden *önce yeniden tanımlandır.*

- **NX_FTP_PASSWORD_SIZE:** İstemci tarafından sağlanan parolada izin verilen bayt sayısını *belirtir.* Varsayılan değer 20 olarak ayarlanır, ancak nx_ftp.h eklenmeden *önce yeniden tanımlandır.*

- **NX_FTP_ACTIVITY_TIMEOUT:** Etkinlik yoksa istemci bağlantısının kaç saniye korunacaklarını belirtir. Varsayılan değer 240 olarak ayarlanır, ancak nx_ftp.h eklenmeden önce *yeniden tanımlandır.*

- **NX_FTP_TIMEOUT_PERIOD:** Sunucu'da istemcinin hareketsizlik olup denetlemesi arasındaki saniye sayısını belirtir. Varsayılan değer 60 olarak ayarlanır, ancak nx_ftp.h eklenmeden *önce yeniden tanımlandır.*
