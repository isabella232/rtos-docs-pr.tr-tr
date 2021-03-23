---
title: Bölüm 2-Azure RTOS NetX DHCP sunucusunu yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX DHCP sunucusu bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 034a4d74c566fbfe94981a42b7e06e7f2ee79d25
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826789"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-dhcp-server"></a><span data-ttu-id="f26c5-103">Bölüm 2-Azure RTOS NetX DHCP sunucusunu yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="f26c5-103">Chapter 2 - Installation and use of the Azure RTOS NetX DHCP Server</span></span>

<span data-ttu-id="f26c5-104">Bu bölümde, Azure RTOS NetX DHCP bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX DHCP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="f26c5-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="f26c5-105">Product Distribution</span></span>

<span data-ttu-id="f26c5-106">Azure RTOS NetX DHCP sunucusu, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="f26c5-106">Azure RTOS NetX DHCP Server can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="f26c5-107">Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="f26c5-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="f26c5-108">**nx_dhcp_server. h**: NETX DHCP sunucusu için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="f26c5-108">**nx_dhcp_server.h**: Header file for NetX DHCP Server</span></span>
- <span data-ttu-id="f26c5-109">**nx_dhcp_server. c**: NETX DHCP sunucusu Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="f26c5-109">**nx_dhcp_server.c**: C Source file for NetX DHCP Server</span></span>
- <span data-ttu-id="f26c5-110">**nx_dhcp_server.pdf**: NETX DHCP sunucusunun PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="f26c5-110">**nx_dhcp_server.pdf**: PDF description of NetX DHCP Server</span></span>
- <span data-ttu-id="f26c5-111">**demo_netx_dhcp_server. c**: NETX DHCP sunucusu gösterimi</span><span class="sxs-lookup"><span data-stu-id="f26c5-111">**demo_netx_dhcp_server.c**: NetX DHCP Server demonstration</span></span>

## <a name="dhcp-installation"></a><span data-ttu-id="f26c5-112">DHCP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="f26c5-112">DHCP Installation</span></span>

<span data-ttu-id="f26c5-113">NetX DHCP sunucusunu kullanabilmeniz için, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-113">In order to use NetX DHCP Server, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="f26c5-114">Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_dhcp_server. h* ve *nx_dhpc_server. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-114">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_dhcp_server.h* and *nx_dhpc_server.c* files should be copied into this directory.</span></span>

## <a name="using-netx-dhcp-server"></a><span data-ttu-id="f26c5-115">NetX DHCP sunucusu kullanma</span><span class="sxs-lookup"><span data-stu-id="f26c5-115">Using NetX DHCP Server</span></span>

<span data-ttu-id="f26c5-116">NetX DHCP sunucusu kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-116">Using NetX DHCP Server is easy.</span></span> <span data-ttu-id="f26c5-117">Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_dhcp_server.* h içermelidir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-117">Basically, the application code must include *nx_dhcp_server.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="f26c5-118">*Nx_dhcp_server. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen DHCP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-118">Once *nx_dhcp_server.h* is included, the application code is then able to make the DHCP function calls specified later in this guide.</span></span> <span data-ttu-id="f26c5-119">Uygulama, yapı işlemine *nx_dhcp_server. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-119">The application must also include *nx_dhcp_server.c* in the build process.</span></span> <span data-ttu-id="f26c5-120">Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-120">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="f26c5-121">NetX DHCP sunucusunu kullanma hakkında daha fazla bilgi için, NETX [DHCP sunucusunun](#constraints-of-the-netx-dhcp-server) [NETX dhcpserver](#requirements-of-the-netx-dhcp-server) ve kısıtlamalarına yönelik aşağıdaki bölümlerde yer alan gereksinimlere bakın.</span><span class="sxs-lookup"><span data-stu-id="f26c5-121">For more details on using NetX DHCP Server, see the following sections [Requirements of the NetX DHCPServer](#requirements-of-the-netx-dhcp-server) and [Constraints of the NetX DHCP Server](#constraints-of-the-netx-dhcp-server).</span></span>

> [!NOTE]
> <span data-ttu-id="f26c5-122">DHCP, NetX UDP hizmetlerini kullandığından, DHCP kullanılmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-122">Since DHCP utilizes NetX UDP services, UDP must be enabled with the *nx_udp_enable* call prior to using DHCP.</span></span>

## <a name="requirements-of-the-netx-dhcp-server"></a><span data-ttu-id="f26c5-123">NetX DHCP sunucusunun gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="f26c5-123">Requirements of the NetX DHCP Server</span></span>

<span data-ttu-id="f26c5-124">NetX DHCP sunucusu, tanınmış DHCP bağlantı noktası 67 ' e atanmış bir UDP yuva bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-124">The NetX DHCP Server requires a UDP socket port assigned to the well known DHCP port 67.</span></span> <span data-ttu-id="f26c5-125">Uygulama, DHCP sunucusunu oluşturmak için en az 548 bayt artı IP, UDP ve Ethernet üst bilgileri (4 baytlık hizalamayla toplam 44 bayt) ile birlikte paket yüküne sahip bir paket havuzu oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-125">To create the DHCP Server, the application must create a packet pool with packet payload at least 548 bytes plus IP, UDP and Ethernet headers (which total 44 bytes with 4 byte alignment).</span></span>

<span data-ttu-id="f26c5-126">Sunucu ve Istemcinin her ikisi de Ethernet donanım adresi ayarlarını kullandığı varsayılır:</span><span class="sxs-lookup"><span data-stu-id="f26c5-126">It is assumed that the Server and Client are both using Ethernet hardware address settings:</span></span>

- <span data-ttu-id="f26c5-127">**Donanım türü**: 1</span><span class="sxs-lookup"><span data-stu-id="f26c5-127">**Hardware type**: 1</span></span>
- <span data-ttu-id="f26c5-128">**Donanım uzunluğu**: 6</span><span class="sxs-lookup"><span data-stu-id="f26c5-128">**Hardware length**: 6</span></span>
- <span data-ttu-id="f26c5-129">**Atlama** sayısı: 0</span><span class="sxs-lookup"><span data-stu-id="f26c5-129">**Hops**: 0</span></span>

### <a name="multiple-client-sessions"></a><span data-ttu-id="f26c5-130">Birden çok Istemci oturumu</span><span class="sxs-lookup"><span data-stu-id="f26c5-130">Multiple Client Sessions</span></span>

<span data-ttu-id="f26c5-131">NetX DHCP sunucusu, etkin DHCP istemcilerinin bir tablosunu ve Istemcinin (' durum ') ne olduğunu (örneğin, DHCP durumları INIT, önyükleme, seçme, ISTEME, yenıleme vb.) tutarak birden çok Istemci oturumunu idare edebilir. Bir sonraki Istemci iletisini almadan önce oturum zaman aşımı süresi dolarsa, Istemci bir IP kiralamaya bağlanmadığı müddetçe sunucu, Istemci oturumu verilerini temizler ve atanan IP adresini kullanılabilir havuza geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="f26c5-131">The NetX DHCP Server can handles multiple Client sessions by keeping a table of active DHCP clients and what 'state' the Client is in e.g. DHCP states INIT, BOOT, SELECTING, REQUESTING, RENEWING etc. If the session time out expires before receiving the next Client message, unless that Client is bound to an IP lease, the Server will clear the Client session data and return the assigned IP address back to the available pool.</span></span> <span data-ttu-id="f26c5-132">Sunucu aynı Istemciden birden çok bulma iletisi alırsa, sunucu oturum zaman aşımını sıfırlar ve Istemcinin sonraki bir Istek iletisinde kabul etmesi için ayrılan IP adresini tutar.</span><span class="sxs-lookup"><span data-stu-id="f26c5-132">If the Server receives multiple DISCOVER messages from the same Client the Server resets the session time out and keeps the IP address reserved for the Client to accept in a subsequent REQUEST message.</span></span>

<span data-ttu-id="f26c5-133">NetX DHCP sunucusu, tek durumlu Istemci DHCP isteğini de kabul eder, örneğin Istemci yalnızca bir Istek iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-133">The NetX DHCP Server also accepts the single state Client DHCP request e.g. the Client only sends a REQUEST message.</span></span> <span data-ttu-id="f26c5-134">Bu, Istemciye daha önce DHCP sunucusundan bir IP kirası atandığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="f26c5-134">This assumes the Client has been previously assigned an IP lease from the DHCP server.</span></span>

### <a name="setting-interface-specific-network-parameters-server-responses"></a><span data-ttu-id="f26c5-135">Arabirime özgü ağ parametreleri sunucu yanıtları ayarlanıyor</span><span class="sxs-lookup"><span data-stu-id="f26c5-135">Setting Interface Specific Network Parameters Server Responses</span></span>

<span data-ttu-id="f26c5-136">Uygulama, *nx_dhcp_set_interface_network_parameters* HIZMETINI kullanarak DHCP istemci isteklerini işleyen her arabirim için yönlendirici, alt ağ MASKESI ve DNS sunucusu parametrelerini ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-136">The application can set the router, subnet mask and DNS server parameters for each interface it handles DHCP Client requests, using the *nx_dhcp_set_interface_network_parameters* service.</span></span> <span data-ttu-id="f26c5-137">Aksi takdirde bu parametreler, sırasıyla sunucunun birincil arabirimindeki IP ağ geçidine, DHCP ağ alt ağına ve DHCP sunucusu IP adresine varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-137">Otherwise these parameters are defaulted to the IP gateway on the Server's primary interface, its DHCP network subnet, and DHCP Server IP address, respectively.</span></span>

<span data-ttu-id="f26c5-138">DHCP sunucusu, DHCP istemcilerine gönderdiği DHCP iletilerinin seçenek verilerinde bu parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-138">The DHCP Server includes these parameters in the option data of DHCP messages it sends to DHCP clients.</span></span>

### <a name="assigning-ip-addresses-to-the-client"></a><span data-ttu-id="f26c5-139">Istemciye IP adresleri atama</span><span class="sxs-lookup"><span data-stu-id="f26c5-139">Assigning IP addresses to the Client</span></span>

<span data-ttu-id="f26c5-140">Istemci bulma iletisi istenen bir IP adresi belirtmezse, DHCP sunucusu kendi havuzundan birini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-140">If the Client DISCOVER message does not specify a requested IP address, the DHCP Server can use one from its own pool.</span></span> <span data-ttu-id="f26c5-141">Sunucuda kullanılabilir IP adresi yoksa, Istemciye bir NACK iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-141">If the Server has no available IP addresses it will send the Client a NACK message.</span></span>

<span data-ttu-id="f26c5-142">NetX DHCP sunucusu, IP adresi kullanılabildiği ve sunucu IP adresi veritabanında bulunduğu sürece Istemci ISTEğI iletisinde istenen IP adresini verir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-142">The NetX DHCP Server will grant the requested IP address in the Client REQUEST message as long as the IP address is available and can be found in the Server IP address database.</span></span> <span data-ttu-id="f26c5-143">Uygulama, *nx_dhcp_create_server_ip_address_list* HIZMETINI kullanarak DHCP istemcilerine atamak için sunucunun kullanılabilir IP adresleri listesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-143">The application creates the Server's list of available IP addresses for assigning to DHCP Clients using the *nx_dhcp_create_server_ip_address_list* service.</span></span> <span data-ttu-id="f26c5-144">Sunucuda istenen IP adresleri yoksa veya başka bir konağa atanırsa, Istemciye bir NACK iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-144">If the Server does not have the requested IP addresses or it is assigned to another host it will send the Client a NACK message.</span></span>

<span data-ttu-id="f26c5-145">DHCP sunucusu bir Istemci isteği aldığında, istemcinin DHCP iletisindeki Istemci MAC adresi alanındaki istemci MAC adresini benzersiz bir şekilde kullandığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f26c5-145">When the DHCP Server receives a Client request, it identifies that Client uniquely using the Client MAC address in the Client MAC address field in the DHCP message.</span></span> <span data-ttu-id="f26c5-146">Istemci MAC adresini değiştirirse veya başka bir alt ağa başka bir yere taşınmışsa, IP adresini kullanılabilir havuza geri döndürmek için sunucuya bir sürüm iletisi göndermelidir ve INIT durumunda yeni bir IP adresi istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-146">If the Client changes it's MAC address or is moved elsewhere onto another subnet it should send a RELEASE message to the Server to return the IP address back to the available pool, and request a new IP address in the INIT state.</span></span>

<span data-ttu-id="f26c5-147">Ayrıntılar için **küçük örnek sistem** bölümünün Şekil 1,1 bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f26c5-147">See Figure 1.1 of the **Small Example System** section for details.</span></span> <span data-ttu-id="f26c5-148">DHCP sunucusu örneğine kaydedilen IP adresi sayısı, DHCP sunucusu denetim bloğunda sunucu adresi dizisinin boyutuyla sınırlıdır ve yapılandırılabilir seçenek NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-148">The number of IP addresses saved to the DHCP Server instance is limited to the size of the server address array in the DHCP Server control block, and defined by the configurable option NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.</span></span>

### <a name="ip-address-lease-times"></a><span data-ttu-id="f26c5-149">IP adresi kiralama süreleri</span><span class="sxs-lookup"><span data-stu-id="f26c5-149">IP Address Lease Times</span></span>

<span data-ttu-id="f26c5-150">Bu kira süresi, yapılandırılabilir seçenekte NX_DHCP_DEFAULT_LEASE_TIME tanımlanan sunucu varsayılan kira süresinden daha azsa, DHCP sunucusu, istek Istemci kira süresini de kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f26c5-150">The DHCP Server will also accept the request Client lease time if that lease time is less than the Server default lease time which is defined in configurable option NX_DHCP_DEFAULT_LEASE_TIME.</span></span> <span data-ttu-id="f26c5-151">Istemciye atanan yenileme ve yeniden bağlama süreleri, kira süresi sonsuzluk (0xFFFFFFFF), bu durumda yenileme ve yeniden bağlama sürelerinin de sonsuz olarak ayarlandığı durumlar dışında %50 ve kira süresinin %85 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-151">Renewal and rebind times assigned to the Client are 50% and 85% of the lease time, respectively, unless the lease time is infinity (0xFFFFFFFF), in which case renewal and rebind times are also set to infinity.</span></span>

### <a name="dhcp-server-timeouts"></a><span data-ttu-id="f26c5-152">DHCP sunucusu zaman aşımları</span><span class="sxs-lookup"><span data-stu-id="f26c5-152">DHCP Server Timeouts</span></span>

<span data-ttu-id="f26c5-153">DHCP sunucusunda, oturum tamamlanana kadar bir sonraki DHCP Istemci iletisini beklemek için kullanıcı yapılandırılabilir bir oturum zaman aşımı NX_DHCP_CLIENT_SESSION_TIMEOUT vardır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-153">The DHCP Server has a user configurable session timeout, NX_DHCP_CLIENT_SESSION_TIMEOUT, for waiting for the next DHCP Client message unless the session is completed.</span></span> <span data-ttu-id="f26c5-154">Sunucu Istemciden sonraki iletiyi aldığında, daha önce gönderilen aynı ileti olup olmamasına bakılmaksızın zaman aşımı sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-154">The time out is reset when the Server receives the next message from the Client regardless if is the same message previously sent.</span></span>

### <a name="internal-error-handling"></a><span data-ttu-id="f26c5-155">İç hata işleme</span><span class="sxs-lookup"><span data-stu-id="f26c5-155">Internal error handling</span></span>

<span data-ttu-id="f26c5-156">DHCP sunucusu, *nx_dhcp_listen_for_messages* Işlevindeki DHCP istemci paketlerini alır ve işler.</span><span class="sxs-lookup"><span data-stu-id="f26c5-156">The DHCP Server receives and processes DHCP Client packets in the *nx_dhcp_listen_for_messages* function.</span></span> <span data-ttu-id="f26c5-157">Bu işlev, paket geçersizse geçerli DHCP Istemci paketini işlemeye devam eder veya DHCP sunucusu bir iç hatayla karşılaşır. n *x_dhcp_listen_for_messages* bir hata durumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f26c5-157">This function will discontinue processing the current DHCP Client packet if the packet is invalid, or the DHCP Server encounters an internal error.n *x_dhcp_listen_for_messages* returns an error status.</span></span> <span data-ttu-id="f26c5-158">DHCP sunucusu iş parçacığı, sonraki DHCP Istemci iletisini almak için bu işlevi çağırmadan önce ThreadX Scheduler ' ın her bir denetimini yeniden denetler.</span><span class="sxs-lookup"><span data-stu-id="f26c5-158">The DHCP Server thread relinquishes control briefly of the ThreadX scheduler before calling this function to receive the next DHCP Client message.</span></span> <span data-ttu-id="f26c5-159">Geçerli sürümde, nx_dhcp_listen_for_messages hata durumu getirleri için günlük desteği yoktur *.*</span><span class="sxs-lookup"><span data-stu-id="f26c5-159">In the current release there is no logging support for error status returns from *nx_dhcp_listen_for_messages.*</span></span>

### <a name="option-55-parameter-request-list"></a><span data-ttu-id="f26c5-160">Seçenek 55: parametre Istek listesi</span><span class="sxs-lookup"><span data-stu-id="f26c5-160">Option 55: Parameter Request List</span></span>

<span data-ttu-id="f26c5-161">NetX DHCP sunucusu, Istemciye geri ileten TEKLIF ve DHCPACK iletilerindeki parametre Istek seçeneği (55) listesine yüklenecek bir seçenek kümesiyle yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-161">The NetX DHCP Server must be configured with a set of options to load to Parameter Request Option (55) list in the OFFER and DHCPACK messages it transmits back to the Client.</span></span> <span data-ttu-id="f26c5-162">Bu seçenekler, Istemci ağı için ağ açısından kritik yapılandırma verilerini içermeli ve varsayılan olarak yönlendirici IP adresi, alt ağ maskesi ve DNS sunucusu olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-162">These options should include network critical configuration data for the Client network and by default is defined to be router IP address, subnet mask, and DNS server.</span></span> <span data-ttu-id="f26c5-163">Seçenek listesi, boşlukla ayrılmış bir liste ve Kullanıcı tarafından yapılandırılabilir NX_DHCP_DEFAULT_SERVER_OPTION_LIST tanımlı bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-163">The option list is a space delimited list and defined in the user configurable NX_DHCP_DEFAULT_SERVER_OPTION_LIST.</span></span> <span data-ttu-id="f26c5-164">Bu listede belirtilen seçeneklerin sayısı aynı zamanda Kullanıcı tanımlı NX_DHCP_DEFAULT_OPTION_LIST_SIZE eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-164">Note the number of options specified in this list must equal NX_DHCP_DEFAULT_OPTION_LIST_SIZE which is also user defined.</span></span>

## <a name="constraints-of-the-netx-dhcp-server"></a><span data-ttu-id="f26c5-165">NetX DHCP sunucusunun kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="f26c5-165">Constraints of the NetX DHCP Server</span></span>

### <a name="dhcp-messages"></a><span data-ttu-id="f26c5-166">DHCP Iletileri</span><span class="sxs-lookup"><span data-stu-id="f26c5-166">DHCP Messages</span></span>

<span data-ttu-id="f26c5-167">NetX DHCP sunucusu, IP adresini Istemciye vermeden önce ağ üzerinde başka bir yerde bir IP adresi atanmamış olduğunu doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="f26c5-167">The NetX DHCP Server does not verify that an IP address has not been assigned elsewhere on the network before granting the IP address to the Client.</span></span> <span data-ttu-id="f26c5-168">Birden çok DHCP sunucusu varsa, bu durum gerçekten olabilir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-168">If there are multiple DHCP servers, this can indeed be the case.</span></span> <span data-ttu-id="f26c5-169">*RFC 2131 ' e kadar, IP adresinin ağda benzersiz olduğunu doğrulama* (örneğin, adrese ping) olduğu için istemcinin sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-169">*As per RFC 2131, it is the Client's responsibility to verify the IP address is unique on its network* (e.g. pinging the address).</span></span> <span data-ttu-id="f26c5-170">Değilse, sunucu, veritabanını Istemciden güncelleştirmek için IP adresine sahip bir reddetme iletisi almalıdır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-170">If it is not, the Server should receive a DECLINE message with the IP address to update its database from the Client.</span></span>

<span data-ttu-id="f26c5-171">NetX DHCP sunucusu FORCE_RENEW iletileri vermiyor.</span><span class="sxs-lookup"><span data-stu-id="f26c5-171">The NetX DHCP Server does not issue FORCE_RENEW messages.</span></span> <span data-ttu-id="f26c5-172">IP adresi kiralamasını yenilemek için DHCP Istemcisine kadar olur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-172">It is up to the DHCP Client to renew its IP address lease.</span></span> <span data-ttu-id="f26c5-173">Ancak, DHCP sunucusu, tüm atanan IP adreslerinde kalan süreyi veritabanında izler.</span><span class="sxs-lookup"><span data-stu-id="f26c5-173">However, the DHCP Server monitors the time remaining on all the assigned IP addresses in its database.</span></span> <span data-ttu-id="f26c5-174">Bir IP adresi kirası sona erdiğinde, bu IP adresi kullanılabilir IP adresleri havuzuna döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f26c5-174">When an IP address lease expires, that IP address is returned to the pool of available IP addresses.</span></span> <span data-ttu-id="f26c5-175">Bu nedenle, IP adresi kiralamasını etkin bir şekilde yenilemek/yeniden bağlamak için Istemciye sahip olur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-175">Hence it is up to the Client to actively renew/rebind its IP address lease.</span></span>

<span data-ttu-id="f26c5-176">Istemci, bir IP kirasına (veya mevcut bir tane yenilendiğinde) verildiğinde ("bağlanır"), oturum verileri temizlenir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-176">Session data is cleared as soon as the Client either is granted ("bound") to an IP lease (or an existing one is renewed).</span></span> <span data-ttu-id="f26c5-177">Istemci paketi sahte bir şekilde kanıtlar veya Istemci yanıtlar arasında zaman aşımına uğrarsa, oturum verileri temizlenir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-177">If a Client packet proves bogus, or the Client times out between responses, session data is cleared.</span></span>

### <a name="saving-data-between-reboots"></a><span data-ttu-id="f26c5-178">Yeniden başlatmalar arasında veri kaydetme</span><span class="sxs-lookup"><span data-stu-id="f26c5-178">Saving Data Between Reboots</span></span>

<span data-ttu-id="f26c5-179">NetX DHCP sunucusu, istemci verilerini Istemci kayıt tablosuna DHCP isteği parametreleri dahil kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f26c5-179">The NetX DHCP Server saves Client data including DHCP request parameters in a Client record table.</span></span> <span data-ttu-id="f26c5-180">Bu tablo geçici olmayan bellekte depolanmaz. bu nedenle, DHCP sunucusu konağının, yeniden başlatmalar arasında bilgilerin kaydedilmemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-180">This table is not stored in non volatile memory, so if the DHCP Server host must reboot that information is not saved between reboots.</span></span>

<span data-ttu-id="f26c5-181">NetX DHCP sunucusu IP adresi kiralama verilerini bir IP adresi tablosuna kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f26c5-181">The NetX DHCP Server saves IP address lease data in a IP address table.</span></span> <span data-ttu-id="f26c5-182">Bu tablo geçici olmayan bellekte depolanmaz. bu nedenle, DHCP sunucusu konağının, yeniden başlatmalar arasında bilgilerin kaydedilmemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-182">This table is not stored in non volatile memory, so if the DHCP Server host must reboot that information is not saved between reboots.</span></span>

### <a name="relay-agents"></a><span data-ttu-id="f26c5-183">Geçiş aracıları</span><span class="sxs-lookup"><span data-stu-id="f26c5-183">Relay Agents</span></span>

<span data-ttu-id="f26c5-184">NetX DHCP sunucusu, ağ DHCP isteklerini desteklemediğinden, ' Relay Agent ' alanı için sıfır bir IP adresi ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-184">The NetX DHCP Server is configured with a zero IP address for the 'Relay agent' field because it does not support out of network DHCP requests.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="f26c5-185">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="f26c5-185">Small Example System</span></span>

<span data-ttu-id="f26c5-186">Aşağıda görüntülenen Şekil 1,1 ' de NetX DHCP sunucusunu kullanmanın ne kadar kolay olduğunu gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="f26c5-186">An example of how easy it is to use the NetX DHCP Server is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="f26c5-187">Bu örnekte, *nx_dhcp_server. h* DHCP içerme dosyası 5. satırda getirilir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-187">In this example, the DHCP include file *nx_dhcp_server.h* is brought in at line 5.</span></span> <span data-ttu-id="f26c5-188">DHCP sunucu iş parçacığı yığın boyutu, IP iş parçacığı yığın boyutu ve test iş parçacığı yığın boyutu, 7-13 satırlarında tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-188">DHCP Server thread stack size, IP thread stack size and test thread stack size are all defined in lines 7-13.</span></span>

<span data-ttu-id="f26c5-189">İlk olarak, DHCP sunucusunu durdurmak, yeniden başlatmak ve sonunda silmek için isteğe bağlı bir test iş parçacığı görevi 57 satırındaki "*test_thread_entry*" işleviyle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-189">First, an optional test thread task for stopping, restarting and eventually deleting the DHCP server is created with the "*test_thread_entry*" function at line 57.</span></span> <span data-ttu-id="f26c5-190">DHCP sunucu denetim bloğu "*dhcp_server*", 20. satırda genel değişken olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-190">A DHCP Server control block "*dhcp_server*" is defined as a global variable at line 20.</span></span> <span data-ttu-id="f26c5-191">Sunucu paket havuzunun, en azından standart DHCP iletisi (548 bayt artı IP ve UDP başlık baytı) kadar büyük bir yüke sahip paketlerle oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f26c5-191">Note that the server packet pool is created with packets having a payload at least as large as the standard DHCP message (548 bytes plus IP and UDP header bytes).</span></span> <span data-ttu-id="f26c5-192">DHCP sunucusu için bir IP örneğini başarıyla oluşturduktan sonra, uygulama DHCP sunucusunu 96. satırda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-192">After successfully creating an IP instance for the DHCP Server, the application creates the DHCP Server in line 96.</span></span> <span data-ttu-id="f26c5-193">Daha sonra uygulama, sunucu IP örneğinin UDP etkin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f26c5-193">Next, the application enables the Server IP instance to be UDP enabled.</span></span> <span data-ttu-id="f26c5-194">DHCP sunucusunu başlatmadan önce, kullanılabilir IP adresi listesi *nx_dhcp_create_server_ip_address_list* hizmeti kullanılarak 137. satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-194">Before starting the DHCP Server, the available IP address list is created in line 137 using the *nx_dhcp_create_server_ip_address_list* service.</span></span> <span data-ttu-id="f26c5-195">Ağ yapılandırma parametreleri *nx_dhcp_set_interface_network_parameters* hizmeti kullanılarak aşağıdaki 138 satırında ayarlanır. uygulama, 141. satırdaki *Nx_dhcp_server_start* çağırdığında DHCP sunucusu hizmetleri kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-195">The network configuration parameters are set in the following line 138 using the *nx_dhcp_set_interface_network_parameters* service, DHCP Server services become available when the application calls the *nx_dhcp_server_start* at line 141.</span></span> <span data-ttu-id="f26c5-196">Test iş parçacığı görevi, DHCP sunucusunu durdurma ve yeniden başlatma kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-196">The test thread task demonstrates the use of stopping and restarting the DHCP server.</span></span>

```c
/* This is a small demo of NetX DHCP Server for the high-performance NetX TCP/IP stack. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nx_dhcp_server.h"

#define     DEMO_TEST_STACK_SIZE       2048
#define     DEMO_SERVER_STACK_SIZE     2048
#define     SERVER_IP_ADDRESS_LIST     "192.168.2.10 192.168.2.11 192.168.2.12"
#define     PACKET_PAYLOAD             1000
#define     PACKET_POOL_SIZE           (PACKET_PAYLOAD * 10)
#define     SERVER_IP_THREAD_STACK     2048

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD          test_thread;
NX_PACKET_POOL     server_pool;
NX_IP              server_ip;
NX_DHCP_SERVER     dhcp_server;

/* Define the counters used in the demo application... */

ULONG             state_changes;

/* Define thread prototypes. */

void     test_thread_entry(ULONG thread_input);
void     nx_etherDriver_mcf5485(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
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

    /* Create the test thread. */
    status = tx_thread_create(&test_thread, "test thread", test_thread_entry, 0,
                pointer, TEST_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_DONT_START);

    if (status)
    {
        printf("Error with DHCP test thread create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the DHCP Server packet pool. */
    status = nx_packet_pool_create(&server_pool, "NetX Main Packet Pool",
                                PACKET_PAYLOAD, pointer, PACKET_POOL_SIZE);
                                pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {
        printf("Error with DHCP server packet pool create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server IP instance. */
    status = nx_ip_create(&server_ip, "NetX DHCP Server IP", NX_DHCP_SERVER_IP_ADDRESS,
                        0xFFFFFF00UL, &server_pool, nx_etherDriver_mcf5485, pointer,
                        SERVER_IP_THREAD_STACK, 1);

    pointer = pointer + DEMO_IP_THREAD_STACK;

    /* Check for IP create errors. */
    if (status)
    {
        printf("Error with DHCP server IP task create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server instance. */
    status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE,"DHCP Server", &server_pool);

    if (status)
    {
        printf("Error with DHCP server create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_SERVER_STACK_SIZE;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors. */
    if (status)
    {
        printf("Error with ARP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable UDP traffic. */
    status = nx_udp_enable(&server_ip);

    /* Check for UDP enable errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable ICMP to enable the ping utility. */
    status = nx_icmp_enable(&server_ip);

    /* Check for errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
    }

    status = nx_dhcp_create_server_ip_address_list(&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);
    status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                        NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                        IP_ADDRESS(10,0,0,1));

    /* Start the DHCP Server. */
    status = nx_dhcp_server_start(&dhcp_server);

    tx_thread_resume(&test_thread);
}

/* Define the test thread. */
void     test_thread_entry(ULONG thread_input)
{

UINT     status;
UINT     keep_spinning;

    /* Just let the test thread be idle till we're ready to shut things down. */
    keep_spinning = 1;
    while(keep_spinning)
    {
        tx_thread_sleep(300);
    }

    printf("Stopping the server...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(500);

    printf("Starting the server...\n");
    status = nx_dhcp_server_start(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server start. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(600);

    printf("Stopping the server for good...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(200);

    printf("Deleting the server...\n");
    status = nx_dhcp_server_delete(&dhcp_server);
    if (status)
    {
        printf("Error with DHCP server delete. Status 0x%x\r\n", status);
        return;
    }
}
```

<span data-ttu-id="f26c5-197">Şekil 1,1 örnek NetX DHCP sunucusu uygulaması</span><span class="sxs-lookup"><span data-stu-id="f26c5-197">Figure 1.1 Example NetX DHCP Server application</span></span>

## <a name="configuration-options"></a><span data-ttu-id="f26c5-198">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f26c5-198">Configuration Options</span></span>

<span data-ttu-id="f26c5-199">NetX DHCP sunucusu oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-199">There are several configuration options for building NetX DHCP Server.</span></span> <span data-ttu-id="f26c5-200">Aşağıdaki listede her biri ayrıntılı açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="f26c5-200">The following list describes each in detail:</span></span>  
  
- <span data-ttu-id="f26c5-201">**NX_DISABLE_ERROR_CHECKING**: Bu seçenek temel DHCP hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-201">**NX_DISABLE_ERROR_CHECKING**: This option removes the basic DHCP error checking.</span></span> <span data-ttu-id="f26c5-202">Genellikle uygulamanın hataları ayıklandıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-202">It is typically used after the application is debugged.</span></span>  
- <span data-ttu-id="f26c5-203">**NX_DHCP_SERVER_THREAD_PRIORITY**: Bu seçenek, DHCP sunucusu iş parçacığının önceliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-203">**NX_DHCP_SERVER_THREAD_PRIORITY**: This option specifies the priority of the DHCP Server thread.</span></span> <span data-ttu-id="f26c5-204">Varsayılan olarak, bu değer DHCP iş parçacığının öncelik 2 ' de çalıştığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-204">By default, this value specifies that the DHCP thread runs at priority 2.</span></span>
- <span data-ttu-id="f26c5-205">**NX_DHCP_TYPE_OF_SERVICE**: Bu seçenek, DHCP UDP istekleri için gereken hizmet türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-205">**NX_DHCP_TYPE_OF_SERVICE**: This option specifies the type of service required for the DHCP UDP requests.</span></span> <span data-ttu-id="f26c5-206">Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-206">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="f26c5-207">**NX_DHCP_FRAGMENT_OPTION**: DHCP UDP istekleri için parça etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-207">**NX_DHCP_FRAGMENT_OPTION**: Fragment enable for DHCP UDP requests.</span></span> <span data-ttu-id="f26c5-208">Varsayılan olarak, bu değer UDP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-208">By default, this value is set to NX_DONT_FRAGMENT to disable UDP fragmenting.</span></span>
- <span data-ttu-id="f26c5-209">**NX_DHCP_TIME_TO_LIVE**: paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-209">**NX_DHCP_TIME_TO_LIVE**: Specifies the number of routers the packet can pass before it is discarded.</span></span> <span data-ttu-id="f26c5-210">Varsayılan değer 0x80 ' dır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-210">The default value is 0x80.</span></span>
- <span data-ttu-id="f26c5-211">**NX_DHCP_QUEUE_DEPTH** Kuyruğu temizlemeye başlamadan önce DHCP sunucusu yuvasının sakladığı paketlerin sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-211">**NX_DHCP_QUEUE_DEPTH** Specifies the number of packets that the DHCP Server socket keeps before flushing the queue.</span></span> <span data-ttu-id="f26c5-212">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-212">The default value is 5.</span></span>
- <span data-ttu-id="f26c5-213">**NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: NETX DHCP sunucusunun paket havuzundan bir paket ayırmasını bekleyeceği süre sonu zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-213">**NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: Specifies the timeout in timer ticks for the NetX DHCP Server to wait for allocate a packet from its packet pool.</span></span> <span data-ttu-id="f26c5-214">Varsayılan değer NX_IP_PERIODIC_RATE olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-214">The default value is set to NX_IP_PERIODIC_RATE.</span></span>
- <span data-ttu-id="f26c5-215">**NX_DHCP_SUBNET_MASK**: Bu, DHCP istemcisinin ile yapılandırılması gereken alt ağ maskesidir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-215">**NX_DHCP_SUBNET_MASK**: This is the subnet mask the DHCP Client should be configured with.</span></span> <span data-ttu-id="f26c5-216">Varsayılan değer 0xFFFFFF00 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-216">The default value is set to 0xFFFFFF00.</span></span>
- <span data-ttu-id="f26c5-217">**NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: Bu, DHCP sunucusu hızlı süreölçerinin, kalan oturum süresini denetlemesi ve zaman aşımına uğramış oturumları işlemek için zaman aşımı süresi.</span><span class="sxs-lookup"><span data-stu-id="f26c5-217">**NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: This is timeout period in timer ticks for the DHCP Server fast timer to check on session time remaining and handle sessions that have timed out.</span></span>
- <span data-ttu-id="f26c5-218">**NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: Bu, DHCP sunucusu yavaş zamanlayıcının, kalan IP adresi kiralama süresini ve zaman aşımına uğradığını denetlemesini sağlayan Zamanlayıcı işaretleri cinsinden zaman aşımı süresi olur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-218">**NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: This is timeout period in timer ticks for the DHCP Server slow timer to check on IP address lease time remaining and handle lease that have timed out.</span></span>
- <span data-ttu-id="f26c5-219">**NX_DHCP_CLIENT_SESSION_TIMEOUT**: Bu zaman aşımı SÜRESI, DHCP sunucusunun sonraki DHCP istemci iletisini almak için bekleyeceği süre sonu dönecektir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-219">**NX_DHCP_CLIENT_SESSION_TIMEOUT**: This is timeout period in timer ticks the DHCP Server will wait to receive the next DHCP Client message.</span></span>
- <span data-ttu-id="f26c5-220">**NX_DHCP_DEFAULT_LEASE_TIME**: Bu, DHCP istemcisine atanan sanıye cinsinden IP adresi kiralama süresi ve aynı zamanda istemciye atanan yenileme ve yeniden bağlama sürelerinin temelini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-220">**NX_DHCP_DEFAULT_LEASE_TIME**: This is IP Address lease time in seconds assigned to the DHCP Client, and the basis for computing the renewal and rebind times also assigned to the Client.</span></span> <span data-ttu-id="f26c5-221">Varsayılan değer 0xFFFFFFFF (Infinity) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-221">The default value is set to 0xFFFFFFFF (infinity).</span></span>
- <span data-ttu-id="f26c5-222">**NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: Bu, istemciye atamaya YÖNELIK kullanılabilir IP adreslerini tutmak Için DHCP sunucusu dizisinin boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-222">**NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: This is size of the DHCP Server array for holding available IP addresses for assigning to the Client.</span></span> <span data-ttu-id="f26c5-223">Varsayılan değer 20 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-223">The default value is 20.</span></span>
- <span data-ttu-id="f26c5-224">**NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: Bu, istemci kayıtlarının TUTULMASı Için DHCP sunucusu dizisinin boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-224">**NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: This is size of the DHCP Server array for holding Client records.</span></span> <span data-ttu-id="f26c5-225">Varsayılan değer 50 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-225">The default value is 50.</span></span>
- <span data-ttu-id="f26c5-226">**NX_DHCP_CLIENT_OPTIONS_MAX**: Bu, geçerli oturumdaki parametre isteği listesinde istenen tüm seçenekleri tutmak Için DHCP istemci örneğindeki dizinin boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-226">**NX_DHCP_CLIENT_OPTIONS_MAX**: This is size of the array in the DHCP Client instance for holding the all the requested options in the parameter request list in the current session.</span></span> <span data-ttu-id="f26c5-227">Varsayılan değer 12 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-227">The default value is 12.</span></span>
- <span data-ttu-id="f26c5-228">**NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: Bu, DHCP sunucusunun varsayılan seçenek listesini tutan, parametre istek LISTESINDEKI geçerli DHCP istemcisine tedarik eden tampondır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-228">**NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: This is the buffer holding the DHCP Server's default list of options to supply to the current DHCP Client in the parameter request list.</span></span> <span data-ttu-id="f26c5-229">Varsayılan değer "1 3 6" dır.</span><span class="sxs-lookup"><span data-stu-id="f26c5-229">The default is "1 3 6."</span></span>
- <span data-ttu-id="f26c5-230">**NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: Bu, DHCP sunucusunun varsayılan seçenek listesini tutan dizinin boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-230">**NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: This is the size of the array to hold the DHCP Server's default list of options.</span></span> <span data-ttu-id="f26c5-231">Varsayılan değer 3 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-231">The default value is 3.</span></span>
- <span data-ttu-id="f26c5-232">**NX_DHCP_SERVER_HOSTNAME_MAX**: Bu, sunucu ana bilgisayar adını tutan arabelleğin boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-232">**NX_DHCP_SERVER_HOSTNAME_MAX**: This is size of the buffer for holding the Server host name.</span></span> <span data-ttu-id="f26c5-233">Varsayılan değer 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-233">The default value is 32.</span></span>
- <span data-ttu-id="f26c5-234">**NX_DHCP_CLIENT_HOSTNAME_MAX**: Bu, geçerli DHCP sunucusu Istemci oturumunda istemci ana bilgisayar adını tutan arabelleğin boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f26c5-234">**NX_DHCP_CLIENT_HOSTNAME_MAX**: This is size of the buffer for holding the Client host name in the current DHCP Server Client session.</span></span> <span data-ttu-id="f26c5-235">Varsayılan değer 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f26c5-235">The default value is 32.</span></span>