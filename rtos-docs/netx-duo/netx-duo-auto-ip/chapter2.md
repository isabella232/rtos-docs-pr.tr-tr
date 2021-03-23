---
title: Bölüm 2-Azure RTOS NetX Duo Oto IP 'yi yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX Duo Oto IP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 42c58a4cdec34a03eda9f42315438e5fbe2ea594
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826170"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-autoip"></a><span data-ttu-id="c81bf-103">Bölüm 2-Azure RTOS NetX Duo Oto IP 'yi yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="c81bf-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo AutoIP</span></span>

<span data-ttu-id="c81bf-104">Bu bölümde, Azure RTOS NetX Duo Oto IP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo AutoIP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="c81bf-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="c81bf-105">Product Distribution</span></span>

<span data-ttu-id="c81bf-106">Azure RTOS NetX Oto, konumundaki genel kaynak kodu depomızdan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="c81bf-106">Azure RTOS NetX AutoIP can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="c81bf-107">Bu paket üç kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir PDF dosyası içerir ve aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="c81bf-107">The package includes three source files, one include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="c81bf-108">**nx_auto_ip. h**: NETX Oto için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="c81bf-108">**nx_auto_ip.h**: Header file for NetX AutoIP</span></span>
- <span data-ttu-id="c81bf-109">**nx_auto_ip. c**: NETX oto Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="c81bf-109">**nx_auto_ip.c**: C Source file for NetX AutoIP</span></span>
- <span data-ttu-id="c81bf-110">**demo_netx_auto_ip. c**: NETX Oto IP tanıtımı Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="c81bf-110">**demo_netx_auto_ip.c**: C Source file for NetX AutoIP Demo</span></span>
- <span data-ttu-id="c81bf-111">**nx_auto_ip.pdf**: NETX otomatik IP 'nin PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="c81bf-111">**nx_auto_ip.pdf**: PDF description of NetX AutoIP</span></span>

## <a name="autoip-installation"></a><span data-ttu-id="c81bf-112">Oto IP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="c81bf-112">AutoIP Installation</span></span>

<span data-ttu-id="c81bf-113">NetX oto 'nin kullanılabilmesi için, daha önce bahsedilen tüm dağıtımın, NetX ' in yüklü olduğu dizine kopyalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81bf-113">In order to use NetX AutoIP, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="c81bf-114">Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_auto_ip. h*, *nx_auto_ip. c* ve *demo_netx_auto_ip. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-114">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_auto_ip.h*, *nx_auto_ip.c*, and *demo_netx_auto_ip.c* files should be copied into this directory.</span></span>

## <a name="using-autoip"></a><span data-ttu-id="c81bf-115">Oto IP 'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="c81bf-115">Using AutoIP</span></span>

<span data-ttu-id="c81bf-116">NetX oto kullanımı kolaydır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-116">Using NetX AutoIP is easy.</span></span> <span data-ttu-id="c81bf-117">Temel olarak uygulama kodu, ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_auto_ip. h* 'yi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c81bf-117">Basically, the application code must include *nx_auto_ip.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span> <span data-ttu-id="c81bf-118">*Nx_auto_ip. h* eklendikten sonra, uygulama kodu daha sonra bu kılavuzun ilerleyen kısımlarında belirtilen Oto IP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="c81bf-118">Once *nx_auto_ip.h* is included, the application code is then able to make the AutoIP function calls specified later in this guide.</span></span> <span data-ttu-id="c81bf-119">Uygulama, yapı işlemine *nx_auto_ip. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c81bf-119">The application must also include *nx_auto_ip.c* in the build process.</span></span> <span data-ttu-id="c81bf-120">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-120">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="c81bf-121">Bu, NetX Oto IP 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c81bf-121">This is all that is required to use NetX AutoIP.</span></span>

> [!NOTE]
> <span data-ttu-id="c81bf-122">CIP, NetX ARP hizmetlerini kullandığından, bu ARP,, Oto IP kullanılmadan önce *nx_arp_enable* çağrısıyla etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c81bf-122">Since AutoIP utilizes NetX ARP services, ARP must be enabled with the *nx_arp_enable* call prior to using AutoIP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="c81bf-123">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="c81bf-123">Small Example System</span></span>

<span data-ttu-id="c81bf-124">NetX oto kullanmanın ne kadar kolay olduğunu gösteren örnek şekil 1,1 ' de aşağıda gösterilen şekilde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-124">An example of how easy it is to use NetX AutoIP is described in Figure 1.1, which appears below.</span></span> <span data-ttu-id="c81bf-125">Bu örnekte, *nx_auto_ip. h* olan Oto IP içerme dosyası, Line 002 ' de getirilir.</span><span class="sxs-lookup"><span data-stu-id="c81bf-125">In this example, the AutoIP include file *nx_auto_ip.h* is brought in at line 002.</span></span> <span data-ttu-id="c81bf-126">Ardından, NetX Oto IP örneği, 090 satırındaki "*tx_application_define*" içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c81bf-126">Next, the NetX AutoIP instance is created in "*tx_application_define*" at line 090.</span></span> <span data-ttu-id="c81bf-127">NetX Oto IP denetim bloğunun "auto_ip_0" daha önce satır 015 adresinde genel bir değişken olarak tanımlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c81bf-127">Note that the NetX AutoIP control block "auto_ip_0" was defined previously as a global variable at line 015.</span></span> <span data-ttu-id="c81bf-128">Başarılı bir şekilde oluşturulduktan sonra, 098. satırda bir NetX oto başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-128">After successful creation, an NetX AutoIP is started at line 098.</span></span> <span data-ttu-id="c81bf-129">IP adresi değiştirme geri çağırma işlevi işlemi, sonraki çakışmaları veya olası DHCP adresi çözümlemesini işlemek için kullanılan 105. satırda başlar.</span><span class="sxs-lookup"><span data-stu-id="c81bf-129">The IP address change callback function processing starts at line 105, which is used to handle subsequent conflicts or possible DHCP address resolution.</span></span>

> [!NOTE]
> <span data-ttu-id="c81bf-130">Aşağıdaki örnekte konak cihazının tek bilgisayarlı bir cihaz olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-130">The example below assumes the host device is a single-homed device.</span></span> <span data-ttu-id="c81bf-131">Birden çok sayfalı bir cihaz için, konak uygulama NetX Oto IP hizmetini kullanarak bir IP adresini yoklamanın ikincil ağ arabirimini belirtmek üzere *nx_auto_ip_interface_*.</span><span class="sxs-lookup"><span data-stu-id="c81bf-131">For a multihomed device, the host application can use the NetX AutoIP service *nx_auto_ip_interface_* set to specify a secondary network interface to probe for an IP address.</span></span> <span data-ttu-id="c81bf-132">Birden çok ağ bağlantılı uygulamalar ayarlama hakkında daha fazla bilgi için [NETX Kullanıcı kılavuzuna](https://docs.microsoft.com/azure/rtos/netx/about-this-guide) bakın.</span><span class="sxs-lookup"><span data-stu-id="c81bf-132">See the [NetX User Guide](https://docs.microsoft.com/azure/rtos/netx/about-this-guide) for more details on setting up multihomed applications.</span></span> <span data-ttu-id="c81bf-133">Ana bilgisayar uygulamasının, IP adresi elde ettiğini doğrulamak için NetX API *nx_status_ip_interface_check* kullanması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c81bf-133">Note further that the host application should use the NetX API *nx_status_ip_interface_check* to verify AutoIP has obtained an IP address.</span></span>

```c
#include "tx_api.h"
#include "nx_api.h"
#include "nx_auto_ip.h"

#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD              thread_0;
NX_PACKET_POOL         pool_0;
NX_IP                  ip_0;

/* Define the AUTO IP structures for the IP instance. */

NX_AUTO_IP             auto_ip_0;

/* Define the counters used in the demo application... */

ULONG                 thread_0_counter;
ULONG                 address_changes;
ULONG                 error_counter;

/* Define thread prototypes. */
void     thread_0_entry(ULONG thread_input);
void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

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
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    16, 16, 1, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
                                    pointer, 4096);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Create an IP instance. */
    status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 4096, 1);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
        error_counter++;

    /* Create the AutoIP instance for IP Instance 0. */
    status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
    pointer = pointer + 4096;

    /* Check AutoIP create status. */
    if (status)
        error_counter++;

    /* Start AutoIP instances. */
    status = **nx_auto_ip_start**(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);

    /* Check AutoIP start status. */
    if (status)
        error_counter++;

    /* Register an IP address change function for IP Instance 0. */
    status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
                                        (void *) &auto_ip_0);

    /* Check IP address change notify status. */
    if (status)
        error_counter++;
}

/* Define the test thread. */

void     thread_0_entry(ULONG thread_input)
{

UINT     status;
ULONG    actual_status;

    /* Wait for IP address to be resolved. */
    do
    {

        /* Call IP status check routine. */
        status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
            &actual_status, 10000);

    } while (status != NX_SUCCESS);

    /* Since the IP address is resolved at this point, the application can now fully utilize NetX! */

    while(1)
    {

        /* Increment thread 0's counter. */
        thread_0_counter++;

        /* Sleep... */
        tx_thread_sleep(10);
    }
}

void          ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
{

ULONG         ip_address;
ULONG         network_mask;
NX_AUTO_IP    *auto_ip_ptr;

    /* Setup pointer to auto IP instance. */
    auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;

    /* Pickup the current IP address. */
    nx_ip_address_get(ip_ptr, &ip_address, &network_mask);

    /* Determine if the IP address has changed back to zero. If so, make sure the AutoIP instance is started. */
    if (ip_address == 0)
    {

        /* Get the last AutoIP address for this node. */
        nx_auto_ip_get_address(auto_ip_ptr, &ip_address);

        /* Start this AutoIP instance. */
        nx_auto_ip_start(auto_ip_ptr, ip_address);
        }

    /* Determine if IP address has transitioned to a non local IP address. */
    else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
    {

        /* Stop the AutoIP processing. */
        nx_auto_ip_stop(auto_ip_ptr);
    }

    /* Increment a counter. */
    address_changes++;
}
```

<span data-ttu-id="c81bf-134">Şekil 1,1 NetX ile Oto IP kullanımı örneği</span><span class="sxs-lookup"><span data-stu-id="c81bf-134">Figure 1.1 Example of AutoIP use with NetX</span></span>

## <a name="configuration-options"></a><span data-ttu-id="c81bf-135">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="c81bf-135">Configuration Options</span></span>

<span data-ttu-id="c81bf-136">NetX AutoSize oluşturmak için birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-136">There are several configuration options for building NetX AutoIP.</span></span> <span data-ttu-id="c81bf-137">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c81bf-137">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="c81bf-138">**NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel Oto IP hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-138">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic AutoIP error checking.</span></span> <span data-ttu-id="c81bf-139">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-139">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="c81bf-140">**NX_AUTO_IP_PROBE_WAIT**: ilk yoklamayı göndermeden önce beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-140">**NX_AUTO_IP_PROBE_WAIT**: The number of seconds to wait before sending first probe.</span></span> <span data-ttu-id="c81bf-141">Varsayılan olarak, bu değer 1 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-141">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="c81bf-142">**NX_AUTO_IP_PROBE_NUM**: gönderilen ARP araştırmaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-142">**NX_AUTO_IP_PROBE_NUM**: The number of ARP probes to send.</span></span> <span data-ttu-id="c81bf-143">Varsayılan olarak, bu değer 3 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-143">By default, this value is defined as 3.</span></span>
- <span data-ttu-id="c81bf-144">**NX_AUTO_IP_PROBE_MIN**: Gönderen yoklamalar arasında beklenecek saniye sayısı alt sınırı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-144">**NX_AUTO_IP_PROBE_MIN**: The minimum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="c81bf-145">Varsayılan olarak, bu değer 1 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-145">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="c81bf-146">**NX_AUTO_IP_PROBE_MAX**: Gönderen yoklamalar arasında beklenecek en fazla saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-146">**NX_AUTO_IP_PROBE_MAX**: The maximum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="c81bf-147">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-147">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="c81bf-148">**NX_AUTO_IP_MAX_CONFLICTS**: işleme gecikmelerini arttırmadan önce, tekrar IP çakışmalarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-148">**NX_AUTO_IP_MAX_CONFLICTS**: The number of AutoIP conflicts before increasing processing delays.</span></span> <span data-ttu-id="c81bf-149">Varsayılan olarak, bu değer 10 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-149">By default, this value is defined as 10.</span></span>
- <span data-ttu-id="c81bf-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: Toplam çakışma sayısı aşıldığında bekleme süresinin uzaleceği saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: The number of seconds to extend the wait period when the total number of conflicts is exceeded.</span></span> <span data-ttu-id="c81bf-151">Varsayılan olarak, bu değer 60 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-151">By default, this value is defined as 60.</span></span>
- <span data-ttu-id="c81bf-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: duyuru gönderilmeden önce beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: The number of seconds to wait before sending announcement.</span></span> <span data-ttu-id="c81bf-153">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-153">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="c81bf-154">**NX_AUTO_IP_ANNOUNCE_NUM**: gönderileceği ARP duyurusu sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-154">**NX_AUTO_IP_ANNOUNCE_NUM**: The number of ARP announces to send.</span></span> <span data-ttu-id="c81bf-155">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-155">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="c81bf-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: gönderme duyurusu arasında beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: The number of seconds to wait between sending announces.</span></span> <span data-ttu-id="c81bf-157">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-157">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="c81bf-158">**NX_AUTO_IP_DEFEND_INTERVAL**: savunma duyurusu arasında beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="c81bf-158">**NX_AUTO_IP_DEFEND_INTERVAL**: The number of seconds to wait between defense announces.</span></span> <span data-ttu-id="c81bf-159">Varsayılan olarak, bu değer 10 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c81bf-159">By default, this value is defined as 10.</span></span>
