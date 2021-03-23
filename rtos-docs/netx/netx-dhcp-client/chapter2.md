---
title: Bölüm 2-Azure RTOS NetX DHCP Istemcisini yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX DHCP istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9224a4df70b8199032066e30108250a3baeb65f5
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826800"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-dhcp-client"></a><span data-ttu-id="f0661-103">Bölüm 2-Azure RTOS NetX DHCP Istemcisini yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="f0661-103">Chapter 2 - Installation and use of Azure RTOS NetX DHCP Client</span></span>

<span data-ttu-id="f0661-104">Bu bölümde, Azure RTOS NetX DHCP bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f0661-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX DHCP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="f0661-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="f0661-105">Product Distribution</span></span>

<span data-ttu-id="f0661-106">NetX için DHCP, adresinde bulunabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="f0661-106">DHCP for NetX is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="f0661-107">Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="f0661-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="f0661-108">**nx_dhcp. h** NetX için DHCP üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="f0661-108">**nx_dhcp.h** Header file for DHCP for NetX</span></span>

- <span data-ttu-id="f0661-109">**nx_dhcp. c** NetX için DHCP için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="f0661-109">**nx_dhcp.c** C Source file for DHCP for NetX</span></span>

- <span data-ttu-id="f0661-110">**nx_dhcp.pdf** NetX için DHCP 'nin PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="f0661-110">**nx_dhcp.pdf** PDF description of DHCP for NetX</span></span>

- <span data-ttu-id="f0661-111">**demo_netx_dhcp. c** NetX DHCP gösterimi</span><span class="sxs-lookup"><span data-stu-id="f0661-111">**demo_netx_dhcp.c** NetX DHCP demonstration</span></span>

- <span data-ttu-id="f0661-112">**demo_netx_multihome_dhcp_client. c** NetX DHCP Istemci, birden çok arabirimde DHCP gösterimi</span><span class="sxs-lookup"><span data-stu-id="f0661-112">**demo_netx_multihome_dhcp_client.c** NetX DHCP Client demonstration of DHCP on multiple interfaces</span></span>

## <a name="dhcp-installation"></a><span data-ttu-id="f0661-113">DHCP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="f0661-113">DHCP Installation</span></span>

<span data-ttu-id="f0661-114">NetX için DHCP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-114">To use DHCP for NetX, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="f0661-115">Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_dhcp. h* ve *nx_dhcp. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-115">For example, if NetX is installed in the directory “*\threadx\arm7\green*” then the *nx_dhcp.h* and *nx_dhcp.c* files should be copied into this directory.</span></span>

## <a name="using-dhcp"></a><span data-ttu-id="f0661-116">DHCP kullanma</span><span class="sxs-lookup"><span data-stu-id="f0661-116">Using DHCP</span></span>

<span data-ttu-id="f0661-117">NetX için DHCP kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="f0661-117">Using DHCP for NetX is easy.</span></span> <span data-ttu-id="f0661-118">Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_dhcp.* h içermelidir.</span><span class="sxs-lookup"><span data-stu-id="f0661-118">Basically, the application code must include *nx_dhcp.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="f0661-119">*Nx_dhcp. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen DHCP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-119">Once *nx_dhcp.h* is included, the application code is then able to make the DHCP function calls specified later in this guide.</span></span> <span data-ttu-id="f0661-120">Uygulama, yapı işlemine *nx_dhcp. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="f0661-120">The application must also include *nx_dhcp.c* in the build process.</span></span> <span data-ttu-id="f0661-121">Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-121">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="f0661-122">Bu, NetX DHCP 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f0661-122">This is all that is required to use NetX DHCP.</span></span>

<span data-ttu-id="f0661-123">DHCP 'nin NetX UDP hizmetlerini kullandığından önce, DHCP kullanmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f0661-123">Note that since DHCP utilizes NetX UDP services, UDP must be enabled with the *nx_udp_enable* call prior to using DHCP.</span></span>

<span data-ttu-id="f0661-124">Daha önce atanmış bir IP adresi almak için DHCP Istemcisi, Istek iletisiyle DHCP işlemini başlatabilir ve "Istenen IP adresi" 50 seçeneğini DHCP sunucusuna alabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-124">To obtain a previously assigned IP address, the DHCP Client can initiate the DHCP process with the Request message and Option 50 “Requested IP Address” to the DHCP Server.</span></span> <span data-ttu-id="f0661-125">DHCP sunucusu, Istemcinin IP adresini veya reddederse bir NACK veriyorsa bir onay iletisiyle yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="f0661-125">The DHCP Server will respond with either an ACK message if it grants the IP address to the Client or a NACK if it refuses.</span></span> <span data-ttu-id="f0661-126">İkinci durumda, DHCP Istemcisi başlangıç durumunda DHCP işlemini bulma iletisi ve istenen IP adresi olmadan yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="f0661-126">In the latter case, the DHCP Client restarts the DHCP process at the Init state with a Discover message and no requested IP address.</span></span> <span data-ttu-id="f0661-127">Ana bilgisayar uygulaması önce DHCP Istemcisini oluşturur, ardından *nx_dhcp_start* ile DHCP işlemini başlatmadan önce istenen IP adresini ayarlamak için *nx_dhcp_request_client_ip* API hizmetini çağırır.</span><span class="sxs-lookup"><span data-stu-id="f0661-127">The host application first creates the DHCP Client, then calls the *nx_dhcp_request_client_ip* API service to set the requested IP address before starting the DHCP process with *nx_dhcp_start*.</span></span> <span data-ttu-id="f0661-128">Daha fazla ayrıntı için bu belgede başka bir yerde örnek bir DHCP uygulaması sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f0661-128">An example DHCP application is provided elsewhere in this document for more details.</span></span>

## <a name="in-the-bound-state"></a><span data-ttu-id="f0661-129">Bağlanma durumunda</span><span class="sxs-lookup"><span data-stu-id="f0661-129">In the Bound State</span></span>

<span data-ttu-id="f0661-130">DHCP istemcisi bağlı durumdayken, DHCP Istemci iş parçacığı, Istemci durumunu Aralık başına bir kez (NX_DHCP_TIME_INTERVAL tarafından belirtildiği gibi) işler ve Istemciye atanan IP kiralamasının kalan süresini azaltır.</span><span class="sxs-lookup"><span data-stu-id="f0661-130">While the DHCP Client is in the bound state, the DHCP Client thread processes the Client state once per interval (as specified by NX_DHCP_TIME_INTERVAL) and decrements the time remaining on the IP lease assigned to the Client.</span></span> <span data-ttu-id="f0661-131">Yenileme süresi geçtiğinde, DHCP Istemci durumu Istemcinin DHCP sunucusundan yenileme isteyeceğini yenıleme durumuna güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-131">When the renewal time has elapsed the DHCP Client state is updated to the RENEW state where the Client will request a renewal from the DHCP Server.</span></span>


## <a name="sending-dhcp-messages-to-the-server"></a><span data-ttu-id="f0661-132">Sunucuya DHCP Iletileri gönderiliyor</span><span class="sxs-lookup"><span data-stu-id="f0661-132">Sending DHCP Messages To The Server</span></span>

<span data-ttu-id="f0661-133">DHCP Istemcisinde, ana bilgisayar uygulamasının DHCP sunucusuna ileti göndermesini sağlayan API hizmetleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f0661-133">The DHCP Client has API services that allow the host application to send a message to the DHCP Server.</span></span> <span data-ttu-id="f0661-134">Not Bu hizmetler, ana bilgisayar uygulamasının, DHCP Istemci iç durumunu güncelleştirmeden önce iletiyi ilk gönderdiklerinden, DHCP Istemci protokolünü el ile çalıştırmasına yönelik DEĞILDIR.</span><span class="sxs-lookup"><span data-stu-id="f0661-134">Note these services are NOT intended for the host application to manually run the DHCP Client protocol as they primarily send the message without necessarily updating the DHCP Client internal state.</span></span>

  - <span data-ttu-id="f0661-135">*nx_dhcp_release*: Bu, ana bilgisayar uygulaması ağdan çıkarken sunucuya bir sürüm iletisi gönderir veya bir IP adresini yeniden gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f0661-135">*nx_dhcp_release*: this sends a RELEASE message to the Server when the host application is either leaving the network or needs relinquish its IP address.</span></span>

  - <span data-ttu-id="f0661-136">*nx_dhcp_decline*: Ana bilgisayar UYGULAMASı, IP adresinin zaten KULLANıMDA olduğunu DHCP istemcisinden bağımsız olarak belirlerse sunucuya bir Red iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f0661-136">*nx_dhcp_decline*: this sends a DECLINE message to the Server if the host application determines independently of the DHCP Client that its IP address is already in use.</span></span>

  - <span data-ttu-id="f0661-137">*nx_dhcp_forcerenew*: Bu, sunucuya bir FORCERENEW iletisi gönderir</span><span class="sxs-lookup"><span data-stu-id="f0661-137">*nx_dhcp_forcerenew*: this sends a FORCERENEW message to the Server</span></span>

  - <span data-ttu-id="f0661-138">*nx_dhcp_send_request*: bu, *nx_dhcp. h*' de belirtildiği gibi bir DHCP ileti türünde bağımsız değişken alır ve iletiyi sunucuya gönderir.</span><span class="sxs-lookup"><span data-stu-id="f0661-138">*nx_dhcp_send_request*: This takes as an argument a DHCP message type, as specified in *nx_dhcp.h*, and sends the message to the Server.</span></span> <span data-ttu-id="f0661-139">Bu, öncelikli olarak DHCP BILDIR iletisini göndermek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f0661-139">This is intended primarily for sending the DHCP INFORM message.</span></span>

<span data-ttu-id="f0661-140">Bu belgenin başka bir yerinde bu hizmetler hakkında daha fazla bilgi için "*DHCP hizmetlerinin açıklaması*" başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="f0661-140">See “*Description of DHCP Services*” for more information about these services elsewhere in this document.</span></span>

## <a name="starting-and-stopping-the-dhcp-client"></a><span data-ttu-id="f0661-141">DHCP Istemcisini başlatma ve durdurma</span><span class="sxs-lookup"><span data-stu-id="f0661-141">Starting and Stopping the DHCP Client</span></span>

<span data-ttu-id="f0661-142">DHCP Istemcisini, bağlantılı bir durum elde etmesinden bağımsız olarak durdurmak için, ana bilgisayar uygulaması *nx_dhcp_stop* çağırır.</span><span class="sxs-lookup"><span data-stu-id="f0661-142">To stop the DHCP Client, regardless if it has achieved a bound state, the host application calls *nx_dhcp_stop*.</span></span>

<span data-ttu-id="f0661-143">Bir DHCP istemcisini yeniden başlatmak için, ana bilgisayar uygulamasının önce yukarıda açıklanan *nx_dhcp_stop* HIZMETINI kullanarak DHCP istemcisini durdurması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0661-143">To restart a DHCP client, the host application must first stop the DHCP Client using the *nx_dhcp_stop* service described above.</span></span> <span data-ttu-id="f0661-144">Daha sonra ana bilgisayar, DHCP Istemcisini sürdürmesini sağlamak için *nx_dhcp_start* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-144">Then the host can call *nx_dhcp_start* to resume the DHCP Client.</span></span> <span data-ttu-id="f0661-145">Ana bilgisayar uygulaması önceki bir DHCP Istemci profilini temizlemenizi istiyorsa (örneğin, başka bir ağdaki önceki bir DHCP sunucusundan elde edilen), ana bilgisayar uygulaması, nx_dhcp_start çağrılmadan önce bu görevi açmak için *nx_dhcp_reinitialize* çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-145">If the host application wishes to clear a previous DHCP Client profile, for example, one obtained from a previous DHCP Server on another network, the host application should call *nx_dhcp_reinitialize* to perform this task internally before calling nx_dhcp_start.</span></span>

<span data-ttu-id="f0661-146">Tipik bir sıra şu olabilir:</span><span class="sxs-lookup"><span data-stu-id="f0661-146">A typical sequence might be:</span></span>

```C
nx_dhcp_stop(&my_dhcp);

nx_dhcp_reinitialize(&my_dhcp);

nx_dhcp_start(&my_dhcp);
```

<span data-ttu-id="f0661-147">Yalnızca tek bir DHCP arabiriminde çalışan DHCP uygulamaları için, DHCP Istemcisi durdurulduğunda DHCP ISTEMCI süreölçeri de etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-147">For DHCP applications running on only a single DHCP interface, stopping the DHCP Client also inactivates the DHCP CLIENT timer.</span></span> <span data-ttu-id="f0661-148">Bu nedenle, artık IP kiralamasının kalan süresini takip tutmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="f0661-148">Thus it is no longer keeping track of the time remaining on the IP lease.</span></span> <span data-ttu-id="f0661-149">Belirli bir arabirimdeki DHCP Istemcisinin durdurulması DHCP Istemci zamanlayıcısını devre dışı vermez, ancak Zamanlayıcı güncelleştirmelerini Bu arabirimdeki IP kirasında kalan süre için durdurur.</span><span class="sxs-lookup"><span data-stu-id="f0661-149">Stopping DHCP Client on a particular interface will not inactivate the DHCP Client timer but will stop timer updates to the time remaining on the IP lease on that interface.</span></span>

<span data-ttu-id="f0661-150">Bu nedenle, ana bilgisayar uygulaması yeniden başlatma veya ağ anahtarlama gerektirmediği takdirde DHCP Istemcisinin durdurulması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="f0661-150">Therefore, stopping the DHCP Client is not advised unless the host application requires rebooting or switching networks.</span></span>

## <a name="using-the-dhcp-client-with-auto-ip"></a><span data-ttu-id="f0661-151">DHCP Istemcisini otomatik IP ile kullanma</span><span class="sxs-lookup"><span data-stu-id="f0661-151">Using the DHCP Client with Auto IP</span></span>

<span data-ttu-id="f0661-152">NetX DHCP Istemcisi, DHCP ve otomatik IP 'nin bir DHCP sunucusunun kullanılabilir veya yanıt verme garantisi olmadığı bir adresi garanti ettiği uygulamalarda otomatik IP protokolüyle aynı anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="f0661-152">The NetX DHCP Client works concurrently with the Auto IP protocol in applications where DHCP and Auto IP guarantee an address where a DHCP Server is not guaranteed to be available or responding.</span></span> <span data-ttu-id="f0661-153">Ancak, ana bilgisayar bir sunucu algılayamazsa veya atanmış bir IP adresi alamazsanız, yerel bir IP adresi için otomatik IP protokolüne geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-153">However, If the host is unable to detect a Server or get an IP address assigned, it can switch to the Auto IP protocol for a local IP address.</span></span> <span data-ttu-id="f0661-154">Ancak bunu yapmadan önce, otomatik IP "araştırma" ve "savunma" aşamaları üzerinden geçtiğinde DHCP Istemcisinin geçici olarak durdurulması önerilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-154">However before doing so, it is advisable to stop the DHCP Client temporarily while Auto IP goes through the “probe” and “defense” stages.</span></span> <span data-ttu-id="f0661-155">Bir otomatik IP adresi konağa atandıktan sonra, DHCP Istemcisi yeniden başlatılabilir ve bir DHCP sunucusu kullanılabilir hale gelirse, ana bilgisayar IP adresi, uygulama çalışırken DHCP sunucusu tarafından sunulan IP adresini kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-155">Once an Auto IP address is assigned to the host, the DHCP Client can be restarted and if a DHCP Server does become available, the host IP address can accept the IP address offered by the DHCP Server while the application is running.</span></span>

<span data-ttu-id="f0661-156">NetX otomatik IP 'si, bir IP adresi değişikliği olayında etkinliklerini izlemek için ana bilgisayar için bir adres değişikliği bildirimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f0661-156">The NetX Auto IP has an address change notification for the host to monitor its activities in the event of an IP address change.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="f0661-157">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="f0661-157">Small Example System</span></span>

<span data-ttu-id="f0661-158">Aşağıdaki şekil 1,1 ' de NetX 'in nasıl kullanıldığını gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="f0661-158">An example of how use NetX is described in Figure 1.1 below.</span></span> <span data-ttu-id="f0661-159">DHCP Istemcisi, 101 satırındaki "*my_thread_entry*" oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f0661-159">The DHCP Client is created “*my_thread_entry*” at line 101.</span></span> <span data-ttu-id="f0661-160">Başarılı oluşturulduktan sonra DHCP işlemi, 108 satırındaki *nx_dhcp_start* çağrısında başlatılır.</span><span class="sxs-lookup"><span data-stu-id="f0661-160">After successful creation, the DHCP process is initiated at the call to *nx_dhcp_start* at line 108.</span></span> <span data-ttu-id="f0661-161">Bu noktada DHCP Istemci girişimleri DHCP sunucusuyla iletişim kurmak için başlatılır.</span><span class="sxs-lookup"><span data-stu-id="f0661-161">At this point the DHCP Client attempts are initiated to contact the DHCP server.</span></span> <span data-ttu-id="f0661-162">Bu işlem sırasında, uygulama kodu 95 satırından başlayarak *nx_ip_status_check* hizmeti (veya ikincil bir arabirim için *NX_IP_INTERFACE_STATUS_CHECK* ) kullanılarak IP örneğine geçerli bir IP adresinin kaydedilmesini bekler.</span><span class="sxs-lookup"><span data-stu-id="f0661-162">During this process, the application code waits for a valid IP address to be registered with the IP instance using the *nx_ip_status_check* service (or *nx_ip_interface_status_check* for a secondary interface) starting at line 95.</span></span> <span data-ttu-id="f0661-163">Bu, daha kısa bir bekleme seçeneğiyle bir döngüde daha yaygın olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="f0661-163">This is more commonly done in a loop with a shorter wait option.</span></span>

<span data-ttu-id="f0661-164">Satır 127 ' den sonra DHCP geçerli bir IP adresi aldıktan sonra, NetX TCP/IP hizmetlerinden yararlanarak istediğiniz gibi uygulama devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-164">After line 127, DHCP has received a valid IP address and the application can then proceed, utilizing NetX TCP/IP services as desired.</span></span>

```C
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nx_dhcp.h"

#define   DEMO_STACK_SIZE     4096
TX_THREAD        my_thread;
NX_PACKET_POOL     my_pool;
NX_IP          my_ip;
NX_DHCP         my_dhcp;

/* Define function prototypes. */

void  my_thread_entry(ULONG thread_input);
void  my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

  /* Enter the ThreadX kernel. */
  tx_kernel_enter();
}


/* Define what the initial system looks like. */

void  tx_application_define(void *first_unused_memory)
{

CHAR  *pointer;
UINT  status;

  
  /* Setup the working pointer. */
  pointer = (CHAR *) first_unused_memory;

  /* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0, 
            pointer, DEMO_STACK_SIZE, 
            2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Initialize the NetX system. */
  nx_system_initialize();

  /* Create a packet pool. */
  status = nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                     1024, pointer, 64000);
  pointer = pointer + 64000;

  /* Check for pool creation error. */
  if (status)
    error_counter++;

  /* Create an IP instance without an IP address. */
  status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
      0xFFFFFF00, &my_pool, my_netx_driver, pointer, 
      DEMO_STACK_SIZE, 1);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Check for IP create errors. */
  if (status)
    error_counter++;

  /* Enable ARP and supply ARP cache memory for my IP Instance. */
  status = nx_arp_enable(&my_ip, (void *) pointer, 1024);
  pointer = pointer + 1024;

  /* Check for ARP enable errors. */
  if (status)
    error_counter++;

  /* Enable UDP. */
  status = nx_udp_enable(&my_ip);
  if (status)
    error_counter++;
}


/* Define my thread. */

void  my_thread_entry(ULONG thread_input)
{

UINT    status;
ULONG    actual_status;
NX_PACKET  *my_packet;

  /* Wait for the link to come up. */
  do
  {

    /* Get the link status. */
    status = nx_ip_status_check(&my_ip, NX_IP_LINK_ENABLED, 
                            &actual_status, 100);

  } while (status != NX_SUCCESS);

  /* Create a DHCP instance. */
  status = nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

  /* Check for DHCP create error. */
  if (status)
    error_counter++;

  /* Start DHCP. */
  nx_dhcp_start(&my_dhcp);

  /* Check for DHCP start error. */
  if (status)
    error_counter++;

  /* Wait for IP address to be resolved through DHCP. */
  nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                        (ULONG *) &status, 100000);

  /* Check to see if we have a valid IP address. */
  if (status)
  {
    error_counter++;
    return;
  }
  else
  {

        /* Yes, a valid IP address is now on lease… All NetX
      services are available.
  }
}
```

<span data-ttu-id="f0661-165">Şekil 1,1 NetX ile DHCP kullanımı örneği</span><span class="sxs-lookup"><span data-stu-id="f0661-165">Figure 1.1 Example of DHCP use with NetX</span></span>

## <a name="multi-server-environments"></a><span data-ttu-id="f0661-166">Çoklu sunucu ortamları</span><span class="sxs-lookup"><span data-stu-id="f0661-166">Multi-Server Environments</span></span>

<span data-ttu-id="f0661-167">Birden çok DHCP sunucusunun bulunduğu ağlarda, DHCP Istemcisi, ilk alınan DHCP sunucusu teklif iletisini kabul eder, Istek durumuna ilerler ve diğer alınan teklifleri yoksayar.</span><span class="sxs-lookup"><span data-stu-id="f0661-167">On networks where there is more than one DHCP Server, the DHCP Client accepts the first received DHCP Server Offer message, advances to the Request state, and ignores any other received offers.</span></span>

## <a name="arp-probes"></a><span data-ttu-id="f0661-168">ARP araştırmaları</span><span class="sxs-lookup"><span data-stu-id="f0661-168">ARP Probes</span></span>

<span data-ttu-id="f0661-169">DHCP Istemcisi, IP adresinin zaten kullanımda olmadığından emin olmak için DHCP sunucusundan IP adresi atamasından sonra bir veya daha fazla ARP araştırmaları gönderecek şekilde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-169">The DHCP Client can be configured to send one or more ARP probes after IP address assignment from the DHCP Server to verify the IP address is not already in use.</span></span> <span data-ttu-id="f0661-170">ARP araştırma adımı, RFC 2131 tarafından önerilir ve özellikle birden fazla DHCP sunucusuna sahip ortamlarda önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f0661-170">The ARP probe step is recommended by RFC 2131 and is particularly important in environments with more than one DHCP Server.</span></span> <span data-ttu-id="f0661-171">Ana bilgisayar uygulaması NX_DHCP_CLIENT_SEND_ARP_PROBE seçeneğini etkinleştirmesine izin verirseniz (ek ARP araştırma seçenekleri için bölümdeki **yapılandırma seçeneklerine** bakın), DHCP istemcisi ' kendine adreslenen ' bir ARP araştırması gönderir ve yanıt için belirtilen zamanı bekler.</span><span class="sxs-lookup"><span data-stu-id="f0661-171">If the host application enables the NX_DHCP_CLIENT_SEND_ARP_PROBE option (see **Configuration Options** in Chapter Two for additional ARP probe options), the DHCP Client will send a ‘self addressed’ ARP probe and wait for the specified time for a response.</span></span> <span data-ttu-id="f0661-172">Hiçbiri alınmazsa, DHCP Istemcisi, bağlantılı duruma ilerletir.</span><span class="sxs-lookup"><span data-stu-id="f0661-172">If none is received, the DHCP Client advances to the Bound state.</span></span> <span data-ttu-id="f0661-173">Yanıt alınmışsa, DHCP Istemcisi adresin zaten kullanımda olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="f0661-173">If a response is received, the DHCP Client assumes the address is already in use.</span></span> <span data-ttu-id="f0661-174">Otomatik olarak sunucuya bir reddetme iletisi gönderir ve Istemciyi yeniden başlatarak başlangıç durumundan DHCP araştırmalarını yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="f0661-174">It automatically sends a DECLINE message to the Server, and reinitializes the Client to restart the DHCP probes again from the INIT state.</span></span> <span data-ttu-id="f0661-175">Bu, DHCP durum makinesini yeniden başlatır ve Istemci sunucuya başka bir bulma iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f0661-175">This restarts the DHCP state machine and the Client sends another DISCOVER message to the Server.</span></span>

## <a name="bootp-protocol"></a><span data-ttu-id="f0661-176">BOOTP Protokolü</span><span class="sxs-lookup"><span data-stu-id="f0661-176">BOOTP Protocol</span></span>

<span data-ttu-id="f0661-177">DHCP Istemcisi Ayrıca, BOOTP protokolünü de destekler.</span><span class="sxs-lookup"><span data-stu-id="f0661-177">The DHCP Client also supports the BOOTP protocol as well the DHCP protocol.</span></span> <span data-ttu-id="f0661-178">Bu seçeneği etkinleştirmek ve DHCP yerine BOOTP 'yi kullanmak için, ana bilgisayar uygulamasının NX_DHCP_BOOTP_ENABLE yapılandırma seçeneğini ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0661-178">To enable this option and use BOOTP instead of DHCP, the host application must set the NX_DHCP_BOOTP_ENABLE configuration option.</span></span> <span data-ttu-id="f0661-179">Ana bilgisayar uygulaması, BOOTP protokolünde belirli IP adresleri talep edebilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-179">The host application can still request specific IP addresses in the BOOTP protocol.</span></span> <span data-ttu-id="f0661-180">Ancak, DHCP Istemcisi, bazı durumlarda BOOTP olarak kullanılmak üzere ana bilgisayar işletim sisteminin yüklenmesini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="f0661-180">However, the DHCP Client does not support loading the host operating system as BOOTP is sometimes used to do.</span></span>

## <a name="dhcp-on-a-secondary-interface"></a><span data-ttu-id="f0661-181">Ikincil bir arabirimde DHCP</span><span class="sxs-lookup"><span data-stu-id="f0661-181">DHCP on a Secondary Interface</span></span>

<span data-ttu-id="f0661-182">NetX DHCP Istemcisi, varsayılan birincil arabirim yerine ikincil arabirimlerde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-182">The NetX DHCP Client can run on secondary interfaces rather than the default primary interface.</span></span>

<span data-ttu-id="f0661-183">NetX DHCP Istemcisini ikincil bir ağ arabiriminde çalıştırmak için, konak uygulamanın, *nx_dhcp_set_interface_index* API HIZMETINI kullanarak DHCP istemcisinin arabirim dizinini ikincil arabirime ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0661-183">To run NetX DHCP Client on a secondary network interface, the host application must set the interface index of the DHCP Client to the secondary interface using the *nx_dhcp_set_interface_index* API service.</span></span> <span data-ttu-id="f0661-184">Arabirimin, *nx_ip_interface_attach* hizmeti kullanılarak birincil ağ arabirimine zaten eklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0661-184">The interface must already be attached to the primary network interface using the *nx_ip_interface_attach* service.</span></span> <span data-ttu-id="f0661-185">İkincil arabirimler ekleme hakkında daha fazla bilgi için bkz. NetX Kullanıcı Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="f0661-185">See the NetX User Guide for more details on attaching secondary interfaces.</span></span>

<span data-ttu-id="f0661-186">Şekil 1,2 ' de aşağıda, ana bilgisayar uygulamasının ikincil arabirimindeki DHCP sunucusuna bağlandığı örnek bir sistem bulunur.</span><span class="sxs-lookup"><span data-stu-id="f0661-186">Below in Figure 1.2 is an example system on which the host application connects to the DHCP server on its secondary interface.</span></span> <span data-ttu-id="f0661-187">Satır 65 ' de, ikincil arabirim IP görevine null bir IP adresi ile iliştirilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-187">On line 65, the secondary interface is attached to the IP task with a null IP address.</span></span> <span data-ttu-id="f0661-188">Satır 104 ' de, DHCP Istemci örneği oluşturulduktan sonra, *nx_dhcp_set_interface_index* çağırarak DHCP istemci arabirimi dizini 1 olarak ayarlanır (örneğin, birincil arabirimden kendisi dizin 0 ' dır).</span><span class="sxs-lookup"><span data-stu-id="f0661-188">On line 104, after the DHCP Client instance is created, the DHCP Client interface index is set to 1 (e.g. the offset from the primary interface which itself is index 0) by calling *nx_dhcp_set_interface_index*.</span></span> <span data-ttu-id="f0661-189">Ardından, DHCP Istemcisi, 108. satırda başlamaya hazırlanmaya başlamıştır.</span><span class="sxs-lookup"><span data-stu-id="f0661-189">Then the DHCP Client is ready to be started in line 108.</span></span>

```C
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nx_dhcp.h"

#define   DEMO_STACK_SIZE     4096
TX_THREAD        my_thread;
NX_PACKET_POOL     my_pool;
NX_IP          my_ip;
NX_DHCP         my_dhcp;

/* Define function prototypes. */

void  my_thread_entry(ULONG thread_input);
void  my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

  /* Enter the ThreadX kernel. */
  tx_kernel_enter();
}


/* Define what the initial system looks like. */

void  tx_application_define(void *first_unused_memory)
{

CHAR  *pointer;
UINT  status;

  
  /* Setup the working pointer. */
  pointer = (CHAR *) first_unused_memory;

  /* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0, 
            pointer, DEMO_STACK_SIZE, 
            2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Initialize the NetX system. */
  nx_system_initialize();

  /* Create a packet pool. */
  status = nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                     1024, pointer, 64000);
  pointer = pointer + 64000;

  /* Check for pool creation error. */
  if (status)
    error_counter++;

  /* Create an IP instance without an IP address. */
  status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
       0xFFFFFF00, &my_pool, my_netx_driver, pointer, STACK_SIZE, 1);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Check for IP create errors. */
  if (status)
    error_counter++;

  status = _nx_ip_interface_attach(&ip_0, "port_2", IP_ADDRESS(0, 0, 0,0), 
                            0xFFFFFF00UL, my_netx_driver);
                            
  /* Enable ARP and supply ARP cache memory for my IP Instance. */
  status = nx_arp_enable(&my_ip, (void *) pointer, 1024);
  pointer = pointer + 1024;

  /* Check for ARP enable errors. */
  if (status)
    error_counter++;

  /* Enable UDP. */
  status = nx_udp_enable(&my_ip);
  if (status)
    error_counter++;
}


void  my_thread_entry(ULONG thread_input)
{

UINT    status;
ULONG    status;
NX_PACKET  *my_packet;

  /* Wait for the link to come up. */
  do
  {

    /* Get the link status. */
    status = nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,& status,100);
  } while (status != NX_SUCCESS);

  /* Create a DHCP instance. */
  status = nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

  /* Check for DHCP create error. */
  if (status)
    error_counter++;

  /* Set the DHCP client interface to the secondary interface. 
    status = nx_dhcp_set_interface_index(&my_dhcp, 1);


  /* Start DHCP. */
  nx_dhcp_start(&my_dhcp);

  /* Check for DHCP start error. */
  if (status)
    error_counter++;

  /* Wait for IP address to be resolved through DHCP. */
  nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                        (ULONG *) &status, 100000);

  /* Check to see if we have a valid IP address. */
  if (status)
  {
    error_counter++;
    return;
  }
  else
  {

        /* Yes, a valid IP address is now on lease… All NetX
      services are available.
  }
}
```

<span data-ttu-id="f0661-190">Şekil 1,2 multihome desteğiyle NetX için DHCP örneği</span><span class="sxs-lookup"><span data-stu-id="f0661-190">Figure 1.2 Example of DHCP for NetX with multihome support</span></span>

## <a name="dhcp-client-on-multiple-interfaces-simultaneously"></a><span data-ttu-id="f0661-191">Aynı anda birden çok arabirimde DHCP Istemcisi</span><span class="sxs-lookup"><span data-stu-id="f0661-191">DHCP Client on Multiple Interfaces Simultaneously</span></span>

<span data-ttu-id="f0661-192">DHCP Istemcisini birden çok arabirimde çalıştırmak için, *nx_api. h* içindeki NX_MAX_PHYSICAL_INTERFACES, cihaza bağlı olan fiziksel arabirimlerin sayısına ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-192">To run DHCP Client on multiple interfaces, NX_MAX_PHYSICAL_INTERFACES in *nx_api.h* must be set to the number of physical interfaces connected to the device.</span></span> <span data-ttu-id="f0661-193">Varsayılan olarak, bu değer 1 ' dir (örn. birincil arabirim).</span><span class="sxs-lookup"><span data-stu-id="f0661-193">By default, this value is 1 (e.g. the primary interface).</span></span> <span data-ttu-id="f0661-194">IP örneğine ek bir arabirim kaydetmek için *nx_ip_interface_attach* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0661-194">To register an additional interface to the IP instance use the *nx_ip_interface_attach* service.</span></span> <span data-ttu-id="f0661-195">İkincil arabirimler ekleme hakkında daha fazla bilgi için bkz. NetX Kullanıcı Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="f0661-195">See the NetX User Guide for more details on attaching secondary interfaces.</span></span>

<span data-ttu-id="f0661-196">Sonraki adım, *nx_dhcp. h* IÇINDEKI NX_DHCP_CLIENT_MAX_RECORDS DHCP 'yi aynı anda çalıştırmak için beklenen en fazla arabirim sayısına ayarlamaya yönelik olur.</span><span class="sxs-lookup"><span data-stu-id="f0661-196">The next step is to set the NX_DHCP_CLIENT_MAX_RECORDS in *nx_dhcp.h* to the maximum number of interfaces expected to run DHCP simultaneously.</span></span> <span data-ttu-id="f0661-197">NX_DHCP_CLIENT_MAX_RECORDS NX_MAX_PHYSICAL_INTERFACES eşit olması gerekmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f0661-197">Note that NX_DHCP_CLIENT_MAX_RECORDS does not have to equal NX_MAX_PHYSICAL_INTERFACES.</span></span> <span data-ttu-id="f0661-198">Örneğin, NX_MAX_PHYSICAL_INTERFACES 3 ve NX_DHCP_CLIENT_MAX_RECORDS 2 ' ye eşit olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-198">For example, NX_MAX_PHYSICAL_INTERFACES can be 3 and NX_DHCP_CLIENT_MAX_RECORDS equal to 2.</span></span> <span data-ttu-id="f0661-199">Bu yapılandırmada, yalnızca iki arabirim (ve herhangi bir zamanda üç fiziksel arabirimden herhangi biri olabilir), herhangi bir anda DHCP 'yi çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-199">In this configuration, only two interfaces (and they can be any two of the three physical interfaces at any time) of the three physical interfaces can run DHCP at any one time.</span></span> <span data-ttu-id="f0661-200">DHCP Istemci kayıtları, ağ arabirimlerine bire bir eşleme içermez, örneğin, Istemci kaydı 1 fiziksel arabirim dizini 1 ile otomatik olarak bağıntılı değildir.</span><span class="sxs-lookup"><span data-stu-id="f0661-200">DHCP Client Records do not have a one to one mapping to network interfaces e.g. Client Record 1 does not automatically correlate to physical interface index 1.</span></span>

<span data-ttu-id="f0661-201">NX_DHCP_CLIENT_MAX_RECORDS Ayrıca, NX_MAX_PHYSICAL_INTERFACES daha büyük olarak ayarlanabilir ancak bu, kullanılmayan istemci kayıtları oluşturur ve belleğin verimsiz bir şekilde kullanılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-201">NX_DHCP_CLIENT_MAX_RECORDS can also be set to greater than NX_MAX_PHYSICAL_INTERFACES but this would create unused client records and be an inefficient use of memory.</span></span>

<span data-ttu-id="f0661-202">Herhangi bir arabirimde DHCP 'yi başlatabilmeniz için, uygulamanın *nx_dhcp_interface_enable* çağırarak bu arabirimleri etkinleştirmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0661-202">Before it can start DHCP on any interface, the application must enable those interfaces by calling *nx_dhcp_interface_enable*.</span></span> <span data-ttu-id="f0661-203">Özel durumun, *nx_dhcp_create* çağrısında otomatik olarak etkinleştirilen (ve aşağıda açıklanan *nx_dhcp_interface_disable* hizmeti kullanılarak devre dışı bırakılabilen) birincil arabirim olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f0661-203">Note that the exception is the primary interface which is automatically enabled in the *nx_dhcp_create* call (and which can be disabled using the *nx_dhcp_interface_disable* service discussed below).</span></span>

<span data-ttu-id="f0661-204">Herhangi bir zamanda, bir arabirim DHCP için devre dışı bırakılabilir ve bu arabirimde DHCP çalıştıran diğer arabirimlerden bağımsız olarak durulabilirler.</span><span class="sxs-lookup"><span data-stu-id="f0661-204">At any time, an interface can be disabled for DHCP or DHCP can be stopped on that interface independently of other interfaces running DHCP.</span></span>

<span data-ttu-id="f0661-205">Yukarıda belirtildiği gibi, DHCP için belirli bir arabirimi etkinleştirmek üzere *nx_dhcp_interface_enable* hizmetini kullanın ve giriş bağımsız değişkeninde fiziksel arabirim dizinini belirtin.</span><span class="sxs-lookup"><span data-stu-id="f0661-205">As mentioned above, to enable a specific interface for DHCP, use the *nx_dhcp_interface_enable* service and specify the physical interface index in the input argument.</span></span> <span data-ttu-id="f0661-206">NX_DHCP_CLIENT_MAX_RECORDS arabirimlerin tümü, arabirim dizini giriş bağımsız değişkeninin NX_MAX_PHYSICAL_INTERFACES daha az olduğu sınırlamasıyla etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-206">Up to NX_DHCP_CLIENT_MAX_RECORDS interfaces can be enabled with the only limitation that the interface index input argument be less than NX_MAX_PHYSICAL_INTERFACES.</span></span>

<span data-ttu-id="f0661-207">Belirli bir arabirimde DHCP 'yi başlatmak için *nx_dhcp_interface_start* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0661-207">To start DHCP on a specific interface, use the *nx_dhcp_interface_start* service.</span></span> <span data-ttu-id="f0661-208">Tüm etkin arabirimlerde DHCP 'yi başlatmak için *nx_dhcp_start* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0661-208">To start DHCP on all enabled interfaces, use the *nx_dhcp_start* service.</span></span> <span data-ttu-id="f0661-209">(DHCP 'yi zaten Başlatan arabirimler *nx_dhcp_start* bundan etkilenmeyecektir.)</span><span class="sxs-lookup"><span data-stu-id="f0661-209">(Interfaces that have already started DHCP will not be affected by *nx_dhcp_start*.)</span></span>

<span data-ttu-id="f0661-210">Bir arabirimdeki DHCP 'yi durdurmak için *nx_dhcp_interface_stop* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0661-210">To stop DHCP on an interface, use the *nx_dhcp_interface_stop* service.</span></span> <span data-ttu-id="f0661-211">DHCP, bu arabirim üzerinde zaten başlatılmış olmalıdır veya bir hata durumu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f0661-211">DHCP must already have started on that interface or an error status is returned.</span></span> <span data-ttu-id="f0661-212">Tüm etkinleştirilen arabirimlerde DHCP 'yi durdurmak için *nx_dhcp_stop* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0661-212">To stop DHCP on all enabled interfaces, use the *nx_dhcp_stop* service.</span></span> <span data-ttu-id="f0661-213">DHCP, diğer arabirimlerden bağımsız olarak herhangi bir zamanda durdurulabilir.</span><span class="sxs-lookup"><span data-stu-id="f0661-213">DHCP can be stopped independently of other interfaces at any time.</span></span>

<span data-ttu-id="f0661-214">Var olan DHCP Istemci hizmetlerinin çoğu bir ' interface ' eşdeğerine sahiptir. *nx_dhcp_interface_release* , arabirime özgü *nx_dhcp_release eşdeğerdir.*</span><span class="sxs-lookup"><span data-stu-id="f0661-214">Most of the existing DHCP Client services have an ‘interface’ equivalent e.g. *nx_dhcp_interface_release* is the interface specific equivalent of *nx_dhcp_release.*</span></span> <span data-ttu-id="f0661-215">DHCP Istemcisi tek bir arabirim için yapılandırılmışsa, aynı eylemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f0661-215">If DHCP Client is configured for a single interface, they perform the same action.</span></span>

<span data-ttu-id="f0661-216">Arabirime özgü olmayan DHCP Istemci hizmetlerinin tipik olarak tüm arabirimlere uygulanacağını, ancak tümünün değil olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f0661-216">Note that non-interface specific DHCP Client services typically apply to all interfaces but not all.</span></span> <span data-ttu-id="f0661-217">İkinci durumda, arabirime özgü olmayan hizmet, arabirim kayıtlarının DHCP Istemci listesinde arama sırasında bulunan ilk DHCP etkin arabirimi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f0661-217">In the latter case, the non-interface specific service applies to the first DHCP enabled interface found in searching the DHCP Client list of interface records.</span></span> <span data-ttu-id="f0661-218">DHCP için birden çok arabirim etkinleştirildiğinde arabirim temelli olmayan bir hizmetin nasıl gerçekleştirildiğinden ilgili üçüncü bölümde bulunan **hizmetlerin açıklamasına** bakın.</span><span class="sxs-lookup"><span data-stu-id="f0661-218">See **Description of Services** in Chapter Three for how a non-interface specific service performs when multiple interfaces are enabled for DHCP.</span></span>

<span data-ttu-id="f0661-219">Aşağıdaki örnek dizide, IP örneğinin iki ağ arabirimi vardır ve ilk olarak ikincil arabirimde DHCP 'yi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f0661-219">In the example sequence below, the IP instance has two network interfaces and first runs DHCP on the secondary interface.</span></span> <span data-ttu-id="f0661-220">Daha sonra bir süre sonra, birincil arabirimde DHCP başlatılır.</span><span class="sxs-lookup"><span data-stu-id="f0661-220">At some time later, it starts DHCP on the primary interface.</span></span> <span data-ttu-id="f0661-221">Ardından birincil arabirimdeki IP adresini serbest bırakır ve birincil arabirimde DHCP 'yi yeniden başlatır:</span><span class="sxs-lookup"><span data-stu-id="f0661-221">Then it releases the IP address on the primary interface and restarts DHCP on the primary interface:</span></span>

```C
nx_dhcp_create(&my_dhcp_client);
/* By default this enables primary interface for DHCP. */

nx_dhcp_interface_enable(&my_dhcp_client, 1); 
/* Secondary interface is enabled. */

nx_dhcp_interface_start(&my_dhcp_client, 1); 
/* DHCP is started on secondary interface. */

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); 
/* DHCP is started on primary interface. */

nx_dhcp_interface_release(&my_dhcp_client, 0); 

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); 
/* DHCP is restarted on primary interface. */
```

<span data-ttu-id="f0661-222">Arabirime özgü hizmetlerin tüm listesi için, Bölüm üçünde **hizmetlerin açıklamasına** bakın.</span><span class="sxs-lookup"><span data-stu-id="f0661-222">For a complete list of interface specific services see **Description of Services** in Chapter Three.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="f0661-223">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f0661-223">Configuration Options</span></span>

<span data-ttu-id="f0661-224">*Nx_dhcp. h* içindeki kullanıcı yapılandırılabilir DHCP seçenekleri, ana bilgisayar uygulamasının belirli GEREKSINIMLERI Için DHCP istemcisini ince olarak değiştirmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f0661-224">User configurable DHCP options in *nx_dhcp.h* allow the host application to fine tune DHCP Client for its particular requirements.</span></span> <span data-ttu-id="f0661-225">Bu parametrelerin listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f0661-225">The following is a list of these parameters:</span></span>  
  
- <span data-ttu-id="f0661-226">**NX_DHCP_ENABLE_BOOTP** Tanımlı, bu seçenek DHCP yerine BOOTP protokolünü sunar.</span><span class="sxs-lookup"><span data-stu-id="f0661-226">**NX_DHCP_ENABLE_BOOTP** Defined, this option enables the BOOTP protocol instead of DHCP.</span></span> <span data-ttu-id="f0661-227">Varsayılan olarak bu seçenek devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-227">By default this option is disabled.</span></span>

- <span data-ttu-id="f0661-228">**NX_DHCP_CLIENT_RESTORE_STATE** Bu, tanımlanmazsa, DHCP Istemcisinin, kira üzerinde kalan süre dahil olmak üzere geçerli DHCP Istemci lisansını kaydetmesine ve bu durumu DHCP Istemci uygulaması yeniden başlatmalar arasında geri yüklemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-228">**NX_DHCP_CLIENT_RESTORE_STATE** If defined, this enables the DHCP Client to save its current DHCP Client license ‘state’ including time remaining on the lease, and restore this state between DHCP Client application reboots.</span></span> <span data-ttu-id="f0661-229">Varsayılan değer devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-229">The default value is disabled.</span></span>

- <span data-ttu-id="f0661-230">**NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL** Ayarlanırsa, DHCP Istemcisi kendi paket havuzunu oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="f0661-230">**NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL** If set, the DHCP Client will not create its own packet pool.</span></span> <span data-ttu-id="f0661-231">Ana bilgisayar uygulamasının, DHCP Istemci paket havuzunu ayarlamak için nx_dhcp_packet_pool_set hizmetini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0661-231">The host application must use the nx_dhcp_packet_pool_set service to set the DHCP Client packet pool.</span></span> <span data-ttu-id="f0661-232">Varsayılan değer devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-232">The default value is disabled.</span></span>

- <span data-ttu-id="f0661-233">**NX_DHCP_CLIENT_SEND_ARP_PROBE** Bu, DHCP Istemcisinin atanmış DHCP adresinin başka bir konağa ait olmadığından emin olmak için IP adresi atamasından sonra bir ARP araştırması göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-233">**NX_DHCP_CLIENT_SEND_ARP_PROBE** Defined, this enables the DHCP Client to send an ARP probe after IP address assignment to verify the assigned DHCP address is not owned by another host.</span></span> <span data-ttu-id="f0661-234">Varsayılan olarak, bu seçenek devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-234">By default, this option is disabled.</span></span>

- <span data-ttu-id="f0661-235">**NX_DHCP_ARP_PROBE_WAIT** Bir ARP araştırması gönderdikten sonra DHCP Istemcisinin yanıt beklediği sürenin uzunluğunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-235">**NX_DHCP_ARP_PROBE_WAIT** Defines the length of time the DHCP Client waits for a response after sending an ARP probe.</span></span> <span data-ttu-id="f0661-236">Varsayılan değer bir saniye (1 \* NX_IP_PERIODIC_RATE)</span><span class="sxs-lookup"><span data-stu-id="f0661-236">The default value is one second (1 \* NX_IP_PERIODIC_RATE)</span></span>

- <span data-ttu-id="f0661-237">**NX_DHCP_ARP_PROBE_MIN** ARP araştırmaları gönderme arasındaki aralıkta bulunan en küçük çeşitlemesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-237">**NX_DHCP_ARP_PROBE_MIN** Defines the minimum variation in the interval between sending ARP probes.</span></span> <span data-ttu-id="f0661-238">Değer 1 saniye olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-238">The value is defaulted to 1 second.</span></span>

- <span data-ttu-id="f0661-239">**NX_DHCP_ARP_PROBE_MAX** ARP araştırmaları gönderme arasındaki aralıktaki en yüksek çeşitleme tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-239">**NX_DHCP_ARP_PROBE_MAX** Defines the maximum variation in the interval between sending ARP probes.</span></span> <span data-ttu-id="f0661-240">Değer 2 saniyeye varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-240">The value is defaulted to 2 seconds.</span></span>

- <span data-ttu-id="f0661-241">**NX_DHCP_ARP_PROBE_NUM** DHCP sunucusu tarafından atanan IP adresinin zaten kullanımda olup olmadığını belirlemek için gönderilen ARP araştırmaları sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-241">**NX_DHCP_ARP_PROBE_NUM** Defines the number of ARP probes sent for determining if the IP address assigned by the DHCP server is already in use.</span></span> <span data-ttu-id="f0661-242">Değer 3 yoklamalara göre varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-242">The value is defaulted to 3 probes.</span></span>

- <span data-ttu-id="f0661-243">**NX_DHCP_RESTART_WAIT** DHCP istemcisine atanan IP adresi zaten kullanımda ise DHCP Istemcisinin DHCP 'yi yeniden başlatması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-243">**NX_DHCP_RESTART_WAIT** Defines the length of time the DHCP Client waits to restart DHCP if the IP address assigned to the DHCP Client is already in use.</span></span> <span data-ttu-id="f0661-244">Değer, varsayılan olarak 10 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="f0661-244">The value is defaulted to 10 seconds.</span></span>

- <span data-ttu-id="f0661-245">**NX_DHCP_CLIENT_MAX_RECORDS** DHCP Istemci örneğine kaydedilecek en fazla arabirim kaydı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-245">**NX_DHCP_CLIENT_MAX_RECORDS** Specifies the maximum number of interface records to save to the DHCP Client instance.</span></span> <span data-ttu-id="f0661-246">DHCP Istemci arabirimi kaydı, belirli bir arabirim üzerinde çalışan DHCP Istemcisinin kaydıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-246">A DHCP Client interface record is a record of the DHCP Client running on a specific interface.</span></span> <span data-ttu-id="f0661-247">Varsayılan değer, fiziksel arabirimlerin sayısı (NX_MAX_PHYSICAL_INTERFACES) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-247">The default value is set as physical interfaces count(NX_MAX_PHYSICAL_INTERFACES).</span></span>

- <span data-ttu-id="f0661-248">**NX_DHCP_CLIENT_SEND_MAX_DHCP_MESSAGE_OPTION** Bu, DHCP Istemcisinin en fazla DHCP ileti boyutu seçeneğini göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-248">**NX_DHCP_CLIENT_SEND_MAX_DHCP_MESSAGE_OPTION** Defined, this enables the DHCP Client to send maximum DHCP message size option.</span></span> <span data-ttu-id="f0661-249">Varsayılan olarak, bu seçenek devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-249">By default, this option is disabled.</span></span>

- <span data-ttu-id="f0661-250">**NX_DHCP_CLIENT_ENABLE_HOST_NAME_CHECK** Bu, DHCP Istemcisinin, nx_dhcp_create çağrısındaki giriş ana bilgisayar adını geçersiz karakterler veya uzunlukla denetlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-250">**NX_DHCP_CLIENT_ENABLE_HOST_NAME_CHECK** Defined, this enables the DHCP Client to check the input host name in the nx_dhcp_create call for invalid characters or length.</span></span> <span data-ttu-id="f0661-251">Varsayılan olarak, bu seçenek devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="f0661-251">By default, this option is disabled.</span></span>

- <span data-ttu-id="f0661-252">**NX_DHCP_THREAD_PRIORITY** DHCP iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="f0661-252">**NX_DHCP_THREAD_PRIORITY** Priority of the DHCP thread.</span></span> <span data-ttu-id="f0661-253">Varsayılan olarak, bu değer DHCP iş parçacığının öncelik 3 ' te çalıştığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-253">By default, this value specifies that the DHCP thread runs at priority 3.</span></span>

- <span data-ttu-id="f0661-254">**NX_DHCP_THREAD_STACK_SIZE** DHCP iş parçacığı yığınının boyutu.</span><span class="sxs-lookup"><span data-stu-id="f0661-254">**NX_DHCP_THREAD_STACK_SIZE** Size of the DHCP thread stack.</span></span> <span data-ttu-id="f0661-255">Varsayılan olarak, boyut 2048 bayttır.</span><span class="sxs-lookup"><span data-stu-id="f0661-255">By default, the size is 2048 bytes.</span></span>

- <span data-ttu-id="f0661-256">**NX_DHCP_TIME_INTERVAL** DHCP Istemci Zamanlayıcı süre sonu işlevinin yürütüldüğü saniye cinsinden Aralık.</span><span class="sxs-lookup"><span data-stu-id="f0661-256">**NX_DHCP_TIME_INTERVAL** Interval in seconds when the DHCP Client timer expiration function executes.</span></span> <span data-ttu-id="f0661-257">Bu işlev, DHCP işlemindeki tüm zaman aşımlarını (örneğin, iletilerin yeniden veya DHCP Istemci durumunun değiştirilmesini) güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f0661-257">This function updates all the timeouts in the DHCP process e.g. if messages should be retransmitted or DHCP Client state changed.</span></span> <span data-ttu-id="f0661-258">Varsayılan olarak, bu değer 1 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="f0661-258">By default, this value is 1 second.</span></span>

- <span data-ttu-id="f0661-259">**NX_DHCP_OPTIONS_BUFFER_SIZE** DHCP seçenekleri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="f0661-259">**NX_DHCP_OPTIONS_BUFFER_SIZE** Size of DHCP options buffer.</span></span> <span data-ttu-id="f0661-260">Varsayılan olarak, bu değer 312 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f0661-260">By default, this value is 312.</span></span>

- <span data-ttu-id="f0661-261">**NX_DHCP_PACKET_PAYLOAD** DHCP Istemci paketi yükünün bayt cinsinden boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-261">**NX_DHCP_PACKET_PAYLOAD** Specifies the size in bytes of the DHCP Client packet payload.</span></span> <span data-ttu-id="f0661-262">Varsayılan değer NX_DHCP_MINIMUM_IP_DATAGRAM + fiziksel üstbilgi boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f0661-262">The default value is NX_DHCP_MINIMUM_IP_DATAGRAM + physical header size.</span></span> <span data-ttu-id="f0661-263">Kablolu bir ağdaki fiziksel üst bilgi boyutu genellikle Ethernet çerçeve boyutudur.</span><span class="sxs-lookup"><span data-stu-id="f0661-263">The physical header size in a wireline network is usually the Ethernet frame size.</span></span>

- <span data-ttu-id="f0661-264">**NX_DHCP_PACKET_POOL_SIZE** DHCP Istemci paket havuzunun boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-264">**NX_DHCP_PACKET_POOL_SIZE** Specifies the size of the DHCP Client packet pool.</span></span> <span data-ttu-id="f0661-265">Varsayılan değer (5 \* NX_DHCP_PACKET_PAYLOAD) olur. Bu, iç paket havuzu ek yükü için dört paket ve yer sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0661-265">The default value is (5 \*NX_DHCP_PACKET_PAYLOAD) which will provide four packets plus room for internal packet pool overhead.</span></span>

- <span data-ttu-id="f0661-266">**NX_DHCP_MIN_RETRANS_TIMEOUT** İletiyi yeniden göndermeden önce istemci iletisine bir DHCP sunucusu yanıtı almak için en düşük bekleme seçeneğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-266">**NX_DHCP_MIN_RETRANS_TIMEOUT** Specifies the minimum wait option for receiving a DHCP Server reply to client message before retransmitting the message.</span></span> <span data-ttu-id="f0661-267">Varsayılan değer, RFC 2131 önerilen 4 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="f0661-267">The default value is the RFC 2131 recommended 4 seconds.</span></span>

- <span data-ttu-id="f0661-268">**NX_DHCP_MAX_RETRANS_TIMEOUT** İletiyi yeniden göndermeden önce istemci iletisine bir DHCP sunucusu yanıtı almak için en fazla bekleme seçeneğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-268">**NX_DHCP_MAX_RETRANS_TIMEOUT** Specifies the maximum wait option for receiving a DHCP Server reply to client message before retransmitting the message.</span></span> <span data-ttu-id="f0661-269">Varsayılan değer, RFC 2131 önerilen 64 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="f0661-269">The default value is the RFC 2131 recommended 64 seconds.</span></span>

- <span data-ttu-id="f0661-270">**NX_DHCP_MIN_RENEW_TIMEOUT** DHCP Istemcisi bir IP adresine bağlandıktan sonra bir DHCP sunucusu iletisi almak ve yenileme isteği göndermek için en az bekleme seçeneğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-270">**NX_DHCP_MIN_RENEW_TIMEOUT** Specifies minimum wait option for receiving a DHCP Server message and sending a renewal request after the DHCP Client is bound to an IP address.</span></span> <span data-ttu-id="f0661-271">Varsayılan değer 60 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="f0661-271">The default value is 60 seconds.</span></span> <span data-ttu-id="f0661-272">Ancak, DHCP Istemcisi en düşük yenileme zaman aşımını varsayılan olarak yapmadan önce DHCP sunucusu iletisinden yenileme ve yeniden bağlama süre sonu zamanlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-272">However, the DHCP Client uses the Renew and Rebind expiration times from the DHCP server message before defaulting to the minimum renew timeout.</span></span>

- <span data-ttu-id="f0661-273">**NX_DHCP_TYPE_OF_SERVICE** DHCP UDP istekleri için gereken hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="f0661-273">**NX_DHCP_TYPE_OF_SERVICE** Type of service required for the DHCP UDP requests.</span></span> <span data-ttu-id="f0661-274">Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-274">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>

- <span data-ttu-id="f0661-275">**NX_DHCP_FRAGMENT_OPTION** DHCP UDP istekleri için parça etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="f0661-275">**NX_DHCP_FRAGMENT_OPTION** Fragment enable for DHCP UDP requests.</span></span> <span data-ttu-id="f0661-276">Varsayılan olarak, bu değer DHCP UDP fragmenting 'yi devre dışı bırakmak için NX_DONT_FRAGMENT.</span><span class="sxs-lookup"><span data-stu-id="f0661-276">By default, this value is NX_DONT_FRAGMENT to disable DHCP UDP fragmenting.</span></span>

- <span data-ttu-id="f0661-277">**NX_DHCP_TIME_TO_LIVE** Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-277">**NX_DHCP_TIME_TO_LIVE** Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="f0661-278">Varsayılan değer 0x80 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-278">The default value is set to 0x80.</span></span>

- <span data-ttu-id="f0661-279">**NX_DHCP_QUEUE_DEPTH** Alma kuyruğunun en yüksek derinlik sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0661-279">**NX_DHCP_QUEUE_DEPTH** Specifies the number of maximum depth of receive queue.</span></span> <span data-ttu-id="f0661-280">Varsayılan değer 4 ' e ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0661-280">The default value is set to 4.</span></span>