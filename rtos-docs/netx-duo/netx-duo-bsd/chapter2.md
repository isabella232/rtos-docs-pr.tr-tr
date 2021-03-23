---
title: Bölüm 2-Azure RTOS NetX Duo BSD yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX Duo BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 582661bc66c51341fc098de9ff7b6fa2a7d746de
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826153"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-bsd"></a><span data-ttu-id="e6fd6-103">Bölüm 2-Azure RTOS NetX Duo BSD yüklemesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="e6fd6-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo BSD</span></span>

<span data-ttu-id="e6fd6-104">Bu bölümde, Azure RTOS NetX Duo BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo BSD component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="e6fd6-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="e6fd6-105">Product Distribution</span></span>

<span data-ttu-id="e6fd6-106">Azure RTOS NetX Duo BSD, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="e6fd6-106">Azure RTOS NetX Duo BSD can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="e6fd6-107">Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="e6fd6-108">**nxd_bsd. h**: NETX Duo BSD için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="e6fd6-108">**nxd_bsd.h**: Header file for NetX Duo BSD</span></span>
- <span data-ttu-id="e6fd6-109">**nxd_bsd. c**: NETX Duo BSD Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="e6fd6-109">**nxd_bsd.c**: C Source file for NetX Duo BSD</span></span>
- <span data-ttu-id="e6fd6-110">**nxd_bsd.pdf**: NETX Duo BSD Kullanıcı Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="e6fd6-110">**nxd_bsd.pdf**: User Guide for NetX Duo BSD</span></span>

<span data-ttu-id="e6fd6-111">Tanıtım dosyaları:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-111">Demo files:</span></span>

- <span data-ttu-id="e6fd6-112">**bsd_demo_udp. c**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-112">**bsd_demo_udp.c**</span></span>
- <span data-ttu-id="e6fd6-113">**bsd_demo_tcp. c**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-113">**bsd_demo_tcp.c**</span></span>
- <span data-ttu-id="e6fd6-114">**bsd_demo_raw. c**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-114">**bsd_demo_raw.c**</span></span>

## <a name="netx-duo-bsd-installation"></a><span data-ttu-id="e6fd6-115">NetX Duo BSD yüklemesi</span><span class="sxs-lookup"><span data-stu-id="e6fd6-115">NetX Duo BSD Installation</span></span>

<span data-ttu-id="e6fd6-116">NetX Duo BSD 'yi kullanmak için, daha önce bahsedilen dağıtımın tamamının NetX Duo 'un yüklü olduğu dizine kopyalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-116">In order to use NetX Duo BSD the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="e6fd6-117">Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_bsd. h* ve *nxd_bsd. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-117">For example, if NetX Duo is installed in the directory "*\threadx\arm7\green*" then the *nxd_bsd.h* and *nxd_bsd.c* files should be copied into this directory.</span></span>

## <a name="building-the-threadx-and-netx-duo-components-of-a-bsd-application"></a><span data-ttu-id="e6fd6-118">Bir BSD uygulamasının ThreadX ve NetX Duo bileşenlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6fd6-118">Building the ThreadX and NetX Duo components of a BSD Application</span></span>

### <a name="threadx"></a><span data-ttu-id="e6fd6-119">ThreadX</span><span class="sxs-lookup"><span data-stu-id="e6fd6-119">ThreadX</span></span>

<span data-ttu-id="e6fd6-120">ThreadX Kitaplığı `bsd_errno` iş parçacığı yerel depolama alanında tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-120">The ThreadX library must define `bsd_errno` in the thread local storage.</span></span> <span data-ttu-id="e6fd6-121">Aşağıdaki yordamı öneririz:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-121">We recommend the following procedure:</span></span>

1. <span data-ttu-id="e6fd6-122">*Tx_port. h*'de TX_THREAD_EXTENSION makrolarından birini aşağıdaki şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-122">In *tx_port.h*, set one of the TX_THREAD_EXTENSION macros as follows:</span></span>
   - `#define TX_THREAD_EXTENSION_3     int bsd_errno`

1. <span data-ttu-id="e6fd6-123">ThreadX kitaplığını yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-123">Rebuild the ThreadX library.</span></span>

> [!NOTE]
> <span data-ttu-id="e6fd6-124">TX_THREAD_EXTENSION_3 zaten kullanılıyorsa, Kullanıcı diğer TX_THREAD_EXTENSION makrolarından birini kullanücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-124">If TX_THREAD_EXTENSION_3 is already used, the user is free to use one of the other TX_THREAD_EXTENSION macros.</span></span>

### <a name="netx-duo"></a><span data-ttu-id="e6fd6-125">NetX Duo</span><span class="sxs-lookup"><span data-stu-id="e6fd6-125">NetX Duo</span></span>

<span data-ttu-id="e6fd6-126">NetX Duo BSD hizmetlerini kullanmadan önce, NetX Duo kitaplığı tanımlı NX_ENABLE_EXTENDED_NOTIFY_SUPPORT oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-126">Before using NetX Duo BSD Services, the NetX Duo library must be built with NX_ENABLE_EXTENDED_NOTIFY_SUPPORT defined.</span></span> <span data-ttu-id="e6fd6-127">Varsayılan olarak tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-127">By default it is not defined.</span></span> <span data-ttu-id="e6fd6-128">BSD RAW yuvaları kullanılacaksa, NetX Duo kitaplığı tanımlı NX_ENABLE_IP_RAW_PACKET_FILTER oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-128">If the BSD raw sockets are to be used, the NetX Duo library must be built with NX_ENABLE_IP_RAW_PACKET_FILTER defined.</span></span>

## <a name="using-netx-duo-bsd"></a><span data-ttu-id="e6fd6-129">NetX Duo BSD kullanma</span><span class="sxs-lookup"><span data-stu-id="e6fd6-129">Using NetX Duo BSD</span></span>

<span data-ttu-id="e6fd6-130">NetX Duo BSD uygulaması projesi, bu kılavuzda daha sonra belirtilen BSD hizmetlerini kullanabilmek için *tx_api. h* ve *nx_api. h* bilgilerini *nxd_bsd* içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-130">A NetX Duo BSD application project must include *nxd_bsd.h* after it includes *tx_api.h* and *nx_api.h* to be able to use BSD services specified later in this guide.</span></span> <span data-ttu-id="e6fd6-131">Uygulama, yapı işlemine *nxd_bsd. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-131">The application must also include *nxd_bsd.c* in the build process.</span></span> <span data-ttu-id="e6fd6-132">Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-132">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="e6fd6-133">Bu, NetX Duo BSD 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-133">This is all that is required to use NetX Duo BSD.</span></span>

<span data-ttu-id="e6fd6-134">NetX Duo BSD hizmetlerini kullanmak için, uygulamanın bir IP örneği oluşturması, ' den paket ayırabilmesi için BSD katmanı için bir paket havuzu oluşturması, iç BSD iş parçacığı yığını için bellek alanı ayırması ve iç BSD iş parçacığının önceliğini belirtmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-134">To utilize NetX Duo BSD services, the application must create an IP instance, create a packet pool for the BSD layer to allocate packets from, allocate memory space for the internal BSD thread stack, and specify the priority of the internal BSD thread.</span></span> <span data-ttu-id="e6fd6-135">BSD katmanı, *bsd_initialize* çağırarak ve parametrelerine geçerek başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-135">The BSD layer is initialized by calling *bsd_initialize* and passing in the parameters.</span></span> <span data-ttu-id="e6fd6-136">Bu belgede daha sonra "küçük örneklerde" gösterilmiştir, ancak prototip aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-136">This is demonstrated in the "Small Examples" later in this document but the prototype is shown below:</span></span>

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                    *CHAR *bsd_thread_stack_area,
                    *ULONG bsd_thread_stack_size,
                    *UINT bsd_thread_priority*);
```

<span data-ttu-id="e6fd6-137">Default_ip, BSD katmanının üzerinde çalıştığı IP örneğidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-137">The default_ip is the IP instance the BSD layer operates on.</span></span> <span data-ttu-id="e6fd6-138">Default_pool, BSD Hizmetleri tarafından paketleri ayırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-138">The default_pool is used by the BSD services to allocate packets from.</span></span> <span data-ttu-id="e6fd6-139">Sonraki iki parametre: bsd_thread_stack_area, bsd_thread_stack_size iç BSD iş parçacığı tarafından kullanılan yığın alanını ve bsd_thread_priority son parametresini tanımlar, iş parçacığının önceliğini belirler.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-139">The next two parameters: bsd_thread_stack_area, bsd_thread_stack_size defines the stack area used by the internal BSD thread, and the last parameter, bsd_thread_priority, sets the priority of the thread.</span></span>

## <a name="netx-duo-bsd-raw-socket-support"></a><span data-ttu-id="e6fd6-140">NetX Duo BSD Ham yuva desteği</span><span class="sxs-lookup"><span data-stu-id="e6fd6-140">NetX Duo BSD Raw Socket Support</span></span>

<span data-ttu-id="e6fd6-141">NetX Duo BSD, ham yuvaları da destekler.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-141">NetX Duo BSD also supports raw sockets.</span></span> <span data-ttu-id="e6fd6-142">NetX Duo BSD içindeki ham yuvaları kullanmak için, NetX Duo kitaplığı tanımlı NX_ENABLE_IP_RAW_PACKET_FILTER ile derlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-142">To use raw sockets in NetX Duo BSD, the NetX Duo library must be compiled with NX_ENABLE_IP_RAW_PACKET_FILTER defined.</span></span> <span data-ttu-id="e6fd6-143">Varsayılan olarak tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-143">By default it is not defined.</span></span> <span data-ttu-id="e6fd6-144">Uygulama daha sonra nx_ip_raw_packet_enable çağırarak önceden oluşturulmuş bir IP örneği için ham yuva işlemeyi etkinleştirmelidir *.*</span><span class="sxs-lookup"><span data-stu-id="e6fd6-144">The application must then enable raw socket processing for a previously created IP instance by calling *nx_ip_raw_packet_enable.*</span></span>

<span data-ttu-id="e6fd6-145">NetX Duo BSD içinde Ham yuva oluşturmak için, uygulama yuva oluşturma hizmeti *yuvasını* kullanır ve protokol ailesini, yuva türünü ve protokolünü belirtir:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-145">To create a raw socket in NetX Duo BSD, the application uses the socket create service *socket* and specifies the protocol family, socket type and protocol:</span></span>

```c
sock_1 = socket(INT protocolFamily, INT socket_type, INT protocol)
```

<span data-ttu-id="e6fd6-146">protocolFamily, IP örneğinde IPv6 'nın etkin olduğu varsayılarak IPv4 yuvaları için AF_INET veya IPv6 yuvaları için AF_INET6.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-146">protocolFamily is AF_INET for IPv4 sockets, or AF_INET6 for IPv6 sockets, assuming IPv6 is enabled on the IP instance.</span></span> <span data-ttu-id="e6fd6-147">Socket_type SOCK_RAW olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-147">The socket_type must be set to SOCK_RAW.</span></span> <span data-ttu-id="e6fd6-148">protokol uygulamaya özeldir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-148">protocol is application specific.</span></span>

<span data-ttu-id="e6fd6-149">Ham paketleri göndermek ve almak ve ham bir yuvayı kapatmak için, uygulama genellikle UDP için aynı BSD hizmetlerini kullanır örn. *SendTo, recvfrom, select* ve *soc_close*.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-149">To send and receive raw packets as well as close a raw socket, the application typically uses the same BSD services as for UDP e.g. *sendto, recvfrom, select* and *soc_close*.</span></span> <span data-ttu-id="e6fd6-150">Ham yuvalar, BSD hizmetlerini *kabul* veya *dinlemeyi* desteklemez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-150">Raw sockets do not support either *accept* or *listen* BSD services.</span></span>

- <span data-ttu-id="e6fd6-151">Varsayılan olarak, alınan IPv4 ham verileri IPv4 üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-151">By default, received IPv4 raw data includes the IPv4 header.</span></span>  <span data-ttu-id="e6fd6-152">Buna karşılık, alınan IPv6 ham verileri IPv6 üst bilgisini içermez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-152">Conversely, received IPv6 raw data does not include the IPv6 header.</span></span>

- <span data-ttu-id="e6fd6-153">Varsayılan olarak, ham IPv6 veya IPv4 paketleri gönderilirken, BSD sarmalayıcı katmanı, verileri göndermeden önce IPv6 veya IPv4 üstbilgisini ekler.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-153">By default, when sending either raw IPv6 or IPv4 packets, the BSD wrapper layer adds the IPv6 or IPv4 header before sending the data.</span></span>

<span data-ttu-id="e6fd6-154">NetX Duo BSD IP_RAW_RX_NO_HEADER, IP_HDRINCL ve IP_RAW_IPV6_HDRINCL dahil ek ham yuva seçeneklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-154">NetX Duo BSD supports additional raw socket options, including IP_RAW_RX_NO_HEADER, IP_HDRINCL and IP_RAW_IPV6_HDRINCL.</span></span>

<span data-ttu-id="e6fd6-155">IP_RAW_RX_NO_HEADER ayarlandıysa IPv4 üst bilgisi kaldırılır, böylece alınan veriler IPv4 üst bilgisini içermez ve bildirilen ileti uzunluğu IPv4 üst bilgisini içermez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-155">If IP_RAW_RX_NO_HEADER is set, the IPv4 header is removed so that the received data does not contain the IPv4 header, and the reported message length does not include the IPv4 header.</span></span>  <span data-ttu-id="e6fd6-156">IPv6 yuvaları için, varsayılan olarak ham yuva alma, IP_RAW_RX_NO_HEADER seçenek kümesine sahip olacak şekilde IPv6 üst bilgisini içermez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-156">For IPv6 sockets, by default the raw socket receive does not include IPv6 header, equivalent to having the IP_RAW_RX_NO_HEADER option set.</span></span> <span data-ttu-id="e6fd6-157">Uygulama, IP_RAW_RX_NO_HEADER seçeneğini temizlemek için *setsockopt* hizmetini kullanabilir, IP_RAW_RX_NO_HEADER seçeneği silinirse, alınan IPv6 RAW verileri IPv6 üst bilgisini içerir ve bildirilen Ileti uzunluğu IPv6 üstbilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-157">Application may use the *setsockopt* service to clear the IP_RAW_RX_NO_HEADER option, Once the IP_RAW_RX_NO_HEADER option is cleared, the received IPv6 raw data would include the IPv6 header, and the reported message length includes the IPv6 header.</span></span>

<span data-ttu-id="e6fd6-158">Bu seçeneğin IPv4 veya IPv6 iletilen verileri üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-158">This option has no effect on IPv4 or IPv6 transmitted data.</span></span>

<span data-ttu-id="e6fd6-159">IP_HDRINCL ayarlandıysa, uygulama veri gönderirken IPv4 üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-159">If IP_HDRINCL is set, the application includes the IPv4 header when sending data.</span></span>  <span data-ttu-id="e6fd6-160">Bu seçeneğin IPv6 iletimi üzerinde hiçbir etkisi yoktur ve varsayılan olarak tanımlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-160">This option has no effect on IPv6 transmission and is not defined by default.</span></span> <span data-ttu-id="e6fd6-161">IP_RAW_IPV6_HDRINCL ayarlandıysa, uygulama veri gönderirken IPv6 üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-161">If IP_RAW_IPV6_HDRINCL is set, the application includes the IPv6 header when sending data.</span></span>  <span data-ttu-id="e6fd6-162">Bu seçeneğin IPv4 iletimi üzerinde hiçbir etkisi yoktur ve varsayılan olarak tanımlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-162">This option has no effect on IPv4 transmission and is not defined by default.</span></span>

<span data-ttu-id="e6fd6-163">IP_HDRINCL ve IP_RAW_IPV6_HDRINCL IPv4 veya IPv6 alımı üzerinde hiçbir etkiye sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-163">IP_HDRINCL and IP_RAW_IPV6_HDRINCL have no effect on IPv4 or IPv6 reception.</span></span>

> [!NOTE]
> <span data-ttu-id="e6fd6-164">BSD 4,3 yuva belirtimi, çekirdeğin ham paketi her bir yuva alma arabelleğine kopyalamasını gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-164">The BSD 4.3 Socket specification specifies that the kernel must copy the raw packet to each socket receive buffer.</span></span> <span data-ttu-id="e6fd6-165">Ancak NetX Duo BSD 'de, aynı protokolü paylaşan birden çok yuva oluşturulduysa, davranış tanımsızdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-165">However in NetX Duo BSD, if multiple sockets are created sharing the same protocol, the behavior is undefined.</span></span>

## <a name="netx-duo-bsd-raw-packet-support"></a><span data-ttu-id="e6fd6-166">NetX Duo BSD ham paket desteği</span><span class="sxs-lookup"><span data-stu-id="e6fd6-166">NetX Duo BSD Raw Packet Support</span></span>

<span data-ttu-id="e6fd6-167">PPPoE için ham paket desteğini etkinleştirmek üzere NetX Duo BSD sarmalayıcısı NX_BSD_RAW_PPPOE_SUPPORT etkinleştirilmiş olarak derlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-167">To enable the raw packet support for PPPoE, NetX Duo BSD wrapper needs to be built with NX_BSD_RAW_PPPOE_SUPPORT enabled.</span></span>

<span data-ttu-id="e6fd6-168">Aşağıdaki komut, PPPoE ham paketlerini işlemek için bir BSD yuvası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-168">The following command creates a BSD socket to handle PPPoE raw packets:</span></span>

```c
Sockfd = socket(AF_PACKET, SOCK_RAW, protocol);
```

<span data-ttu-id="e6fd6-169">Geçerli BSD uygulamasının AF_PACKET Family 'de yalnızca iki protokol türü desteklenir</span><span class="sxs-lookup"><span data-stu-id="e6fd6-169">The current BSD implementation only supports two protocol types in AF_PACKET family</span></span>

- <span data-ttu-id="e6fd6-170">`ETHERTYPE_PPPOE_DISC`: PPPoE bulma paketleri.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-170">`ETHERTYPE_PPPOE_DISC`: PPPoE Discovery packets.</span></span> <span data-ttu-id="e6fd6-171">MAC veri çerçevesinde, bulma paketleri 0x8863 Ethernet çerçeve türüne sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-171">In the MAC data frame, the Discovery packets have the Ethernet frame type 0x8863.</span></span>

- <span data-ttu-id="e6fd6-172">`ETHERTYPE_PPPOE_SESS`: PPP oturum paketleri.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-172">`ETHERTYPE_PPPOE_SESS`: PPP Session packets.</span></span> <span data-ttu-id="e6fd6-173">MAC veri çerçevesinde, oturum paketleri 0x8864 Ethernet çerçeve türüne sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-173">In the MAC data frame, the Session packets have the Ethernet frame type 0x8864.</span></span>

<span data-ttu-id="e6fd6-174">Yapı, `sockaddr_ll` PPPoE çerçevelerini gönderirken veya alırken parametreleri belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-174">The structure `sockaddr_ll` is used to specify parameters when sending or receiving PPPoE frames.</span></span>

<span data-ttu-id="e6fd6-175">`struct sockaddr_ll` şöyle bildirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-175">`struct sockaddr_ll` is declared as:</span></span>

```c
struct sockaddr_ll
{
    USHORT  sll_family;     /* Must be AF_PACKET */
    USHORT  sll_protocol;   /* LL frame type */
    INT     sll_ifindex;    /* Interface Index. */
    USHORT  sll_hatype;     /* Header type */
    UCHAR   sll_pkttype;    /* Packet type */
    UCHAR   sll_halen;      /* Length of address */
    UCHAR   sll_addr[8];    /* Physical layer address */
};
```

> [!NOTE]
> <span data-ttu-id="e6fd6-176">Yapıdaki her alan veya tarafından kullanılmaz `sendto()` `recvfrom()` .</span><span class="sxs-lookup"><span data-stu-id="e6fd6-176">Not every field in the structure is used by `sendto()` or `recvfrom()`.</span></span> <span data-ttu-id="e6fd6-177">`sockaddr_ll`PPPoE paketlerinin gönderilmesi ve alınması için aşağıdaki açıklamaya bakın.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-177">See the description below on how to set up the `sockaddr_ll` for sending and receiving PPPoE packets.</span></span>

<span data-ttu-id="e6fd6-178">AF_PACKET ailesinde oluşturulan yuva, belirtilen Protokolden bağımsız olarak, PPPoE bulma paketleri veya PPP oturum paketleri göndermek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-178">Socket created in the AF_PACKET family can be used to send either PPPoE Discovery packets or PPP session packets, regardless of the protocol specified.</span></span> <span data-ttu-id="e6fd6-179">Bir PPPoE paketi iletilirken, uygulama, MAC üstbilgileri (hedef MAC adresi, kaynak MAC adresi ve çerçeve türü) dahil, düzgün şekilde biçimlendirilen PPPoE çerçevesini içeren arabelleği hazırlanmalıdır. Arabelleğin boyutu 14 baytlık Ethernet üstbilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-179">When transmitting a PPPoE packet, application must prepare the buffer that includes properly formatted PPPoE frame, including the MAC headers (Destination MAC address, source MAC address, and frame type.) The size of the buffer includes the 14-byte Ethernet header.</span></span>

<span data-ttu-id="e6fd6-180">`sockaddr_ll`Yapısı, `sll_ifindex` Bu paketi göndermek için kullanılacak fiziksel arabirimi belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-180">The `sockaddr_ll` struct, the `sll_ifindex` is used to indicate the physical interface to be used for sending this packet.</span></span> <span data-ttu-id="e6fd6-181">Yapıdaki alanların geri kalanı kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-181">The rest of the fields in the structure are not used.</span></span> <span data-ttu-id="e6fd6-182">Kullanılmayan alanlara ayarlanan değerler BSD iç işlemi tarafından yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-182">Values set to the unused fields are ignored by the BSD internal process.</span></span>

<span data-ttu-id="e6fd6-183">Aşağıdaki kod bloğunda bir PPPoE paketinin nasıl iletilmesi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-183">The following code block illustrates how to transmit a PPPoE packet:</span></span>

```c
struct sockaddr_ll peer_addr;

/* Transmit a PPPoE frame using the primary network interface. */
peer_addr.sll_ifindex = 0;
n = sendto(sockfd, frame, frame_size, 0, (struct
        sockaddr*)&peer_addr, sizeof(peer_addr));
```

<span data-ttu-id="e6fd6-184">Dönüş değeri, aktarılan bayt sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-184">The return value indicates the number of bytes transmitted.</span></span> <span data-ttu-id="e6fd6-185">PPPoE paketleri ileti tabanlı olduğundan, başarılı bir iletimde, gönderilen bayt sayısı, 14 baytlık Ethernet üst bilgisi dahil olmak üzere paketin boyutuyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-185">Since PPPoE packets are message-based, on a successful transmission, the number of bytes sent matches the size of the packet, including the 14-byte Ethernet header.</span></span>

<span data-ttu-id="e6fd6-186">PPPoE paketleri kullanılarak alınabilir `recvfrom()` .</span><span class="sxs-lookup"><span data-stu-id="e6fd6-186">PPPoE packets can be received using `recvfrom()`.</span></span> <span data-ttu-id="e6fd6-187">Alma arabelleğinin Ethernet MTU boyutu iletisine yetecek kadar büyük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-187">The receive buffer must be big enough to accommodate message of Ethernet MTU size.</span></span> <span data-ttu-id="e6fd6-188">Alınan PPPoE paketi 14 baytlık Ethernet üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-188">The received PPPoE packet includes 14-byte Ethernet header.</span></span> <span data-ttu-id="e6fd6-189">PPPoE paketleri alındığında, PPPoE bulma paketleri yalnızca protokol ile oluşturulan yuva tarafından alınabilir `ETHERTYPE_PPPOE_DISC` .</span><span class="sxs-lookup"><span data-stu-id="e6fd6-189">On receiving PPPoE packets, PPPoE Discovery packets can only be received by socket created with protocol `ETHERTYPE_PPPOE_DISC`.</span></span> <span data-ttu-id="e6fd6-190">Benzer şekilde, PPP oturum paketleri yalnızca protokolle oluşturulan yuva tarafından alınabilir `ETHERTYPE_PPPOE_SESS` .</span><span class="sxs-lookup"><span data-stu-id="e6fd6-190">Similarly, PPP session packets can only be received by socket created with protocol `ETHERTYPE_PPPOE_SESS`.</span></span> <span data-ttu-id="e6fd6-191">Aynı protokol türü için birden çok yuva oluşturulduysa, gelen PPPoE paketleri ilk oluşturulan yuvaya iletilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-191">If multiple sockets are created for the same protocol type, arriving PPPoE packets are forwarded to the socket created first.</span></span> <span data-ttu-id="e6fd6-192">Protokol için oluşturulan ilk yuva kapalıysa, bu paketlerin alınması için oluşturma sırasındaki sonraki yuva kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-192">If the first socket created for the protocol is closed, the next socket in the order of creation is used for receiving these packets.</span></span>

<span data-ttu-id="e6fd6-193">Bir PPPoE paketi alındıktan sonra, yapı içindeki aşağıdaki alanlar `sockaddr_ll` geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-193">After a PPPoE packet is received, the following fields in the `sockaddr_ll` struct are valid:</span></span>
- <span data-ttu-id="e6fd6-194">**sll_family**: BSD iç tarafından AF_PACKET olacak şekilde ayarlayın</span><span class="sxs-lookup"><span data-stu-id="e6fd6-194">**sll_family**: Set by the BSD internal to be AF_PACKET</span></span>
- <span data-ttu-id="e6fd6-195">**sll_ifindex**: paketin alındığı arabirimi gösterir</span><span class="sxs-lookup"><span data-stu-id="e6fd6-195">**sll_ifindex**: Indicates the interface from which the packet is received</span></span>
- <span data-ttu-id="e6fd6-196">**sll_protocol**: alınan paket türüne ayarlı: `ETHERTYPE_PPPOE_DISC` veya `ETHERTYPE_PPPOE_SESS`</span><span class="sxs-lookup"><span data-stu-id="e6fd6-196">**sll_protocol**: Set to the type of packet received: `ETHERTYPE_PPPOE_DISC` or `ETHERTYPE_PPPOE_SESS`</span></span>

## <a name="eliminating-internal-bsd-thread"></a><span data-ttu-id="e6fd6-197">Iç BSD Iş parçacığını ortadan kaldırma</span><span class="sxs-lookup"><span data-stu-id="e6fd6-197">Eliminating Internal BSD Thread</span></span>

<span data-ttu-id="e6fd6-198">Varsayılan olarak, BSD bazı işlemlerini gerçekleştirmek için bir iç iş parçacığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-198">By default, BSD utilizes an internal thread to perform some of its processing.</span></span> <span data-ttu-id="e6fd6-199">Sıkı bellek kısıtlamalarına sahip sistemlerde, BSD, iç BSD iş parçacığını ortadan kaldıran ve bunun yerine aynı işlemi gerçekleştirmek için bir iç süreölçer kullanan NX_BSD_TIMEOUT_PROCESS_IN_TIMER tanımlanmış ile oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-199">In systems with tight memory constraints, BSD can be built with NX_BSD_TIMEOUT_PROCESS_IN_TIMER defined, which eliminates the internal BSD thread and instead uses an internal timer to perform the same processing.</span></span> <span data-ttu-id="e6fd6-200">Bu, iç BSD iş parçacığı denetim bloğu ve yığını için gereken belleği ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-200">This eliminates the memory required for the internal BSD thread control block and stack.</span></span> <span data-ttu-id="e6fd6-201">Ancak, genel Zamanlayıcı işlemesi önemli ölçüde artar ve BSD işlemi gerekenden daha yüksek bir önceliğe göre de çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-201">However, overall timer processing is significantly increased and the BSD processing may also execute at a higher priority than needed.</span></span>

<span data-ttu-id="e6fd6-202">BSD yuvalarını ThreadX Zamanlayıcı bağlamında çalışacak şekilde yapılandırmak için, *nxd_bsd. h* içinde NX_BSD_TIMEOUT_PROCESS_IN_TIMER tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-202">To configure BSD sockets to run in the ThreadX timer context, define NX_BSD_TIMEOUT_PROCESS_IN_TIMER in *nxd_bsd.h*.</span></span> <span data-ttu-id="e6fd6-203">BSD katmanı Zamanlayıcı bağlamındaki BSD görevlerini yürütmek üzere yapılandırılmışsa, *bsd_initialize* çağrısında aşağıdaki üç parametre yok SAYıLıR ve null olarak ayarlanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-203">If the BSD layer is configured to execute the BSD tasks in the timer context, in the call to *bsd_initialize*, the following three parameters are ignored, and should be set to NULL:</span></span>

- <span data-ttu-id="e6fd6-204">**bsd_thread_stack_area**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-204">**bsd_thread_stack_area**</span></span>
- <span data-ttu-id="e6fd6-205">**bsd_thread_stack_size**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-205">**bsd_thread_stack_size**</span></span>
- <span data-ttu-id="e6fd6-206">**bsd_thread_priority**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-206">**bsd_thread_priority**</span></span>

## <a name="netx-duo-bsd-with-dns-support"></a><span data-ttu-id="e6fd6-207">DNS desteğiyle NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="e6fd6-207">NetX Duo BSD with DNS Support</span></span>

<span data-ttu-id="e6fd6-208">NX_BSD_ENABLE_DNS tanımlanmışsa NetX Duo BSD, ana bilgisayar adı veya ana bilgisayar IP bilgilerini almak için DNS sorguları gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-208">If NX_BSD_ENABLE_DNS is defined, NetX Duo BSD can send DNS queries to obtain hostname or host IP information.</span></span> <span data-ttu-id="e6fd6-209">Bu özellik, *nx_dns_create* hizmeti kullanılarak bir NETX DNS istemcisinin daha önce oluşturulmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-209">This feature requires a NetX DNS Client to be previously created using the *nx_dns_create* service.</span></span> <span data-ttu-id="e6fd6-210">Bir veya daha fazla bilinen DNS sunucusu IP adresi, IPv4 sunucusu adreslerini eklemek için *nx_dns_server_add* hizmeti kullanılarak veya IPv4 veya IPv6 sunucu adreslerini eklemek için *NXD_DNS_SERVER_ADD* hizmeti kullanılarak DNS örneğine kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-210">One or more known DNS server IP addresses must be registered with the DNS instance using the *nx_dns_server_add* service for adding IPv4 server addresses, or using the *nxd_dns_server_add* service for adding either IPv4 or IPv6 server addresses.</span></span>

<span data-ttu-id="e6fd6-211">DNS hizmetleri ve bellek ayırma, *GetAddrInfo* ve *GetNameInfo* Hizmetleri tarafından kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-211">DNS services and memory allocation are used by *getaddrinfo* and *getnameinfo* services:</span></span>

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
        const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
        char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

<span data-ttu-id="e6fd6-212">BSD uygulaması, bir ana bilgisayar adı ile *GetAddrInfo* çağırdığında NETX BSD, IP adresini almak için aşağıdaki hizmetlerden herhangi birini çağırır:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-212">When the BSD application calls *getaddrinfo* with a hostname, NetX BSD will call any of the below services to obtain the IP address:</span></span>

- <span data-ttu-id="e6fd6-213">**nx_dns_ipv4_address_by_name_get**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-213">**nx_dns_ipv4_address_by_name_get**</span></span>
- <span data-ttu-id="e6fd6-214">**nxd_dns_ipv6_address_by_name_get**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-214">**nxd_dns_ipv6_address_by_name_get**</span></span>
- <span data-ttu-id="e6fd6-215">**nx_dns_cname_get**</span><span class="sxs-lookup"><span data-stu-id="e6fd6-215">**nx_dns_cname_get**</span></span>

<span data-ttu-id="e6fd6-216">*Nx_dns_ipv4_address_by_name_get* ve *nxd_dns_ipv6_address_by_name_get* için netx BSD sırasıyla ipv4_addr_buffer ve ipv6_addr_buffer bellek alanını kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-216">For *nx_dns_ipv4_address_by_name_get* and *nxd_dns_ipv6_address_by_name_get*, NetX BSD uses the ipv4_addr_buffer and ipv6_addr_buffer memory areas respectively.</span></span> <span data-ttu-id="e6fd6-217">Bu arabelleklerin boyutu, sırasıyla (NX_BSD_IPV4_ADDR_PER_HOST \* 4) ve (NX_BSD_IPV6_ADDR_PER_HOST \* 16) tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-217">The size of these buffers are defined by (NX_BSD_IPV4_ADDR_PER_HOST \* 4) and (NX_BSD_IPV6_ADDR_PER_HOST \* 16) respectively.</span></span>

<span data-ttu-id="e6fd6-218">NETX BSD, *GetAddrInfo*'dan adres bilgilerini döndürmek için, bellek alanı başka bir yapılandırılabilir seçenekler kümesi, NX_BSD_IPV4_ADDR_MAX_NUM ve NX_BSD_IPV6_ADDR_MAX_NUM tarafından tanımlanmış olan Nx_bsd_addrinfo_pool_memory threadx blok bellek tablosunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-218">For returning address information from *getaddrinfo*, NetX BSD uses the ThreadX block memory table nx_bsd_addrinfo_pool_memory, whose memory area is defined by another set of configurable options, NX_BSD_IPV4_ADDR_MAX_NUM and NX_BSD_IPV6_ADDR_MAX_NUM.</span></span>

<span data-ttu-id="e6fd6-219">Yukarıdaki yapılandırma seçenekleri hakkında daha fazla bilgi için bkz. **genel yapılandırma seçenekleri** .</span><span class="sxs-lookup"><span data-stu-id="e6fd6-219">See **General Configuration Options** for more details on the above configuration options.</span></span>

<span data-ttu-id="e6fd6-220">Ayrıca, NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa ve konak girişi kurallı bir ad ise NetX Duo BSD, daha önce oluşturulmuş bir blok havuzundan belleği dinamik olarak ayırır _nx_bsd_cname_block_pool</span><span class="sxs-lookup"><span data-stu-id="e6fd6-220">Additionally, if NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, and the host input is a canonical name, NetX Duo BSD will allocate memory dynamically from a previously created block pool \`_nx_bsd_cname_block_pool</span></span>

> [!NOTE]
> <span data-ttu-id="e6fd6-221">*GetAddrInfo* çağrıldıktan sonra, *freeaddrinfo* hizmeti kullanılarak, kaynak bağımsız değişkeni tarafından işaret edilen belleğin blok tabloya geri bırakılması için BSD uygulaması sorumludur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-221">After calling *getaddrinfo* the BSD application is responsible for releasing the memory pointed to by the res argument back to the block table using the *freeaddrinfo* service.</span></span>

## <a name="netx-duo-bsd-limitations"></a><span data-ttu-id="e6fd6-222">NetX Duo BSD sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="e6fd6-222">NetX Duo BSD Limitations</span></span>

<span data-ttu-id="e6fd6-223">NetX Duo BSD, performans ve mimari sorunlarından dolayı tüm BSD 4,3 yuva özelliklerini desteklemez:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-223">Due to performance and architecture issues, NetX Duo BSD does not support all the BSD 4.3 socket features:</span></span>

<span data-ttu-id="e6fd6-224">*Gönderme, alma, SendTo* ve *RECVFROM* çağrılarında Int bayrakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-224">INT flags are not supported for *send, recv, sendto* and *recvfrom* calls.</span></span>

## <a name="general-configuration-options"></a><span data-ttu-id="e6fd6-225">Genel yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="e6fd6-225">General Configuration Options</span></span>

<span data-ttu-id="e6fd6-226">*Nxd_bsd. h* içindeki kullanıcı yapılandırılabilir seçenekleri, uygulamanın, belirli uygulama gereksinimleri Için NETX Duo BSD yuvaları üzerinde ince ayar yapmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-226">User configurable options in *nxd_bsd.h* allow the application to fine tune NetX Duo BSD sockets for its particular application requirements.</span></span>

<span data-ttu-id="e6fd6-227">Derleme zamanında ayarlanan yapılandırılabilir seçeneklerin listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e6fd6-227">The following is the list of configurable options that are set at compile time:</span></span>

- <span data-ttu-id="e6fd6-228">**NX_BSD_TCP_WINDOW**: TCP yuvası oluşturma çağrılarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-228">**NX_BSD_TCP_WINDOW**: Used in TCP socket create calls.</span></span> <span data-ttu-id="e6fd6-229">64K, 100Mb Ethernet için tipik bir pencere boyutudur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-229">64k is typical window size for 100Mb Ethernet.</span></span> <span data-ttu-id="e6fd6-230">Varsayılan değer 65535 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-230">The default value is 65535.</span></span>

- <span data-ttu-id="e6fd6-231">**NX_BSD_SOCKFD_START**: Bu, BSD yuvası dosya tanımlayıcısı başlangıç değerinin mantıksal dizinidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-231">**NX_BSD_SOCKFD_START**: This is the logical index for the BSD socket file descriptor start value.</span></span> <span data-ttu-id="e6fd6-232">Varsayılan olarak, bu seçenek 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-232">By default this option is 32.</span></span>

- <span data-ttu-id="e6fd6-233">**NX_BSD_MAX_SOCKETS**: BSD katmanında kullanılabilir olan en fazla toplam yuva sayısını belirtir ve 32 katı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-233">**NX_BSD_MAX_SOCKETS**: Specifies the maximum number of total sockets available in the BSD layer and must be a multiple of 32.</span></span> <span data-ttu-id="e6fd6-234">Değer, varsayılan olarak 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-234">The value is defaulted to 32.</span></span>

- <span data-ttu-id="e6fd6-235">**NX_BSD_SOCKET_QUEUE_MAX**: alma yuvası sırasında depolanan en fazla UDP paketi sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-235">**NX_BSD_SOCKET_QUEUE_MAX**: Specifies the maximum number of UDP packets stored on the receive socket queue.</span></span> <span data-ttu-id="e6fd6-236">Değer, varsayılan olarak 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-236">The value is defaulted to 5.</span></span>

- <span data-ttu-id="e6fd6-237">**NX_BSD_MAX_LISTEN_BACKLOG**: Bu, BSD TCP yuvaları için dinleme kuyruğunun boyutunu (' Backlog ') belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-237">**NX_BSD_MAX_LISTEN_BACKLOG**: This specifies the size of the listen queue ('backlog') for BSD TCP sockets.</span></span> <span data-ttu-id="e6fd6-238">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-238">The default value is 5.</span></span>

- <span data-ttu-id="e6fd6-239">**NX_MICROSECOND_PER_CPU_TICK**: Zamanlayıcı Zamanlayıcı numarası başına mikrosaniye sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-239">**NX_MICROSECOND_PER_CPU_TICK**: Specifies the number of microseconds per scheduler timer tick.</span></span>

- <span data-ttu-id="e6fd6-240">**NX_BSD_TIMEOUT**: BSD Için gereken NETX Duo iç çağrılarındaki süreölçer işaretleri cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-240">**NX_BSD_TIMEOUT**: Specifies the timeout in timer ticks on NetX Duo internal calls required by BSD.</span></span> <span data-ttu-id="e6fd6-241">Varsayılan değer (20 \* NX_IP_PERIODIC_RATE) değeridir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-241">The default value is (20 \* NX_IP_PERIODIC_RATE).</span></span>

- <span data-ttu-id="e6fd6-242">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: NETX Duo bağlantı kesme çağrısının süreölçer işaretleri cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-242">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: Specifies the timeout in timer ticks on NetX Duo disconnect call.</span></span> <span data-ttu-id="e6fd6-243">Varsayılan değer 1’dir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-243">The default value is 1.</span></span>

- <span data-ttu-id="e6fd6-244">**NX_BSD_PRINT_ERRORS**: ayarlanırsa, bir BSD işlevinin hata durumu dönüşü bir satır numarası ve hata türü döndürür, örneğin hatanın gerçekleştiği NX_SOC_ERROR.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-244">**NX_BSD_PRINT_ERRORS**: If set, the error status return of a BSD function returns a line number and type of error e.g. NX_SOC_ERROR where the error occurs.</span></span> <span data-ttu-id="e6fd6-245">Bu, uygulama geliştiricisinin hata ayıklama çıkışını tanımlamasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-245">This requires the application developer to define the debug output.</span></span> <span data-ttu-id="e6fd6-246">Varsayılan ayar devre dışıdır ve *nxd_bsd. h* içinde herhangi bir hata ayıklama çıkışı belirtilmez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-246">The default setting is disabled and no debug output is specified in *nxd_bsd.h*.</span></span>

- <span data-ttu-id="e6fd6-247">**NX_BSD_TIMER_RATE**: BSD düzenli zamanlayıcı görevinin çalışması için gereken Aralık.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-247">**NX_BSD_TIMER_RATE**: Interval after which BSD periodic timer task runs.</span></span> <span data-ttu-id="e6fd6-248">Varsayılan değer 1 saniyedir (1 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="e6fd6-248">The default value is 1 second (1 \* NX_IP_PERIODIC_RATE).</span></span>

- <span data-ttu-id="e6fd6-249">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER**: ayarlanırsa, bu seçenek BSD zaman aşımı işleminin sistem Zamanlayıcı bağlamında yürütülmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-249">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER**: If set, this option allows the BSD timeout process to execute in the system timer context.</span></span> <span data-ttu-id="e6fd6-250">Varsayılan davranış devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-250">The default behavior is disabled.</span></span> <span data-ttu-id="e6fd6-251">Bu özellik, Bölüm 2 "NetX Duo BSD yüklemesi ve kullanımı" bölümünde daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-251">This feature is described in more detail in Chapter 2 "Installation and Use of NetX Duo BSD".</span></span>

- <span data-ttu-id="e6fd6-252">**NX_BSD_RAW_PPPOE_SUPPORT**: PPPoE ham paket desteğini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-252">**NX_BSD_RAW_PPPOE_SUPPORT**: Enable PPPoE raw packet support.</span></span> <span data-ttu-id="e6fd6-253">Varsayılan olarak bu seçenek etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-253">By default this option is not enabled.</span></span>

- <span data-ttu-id="e6fd6-254">**NX_BSD_ENABLE_DNS**: etkinleştirilirse NETX Duo BSD bir ana bilgisayar adı veya ana bilgisayar IP adresi IÇIN bir DNS sorgusu gönderir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-254">**NX_BSD_ENABLE_DNS**: If enabled, NetX Duo BSD will send a DNS query for a hostname or host IP address.</span></span> <span data-ttu-id="e6fd6-255">Daha önce oluşturulup başlatılmış bir DNS Istemci örneği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-255">Requires a DNS Client instance to be previously created and started.</span></span> <span data-ttu-id="e6fd6-256">Varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-256">By default it is not enabled.</span></span>

- <span data-ttu-id="e6fd6-257">**NX_BSD_SOCKET_RAW_PROTOCOL_TABLE_SIZE**: Ham yuva tablosunun boyutunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-257">**NX_BSD_SOCKET_RAW_PROTOCOL_TABLE_SIZE**: Defines the size of the raw socket table.</span></span> <span data-ttu-id="e6fd6-258">Değer ikinin üssü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-258">The value must be a power of two.</span></span> <span data-ttu-id="e6fd6-259">NetX BSD, ham paketlerin gönderilmesi ve alınması için NX_BSD_SOCKETS türünde bir yuva dizisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-259">NetX BSD creates an array of sockets of type NX_BSD_SOCKETS for sending and receiving raw packets.</span></span> <span data-ttu-id="e6fd6-260">NX_ENABLE_IP_RAW_PACKET_FILTER etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-260">NX_ENABLE_IP_RAW_PACKET_FILTER must be enabled.</span></span> <span data-ttu-id="e6fd6-261">Varsayılan olarak 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-261">By default it is 32.</span></span>

- <span data-ttu-id="e6fd6-262">**NX_BSD_IPV4_ADDR_MAX_NUM**: *GetAddrInfo* tarafından döndürülen en fazla IPv4 adresi sayısı.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-262">**NX_BSD_IPV4_ADDR_MAX_NUM**: Maximum number of IPv4 addresses returned by *getaddrinfo*.</span></span> <span data-ttu-id="e6fd6-263">NX_BSD_IPV6_ADDR_MAX_NUM ile birlikte, bu, *GetAddrInfo* içinde bilgi depolamaya yönelik olarak bellek ayırmak Için NETX BSD bloğu havuzunun boyutunu nx_bsd_addrinfo_block_pool tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-263">This along with NX_BSD_IPV6_ADDR_MAX_NUM defines the size of the NetX BSD block pool nx_bsd_addrinfo_block_pool for dynamically allocating memory to address information storage in *getaddrinfo*.</span></span> <span data-ttu-id="e6fd6-264">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-264">The default value is 5.</span></span>

- <span data-ttu-id="e6fd6-265">**NX_BSD_IPV6_ADDR_MAX_NUM**: *GetAddrInfo* tarafından döndürülen en fazla IPv6 adresi sayısı.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-265">**NX_BSD_IPV6_ADDR_MAX_NUM**: Maximum number of IPv6 addresses returned by *getaddrinfo*.</span></span> <span data-ttu-id="e6fd6-266">NX_BSD_IPV4_ADDR_MAX_NUM ile birlikte, bu, *GetAddrInfo* içinde bilgi depolamaya yönelik olarak bellek ayırmak Için NETX BSD bloğu havuzunun boyutunu nx_bsd_addrinfo_block_pool tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-266">This along with NX_BSD_IPV4_ADDR_MAX_NUM defines the size of the NetX BSD block pool nx_bsd_addrinfo_block_pool for dynamically allocating memory to address information storage in *getaddrinfo*.</span></span>

- <span data-ttu-id="e6fd6-267">**NX_BSD_IPV4_ADDR_PER_HOST**: DNS sorgusu başına depolanan en yüksek IPv4 adreslerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-267">**NX_BSD_IPV4_ADDR_PER_HOST**: Defines maximum IPv4 addresses stored per DNS query.</span></span> <span data-ttu-id="e6fd6-268">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-268">The default value is 5.</span></span>

- <span data-ttu-id="e6fd6-269">**NX_BSD_IPV6_ADDR_PER_HOST**: DNS sorgusu başına depolanan en yüksek IPv6 adreslerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-269">**NX_BSD_IPV6_ADDR_PER_HOST**: Defines maximum IPv6 addresses stored per DNS query.</span></span> <span data-ttu-id="e6fd6-270">Varsayılan değer 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-270">The default value is 2.</span></span>

## <a name="bsd-socket-options"></a><span data-ttu-id="e6fd6-271">BSD yuvası seçenekleri</span><span class="sxs-lookup"><span data-stu-id="e6fd6-271">BSD Socket Options</span></span>

<span data-ttu-id="e6fd6-272">Aşağıdaki NetX Duo BSD yuva seçeneklerinin listesi, *setsockopt* hizmeti kullanılarak her yuva temelinde çalışma zamanında etkinleştirilebilir (veya devre dışı bırakılabilir):</span><span class="sxs-lookup"><span data-stu-id="e6fd6-272">The following list of NetX Duo BSD socket options can be enabled (or disabled) at run time on a per socket basis using the *setsockopt* service:</span></span>

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, 
                const void *option_value, INT option_length);
```

<span data-ttu-id="e6fd6-273">Option_level için iki farklı ayar vardır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-273">There are two different settings for option_level.</span></span>

<span data-ttu-id="e6fd6-274">Çalışma zamanı yuva seçeneklerinin ilk türü yuva düzeyi seçenekleri için SOL_SOCKET.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-274">The first type of run time socket options is SOL_SOCKET for socket level options.</span></span> <span data-ttu-id="e6fd6-275">Yuva düzeyi seçeneğini etkinleştirmek için, *sol_socket olarak ayarlanan* option_level ve option_name belirli bir seçeneğe ayarla ' yı çağırın. örneğin, so_broadcast *.*</span><span class="sxs-lookup"><span data-stu-id="e6fd6-275">To enable a socket level option, call *setsockopt* with option_level set to SOL_SOCKET and option_name set to the specific option e.g. SO_BROADCAST *.*</span></span> <span data-ttu-id="e6fd6-276">Bir seçenek ayarı almak için, option_level tekrar SOL_SOCKET olarak ayarlanan option_name için *getsockopt* çağırın.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-276">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to SOL_SOCKET.</span></span>

<span data-ttu-id="e6fd6-277">Çalışma zamanı yuva düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-277">The list of run time socket level options is shown below.</span></span>

- <span data-ttu-id="e6fd6-278">**So_broadcast**: ayarlandıysa, NETX yuvalarından yayın paketlerinin gönderilmesini ve alınmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-278">**SO_BROADCAST**:  If set, this enables sending and receiving broadcast packets from Netx sockets.</span></span> <span data-ttu-id="e6fd6-279">Bu, NetX Duo için varsayılan davranıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-279">This is the default behavior for NetX Duo.</span></span> <span data-ttu-id="e6fd6-280">Tüm yuvalarda bu yetenek vardır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-280">All sockets have this capability.</span></span>

- <span data-ttu-id="e6fd6-281">**SO_ERROR**: *getsockopt* hizmeti kullanılarak belirtilen yuvanın önceki yuva işleminde yuva durumunu elde etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-281">**SO_ERROR**:  Used to obtain socket status on the previous socket operation of the specified socket, using the *getsockopt* service.</span></span> <span data-ttu-id="e6fd6-282">Tüm yuvalarda bu yetenek vardır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-282">All sockets have this capability.</span></span>

- <span data-ttu-id="e6fd6-283">**SO_KEEPALIVE**: AYARLANıRSA, TCP canlı tut özelliğini sunar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-283">**SO_KEEPALIVE**:  If set, this enables the TCP Keep Alive feature.</span></span> <span data-ttu-id="e6fd6-284">Bu, NetX Duo kitaplığının *nx_user. h* içinde tanımlanan NX_TCP_ENABLE_KEEPALIVE oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-284">This requires the NetX Duo library to be built with NX_TCP_ENABLE_KEEPALIVE defined in *nx_user.h*.</span></span> <span data-ttu-id="e6fd6-285">Bu özellik varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-285">By default this feature is disabled.</span></span>

- <span data-ttu-id="e6fd6-286">**SO_RCVTIMEO**: Bu, NETX Duo BSD yuvalarda paketlerin alınması için saniye cinsinden bekleme seçeneğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-286">**SO_RCVTIMEO**:  This sets the wait option in seconds for receiving packets on NetX Duo BSD sockets.</span></span> <span data-ttu-id="e6fd6-287">Varsayılan değer NX_WAIT_FOREVER (0xFFFFFFFF) veya engelleyici olmayan bir etkin ise, NX_NO_WAIT (0x0).</span><span class="sxs-lookup"><span data-stu-id="e6fd6-287">The default value is the NX_WAIT_FOREVER (0xFFFFFFFF) or, if non-blocking is enabled, NX_NO_WAIT (0x0).</span></span>

- <span data-ttu-id="e6fd6-288">**SO_RCVBUF**: Bu, TCP yuvasının pencere boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-288">**SO_RCVBUF**:  This sets the window size of the TCP socket.</span></span> <span data-ttu-id="e6fd6-289">NX_BSD_TCP_WINDOW varsayılan değeri, BSD TCP yuvaları için 64K olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-289">The default value, NX_BSD_TCP_WINDOW, is set to 64k for BSD TCP sockets.</span></span> <span data-ttu-id="e6fd6-290">65535 üzerinden boyutu ayarlamak için NetX Duo kitaplığının NX_TCP_ENABLE_WINDOW_SCALING tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-290">To set the size over 65535 requires the NetX Duo library to be built with the NX_TCP_ENABLE_WINDOW_SCALING be defined.</span></span>

- <span data-ttu-id="e6fd6-291">**SO_REUSEADDR**: ayarlandıysa, bu, birden çok yuvaların bir bağlantı noktasıyla eşleştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-291">**SO_REUSEADDR**:  If set, this enables multiple sockets to be mapped to one port.</span></span> <span data-ttu-id="e6fd6-292">Genel kullanım, TCP sunucu soketi içindir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-292">The typical usage is for the TCP Server socket.</span></span> <span data-ttu-id="e6fd6-293">Bu, NetX Duo yuvaları varsayılan davranışıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-293">This is the default behavior of NetX Duo sockets.</span></span>

<span data-ttu-id="e6fd6-294">Çalışma zamanı yuva seçeneklerinin ikinci türü, IP seçenek düzeyidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-294">The second type of run time socket options is the IP option level.</span></span> <span data-ttu-id="e6fd6-295">Bir IP düzeyi seçeneğini etkinleştirmek için, *setsockopt* ' i çağırın option_level IP_PROTO olarak ayarlayın ve option_name IP_MULTICAST_TTL seçeneğine ayarlayın *.*</span><span class="sxs-lookup"><span data-stu-id="e6fd6-295">To enable an IP level option, call *setsockopt* with option_level set to IP_PROTO and option_name set to the option e.g. IP_MULTICAST_TTL *.*</span></span> <span data-ttu-id="e6fd6-296">Bir seçenek ayarı almak için, option_level tekrar IP_PROTO olarak ayarlanan option_name için *getsockopt* çağırın.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-296">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to IP_PROTO.</span></span>

<span data-ttu-id="e6fd6-297">Çalışma zamanı IP düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-297">The list of run time IP level options is shown below.</span></span>

- <span data-ttu-id="e6fd6-298">**IP_MULTICAST_TTL**: Bu, UDP yuvaları için yaşam süresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-298">**IP_MULTICAST_TTL**:  This sets the time to live for UDP sockets.</span></span> <span data-ttu-id="e6fd6-299">Yuva oluşturulduğunda varsayılan değer NX_IP_TIME_TO_LIVE (0x80).</span><span class="sxs-lookup"><span data-stu-id="e6fd6-299">The default value is NX_IP_TIME_TO_LIVE (0x80) when the socket is created.</span></span> <span data-ttu-id="e6fd6-300">Bu değer, bu yuva seçeneği ile *setsockopt* çağırarak geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-300">This value can be overridden by calling *setsockopt* with this socket option.</span></span>

- <span data-ttu-id="e6fd6-301">**IP_RAW_IPV6_HDRINCL**: Bu seçenek ayarlandıysa, çağıran uygulama, BSD tarafından oluşturulan ham IPv6 yuvaları üzerinde aktarılan verilere bir IPv6 üst bilgisi ve isteğe bağlı olarak uygulama üstbilgileri eklememelidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-301">**IP_RAW_IPV6_HDRINCL**:  If this option is set, the calling application must append an IPv6 header and optionally application headers to data being transmitted on raw IPv6 sockets created by BSD.</span></span> <span data-ttu-id="e6fd6-302">Bu seçeneği kullanmak için, IP görevinde Ham yuva işlemenin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-302">To use this option, raw socket processing must be enabled on the IP task.</span></span>

- <span data-ttu-id="e6fd6-303">**IP_ADD_MEMBERSHIP**: ayarlanırsa, belirtilen IGMP grubuna katılması için bu seçenekler BSD yuvasını (yalnızca UDP yuvaları için geçerlidir) sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-303">**IP_ADD_MEMBERSHIP**:  If set, this options enables the BSD socket (applies only to UDP sockets) to join the specified IGMP group.</span></span>

- <span data-ttu-id="e6fd6-304">**IP_DROP_MEMBERSHIP**: ayarlanırsa, bu seçenekler belirtilen IGMP grubunu BıRAKMAK için BSD yuvasını (yalnızca UDP yuvaları için geçerlidir) sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-304">**IP_DROP_MEMBERSHIP**:  If set, this options enables the BSD socket (applies only to UDP sockets) to leave the specified IGMP group.</span></span>

- <span data-ttu-id="e6fd6-305">**IP_HDRINCL**: Bu seçenek ayarlandıysa, ÇAĞıRAN uygulamanın IP üst bilgisini ve isteğe bağlı olarak uygulama üst bilgilerini BSD içinde oluşturulan ham IPv4 yuvaları üzerinde aktarılan verilere ekleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-305">**IP_HDRINCL**:  If this option is set, the calling application must append the IP header and optionally application headers to data being transmitted on raw IPv4 sockets created in BSD.</span></span> <span data-ttu-id="e6fd6-306">Bu seçeneği kullanmak için, IP görevinde Ham yuva işlemenin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-306">To use this option, raw socket processing must be enabled on the IP task.</span></span>

- <span data-ttu-id="e6fd6-307">**IP_RAW_RX_NO_HEADER**: silinirse, ıPV6 üstbilgisi BSD içinde oluşturulan ham IPv6 yuvaları için alınan verilere dahildir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-307">**IP_RAW_RX_NO_HEADER**:  If cleared, the IPv6 header is included with the received data for raw IPv6 sockets created in BSD.</span></span> <span data-ttu-id="e6fd6-308">IPv6 üstbilgileri, BSD RAW IPv6 Yuvaları ' nda varsayılan olarak kaldırılır ve paket uzunluğu IPv6 üst bilgisini içermez.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-308">IPv6 headers are removed by default in BSD raw IPv6 sockets, and the packet length does not include the IPv6 header.</span></span>

<span data-ttu-id="e6fd6-309">Ayarlanırsa, IPv4 üstbilgisi, IPv4 türündeki BSD RAW yuvalarda alınan verilerden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-309">If set, the IPv4 header is removed from received data on BSD raw sockets of type IPv4.</span></span> <span data-ttu-id="e6fd6-310">IPv4 üstbilgileri, BSD ham IPv4 Yuvaları ' nda varsayılan olarak dahil edilir ve paket uzunluğu IPv4 üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-310">IPv4 headers are included by default in BSD raw IPv4 sockets and packet length includes the IPv4 header.</span></span>

<span data-ttu-id="e6fd6-311">Bu seçeneğin IPv4 veya IPv6 iletim verisi üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-311">This option has no effect on either IPv4 or IPv6 transmission data.</span></span>

## <a name="small-ipv4-example"></a><span data-ttu-id="e6fd6-312">Küçük IPv4 örneği</span><span class="sxs-lookup"><span data-stu-id="e6fd6-312">Small IPv4 Example</span></span>

<span data-ttu-id="e6fd6-313">IPv4 ağları için NetX Duo BSD hizmetlerinin nasıl kullanılacağına ilişkin bir örnek aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-313">An example of how to use NetX Duo BSD services for IPv4 networks is described below.</span></span> <span data-ttu-id="e6fd6-314">Bu örnekte, *nxd_bsd. h* içerme dosyası, 8. satırda getirilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-314">In this example, the include file *nxd_bsd.h* is brought in at line 8.</span></span> <span data-ttu-id="e6fd6-315">Ardından, IP örneği *bsd_ip* ve paket havuzu *bsd_pool* , 20 ve 21. satırda genel değişkenler olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-315">Next, the IP instance *bsd_ip* and packet pool *bsd_pool* are created as global variables at line 20 and 21.</span></span> <span data-ttu-id="e6fd6-316">Bu tanıtımda *, _nx_ram_network_driver* bir RAM (sanal) ağ sürücüsü kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-316">Note that this demo uses a ram (virtual) network driver *, _nx_ram_network_driver*.</span></span> <span data-ttu-id="e6fd6-317">İstemci ve sunucu, bu örnekteki tek IP örneğinde aynı IP adresini paylaşır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-317">The client and server will share the same IP address on single IP instance in this example.</span></span>

<span data-ttu-id="e6fd6-318">İstemci ve sunucu iş parçacıkları 62 ve 68 satırlarında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-318">The client and server threads are created on lines 62 and 68.</span></span> <span data-ttu-id="e6fd6-319">Paketleri iletmek için BSD paket havuzu, 78 satırı üzerinde oluşturulur ve 87. satırdaki IP örneği oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-319">The BSD packet pool for transmitting packets is created on line 78 and used in the IP instance creation on line 87.</span></span> <span data-ttu-id="e6fd6-320">IP iş parçacığı görevinin *nx_ip_create* çağrısında öncelik 1 verildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-320">Note that the IP thread task is given priority 1 in the *nx_ip_create* call.</span></span> <span data-ttu-id="e6fd6-321">Bu iş parçacığı, programda en iyi NetX performansı için tanımlanan en yüksek öncelik görevi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-321">This thread should be the highest priority task defined in the program for optimal NetX performance.</span></span>

<span data-ttu-id="e6fd6-322">IP örneği, sırasıyla 88 ve 110 satırlarında ARP ve TCP hizmetleri için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-322">The IP instance is enabled for ARP and TCP services on lines 88 and 110 respectively.</span></span> <span data-ttu-id="e6fd6-323">BSD Hizmetleri 'nin kullanılabilmesi için son gereksinim, BSD için gereken tüm veri yapılarını ve NetX ve ThreadX kaynaklarını ayarlamak üzere 120 satırındaki *bsd_initialize* çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-323">The last requirement before BSD services can be used is to call *bsd_initialize* on line 120 to set up all data structures and NetX and ThreadX resources needed by BSD.</span></span>

<span data-ttu-id="e6fd6-324">Sunucu iş parçacığı girişi işlevi daha sonra tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-324">The server thread entry function is defined next.</span></span> <span data-ttu-id="e6fd6-325">BSD TCP yuvası 149. satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-325">The BSD TCP socket is created on line 149.</span></span> <span data-ttu-id="e6fd6-326">Sunucu IP adresi ve bağlantı noktası 160-163 satırları üzerinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-326">The server IP address and port are set on lines 160-163.</span></span> <span data-ttu-id="e6fd6-327">Ana bilgisayarın IP adresine ve bağlantı noktasına uygulanan *hton* ve ağ bayt *sıralaması makrolarının kullanımını aklınızda yazın.*</span><span class="sxs-lookup"><span data-stu-id="e6fd6-327">Note the use of host to network byte order macros *htonl* and *htons* applied to the IP address and port.</span></span> <span data-ttu-id="e6fd6-328">Bu, birden çok baytlık verilerin ağ bayt düzeninde BSD hizmetlerine gönderildiği BSD yuvası belirtimiyle uyumludur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-328">This is in compliance with BSD socket specification that multi byte data is submitted to the BSD services in network byte order.</span></span>

<span data-ttu-id="e6fd6-329">Ardından, ana sunucu yuvası 166. satırdaki *BIND* hizmeti kullanılarak bağlantı noktasına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-329">Next, the master server socket is bound to the port using the *bind* service on line 166.</span></span> <span data-ttu-id="e6fd6-330">Bu, 180. satırdaki *dinleme* HIZMETINI kullanan TCP bağlantı istekleri için dinleme yuvadır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-330">This is the listening socket for TCP connection requests using the *listen* service on line 180.</span></span> <span data-ttu-id="e6fd6-331">Buradan sunucu iş parçacığı işlevinden *thread_server_entry*, satır 202 ' de *Select* çağrısını kullanarak alma olaylarını denetlemek için döngüler.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-331">From here the server thread function, *thread_server_entry*, loops to check for receive events using the *select* call on line 202.</span></span> <span data-ttu-id="e6fd6-332">Alma olayı, okuma için hazırlanma listesi karşılaştırılmasıyla belirlenen bir bağlantı isteği ise, 213 satırı *kabul eder* .</span><span class="sxs-lookup"><span data-stu-id="e6fd6-332">If a receive event is a connection request, which is determined by comparing the read ready list, it calls *accept* on line 213.</span></span> <span data-ttu-id="e6fd6-333">Bağlantı isteğini işlemek ve 223 satırındaki bir Istemciye bağlı TCP sunucusu yuvaları ana listesine eklemek için bir alt sunucu yuvası atanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-333">A child server socket is assigned to handle the connection request and added to the master list of TCP server sockets connected to a Client on line 223.</span></span> <span data-ttu-id="e6fd6-334">Yeni bağlantı isteği yoksa, sunucu iş parçacığı daha sonra 236 satırından başlayan for döngüsünde alma olayları için şu anda bağlı olan tüm yuvaları denetler.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-334">If there are no new connection requests, the server thread then checks all the currently connected sockets for receive events in the for loop starting on line 236.</span></span> <span data-ttu-id="e6fd6-335">Alma olayı beklenirken, veri alınana (bağlantı diğer tarafa kapalı) *ve yuva* 277 satırındaki *soc_close* hizmeti kullanılarak kapatıldıktan kadar bu yuvaya *gönderme* ve alma işlemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-335">When a receive event waiting is detected, it calls *send* and *recv* on that socket until no data is received (connection closed on the other side) and the socket is closed using the *soc_close* service on line 277.</span></span>

<span data-ttu-id="e6fd6-336">Sunucu iş parçacığı kurulduktan sonra, *Thread_client_entry* istemci iş parçacığı girişi işlevi, 326 numaralı satırda bir yuva oluşturur ve 337. satırdaki *Connect* çağrısını kullanarak TCP sunucu yuvasına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-336">After the server thread sets up, the Client thread entry function, *thread_client_entry,* creates a socket on line 326 and connects with the TCP server socket using the *connect* call on line 337.</span></span> <span data-ttu-id="e6fd6-337">Ardından, sırasıyla *gönderme* ve *alma hizmetlerini kullanarak paket gönderme ve alma* döngüleri olur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-337">It then loops to send and receive packets using the *send* and *recv* services respectively.</span></span> <span data-ttu-id="e6fd6-338">Daha fazla veri alınmadığında, *soc_close* hizmeti kullanılarak 398 satırındaki yuvayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-338">When no more data is received, it closes the socket on line 398 using the *soc_close* service.</span></span> <span data-ttu-id="e6fd6-339">Bağlantı kesildikten sonra, istemci iş parçacığı girişi işlevi yeni bir TCP yuvası oluşturur ve while döngüsü 321. satırda başladığında başka bir bağlantı isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-339">After disconnection, the client thread entry function creates a new TCP socket and makes another connection request in the while loop started on line 321.</span></span>

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection, sending,
and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQR
    STUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */

ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */

VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */
int     main()
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

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool", 128,
                                pointer, 16384);

    pointer = pointer + 16384;
    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                    0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                    pointer, 2048, 1);
                    pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable ARP \n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize (&bsd_ip, &bsd_pool,pointer, 2048, 2);
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT       status, sock, sock_tcp_server;
ULONG     actual_status;
INT       Clientlen;
INT       i;
UINT      is_set = NX_FALSE;
struct    sockaddr_in serverAddr;
struct    sockaddr_in ClientAddr;

    tx_thread_sleep(100);

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
        &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("Error on Server socket %d create \n", sock_tcp_server);
        return;
    }

    printf("Server socket %d created\n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    serverAddr.sin_port = htons(SERVER_PORT);

    /* Bind this server socket */
    status = bind (sock_tcp_server, (struct sockaddr *) &serverAddr,
                sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error on Server Socket %d Bind \n", sock_tcp_server);
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen (sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error on Server Socket %d Listen\n", sock_tcp_server);
        return;
    }
    else
        printf("Server socket %d listen complete\n", sock_tcp_server);

    /* All set to accept client connections */

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ((status == 0xFFFFFFFF) || (status == 0))
        {

            printf("Error with select. Status 0x%x\n", status);

            continue;
        }

        /* Check for a connection request. */
        is_set = FD_ISSET(sock_tcp_server, &read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,(struct sockaddr*)&ClientAddr,
                        &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i , &master_list)) &&
                (FD_ISSET(i , &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server received no data from Client on
                            socket %d)\n", i);
                        break;
                    }
                    else if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server receiving data from Client on
                            socket %d\n", i);
                        break;
                    }
                    if(status == SERVER_RCV_BUFFER_SIZE) status--;
                    Server_Rcv_Buffer[status] = 0;
                    printf("Server socket %d received %d bytes: %s\n ",
                            i, (ULONG)status, Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                        Client\n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                        Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != NX_SOC_ERROR)
                {
                    printf("Server socket %d closed \n", i);
                }
                else
                {
                    printf("Error on closing Server socket %d \n", i);
                }
            }
        }

    /* Loop back to check any next client connection */
    }
}

CHAR     Client_Rcv_Buffer[100];

VOID     thread_client_entry(ULONG thread_input)
{

INT        status;
INT        sock_tcp_client, length;
struct     sockaddr_in echoServAddr;
struct     sockaddr_in localAddr; /

    /* Let the server side get set up. */
    tx_thread_sleep(200);

    /* Set local port for displaying IP address and port. */
    memset(&localAddr, 0, sizeof(localAddr));
    localAddr.sin_family = AF_INET;
    localAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    localAddr.sin_port = htons(CLIENT_PORT);

    /* Set server port and IP address which we need to connect. */
    memset(&echoServAddr, 0, sizeof(echoServAddr));
    echoServAddr.sin_family = AF_INET;
    echoServAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    echoServAddr.sin_port = htons(SERVER_PORT);

    /* Now make client connections with the server. */
    while (1)
    {

        printf("\n");

        /* Create BSD TCP Socket */
        sock_tcp_client = socket( AF_INET, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n", sock_tcp_client);
            return;
        }

        printf("Client socket %d created\n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr,
                        sizeof(echoServAddr));

        /* Check for error. */
        if (status != OK)
        {
            printf("Error on Client socket %d connect\n", sock_tcp_client);
                    soc_close(sock_tcp_client);
            return;
        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr,
                            &length);

        printf("Client port = %lu , Client = 0x%x,",
            htonl(localAddr.sin_port), htonl(localAddr.sin_addr.s_addr));

        length = sizeof(struct sockaddr_in);

        status = getpeername( sock_tcp_client, (struct sockaddr *)
                            &echoServAddr, &length);

        printf("Remote port = %lu, Remote IP = 0x%x \n",
                htonl(echoServAddr.sin_port),
                htonl(echoServAddr.sin_addr.s_addr));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
            sock_tcp_client);

            status = send(sock_tcp_client, "Hello", (sizeof("Hello")), 0);

            if (status == ERROR)
            {
                printf("Error: Client Socket (%d) send \n", sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,100,0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    380 printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Nothing received by Client on socket %d\n",
                            sock_tcp_client);
                }

                break;
            }
            else
            {
                printf("Client socket %d received %d bytes: %s\n",
                        sock_tcp_client,
                        status, Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = soc_close(sock_tcp_client);

        if (status != ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```

## <a name="small-ipv6-example-system"></a><span data-ttu-id="e6fd6-340">Küçük IPv6 örnek sistemi</span><span class="sxs-lookup"><span data-stu-id="e6fd6-340">Small IPv6 Example System</span></span>

<span data-ttu-id="e6fd6-341">IPv6 ağları için NetX Duo BSD hizmetlerinin nasıl kullanılacağına ilişkin bir örnek aşağıdaki programda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-341">An example of how to use NetX Duo BSD services for IPv6 networks is described in the program below.</span></span> <span data-ttu-id="e6fd6-342">Bu örnek, daha önce birkaç önemli farklılık ile açıklanan IPv4 tanıtım programına çok benzer.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-342">This example is very similar to the IPv4 demo program previously described with a few important differences.</span></span>

<span data-ttu-id="e6fd6-343">İstemci ve sunucu iş parçacıkları, BSD paket havuzu, IP örneği ve BSD başlatması, IPv4 BSD yuvaları için yaptığı gibi olur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-343">The client and server threads, BSD packet pool, IP instance and BSD initialization happens as it does for IPv4 BSD sockets.</span></span>

<span data-ttu-id="e6fd6-344">Sunucu iş parçacığı girişi işlevinde *thread_server_entry*, *sockaddr_in6* ve 145-148 numaralı satırlarda *NXD_ADDRESS* veri türlerini kullanarak birkaç IPv6 değişkeni tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-344">In the server thread entry function, *thread_server_entry*, defines a couple IPv6 variables using *sockaddr_in6* and *NXD_ADDRESS* data types on lines 145-148.</span></span> <span data-ttu-id="e6fd6-345">NXD_ADDRESS veri türü aslında hem IPv4 hem de IPv6 adres türlerini saklayabilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-345">The NXD_ADDRESS data type can actually store both IPv4 and IPv6 address types.</span></span>

<span data-ttu-id="e6fd6-346">Daha sonra, sunucu iş parçacığı IP örneğindeki IPv6 ve ICMPv6 'Yı 161 ve 169 numaralı satırda sırasıyla *nxd_ipv6_enable* ve *nxd_icmpv6_enable* hizmetini kullanarak sunar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-346">Next, the server thread enables IPv6 and ICMPv6 on the IP instance using the *nxd_ipv6_enable* and *nxd_icmpv6_enable* service respectively on line 161 and 169.</span></span> <span data-ttu-id="e6fd6-347">Sonra, bağlantı yerel ve genel IP adresleri IP örneğiyle kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-347">Next, the link local and global IP addresses are registered with the IP instance.</span></span> <span data-ttu-id="e6fd6-348">Bu, 180 ve 195 satırlarında *nxd_ipv6_address_set* hizmeti kullanılarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-348">This is done using the *nxd_ipv6_address_set* service on lines 180 and 195.</span></span> <span data-ttu-id="e6fd6-349">Daha sonra, yinelenen adres algılama protokolünü tamamlaması için IP iş parçacığı görevinin yeterince uzun sürmesine izin verebilir ve bu adresleri 201 numaralı satırdaki *tx_thread_sleep* çağrısında geçerli adresler olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-349">It then sleeps long enough for the IP thread task to complete the Duplicate Address Detection protocol and register these addresses as valid addresses on the *tx_thread_sleep* call on line 201.</span></span>

<span data-ttu-id="e6fd6-350">Sonra TCP sunucusu yuvası, 204 satırındaki AF_INET6 yuva türü giriş bağımsız değişkeniyle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-350">Next, the TCP server socket is created with the AF_INET6 socket type input argument on line 204.</span></span> <span data-ttu-id="e6fd6-351">Yuva IPv6 adresi ve bağlantı noktası, 216-221 satırlarında, verileri de BSD yuva Hizmetleri için ağ bayt sırasına koymak üzere *htonl* ve *hton* makroları kullanımını belirterek ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-351">The socket IPv6 address and port are set on lines 216-221, again noting the use of *htonl* and *htons* macros to put data in network byte order for BSD socket services.</span></span> <span data-ttu-id="e6fd6-352">Buradan, sunucu iş parçacığı girişi işlevi, IPv4 örneği ile neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-352">From here on, the server thread entry function is virtually identical to the IPv4 example.</span></span>

<span data-ttu-id="e6fd6-353">İstemci iş parçacığı girişi işlevi *thread_client_entry*, bir sonraki adımda tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-353">The client thread entry function, *thread_client_entry*, is defined next.</span></span> <span data-ttu-id="e6fd6-354">Bu örnekteki TCP istemcisi TCP sunucusuyla aynı IP örneğini ve IPv6 adresini paylaştığından, IP örneğinde IPv6 veya ICMPv6 hizmetlerini etkinleştirmek zorunda kalmaz.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-354">Note that because the TCP client in this example shares the same IP instance and IPv6 address as the TCP server, we do not need to enable IPv6 or ICMPv6 services on the IP instance again.</span></span> <span data-ttu-id="e6fd6-355">Ayrıca, IPv6 adresi zaten IP örneğiyle birlikte kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-355">Further, the IPv6 address is also already registered with the IP instance.</span></span> <span data-ttu-id="e6fd6-356">Bunun yerine, istemci iş parçacığı girişi işlevi yalnızca sunucunun ayarlaması için 368 satırını bekler.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-356">Instead, the client thread entry function simply waits on line 368 for the server to set up.</span></span> <span data-ttu-id="e6fd6-357">Sunucu adresi ve bağlantı noktası ayarlanır, ana bilgisayar 387-392 satırlarında ağ baytı sıralaması makrolarıyla birlikte kullanılır ve ardından Istemci, 412. satırdaki TCP sunucusuyla bağlantı kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-357">The server address and port are set, using the host to network byte order macros on lines 387-392, and then the Client can connect with the TCP server on line 412.</span></span> <span data-ttu-id="e6fd6-358">378-383. satırlardaki yerel IP adresi veri türlerinin yalnızca 425 ve 434 sırasıyla *GetSockName* ve *GetPeerName* hizmetlerini göstermek için kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-358">Note that the local IP address data types in lines 378-383 are used only to demonstrate the *getsockname* and *getpeername* services on lines 425 and 434 respectively.</span></span> <span data-ttu-id="e6fd6-359">Veriler ağdan geldiği için, 378-383 satırlarında kullanılan bayt sırası makrolarını barındırmak için ağ.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-359">Because the data is coming from the network, the network to host byte order macros as used in lines 378-383.</span></span>

<span data-ttu-id="e6fd6-360">İstemci iş parçacığı girişi işlevi, bir TCP yuvası oluşturduğu bir döngü girer, bir TCP bağlantısı yapar ve IPv4 örneği ile aynı şekilde daha fazla veri alınana kadar, TCP sunucusuyla veri gönderir ve alır.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-360">Next the client thread entry function enters a loop in which it creates a TCP socket, makes a TCP connection and sends and receives data with the TCP server until no more data is received virtually the same as the IPv4 example.</span></span> <span data-ttu-id="e6fd6-361">Ardından, 483. satırdaki yuvayı kapatır, kısa bir süre duraklayıp başka bir TCP yuvası oluşturur ve bir TCP sunucu bağlantısı ister.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-361">It then closes the socket on line 483, pauses briefly and creates another TCP socket and requests a TCP server connection.</span></span>

<span data-ttu-id="e6fd6-362">IPv4 örneğinde önemli bir *farklılık, AF_INET6* giriş bağımsız değişkenini kullanarak bir IPv6 yuvası belirtmektir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-362">One important difference with the IPv4 example is the *socket* calls specify an IPv6 socket using the AF_INET6 input argument.</span></span> <span data-ttu-id="e6fd6-363">Diğer önemli fark, TCP Istemci *bağlantı* çağrısının bir *sockaddr_in6* veri türü ve bir length bağımsız değişkenini *sockaddr_in6* veri türü boyutuna ayarlamış olması gerektiğidir.</span><span class="sxs-lookup"><span data-stu-id="e6fd6-363">Another important difference is that the TCP Client *connect* call takes an *sockaddr_in6* data type and a length argument set to the size of the *sockaddr_in6* data type.</span></span>

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection,
disconnection, sending, and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */
ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */
VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

int     main()
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

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool",
    128, pointer, 16384);

    pointer = pointer + 16384;

    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                        0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                        pointer, 2048, 1);
                        pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in enable ARP on BSD IP instance\n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 2);

    /* Check BSD initialize status. */
    if (status)
    {
        error_counter++;
        printf("Error in BSD initialize \n");
    }

    pointer = pointer + 2048;
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT             status, sock, sock_tcp_server;
ULONG           actual_status;
INT             Clientlen;
INT             i;
UINT            is_set = NX_FALSE;
NXD_ADDRESS     ip_address;
struct          sockaddr_in6 serverAddr;
struct          sockaddr_in6 ClientAddr;
UINT            iface_index, address_index;

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
            &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable IPv6 */
    status = nxd_ipv6_enable(&bsd_ip);
    if((status != NX_SUCCESS) && (status != NX_ALREADY_ENABLED))
    {
        printf("Error with IPv6 enable 0x%x\n", status);
        return;
    }

    /* Enable ICMPv6 */
    status = nxd_icmp_enable(&bsd_ip);

    if(status)
    {
        printf("Error with ECMPv6 enable 0x%x\n", status);
        return;
    }

    /* Set the primary interface for our DNS IPv6 addresses. */
    iface_index = 0;

    /* This assumes we are using the primary network interface (index 0). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, NX_NULL, 10,
                                &address_index);

    if (status)
        return;

    /* Set ip_0 interface address. */
    ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    ip_address.nxd_ip_address.v6[0] = htonl(0x20010db8);
    ip_address.nxd_ip_address.v6[1] = htonl(0x0000f101);
    ip_address.nxd_ip_address.v6[2] = 0;
    ip_address.nxd_ip_address.v6[3] = htonl(0x101);

    /* Set the host global IP address. We are assuming a 64
    bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, &ip_address, 64,
                                &address_index);

    if (status)
        return;

    /* Wait for IPv6 stack to finish DAD process. */
    tx_thread_sleep(400);

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET6, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("\nError: BSD TCP Server socket create \n");
        return;
    }

    printf("\nBSD TCP Server socket created %lu \n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    serverAddr.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    serverAddr.sin6_addr._S6_un._S6_u32[2] = 0x0;
    serverAddr.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    serverAddr.sin6_port = htons(SERVER_PORT);
    serverAddr.sin6_family = AF_INET6;

    /* Bind this server socket */
    status = bind(sock_tcp_server, (struct sockaddr *) &serverAddr,
                    sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error: Server Socket Bind \n");
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen(sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error: Server Socket Listen\n");
        return;
    }
    else
        printf("Server Listen complete\n");

    /* All set to accept client connections */
    printf("Now accepting client connections\n");

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ( (status == 0xFFFFFFFF) || (status == 0) )
        {
            printf("Error with select? Status 0x%x. Try again\n", status);

            continue;
        }

        /* Detected a connection request. */
        is_set = FD_ISSET(sock_tcp_server,&read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,
            (struct sockaddr*)&ClientAddr,
            &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {
                printf("New connection %d\n", sock);

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i, &master_list)) &&
                (FD_ISSET(i, &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server socket %d received no data from
                                Client)\n", i);

                        break;
                    }
                    else if (status == 0xFFFFFFFF)
                    {
                        printf("Error on Server socket %d receiving data from
                                Client\n", i);

                        break;
                    }

                    printf("Server socket %d received from Client %lu bytes:
                            %s\n ", i, (ULONG)status,
                            Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                                Client \n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                                Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != ERROR)
                {
                    printf("Server socket %d closing\n", i);
                }
                else
                {

                    printf("Error on Server socket %d closing\n", i);
                }
            }
        }

        /* Loop back to check any next client connection */
    }
}

#define     CLIENT_BUFFER_SIZE 100
CHAR        Client_Rcv_Buffer[CLIENT_BUFFER_SIZE];

VOID        thread_client_entry(ULONG thread_input)
{

INT         status;
INT         sock_tcp_client, length;
struct      sockaddr_in6 echoServAddr6;
struct      sockaddr_in6 localAddr6; address */

    /* Wait for the server side to get set up, including the DAD process. */
    tx_thread_sleep(500);

    /* ICMPv6 and IPv6 should already be enabled on the IP instance
    by the server thread entry function. */

    /* Further the IPv6 address is already established with the IP instance.
    so no need to wait for DAD completion. */

    /* Set local port and IP address (used only for getsockname call). */
    memset(&localAddr6, 0, sizeof(localAddr6));
    localAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    localAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    localAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    localAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    localAddr6.sin6_port = htons(CLIENT_PORT);
    localAddr6.sin6_family = AF_INET6;

    /* Set Server port and IP address to connect to the TCP server. */
    memset(&echoServAddr6, 0, sizeof(echoServAddr6));
    echoServAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    echoServAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    echoServAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    echoServAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    echoServAddr6.sin6_port = htons(SERVER_PORT);
    echoServAddr6.sin6_family = AF_INET6;

    /* Now make client connections with the server. */
    while (1)
    {
        printf("\n");

        /* Create BSD TCP Socket */

        sock_tcp_client = socket(AF_INET6, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n");
            return;
        }

        printf("Client socket %d created \n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr6,
                sizeof(echoServAddr6));

        /* Check for error. */
        if (status != NX_SOC_OK)
        {
            printf("Error on Client socket %d connect\n");
            soc_close(sock_tcp_client);
            return;

        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr6,
        &length);

        printf("Client port = %lu , Client = 0x%x 0x%x 0x%x 0x%x,",
                ntohs(localAddr6.sin6_port),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[3]));

        length = sizeof(struct sockaddr_in6);

        status = getpeername(sock_tcp_client, (struct sockaddr *)
                            &echoServAddr6, &length);

        printf("Remote port = %lu, Remote IP = 0x%x 0x%x 0x%x 0x%x \n",
                ntohs(echoServAddr6.sin6_port),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[3]));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
                sock_tcp_client);

            status = send(sock_tcp_client, "Hello", sizeof("Hello"), 0);

            if (status == NX_SOC_ERROR)
            {
                printf("Error on Client Socket (%d) send \n",
                        sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message: Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,
                        CLIENT_BUFFER_SIZE, 0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Client received no data on socket %d\n",
                            sock_tcp_client);
                }

            break;
            }
            else
            {
                printf("Client socket %d received %d bytes and this message:
                        %s\n", sock_tcp_client, status,
                        Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = oc_close(sock_tcp_client);

        if (status != NX_SOC_ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```
