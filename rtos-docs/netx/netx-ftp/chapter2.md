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
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-ftp"></a><span data-ttu-id="7b6fb-103">Bölüm 2-Azure RTOS NetX FTP yüklemesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="7b6fb-103">Chapter 2 - Installation and use of Azure RTOS NetX FTP</span></span>

<span data-ttu-id="7b6fb-104">Bu bölümde, Azure RTOS NetX FTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX FTP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="7b6fb-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="7b6fb-105">Product Distribution</span></span>

<span data-ttu-id="7b6fb-106">Azure RTOS NetX, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/]) .</span><span class="sxs-lookup"><span data-stu-id="7b6fb-106">Azure RTOS NetX can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/]).</span></span> <span data-ttu-id="7b6fb-107">Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="7b6fb-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="7b6fb-108">**nx_ftp. h**: NETX için FTP için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="7b6fb-108">**nx_ftp.h**: Header file for FTP for NetX</span></span>
- <span data-ttu-id="7b6fb-109">**nx_ftp_client. c**: NETX Için FTP istemcisi Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="7b6fb-109">**nx_ftp_client.c**: C Source file for FTP Client for NetX</span></span>
- <span data-ttu-id="7b6fb-110">**nx_ftp_server. c**: NETX Için FTP sunucusu Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="7b6fb-110">**nx_ftp_server.c**: C Source file for FTP Server for NetX</span></span>
- <span data-ttu-id="7b6fb-111">**filex_stub. h**: FileX yoksa saplama dosyası</span><span class="sxs-lookup"><span data-stu-id="7b6fb-111">**filex_stub.h**: Stub file if FileX is not present</span></span>
- <span data-ttu-id="7b6fb-112">**nx_ftp.pdf**: NETX için FTP 'nin PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="7b6fb-112">**nx_ftp.pdf**: PDF description of FTP for NetX</span></span>
- <span data-ttu-id="7b6fb-113">**demo_netx_ftp. c**: FTP demo sistemi</span><span class="sxs-lookup"><span data-stu-id="7b6fb-113">**demo_netx_ftp.c**: FTP demonstration system</span></span>

## <a name="ftp-installation"></a><span data-ttu-id="7b6fb-114">FTP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="7b6fb-114">FTP Installation</span></span>

<span data-ttu-id="7b6fb-115">NetX için FTP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-115">In order to use FTP for NetX, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="7b6fb-116">Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_ftp. h*, *nx_ftp_client. c* ve *nx_ftp_server. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-116">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_ftp.h*, *nx_ftp_client.c*, and *nx_ftp_server.c* files should be copied into this directory.</span></span>

## <a name="using-ftp"></a><span data-ttu-id="7b6fb-117">FTP kullanma</span><span class="sxs-lookup"><span data-stu-id="7b6fb-117">Using FTP</span></span>

<span data-ttu-id="7b6fb-118">NetX için FTP kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-118">Using FTP for NetX is easy.</span></span> <span data-ttu-id="7b6fb-119">Temel olarak, uygulama kodu, sırasıyla ThreadX, FileX ve NetX kullanmak için, *tx_api. h, fx_api. h* ve *nx_api. h* dahil *nx_ftp.* h 'yi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-119">Basically, the application code must include *nx_ftp.h* after it includes *tx_api.h, fx_api.h,* and *nx_api.h*, in order to use ThreadX, FileX, and NetX, respectively.</span></span> <span data-ttu-id="7b6fb-120">*Nx_ftp. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen FTP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-120">Once *nx_ftp.h* is included, the application code is then able to make the FTP function calls specified later in this guide.</span></span> <span data-ttu-id="7b6fb-121">Uygulama ayrıca yapı işlemine *nx_ftp_client. c* ve *nx_ftp_server. c* içermelidir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-121">The application must also include *nx_ftp_client.c* and *nx_ftp_server.c* in the build process.</span></span> <span data-ttu-id="7b6fb-122">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-122">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="7b6fb-123">Bu, NetX FTP 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-123">This is all that is required to use NetX FTP.</span></span>

> [!NOTE]
> <span data-ttu-id="7b6fb-124">FTP, NetX TCP hizmetlerinden yararlandığından, FTP kullanılmadan önce *nx_tcp_enable* çağrısıyla TCP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-124">Since FTP utilizes NetX TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using FTP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="7b6fb-125">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="7b6fb-125">Small Example System</span></span>

<span data-ttu-id="7b6fb-126">Aşağıdaki gibi, Şekil 1,1 ' de NetX FTP kullanmanın ne kadar kolay olduğunu gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-126">An example of how easy it is to use NetX FTP is described in Figure 1.1 that appears below.</span></span>

> [!NOTE]
> <span data-ttu-id="7b6fb-127">Bu, tek bir ağ arabirimine sahip bir konak cihazına yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-127">This is for a host device with a single network interface.</span></span>

<span data-ttu-id="7b6fb-128">Bu örnekte, *nx_ftp_client. h* ve *NX_FTP_SERVER. h* FTP içerme dosyası 10. ve 11. satırda getirilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-128">In this example, the FTP include file *nx_ftp_client.h* and *nx_ftp_server.h* are brought at line 10 and 11.</span></span> <span data-ttu-id="7b6fb-129">Sonra, FTP sunucusu 134 satırındaki "*tx_application_define*" içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-129">Next, the FTP Server is created in "*tx_application_define*" at line 134.</span></span> <span data-ttu-id="7b6fb-130">FTP sunucu denetimi bloğunun "*sunucu*" daha önce satır 31 ' de genel değişken olarak tanımlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-130">Note that the FTP Server control block "*Server*" was defined as a global variable at line 31 previously.</span></span> <span data-ttu-id="7b6fb-131">Başarılı bir şekilde oluşturulduktan sonra, 363. satırda bir FTP sunucusu başlatılır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-131">After successful creation, an FTP Server is started at line 363.</span></span> <span data-ttu-id="7b6fb-132">Satır 183 ' de FTP Istemcisi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-132">At line 183 the FTP Client is created.</span></span> <span data-ttu-id="7b6fb-133">Son olarak, Istemci dosyayı 229. satıra yazar ve dosyayı 318. satırda geri okur.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-133">And finally, the Client writes the file at line 229 and reads the file back at line 318.</span></span>

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

<span data-ttu-id="7b6fb-134">Şekil 1,1 NetX ile FTP Istemcisi ve sunucu örneği (tek ağ arabirimi ana bilgisayarı)</span><span class="sxs-lookup"><span data-stu-id="7b6fb-134">Figure 1.1 Example of FTP Client and Server with NetX (Single network interface host)</span></span>

## <a name="configuration-options"></a><span data-ttu-id="7b6fb-135">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7b6fb-135">Configuration Options</span></span>

<span data-ttu-id="7b6fb-136">NetX için FTP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-136">There are several configuration options for building FTP for NetX.</span></span> <span data-ttu-id="7b6fb-137">Aşağıdaki listede her biri ayrıntılı açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="7b6fb-137">The following list describes each in detail:</span></span>  

- <span data-ttu-id="7b6fb-138">**NX_FTP_SERVER_PRIORITY**: FTP sunucusu iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-138">**NX_FTP_SERVER_PRIORITY**: The priority of the FTP Server thread.</span></span> <span data-ttu-id="7b6fb-139">Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-139">By default, this value is defined as 16 to specify priority 16.</span></span>

- <span data-ttu-id="7b6fb-140">**NX_FTP_MAX_CLIENTS**: sunucunun tek seferde işleyebileceği en fazla istemci sayısı.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-140">**NX_FTP_MAX_CLIENTS**: The maximum number of Clients the Server can handle at one time.</span></span> <span data-ttu-id="7b6fb-141">Varsayılan olarak, bu değer 4 Istemciyi aynı anda desteklemek için 4 ' ü destekler.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-141">By default, this value is 4 to support 4 Clients at once.</span></span>

- <span data-ttu-id="7b6fb-142">**NX_FTP_SERVER_MIN_PACKET_PAYLOAD**: TCP, IP ve ağ çerçevesi ÜSTBILGILERI ve http verileri dahil olmak üzere, bayt cinsinden sunucu paket havuzu yükünün en küçük boyutu.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-142">**NX_FTP_SERVER_MIN_PACKET_PAYLOAD**: The minimum size of the Server packet pool payload in bytes, including TCP, IP and network frame headers plus HTTP data.</span></span> <span data-ttu-id="7b6fb-143">Varsayılan değer, 256 (dosya adı dosya boyutu için en fazla dosya adı) + dosya bilgileri için 12 bayt ve NX_PHYSICAL_TRAILER.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-143">The default value is 256 (maximum length of filename in FileX) + 12 bytes for file information, and NX_PHYSICAL_TRAILER.</span></span>

- <span data-ttu-id="7b6fb-144">**NX_FTP_NO_FILEX**: tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-144">**NX_FTP_NO_FILEX**: Defined, this option provides a stub for FileX dependencies.</span></span> <span data-ttu-id="7b6fb-145">Bu seçenek tanımlanmışsa FTP Istemcisi herhangi bir değişiklik yapılmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-145">The FTP Client will function without any change if this option is defined.</span></span> <span data-ttu-id="7b6fb-146">FTP sunucusunun, düzgün çalışması için bir veya daha fazla FileX hizmeti oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-146">The FTP Server will need to either be modified or the user will have to create a handful of FileX services in order to function properly.</span></span>

- <span data-ttu-id="7b6fb-147">**NX_FTP_CONTROL_TOS**: FTP TCP denetim istekleri için gereken hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-147">**NX_FTP_CONTROL_TOS**: Type of service required for the FTP TCP control requests.</span></span> <span data-ttu-id="7b6fb-148">Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-148">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span> <span data-ttu-id="7b6fb-149">Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-149">This define can be set by the application prior to inclusion of *nx_ftp.h*.</span></span>

- <span data-ttu-id="7b6fb-150">**NX_FTP_DATA_TOS**: FTP TCP veri istekleri için gereken hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-150">**NX_FTP_DATA_TOS**: Type of service required for the FTP TCP data requests.</span></span> <span data-ttu-id="7b6fb-151">Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-151">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span> <span data-ttu-id="7b6fb-152">Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-152">This define can be set by the application prior to inclusion of *nx_ftp.h*.</span></span>

- <span data-ttu-id="7b6fb-153">**NX_FTP_FRAGMENT_OPTION**: FTP TCP istekleri için parça etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-153">**NX_FTP_FRAGMENT_OPTION**: Fragment enable for FTP TCP requests.</span></span> <span data-ttu-id="7b6fb-154">Varsayılan olarak, bu değer FTP TCP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-154">By default, this value is NX_DONT_FRAGMENT to disable FTP TCP fragmenting.</span></span> <span data-ttu-id="7b6fb-155">Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-155">This define can be set by the application prior to inclusion of *nx_ftp.h*.</span></span>

- <span data-ttu-id="7b6fb-156">**NX_FTP_CONTROL_WINDOW_SIZE**: denetim yuvası pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-156">**NX_FTP_CONTROL_WINDOW_SIZE**: Control socket window size.</span></span> <span data-ttu-id="7b6fb-157">Varsayılan olarak, bu değer 400 bayttır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-157">By default, this value is 400 bytes.</span></span> <span data-ttu-id="7b6fb-158">Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-158">This define can be set by the application prior to inclusion of *nx_ftp.h*.</span></span>

- <span data-ttu-id="7b6fb-159">**NX_FTP_DATA_WINDOW_SIZE**: veri yuvası pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-159">**NX_FTP_DATA_WINDOW_SIZE**: Data socket window size.</span></span> <span data-ttu-id="7b6fb-160">Varsayılan olarak, bu değer 2048 bayttır.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-160">By default, this value is 2048 bytes.</span></span> <span data-ttu-id="7b6fb-161">Bu tanımlama, *nx_ftp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-161">This define can be set by the application prior to inclusion of *nx_ftp.h*.</span></span>

- <span data-ttu-id="7b6fb-162">**NX_FTP_TIME_TO_LIVE**: Bu paketin atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-162">**NX_FTP_TIME_TO_LIVE**: Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="7b6fb-163">Varsayılan değer 0x80 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-163">The default value is set to 0x80, but can be redefined prior to inclusion of *nx_ftp.h.*</span></span>

- <span data-ttu-id="7b6fb-164">**NX_FTP_SERVER_TIMEOUT**: iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-164">**NX_FTP_SERVER_TIMEOUT**: Specifies the number of ThreadX ticks that internal services will suspend for.</span></span> <span data-ttu-id="7b6fb-165">Varsayılan değer 100 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-165">The default value is set to 100, but can be redefined prior to inclusion of *nx_ftp.h.*</span></span>

- <span data-ttu-id="7b6fb-166">**NX_FTP_USERNAME_SIZE**: istemcinin sağladığı *Kullanıcı adında* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-166">**NX_FTP_USERNAME_SIZE**: Specifies the number of bytes allowed in a client supplied *username*.</span></span> <span data-ttu-id="7b6fb-167">Varsayılan değer 20 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-167">The default value is set to 20, but can be redefined prior to inclusion of *nx_ftp.h.*</span></span>

- <span data-ttu-id="7b6fb-168">**NX_FTP_PASSWORD_SIZE**: istemci tarafından sağlanan *parolada* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-168">**NX_FTP_PASSWORD_SIZE**: Specifies the number of bytes allowed in a client supplied *password*.</span></span> <span data-ttu-id="7b6fb-169">Varsayılan değer 20 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-169">The default value is set to 20, but can be redefined prior to inclusion of *nx_ftp.h.*</span></span>

- <span data-ttu-id="7b6fb-170">**NX_FTP_ACTIVITY_TIMEOUT**: bir etkinlik olmadığında istemci bağlantısının korunacağı saniye sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-170">**NX_FTP_ACTIVITY_TIMEOUT**: Specifies the number of seconds a client connection is maintained if there is no activity.</span></span> <span data-ttu-id="7b6fb-171">Varsayılan değer 240 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-171">The default value is set to 240, but can be redefined prior to inclusion of *nx_ftp.h.*</span></span>

- <span data-ttu-id="7b6fb-172">**NX_FTP_TIMEOUT_PERIOD**: Istemci için sunucu denetimi eylemsizlik arasındaki saniye sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-172">**NX_FTP_TIMEOUT_PERIOD**: Specifies the number of seconds between the Server checking for client inactivity.</span></span> <span data-ttu-id="7b6fb-173">Varsayılan değer 60 olarak ayarlanır, ancak *nx_ftp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7b6fb-173">The default value is set to 60, but can be redefined prior to inclusion of *nx_ftp.h.*</span></span>
