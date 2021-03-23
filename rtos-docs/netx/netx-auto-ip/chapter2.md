---
title: Bölüm 2-Azure RTOS NetX oto 'nin yüklenmesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX için yükleme, kurulum ve kullanımla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 269a3b4e9754fdc19e2cf1482d483fad2b841de9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825612"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-autoip"></a><span data-ttu-id="9bbcd-103">Bölüm 2-Azure RTOS NetX oto 'nin yüklenmesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="9bbcd-103">Chapter 2 - Installation and use of Azure RTOS NetX AutoIP</span></span>

<span data-ttu-id="9bbcd-104">Bu bölümde, Azure RTOS NetX için yükleme, kurulum ve kullanımla ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX AutoIP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="9bbcd-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="9bbcd-105">Product Distribution</span></span>

<span data-ttu-id="9bbcd-106">NetX için Oto IP adresinden kullanılabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="9bbcd-106">AutoIP for NetX is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="9bbcd-107">Bu paket üç kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir PDF dosyası içerir ve aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="9bbcd-107">The package includes three source files, one include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="9bbcd-108">**nx_auto_ip. h**: NETX Oto için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="9bbcd-108">**nx_auto_ip.h**: Header file for NetX AutoIP</span></span>
- <span data-ttu-id="9bbcd-109">**nx_auto_ip. c**: NETX oto Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="9bbcd-109">**nx_auto_ip.c**: C Source file for NetX AutoIP</span></span>
- <span data-ttu-id="9bbcd-110">**demo_netx_auto_ip. c**: NETX Oto IP tanıtımı Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="9bbcd-110">**demo_netx_auto_ip.c**: C Source file for NetX AutoIP Demo</span></span>
- <span data-ttu-id="9bbcd-111">**nx_auto_ip.pdf**: NETX otomatik IP 'nin PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="9bbcd-111">**nx_auto_ip.pdf**: PDF description of NetX AutoIP</span></span>

## <a name="autoip-installation"></a><span data-ttu-id="9bbcd-112">Oto IP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="9bbcd-112">AutoIP Installation</span></span>

<span data-ttu-id="9bbcd-113">NetX oto 'nin kullanılabilmesi için, daha önce bahsedilen tüm dağıtımın, NetX ' in yüklü olduğu dizine kopyalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-113">In order to use NetX AutoIP, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="9bbcd-114">Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_auto_ip. h*, *nx_auto_ip. c* ve *demo_netx_auto_ip. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-114">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_auto_ip.h*, *nx_auto_ip.c*, and *demo_netx_auto_ip.c* files should be copied into this directory.</span></span>

## <a name="using-autoip"></a><span data-ttu-id="9bbcd-115">Oto IP 'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="9bbcd-115">Using AutoIP</span></span>

<span data-ttu-id="9bbcd-116">NetX oto kullanımı kolaydır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-116">Using NetX AutoIP is easy.</span></span> <span data-ttu-id="9bbcd-117">Temel olarak uygulama kodu, ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_auto_ip. h* 'yi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-117">Basically, the application code must include *nx_auto_ip.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span> <span data-ttu-id="9bbcd-118">*Nx_auto_ip. h* eklendikten sonra, uygulama kodu daha sonra bu kılavuzun ilerleyen kısımlarında belirtilen Oto IP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-118">Once *nx_auto_ip.h* is included, the application code is then able to make the AutoIP function calls specified later in this guide.</span></span> <span data-ttu-id="9bbcd-119">Uygulama, yapı işlemine *nx_auto_ip. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-119">The application must also include *nx_auto_ip.c* in the build process.</span></span> <span data-ttu-id="9bbcd-120">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-120">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="9bbcd-121">Bu, NetX Oto IP 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-121">This is all that is required to use NetX AutoIP.</span></span>

> [!NOTE]
> <span data-ttu-id="9bbcd-122">CIP, NetX ARP hizmetlerini kullandığından, bu ARP,, Oto IP kullanılmadan önce *nx_arp_enable* çağrısıyla etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-122">Since AutoIP utilizes NetX ARP services, ARP must be enabled with the *nx_arp_enable* call prior to using AutoIP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="9bbcd-123">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="9bbcd-123">Small Example System</span></span>

<span data-ttu-id="9bbcd-124">NetX oto kullanmanın ne kadar kolay olduğunu gösteren örnek şekil 1,1 ' de aşağıda gösterilen şekilde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-124">An example of how easy it is to use NetX AutoIP is described in Figure 1.1, which appears below.</span></span> <span data-ttu-id="9bbcd-125">Bu örnekte, *nx_auto_ip. h* olan Oto IP içerme dosyası, Line 002 ' de getirilir.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-125">In this example, the AutoIP include file *nx_auto_ip.h* is brought in at line 002.</span></span> <span data-ttu-id="9bbcd-126">Ardından, NetX Oto IP örneği, 090 satırındaki "*tx_application_define*" içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-126">Next, the NetX AutoIP instance is created in "*tx_application_define*" at line 090.</span></span> <span data-ttu-id="9bbcd-127">NetX Oto IP denetim bloğunun "auto_ip_0" daha önce satır 015 adresinde genel bir değişken olarak tanımlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-127">Note that the NetX AutoIP control block "auto_ip_0" was defined previously as a global variable at line 015.</span></span> <span data-ttu-id="9bbcd-128">Başarılı bir şekilde oluşturulduktan sonra, 098. satırda bir NetX oto başlatılır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-128">After successful creation, an NetX AutoIP is started at line 098.</span></span> <span data-ttu-id="9bbcd-129">IP adresi değiştirme geri çağırma işlevi işlemi, sonraki çakışmaları veya olası DHCP adresi çözümlemesini işlemek için kullanılan 105. satırda başlar.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-129">The IP address change callback function processing starts at line 105, which is used to handle subsequent conflicts or possible DHCP address resolution.</span></span>

> [!NOTE]
> <span data-ttu-id="9bbcd-130">Aşağıdaki örnekte konak cihazının tek bilgisayarlı bir cihaz olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-130">The example below assumes the host device is a single-homed device.</span></span> <span data-ttu-id="9bbcd-131">Birden çok sayfalı bir cihaz için, konak uygulama NetX Oto IP hizmetini kullanarak bir IP adresini yoklamanın ikincil ağ arabirimini belirtmek üzere *nx_auto_ip_interface_*.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-131">For a multihomed device, the host application can use the NetX AutoIP service *nx_auto_ip_interface_* set to specify a secondary network interface to probe for an IP address.</span></span> <span data-ttu-id="9bbcd-132">Birden çok ağ bağlantılı uygulamalar ayarlama hakkında daha fazla bilgi için **NETX Kullanıcı kılavuzuna** bakın.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-132">See the **NetX User Guide** for more details on setting up multihomed applications.</span></span> <span data-ttu-id="9bbcd-133">Ana bilgisayar uygulamasının, IP adresi elde ettiğini doğrulamak için NetX API *nx_status_ip_interface_check* kullanması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-133">Note further that the host application should use the NetX API *nx_status_ip_interface_check* to verify AutoIP has obtained an IP address.</span></span>

## <a name="example-of-autoip-use-with-netx"></a><span data-ttu-id="9bbcd-134">NetX ile Oto IP kullanımı örneği</span><span class="sxs-lookup"><span data-stu-id="9bbcd-134">Example of AutoIP use with NetX</span></span>

```c
000 #include "tx_api.h"
001 #include "nx_api.h"
002 #include "nx_auto_ip.h"
003
004 #define         DEMO_STACK_SIZE         4096
005
006 /* Define the ThreadX and NetX object control blocks... */
007
008 TX_THREAD         thread_0;
009 NX_PACKET_POOL    pool_0;
010 NX_IP             ip_0;
011
012
013 /* Define the AUTO IP structures for the IP instance. */
014
015 NX_AUTO_IP         auto_ip_0;
016
017
018 /* Define the counters used in the demo application... */
019
020 ULONG             thread_0_counter;
021 ULONG             address_changes;
022 ULONG             error_counter;
023
024
025 /* Define thread prototypes. */
026
027 void     thread_0_entry(ULONG thread_input);
028 void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
029 void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
030
031
032 /* Define main entry point. */
033
034 int main()
035 {
036
037     /* Enter the ThreadX kernel. */
038     tx_kernel_enter();
039 }
040
041
042 /* Define what the initial system looks like. */
043
044 void     tx_application_define(void *first_unused_memory)
045 {
046
047 CHAR     *pointer;
048 UINT     status;
049
050
051     /* Setup the working pointer. */
052     pointer = (CHAR *) first_unused_memory;
053
054     /* Create the main thread. */
055     tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
056                     pointer, DEMO_STACK_SIZE,
057                     16, 16, 1, TX_AUTO_START);
058
059     pointer = pointer + DEMO_STACK_SIZE;
060
061     /* Initialize the NetX system. */
062     nx_system_initialize();
063
064     /* Create a packet pool. */
065     status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
066                                     pointer, 4096);
067                                     pointer = pointer + 4096;
068
069     if (status)
070         error_counter++;
071
072     /* Create an IP instance. */
073     status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
074                             0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
075                             pointer, 4096, 1);
076                             pointer = pointer + 4096;
077
078     if (status)
079         error_counter++;
080
081     /* Enable ARP and supply ARP cache memory for IP Instance 0. */
082     status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
083     pointer = pointer + 1024;
084
085     /* Check ARP enable status. */
086     if (status)
087         error_counter++;
088
089     /* Create the AutoIP instance for IP Instance 0. */
090     status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
091     pointer = pointer + 4096;
092
093     /* Check AutoIP create status. */
094     if (status)
095         error_counter++;
096
097     /* Start AutoIP instances. */
098     status = nx_auto_ip_start(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);
099
100     /* Check AutoIP start status. */
101     if (status)
102         error_counter++;
103
104     /* Register an IP address change function for IP Instance 0. */
105     status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
106                                         (void *) &auto_ip_0);
107
108     /* Check IP address change notify status. */
109     if (status)
110         error_counter++;
111     }
112
113
114     /* Define the test thread. */
115
116     void thread_0_entry(ULONG thread_input)
117     {
118
119     UINT      status;
120     ULONG     actual_status;
121
122
123          /* Wait for IP address to be resolved. */
124         do
125         {
126
127             /* Call IP status check routine. */
128             status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
129                                         &actual_status, 10000);
130
131         } while (status != NX_SUCCESS);
132
133         /* Since the IP address is resolved at this point, the application
134         can now fully utilize NetX! */
135
136         while(1)
137         {
138
139
140
141             /* Increment thread 0's counter. */
142             thread_0_counter++;
143
144             /* Sleep... */
145             tx_thread_sleep(10);
146         }
147     }
148
149
150     void ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
151     {
152
153     ULONG         ip_address;
154     ULONG         network_mask;
155     NX_AUTO_IP    *auto_ip_ptr;
156
157
158     /* Setup pointer to auto IP instance. */
159     auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;
160
161     /* Pickup the current IP address. */
162     nx_ip_address_get(ip_ptr, &ip_address, &network_mask);
163
164     /* Determine if the IP address has changed back to zero. If so,
165     make sure the AutoIP instance is started. */
166     if (ip_address == 0)
167     {
168
169         /* Get the last AutoIP address for this node. */
170         nx_auto_ip_get_address(auto_ip_ptr, &ip_address);
171
172         /* Start this AutoIP instance. */
173         nx_auto_ip_start(auto_ip_ptr, ip_address);
174     }
175
176     /* Determine if IP address has transitioned to a non local IP address. */
177     else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
178     {
179
180         /* Stop the AutoIP processing. */
181         nx_auto_ip_stop(auto_ip_ptr);
182     }
183
184     /* Increment a counter. */
185     address_changes++;
186 }
```

## <a name="configuration-options"></a><span data-ttu-id="9bbcd-135">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="9bbcd-135">Configuration Options</span></span>

<span data-ttu-id="9bbcd-136">NetX AutoSize oluşturmak için birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-136">There are several configuration options for building NetX AutoIP.</span></span> <span data-ttu-id="9bbcd-137">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9bbcd-137">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="9bbcd-138">**NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel Oto IP hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-138">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic AutoIP error checking.</span></span> <span data-ttu-id="9bbcd-139">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-139">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="9bbcd-140">**NX_AUTO_IP_PROBE_WAIT**: ilk yoklamayı göndermeden önce beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-140">**NX_AUTO_IP_PROBE_WAIT**: The number of seconds to wait before sending first probe.</span></span> <span data-ttu-id="9bbcd-141">Varsayılan olarak, bu değer 1 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-141">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="9bbcd-142">**NX_AUTO_IP_PROBE_NUM**: gönderilen ARP araştırmaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-142">**NX_AUTO_IP_PROBE_NUM**: The number of ARP probes to send.</span></span> <span data-ttu-id="9bbcd-143">Varsayılan olarak, bu değer 3 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-143">By default, this value is defined as 3.</span></span>
- <span data-ttu-id="9bbcd-144">**NX_AUTO_IP_PROBE_MIN**: Gönderen yoklamalar arasında beklenecek saniye sayısı alt sınırı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-144">**NX_AUTO_IP_PROBE_MIN**: The minimum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="9bbcd-145">Varsayılan olarak, bu değer 1 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-145">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="9bbcd-146">**NX_AUTO_IP_PROBE_MAX**: Gönderen yoklamalar arasında beklenecek en fazla saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-146">**NX_AUTO_IP_PROBE_MAX**: The maximum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="9bbcd-147">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-147">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="9bbcd-148">**NX_AUTO_IP_MAX_CONFLICTS**: işleme gecikmelerini arttırmadan önce, tekrar IP çakışmalarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-148">**NX_AUTO_IP_MAX_CONFLICTS**: The number of AutoIP conflicts before increasing processing delays.</span></span> <span data-ttu-id="9bbcd-149">Varsayılan olarak, bu değer 10 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-149">By default, this value is defined as 10.</span></span>
- <span data-ttu-id="9bbcd-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: Toplam çakışma sayısı aşıldığında bekleme süresinin uzaleceği saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: The number of seconds to extend the wait period when the total number of conflicts is exceeded.</span></span> <span data-ttu-id="9bbcd-151">Varsayılan olarak, bu değer 60 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-151">By default, this value is defined as 60.</span></span>
- <span data-ttu-id="9bbcd-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: duyuru gönderilmeden önce beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: The number of seconds to wait before sending announcement.</span></span> <span data-ttu-id="9bbcd-153">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-153">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="9bbcd-154">**NX_AUTO_IP_ANNOUNCE_NUM**: gönderileceği ARP duyurusu sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-154">**NX_AUTO_IP_ANNOUNCE_NUM**: The number of ARP announces to send.</span></span> <span data-ttu-id="9bbcd-155">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-155">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="9bbcd-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: gönderme duyurusu arasında beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: The number of seconds to wait between sending announces.</span></span> <span data-ttu-id="9bbcd-157">Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-157">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="9bbcd-158">**NX_AUTO_IP_DEFEND_INTERVAL**: savunma duyurusu arasında beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-158">**NX_AUTO_IP_DEFEND_INTERVAL**: The number of seconds to wait between defense announces.</span></span> <span data-ttu-id="9bbcd-159">Varsayılan olarak, bu değer 10 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9bbcd-159">By default, this value is defined as 10.</span></span>