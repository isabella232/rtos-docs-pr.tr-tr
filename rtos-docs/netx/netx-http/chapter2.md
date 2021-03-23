---
title: Bölüm 2-NetX HTTP yüklemesi ve kullanımı
description: Bu bölümde, NetX HTTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: db621e38e9d2324ca3ce2398aee9f729b05886ee
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826716"
---
# <a name="chapter-2---installation-and-use-of-netx-http"></a><span data-ttu-id="15812-103">Bölüm 2-NetX HTTP yüklemesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="15812-103">Chapter 2 - Installation and use of NetX HTTP</span></span>

<span data-ttu-id="15812-104">Bu bölümde, NetX HTTP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="15812-104">This chapter contains a description of various issues related to installation, setup, and usage of the NetX HTTP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="15812-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="15812-105">Product Distribution</span></span>

<span data-ttu-id="15812-106">Azure RTOS NetX, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="15812-106">Azure RTOS NetX can be obtained from our public source code repository at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span>

- <span data-ttu-id="15812-107">**nx_http_client. h** NetX için HTTP Istemcisi üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="15812-107">**nx_http_client.h** Header file for HTTP Client for NetX</span></span>
- <span data-ttu-id="15812-108">**nx_http_server. h** NetX için HTTP sunucusu üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="15812-108">**nx_http_server.h** Header file for HTTP Server for NetX</span></span>
- <span data-ttu-id="15812-109">**nx_http_client. c** NetX için HTTP Istemcisi için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="15812-109">**nx_http_client.c** C Source file for HTTP Client for NetX</span></span>
- <span data-ttu-id="15812-110">**nx_http_server. c** NetX için HTTP sunucusu için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="15812-110">**nx_http_server.c** C Source file for HTTP Server for NetX</span></span>
- <span data-ttu-id="15812-111">**nx_md5. c** MD5 Özet algoritmaları</span><span class="sxs-lookup"><span data-stu-id="15812-111">**nx_md5.c** MD5 digest algorithms</span></span>
- <span data-ttu-id="15812-112">**filex_stub. h** FileX yoksa saplama dosyası</span><span class="sxs-lookup"><span data-stu-id="15812-112">**filex_stub.h** Stub file if FileX is not present</span></span>
- <span data-ttu-id="15812-113">**nx_http.pdf** NetX için HTTP açıklaması</span><span class="sxs-lookup"><span data-stu-id="15812-113">**nx_http.pdf** Description of HTTP for NetX</span></span>
- <span data-ttu-id="15812-114">**demo_netx_http. c** NetX HTTP tanıtımı</span><span class="sxs-lookup"><span data-stu-id="15812-114">**demo_netx_http.c** NetX HTTP demonstration</span></span>

## <a name="http-installation"></a><span data-ttu-id="15812-115">HTTP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="15812-115">HTTP Installation</span></span>

<span data-ttu-id="15812-116">NetX için HTTP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="15812-116">In order to use HTTP for NetX, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="15812-117">Örneğin, NetX, "*\threadx\arm7\green*" dizinine yüklenirse, NETX http istemci uygulamaları için *nx_http_client. h* ve *Nx_http_client. c* ve netx http sunucu uygulamaları için *nx_http_server. h* ve *nx_http_server. c* .</span><span class="sxs-lookup"><span data-stu-id="15812-117">For example, if NetX is installed in the directory “*\threadx\arm7\green*” then the *nx_http_client.h* and *nx_http_client.c* for NetX HTTP Client applications, and *nx_http_server.h* and *nx_http_server.c* for NetX HTTP Server applications.</span></span> <span data-ttu-id="15812-118">*nx_md5. c* bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="15812-118">*nx_md5.c* should be copied into this directory.</span></span> <span data-ttu-id="15812-119">Tanıtım ' RAM sürücüsü ' uygulaması NetX HTTP Istemcisi ve sunucu dosyaları aynı dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="15812-119">For the demo ‘ram driver’ application NetX HTTP Client and Server files should be copied into the same directory.</span></span>

## <a name="using-http"></a><span data-ttu-id="15812-120">HTTP kullanma</span><span class="sxs-lookup"><span data-stu-id="15812-120">Using HTTP</span></span>

<span data-ttu-id="15812-121">NetX için HTTP kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="15812-121">Using HTTP for NetX is easy.</span></span> <span data-ttu-id="15812-122">Temel olarak, uygulama kodu, sırasıyla ThreadX, FileX ve NetX kullanmak için *tx_api. h, fx_api. h* ve *nx_api. h* dahil *nx_http_client. h* ve/veya *nx_http_server. h* içermelidir.</span><span class="sxs-lookup"><span data-stu-id="15812-122">Basically, the application code must include *nx_http_client.h* and/or *nx_http_server.h* after it includes *tx_api.h, fx_api.h,* and *nx_api.h*, in order to use ThreadX, FileX, and NetX, respectively.</span></span> <span data-ttu-id="15812-123">HTTP üstbilgi dosyaları eklendikten sonra, uygulama kodu daha sonra bu kılavuzda belirtilen HTTP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="15812-123">Once the HTTP header files are included, the application code is then able to make the HTTP function calls specified later in this guide.</span></span> <span data-ttu-id="15812-124">Uygulama, yapı işlemine *nx_http_client. c*, *nx_http_server. c* ve *MD5. c* ' yi de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="15812-124">The application must also include *nx_http_client.c*, *nx_http_server.c*, and *md5.c* in the build process.</span></span> <span data-ttu-id="15812-125">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="15812-125">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="15812-126">Bu, NetX HTTP 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="15812-126">This is all that is required to use NetX HTTP.</span></span>

>[!NOTE] 
> <span data-ttu-id="15812-127">Yapı işleminde NX_HTTP_DIGEST_ENABLE belirtilmemişse, *MD5. c* dosyasının uygulamaya eklenmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="15812-127">If NX_HTTP_DIGEST_ENABLE is not specified in the build process, the *md5.c* file does not need to be added to the application.</span></span> <span data-ttu-id="15812-128">Benzer şekilde, HTTP Istemci özellikleri gerekmiyorsa *nx_http_client. c* dosyası atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="15812-128">Similarly, if no HTTP Client capabilities are required, the *nx_http_client.c* file may be omitted.</span></span>

>[!NOTE] 
> <span data-ttu-id="15812-129">HTTP, NetX TCP hizmetlerinden yararlandığından, HTTP kullanılmadan önce *nx_tcp_enable* çağrısıyla TCP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="15812-129">Since HTTP utilizes NetX TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using HTTP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="15812-130">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="15812-130">Small Example System</span></span>

<span data-ttu-id="15812-131">Aşağıda görüntülenen Şekil 1,1 ' de NetX HTTP kullanmanın ne kadar kolay olduğunu gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="15812-131">An example of how easy it is to use NetX HTTP is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="15812-132">Bu örnekte, *nx_http_client. h ve nx_http_server. h* http içerme dosyası 8. satırda getirilir.</span><span class="sxs-lookup"><span data-stu-id="15812-132">In this example, the HTTP include file *nx_http_client.h and nx_http_server.h are* brought in at line 8.</span></span> <span data-ttu-id="15812-133">Ardından, HTTP sunucusu 131 satırındaki "*tx_application_define*" içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="15812-133">Next, the HTTP Server is created in “*tx_application_define*” at line 131.</span></span>

>[!NOTE] 
> <span data-ttu-id="15812-134">HTTP sunucu denetim bloğu "*sunucu*" daha önce 25. satırda genel değişken olarak tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="15812-134">The HTTP Server control block “*Server*” was defined as a global variable at line 25 previously.</span></span>

<span data-ttu-id="15812-135">Başarılı bir şekilde oluşturulduktan sonra, 136. satırda bir HTTP sunucusu başlatılır.</span><span class="sxs-lookup"><span data-stu-id="15812-135">After successful creation, an HTTP Server is started at line 136.</span></span> <span data-ttu-id="15812-136">Satır 149 ' de HTTP Istemcisi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="15812-136">At line 149 the HTTP Client is created.</span></span> <span data-ttu-id="15812-137">Son olarak, Istemci dosyayı 157. satıra yazar ve dosyayı 195. satırda geri okur.</span><span class="sxs-lookup"><span data-stu-id="15812-137">And finally, the Client writes the file at line 157 and reads the file back at line 195.</span></span>

```c
/* This is a small demo of HTTP on the high-performance NetX TCP/IP stack.
This demo relies on ThreadX, NetX, and FileX to show a simple HTML
transfer from the client and then back from the server. */

#include "tx_api.h"
#include "fx_api.h"
#include "nx_api.h"
#include "nx_http_client.h"
#include "nx_http_server.h"
#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_0;
TX_THREAD         thread_1;
NX_PACKET_POOL    pool_0;
NX_PACKET_POOL    pool_1;
NX_IP             ip_0;
NX_IP             ip_1;
FX_MEDIA          ram_disk;

/* Define HTTP objects. */

NX_HTTP_SERVER    my_server;
NX_HTTP_CLIENT    my_client;

/* Define the counters used in the demo application... */

ULONG             error_counter;

/* Define the RAM disk memory. */

UCHAR             ram_disk_memory[32000];

/* Define function prototypes. */

void     thread_0_entry(ULONG thread_input);
VOID     _fx_ram_driver(FX_MEDIA *media_ptr) ;
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
UINT     authentication_check(NX_HTTP_SERVER *server_ptr, UINT request_type,
                              CHAR *resource, CHAR **name, CHAR **password, 
                              CHAR **realm);

/* Define the application's authentication check. This is called by
the HTTP server whenever a new request is received. */
UINT authentication_check(NX_HTTP_SERVER *server_ptr, UINT request_type,
                         CHAR *resource, CHAR **name, CHAR **password, 
                         CHAR **realm);
{

    /* Just use a simple name, password, and realm for all
    requests and resources. */
    *name = "name";
    *password = "password";
    *realm = "NetX HTTP demo";

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
                    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create packet pool. */
    nx_packet_pool_create(&pool_0, "NetX Packet Pool 0",
                         600, pointer, 8192);
                         pointer = pointer + 8192;

    /* Create an IP instance. */
    nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(1, 2, 3, 4),
                0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                pointer, 4096, 1);
                pointer = pointer + 4096;

    /* Create another packet pool. */
    nx_packet_pool_create(&pool_1, "NetX Packet Pool 1", 600, pointer, 8192);
                         pointer = pointer + 8192;

    /* Create another IP instance. */
    nx_ip_create(&ip_1, "NetX IP Instance 1", IP_ADDRESS(1, 2, 3, 5),
                0xFFFFFF00UL, &pool_1, _nx_ram_network_driver,
                pointer, 4096, 1);
                pointer = pointer + 4096;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    nx_arp_enable(&ip_0, (void *) pointer, 1024);
                 pointer = pointer + 1024;

    /* Enable ARP and supply ARP cache memory for IP Instance 1. */
    nx_arp_enable(&ip_1, (void *) pointer, 1024);
                 pointer = pointer + 1024;

    /* Enable TCP processing for both IP instances. */
    nx_tcp_enable(&ip_0);
    nx_tcp_enable(&ip_1);

    /* Open the RAM disk. */
                 _fx_ram_driver, ram_disk_memory, pointer, 4096) ;
                 pointer += 4096;

    /* Create the NetX HTTP Server. */
    nx_http_server_create(&my_server, "My HTTP Server", &ip_1, &ram_disk,
                         pointer, 4096, &pool_1, authentication_check, NX_NULL);
                         pointer = pointer + 4096;

    /* Start the HTTP Server. */
    nx_http_server_start(&my_server);
}

/* Define the test thread. */
void     thread_0_entry(ULONG thread_input)
{

NX_PACKET     *my_packet;
UINT          status;

    /* Create an HTTP client instance. */
    status = nx_http_client_create(&my_client, "My Client", &ip_0,
                                  &pool_0, 600);

    /* Check status. */
    if (status)
        error_counter++;

    /* Prepare to send the simple 103-byte HTML file to the Server. */
    status = nx_http_client_put_start(&my_client, IP_ADDRESS(1,2,3,5),
                                      "/test.htm", "name", "password", 103, 50);
    /* Check status. */
    if (status)
        error_counter++;

    /* Allocate a packet. */
    status = nx_packet_allocate(&pool_0, &my_packet, NX_TCP_PACKET,
                               NX_WAIT_FOREVER);
    /* Check status. */
    if (status != NX_SUCCESS)
        return;

    /* Build a simple 103-byte HTML page. */
    nx_packet_data_append(my_packet, "<HTML>\r\n", 8,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet,
                         "<HEAD><TITLE>NetX HTTP Test</TITLE></HEAD>\r\n", 44,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<BODY>\r\n", 8,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<H1>NetX Test Page</H1>\r\n", 25,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</BODY>\r\n", 9,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</HTML>\r\n", 9,
                         &pool_0, NX_WAIT_FOREVER);

    /* Complete the PUT by writing the total length. */
    status = **nx_http_client_put_packet**(&my_client, my_packet, 50);

    /* Check status. */
    if (status)
        error_counter++;

    /* Now GET the file back! */
    status = nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5),
                                     "/test.htm", NX_NULL, 0, "name", 
                                     "password", 50);

    /* Check status. */
    if (status)
        error_counter++;

    /* Get a packet. */
    status = nx_http_client_get_packet(&my_client, &my_packet, 20);

    /* Check for an error. */
    if ((status) || (my_packet -> nx_packet_length != 103))
        error_counter++;

    /* Check to see if we have a packet. */
    if (status == NX_SUCCESS)
    {

        /* Yes, release it! */
        nx_packet_release(my_packet);
    }

    /* Flush the media. */
     fx_media_flush(&ram_disk);
 }
```

<span data-ttu-id="15812-138">Şekil 1,1 NetX ile HTTP kullanımı örneği</span><span class="sxs-lookup"><span data-stu-id="15812-138">Figure 1.1 Example of HTTP use with NetX</span></span>

## <a name="configuration-options"></a><span data-ttu-id="15812-139">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="15812-139">Configuration Options</span></span>

<span data-ttu-id="15812-140">NetX için HTTP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="15812-140">There are several configuration options for building HTTP for NetX.</span></span> <span data-ttu-id="15812-141">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15812-141">Following is a list of all options, where each is described in detail.</span></span> <span data-ttu-id="15812-142">Varsayılan değerler listelenir, ancak *nx_http_client. h ve nx_http_server. h*'ye dahil etmeden önce yeniden tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="15812-142">The default values are listed, but can be redefined prior to inclusion of *nx_http_client.h and nx_http_server.h*:</span></span>

- <span data-ttu-id="15812-143">**NX_DISABLE_ERROR_CHECKING** Tanımlı, bu seçenek temel HTTP hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="15812-143">**NX_DISABLE_ERROR_CHECKING** Defined, this option removes the basic HTTP error checking.</span></span> <span data-ttu-id="15812-144">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="15812-144">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="15812-145">**NX_HTTP_SERVER_PRIORITY** HTTP sunucusu iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="15812-145">**NX_HTTP_SERVER_PRIORITY** The priority of the HTTP Server thread.</span></span> <span data-ttu-id="15812-146">Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-146">By default, this value is defined as 16 to specify priority 16.</span></span>
- <span data-ttu-id="15812-147">**NX_HTTP_NO_FILEX** Tanımlı, bu seçenek FileX bağımlılıkları için bir saplama sağlar.</span><span class="sxs-lookup"><span data-stu-id="15812-147">**NX_HTTP_NO_FILEX** Defined, this option provides a stub for FileX dependencies.</span></span> <span data-ttu-id="15812-148">Bu seçenek tanımlandıysa, HTTP Istemcisi herhangi bir değişiklik yapılmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="15812-148">The HTTP Client will function without any change if this option is defined.</span></span> <span data-ttu-id="15812-149">HTTP sunucusunun değiştirilmesi veya kullanıcının düzgün çalışması için bir çok sayıda FileX hizmeti oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="15812-149">The HTTP Server will need to either be modified or the user will have to create a handful of FileX services in order to function properly.</span></span>
- <span data-ttu-id="15812-150">**NX_HTTP_TYPE_OF_SERVICE** HTTP TCP istekleri için gereken hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="15812-150">**NX_HTTP_TYPE_OF_SERVICE** Type of service required for the HTTP TCP requests.</span></span> <span data-ttu-id="15812-151">Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-151">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="15812-152">**NX_HTTP_SERVER_THREAD_TIME_SLICE** Aynı önceliğe sahip iş parçacıklarını oluşturmadan önce, sunucu iş parçacığının çalışmasına izin verilen süreölçer onay işareti sayısı.</span><span class="sxs-lookup"><span data-stu-id="15812-152">**NX_HTTP_SERVER_THREAD_TIME_SLICE** The number of timer ticks the Server thread is allowed to run before yielding to threads of the same priority.</span></span> <span data-ttu-id="15812-153">Varsayılan değer 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="15812-153">The default value is 2.</span></span>
- <span data-ttu-id="15812-154">**NX_HTTP_FRAGMENT_OPTION** HTTP TCP istekleri için parça etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="15812-154">**NX_HTTP_FRAGMENT_OPTION** Fragment enable for HTTP TCP requests.</span></span> <span data-ttu-id="15812-155">Varsayılan olarak, bu değer HTTP TCP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT.</span><span class="sxs-lookup"><span data-stu-id="15812-155">By default, this value is NX_DONT_FRAGMENT to disable HTTP TCP fragmenting.</span></span>
- <span data-ttu-id="15812-156">**NX_HTTP_SERVER_WINDOW_SIZE** Sunucu yuvası pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="15812-156">**NX_HTTP_SERVER_WINDOW_SIZE** Server socket window size.</span></span> <span data-ttu-id="15812-157">Varsayılan olarak, bu değer 2048 bayttır.</span><span class="sxs-lookup"><span data-stu-id="15812-157">By default, this value is 2048 bytes.</span></span>
- <span data-ttu-id="15812-158">**NX_HTTP_TIME_TO_LIVE** Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-158">**NX_HTTP_TIME_TO_LIVE** Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="15812-159">Varsayılan değer 0x80 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-159">The default value is set to 0x80.</span></span>
- <span data-ttu-id="15812-160">**NX_HTTP_SERVER_TIMEOUT** İç hizmetlerin askıya alınacağı ThreadX ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-160">**NX_HTTP_SERVER_TIMEOUT** Specifies the number of ThreadX ticks that internal services will suspend for.</span></span> <span data-ttu-id="15812-161">Varsayılan değer 10 saniyeye ayarlanır (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="15812-161">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="15812-162">**NX_HTTP_SERVER_TIMEOUT_ACCEPT** İç *nx_tcp_server_socket_accept* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-162">**NX_HTTP_SERVER_TIMEOUT_ACCEPT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_server_socket_accept* calls.</span></span> <span data-ttu-id="15812-163">Varsayılan değer (10 \* NX_IP_PERIODIC_RATE) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-163">The default value is set to (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="15812-164">**NX_HTTP_SERVER_TIMEOUT_DISCONNECT** İç *nx_tcp_socket_disconnect* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-164">**NX_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_disconnect* calls.</span></span> <span data-ttu-id="15812-165">Varsayılan değer 10 saniyeye ayarlanır (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="15812-165">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="15812-166">**NX_HTTP_SERVER_TIMEOUT_RECEIVE** İç *nx_tcp_socket_receive* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-166">**NX_HTTP_SERVER_TIMEOUT_RECEIVE** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_receive* calls.</span></span> <span data-ttu-id="15812-167">Varsayılan değer 10 saniyeye ayarlanır (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="15812-167">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="15812-168">**NX_HTTP_SERVER_TIMEOUT_SEND** İç *nx_tcp_socket_send* çağrılarında iç hizmetlerin askıya alınacağı threadx ticks sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-168">**NX_HTTP_SERVER_TIMEOUT_SEND** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_send* calls.</span></span> <span data-ttu-id="15812-169">Varsayılan değer 10 saniyeye ayarlanır (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="15812-169">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="15812-170">**NX_HTTP_MAX_HEADER_FIELD** HTTP üst bilgisi alanının en büyük boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-170">**NX_HTTP_MAX_HEADER_FIELD** Specifies the maximum size of the HTTP header field.</span></span> <span data-ttu-id="15812-171">Varsayılan değer 256 ' dir.</span><span class="sxs-lookup"><span data-stu-id="15812-171">The default value is 256.</span></span>
- <span data-ttu-id="15812-172">**NX_HTTP_MULTIPART_ENABLE** Tanımlandıysa, HTTP sunucusunun çok parçalı HTTP isteklerini desteklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="15812-172">**NX_HTTP_MULTIPART_ENABLE** If defined, enables HTTP Server to support multipart HTTP requests.</span></span>
- <span data-ttu-id="15812-173">**NX_HTTP_SERVER_MAX_PENDING** HTTP sunucusu için sıraya alınabilen bağlantı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-173">**NX_HTTP_SERVER_MAX_PENDING** Specifies the number of connections that can be queued for the HTTP Server.</span></span> <span data-ttu-id="15812-174">Varsayılan değer 5 ' e ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-174">The default value is set to 5.</span></span>
- <span data-ttu-id="15812-175">**NX_HTTP_MAX_RESOURCE** İstemci tarafından sağlanan *kaynak adında* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-175">**NX_HTTP_MAX_RESOURCE** Specifies the number of bytes allowed in a client supplied *resource name*.</span></span> <span data-ttu-id="15812-176">Varsayılan değer 40 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-176">The default value is set to 40.</span></span>
- <span data-ttu-id="15812-177">**NX_HTTP_MAX_NAME** İstemci tarafından sağlanan *Kullanıcı adında* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-177">**NX_HTTP_MAX_NAME** Specifies the number of bytes allowed in a client supplied *username*.</span></span> <span data-ttu-id="15812-178">Varsayılan değer 20 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-178">The default value is set to 20.</span></span>
- <span data-ttu-id="15812-179">**NX_HTTP_MAX_PASSWORD** İstemci tarafından sağlanan *parolada* izin verilen bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-179">**NX_HTTP_MAX_PASSWORD** Specifies the number of bytes allowed in a client supplied *password*.</span></span> <span data-ttu-id="15812-180">Varsayılan değer 20 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-180">The default value is set to 20.</span></span>
- <span data-ttu-id="15812-181">**NX_HTTP_SERVER_MIN_PACKET_SIZE** Sunucu oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-181">**NX_HTTP_SERVER_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at Server creation.</span></span> <span data-ttu-id="15812-182">En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="15812-182">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="15812-183">Varsayılan değer 600 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-183">The default value is set to 600.</span></span>
- <span data-ttu-id="15812-184">**NX_HTTP_CLIENT_MIN_PACKET_SIZE** Istemci oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-184">**NX_HTTP_CLIENT_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at Client creation.</span></span> <span data-ttu-id="15812-185">En küçük boyut, HTTP üstbilgisinin tamamının tek bir pakette yer aldığından emin olmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="15812-185">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="15812-186">Varsayılan değer 300 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-186">The default value is set to 300.</span></span>
- <span data-ttu-id="15812-187">**NX_HTTP_SERVER_RETRY_SECONDS** *sunucu yuvası yeniden aktarım zaman aşımını saniye cinsinden ayarlayın. Varsayılan değer* 2 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-187">**NX_HTTP_SERVER_RETRY_SECONDS** *Set the Server socket retransmission timeout in seconds. The* default value is set to 2.</span></span>
- <span data-ttu-id="15812-188">**NX_HTTP_SERVER_RETRY_MAX** Bu, sunucu yuvasıyla maksimum yeniden iletim sayısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="15812-188">**NX_HTTP_SERVER_RETRY_MAX** This sets the maximum number of retransmissions on Server socket.</span></span> <span data-ttu-id="15812-189">Varsayılan değer 10 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-189">The default value is set to 10.</span></span>
- <span data-ttu-id="15812-190">**NX_HTTP_SERVER_RETRY_SHIFT** Bu değer, sonraki yeniden iletim zaman aşımını ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="15812-190">**NX_HTTP_SERVER_RETRY_SHIFT** This value is used to set the next retransmission timeout.</span></span> <span data-ttu-id="15812-191">Geçerli zaman aşımı, bu nedenle, yuva zaman aşımı kaydırma değerine göre kaydırılan, o kadar yeniden iletim sayısı ile çarpılır.</span><span class="sxs-lookup"><span data-stu-id="15812-191">The current timeout is multiplied by the number of retransmissions thus far, shifted by the value of the socket timeout shift.</span></span> <span data-ttu-id="15812-192">Zaman aşımını katlama için varsayılan değer 1 ' e ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-192">The default value is set to 1 for doubling the timeout.</span></span>
- <span data-ttu-id="15812-193">**NX_HTTP_ SERVER_TRANSMIT_QUEUE_DEPTH** Bu, sunucu yuvası yeniden iletim kuyruğunda sıraya alınabilen en fazla paket sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="15812-193">**NX_HTTP_ SERVER_TRANSMIT_QUEUE_DEPTH** This specifies the maximum number of packets that can be enqueued on the Server socket retransmission queue.</span></span> <span data-ttu-id="15812-194">Sıraya alınan paketlerin sayısı bu sayıya ulaşırsa, bir veya daha fazla sıraya alınmış paket yayınlanana kadar başka paket gönderilemez.</span><span class="sxs-lookup"><span data-stu-id="15812-194">If the number of packets enqueued reaches this number, no more packets can be sent until one or more enqueued packets are released.</span></span> <span data-ttu-id="15812-195">Varsayılan değer 20 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="15812-195">The default value is set to 20.</span></span>